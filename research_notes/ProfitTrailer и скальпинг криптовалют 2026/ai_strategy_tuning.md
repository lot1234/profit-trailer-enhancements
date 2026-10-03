# AI-assisted design, tuning and validation of crypto bot strategies (ProfitTrailer and alternatives), as of 2026-10-03

Scope: what LLMs (Claude and others) and current ML/quant tooling can realistically do for a retail trader tuning ProfitTrailer (PT) configs or moving to alternatives; how to avoid self-deception; what tooling is needed when PT has no native backtester. Source quality is noted inline. Undated findings come from 2025–2026 unless marked otherwise.

---

## 1. Does ProfitTrailer have backtesting, paper trading, an API or exportable trade logs? How do people backtest PT strategies?

### Takeaway
PT has **no native historical backtester**. Its developers said in 2018 that they lacked "the data nor infrastructure" to build one, and its official feature list in 2026 still offers only "Advanced Paper Trading" (Test Mode). Test Mode is a forward test: it runs live market data with a virtual balance. PT also exposes its data and config to external tools through a license-key/server-token API, which PT Magic uses. Backtesting a PT strategy therefore means **re-implementing its logic elsewhere**, for example in Freqtrade, TradingView Pine, vectorbt or Jesse, and then forward-testing the real PT config in Test Mode.

### Cited Findings
- **Backtesting is officially out of scope (dated 2018-02-27).** The PT feature-request ("enhancement games") README lists under "Not allowed": "Backtesting - We do not have the data nor infrastructure required to build a proper back testing logic. (Anyone can provide the data?)". This line was added to the README in Feb 2018. — [profit-trailer-enhancements README (fork of the official PT enhancements repo)](https://github.com/lot1234/profit-trailer-enhancements)
- **Official product page (2026)** lists "Advanced Paper Trading", "Advanced Stats", "40+ Buy-Sell Indicators", the ability to "process your TradingView alerts through an addon", and support for Binance, Binance Futures, KuCoin, Bybit, Kraken and others, plus OANDA forex. It does **not** list backtesting. — [profittrailer.com](https://profittrailer.com)
- **Conflicting claim.** A third-party review site says PT "offers paper trading and backtesting". This is a low-quality aggregator that also carries a "High-Risk Project — Not Recommended" banner, and no PT primary source supports the backtesting claim. — [coinspot.io review](https://coinspot.io/en/reviews/profit-trailer); contradicted by [PT enhancements README](https://github.com/lot1234/profit-trailer-enhancements) and [profittrailer.com](https://profittrailer.com)
- **Test Mode.**
  - Enabled via the "Run in Test Mode" setting, with a configurable "Test Mode Balance". A red indicator appears in the GUI header while it is on. — [PT Wiki: Web Interface Guide](https://wiki.profittrailer.com/webinterfaceguide)
  - The PT Academy recommends running "in Test Mode for a few weeks before really taking off… to make sure there are no mistakes left in your code and to avoid unnecessary losses or wrong entries and/or exits". — [PT Wiki: Setup buy strategy](https://wiki.profittrailer.com/en/Academy/Basic/Setupbuystrategy); [PT Wiki: Setup sell strategy](https://wiki.profittrailer.com/en/Academy/Basic/Setupsellstrategy)
- **Trade logs in the GUI.**
  - The web UI has a Sales Log and a Sell History tab (searchable, paginated) and lets you add buy records manually.
  - "Log History" sets how many days of buy/sell history are kept: "older history will be removed from the bot". Logs need external archiving if you want long histories for AI analysis.
  - Profit can be calculated by the MARKUP or TCV method, and a "Custom Exchange Fee" setting exists.
  - Source for all of the above: [PT Wiki: Web Interface Guide](https://wiki.profittrailer.com/webinterfaceguide)
- **API for external tools.**
  - PT Magic, a community tool, requires a "server API token assigned in your PT Account Settings… to gain access [to] PT's data". It also needs the PT license key "to change your settings for PT 2.0 and above".
  - PT Magic has its own TestMode in which "no Profit Trailer files will be changed". It uses "analyzer" settings fed with market data, such as CoinMarketCap.
  - Source for all of the above: [PT Magic wiki: settings.general](https://github.com/PTMagicians/PTMagic/wiki/settings.general)
  - The license key is "required to authenticate with ProfitTrailer's config API to allow writing and switching of configurations". — [PT Magic wiki: settings.general](https://github.com/Legedric/ptmagic/wiki/settings.general) (older fork; via search summary)
- **PT config syntax is plain-text and machine-editable,** so it is easy for an LLM to translate into or out of. Examples: `DEFAULT_A_buy_strategy = RSI`, `DEFAULT_A_buy_value = 40`, `DEFAULT_buy_strategy_formula = A && B` / `A || B`, and indicator parameters such as `EMACROSS_candle_period = 43200`. — [PT Wiki: Setup buy strategy](https://wiki.profittrailer.com/en/Academy/Basic/Setupbuystrategy); [PT Wiki: Setup sell strategy](https://wiki.profittrailer.com/en/Academy/Basic/Setupsellstrategy)
- **Historical third-party PT backtesting was done in TradingView.** "Backtest-Partners" published a "TradingView backtesting script for cryptocurrency trading using the ProfitTrailer automated trading platform" (repo created 2018-09, inactive since). — [GitHub: Backtest-Partners/backtest-partners-ultimate](https://github.com/Backtest-Partners/backtest-partners-ultimate)
- **Freqtrade warns that bar-level backtests cannot see intra-candle order.** One big limitation is the "inability to know how prices moved intra-candle". The mitigation is `--timeframe-detail 5m`, which simulates intra-candle movement from a lower timeframe. This matters for PT-style trailing buys and sells. Freqtrade also says "backtesting will never replace running a strategy in dry-run mode". — [Freqtrade docs: Backtesting](https://www.freqtrade.io/en/stable/backtesting/)

### Inferences
- A rigorous PT workflow has two legs:
  1. **Research leg (offline):** re-implement the PT buy, sell, trailing and DCA rules in a backtestable engine and do all parameter search there.
  2. **Confirmation leg (online):** run the exact candidate PT config in Test Mode for weeks, then on small live capital, and compare the results against the offline model.
- The re-implementation will only approximate PT. PT's internal trailing and DCA mechanics, its order-type handling and its Test Mode fill model are not fully documented. A Test-Mode vs re-implementation reconciliation step is therefore needed: compare trade by trade on the same period.
- Freqtrade is the most natural target for a port: Python strategies, trailing and custom stoploss, a DCA-like position-adjustment feature, and a dry-run mode. Its DCA/position-adjustment API was not verified in this session, so check the current docs.
- PT's GUI log retention limit means a retail user who wants AI-driven loss analysis should regularly pull PT data (via the API token or by exporting the sales log) into a CSV or Parquet store.
- **Security observation (inference, not verified):** GitHub search for "profittrailer backtest" returns a repo created 2025-11-14 by a random-named account. It is keyword-stuffed with topics like "ptmagic", "ptplus" and "feeder" and claims PT "featuring backtesting". This pattern resembles the fake trading-bot repos used to spread malware. Treat such repos as untrusted. — [GitHub: insignificant-pigeonhole504/profit-trailer](https://github.com/insignificant-pigeonhole504/profit-trailer)

### Gaps
- No primary PT documentation was found that shows the exact REST endpoints, response schema or rate limits of PT's data API, or whether CSV export of the sales log exists in current 2.x versions. Verify on a live install or in the PT Discord.
- No source documents how PT Test Mode simulates fills: whether it assumes a fill at the trigger price, whether it applies spread, slippage or partial fills, and whether it applies the "Custom Exchange Fee". This determines how optimistic Test Mode results are.
- No currently maintained, reputable third-party PT backtester was found. The PT Feeder / PT Magic / PT Tracker ecosystem appears largely dormant; this was not verified in depth.

---

## 2. What does 2024–2026 evidence say about LLMs as trading agents and strategy developers?

### Takeaway
The evidence consistently says that **LLMs used directly as autonomous traders are unreliable**:
- Most fail to beat buy-and-hold under rigorous evaluation.
- Results swing widely from run to run.
- Live real-money contests in 2025 mostly lost money.
- Benchmark rankings do not follow general "intelligence" leaderboards.

The more promising and more reproducible use is **LLM as quant researcher or coder**: it generates strategy code that is then tested deterministically. The research field itself has a serious reproducibility problem. A 2026 survey found that only 1 of 19 closed-loop studies reported an explicit transaction-cost model.

### Cited Findings
**Live real-money contests (Nof1 Alpha Arena)**
- **Season 1 setup (Oct 18 – Nov 3, 2025).** Six models each got $10,000 of real capital to trade crypto perpetuals on Hyperliquid (BTC, ETH, SOL, BNB, DOGE, XRP), with identical prompts and data. — [iWeaver](https://www.iweaver.ai/blog/alpha-arena-ai-trader-showdown); [AI World](https://aiworld.eu/story/ai-agents-against-the-market)
- **Season 1 final standings,** as announced by Nof1 founder Jay A. Zhang on Nov 3, 2025. — [ForkLog](https://forklog.com/en/four-out-of-six-ai-models-suffer-losses-in-trading-tournament)

  | Rank | Model | Final balance (from $10,000) |
  |---|---|---|
  | 1 | Qwen3 Max | $12,231 |
  | 2 | DeepSeek | $10,489 |
  | 3 | Claude Sonnet 4.5 | $5,799 |
  | 4 | Gemini 2.5 Pro | $5,445 |
  | 5 | Grok 4 | $4,208 |
  | 6 | GPT-5 | $4,126 |

  - **Conflicting snapshots.** LinkedIn posts and videos circulate different "final" numbers, for example DeepSeek first at $12,288, or DeepSeek at $21,653. These reflect mid-season peaks or different capture times. — [LinkedIn post](https://www.linkedin.com/posts/yaelkroy_ai-fintech-deepseek-activity-7392244248378515456-B8rn); [YouTube](https://www.youtube.com/watch?v=1Zpd0oxsEgY)
  - DeepSeek peaked above $23,000 around Oct 27 before a market-wide drop from Oct 29. — [AI World](https://aiworld.eu/story/ai-agents-against-the-market)
- **Season 1 behaviour.**
  - Qwen made about 43 trades, fewer than 3 per day; "trade count alone does not prove why Qwen won". — [iWeaver results analysis](https://www.iweaver.ai/blog/alpha-arena-ai-trading-season-1-results)
  - Commentary describes Gemini as "hyperactive", with fees chewing through capital, and summarises the lessons as "harness over hype" (strict JSON schemas, explicit exits before entry) and "risk is the product" (fees, leverage, stop distance). This is a secondary video summary. — [YouTube](https://www.youtube.com/watch?v=1Zpd0oxsEgY)
  - Models reportedly traded at 10x–15x leverage. This comes from a LinkedIn post and is unverified. — [LinkedIn](https://www.linkedin.com/posts/edwardstead_be-honest-you-have-a-favorite-model-so-activity-7388970202992066560-4ACi)
- **Season 1.5 (US equities, ended Dec 3, 2025).**
  - Eight models ran four themed contests each ("New Baseline", "Monk Mode", "Max Leverage", "Situational Awareness"), 32 runs in total, with $10,000 per run. — [LinkedIn analysis](https://www.linkedin.com/posts/victor-zhorin_in-late-2025-nof1-ran-alpha-arena-season-activity-7458491378105315328-gElz); [FA Mag / Bloomberg](https://www.fa-mag.com/news/ai-bots-auditioning-for-wall-street-trading-are-mostly-losing-86902.html)
  - The aggregate portfolio lost roughly one third. Only 6 of 32 runs were profitable, and all six were Grok 4.20, which won at about +12% aggregate. — [LinkedIn analysis](https://www.linkedin.com/posts/victor-zhorin_in-late-2025-nof1-ran-alpha-arena-season-activity-7458491378105315328-gElz); [Yahoo Finance](https://finance.yahoo.com/news/elon-musks-grok-4-20-123855766.html); [TradeRank](https://www.traderank.ai/blog/alpha-arena-alternatives-2026)
  - In one round Qwen made 1,418 trades against Grok's 158, from identical prompts. — [BigGo Finance (summarising Bloomberg)](https://finance.biggo.com/news/5BSX_Z0BaoGGrU-ID27J)
- **Organiser's own view.**
  - Nof1's founder: "LLMs can't really make money by themselves… You need basically a very sophisticated harness and scaffolding and data platform in order to even give them a chance."
  - Also: "Giving an LLM money right now and just having it go — that's not a thing yet."
  - Bloomberg notes that backtesting "doesn't really work for AI" because models already know historical outcomes (lookahead contamination), so they must be evaluated live.
  - Source for all of the above: [FA Mag (Bloomberg syndication)](https://www.fa-mag.com/news/ai-bots-auditioning-for-wall-street-trading-are-mostly-losing-86902.html)
- **2026 status.**
  - As of Aug 6, 2026, nof1.ai still showed Season 1.5 with "models no longer running". No public Season 2 roster or results had been posted. — [TradeRank](https://www.traderank.ai/traderank-vs-alpha-arena)
  - Nof1 raised $15M in May 2026 (co-led by SUI Group and Karatage) to build a consumer product. — [CoinDesk, 2026-05-15](https://www.coindesk.com/tech/2026/05/15/wall-street-is-starting-to-notice-one-of-crypto-s-smartest-ai-bets); [Dealroom](https://dealroom.co/companies/nof1)
  - TradeRank, an alternative arena, runs continuous seasons with **simulated** capital. — [TradeRank](https://www.traderank.ai/blog/alpha-arena-alternatives-2026)

**Academic benchmarks**
- **StockBench** (Tsinghua; arXiv 2510.02209, v2 Mar 2026). This is a contamination-free multi-month benchmark of daily decisions on DJIA stocks.
  - "most models struggle to outperform the simple buy-and-hold baseline". — [arXiv](https://arxiv.org/abs/2510.02209)
  - Agents "fail to recognize and respond to bear market conditions", and reasoning models produce more schema/format errors. This comes from a secondary summary. — [maxpool summary](https://maxpool.dev/research-papers/stockbench_llm_trading_report.html)
- **LiveTradeBench** (UIUC; arXiv 2511.03628). It ran 50-day live evaluations of 21 LLMs on US stocks and Polymarket. "high LMArena scores do not imply superior trading outcomes". — [arXiv](https://arxiv.org/abs/2511.03628)
- **FINSABER** (arXiv 2505.07078). It tested over two decades and 100+ symbols, with survivorship, look-ahead and data-snooping controls.
  - "previously reported LLM advantages deteriorate significantly". LLM strategies were "overly conservative in bull markets… overly aggressive in bear markets". — [arXiv HTML](https://arxiv.org/html/2505.07078v3); [RePEc](https://ideas.repec.org/p/arx/papers/2505.07078.html)
  - Average Sharpe by regime (bull / sideways / bear): Buy-and-Hold 0.61 / 0.48 / −0.28; FinAgent 0.12 / 0.19 / −0.38; FinMem −0.19 / −0.10 / −0.97. — [alphaXiv overview](https://www.alphaxiv.org/abs/2505.07078)
- **AI-Trader** (live and replay-causal evaluation across US equities, A-shares and crypto; secondary summary).
  - MiniMax-M2 and DeepSeek-v3.1 beat GPT-5, Claude-3.7-Sonnet and others.
  - "No model beat the A-share baseline".
  - In falling crypto markets, "the 'best' model was the one that lost the least".
  - Source: [Medium summary, May 2026](https://medium.com/@Micheal-Lanham/ai-trader-and-the-moving-target-problem-in-financial-evaluation-04b87199523f)
- **Agent Market Arena** (ACM Web Conference 2026). A lifelong real-time multi-market benchmark (stocks and crypto). Agent architecture vs LLM backbone is one of its research questions. — [ACM DL](https://dl.acm.org/doi/10.1145/3774904.3792821); [alphaXiv](https://www.alphaxiv.org/abs/2510.11695v1)
- **KTD-Fin** (arXiv 2605.28359, May 2026). Ten frontier LLM agents traded CSI300 over 2024–2026 under leakage control. Returns were "largely explained by passive market and style exposure, with limited evidence of persistent stock-selection alpha". — [arXiv](https://arxiv.org/abs/2605.28359)
- **TradingAgents** (multi-agent framework, arXiv 2412.20138, Dec 2024 – Jun 2025). It claims improvements in cumulative return, Sharpe and max drawdown over baselines. It is an influential framework, but it was evaluated on short windows, the kind FINSABER criticises. — [arXiv](https://arxiv.org/abs/2412.20138)
- **AlphaForgeBench** (NTU/HKUST, arXiv 2602.18481, Feb–May 2026). This is the most relevant to "AI helps design strategies".
  - Used directly as trading agents, LLMs "exhibit extreme run-to-run" behavioural instability. — [RePEc abstract](https://ideas.repec.org/p/arx/papers/2602.18481.html)
  - Reframing them to generate strategy *code* that is then backtested deterministically gave "96% backtest pass rates" across six frontier LLMs and 35,190 implementations. Run-to-run variance was "an order of magnitude smaller" than variance between queries. — [arXiv HTML v2](https://arxiv.org/html/2602.18481v2)
- **Field-level reproducibility (survey, arXiv 2605.19337, screened to 2026-03-09).** Of 19 primary closed-loop studies:
  - only 2 reported time-consistent train/test splits;
  - only 1 reported an explicit transaction-cost model;
  - only 1 documented survivorship handling;
  - none reached the highest reproducibility level.
  - Source: [arXiv](https://arxiv.org/abs/2605.19337)
- **Memorization and look-ahead in LLMs themselves.**
  - LLMs recall exact economic values from before their cutoff. Telling them not to use post-cutoff knowledge "did not prevent memorization". — [Lopez-Lira, Tang & Zhu, arXiv 2504.14765](https://arxiv.org/html/2504.14765v2); [Swedroe summary](https://larryswedroe.substack.com/p/the-illusion-of-foresight)
  - A related paper estimates that about 37% of the apparent news-to-stock-return predictive effect is amplified by memorization. — [CFA UK summary of Gao, Jiang & Yan "Detecting Lookahead Bias in LLM Forecasts"](https://connect.cfauk.org/discussion/llms-research-lookahead-bias-for-prediction-tasks)

### Inferences
- For a retail PT user, the evidence argues **against letting an LLM make live buy and sell decisions**. It argues **for using the LLM offline**: write and review deterministic rules, configs and code, then validate them with standard quant methods. That is AlphaForgeBench's "white-box code" paradigm, as opposed to "black-box action emission".
- Alpha Arena is a public demonstration, not evidence of skill. The runs were short, used a single regime, were leveraged and had n≈6–8 models. That still teaches the operational lessons: fees and overtrading, leverage, and the need for exit rules defined before entry.
- Any LLM-assisted backtest over periods inside the model's training data is suspect if the LLM makes *judgments* inside the loop (sentiment, regime calls). It is much less of a problem if the LLM only wrote the code and the code makes the decisions.

### Gaps
- No public Alpha Arena Season 2 (or other 2026 real-money LLM crypto contest) results could be verified as of the latest sources (Aug 2026). TradeRank's own "Season 9" figures were not independently checked.
- No peer-reviewed study was found that measures LLM help in *tuning an existing rule-based bot* (PT-like DCA/trailing), as opposed to LLM-as-trader.
- No public, rigorous data was found on Claude-specific results in trading benchmarks beyond Alpha Arena Season 1 (Claude Sonnet 4.5 finished 3rd of 6 with about −42%).

---

## 3. Practical roles where an AI assistant helps

### Takeaway
The roles with the best evidence and lowest risk are:
- translating ideas into code or config;
- writing backtest harnesses and analysis scripts;
- adversarial code review for look-ahead and other bugs;
- trade-log forensics;
- generating robustness tests (walk-forward, Monte Carlo, parameter-stability maps);
- building monitoring and alerting.

Market-regime filters and risk sizing are useful when the LLM *codes* them as deterministic rules, not when it judges them live. All AI output has to be verified, because LLMs readily write code with look-ahead bugs that produce beautiful but fake equity curves.

### Cited Findings
- **Code generation works mechanically but bugs are common.**
  - Frontier LLMs produced executable strategy code with a 96% backtest pass rate. — [AlphaForgeBench](https://arxiv.org/html/2602.18481v2)
  - A practitioner names look-ahead bias in AI-written backtests as "the most expensive single hallucination category". The model uses today's close to decide today's entry or misaligns shifted columns, and "the code runs, the equity curve looks great". — [Marketcalls](https://www.marketcalls.in/llm-models/why-ai-hallucinates-how-to-catch-it-and-what-traders-and-investors-must-know.html)
  - An r/algotrading thread is titled "LLMs are not the right tool for algo trading". Only a search snippet was available, so the date and full context are unverified. The snippet contains both the view that backtest results become "completely untrustworthy due to bugs or logical errors" and the view that "LLMs are actually creating usable models now. Yeah, there are usually bugs". — [Reddit r/algotrading](https://www.reddit.com/r/algotrading/comments/1qbvzxn/llms_are_not_the_right_tool_for_algo_trading)
- **Adversarial review pattern.**
  - Ask a *fresh* chat to review the code "specifically for look-ahead bias, future leakage, and survivorship bias… assume the code is broken and find the break". — [Marketcalls](https://www.marketcalls.in/llm-models/why-ai-hallucinates-how-to-catch-it-and-what-traders-and-investors-must-know.html)
  - Add assertions (for example, "max drawdown must be between 0 and 1"), require explicit lags, and verify AI-reported metrics against raw data. — [QuantVPS blog](https://www.quantvps.com/blog/algorithmic-trading-with-llm)
- **Tool-assisted bias detection.**
  - Freqtrade's `lookahead-analysis` command exists because backtesting "calculates all indicators at once", so future-peeking indicators falsify results.
  - In Freqtrade's words, "Usually the bias in the strategy is THE driving factor for 'too good to be true' profits."
  - Source for both points: [Freqtrade docs: Lookahead analysis](https://www.freqtrade.io/en/stable/lookahead-analysis/)
- **LLM tooling that grounds code in the real API.** An MCP server provides "read-only… Freqtrade codebase introspection. Helps LLMs write better strategy code by providing access to method signatures, type hints, enums, config schema, and documentation". — [GitHub: yalcin/freqtrade-mcp](https://github.com/yalcin/freqtrade-mcp)
- **AI-driven backtest and hyperopt loops.** An MCP server exposes "Freqtrade backtesting, hyperopt and market-data tools to Claude", plus a LangGraph agent that "generates and optimizes trading strategies". This is a small community project (about 9 stars), not vetted. — [GitHub: dasein108/freqtrade_dev_mcp](https://github.com/dasein108/freqtrade_dev_mcp)
- **Robustness features that an AI can drive or interpret.**
  - Jesse ships "Monte Carlo Analysis… trade-order shuffling and candles-based simulations to distinguish skill from luck", "Rule Significance Testing", and a scikit-learn ML pipeline. — [GitHub: jesse-ai/jesse](https://github.com/jesse-ai/jesse)
  - vectorbt offers "large-scale parameter sweeps" and "robustness testing with walk-forward optimization". — [GitHub: polakowo/vectorbt](https://github.com/polakowo/vectorbt)
- **Regime awareness is a documented weakness of LLM traders**, which argues for explicit, coded regime filters:
  - LLM strategies "miss upside in bull markets and incur heavy losses in bear markets due to poor risk control". — [FINSABER](https://arxiv.org/html/2505.07078v3)
  - StockBench agents fail to recognize bear markets. — [maxpool summary](https://maxpool.dev/research-papers/stockbench_llm_trading_report.html)
- **PT-specific regime switching exists in the ecosystem.** PT Magic reads PT data, uses "analyzer" settings with market data, and needs the PT license key to change PT settings. It is a rule-based, market-condition-driven config switcher an AI could help tune. — [PT Magic wiki](https://github.com/PTMagicians/PTMagic/wiki/settings.general)
- **Monitoring and portfolio queries via natural language.** The Hummingbot MCP gives an AI assistant portfolio balances, order history, prices and funding rates. It also gives tools to place orders and deploy bots. — [Hummingbot MCP docs](https://hummingbot.org/mcp/)
- **Anecdotal "AI agent made money" claims are weak evidence.** One example: a Claude Haiku news agent made $19.48 in one week on a $1,000 paper account (Jan 13–17, 2026). That is a tiny sample, one regime, and a vendor blog. — [QuantVPS blog](https://www.quantvps.com/blog/algorithmic-trading-with-llm)

### Inferences
Concrete high-value roles for a PT user, roughly in order of value relative to risk:
1. **Config ↔ code translation.**
   - Convert the PT `buy_strategy_formula` / DCA / trailing settings into a Freqtrade strategy, vectorbt signals or Pine Script.
   - Convert research results back into PT `.properties` values.
   - Document every assumption, for example how "trailing" is interpreted.
2. **Trade-log forensics.**
   - Feed the exported PT sales log and Test Mode log into pandas.
   - Have the AI segment losses by pair, hour, volatility, BTC trend, DCA depth and time-in-trade.
   - Find patterns such as "losses cluster when BTC 4h trend < 0" or "DCA level ≥3 has negative expectancy".
   - The AI should write the analysis *code* and the human reads the numbers. The AI should not just "eyeball" a CSV.
3. **Backtest harness and reconciliation.** Build the re-implementation, then a reconciliation report comparing the backtest against PT Test Mode on the same dates.
4. **Adversarial code review.** Look-ahead, off-by-one candle alignment, fee double-counting, survivorship (delisted pairs), and unrealistic fills on trailing orders.
5. **Robustness test generation.** Walk-forward splits, CSCV/PBO computation, deflated Sharpe, trade-order Monte Carlo for drawdown distribution, and parameter-neighbourhood heatmaps (is the optimum a plateau or a spike?).
6. **Regime filters coded as rules,** for example BTC trend or volatility percentile gates. These must themselves be validated out of sample, because they are extra parameters.
7. **Risk sizing and limits,** for example a max DCA budget per pair or a portfolio heat cap, plus **monitoring and alerts** (Telegram/email on drawdown thresholds, API errors, stuck orders). The monitoring code is deterministic; the LLM only writes it.
8. **Not recommended:** the LLM directly deciding live trades or live parameter changes without a human gate.

### Gaps
- No controlled study was found that quantifies how often LLM-written backtest code contains look-ahead or other bugs. The evidence is practitioner reports.
- No published, validated PT → Freqtrade translation was found to reuse. It would need to be built and verified.

---

## 4. Correct validation methodology for parameter tuning

### Takeaway
The main danger is the **multiple-testing / selection-bias problem**. If you try enough parameter combinations, noise alone produces impressive Sharpe ratios. An AI makes this worse because it makes trying thousands of variants nearly free. The defensible protocol has six parts:
1. Fix the hypothesis and the parameter ranges in advance.
2. Count every trial.
3. Use time-ordered out-of-sample (OOS) and walk-forward testing.
4. Compute the Probability of Backtest Overfitting (PBO, via CSCV) and the Deflated Sharpe Ratio (DSR).
5. Model fees, slippage and intra-candle fills realistically.
6. Forward-test (paper / Test Mode), then go live with small capital and compare the live results against the backtest.

### Cited Findings
- **Random-walk demonstration (Bailey, Borwein, López de Prado, Zhu).**
  - 1,000 daily random-walk prices, with parameters optimised (entry day, holding period, stop loss, side), gave an annualised Sharpe of 1.27 and a PSR statistic of 2.83, which implies "less than 1% probability" that the true SR ≤ 0.
  - This was "despite the fact that no true seasonal effect exists".
  - Source: [Bailey et al., "The Probability of Backtest Overfitting" (PDF)](https://www.davidhbailey.com/dhbpapers/backtest-prob.pdf); [Pseudo-Mathematics and Financial Charlatanism (PDF)](https://obj.portfolioconstructionforum.edu.au/articles_perspectives/Pseudo-mathematics-and-financial-charlatanism.pdf)
- **Definitions.**
  - PBO is "the probability that the configuration selected as best in-sample performs below the median configuration out-of-sample".
  - It is estimated with CSCV: split the trial-returns matrix into S blocks, use every combination of S/2 blocks as train and the rest as test, and count how often the in-sample winner ranks below the median OOS.
  - PBO "rises with the number of trials for a fixed sample length".
  - Source: [AuditZK calculator page citing Bailey et al. 2017, J. Computational Finance 20(4)](https://www.auditzk.com/tools/backtest-overfitting)
- **Deflated Sharpe Ratio (Bailey & López de Prado 2014, J. Portfolio Management 40(5)).** It corrects for selection bias across multiple trials and for non-normal returns. Related tools are the Probabilistic Sharpe Ratio and Minimum Track Record Length. — [Portfolio Optimization book §8.3](https://portfoliooptimizationbook.com/book/8.3-dangers-backtesting.html)
- **Practical rules from the same literature:**
  - "Keep track of the number of backtests conducted on a dataset so that the probability of backtest overfitting may be estimated and the Sharpe ratio may be properly deflated."
  - "Do not backtest until all your research is complete", meaning avoid the tweak-and-rerun loop.
  - Develop models across whole universes rather than single securities.
  - Source: [Portfolio Optimization book §8.3](https://portfoliooptimizationbook.com/book/8.3-dangers-backtesting.html)
- **Worked replication (2,500 configs × 20 pairs = 50,000 strategies).**
  - The best Sharpe was 2.00 net of costs, against an expected maximum of 2.72 under the null for N=50k, so it was *below* what pure noise would produce.
  - DSR was 0.029 against a 0.95 bar. Median per-pair PBO was 0.28.
  - The 50,000 nominal trials equalled about 434 effective independent trials.
  - Source: [Daru Finance research review](https://daru.finance/research-review/lopez-de-prado/backtest-overfitting)
- **Freqtrade-specific guards.**
  - Hyperopt limits decimals to 3 places because "every value more precise than this will usually result in overfitted results".
  - It supports loss functions such as `SharpeHyperOptLossDaily`, `--min-trades`, and protections optimisation.
  - Source: [Freqtrade docs: Hyperopt](https://www.freqtrade.io/en/stable/hyperopt/)
  - `--fee` is "applied twice (on trade entry and exit)". — [Freqtrade docs: Lookahead analysis CLI](https://www.freqtrade.io/en/stable/lookahead-analysis/)
  - `--timeframe-detail` reduces intra-candle optimism. — [Freqtrade docs: Backtesting](https://www.freqtrade.io/en/stable/backtesting/)
- **ML retraining.** FreqAI retrains models "with a predetermined frequency" and "can backtest strategies (emulating reality with periodic retraining on historic data)". This is effectively rolling walk-forward for ML models. — [Freqtrade docs: FreqAI](https://www.freqtrade.io/en/stable/freqai/)
- **Cost modelling is routinely missing even in research.** Only 1 of 19 primary LLM-trading studies reported an explicit transaction-cost model. — [arXiv 2605.19337 survey](https://arxiv.org/abs/2605.19337)
- **Paper → small live → scale (practitioner heuristic, vendor blog, not academic).**
  - Paper trade 2–4 weeks or 30–50 trades.
  - Then trade at 25–50% of intended size.
  - Scale up only if live metrics are within 10–15% of the backtest.
  - Source: [TradeZella blog (2026)](https://www.tradezella.com/blog/backtesting-trading-strategies)
- **Live testing is necessary but small samples mislead.** Alpha Arena runs lasted about 2 weeks. Commentators stress that "the short duration, leverage, market regime, prompting setup, and small number of models make it a benchmark result, not an investable performance record". — [iWeaver](https://www.iweaver.ai/blog/alpha-arena-ai-trading-season-1-results)

### Inferences
A concrete protocol for a PT/Freqtrade user:
1. **Pre-register** in a text file, before running anything: the hypothesis, the parameter grid and ranges, the objective (for example daily Sharpe or Calmar after fees), and the minimum trade count.
2. **Data split.**
   - Hold out the most recent 20–30% of history as a sealed OOS set, touched once.
   - Use walk-forward windows on the rest, for example 6 months optimise / 1–2 months test, rolled forward.
   - Crypto regimes are short, so include at least one bear, one bull and one chop period.
3. **Log every trial** (the AI agent should write this automatically), compute **PBO via CSCV** across the trial matrix, and report **DSR** with the true trial count.
4. **Prefer plateaus over peaks.** Accept parameters whose neighbours also perform well; reject isolated spikes.
5. **Cost realism.**
   - Exchange taker fees on both sides, plus slippage assumptions per pair liquidity.
   - Use `--timeframe-detail 1m` for trailing logic.
   - Model minimum order size and DCA capital lock-up.
   - For PT-style DCA, model the worst-case capital tied up in "bags".
6. **Monte Carlo** of the trade sequence to get a drawdown distribution, not a single max drawdown. Size so that the 95th-percentile drawdown is tolerable.
7. **Forward test.**
   - Run PT Test Mode or Freqtrade dry-run on the *same* config for several weeks.
   - Reconcile against what the backtest predicts for that period.
   - Then go live with small capital and pre-defined kill criteria (for example, stop if live drawdown exceeds the backtest's 95th percentile).
8. **Re-optimise on a schedule, not after every loss.** Re-optimising after each loss is the tweak-and-rerun trap.

### Gaps
- No crypto-specific study was found that gives recommended walk-forward window lengths for minute-to-hour scalping or DCA bots. Window choice remains a judgment call.
- Exact current Binance, Bybit and KuCoin fee tiers and realistic slippage for small-cap alts were not researched here. Another researcher may cover them.

---

## 5. Tooling landscape in 2026

### Takeaway
- **Engine:** the open-source Python stack is mature. Freqtrade (+FreqAI, hyperopt, lookahead and recursive analysis, dry-run) is the closest PT replacement or research engine for spot DCA and trailing bots. vectorbt suits fast parameter sweeps and walk-forward. Jesse has built-in Monte Carlo and significance testing. NautilusTrader offers high-fidelity event-driven backtest-to-live parity. Hummingbot is execution-oriented and now has an official MCP server.
- **Data:** free Binance public data (klines down to 1s, aggTrades, trades) covers most retail needs.
- **LLM access:** MCP servers now let Claude or other LLMs reach exchanges (CCXT), Freqtrade and Hummingbot. Most are small community projects, and several can place live orders.

### Cited Findings
- **Freqtrade.**
  - Backtesting with explicit assumptions and `--timeframe-detail`; dry-run is recommended as the next step. — [Freqtrade: Backtesting](https://www.freqtrade.io/en/stable/backtesting/)
  - `lookahead-analysis`. — [Freqtrade: Lookahead analysis](https://www.freqtrade.io/en/stable/lookahead-analysis/)
  - Hyperopt with loss functions and protection spaces. — [Freqtrade: Hyperopt](https://www.freqtrade.io/en/stable/hyperopt/)
  - FreqAI: per-pair ML models with periodic retraining, both in backtest and live. FreqAI cannot be combined with dynamic `VolumePairlists`. — [Freqtrade: FreqAI](https://www.freqtrade.io/en/stable/freqai/)
- **vectorbt** (about 8.8k stars). Vectorized pandas/NumPy/Numba engine with an optional Rust engine, "large-scale parameter sweeps", and "robustness testing with walk-forward optimization". It is the community edition of the commercial VectorBT PRO. — [GitHub: polakowo/vectorbt](https://github.com/polakowo/vectorbt)
- **Jesse.** Backtests "without look-ahead bias", Monte Carlo (trade shuffling and candle-based), rule significance testing, a scikit-learn ML pipeline, and paper and live trading. — [GitHub: jesse-ai/jesse](https://github.com/jesse-ai/jesse)
- **NautilusTrader.**
  - A Rust-native, deterministic, event-driven engine. "The same strategy and execution-algorithm code can run across backtest and live systems", but "live execution still introduces venue, transport, timing… behavior that a simulation may not reproduce".
  - It has crypto CEX and DEX adapters.
  - "built-in AI/ML tooling" is explicitly out of scope.
  - Source: [GitHub: nautechsystems/nautilus_trader](https://github.com/nautechsystems/nautilus_trader)
- **Hummingbot.**
  - Hummingbot API (formerly `backend-api`) with MCP integration for Claude, ChatGPT and Gemini. — [Hummingbot API](https://hummingbot.org/hummingbot-api)
  - The MCP server gives data (balances, order history, prices, funding) and tools (place orders, manage positions, deploy bots). Hummingbot warns: "Treat MCP as a privileged control plane: for production, run Hummingbot API behind Tailscale so it is not reachable on a public IP." — [Hummingbot MCP](https://hummingbot.org/mcp/)
  - Claude Code skills and an "AI Trading Agents" course module were added in Feb–Mar 2026. — [Hummingbot newsletter Feb/Mar 2026](https://hummingbot.substack.com/p/hummingbot-newsletter-februarymarch)
  - The Docker MCP Catalog lists 21 tools. — [Docker Hub MCP catalog](https://hub.docker.com/mcp/server/hummingbot-mcp/tools?toolSearch=get_positions)
- **Freqtrade MCP servers (community).**
  - kukapay/freqtrade-mcp: about 146 stars, connects to a running Freqtrade bot. — [GitHub](https://github.com/kukapay/freqtrade-mcp)
  - yalcin/freqtrade-mcp: read-only codebase introspection. — [GitHub](https://github.com/yalcin/freqtrade-mcp)
  - dasein108/freqtrade_dev_mcp: backtesting and hyperopt tools for Claude. — [GitHub](https://github.com/dasein108/freqtrade_dev_mcp)
  - furkankoykiran/freqtrade-mcp: TypeScript, REST API. — [GitHub](https://github.com/furkankoykiran/freqtrade-mcp)
  - All are small projects with roughly 2 to 150 stars.
- **CCXT MCP servers.**
  - @lazydino/ccxt-mcp. Its config example stores exchange `apiKey` and `secret` directly in the MCP JSON config. — [mcpservers.org](https://mcpservers.org/servers/lazy-dinosaur/ccxt-mcp); [mcp.so](https://mcp.so/servers/ccxt-mcp)
  - doggybee/mcp-server-ccxt (about 92 stars). — [Augment registry](https://www.augmentcode.com/mcp/mcp-server-ccxt)
  - Both expose fetchTicker, fetchOrderBook, fetchTrades and OHLCV, plus trading functions.
  - A 2026 list of finance MCP servers also exists. — [Mnemox list (2026)](https://www.mnemox.ai/blog/mcp-servers-finance)
- **Binance public data** (data.binance.vision).
  - Free daily and monthly files for all symbols: spot and USD-M/COIN-M futures klines (1s to 1mo), aggTrades and trades.
  - Each file has a SHA256 CHECKSUM.
  - Spot timestamps are in **microseconds from 2025-01-01**, which is a common parsing bug.
  - Archived files are occasionally corrected (there is a changelog).
  - Source: [GitHub: binance/binance-public-data](https://github.com/binance/binance-public-data)
- **Benchmarks for LLM tool use and code** (2026): FinMCP-Bench (financial tool use under MCP, 2026-03) and QuantCode-Bench (executable algo-trading strategy code generation, 2026-04). — [Awesome-LLM-Quantitative-Trading-Papers](https://github.com/Tom-roujiang/Awesome-LLM-Quantitative-Trading-Papers)

### Inferences
Suggested minimal retail stack for "AI-assisted tuning of a PT-style strategy":

| Purpose | Tool |
|---|---|
| Data | Binance public data, or CCXT for other exchanges |
| Research and sweeps | vectorbt (or Freqtrade hyperopt) |
| PT-logic replica and dry-run | Freqtrade |
| Statistics | Python implementation of CSCV/PBO and DSR |
| AI | Claude Code or similar, working on the *repository*. Optionally a read-only MCP (Freqtrade introspection, read-only exchange data) |

- PT stays the live executor if the user prefers it. Configs are hand-transferred after validation.
- Prefer **read-only** MCP connections, or none at all, for research. An MCP with order-placing tools should be treated like giving the model your trading account.

### Gaps
- Kaiko and other paid tick or order-book vendors were not researched. Their pricing and retail suitability are unknown here.
- No 2026 release notes were checked for Freqtrade, Hummingbot, Jesse or Nautilus (versions, new walk-forward features). Verify current versions before relying on specific flags.
- No official Binance- or Anthropic-maintained exchange MCP server was confirmed in this session. The CCXT MCPs found are community-maintained.

---

## 6. Risks of letting AI make live trading decisions

### Takeaway
Five risks are well documented:
1. Indirect prompt injection and adversarial market or news data. Small, human-invisible manipulations measurably cost money.
2. Hallucinated or unstable outputs: run-to-run variance and schema errors.
3. Look-ahead and memorization that make LLM backtests look better than reality.
4. Credential compromise, of which the 3Commas leak is the canonical bot-ecosystem example.
5. Over-privileged agent tooling.

Mitigations are architectural:
- Keep the LLM out of the live decision loop, or behind deterministic hard limits.
- Give it least-privilege, trade-only, IP-whitelisted keys.
- Sanitize and canonicalize inputs.
- Require human approval for config changes.

### Cited Findings
- **Adversarial news (arXiv 2601.13082, Jan 2026).**
  - Human-imperceptible Unicode homoglyphs and hidden-text clauses in headlines were tested against FinBERT, FinGPT, FinLLaMA and six general LLMs inside a Backtrader trading system.
  - A one-day attack over 14 months "can reliably mislead LLMs and reduce annual returns by up to 17.7 percentage points".
  - The reasoning model O3 was more robust but was not the best performer without attack.
  - Source: [arXiv abstract](https://arxiv.org/abs/2601.13082); [arXiv HTML](https://arxiv.org/html/2601.13082v1)
- **Market Signal Injection (arXiv 2609.18357, Sep 2026).**
  - Changing only formatting, ordering or qualitative commentary, with no explicit instructions, shifted LLM pricing-agent behaviour.
  - "larger models are not consistently more robust".
  - Input canonicalization removed the tested sentiment attacks; decision-boundary anchoring gave partial mitigation.
  - Source: [Machine Brief abstract](https://www.machinebrief.com/news/market-signal-injection-adversarial-context-manipulation-of-7ddu); [AI Security Portal](https://aisecurity-portal.org/en/literature-database/market-signal-injection-adversarial-context-manipulation-of-llm-pricing-agents)
- **Financial prompt injection is economically motivated.** A crafted news item or social post could instruct an agent to trade, and "the attacker profits from the manipulated trade". Self-replicating injections can spread through multi-agent systems. — [SoK: Security of Autonomous LLM Agents in Agentic Commerce, arXiv 2604.15367](https://arxiv.org/html/2604.15367v1)
- **Instability and hallucination in action emission.**
  - LLM trading agents show "extreme run-to-run" behavioural instability. — [AlphaForgeBench](https://ideas.repec.org/p/arx/papers/2602.18481.html)
  - Reasoning models produced more format errors in StockBench. — [maxpool summary](https://maxpool.dev/research-papers/stockbench_llm_trading_report.html)
  - Identical prompts produced trade counts ranging from 158 to 1,418 in Alpha Arena 1.5. — [BigGo/Bloomberg](https://finance.biggo.com/news/5BSX_Z0BaoGGrU-ID27J)
- **Temporal leakage.**
  - News timestamps often record publication time rather than the time the item became available to the pipeline. Without ingestion-lag modelling, agents "are therefore likely to exhibit inflated backtest performance". — [Agentic Trading survey, arXiv 2605.19337](https://arxiv.org/html/2605.19337v1)
  - LLMs memorize pre-cutoff data, and instructions do not prevent it. — [Lopez-Lira et al.](https://arxiv.org/html/2504.14765v2)
- **API key compromise in the bot ecosystem (Oct–Dec 2022).**
  - 3Commas' CEO confirmed on Dec 28, 2022 that about 100,000 API keys published by a hacker came from its service. — [SiliconANGLE](https://siliconangle.com/2022/12/29/crypto-trading-service-3commas-confirms-massive-api-key-leak-hack); [3Commas notice](https://3commas.io/blog/notice-on-api-data-disclosure-incident)
  - Losses were about $20M. — [Halborn](https://www.halborn.com/blog/post/explained-the-3commas-breach-december-2022)
  - The company initially called the reports "false rumors". — [ForkLog](https://forklog.com/en/api-key-leaks-and-exchange-inaction-a-hapi-analysis-of-the-3commas-incident)
  - Attackers drained accounts "through market manipulation, not withdrawals — proof that a no-withdrawal key alone isn't enough". The recommended controls are no-withdrawal permissions, IP whitelisting and careful choice of where keys are stored. — [Bitsgap blog](https://bitsgap.com/blog/is-it-safe-to-connect-your-exchange-api-to-a-trading-bot)
- **Agent tooling as an attack surface.**
  - Hummingbot calls its MCP "a privileged control plane" and recommends keeping it off public IPs. — [Hummingbot MCP](https://hummingbot.org/mcp/)
  - Some CCXT MCP configs keep exchange secrets in plain JSON. — [mcpservers.org](https://mcpservers.org/servers/lazy-dinosaur/ccxt-mcp)
- **Regulatory and liability angle.** "Firms deploying LLM agents may face heightened liability if hallucinated outputs cause client losses." — [Agentic Trading survey](https://arxiv.org/html/2605.19337v1)
- **Organiser view.** Even the operator of the main live LLM-trading arena says LLMs need "a very sophisticated harness and scaffolding". — [FA Mag/Bloomberg](https://www.fa-mag.com/news/ai-bots-auditioning-for-wall-street-trading-are-mostly-losing-86902.html)

### Inferences
Risk controls for a retail PT or Freqtrade user who uses AI:
- **Separation of duties.** The LLM proposes configs and code; deterministic software executes; a human approves changes. Never let an LLM edit live PT config via the license-key config API without review. PT Magic-style automatic config switching should use rule-based analyzers that were backtested, not free-form LLM judgments.
- **Hard limits outside the LLM.** Max position or DCA budget per pair, max open pairs, daily loss stop, and exchange-side stop-losses where supported. These should be enforced in bot config or code that the LLM cannot override at runtime.
- **Keys.**
  - Trade-only, no withdrawal, IP-whitelisted to the bot's VPS.
  - Separate sub-accounts with capped balances for experiments.
  - Never paste exchange secrets into a chat. Keep them in environment variables or a secrets manager that MCP servers read; do not store them in prompt-visible config.
  - Rotate keys after any third-party tool exposure.
- **Untrusted inputs.** If any news or social sentiment feeds a strategy:
  - canonicalize text (strip zero-width and hidden characters, normalize Unicode);
  - treat it as data, never instructions;
  - cap the position impact of any text-derived signal.
- **Supply chain.** Install bot add-ons and MCP servers only from known repositories. Low-star, keyword-stuffed "ProfitTrailer" repos are a red flag (see section 1).

### Gaps
- No documented real-world incident was found of a prompt injection causing losses in a *retail* LLM crypto-trading bot. The evidence comes from controlled studies and threat modelling.
- No research was done on exchange-side features (for example Binance API key permission granularity or sub-account limits in 2026). Confirm per exchange.
