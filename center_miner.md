
### 中心节点挖矿
### 安装
#### IPFS
```
git clone https://github.com/filepp/go-ipfs
cd go-ipfs
make build
cp cmd/ipfs /usr/local/bin
```
####Louts（略）
#### IPFC
```
git clone  https://git.filep.vip/ruitai/ipfc
cd ipfc
make
cp ipfc /usr/local/bin
```
### 运行
#### IPFS

初始化ipfs仓库
```
export IPFS_PATH=/path/to/ipfsrepo  //指定ipfs仓库目录
ipfs init
```

修改配置文件`/path/to/ipfsrepo/config`
```
  "Addresses": {
    "Swarm": [
      "/ip4/0.0.0.0/tcp/4001",
      "/ip6/::/tcp/4001",
      "/ip4/0.0.0.0/udp/4001/quic",
      "/ip6/::/udp/4001/quic"
    ],
    "Announce": [],
    "NoAnnounce": [],
    "API": "/ip4/127.0.0.1/tcp/5001",  // 这里改成 "/ip4/0.0.0.0/tcp/5001"
    "Gateway": "/ip4/127.0.0.1/tcp/8080"
  },

```

运行ipfs，需要指定矿工角色(miner-role=0代表中心节点)
```
ipfs daemon --enable-pubsub-experiment=true --enable-mining=true --miner-role=0
```

查看 peerID, 后续配置ipfc配置文件会用到。
```
ipfs id
```

####Louts（略）

#### IPFC

修改配置，配置文件同在这里获取 `https://github.com/filepp/ipfc/blob/master/conf/ipfc.yaml`， 主要修改一下几项
```
repo:
  dir: /data/ipfc_data  // 缓存数据目录

lotus:
  api_addr: /ip4/192.168.3.201/tcp/7846/http
  token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBbGxvdyI6WyJyZWFkIiwid3JpdGUiLCJzaWduIiwiYWRtaW4iXX0.5xj_v75Dgl9Mf0d8Tdz-D6YAI-2ImMq5pE9fuF6Gn4U

ipfs:
  peer_id: 12D3KooWP7We1ubNk7U7iQNUihZeDgtcVy8fRQPhVBQs6pjHawm4
  api_addr: /ip4/192.168.3.201/tcp/5001
  replicas: 3

eth:
  network: https://data-seed-prebsc-1-s1.binance.org:8545/
  contract_address: 0xFD3Bf3756AeC1C37d0dD2561369e9D4c94051027
  private_key: 080ebaab2013d69ac721ff891060f5fdb60cf1a2e353db77f3bca7e5e01de0ff  // 钱包私钥，该地址至少持有100万FC
```

运行ipfc，可通过环境变量设置配置文件路径，(ipfc和lotus必须运行同一台主机上，或者将IPFC的文件目录挂载到lotus主机上且路径一致)
```
export ENV_IPFC_CONFIG_PATH=conf/ipfc.yaml
./ipfc
```

