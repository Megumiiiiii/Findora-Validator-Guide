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
```
sudo apt update -y && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt install docker-ce
```
Or go there
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
wget https://github.com/FindoraNetwork/findora-wiki-docs/raw/main/.gitbook/assets/fn
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
```
Then save your keys there
```
cp tmp.gen.keypair /data/findora/mainnet/mainnet_node.key
```
See your `mainnet_node.key` that is your keys
```
cat /data/findora/mainnet/mainnet_node.key
```

Your `mainnet_node.key` should be like this
<p align="left"><img height="100" height="auto" src="https://user-images.githubusercontent.com/98658943/194928553-6d50f5d4-7eb2-43ef-a6c1-78e2b3478d2e.png"</p>

> Don't forget to backup your keys, you will need this to restore your wallet. And also **don't share your mnemonic pharse / `sec_key` with anyone**

After it's all ready, you can continue to the next step

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

### Update
For the update scripts refer to this [link](https://wiki.findora.org/docs/validators/update-version#update-image-version)

If there is an update, it will definitely be announced on discord so don't forget to join

### Safety Clean
This is a magic script that can be used in case of errors after installation

[Safety Clean](https://wiki.findora.org/docs/validators/update-version/#auto-safety-clean)


#### Useful command

- Check Logs:
```
docker logs -f findorad
```
- Check Local Node Status:
```
curl 'http://localhost:26657/status'
```
```
curl 'http://localhost:8669/version'
```
```
curl 'http://localhost:8668/version'
```
Only if you set the 'ENABLE_LEDGER_SERVICE'
```
curl 'http://localhost:8667/version'
```
Only if you set the 'ENABLE_QUERY_SERVICE'



<strong><p style="font-size=16px"> You have successfully installed node</p></strong>

Next steps is how to fund your validator and stake FRA


# Staking Guide

### Minimum self-stake and where you can buy FRA
Validators must stake a minimum of 10,000 FRA to register as a validator. Before you can stake FRA to your validator, you must transfer FRA from existing wallet to your Validator Wallet.

You can get your Validator's wallet Address by using this command
```
fn show
```

If you don't have FRA,
You can buy from any exchange listed on [CEX Lists](https://coinmarketcap.com/currencies/findora/markets/)

> Kucoin only support Findora EVM(0x.....) for withdrawing, you need to transfer from EVM to Findora Wallet(fra....) before you can stake it.
>> To transfer your FRA from EVM to Findora Wallet, use Prism Feature. See this [Guide](https://wiki.findora.org/docs/dapp/wallet/)
>>> **Note**: Don't use Prism to withdraw or deposit from CEX or you will lost your FRA, because CEX doesn't support internal transaction 


## Node Operations
### fn CLI tool
Besides node setup, the fn tool is also used for general validator staking operations such as staking FRA into the validator, setting the commission rate the validator charges, transferring FRA balance on the validator to another wallet address and claiming FRA rewards.

To see the list of all sub-commands under `fn` use the `--help` flag as shown below:
```
fn --help
```
Output:
```
FindoraNetwork
A command line tool of the Findora Network
USAGE:
    fn [SUBCOMMAND]
FLAGS:
    -h, --help       Prints help information
    -v, --version
SUBCOMMANDS:
    account              Return user contract account information
    asset                manipulate custom asset
    claim                Claim accumulated FRA rewards
    contract-deposit     Transfer FRA from a Findora account to the specified Ethereum address
    contract-withdraw    Transfer FRA from an Ethereum address to the specified Findora account
    delegate             Delegating operations
    dev                  Manage development clusters on your localhost
    gen-eth-key          Generate an Ethereum address
    genkey               Generate a random Findora public key/private key
Pair
    help                 Prints this message or the help of the given subcommand(s)
    replace_staker       Replace the staker of the validator with target address
    setup                Setup environment variables for staking transactions
    show                 View Validator status and accumulated rewards
    stake                Stake tokens (i.e. bond tokens) from a Findora account to a Validator
    staker-update        Update information of a validator
    transfer             Transfer tokens from one address to another
    transfer-batch       Transfer tokens from one address to many others
    undelegate           Undelegating operations
    unstake              Unstake tokens (i.e. unbond tokens) from a Validator
    wallet               manipulates a findora wallet   stake FRAs to a custom validator
```
It's all of lists sub-command that can you use

And to get detailed info about a specific sub-command, use the `--help` flag along with the command.

Example:
```
fn staker-update --help
```
Output:
```
fn-staker-update
Update information of a validator
USAGE:
    fn staker-update [OPTIONS]
FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information
OPTIONS:
    -R, --commission-rate <Rate>              the commission rate of your
node, a float number from 0.0 to 1.0, optional
    -M, --validator-memo <Memo>               the description of your node, optional
        --validator-memo-desc <Desc>
        --validator-memo-logo <Logo>
        --validator-memo-name <Name>
        --validator-memo-website <Website>
```
### Stake Initial FRA and Set Commission Rate
After receiving FRA to your Validator's wallet, you must stake a minimum of 10,000 FRA to become a validator (make sure you have more than 10,000 FRA in your Validator's wallet for fees). Only the top 100 validators (with the most FRA staked) will earn FRA rewards.

> **Note**: Before staking, wait for 100% data synchronization of your validator node, otherwise you may be charged a 'validator node offline' penatly fee.
>> Use command below to check synchronization status
```
curl 'http://localhost:26657/status'
```
If `"catching_up=true"` it means it's not sync yet, wait till `"catching_up=false"`


Then create a file called `staker_memo` while waiting for your node to sync
```
nano staker_memo
```
Submit all details you want

Example:
```
{
  "name": "Findora",
  "desc": " This is just example  ",
  "website": "https://www.findora.org",
  "logo": "https://example-logo.png"
}
```
Save `CTRL+X` `Y` `Enter`

After your node sync, you can start to stake FRA to your validator using command below
```
fn stake -n $((10000 * 1000000)) -R 0.05 -M "$(cat staker_memo)"
```
> With the command above, that means you stake 10,000FRA and set your validator commission rate to 5% . Also make sure to run that command in the same directory where you created the `staker_memo`
>> You can update your commission rate and memo using `fn staker-update` like this
```
fn staker-update -R 0.1 -M "$(cat staker_memo)
```
### Stake Additional FRA
Use this command to stake more FRA, let say you want to stake 3,000 FRA
```
fn stake -a -n $((3000 * 1000000))
```

#### View Node Information
To find information about your validator node, use this
```
fn show
```
#### Claim Rewards
If your validator is a top 100 validator, it will earn rewards which will show up like this `"rewards":100,` in section on `fn show` . To claim
```
fn claim -n $((10 * 1000000))
```
#### Unstake Some FRA
Use it to unstake some FRA, but keep on mind, there will be `unbound_period` which means your FRA can be used for transaction after 113400 blocks after unstake 
```
fn unstake -n $((10 * 1000000))
```
#### Close Validator and unstake all of your FRA
```
fn unstake
```
> **Note**:This command will unstake all of your FRA and remove your node from the Findora Network.
