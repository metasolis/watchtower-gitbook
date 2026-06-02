---
hidden: true
---

# First Loss Capital v2 Architecture

### What this page covers

This model of First-Loss Curation is embedded into Watchtower's yield bearing stablecoin 1AU Dollar ($IAUD). For more information into IAUD's v2 architecture.&#x20;

How **first-loss / junior** capital can sit in IAUD v2 without breaking **Morpho-style markets** at Layer 3. This is an **additive** design: the core v2 doc ships **markets + pro-rata bad debt**; junior is recommended as a **bank/vault waterfall**, not as a second USDC supplier in the same market.

Reference: Perena [USD\* Junior](https://perena.gitbook.io/perena/products/usd-junior). Full detail: `docs/IAUD_Version_2.md` §6.10 and §14.

***

### High-level picture

**Senior** 1AUD holders want hardware lending yield with **defined protection**: something absorbs losses before their token price falls.

**First-loss capital** is a separate risk bucket—higher expected return, first hit on losses—analogous to USD\*-J “standing at the front of the line.”

IAUD v2 already has:

| Mechanism                       | Layer   | Behavior                                                                                          |
| ------------------------------- | ------- | ------------------------------------------------------------------------------------------------- |
| Isolated markets + curator caps | L3 + L2 | Limits _where_ losses can originate.                                                              |
| Pro-rata bad debt               | L3      | If a market fails, **every USDC supplier to that market** shares the write-down by supply shares. |

First-loss adds:

| Mechanism                 | Layer               | Behavior                                                                                                                            |
| ------------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Junior / first-loss vault | L2 (+ L1 waterfall) | Absorbs **reported** losses **before** senior vault NAV and senior 1AUD price—if implemented with an explicit `accrue_loss` policy. |

**Status:** Architecturally compatible; **not** specified for initial v2 launch (open design in engineering doc §14).

***

### What first-loss is _not_

* **Not** the same as **Curator**—curators set caps and adapters; they do not post first-loss capital.
* **Not** automatic if you only add a “junior vault” that **also `supply`s USDC to the same L3 market** as the Hardware Lending Vault. Morpho math then splits bad debt **pro-rata between suppliers**. Junior only “eats first” in that hybrid if it holds \~all supply in that market.
* **Not** a substitute for **liquidation, auction, and underwriting** on unique NFT collateral.

***

### Recommended pattern: bank / vault waterfall

Keep L3 **Morpho-pure**. One primary supplier per market (the senior Hardware Lending adapter). Handle tranching **above** L3:

```
L3  market bad debt  →  pro-rata among that market’s suppliers (typically 100% senior vault)
        ↓
L2  Hardware Lending Vault  real_assets()  drops
        ↓
L1  Bank accrue_loss:
      1) Debit First-Loss Vault NAV (up to policy limit)
      2) Debit other vaults (pro-rata or ordered list)
      3) Reduce iaud_price for remaining 1AUD
```

**Yield (Perena-like, optional):** Junior stakers could receive a **higher share** of bank-level yield via a **leverage factor** on junior TVL in the split formula (e.g. base \~2× on junior weight when junior is below a target % of total TVL). Exact formula is an open product decision.

**Capital form (open):** Junior might stake **1AUD into escrow** (amplify) or **USDC** into a dedicated vault slot—engineering doc lists both as v2.1 questions.

***

### Vault registry fit

The bank allows **up to 16 vault slots** (slot 0 = USDC reserve). A **FirstLoss** vault type would occupy a curator-assigned slot (e.g. slot 2):

* Holds escrowed 1AUD or USDC per policy.
* **Does not** need to `allocate` into L3 if the waterfall is bank-level only.
* Oracle / team accounts may be minimal compared to External Yield vaults.

**Sentinel** can still deallocate senior vaults and cut caps; junior might have separate **cooldown / instant exit fees** (Perena uses 7-day standard unstake with 50 bps, instant 100 bps, emergency 1000 bps if junior TVL < 10% of total—product choices for Watchtower).

***

### Loss and yield ordering (implementation notes)

**When losses are recognized:**

1. L3 liquidation / bad debt reduces market supplier assets.
2. Senior adapter `real_assets()` reflects impairment.
3. Bank compares aggregate NAV to policy; **`accrue_loss`** applies waterfall to junior vault `yielding_tvl` first.

**When yield is recognized:**

* Interest from L3 still lifts senior vault `real_assets()` first in economic terms.
* Bank-level **yield split** can overweight junior (dynamic leverage) when junior TVL is thin—incentivizes replenishing the buffer.

**Invariants to preserve:**

* `total_iaud_minted ≤ Σ vault_nav` after every step.
* Junior cannot be **over-credited** on yield without corresponding TVL (monotonic yield reporting rules from Perena external-yield pattern if similar hooks are reused).

***

### Comparison table

| Approach                                | Junior “eats first”?     | Fits L3 pro-rata?     |
| --------------------------------------- | ------------------------ | --------------------- |
| Junior + senior both supply same market | Only approximately       | Hybrid                |
| Junior vault + L1 waterfall             | Yes (policy-driven)      | Yes                   |
| Pro-rata only (v2 initial)              | No                       | Yes                   |
| Perena USD\*-J (product)                | Yes, at stablecoin stack | N/A (different layer) |

***

### Ship recommendation

Engineering doc recommends: **ship v2 without junior**; add **v2.1** after L3 bad-debt and NAV telemetry exist in testnet/mainnet. Sub-questions for v2.1: denomination, waterfall order across non-junior vaults, leverage formula, exit fees, prohibition on dual-supply to same market.

***

### Related pages

* **IAUD v2 Architecture** — how losses hit 1AUD price today.
* **Lending v2** — suppliers, borrowers, bad debt at L3.
* **Auctions v2** — recovering USDC before bad debt crystallizes.
