Rebalancer.v2
=============

What is this?
-------------

A simple and conservative trading idea applied to a cryptocurrecy portfolio, producing a
consistent and linear percentage profit against no trading (HODLing). Currently supports
[Binance](https://www.binance.com/) a popular cryptocurrency exchange and [Telegram](https://my.telegram.org/) 
updates set to daily. The bot is able to trade any number of BTC pairs and for the exclusion of 
specified assets on the exchange. For example, if you had 1 BTC on the exchange you could
protect 0.5 BTC of that from the bot and it would not be considered in rebalancing. Trades
that do not fill in the user configured time are automatically
cancelled. All operation of the bot can be configured from **portfolio.csv** and 
**config-blank.yaml**.

Explained
---------

A portfolio is defined by a series of coins/tokens and their target percentage of the
portoflio in USD. Every hour (user configurable) exchange data is taken and live
percentages are calculated, followed by trades to reacquire target percentages for 
each coin which may have changed due to price action. Simple, right?

Why?
----

Rebalancing from a trading perspective is essentially a profit taker for short term
bullish action and in **all** backtests proves to be profitable against no trading
(HODLing).

This is a strong, consistent and low-risk methid for profit compared to many forms of
technical analysis due to fundamental information regarding a trading pairs price action
against the overall market, i.e. target percentages.

Future Ideas
------------

1. Implement etherscan.io API to include cold stored cryptocurrencies in rebalancing. Whilst
cold stored coins/tokens cannot be readily traded, so long as enough of each asset is
contained on exchange this remains possible.
2. Live plotting of rebalance vs hodling sent to Telegram with daily updates.

Configuring the bot
-------------------

First configure your API_KEY and API_SECRET in environment variables. To do this from terminal write:

    export API_KEY="API_KEY"
    export API_SECRET="API_SECRET"
    
Then you will need an api_id and api_hash from [Telegram](https://my.telegram.org/). Log in and 
press API Development Tools. Then enter you Telegram API details into the environment variables as:

    export api_id="api_id"
    export api_hash="api_hash"
    
Remember these details must remain secret and secure, **do not share them with anyone!**

**config-blank.yaml** contains all the information about the timing and type of rebalance for the bot.
Important settings are, *tester_type*, *livetest_test*, *telegram_on* and *username*. If you
want to run a live run on an exchange set *livetest_test* to **False**, this will tell Binance
that order requests *are not* test orders. *tick_duration* should be defaulted to 1 and all other time 
based variables should be written in seconds.

**portfolio.csv** has a simple structure. Define the coin pairs you wish to add to the bot,
**remember only add BTC pairs and to be safe only add highly liquid coins (100BTC+/24hr)**.
If you want to use all specified assets from exchange then leave the *protected balance* column
as zero. If you do want to protect some 'on-exchange' assets from the bot, the column is absolute 
amount not percentage amount of the asset. The *column* is the desired percentage of the
portfolio you want the coins to take up.

**NOTE**: All coins are traded against BTC so make sure BTC is in your portfolio, the bot will
not actually trade BTCUSDT, it is only used to value the coins in USD.