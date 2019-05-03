<intro shit>
The first time I an order book was on GDAX (now Coinbase Pro), buying BTC for USD. (do a bit here)

The order book is what records the interest of buyers and sellers of a particular good, contract, or asset and ultimately, with a matching engine that decides when to make a trade, determines its price, its value. The order book is the linchpin of the double auction mechanism, which has evolved from the Dutch auction in the information age.

Originally, the execution of trades from the order book were determined by a centralized market maker, ie a human being looking at a hand written log of bids (offers to buy) and asks (offers to sell), but with the advent of electronic trading, more specifically with the introduction of the NASDAQ exchange in 1971, the auction mechanism has become algorithmic, more decentralized. The matching engine is now a discrete set of rules (that vary from exchange to exchange). (keep up this bit to have a full paragraph)

The Limit order book is at the center of all open market exchange.

Order books are at the center of cryptocurrency exchanges (do a bit here)
</into shit>

<psuedo code shit>
The order book is a two sided data structure. There is a buy side and a sell side, otherwise known as the bid side and the ask side. 

	1. We are going to request the orderbook state from the Coinbase api and we will build a limit order book data structure in memory
	2. We are going to receive a stream of events from Coinbase via a WebSocket connection, and update our limit order book in memory on each tick from that stream. Our initial http request will have the last update sequence id, so we will process the websocket stream to pick up where that request left off (we will need to queue up our events in state before adding to order book to ensure we do this correctly).
	3. The bid and ask sides of the order book shall be ordered by price, so we can quickly group the orders' volume (forming the values that make up the red and green bars below)
	4. We will publish the state of our order book to our front end (in this case just the console IO)



(credit Ricky han)
</psuedo code shit>

<code shit>
</code shit>