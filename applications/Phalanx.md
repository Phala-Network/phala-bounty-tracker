# Bounty Proposal: [Phalanx - The Phala Darkpool Exchange]

## Proponent:
[Khala Address]
## Date
07.02.2022
## Requested allocation:
50,000$(5000$ for the collator)
## Short description:
A decentralized dark pool exchange built on top of Phala, focused on 
order privacy and mid-price clearing.

## Context of the bounty:
The Phalanx project is the continuity of the DarkPool project, which won 2nd place during the Phala/Encode-Hackathon-2021
The team members are:
- Geoffrey Tsuigi: tsui.geoffrey@gmail.com (original creator of the DarkPool and winner of the Phala/Encode-Hackathon-2021)
- Claudio Ciardelli: claudio.ciardelli@gmail.com
- Kazunobu Ndong: ndongmefane@gmail.com

## Problem statement:
The aim of this project is to solve the following issues found in current exchanges:
- Centralized Exchanges
Orderbook exchange. Intuitive but centralized risk is against  the spirit of DeFi.
- Decentralized Orderbook Exchange
Just as intuitive as centralized orderbook exchanges, but not economically viable due to transaction fees (gas costs) of constantly sending, updating, canceling orders
- Decentralized AMM Exchange
Solves the transaction fee problem by getting rid of market makers, but comes with high slippage costs, low liquidity, and order frontrunning

The diagram below shows an example of a Buying Order treatment in Phalanx:
![alt text](https://github.com/projectphalanx/phalanx-docs/blob/master/phalanx0.jpg?raw=true)

## Proposal Objective & Solutions:  
 Using Smart-Contract confidentiality, and native HTTP requests from Smart-contracts enabled by the Phala blockchain, the phalanx project aims is  to deliver the following:

- A web based darkpool exchange application allowing users to perform swaps between a limited set of currencies via a hidden orderbook. The darkpool exchange would be designed so as to be able to work with multiple market pairs. The application would rely on the underlying technology provided by Phala to access assets, with the initial assumption that this would cover Substrate based tokens and ERC20 tokens. 

- As explained in the [whitepaper](https://github.com/projectphalanx/phalanx-docs/blob/master/whitepaper.pdf) the orders placed in the orderbook will be executed as soon as there are matching bid and ask orders. 

- Orders will be executed at a reference price that will be determined by a "market price module" that will retrieve information from one or more reliable price source. (At the time of writing (31/12/2021) the market price is dependent on the availability of the phala http extension for its FAT Contract technology.)

Further details about our proposal logic can be found in our [whitepaper](https://github.com/projectphalanx/phalanx-docs/blob/master/whitepaper.pdf).

## Main differences with the Darkpool Exchange submitted during the Phala/Encode-Hackathon-2021
- This project will use Phala Fat Contract through the Ink! smart contract Library, instead of using the native contract. This allows for a more compact file system,easier maintenance of the program, and it will also make it easier to attract new developpers to the project.
- Advanced front-end compared to the Hackathon version.

The following features will also be added:
- A mid-price clearing mechanism was established and will be used for this version
- User-specified time limits on live orders to expire automatically, 
- User-specified toggles for how much/little privacy they want on their specific order,
- Queueing logic such as pushing large orders back to the end of the queue after X amount of their order has been filled to prevent large whale orders from clogging the queue. 

## Project Tracker
The completion of milestones 2 and 4 is conditionned on some Phala features that are not yet available (access to external tokens, execution of http calls on a secure worker) the estimated completion dates below might be affected by delays in the Phala 2022 roadmap.

| Milestone   | Est Date | Deliverable  | Allocation on completion  |        Stand-By       |       In work       |     Review     |       Completed        |
| --------------------------------- | --------------------------------- |--------------------------------- | -------------------------------------------- |  :--------------------: | :--------------------: | :--------------------: | :--------------------: |
| 0. | T0(*) | Kickoff|  | <ul><li>[x] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> |
| 1. | T0+2 months | Technical Design + Order Book | 10,000$ |  <ul><li>[x] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> |
| 2. | T0+4 months | Match orders and Token Transfers | 10,000$ |  <ul><li>[x] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> |
| 3. | T0+7 months | Front End | 10,000$ |  <ul><li>[x] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> |
| 4. | T0+9 months | Market Price | 10,000$ |  <ul><li>[x] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> |
| 5. | T0+12months | GoLive | 5000$ | <ul><li>[x] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> |

(*)T0 represents the validation date of the On-Chain bounty proposal


