# EPF5 Dev Updates - Week 14

## What I did this week
I participated in weekly standup and Office hour. 

I continued made updates to my implementation work on Teku and Besu based on the reviewers request.

## Besu Client Implementation

I focused on refining the Logic of the genesis function and the test cases. I also made modifications to the PR base on the reviewer's requested changes.

Hopefully the PR should be merged this week as clas, method and test cases responsible for the Ephemery Genesis update has been thoroughly reviewed. Here is a link to the [Ephemery Native support PR on Besu](https://github.com/hyperledger/besu/pull/7563)

## Teku Client Implementation

I further refined the codebase and made changes based on the reviewers request. And we finally got it merged!
Here is a link to the merged PR [Ephemery Network Support on Teku PR](https://github.com/Consensys/teku/pull/8543). 

 🎉 Congratulations to us at Ephemery we now have native support for Ephemery on Teku.
 
 With this merged PR we can now run the Ephemery network on Teku without extra arguments or manual config process.

Just like other supported clients on Teku we can now start ephemery with the `teku --network ephemery` flag. And update the genesis config when it's due for update. The genesis function is been called on client start and check if an update is required and make the necessary update once it's due for update.

### What's Next
Further implementation work is still needed for the genesis reset. If this is done, node runners will not need to manually delete their db on genesis update.

Details of the work that would be done can be found in the issue [Implement genesis reset](https://github.com/Consensys/teku/issues/8589).


## Ephemery Documentation
I created a client-implementations file on the Ephemery resource github repo to help track all client implementation work done so far. Here are links to the [Add client implementation status file issue](https://github.com/ephemery-testnet/ephemery-resources/issues/9) and [Add client implementation status file PR]()

### Other Contribution Work

- Working on this issue on Besu [Parameterize Consolidation Request contract address](https://github.com/hyperledger/besu/issues/7381)
- Fix table format on the Ethereum website documentation. Here is a link to the [Fix issues with table format PR](https://github.com/ethereum/ethereum-org-website/pull/13870)


## What I will do next week
- Commence Genesis reset implementation on Teku
- Follow up on the PR from the Besu team for any requested updates
- Work on the Parameterize Consolidation Request contract address issue on Besu
- Continue the documentation work on the Ephemery repo


## References
- [Ephemery.dev](https://ephemery.dev)
- [Besu Repo](https://github.com/hyperledger/besu)
- [Teku Repo](https://github.com/Consensys/teku)
