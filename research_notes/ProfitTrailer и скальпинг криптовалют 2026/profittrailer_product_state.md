# ProfitTrailer: product state as of October 2026

Research date: 2026-10-03. Sources were read with Tavily search/extract. GitHub API access to taniman/profit-trailer was blocked in this session, so release dates come from the public GitHub Atom feed and release pages. Anything marked [HISTORICAL] dates from 2017–2023. Anything marked [OFFICIAL] is the vendor's own claim and has not been checked independently.

---

## 1. Latest version, release cadence and how actively it is developed (2025–2026)

### Takeaway
The latest version is **ProfitTrailer 2.6.0 ("New GUI Release")**. GitHub shows it released on about 8 Sep 2026, and the Atom feed shows the entry was last updated on 2026-09-30. 2.6.0 is the first minor-version bump after a long 2.5.x line (2.5.63 to 2.5.72). Development continues, but at a slow pace that is mostly maintenance. There were 7 releases in 2025 (five of them in January–February), then no release for about 9.5 months (June 2025 to March 2026), then 3 releases in 2026. There is no "V3".

### Cited Findings
- **2.6.0, "New GUI Release".** GitHub UI date: "released this 08 Sep". Atom `<updated>`: 2026-09-30T12:41:28Z. It is described as "a major GUI update". New in it: **Kraken Futures support** (CROSSED/ISOLATED margin, `buy_leverage`), and an `allowed_underlying_type` pairs property for filtering Binance Futures underlying types (e.g. `COIN,TOKEN`). It also includes a modernized desktop and mobile GUI covering settings, config editing, trade tables, statistics, diagnostics and setup. Further changes: **Test mode can start without exchange API keys**, strategy actions pause during exchange API cooldowns, Poloniex and stale-WebSocket handling is better, and there are fixes for formula variable/token replacement plus "diagnostics for invalid formulas", DCA max-cost validation, and "short PT Assistant API keys". Compatibility: Windows/Linux/macOS; Chrome, Firefox and Safari, with Edge limited. — [GitHub releases.atom](https://github.com/taniman/profit-trailer/releases.atom); [GitHub releases page](https://github.com/taniman/profit-trailer/releases)
- **2.5.72**, 2026-05-05: "Fix BINANCEFUTURES websockets system upgrade" plus small fixes. — [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)
- **2.5.71**, 2026-03-26: rebuilt stats indexes, a config-validation fix for single-letter coins, an ATR/HMA fix, Huobi spot websocket and Huobi Futures fixes, a fix for NaN indicators, a fix for orders created directly on Binance, and a switch of the Binance ticker websocket to individual tickers "instead of deprecated event". — [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)
- **2.5.70**, 2025-06-10: allow BUY_TIMEOUT_AFTER_SELL for DCA EQ sells, plus Kraken and Huobi Futures fixes. — [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)
- **2.5.69**, 2025-03-13: fixed the Bybit "account type only support UNIFIED" error. **2.5.68**, 2025-02-17: Bybit leverage info fix and an EQ sale rounding fix. **2.5.66** and **2.5.65**, both 2025-01-14: fixes for Bybit COIN-M and Bybit API changes that hid balances. **2.5.64**, 2025-01-13. **2.5.63**, 2025-01-08: fixed Bybit price rounding and a Bybit spot crash. 2.5.67 does not appear in the release list. — [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)
- Every 2.5.x release carries the warning "You **CANNOT** rollback after upgrading from a 2.4.x version" and points to the 2.5.0 notes. — [GitHub releases](https://github.com/taniman/profit-trailer/releases)
- **2.5.0 ("2.5.0 is here!")** was a breaking release. Its notes include "Properties and Strategies REMOVED (DO NOT SKIP) – You will need to remove all of these properties from your current config… already deprecated in 2.4 release", plus Breaking Changes, NEW Exchanges, NEW INDICATORS and "Dynamic logic properties". The exact date could not be extracted. — [GitHub release 2.5.0](https://github.com/taniman/profit-trailer/releases/tag/2.5.0)
- An undated 2.5.x "Anniversary New Features" release added `FUNDINGFEE` as a dynamic variable for open positions and user-defined global variables (`X_BUY_VAR_FORMULA`/`X_BUY_VAR_LABEL`, `X_SELL_VAR_FORMULA`/`LABEL`) for use in formulas. It also added Bybit exchange-side TPS/TSL/SL orders and funding-fee registration for test-mode bots. — [GitHub releases page 3](https://github.com/taniman/profit-trailer/releases?page=3)
- The GitHub repo distributes **binaries only**. Every release tag points to the same commit `04d8f20` ("Update README.md", May 14, 2020), the signing GPG key is shown as "Expired", and releases are published by the single account `taniman`. — [GitHub tags](https://github.com/taniman/profit-trailer/tags)
- [OFFICIAL] TOS: "Lifetime licenses are version controlled. If you own a Multi Exchange V2 license you get new features and bug fixes until V3 is released. Once V3 is released we will only do critical bug fixes… Once V4 is released V2 will not receive any more bug fixes." — [ProfitTrailer Terms of Service](https://profittrailer.com/terms-of-services)
- [OFFICIAL] The Multi Exchange Upgrade product page says "If you wish to upgrade to V3 when it comes out you would have to pay an upgrade fee". As of Oct 2026 no V3 exists; 2.6.0 is the latest. — [Multi Exchange Upgrade](https://profittrailer.com/product/profittrailer-multi-exchange-upgrade); [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)
- Wiki freshness: the "Exchange info" page reads "Last edited by Administrator 01/21/2024". — [Wiki Exchange info](https://wiki.profittrailer.com/en/exchangeinfo). The changelog URL `wiki.profittrailer.com/en/changelog` returns 404. — (tavily_extract result, 2026-10-03)

### Inferences
- Since 2025 the work has been mostly **reactive maintenance**: keeping up with exchange API changes on Bybit, Binance and Huobi. 2.6.0 is the first sizable feature/UI release in a long time. It came out on 8 Sep, ProfitTrailer's founding anniversary (the company "was started in September 8th 2017"), which suggests an anniversary-timed release.
- The 9.5-month gap with no release (Jun 2025 to Mar 2026) is a warning sign of limited development capacity. It looks like a small team, possibly a single maintainer.
- A returning user whose configs date from 2018–2021 (2.0–2.4 era) should expect to **rewrite or migrate configs**. 2.5.0 removed properties deprecated in 2.4, and once upgraded you cannot roll back.

### Gaps
- I could not get exact dates for 2.5.0 through 2.5.62 (the GitHub UI extracts had no timestamps), so 2023–2024 cadence is unknown.
- I found no official public roadmap or V3 timeline. news.profittrailer.com could not be fetched.
- The size of the dev team and any staff changes are unknown.

---

## 2. Licensing and pricing today

### Takeaway
[OFFICIAL] The headline offer is a **subscription at €50/month or €449/year**: "License Only", run 3 live bots, 7 config slots. The **€1,999 lifetime license is listed but shown as "Out of stock"**, so it cannot currently be bought. Add-ons are billed separately: API key slots, TradingView integration, config slots, signals, and hosted VPS. Old "legacy" single-exchange lifetime licenses still work on V2 and can be upgraded to multi-exchange for €200.

### Cited Findings
- [OFFICIAL] Homepage pricing: Subscription "Monthly / Yearly €50 / 449, Save 25% with yearly billing, License Only". It includes the listed crypto exchanges plus OANDA forex, "Live Support On Discord", "Run 3 live bots", "Store up to 7 custom configurations", "40+ Buy-Sell Indicators", "Advanced Paper Trading", "Advanced Notification" and "Advanced Stats". The Lifetime tier is **€1,999** with the same feature list. — [profittrailer.com](https://profittrailer.com)
- [OFFICIAL] The Lifetime (License Only) product page (SKU PTPRLIFEADVANCEDV2) shows **"€1,999.00 Out of stock"**. — [Lifetime product page](https://profittrailer.com/product/profittrailer-lifetime-license-only/)
- [OFFICIAL] The Sub (License Only) page shows "From: €50.00 / month" with 1-month and 12-month plans. — [Sub product page](https://profittrailer.com/product/profittrailer-subscription-license-only/). An indexed variant of the same product showed "From: €50.00 / month and a €9,999.00 sign-up fee". This looks like a store-configuration artifact; the live page does not show it. — [profittrailer.com?p=76954 search snippet](https://profittrailer.com?p=76954)
- [OFFICIAL] The "All-In-1 Subscription" (SKU PTCLOUD) offers variants "Advanced Cloud 3 Bots, Basic Cloud 3 Bots, Signals Cloud 2 Bots, Basic Cloud 2 Bots, Advanced Cloud 2 Bots" on 1- or 12-month plans. No price was visible in the extract. — [All-In-1 Subscription](https://profittrailer.com/product/profittrailer-subscription)
- [OFFICIAL] Add-ons: **API key slot €12.50/month**, **Config Save Slots €10–€50**, **PT TradingView Integration from €5/month**, **Multi Exchange Upgrade €200** (marked down from €300, "ONLY FOR LEGACY LICENCES", and the upgrade "locked to version 2"). — [Multi Exchange Upgrade](https://profittrailer.com/product/profittrailer-multi-exchange-upgrade); [TradingView Integration](https://profittrailer.com/product/pt-tradingview-integration/)
- [OFFICIAL] Hosting: "ProfitTrailer VPS" from €15/month for 1–5 live bots, with automatic PT updates and monitoring. — [PT VPS](https://profittrailer.com/product/profittrailer-vps). "ProfitTrailer Hetzner VPS" from €40/month ("prices are the same as the provider… round up and add €5 management fees"), pre-installed with PTManager, "1-2 GB of RAM to run 1 bot". — [Hetzner VPS](https://profittrailer.com/product/profittrailer-hetzner-vps)
- Third-party pricing summary (BitDegree): lifetime €1,999; subscription €50/month; TradingView €5/month; API slot €12.5/month; config slots €10–50; multi-exchange upgrade €200; signals "from €14.99 to €50.00/month" depending on provider; Hetzner VPS "from €12/month". The VPS figure conflicts with the current official €40. — [BitDegree review](https://www.bitdegree.org/crypto/profit-trailer-review)
- [OFFICIAL] TOS terms that matter. Refunds only within 14 days and only on the first order, pro rata, and "not granted because of market conditions and performance of settings". No refunds on renewals, upgrades, API or config products. "We do not allow or support resale of the license". "We do not allow the sale or renting of settings… liable for up to 100000 Euro". Up to €500,000 liability for altering the software and €1,000,000 for using a cracked version. License "for personal use". "ProfitTrailer is not responsible for any support or maintenance regarding the Website or Software." TOS version 2.7, last updated 01.01.2021. — [Terms of Service](https://profittrailer.com/terms-of-services)
- [OFFICIAL] If an exchange "packs up and leaves", support is removed and legacy holders of that exchange get 50% off the multi-exchange upgrade. — [Terms of Service](https://profittrailer.com/terms-of-services)
- Secondary market: r/ProfitTrailer has posts selling lifetime licenses at a steep discount, e.g. "Selling ProfitTrailer lifetime license, priced at 500 USDT" (post ID suggests about late 2024) and "Selling ProfitTrailer lifetime + feeder (worth $2000 and sell it for 500$)". The TOS forbids resale. — [r/ProfitTrailer listing](https://www.reddit.com/r/ProfitTrailer/comments/1hmnat5/selling_profittrailer_lifetime_licence); [r/ProfitTrailer](https://www.reddit.com/r/ProfitTrailer)

### Inferences
- In practice a new license today means a **subscription of about €449–600/year**, before VPS, API slots or TradingView. A fully kitted setup (subscription, TradingView and a VPS) costs roughly €700–1,100/year. That is far more than free open-source alternatives.
- Lifetime licenses selling at about 75% off on Reddit suggests weak perceived value and many inactive former users.
- A returning user who **already owns a legacy or V2 lifetime license** can probably reactivate at little or no cost. They would pay only if they need the multi-exchange upgrade (€200) or extra slots. This is the strongest economic argument for returning.

### Gaps
- Prices for the All-In-1 "Cloud" tiers (Basic, Advanced, Signals) were not visible.
- It is unclear whether "Out of stock" on the lifetime license is temporary or a quiet discontinuation.
- No price-change history was found. The €50/month figure appears in BitDegree and other reviews, so it seems stable.

---

## 3. Feature set: strategies, DCA, trailing, paper/test mode, backtesting, config format and automation

### Takeaway
ProfitTrailer is still the same **indicator-threshold, property-file-driven bot** returning users will recognize. Strategies are lettered (`DEFAULT_A_buy_strategy = LOWBB`, etc.) and combined through boolean and level formulas. It adds trailing buy/sell, a deep DCA engine, Sell-Only Mode, reversal trading, user variables, shorting on futures, signals and TradingView alerts (paid add-on). It has **paper/Test Mode but no evidence of a native backtester**: the official wiki tells users to run Test Mode "for a few weeks" instead.

### Cited Findings
- Config model: settings live in three GUI sections, **Indicators, Pairs and DCA**. Example syntax: `DEFAULT_A_buy_strategy = LOWBB`, `DEFAULT_A_buy_value = 0`, `DEFAULT_A_buy_value_limit = -10`, `DEFAULT_B_buy_strategy = STOCH`… "You can have 103 strategies used at one time, so A through CZ." — [Wiki: Buy and Sell Logic](https://wiki.profittrailer.com/en/buyandselllogic)
- Indicator parameters go in the Indicators tab with candle periods in **seconds**, e.g. `RSI_candle_period = 7200`, `RSI_length = 14`. Named examples include SAR, RANGEFILTER and ADX+DI. — [Wiki: Understanding indicators](https://wiki.profittrailer.com/en/Academy/Basic/Indicators)
- Strategy names in official materials: LOWBB, HIGHBB, RSI, STOCH, GAIN, EMACROSS, BBWIDTH, MACD, EMAGAIN, SIGNAL, REVERSALGAIN; HMA/ATR are mentioned in 2.5.71 fixes. — [Wiki: Buy and Sell Logic](https://wiki.profittrailer.com/en/buyandselllogic); [All-In-1 product page](https://profittrailer.com/product/profittrailer-subscription); [Wiki FAQ](https://wiki.profittrailer.com/en/common); [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)
- Strategy counts are inconsistent across official pages. The homepage says "More than 40 built-in indicators". Product pages say "20+ different buy/sell strategies… combine up to 26". The wiki says 103 (A–CZ). — [profittrailer.com](https://profittrailer.com); [Lifetime product](https://profittrailer.com/product/profittrailer-lifetime-license-only/); [Wiki Buy/Sell Logic](https://wiki.profittrailer.com/en/buyandselllogic)
- Formulas: `default_buy_strategy_formula` and `default_sell_strategy_formula` allow any boolean combination, e.g. "Formula - A || (B && D)". A "Level(X) formula" requires strategies to become true **in a certain order**. — [Wiki: Web Interface Guide](https://wiki.profittrailer.com/webinterfaceguide); [Wiki: Buy Strategy Level(X) Formula](https://wiki.profittrailer.com/config/buystrategylevelxformula). User-defined global variables (`X_BUY_VAR_FORMULA`) and a `FUNDINGFEE` variable were added in 2.5.x. — [GitHub releases p.3](https://github.com/taniman/profit-trailer/releases?page=3)
- Trailing: `DEFAULT_trailing_buy` (trails price downward before buying) and `DEFAULT_trailing_profit` (trails upward before selling). — [Wiki: Buy and Sell Logic](https://wiki.profittrailer.com/en/buyandselllogic)
- DCA: `DEFAULT_DCA_enabled = true` or a percent trigger (e.g. `-2`), `DEFAULT_DCA_buy_percentage`, `max_cost`, `max_buy_times`, separate DCA sell strategies, and level-specific settings. — [Wiki: Buy and Sell Logic](https://wiki.profittrailer.com/en/buyandselllogic)
- Reversal trading: intentionally sells at a loss and rebuys lower (`reversal_start_trigger`, `reversal_rebuy_drop_trigger`, `reversal_rebuy_rise_trigger`), with a REVERSALGAIN sell strategy. — [Wiki: Buy and Sell Logic](https://wiki.profittrailer.com/en/buyandselllogic)
- Filters and protections shown in the GUI: Sell Only Mode (SOM) triggers, panic sell, sell-wall detection, min/max 24h change %, `pair_min_listed_days` ("TOO NEW"), max spread, min buy volume, rebuy timeout, max pairs, and signal label matching. — [Wiki: Web Interface Guide](https://wiki.profittrailer.com/webinterfaceguide)
- Shorting: "ProfitTrailer supports shorting on BitMEX and Binance Futures and Bybit exchange." A bot runs **either** long or short mode, set with `shorting = true` in PAIRS. — [Wiki FAQ](https://wiki.profittrailer.com/en/common)
- Signals and TradingView: `DEFAULT_A_buy_strategy = SIGNAL` buys from signal providers. — [Wiki: Signal Setup](https://wiki.profittrailer.com/signals). [OFFICIAL] The TradingView Integration add-on (from €5/month) lets "TradingView… send alerts to your bot". — [PT TradingView Integration](https://profittrailer.com/product/pt-tradingview-integration/)
- Paper trading: "Run in Test Mode" toggle and "Test Mode Balance" setting. — [Wiki: Web Interface Guide](https://wiki.profittrailer.com/webinterfaceguide). 2.6.0 lets Test mode start without exchange API keys. — [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)
- **Backtesting:** the official wiki repeatedly says "We always suggest to run your bot in Test Mode for a few weeks before really taking off". No backtesting feature appears in the official site's feature list, the wiki pages reviewed, or the 2025–2026 release notes. — [Wiki: Indicators](https://wiki.profittrailer.com/en/Academy/Basic/Indicators); [profittrailer.com](https://profittrailer.com). Coinspot claims PT "offers paper trading and backtesting". This conflicts with the official materials and the claim is unsourced. — [Coinspot review](https://coinspot.io/en/reviews/profit-trailer)
- Notifications: Discord bot (two instances) and Telegram. — [Wiki: Web Interface Guide](https://wiki.profittrailer.com/webinterfaceguide)
- License and API-key management goes through the "PT Assistant" Discord bot and settings tab (voucher redemption for license upgrades, API slots, configs, signals). — [Wiki: PT Assistant](https://wiki.profittrailer.com/ptassistant); [Wiki: Web Interface Guide](https://wiki.profittrailer.com/webinterfaceguide)
- Runtime: a Java application started with `Run-ProfitTrailer.cmd` ("If you did double click the jar file ProfitTrailer will not run"), with a browser GUI. — [Wiki FAQ](https://wiki.profittrailer.com/en/common)
- Bot management: the official PTManager (GitHub org `profittrailerbv`, repo ProfitTrailerManager) comes pre-installed on the Hetzner VPS product. — [Hetzner VPS](https://profittrailer.com/product/profittrailer-hetzner-vps); [GitHub ProfitTrailerManager](https://github.com/profittrailerbv/ProfitTrailerManager)

### Inferences
- For a user who already writes PT configs, the core mental model and property syntax still apply. Formulas, levels and variables give more expressive logic than in 2018–2020.
- The lack of a native backtester is the largest functional gap against Freqtrade, Gunbot and Cryptohopper. Validating a scalping strategy means weeks of forward testing in Test Mode, or building an external backtester that re-implements PT's indicator semantics.
- PT is closed source, and the TOS forbids altering or reverse-engineering it. Automation is therefore limited to config edits, TradingView/signal inputs and companion tools. Custom code cannot run inside the strategy loop.

### Gaps
- I did not retrieve the full current list of indicators and strategies; the wiki strategies URL `/en/strategies` returned 404. Whether newer strategy types exist (e.g. VWAP, ichimoku) is unverified.
- No public REST API documentation was found. Whether PT exposes a documented local API, as earlier add-ons relied on, could not be confirmed.
- Whether order-book or tick-level scalping is supported (versus candle-based indicators with 1m minimum periods) was not documented in the pages reviewed. The minimum candle period listed is 1m = 60 seconds.

---

## 4. Ecosystem tools (PT Feeder, PT Magic, trackers) and community activity in 2025–2026

### Takeaway
The third-party ecosystem that once made PT stand out (PT Feeder, PT Magic, PT+) has largely **stalled**. Code pushes stopped in 2023–2024, and **PT Feeder is listed as "Out of stock" in the official shop**. Community activity is low: Trustpilot has 0 reviews in the last 12 months, and Reddit mostly has "is it still active?" threads and license resale posts.

### Cited Findings
- [OFFICIAL] The PT Feeder product page shows "€169.00 Out of stock". It is described as automated on-the-fly changes to PT settings based on market and pair indicators, PT exposure, and volatility. — [PT Feeder product](https://profittrailer.com/product/pt-feeder)
- GitHub `mehtadone/PTFeeder`, the "Official GitHub for… PT Feeder" (docs and README only): 175 stars, **last push 2023-05-29**. — [GitHub PTFeeder](https://github.com/mehtadone/PTFeeder) (push date from a GitHub repository search run 2026-10-03)
- GitHub `PTMagicians/PTMagic` ("A Complete Profit Trailer Add-On"): 49 stars, **last push 2024-04-14**. — [GitHub PTMagic](https://github.com/PTMagicians/PTMagic) (push date from GitHub search)
- Official `profittrailerbv/ProfitTrailerManager`: 12 stars, last push 2024-11-22. — [GitHub ProfitTrailerManager](https://github.com/profittrailerbv/ProfitTrailerManager)
- Other community repos are mostly dormant. `ptplus/ptplus` ("Profit Trailer's Missing GUI"): last push 2023-04-23. `ColeBennett/binance-auto-blacklist`: 2022-09. `rafffael/profit-trailer` Docker: 2023-12. `canecasama/profittrailer_nas`: 2024-06. `izzymoren0/profittrailer` container PoC: 2025-07. — [ptplus](https://github.com/ptplus/ptplus); [binance-auto-blacklist](https://github.com/ColeBennett/binance-auto-blacklist); [rafffael/profit-trailer](https://github.com/rafffael/profit-trailer); [canecasama/profittrailer_nas](https://github.com/canecasama/profittrailer_nas)
- **Caution:** an unofficial repo `insignificant-pigeonhole504/profit-trailer`, created and pushed 2025-11-14 with 0 stars, describes itself as "Automate your cryptocurrency trading with ProfitTrailer, a customizable bot featuring backtesting". Its random username and its claim of a backtesting feature not found in official docs fit common fake-download/malware lure patterns. Use only the official `taniman/profit-trailer` releases. — [GitHub repo](https://github.com/insignificant-pigeonhole504/profit-trailer)
- Trustpilot: 13 reviews, TrustScore 4.1, **"0 reviews in the last 12 months"**, and "This company hasn't invited customers recently". Almost all reviews are from a Feb 13–16, 2021 burst. The newest is Mar 2, 2021, 1 star: "pt went from great to terrible. Left a few weeks ago, will not return." — [Trustpilot](https://www.trustpilot.com/review/profittrailer.com)
- [HISTORICAL, 2021] Trustpilot praise: "The most sophisticated retail bot available. With an add-on like PTFeeder or PTMagic the amount of configuration possible is mind-boggling… not for beginning traders." Criticism: "No strategies on the default lists, not a clear guide… many others (also free) bot give more." — [Trustpilot](https://www.trustpilot.com/review/profittrailer.com)
- Discord is the only official support channel. BitDegree (undated) reports "4,000+ members". — [BitDegree review](https://www.bitdegree.org/crypto/profit-trailer-review). [OFFICIAL] The homepage advertises "Live Support On Discord" and "A wide and dedicated community". — [profittrailer.com](https://profittrailer.com)
- Reddit r/ProfitTrailer topics include "Is ProfitTrailer still active?" (post ID suggests about Jan 2024), "Selling profittrailer lifetime licence" (about late 2024), and [HISTORICAL] "Does anybody still actively use their profit trailer trading bot…", with the reply "I haven't turned mine back on in about 18 months… might have broken even". The post contents could not be fetched; snippets only. — [Is ProfitTrailer still active?](https://www.reddit.com/r/ProfitTrailer/comments/190oerf/is_profittrailer_still_active); [Does anybody still actively use…](https://www.reddit.com/r/ProfitTrailer/comments/qev0k1/does_anybody_still_actively_use_their_profit)

### Inferences
- A returning user should not count on PT Feeder or PT Magic as maintained dynamic-config layers. Building their own config-switching layer (scripts that rewrite PT config files or use PTManager) is probably required.
- Measurable public engagement (Trustpilot, Reddit, GitHub) has declined sharply since about 2021. The Discord may be more active than this public footprint suggests, but I could not measure that.

### Gaps
- I could not get current Discord member or online counts (the invite link and API were not reachable through the proxy). The "4,000+" figure is undated.
- "PT Tracker": no current repo or product was found.
- Reddit posts could not be fetched (Tavily extract failed), so exact post dates and comment sentiment are approximate.
- No 2025–2026 YouTube reviews dedicated to PT were found; the 2025 YouTube results were generic bot roundups.

---

## 5. Supported exchanges in 2026: spot vs futures, and dropped exchanges

### Takeaway
[OFFICIAL] Supported: **Binance (spot and Futures USDⓈ-M/COIN-M), Binance US, Bybit (spot, inverse, USDT perps), KuCoin and KuCoin Futures, Huobi/HTX and Huobi Futures, Kraken spot, Kraken Futures (new in 2.6.0), Poloniex, and OANDA (forex)**. BitMEX is still referenced for shorting in the wiki. **OKX, Coinbase, Bitget, Gate.io and Hyperliquid are not listed** anywhere official. Much of the exchange documentation is stale.

### Cited Findings
- [OFFICIAL] Homepage exchange list: "Poloniex, Binance, BinanceUS, Binance Futures, Kucoin, Kucoin Futures, Huobi, Huobi Futures, Bybit, Bybit Futures, Kraken" plus "OANDA Forex". — [profittrailer.com](https://profittrailer.com)
- [OFFICIAL] 2.6.0 adds **Kraken Futures**, with cross and isolated margin. — [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)
- Wiki exchange page (last edited 01/21/2024) covers Binance.com, Binance US, "Binance DEX (binance.org)", Binance Futures (USD(s)-M listing "USDT, BUSD"; COIN-M), Poloniex, Bitmex (XBT), KuCoin and KuCoin Futures (USDTM and coin-margined), Huobi and Huobi Futures ("Huobi Global is now HBG.com"), Bybit spot, Bybit inverse and Bybit USDT perpetual, Binance.us ("US Allowed"), Kraken Spot ("US Allowed"), and OANDA. Minimum candle period on most exchanges is 1m. — [Wiki: Exchange info](https://wiki.profittrailer.com/en/exchangeinfo)
- Shorting is supported on BitMEX, Binance Futures and Bybit (one direction per bot). — [Wiki FAQ](https://wiki.profittrailer.com/en/common)
- Exchange-specific maintenance in 2025–2026 releases touched Bybit (UNIFIED account, COIN-M, rounding, leverage), Binance (ticker websocket, Futures websocket), Huobi spot and futures, Kraken and Poloniex. This shows these integrations are still being kept alive. — [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)
- [HISTORICAL] Older third-party lists mention Bittrex and BitMEX among PT's exchanges. — [Coinspot review](https://coinspot.io/en/reviews/profit-trailer)
- [OFFICIAL] The shop footer lists "Sponsors: Binance, Bybit, Kucoin". — [Lifetime product page](https://profittrailer.com/product/profittrailer-lifetime-license-only/)

### Inferences
- The wiki still references BUSD and "Binance DEX (binance.org)", and calls Huobi "HBG.com" rather than its current HTX brand. This is based on general knowledge, not a source fetched here: Binance wound down BUSD in 2023–24 and the BNB Beacon Chain/Binance DEX was sunset in 2024. The exchange docs have therefore not kept pace with reality.
- Bittrex (closed 2023) no longer appears in the official list, so it appears dropped. BitMEX is absent from the homepage list but still in the wiki, so its status is unclear.
- For a scalper, the practical venues are Binance/Binance Futures, Bybit, KuCoin and Kraken. Users who need OKX, Bitget, Coinbase Advanced or Hyperliquid must look elsewhere. Freqtrade reaches these through CCXT, and Gunbot lists OKX, Coinbase and others.

### Gaps
- There is no authoritative, dated official list of dropped exchanges (Bittrex, BitMEX, Binance DEX).
- Whether Binance US and KuCoin integrations still work end-to-end in 2026 was not independently verified.

---

## 6. Known problems, complaints, controversies, security issues and decline signals

### Takeaway
I found **no evidence of a hack, exit scam or security breach**. The signals of decline or neglect are many: a stale website (the pricing page is a lorem-ipsum template, the footer says © 2021), the lifetime license and PT Feeder are out of stock, there are no Trustpilot reviews in the last 12 months, the ecosystem repos are dormant, there was a 9.5-month release gap, the wiki is out of date, and licenses resell at about 75% off. The licensing and TOS terms are restrictive and owner-friendly, and the legal entity is in Curaçao.

### Cited Findings
- The official `/pricing` page renders a theme placeholder ("Lorem ipsum…", clothing size charts "XS 34-36… Bust, cm"). — [profittrailer.com/pricing](https://profittrailer.com/pricing)
- Site and product page footers read "© 2021 All rights reserved". — [Lifetime product page](https://profittrailer.com/product/profittrailer-lifetime-license-only/)
- Lifetime license "Out of stock"; PT Feeder "Out of stock". — [Lifetime](https://profittrailer.com/product/profittrailer-lifetime-license-only/); [PT Feeder](https://profittrailer.com/product/pt-feeder)
- Legal entity: "ProfitTrailer B.V., a limited liability company incorporated under the laws of the Curaçao… registration number 149091… Kaya Seru Kristòf 9, Curaçao". Disputes go exclusively to the courts of Willemstad, Curaçao. — [Terms of Service](https://profittrailer.com/terms-of-services). Coinspot says the team operates out of Rotterdam, Netherlands, with the entity registered in Curaçao, and tags PT "High-Risk Project — Not Recommended". — [Coinspot review](https://coinspot.io/en/reviews/profit-trailer). Trustpilot lists the contact country as the Netherlands and warns "This company may be associated with high-risk investments." — [Trustpilot](https://www.trustpilot.com/review/profittrailer.com)
- The TOS disclaims responsibility for support and maintenance and imposes large contractual penalties: €500k for altering the software, €1M for cracked versions, €100k for selling or renting settings. — [Terms of Service](https://profittrailer.com/terms-of-services)
- [HISTORICAL, 2019] Reddit: "Profit Trailer setup is convoluted. Their licensing and activation process is horrible. They'll keep your information such as your name/address…" — [r/ProfitTrailer "My review of pt"](https://www.reddit.com/r/ProfitTrailer/comments/btphm2/my_review_of_pt)
- Negative review (undated, low-quality site): "the interface of the trading bot is far behind the leading trading robots… clients… have many times reported about different types of glitches". — [EliteCurrensea](https://elitecurrensea.com/software-providers/profit-trailer)
- Security: BitDegree says "no scam reports or hacking incidents to date" and stresses SSL and VPS setup. — [BitDegree](https://www.bitdegree.org/crypto/profit-trailer-review). PT is self-hosted, so API keys stay on the user's machine or VPS. — [profittrailer.com](https://profittrailer.com)
- Signs of reduced media visibility: Zignaly's PT review page (originally May 2022, "updated" March 30, 2026) still says PT "receives regular updates" but is generic, and Zignaly itself no longer offers DIY bots. — [Zignaly review](https://zignaly.com/crypto-trading/bots/profittrailer-bot-review)
- Release notes list recurring exchange-breakage fixes, e.g. "Fix Bybit API change causing coin balances not to be seen" and "Fix Bybit spot crashing". Each exchange API change has caused temporary breakage until a patch shipped. — [releases.atom](https://github.com/taniman/profit-trailer/releases.atom)

### Inferences
- The company is operating and shipping (2.6.0 in Sep 2026), but it looks like a **low-investment, maintenance-mode business**. The storefront, docs and community are not being refreshed.
- The main risks to a returning user are dependency risks rather than fraud: exchange APIs breaking with slow fixes, no backtester, a closed and unmodifiable codebase, and vendor-controlled license activation through Discord and PT Assistant. If the vendor stops operating, license validation could prevent the bot from running. This is inferred from the license model; no kill-switch behaviour was documented.

### Gaps
- No outage reports or status-page history were found.
- Nothing is known about ownership or management changes, and there was no news coverage of the company in 2025–2026.
- No independent security audit exists.

---

## 7. How ProfitTrailer compares to alternatives in 2026

### Takeaway
PT is now a niche, closed-source, self-hosted bot that costs about €450–600/year with no native backtesting. **Freqtrade** (free, open-source Python, strong backtesting and hyperopt, CCXT exchange breadth) beats it on flexibility and validation for a config- or strategy-writing user. **Gunbot** is the closest commercial analogue (self-hosted, one-time license, backtesting, JS strategies on higher tiers). Cloud SaaS bots (3Commas, Cryptohopper, Bitsgap) are cheaper per month and include backtesting or marketplaces, but they hold your API keys in the cloud. **ProfitTrailer does not appear in the major 2026 comparison lists reviewed.**

### Cited Findings
- Freqtrade: "Free and open source", "Strong backtesting and optimization features", "Python strategies, backtesting, broad exchange support via CCXT". Downside: "Requires technical setup and ongoing maintenance". — [TokenTax, updated Jul 2026](https://tokentax.co/blog/best-crypto-trading-bot). Freqtrade is described as the only Hyperliquid-compatible bot "with a first-class backtesting workflow" (`freqtrade backtesting`, Python `IStrategy` class, GPL-3.0). — [Chainstack, 2026](https://chainstack.com/hyperliquid-trading-bots-2026)
- Hummingbot: free and open source, "Best for market making and arbitrage builders", with a strong CEX/DEX connector ecosystem. — [TokenTax](https://tokentax.co/blog/best-crypto-trading-bot)
- Gunbot pricing conflicts between sources: "$45-499 once" with grid, DCA, futures and backtest features — [bitcointradingbots.com (2026)](https://bitcointradingbots.com/bots); "€59–€249 lifetime" with backtesting, simulated trading, TradingView alerts, REST API and custom JavaScript strategies on higher tiers — [Phaedra Solutions](https://www.phaedrasolutions.com/blog/best-ai-trading-bots); "One-time purchase from 0.008 BTC (~$400)" with exchanges including Binance, Coinbase, Kraken, Bybit, OKX, KuCoin and Gate.io — [aitrading-bot.com, Jul 2026](https://aitrading-bot.com/gunbot). Gunbot is closed source, with the license registered against an ERC-20 wallet. — [CryptoMarkets.tools, Sep 2026](https://cryptomarkets.tools/collections/self-hosted)
- 3Commas: "Free (1 bot) / Starter from $29/mo / Advanced from $49/mo", 18+ exchanges, paper trading, marketplace. — [altFINS 2026](https://altfins.com/best/crypto-trading-and-investing/crypto-trading-bots). Coin Bureau lists 3Commas annual-billing prices of Starter $16, Pro $38 and Expert $94 per month (as of Sept 2, 2026). — [Coin Bureau, Sep 2026](https://coinbureau.com/analysis/best-crypto-ai-trading-bots)
- Cryptohopper: Pioneer free, Explorer $24.16/month, Adventurer $57.50/month, Hero $107.50/month (annual), with backtesting and paper trading, a marketplace, and many exchanges including OKX, Coinbase Advanced and Kraken. — [Coin Bureau](https://coinbureau.com/analysis/best-crypto-ai-trading-bots); [TokenTax](https://tokentax.co/blog/best-crypto-trading-bot)
- Bitsgap from $23/month (grid, DCA, COMBO; 15+ exchanges). — [altFINS 2026](https://altfins.com/best/crypto-trading-and-investing/crypto-trading-bots). Typical subscription range is "$15 to $30 for an entry tier and up to $90 to $149 for top plans". — [CoinGape, Sep 2026](https://coingape.com/best-crypto-trading-bots)
- bitcointradingbots.com's 2026 table of "36 platforms" ranks Hummingbot (8.1), Freqtrade (8.0) and Gunbot (7.7) as the top self-hosted bots. ProfitTrailer is not among the bots listed in the extract. — [bitcointradingbots.com](https://bitcointradingbots.com/bots). Other 2026 roundups also omit PT from their shortlists: CoinGape (12 bots), altFINS, Coin Bureau, TokenTax (10 picks) and Block Research (6 options). — [CoinGape](https://coingape.com/best-crypto-trading-bots); [altFINS](https://altfins.com/best/crypto-trading-and-investing/crypto-trading-bots); [TokenTax](https://tokentax.co/blog/best-crypto-trading-bot); [Block Research](https://blockresearch.ai/blog/best-crypto-trading-bots-2026)
- ProfitTrailer for comparison: €50/month or €449/year subscription, lifetime €1,999 (out of stock), 3 live bots, 40+ indicators, paper trading, no native backtesting in official docs, closed source with modification forbidden by TOS. — [profittrailer.com](https://profittrailer.com); [Terms of Service](https://profittrailer.com/terms-of-services); [Wiki Indicators](https://wiki.profittrailer.com/en/Academy/Basic/Indicators)

### Inferences
- **Cost:** PT (about €449–600/year) costs more than Freqtrade or Hummingbot (free), more than a Gunbot one-time license over a 1–2 year horizon, and about the same as or more than mid-tier 3Commas or Cryptohopper.
- **Flexibility and scriptability:** PT is behind Freqtrade (full Python), Gunbot (JS strategies) and Hummingbot. PT's formula and variable system is powerful within the property-file paradigm but cannot run arbitrary code.
- **Backtesting:** PT is behind every major alternative compared here.
- **PT's remaining advantages:** an existing user's familiarity with its DCA, trailing and formula semantics; a mature DCA engine; a GUI; and, for owners of a legacy or V2 lifetime license, near-zero marginal cost.
- For a returning user who "wrote their own strategies/configs", the realistic options are: (a) reuse an existing PT lifetime license for familiar DCA/trailing scalping, with forward testing in Test Mode; or (b) port the logic to Freqtrade to get backtesting, hyperopt and broader exchange access, at the cost of rewriting in Python.

### Gaps
- No head-to-head benchmark of PT against alternatives (execution speed, fill quality, scalping suitability) was found from 2025–2026.
- Gunbot pricing is inconsistent across sources ($45–499, €59–249, about $400), so check Gunbot's official site before quoting.
- No 2025–2026 third-party review was found that tested PT hands-on. The available reviews (Coinspot 2025, BitDegree, Zignaly) are largely descriptive or recycled.
