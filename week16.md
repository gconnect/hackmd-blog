# EPF5 Dev Updates - Week 16

## What I did this week
I participated in weekly standup and Office hour. At this week's [office hour](https://github.com/eth-protocol-fellows/cohort-five/issues/452).

This week, I continued my implementation work on the Ephemery reset feature on the Teku client. And further tested my Besu implementation on other clients and refined the client implementation status doc on the Epehemery repo. Below are the details and links to PRs of each of the work done;

## Besu Client Implementation

I further tested the current implementation on other clients like Prysm and Lighthouse. The Besu EL client on Ephemery network synced properly with the CL clients, showing connected pairs, finalized transaction hash and forked choice.

My reviewer Sally MacFarlane from the Besu team was away from the week. So no review was done. Hopefully the review gets finalized and possible merged this coming week.

Here is a link to the [Ephemery Native support PR on Besu](https://github.com/hyperledger/besu/pull/7563)

## Teku Client Implementation

I continued my implementation work to [add the Ephemery reset feature](https://github.com/Consensys/teku/issues/8589) on the Teku client.

To achieve the above , I broke the task into smaller issues;

Here are links to the merged and unmerged PRs
- [x] [Update network file](https://github.com/Consensys/teku/pull/8631 ) : This PR adds an additional Field to the network file and also wrote some test for it.
- [x] [Add deposit chainId](https://github.com/Consensys/teku/pull/8639) : This PR adds the deposit chainId on start of the node.

- [ ] [Check network on start and reset db](https://github.com/Consensys/teku/pull/8642) : This PR handles some check for Ephemery and reset the db when update is due. By deleting the old db.


## Ephemery Repo 

I made some changes based on my mentor's suggestion to the doc I created to provide an easy way to check the current status of Ephemery client implementation.

I added an extra column to the table and modified the intro.

Here is a link to the [PR](https://github.com/ephemery-testnet/ephemery-resources/pull/10)


## Other Contribution Work on Besu

The Parameterize consolidation request issue was merged. 
The implementation involves creating a custom class and adding getter for the consolidation address for managing all addresses and also created test for it.

Here is a link to the merged [PR](https://github.com/hyperledger/besu/pull/7647) 



## What I will do next week
- Follow up on the reset PR and continue working on the DB reset implementation on Teku
- Follow up on the PR from the Besu team for any requested updates
- Follow up on the documentation [PR](https://github.com/ephemery-testnet/ephemery-resources/pull/10) on the Ephemery repo


## References
- [Ephemery.dev](https://ephemery.dev)
- [Besu Repo](https://github.com/hyperledger/besu)
- [Teku Repo](https://github.com/Consensys/teku)
