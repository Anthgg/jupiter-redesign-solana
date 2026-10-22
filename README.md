# UI/UX Redesign Case Study: Jupiter Exchange 3.0
**Challenge:** Superteam India — Redesign Your Favourite App on Solana  
**Selected Platform:** **Jupiter Exchange (`jup.ag`)**  
**Category:** DeFi / DEX Aggregator Experience  
**Prize Pool:** \$1,500 USDC (1st: \$700, 2nd: \$500, 3rd: \$300)  
**Deliverable:** Comprehensive Design Rationale, Before/After Audits, and Interactive Visual Specifications  

---

## 1. Executive Summary & Design Mission

Jupiter is undeniably the engine of Solana DeFi, routing billions in weekly volume. Yet, as Solana scales to millions of mobile-first users, Jupiter's core swap interface suffers from **technical debt and cognitive overload**:
- High friction for non-expert traders navigating Priority Fees, Jito MEV tips, and Dynamic Slippage.
- Cryptic error modals when transactions fail under network congestion.
- Zero awareness or built-in utility for stranded SPL token account rent (~0.002039 SOL per empty account).

**Our Mission:**  
Redesign Jupiter's core Swap interaction into an intuitive, transparent, and aesthetically refined experience that preserves institutional-grade routing power while delivering consumer-grade simplicity.

---

## 2. Eligibility Questions & Core Rationale

### Q1: Which app did you redesign, and which features did you pick?
**Answer:**  
We redesigned **Jupiter Exchange (`jup.ag`)**, focusing on three high-friction touchpoints:
1. **The Swap Execution & Protection Modal:** Replacing fragmented priority fee sliders (Turbo/Ultra/Custom) with an automated, MEV-aware **Smart Guard** system.
2. **The Post-Swap Settlement & "Rent-Back" Tray:** A native feature that identifies and reclaims empty token account rent directly on swap completion.
3. **The Mobile-First Confirmation Drawer:** Re-architected for single-thumb ergonomics, real-time price impact visualization, and plain-English pre-flight simulation.

### Q2: What was the biggest problem you found in the current design, in 2–3 sentences?
**Answer:**  
In the current Jupiter interface, critical execution parameters (priority fees, Jito tips, and slippage tolerance) are fragmented across buried dropdowns and technical sliders that overwhelm non-power users while failing to clearly communicate real-world MEV sandwich risk. Additionally, failed transactions due to expired blockhashes or unsimulated routes provide vague cryptographic error logs rather than actionable, plain-English remedies.

---

## 3. In-Depth Feature Breakdown: Before vs. After

### Feature 1: The "Smart Guard" Execution Engine (Replacing Manual Fee Sliders)

#### The Problem (Current UX)
Traders currently face 4 different levers when swapping:
- Priority Level: Fast / Turbo / Ultra / Custom (microlamports/CU)
- Jito Tip Level: None / Min / Median / High
- Slippage Tolerance: 0.1% / 0.5% / 1.0% / Dynamic
- Max Accounts Lock

During high volatility, users guess random numbers, frequently overpaying fees by 10x or experiencing failed transactions when the blockhash expires.

#### The Redesign (After)
We consolidated these 4 technical controls into a single, intuitive **Execution Mode Selector**:
- **Shielded (Default):** Automated Jito bundle protection. Transactions are never broadcast to the public mempool, eliminating front-running and sandwich attacks. Zero priority fee charged if the trade fails.
- **Turbo (Speed-First):** Aggressive dynamic priority fee computed directly against the current leader's blockspace demand.
- **Economy:** Standard baseline fee for non-urgent staker / DCA rebalancing.

```
+-------------------------------------------------------------+
| JUPITER SMART GUARD                                         |
| [⚡ Shielded (Anti-MEV)]    [🚀 Turbo]    [🌱 Economy]      |
|                                                             |
| Route: SOL -> Raydium CLMM -> Phoenix -> USDC              |
| Expected Output: 842.15 USDC (Minimum Guaranteed: 840.45)   |
| Maximum Price Impact: 0.04%                                 |
| Protection: Jito Private Bundle Active (0% Sandwich Risk)  |
+-------------------------------------------------------------+
```

---

### Feature 2: Native "Rent-Back" Reclaim Tray

#### The Problem (Current UX)
Every time a user trades a new meme coin or SPL token on Solana, a token account is created locking **0.002039 SOL** (~$0.30 - $0.40 USD). Active traders accumulate 20 to 50 empty accounts, stranding $10 to $20 in rent that requires sketchy third-party burner apps to reclaim.

#### The Redesign (After)
When a user sells 100% of a token balance on Jupiter, our redesigned swap receipt includes an automatic or 1-tap **"Close Account & Reclaim Rent"** toggle:
- *"Selling entire balance of $BONK: Toggle to close token account and receive +0.00204 SOL back into your wallet instantly."*
- Net effect: The user's network fee is completely neutralized by the rent refund!

---

### Feature 3: Ergonomic Mobile Confirmation Drawer

#### The Problem (Current UX)
On mobile devices, Jupiter's confirmation dialog sits awkwardly in the viewport center, forcing users to stretch their thumbs to the top corners to review route details or dismiss errors.

#### The Redesign (After)
- Bottom-sheet sheet physics with haptic feedback.
- Visual token pill comparison (`SOL` ➔ `USDC`) with animated route path.
- Clear, high-contrast **"Hold to Swap"** or biometric swipe gesture preventing accidental taps on high-value orders.

---

## 4. Design Architecture & Visual Assets

We have authored a standalone, interactive HTML/CSS responsive prototype demonstrating the complete interactive flow, before/after comparisons, and mobile drawer transitions.

- Interactive Prototype File: `jupiter_redesign_preview.html`
- Color Palette: Deep Slate `#0B0E14`, Solana Electric Purple `#9945FF`, Cyber Emerald `#14F195`, Clean White `#F9FAFB`.
- Typography: Inter Display + JetBrains Mono for financial figures.

---
*Submitted for Superteam India Open Design Bounty Evaluation.*
