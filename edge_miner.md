
## 边缘节点挖矿

### 编译代码
```
git clone https://github.com/filepp/go-ipfs
cd go-ipfs
make build
cp cmd/ipfs /usr/local/bin
```


### 初始化
```
export IPFS_PATH=/path/to/ipfsrepo  //指定ipfs仓库目录
ipfs init
```

### 修改配置文件

修改上面指定目录配置文件 `$IPFS_PATH/config`

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

### 运行IPFS


运行ipfs，需要指定矿工角色,(miner-role=1代表边缘节点)
```
ipfs daemon --enable-pubsub-experiment=true --enable-mining=true --miner-role=0
```

查看 peerID, 该id在web页面创建矿工时作为参数使用。
```
ipfs id
```


### 创建矿工
1 使用chrome浏览器，安装MetaMask钱包  
2 MetaMask钱包配置好BSC地址。  
```
主网
https://bsc-dataseed1.binance.org/
链id: 56
```
```
测试网
https://data-seed-prebsc-1-s1.binance.org:8545/
链id： 97 
```
3 打开创建矿工页面，连接钱包。填入钱包地址和ipfs节点的id，点击创建矿工按钮。（确保钱包中有足够的BNB）