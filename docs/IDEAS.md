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

### 1.1 Per-expense virtual cards
- Every recurring expense gets its **own card** — Netflix has a card, rent has a card, the gym has a card.
- Spend control is per-card, so a leak is contained to one line item instead of the whole account.
- The **agent** holds the switch: it can turn a card on or off based on usage, not just the user toggling it manually.
  - Implies the agent has a usage signal per subscription and acts on it (e.g. unused for N months → pause).

### 1.2 Spend analysis — backward and forward
- **Backward:** categorize and analyze historical spend from the user's wallet activity.
- **Forward:** predict *future* expenses, which is the actual differentiator. Budgeting is automated rather than a form the user fills in.

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
- [ ] Card rails: who issues? On-chain spend authorization vs. a real card network (Visa/Mastercard BIN sponsor)?
- [ ] Where does off-chain merchant data come from for categorization, if spend is on-chain?
- [ ] How much authority does the agent have — advisory, approve-with-confirmation, or fully autonomous?
- [ ] Does the agent also *fund* forecasted expenses (pre-allocate / auto-save into buckets)?

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
