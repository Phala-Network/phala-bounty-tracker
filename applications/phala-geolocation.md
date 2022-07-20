# Part 1: Retrieve workers' geolocation privately by their IPs

## Motivation
In modern cloud computing, latency is crucial for application deployments. For example, servers are more likely to be deployed in Europe if users are also mostly located in Europe to reduce latency. Consequently, this proposal (Part 1) aims to deliver a simple strategy to roughly measure the latency between any two workers by obtaining their respective geolocations.

## Target

The target of this proposal (Part 1) is to obtain workers' geolocations inside their respective SGX enclaves so that nobody could retrieve their actual latitude or longitude. Instead, these data will be firstly desensitized, and then be summited to the blockchain. 

## Design

This proposal (Part 1) will be implemented by a native smart contract. Detailedly, there will be a side task repeatedly obtaining workers' geolocations, desensitizing them, and calling a command from our implemented geolocations smart contract. This contract will collect and format these desensitized data for querying.

## Milestones

- Implement the algorithm and submit the PR
- Work with the dev team for the PR to be merged.

---

# Part 2: Off-Chain Latency Graph Optimization

# Motivation

Previously [Geolocation Probing](https://github.com/Phala-Network/phala-blockchain/pull/445) was implemented to determine the physical locations of workers by their desensitized public IP addresses and thereby estimating their network latencies based on their geolocations. However, there is actually no accurate mapping between network latencies and geolocations as network packages are routed in a very complicated way. Consequently, a mapping (function) between workers’ identities and latencies must be manually constructed to suit our needs.

In this proposal, we seek to create the above-mentioned mapping by assigning each worker a coordinate in a virtual $d$ dimensional space. Namely, a latency graph is created where each vertex represents a worker and the distance, defined by L-2 norm, between any two vertices represents the latency between them. Nevertheless, optimizing coordinates of all workers until converged usually requires abundant data to be shared among workers, and therefore simply storing these data on-chain will significantly contribute to the congestion of the blockchain. Consequently, in this proposal, we adopt federated learning to achieve off-chain latency graph optimization.

# Targets

The target of this proposal (Part 2) is to build a mechanism for workers to corporately and adaptively optimize the latency graph off-chain until converged so that latency between any two workers can be estimated on every worker accurately and fastly. This graph can be used to support various downstream applications, e.g. CDN services, game servers, P2P communication, etc.

# Design

## Overview

In our proposal (Part 2), each worker initially has a $N \times d$ dynamic array representing the coordinates of each worker in the graph, where $N$ denotes the total number of workers in the network, and $d$ denotes the dimension of the graph. Each epoch of graph optimizing contains 5 steps:

- [Dataset Collection] Each worker measures the real latency between itself and some other workers, and stores these data in a dataset.
- [Optimization] Each worker optimizes its own coordinate in its local latency graph using the collected dataset.
- [Sharing] Each worker shares its local latency graph with some other workers.
- [Aggregation] Each worker aggregates all received latency graphs into a new graph, replacing its local graph.
- [Iterating] Repeat step 1 to step 4 until the graph is converged.

These steps will be detailedly elaborated in the following.

## Algorithm

Firstly, let’s assume the latency graph is a $d$-dimensional space where $d$ is a hyper-parameter that we need to tune in practice. The coordinate of a worker $w_i$ is thus represented by $(x_0^i, x_1^i,\cdots,x_{D-1}^i)$. We define the L2 norm distance between two workers in the graph as the estimated latency between them:

$$
L_{i,j}=(\sum_k^D(x_k^i-x_k^j)^2)^\frac{1}{2}
$$

The origin (i.e. $(0,0,\cdots,0)$) is assigned to the coordinate of a newly added worker by default. In other words, all workers will be located at the origin before at initial. Consequently, each worker $w_i$ will initialize a $N \times d$ array (marked by $\mathcal{G}_i$) to denote coordinates of all workers in the network. Moreover, the local dataset $\mathcal{D}_i$ of each worker $w_i$ is a $N \times 1$ array, denoting the real latency from $w_i$ to other workers.

### 0. Dataset Collection

At the beginning of every epoch, each worker $w_i$ will actively measure the real latency between itself and other workers. the measured latency $L_{i,j}$ will be added to the local dataset by EMA:

$$
\mathcal{D}_i[j] = \beta_d \mathcal{D}_i[j] + (1 - \beta_d) L_{i,j},
$$

where $\beta$j is a momentum factor that is usually set to $0.9$. Here, EMA is employed to retrieve the mean of measured latency, ignoring the fluctuation of measurements and contributing to the stability of the graph.

### 1. Optimization

Since the collected dataset $\mathcal{D}_i$ only contains latencies from $w_i$ to others, during the optimization phase it can only optimize its own coordinate in $\mathcal{G}_i$ (in fact, $w_i$ can only measure the latency from itself to others, it cannot measure the latency from $w_j$ to $w_k$). Specifically, $w_i$ optimizes its coordinate by minimizing the overall system energy (Similar to [Vivaldi](https://dl.acm.org/doi/pdf/10.1145/1030194.1015471). However, different from Vivaldi, in our proposal we adopt a momentum-based optimizer, which could effectively rectify the estimation of the solution.

![](https://imgur.com/iXbBrfV.png)

Then, after optimizing to an ideal solution, coordinates rebase needs to be performed, which generally moves vertices near the origin.

![](https://imgur.com/fzt2Nob.png)

## Sharing and Aggregation

Finally, each worker’s solution needs to be broadcasted to others for the system to converge. Specifically, each worker $w_i$ will share its local graph $\mathcal{G_i}$ to others, and after sharing, $w_i$ will replace its local graph with the averaging of all received graphs:

$$
\mathcal{G}_i[j] = \frac{1}{N} \sum_k \mathcal{G}_k[j]
$$

## Other Considerations

### Communication overhead

All formulas related to $N$ can be replaced by $S$, where $S$ represents a subset of total workers. This will effectively reduce the communication overhead while maintaining the estimation unchanged.

### Implementation

Ideally, the algorithm in this proposal can be implemented with the side-task inside pruntime to ensure integrity.

# Milestones

- Implement the algorithm and submit the PR
- Work with the dev team for the PR to be merged.