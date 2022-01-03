# Tracker for Phala Bounty Projects

This repository contains all the technical details about Phala's bounty projects.
It records all the interactions between the project developers and the curators and is meant to help our community members and the Council to understand and track the progress of Phala improvements.

## What is Phala Bounty

The [Phala Treasury](https://wiki.phala.network/en-us/docs/governance/4-treasury/) collects its funds mainly from transaction fees, slashing, and Secure Worker mining commission (20%). The Treasury is ultimately controlled by the [Council](https://wiki.phala.network/en-us/docs/governance/2-join-the-council/) and is used for the benefit of the Phala ecosystem.

For now, there are two kinds of Treasury spending: the *Tip* for minor contributions like a bug fix, code optimization, and document improvement, and the *Bounty* for more serious contributions like extending the capabilities of the Phala network.

To apply for the Phala Bounty, refer to our [tutorial](https://wiki.phala.network/en-us/docs/governance/4-treasury/#creating-a-bounty-proposal) and create the Bounty Proposal through the on-chain Governance module.

## Bounty Procedure

1. [Create a Bounty Proposal](https://wiki.phala.network/en-us/docs/governance/4-treasury/#creating-a-bounty-proposal) on chain and follow the following steps for application.
    - Fork this repository.
    - In the newly created fork, create a new file under the [`applications`](applications) folder and name it after your project: `project_name.md`.
    - Fill out the details of your project. Your document should at least include the following aspects:
        - Motivation
          - What improvement needs to be made on what shortcomings?
        - Targets
          - The objective and the key results of this project. We recommend a clear benchmark to evaluate the project.
        - Design
          - An overall design of your solution, could be better if with the necessary background knowledge and investigations.
        - Milestones
          - A project can be separated into several milestones to deliver, each with its own benchmark to evaluate.
    - Once you're done, create a pull request. The pull request should only contain *one new file*—the Markdown file your created.
2. Proposal Review and Revision.
    - The Council and the Phala Team can (and usually does) issue comments and request changes on the pull request.
    - Clarifications and amendments made in the comments need to be included in the application. You may address feedback by directly modifying your application and leaving a comment once you're done. Generally, if you don't reply within 2 weeks, the application will be closed due to inactivity, but you're always free to reopen it as long as it hasn't been rejected.
    - The application will be accepted and merged as soon as it receives the required number of approvals, or closed after two weeks of inactivity. Unless specified otherwise, the day on which it is accepted will be considered the starting date of the project, and will be used to estimate delivery dates.
3. Curator and Shepherd Assignment.
    - Curator is the domain expert to whom the Council delegates the curation activity of a spending proposal.
    - Shepherd is the project secretary who helps bounty applicants to format their proposal, arrange a discussion and promote the whole bounty process.
4. Project Implementation
5. Milestone Deliver
6. Bounty Close

## Bounty Projects

| Team                              | Project                                      | Link                                                                 |       Terminated       |     First Delivery     |       Completed        |
| --------------------------------- | -------------------------------------------- | -------------------------------------------------------------------- | :--------------------: | :--------------------: | :--------------------: |
| [Soptq](https://github.com/Soptq) | Network Connectivity Improvement for Workers | [Github](https://github.com/Soptq/phala-blockchain/tree/prouter-ms1) | <ul><li>[ ] </li></ul> | <ul><li>[x] </li></ul> | <ul><li>[ ] </li></ul> |


## Related Resources

- [Phala Governance](https://wiki.phala.network/en-us/docs/governance/about-governance/)
- [Phala Tokenomics](https://wiki.phala.network/en-us/docs/tokenomic/understand-phala-tokenomics/)
- (Informal) [Phala Research Interests](https://hackmd.io/@h4x3rotab/Hybe1S89_)
