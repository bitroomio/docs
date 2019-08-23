# Public API Endpoints
## Terminology
* `base currency` refers to the asset that is the `volume` of a symbol.
* `quote currency` refers to the asset that is the `price` of a symbol.
* `amount=price*volume`, `amount` measured by `quote currency`.

## Market Data endpoints
### order book
```
GET /api/ex/public/orderbook
```

**Parameters:**

Name | Type | Mandatory | Description
------------ | ------------ | ------------ | ------------
pair | STRING | YES |
limit | INT | NO | Default 10 Valid limits:[10, 100]

**Response:**
```javascript
{
  "bids": [
    [
      "4.00000000",     // price
      "431.00000000"    // volume
    ]
  ],
  "asks": [
    [
      "4.00000200",
      "12.00000000"
    ]
  ]
}
```

### 24hr ticker price change statistics
```
GET /api/ex/public/ticker/24hr
```
24 hour rolling window price change statistics. **Careful** when accessing this with no `pair`.

**Parameters:**

Name | Type | Mandatory | Description
------------ | ------------ | ------------ | ------------
pair | STRING | NO |

* If the pair is not sent, tickers for all pairs will be returned in a map.

**Response:**
```javascript
Example: /api/ex/public/ticker/24hr?pair=BNB/USDT

{
    "start_price": "27.84", // Price before 24 hours
    "current_price": "26.87", // current price
    "percent": "-0.0348", // -3.48%
    "high": "27.33", // high price
    "low": "26.75", // low price
    "amount": "4449349.207", // USDT
    "volume": "164679.4", // BNB
    "sort": 3,
    "base_full_name": "base_full_name",
    "count": 7368  // Trades executed count
}
```
OR
```javascript
Example: /api/ex/public/ticker/24hr

{
    "ANKR/BTC": 
    {
        "amount": "22.64606206",
        "base_full_name": "ANKR",
        "current_price": "0.00000038",
        "high": "0.0000004",
        "low": "0.00000037",
        "percent": "-0.0952",
        "sort": 7,
        "start_price": "0.00000042",
        "volume": "59193602",
        "count": 76
    },
    "BMT/USDT": 
    {
        "amount": "1040779.9498851",
        "base_full_name": "Bitroom",
        "current_price": "0.0893",
        "high": "0.0894",
        "low": "0.0891",
        "percent": "0",
        "sort": 1,
        "start_price": "0.0893",
        "volume": "11662164.5",
        "count": 190
    },
    ...
}
```