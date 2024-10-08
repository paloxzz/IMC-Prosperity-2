# IMC-Prosperity-2 Trading Challenge
Welcome to our GitHub repository for the strategies and approaches we used during the Prosperity2 trading challenge, a flagship 15-day event organized by IMC Trading. 

---
## Team 8848
Undergraduate students from IIT BHU(Varanasi).

- Priyanshu [LinkedIn](https://www.linkedin.com/in/paloxzz/)
- Arin Dhaulakhandi [LinkedIn](https://www.linkedin.com/in/arin-dhaulakhandi-bb4b0626a/)
- Ritwij Verma
- Mohit Agrawal

---

## Our Experience
The Prosperity-2 challenge was intense yet rewarding(in context of knowledge, XD!). Below, we've outlined our experiences with each challenge, their approach, and a few lessons here and there.

## Round 1
### Algorithm Challenge

**Objective:**  
In this round, we were introduced to the first two tradable products: `STARFRUIT` and `AMETHYSTS`. While the value of `AMETHYSTS` has historically remained stable, the value of `STARFRUIT` fluctuates over time.

**Position Limits:**
- `STARFRUIT`: 20
- `AMETHYSTS`: 20


#### Key Components

1. **Fair Value (FV) Updates**
   - We regularly updated the fair value of the products based on current market conditions, ensuring that we were trading at or near the most accurate price levels.

2. **Executing Scratches**
   - Perform market-taking actions under or near fair value orders, avoiding transactions at the worst bid/ask levels.


3. **Stop Loss Implementation**
   - Trading was halted when inventory levels exceeded a predefined limit. This ensured that stop loss actions were not triggered at unfavorable bid/ask levels, protecting against large losses.

4. **Market Making Around FV**
   - We engaged in market making near the fair value, adjusting the maximum trade amounts based on inventory levels and the size of order skew to maintain optimal liquidity without overexposure.

#### AMETHYSTS: A Stable Approach

AMETHYSTS have a well-established fair value of 10,000 units, with minimal fluctuations (±2). Given this stability, we directly applied our market-making strategy without needing to frequently adjust the fair value.


#### STARFRUIT: A Dynamic Approach

STARFRUIT exhibited strong trends with potential for daily reversals. To account for this volatility, we implemented a **rolling linear regression model** to predict price movements.

#### Price Prediction Model

We modeled the price using linear regression:
- **Formula**: 
  $P_t = \beta_0 + \beta_1 t$

- **Prediction**: 
  $\hat{P}_{t+1} = \hat{\beta_0} + \hat{\beta_1}(t+1)$

#### SOBI (Static Order Book Imbalance)

To reduce noise and avoid biases from small bid/ask spreads, we incorporated the **mid-volume weighted average price (VWAP)** from the order book instead of relying solely on the midprice.

#### Optimizing the Rolling Window

We evaluated various rolling window sizes using heatmaps to find the optimal window for accurate price predictions.

#### Market Making vs. Market Taking

- **Market Making**: Involves placing buy (bid) and sell (ask) orders at various price levels to provide liquidity without the intent of immediate execution.
  
- **Market Taking**: Focuses on executing trades by matching orders with existing ones in the order book to fill positions quickly, regardless of price levels.

### Manual Challenge

**Objective:**  
A huge school of goldfish arrived at our shores. And they all brought scuba gear they want to get rid of fast. For the right price of course.

You only have two chances to offer a good price. Each one of the goldfish will accept the lowest bid that is over their reserve price. There's a constant desire for scuba gear on the archipelago. So, at the end of the round, you'll be able to sell them for 1000 SeaShells a piece. Your goal is to set prices that ensure a profitable trade with as many goldfish as possible.

**Our Approach:**  
- Although it was a fairly easy round, we messed up very bad by not going with mathematical results and bringing in- intution, more than we should have. As a result, we got >1000 rank in the manual challenge by the end of Round-1.
**Hint for Optimal Soln:**  
- We first buy everything below our lowest bid(a), and afterwards be buy everything below our highest bid(b). Just Monte Carlo the results. We can draw samples from a given distribution with numpy.random.triangular function, where we set the left (lower limit) to 900, and both mode and right (higher limit) to 1000.

## Round 2:
### Algorithm Challenge
**Objective:**  
In this round, we continued trading the products introduced in Round 1 (`STARFRUIT` and `AMETHYSTS`), while also being introduced to a new product: `ORCHIDS`. The value of `ORCHIDS` was influenced by various observable factors, such as hours of sunlight, humidity, shipping costs, tariffs, and storage capacity. Our task was to optimize our trading algorithm by identifying the connections between these factors and the price of `ORCHIDS`.

**Position Limits:**
- `ORCHIDS`: 100

**Our Approach:**  

### Manual Challenge

**Objective:**  
Today is a special day. Representatives from three other archipelagos are visiting to trade their currencies with us. You can trade Wasabi roots with Sing the Songbird, Pizza slices with Devin the Duck, and Snowballs with Pam the Penguin.

Your objective is to trade these currencies and maximize your profit in SeaShells. The number of trades is limited to 5.

**Our Approach:**  We calculated the profit of each possible answer(can be solved by doing simple brute-force or using dynamic programming or graph techniques), and ended up submitting seashells -> pizza slices -> wasabi roots -> seashells -> pizza slices -> seashells, which gave the maximum profit of ~113,938.


## Round 3:
### Algorithm Challenge
**Objective:**  
In Round 3, we were introduced to a new product: the `GIFT_BASKET`, which contains four `CHOCOLATE` bars, six `STRAWBERRIES`, and a single `ROSES`. These items, along with the products from the previous rounds (`STARFRUIT`, `AMETHYSTS`, `ORCHIDS`), could all be traded on the island exchange. Our task was to determine whether it was more profitable to trade the `GIFT_BASKET` as a whole or to sell its individual contents separately.


**Our Approach:**  
- **Spread Trading**: Focused on trading the spread between the Gift Basket and its underlying components.
  - **Spread Formula**: `Spread = Basket Price - Synthetic Price (sum of components)`
  - **Key Hypotheses**:
    1. **Leading/Lagging Relationships**: Explored whether the synthetic prices or basket prices led the other in market movement.
    2. **Mean Reversion**: Checked if the spread between basket and synthetic prices exhibited mean-reverting behavior.

#### Observations:
- Historical data showed that the spread price oscillated around ~368.
- **Adopted a Mean-Reversion Strategy**:
  - **Buy Spreads**: When the spread price was below the historical average.
  - **Sell Spreads**: When the spread price was above the historical average.

#### Challenges:
- **Position Limits**: Restricted the number of trades and opportunities to exploit market inefficiencies.
- **Timing Trades**: Crucial to avoid missing opportunities for mean reversion due to sudden price shifts.

#### Improved Strategy:
- **Adaptive Z-Score Trading Approach**:
  - **Z-Score Calculation**: Used a modified z-score based approach to evaluate whether the GIFT_BASKET was overvalued (z_score_diff > 2) or undervalued (z_score_diff < -2).
  - **Rolling Window**: A smaller rolling window was implemented to capture volatility spikes, which enabled more precise trading near local minima and maxima.

#### Outcome:
- The modified strategy improved the accuracy of trades by accounting for sudden volatility.
- **Drawbacks**: The strategy struggled in scenarios where volatility spikes coincided with overall downtrends, leading to misaligned trades during market corrections.

### Manual Challenge

**Objective:**  
A mysterious message in a bottle washed ashore. It turns out to contain a treasure map belonging to the legendary Iguana Jones. Apparently, bounty is scattered all over the archipelago. The adventurer-archeologist also left a note with the treasure map containing some hints on how to find the biggest treasures and how to keep them to yourself.

Your goal is to choose up to three expedition destinations and take home the most treasure. Each tile is said to hold at least 7.5k SeaShells, but rumors are going around that there might be multiple chests in one tile. 
  
## Round 4:

### Algorithm Challenge

**Objective:**  
Round 4 introduced a new product: the `COCONUT_COUPON`. These coupons granted the right to buy `COCONUT` at a fixed price of 10,000 SeaShells after 250 trading days. Our challenge was to trade these coupons as a separate asset while predicting whether it would be more profitable to exercise the coupons and buy the actual `COCONUT` at the end of the period.

**Position Limits:**
- `COCONUT`: 300
- `COCONUT_COUPON`: 600

#### Vega Explained:
- **Vega** is the measurement of an option's price sensitivity to changes in the volatility of the underlying asset.

#### Underlying Assets:
- **COCONUT**: The base asset.
- **COCONUT_COUPON**: European call option with a strike price of 10,000 and a time to maturity of 250 days.

#### Strategy:
- **Focus**: Vega trading, primarily exploiting changes in implied volatility (IV) in the market.
- **IV Calculation**: Used the Black-Scholes model to compute implied volatility.
  - **Observations**: IV oscillated around ~16%, showing strong intraday mean-reverting behavior.

#### Trading Approach:
1. **Initial Strategy: Pyramid-Style Grid Trading**:
   - **Concept**: Increased position size progressively as IV deviated from its average.
   - **Challenges**: Weaker mean-reversion signals at lower z-scores made the approach less effective.
   
2. **Modified Strategy: Trapezoid-Style Grid Trading**:
   - **Avoided Trades**: Below a certain z-score threshold, trades were skipped to avoid low-confidence opportunities.
   - **Successful Trade Zones**: Found that going all-in near a z-score of 1.5 yielded the most profitable trades.

#### Challenges:
- **Delta-Hedging**: Initially employed delta-hedging to minimize risk, but this approach led to losses.

#### Further Trials:
- Explored various alternative hedging techniques, including:
  - **Naked Trading**: Avoided hedging altogether.
  - **Flipped Hedge Strategy**: Switched the hedge based on IV levels.
  
#### Conclusion:
- **Final Approach**: Flipped the hedge, making trading decisions based on underlying asset signals influenced by IV. This adaptive method proved more effective at capitalizing on market volatility.

### Manual Challenge

**Objective:**  
In this challenge, we were again bidding on `SCUBA_GEAR`, but with a twist. This time, the second bid also considered the average second bid of all other traders in the archipelago. If our second bid was under the average, our probability of securing a deal decreased based on a scaling factor, adding a dynamic element to our bidding strategy.

## Round 5:

### Algorithm Challenge

**Objective:**  
In the final round, no new products were introduced, but we gained access to valuable information: the `counter_party` aka bots' trading behaviour in each trade. So, basically it was a strategy optimization round.

**Approach:**
Through the data colleced from the counter parties, various conditions can be made for different assets as each counter party had a unique behavior with a certain asset like buying high/low and selling low/high for coconuts, etc., which could easily be identified by plotting the data for visual representation.
However we were not able to implement the updates due to our university term examinations and thus missed the algo trading round.

### Manual Challenge

**Objective:**  
In the final challenge, we were invited to trade foreign goods on the Northern Archipelago. The penguins’ trusted news source, Iceberg, provided us with critical market information, but we also had to manage the increasing costs of trading each good as we conducted more trades.

**Our Approach:**  
- **News Analysis:** Using insights from the Iceberg news source, we identified key trends and market movements in the Northern Archipelago. This allowed us to make informed decisions about which foreign goods to trade, timing our entries and exits for maximum impact.
- **Profitability Check:** We employed Monte Carlo simulations to assess the profitability of each trade. 
- **Selective Trading:** Rather than engaging in broad trading across all goods, we focused on a few high-margin opportunities, ensuring that the rising costs did not erode our profits.


## Results
### Final Rank: 219th overall, 13th in India.

## Final Thoughts

Participating in Prosperity-2 was an invaluable experience that tested our trading knowledge and problem-solving skills in a fast-paced setting. Each challenge pushed us to think critically and adapt quickly, which will hopefully be beneficial in our future endeavors.

We hope this repository serves as a useful resource for anyone looking to understand how we tackled the challenges! Peace!
