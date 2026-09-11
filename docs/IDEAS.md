# Prism — Idea Log

Running log of ideas for Prism. Newest at the top.

---

## Product structure — two surfaces

Prism splits into two agentic banking experiences sharing one on-chain core:

1. **Personal agentic banking** — the AI CFO for an individual
2. **Business agentic banking** — the AI CFO for a company *(detail pending)*

---

## 1. Personal agentic banking (v0, in progress)

**Thesis: your entire expense life is managed by an agent, not by you.**

### 1.0 The account: one wallet, four rails

The consumer model stays deliberately simple — **you deposit into one wallet, and the agent manages everything from there.** No accounts, no products to pick. The wallet is the hub; everything else is a rail hanging off it.

```
                  deposit
                     │
              ┌──────▼──────┐
              │   WALLET    │  ← single balance, agent-managed
              └──┬───┬───┬──┘
                 │   │   │
   ┌─────────────┘   │   └─────────────┐
   │            ┌────┴────┐            │
   ▼            ▼         ▼            ▼
CARDS        YIELD    FIAT RAILS   CROSS-CHAIN
per-expense  idle     send/receive  trade any token
virtual      balance  fiat in/out   BTC, memes,
cards        earns                  everything
```

- **Cards.** Wallet connects to the card provider; the per-expense virtual cards (1.1) spend directly against it.
- **Yield.** Idle balance earns by default rather than sitting dead. Not a product the user opts into — the resting state of money in Prism.
- **Fiat rails.** Send and receive real-world fiat, so this functions as an actual bank account and not a crypto wallet with extra steps.
- **Cross-chain trading.** Connected out to every other chain — BTC, memecoins, anything. The product is token-agnostic (see core concept); the wallet is the trading surface too.

**Design tension worth solving early:** yield-bearing balance and instant card authorization pull against each other. Money earning yield must still clear a swipe in ~2 seconds. That likely means just-in-time unwind at authorization, or a hot/cold split the agent rebalances — and it is a core piece of engineering, not a detail.

### 1.1 Per-expense virtual cards
- Every recurring expense gets its **own card** — Netflix has a card, rent has a card, the gym has a card.
- Spend control is per-card, so a leak is contained to one line item instead of the whole account.
- The **agent** holds the switch: it can turn a card on or off based on usage, not just the user toggling it manually.
  - Implies the agent has a usage signal per subscription and acts on it (e.g. unused for N months → pause).

### 1.2 Spend analysis — backward and forward
- **Backward:** categorize and analyze historical spend from the user's wallet activity.
- **Forward:** predict *future* expenses, which is the actual differentiator. Budgeting is automated rather than a form the user fills in.

### 1.2 The card product itself

Ambition: **the best card in the industry**, not a crypto-card compromise. The rewards stack is where it differentiates.

- **Premium perks.** Lounge access and the usual premium-tier benefits, so it competes on the same ground as a top-tier consumer card. *(→ open question: "launch access" may instead mean early access to token launches on Robinhood — a crypto-native perk no other card can offer. Confirm which, or do both.)*
- **Points.** Card earns points; points convert into other rewards. Standard, expected, table stakes.
- **Brand-token cashback — the differentiated one.** Spend at a brand, get **that brand's token back as cashback**. Buy from Apple, get Apple back.

#### Why brand-token cashback is the strongest idea here

It closes the loop with the spend-to-investment graph (1.4). Everywhere else, cashback is a small rebate you spend again. Here, **your consumption quietly builds a portfolio of the companies you actually use.**

```
spend at Apple ──► cashback in Apple ──► you now hold Apple
      │                                        │
      └──── recurring spend compounds ─────────┘
             the position grows with the habit
```

- It makes the 1.4 thesis *automatic* instead of advisory. The tree says "your spending shows you believe in this category" — the cashback acts on it without the user lifting a finger.
- The pitch writes itself: *"you already made Apple rich. Now you own some of it."*
- Retention is structural — leaving means giving up an accumulating position, not just a points balance.
- Only works because this is built on a brokerage chain. A normal neobank cannot pay you in equity.

#### Meme coin cashback — the fallback tier

Answers the "what if the brand isn't listed?" case. **No stock behind the brand → the user gets a meme coin instead**, selected by a Prism engine. Sourced from either on-chain Solana meme coins or Robinhood Chain meme coins.

So the cashback ladder is:

| Brand type | Cashback asset |
|---|---|
| Publicly listed | That brand's token / tokenized equity |
| Not listed | Meme coin, chosen by the selection engine |

Two notes on this, one upside and one risk:

**Upside — the selection engine is a distribution business.** Paying cashback in a meme coin creates continuous, recurring buy pressure on that coin, sourced from real consumer spend rather than speculation. Meme coin teams would pay meaningfully for that slot. This is plausibly a second revenue line and a reason for projects to court Prism — but it also means the engine's ranking must be honest about whether placement is paid, or the feature becomes a liability the first time a selected coin collapses.

**Risk — this tier behaves nothing like the equity tier.** Equity cashback compounds into ownership; a meme coin can go to zero in a week. Users will not distinguish between the two tiers by themselves, so the product has to: different framing, different expectations, possibly an opt-out into plain stablecoin cashback for users who don't want the exposure.

**Possible tie-in with hoodmaker.** Sourcing meme coins for cashback payouts needs liquidity and routing on Robinhood Chain — which is what the sibling project is built around. Worth checking whether hoodmaker becomes Prism's execution layer for this tier rather than routing through third-party venues.

#### Crypto-collateralized EMI — "don't sell your Bitcoin to buy things"

Any card spend can be split into **4 monthly installments at zero interest**, with the user's existing crypto posted as collateral. Collateral can be BTC, ETH, SOL, or even meme coins. After the 4-month window, interest kicks in.

```
spend $2,000 ──► split into 4 × $500 ──► post BTC as collateral
                                              │
                  months 1–4: 0% interest ────┤
                  month 5+:   interest accrues ┘
```

**Why this is the right product for this user base.** The real pain isn't affordability — it's that crypto holders don't want to *sell* to spend. Selling is a taxable event and a break in conviction. This converts a dead, illiquid conviction position into working purchasing power without unwinding it. That's a sharper pitch than any BNPL offer: *"keep your Bitcoin, spend anyway."*

**Where "zero interest" actually comes from.** It isn't charity, and the economics should be stated plainly internally:
- The loan is **over-collateralized**, so credit risk is near zero — unlike conventional BNPL, this needs no underwriting and no credit bureau.
- The locked collateral can earn while it sits (ties directly into the yield rail, 1.0).
- Interchange on the original spend.
- Revenue arrives at **month 5**, on balances that roll past the free window — the same model as a credit card's grace period.

**Retention effect.** An open EMI means collateral is locked in Prism. Leaving requires repaying first. Combined with accumulating cashback positions (1.2), the switching cost compounds.

**Risks that need real design, not a footnote:**
- **Liquidation is the worst experience in the product.** "Your Bitcoin was sold while you slept because SOL dumped 30%" will churn a user permanently and generate the screenshots that define the brand. The agent should pre-warn, offer top-up, and auto-deleverage *before* forced liquidation — this is exactly the kind of thing an AI CFO should be doing on the user's behalf.
- **Meme coins as collateral need drastically different terms.** Tiered LTV by asset: BTC/ETH generous, SOL moderate, meme coins very low or excluded. A meme coin can gap down faster than any liquidation engine can react, leaving the loan undercollateralized and the loss on Prism's book.
- **This is consumer credit.** BNPL is under active regulatory tightening in several markets, and crypto-collateralized consumer lending adds a second licensing question on top.

*Terminology note: "EMI" suggests India as a first market — worth confirming, since it drives the fiat rails, licensing, and card issuer decisions.*

### Open questions (card & rewards)
- [ ] LTV tiers per collateral asset, and which assets are excluded as collateral entirely?
- [ ] Who takes the loss on an undercollateralized liquidation — Prism's balance sheet or a lending partner's?
- [ ] What's the post-4-month interest rate, and is that the main revenue line or a backstop?
- [ ] Is the EMI book funded by Prism, by the yield pool (user deposits lending to user borrowers), or a third-party lender?
- [ ] First market — the "EMI" framing implies India; confirm, as it drives rails, licensing, and issuer choice.
- [ ] **"Launch access" — lounge access, or early access to Robinhood token launches?** Materially different features.
- [ ] Cashback asset: tokenized equity of the brand? Availability is jurisdiction-dependent — which markets can actually receive it, and what's the fallback (fractional shares, points, stablecoin) where it isn't permitted?
- [x] ~~What happens when the brand isn't listed?~~ → **meme coin cashback tier** (above).
- [ ] How does the meme coin selection engine rank? Liquidity, momentum, paid placement, safety screen? Is paid placement disclosed?
- [ ] Rug protection: what happens to the user when a cashback meme coin collapses? Is there an auto-convert-to-stable option?
- [ ] Opt-out: can a user choose stablecoin cashback instead of meme coin exposure?
- [ ] Who funds the rewards? Interchange alone, or brand-funded (brands pay for equity-linked loyalty — potentially a second revenue line)?
- [ ] Does cashback-as-equity create a taxable event at receipt, and does the agent track cost basis for the user?

### 1.3 How the forecast works
Two inputs combine:
- **Inferred from wallet history — cadence detection.** The agent learns periodicity from past on-chain spend: a movie once a month, a trip every three months, an annual renewal. It projects those forward into an expected cost curve: *"your predicted spend next quarter is X because you typically do A, B, C."*
- **Elicited in chat — forward intent.** The agent proactively asks *"are you planning anything else coming up?"* and folds the answer into the forecast. Planned one-offs (a wedding, a move, a new laptop) never appear in history, so they have to be asked for.

The forecast is the budget. The user doesn't set one; the agent derives it and manages against it.

### 1.4 Spend-to-investment graph ("where does my money actually go?")

**Thesis: your own spending is the best investment research you have, and nobody surfaces it to you. A bank should.**

Every transaction gets an expandable **money-flow tree**: this payment went to brand X, brand X's economics run on suppliers A, B, C, and *these* are the investable names in that chain.

**The key move is going upstream, not stopping at the brand.** Subscribing to ChatGPT doesn't mean "invest in OpenAI" — OpenAI isn't the trade, and the obvious surface read is the shallow one. The real exposure sits behind it: compute, data centers, cheap manufacturing, power. The tree's job is to walk from the thing you paid for to the listed companies that actually capture that spend.

```
$20 ChatGPT subscription
└── OpenAI (private — not directly investable)
    ├── Compute / accelerators ....... NVDA, AMD
    ├── Foundry / manufacturing ...... TSM
    ├── Data center & cloud .......... MSFT, and DC REITs
    └── Power & cooling .............. utilities, grid names

$12 burger
└── Restaurant brand ................ MCD / QSR
    ├── Beef & protein supply ........ TSN
    ├── Potatoes / frozen ............ LW
    ├── Distribution ................. SYY
    └── Packaging .................... PKG
```

**Two levels of signal:**
- **Your own spend.** Bucket it and you can see your real exposure: "I spend most here, so I believe in this category" — a thesis derived from behavior instead of vibes.
- **Aggregate user spend.** Across all Prism users, spending *is* a leading indicator — it moves ahead of reported revenue. If category spend is accelerating across the base, that's a signal to surface: *"more people are spending here, this looks like it's about to run."* This aggregate is proprietary data that no brokerage or research desk has in this form — likely the deepest moat in the product.

**Framing to the user:** not "buy this," but *"if you think burgers are going to skyrocket, here's the chain that captures it."* Give the tree and the reasoning, let the conviction be theirs.

**Strategic fit with Robinhood:** this is why the Robinhood build is more than distribution — the insight ends in a tradeable ticker, and the brokerage is already in the same surface. Spend → money-flow tree → thesis → buy, with no hop out of the product. The loop closes in a way a standalone neobank can't match.

### Open questions (investment layer)
- [ ] Where does the supply-chain graph come from — licensed data (e.g. supplier/customer relationship datasets), LLM-constructed, or hand-curated for the top N brands?
- [ ] Merchant → brand → parent-company resolution is the hard plumbing problem; what resolves it?
- [ ] Regulatory line: surfacing exposure trees and aggregate spend trends is research/data; naming a ticker as a suggestion edges toward advice. Where does this sit, and under whose license — ours or Robinhood's?
- [ ] Does the aggregate signal get sold/surfaced as its own product later?

### Open questions (personal)
- [ ] Custody model: self-custody (agent needs session keys / spend policies) or custodial (simpler UX, heavier licensing)?
- [ ] Where does the yield come from — T-bill-backed stablecoins, lending markets, something native to Robinhood Chain? Risk disclosure to the user?
- [ ] Fiat rails: partner bank / licensed provider per geography. Which market first?
- [ ] Bridging: who moves assets cross-chain, and who eats the risk when a bridge fails?
- [ ] Card rails: who issues? On-chain spend authorization vs. a real card network (Visa/Mastercard BIN sponsor)?
- [ ] Where does off-chain merchant data come from for categorization, if spend is on-chain?
- [ ] How much authority does the agent have — advisory, approve-with-confirmation, or fully autonomous?
- [ ] Does the agent also *fund* forecasted expenses (pre-allocate / auto-save into buckets)?

---

## Business model — free to the user, funded by the token

**Principle: the app charges the user nothing.** No subscription, no account fees, no per-transaction charges. Free to use, in the spirit of Fomo.

**Primary revenue: trading fees on the PRISM token.** The token launches on Robinhood and trades; the fees that trading generates fund the company. The bank is free because the token pays for it.

### Revenue lines, mapped against the "free" principle

| Line | Who pays | Consistent with "free to use"? |
|---|---|---|
| PRISM token trading fees | Traders | Yes — primary line |
| Card interchange | Merchants | Yes — user never sees it |
| Brand-funded rewards / paid meme coin placement | Brands & projects | Yes |
| Yield spread on idle balances | Spread, not a fee | Yes, if disclosed |
| **EMI interest after month 4** | **The user** | **Conflict — see below** |

### Two tensions to resolve deliberately

**1. "No other charge" vs. month-5 EMI interest.** The EMI product (1.2) charges interest once the 4-month window closes. That is a direct user charge. Either the principle means "no *fees*, but interest on borrowed money is not a fee" — a defensible line most users accept — or the EMI needs a different backend. Worth writing the exact sentence that will appear in marketing, because "the app is free" and "you'll be charged interest" have to coexist on the same page.

**2. Cost structure is hard currency; token revenue is not.** The product carries real, recurring cash costs — card issuing, lounge access, cashback paid in equity and meme coins, and the float on interest-free lending. Token trading fees are cyclical and tend to be highest at launch, then decay with attention. Funding fixed recurring costs from reflexive, volume-dependent revenue is the failure mode that kills token-funded consumer products: the perks get cut exactly when sentiment is already weak, which accelerates the decline.

This doesn't argue against the model — it argues for sizing perks against a **conservative floor** of token revenue, with interchange and the post-window interest as the load-bearing base, and token fees treated as the upside that funds growth rather than the thing that keeps the lights on.

### Open questions (business model)
- [ ] What is the exact fee mechanism on PRISM — a protocol-level trading fee, or a share of venue fees? Who captures it?
- [ ] What's the conservative-case token revenue, and does the perk stack survive at that level?
- [ ] Is the token purely a revenue instrument, or does it carry product utility (fee discounts, reward multipliers, tiering)?
- [ ] How do the free perks stay funded through a bear market?

---

## 2026-09-11 — Core concept (v0, in progress)

**Prism is an on-chain, stablecoin-based neobank built on Robinhood Chain, with an AI agent as the primary interface — an "AI CFO" rather than a banking app.**

### What it is
- **On-chain neobank.** Balances, payments, yield, and credit all settle on-chain; stablecoins are the account unit, not a crypto side-feature.
- **AI-first interface.** The product is an agentic layer — an AI CFO / banking agent that acts on the user's behalf (moves, allocates, pays, reports) rather than a dashboard the user operates manually.
- **Built on Robinhood.** Robinhood Chain is the settlement home and the distribution wedge.

### Token
- Launch a **PRISM token on Robinhood**, using Robinhood's distribution as the go-to-market channel.
- The **product itself is token-agnostic** — supports all tokens, not just PRISM. The token is the network/GTM asset; the bank serves whatever assets the user holds.

### Positioning notes
- "Neobank" framing, not "DeFi app" — the target experience is a bank account you talk to.
- Tech stack is deliberately undecided; the product thesis leads.

### Open (to be filled in)
- [ ] Offering / product surface — *user is detailing this next*
- [ ] Target user (consumer? crypto-native treasury? SMB?)
- [ ] Revenue model
- [ ] Token utility & mechanics
- [ ] Regulatory / licensing posture
- [ ] Robinhood relationship: permissionless build vs. partnership
