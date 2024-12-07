# CFSSL

CFSSL（Cloudflare's PKI and TLS toolkit）是一个开源的公钥基础设施（PKI）工具包，支持证书颁发、签名、验证等功能，方便集成到自动化流程中，尤其适用于需要大规模自动化管理TLS/SSL证书的场景。

- [CFSSL GitHub 仓库](https://github.com/cloudflare/cfssl)

------

## 安装 CFSSL

### 下载 CFSSL 软件包

以下命令用于下载 CFSSL 工具包的可执行文件，包括：

- **`cfssl`**：证书生成工具。
- **`cfssljson`**：用于处理 JSON 格式的输出。
- **`cfssl-certinfo`**：用于查看证书信息。

执行以下命令下载所需文件：

```bash
wget https://github.com/cloudflare/cfssl/releases/download/v1.6.5/cfssl_1.6.5_linux_amd64
wget https://github.com/cloudflare/cfssl/releases/download/v1.6.5/cfssljson_1.6.5_linux_amd64
wget https://github.com/cloudflare/cfssl/releases/download/v1.6.5/cfssl-certinfo_1.6.5_linux_amd64
```

### 安装 CFSSL 到系统路径

将下载的文件移动到系统的可执行路径 `/usr/bin/` 中，并赋予执行权限：

```bash
sudo cp cfssl_1.6.5_linux_amd64 /usr/bin/cfssl
sudo cp cfssljson_1.6.5_linux_amd64 /usr/bin/cfssljson
sudo cp cfssl-certinfo_1.6.5_linux_amd64 /usr/bin/cfssl-certinfo
sudo chmod +x /usr/bin/cfssl*
```

### 验证安装

运行以下命令，确认 CFSSL 安装成功并检查版本信息：

```bash
cfssl version
```

输出示例：

```
Version: 1.6.5
Runtime: go1.22.0
```

------

## 生成 CA 证书

### 创建 CA 配置文件

#### 生成 `ca-config.json` 配置文件

`ca-config.json` 定义了 CA 的签名策略和证书有效期配置：

```bash
tee ca-config.json <<EOF
{
  "signing": {
    "default": {
      "expiry": "876000h"
    },
    "profiles": {
      "default": {
        "expiry": "876000h",
        "usages": ["signing", "key encipherment", "server auth", "client auth"]
      },
      "server": {
        "expiry": "876000h",
        "usages": ["signing", "key encipherment", "server auth"]
      },
      "client": {
        "expiry": "876000h",
        "usages": ["signing", "key encipherment", "client auth"]
      }
    }
  }
}
EOF
```

#### 生成 `ca-csr.json` 文件

`ca-csr.json` 定义了 CA 的基本信息，例如组织名、国家、省份等：

```bash
tee ca-csr.json <<EOF
{
    "CA": {
        "expiry": "876000h"
    },
    "CN": "ateng.local",
    "key": {
        "algo": "rsa",
        "size": 2048
    },
    "names": [
        {
            "C": "CN",
            "L": "Chongqing",
            "ST": "Chongqing",
            "O": "Ateng",
            "OU": "Ateng"
        }
    ]
}
EOF
```

### 生成 CA 证书和私钥

使用以下命令生成 CA 的证书和私钥：

```bash
cfssl gencert -initca ca-csr.json | cfssljson -bare ca
```

验证生成的 CA 证书：

```bash
cfssl certinfo -cert ca.pem
```

------

## 生成服务端证书

### 创建服务端配置文件

#### 生成 `server-csr.json` 文件

`server-csr.json` 定义了服务端证书的通用名（CN）以及主机名信息：

```bash
tee server-csr.json <<EOF
{
    "CN": "nginx.ateng.local",
    "hosts": [
        "nginx.ateng.local",
        "localhost",
        "127.0.0.1",
        "192.168.1.10"
    ],
    "key": {
        "algo": "rsa",
        "size": 2048
    },
    "names": [
        {
            "C": "CN",
            "L": "Chongqing",
            "ST": "Chongqing",
            "O": "Ateng",
            "OU": "Nginx"
        }
    ]
}
EOF
```

### 生成服务端证书和私钥

执行以下命令生成服务端证书和私钥：

```bash
cfssl gencert -ca=ca.pem -ca-key=ca-key.pem -config=ca-config.json -profile=server server-csr.json | cfssljson -bare server
```

验证生成的服务端证书：

```bash
cfssl certinfo -cert server.pem
```

------

## 生成客户端证书

### 创建客户端配置文件

#### 生成 `client-csr.json` 文件

`client-csr.json` 定义了客户端证书的通用名（CN）和基本信息：

```bash
tee client-csr.json <<EOF
{
    "CN": "client.ateng.local",
    "hosts": [
        ""
    ],
    "key": {
        "algo": "rsa",
        "size": 2048
    },
    "names": [
        {
            "C": "CN",
            "L": "Chongqing",
            "ST": "Chongqing",
            "O": "Ateng",
            "OU": "Client"
        }
    ]
}
EOF
```

### 生成客户端证书和私钥

执行以下命令生成客户端证书和私钥：

```bash
cfssl gencert -ca=ca.pem -ca-key=ca-key.pem -config=ca-config.json -profile=client client-csr.json | cfssljson -bare client
```

验证生成的客户端证书：

```bash
cfssl certinfo -cert client.pem
```

## 证书说明

以下是与证书相关文件的说明及作用

| **文件名**       | **类型**   | **作用**                                             | **用途**                                          | **分发建议**                       |
| ---------------- | ---------- | ---------------------------------------------------- | ------------------------------------------------- | ---------------------------------- |
| `ca.pem`         | CA 根证书  | 提供信任链的根，用于验证下级证书的有效性             | 部署在客户端或服务端，用于验证 TLS 通信的对端证书 | 安全分发，提供给所有客户端和服务端 |
| `ca-key.pem`     | CA 私钥    | 用于签发下级证书                                     | 用于签署服务端和客户端证书                        | 严格保密，不分发                   |
| `server.pem`     | 服务端证书 | 提供 TLS 加密通信能力                                | 部署到服务端，用于与客户端建立安全连接            | 部署到服务端                       |
| `server-key.pem` | 服务端私钥 | 解密客户端发送的数据，与 `server.pem` 配对使用       | 部署到服务端，保护通信机密性                      | 严格保密，仅部署到服务端           |
| `client.pem`     | 客户端证书 | 用于客户端身份认证                                   | 部署到客户端，用于双向认证场景                    | 部署到客户端                       |
| `client-key.pem` | 客户端私钥 | 保护客户端发送数据的机密性，与 `client.pem` 配对使用 | 部署到客户端，用于与服务端建立安全连接            | 严格保密，仅部署到客户端           |

**补充说明**

1. **CA 文件**
    - `ca.pem` 是信任链的基础，必须在客户端和服务端间分发，以建立信任。
    - `ca-key.pem` 是签署证书的私钥，必须保存在安全环境中，不得泄露。
2. **服务端文件**
    - `server.pem` 和 `server-key.pem` 必须一起部署在服务端，用于加密通信和身份验证。
    - 服务端文件仅适用于特定服务器的配置，私钥需妥善保管。
3. **客户端文件**
    - `client.pem` 和 `client-key.pem` 必须一起部署在客户端，用于双向认证和安全通信。
    - 私钥文件应严格限制访问权限，避免因泄露导致安全问题。
