# 0gchain Testnet Guide
```will always update```
<p align="center">
  <img src="https://github.com/hubofvalley/Testnet-Guides/assets/100946299/fe21ef6a-0979-4ac1-8d92-6d1bcf76c7cc" alt="let’s build 0G together" width="600" height="300">
</p>

<p align="center">
  <img src="https://github.com/hubofvalley/Testnet-Guides/assets/100946299/b1a15f39-8e6a-428f-846b-4c430eac872b" width="400" height="200">
</p>


## 0gchain <a href="https://0g.ai/"><img src="https://github.com/hubofvalley/Testnet-Guides/assets/100946299/916ed2ba-bf46-48ea-b4f9-6d48c1eac3ed" width="50" height="50">


- **WHAT IS 0gchain?** 
ZeroGravity (0G) is the first infinitely scalable, decentralized data availability layer featuring a built-in general-purpose storage system. This enables 0G to offer a highly scalable on-chain database suitable for various Web2 and Web3 data needs, including on-chain AI. Additionally, as a data availability layer, 0G ensures seamless verification of accurate data storage.

In the sections below, we will delve deeper into this architecture and explore the key use cases it unlocks.

- **0G’s Architecture**
0G achieves high scalability by dividing the data availability workflow into two main lanes:

  1. **Data Storage Lane**: This lane achieves horizontal scalability through data partitioning, allowing for rapid storage and access of large amounts of data.

  2. **Data Publishing Lane**: This lane ensures data availability using a quorum-based system with an "honest majority" assumption, where the quorum is randomly selected via a Verifiable Random Function (VRF). This method avoids data broadcasting bottlenecks and supports larger data transfers in the Storage Lane.

0G Storage is an on-chain database made up of Storage Nodes that participate in a Proof of Random Access (PoRA) mining process. Nodes are rewarded for correctly responding to random data queries, promoting network participation and scalability.

0G DA (Data Availability) Layer is built on 0G Storage and uses a quorum-based architecture for data availability confirmation. The system relies on an honest majority of nodes, with quorum selection randomized by VRF and GPUs enhancing the erasure coding process for data storage.

- **0G solving target**
The increasing need for greater Layer 2 (L2) scalability has coincided with the rise of Data Availability Layers (DALs), which are essential for addressing Ethereum's scaling challenges. L2s handle transactions off-chain and settle on Ethereum for security, requiring transaction data to be posted somewhere for validation. By publishing data directly on Ethereum, high fees are distributed among L2 users, enhancing scalability.

DALs offer a more efficient method for publishing and maintaining off-chain data for inspection. However, existing DALs struggle to manage the growing volume of on-chain data, especially for data-intensive applications like on-chain AI, due to limited storage capacity and throughput.

0G offers a solution with a 1,000x performance improvement over Ethereum's danksharding and a 4x improvement over Solana's Firedancer, providing the infrastructure needed for massive Web3 data scalability. Key applications of 0G include:

1. **AI**: 0G Storage can handle large datasets, and 0G DA enables the rapid deployment of AI models on-chain.
2. **L1s / L2s**: These networks can use 0G for data availability and storage, with partners like Polygon, Arbitrum, Fuel, and Manta Network.
3. **Bridges**: Networks can store their state using 0G, facilitating secure cross-chain transfers by storing and communicating user balances.
4. **Rollups-as-a-Service (RaaS)**: 0G provides DA and storage infrastructure for RaaS providers like Caldera and AltLayer.
5. **DeFi**: 0G's scalable DA supports efficient DeFi on specific L2s and L3s, enabling fast settlement and high-frequency trading.
6. **On-chain Gaming**: Gaming requires reliable storage of cryptographic proofs and metadata, such as player assets and actions.
7. **Data Markets**: Web3 data markets can store their data on-chain, feasible on a large scale with 0G.

0G is a scalable, low-cost, and programmable DA solution essential for bringing vast amounts of data on-chain. Its role as an on-chain data storage solution unlocks numerous use cases, providing the database infrastructure for any on-chain application. 0G efficiently stores and proves the availability of any Web2 or Web3 data, extending benefits beyond confirming L2 transactions.

For more detailed information, visit the [0G DA documentation](https://docs.0g.ai/0g-doc/docs/0g-da)

With Public Testnet, 0gchain’s docs and code become public. Check them out below!
    - [0gchainWebsite](https://0g.ai/)
    - [0gchainX](https://x.com/0G_labs)
    - [0gchainDiscord](https://discord.com/invite/0glabs)
    - [0gchainDocs](https://docs.0g.ai/0g-doc)
    - [0gchainGithub](https://github.com/0glabs)
    - [0gchainExplorer](https://testnet.0g.explorers.guru)
    
Grand Valley's 0G public endpoints:
- rpc : not available
- json-rpc : not available

## 0gchain Node Deployment Guide
guide's current binaries version: ``v0.2.3``
current chain : ``zgtendermint_16600-2``

### 1. Install dependencies for building from source
   ```bash
    sudo apt update && \
    sudo apt install curl git jq build-essential gcc unzip wget lz4 openssl -y
   ```

### 2. install go
   ```bash
  cd $HOME && \
  ver="1.22.0" && \
  wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
  sudo rm -rf /usr/local/go && \
  sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
  rm "go$ver.linux-amd64.tar.gz" && \
  echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile && \
  source ~/.bash_profile && \
  go version
   ```

### 3. set vars
  EDIT YOUR MONIKER
   ```
  echo "export WALLET="wallet"" >> $HOME/.bash_profile
  echo "export MONIKER="<your-moniker>"" >> $HOME/.bash_profile
  echo "export OG_CHAIN_ID="zgtendermint_16600-2"" >> $HOME/.bash_profile
  echo "export OG_PORT="26"" >> $HOME/.bash_profile
  source $HOME/.bash_profile
   ```

### 4. download binary
   ```bash
   git clone -b v0.2.3 https://github.com/0glabs/0g-chain.git
   cd 0g-chain
   make install
   0gchaind version
   ```

### 5. config and init app
   ```bash
   cd $HOME
   0gchaind init $MONIKER --chain-id $OG_CHAIN_ID
   0gchaind config chain-id $OG_CHAIN_ID
   0gchaind config node tcp://localhost:${OG_PORT}657
   0gchaind config keyring-backend os
   ```

### 6. download genesis.json
   ```bash
   wget https://github.com/0glabs/0g-chain/releases/download/v0.2.3/genesis.json -O $HOME/.0gchain/config/genesis.json
   ```

### 7. Add seeds to the config.toml
   ```bash
SEEDS="81987895a11f6689ada254c6b57932ab7ed909b6@54.241.167.190:26656,010fb4de28667725a4fef26cdc7f9452cc34b16d@54.176.175.48:26656,e9b4bc203197b62cc7e6a80a64742e752f4210d5@54.193.250.204:26656,68b9145889e7576b652ca68d985826abd46ad660@18.166.164.232:26656" && \
   sed -i.bak -e "s/^seeds *=.*/seeds = \"${SEEDS}\"/" $HOME/.0gchain/config/config.toml
   ```

### 8. Add peers to the config.toml (i recommend using seeds only, but it's up to you whether to add peers) (currently no peers)
   ```bash
peers=""
sed -i -e "s|^persistent_peers *=.*|persistent_peers = \"$peers\"|" $HOME/.0gchain/config/config.toml
   ```

### 9. set custom ports in config.toml file
   ```bash
   sed -i.bak -e "s%:26658%:${OG_PORT}658%g;
   s%:26657%:${OG_PORT}657%g;
   s%:6060%:${OG_PORT}060%g;
   s%:26656%:${OG_PORT}656%g;
   s%^external_address = \"\"%external_address = \"$(wget -qO- eth0.me):${OG_PORT}656\"%;
   s%:26660%:${OG_PORT}660%g" $HOME/.0gchain/config/config.toml
   ```

### 10. config pruning to save storage (optional) (if u want to run a full node, skip this task)
   ```bash
   sed -i \
      -e "s/^pruning *=.*/pruning = \"custom\"/" \
      -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"100\"/" \
      -e "s/^pruning-interval *=.*/pruning-interval = \"10\"/" \
      "$HOME/.0gchain/config/app.toml"
   ```

### 11. open json-rpc endpoints (required for running the storage node and storage kv)
   ```bash
   sed -i \
    -e 's/address = "127.0.0.1:8545"/address = "0.0.0.0:8545"/' \
    -e 's|^api = ".*"|api = "eth,txpool,personal,net,debug,web3"|' \
    $HOME/.0gchain/config/app.toml
   ```

### 12. set minimum gas price and enable prometheus
   ```bash
   sed -i "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0ua0gi\"/" $HOME/.0gchain/config/app.toml
   sed -i -e "s/prometheus = false/prometheus = true/" $HOME/.0gchain/config/config.toml
   ```

### 13. disable indexer (optional) (if u want to run a full node, skip this task)
   ```bash
   sed -i -e "s/^indexer *=.*/indexer = \"null\"/" $HOME/.0gchain/config/config.toml
   ```

### 14. create service file
   ```bash
   sudo tee /etc/systemd/system/0gchaind.service > /dev/null <<EOF
   [Unit]
   Description=0G Node
   After=network.target

   [Service]
   User=$USER
   Type=simple
   ExecStart=$(which 0gchaind) start --home $HOME/.0gchain
   Restart=on-failure
   LimitNOFILE=65535

   [Install]
   WantedBy=multi-user.target
   EOF
   ```

### 15. start the node
   ```bash
   sudo systemctl daemon-reload && \
   sudo systemctl enable 0gchaind && \
   sudo systemctl restart 0gchaind && sudo journalctl -u 0gchaind -fn 100 -o cat
   ```

#   Keys commands
## 1. create wallet
  ```bash
  0gchaind keys add $WALLET --eth
  ```
  ![SAVE YOUR SEEDS PHRASE!](https://img.shields.io/badge/SAVE%20YOUR%20SEEDS%20PHRASE!-red)
   
   query the 0x address
  ```bash
  echo "0x$(0gchaind debug addr $(0gchaind keys show $WALLET -a) | grep hex | awk '{print $3}')"
  ```
  THEN U MUST REQUEST THE TEST TOKEN FROM THE [FAUCET](https://faucet.0g.ai/) BY ENTERING YOUR 0X ADDRESS

  OR YOU CAN IMPORT YOUR EXISTING WALLET
  ```bash
  0gchaind keys add $WALLET --recover --keyring-backend os --eth
  ```

## 2. check node synchronization
  ```bash
  0gchaind status | jq .sync_info
  ```
  make sure your node block height has been synced with the latest block height. or you can check the ```catching_up``` value must be ```false```

## 3. check your balance
  ```bash
  0gchaind q bank balances $(0gchaind keys show $WALLET -a)
  ```

## 4. create validator
  EDIT YOUR IDENTITY, WEBSITE URL, YOUR MAIL AND YOUR DETAILS. BUT THOSE ARE OPTIONAL
  ```bash
  0gchaind tx staking create-validator \
  --amount=1000000ua0gi \
  --pubkey=$(0gchaind tendermint show-validator) \
  --moniker=$MONIKER \
  --chain-id=$OG_CHAIN_ID \
  --commission-rate=0.10 \
  --commission-max-rate=0.20 \
  --commission-max-change-rate=0.01 \
  --min-self-delegation=1 \
  --from=$WALLET \
  --identity=<your-identity> \
  --website=<your-website-url> \
  --security-contact=<your-mail> \
  --details="let's buidl 0g together" \
  --gas=auto --gas-adjustment=1.4 \
  -y
  ```
  ```1uaogi = (10)^(-6)AOGI = 0.000001AOGI```

## 5. BACKUP YOUR VALIDATOR <img src="https://img.shields.io/badge/IMPORTANT-red" alt="Important" width="100">
  ```bash
  nano /$HOME/.0gchain/config/priv_validator_key.json
  ```
  ```bash
  nano /$HOME/.0gchain/data/priv_validator_state.json
  ```
  copy all of the contents of the ![priv_validator_key.json](https://img.shields.io/badge/priv__validator__key.json-red) !and ![priv_validator_key.json](https://img.shields.io/badge/priv__validator__state.json-red) files and save them in a safe place. This is a vital step in case you need to migrate your validator node

## 6. delegate token to validator
  ### self delegate
  ```bash
  0gchaind tx staking delegate $(0gchaind keys show $WALLET --bech val -a) 1000000ua0gi --from $WALLET --chain-id zgtendermint_16600-1 --gas=auto --gas-adjustment=1.4 --fees=800ua0gi -y
  ```
  ### delegate to <a href="https://testnet.0g.explorers.guru/validator/0gvaloper1yzwlgyrgcg83u32fclz0sy2yhxsuzpvprrt5r4"><img src="https://github.com/hubofvalley/Testnet-Guides/assets/100946299/e8704cc4-2319-4a21-9138-0264e75e3a82" alt="GRAND VALLEY" width="50" height="50">
</a>
  
  ```bash
  0gchaind tx staking delegate 0gvaloper1yzwlgyrgcg83u32fclz0sy2yhxsuzpvprrt5r4 1000000ua0gi --from $WALLET --chain-id zgtendermint_16600-1 --gas=auto --gas-adjustment=1.4 --fees=800ua0gi -y
  ```

#  delete the node
  ```bash
  sudo systemctl stop 0gchaind
  sudo systemctl disable 0gchaind
  sudo rm -rf /etc/systemd/system/0gchaind.service
  sudo rm -r 0g-chain
  sudo rm -rf $HOME/.0gchain
  sed -i "/OG_/d" $HOME/.bash_profile
  ```

#  upgrade the node
  ```bash
  cd $HOME
  rm -rf $HOME/0g-chain
  git clone -b <0G node version> https://github.com/0glabs/0g-chain.git
  make install
  source .profile
  0gchaind version
  # Restart the node
  sudo systemctl restart 0gchaind && sudo journalctl -u 0gchaind -fn 100 -o cat
  ```
  please check the latest node version!
