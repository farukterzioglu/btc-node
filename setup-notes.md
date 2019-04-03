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

```
$ btcctl --wallet listunspent
[
  {
    "txid": "93acd5ba96d321e36396951b16383b2e1a785fec37a0f40a611388ecca246182",
    "vout": 1,
    "address": "sb1qnr9n2d5r5vy2jq5s9hy6hz52p8u7742v5wvgzp",
    "account": "default",
    "scriptPubKey": "001498cb353683a308a902902dc9ab8a8a09f9ef554c",
    "amount": 28.99999776,
    "confirmations": 1,
    "spendable": true
  },
  {
    "txid": "93acd5ba96d321e36396951b16383b2e1a785fec37a0f40a611388ecca246182",
    "vout": 0,
    "address": "SPDwD28Dgf3ZH5g531sEnwWnKU6gVBWHmL",
    "account": "account1",
    "scriptPubKey": "76a914152b652a7e2fa603bc02015807636700472d748388ac",
    "amount": 21,
    "confirmations": 1,
    "spendable": true
  },
  {
    "txid": "f1f30ce106a0229226d4b359eef76131126898cf21c4f8d25b83cbf344288e6b",
    "vout": 0,
    "address": "SRtMoJ23DR5Y8duDjBV2do9ycUNyyRTdga",
    "account": "default",
    "scriptPubKey": "76a914325ffb13cf2fb0ff2a1f1d4cbca9bae15932f76288ac",
    "amount": 50,
    "confirmations": 100,
    "spendable": true
  }
]
```

```
$ btcctl --wallet sendtoaddress "SPDwD28Dgf3ZH5g531sEnwWnKU6gVBWHmL" 1
$ btcctl --wallet listunspent
[
  {
    "txid": "93acd5ba96d321e36396951b16383b2e1a785fec37a0f40a611388ecca246182",
    "vout": 1,
    "address": "sb1qnr9n2d5r5vy2jq5s9hy6hz52p8u7742v5wvgzp",
    "account": "default",
    "scriptPubKey": "001498cb353683a308a902902dc9ab8a8a09f9ef554c",
    "amount": 28.99999776,
    "confirmations": 1,
    "spendable": true
  },
  {
    "txid": "93acd5ba96d321e36396951b16383b2e1a785fec37a0f40a611388ecca246182",
    "vout": 0,
    "address": "SPDwD28Dgf3ZH5g531sEnwWnKU6gVBWHmL",
    "account": "account1",
    "scriptPubKey": "76a914152b652a7e2fa603bc02015807636700472d748388ac",
    "amount": 21,
    "confirmations": 1,
    "spendable": true
  }
]
```

```
$ btcctl --wallet generate 1
6860d2ee3a809e3ab4654fdb735fb695bbc8453bd067b98313a2e29d50c7a92c
$ btcctl --wallet getblock 6860d2ee3a809e3ab4654fdb735fb695bbc8453bd067b98313a2e29d50c7a92c
{
  "hash": "6860d2ee3a809e3ab4654fdb735fb695bbc8453bd067b98313a2e29d50c7a92c",
  "confirmations": 1,
  "strippedsize": 411,
  "size": 411,
  "weight": 1644,
  "height": 102,
  "version": 805306371,
  "versionHex": "30000003",
  "merkleroot": "dce7f2ec8f3f7fc14543232e3b472d075033f842dc087d350420aa484da1d7d5",
  "tx": [
    "450116e82d27b3a490df4b249c94ccc2d1f14551885c657010eb29585043679a",
    "84d1ad2793e087b035edca57f8b3a01f4260d10b7723bdf969684a784173eda6"
  ],
  "time": 1553101543,
  "nonce": 3,
  "bits": "207fffff",
  "difficulty": 1,
  "previousblockhash": "2913ec45abcb8a7bf779ddf1f2e60e4620682438a82ad126030491ab3c9e6adf"
}

// Check the tx below (84d1ad....) 1 for receipent, 48 is change. note the vout's
$ btcctl --wallet listunspent
[
  {
    "txid": "84d1ad2793e087b035edca57f8b3a01f4260d10b7723bdf969684a784173eda6",
    "vout": 1,
    "address": "SPDwD28Dgf3ZH5g531sEnwWnKU6gVBWHmL",
    "account": "account1",
    "scriptPubKey": "76a914152b652a7e2fa603bc02015807636700472d748388ac",
    "amount": 1,
    "confirmations": 1,
    "spendable": true
  },
  {
    "txid": "84d1ad2793e087b035edca57f8b3a01f4260d10b7723bdf969684a784173eda6",
    "vout": 0,
    "address": "sb1qcx0ftwkeadgnhavuucl9krpqxtyh63qu2khwvf",
    "account": "default",
    "scriptPubKey": "0014c19e95bad9eb513bf59ce63e5b0c2032c97d441c",
    "amount": 48.99999776,
    "confirmations": 1,
    "spendable": true
  },
  {
    "txid": "93acd5ba96d321e36396951b16383b2e1a785fec37a0f40a611388ecca246182",
    "vout": 0,
    "address": "SPDwD28Dgf3ZH5g531sEnwWnKU6gVBWHmL",
    "account": "account1",
    "scriptPubKey": "76a914152b652a7e2fa603bc02015807636700472d748388ac",
    "amount": 21,
    "confirmations": 2,
    "spendable": true
  },
  {
    "txid": "93acd5ba96d321e36396951b16383b2e1a785fec37a0f40a611388ecca246182",
    "vout": 1,
    "address": "sb1qnr9n2d5r5vy2jq5s9hy6hz52p8u7742v5wvgzp",
    "account": "default",
    "scriptPubKey": "001498cb353683a308a902902dc9ab8a8a09f9ef554c",
    "amount": 28.99999776,
    "confirmations": 2,
    "spendable": true
  },
  {
    "txid": "65a2b9453df52607c4845146d19a8159d52941a36f792e72fd420c83592f82fd",
    "vout": 0,
    "address": "SRtMoJ23DR5Y8duDjBV2do9ycUNyyRTdga",
    "account": "default",
    "scriptPubKey": "76a914325ffb13cf2fb0ff2a1f1d4cbca9bae15932f76288ac",
    "amount": 50,
    "confirmations": 100,
    "spendable": true
  }
]
```


// Check the first tx from that block. It is not mature (confirm : 1) so not listed in unspent txs
```
$ btcctl --wallet gettransaction 450116e82d27b3a490df4b249c94ccc2d1f14551885c657010eb29585043679a
{
  "amount": 50.00000224,
  "confirmations": 1,
  "blockhash": "6860d2ee3a809e3ab4654fdb735fb695bbc8453bd067b98313a2e29d50c7a92c",
  "blockindex": 0,
  "blocktime": 1553101543,
  "txid": "450116e82d27b3a490df4b249c94ccc2d1f14551885c657010eb29585043679a",
  "walletconflicts": [],
  "time": 1553101543,
  "timereceived": 1553101543,
  "details": [
    {
      "account": "default",
      "address": "SRtMoJ23DR5Y8duDjBV2do9ycUNyyRTdga",
      "amount": 50.00000224,
      "category": "immature",
      "vout": 0
    }
  ],
  "hex": "01000000010000000000000000000000000000000000000000000000000000000000000000ffffffff17016608ab83ffbcada19ffd0b2f503253482f627463642fffffffff01e0f2052a010000001976a914325ffb13cf2fb0ff2a1f1d4cbca9bae15932f76288ac00000000"
}
```

```
// Create new repository in Github -> [my_btcd]
cd $GOPATH/src/github.com/btcsuite/btcd
git remote rename origin upstream
git remote add origin [my_btcd]
git push -u origin master

// Implement these 
https://github.com/farukterzioglu/btcd-tutorial/commit/f3ed12356fd02e9dfe0785610807618461fbf5be

// Build btcd
GO111MODULE=on go install -v . ./cmd/...

btcctl --wallet transfertransaction [ADDRESS] [TX_ID]

```

```
// Create new repository in Github -> [my_btcwallet]
cd $GOPATH/src/github.com/btcsuite/btcwallet
git remote rename origin upstream
git remote add origin [my_btcd]
git push -u origin master

// Add to 'go.mod'
replace github.com/btcsuite/btcd => ../btcd

// Implement changes in here
https://github.com/farukterzioglu/btcwallet-tutorial/commits/transferTx
874e6a28ed164656f5c5bf7fd42c9a15bc54fca5 ->   

btcctl --wallet listunspent
btcctl --wallet transfertransaction SPDwD28Dgf3ZH5g531sEnwWnKU6gVBWHmL 65a2b9453df52607c4845146d19a8159d52941a36f792e72fd420c83592f82fd
btcctl --wallet gettransaction 00a04951adcfad95a825740312b232eb6b354160125772741d748845045c131c
```