# Prism

**An on-chain neobank where an AI agent runs your money. Personal and business. Built on Robinhood Chain.**

> New to the team? This page is the whole idea. ~5 minutes.
> Deeper reasoning and open questions live in [IDEAS.md](IDEAS.md).

---

## 1. The one-liner

- **Prism = a stablecoin bank account + an AI CFO that actually operates it.**
- Not a dashboard you read. An agent that spends, saves, forecasts, invests, and reports **for you**.
- Two products, one core: **Personal** (your money) and **Business** (your company's money).
- Free to use. Funded by trading fees on the **PRISM token**, launched on Robinhood.

## 2. Why Robinhood

- **Distribution** — the token launches to Robinhood's user base.
- **Brokerage in the same surface** — an insight can end in a trade without leaving the product.
- **Stocks + crypto + bank account in one place** — no competitor has all three.
- Product is **token-agnostic**: PRISM is the GTM asset, the bank supports every token.

## 3. The account (same core for both products)

- Deposit into **one wallet**. No products to choose.
- Four rails hang off it:
  - **Cards** — spend anywhere
  - **Yield** — idle balance earns by default
  - **Fiat rails** — real send/receive of fiat
  - **Cross-chain** — trade BTC, memes, anything
- The agent moves money between rails. The user doesn't think about it.

---

# PERSONAL

## 4. Cards

- **One card per recurring expense** — Netflix has a card, rent has a card, gym has a card.
- A leak is contained to one line item, never the whole account.
- **The agent holds the on/off switch** — unused subscription gets paused automatically.
- Premium tier: lounge access + standard perks. *(or token-launch access — TBD)*
- Points, convertible to rewards.

## 5. Cashback — you get paid in what you bought

The differentiator. Cashback ladder:

| You spend at | You get back |
|---|---|
| A listed company (Apple) | **That company's stock/token** |
| An unlisted brand | **A meme coin**, picked by our engine (Solana or Robinhood Chain) |

- Your consumption **quietly compounds into ownership of what you consume**.
- Pitch: *"you already made Apple rich — now you own some of it."*
- Only possible because we're on a brokerage chain. A normal neobank cannot pay you in equity.

## 6. Spend analysis — backward and forward

- **Backward** — categorize and analyze all past spend.
- **Forward** — *this is the real feature*. The agent predicts future expenses:
  - **Cadence detection** — movie monthly, trip quarterly, renewal annually → projected forward
  - **Chat elicitation** — agent asks *"anything planned coming up?"* and folds it in
- **The forecast becomes the budget.** The user never sets one.

## 7. Spend-to-investment graph

- Every transaction expands into a **money-flow tree**: where your money actually went.
- **Goes upstream, not to the obvious name.** ChatGPT sub ≠ "buy OpenAI" → the real exposure is NVDA, TSM, MSFT, power.
- Burger → MCD, plus beef, potatoes, distribution, packaging.
- Framing: not *"buy this"* → *"if you think burgers skyrocket, here's the chain that captures it."*
- **Aggregate spend across all users is a leading indicator** — it moves ahead of reported earnings. No brokerage has this data. Likely our deepest moat.

## 8. Credit — "don't sell your Bitcoin to buy things"

- Any card spend splits into **4 monthly installments at 0% interest**.
- Backed by **crypto you already hold** as collateral — BTC, ETH, SOL, even meme coins.
- Interest starts after month 4.
- **Why it works:** over-collateralized → no underwriting, no credit bureau.
- **Why users want it:** selling crypto is a taxable event and a break in conviction. This spends without selling.
- **Must get right:** liquidation UX. Agent pre-warns and auto-deleverages *before* forced sale.

---

# BUSINESS

## 9. The wedge: banking as a CLI

- **A CLI is mandatory.** Companies build their own logic on top of their bank.
- Reachable from **every coding terminal and every AI chat**.
- Three surfaces, one core: **CLI · API · MCP server**.
- **"Accessible from AI chats" = an MCP server** — Claude Code, Cursor, or any internal agent gains money as a capability. No integration project.
- **Strategically the biggest idea in the doc:** not "a bank with AI in it" — **the money layer other people's agents run on**.
- Every company building agents eventually needs the agent to *pay* for something. Nobody owns that answer yet.
- Also where stablecoins genuinely beat banks: no batch windows, no banking hours, 24/7, API-native.
- Ships for personal accounts too.

## 10. Business feature set

*Researched against what Mercury, Brex, Ramp, Bridge, BVNK, Conduit, Rise and the 2026 AI-CFO stack actually ship. Table stakes must exist or finance teams won't switch; the right column is where we win.*

**Accounts & treasury**
- Multi-currency stablecoin accounts; virtual accounts / IBANs
- Sub-accounts per entity, team, or project
- Auto-sweep idle cash into yield; automated rebalancing and netting across chains
- Multi-entity consolidation; FX between stablecoins and fiat

**Payments**
- Global payouts with local rails on the destination side (100+ countries)
- Batch, scheduled, and recurring payments
- Approval workflows, vendor allowlists, dual authorization

**AP (accounts payable)**
- Invoice intake + extraction, auto-coding, PO matching
- Approval routing, duplicate and fraud flagging before payment

**AR (accounts receivable)**
- Invoicing, payment links, auto-reconciliation of incoming funds
- Dunning and collections chasing, run by the agent

**Cards**
- Corporate cards; virtual card per employee, vendor, or subscription
- Policy enforcement, receipt capture, auto-categorization

**Payroll & contractors**
- Global contractor payments in stablecoin or local currency
- Tax document collection (W-8/W-9, 1099), compliance handling
- EOR via partner for full employees

**Close & accounting**
- Continuous auto-reconciliation (industry benchmark: 90%+ auto-match)
- Journal entries, intercompany reconciliation, variance narratives
- QuickBooks / Xero / NetSuite sync; full audit trail

**FP&A**
- Continuously-updated cash flow forecast, runway, burn
- Scenario planning, anomaly alerts
- AI forecasts benchmark at 92–97% accuracy vs 60–70% for spreadsheets

**Credit**
- Collateralized credit line against corporate crypto holdings
- Business EMI on card spend, same mechanism as personal

**Compliance & controls**
- KYB, sanctions screening, travel rule
- Role-based access, segregation of duties, SOC 2 on the roadmap

**Developer**
- CLI, REST API, MCP server, webhooks, sandbox
- Scoped, revocable keys with per-key spend policy

## 11. Security — the constraint that makes it adoptable

- A CLI that moves money is **a credential in a terminal**.
- An MCP server that moves money is **a payment tool attached to a model reading untrusted input**.
- **Prompt injection is the sharp edge** — a malicious email or PR description could induce a payment.
- Mitigation must be **architectural, not prompt-level**:
  - Scoped, revocable keys; per-key limits; CI keys can't touch treasury
  - Policy enforced **server-side**, where the model cannot argue past it
  - Destination allowlists; out-of-band confirmation above a threshold
  - Every action attributable to a key, a policy, and a human owner
- **This is a selling point, not a cost.** No finance team gives an agent live payment access without it.

---

## 12. Business model

- **The app charges the user nothing.** No subscription, no account fees, no per-transaction charges.
- **Primary revenue: PRISM token trading fees.**
- Other lines, none paid by the user:

| Line | Who pays |
|---|---|
| PRISM trading fees | Traders |
| Card interchange | Merchants |
| Brand-funded rewards / meme coin placement | Brands & projects |
| Yield spread | Spread, not a fee |
| EMI interest after month 4 | The user — *the one exception* |

## 13. Known tensions (be honest with candidates and partners)

- **"Free app" vs. month-5 EMI interest.** Needs one clear sentence that survives a marketing page.
- **Hard costs, soft revenue.** Lounge access, equity cashback, card issuing and 0% float are recurring cash costs; token fees peak at launch and decay. Size perks against a conservative floor.
- **Yield vs. instant card auth.** Earning balance must still clear a swipe in ~2s → just-in-time unwind or hot/cold split.
- **Meme coin cashback ≠ equity cashback.** One compounds, one can go to zero. Same word, different risk. Needs different framing + a stablecoin opt-out.
- **Liquidation is the worst possible UX.** "My BTC sold while I slept" is the screenshot that defines the brand.
- **Regulatory surface is wide.** Consumer credit, investment suggestions, fiat rails, KYB/KYC — all live questions.

## 14. Open decisions

- [ ] Custody: self-custody (agent needs session keys) vs. custodial (simpler UX, heavier licensing)
- [ ] First market — "EMI" framing suggests India; drives rails, licensing, issuer
- [ ] Card rails: real network card (needs BIN sponsor) vs. on-chain authorization
- [ ] Where the supply-chain graph for §7 comes from; merchant → brand → parent resolution
- [ ] Build order — **CLI/MCP may be the faster wedge** than the consumer app (developers adopt without a licence-heavy launch)
- [ ] Does [hoodmaker](https://github.com/trade100x/hoodmaker) become the liquidity/execution layer for meme coin cashback?

---

*Sources for §10 benchmarks: [Mercury/Brex/Ramp comparison](https://fintechlabs.com/mercury-vs-brex-vs-ramp-2026-which-finance-stack-should-smbs-use/) · [stablecoin infrastructure providers](https://eco.com/support/en/articles/15232571-best-stablecoin-infrastructure-providers-for-b2b-platforms-2026) · [treasury automation](https://eco.com/support/en/articles/15232575-best-stablecoin-treasury-automation-platforms-2026-sweeps-rebalancing-and-netting) · [AI finance stack](https://chatfin.ai/blog/finance-ai-stack-2026-tools-cfos-close-ap-ar-fpa-reporting/) · [crypto payroll](https://www.riseworks.io/)*
