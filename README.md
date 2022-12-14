<h1 align="center">EmpowerChain</h1>

![192093493-67779857-653e-4018-8c78-49530690f7a0](https://user-images.githubusercontent.com/113949717/193150573-97680cf9-4bd2-43b5-9aed-cb56f294da92.png)
**Prepare testnet altruistic-1**

*We will install and update the necessary packages*
```
sudo apt update && sudo apt upgrade -y && \
sudo apt install curl tar wget clang pkg-config libssl-dev jq build-essential bsdmainutils git make ncdu gcc git jq chrony liblz4-tool -y
```
*Installing Go 1.18.3*
```
cd $HOME && version="1.18.3" && \
wget "https://golang.org/dl/go$version.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$version.linux-amd64.tar.gz" && \
rm "go$version.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && \
source $HOME/.bash_profile && \
go version
```
*Install binary empowerd*
```
cd $HOME && git clone https://github.com/empowerchain/empowerchain && \
cd empowerchain/chain && \
make install && \
empowerd version --long | head
```
*Enter your node name in the moniker section ( < > ) remove it as well*
```
empowerd init <MONIKER> --chain-id altruistic-1 && \
empowerd config chain-id altruistic-1
```
*Replace wallet name with your wallet name and remove ( < > ) as well*
```
empowerd keys add <WALLET_NAME>
```
*Create a genesis account, enter your wallet name in <walletname> and remove ( < > ) as well*
  
*:warning:Save the secret words of your wallet:warning:*
```
empowerd add-genesis-account <WALLET_NAME> 1000000umpwr
  ```
*Create gentx*
  
*Enter your own information in the sections where I entered my information*
  ```
 empowerd gentx <WALLET_NAME> 1000000umpwr \
--chain-id=altruistic-1 \
--moniker="<MONIKER>" \
--commission-max-change-rate 0.1 \
--commission-max-rate 0.2 \
--commission-rate 0.05 \
--pubkey $(empowerd tendermint show-validator) \
--website="" \
--security-contact="" \
--identity="" \
--details=""
  ```

