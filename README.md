# Open93AtHome-V3

## 简介

这是一个类似于 [OpenBMCLAPI](https://github.com/bangbang93/openbmclapi) **主控端**的分发文件项目，经过三次重构，现已可以完美兼容 **Node、Python、C#、PHP** 端
> [!TIP]
> 本项目实际可被用于分发任何有效 Git 仓库内的文件，因此并不与 bangbang93HUB 有任何关联

## 部署

以下是基于修改现有 OpenBMCLAPI 节点端的办法
> [!IMPORTANT]
> 以下方法仅在 **Node、Python、C#、PHP 端**进行了测试，其他端的方法理论可行但未经验证。
> 如果不行请自行解决或开 issue 进行询问，不要当作 bug 发到人家仓库去

### [Node 端](https://github.com/bangbang93/openbmclapi)

以下方法二选一，根据实际情况

#### 基于修改源代码

| 位置                 | 目的     | 做法                                                                    |
|--------------------|--------|-----------------------------------------------------------------------|
| **cluster.ts** L59 | 修改上线地址 | 修改 `private readonly prefixUrl = process.env.CLUSTER_BMCLAPI ??` 后面的值 |

#### 基于修改环境变量

| 位置       | 目的     | 做法                     |
|----------|--------|------------------------|
| **.env** | 修改上线地址 | `CLUSTER_BMCLAPI=上线地址` |

**同时，由于 node 端的白名单机制，还需要进行以下步骤之一：**

#### 修改代码（有哪个改哪个）

| 位置                      | 目的    | 做法                                                                      |
|-------------------------|-------|-------------------------------------------------------------------------|
| **dist/cluster.js** L38 | 修改白名单 | 修改 `const whiteListDomain = ['localhost', 'bangbang93.com'];`，添加上你上线的域名 |
| **cluster.js** L46      | 修改白名单 | 修改 `const whiteListDomain = ['localhost', 'bangbang93.com'];`，添加上你上线的域名 |

#### 域名欺骗法

使用你的域名，新建一个 **CNAME** 解析（也可以用别的，不作赘述），名称为 `bangbang93.com.xxxxxx`或者`localhost.xxxxxx`
（后面接你的域名，总之含有`bangbang93.com`或者`localhost`的关键词就行），解析到服务器地址，然后将上线地址改成该地址

### [Go 端](https://github.com/LiterMC/go-openbmclapi)

| 位置                   | 目的     | 做法                          |
|----------------------|--------|-----------------------------|
| **main.go** L57      | 修改上线地址 | 修改 `const ClusterServerURL` |
| **hijacker.go** L107 | 修改下载地址 | 修改 `const hijackingHost`    |

### [Python 端](https://github.com/TTB-Network/python-openbmclapi)

| 位置                 | 目的     | 做法        |
|--------------------|--------|-----------|
| **config.yml** L15 | 修改上线地址 | 修改 `url:` |

### [C# 端](https://github.com/SaltWood-Studio/CSharp-OpenBMCLAPI)

| 位置                          | 目的     | 做法                                                                 |
|-----------------------------|--------|--------------------------------------------------------------------|
| **Modules/HttpRequest.cs**  | 修改上线地址 | 注释 `14 ~ 16`行，在 `12` 行后另起一行，输入</br>`BaseAddress = new Uri("xxxx")` |
| **Modules/Cluster.cs** L704 | 修改下载地址 | 修改 `GetRedirectUrls` 方法调用中插值字符串的值（不加 `/`）                          |

### [PHP 端](https://github.com/AppleBlockTeam/php-openbmclapi)

| 位置                 | 目的     | 做法              |
|--------------------|--------|-----------------|
| **config.php** L18 | 修改上线地址 | 修改 `CenterUrl:` |

## 调试

1. 将此项目 `git clone` 到本地
2. 使用**支持 Type Script 的 IDE** 打开项目
3. 愉快的开发吧🎉

``` shell
git clone https://github.com/SaltWood-Studio/Open93AtHome-V3.git
cd Open93AtHome-V3
```

### 贡献

提交 PR 前请确保你的代码至少经过编译测试

# 特别鸣谢

- **[openbmclapi](https://github.com/bangbang93/openbmclapi)**: 由 @bangbang93 大佬的项目获得了想法，诞生了此项目
- **[93AtHome-Dashboard](https://github.com/Mxmilu666/93Home-Dash)**: 由 @Mxmilu666 大佬为本项目编写的仪表盘
- **[bangbang93Hub](https://github.com/Mxmilu666/bangbang93HUB)**: 由 @Mxmilu666 大佬提出想法并付诸实践
- **[tianxiu2b2t](https://github.com/tianxiu2b2t)**: 帮助解决了 Avro 部分的问题，解答了一些弱智问题
