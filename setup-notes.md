### Install Go
http://golang.org/doc/install

### Check Go
```bash
$ go version
$ go env GOROOT GOPATH
```

### Install btcd
```bash
$ git clone https://github.com/btcsuite/btcd $GOPATH/src/github.com/btcsuite/btcd
$ cd $GOPATH/src/github.com/btcsuite/btcd
$ GO111MODULE=on go install -v . ./cmd/...

$ export BTCFILES=/media/farukterzioglu/files/btc
$ cd $BTCFILES
```

### Install btcwallet
```
git clone https://github.com/btcsuite/btcwallet  $GOPATH/src/github.com/btcsuite/btcwallet 
$ cd $GOPATH/src/github.com/btcsuite/btcwallet 
$ GO111MODULE=on go install -v . ./cmd/...
```


### Create btcd config
```bash
$ mkdir  ~/.btcd
$ touch ~/.btcd/btcd.conf 
$ nano ~/.btcd/btcd.conf

// Paste below
rpcuser=myuser
rpcpass=SomeDecentp4ssw0rd
rpclimituser=mylimituser
rpclimitpass=Limitedp4ssw0rd
simnet=1
```

### Create btcwallet config
```bash
$ mkdir ~/.btcwallet
$ touch ~/.btcwallet/btcwallet.conf
$ nano ~/.btcwallet/btcwallet.conf 

//Paste below
simnet=1
username=myuser
password=SomeDecentp4ssw0rd
btcdusername=myuser
btcdpassword=SomeDecentp4ssw0rd
```

### Create btcctl config
```bash
$ mkdir ~/.btcctl
$ sudo touch ~/.btcctl/btcctl.conf
$ nano ~/.btcctl/btcctl.conf

rpcuser=myuser
rpcpass=SomeDecentp4ssw0rd
simnet=1
```

### Start BTCD
```bash
$ btcd
//Leave it open&running
```

### Start Btc Wallet
```bash
btcwallet --create
// Save the seed & password  
btcwallet
// Leave it open&running
```

From another terminal  
```bash
// Open wallet session
$ btcctl --wallet walletpassphrase "[WALLET-PASSWORD]" 6000
// Create a new address (and save it)
$ btcctl --wallet getnewaddress
//Save the address [NEW_ADDRESS]
```

BTCD with mining  
Stop btcd and start with new address  
```bash
btcd --miningaddr=[NEW_ADDRESS]
```

```bash
$ btcctl generate 100
$ btcctl --wallet getbalance
$ btcctl --wallet createnewaccount account1
$ btcctl --wallet getnewaddress account1 //save the address -> [RECIPIENT]
$ btcctl --wallet sendtoaddress "[RECIPIENT]" 21
$ btcctl --wallet generate 1 //save the block id -> [BLOCK_ID]
$ btcctl --wallet getbalance
$ btcctl --wallet getblock [BLOCK_ID] // save tx ids -> [TX_ID_1, TX_ID_2]
$ btcctl --wallet gettransaction TX_ID_1
$ btcctl --wallet gettransaction TX_ID_2
```
