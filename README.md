#  [![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Dependency Status][daviddm-image]][daviddm-url]

> Weixin Pay functions for node


支持QQ群：39287176


## Install

```sh
$ npm install --save node-weixin-pay
```


## Usage


> 通用功能

1、初始化对象与基本数据

```js
var nodeWeixinPay = require('node-weixin-pay');
var nodeWeixinConfig = require('node-weixin-config');


var merchant = {
  id: process.env.MERCHANT_ID || 'id',
  key: process.env.MERCHANT_KEY || 'key'
};
var app = {
  id: process.env.APP_ID || 'appid',
  secret: process.env.APP_SECRET || 'appsecret',
  token: process.env.APP_TOKEN || 'apptoken'
};

//校验数据的正确性
nodeWeixinConfig.app.init(app);
nodeWeixinConfig.merchant.init(merchant);

var params = { openid: process.env.OPENID,
  spbill_create_ip: '1.202.241.25',
  notify_url: 'http://wx.domain.com/weixin/pay/main',
  body: '测试支付',
  out_trade_no: '111',
  total_fee: '1',
  trade_type: 'JSAPI',
  appid: app.id,
  mch_id: merchant.id,
  nonce_str: 'XjUw56N8MjeCUqHCwqgiKwr2CJVgYUpe' };
  
```

2、签名一个请求

```js

var sign = nodeWeixinPay.sign(merchant, params);
```


3、准备一个支付配置

```js
var id = 'id';
var config = nodeWeixinPay.prepay(id, app, merchant);
```


> 具体的API请求部分

4、发送统一支付请求

```js
var config = nodeWeixinPay.api.unified(config, params, function(error, data) {
});
```

5、发送订单查询请求

```js
var config = nodeWeixinPay.api.query(config, params, function(error, data) {
});
```

6、发送订单关闭请求

```js
var config = nodeWeixinPay.api.close(config, params, function(error, data) {
});
```

7、发送创建退款请求

```js
var config = nodeWeixinPay.refund.create(config, params, function(error, data) {
});
```

8、发送退款查询请求

```js
var config = nodeWeixinPay.refund.query(config, params, function(error, data) {
});
```

9、发送下载对账单请求

```js
var config = nodeWeixinPay.statements(config, params, function(error, data) {
});
```

10、发送测速报告请求

```js
var config = nodeWeixinPay.report(config, params, function(error, data) {
});
```

> 处理微信回调

10、外理回调数据

```js
nodeWeixinPay.handle(app, merchant, json, resultValidatorfunction(error, result, rawData) {
});
```



## License

MIT © [node-weixin](blog.3gcnbeta.com)


[npm-image]: https://badge.fury.io/js/node-weixin-pay.svg
[npm-url]: https://npmjs.org/package/node-weixin-pay
[travis-image]: https://travis-ci.org/node-weixin/node-weixin-pay.svg?branch=master
[travis-url]: https://travis-ci.org/node-weixin/node-weixin-pay
[daviddm-image]: https://david-dm.org/node-weixin/node-weixin-pay.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/node-weixin/node-weixin-pay
