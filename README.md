# woo-python
Python SDK (sync and async) for Woo cryptocurrency exchange with Rest and WS capabilities.

- You can check the SDK docs here: [SDK](https://docs.ccxt.com/#/exchanges/woo)
- You can check Woo's docs here: [Docs](https://www.google.com/search?q=google+woo+cryptocurrency+exchange+api+docs)
- Github repo: https://github.com/ccxt/woo-python
- Pypi package: https://pypi.org/project/woo-api


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

main()
```

### Async

```Python
import sys
import asyncio
from woo import WooAsync

### on Windows, uncomment below:
# if sys.platform == 'win32':
# 	asyncio.set_event_loop_policy(asyncio.WindowsSelectorEventLoopPolicy())

async def main():
    instance = WooAsync({})
    ob =  await instance.fetch_order_book("BTC/USDC")
    print(ob)
    #
    # balance = await instance.fetch_balance()
    # order = await instance.create_order("BTC/USDC", "limit", "buy", 1, 100000)

    # once you are done with the exchange
    await instance.close()

asyncio.run(main())
```



### Websockets

```Python
import sys
from woo import WooWs

### on Windows, uncomment below:
# if sys.platform == 'win32':
# 	asyncio.set_event_loop_policy(asyncio.WindowsSelectorEventLoopPolicy())

async def main():
    instance = WooWs({})
    while True:
        ob = await instance.watch_order_book("BTC/USDC")
        print(ob)
        # orders = await instance.watch_orders("BTC/USDC")

    # once you are done with the exchange
    await instance.close()

asyncio.run(main())
```





#### Raw call

You can also construct custom requests to available "implicit" endpoints

```Python
        request = {
            'type': 'candleSnapshot',
            'req': {
                'coin': coin,
                'interval': tf,
                'startTime': since,
                'endTime': until,
            },
        }
        response = await instance.public_post_info(request)
```


## Available methods

### REST Unified

- `create_convert_trade(self, id: str, fromCode: str, toCode: str, amount: Num = None, params={})`
- `create_market_buy_order_with_cost(self, symbol: str, cost: float, params={})`
- `create_market_sell_order_with_cost(self, symbol: str, cost: float, params={})`
- `create_order(self, symbol: str, type: OrderType, side: OrderSide, amount: float, price: Num = None, params={})`
- `create_trailing_amount_order(self, symbol: str, type: OrderType, side: OrderSide, amount: float, price: Num = None, trailingAmount=None, trailingTriggerPrice=None, params={})`
- `create_trailing_percent_order(self, symbol: str, type: OrderType, side: OrderSide, amount: float, price: Num = None, trailingPercent=None, trailingTriggerPrice=None, params={})`
- `fetch_accounts(self, params={})`
- `fetch_balance(self, params={})`
- `fetch_closed_orders(self, symbol: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_convert_currencies(self, params={})`
- `fetch_convert_quote(self, fromCode: str, toCode: str, amount: Num = None, params={})`
- `fetch_convert_trade_history(self, code: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_convert_trade(self, id: str, code: Str = None, params={})`
- `fetch_currencies(self, params={})`
- `fetch_deposit_address(self, code: str, params={})`
- `fetch_deposits_withdrawals(self, code: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_deposits(self, code: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_funding_history(self, symbol: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_funding_interval(self, symbol: str, params={})`
- `fetch_funding_rate_history(self, symbol: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_funding_rate(self, symbol: str, params={})`
- `fetch_funding_rates(self, symbols: Strings = None, params={})`
- `fetch_ledger(self, code: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_leverage(self, symbol: str, params={})`
- `fetch_markets(self, params={})`
- `fetch_my_trades(self, symbol: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_ohlcv(self, symbol: str, timeframe='1m', since: Int = None, limit: Int = None, params={})`
- `fetch_open_orders(self, symbol: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_order_book(self, symbol: str, limit: Int = None, params={})`
- `fetch_order_trades(self, id: str, symbol: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_order(self, id: str, symbol: Str = None, params={})`
- `fetch_orders(self, symbol: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_position(self, symbol: Str, params={})`
- `fetch_positions(self, symbols: Strings = None, params={})`
- `fetch_status(self, params={})`
- `fetch_time(self, params={})`
- `fetch_trades(self, symbol: str, since: Int = None, limit: Int = None, params={})`
- `fetch_trading_fees(self, params={})`
- `fetch_transfers(self, code: Str = None, since: Int = None, limit: Int = None, params={})`
- `fetch_withdrawals(self, code: Str = None, since: Int = None, limit: Int = None, params={})`
- `add_margin(self, symbol: str, amount: float, params={})`
- `cancel_all_orders_after(self, timeout: Int, params={})`
- `cancel_all_orders(self, symbol: Str = None, params={})`
- `cancel_order(self, id: str, symbol: Str = None, params={})`
- `default_network_code_for_currency(self, code)`
- `describe(self)`
- `edit_order(self, id: str, symbol: str, type: OrderType, side: OrderSide, amount: Num = None, price: Num = None, params={})`
- `encode_margin_mode(self, mode)`
- `get_asset_history_rows(self, code: Str = None, since: Int = None, limit: Int = None, params={})`
- `get_currency_from_chaincode(self, networkizedCode, currency)`
- `get_dedicated_network_id(self, currency, params: dict)`
- `modify_margin_helper(self, symbol: str, amount, type, params={})`
- `nonce(self)`
- `reduce_margin(self, symbol: str, amount: float, params={})`
- `repay_margin(self, code: str, amount: float, symbol: Str = None, params={})`
- `set_leverage(self, leverage: Int, symbol: Str = None, params={})`
- `set_position_mode(self, hedged: bool, symbol: Str = None, params={})`
- `set_sandbox_mode(self, enable: bool)`
- `transfer(self, code: str, amount: float, fromAccount: str, toAccount: str, params={})`
- `withdraw(self, code: str, amount: float, address: str, tag=None, params={})`

### REST Raw

- `v1_pub_get_hist_kline(request)`
- `v1_pub_get_hist_trades(request)`
- `v1_public_get_info(request)`
- `v1_public_get_info_symbol(request)`
- `v1_public_get_system_info(request)`
- `v1_public_get_market_trades(request)`
- `v1_public_get_token(request)`
- `v1_public_get_token_network(request)`
- `v1_public_get_funding_rates(request)`
- `v1_public_get_funding_rate_symbol(request)`
- `v1_public_get_funding_rate_history(request)`
- `v1_public_get_futures(request)`
- `v1_public_get_futures_symbol(request)`
- `v1_public_get_orderbook_symbol(request)`
- `v1_public_get_kline(request)`
- `v1_private_get_client_token(request)`
- `v1_private_get_order_oid(request)`
- `v1_private_get_client_order_client_order_id(request)`
- `v1_private_get_orders(request)`
- `v1_private_get_client_trade_tid(request)`
- `v1_private_get_order_oid_trades(request)`
- `v1_private_get_client_trades(request)`
- `v1_private_get_client_hist_trades(request)`
- `v1_private_get_staking_yield_history(request)`
- `v1_private_get_client_holding(request)`
- `v1_private_get_asset_deposit(request)`
- `v1_private_get_asset_history(request)`
- `v1_private_get_sub_account_all(request)`
- `v1_private_get_sub_account_assets(request)`
- `v1_private_get_sub_account_asset_detail(request)`
- `v1_private_get_sub_account_ip_restriction(request)`
- `v1_private_get_asset_main_sub_transfer_history(request)`
- `v1_private_get_token_interest(request)`
- `v1_private_get_token_interest_token(request)`
- `v1_private_get_interest_history(request)`
- `v1_private_get_interest_repay(request)`
- `v1_private_get_funding_fee_history(request)`
- `v1_private_get_positions(request)`
- `v1_private_get_position_symbol(request)`
- `v1_private_get_client_transaction_history(request)`
- `v1_private_get_client_futures_leverage(request)`
- `v1_private_post_order(request)`
- `v1_private_post_order_cancel_all_after(request)`
- `v1_private_post_asset_main_sub_transfer(request)`
- `v1_private_post_asset_ltv(request)`
- `v1_private_post_asset_withdraw(request)`
- `v1_private_post_asset_internal_withdraw(request)`
- `v1_private_post_interest_repay(request)`
- `v1_private_post_client_account_mode(request)`
- `v1_private_post_client_position_mode(request)`
- `v1_private_post_client_leverage(request)`
- `v1_private_post_client_futures_leverage(request)`
- `v1_private_post_client_isolated_margin(request)`
- `v1_private_delete_order(request)`
- `v1_private_delete_client_order(request)`
- `v1_private_delete_orders(request)`
- `v1_private_delete_asset_withdraw(request)`
- `v2_private_get_client_holding(request)`
- `v3_public_get_insurancefund(request)`
- `v3_private_get_algo_order_oid(request)`
- `v3_private_get_algo_orders(request)`
- `v3_private_get_balances(request)`
- `v3_private_get_accountinfo(request)`
- `v3_private_get_positions(request)`
- `v3_private_get_buypower(request)`
- `v3_private_get_referrals(request)`
- `v3_private_get_referral_rewards(request)`
- `v3_private_get_convert_exchangeinfo(request)`
- `v3_private_get_convert_assetinfo(request)`
- `v3_private_get_convert_rfq(request)`
- `v3_private_get_convert_trade(request)`
- `v3_private_get_convert_trades(request)`
- `v3_private_post_algo_order(request)`
- `v3_private_post_convert_rft(request)`
- `v3_private_put_order_oid(request)`
- `v3_private_put_order_client_client_order_id(request)`
- `v3_private_put_algo_order_oid(request)`
- `v3_private_put_algo_order_client_client_order_id(request)`
- `v3_private_delete_algo_order_order_id(request)`
- `v3_private_delete_algo_orders_pending(request)`
- `v3_private_delete_algo_orders_pending_symbol(request)`
- `v3_private_delete_orders_pending(request)`

### WS Unified

- `describe(self)`
- `watch_public(self, messageHash, message)`
- `watch_order_book(self, symbol: str, limit: Int = None, params={})`
- `fetch_order_book_snapshot(self, client, message, subscription)`
- `watch_ticker(self, symbol: str, params={})`
- `watch_tickers(self, symbols: Strings = None, params={})`
- `watch_bids_asks(self, symbols: Strings = None, params={})`
- `watch_ohlcv(self, symbol: str, timeframe='1m', since: Int = None, limit: Int = None, params={})`
- `watch_trades(self, symbol: str, since: Int = None, limit: Int = None, params={})`
- `check_required_uid(self, error=True)`
- `authenticate(self, params={})`
- `watch_private(self, messageHash, message, params={})`
- `watch_private_multiple(self, messageHashes, message, params={})`
- `watch_orders(self, symbol: Str = None, since: Int = None, limit: Int = None, params={})`
- `watch_my_trades(self, symbol: Str = None, since: Int = None, limit: Int = None, params={})`
- `watch_positions(self, symbols: Strings = None, since: Int = None, limit: Int = None, params={})`
- `set_positions_cache(self, client: Client, type, symbols: Strings = None)`
- `load_positions_snapshot(self, client, messageHash)`
- `watch_balance(self, params={})`

## Contribution
- Give us a star :star:
- Fork and Clone! Awesome
- Select existing issues or create a new issue.