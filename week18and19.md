# EPF5 Dev Updates - Week 18 & 19

## What I did this week
This week update is a combination of week 18 and 19. As usual, I participated in both week 18 and 19 weekly standup and Office hour. Here are the details of the office hours for [week 18](https://github.com/eth-protocol-fellows/cohort-five/issues/488) and [week 19](https://github.com/eth-protocol-fellows/cohort-five/issues/503) respectively.

This week, I continued working on the database reset feature on the Teku client. For now I am focusing on getting the reset feature completed on Teku before moving on to the Besu client.


## Teku Client Implementation
I continued working on the Ephemery reset feature on the Teku client. 

My previous PR which runs a check to determine the network and node start before the reset happens was merged. Here is a link to the [ Merged PR to check the network on start and reset the db](https://github.com/Consensys/teku/pull/8642/).

As part of the smaller PRs required before the reset feature is completed, I created another [PR to validate the slot on Ephemery and throw the appropriate exception](https://github.com/Consensys/teku/pull/8759). For this implementation I created a custom EphemerySlotValidationService class and also wrote test for it.

The EphemerySlotValidationService extends the Service class and implements the SlotEventsChannel. This service will startup in the BeaconChainController alongside other services. The EphemerySolotValidationService checks the slot, and fails with IllegalStateException if its too high.


## What I will do next week
- Follow up on the slot validation PR and continue working on the DB reset implementation on Teku
- And potentially Start working on the reset feature on Besu


## References
- [Ephemery.dev](ephemery.dev)
- [Teku Repo](https://github.com/Consensys/teku)