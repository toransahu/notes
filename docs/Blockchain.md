[TOC]

# Introduction
## Trade-offs
- Public vs Private
- Security vs Performance


# Terminologies
- Genesis
- Consensus
    - Proof-of-Work
    - Proof-of-Stake
    - Proof of Byzantine Fault Tollerance 
- Black Node/Block
- Orphan Block (Purple)
- Immutable distributed Ledger
- Double Spending
- Node
    - Any computer that connects to the Bitcoin network is called a node
    -  every mining computer, every computer that has a bitcoin wallet and by special sites that give blockchain monitor services
- Full Node
    - Nodes that fully verify all of the rules of Bitcoin
    - Full nodes download every block and transaction and check them against Bitcoin's consensus rules
- Merkle Tree
    - Hash of transaction in a block
- Keys    
    - [Source](https://www.coindesk.com/information/how-do-bitcoin-transactions-work/)
    - Private Key (64): Assiged to node on joining network
    - Public Key (34): same as above but can be publiced, same as bitcoin QR code 
        - balances in wallet are fetched from bitcoin address, which is public key of the wallet

# Components
- Transactions
    - commits changes to the blockchain
    - contains signature of owner of address
    - many transactions inside a block
- Blocks
    - conatins an ordered bunch of transactions
        - timestamps the transactions, are immutable
    - each block references the previous block
    
## Block
- Hash
- Data
- Previous Hash
    

# Features
- Encryption of data
- Proof-of-work
- History
- Decentralized Data
- Trust in Data
- No Intermediaries
- Network Type
    - Public 
    - Private
- Authentication    
    - peers signs the transaction with their private key
       

# Applications
- Banking & Money Transfer
- Healthcare
- All types of document management
    - Land / Real State
        - Owner's Doc
        - Transfer Deeds
        - Land History
    - Certificates
        - Birth
        - Caste
        - Marriage
        - Death
    - Contracts
- Governance
    - All the govt. data
- Voting
    - Voter Registration
    - Voter Identification
    - Electronic Voting
- Cloud Storage
- Digital Twin
- Energy management
- Online Music
- Retail Shops
- Crowdfunding
    - Startups
    - Govt. & Contractor
- Avoid Intermediaters
    - Advocate
    - Bank
    - Other 3rd Parties
- Blockchain + AI
    - Decentralized AI platform
    
# Facts    
- data commited to ledger cann't be changed

# Frameworks
Source1: https://medium.com/hyperlegendary/6-blockchain-frameworks-to-build-enterprise-blockchain-how-to-choose-them-2b7d50ba275c  
Source2: https://www.blockchain-council.org/blockchain/list-of-best-open-source-blockchain-platforms/

- Hyperledger (active Consumer): https://github.com/hyperledger/composer/
- Ethereum: https://github.com/ethereum
- MultiChain: https://github.com/MultiChain , https://www.multichain.com
- OpenBlockChain : https://github.com/openblockchain
- Eris

# Workflow
- genesis
- few transactions by few peoples
- transactions stored temporary in transaction pool
- many miners try to solve for candidate block
    - candidate block is the next block going to be added to the blockchain
    - a block can store a limited amount of transactions (1MB, in Bitcoin Hard Cash 8MB, 500 transactions etc.)
    - they will take the all transaction data and create hash from that by making chnages in nonce
- any one miner won the race
- he will broadcast the hash/new to the network
- rest of the miners will validate the calculated hash
    - there are some math like value of hash should be less than [target](http://learnmeabitcoin.com/guide/blocks)
        - source: http://learnmeabitcoin.com/guide/blocks)
        - or a simple math for example, hash should start with 0000
- if validations succeed, all the         

    
# FAQ
- how data changes reaches to the leader
- how leader'd PoW are verified
- where the new block will get added if one leader solved the problem
- what is the mathematical problem to be solved
- how many transactions in single block
- when is new block created and why?
- how creation/updation in doc will be validated, before audit?
- how to avoid false data entry by doctors?
- how to add real time data like, pulse, heartbit directly from device? include IoT?
- who are PoW validators? Are the other miners?
- who are ledger keepers? are they miners?


----------------------------------------------------------

# Multichain

## [Installation](https://www.multichain.com/download-install/)


```bash
su (enter root password)

cd /tmp
wget https://www.multichain.com/download/multichain-1.0.5.tar.gz
tar -xvzf multichain-1.0.5.tar.gz
cd multichain-1.0.5
mv multichaind multichain-cli multichain-util /usr/local/bin (to make easily accessible on the command line)

exit (to return to your regular user)
```

## Getting Started

### [Nodes On Different Servers](https://www.multichain.com/getting-started/)

#### Node 1 Initial Setup on Server 1
- Run 
    ```bash
    #Create chain1
    multichain-util create chain1
    ```
    
- Output
    ```bash
    MultiChain 1.0.5 Utilities (latest protocol 10011)

    Blockchain parameter set was successfully generated.
    You can edit it in /home/toran/node1/chain1/params.dat before running multichaind for the first time.

    To generate blockchain please run "multichaind chain1 -daemon".
    ```

- Run
    ```bash
    #Initialize Blockchain with genesis block
    multichaind chain1 -daemon
    ```    
    
- Output
    ```bash
    MultiChain 1.0.5 Daemon (latest protocol 10011)

    Starting up node...

    Looking for genesis block...
    Genesis block found

    Other nodes can connect to this node using:
    multichaind chain1@192.168.1.100:6725

    Listening for API requests on port 6724 (local only - see rpcallowip setting)

    Node ready.
    ```    

#### Node 2 Connection with Node 1 on Server 2

- Run
    ```bash
    multichaind chain1@192.168.1.100:6725
    
    # aws node
    multichaind -datadir=/home/toran/node2 -port=10255 -rpcport=10254 mychain@34.254.186.152:6821 -daemon
    ```
    
- Output  
    ```bash
    MultiChain 1.0.5 Daemon (latest protocol 10011)

    Retrieving blockchain parameters from the seed node 192.168.1.100:6725 ...
    Blockchain successfully initialized.

    Please ask blockchain admin or user having activate permission to let you connect and/or transact:
    multichain-cli chain1 grant 1UcDevL9XAeEeHu5qtjBqcdXTsLfELW3nHt5YR connect
    multichain-cli chain1 grant 1UcDevL9XAeEeHu5qtjBqcdXTsLfELW3nHt5YR connect,send,receive
    ```

#### Back on Server 1
- Run  
    ```bash
    multichain-cli chain1 grant 1UcDevL9XAeEeHu5qtjBqcdXTsLfELW3nHt5YR connect
    ```    
    
#### Back on Server 2
- Run  
    ```bash
    #Now try reconnecting again
    multichaind chain1 -daemon
    ```    


#### Delete  a Chain
```bash
#Stop it running
multichain-cli chain1 stop

#Delete its directory
sudo rm -r ~/.multichain/chain1
```


### [Nodes On Same Server](https://www.multichain.com/qa/563/multiple-nodes-server-connecting-chain-using-different-users)

#### Node 1 Initial Setup

- Run
    ```bash
    mkdir /home/toran/node1
    multichain-util create chain1 -datadir=/home/toran/node1
    ```

- Output
    ```bash
    MultiChain 1.0.5 Utilities (latest protocol 10011)

    Blockchain parameter set was successfully generated.
    You can edit it in /home/toran/node1/chain1/params.dat before running multichaind for the first time.

    To generate blockchain please run "multichaind chain1 -daemon".
    ```

- Run  
    ```bash
    multichaind chain1 -daemon -datadir=/home/toran/node1
    ```

- Output
    ```bash
    MultiChain 1.0.5 Daemon (latest protocol 10011)

    Starting up node...

    Looking for genesis block...
    Genesis block found

    Other nodes can connect to this node using:
    multichaind chain1@192.168.1.100:6725

    Listening for API requests on port 6724 (local only - see rpcallowip setting)

    Node ready.
    ```

#### Node 2 Connection with Node 1
Syntax: `multichaind -datadir=<your_path_to_multichain2nd_directory> -port=10255 -rpcport=10254 chain0 -daemon`

- Run  
    ```bash
    mkdir /home/toran/node2
    multichaind chain1@<chain1-ip>:<chain1-port> -datadir=/home/toran/node2
    ```

- Output  
    ```bash
    MultiChain 1.0.5 Daemon (latest protocol 10011)

    Retrieving blockchain parameters from the seed node 192.168.1.100:6725 ...
    Blockchain successfully initialized.

    Please ask blockchain admin or user having activate permission to let you connect and/or transact:
    multichain-cli chain1 grant 1UcDevL9XAeEeHu5qtjBqcdXTsLfELW3nHt5YR connect
    multichain-cli chain1 grant 1UcDevL9XAeEeHu5qtjBqcdXTsLfELW3nHt5YR connect,send,receive
    ```

- Run  
    ```bash
    multichain-cli chain1 -datadir=/home/toran/node1 grant 1UcDevL9XAeEeHu5qtjBqcdXTsLfELW3nHt5YR connect
    ```
    
    
Commands in Interactive Mode

sudo mkdir ~/.multichain/chain1      

multichain-cli chain1 -datadir=/home/toran/node1   

multichaind -datadir=/home/toran/node2 -port=10255 -rpcport=10254 mychain@34.254.186.152:6821 -daemon


multichain-cli mychain -datadir=/home/toran/node2


---------------------------------------------
- allow port range in aws instance, like 1000-9999 in all multichain nodes aws instace
- while running the node chain@ip:port, this port is used in cli
- while API port is used in python/code


--------------------------------------
multichain-cli -datadir=/home/ubuntu/toran-aws block-chain create stream "scheme" true


- connect
    `multichaind -datadir=/home/ubuntu/vin-aws-new block-chain@13.232.100.99:2657`
    
    
-------------------------------
IP:
vin-new: 34.255.8.211
tom: 13.232.130.184
my: 13.232.100.99
