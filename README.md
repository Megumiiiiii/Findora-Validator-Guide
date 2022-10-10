<p align="center"><img height="120" height="auto" src="https://findora.org/wp-content/uploads/2022/06/Logo_Purple-1.png"</p>
  
# Findora Validator Setup

Official Documentation:

>- [Validator setup instructions](https://wiki.findora.org/docs/validators/validators-get-started/)
>- [Official Website](https://www.findora.org/)
>- [Official Telegram](https://t.me/findoraen)
>- [Official Discord](https://discord.gg/findora)
>- [Official Twitter](https://twitter.com/findora)

Explorer 

>- [Findora Explorer](https://findorascan.io/)

### System Requirements
- Minimum: 8GB RAM, 2 Core CPU (2.90GHz per core), 100GB Hard Disk
- Recommended: 16GB RAM, 4 Core CPU (2.90Ghz per core), 300GB Hard Disk


### Setup the fn CLI Tool
`fn`: Findora Node Setup (fn) is a command-line (CLI) utility that allows you to set up a validator node and stake/unstake FRA.

- [Linux](https://wiki.findora.org/bin/linux/fn)
- [MacOs](https://wiki.findora.org/bin/macos/fn)

Download file and move to your path:
```
wget https://wiki.findora.org/bin/linux/fn

chmod +x fn

mv fn /usr/local/bin/
```

### Generate new Key
Generate a new random pair of public and private keys that will be used for FRA staking:
```
fn genkey > tmp.gen.keypair
```
View your keys `cat tmp.gen.keypair` and save it to `/data/findora/mainnet/mainnet_node.key`

<b>Note</b>: *If the directory does not exist, you will need to create it first*
```
sudo mkdir -p /data/findora/mainnet
cd /data/findora/mainnet
nano mainnet_node.key
```
Fill with `temp.gen.keypair` 's content.
Then save it `CTRL+X` `Y` `Enter`


Your `mainnet_node.key` should be like this
<p align="left"><img height="100" height="auto" src="https://user-images.githubusercontent.com/98658943/194928553-6d50f5d4-7eb2-43ef-a6c1-78e2b3478d2e.png"</p>

After it's all ready, we can continue to the next step.

### Download & Run the scripts
	
Back to your $HOME if you still in `~/data/findora/mainnet/` then download

To download:
```
wget https://wiki.findora.org/assets/files/node_init_mainnet-423a36f2adaaeab9de7ff63e61d3d4c1.sh
```
After finished downloading, run the script:
```
bash -x node_init_mainnet-423a36f2adaaeab9de7ff63e61d3d4c1.sh
```
