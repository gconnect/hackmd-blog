# Final Development Update - Native Implementation of Ephemery Testnet on Besu & Teku Client Pairs


## Abstract
This project was focused on providing native support for Ephemery on Besu and Teku client pairs. 

First of all, you might be hearing about Ephemery for the first time, [Ephemery](https://ephemery.dev/) testnet is a network that rolls back to the genesis after a set period of time. 

Ephemery is focused on short term and heavy testing usecases. The purpose of this is also to avoid problems like insufficient testnet funds, inactive validators, state bloat faced by long-running testnets.

Since this testnet is still pretty new to the ecosystem, user adoption becomes really important. And to help increase the adoption the user experience of using Ephemery needed to be as smooth as possible.

Running a node shouldn't be complicated and to help reduce this complexities especially for non-technical people it becomes important to provide native support for Ephemery on different client pairs.

Here is a link to my initial [project proposal](https://github.com/eth-protocol-fellows/cohort-five/blob/main/projects/native-ephemery-client-pair-implementation.md).

## Status Report

### Initial Status
Before my implementation,  Ephemery only had native support for Geth, Reth, Lighthouse and Lodestar clients. Specificlly focused on the genesis function with genesis reset still in progress for the above mentioned clients. These implementations were done by past EPF fellows.

Also there was no way of tracking the client implementation work done. Which makes contribution a little difficult. Initially, I wasn't completely sure what work was left and what client implementation was needed. However, thanks to my mentor Mario Havel for pointing me to some resources and past fellow updates, which gave me a better idea of what I needed to do.

Before my implementation, setting up Ephemery on Teku and Besu required a manual process of downloading the genesis files from the Ephemery repo locally to your machine and then using the commands provided by both clients to indicate the path to the genesis file and bootnodes.

The process of doing this can be quite exhausting, and this calls for native implementation.

## Besu and Teku Client Implementation Details
Unlike other network implementation, Ephemery implementation on clients does not follow exactly the same pattern as other networks like Sepolia, holesky etc. This is because the network resets after a given period of time. And due to this network updates the chainId and genesis timestamp is usually not static and this calls for a custom implementation on clients.

### Besu Client Implementation
To achieve the native support on Besu, I made some update to the following files;

- `NetworkName.java`: This was where I added the base Ephemery genesis file and chainId.
- `BesuCommandTest`: Here are added test to check Ephemery values are used.
- `NetworkDeprecationMessageTest.java`: Added Ephemery to the Network Deprecation Test to generate deprecation message for deprecated networks. And this will most likely never happen Ephemery as this type of network are not easily deprecated.
- `EphemeryGenesisFile`: Created a custom EphemeryGenesisFile class to check for updates and override the existing genesis config with the updated data. The logic for this was done with following the [Ephemery EIP 6916](https://eips.ethereum.org/EIPS/eip-6916)
- `BesuCommandTest`: Added check for Ephemery on the BesuCommandTest file.
- `EphemeryGenesisFileTest`: Wrote test to cover different scenarios when performing the genesis update to ensure the update happens as at when due and only applies to Ephemery network.
- `ephemery.json`: Added Ephemery genesis config file to the resource directory and updated the existing genesis file to suit the genesis file structure used on Besu. Addded th`ethhash` variable, `discovery` and array of `bootnodes.`
- `changelog.md`: Updated the changelog.md file with the Ephemery Implementation done


### Current State
After the implementation work was done on both the Besu and Teku client pairs. Ephemery now has native support for Teku and Besu. What this means is that we can now use `besu --network ephemery` flag on besu and `teku --network ephemery` flag on the Teku, similar to what is obtainable with other supported networks on both clients.

And not only can you use the flags, the genesis update is also handled automatically. And the genesis. reset feature is also implemented on Teku. With the genesis reset the database reset happens automatically when the genesis update happens. The reset is handled via a systemd service.

In addition to the above, I also updated the documentation for both clients to reflect the implementation of work done, making the Ephemery setup process as easy as possible..

### Roadmap
Here is a breakdown of the implementation work done on both clients.

- [x] Initial Research and Planning
- [x] Develop the Ephemery function for genesis handling on Besu and Test
- [x] Develop the Ephemery function for genesis handling on Teku and Test
- [x] Client Integration with Teku
- [x] 	Client Integration with Besu
- [x] Create genesis reset function on Teku and Test
- [x] Add documentation for Ephemery on Teku 
- [x] Add documentation for Ephemery on Besu
- [x] Create client implementation status doc on Ephemery repo
- [x] Testing and Refinement
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
- [Add documentation for Ephemery on Besu](https://github.com/hyperledger/besu-docs/pull/1727)
- [Add documentation for Ephemery on Teku doc]( https://github.com/Consensys/doc.teku/pull/621)

### Other Merged PRs Not related to Ephemery Implementation
- [fromBytes fromHexString on Teku](https://github.com/Consensys/teku/pull/8573) 
- [parameterise consolidation contract address on Besu](https://github.com/hyperledger/besu/pull/7647 )
- [Ethereum Website - Fix issues with table format](https://github.com/ethereum/ethereum-org-website/pull/13870)
- [Ethereum Protocol Fellowship Wiki - Create content for scourge under the staking economics track ](https://github.com/eth-protocol-fellows/protocol-studies/pull/300)


### Ephemery Implementation Open Issues and PRs

#### Open Issue
- [Add documentation for Ephemery on Teku](https://github.com/Consensys/doc.teku/issues/620)
- [Ephemery Reset Feature on Besu](https://github.com/hyperledger/besu-docs/issues/1726)

#### Open PRs
-  [Update the client implementation status for Besu and Teku on Ephemery repo](https://github.com/ephemery-testnet/ephemery-resources/pull/15)

### Screenshots From Besu and Teku Node Interactions

#### Besu Client
![Screenshot 2024-09-18 at 5.17.19 AM](https://hackmd.io/_uploads/BJeBSyB-Jl.png)
![Screenshot 2024-09-18 at 5.17.07 AM](https://hackmd.io/_uploads/ryxLSyHZJg.png)
![Screenshot 2024-09-18 at 5.16.52 AM](https://hackmd.io/_uploads/SyeUS1BW1l.png)

#### Teku Client
![Screenshot 2024-09-18 at 5.16.35 AM](https://hackmd.io/_uploads/BJCBByHZye.png)


## Future of the Project
Beyond the fellowship, I would still love to work on this project. Currently the genesis reset has not been implemented in the Besu client. As soon as possible, I would like to commence work on it to completely close that out. 

Also for better smooth validator experience in line with the reset feature on Teku, as suggested by my mentor Paul Harris, the validator client may actually need onSlot processing also to terminate it. So for this I would need to raise a PR for that later on.

Furthermore, as can be seen from this [client implementation status table](https://github.com/ephemery-testnet/ephemery-resources/blob/master/client-implementations.md) native support is still needed in several other client pairs. To quickly progress with the Ephemery network across different clients, I would like to continue client implementation by picking any of the client pairs that has not yet been implemented.

In addition, I would like to add to the number of validators we have on Ephemery, by being a validator myself.

When I wasn't certain on what I was going to work on, and I noticed most protocol projects are usually written in Go or Rust. So I decided to take a two weeks crash course on Go and Rust. I have not yet had the opportunity apply this knowledge in any protocol project. At least not yet. 

Since I ended up working on Ephemery and the Client Pairs I worked on made use of Java. But I know this knowledge will come in handy in the future. Especially as I planned working on other client pairs. And would most likely select client pairs that is written Rust and Go.

Overall, I would still like to have a much deeper knowledge of the Consensus client by continuing my contribution work on Teku by working on existing issues and possibly new features as I progress.

### Ephemery Client Implementation Status
#### EL Clients
![Screenshot 2024-11-02 at 9.27.31 PM](https://hackmd.io/_uploads/Bk5cvkSWke.png)

#### CL Clients
![Screenshot 2024-11-02 at 9.27.42 PM](https://hackmd.io/_uploads/HJ99DJS-ke.png)


## Self-evaluation, general feedback about my project and activity within EPF


### Self-Evaluation and Activity Within EPF
The motivation to learn more about the Ethereum Protocol stemmed from the Ethereum Frontiers event I attended in Kenya. Though I missed most part of the sessions because my flight arrived late, during my conversation with some of the attendees, I felt like I knew very little about the Ethereum protocol itself. Even though I have been a blockchain developer for about 3 years now, I was mostly focused on Application level development.

I became uncomfortable about how little I knew about the Ethereum Protocol, so when I saw the call for application for this cohort, I quickly applied. Going through the application form. I was somewhat sure my application wouldn't be accepted but I applied anyway.

Afterward, I received a mail that my application was rejected but I can still join permissionlessly. When I saw that I could join permissionlessly, I was really excited because all that really mattered to me was to learn more about the Protocol and I knew joining the fellowship was the easiest way for me to achieve that.

Week 0 of the fellowship and the first office hour by Tim Beiko was a really insightful one, as I learnt about EIPs and Ethereum governance. The subject of EIP was really interesting for me because I have been seeing EIPs but didn't really know much about them.

Fast forward, at the start of the fellowship during office hours and stand-up, I was really intimidated by some of the Fellows, because I felt they knew alot and I was just beginning my journey. Some of the terminologies and abbreviations used during this calls was really difficult to grapes. But in order to meetup with the pace of the fellowship, I commited weeks to learning everything I could by going through the entire [Ethereum Protocol Study Group Wiki](https://epf.wiki/), [Ethereum roadmap](https://ethereum.org/en/roadmap/), [Ethereum Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf) and the consume all the content on the [Ethereum Protocol Fellowship channel](https://www.youtube.com/@ethprotocolfellows/streams). I also did series of practice on how to run a node, by running different nodes and observing how it works. I also created a [video on how to run a geth and prysm node](https://youtu.be/tM5qmGFBETM).

During the fellowship, I also learned about All core dev calls. These are weekly calls. I tried to attend some of the calls. I even had to turn on my notification on the [Ethereum channel](https://www.youtube.com/@EthereumProtocol) so that I get updated whenever there is call.

I would say doing all of this in a very short period of time can be very exhausting so do what works for you. Just know how you learn.

### General Feedback About My Project
One of the most challenging parts of the fellowship was deciding what to work on. Before joining the fellowship, I loved the whole idea of account abstract, even gave some talk on it at some local developer conference. So I really wanted to learn more about it. 

In my mind I thought I was going to work on it. After some weeks into the fellowship, I spent some time trying to learn more about Account abstraction, consumed almost all the content on the [Account Abstraction official website](https://www.erc4337.io/) but still wasn't sure specifically which area of Account Abstraction I should work on. 

After much confusion and seeing we are already approaching the project presentation. I went over the listed [proposed projected ideas](https://github.com/eth-protocol-fellows/cohort-five/blob/main/projects/project-ideas.md) many times, highlighted some of the project that caught my interest. And finally narrowed it down to [Ephemery](https://ephemery.dev/).

The initial Ephemery proposal I wrote showed I didn't really understand what I needed to do, because I just copied everything that was on the [issues roadmap](https://github.com/ephemery-testnet/ephemery-resources/issues/1) of the project instead of narrowing it down to actual implementation that can be completed within the timeframe. Thanks to Mario for the guidance!

With the knowledge gained from learning about the Consensus and Execution layer and also running of nodes. I figured working on the Ephemery project will help have a better understanding of both layers. And I most say deciding to work on this project has been one of the best decisions I made in the fellowship. 

As I have had the opportunity to learn more about nodes, Ethereum network, what it takes to maintain a network and how the EL and CL come together. 

Given the unique nature of Ephemery implementation on clients, I have also had the opportunity to brush up on my Java skills and improve on my ability to write test and to write code following an EIP, specifically the [Ephemery EIP 6916](https://eips.ethereum.org/EIPS/eip-6916)

I have also had the privilege to be mentored by some of the great minds within the Ethereum Protocol worthy of mention are Paul Harris from the Teku team, very patient with me and always quick to respond to my questions. Sally Macfarlane from the Besu team who was also there to guide my implementation work on the Besu client. pk910 and Mario Havel from the Ephemery team who were always there to help me out with anything I needed to move forward with the project. And thanks to Holly one of the past fellow and Ephemery contributor for sharing some of your updates with me. They were really useful in giving me a sense of direction.


## Feedback about EPF
 
 I think the idea of EPF is a very good one, as it gives newbies into protocol contribution a learning ground where they can get comfortable and have the opportunity to meet with approachable OGs within the Ethereum Protocol. Thanks to Josh and Mario for putting this together!

I would love to see this initiative continue running. During one of  the weekly stand breakout rooms when I shared my experience, one of the fellows mentioned that things would have been a lot easier for me if I started with the Ethereum Protocol Study Group, which is very correct. 

Because this was the feeling I had when I found out about the Women in Ehtereum Protocol which is specially designed for women to get comfortable working in teams, open source and on the Ethereum Protocol. Unfortunately I also found out about it when I was already in the fellowship.

My suggestion for EPF would be to adjust some discussions that are too high-level, as they might not consider Protocol beginners in the room. Sometimes one might struggle to understand the discussions and make valuable contributions.

My advice for new fellows is that if this is an area you are really interested in, start now to study. There are a lot of things to learn which you might not have the time to catch up with by the time you start working on projects. Don't get carried away by the different All core devs call. Join the ones that meet your interest. Learn in public, ask questions and don't be shy!

When it comes to project selection, unless you have a concrete idea and implementation strategy, don't waste time trying to build out your idea from scratch. It's easier to pick from the list of already existing problems, than thinking about what to work on.

## Conclusion

I am happy to be a part of EPF cohort 5, the fellows and mentors I met, the opportunity my participation has opened up for me. 

I now have confidence when it comes to protocol contributions. I look forward to continuing this journey and growing beyond where I am now!

Worthy of mention, I started the fellowship as a permissionless fellow and ended the fellowship as an official Ethereum Protocol Fellow. Really excited for the opportunity and what's ahead!

To follow up on my [other weekly updates here is a link](https://hackmd.io/@gconnect).

Long live Ethereum Protocol, and long live the Ethereum Protocol Fellowship!
