# EOS 第一课作业，Mac系统

参考：
https://developers.eos.io/eosio-home/docs

# 课程大纲

## 第⼀课：EOS基本环境搭建和操作

1.环境搭建以及安装

2.nodeos 和cleos命令使用

3.钱包和账户的使用

4.代币合约部署

5.系统合约部署

6.创建代币

7.账户、秘钥、钱包、权限等使用

8.智能合约文件 wast文件和ABI文件生成

# 第一课作业

## 1.搭建自己的节点
如果没有条件的可以使用EOS 的麒麟测试网。
测试网地址：https://api-kylin.eosasia.one

1.1 使用brew安装eosio：
brew tap eosio/eosio
brew install eosio

1.2 创建contracts文件夹：
mkdir contracts
cd contracts
找到文件夹路径：
pwd

1.3 搭建节点：
nodeos -e -p eosio \
--plugin eosio::producer_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--data-dir CONTRACTS_DIR/eosio/data \
--config-dir CONTRACTS_DIR/eosio/config \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--verbose-http-errors \
--filter-on='*' >> CONTRACTS_DIR/nodeos.log 2>&1 &
其中，CONTRACTS_DIR/ 改为contracts的路径

1.4 查看节点日志：
tail -f nodeos.log

1.5 创建节点后去eosio/config更改config.ini:
http-server-address = 0.0.0.0:8888

1.6 修改后重启节点：
pkill nodeos

nodeos -e -p eosio \
--plugin eosio::producer_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--data-dir CONTRACTS_DIR/eosio/data \
--config-dir CONTRACTS_DIR/eosio/config \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--verbose-http-errors \
--filter-on='*' >> CONTRACTS_DIR/nodeos.log 2>&1 &
其中，CONTRACTS_DIR/ 改为contracts的路径


## 2.创建自己的账户
搭建测试网络的同学请创建系统账户，创建系统账户之前请创建系统token：SYS、EOS到eosio.token下

系统账户：eosio.stake、eosio.saving、eosio.ramfee、eosio.ram、eosio.names

eosio.msig、eosio.bpay

使用EOS的system合约创建账户，并且分配RAM，CPU资源。

2.1 创建系统钱包
cleos wallet create --to-console
得到钱包地址：PW5J981X1QNhyS88R9fd6Cgh9KuwG1MNMbD2mUgGrx1YMDd12S6eR

解锁钱包（创建后默认已解锁，一段时间后自动上锁）
cleos wallet unlock
输入系统钱包的地址

2.2 创建公私钥对
cleos create key --to-console
得到公私钥地址：
私：
5Kgtc2zwDAckzXb5Syn3Bfgostj6ccu29YMkhjs7J4nL2FsEKcF
公：
EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

导入系统地址：
cleos wallet import

导入EOSIO development key:
5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
对应公钥：
EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV

2.3 创建账户 cleos create account eosio 公钥 公钥
普通账户：
cleos create account eosio test EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

cleos create account eosio test1 EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

创建系统账户：
cleos create account eosio eosio.token EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

cleos create account eosio eosio.stake EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

cleos create account eosio eosio.saving EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

cleos create account eosio eosio.ramfee EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

cleos create account eosio eosio.ram EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

cleos create account eosio eosio.names EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

cleos create account eosio eosio.msig EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

cleos create account eosio eosio.bpay EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy

2.4 查看账户状态
cleos get account 用户名

2.5 部署代币合约
下载部署合约代码
git clone https://github.com/EOSIO/eosio.contracts --branch v1.4.0 --single-branch

编译代币合约
eosio-cpp -I include -o eosio.token.wasm src/eosio.token.cpp --abigen

将合约部署到eosio.token上并且产生系统token：
cleos set contract eosio.token /Users/qikun/contracts/eosio.contracts/eosio.token -p eosio.token

创建系统货币
cleos push action eosio.token create '[ "eosio", "1000000000.0000 SYS"]' -p eosio.token@active 
cleos push action eosio.token create '[ "eosio", "1000000000.0000 EOS"]' -p eosio.token@active


## 3.创建自己的token，token名称、数量可以自己定义，并且尝试向其他账户转账。
作业提交请提交截图或者节点地址和账户名称验证。

创建个人代币
cleos push action eosio.token create '[ "eosio", "1000000000.0000 LQK"]' -p eosio.token@active

发行
cleos push action eosio.token issue '["test", "1000.0000 LQK", "memotest"]' -p eosio@active

转账
cleos push action eosio.token transfer '["test", "test1", "100.0000 LQK", "memotest"]' -p test@active


查询余额

cleos get currency balance eosio.token eosio LQK

cleos get currency balance eosio.token test LQK

cleos get currency balance eosio.token test1 LQK
