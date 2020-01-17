# API操作示例

## 相关帐号

* 债仓管理合约: danchorsmart
* 稳定币合约: danchortoken

## 生成USN

向合约帐号 danchorsmart 转账EOS, memo格式:  "`issue:质押率`" 

```
cleos transfer testuseraaaa danchorsmart "100 EOS" "issue:15000"
```

## 通过降低质押率，生成新的USN

调用合约帐号的 adjust action: 

```
cleos push action danchorsmart adjust '["testuseraaaa", 15000, true]' -p testuseraaaa
```

## 偿还USN，并减少抵押量

向合约帐号 danchorsmart 转账USN, memo格式:  "`repay:质押率`" 

```
cleos transfer -c danchortoken testuseraaaa danchorsmart "11.0000 USN" "repay:15000"
```

## 仅偿还USN， 但不减少抵押量

向合约帐号 danchorsmart 转账USN, memo格式:  "`repay:0`" 

```
cleos transfer -c danchortoken testuseraaaa danchorsmart "11.0000 USN" "repay:0"
```

## 仅增加抵押量

向合约帐号 danchorsmart 转账EOS, memo格式:  "`deposit`" 

```
cleos transfer testuseraaaa danchorsmart "100 EOS" "deposit"
```

## 仅降低抵押量

调用合约帐号的 withdraw action: 

```
cleos push action danchorsmart withdraw '["testuseraaaa", "11.0000 EOS"]' -p testuseraaaa
```

## 爆仓抢拍

先查询合约数据库，获取爆仓单信息:

```
cleos get table danchorsmart danchorsmart auctions

{
  "rows": [{
      "aid": 1,
      "user": "testuseraaaa",
      "price": 15063,
      "pledge": "200.0000 EOS",
      "issue": "327.9066 USN",
      "remain_pledge": "169.9345 EOS",
      "remain_issue": "327.9066 USN",
      "create_time": "2019-12-31T07:56:00"
    },,{
      "aid": 2,
      "user": "testuserbbbb",
      "price": 15063,
      "pledge": "200.0000 EOS",
      "issue": "245.9300 USN",
      "remain_pledge": "169.9509 EOS",
      "remain_issue": "245.9300 USN",
      "create_time": "2019-12-31T07:56:00"
    }
  ],
  "more": false
}
```

如果有存在爆仓的订单，可以直接参与抢拍, 获得最多9折优惠的EOS，

抢拍方式为 向合约帐号 danchorsmart 转账USN, memo格式:  "`bid:爆仓单id`" 

```
cleos transfer -c danchortoken testuseraaaa danchorsmart "100 USN" "bid:2"
```