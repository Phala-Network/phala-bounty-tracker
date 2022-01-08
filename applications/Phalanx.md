# Bounty Proposal: [Phalanx - The Phala Darkpool Exchange]

## Proponent:
[Khala Address]
## Date
08.01.2022
## Requested allocation:
50,000$
## Proposed Curator reward:
1000$
## Short description:

A Darkpool: A fast Exchange with transactions confidentiality

## Context of the bounty:

The Phalanx project is the continuity of the DarkPool projects, which won 2nd place during the Phala/Encode-Hackathon-2021
The team members are:
- Geoffrey Tsuigi: tsui.geoffrey@gmail.com (original creator of the DarkPool and winner of the Phala/Encode-Hackathon-2021)
- Claudio Ciardelli: claudio.ciardelli@gmail.com
- Kazunobu Ndong: ndongmefane@gmail.com

points discussed in advance in any channel related to the bounty proposal and background research for your project. 
background of the proponent, team credentials. 
their motivation (including any conflict of interests or association to any governing bodies)
any known backups already behind the solution (known token holders, organizations or collectives building on Kusama Network or participating in its governance mechanism in any way).

## Problem statement:

The aim of this project is to solve the following issues found in current exchanges:
- Centralized Exchanges
Orderbook exchange. Intuitive but centralized risk is against  the spirit of DeFi.
- Decentralized Orderbook Exchange
Just as intuitive as centralized orderbook exchanges, but not economically viable due to transaction fees (gas costs) of constantly sending, updating, canceling orders
- Decentralized AMM Exchange
Solves the transaction fee problem by getting rid of market makers, but comes with high slippage costs, low liquidity, and order frontrunning

## Proposal Objective & Solutions:
  
 Using Smart-Contract confidentiality, and native HTTP requests from Smart-contracts enabled by the Phala blockchain, the phalanx project aims is  to deliver the following:

- A web based darkpool exchange application allowing users to perform swaps between a limited set of currencies via a hidden orderbook. The darkpool exchange would be designed so as to be able to work with multiple market pairs. The application would rely on the underlying technology provided by Phala to access assets, with the initial assumption that this would cover Substrate based tokens and ERC20 tokens. 

- As explained in the whitepaper (CC: add link) the orders placed in the orderbook will be executed as soon as there are matching bid and ask orders. 

- Orders will be executed at a reference price that will be determined by a "market price module" that will retrieve information from one or more reliable price source. (At the time of writing (31/12/2021) the market price is dependent on the availability of the phala http extension for its FAT Contract technology.)

Further details about our proposal logic can be found in our [whitepaper](https://github.com/projectphalanx/phalanx-docs/blob/master/whitepaper.pdf).

## Project Tracker

| Milestone                              | Deliverable                                      | Link                                                                 |       In work       |     Review     |       Completed        |
| --------------------------------- | -------------------------------------------- | -------------------------------------------------------------------- | :--------------------: | :--------------------: | :--------------------: |
| 13.01.2022 | Working DarkDex Backend prototype | [Github](https://github.com/projectphalanx/Ink_Contract) | <ul><li>[x] </li></ul> | <ul><li>[ ] </li></ul> | <ul><li>[ ] </li></ul> |


