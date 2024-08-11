# EPF5 Dev Updates - Week 9

## What I did this week
I actively participated in weekly standups and office hours, and delved deeper into understanding genesis generation and its implementation on the Besu client. 

To clarify my understanding, I consulted with my mentor Mario Havel, who provided valuable insights and guidance.

Additionally, I reached out to Holly Atkinson, a former EPF fellow, who shared her experience and resources on implementing genesis generation on Geth and Loadstar clients. 

I reviewed her [updates](https://hackmd.io/@HOL/Hyp4bXfV6) and GitHub PRs to inform my approach to Besu and Teku client implementation.

I have begun working on the genesis generation logic but have yet to integrate it into the Besu client. 

Currently, I am determining the appropriate location for the genesis implementation within the Besu codebase. I am continuing to explore and confirm the correct placement to ensure a seamless integration.

Here is what the standalone **Ephemery genesis generation** code looks like. This is subject to modifications;

```java

package org.example;

import java.io.FileWriter;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.time.Instant;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;
import org.json.simple.parser.ParseException;
import org.junit.Test;

import java.time.temporal.ChronoUnit;

import static org.junit.Assert.assertTrue;


public class GenerateGenesis {
    private static final String GENESIS_FILE = "ephemery.json";
    private static final int PERIOD = 28; // 28 days

    public static void main(String[] args) {
        try {
            if (Files.exists(Paths.get(GENESIS_FILE))) {
                JSONObject genesis = readGenesisFile(GENESIS_FILE);
                System.out.println("Starting network again...");
                JSONObject config = (JSONObject) genesis.get("config");
                String timestampStr = (String) genesis.get("timestamp");
                long genesisTimestamp = Long.parseLong(timestampStr);
                long chainId = (Long) config.get("chainId");

                // Calculate the number of periods since genesis
                long periodInSeconds = (PERIOD * 24 * 60 * 60);
                long currentTimestamp = Instant.now().getEpochSecond();
                long periodsSinceGenesis = ChronoUnit.DAYS.between(Instant.ofEpochSecond(genesisTimestamp), Instant.now()) / PERIOD;
                System.out.println(periodsSinceGenesis);
                if (currentTimestamp > (genesisTimestamp + periodInSeconds)) {

                    // Create new genesis data
                    long newGenesisTimestamp = genesisTimestamp + (periodsSinceGenesis * periodInSeconds);
                    long newChainId = chainId + periodsSinceGenesis;

                    // Update the genesis data with new values
                    config.put("chainId", newChainId);
                    genesis.put("timestamp", String.valueOf(newGenesisTimestamp));

                    System.out.println("chainId" + newChainId);
                    System.out.println("timestamp" + newGenesisTimestamp);

                    // Save the new genesis to a file
                    writeGenesisFile(GENESIS_FILE, genesis);
                    System.out.println("New genesis created and saved as " + GENESIS_FILE);
                } else {
                    System.out.println("No need to update genesis yet.");
                }
            } else {
                System.out.println("Genesis file does not exist.");
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static JSONObject readGenesisFile(String filePath) throws IOException, ParseException {
        String content = new String(Files.readAllBytes(Paths.get(filePath)));
        JSONParser parser = new JSONParser();
        return (JSONObject) parser.parse(content);
    }

    public static void writeGenesisFile(String filePath, JSONObject genesis) throws IOException {
        try (FileWriter file = new FileWriter(filePath)) {
            file.write(genesis.toJSONString());
        }
    }

}
```




## What I will do next week
- Continue working on Besu client implementation with focus on the genesis generation.
- Make inital PR to show the work that has been done so far and most likely start a conversation with the Besu team on where they think will be best to have the genesis generation function.



## Blockers 

- None at the moment!


## References
- [Ephemery.dev](https://ephemery.dev)
- [Besu Repo](https://github.com/hyperledger/besu)
- [Holly's Update](https://hackmd.io/@HOL/SJwLmrUmR)
- [Besu documentation](https://besu.hyperledger.org/)


 