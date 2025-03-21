# woo-python
Python SDK (sync and async) for Woo with Rest and WS capabilities.

You can check Woo's docs here: [Docs](https://ccxt.com)


You can check the SDK docs here: [SDK](https://docs.ccxt.com/#/exchanges/woo)

*This package derives from CCXT and allows you to call pretty much every endpoint by either using the unified CCXT API or calling the endpoints directly*

## Installation

```
pip install woo-api
```

## Usage

### Sync

```Python
from woo import WooSync

def main():
    instance = WooSync({})
    ob =  instance.fetch_order_book("BTC/USDC")
    print(ob)
    #
    # balance = instance.fetch_balance()
    # order = instance.create_order("BTC/USDC", "limit", "buy", 1, 100000)
```

### Async

```Python
import asyncio
from woo import WooAsync

async def main():
    instance = WooAsync({})
    ob =  await instance.fetch_order_book("BTC/USDC")
    print(ob)
    #
    # balance = await instance.fetch_balance()
    # order = await instance.create_order("BTC/USDC", "limit", "buy", 1, 100000)

asyncio.run(main())
```

### Websockets

```Python
from woo import WooWs

async def main():
    instance = WooWs({})
    while True:
        ob = await instance.watch_order_book("BTC/USDC")
        print(ob)
        # orders = await instance.watch_orders("BTC/USDC")
```

