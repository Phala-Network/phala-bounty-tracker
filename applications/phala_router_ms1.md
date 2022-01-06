# Improve Network Connectivity between Phala Workers

## Motivation

As a permissionless computing cloud, Phala enables anyone with trusted hardware to freely join the network, this means workers can be in different network situations, with many of them not possessing public IP addresses, behind the firewall or NAT server.

In Phala blockchain, two kinds of contract requests are supported: Command and Query. Unlike Command which is uploaded to the blockchain and downloaded by workers during block syncing, the Query is meant to be sent directly to the workers and processed by the contracts. Moreover, to support future inter-contract messaging, direct communication between workers is a necessity. So it is urgent to design a solution to improve the network connectivity among workers in the Phala blockchain and enable direct network access for the workers.

## Targets

- Enable direct access to the workers with no public IP addresses, behind the firewall or NAT server;
- Support anonymous communication to preserve the privacy of workers;
- Support low-latency transmission (expect <1s);
- Support the measurement of forwarded traffic for valuation;

## Investigation and Design

### Summary

Currently, there are mainly 2 ways for us to implement a connection mechanism between workers: **bridge existing solutions** and **implement our own protocol**. In the following survey, I would explain in detail each direction with advantages, disadvantages. The ultimate goal is to create a router-alike middleware between different workers’ runtime, that is not only _robust_, but also _fast_ and _privacy preserving_.

### Bridge Existed Solutions
---

There are mainly two existing solutions in the world that directly match our needs: [TOR Project](https://www.torproject.org/) and [i2p](https://geti2p.net/en/). _Both aim to create a transparent layer on the current WWW infrastructure to achieve anonymous accessing_. I would recommend reading [An Introduction to Tor vs I2P](https://www.ivpn.net/privacy-guides/an-introduction-to-tor-vs-i2p/#:~:text=We%20see%20that%20both%20Tor,true%20darknet%2C%20if%20you%20will.) first to get an initial impression of these two technologies.

### TOR Project

TOR is originally maintained by the US military and it receives funds from the US government as well, and it designed the way more **centralized**. That is, TOR generally requires a so-called `Directory Server`  to keep track of all available relays in the world, to be fully functional. When a node intends to initiate a connection to a target, it must first fetch all available relays and some other necessary data from the `Directory Server`, and plan a circuit (path) according to them. _As a result,_ `Directory Server` _is limited and public, making it easy to be attacked or banned._

![](https://imgur.com/Wg96ZFU.jpg)

[Run Your Own Tor Network - ritter.vg](https://ritter.vg/blog-run_your_own_tor_network.html) depicts approximate steps to configure a private `Directory Server` and therefore to set up a private TOR network. Consequently, to bridge TOR with Phala Network, we need to mock `Directory Server` behavior and save essential data to the blockchain (i.e. making `Directory Server` on the blockchain). However, `Directory Server` is implemented **inside** TOR client, which makes it hard for us to implement our own `Directory Server` **non-invasively**, without modifying any TOR source code. 

#### The advantages of bridging TOR project with Phala Network:

* **Robust.** TOR has been running for many years and is considered mature. 
* **Compatible with Web2**. TOR can access regular web pages.
* **Written by** `C`, should be easy to be called by `Rust` or any other language. 

#### The drawbacks of bridging TOR project with Phala Network:

* **Difficult to integrate with Phala Network**. Integrating needs to completely separate `Directory Server` from TOR client and then implement custom functions to interact with Phala Blockchain.
* **Large state size**. `Directory Server` saves state data of all relays, which may be too big for blockchain.
* **Possible privacy leakage**. With `Onion Router`, the data transferred by the exit relay is plain text, without any encryption.

#### Workload if we go this way:

* Investigate TOR source code to figure out how `Directory Server` works.
* Investigate TOR source code to figure out if TOR can work with third-party `Directory Server`.
    * If true, then continue.
    * If false, then we have to fork `TOR` and make it work with third-party `Directory Server`
* Implement simple `Directory Server`.
* Replace database in simple `Directory Server` with blockchain storage.
* Implement infrastructures for Phala workers talking to others.
* Test in a simulated environment (localhost).
* Test in a real-world environment (VPS).
* Launch.

#### Does TOR support configuring the number of hops?

Most likely NO. The first, second, and third relay server in TOR shares different responsibilities. Thus the number of hops cannot be configured without touching source code.

#### Measuring passing traffic?

Yes. [TorPlusVPN · Wiki · Legacy / Trac · GitLab](https://gitlab.torproject.org/legacy/trac/-/wikis/doc/TorPlusVPN). Not recommended by TOR.

### i2p

On the other hand, i2p, created in 2003, is much more decentralized compared to TOR. It utilizes **Distributed Hash Table (DHT)** to act as `Directory Server` in TOR realm. Each node establishes a P2P connection with only a few other nodes,  and therefore no individual owns all nodes’ state data in the network. When a node wants to join the network, it retrieves some nodes' state data from `Reseeding Server`(Like Torrent). A `Reseeding Server` is just a service that shares some of its peers to requestors (usually 75%), and thus it is relatively easier for us to implement our custom version. Specifically, we can save some nodes’ state data on the chain, and implement a `Reseeding Server` listening to localhost and returning `i2p`-compatible peers data package (SU3 format).

![](https://imgur.com/NNy0JiR.jpg)

#### The advantages of bridging i2p with Phala Network:

* **Robust as well**. i2p is also a project that started nearly 20 years.
* **Designed for p2p connection**. Compared to TOR, i2p does not provide the ability to anonymously access regular web pages or bigger, public internet. It aims to be _network within the internet,_ which I think matches the envision of Phala Network.
* **Easier to be integrated with blockchain**. `Reseeder server` is simple, and should be quite easy to be mocked.
* **Privacy-Preserving**. I2p utilizes `Garlic Router`, which performs package-wise routing, making MIIM attacks and other attacks nearly impossible.
* **Small state size**. Only a few state data needs to be stored on-chain.

#### The disadvantages of bridging i2p with Phala Network:

* **Written by** `Java` [i2p/i2p.i2p](https://github.com/i2p/i2p.i2p)and `CPP` [PurpleI2P/i2pd](https://github.com/PurpleI2P/i2pd). To my knowledge these two languages need explicit binding in order to be used by other languages.

#### Workload if we go this way:

* Create a fake local database, and rewrite [PurpleI2P/pyseeder](https://github.com/PurpleI2P/pyseeder).
* Replace local database with blockchain storage.
* Implement infrastructures for Phala workers talking to others.
* Test in a simulated environment (localhost).
* Test in a real-world environment (VPS).
* Launch.

#### How to embed i2p into Phala Network?

1. We can teach the user to install i2p and configure it to connect to Phala Network.
2. Or we can repackage i2p ( including modifying it ) and deliver it with Phala Network.

#### How does Phala APP knows the destination when the identity in Phala Network and i2p network is not the same?

Probably we need to let user register their i2p network identities to the blockchain, or we can hack the i2p code to retrieve and register identities automatically.

#### Run Phala Network inside i2p network?

Yes, we can, since we can customize the data package to be only recognizable by Phala APP ( like XMR ). However, we still need to record a routing table in our blockchain.

#### Does i2p support configuring the number of hops?

Yes. i2p supports configuring different hops for different tunnels at runtime.    The default hop length is 3 for outbound connection and 3 for inbound connection so the total is 6 hops for a connection. However, it can be configured to even 0.

#### Does i2p support measuring inbound and outbound traffic?

To my best knowledge, there is currently no elegant way to measure inbound and outbound traffic out of the box. However, there are some data provided natively by i2p that could be possibly helpful for incentives:
* Send and receive package size.
* Network speed.
* The count of inbound and outbound tunnels.
* Tunnel creation success rate and corresponding latency and speed.
* Uptime.
* Connected peers.

### Implement Our Own
---

The idea behind TOR and i2p is fairly simple: Planning a connection path and transferring data package along this path. In practice, there are 3 major problems and we already had all answers to them:
1. _How to plan a path?_ We can just do a random selection.
2. _How to transfer data safely?_ We can employ P2P encryption.
3. _How to handle NAT problem?_ We can divide all workers into two types: Common Worker (CW) and NAT-ed Worker (NW). Each NW must keep a persistent connection with at least one CW, letting this (these) CW be its delegate(s).

However, while implementing our own solution for network routing shows the most flexibility, it is considered very immature compared to TOR or i2p. _Consequently, extensive rabbit holes is expected_

#### The advantages of implementing our own router:

* **Flexible**. We basically can do whatever we want.

#### The drawbacks of implementing our own router:

* **Immature**. Our implementation is expected to be less robust and has less performance compared to TOR or i2p.
* **Possibly high latency**. Our implementation uses a proxy server for NAT-ed workers for simplicity, which TOR or i2p usually use UDP/TCP hole punching. The latter one is much faster than the proxy.

#### Workload if we go this way:

* Implement persistent connection.
* Implement key-pair exchange protocol.
* Implement route table and related worker registration mechanism.
* Implement routing.
* Implement infrastructures for Phala workers talking to others.
* Test in a simulated environment (localhost).
* Test in a real-world environment (VPS).
* Launch.

## The overview architecture
![](https://imgur.com/23K4uy2.jpg)

As this figure illustrated, there will be a dedicated communication component named **PRouter**. PRouter will mainly handle the following tasks for the worker:
1. Start/Stop/Monitor i2pd, register local rpc endpoint to the i2p network.
2. Register worker's public endpoint to the Phala Blockchain.
3. Translate any worker's phala identity to its corresponding public endpoint.
4. Act as daemon process for i2pd.

So essentially, all worker-to-worker communications will be handled by PRouter. It will also provide a REST style server for PRuntime to directly communicate with any worker in the phala network.

## Milestones

### Milestone 1: A Phala Network Layer based on i2p that enables p2p connections between Phala workers.

* [~2021.11.8] Research possible ways of implementing P2P connection in Phala Network. Determine technology roadmap.
* [~2021.12.31] Deliver working implementation that achieves connections between workers.
    * i2p source code integrating.
    * Key generating.
    * Configuration generating.
    * Phala identity and i2p identity binding.
    * Testing.
* [~2021.1.31] Refactor according to Phala Dev’s feedback and finally merge into Phala Network. 

### Milestone 2: Incentives on the Phala Network Layer.

* [~2021.12.31] Research possible ways that encourage high-quality network connection on the network layer.