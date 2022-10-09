# Ethereum-project
Website for use of blockchain and smart contract technology to facilitate real-estate property transactions

# Why
The current processes of buying, selling and renting property are carried out for the most part by third party real-estate agents. As a result of this, there is an element of trust required from the transacting parties (buyers, sellers, landlords & tenants).

This trust gives rise to various problems that affect the speed, cost and security of the real estate transaction processes.

# Steps:
  1. Setup a private Ethereum network that utilizes Proof-of-Authority consensus
  2. Design, write, compile and deploy the smart contracts responsible for key activities in a modified version of the real estate transaction process, onto the private      network.
  
 
# How to setup private ethereum network

## Steps to Set Up Private Ethereum Network

Below is the step-by-step guide to setting up a private Ethereum network.

### Step 1: Install Geth on Your System

Click here to Go to the official Geth download page and download setup according to your operating system.
Geth download

While installing Geth make sure to select both checkboxes as shown below.
Select checkboxes

After installing Geth on your system open PowerShell or command prompt and type geth and press enter, the following output will be displayed.
Check geth installation

### Step 2: Create a Folder For Private Ethereum

Create a separate folder for this project. In this case, the folder is MyNetwork.
Create a new folder inside the folder MyNetwork for the private Ethereum network as it keeps your Ethereum private network files separate from the public files. In this example folder is MyPrivateChain.
### Step 3: Create a Genesis Block


The blockchain is a distributed digital register in which all transactions are recorded in sequential order in the form of blocks. There are a limitless number of blocks, but there is always one separate block that gave rise to the whole chain i.e. the genesis block.

Genesis Block

As seen in the above diagram we can see that blockchain is initialized with the genesis block.

To create a private blockchain, a genesis blockis needed. To do this, create a genesis file, which is a JSON file with the following commands-

{

     “config”:{

        “chainId”:987,

        “homesteadBlock”:0,

        “eip150Block”:0,

        “eip155Block”:0,

        “eip158Block”:0

    },

    “difficulty”:”0x400″,

    “gasLimit”:”0x8000000″,

    “alloc”:{}

}

Explanation:

config: It defines the blockchain configuration and determines how the network will work.
chainId: This is the chain number used by several blockchains. The Ethereum main chain number is “1”. Any random number can be used, provided that it does not match with another blockchain number.
homesteadBlock: It is the first official stable version of the Ethereum protocol and its attribute value is “0”.
One can connect other protocols such as Byzantium, eip155B, and eip158. To do this, under the homesteadBlock add the protocol name with the Block prefix (for example, eip158Block) and set the parameter “0” to them.
difficulty: It determines the difficulty of generating blocks. Set it low to keep the complexity low and to avoid waiting during tests.
gasLimit: Gas is the “fuel” that is used to pay transaction fees on the Ethereum network. The more gas a user is willing to spend, the higher will be the priority of his transaction in the queue. It is recommended to set this value to a high enough level to avoid limitations during tests.
alloc: It is used to create a cryptocurrency wallet for our private blockchain and fill it with fake ether. In this case, this option will not be used to show how to initiate mining on a private blockchain.
This file can be created by using any text editor and save the file with JSON extension in the folder MyNetwork.

### Step 4: Execute genesis file

Open cmd or PowerShell in admin mode enter the following command-

geth –identity “yourIdentity” init \path_to_folder\CustomGenesis.json –datadir \path_to_data_directory\MyPrivateChain

Parameters-
path_to_folder- Location of Genesis file.
path_to_data_directory- Location of the folder in which the data of our private chain will be stored.

The above command instructs Geth to use the CustomGenesis.json file.

After executing the above command Geth is connected to the Genesis file and it seems like this:

excute genesis

### Step 5: Initialize the private network

Launch the private network in which various nodes can add new blocks for this we have to run the command-

geth –datadir \path_to_your_data_directory\MyPrivateChain –networkid 8080

Initialize private network

The command also has the identifier 8080. It should be replaced with an arbitrary number that is not equal to the identifier of the networks already created, for example, the identifier of the main network Ethereum (“networkid = 1”). After successfully executing the command we can see like this-

output

Note:

The highlighted text is the address of geth.ipc file finds it in your console and copy it for use in the next step.

Every time there is a need to access the private network chain, one will need to run commands in the console that initiate a connection to the Genesis file and the private network.

Now a personal blockchain and a private Ethereum network is ready.

### Step 6: Create an Externally owned account(EOA)

Externally Owned Account(EOA) has the following features-

Controlled by an External party or person.
Accessed through private Keys.
Contains Ether Balance.
Can send transactions as well as ‘trigger’ contract accounts.
Steps to create EOA are:

To manage the blockchain network, one need EOA. To create it, run Geth in two windows. In the second window console enter the following command-

geth attach \path_to_your_data_directory\YOUR_FOLDER\geth.ipc

or

geth attach \\.\pipe\geth.ipc

This will connect the second window to the terminal of the first window. The terminal will display the following-

Output

Create an account by using the command-

personal.newAccount()

After executing this command enter Passphrase and you will get your account number and save this number for future use.

save account number

To check the balance status of the account execute the following command-

ether balance

It can be seen from the above screenshot that it shows zero balance. This is because when starting a private network in the genesis file, we did not specify anything in the alloc attribute.

### Step 7: Mining our private chain of Ethereum

If we mine in the main chain of Ethereum it will require expensive equipment with powerful graphics processors. Usually, ASICs are used for this but in our chain high performance is not required and we can start mining by using the following command-

miner.start()

miner.start()

If the balance status is checked after a couple of seconds the account is replenished with fake ether. After that, one can stop mining by using the following command-

miner.stop()

miner.stop()

