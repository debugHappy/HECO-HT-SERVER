# HECO HT 服务端 ，请本地部署，不用担心私钥泄露。
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
--data-urlencode 'fromAddress=来自谁' \
--data-urlencode 'toAddress=给谁转' \
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

# 四：代币 转账

~~~
curl -X POST \
  http://192.168.1.21:8989/token_trans \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'from_address_private=来源地址的私钥&fromAddress=从哪个地址转&toAddress=转出到那个地址&amount=转出数量'
~~~

## 返回结果
~~~
{
    "code": 1,
    "msg": "ok",
    "data": {
        "blockHash": "0x3175f5007700b762600cb43f1b150d020b57ce6f59e112c454da80c2be209e44",
        "blockNumber": 6253207,
        "contractAddress": null,
        "cumulativeGasUsed": 2656657,
        "from": "0xc0b7a9d008f9df4da0ae8f873623241a25264129",
        "gasUsed": 51677,
        "logs": [
            {
                "address": "0x4c9e49f4fdEbD0a5817C5C1ae207EcEaD997a29e",
                "topics": [
                    "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                    "0x000000000000000000000000c0b7a9d008f9df4da0ae8f873623241a25264129",
                    "0x000000000000000000000000986b0d9aeaae529ca02399ba3a030c9eb7a0ce93"
                ],
                "data": "0x00000000000000000000000000000000000000000000000000000006fc23ac00",
                "blockNumber": 6253207,
                "transactionHash": "0x9269149fbb44a15257d6e197eea91123642478a7b3383bccb3482e15f0db47ab",
                "transactionIndex": 24,
                "blockHash": "0x3175f5007700b762600cb43f1b150d020b57ce6f59e112c454da80c2be209e44",
                "logIndex": 42,
                "removed": false,
                "id": "log_75863e88"
            }
        ],
        "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001000000000000000800000000000001000000000000000000000000008001008000000000000000000000000000000000000000000000000000000000000000000000000000000000000000018000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000000100000000000000000000000000000000000000000000000000008000000000000000000000400000000000000000000000000000000000",
        "status": true,
        "to": "0x4c9e49f4fdebd0a5817c5c1ae207ecead997a29e",
        "transactionHash": "0x9269149fbb44a15257d6e197eea91123642478a7b3383bccb3482e15f0db47ab",
        "transactionIndex": 24
    }
}
~~~


# 五：获取地址里面的HT和token数量

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
        "ht": "0.0499224845",
        "token_balance": 99999970
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
        "status": "1",
        "message": "OK",
        "result": {
            "status": "1"
        }
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
# HT代币异步通知数据如下：

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



# 九： token代币交易监控
~~~
1：修改配置文件异步通知地址 web_api_token_domain 改为你自己的

2：调用保存监控地址接口 

3：启动： pm2 start block_token.js

4:系统会自动的过滤不是系统币地址 ，如果监控到是系统的币地址 ，那么会发送异步通知到配置的那个回调地址里面

~~~
# token代币异步通知数据如下：

~~~

{ from:
   '0x42c9c9148a3d01f97e95d79e2629fc601dce9bdfa8f4d341b4d51dd20e9cd1e7',
  to: '0x2b9210748cef1bd439becfd095b59c6322997599',
  txID:
   '0x42c9c9148a3d01f97e95d79e2629fc601dce9bdfa8f4d341b4d51dd20e9cd1e7',
  amount: 1000000000000000,
  extra:
   { blockNumber: '6251540',
     timeStamp: '1625648358',
     hash:
      '0x42c9c9148a3d01f97e95d79e2629fc601dce9bdfa8f4d341b4d51dd20e9cd1e7',
     nonce: '26',
     blockHash:
      '0xecd534c27c61e50f5dce78ea2a6da7e2cf23ea923dd2cdd0193f1c8f2a3f4fe2',
     from: '0x2f775f389bfc9a7bdc21e59c1a8da4cc63840326',
     contractAddress: '0x4c9e49f4fdebd0a5817c5c1ae207ecead997a29e',
     to: '0x2b9210748cef1bd439becfd095b59c6322997599',
     value: '1000000000000000000000000',
     tokenName: 'LongYuanBi Token',
     tokenSymbol: 'LYB',
     tokenDecimal: '9',
     transactionIndex: '68',
     gas: '4247773',
     gasPrice: '1500000000',
     gasUsed: '4225151',
     cumulativeGasUsed: '7830469',
     input: 'deprecated',
     confirmations: '7764' } }


~~~


# 联系我

~~~
qq ： 84075041
~~~
