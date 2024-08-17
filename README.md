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
