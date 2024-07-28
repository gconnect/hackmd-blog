# EPF5 Week 7 Update

## What I did this week

- Attended daily standup meetings to discuss progress.
- Presented my proposal during the office hour, providing updates and receiving feedback.
- Joined the ConsenSys Discord community and specific channels for Teku and Besu to engage with the community and gather insights.
- Also joined the Besu Hyperledger Discord to engage with the community and gain a deeper understanding of Besu.
- Practiced Custom Setup for Ephemery on Geth and Lighthouse

I was able to setup the geth client and lighthouse client using this command

```bash=

Commands to run when setting up the execution client
geth --datadir geth-ephemery init ../../ephemery/genesis.json (depending on the path your genesis file is located)

source ephemery/nodevars_env.txt  ( read the boot node files)

geth --datadir geth-ephemery --authrpc.jwtsecret=../../jwtsecret --bootnodes $BOOTNODE_ENODE (get the path to your jwt secret)

lighthouse bn -t ephemery --execution-endpoint http://localhost:8551 --execution-jwt=./../jwtsecret --boot-nodes=$BOOTNODE_ENR_LIST


// light node setup
// allowing insecure genesis sync
lighthouse bn -t ../ephemery --execution-endpoint http://localhost:8551 --execution-jwt=../../jwtsecret --boot-nodes=$BOOTNODE_ENR_LIST --allow-insecure-genesis-sync

// syncing with a checkpoint
lighthouse bn -t ../ephemery --execution-endpoint http://localhost:8551 --execution-jwt=../jwtsecret --boot-nodes=$BOOTNODE_ENR_LIST --checkpoint-sync-url=https://checkpointz.bordel.wtf/ 
```





Documented the setup steps and captured screenshots and videos as part of the walkthrough.
Setting Up Environment for Besu and Teku

Installed necessary libraries and tools to prepare my machine for running Besu and Teku clients. Specifically, I installed:
Java
Besu client
Teku client
Testing on Sepolia Network

Tested the Besu client on the Sepolia network to ensure proper functionality and setup.
Custom Setup for Ephemery on Besu and Teku

Completed a custom setup for Ephemery on both Besu and Teku clients, exploring different configurations and settings.
Studying Besu Documentation and GitHub Repository

Began an in-depth study of the Besu documentation and its GitHub repository to understand the architecture and identify areas for implementation.
This study is crucial for determining where and how to integrate my proposed solution within the Besu client.
Issue Creation for Ephemery Implementation on Besu

Created an issue on the Besu GitHub repository to track and discuss the implementation of Ephemery on the Besu client.
The issue can be found here.
Next Steps
Continue studying Besu's documentation and codebase.
Start implementing the proposed solution for Ephemery on the Besu client.
Collaborate with the community and team members to refine the approach and address any challenges.
Provide regular updates and document progress for future reports.