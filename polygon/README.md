![alt text](https://uploads-ssl.webflow.com/5f9a1900790900e2b7f25ba1/611f9d12419f2e2b75f158fb_polygon-logo.svg)

# About
These scripts will install an archival Polygon node. 

## Edit version variables (your choice)
```bash
# erigon
erigon=v2.35.x
#go
gover=1.19.x
#heimdall
heimdall=v0.3.x
```


## Install Heimdall ***first*** & sync
```
cd polygon

chmod +x heimdall.sh

./heimdall.sh
```
## Check sync status
```
curl http://localhost:26657/status
```
```bash
"network": should be "heimdall-137" and "catching_up": false
```

## Install Erigon
```
cd polygon

chmod +x erigon-polygon.sh

./erigon-polygon
```

## Check Logs
```bash
# Erigon
sudo journalctl -fu erigon
```
```bash
# Heimdall
sudo journalctl -fu heimdalld
sudo journalctl -fu heimdallr
```

## Snapshots 
https://snapshot.polygon.technology/

## Stop Erigon
```
sudo systemctl stop erigon
```
## Cleanup Data
```
sudo rm -r /var/lib/erigon/*
```

## Download with Aria2
```
aria2c --file-allocation=none -c -x 10 -s 10 https://matic-blockchain-snapshots.s3-accelerate.amazonaws.com/matic-mainnet/erigon-archive-snapshot-2023-01-12.tar.gz
```

## Decompress with Pigz
```
cd /var/lib/erigon

pigz -dc mysql-binary-backup.tar.gz | pv | tar xf -
```