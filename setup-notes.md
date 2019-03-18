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
$ sudo touch ./btcd-sim.conf
$ cat >> ./btcd-sim.conf <<EOL
rpcuser=myuser
rpcpass=SomeDecentp4ssw0rd
rpclimituser=mylimituser
rpclimitpass=Limitedp4ssw0rd
simnet=1
datadir=./btcd/data
rpccert=./btcd/rpc.cert
rpckey=./btcd/rpc.key
EOL
```

### Create btcwallet config
```bash
$ sudo touch ./btcwallet-sim.conf
$ cat >> ./btcwallet-sim.conf <<EOL
simnet=1
appdata=./btcwallet/data
logdir=./btcwallet/data
rpcconnect=localhost:18556
username=myuser
password=SomeDecentp4ssw0rd
btcdusername=myuser
btcdpassword=SomeDecentp4ssw0rd
rpccert=./btcd/rpc.cert
rpckey=./btcd/rpc.key
EOL
```

### Create btcctl config
```bash
$ sudo touch ./btcctl-sim.conf
$ cat >> ./btcctl-sim.conf <<EOL
rpcuser=myuser
rpcpass=SomeDecentp4ssw0rd
simnet=1
rpccert=./btcd/rpc.cert
rpckey=./btcd/rpc.key
EOL
```

### Start BTCD
```bash
$ btcd -C ./btcd-sim.conf
//Leave it open&running
```

### Start Btc Wallet
```bash
btcwallet -C ./btcwallet-sim.conf --create
// Save the seed  
btcwallet -C ./btcwallet-sim.conf
// Leave it open&running
```

From another terminal  
```bash
// Open wallet session
$ btcctl -C ./btcctl-sim.conf --wallet walletpassphrase "[WALLET-PASSWORD]" 6000
// Create a new address (and save it)
$ btcctl -C ./btcctl-sim.conf --wallet getnewaddress
```

BTCD with mining
Stop btcd and start with new address  
```bash
btcd -C ./btcd-sim.conf --miningaddr=SbV6wEdURVhXtGk46UTvKYvzXVfM41u7i5
```

```bash
btcctl -C ./btcctl-sim.conf generate 100
```
