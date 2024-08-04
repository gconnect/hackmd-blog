# EPF5 Dev Updates - Week 8

## What I did this week
- Participated in weekly standup and office hour
- Started implementing native support for Ephemery Testnet on Besu client.

### Native Client Support for Ephemery Testnet on Besu Client
Here is a breakdown of the current implementation work done;

- git clone the Besu repo, setup and run locally
- Add the `ephemery.json` (Genesis file) to the `config/src/main/resources` directory
- Add Ephemery to the `besu/cli/config/NetworkName.java` file like this 

```bash
  /** EPHEMERY network name. */
  EPHEMERY("/ephemery.json", BigInteger.valueOf(39438135)),
````

- Add the bootnode to the `ephemery.json` genesis file
```bash
   "discovery": {
      "bootnodes": [
        "enode://50a54ecbd2175497640bcf46a25bbe9bb4fae51d7cc2a29ef4947a7ee17496cf39a699b7fe6b703ed0feb9dbaae7e44fc3827fcb7435ca9ac6de4daa4d983b3d@137.74.203.240:30303",
        "enode://0f2c301a9a3f9fa2ccfa362b79552c052905d8c2982f707f46cd29ece5a9e1c14ecd06f4ac951b228f059a43c6284a1a14fce709e8976cac93b50345218bf2e9@135.181.140.168:30343"
      ]
    }
```

- Add Test for the Ephemery network config 
Test can be add in the `/besu/cli/BesuCommandTest.java
` file.

```bash
  @Test
  public void ephemeryValuesAreUsed() {
    parseCommand("--network", "ephemery");

    final ArgumentCaptor<EthNetworkConfig> networkArg =
            ArgumentCaptor.forClass(EthNetworkConfig.class);

    verify(mockControllerBuilderFactory).fromEthNetworkConfig(networkArg.capture(), any());
    verify(mockControllerBuilder).build();

    assertThat(networkArg.getValue()).isEqualTo(EthNetworkConfig.getNetworkConfig(EPHEMERY));

    assertThat(commandOutput.toString(UTF_8)).isEmpty();
    assertThat(commandErrorOutput.toString(UTF_8)).isEmpty();
  }
```
-  Add Ehemery to the `/besu/src/test/java/besu/cli/NetworkDeprecationMessageTest` file

```bash
  @ParameterizedTest
  @EnumSource(
      value = NetworkName.class,
      names = {
        "MAINNET", "SEPOLIA", "DEV", "CLASSIC", "MORDOR", "HOLESKY", "LUKSO", "EPHEMERY"
      })
```
### Test Output
Click on the the play icon on the ephemery test script and select `Run BesuCommandTest.ephem..`

![Screenshot 2024-08-04 at 11.31.23 PM](https://hackmd.io/_uploads/ry5rZt6KC.png)

### Run the node to test implementation

Here is the command for running the node from the clone ;

 
To see all of the gradle tasks that are available:
```bash
cd besu
./gradlew tasks

# Build from source - Build the distribution binaries: 
cd besu
./gradlew installDist

# Run from the binaries you built from source

cd build/install/besu  && ./bin/besu --network ephemery

```

The output should look like this 

![Screenshot 2024-08-05 at 12.00.15 AM](https://hackmd.io/_uploads/HkeGdtat0.png)


![Screenshot 2024-08-05 at 12.01.16 AM](https://hackmd.io/_uploads/r1cr_F6tR.png)

![Screenshot 2024-08-05 at 12.01.30 AM](https://hackmd.io/_uploads/ry3I_tpKC.png)

#### Note
Ephemery Testnet is currently running using the flag `--ephemery` current implementation makes use of the default
`ephemery.json` genesis. Future updates will ensure the genesis is update base on the genesis reset logic.

## What I will do next week
- Continue working on Besu client implementation
- Update the current implementation done on the `NetworkName.java` file so that the chainId is dynamic instead of constant to align with the new genesis gotten from the implementation logic for the genesis reset function
- Work on the genesis reset function and figure out where the code will be added on the Besu client
- Setup Teku client locally on my machine


## Blockers 

- None at the moment!


## References
- [Ephemery.dev](https://ephemery.dev)
- [Besu Repo](https://github.com/hyperledger/besu)
- [Teku documentation](https://docs.teku.consensys.io/)
- [Besu documentation](https://besu.hyperledger.org/)


 