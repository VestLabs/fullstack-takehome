# Vest Fullstack Take Home Assignment

Vest Labs is a quantitative crypto research firm building a Vest Exchange - a highly capital efficient perpetual futures exchange that uses zero-knowledge proofs to ensure the fairest pricing for traders and liquidity providers.

As a fullstack developer, you will not only be on the consumer-facing side, developing and testing groundbreaking ideas with real users, but also work closely with the infrastructure team on architecting solutions that enable product features. One of the core components of our product is a robust and reliable candlestick chart. In this takehome assignment, you will be tasked with creating a frontend application that displays the candlestick chart.

### Objective

Display a candlestick chart for ETH-PERP that fetches (REST) and streams (WS) 1 minute candlestick data in real time using the following APIs:

The REST endpoint is `https://serverprod.vest.exchange`

`GET /v1/ohlcv/klines`

Params (all required):
- symbol (e.g. "ETH-PERP")
- interval (supports 1m, 3m, 5m, 15m, 30m, 1h, 2h, 4h, 6h, 8h, 12h, 1d, 3d, 1w, 1M)
- startTime (nanoseconds since epoch)
- endTime (nanoseconds since epoch)
- countBack (number of bars to return from endTime)

Example query:
```https://serverprod.vest.exchange/v1/ohlcv/klines?symbol=ETH-PERP&interval=1m&startTime=1726161417000&endTime=1726179479000&countBack=302```

Example response (brotli encoded):
```
[
    [
        1726161300000.0, // open time
        144.1074, // open
        144.1718, // high
        144.052, // low
        144.1362, // close
        0.0, // volume
        1726161359999.0, // close time
        0.0, // quote volume
        0.0 // num of trades
    ],
    ...
]
```

The WS endpoint is `wss://wsprod.vest.exchange/ws-api?xwebsocketserver=restserver0&version=1.0`

Send the following JSON message to the server to subscribe to a candlesticks stream:
```
{
    "method": "SUBSCRIBE",
    "params": ["ETH-PERP@kline_1m"]
}
```

Example response (Brotli encoded):
```
{
    "channel": "ETH-PERP@kline_1m",
    "data": {
        "s": "ETH-PERP",
        "k": {
            "s": "ETH-PERP",
            "o": 145.65211,
            "h": 145.709
            "l": 145.5309
            "c": 145.6869,
            "v": 0.0
            "t": 172618026121,
            "i": "1m",
        }
    }
}
```

**Bonus Points:**
- Include a dropdown to select for different markets
- Handle switching of intervals
- Polished UI following this [Figma design](https://www.figma.com/design/Y0xGAiudDKFthVWTLnyWCT/Frontend-Takehome-Assignment?node-id=0-1&t=yoY7GTwdIDD29wlo-1)

### Technical Specifications
- Use React
- Use TradingView's [`lightweight-charts`](https://github.com/tradingview/lightweight-charts) library for the candlestick chart

### Tips
- Focus on displaying the OHLC data (feel free to ignore volume, quote volume, and number of trades)
- Don't focus too much on the UI (it's a bonus point for a reason), we're mostly looking for functionality
- TradingView should already have client-side caching so you don't need to implement caching
- Ensure that WS messages are decoded correctly (they are Brotli compressed)

### Evaluation Criteria:
- **Functionality**: Does the application meet the requirements?
- **Code Quality**: Is the code well-organized, readable, and maintainable?
- **Bonus Features**: Are any of the bonus features implemented?

### Submission:
Please submit your assignment as a github repo link to [max@vest.xyz](mailto:max@vest.xyz). If you have any questions or need clarifications, feel free to reach out.