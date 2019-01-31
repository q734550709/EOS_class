# EOS 第二课作业，Mac系统

参考：
https://developers.eos.io/eosio-home/docs

# 课程大纲

## 第⼆课：智能合约初级设计

1.EOS智能合约的开发
2.智能合约的Action 和Transaction 
3.智能合约的数据类型
4.智能合约的里面的内联通信和延时通信

## 第二课作业

1.创建一个叫game的用户。
cleos create account eosio game EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy


2.写一个游戏合约把第一课自己创建的token通过游戏合约转账给game用户。




3.游戏合约只能由特定的用户调用转账。

3.1 给test4设定权限
cleos set account permission test4 active '{"threshold": 1, "keys":[{"key":"EOS8ZQsNEFYgmPh951YtCdMyfoqnjGV3Z5U6CnDuryH2mg9YvtcZy", "weight":1}],"accounts":[{"permission":{"actor":"test4","permission":"eosio.code"},"weight":1}]}' owner -p test4
