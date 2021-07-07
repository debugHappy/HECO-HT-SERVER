# HECO HT  服务端 ，请本地部署，不用担心私钥泄露。
#  不用担心私钥泄露。
# 不用担心私钥泄露。
# 不用担心私钥泄露。



# 安装

~~~
 npm install 
~~~

~~~
修改配置文件 conf/config.js
~~~

~~~
启动：内部服务：

1：pm2 start startServer.json
~~~

# 一：生成币地址本地地址

~~~
curl --location --request POST 'http://192.168.1.21:8989/generate_address'
~~~
## 生成币地址返回结果
~~~
{
    "code": 1,
    "msg": "ok",
    "data": {
        "address": "0x18365C154FDD2BB74b639aA1461e1C59c1bc08f7",
        "privateKey": "0x0b740aa7fbb94b51d740918b7f1a01e7ae423632fa5b04f03341e3bfc4bbd351"
    }
}
~~~


# 二：检测地址是否正确

~~~
curl --location --request POST 'http://192.168.1.21:8989/isAddress' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'address=TXygJpjJtCup78nnJN9qBxrwpiqW2A1yDJ'
~~~
## 检测地址是否正确返回结果
~~~
{
    "code": 1,
    "msg": "ok",
    "data": {
        "status": true
    }
}
~~~

# 三：HECO HT转账

~~~
curl --location --request POST 'http://192.168.1.21:8989/trx_trans' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'from_address_private=发送人的私钥' \
--data-urlencode 'fromAddress=TDKGuuBEcHXj7g28NUZpVy4oG4DQpR2fG6' \
--data-urlencode 'toAddress=TAqF1BphciVbxzMR2qJyWdBWRFzz6xj2nh' \
--data-urlencode 'amount=0.01' 
~~~
## HT转账结果
~~~
{
    "code": 1,
    "msg": "ok",
    "data": {
        "blockHash": "0x85d09a4586d3438811b756a04d1c5deb4d124058756973ce1b991b887ef88691",
        "blockNumber": 6249990,
        "contractAddress": null,
        "cumulativeGasUsed": 125473,
        "from": "0xc0b7a9d008f9df4da0ae8f873623241a25264129",
        "gasUsed": 21000,
        "logs": [],
        "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "status": true,
        "to": "0xa4aa64949b83049ccdd4e03d6e554a6c063e8e9d",
        "transactionHash": "0xcce364a4cda88bc984b05dd3321bd4b8aa3d50e4162eaf050f5564e1798b7b70",
        "transactionIndex": 3
    }
}
~~~



# 五：获取地址里面的HT数量

~~~
curl --location --request POST 'http://192.168.1.21:8989/get_money' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'address=地址0x开头的地址'
~~~

## 返回结果
~~~
{
    "code": 1,
    "msg": "ok",
    "data": {
        "ht": "0.497537"
    }
}
~~~


# 六：根据交易hash查询交易信息

~~~
curl --location --request POST 'http://192.168.1.21:8989/GetTransactionById' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'trxid=2a985f0c5fd37aaffca2f9c29bd1eaa50ccaae6adef7585b73ad89ae67b745a4'
~~~

## 返回结果
~~~
{
    "code": 1,
    "msg": "ok",
    "data": {
        "blockHash": "0x85d09a4586d3438811b756a04d1c5deb4d124058756973ce1b991b887ef88691",
        "blockNumber": 6249990,
        "from": "0xC0b7A9D008f9Df4da0Ae8F873623241a25264129",
        "gas": 21000,
        "gasPrice": "1000000000",
        "hash": "0xcce364a4cda88bc984b05dd3321bd4b8aa3d50e4162eaf050f5564e1798b7b70",
        "input": "0x",
        "nonce": 2,
        "to": "0xA4Aa64949B83049CcDD4e03D6e554A6c063e8E9D",
        "transactionIndex": 3,
        "value": "2100000000000000",
        "v": "0x224",
        "r": "0x5c1bc665c87ca8b55bce9c768caab7de453e154ee7b95b73c9133d177d17d10e",
        "s": "0x6b741d0eecc0e024277416c44214cdd8f9c226325325c799735348e2be5eaf20"
    }
}
~~~




# 七： 保存需要监控的地址，接口如下

~~~
curl --location --request POST 'http://192.168.1.21:8989/save_check_address' \
--header 'Content-Type: application/json' \
--data-raw '[
    "TDhSd1bZEfCD5HF2dy8dGicZbYfg1MWxND",
    "TNhd6HJmBuvfR3F129p8zBC3nTKh4E3Gnf", 
    "TC1CYwkVLYa3aBDVEoEsC3wmTPKCBEdoGf"
]'
~~~
## 接口返回

~~~
{
    "code": 1,
    "msg": "ok",
    "data": {
        "success_num": 1
    }
}
~~~

# 八： HT交易监控
~~~
1：修改配置文件异步通知地址 web_api_ht_domain 改为你自己的

2：调用保存监控地址接口 

3：启动： pm2 start monitor_block_trx.js

4:系统会自动的过滤不是系统币地址 ，如果监控到是系统的币地址 ，那么会发送异步通知到配置的那个回调地址里面

~~~
# HT异步通知数据如下：

~~~

{
	"owner_address": "TSSrhM7VRWFZMwPZ4QPqrZULTP4swAkkyW",
	"to_address": "THK7MrUT6FBCS1RPqgcspY3ehP6pAo7DoN",
	"txID": "07450f4027f3ab21bf178d36bf57815b73f8e4d2fb8b8c5e0556d1b67cb7ea13",
	"amount": 4200,
	"extra": {
		"ret": [{
			"contractRet": "SUCCESS"
		}],
		"signature": ["84c2cdb5990fc3f6fd46278b9575c646377cdb3190765df4215df056bb4e9741e2dd5cd9f8bfbab5f674469218f2074e73b14a48e9460b7f115df77d8aaa8a0601"],
		"txID": "07450f4027f3ab21bf178d36bf57815b73f8e4d2fb8b8c5e0556d1b67cb7ea13",
		"raw_data": {
			"contract": [{
				"parameter": {
					"value": {
						"amount": 4200,
						"asset_name": "31303033353333",
						"owner_address": "41b4bcb59b5a7d446ad2ec0780af85fa36c4ed14ee",
						"to_address": "41508c7d8edcd6c0eb1f24dbb898cbf610d2e2f789"
					},
					"type_url": "type.googleapis.com/protocol.TransferAssetContract"
				},
				"type": "TransferAssetContract"
			}],
			"ref_block_bytes": "4c96",
			"ref_block_hash": "00f3655724057d2a",
			"expiration": 1615975383000,
			"timestamp": 1615975325824
		},
		"raw_data_hex": "0a024c96220800f3655724057d2a40d8ff8dfd832f5a74080212700a32747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e736665724173736574436f6e7472616374123a0a0731303033353333121541b4bcb59b5a7d446ad2ec0780af85fa36c4ed14ee1a1541508c7d8edcd6c0eb1f24dbb898cbf610d2e2f78920e8207080c18afd832f"
	}
}

~~~




# 联系我

~~~
qq ： 84075041
~~~