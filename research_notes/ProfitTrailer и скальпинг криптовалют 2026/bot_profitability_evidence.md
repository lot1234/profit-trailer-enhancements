# Do retail crypto trading bots (ProfitTrailer-style spot scalping / DCA) make money in 2024–2026? Evidence review

Scope note: research done 2026-10-03. Evidence from 2024–2026 is the focus; anything older is labelled **[historical]**. Source quality is flagged as follows: **[academic]** means peer-reviewed or a preprint, **[vendor]** means the bot or exchange company's own material, **[affiliate]** means a review site that earns referral fees, and **[anecdote]** means a single user's report.

---

## 1. What do independent user reports, public trackers and published results say about ProfitTrailer profitability in 2024–2026?

### Takeaway
I found **no independent, verified ProfitTrailer track record from 2024–2026**. That covers public PT Tracker stats, Myfxbook-style audits and community leaderboards. The product is still sold and maintained. What exists about it online is affiliate reviews with vague, unverifiable return claims, plus signs that the user base has shrunk a lot since the 2018–2021 peak.

### Cited Findings
- ProfitTrailer is still being developed. Its GitHub release notes cover the 2.5.x line: fixes for Bybit spot and Huobi futures, a "modernized GUI", Binance Futures pair views with an `allowed_underlying_type` filter, fixes to DCA max-cost validation, and PT Assistant API keys. So the product has expanded from spot into futures. I could not capture exact release dates from the page. — [GitHub taniman/profit-trailer releases](https://github.com/taniman/profit-trailer/releases)
- PT Feeder, the add-on that changes PT settings automatically, is still sold at €200. — [ProfitTrailer PT Feeder product page](https://profittrailer.com/product/pt-feeder) **[vendor]**
- The ProfitTrailer terms of service say lifetime licences are version-controlled: after the next major version ships, older versions get only critical fixes. If an exchange "packs up and leaves", PT drops support for it and offers legacy licence holders 50% off an upgrade. The terms are governed by Curaçao law. — [ProfitTrailer Terms of Service](https://profittrailer.com/terms-of-services) **[vendor]**
- A 2025 review says Profit Trailer "continues to occupy a niche", describes features and gives no performance data. — [CoinSpot.io ProfitTrailer Review 2025](https://coinspot.io/en/reviews/profit-trailer) **[affiliate]**
- A 2026 review says "many users report profits of around 1% in a month while others could make 5x". It gives no data source, and the same page steers readers to Cryptohopper, Coinrule and Bitsgap. — [CaptainAltcoin Profit Trailer Review 2026](https://captainaltcoin.com/profit-trailer-review/) **[affiliate, unverifiable]**
- A claim appears in review-site results that PT once had "more than 30,000 active traders, but today only around 5,500 or so left, according to its Reddit and Twitter communities". I could not verify the original page, its date or its method; it probably comes from [BitcoinWisdom ProfitTrailer review](https://bitcoinwisdom.com/profittrailer/) or [JonathonSpire PT review](https://jonathonspire.com/profit-trailer/). **[unverified]**
- An older review describes PT as getting "mixed reviews": some users claim it is very profitable, others recommend against it. — [EliteCurrensea ProfitTrailer review](https://elitecurrensea.com/software-providers/profit-trailer) **[affiliate, undated]**
- Zignaly's 2025 update on its PT review page says it "no longer offer[s] standalone copy trading, signal marketplaces or DIY trading bots" and has moved to index-style portfolios. This points to an industry move away from retail DIY bots. — [Zignaly ProfitTrailer Bot Review](https://zignaly.com/crypto-trading/bots/profittrailer-bot-review) **[vendor]**
- A search of Reddit for "ProfitTrailer 2024/2025 PT tracker results" turned up **no** r/ProfitTrailer threads with shared 2024–2026 performance. Results were unrelated threads. This is an absence of evidence: the community is quiet or not indexed. — [Tavily search restricted to reddit.com, see Gaps]

### Inferences
- There is no public, audited PT record for 2024–2026, and affiliate reviews have a reason to inflate. So claims like "1%/month" or "5x" should be treated as marketing. The most likely real picture is a wide spread of outcomes with heavy survivorship bias: users who lost money stop posting and leave the community, which fits the reported fall in users.
- PT's move toward futures support suggests that the classic setup (spot altcoin trailing buys plus DCA on BTC/USDT-quoted alts) no longer pulls in users the way it did in 2018–2021.

### Gaps
- I could not find any PT Tracker leaderboard, shared PT stats page, or Myfxbook-like verified PT account for 2024–2026. The PT Discord and forums are not searchable through these tools.
- I could not confirm the dates of the latest PT releases or the "30,000 → 5,500 users" figure.
- I found no ProfitTrailer user survey or company disclosure of aggregate user P&L.

---

## 2. What does evidence say about comparable bots (Freqtrade, Gunbot, 3Commas DCA, Cryptohopper, Pionex grid, Hummingbot): typical returns, drawdowns, failure modes?

### Takeaway
No bot platform publishes audited aggregate user returns. The best evidence comes from three places: (a) the platforms' own disclaimers, which now openly say profits are not guaranteed and that DCA and grid strategies lose in downtrends; (b) independent breakdowns of popular community strategies, which show very high win rates hiding underperformance; and (c) a 2025 arXiv paper showing that a plain grid has roughly zero expected return before fees. The reported "returns" are mostly backtests, cherry-picked screenshots or affiliate estimates.

### Cited Findings
**Freqtrade**
- The official Freqtrade docs say "most public strategies are not good performers". They warn that backtesting "can be very easy to distort results so a strategy will look a lot more profitable than it really is", and say dry-run (forward testing) "is a much more reliable indicator". — [Freqtrade Strategy Quickstart docs](https://www.freqtrade.io/en/stable/strategy-101) **[vendor/open-source docs]**
- An independent breakdown (posted 2026-09-07) looks at NASOSv4, "one of the most downloaded Freqtrade strategies ever written". It "won 94% of its trades. 2,299 trades. Seven years of data. And it still finished behind doing nothing at all", and the 94% figure is produced by "one hand-written rule". The strategy buys sharp drops and grabs a small bounce. — [YouTube: "This Algotrading Bot Wins 94% Of Its Trades. That's The Problem."](https://www.youtube.com/watch?v=17hnn9SehfE) **[independent analysis; backtest]**
- Example of backtest marketing: Medium posts claim "8787%+ ROI over 1024 days" and "4450% profit" for Freqtrade RSI/MACD/Bollinger strategies, all from backtests. — [Medium, ImbueDesk 8787% ROI](https://imbuedeskpicasso.medium.com/the-8787-roi-algo-strategy-unveiled-for-crypto-futures-22a5dd88c4a5); [Medium, 2509% case study](https://imbuedeskpicasso.medium.com/2509-profit-unlocked-a-case-study-on-algorithmic-trading-with-freqtrade-39b1051c0f1e) **[promotional backtests]**
- r/algotrading threads show the pattern of users with a strategy that "managed to double the initial capital" in a 5-year backtest asking what to do next. — [r/algotrading "got 100% on backtest what to do?"](https://www.reddit.com/r/algotrading/comments/1lmzy9z/got_100_on_backtest_what_to_do) **[anecdote]**

**3Commas DCA**
- A 2026 review says DCA bots "can generate 8–15% annualized returns on average… when configured conservatively on BTC and ETH". It estimates bull markets at 15–35% and bear markets at −5% to −15%, and in a bear market "all safety orders trigger, maximum capital deployed at worst prices… bot gets 'stuck'". Its key point: "DCA bots are NOT market-neutral. They are fundamentally long-biased… In a sustained downtrend, they lose money. This is the most important thing 3Commas' marketing underemphasizes." The numbers are "community-reported results… and our testing" and are not audited. — [TradeAlgo 3Commas Review 2026](https://www.tradealgo.com/trading-guides/crypto/3commas-review) **[review site; unverified figures]**
- 3Commas' own illustrative case: when "Bitcoin dropped 30% in two days", a DCA bot with tight stop-losses and capped averaging orders "lost only 8%", while one "using no stop loss saw a 45% drawdown". — [3Commas blog: Risk Management Settings for AI Trading Bots](https://3commas.io/blog/ai-trading-bot-risk-management-guide) **[vendor, illustrative scenario]**
- The 3Commas backtesting guide warns that "a strategy that crushes a bull run might sink in a sideways chop" and that "a very high win rate (like 100%) can sometimes indicate an overly safe or overly tight setup which might break down in live conditions". — [3Commas Help: DCA Bot Backtesting Guide](https://help.3commas.io/en/articles/11477934-dca-bot-backtesting-guide) **[vendor]**
- **[historical, Dec 2022]** In the 3Commas API-key breach, about 100,000 users' API keys were posted. Attackers used them to steal an estimated $20–22M from users' exchange accounts. 3Commas denied responsibility at first and confirmed the leak on Dec 28–29, 2022. — [Halborn explainer](https://www.halborn.com/blog/post/explained-the-3commas-breach-december-2022); [Decrypt](https://decrypt.co/118094/after-repeated-denials-3commas-admits-it-was-source-for-earlier-hacks); [SiliconANGLE](https://siliconangle.com/2022/12/29/crypto-trading-service-3commas-confirms-massive-api-key-leak-hack)

**Pionex grid / DCA**
- Pionex's own disclaimer: the grid bot "does not guarantee profits. You can lose money if the asset falls in value, even when completed grid trades show a profit… fees, unfilled orders and a falling asset price can reduce returns or lead to an overall loss." Its AI parameter suggestions "describe historical tests, not expected future returns." — [Pionex blog: Grid Bot](https://www.pionex.com/blog/pionex-grid-bot) **[vendor]**
- Community rules that Pionex itself repeats: "Stick to liquid pairs. BTC, ETH, SOL, BNB. Avoid low-volume altcoins where spreads eat bot profit"; "Set the grid range wider than you think you need. Breaking out of the range is how most bot users get stuck"; "Avoid leverage"; "Treat fixed monthly-return promises as a warning sign." — [Pionex blog: 15 Reddit questions answered](https://www.pionex.com/blog/15-reddit-questions-about-crypto-trading-bots-and-pionex-answered-with-real-data) **[vendor]**
- Pionex advertises a 0.05% trading fee. — [Pionex Google Play listing](https://play.google.com/store/apps/details?id=com.pionex.client&hl=en_US) **[vendor]**
- **[historical, 2022–23 bear market]** A YouTuber with 760K subscribers started a BTC grid bot on 15 March 2022. It was at about −28%, against −34% for a lump-sum buy, and a plain weekly DCA buy was at about +10% over the same period. The grid lost less than holding, but simple scheduled buying beat it. — [MoneyZG: Pionex Grid Trading Bots, My Results](https://www.youtube.com/watch?v=qPLZspKquvw) **[anecdote, posted June 2023]**
- **[historical/anecdote]** A Medium user showed "my oldest Grid Trading Bot, running 135 days with an annualized return of ~95%". It is a single screenshot with no comparison to the bear-market period. — [Medium, SingaporeHODL](https://medium.com/@SingaporeHODL/how-i-started-using-pionex-trading-bots-and-why-you-should-too-2a3b1990461a) **[anecdote, survivorship]**

**Grid trading theory (academic)**
- Chen, Chen & Jang (arXiv, June 2025) show that "under simple assumptions, [the traditional grid strategy's] expected return is essentially zero". With fees, "a smaller grid size… is more susceptible to transaction fees". They tested 1-minute Binance BTC and ETH data from January 2021 to July 2024 with a 0.08% fee. The authors' own Dynamic Grid (DGT), which resets the grid instead of stopping, beat both the plain grid and buy-and-hold in backtest. — [arXiv 2506.11921](https://arxiv.org/abs/2506.11921); [HTML version](https://arxiv.org/html/2506.11921v1) **[academic preprint; in-sample-style backtest of authors' own method]**

**Hummingbot / market making**
- Hummingbot's own docs: "Market making is not a risk-free, always profitable trading operation… You are not going to find a cookie cutter, ready-to-use… always profitable strategy." — [Hummingbot: What is Market Making?](https://hummingbot.org/blog/what-is-market-making) **[vendor]**
- A market maker earns the spread "only if fees, adverse selection, inventory drift, and execution risk do not overwhelm that spread". — [Cube Exchange: What is Hummingbot Trading?](https://www.cube.exchange/what-is/hummingbot-trading) **[exchange explainer]**
- **[historical, 2020 liquidity-mining era]** A Hummingbot user reported +17.1% over 3 days of pure market making on a hand-picked range-bound pair. — [Hummingbot Medium: Sharing is caring](https://medium.com/@hummingbot/sharing-is-caring-3-trading-pairs-i-picked-f5bf75f36560) **[vendor-published anecdote]**

**Gunbot**
- Gunbot's FAQ: "profitability is far from guaranteed". It also offers a "Profit After Costs Simulator" for fees and slippage. — [Gunbot FAQ: Do Trading Bots Actually Work](https://www.gunbot.com/support/faq/do-trading-bots-work-make-money) **[vendor]**
- Gunbot's 4.4/5 Trustpilot score is mostly "Invited" reviews about support and community, not verified returns. One Dec 2025 two-star review says "still not success". — [Trustpilot Gunbot](https://www.trustpilot.com/review/gunbot.com) **[review aggregator]**

### Inferences
- Across platforms, the vendors' own risk language (Pionex, 3Commas, Hummingbot, Gunbot, Freqtrade) now agrees with the academic results: these tools automate execution, they do not create an edge.
- The 94%-win-rate-but-underperforms result for NASOSv4 is exactly what ProfitTrailer-style "buy the dip, sell on a small trailing profit, DCA if it keeps falling" produces. Many small wins and a few large losses or stuck bags give a high win rate with negative or sub-benchmark expectancy.
- Grid and DCA bots are not market-neutral. Their P&L is dominated by the direction of the underlying asset. Realised "grid profit" can hide large unrealised losses on held inventory.

### Gaps
- No platform (3Commas, Cryptohopper, Pionex, Bitsgap) publishes audited aggregate user P&L or the share of users who are profitable. I found no independent dataset on that.
- I found no 2024–2026 Cryptohopper performance evidence beyond marketing.
- Hummingbot evidence for 2024–2026 retail operators, where liquidity-mining rewards are smaller, was not found.

---

## 3. Academic / quantitative studies (2022–2026) on technical-analysis and short-term retail trading profitability in crypto after fees and slippage; alpha decay

### Takeaway
The literature is split, and the split tracks the sample period. Studies using data up to about 2018–2019 found strong technical-rule profitability: thousands of rules, break-even costs well above actual fees. Newer studies are more cautious. A 2024 Korean study finds major crypto markets "weak-form efficient in general" and suggests the earlier evidence "might be sample-specific". A 2024 study using 75,360 rules plus corrections for false discoveries finds out-of-sample outperformance mainly on a *risk-adjusted* basis, meaning smaller drawdowns, not raw return. Overall this fits alpha decay, and the surviving benefit of simple TA is mostly drawdown control, not scalping profit.

### Cited Findings
- **[historical data, published 2021]** Hudson & Urquhart tested "almost 15,000 technical trading rules" on BTC and three other cryptos and found "significant predictability and profitability" with "breakeven transaction costs… substantially higher than those typically found in cryptocurrency markets". The main benefit was that rules "significantly reduce the potential drawdowns" versus buy-and-hold. They also found "Bitcoin does not offer any positive returns in the out-of-sample period" and noted that "the reported profitability of technical trading has declined over time" in the wider literature. — [Hudson & Urquhart, Annals of Operations Research 297 (2021)](https://link.springer.com/article/10.1007/s10479-019-03357-1); [open PDF](https://centaur.reading.ac.uk/85715/8/Hudson-Urquhart2019_Article_TechnicalTradingAndCryptocurre.pdf) **[academic]**
- **[2024]** Deprez & Frömmel used "75,360 simple technical trading rules… daily and intraday frequencies". They selected the best rules after transaction costs using a multiple-hypothesis (false-discovery) procedure and formed portfolios. They found that "especially risk–return wise, simple technical trading rules can outperform a buy-and-hold strategy in the bitcoin market out-of-sample." — [Deprez & Frömmel, International Review of Economics & Finance 93 (2024) 858–874](https://ideas.repec.org/a/eee/reveco/v93y2024ipbp858-874.html); [Ghent University record](https://biblio.ugent.be/publication/01HY3C3S169G1N6QNYR55NZMFB) **[academic]**
- **[2024]** Jin, Jung & Song tested SAR, MACD, MFI, CCI and RSI rules on BTC, ETH, BNB, XRP and ADA. They concluded: "cryptocurrency market are weak-form efficient in general. The results are contrary to the evidence of inefficient cryptocurrency markets documented in the previous literature… we suspect that the evidence of inefficient markets might be sample-specific… Our results also cast doubt on the profitability of programmatic trading systems built on technical indicators." — [Jin, Jung & Song, Journal of Derivatives and Quantitative Studies 32(1) (2024) 23–35](https://www.emerald.com/jdqs/article/32/1/23/1214013/Do-technical-trading-rules-outperform-the-simple) **[academic]**
- **[historical, 2020]** Gerritsen et al. found that only the trading range breakout rule beat buy-and-hold on Sharpe, "for the full sample period and during periods of strongly trending markets. Other technical trading rules do not outperform the buy-and-hold strategy." — [Gerritsen et al., Finance Research Letters 34 (2020)](http://dirkgerritsen.nl/uploads/gerritsen_et_al_2020_bitcoin_trading_rules.pdf) **[academic]**
- **[2025 preprint, 2024 out-of-sample]** A comparison on BTC, trained 2021–Jan 2024 and tested 10 Jan–31 Dec 2024 (after spot ETF approval), found an LSTM model returned about 65.23% cumulative and "significantly outperform[ed]" both an EMA crossover (parameters grid-searched on training data) and MACD+ADX. — [arXiv 2511.00665: Technical Analysis Meets Machine Learning: Bitcoin Evidence](https://arxiv.org/html/2511.00665v1) **[academic preprint]**
- In a 2024 market-neutral crypto strategy paper, "even a 0.1% transaction cost significantly impacts our returns… profitability is almost halved" for the frequently trading variant. The less frequent method was barely affected. — [arXiv 2405.15461](https://arxiv.org/html/2405.15461v1) **[academic preprint]**
- **[historical data 2015–2022; retail context]** BIS Working Paper 1049 used app data from 95 countries. It found that "73% of users downloaded their app when the price of Bitcoin was above $20,000", that over 75% of simulated retail users "would have lost money", and that "the median investor would have lost 48%" of $900 invested. Larger holders sold while small users bought. — [BIS Working Paper 1049](https://www.bis.org/publications/working-paper-1049-crypto-trading-and-bitcoin-prices-evidence-new-database-retail-adoption.pdf); [The Block summary](https://www.theblock.co/news/regulation/2023-02-20-majority-of-bitcoin-retail-investors-lost-money-in-the-last-seven-years-bis-213372) **[academic/institutional]**

### Inferences
- Older papers that found TA profitable were mostly measuring **daily-frequency, trend-following** rules whose value came from sitting out crashes. That is a different strategy from ProfitTrailer-style intraday mean-reversion scalping, which buys dips and adds DCA, and so takes *more* exposure in crashes.
- The move from "profitable" (data before 2019) to "weak-form efficient" (2024 papers) fits alpha decay or sample-specific inefficiency in the 2017–2021 retail boom era.
- Frequency matters a lot. Studies repeatedly find fees roughly halve returns for high-turnover variants, and scalping is the highest-turnover retail style.

### Gaps
- I could not access the full text of Deprez & Frömmel (2024). So I could not confirm whether the **intraday** rule classes survived costs, or whether the out-of-sample outperformance came from daily rules only. This is the most relevant missing detail for scalping.
- I found no academic study that directly measures *retail bot users'* realised P&L, for example from exchange API account data.
- I found no 2022–2026 paper that formally estimates alpha decay, such as a rolling-window profitability decline for crypto TA rules. The decay conclusion is inferred by comparing papers across sample periods.

---

## 4. Specific failure modes of DCA and scalping bots

### Takeaway
The documented failure modes all point the same way for a ProfitTrailer-style spot altcoin DCA/scalping setup in 2024–2026. Most altcoins trended down against BTC and USD, so DCA left bots holding bags. New listings, the classic scalping fodder, mostly collapsed. Thin altcoin order books plus flash crashes such as 10/10/2025 hit hardest where these bots trade. Regular-tier fees take a large share of thin targets. Overfit configurations and over-optimised backtests make the risk look smaller than it is.

### Cited Findings
**Bag holding / DCA amplifying drawdowns in downtrends**
- DCA bots are "fundamentally long-biased"; in bear markets "all safety orders trigger, maximum capital deployed at worst prices… bot gets 'stuck' holding at a loss". — [TradeAlgo 3Commas Review 2026](https://www.tradealgo.com/trading-guides/crypto/3commas-review) **[review site]**
- A 30% BTC drop in 2 days caused a 45% drawdown for a DCA bot with no stop-loss, against 8% with tight stops and capped safety orders. — [3Commas blog](https://3commas.io/blog/ai-trading-bot-risk-management-guide) **[vendor scenario]**
- 2026 bear market: CryptoQuant analyst Darkfost reported that about 84% of Binance-listed altcoins traded below their 200-day moving average. Total crypto market cap was about 51% below its peak at $2.15T, BNB, XRP and SOL were 60–75% below their highs, and "most low-cap altcoins have dropped 80% to 90% from all-time peaks". The article is dated around late June, apparently 2026. — [Bitcoin Foundation news, "84% of Binance Altcoins Trade Below 200-Day MA"](https://bitcoinfoundation.org/news/altcoins/altcoins-decline) **[news citing on-chain analyst]**
- Late-September 2026 regime change: in August 2026, 80% of Binance altcoins were below the 200DMA; by late September only 13% were. The Altcoin Season Index was at 53, still neutral and below the 75 threshold. Glassnode warned that such risk appetite "has often lined up with local tops in BTC". — [BeInCrypto, Sept 2026](https://beincrypto.com/altcoin-season-signals-2025-market-top) **[news citing Glassnode/CryptoQuant]**

**New listings / delistings / small-cap decay**
- CryptoRank data: Binance listed 100 tokens in 2025, 93 traded in the red, and the median ROI was 0.22x. More than 11 million new tokens were issued in 2025. — [BeInCrypto via Yahoo Finance](https://finance.yahoo.com/news/weak-2025-token-listing-returns-075654664.html)
- Earlier 2025 snapshot: "only 11.1% of tokens listed on Binance in 2025 posted a positive return… average loss of 44%". — [Binance Square post](https://www.binance.com/en/square/post/22373674038210) **[user post on exchange's social feed]**
- The MarketVector small-cap index hit its lowest level since November 2020 by November 2025. Over five years it returned about −8%, against about +380% for the large-cap index. Kaiko's small-cap cohort was down over 30% in 2024. — [CryptoSlate citing Bloomberg/Kaiko](https://cryptoslate.com/small-cap-crypto-assets-just-hit-a-humiliating-four-year-low-proving-the-alt-season-thesis-is-officially-dead)

**Low-liquidity slippage and flash crashes / exchange outages**
- After FTX, altcoin liquidity "has taken a particularly hard hit". 1%, 2% and 4% depth stayed mostly flat while market makers concentrated quotes very close to mid. Offshore exchanges' share of altcoin depth rose from 65% to 71%. — [Kaiko: Crypto Liquidity Concentration Report](https://www.kaiko.com/resources/the-crypto-liquidity-concentration-report) **[industry research]**
- On 10/10/2025, "high volumes coincided with very high spreads and therefore very low liquidity". — [Kaiko: State of Liquidity on Korean Crypto Markets, Dec 2025](https://resources.kaiko.com/hubfs/Research/The%20State%20of%20Liquidity%20on%20Korean%20Crypto%20Markets.pdf) **[industry research]**
- The 10/10/2025 crash liquidated about $19.3B in 24 hours across 1.66 million accounts. BTC fell 14.5%, while "smaller tokens dropped 40% to 70% intraday". USDe briefly traded at $0.65 on Binance only. "Eleven months later, Bitcoin trades more than a third below its pre-crash level." — [Datawallet: October 10 Crypto Crash Explained](https://www.datawallet.com/crypto/october-10-crypto-crash-explained)
- On the same day, "Binance reported 'systems under heavy load' with API failures and deposit delays. dYdX was offline for eight hours. Lighter experienced a 4.5-hour outage." — [CoinGecko: What Is October 10th?](https://www.coingecko.com/learn/october-10-crypto-crash-explained)
- ATOM/USDT reportedly "flash dumped to $0.001 on Binance", and wBETH and BNSOL fell about 80% from their pegs within minutes on Binance. — [Medium academic-style analysis (Jung-Hua Liu)](https://medium.com/@gwrx2005/the-october-11-2025-crypto-black-swan-crash-an-academic-analysis-db92a3d2ad66); [Galaxy Research](https://www.galaxy.com/insights/research/cryptos-flash-crash-liquidation-binance-adl-auto-deleveraging)
- Binance BTC 1% market depth was above $600M at the October 2025 all-time high and later fell below $400M. Aggregated 2% depth was about 30% below its 2025 high. — [CryptoSlate citing Kaiko](https://cryptoslate.com/bitcoin-struggles-to-reclaim-90000-amid-plummeting-liquidity-and-waning-market-depth)

**Fees eating thin margins**
- Binance spot fees for a Regular user (under $1M 30-day volume): **0.100% maker / 0.100% taker**, or 0.075% each with the BNB discount. Maker fees only drop below taker at VIP tiers, for example VIP 3 (≥$20M volume) pays 0.040% / 0.060%. — [Binance Spot Trading Fee Rate](https://www.binance.com/en/fee/trading) **[exchange]**
- With grid strategies, fees cause "a sharp drop in profitability" at small grid sizes. — [arXiv 2506.11921](https://arxiv.org/html/2506.11921v1) **[academic]**

**Overfitting**
- Freqtrade warns backtests "can be very easy to distort". — [Freqtrade docs](https://www.freqtrade.io/en/stable/strategy-101)
- A high win rate built on a hand-written exit rule, as in NASOSv4 with 94% wins, still underperformed over 7 years. — [YouTube NASOSv4 analysis](https://www.youtube.com/watch?v=17hnn9SehfE)
- Pionex AI-suggested grid settings "would have performed well under those conditions", i.e. they are fitted to the last 7, 30 or 180 days. — [Pionex blog](https://www.pionex.com/blog/15-reddit-questions-about-crypto-trading-bots-and-pionex-answered-with-real-data) **[vendor]**

**Security / fraud / vendor risk**
- The CFTC advisory "AI Won't Turn Trading Bots into Money Machines" (Jan 25, 2024) warns that fraudsters "tout automated trading algorithms… that promise unreasonably high or guaranteed returns… AI technology can't predict the future or sudden market changes." It cites Mirror Trading International, which took about 30,000 BTC (about $1.7B) on a promise of "at least 10% each month". — [CFTC Customer Advisory](https://www.cftc.gov/LearnAndProtect/AdvisoriesAndArticles/AITradingBots.html); [KKC summary](https://kkc.com/advisories/ai-trading-bot-scams) **[regulator]**
- API-key compromise at a bot vendor: 3Commas, Dec 2022, about $20M stolen. — [Halborn](https://www.halborn.com/blog/post/explained-the-3commas-breach-december-2022) **[historical]**

### Inferences
- **Fee arithmetic (my calculation from Binance's published fees):** a ProfitTrailer-style 1% trailing take-profit on a Regular-tier account pays 0.2% round-trip, or 0.15% with BNB. That is 15–20% of the gross target before any slippage. On a 0.5% scalp it is 30–40%. Because Binance charges Regular users the same maker and taker rate, maker-only orders do **not** cut fees at retail tier. They only avoid paying the spread.
- On 10/10, a spot bot with low resting buy orders or DCA triggers on altcoins could have filled near extreme wicks. That can help if price recovers, but only if the coin recovers. A bot whose stop-loss sells at market would have sold at the wick. Exchange API failures during the event meant bots could not reliably manage orders.
- In ProfitTrailer's original setup, trading many small-cap pairs and buying "pumping" or dipping coins, every listed risk compounds: worst liquidity, highest delisting risk, worst 2024–2026 relative performance.

### Gaps
- I found no data on how many retail bot accounts were hit by delistings, or on realised slippage for retail bots on small caps.
- I did not search FCA or ESMA warnings specifically for trading bots; only the CFTC advisory is covered.
- I found no source quantifying ProfitTrailer-specific losses during 10/10/2025 or the 2026 drawdown.

---

## 5. Why scalping worked better in 2017–2021 than now: data on how the edge changed

### Takeaway
The conditions that made ProfitTrailer-style altcoin scalping work in 2017–2021 were: a fast-growing retail crowd, broad altcoin seasons where most coins rose against BTC, and many new listings that pumped. Since 2023 the market has become institutional and BTC-dominated. Retail's share of flow has collapsed, the expected broad altseason never fully arrived, small caps have lost money over five years, and liquidity has concentrated in the top coins. A long-only dip-buying and DCA bot on alts had a strong tailwind in 2017–2021 and a headwind in 2024–2026.

### Cited Findings
- On Coinbase, retail's share of trading volume fell from about 80% in Q1 2018 to about 18% in Q1 2024, as institutional volume grew. — [GreySpark Substack citing The Block](https://greyspark.substack.com/p/institutional-crypto-trading-volumes) **[secondary, citing The Block data]**
- **[historical]** Global daily active users of crypto exchange apps rose "from 100,000 to more than 30 million" between August 2015 and November 2021, with surges triggered by rising BTC prices. — [The Block on BIS data](https://www.theblock.co/news/regulation/2023-02-20-majority-of-bitcoin-retail-investors-lost-money-in-the-last-seven-years-bis-213372); [BIS WP 1049](https://www.bis.org/publications/working-paper-1049-crypto-trading-and-bitcoin-prices-evidence-new-database-retail-adoption.pdf)
- Altcoin Season Index history: in 2023 it was "largely below 30". In March 2024 it only briefly crossed 75. It peaked at 88 in December 2024, "however, a sustained or broad-based 'Altcoin Season' failed to materialize". Since early 2025 it occasionally hit about 12, and was about 41 in February 2026. — [Bitpanda: Bitcoin vs. Altcoins](https://blog.bitpanda.com/en/bitcoin-vs-altcoins-which-market-phase-dominating-and-what-it-means-investors) **[exchange research blog]**
- After BTC's March 2024 all-time high, "the rotation outward into altcoins that had taken place in previous cycles didn't occur… BTC dominance remained almost flat". Even the November 2024 rally only moved BTC dominance from 57% to 51%. In previous post-halving periods ETH grew 5–10x in market cap; in 2024 it lagged. — [Bybit x Block Scholes: The Altcoin Rotation](https://www.blockscholes.com/research/bybit-x-block-scholes-the-altcoin-rotation-why-and-when-altcoins-outperform-bitcoin) **[industry research]**
- The CryptoRank altseason index went from about 88 in December 2024 to 16 by April 2025. Alt volume concentrated in the top 10 altcoins as "institutional flows [were] channeled into Bitcoin and Ethereum exchange-traded products". — [CryptoSlate](https://cryptoslate.com/small-cap-crypto-assets-just-hit-a-humiliating-four-year-low-proving-the-alt-season-thesis-is-officially-dead)
- Kaiko Q1 2025: weekly volumes for major tokens were down 30% from late 2024. AI and memecoin sectors posted "average losses above 50%". Altcoin volatility hit "multi-year or all-time highs for certain tokens", and the environment "favored larger-cap assets". — [TradingView/NewsBTC on Kaiko Q1 2025 report](https://www.tradingview.com/news/newsbtc:3c89383f8094b:0-kaiko-report-highlights-key-drivers-of-q1-crypto-market-decline-and-outlook-for-q2)
- Derivatives were 77.5% of total exchange volume in 2025, with perpetuals at about $62T of $79T. Market-research firm's estimate. — [Mordor Intelligence](https://www.mordorintelligence.com/industry-reports/crypto-exchange-market) **[market-research vendor, moderate reliability]**
- One claim says "over 70% of crypto trade volume is driven by automated trading bots" and that algorithmic volume "exceeded $94 trillion" in 2023. It is unsourced and comes from a market maker's blog. — [Gravity Team blog](https://www.gravityteam.co/blog/ai-crypto-market-making-trading) **[low reliability; no primary data]**
- Academic shift: data before 2019 shows TA rules profitable with large cost margins ([Hudson & Urquhart 2021](https://link.springer.com/article/10.1007/s10479-019-03357-1)). A 2024 study finds weak-form efficiency and calls the earlier evidence possibly "sample-specific" ([Jin, Jung & Song 2024](https://www.emerald.com/jdqs/article/32/1/23/1214013/Do-technical-trading-rules-outperform-the-simple)).

### Inferences
- In 2017–2021, ProfitTrailer's edge was probably mostly **market beta plus regime**: a long-only bot buying dips in a broad uptrend, on alts that rose against BTC, recovers almost every bag, so DCA looks like a sure thing. The trailing logic and indicators mattered less than the tailwind. This fits the academic finding that rule profitability is sample-specific.
- Less naive retail flow, more professional market makers quoting tightly near mid (see the Kaiko 0.1% depth observation), and liquidity concentrated in the top coins all reduce the small, frequent mispricings that retail scalpers used to capture.
- Retail speculative activity has moved to perps and on-chain memecoins. A spot BTC/USDT-quoted altcoin scalping bot now competes in a thinner, more professional order book.

### Gaps
- I found no direct quantitative series of "retail scalping edge over time", such as average intraday mean-reversion profit after costs by year for top-100 alts. The decay is inferred from regime and microstructure data.
- I found no reliable primary figure for the share of crypto volume executed by algorithms or bots. The 70% figure is unsourced.

---

## 6. What profitable retail bot users in 2025–2026 report doing differently

### Takeaway
There is little verifiable evidence of consistently profitable retail bot users in 2025–2026. The recurring practices are:
- trading only liquid majors (BTC, ETH, SOL, BNB);
- using grids only in ranges, with wide bands;
- capping or stopping DCA (hard stop-losses, limited safety orders);
- adding regime or session filters;
- forward testing instead of trusting backtests;
- avoiding leverage, or treating futures as a hedge rather than a return engine.

Where profitable bots are described, the edge tends to come from exchange-specific structure or microstructure (fees, rebates, specific inefficiencies), not from indicator signals.

### Cited Findings
- "Stick to liquid pairs. BTC, ETH, SOL, BNB. Avoid low-volume altcoins where spreads eat bot profit"; "Set the grid range wider than you think you need"; "Avoid leverage until you can calculate your liquidation price manually"; "Paper trade first". — [Pionex blog: 15 Reddit questions](https://www.pionex.com/blog/15-reddit-questions-about-crypto-trading-bots-and-pionex-answered-with-real-data) **[vendor summarising community]**
- Start with "a liquid and well-known pair like BTC/USDT or ETH/USDT". Test separately in bull, bear and sideways phases. "Trust behavior over ROI." — [3Commas Help: DCA Bot Backtesting Guide](https://help.3commas.io/en/articles/11477934-dca-bot-backtesting-guide) **[vendor]**
- Use stop-losses, cap averaging orders, reduce position size in volatility, and pause bots around major events or exchange outages. — [3Commas risk management guide](https://3commas.io/blog/ai-trading-bot-risk-management-guide) **[vendor]**
- One r/algotrading user runs a mean-reversion Freqtrade strategy with a custom entry check "to not trade in Asian session. It's low liquidity". — [r/algotrading "New - Best Freqtrade Strategies"](https://www.reddit.com/r/algotrading/comments/1im5huf/new_best_freqtrade_strategies) **[anecdote]**
- Another r/algotrading user says their profitable bot "doesn't predict the direction but exploits particular exchange" behaviour. The edge is structural, not TA. — [r/algotrading "Is TA algo trading real?"](https://www.reddit.com/r/algotrading/comments/1vpfgjp/is_ta_algo_trading_real) **[anecdote]**
- Threads still ask "Is anyone here actually successful at this in live real money?" — the poster says "most never pan out". — [r/algotrading](https://www.reddit.com/r/algotrading/comments/1u9ongr/genuine_question_is_anyone_here_actually) **[anecdote]**
- Freqtrade recommends dry-run/forward testing as "a much more reliable indicator of potential performance than backtesting". — [Freqtrade docs](https://www.freqtrade.io/en/stable/strategy-101)
- Academic support for regime and trend filters as risk tools: TA rules' main documented benefit is "significantly reduc[ing] the potential drawdowns" ([Hudson & Urquhart](https://link.springer.com/article/10.1007/s10479-019-03357-1)), and the 2024 outperformance is "especially risk–return wise" ([Deprez & Frömmel 2024](https://ideas.repec.org/a/eee/reveco/v93y2024ipbp858-874.html)).
- An adaptive or reset grid on BTC and ETH only, with maker-level fees (0.08%), beat the static grid and buy-and-hold in a 2021–2024 backtest. — [arXiv 2506.11921](https://arxiv.org/abs/2506.11921) **[academic preprint; backtest]**
- Futures and leverage risk: on 10/10/2025, $16.7B of long positions were liquidated, against $2.5B of shorts, and auto-deleveraging force-closed even hedged and profitable positions. — [Datawallet (Coinglass data)](https://www.datawallet.com/crypto/october-10-crypto-crash-explained); [Galaxy Research](https://www.galaxy.com/insights/research/cryptos-flash-crash-liquidation-binance-adl-auto-deleveraging)
- Pionex markets a spot-futures funding-rate "arbitrage" bot as delta-neutral. That is a structural carry trade, not directional TA. — [YouTube "Best Crypto Trading Bots 2025"](https://www.youtube.com/watch?v=Pjpx7Ik3PB4) **[promotional video]**

### Inferences
- Taken together, a realistic 2026 retail bot has these features:
  - (1) BTC, ETH and a few top-10 pairs only, not a 50–100-pair altcoin universe;
  - (2) a regime filter that turns long-only DCA or dip-buying off in confirmed downtrends, for example price below the 200-day MA;
  - (3) a hard cap on DCA depth plus a portfolio-level stop;
  - (4) fee optimisation through the BNB discount or a VIP tier; maker-only orders alone do not lower fees for Binance Regular users;
  - (5) months of forward testing before scaling up;
  - (6) a benchmark against simple scheduled DCA or holding BTC, which beat a grid bot in at least one documented 2022–23 case.
- "Futures instead of spot" adds two-way trading but brings in liquidation and auto-deleveraging risk. On 10/10/2025 that risk was concentrated in exactly the leveraged long positions a DCA-style bot would hold.
- Realistic expectation: the best-supported claim is that a well-run bot can **reduce drawdown or smooth exposure** compared with holding. The claim that it can **reliably produce positive returns independent of market direction** is not supported. A user who scalped profitably in 2018–2021 should treat that history as largely regime-driven, not as proof of a durable edge.

### Gaps
- I found no verified, audited track records of 2025–2026 retail bot users, profitable or not. All "what works" evidence is vendor guidance or anonymous anecdote, with strong survivorship bias.
- I found no data comparing maker-only versus taker scalping profitability for retail accounts.
- I found no systematic evidence on whether regime filters such as 200DMA or BTC-trend gates improve live (not backtested) DCA-bot returns in 2024–2026.
