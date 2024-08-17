# IMC-Prosperity-2



## Results
### Final Rank: 219th overall (top 2%), 13th in India.

| Rank    | Overall | Manual | Algorithmic | Country |
| ------- | ------- | ------ | ----------- | ------- |
| Round 1 | 729     | ------ | 571         | ------- |
| Round 2 | 243     | ------ | ------      | ------- |
| Round 3 | 260     | ------ | ------      | ------- |
| Round 4 | 215     | ------ | 201         | 12      |
| Round 5 | 219     | 352    | 229         | 13      |

---
# Team 8848
Undergraduate students from IIT BHU(Varanasi).

- Priyanshu [LinkedIn](https://www.linkedin.com/in/paloxzz/)
- Arin Dhaulakhandi [LinkedIn](https://www.linkedin.com/in/arin-dhaulakhandi-bb4b0626a/)
- Ritwij Verma
- Mohit Agrawal

---

# Round-1

Introduction of Tradable Products: STARFRUIT and AMETHYSTS

Two notable products have been introduced for trading in the archipelago: AMETHYSTS and STARFRUIT. AMETHYSTS have maintained a stable value over time, offering a dependable reference point. Conversely, STARFRUIT has experienced significant price fluctuations, reflecting dynamic trends and possible reversals throughout the trading day.

Market Making Strategy

Our approach to market making involves the following key steps:

Fair Value (FV) Updates: Regularly update the fair value of the product based on current market conditions.
Executing Scratches: Perform market-taking actions under or near fair value orders, avoiding transactions at the worst bid/ask levels.
Stop Loss Implementation: Halt trading if inventory levels exceed a set limit, ensuring that the stop loss is not executed against the worst bid/ask prices.
Market Making Around FV: Engage in market making near the fair value, adjusting the maximum trade amounts based on inventory levels and order size skew.
AMETHYSTS: A Stable Approach

AMETHYSTS have a well-established fair value of 10,000 units, with minimal fluctuations (±2). Given this stability, we directly applied our market-making strategy without needing to frequently adjust the fair value.
STARFRUIT: A Dynamic Approach

STARFRUIT, in contrast, displays strong trends and potential daily reversals. To manage this, we implemented a rolling linear regression model:

$P_t=\beta_0+\beta_1 t$

This model allowed us to predict the price for the next time step:

$\hat{P_{t+1}}=\hat{\beta_0}+\hat{\beta_0}(t+1)$


Incorporating SOBI (Static Order Book Imbalance): To reduce noise, we stored the mid-volume weighted average price (VWAP) from the order book rather than relying solely on the midprice. This approach minimized biases, especially in scenarios where small bid/ask spreads caused distortions.

Optimizing the Rolling Window: We evaluated various rolling window sizes using heatmaps to find the optimal window for accurate price predictions.

Market Making and Market Taking Explained

Market Making: This involves placing both buy (bid) and sell (ask) orders at various price levels within the order book to provide liquidity. These orders are designed to create a trading environment rather than for immediate execution.

Market Taking: This strategy focuses on executing trades by matching orders with existing ones in the order book, primarily aiming to fill positions, regardless of price levels.

# Round-3

# Spread Trading with Gift Baskets

- New Assets Introduced:
  - Gift baskets, chocolates, roses, strawberries.
  - Gift basket composition: 4 chocolates, 6 strawberries, 1 rose.
  
- Strategy:
  - Focused on trading spreads: `Spread = Basket Price - Synthetic Price`.
  - Hypotheses:
    1. Leading/Lagging Relationships: Explored whether synthetic prices or basket prices led the other.
    2. Mean Reversion: Investigated if the spread between basket and synthetic prices was mean-reverting.

- Observations:
  - Spread price consistently oscillated around ~368 across historical data.
  - Adopted a mean-reversion strategy:
    - Buy spreads: When the spread price was below average.
    - Sell spreads: When the spread price was above average.

- Challenges:
  - Position limits restricted the number of trades.
  - Timing trades was critical to avoid missing reversion opportunities.


- Better, adaptive Strategy:
  - Implemented a modified z-score based trading approach: calculated z_score_diff and evaluated if GIFT_BASKET is overvalued(z_score_diff>2) or undervalued(z_score_diff< -2).
  - The small rolling window captured volatility spikes, helping to trade closer to local minima/maxima.

Still, the implementation was not up to the mark and the strategy fails when spikes in assets correspond to dips during downtrends.


  
# Round-4

# Vega Trading with COCONUT_COUPON Options

Vega is the measurement of an option's price sensitivity to changes in the volatility of the underlying asset.

- Underlying Assets:
  - COCONUT: Asset.
  - COCONUT_COUPON: European call option, strike price of 10000, time to maturity 250 days.

- Strategy:
  - Focused on vega trading, exploiting changes in implied volatility (IV).
  - Calculated IV using Black-Scholes:
    - Observed IV oscillated around ~16%.
    - Identified strong intraday mean-reverting behavior.

- Trading Approach:
  - Initial Strategy: Pyramid-style grid trading:
    - Increased position size as IV deviated from its average.
    - Found that weaker mean-reversion signals at lower z-scores were ineffective.
  - Modified Strategy: Trapezoid-style grid trading:
    - Avoided trading below a certain z-score threshold.
    - Discovered that going all-in near a z-score of 1.5 was the most profitable.

- Challenges:
  - Delta-hedging resulted in losses.

- Further trials:
  - Explored alternative hedging decisions:
    - Naked trading.
    - Flipping the hedge based on IV levels.
  - Conclusion: Flipped the hedge, using underlying asset signals based on IV to trade.

  
# Round-5

University exams were on the head, so couldn't do anything in context of the competition.
