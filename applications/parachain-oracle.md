# Provide a data aggregation mechanism based on Phala workshop
# for offchain worker in the Federated 
# and decentralised parchain oracle common good parachain 

## Motivation

The oracle primitive has been missing from the Dotsama ecosystem.
As a response to this, a federated and decentralised parchain 
oracle system was originally described here:
https://forum.polkadot.network/t/help-us-create-a-federated-and-decentralised-parachain-oracle-system/1190
Other issues concerning such a system are disscussed here:
https://forum.polkadot.network/t/oracles-for-polkadot/1286
In light of this, the creation of a common good parachain seems imminent.
We are proceeding with a MVP towards this. 
The architecture of this parachain will be based on some of the information found here:
https://github.com/Kylin-Network/KylinDocs/blob/main/whitepaper/A_decentralized_data_market_place_as_a_source_of_truth.pdf
Section 4.4.4 of this document suggests the use of multiple buffers
to aggregate data in the most accurate, democratic and persistent way. 
A great solution for securing and encrypting the offchain worker buffer has been proposed by Phala here:
https://github.com/Phala-Network/oracle-workshop
This feature will be delivered with the MVP submitted with grant application to W3F.

## Targets

- Provide a first iteration of a data aggregation mechanism to the Phala solution by calculation the mean on a running buffer. 
- Determine buffer optimisation parameters  
- Provide a configuration mechanism for this aggregation mechanism
- Publish a SLA for every resolution of the buffer

   
## Investigation and Design
This proposal will be implemented by a native smart contract using Ink! or Swanky.
Investigation into possible variants of the offchain worker need to be researched.

 
### Summary
Since the Federated and decentralized parachain oracle is a common-good effort,
this proposal also sollicits any help that could 
provide runway for building the MVP for the W3F application.


## Milestones

### Milestone 1: data aggregation mechanism

* [~2022.12.20] Research & refactor 
* [~2023.01.30] Aggregation buffer
* [~2023.02.14] Aggregation buffer optimisations

### Milestone 2: Business logic

* [~2023.03.15]  Staking and slashing
* [~2023.03.30]  Buffer configuration and SLA

