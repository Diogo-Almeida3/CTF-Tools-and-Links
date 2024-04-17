# Tools

- **[Web3.py](https://web3py.readthedocs.io/en/stable/)**
- **[Foundry](https://book.getfoundry.sh/)**
- **[Electrum wallet client](https://electrum.org/)**
- **[MyCrypto Wallet client](https://mycrypto.com/)**
- **[Metamask](https://metamask.io/)**


# Foundry Tutorial

Calling a view function (That queries data):

- cast call $ADDRESS_TARGET "functionToCall()" --rpc-url $RPC_URL
- cast call $ADDRESS_TARGET "functionWithArgs(uint, bool)" 5 true --rpc-url $RPC_URL

Calling a normal function (That modifies data | Payable functions require a value):

- cast send $ADDRESS_TARGET "functionToCall()" --rpc-url $RPC_URL --private-key $PRIVATE_KEY
- cast send $ADDRESS_TARGET "functionWithArgs(uint)" 100 --rpc-url $RPC_URL --private-key $PRIVATE_KEY
- cast send $ADDRESS_TARGET "functionToCall()" --rpc-url $RPC_URL --private-key $PRIVATE_KEY --value 100

Create and deploy smart contracts:

- forge init --no-git
- src/: This is where you write your smart contracts. It initially contains an example contract called Counter.sol.
- test/: This is where you write tests. There is an example test file called Counter.t.sol. You can run these tests using the forge test command. Feel free to explore this feature on your own as it is highly useful but beyond the scope of our discussion.
- script/: This folder is used for scripts, which are batch Solidity commands that run on-chain. An example script could be a deployment script. The folder contains an example script called Counter.s.sol. You can execute these scripts using forge script script/Counter.s.sol along with additional flags based on your requirements. Feel free to experiment with this feature as it is extremely useful.
- lib/: This is where you place any libraries. By default, there is only one library called forge-std, which includes useful functions for debugging and testing. You can download additional libraries using the forge install command. For example, you can install the commonly used openzeppelin-contracts library from the OpenZeppelin repository with forge install openzeppelin/openzeppelin-contracts.
- foundry.toml: This is the configuration file for forge. You usually don't need to deal with it during exploitation, but it is helpful for development purposes.

# Deploying a contract

After completing the code:

- forge create src/Contract.sol:ContractName --rpc-url $RPC_URL --private-key $PRIVATE_KEY

After executing this command, the deployer's address (which is essentially our address), the transaction hash, and the deployed contract's address will be printed on the screen. The deployed contract's address is the one we need to use for interacting with it.

If our contract has a payable constructor, we can use the --value flag in the same way as in the cast send command:

- forge create src/Contract.sol:ContractName --rpc-url $RPC_URL --private-key $PRIVATE_KEY --value 10000

Additionally, if the constructor has arguments, we can specify them using the --constructor-args flag and provide the arguments in the same order they appear in the constructor. For example, if the constructor is defined as constructor(uint256, bytes32, bool), we would use the following command:

- forge create src/Contract.sol:ContractName --rpc-url $RPC_URL --private-key $PRIVATE_KEY --constructor-args 14241 0x123456 false
