# EPF5 Dev Updates - Week 15

## What I did this week
I participated in weekly standup and Office hour. At this week's office hour we hosted [Parithosh Jayanthi](https://parithosh.com/), Pari is part of EF Devops team, specifically working on PandaOps which is a group helping with core development. 

He is also involved in protocol upgrades,  hard fork testing, devnets and testnets, shadow forks, ton of cool new devops tooling.

We had the opportunity of asking him questions about his work at EF, testing and toolings.

This week, I started working on the Ephemery reset feature on the Teku client. And further refined the Besu implementation and also worked on a Besu issue I picked up. The details of the implementation work done can be found below;

## Besu Client Implementation

I refined the genesis function implementation and test. I also went on to test the implementation on the Teku client.

The reviewer Sally Macfarla confirmed the implementation is looking okay but would need to get other members of the Besu team to review it further before it can be merged. Here is a link to the [Ephemery Native support PR on Besu](https://github.com/hyperledger/besu/pull/7563)

## Teku Client Implementation

I started working on on the database reset which involves deleting the generated db and recreating a new db on when update is due on Ephemery network. Here is a link to the raised [draft PR of the current implementation](https://github.com/Consensys/teku/pull/8626) work done.


### Other Contribution Work

I started working on this issue on Besu [Parameterize Consolidation Request contract address](https://github.com/hyperledger/besu/issues/7381) and created a [PR](https://github.com/hyperledger/besu/pull/7647) for it, still under review.



## What I will do next week
- Follow on the PR and continue working on the DB reset implementation on Teku
- Follow up on the PR from the Besu team for any requested updates
- Follow up on the Parameterize Consolidation Request contract address PR on Besu
- Follow up on the documentation [PR](https://github.com/ephemery-testnet/ephemery-resources/pull/10) on the Ephemery repo


## References
- [Ephemery.dev](https://ephemery.dev)
- [Besu Repo](https://github.com/hyperledger/besu)
- [Teku Repo](https://github.com/Consensys/teku)
