FROM golang:1.10.4

MAINTAINER Olaoluwa Osuntokun <laolu32@gmail.com>

# Grab and install the latest version of btcd and it's dependencies.
RUN go get github.com/btcsuite/btcd/...

# wallet, p2p, and rpc
EXPOSE 8332 8333 8334

# testnet wallet, p2p, and rpc
EXPOSE 18332 18333 18334

# simnet wallet, p2p, and rpc
EXPOSE 18555 18556 

RUN mkdir /root/.btcd && mkdir /root/.btcctl

ADD btcd.conf /root/

WORKDIR /root

ENTRYPOINT ["btcd", "-C", "btcd.conf"]
