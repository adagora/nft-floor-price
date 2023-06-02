# nft-floor-price

Oracle = place to get information

nft oracle design, we should focus on liquidity of price. Our collections should be traded quickly, i.e. nft listed for a low price should be sold quickly. 
about oracle: 
- chainlink oracle work well with top collections nft (top = with high liquidity) 
- nft oracle from marketplaces, guaranteed price accuracy and price security, timeliness can not meet the market requirements,
- NFTX : vToken is NFT covered, and vToken can be used to determine the floor price. Advantage good fluidity, supposedly solves the liquidity problem for weak NFTs. Problem with security oracle, vulnerable to market manipulation due to lack of the lack of depth of liquidity in AMM, 
- oracle z abacus, The "liquidity lock" designed by Abacus is satisfactory in terms of price accuracy, timeliness and security, and it is more refined in pricing --- locking liquidity for each NFT valuation rather than quoting a floor price. But Abacus's method has a drawback: capital inefficient.

# Requirement:
- double checking
- wait for validate if price is correct
- delay / timelock
- fallback
- falling back e.g to the Tellor ETH:USD oracle under the following (extreme) conditions
- interesting: https://www.hindawi.com/journals/mpe/2022/3936414/

# why?
- do not assume: chainlink is always correct (e.g multisig can be compromised)
- Competing protocols like Compound double-check Chainlink price data against other sources, like Uniswap (sanity-check), before injecting into the protocol. Aave has chosen not to do this.


# other:
Are swap price and twap price same? price oracles used for price but how is it so fast that when we execute swap on uniswap platform it executes very quick?
The TWAP is an average of the current swap price and past swap prices. When you want to use Uniswap to imply a "current market price". When you trade on Uniswap, that's not TWAP, that's just the swap price. Transactions execute whenever the next block is added, which is frequent on Ethereum - that's why it's so fast.

when you creating price oracle you want to pass longer time period, like more than last 100 seconds, it timeframe is to short it is easy to atacker to manipulate buy selling in pool without much liquidity buying on uniswap, too long like 1w it can also be out of touch.

uniswap can be oracle to get the current price of token but atacker can easy manipilate if you rely on latest price of oracle can not rely on the latest price in the pool, thats why TWAP(historical prices, along with timestamp block,< less manipulation) was introduced.

# TODO
algorithm can be summarized in four abstract steps:
- Remove extreme outliers from the transaction data stream
