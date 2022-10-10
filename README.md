<p align="center"><img height="120" height="auto" src="https://findora.org/wp-content/uploads/2022/06/Logo_Purple-1.png"</p>
  
# Mainnet Node Installation Guide

Official Documentation:

>- [Validator setup instructions](https://wiki.findora.org/docs/validators/validators-get-started/)
>- [Official Website](https://www.findora.org/)
>- [Official Telegram](https://t.me/findoraen)
>- [Official Discord](https://discord.gg/findora)
>- [Official Twitter](https://twitter.com/findora)

Explorer 

[Findora Explorer](https://findorascan.io/)

### System Requirements
- Minimum: 8GB RAM, 2 Core CPU (2.90GHz per core), 100GB Hard Disk
- Recommended: 16GB RAM, 4 Core CPU (2.90Ghz per core), 300GB Hard Disk
    - example
      - AWS T3 t3.2xlarge
      - AliCloud g6 g6.2xlarge
      - GCP n2 n2-standard-8
      - Contabo Cloud VPS M

### Install Docker
If you don't have docker in your system, install it first

[How to install docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04)

### Firewall
This is the commands to configure the needed ports on Ubuntu 20.04LTS using `ufw`:
```
sudo ufw allow 22 && sudo ufw allow 26657/tcp && sudo ufw allow 8545/tcp && sudo ufw allow 8667/tcp && sudo ufw allow 8668/tcp && sudo ufw allow 8669/tcp && sudo ufw enable
```
[Tutorial about ufw](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04)

### Setup the fn CLI Tool
`fn`: Findora Node Setup (fn) is a command-line (CLI) utility that allows you to set up a validator node and stake/unstake FRA.

- [Linux](https://wiki.findora.org/bin/linux/fn)
- [MacOs](https://wiki.findora.org/bin/macos/fn)

Download the file and move to your path
```
wget https://wiki.findora.org/bin/linux/fn

chmod +x fn

mv fn /usr/local/bin/
```

### Generate new Key
Generate a new random pair of public and private keys that will be used for FRA staking
```
fn genkey > tmp.gen.keypair
```
Before continue to the installation steps.
You will need to create a directory to save your keys. 
To do it, open new window then run these command
```
sudo mkdir -p /data/findora/mainnet
cd /data/findora/mainnet
nano mainnet_node.key
```
Back to first window and use this command to view your keys
```
cat tmp.gen.keypair
```
Copy all content from it and paste to second window.
Then save, this is how to save it `CTRL+X` `Y` `Enter`

Your `mainnet_node.key` should be like this
<p align="left"><img height="100" height="auto" src="https://user-images.githubusercontent.com/98658943/194928553-6d50f5d4-7eb2-43ef-a6c1-78e2b3478d2e.png"</p>

Close your second window

After it's all ready, you can continue to the next step.

### Download & Run the script
Running scripts can take a while, because this will downloading a lot of files and then extract them

Download Automated Script:
```
wget https://wiki.findora.org/assets/files/node_init_mainnet-423a36f2adaaeab9de7ff63e61d3d4c1.sh
```
After finished downloading, run the script:
```
bash -x node_init_mainnet-423a36f2adaaeab9de7ff63e61d3d4c1.sh
```

### Connect to Network

To connect fn with the Findora Network, use this command:
```
fn setup -S https://prod-mainnet.prod.findora.org
```
To connect your staking key to fn, use the below command. This allows fn to sign transactions on your behalf
```
fn setup -O /data/findora/mainnet/node.mnemonic
```
To connect your Node Key to fn, use the command below
```
fn setup -K /data/findora/mainnet/tendermint/config/priv_validator_key.json
```

### Backup
Backup the following files for later if you want to migrate servers
 
`/data/findora/mainnet/mainnet_node.key` & `/data/findora/mainnet/node.mnemonic`

And backup `config` folder from `/data/findora/mainnet/tendermint`

This is the guide how to Migrate Servers by [@EasyNode](https://twitter.com/EasyNode)

[How to Migrate](https://guides.easynode.one/findora/moving)


<strong><p style="font-size=14px">Useful command</p></strong>

- Check Logs:
```
docker logs -f findorad
```
- Check Local Node Status:
```
curl 'http://localhost:26657/status'
curl 'http://localhost:8669/version'
curl 'http://localhost:8668/version' # Only if you set the 'ENABLE_LEDGER_SERVICE'
curl 'http://localhost:8667/version' # Only if you set the 'ENABLE_QUERY_SERVICE'
```

<strong><p style="font-size=16px"> You have successfully installed node</p></strong>

Next steps is how to fund your validator and stake FRA

# Staking Guide
Validators must stake a minimum of 10,000 FRA to register as a validator. Before you can stake FRA to your validator, you must first transfer FRA to the Findora Address of your validator.

If you don't have FRA,
You can buy from any exchange listed on [this page](https://coinmarketcap.com/currencies/findora/markets/)

**Note**: Kucoin only support Findora EVM(0x.....) to withdrawing ,you need to transfer from EVM to Findora Wallet(fra....) first before you can stake it.

To transfer your FRA from EVM to Findora Wallet, use Prism Feature. See this [guide](https://wiki.findora.org/docs/dapp/wallet/)
