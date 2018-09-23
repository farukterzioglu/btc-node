docker build --rm -t btcd-in-docker:simnet .  
docker run -p 18555:18555 -it -v /root/btcd/:/root/btcd/ --name btcd-simnet btcd-in-docker:simnet --externalip 0.0.0.0  
docker run -p 18555:18555 -p 18556:18556 -v /root/btcd/:/root/btcd/ -i -t --entrypoint /bin/bash 93fe8c283791