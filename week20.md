# EPF5 Dev Updates - Week 20

## What I did this week
As part of the regular EPF activities. I participated in the weekly standup and [Office hour](https://github.com/eth-protocol-fellows/cohort-five/issues/513). I also watched one of the past [Consensus layer meeting 144](https://www.youtube.com/watch?v=p3FRr5umt4U).

This week, I continued working on the database reset feature on the Teku client.


## Teku Client Implementation
I continued working on the Ephemery reset feature on the Teku client. 

My on-going [PR to validate the slot on Ephemery and throw the appropriate exception](https://github.com/Consensys/teku/pull/8759). I received some comments from my mentor Paul Harris regarding how the slot validation should be handled in the custom EphemerySlotValidationService and some test changes.

I worked on making the requested changes and updated the test cases.


## What I will do next week
- Follow up on the slot validation PR and continue working on the DB reset implementation on Teku
- Work on my final report
- Work on my presentation
- Create documentation guide on Ephemery repo, detailing the setup steps for both Teku and Besu.


## References
- [Ephemery.dev](ephemery.dev)
- [Teku Repo](https://github.com/Consensys/teku)