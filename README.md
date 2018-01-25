# RoyalBitcoin-Explorer

纯真比特币的区块链浏览器，基于 [bitcore-node](https://github.com/bitpay/bitcore-node) 进行定制构建。

## Badge

### GitHub

[![GitHub followers](https://img.shields.io/github/followers/NewEconomicTeam.svg?label=github%20follow)](https://github.com/NewEconomicTeam/RoyalBitcoin-Explorer) [![GitHub stars](https://img.shields.io/github/stars/NewEconomicTeam/RoyalBitcoin-Explorer.svg?label=github%20stars)](https://github.com/NewEconomicTeam/RoyalBitcoin-Explorer) [![GitHub watchers](https://img.shields.io/github/watchers/NewEconomicTeam/RoyalBitcoin-Explorer.svg?label=github%20watch)](https://github.com/NewEconomicTeam/RoyalBitcoin-Explorer) [![GitHub repo size in bytes](https://img.shields.io/github/repo-size/NewEconomicTeam/RoyalBitcoin-Explorer.svg)](https://github.com/NewEconomicTeam/RoyalBitcoin-Explorer)

### 其他

[![license](https://img.shields.io/github/license/NewEconomicTeam/RoyalBitcoin-Explorer.svg)](https://github.com/NewEconomicTeam/RoyalBitcoin-Explorer)

## 镜像标签(tags)

- `littlemo/rbtc-explorer:latest`

## 使用说明

在使用时应按需为Web服务器进行端口映射，并挂载 `bitcore-node.json` 配置文件到路径 `/app/bitcore/rbtc_node/bitcore-node.json` 下（建议进行只读挂载）

### bitcore-node.json 用例

```json
{
  "network": "livenet",
  "port": 80,
  "services": [
    "bitcoind",
    "insight-api",
    "insight-ui",
    "web"
  ],
  "servicesConfig": {
    "insight-ui": {
      "routePrefix": "",
      "apiPrefix": "api"
    },
    "insight-api": {
      "routePrefix": "api",
      "disableRateLimiter": true,
      "enableCache": true
    },
    "bitcoind": {
      "connect": [
        {
          "rpchost": "127.0.0.1",                   // 替换为相应节点主机的IP地址
          "rpcport": 8332,                          // 替换为相应节点主机的RPC服务端口
          "rpcuser": "username",                    // 替换为相应节点主机的RPC用户名
          "rpcpassword": "password",                // 替换为相应节点主机的RPC密码
          "zmqpubrawtx": "tcp://10.0.0.3:28332",    // 替换为相应节点主机的ZMQ服务IP&端口，下同
          "zmqpubhashtx": "tcp://10.0.0.3:28332",
          "zmqpubrawblock": "tcp://10.0.0.3:28332",
          "zmqpubhashblock": "tcp://10.0.0.3:28332"
        }
      ]
    }
  }
}
```

## 启动容器

### docker-cli

```bash
$ docker run -d -p 80:80 -v /paht/to/bitcore-node.json:/app/bitcore/rbtc_node/bitcore-node.json --name rbtc-explorer littlemo/rbtc-explorer:latest
```

### docker-compose

```yml
version: '2'
services:
  explorer:
    image: littlemo/rbtc-explorer
    container_name: rbtc-explorer
    restart: unless-stopped
    ports:
      - "80:80"
    volumes:
      # 挂载配置文件
      - /paht/to/bitcore-node.json:/app/bitcore/rbtc_node/bitcore-node.json:ro
```

## 问题

如果您在使用该镜像时遇到任何问题，请查看镜像源码的 [NewEconomicTeam/RoyalBitcoin-Explorer](https://github.com/NewEconomicTeam/RoyalBitcoin-Explorer) Repo，并在其中提交 Issues 给我们，多谢您的帮助~~
