Simple contract for testing nukomask

Basic development environment setup

If you already have a testnet or wanna burn some real nuko skip to nukotest instructions

Install the latest nukomask release for your favorite browser: https://github.com/nekonium/NukoMask
or from my fork https://github.com/SerendipityDoDa/NukoMask if it is newer

Download and extract the latest release of https://github.com/nekonium/go-nekonium

Create a file named genesis_private.json in the gnekonium folder with the following content:
{
  "config": {
        "chainId": 2,
        "homesteadBlock": 0,
        "eip150Block": 0,
        "eip155Block": 100,
        "eip158Block": 100
  },
  "coinbase"   : "0x0000000000000000000000000000000000000000",
  "difficulty" : "0x200",
  "extraData"  : "",
  "gasLimit"   : "0x2fefd8",
  "nonce"      : "0x0000000000000042",
  "mixhash"    : "0x0000000000000000000000000000000000000000000000000000000000000000",
  "parentHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
  "timestamp"  : "0x00",
  "alloc": {
  }
}

Initialize testnet with: gnekonium --datadir privatenet init genesis_private.json

Use nukomask to "Export Private Key" of "Account 1" and save the key in the gnekonium folder

Import the private key with: gnekonium --datadir privatenet account import "MetaMask Account 1 Private Key"
Delete that "MetaMask Account 1 Private Key" for security

Start testnet with: gnekonium --networkid "10" --rpc --rpcaddr "localhost"  --rpccorsdomain "*" --nodiscover --datadir privatenet --mine --minerthreads 1 console
It might take some time to generate the DAG the first time

Select the testnet in nukomask using: localhost 8293
If everything is running properly you should see the "Account 1" balance growing.

-nukotest instructions

Download and extract the latest release of nukotest https://github.com/SerendipityDoDa/nukotest

Open the latest release of https://github.com/nekonium/browser-solidity
Open the contract file nukotest/contracts/Test.sol
It should have compiled automatically but if not hit the compile button on the Settings tab
I can't seem to select "Injected Web3" so I use Web3 Provider
You should see the account imported into gnekonium testnet

One can either use the mining node instance or open another terminal and attach to the existing instance with: gnekonium attach
Then unlock the account you added with: personal.unlockAccount(eth.accounts[0]) 
Use the create button on the Contract tab
copy the contract address for use in the test

nukotest uses node.js npm to install a test web server called lite-server.
Change to the nukotest folder and run: npm install
Once npm install completes run the test server with: npm run dev
If you would rather use your own web server then you will need to host the "nukotest/src" folder.

I get an error from nukomask when I attempt to run the DoTest function: MetaMask - RPC Error: Internal JSON-RPC error. Object { code: -32603, message: "Internal JSON-RPC error." } inpage.js:1:3679
but the test is now working in my fork of nukomask
Stepping through the process on testnet yeilds the same RPC error
Web3 simply doesn't log it to the console because it is normal I guess






