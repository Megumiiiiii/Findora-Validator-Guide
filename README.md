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


# Setup the fn CLI Tool
`fn`: Findora Node Setup (fn) is a command-line (CLI) utility that allows you to set up a validator node and stake/unstake FRA.

- [Linux](https://wiki.findora.org/bin/linux/fn)
- [MacOs](https://wiki.findora.org/bin/macos/fn)

Download file and move to your path:
```
wget https://wiki.findora.org/bin/linux/fn

chmod +x fn

mv fn /usr/local/bin/
```

# Generate new Key
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
