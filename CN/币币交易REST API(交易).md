# 币币交易REST API(交易)

## 开始使用    

REST，即Representational State Transfer的缩写，是目前最流行的一种互联网软件架构。它结构清晰、符合标准、易于理解、扩展方便，正得到越来越多网站的采用。其优点如下：    
> - 在 `RESTful` 架构中，每一个 `URL` 代表一种资源；    
> - 客户端和服务器之间，传递这种资源的某种表现层；    
> - 客户端通过四个 `HTTPS` 指令，对服务器端资源进行操作，实现“表现层状态转化”。   

建议开发者使用 `REST API` 进行币币交易或者资产提现等操作。    
    
## 请求交互    

`REST` 访问的根URL：`https://www.ezb.com/` 或 `https://api.ezb.com/`

所有请求基于 `Https` 协议，请求头信息中 `contentType` 需要统一设置为：`application/x-www-form-urlencoded`    
	
请求交互说明    
> 1. 请求参数：根据接口请求参数规定进行参数封装。    
> 2. 提交请求参数：将封装好的请求参数通过 `POST` 或 `GET` 方式提交至服务器。    
> 3. 服务器响应：服务器首先对用户请求数据进行参数安全校验，通过校验后根据业务逻辑将响应数据以 `JSON` 格式返回给用户。    
> 4. 数据处理：对服务器响应数据进行处理。 

## API参考  

### 币币交易 API 

#### 1.添加委托订单 

请求参数	

|参数|必选|类型|Example参数|说明|
|:-----  |:------- |:-------|:-----|-----|
|symbol    |true    |String  |`BAR/USDT` |交易对|
|price    |true    |double| 0.020 | 挂单价格     |
|amount    |true    |double  |1 |交易数量|
|direction    |true    |String  |`BUY` or `SELL` |交易类型：买入，或者卖出|
|type    |true    |String  |`LIMIT_PRICE` or `MARKET_PRICE` |价格类型：限价交易，或者市价交易|

请求示例1：
```
curl -d "symbol=AIS^%^2FUSDT^&price=1^&amount=1^&direction=BUY^&type=LIMIT_PRICE" "https://api.ezb.com/exchange/order/add?apiKey=XXXXXXXX" 
```

请求示例2:	

```javascript
# Request
POST https://api.ezb.com/exchange/order/add?apiKey=XXXXXXXX
{
  "symbol"："BAR/USDT",
  "price"："1.0000",
  "amount"："3",
  "direction"："BUY",
  "type"："LIMIT_PRICE",
}
# Response
{
	"code": 0,
	"message": "SUCCESS",
	"data": {
		"symbol": "BAR/USDT",
		"orderId": "E204977003474976768",
		"price": 1.0000,
		"direction": "SELL"
	}
}
```

返回值说明	

|字段|描述|
|-|-|
|code|`0` 成功<br>`500` 失败 |
|orderId|订单ID|
|price|挂单价格|
|direction|挂单价格|


#### 2.查询历史委托 

请求参数	

|参数|必选|类型|Example参数|说明|
|:-----  |:-------|:-----|:-----|-----|
|symbol    |true    |string  |BAR/USDT |交易币对，比如：`BAR/USDT`,`TRX/USDT`|
|pageNo    |true    |int   |0|第几页|
|pageSize    |true    |int   |10|No of lines in 1 Page|

请求示例:	

> https://api.ezb.com/exchange/order/history?apiKey=XXXXXXXX

```javascript
# Request
POST https://api.ezb.com/exchange/order/history?apiKey=XXXXXXXX
{
  "symbol"："BAR/USDT",
  "pageNo"："0",
  "pageSize"："10",
}
# Response
{
	"content": [{
		"orderId": "E153536006577170",
		"memberId": 13526,
		"type": "LIMIT_PRICE",
		"amount": 10.00000000,
		"symbol": "BAR/USDT",
		"tradedAmount": 0,
		"turnover": 0E-8,
		"coinSymbol": "ETH",
		"baseSymbol": "USDT",
		"status": "TRADING",
		"direction": "BUY",
		"price": 1.00000000,
		"time": 1535360065771,
		"completedTime": null,
		"canceledTime": null,
		"detail": [],
		"completed": false
	}],
	"last": true,
	"totalElements": 1,
	"totalPages": 1,
	"first": true,
	"numberOfElements": 1,
	"sort": [{
		"direction": "DESC",
		"property": "time",
		"ignoreCase": false,
		"nullHandling": "NATIVE",
		"ascending": false,
		"descending": true
	}],
	"size": 10,
	"number": 0
}
```

返回值说明	

|返回字段|字段类型|说明   |
|:-----   |:------|:-----------------------------   |
|orderId   |string    | 订单id  |
|memberId  |long | 用户id                       |
|type  |string | 挂单类型                      |
|amount  |BigDecimal | 数量                      |
|symbol  |string | 交易对                  |
|coinSymbol  |string | 币单位                      |
|baseSymbol  |string | 结算币种      |
|status  |string | 状态  `TRADING` 交易中,`COMPLETED` 已完成,`CANCELED` 已取消           |
|direction  |string | 订单方向   `BUY` or `SELL`           |
|price  |string | 价格                 |
|time  |string | 委托时间                 |
|completedTime  |string | 交易完成时间     |
|canceledTime  |string | 取消时间                 |
|detail  |string | 明细             |


#### 3.查询当前委托 

请求参数	


|参数|必选|类型|Example参数|说明|
|:-----  |:-------|:-----|:-----|-----|
|symbol    |true    |string  |BAR/USDT |交易币对，比如：`BAR/USDT`,`TRX/USDT`|
|pageNo    |true    |int   |0|第几页|
|pageSize    |true    |int   |10|No of lines in 1 Page|


请求示例:	

> https://api.ezb.com/exchange/order/current?apiKey=XXXXXXXX

```javascript
# Request
GET https://api.ezb.com/exchange/order/current
{
  "symbol"："BAR/USDT",
  "pageNo"："0",
  "pageSize"："10",
}
# Response
{
	"content": [{
		"orderId": "E153536006577170",
		"memberId": 13526,
		"type": "LIMIT_PRICE",
		"amount": 10.00000000,
		"symbol": "ETH/USDT",
		"tradedAmount": 0,
		"turnover": 0E-8,
		"coinSymbol": "ETH",
		"baseSymbol": "USDT",
		"status": "TRADING",
		"direction": "BUY",
		"price": 2.00000000,
		"time": 1535360065771,
		"completedTime": null,
		"canceledTime": null,
		"detail": [],
		"completed": false
	}],
	"last": true,
	"totalElements": 1,
	"totalPages": 1,
	"first": true,
	"numberOfElements": 1,
	"sort": [{
		"direction": "DESC",
		"property": "time",
		"ignoreCase": false,
		"nullHandling": "NATIVE",
		"ascending": false,
		"descending": true
	}],
	"size": 100,
	"number": 0
}
```
返回值说明	

|返回字段|字段类型|说明   |
|:-----   |:------|:-----------------------------   |
|orderId   |string    | 订单id  |
|memberId  |long | 用户id                       |
|type  |string | 挂单类型                      |
|amount  |BigDecimal | 数量                      |
|symbol  |string | 交易对                  |
|coinSymbol  |string | 币单位                      |
|baseSymbol  |string | 结算币种      |
|status  |string | 状态  `TRADING` 交易中,`COMPLETED` 已完成,`CANCELED` 已取消 |
|direction  |string | 订单方向    `BUY` or `SELL`     |
|price  |string | 价格        |
|time  |string | 时间        |
|completedTime  |string | 交易完成时间     |
|canceledTime  |string | 取消时间                 |
|detail  |string | 明细             |


#### 4.订单详情（查询用户订单详情）

请求参数	

|参数|必选|类型|Example参数|说明|
|:-----  |:-------|:-----|:-----|-----|
|orderId    |true    |string  |E156281339431634 |订单orderId|

请求示例:	

> http://api.ezb.com/exchange/order/content/{orderId}?apiKey=XXXXXXXX

```javascript
# Request
POST http://api.ezb.com/exchange/order/content/E156281339431634?apiKey=XXXXXXXX

# Response
{
    "code": 0,
    "message": "SUCCESS",
    "data": {
        "orderId": "E156281339431634",
        "memberId": 2585648,
        "type": "LIMIT_PRICE",
        "amount": 5,
        "symbol": "XRP/USDT",
        "tradedAmount": 3,
        "turnover": 1.3632,
        "coinSymbol": "XRP",
        "baseSymbol": "USDT",
        "status": "TRADING",
        "direction": "SELL",
        "price": 0.4544,
        "time": 1562813394316,
        "completedTime": null,
        "canceledTime": null,
        "marginTrade": 0,
        "burstTrade": 0,
        "detail": [
            {
                "_id": "5d26a3d9fd5bec7fea18046f",
                "orderId": "E156281339431634",
                "price": 0.4544,
                "amount": 1,
                "turnover": 0.4544,
                "fee": 0.0004544,
                "time": 1562813401727
            },
            {
                "_id": "5d26a3f3fd5bec7fea1804a7",
                "orderId": "E156281339431634",
                "price": 0.4544,
                "amount": 2,
                "turnover": 0.9088,
                "fee": 0.0009088,
                "time": 1562813427538
            }
        ],
        "checkFlag": null,
        "completed": false
    }
}
```

###### 错误时返回：
``` javascript
{
    "code": 500,
    "message": "orderId error",
    "data": null
}
```

返回值说明	

|返回字段|字段类型|说明   |
|:-----   |:------|:-----------------------------   |
|code  |int | `0`成功,`500`失败                       |
|orderId   |string    | 订单id  |
|memberId  |long | 用户id                       |
|type  |string | 挂单类型                      |
|amount  |BigDecimal | 数量                      |
|symbol  |string | 交易对                  |
|coinSymbol  |string | 币单位                      |
|baseSymbol  |string | 结算币种      |
|status  |string | 状态  `TRADING` 交易中,`COMPLETED` 已完成,`CANCELED` 已取消 |
|direction  |string | 订单方向    `BUY` or `SELL`     |
|price  |string | 价格                 |
|time  |string | 时间                 |
|completedTime  |string | 交易完成时间     |
|canceledTime  |string | 取消时间                 |
|detail  |string | 明细             |
|completed  |string |             |




#### 5.查询委托成交明细

请求参数	

|参数名|必选|类型|Example参数|说明|
|:-----  |:-------|:-----|:-----|-----|
|orderId    |ture    |string | E156281339431634|订单id     |


请求示例:	

https://api.ezb.com/exchange/order/detail/E156281339431634?apiKey=XXXXXXXX

```javascript
# Request
POST https://api.ezb.com/exchange/order/detail/E156281339431634?apiKey=XXXXXXXX
{
  "orderId"："E156281339431634",
}
# Response
[
    {
        "orderId": "E156281339431634",
        "price": 0.4544,
        "amount": 1,
        "turnover": 0.4544,
        "fee": 0.0004544,
        "time": 1562813427538
    },
    {
        "orderId": "E156281339431634",
        "price": 0.4544,
        "amount": 2,
        "turnover": 0.9088,
        "fee": 0.0009088,
        "time": 1562813427538
    },
    {
        "orderId": "E156281339431634",
        "price": 0.4544,
        "amount": 2,
        "turnover": 0.9088,
        "fee": 0.0009088,
        "time": 1562813427538
    }
]
```
返回值说明	

|返回字段|字段类型|说明   |
|:-----   |:------|:-----------------------------   |
| _id   |string    | key值  |
|orderId |string | 订单的orderId |
|price  |string | 价格                 |
|amount  |double | 数量                 |
|time  |long | 时间                 |
|turnover  |double | 成交额     |
|fee  |double | 手续费                 |



#### 6.撤单

请求参数	

|参数|必选|类型|Example参数|说明|
|:-----  |:-------|:-----|:-----|-----|
|orderId    |ture    |string | E156281339431634|订单id     |


请求示例:	

```javascript
# Request
POST https://api.ezb.com/exchange/order/cancel/E156281339431634?apiKey=XXXXXXXX
{

}
# Response
{
	"code": 0,
	"message": "成功",
	"data": null
}
```

###### 错误时返回：
``` javascript
{
    "code": 500,
    "message": "订单不在交易",
    "data": null
}
```
返回值说明	

|字段|描述|
|-|-|
|code|`0` 成功<br>`500` 失败 |


#### 7.获取所有资产不为0的钱包信息

请求参数：`无`


请求示例:	
> https://api.ezb.com/exchange/order/wallet?apiKey=XXXXXXXX

```javascript
# Request
GET https://api.ezb.com/exchange/order/wallet?apiKey=XXXXXXXX
{
	
}
# Response
{
	"code": 0,
	"message": "success",
	"data": [{
		"unit": "AIS",
		"balance": "1",
		"frozenBalance": "1",
		"memberId": 37965
	}, {
		"unit": "ALX",
		"balance": "0",
		"frozenBalance": "1",
		"memberId": 37965
	}, {
		"unit": "BAR",
		"balance": "0.00000000000000001",
		"frozenBalance": "0.111111111111",
		"memberId": 37965
	}, {
		"unit": "USDT",
		"balance": "9998.974",
		"frozenBalance": "1",
		"memberId": 37965
	}]
}
```
返回值说明	

|参数|类型|Example参数|说明|
|:-----  |:-----|:-----|-----|
|uint     |string | USDT|币种,`BAR`，`USDT`等    |
|balance     |string | 99 |余额    |
|frozenBalance     |string | 1|冻结余额    |
|memberId     |int | 12225|用户id    |