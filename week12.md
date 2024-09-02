# EPF5 Dev Updates - Week 12

## What I did this week
I participated in weekly standup and Office hour. 
This week office hour we had Alex Stokes! Alex is part of Consensus R&D team in Ethereum Foundation(EF) and he is a well known researcher of the consensus layer. 

He also runs ACD most of the week. In the office hour he shared his his story and discussed on current CL research, specs, and we had the opportunity of asking him questions related to CL and other core protocol subjcts.

I got some suport from my mentors at Mario and pk910 from the Ephemery team on the Matrix contributor community platform regarding the Teku implementation. I went through the reources provided by Mario showing the discussions  regarding the genesis SSZ on the Loadstar and Lighthouse client implementation.

## Besu Client Implementation

I have added the necessary configuration files for the Busu client and create a custom logic for the Ephemery genesis function. With a couple of test to handle different scenarios.

My [PR](https://github.com/hyperledger/besu/pull/7471/) is still under review by the Besu team and I am making changes as requested by the review Sally Macfarla who is currently my mentor from the Besu team

## Teku Client Implementation
I started adding the configuation files on the Teku client. Here is a link to the [issue](https://github.com/Consensys/teku/issues/8537) I created on Teku. And a [draft PR](https://github.com/Consensys/teku/pull/8543). So far I have added most of the required configuation files. 

Paul Harris is currently reviewing my work and will be mentoring me during my EPF work on the Teku Client.

I also co-worked on this [issue](https://github.com/Consensys/teku/issues/8506) regarding SSZ conversion fromBytes format and fromHexString. I worked on the fromBytes and also created test for it. Here is a link to the [PR](https://github.com/Consensys/teku/pull/8540)


## What I will do next week
- Follow up on the PR from the Besu team for any requested updates
- Follow up on the PR from the Teku team for any requested updates
- Figure out the best way to handle the genesis SSZ for Ephemery. To ensure the updated genesis state is loaded at all time.
- Possibly create a custom function to handle update of the ephemery.yaml configuration file.


## Blockers 

- None at the moment!


## References
- [Ephemery.dev](https://ephemery.dev)
- [Besu Repo](https://github.com/hyperledger/besu)

 