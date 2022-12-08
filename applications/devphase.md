# devPHAse - development tool for Phala Phat contracts

# Part 1: MVP

## Motivation
In smart contracts development process crucial part is testing.
Covering entire code base with tests is must-have. On the other hand preparing special environment for every test maybe be time-consuming. 
Ethereum has a lot of tools for that e.g. hardhat, truffle or waffle.

## Target

The target of this proposal (Part 1) is to create tool which will help developers testing their Phat contracts.

## Overview

This proposal (Part 1) will be MVP of tool including:
- initiation of project with templates
- compilation of contracts using rust compiler
- creating type bindings for TS tests
- downloading latest Phala stack (node + pruntime + pherry)
- starting Phala stack in standalone mode
- configuring Phala stack (creating gatekeeper, clusters, deploying system contracts etc.)
- executing tests using runtime stack

## Milestones

- Create MVP

## Notes
MVP is already created and published  
https://github.com/l00k/devphase  
https://www.npmjs.com/package/devphase  

Better overview how it works is described in devPHAse github page.


---

# Part 2: Maintainence of product

# Motivation

Phala is still in early stage and it keeps growing and chaning fast.  
All changes in stack configuration need to be reflected in devPHAse code.

# Targets

The target of this proposal (Part 2) is to adjust code to current Phala implmentation in daily basis.

## Overview

Considering nature of this part I think it is good idea to split Part 2 into monthly basis.
