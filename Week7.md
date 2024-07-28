# EPF5 Week 7 Update

## What I did this week

- Attended daily standup meetings to discuss progress.
- Presented my proposal during the office hour, providing updates and receiving feedback.
- Joined the ConsenSys Discord community and specific channels for Teku and Besu to engage with the community and gather insights.
- Also joined the Besu Hyperledger Discord to engage with the community and gain a deeper understanding of Besu.
- Practiced Custom Setup for Ephemery on Geth and Lighthouse
- Installed necessary libraries and tools to prepare my machine for running Besu and Teku clients. Specifically, I installed: Java, Besu client, Teku client and inteliJ IDE in preparation for Java development.
- Tested the Besu client on the Sepolia network to ensure everything checks out before running it on Ephemery.
- Completed a custom setup for Ephemery on both Besu and Teku clients, exploring different configurations and settings.
- Began an in-depth study of the Besu documentation and its GitHub repository to understand the architecture and identify areas for implementation.This study is crucial for determining where and how to integrate my proposed solution within the Besu client.
- Created an [issue](https://github.com/hyperledger/besu/issues/7387) on the Besu GitHub repository to track and discuss the implementation of Ephemery on the Besu client.
- Forked and Clone the Besu repository to my machine. Installed the necessary dependencies and ran the node the client from my local cloned version.


## Ephemery Custom Setup on Geth and Lighthouse
I was able to successfully performed a custom setup for Ephemery on both Geth and Lighthouse client using this command;

### Note
Before running the below command ensure you download the latest [ephemery tar.gz file](https://github.com/ephemery-testnet/ephemery-genesis/releases/). Also ensure you have [Lighthouse](https://lighthouse-book.sigmaprime.io/installation.html) and [Geth](https://geth.ethereum.org/downloads) installed on your machine.


### Step 1 - Generate JWT secret
Run this command to generate your jwtsecret

```bash
openssl rand -hex 32 | tr -d "\n" | sudo tee /secrets/jwtsecret.hex
```

### Step 2 - Start the Execution Client
```bash=
geth --datadir geth-ephemery init ./ephemery/genesis.json # path  to your genesis.json file


# // use this to load the env variables in nodevars_env.txt file
source ephemery/nodevars_env.txt

geth --datadir geth-ephemery --authrpc.jwtsecret=./jwtsecret --bootnodes $BOOTNODE_ENODE 

```

### Step 3 - Start the Consensus Client
```bash=
lighthouse bn -t ephemery --execution-endpoint http://localhost:8551 --execution-jwt=./jwtsecret --boot-nodes=$BOOTNODE_ENR_LIST


# Allowing insecure genesis sync
lighthouse bn -t ../ephemery --execution-endpoint http://localhost:8551 --execution-jwt=./jwtsecret --boot-nodes=$BOOTNODE_ENR_LIST --allow-insecure-genesis-sync

# Alternatively
 
# syncing with a checkpoint
lighthouse bn -t ../ephemery --execution-endpoint http://localhost:8551 --execution-jwt=./jwtsecret --boot-nodes=$BOOTNODE_ENR_LIST --checkpoint-sync-url=https://checkpointz.bordel.wtf/ 
```

## Running Teku and Besu on Sepolia

### Note
Before running the below command ensure you have [Besu](https://besu.hyperledger.org/public-networks/get-started/install/binary-distribution) and [Teku](https://docs.teku.consensys.io/get-started/install/install-binaries) installed on your machine. 

For this setup we don't need to download sepolia because Teku and Besu have native support for Sepolia.

### Step 1 - Generate JWT secret
Run this command to generate your jwtsecret

```bash
openssl rand -hex 32 | tr -d "\n" | sudo tee /secrets/jwtsecret.hex
```

### Step 2 - Besu Execution Client Setup

```bash
besu  --network=sepolia            
  --rpc-http-enabled=true      
  --rpc-http-host=0.0.0.0      
  --rpc-http-cors-origins="*"  
  --rpc-ws-enabled=true        
  --rpc-ws-host=0.0.0.0        
  --host-allowlist="*"         
  --engine-host-allowlist="*"  
  --engine-rpc-enabled
  --data-path=besu-holesky
  --engine-jwt-secret=./jwtsecret
```

### Step 3 - Teku Consensus Client Setup

Without checkpoint you can use this command add the` --initial-state` flag
```bash
teku --network=sepolia 
    --initial-state=https://sepolia.beaconstate.info  
    --ee-endpoint=http://localhost:8551
    --ee-jwt-secret-file=jwtsecret 
    --metrics-enabled=true
    --rest-api-enabled=true
```

Alternatively with checkpoint
```bash
 teku --network=sepolia  
  --ee-endpoint=http://localhost:8551           
  --ee-jwt-secret-file=jwtsecret
  --metrics-enabled=true
  --rest-api-enabled=true
  --p2p-advertised-ip=127.0.0.1:30303
  --checkpoint-sync-url=https://sepolia.be
```

## Custom Setup for Ephemery on Besu and Teku
Similar to what we did when setting up geth and Lighthouse is what we are goin to do here for Ephmery custom implementation on Besu and Teku.

Before running the below command ensure you download the latest [ephemery tar.gz file](https://github.com/ephemery-testnet/ephemery-genesis/releases/). 

Also ensure you have [Besu](https://besu.hyperledger.org/public-networks/get-started/install/binary-distribution) and [Teku](https://docs.teku.consensys.io/get-started/install/install-binaries) installed on your machine.

### Step 1 - Generate JWT secret
Run this command to generate your jwtsecret

```bash
openssl rand -hex 32 | tr -d "\n" | sudo tee /secrets/jwtsecret.hex
```

// use this to load the env variables in nodevars_env.txt file
```bash
source ephemery/nodevars_env.txt
```
### Step 2 - Besu Execution Client Setup

```bash
besu --genesis-file=ephemery/besu.json    
  --bootnodes=$BOOTNODE_ENODE      
  --rpc-http-enabled=true      
  --rpc-http-host=0.0.0.0      
  --rpc-http-cors-origins="*"  
  --rpc-ws-enabled=true        
  --rpc-ws-host=0.0.0.0        
  --host-allowlist="*"         
  --engine-host-allowlist="*"  
  --engine-rpc-enabled         
  --data-path=besu-ephemery
  --engine-jwt-secret=./jwtsecret
```

### Step 3 - Teku Consensus Client Setup
```bash
 teku --genesis-state=ephemery/besu.json 
 --ee-endpoint=http://localhost:8551  
 --ee-jwt-secret-file=./jwtsecret  
 --metrics-enabled=true 
 --rest-api-enabled=true  
 --p2p-discovery-bootnodes=$BOOTNODE_ENR_LIST   
 --ignore-weak-subjectivity-period-enabled
```

## What I will do next week

- Continue studying Besu's documentation and codebase.
- Start implementing the --ephemery flag support on the Besu client.
- Add test to the implementation
- Figure out how and where in the Besu code base to handle the genesis reset function
- Collaborate with the community and mentor to when the need arise


## blockers
None at the moment.
