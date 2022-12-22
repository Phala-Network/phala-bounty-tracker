# Building a Common Good Parachain Oracle Using Phala Phat contracts for secured feeds 

## Motivation
The lack of an oracle primitive in the Dotsama ecosystem has been addressed with the original proposal for a federated and decentralized parachain oracle system [here](https://forum.polkadot.network/t/help-us-create-a-federated-and-decentralised-parachain-oracle-system/1190). Further discussion can be found [here](https://forum.polkadot.network/t/oracles-for-polkadot/1286). This has prompted the development of a MVP towards creating a common good parachain, leveraging Phala's secure and private oracle system. This feature and the associated framework will be submitted with a grant application to the Web3 Foundation.

## Targets
+ MVP for a Common Good Parachain Oracle 
  + Ink contract around a Phat contract
  + Reporter registration and feed management
  + Create query 
  + Consume feed
  + Reporter inputs/aggregation  
  + Direct Integration
  + Business logic
  + Reporter staking/reward/slash
  + Fees
  + Fund Feed
  + Reporter Phat contract
  + Factory Phat contract

## Investigation and Design
This proposal will be implemented by a native smart contract using Ink! and Phat contracts.

## Milestones
+ **[~2023.01.23]**  (15K)
  + Phat contract on parachain oracle
    - Record Phat reporter + info in parachain oracle registry
    - Send https requests to fetch any data from the web and other parchains via RPC
    - Phat reporter inputs aggregation
    - XCM Feed management leveraging Phat contracts: route queries according to matching between 
        demand and supply of Phat reporter feeds        
  
+ **[~2023.02.23]**  (15K)
    
    + Consumer parachain oracle phat contract  
      - XCM create feed  
      - XCM consume feed
        + Obtain direct answer from keeper
        + Phat keepers aggregated answer
    
+ **[~2023.03.23]**  (15K)
    + Phat reporter staking/reward/slash
    + XCM Funding and NFT minting for Phat data feeds
    + Fees
  

## Conclusion
Phala's secure and private feeds are ideal for creating a common good parachain oracle. This proposal will provide a secure and reliable data feed for the Dotsama ecosystem