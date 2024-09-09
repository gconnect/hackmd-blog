# EPF5 Dev Updates - Week 13

## What I did this week
I participated in weekly standup and Office hour. 
This week office hour we had Toni Wahrstätter! Toni is a researcher from Applied Research Group (EF team) known mostly for his data analysis work. 

He is mainly focused on consensus research, using data for empirical analysis of the current Ethereum network and research proposals. 

He is also interested in subjects around privacy and censorship resistance efforts. We had the opportunity of asking him questions around CL, privacy and Protocol level data analysis. He also shared some helpful resources for those looking to go into Protocol Data Analysis. He mentioned [xatu](xatuhttps://github.com/nerolation/pyxatu). Xatu contains alot of Ethereum data situable for analysis.

I continued my client implementation work on both Besu and Teku.

## Besu Client Implementation

I focused on refining the Logic of the genesis function and the test cases. I also made modifications to the PR base on the reviewer's requested changes.

I created a new [Ephemery Network Support on Besu PR](https://github.com/hyperledger/besu/pull/7563) is still under review by Sally Macfarla from the Besu team she said she won't be available until Tuesday. Until then I am also checking & testing the code to ensure everything works as expected. I ran the Besu client alongside the Teku client using the `--ephemery` flag and they both connected fine.

## Teku Client Implementation
I had an extensive meeting with Paul Harris to discuss best implementation approach that will work for the Teku client. During the meeting I explained to Harris what [Ephemery](ephemery.dev) network is about and our expectations regarding how it should work on clients. 

In the meeting we went over the Teku codebase focusing on the TekuConfiguation and the Configuration builder to find a situable place for implementation especially with regards to the config file. 

The `ephemery.yaml` since this file will need to be updated. In my previous implementation I added the `ephemery.ssz` and `ephemery.yaml` file manually as was the case with other network. 

But given the unique nature of Ephemery network. I had to remove the `ephemery.ssz` file and instead utilized the checkpointSync feature provided in the `Eth2NetworkConfiguration.java` file in the Teku codebase.

And to update the `ephemery.yaml`. I created a seperate EphemeryNetwork class with an `update` method to handle the update of the yaml file with the utilizing of the NetworkConfigurationBuilder.

During the meeting we ran into a couple of error while trying to run the Ephemery network this was due to the nature of the config file which was not completely in sync with other network config file like mainnet. Ephemery had some extra Network config field which were not supported by Teku. So that will mean updating the existing Network test to do a seperate check for Ephemery to avoid those run time errors and warnings.

Got some warnings like this;
```bash
Unknown extra config params  2024-09-05 01:14:35.363+01:00 | Test worker | WARN  | SpecConfigReader | Ignoring unknown items in network configuration: TARGET_NUMBER_OF_PEERS,WHISK_EPOCHS_PER_SHUFFLING_PHASE,WHISK_PROPOSER_SELECTION_GAP,EIP7594_FORK_VERSION,MAX_CELLS_IN_EXTENDED_MATRIX,MAX_REQUEST_DATA_COLUMN_SIDECARS,NUMBER_OF_COLUMNS,CUSTODY_REQUIREMENT,EIP7594_FORK_EPOCH,DATA_COLUMN_SIDECAR_SUBNET_COUNT,SAMPLES_PER_SLOT
2024-09-05 01:14:35.478+01:00 | Test worker | WARN  | SpecConfigReader | Ignoring unknown items in network configuration: TARGET_NUMBER_OF_PEERS,WHISK_EPOCHS_PER_SHUFFLING_PHASE,WHISK_PROPOSER_SELECTION_GAP,EIP7594_FORK_VERSION,MAX_CELLS_IN_EXTENDED_MATRIX,MAX_REQUEST_DATA_COLUMN_SIDECARS,NUMBER_OF_COLUMNS,CUSTODY_REQUIREMENT,EIP7594_FORK_EPOCH,DATA_COLUMN_SIDECAR_SUBNET_COUNT,SAMPLES_PER_SLOT
```

Here is a link to the [Ephemery Network Support on Teku PR](https://github.com/Consensys/teku/pull/8543). So far I have added most of the required configuation files. Pending review from Paul Harris.

### Other Contribution Work

I also worked on this [issue](https://github.com/Consensys/teku/issues/8506) regarding SSZ conversion fromBytes format and fromHexString. I created the fromByte and fromHexString and also created test for them. 

So far this has been merged. Here is a link to the [merged PR](https://github.com/Consensys/teku/pull/8573 ) And it happens to be my first merged client protocol contribution. 🎉

## Lessons Learnt So Far
My implementation work on both clients are quite big and I made the mistake of trying to complete them in one big PR instead of breaking them down in bits.

Working on this project has also helped me to learn about Teku and Besu. First of all it made me to start coding in Java again after about 5 years of not writing Java. And I am really happy about the fact that my Java knowledge has started coming back.

The Ephemery implementation work has helped me to understand what it means to setup a network, all the necessary configurations files involved, both client and infrastructure setup requirements. And I have also learnt to code following an EIP standard.

And more importantly I have become comfortable running nodes and studying the Besu and Teku codebase to understand what EL client and CL client implementation look like and been able to confidently contribute to these large codebase is something I don't take forgranted.

## What I will do next week
- Follow up on the PR from the Besu team for any requested updates
- Follow up on the PR from the Teku team for any requested updates
- Further test implementation
- Will pick an issue from either Besu or Teku
- Start documenting the work done on the Ephemery repo


## References
- [Ephemery.dev](https://ephemery.dev)
- [Besu Repo](https://github.com/hyperledger/besu)
- [Teku Repo](https://github.com/Consensys/teku)
