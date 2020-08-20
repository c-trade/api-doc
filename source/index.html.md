---
title: C-Trade API 

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

includes:
  - errors

search: true
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
          "minSize": 1
        }
      ],
    }
  }
}
```

This endpoint retrieves contracts menu.

### HTTP Request

`GET https://api.c-trade.com/public/contracts-menu`

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
curl --location --request GET 'https://api.c-trade.com/public/order-book/BTCUSD/200'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "ts": 15816876568905832,
      "bids": {
        "10235": 1.30376,
        "10236": 0.081586,
        "10237": 0.127691,
        "10238": 0.366522,
        "10240": 24.3739479999,
        "10241": 0.090064,
        "10242": 0.0020769999,
        "10243": 0.0012099999,
        "10244": 9.400743,
        "10249.39": 0.196964,
        "10249.35": 5.977335,
        "10249.34": 3.5499999999,
        "10249.28": 2,
        "10249.08": 2,
        "10248.89": 0.070299,
        "10248.57": 0.01,
        "10248.24": 0.01,
        "10248.18": 0.2,
        "10248.12": 0.019512,
        "10246.58": 5.6399999999,
        "10246.56": 0.841608,
        "10246.55": 0.091852,
        "10246.2": 0.1154329999,
        "10246.19": 0.103809,
        "10245.9": 0.2,
        "10245.88": 0.2928009999,
        "10245.77": 1.25,
        "10245.56": 1.606115,
        "10245.55": 0.195051,
        "10245.22": 0.2439649999,
        "10244.88": 0.0044879999,
        "10244.87": 0.0011199999,
        "10244.56": 1.606287,
        "10244.33": 0.175426,
        "10244.31": 0.0869999999,
        "10244.11": 0.7335979999,
        "10244.03": 0.5839999999,
        "10243.91": 0.130304,
        "10243.9": 1.6063689999,
        "10243.63": 0.002,
        "10243.49": 0.0168239999,
        "10243.31": 0.2999999999,
        "10243.3": 1.606478,
        "10243.19": 0.2,
        "10243.18": 0.4,
        "10243.16": 0.244039,
        "10243.15": 0.0336489999,
        "10243.13": 4.4,
        "10243.09": 0.01682,
        "10243.05": 0.016108,
        "10242.18": 0.225828,
        "10241.74": 0.0336289999,
        "10241.67": 0.2214359999,
        "10241.11": 0.160975,
        "10241.1": 0.244061,
        "10240.99": 0.0488009999,
        "10240.92": 0.195294,
        "10240.5": 0.183678,
        "10240.2": 0.3952379999,
        "10240.1": 0.240073,
        "10240.03": 0.152429,
        "10239.72": 0.317338,
        "10239.6": 0.14649,
        "10239.25": 1,
        "10239.19": 0.100927,
        "10239.04": 0.244115,
        "10238.95": 0.2,
        "10238.93": 0.2441659999,
        "10238.92": 0.388952,
        "10238.88": 0.030394,
        "10238.86": 0.095956,
        "10238.23": 0.0285669999,
        "10238.22": 0.244183,
        "10238.19": 0.0034169999,
        "10237.8": 0.226379,
        "10237.79": 0.01,
        "10237.5": 0.001678,
        "10237.37": 0.0010269999,
        "10237.17": 0.251039,
        "10236.98": 0.244185,
        "10236.84": 0.02,
        "10236.74": 0.3048589999,
        "10236.61": 0.012503,
        "10236.5": 0.100338,
        "10236.21": 1.4269689999,
        "10236.19": 0.002089,
        "10236.16": 0.0376649999,
        "10236.12": 0.0120059999,
        "10235.85": 0.065753,
        "10235.56": 3.173,
        "10235.53": 0.0010499999,
        "10235.36": 0.01,
        "10235.09": 0.036537,
        "10234.93": 0.244197,
        "10234.89": 0.2802879999,
        "10234.88": 0.001309,
        "10234.78": 0.0010499999,
        "10234.69": 0.01,
        "10234.68": 0.0035049999,
        "10234.51": 0.0053699999
      },
      "asks": {
        "10260": 0.1248129999,
        "10263": 0.4245209999,
        "10264": 0.143539,
        "10265": 0.127448,
        "10266": 0.047008,
        "10267": 1.015334,
        "10268": 0.1268529999,
        "10269": 0.317711,
        "10270": 5.047899,
        "10271": 0.1467,
        "10272": 0.271602,
        "10251.77": 0.4975919999,
        "10251.78": 0.068425,
        "10251.81": 2,
        "10251.85": 2,
        "10251.86": 2,
        "10251.88": 0.2999999999,
        "10251.98": 0.437466,
        "10251.99": 0.0299999999,
        "10252.87": 0.010943,
        "10252.9": 0.243921,
        "10252.93": 0.402316,
        "10253.63": 0.425283,
        "10253.7": 0.329095,
        "10253.99": 0.1,
        "10254.49": 0.2,
        "10255.17": 0.002926,
        "10255.31": 0.3999619999,
        "10255.32": 0.3911029999,
        "10255.33": 0.149428,
        "10255.34": 0.144064,
        "10255.35": 0.0488009999,
        "10255.59": 0.1306509999,
        "10256.4": 0.131441,
        "10256.41": 0.1993689999,
        "10256.49": 0.191283,
        "10256.5": 1.44665,
        "10256.63": 0.04,
        "10256.92": 0.2399999999,
        "10257.48": 0.3157929999,
        "10257.54": 0.05,
        "10258.74": 0.0025339999,
        "10259.05": 0.023192,
        "10259.08": 0.00936,
        "10259.36": 0.4258259999,
        "10259.54": 4.4,
        "10259.63": 0.243685,
        "10259.85": 0.036614,
        "10260.19": 3.9089999999,
        "10260.31": 0.11271,
        "10260.49": 0.1542179999,
        "10260.5": 0.003504,
        "10260.69": 0.1605179999,
        "10261.34": 0.195053,
        "10261.37": 0.04761,
        "10261.67": 0.0016999999,
        "10261.69": 0.243685,
        "10262.02": 0.162524,
        "10262.03": 0.0245389999,
        "10262.61": 0.194882,
        "10262.64": 0.252,
        "10263.74": 0.185564,
        "10263.75": 0.2436099999,
        "10264.42": 4.248,
        "10264.9": 0.044524,
        "10265.07": 0.0971899999,
        "10265.81": 0.2435269999,
        "10266.36": 0.016806,
        "10266.66": 0.0016,
        "10266.81": 0.0336199999,
        "10267.53": 0.117072,
        "10267.87": 0.243479,
        "10267.92": 0.2921719999,
        "10267.93": 0.0336199999,
        "10268.32": 0.174468,
        "10268.52": 0.1,
        "10268.53": 0.016784,
        "10268.65": 4.024,
        "10269.23": 0.001021,
        "10269.25": 0.5,
        "10269.84": 0.012259,
        "10269.92": 0.243546,
        "10269.97": 0.6872129999,
        "10269.99": 0.078392,
        "10270.04": 0.0019469999,
        "10270.23": 0.017288,
        "10270.51": 0.028791,
        "10270.56": 8.8,
        "10270.8": 0.0020939999,
        "10270.83": 0.001064,
        "10271.17": 0.0013209999,
        "10271.41": 0.0025799999,
        "10271.69": 6.232033,
        "10271.98": 0.243546,
        "10272.09": 0.1947019999,
        "10272.1": 0.048675,
        "10272.23": 0.051511,
        "10272.56": 0.1008339999,
        "10272.61": 0.3135999999,
        "10272.7": 0.001946
      }
    }
  }
}
```

This endpoint retrieves a specific order book.

### HTTP Request

`GET https://api.c-trade.com/public/order-book/<contractsymbol>/<ordernumber>`

### URL Parameters

Parameter | Description
--------- | -----------
contractsymbol | The symbol of the contract
ordernumber | The specific ordernumber

# Orders/Wallet Endpoints

## HMAC Signature Calculation

```
// Example for calculating signature message for a POST Request to {{base_url}}/api/open-orders
{
    timestamp:1587820973,
    recvWindow:10000,
    orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'
}

signature_message = "POST" + "\n" + "/api/open-orders" + "\n" + "1587820973" + "{timestamp:1587820973,recvWindow:10000,orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'}"
signature = HMAC(signature_message)

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
  "error": {
    "code": 3037,
    "message": "Payload_Instant_Liquidation",
    "description": {
      "natsPayload": {
        "symbol": "BTCUSD",
        "size": 1,
        "side": 2,
        "type": 2,
        "timeInForce": 2,
        "limitPrice": 100,
        "stopPrice": 0,
        "trailingAmount": 0,
        "orderID": "8b9fe45a-17a1-4df5-b074-eb78ce10824e",
        "userID": "332424",
        "balance": 10,
        "orderMargin": 0.01040456,
        "liquidationPrice": 104.26539296,
        "takerFee": 0.075,
        "makerFee": -0.025,
        "filledPrice": 0,
        "orderValue": 0.01
      },
      "mtCalc": {
        "liquidationPrice": 104.26539296,
        "maintainanceMarginPerc": 5,
        "initialMarginPerc": 9.0909,
        "leverage": 11,
        "initialCollateral": 0.00090909,
        "takerfeePerc": 0.075,
        "fundingRate": 0.91,
        "markPrice": 9054.91,
        "orderSize": 0.01,
        "transactionFee": -0.0000075,
        "twoWayFee": 0.000015,
        "maintainanceMargin": 0.0005,
        "costNormal": 0.00092409,
        "costAbnormal": 0.01040456,
        "cost": 0.01040456,
        "pLatMarkPrice": -0.00988956
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
timeinForce	| NO |	GTC
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
      },
      {
        "sym": "BTCUSD",
        "ts": 1583408427,
        "o": "fc5c5144-e448-4fc4-9593-80c8f9e0dcbf",
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
        "ts": 1583411706,
        "o": "569ab73e-e1cb-4cb8-8d57-4c887dedd4af",
        "q": 1,
        "eq": 1,
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
        "ts": 1583411757,
        "o": "427054a0-2b12-4afa-b7fc-3bf71e476bbc",
        "q": 1,
        "eq": 1,
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
        "ts": 1583411759,
        "o": "070f683f-9d4c-47cd-a277-66e4f6442aae",
        "q": 1,
        "eq": 1,
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
        "ts": 1583411761,
        "o": "d3355d81-d75a-4841-968f-5f3972a20544",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896,
        "ep": 8896.5,
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

> // Example for calculating signature message for a Socket message request to {{base_url}}/updatesV2

> signature_message = "/updatesV2" + "\n" + "1587820973" + "\n" + "{"contract":"BTCUSD","orderbook":""}"
> signature = HMAC(signature_message)

> // computed signature should be Hexadecimal equivalent of the HMAC signature.

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