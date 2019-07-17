# Getting Started

## API overview

The following functions can be quickly implemented through the `API`:
>- Market updates
>- Trading information
>- Match Depth 
>- Order Information
>- Place Order
>- Cancel Order

All the requests are based on the `https` protocol, and 
`contentType should be set as `application/x-www-form-urlencoded` 
in the request header.

For example:
```javascript
contentType:'application/x-www-form-urlencoded'
```

## Get API Permissions

The user's API permissions are obtained from the website's footer
`Apply API Key`.


## API概述    

通过 `API` 您可以快速实现如下功能   
> - 市场最新行情    
> - 交易信息    
> - 账户信息  
> - 买方卖方深度信息    
> - 订单信息    
> - 快速买进卖出    
> - 撤销订单


所有请求基于 `https` 协议，请求头信息中 `contentType` 需要统一设置为: `'application/x-www-form-urlencoded'`

例如：
```javascript
contentType:'application/x-www-form-urlencoded'
```


## 开启API权限    

用户的API权限在网站底部的`Apply API Key`内获取。点击`创建`即可获得
