# API Explanation

## The relevant accounts

* Contract Account : danchorsmart
* Token Account : danchortoken

## Issue USN

transfer EOS to danchorsmart , memo format is :  "`issue:rate`" 

```
cleos transfer testuseraaaa danchorsmart "100 EOS" "issue:15000"
```

## By reducing the charge rate to issue new USN 

call the `adjust` action of  Contract : 

```
cleos push action danchorsmart adjust '["testuseraaaa", 15000, true]' -p testuseraaaa
```

## Repay USN and withdraw EOS

transfer USN to danchorsmart, memo format is: "`repay:rate`" 

```
cleos transfer -c danchortoken testuseraaaa danchorsmart "11.0000 USN" "repay:15000"
```

## Only Repay USN 

transfer USN to danchorsmart, memo format is:  "`repay:0`" 

```
cleos transfer -c danchortoken testuseraaaa danchorsmart "11.0000 USN" "repay:0"
```

## Deposit

transfer EOS to danchorsmart, memo format is:  "`deposit`" 

```
cleos transfer testuseraaaa danchorsmart "100 EOS" "deposit"
```

## Withdraw EOS

call the `withdraw` action of  Contract : 

```
cleos push action danchorsmart withdraw '["testuseraaaa", "11.0000 EOS"]' -p testuseraaaa
```

## Bid

Check to see if there is an auction: 

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

If has any auction, You can buy it at a discount of 2%～10%

transfer USN to danchorsmart, memo format is:  "`bid:aid`" 

```
cleos transfer -c danchortoken testuseraaaa danchorsmart "100 USN" "bid:2"
```

[中文文档](./README_zh.md)