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

使用brew安装eosio：
brew tap eosio/eosio
brew install eosio

创建contracts文件夹：
mkdir contracts
cd contracts
找到文件夹路径：
pwd

搭建节点：
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

查看节点：
tail -f nodeos.log

创建节点后去eosio/config更改config.ini:
http-server-address = 0.0.0.0:8888


## 2.创建自己的账户
搭建测试网络的同学请创建系统账户，创建系统账户之前请创建系统token：SYS、EOS到eosio.token下
系统账户：eosio.stake、eosio.saving、eosio.ramfee、eosio.ram、eosio.names
eosio.msig、eosio.bpay
使用EOS的system合约创建账户，并且分配RAM，CPU资源。




## 3.创建自己的token，token名称、数量可以自己定义，并且尝试向其他账户转账。
作业提交请提交截图或者节点地址和账户名称验证。
