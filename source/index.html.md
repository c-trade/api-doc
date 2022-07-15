---
title: C-Trade API 

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the official documentation for the C-Trade APIs and Websocket! Here you can find details on how to access all of our endpoints, their respective expected outputs, and possible errors you may encounter.

# REST API 

HTTP-based API with full trading and asset management functionality, with public orderbook and trades data as well as private account data and order management.

REST endpoint URL: https://api.c-trade.com

Requests and responses use JSON.

# Market Data Endpoints

## Get Contracts Menu

```shell
curl --location --request GET 'https://api.c-trade.com/public/contracts-menu' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "BTC": [
        {
          "name": "BTCUSD",
          "description": "A BTCUSD perpetual contract has no expiry date. It is derived from BTC and priced on the .BTCUSD Index. Each contract is worth 1 USD in BTC. Funding is paid and received every 8 hours - 00:00 ,08:00, 16:00 UTC time.",
          "type": "InversePerpetual",
          "expiryTS": 0,
          "settledIn": "BTC",
          "dependentOnIndex": ".BTCUSD",
          "underlyingBaseCurrency": "BTC",
          "underlyingQuoteCurrency": "USD",
          "minPriceINC": 0.5,
          "makerFee": -0.025,
          "takerFee": 0.075,
          "maxSize": 10000000,
          "minSize": 1,
          "sizePrecision": 1,
          "sizeIncrement": 0.1,
        }
      ],
    }
  }
}
```

This endpoint retrieves contracts menu.

### HTTP Request

`GET https://api.c-trade.com/public/contracts-menu`


## Get Contracts

```shell
curl --location --request GET 'https://api.c-trade.com/public/contracts' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "BTCUSD": [
        {
          "contract": "BTCUSD",
          "ticker_id": "BTC-USD",
          "base_currency": "BTC",
          "target_currency": "USD",
          "last_price": 15250,
          "target_volume": 0,
          "bid": 16325.5,
          "ask": 16326,
          "high": 15250,
          "low": 15250,
          "product_type": "InversePerpetual",
          "open_interest": 78039309,
          "index_price": 16326.21,
          "index_name": ".BTCUSD",
          "index_currency": null,
          "start_timestamp": 0,
          "end_timestamp": 0,
          "funding_rate": 0.0001,
          "next_funding_rate": 0.0001,
          "next_funding_rate_timestamp": 1605283200000,
          "maker_fee": -0.025,
          "taker_fee": 0.075,
          "base_volume": 0
        }
      ]
    }
  }
}
```

This endpoint retrieves all contracts details.

### HTTP Request

`GET https://api.c-trade.com/public/contracts`

## Get Contract Detail

```shell
curl --location --request GET 'https://api.c-trade.com/public/contracts/BTCUSD' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
    "success": {
        "code": 100,
        "message": "Success",
        "data": {
            "name": "BTCUSD",
            "description": "A BTCUSD perpetual contract has no expiry date. It is derived from BTC and priced on the .BTCUSD Index. Each contract is worth 1 USD in BTC. \n\nFunding is paid and received every 8 hours - 00:00 ,08:00, 16:00 UTC time.",
            "groupName": "BTC",
            "underlyingQuoteCurrency": "USD",
            "underlyingBaseCurrency": "BTC",
            "baseBON": ".BTCBON",
            "quoteBON": ".USDBON",
            "settledIn": "BTC",
            "type": 2,
            "makerFee": -0.0250,
            "takerFee": 0.0750,
            "settlementFee": 0.0000,
            "maxPrice": 1000000.0000000000,
            "minPrice": 0.5000000000,
            "refrenceUrl": "",
            "nextFundingTS": 946684800000,
            "premium": 0.0000,
            "longFundingRate": 0.0000,
            "shortFundingRate": 0.0000,
            "fundingInterval": 480,
            "addedOnTS": 0,
            "futureSettlementTS": 0,
            "status": true,
            "dependentOnIndex": ".BTCUSD",
            "sortOrder": 1,
            "minSize": 1,
            "maxSize": 1000000,
            "sizePrecision": 1,
            "sizeIncrement": 0.1,
            "markPriceDecimalScale": 2,
            "fundingRateDecimalScale": 8,
            "impactMarginSize": 0.1000,
            "strike": 0.00000000,
            "isCall": false,
            "settlementIndex": "",
            "fundingIntervalOffset": 0,
            "adlPerc": 50.0000,
            "adlMinBalance": -2.0000000000,
            "markPriceInterval": 5,
            "minRiskLimit": 0,
            "tbl_CurrencySetting_SettledIn": null,
            "tbl_Index_Master_DependentOnIndex": null,
            "tbl_ReferralComissions": null,
            "tbl_Positions": null,
            "tbl_PremiumIndices_Master": null,
            "tbl_MarkPrices": null,
            "tbl_FundingRates": null,
            "tbl_RiskLimits_Master": null,
            "tbl_Customers_RiskLimit": null,
            "tbl_Customers_Leverage": null
        }
    }
}
```

This endpoint retrieves a specific contract detail.

### HTTP Request

`GET https://api.c-trade.com/public/contracts/<contractsymbol>`

### URL Parameters

Parameter | Description
--------- | -----------
contractsymbol | The symbol of the contract

## Get Charts

```shell
curl --location --request GET 'https://api.c-trade.com/public/charts/BTCUSD/1M?limit=100&ts=1574813820000'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      [
        1575352620000,
        0.02034625,
        0.0203485,
        0.02035075,
        0.0203445,
        0
      ],
      [
        1575352560000,
        0.0203465,
        0.02034625,
        0.0203465,
        0.02033875,
        0
      ],
      [
        1575352500000,
        0.0203465,
        0.0203465,
        0.020355,
        0.020346,
        0
      ],
      [
        1575352440000,
        0.020346,
        0.0203465,
        0.0203475,
        0.020342,
        0
      ],
      [
        1575347400000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ]
    ]
  }
}
```

This endpoint retrieves charts of a specific contract detail.

### HTTP Request

`GET https://api.c-trade.com/public/charts/<contractsymbol>/<interval>`

### URL Parameters

Parameter | Description
--------- | -----------
contractsymbol | The symbol of the contract
interval | The interval of charts

### Request Parameters

Parameter | Required | Description
--------- | ----------- | -----------
limit | false | Limit for data size per page, default = 500, max = 1000
ts | false | From timestamp in milliseconds, default = current time


## Get funding history

```shell
curl --location --request GET 'https://api.c-trade.com/public/funding-history' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:
> by default user will get the first 100 reverse results

```json
{
    "success": {
        "code": 100,
        "message": "Success",
        "data": [
            {
                "contractName": "BTCUSD",
                "rate": 0.00010000,
                "ts": 1595404800000
            },
            {
                "contractName": "BTCUSD",
                "rate": 0.00010000,
                "ts": 1595376000000
            }
        ]
    }
}
```

This endpoint retrieves indices list.

### HTTP Request

`GET https://api.c-trade.com/public/indices-hierarchy`

### Request Payload

FieldName | Mandatory | Valid Values | Default Values
--------- | ----------- | ----------- | -----------
timestamp | YES | BTCUSD | No value
recvWindow | NO	| Number of records | 100
Contract | NO | Valiid Timestamp | 0

## Get Indices Details

```shell
curl --location --request GET 'https://api.c-trade.com/public/indices-detailed-breakdown/.BTCUSD/1'
```

> The above command returns JSON structured like this:

```json
{
    "success": {
        "code": 100,
        "message": "Success",
        "data": {
            "composite_breakdown": [
                {
                    "ts": 1595415300000,
                    "indexTicker": null,
                    "exchange": "kraken",
                    "price": 9344.6000000000,
                    "weightage": 25.00
                },
                {
                    "ts": 1595415300000,
                    "indexTicker": null,
                    "exchange": "gemini",
                    "price": 9345.6700000000,
                    "weightage": 0.00
                },
                {
                    "ts": 1595415300000,
                    "indexTicker": null,
                    "exchange": "coinbase pro",
                    "price": 9344.0500000000,
                    "weightage": 25.00
                },
                {
                    "ts": 1595415300000,
                    "indexTicker": null,
                    "exchange": "bittrex",
                    "price": 9348.3600000000,
                    "weightage": 25.00
                },
                {
                    "ts": 1595415300000,
                    "indexTicker": null,
                    "exchange": "bitstamp",
                    "price": 9345.7800000000,
                    "weightage": 25.00
                },
            ],
            "indices_using_this": [],
            "contracts_using_this": [
                "BTCUSD"
            ]
        }
    }
}
```

This endpoint retrieves details of a specific index.

### HTTP Request

`GET https://api.c-trade.com/public/public/indices-detailed-breakdown/<index>/<time>`

### URL Parameters

Parameter | Description
--------- | -----------
index | The index 
time | time for the chart data grouping(in minutes)

## Get Index Data

```shell
curl --location --request GET 'https://api.c-trade.com/public/indices/BTCUSD/1?limit=500&ts=1575465605000'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "1575526080000": 0.0198514792,
      "1575526020000": 0.0198466875,
      "1575525960000": 0.0198418708,
      "1575525900000": 0.0198365833,
      "1575525840000": 0.0198352625,
      "1575525780000": 0.0198287083,
      "1575525720000": 0.0198319167,
      "1575525660000": 0.0198282167,
      "1575525600000": 0.0198256625,
      "1575525540000": 0.0198257458,
      "1575525480000": 0.0198243708,
      "1575525420000": 0.0198236875,
      "1575525360000": 0.0198235625,
      "1575525300000": 0.0198266958,
      "1575525240000": 0.019828125,
      "1575525180000": 0.0198328417,
      "1575525120000": 0.0198271958,
      "1575525060000": 0.0198272042,
      "1575525000000": 0.0198370917,
      "1575524940000": 0.0198313875,
    }
  }
}
```

This endpoint retrieves data of a specific index.

### HTTP Request

`GET https://api.c-trade.com/public/indices/<index>/<interval>?limit=<limit>&ts=<ts>`

### URL Parameters

Parameter | Description
--------- | -----------
index | The index 
interval | The interval of charts

### Request Parameters

Parameter | Required | Description
--------- | ----------- | -----------
limit | false | Limit for data size per page, default = 500, max = 1000
ts | false | From timestamp in milliseconds, default = current time

## Get Index Chart OHLC

```shell
curl --location --request GET 'https://api.c-trade.com/public/indices-charts/.BTCUSD/1M?limit=1000&ts=1575465605000'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      [
        1575465540000,
        0.0201525,
        0.02013525,
        0.0201535,
        0.020135
      ],
      [
        1575465480000,
        0.020147,
        0.0201525,
        0.0201525,
        0.0201455
      ],
      [
        1575465420000,
        0.02016475,
        0.020147,
        0.0201645,
        0.020147
      ],
      [
        1575465360000,
        0.020161,
        0.02016475,
        0.020165,
        0.020161
      ],
      [
        1575465300000,
        0.0201675,
        0.020161,
        0.0201675,
        0.020161
      ]
    ]
  }
}
```

This endpoint retrieves index chart OHLC of a specific index.

### HTTP Request

`GET https://api.c-trade.com/public/indices-charts/<index>/<interval>?limit=<limit>&ts=<ts>`

### URL Parameters

Parameter | Description
--------- | -----------
index | The index 
interval | The interval of charts

### Request Parameters

Parameter | Required | Description
--------- | ----------- | -----------
limit | false | Limit for data size per page
ts | false | From timestamp in milliseconds

## Get Order Book

```shell
curl --location --request GET 'https://api.c-trade.com/public/orderbook/BTCUSD/5'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "ts": 1605262933633794000,
      "bids": [
        [
          16325.5,
          202599
        ],
        [
          16325,
          227408
        ],
        [
          16324.5,
          206122
        ],
        [
          16324,
          152706
        ],
        [
          16323.5,
          203795
        ]
      ],
      "asks": [
        [
          16338,
          44485
        ],
        [
          16337.5,
          42068
        ],
        [
          16337,
          42591
        ],
        [
          16336.5,
          36627
        ],
        [
          16336,
          46735
        ]
      ]
    }
  }
}
```

This endpoint retrieves a specific order book.

### HTTP Request

`GET https://api.c-trade.com/public/orderbook/<contractsymbol>/<ordernumber>`

### URL Parameters

Parameter | Description
--------- | -----------
contractsymbol | The symbol of the contract
ordernumber | The specific ordernumber

# Orders/Wallet Endpoints

## HMAC Signature Calculation

```shell
// Example for calculating signature message for a POST Request to {{base_url}}/api/open-orders
{
    timestamp:1587820973,
    recvWindow:10000,
    orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'
}

signature_message = "POST" + "\n" + "/api/open-orders" + "\n" + "1587820973" + "\n" + "{timestamp:1587820973,recvWindow:10000,orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'}"
signature = HMAC(signature_message)

// computed signature should be Hexadecimal equivalent of the HMAC signature. 
```
```python
# Example for calculating signature message for a POST Request to {{base_url}}/api/open-orders
import hmac
import json
import hashlib

def CalcHMAC_API(method, url, timestamp, payload, key):
  res = ''
  res += method.upper() + '\n'
  res += url + '\n'
  res += str(timestamp) + '\n'
  res += json.dumps(payload, separators=(',', ':'))
  h = hmac.new(bytes(key, 'utf-8'), bytes(res, 'utf-8'), hashlib.sha256)
  return h.hexdigest()

apiSecret = "xxxxxxxxxxxxxxxxx"
hamc = CalcHMAC_API("POST", "/api/open-orders", "1587820973", "{timestamp:1587820973,recvWindow:10000,orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'}", apiSecret)

# computed signature should be Hexadecimal equivalent of the HMAC signature. 
```
```javascript
var data = {
  timestamp:1593093984,
  Contract:'BTCUSD'
}

var signature_message = "POST" + "\n" + "/api/position-details" + "\n" + "1593093984" + "\n" + JSON.stringify(data);
var signature = sha256.hmac(secret_key, signature_message);

// computed signature should be Hexadecimal equivalent of the HMAC signature. 
```

Message authentication signature. The request message is hashed with the API secret key using SHA256 algorithm. The structure of the message:

* Request method. (e.g. "GET or "POST")
* Request URI including the query parameters for GET.
* The unix timestamp value
* The payload in JSON format only for POST.
* To ensure the signature is successfully validated, please be aware of the following:
    * Each piece of information in the signature message should be separated by a new line. (see the example)
    * The payload should not contain any whitespace between the names and values
    * The Request URI should not contain the host name. e.g. `/api/orders` instead of `https://myexchange.com/api/orders`


## POST New Order

```shell
curl --location --request POST 'https://api.c-trade.com/api/new-order' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: FBDF9E1CC798C5897D6E32A2ED336B762C3E3565ABE16A482DC0E30A2F775227B18F0D93E77F38BB6397C73FA814E165D237B85AE01CA6510E9DE528ADA29DB2' \
--data-raw '{
    "symbol": "BTCUSD",
    "side": "SELL",
    "orderQty": 1,
    "price": 100,
    "stopPrice": 0,
    "orderType": "LIMIT",
    "timeinForce": "DO"
}'
```

> The above command returns JSON structured like this:

```json
{
    "success": {
        "code": 100,
        "message": "Success",
        "data": {
            "natsPayload": {
                "symbol": "BTCUSD",
                "side": 2,
                "type": 2,
                "limitPrice": 100.0,
                "stopPrice": 0.0,
                "orderID": "62da8a28-f47b-46c6-a7e0-f0f87696e0e1",
                "userID": "123456789ABCDE",
                "stopOrderActivated": false,
                "status": 1,
                "remaining": 1.0,
                "takerFee": 0.075,
                "makerFee": -0.025,
                "size": 1.0,
                "liquidationPrice": 20000.0,
                "isReduceOnly": false,
                "isCloseOnTrigger": false,
                "isHiddenOrder": false,
                "isPostOnly": false,
                "timeInForce": 2,
                "cancellationCounter": 0,
                "triggerType": 0,
                "balance": 114.87088463,
                "orderMargin": 0.010015,
                "orderValue": 0.01,
                "userContract": {
                    "user": "123456789ABCDE",
                    "contract": "BTCUSD"
                }
            },
            "mtCalc": {
                "liquidationPrice": 20000.0,
                "maintainanceMarginPerc": 0.5,
                "initialMarginPerc": 100.0,
                "leverage": 1.0,
                "initialCollateral": 0.01,
                "takerfeePerc": 0.075,
                "fundingRate": 0.00115296,
                "markPrice": 19824.83,
                "orderSize": 0.01,
                "transactionFee": -7.5E-06,
                "twoWayFee": 1.5E-05,
                "maintainanceMargin": 5E-05,
                "costNormal": 0.010015,
                "costAbnormal": 0.01001455,
                "cost": 0.010015,
                "pLatMarkPrice": -0.00994955,
                "costOfPlacingNewOrder": 0.0,
                "balance": 0.0
            }
        }
    }
}
```

This endpoint create a new order

### HTTP Request

`POST https://api.c-trade.com/api/new-order`

Note: place order using api-key and HMAC authentication.

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
symbol | Yes | BTCUSD
side| Yes | BUY,SELL
orderQty | Yes | Integer and Greater than Zero
price | Yes | Decimal and Greater than Zero
stopPrice | Yes |	Decimal and Greater than Zero
orderType	| Yes	| LIMIT
timeinForce	| NO |	GTC/DO/IOC/FOK
triggerType	| NO | 	MarkPrice
isReduceOnly | NO | True/False
IsCloseOnTrigger | NO | True/False
IsPostOnly | NO | True/False

## POST Cancel Order

```shell
curl --location --request POST 'https://api.c-trade.com/api/cancel-order' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: EF950375703CE12226EE653B78B5154B3563ECFA0C458C0476025C4246B0CCBB52E2987CF2E95BDEB6D5A8E01BF87302DF0C8EE601DC4716B918979F27451C89' \
--data-raw '{
	"timestamp":"1587820973",
	"recvWindow":10000,
	"orderID":"3ec4facb-c2bf-4bdf-8adf-b11e2851d235"
}'
```

This endpoint cancel a new order

```json
{
  "success": [
    {
      "success": {
        "code": 100,
        "message": "Success",
        "data": {
          "userID": "37FB2199FDF244",
          "order_id": "d45e47a8-24f1-4718-b350-77798a91f67a",
          "symbol":"BTCUSD"
        }
      }
    }
  ]
}

### HTTP Request

`POST https://api.c-trade.com/api/cancel-order`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
orderID | Yes | string

## POST All Orders

```shell
curl --location --request POST 'https://api.c-trade.com/api/new-order' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: FBDF9E1CC798C5897D6E32A2ED336B762C3E3565ABE16A482DC0E30A2F775227B18F0D93E77F38BB6397C73FA814E165D237B85AE01CA6510E9DE528ADA29DB2' \
--data-raw '{
    "symbol": "BTCUSD",
    "side": "SELL",
    "orderQty": 1,
    "price": 100,
    "stopPrice": 0,
    "orderType": "LIMIT",
    "timeinForce": "DO"
}'
```

This endpoint post all order // todo

### HTTP Request

`POST https://api.c-trade.com/api/all-orders`

Note: place order using api-key and HMAC authentication.

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
DateTo | NO | string 'yyyy/mm/dd'
DateFrom | NO | string 'yyyy/mm/dd'
Contract | NO | BTCUSD
OrderStatus | NO | true or false
Limit | NO | MAX:1000
timestamp | YES | Current UTC TS
recvWindow | YES | Default: 30sec ,any integar value

### Response

FieldName |	Short Description
--------- | -----------
sym | Symbol or ContractName
o | Orderid
sp | Stop price
p | Price
r |	Remaining
s | Order Side "S": Sell, "B": Buy
ts | Accepted Timestamp
u | UserID
q | Quantity or Size
st | Order Status
tif | Time in force
t | Order Type
v | Order Value
fp | Filled Price
odst | Order detailed Status

## POST My Trade History

```shell
curl --location --request POST 'https://api.c-trade.com/LP/my-trade-history' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: 14F846BFC247D40B56A71547888C0E51D226E835683A530BE55A27ED93C3B6F1681C4F8EFED8BAD949B9C8A12D8E323A931FD33FD54B703D23367E272E662ECB' \
--data-raw '{
	"side":"sell",
	"symbol":"",
	"orderid":""
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      {
        "sym": "BTCUSD",
        "ts": 1583394834,
        "o": "d3e87c02-d02d-4078-aef9-b4e2e29fcf51",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8800,
        "ep": 8800,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "BTCUSD",
        "ts": 1583403228,
        "o": "d145b742-716e-470a-bcaf-2052ea918be6",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "BTCUSD",
        "ts": 1583404613,
        "o": "01bf5823-b4be-41b3-83bd-98bb767ab15f",
        "q": 20,
        "eq": 20,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "BTCUSD",
        "ts": 1583404622,
        "o": "6efbd950-2bd0-4d84-88a8-0871184cbbb2",
        "q": 20,
        "eq": 20,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "BTCUSD",
        "ts": 1583404742,
        "o": "bc2aab73-ad09-4a76-a7be-f54a5e4a8711",
        "q": 10,
        "eq": 10,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "BTCUSD",
        "ts": 1583408427,
        "o": "1a1052d7-5511-496b-addd-b54cc4c2a3a8",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      }
    ]
  }
}      
```


This endpoint post my trade history  //todo

### HTTP Request

`POST https://api.c-trade.com/api/my-trade-history`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
DateTo | NO | string 'yyyy/mm/dd'
DateFrom | NO | string 'yyyy/mm/dd'
Contract | NO | BTCUSD

### Response

FieldName |	Short Description
--------- | -----------
sym | Symbol or ContractName
ts | Timestamp
o | Orderid
q	| Quantity or Size
eq | Entry Quantity
v	| Order Value
t	| Order Type
sp | Stop price
p	| Price
ep | Entry Price
r	| Remaining
s	| Order Side "S": Sell, "B": Buy
tif	| Time in force

## POST My Trade History

```shell
curl --location --request POST 'https://api.c-trade.com/api/open-orders' \
--header 'apiKey: cee3d621-86b6-4db2-85a8-f69db6b4cc99' \
--header 'Content-Type: application/json' \
--header 'HMAC: eedcfe4022dce12898e9171327de3daa3e1339dd5f788a778effdc85d02456b5' \
--data-raw '{
	"timestamp":"1590230834",
	"recvWindow":10000,
	"Contract":"BTCUSD"
}'
```

This endpoint post open orders  //todo

### HTTP Request

`POST https://api.c-trade.com/api/open-orders`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
Contract | NO | BTCUSD

## POST Wallet Balance

```shell
curl --location --request POST 'https://api.c-trade.com/api/wallet-balance' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: 56E8B6C4AE66DBFFF1C11E79C03F9938E9C8A0E1B4005DFEE7769700B861A9B411C9FDF7ACB048F643E793A9890B01410F1A82B69C87C5920BDB54E33DA3FDF8' \
--data-raw '{
	"timestamp":"1587820973",
	"recvWindow":10000,
	"currency":"BTC"
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      {
        "currency": "BTC",
        "balance": 25.90798327
      }
    ]
  }
}
```

This endpoint get wallet balance

### HTTP Request

`POST https://api.c-trade.com/api/wallet-balance`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
Contract | NO | BTCUSD

## POST Cancel All Orders

```shell
curl --location --request POST 'https://api.c-trade.com/api/cancel-all-orders' \
--header 'Content-Type: application/json' \
--header 'apiKey: cee3d621-86b6-4db2-85a8-f69db6b4cc99' \
--header 'HMAC: 90e665bf0ab0f2867bc9472a8762ff336a984d4361ec819e0beac328238852bf' \
--data-raw '{
	"timestamp":"1590230603",
	"recvWindow":1000
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": [
    {
      "success": {
        "code": 100,
        "message": "Success",
        "data": {
          "userID": "332424",
          "order_id": "d45e47a8-24f1-4718-b350-77798a91f67a",
          "symbol":"BTCUSD"
        }
      }
    }
  ],
  "error": []
}
```

This endpoint cancel all orders.

### HTTP Request

`POST https://api.c-trade.com/api/cancel-all-orders`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
Contract | NO | BTCUSD

## POST Order Detail

```shell
curl --location --request POST 'https://api.c-trade.com/api/order-detail' \
--header 'apiKey: bd9fb587-7a0c-437e-b8ca-57c05ee52ad6' \
--header 'Content-Type: application/json' \
--header 'HMAC: bcd91b4b7ef7cd6a4406de364ef4daaad279b7a9db9559f953ec6ec4eb447186' \
--data-raw '{
	"timestamp":"1592471370",
	"recvWindow":10000,
	"Contract":"BTCUSD"
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      {
        "sym": "BTCUSD",
        "ts": 1592199466766,
        "o": "dc5e773d-f304-4c97-9d29-baa9c5fb2884",
        "u": "332424",
        "sp": 0,
        "p": 100,
        "r": 1,
        "s": "S",
        "q": 1,
        "st": true,
        "tif": "DO",
        "t": "Limit",
        "odst": "Rejected",
        "v": 0.01,
        "fp": 0,
        "trg": false,
        "trgtyp": 0
      }
    ]
  }
}
```

This endpoint get order detail

### HTTP Request

`POST https://api.c-trade.com/api/order-detail`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
Contract | NO | BTCUSD

### Response
FieldName | Short Description 
--------- | ----------- 
sym | Contract Name
ts | Timestamp 
o | OrderId 
u | Order-side "S": Sell, "B": Buy
sp | Stop Price
p | Price
r | Remaining
s | Order side
q | Size or quantity
st | Non-active statuys
tif | Time in Force
t | Order type
odst | Order detailed Status : Accepted, PartiallyFilled, Filled, Cancel, Rejected
v | Value
fp | Full Price
trg | Trigger
trgtyp | Trigger : 0(Last Price), 1(Mark Price), 2(Index Price)

## POST Update Order

```shell
curl --location --request POST 'https://api.c-trade.com/api/update-order' \
--header 'apiKey: bd9fb587-7a0c-437e-b8ca-57c05ee52ad6' \
--header 'Content-Type: application/json' \
--header 'HMAC: bcd91b4b7ef7cd6a4406de364ef4daaad279b7a9db9559f953ec6ec4eb447186' \
--data-raw '{
    "timestamp":"1592199378",
	  "recvWindow":10000,
    "OrderID":"fc963bbf-59fe-4915-aedd-ce7a98a97e91",
	  "size":2,
	  "price":"",
	  "stopPrice":""
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "natsPayload": {
        "symbol": "XBTUSD",
        "size": 2,
        "side": 1,
        "type": 2,
        "timeInForce": 2,
        "limitPrice": 1700,
        "stopPrice": 0,
        "trailingAmount": 0,
        "orderID": "11446e69-fbe4-4130-a628-45328dd99463",
        "userID": "332424",
        "balance": 31.35895787,
        "orderMargin": 0.000012,
        "liquidationPrice": 0.5,
        "takerFee": 0.011,
        "makerFee": -0.025,
        "filledPrice": 0,
        "orderValue": 0.00117647,
        "isReduceOnly": false,
        "isCloseOnTrigger": false,
        "isHiddenOrder": false,
        "isPostOnly": false,
        "triggerType": 0
      },
      "mtCalc": {
        "liquidationPrice": 0.5,
        "maintainanceMarginPerc": 0.5,
        "initialMarginPerc": 1,
        "leverage": 0,
        "initialCollateral": 0.00001176,
        "takerfeePerc": 0.011,
        "fundingRate": -0.027,
        "markPrice": 9227.65,
        "orderSize": 0.00117647,
        "transactionFee": -1.2e-7,
        "twoWayFee": 2.4e-7,
        "maintainanceMargin": 0.00000588,
        "costNormal": 0.000012,
        "costAbnormal": -0.00095361,
        "cost": 0.000012,
        "pLatMarkPrice": 0.00095973,
        "costOfPlacingNewOrder": 0
      }
    }
  }
}
```

This endpoint get order detail

### HTTP Request

`POST https://api.c-trade.com/api/update-order`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO | Default is 10 seconds
OrderID | YES | String
size | YES/NO	| Integer and Greater than Zero
price | YES/NO | Decimal and Greater than Zero
stopPrice | YES/NO | Decimal and Greater than Zero

Note :Between size or price or stopPrice one of them is required in requested payload.

## POST Position Details

```shell
curl --location --request POST 'https://api.c-trade.com/api/position-details \
--header 'apiKey: bd9fb587-7a0c-437e-b8ca-57c05ee52ad6' \
--header 'Content-Type: application/json' \
--header 'HMAC: bcd91b4b7ef7cd6a4406de364ef4daaad279b7a9db9559f953ec6ec4eb447186' \
--data-raw '{
    "timestamp":"1593093984",
	  "recvWindow":10000,
    "Contract":"XBTM20"
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      {
        "account": "332424",
        "symbol": "XBTM20",
        "underlying": ".BXBT",
        "settleCurrency": "BTC",
        "baseCurrency": "BTC",
        "quoteCurrency": "USD",
        "type": 3,
        "size": 1,
        "markValue": 0.00010857,
        "avgEntryPrice": 9420.5,
        "markPrice": 9210.5,
        "liquidationPrice": 4722.12,
        "positionMargin": 0.00010381,
        "unrealizedPnl": -0.00000242,
        "realizedPnl_Fee": -8e-8,
        "realizedPnl_Funding": 0,
        "realizedPnl_Earning": 0,
        "bankruptPrice": 4710.31,
        "timeStamp": 1593091762,
        "initial": {
          "leverage": 1,
          "initialMarginPercent": 0,
          "maintenanceMarginPercent": 0.005
        }
      }
    ]
  }
}
```
### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
Contract | NO | BTCUSD

# WebSocket API

## Establish a Connection

C-trade offers a complete pub/sub API with table diffing over WebSocket. You may subscribe to real-time changes on any available table.

Connect your websocket client to `ws.c-trade.com/updatesV2`
Command: `{ operation": "argument" }`

### Operation

Operation |
--------- |
subscribe |
authorization:token | 
query	| 
logout |	
unsubscribe |	

### Argument

Events | Instruments 
--------- | ----------- 
trades | BTCUSD
orderbook | BTC 
mytrades | 
myorders | 
positions |

## Establish a Connection using API key

An APIkey based authentication request will require HMAC Signature for following payload

```json
{
  "apikey" : "user's API public key here",
  "timestamp": 1586860702
}
```

* if the authentication request comes after 10 seconds from the time (timestamp) it mentions in the request payload, we will not serve it.
* HMAC Signature will be computed using your API Secret Key.
* You will append computed HMAC Signature in the payload as shown below

```json
{
  "apikey" : "dbea9305-5289-48a1-a0a3-6558f28aaa00",
  "timestamp": 1586860702,
  "signature": "computed hmac for above goes here"
}           
```

## HMAC Signature Calculation

Message authentication signature. The request message is hashed with the API secret key using SHA256 algorithm. The structure of the message:

* Request URI i.e. /updatesV2
* The unix timestamp value
* The payload in JSON format.
* To ensure the signature is successfully validated, please be aware of the following:
    * Each piece of information in the signature message should be separated by a new line. (see the example)
    * The payload should not contain any whitespace between the names and values
    * The Request URI should not contain the host name. e.g. '/updatesV2' instead of 'https://myexchange.com/updatesV2'

```shell
// Example for calculating signature message for a POST Request to {{base_url}}/api/open-orders
{
    timestamp:1587820973,
    recvWindow:10000,
    orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'
}

signature_message = "POST" + "\n" + "/api/open-orders" + "\n" + "1587820973" + "\n" + "{timestamp:1587820973,recvWindow:10000,orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'}"
signature = HMAC(signature_message)

// computed signature should be Hexadecimal equivalent of the HMAC signature. 
```
```python
# Example for calculating signature message for a POST Request to {{base_url}}/api/open-orders
import hmac
import json
import hashlib

def CalcHMAC_API(method, url, timestamp, payload, key):
  res = ''
  res += method.upper() + '\n'
  res += url + '\n'
  res += str(timestamp) + '\n'
  res += json.dumps(payload, separators=(',', ':'))
  h = hmac.new(bytes(key, 'utf-8'), bytes(res, 'utf-8'), hashlib.sha256)
  return h.hexdigest()

apiSecret = "xxxxxxxxxxxxxxxxx"
hamc = CalcHMAC_API("POST", "/api/open-orders", "1587820973", "{timestamp:1587820973,recvWindow:10000,orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'}", apiSecret)

# computed signature should be Hexadecimal equivalent of the HMAC signature. 
```
```javascript
var data = {
  timestamp:1593093984,
  Contract:'BTCUSD'
}

var signature_message = "POST" + "\n" + "/api/position-details" + "\n" + "1593093984" + "\n" + JSON.stringify(data);
var signature = sha256.hmac(secret_key, signature_message);

// computed signature should be Hexadecimal equivalent of the HMAC signature. 
```

# WebSocket Market Data Stream

Authentication is not required for market data stream

## Order Book (Snapshot)

Command:`{ "op": "query", "args": ["orderbook:BTCUSD"] }`

> Example Response

> //Order book Snapshot for BTCUSD contract at 1592828870981575587 timestamp

```json
     {
      "data": {
        "ts": 1592828870981575587,
        "type": "snapshot",
        "buy": {
          "8944": 50000.0,
          "8945": 50000.0,
          "8946": 50000.0,
          "8947": 50000.0
          },
        "sell": {
          "10000": 2651.0,
          "9043": 30330.0,
          "9044": 50000.0,
          "9045": 590261.0
          }
        },
      "event": "orderbook",
      "instrument": "BTCUSD"
     }
```

## Order Book (Ticker)

Command:`{ "op": "subscribe", "args": ["orderbook:BTCUSD"] }`

> Example Response

> //Order book Ticker for BTCUSD contract at 1592829185415529209 timestamp

```json
{
  "data": {
    "ts": 1592829185415529209,
    "type": "ticker",
    "buy": {
      "inserted": {},
      "changed": {},
      "deleted": {}
      },
    "sell": {
      "inserted": {},
      "changed": {
        "9043": 30331.0
        },
      "deleted": {}
      }
    },
  "event": "orderbook",
  "instrument": "BTCUSD"
}
```

## Orderbook_L25

Command:`{ "op": "subscribe", "args": ["orderbook_L25:BTCUSD"] }`

> Example Response
> //First 25 level of orderbook for BTCUSD

```json
  {
    "data": {
      "ts": 1593158809487605173,
      "type": "ticker",
      "buy": {
        "inserted": {},
        "changed": {
          "9037": 13946.0
        },
        "deleted": {}
      },
      "sell": {
        "inserted": {},
        "changed": {},
        "deleted": {}
      }
    },
    "event": "orderbook_L25",
    "instrument": "BTCUSD"
  }
```

## Trade (Snapshot)

Command:`{ "op": "query", "args": ["trades:BTCUSD"] }`

> Example Response

> // One item per match and multiple items per snapshot on group change.

```json
{
  "data": [
  {
      "ts": 1592829837839, // timestamp
      "q": 100.0, // size or quantity
      "p": 9043.0, // price
      "s": "B" // order-side "S": Sell, "B": Buy
      },
      {
      "ts": 1592829390110, // timestamp
      "q": 100.0, // size or quantity
      "p": 9043.0, // price
      "s": "B" // order-side "S": Sell, "B": Buy
      },
  ],
  "event": "trades",
  "instrument": "BTCUSD",
  "op": "query"
}

```

### Response
FieldName | Short Description 
--------- | ----------- 
ts | Timestamp in milliseconds
q | Size or quantity 
p | Price 
s | Order-side "S": Sell, "B": Buy

## Trade (Ticker)

Command:`{ "contract": "BTCUSD"}`

> Example Response

> // One item per match and multiple items per snapshot on group change.

```json
{
  "data": [
    {
      "ts": 1592831064637,
      "q": 1.0,
      "p": 9043.0,
      "s": "S"
      }
    ],
    "event": "trades",
    "instrument": "BTCUSD"
  }
}
```

### Response
FieldName | Short Description 
--------- | ----------- 
ts | Timestamp in milliseconds
q | Size or quantity 
p | Price 
s | Order-side "S": Sell, "B": Buy

## Chart (Ticker)

Command:`{ "op": "subscribe", "args": ["chart_1m:BTCUSD"] }`

> Example Response

> // One item per match and multiple items per snapshot on group change.

```json
{
  "data": [
    1592893560000,  // timestamp
    9043.0,         // open
    9043.0,         // high
    9043.0,         // low
    9043.0,         // close
    0.0             // volume
  ],
  "event": "chart_1m",
  "instrument": "BTCUSD"
}
```

## Mark Price & Index Price

Command:`{ "op": "subscribe", "args": ["markprice:BTCUSD"] }`

> Example Response

```json
{
"data": {
  "IP": 9050.0,  // index price
  "P": 8951.97,  // price
  "T": 1592831293000  // timestamp
  },
"event": "markprice",
"instrument": "BTCUSD"
}
```

### Response
FieldName | Short Description 
--------- | ----------- 
IP | Index price
P | Price
T | Timestamp in milliseconds 

## Premium Index 

Command: `{ "op": "subscribe", "args": ["premiumindex:BTCUSD"] }`

> Example Response

```json
{
  "data": {
    "R": -0.00061276,
    "T": 1592890620000
  },
  "event": "premiumindex",
  "instrument": "BTCUSD"
}
```

### Response
FieldName | Short Description 
--------- | ----------- 
r | Premium rate
t | Timestamp 

## Funding Rate 

Command: `{ "op": "subscribe", "args": ["fundingrate:BTCUSD"] }`

> Example Response

> // One item per match and multiple items per snapshot on group change.

```json
{
  "data": {
    "R": -0.03040413,
    "T": 1592812800000
    },
  "event": "fundingrate",
  "instrument": "BTCUSD",
  "op": "query"
}
```

### Response
FieldName | Short Description 
--------- | ----------- 
R | Funding rate
T | Timestamp 

## Funding Rate Prediction

Command: `{ "op": "subscribe", "args": ["fundingrate_prediction:BTCUSD"] }`

> Example Response

> // One item per match and multiple items per snapshot on group change.

```json
{
  "data": {
    "R": -0.03040413,
    "T": 1592812800000,
    "NT": 1595030400000,
    },
  "event": "fundingrate_prediction",
  "instrument": "BTCUSD",
  "op": "query"
}
```

### Response
FieldName | Short Description 
--------- | ----------- 
R | Funding rate
T | Timestamp 
NT | Next funding settlement timestamp

## Stats 

Command: `{ "op": "subscribe", "args": ["stats:BTCUSD"] }`

> Example Response

> // Return 24 hours high, 24 low and 24 hour turnover and open interest

```json
{
  "data": {
    "volume": 250844,
    "turn_over": 27.74820594290235390496,
    "max": 9045.0,
    "min": 9037.0,
    "change": 0.0,
    "open_interest": 1145386,
    "updated_at": 1593162835
  },
  "event": "stats",
  "instrument": "BTCUSD"
}
```

## Notification 

Command: `{ "op": "subscribe", "args": ["notification"] }`

> Example Response

System-wide notifications

```json
{
    "data": {
      "type": "Success",
      "title": "Order Filled",
      "content": "10 contract of BTCUSD bought at 9045. The order has fully filled",
      "time": "10:09:52"
    },
    "event": "notification"
}
```

# WebSocket User Data Stream

<aside class="notice">
Authentication is required for user data stream
</aside>

## User Margin 

Command: `{ "contract": "BTCUSD" }`

> Example Response

```json
{
  "user_margin_ticker-BTCUSD":{
      "userId":"id123",
      "data":{
        "rl":400,
        "cl":63.0,
        "im":1.5000,
        "mm":1.0000,
        "ml":66.67
      }
  }
}
```

## User Margin 

Command: `{ "op": "subscribe", "args": ["marginsettings:BTCUSD"] }`

> Example Response

```json
{
  "data": {
    "rl": 600,
    "cl": 2.0,
    "im": 50.0,
    "mm": 5.5000,
    "ml": 16.67
  },
  "event": "marginsettings",
  "instrument": "BTCUSD"
}
```

## Position

Command: `{ "op": "subscribe", "args": ["positions:BTCUSD"]}`

> Example Response

```json
{
  "data": {
    "open": [
    {
        "pid": "b38ec35d-d67d-4cfe-8890-d4cfccda724a",
        "sym": "BTCUSD",
        "size": -2,
        "value": 0.00022314,
        "collateral_currency": "BTC",
        "entry_price": 9041.5,
        "mark_price": 8962.86,
        "liq_price": 9411.88,
        "margin": 0.00002962,
        "leverage_x": 8.0,
        "uPNL": 0.00000194,
        "uPNL_ROE": 0.0,
        "rPNL": -0.00000002
        }
    ],
    "closed": []
    },
  "event": "positions",
  "instrument": "BTCUSD"
  }
}
```

## My Order (Snapshot)

To filter your orderbook by contract, please include the contract symbol in the command, eg:

Command: `{ "op": "query", "args": ["myorders:BTCUSD"]}`

> Example Response

```json
{
  "data": [
  {
      "sym": "BTCUSD",                                //contract name
      "ts": 1592831064637,                            // acceptance timestamp
      "o": "08e7eea6-d2c5-4106-8e77-481eb41de0d7",    // OrderID
      "u": "37E1E7C53842BD",                          // UserID
      "sp": 0.0,                                      // stop price
      "p": 9043.0,                                    // price
      "r": 0,                                         // remaining
      "s": "S",                                       // order-side "S": Sell, "B": Buy
      "q": 1.0,                                       // size or quantity
      "st": true,                                     // Status
      "tif": "GTC",                                   // Time In Force
      "t": "Limit",                                   // Order Type
      "odst": "Filled",                               // Order detailed Status
      "v": 0.00011058,                                // Value
      "fp": 9043.0,                                   // Fill Price
      "trg": false,
      "reduce": false,
      "trgtyp": 0                                     // trigger type
      },
    {
      "sym": "BTCUSD",
      "ts": 1592830820512,
      "o": "c174b30b-9d13-4067-921e-2d837a2afb6c",
      "u": "37E1E7C53842BD",
      "sp": 0.0,
      "p": 99999.0,
      "r": 100,
      "s": "S",
      "q": 100.0,
      "st": false,
      "tif": "GTC",
      "t": "Limit",
      "odst": "Accepted",
      "v": 0.00100001,
      "fp": 0.0,
      "trg": false,
      "reduce": false,
      "trgtyp": 0
      },
  ],
  "event": "myorders",
  "instrument": "BTCUSD",
  "op": "query"
  }
}
```

### Response
FieldName | Short Description 
--------- | ----------- 
sym | Contract Name
ts | Timestamp 
o | OrderId 
u | Order-side "S": Sell, "B": Buy
sp | Stop Price
p | Price
r | Remaining
s | Order side
q | Size or quantity
st | Non-active statuys
tif | Time in Force
t | Order type
odst | Order detailed Status : Accepted, PartiallyFilled, Filled, Cancel, Rejected
v | Value
fp | Full Price
trg | Trigger
trgtyp | Trigger : 0(Last Price), 1(Mark Price), 2(Index Price)

## My Order (Ticker)

Command: `{ "op": "subscribe", "args": ["myorders:BTCUSD"] }`

> Example Response

> // One item per match and multiple items per snapshot on group change.

```json
{
  "data": [
    {
      "sym": "BTCUSD",
      "ts": 1592834247533,
      "o": "78307e2a-9cfe-40e2-bf1e-8f7650133c52",
      "u": "37E1E7C53842BD",
      "sp": 0.0,
      "p": 99999.0,
      "r": 100,
      "s": "S",
      "q": 100.0,
      "st": false,
      "tif": "GTC",
      "t": "Limit",
      "odst": "Accepted",
      "v": 0.00100001,
      "fp": 0.0,
      "trg": false,
      "reduce": false,
      "trgtyp": 0
      }
    ],
    "event": "myorders",
    "instrument": "BTCUSD"
  }
}
```

### Response
FieldName | Short Description 
--------- | ----------- 
sym | Contract Name
ts | Timestamp 
o | OrderId 
u | Order-side "S": Sell, "B": Buy
sp | Stop Price
p | Price
r | Remaining
s | Order side
q | Size or quantity
st | Non-active statuys
tif | Time in Force
t | Order type
odst | Order detailed Status : Accepted, PartiallyFilled, Filled, Cancel, Rejected
v | Value
fp | Full Price
trg | Trigger
trgtyp | Trigger : 0(Last Price), 1(Mark Price), 2(Index Price)

### Response
FieldName | Short Description 
--------- | ----------- 
ts | Timestamp in milliseconds
q | Size or quantity 
p | Price 
s | Order-side "S": Sell, "B": Buy

## My Trades (Snapshot)

Command: `{ "op": "query", "args": ["mytrades:BTCUSD"] }`

To filter your trades by contract, please include the contract symbol in the command, eg:

> Example Response

```json
{
  "data": [
  {
      "sym": "BTCUSD",
      "ts": 1592831064,
      "o": "08e7eea6-d2c5-4106-8e77-481eb41de0d7",
      "q": 1.0,
      "eq": 1.0,
      "v": 0.0,
      "t": "Limit",
      "sp": 0.000000000000000,
      "p": 9043.000000000000000,
      "ep": 9043.0000000000,
      "r": 0.0,
      "s": "S",
      "tif": "GTC",
      "fee": -0.0000000100,
      "rpnl": 0.0000000000
      },
      {
      "sym": "BTCUSD",
      "ts": 1592830673,
      "o": "13f88c45-bd1f-4405-b435-2952dd3bfa5c",
      "q": 1.0,
      "eq": 1.0,
      "v": 0.0,
      "t": "Limit",
      "sp": 0.000000000000000,
      "p": 9040.000000000000000,
      "ep": 9040.0000000000,
      "r": 0.0,
      "s": "S",
      "tif": "GTC",
      "fee": -0.0000000100,
      "rpnl": 0.0000000000
      }
  ],
  "event": "mytrades",
  "instrument": "BTCUSD",
  "op": "query"
  }
}
```

## My Trades (Ticker)

Command:`{ "op": "query", "args": ["mytrades:BTCUSD"] }`

> Example Response

```json
{
  "data": [
    {
      "sym": "BTCUSD",
      "ts": 1592830673,
      "o": "13f88c45-bd1f-4405-b435-2952dd3bfa5c",
      "q": 1.0,
      "eq": 1.0,
      "v": 0.0,
      "t": "Limit",
      "sp": 0.0,
      "p": 9040.0,
      "ep": 9040.0,
      "r": 0.0,
      "s": "S",
      "tif": "GTC",
      "fee": -0.00000001,
      "rpnl": 0.0
    }
  ],
  "event": "mytrades",
  "instrument": "BTCUSD"
}
```

## Balances

Command: `{ "op": "subscribe/query", "args": ["balances:BTC"]}`

> Example Response

```json
{
  "data": {
    "currency": "BTC",
    "balance": 201974.84537896,
    "bonus": 0.80966297,
    "upnl": 0.00000174,
    "margin": 201975.65504367,
    "position": 0.00002942,
    "order": 0.00012522,
    "available": 201975.65488903,
    "breakdown": {
      "XBTM20": {
        "upnl": 0.0,
        "position": 0.0,
        "order": 0.0
        },
      "BTCUSD": {
        "upnl": 0.00000174,
        "position": 0.00002942,
        "order": 0.00012522
        }
        }
        },
  "event": "balances",
  "instrument": "BTC"
  }
}
```         