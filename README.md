
#### Install Go Ethereum Tools

* Open your browser and navigate to the Go Ethereum Tools download page at [link](https://geth.ethereum.org/downloads/)

* Scroll down to the "Stable Releases" section

* Download latest version, in this case it is "Geth & Tools 1.10.1" 

* Decompress the archive in the "Downloads" folder, and rename the folder as **blockchain-tools**. 

* Open a terminal window, navigate to the blockchain-tools folder

#### Step 1: Generate two new nodes with new account addresses that will serve as your pre-approved sealer addresses.

* Create accounts for two nodes for the network;

- ./geth --datadir node1 account new
- ./geth --datadir node2 account new

##### Step 2: Next, generate your genesis block.

* Type the following command and press enter
 
 - ./puppeth

* Type in a name for your network and hit enter

* Type 2 to pick the Configure new genesis option
* Type 1 to choose Create new genesis from scratch
* Choose the Clique (Proof of Authority) consensus algorithm.
* Hit enter to skip "How many seconds should blocks take? (default = 15)" question

* Paste both account addresses from the first step one at a time into the list of accounts to seal. 

* Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

* Type **No** for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

* Choose a Chain/Netwrok ID (make sure to choose a 3 digit number that you've never used before as Chain/Network ID)

* When you are back at the main menu, choose the "Manage existing genesis" option.

* Choose Export genesis configurations. This will fail to create two of the files, but you only need networkname.json.

##### Step 3: Initialize the nodes with the genesis' json file.

* Using geth, initialize each node with the new networkname.json.

- ./geth --datadir node1 init networkname.json
- ./geth --datadir node2 init networkname.json

##### Step 4: Now the nodes can be used to begin mining blocks.

* Run the nodes in separate terminal windows with the commands:

- ./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
- ./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
  
##### Step 5: With both nodes up and running, the blockchain can be added to MyCrypto for testing.

* Open the MyCrypto app
* Click Change Network at the bottom left
* Click "Add Custom Node", then add the custom network information that you set in the genesis.
* Make sure that you scroll down to choose Custom in the "Network" column to reveal more options like Chain ID
![](custom_node.png)
* Type ETH in the Currency box.
* In the Chain ID box, type the chain id you generated during genesis creation.
* In the URL box type: http://127.0.0.1:8545.  This points to the default RPC port on your local machine.
* Click Save & Use Custom Node.

##### Step 6: After connecting to the custom network in MyCrypto, it can be tested by sending money between accounts.

* Select the View & Send option from the left menu pane
* Click Keystore file.
* Click Select Wallet File, then navigate to the keystore directory inside your Node1 directory, select the file located there, provide your password when prompted and then click Unlock.(This will open your account wallet inside MyCrypto.)
* Check your balance. This is the balance that was pre-funded for this account in the genesis configuration; however, these millions of ETH tokens are just for testing purposes.
* In the To Address box, type the account address from Node2, then fill in an arbitrary amount of ETH
* Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.
![](number_of_ETH_sent.png)
* Click the Check TX Status when the green message pops up, confirm the logout
![](TX_hash.png)
* You should see the transaction go from Pending to Successful in around the same blocktime you set in the genesis.
![](transaction_pending.png)
* You can click the Check TX Status button to update the status.











