# Final Development Update - Native Implementation of Ephemery Testnet on Besu & Teku Client Pairs


## Abstract
This project was focused on providing native support for Ephemery on Besu and Teku client pairs. 

First of all if you are just hearing about Ephemery for the first time, [Ephemery](https://ephemery.dev/) testnet is a network that rolls back to the genesis after a set period of time. 

Ephemery is focused on short term and heavy testing usecases. The purpose of this is also to avoid problems like insufficient testnet funds, inactive validators, state bloat, and similar issues faced by long-running testnets.

Since this testnet is still pretty new to the ecosystem, user adoption becomes really important. And to help increase the adoption the user experience of using Ephemery needed to be as smooth as possible.

Running a node shouldn't be complicated and to help reduce this complexities especially for non-technical people it becomes important to provide native support for Ephemery on different client pairs.

Here is a link to my initial [project proposal](https://github.com/eth-protocol-fellows/cohort-five/blob/main/projects/native-ephemery-client-pair-implementation.md).

## Status Report

### Initial Status
Before my implementation Ephemery only had native support for Geth, Reth, Lighthouse and Lodestar clients. Specificlly focused on the genesis function with genesis reset still in progress for the above mentioned clients. These implementation were done by past fellows.

Also there was no way of tracking the client implementation work done. Which makes contribution a little difficult. As I was not completely sure initially when I started as to what is left and what client implementation was needed. But thanks to my mentor @Mario Harvel for pointing me to some resources and past fellow updates which gave me an idea on what I needed to do.

Before my implementation to setup Ephemery on Teku and Besu requires manual process of downloading the genesis files from the Ephemery repo locally to your machine and then using the commands provided by both clients to indicate the path to the genesis file and bootnodes.

The process of doing this can be quite exhausting, and this calls for native implementation.

### Current State
After the implementation work done on both the Besu and Teku client pairs. Ephemery now have native support for Teku and Besu. What this mean is that we can now use `besu --network ephemery` flag on besu and `teku --network ephemery` flag on the Teku, similar to what is obtainable with other supported networks on both clients.

And not only can you use the flags genesis update is also handled automatically. And genesis reset feature also implemented on Teku. With the genesis reset the database reset happens automatically when the genesis update happens. The reset is handled via a systemd service.

In addition to the above, I also updated the current docuementation on both clients to reflect the implementation work done. To make the Ephemery setup process as easy as possible.

### Roadmap
Here is a breakdown of the implementation work done on both clients

- [x] Create genesis function on Besu and Test
- [x] Create genesis function on Teku and Test
- [x] Create genesis reset function on Teku and Test
- [x] Add documentation for Ephemery on Teku 
- [x] Add documentation for Ephemery on Besu
- [x] Create client implementation status doc on Ephemery repo
- [ ] Create genesis reset function on Besu - (In progress)
- [ ] Redesign the Ephemery website - (In progress)
- [ ] Create tutorial workthrough for current implementation - (In progress)


### Ephemery Implementation Merged PRS
 - [Add Native ephemery support on Teku](https://github.com/Consensys/teku/pull/8543)
 - [Add native support for Ephemery on Besu](https://github.com/hyperledger/besu/pull/7563)
 - [Ephemery reset on teku - Update network file](https://github.com/Consensys/teku/pull/8631)
 - [Ephemery reset on teku  - Add deposit chainId on start]( https://github.com/Consensys/teku/pull/8639)
- [ Ephemery reset on teku - Check network on start and reset db](https://github.com/Consensys/teku/pull/8642/)
- [Ephemery reset on teku - create EphemerySlotValidationService and test](https://github.com/Consensys/teku/pull/8759)
- [Add client implementation status on Ephemery repo](https://github.com/ephemery-testnet/ephemery-resources/pull/10)
- [Besu update on Ephemery repo](https://github.com/ephemery-testnet/ephemery-resources/pull/12)
- [Add update for Besu and Teku on Ephemry repo](https://github.com/ephemery-testnet/ephemery-resources/pull/15)

### Other Merged PRs Not related to Ephemery Implementation
- [fromBytes fromHexString on Teku](https://github.com/Consensys/teku/pull/8573) 
- [parameterise consolidation contract address on Besu](https://github.com/hyperledger/besu/pull/7647 )
- [Ethereum Website - Fix issues with table format](https://github.com/ethereum/ethereum-org-website/pull/13870)

### Ephemery Implementation Open Issues and PRs

#### Open Issue
-  [Add documentation for Ephemery on Besu](https://github.com/hyperledger/besu/issues/7736) 
- [Add documentation for Ephemery on Teku](https://github.com/Consensys/doc.teku/issues/620)
- [Ephemery Reset Feature on Besu](https://github.com/hyperledger/besu-docs/issues/1726)

#### Open PRs
- [Add documentation for Ephemery on Teku]( https://github.com/Consensys/doc.teku/pull/621)
- [Add documentation for Ephemery on Besu](https://github.com/hyperledger/besu-docs/pull/1727)


## Future of the Project
Beyond the fellowship, I would still love to work on this project. Currently the genesis reset has not been implemented in the Besu client. As soon as possible, I would like to commence work on it to completely close that out. 

Also for better smooth validator experience in line with the reset feature on Teku, as suggested by my mentor Paul Harris, the validator client may actually need onSlot processing also to terminate it. So for this I would need to raise a PR for that later on.

Furthermore, as can be seen from this [client implementation status table](https://github.com/ephemery-testnet/ephemery-resources/blob/master/client-implementations.md) native support is still needed in several other client pairs. To quickly progress with the Ephemery network across different clients. I would like to continue client implementation by picking any of the client pairs that has not yet been implemented.

In addition, I would like to improve on the number of validators we have on Ephemery, by been a validator myself.


## Self-evaluation, general feedback about my project and activity within EPF


### Self-Evaluation and Activity Within EPF
The motivation to learn more about the Ethereum Protocol stem out from the Ethereum Frontiers event I attended in Kenya. Though I missed most part of the sessions because my flight arrived late, but during my conversation with some of the attendees, I felt like knew very little about the Ethereum protocol itself. Even though I have been a blockchain developer for about 3 years now, I was mostly focused on Application level development.

I wasn't happy with myself about how little I knew about the Ethereum Protocol, so when I saw the call for application for this cohort, I quickly applied. Going through the application form. I was somewhat sure my application won't be accepted but I applied anyways.

Behold, I received a mail that my application was rejected but I can still join permissionlesly. When I saw that I could join permissionlessly I was really excited because all that really mattered to me was to learn more about the Protocol and I knew joining the fellowship was the easiest way for me to achieve that.

Week 0 of the fellowship and the first office hour by Tim Becko was a really insightful one, as I learnt about EIPs and Ethereum governance. The subject of EIP was really interesting for me because I have been seeing EIPs but didn't really know much about them.

Fast forward, at the start of the fellowship during office hour and stand-up, I was really intimidated by some of the Fellows because I felt they knew alot and I was just beginning my journey. Some of the terminologies and abbreviations used during this calls was really difficult to grapes. But in order to meetup with the pace of the fellowship, I commited weeks to learning everything I could by going through the entire [Ethereum Protocol Study Group Wiki](https://epf.wiki/), [Ethereum roadmap](https://ethereum.org/en/roadmap/), [Ethereum Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf) and the consume all the content on the [Ethereum Protocol Fellowship channel](https://www.youtube.com/@ethprotocolfellows/streams). I also did series of practice on how to run a node, by running different nodes and observing how it works. I also created a [video on how to run a geth and prysm node](https://youtu.be/tM5qmGFBETM).

During the fellowship, I also learned about All core dev calls. These are weekly calls. And tried to attend some of the calls. I even had to turn on my notification on the [Ethereum channel](https://www.youtube.com/@EthereumProtocol) so that I get updated whenever there is call.

I would say doing all of this in a very short period of time can be very exhausting so do what works for you. Just know how you learn.

### General Feedback About My Project
One of the most challenging part of the fellowship was deciding what to work on. Before joining the fellowship, I love the whole idea of account abstract, even gave some talk on it at some local developer conference. So I really wanted to learn more about it. 

In my mind I thought I was going to work on it. After some weeks into the fellowship, I spent some time trying to learn more about Account abstraction, consumed almost all the content on the [Account Abstraction official website](https://www.erc4337.io/) but still wasn't sure specifically which area of Account Abstraction I should work on. 

After much confusion and seeing we are already approaching project presentation. I went over the listed projected ideas many times, highlighted some of the project that caught my interest. And finally narrowed it down to [Ephemery](https://ephemery.dev/).

The initial Ephemery proposal I wrote showed I didn't really understand what I needed to do, because I just copied everything that was on the [issues roadmap](https://github.com/ephemery-testnet/ephemery-resources/issues/1) of the project instead of narrowing it down to actual implementation that can be completed within the timeframe. Thanks to Mario for the guidance!

With the knowledge gained from learning about the Consensus and Execution layer and also running of nodes. I figured working on the Ephemery project will help have a better understanding of both layers. And I most say deciding to work on this project has been one of the best decisions I made in the fellowship. 

As I have had the opportunity to learn more about nodes, Ethereum network, what it takes to maintain a network and how the EL and CL come together. 

Given the unique nature of Ephemery implementation on clients, I have also had the opportunity to brush up on my Java skills and improve on my ability to write test and to write code following an EIP, specifically the [Ephemery EIP6916](https://eips.ethereum.org/EIPS/eip-6916)

I have also had the priviledge to be mentor by some of the great minds within the Ethereum Protocol worthy of mention are Paul Harris from the Teku team, very patient with me and always quick to respond to my questions. Sally Macfarlane from the Besu team who was also there to guide my implementation work on the Besu client. pk39 and Mario Harvel from the Ephemery team who was always there to help me out with anything I needed to move forward with the project. And thanks to Holly one of the past fellow and Ephemery contributor for sharing some of your updates with me. They were really useful in giving me a sense of direction.


## Feedback about EPF



## Quick Links to Weekly Updates
