# 币币交易REST API(行情)

## 开始使用    

REST，即Representational State Transfer的缩写，是目前最流行的一种互联网软件架构。它结构清晰、符合标准、易于理解、扩展方便，正得到越来越多网站的采用。其优点如下：    
> - 在 `RESTful` 架构中，每一个 `URL` 代表一种资源；    
> - 客户端和服务器之间，传递这种资源的某种表现层；    
> - 客户端通过四个 `HTTPS` 指令，对服务器端资源进行操作，实现“表现层状态转化”。   

建议开发者使用 `REST API` 进行币币交易或者资产提现等操作。    
    
## 请求交互    

`REST` 访问的根URL：`https://api.ezb.com/`

所有请求基于 `Https` 协议，请求头信息中 `contentType` 需要统一设置为：`application/x-www-form-urlencoded`    
	
请求交互说明    
> 1. 请求参数：根据接口请求参数规定进行参数封装。    
> 2. 提交请求参数：将封装好的请求参数通过 `POST` 或 `GET` 方式提交至服务器。    
> 3. 服务器响应：服务器首先对用户请求数据进行参数安全校验，通过校验后根据业务逻辑将响应数据以 `JSON` 格式返回给用户。    
> 4. 数据处理：对服务器响应数据进行处理。 

## API参考  

### 币币行情 API 

1.获取ezb所有币对币币行情数据  

> URL: `https://api.ezb.com/market/symbol-thumb`

请求参数: `无`

请求示例:	
> https://api.ezb.com/market/symbol-thumb

```javascript
# Request
GET https://api.ezb.com/market/symbol-thumb

# Response
[
    {
        "symbol": "ETC/BTC",
        "open": 0.000558,
        "high": 0.000579,
        "low": 0.000561,
        "close": 0.000572,
        "chg": 0.0251,
        "change": 0.000014,
        "volume": 262218.3099,
        "turnover": 546.7331247682,
        "lastDayClose": 0.000558,
        "usdRate": 5.3464554,
        "baseUsdRate": 9336.92,
        "closeStr": null,
        "isShow": 0,
        "coinScale": 2,
        "baseCoinScale": 8,
        "zone": 0
    },
    {
        "symbol": "PVS/USDT",
        "open": 0.007,
        "high": 0.007,
        "low": 0,
        "close": 0.005,
        "chg": -0.2858,
        "change": -0.002,
        "volume": 26061.8376,
        "turnover": 652.055,
        "lastDayClose": 0.007,
        "usdRate": 0.005,
        "baseUsdRate": 1,
        "closeStr": null,
        "isShow": 0,
        "coinScale": 4,
        "baseCoinScale": 4,
        "zone": 1
    }
]
```

返回值说明	

|字段|描述|
|-|-|
|symbol|币对|
|open|开盘价|
|high|最高价|
|low|最低价|
|close|最新成交价|
|chg|涨跌幅|
|change|涨跌幅（相对昨日收盘）|
|volume|24小时量|
|change|涨跌幅（相对昨日收盘）|
|turnover| |
|lastDayClose|昨日收盘价|


2.获取ezb指定币对币币行情数据 

> URL: `https://api.ezb.com/market/findThumbBySymbol?symbol=BAR/USDT`	


请求参数	

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|symbol|String|是|币对 <br>如: `eth_btc`、`zec_btc`、 `all`|
请求示例：
> https://api.ezb.com/market/findThumbBySymbol?symbol=BAR/USDT

```javascript
# Request
GET https://api.ezb.com/market/findThumbBySymbol
{
  "symbol"："BAR/USDT",
}

# Response{
    {
    "symbol": "BAR/USDT",
    "open": 0.3266,
    "high": 0.3361,
    "low": 0.319,
    "close": 0.3346,
    "chg": 0.0529,
    "change": 0.0168,
    "volume": 14489674.8038,
    "turnover": 7736722.08326843,
    "lastDayClose": 0.3178,
    "usdRate": 0.3346,
    "baseUsdRate": 1,
    "closeStr": null,
    "isShow": 1,
    "coinScale": 4,
    "baseCoinScale": 4,
    "zone": 0
	}
}
```

返回值说明

|字段|描述|
|-|-|
|symbol|币对|
|open|开盘价|
|high|最高价|
|low|最低价|
|close|最新成交价|
|chg|涨跌幅|
|change|涨跌幅（相对昨日收盘）|
|volume|24小时量|
|change|涨跌幅（相对昨日收盘）|
|turnover| |
|lastDayClose|昨日收盘价|


3.获取ezb市场深度

URL: `https://api.ezb.com/market/exchange-plate-full?symbol=BAR/USDT`	

请求参数	

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|symbol|String|是|币对如 `BAR/USDT`|


请求示例
> https://api.ezb.com/market/exchange-plate-full?symbol=BAR/USDT

```javascript
# Request
GET  "https://api.ezb.com/market/exchange-plate-full"
{
  "symbol"："BAR/USDT",
}
# Response
{
    "ask": {
        "direction": "SELL",
        "highestPrice": 1254,
        "items": [
            {
                "price": 0.33,
                "amount": 17831.9014
            },
            {
                "price": 0.3308,
                "amount": 900
            }
        ],
        "lowestPrice": 0.33,
        "maxAmount": 309977.7161,
        "minAmount": 309977.7161,
        "symbol": "BAR/USDT"
    },
    "bid": {
        "direction": "BUY",
        "highestPrice": 0.3298,
        "items": [
            {
                "price": 0.3298,
                "amount": 11661.84
            },
            {
                "price": 0.3297,
                "amount": 16384.2789
            }
        ],
        "lowestPrice": 0.01,
        "maxAmount": 3961739.5338,
        "minAmount": 3961739.5338,
        "symbol": "BAR/USDT"
    }
}
```

返回值说明:
```
ask :卖方深度
bid :买方深度
```



4.获取EZB历史交易信息

URL: `https://api.ezb.com/market/latest-trade?symbol=XXX&size=XXX`	

请求参数	

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|symbol|String|是|币对 <br>如 `BAR/USDT`|
|size|Integer|是|返回的条数，入10|

请求示例
> https://api.ezb.com/market/latest-trade?symbol=BAR/USDT&size=4

```javascript
# Request
GET https://api.ezb.com/market/latest-trade
{
  "symbol"："BAR/USDT",
  "size"："4"
}
# Response[
    {
        "symbol": null,
        "price": 0.3351,
        "priceStr": null,
        "amount": 9454.7369,
        "amountStr": null,
        "buyTurnover": null,
        "sellTurnover": null,
        "direction": "BUY",
        "buyOrderId": null,
        "sellOrderId": null,
        "time": 1563338480253
    },
    {
        "symbol": null,
        "price": 0.3344,
        "priceStr": null,
        "amount": 1272,
        "amountStr": null,
        "buyTurnover": 425.3568,
        "sellTurnover": 425.3568,
        "direction": "SELL",
        "buyOrderId": "E207474654271512576",
        "sellOrderId": "E207477203171024896",
        "time": 1563338419983
    }
]
```

返回值说明:

|字段|描述|
|-|-|
|time|交易时间|
|amount|交易数量|
|price|交易价格|
|direction|BUY/SELL|



5.获取K线数据

URL: `https://api.ezb.com/market/history?symbol=BAR/USDT&from=1558158143000&to=1563342143457&resolution=60`	

请求参数	

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|symbol|String|是|币对如 `BAR/USDT`|
|from|long|是|开始时间，时间戳，精确到毫秒|
|to|long|是|结束时间，时间戳，精确到毫秒|
|resolution|String|是|`1`：1分钟<br>`5`：5分钟<br>`15`：15分钟<br>`30`：30分钟<br>`1H`：1小时<br>`1D`：1日<br>`1W`：1周<br>`1M`：1月<br>|

请求示例
> http://api.ezb.com/market/history?symbol=BAR/USDT&from=1558158143000&to=1563342143457&resolution=60

```javascript
# Request
GET https://api.ezb.com/market/history
{
  "symbol"："BAR/USDT",
  "from"："1558158143000",
  "to"："1563342143457",
  "resolution"："60"
}
# Response
[
    [
        1558159200000,
        0.4038,
        0.405,
        0.4031,
        0.404,
        465919.6251
    ],
    [
        1558162800000,
        0.4046,
        0.4059,
        0.4022,
        0.4048,
        493988.8505
    ]
]
```

返回值说明:

|字段|描述|
|-|-|
|1558159200000|时间戳|
|0.4038|开|
|0.405|高|
|0.4031|低|
|0.404|收|
|465919.6251|交易量|