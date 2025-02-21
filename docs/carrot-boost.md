---
layout: default
title: "Carrot Boost (Leverage)"
---

# Carrot Boost: Leveraging Your Position

**Carrot Boost** refers to the loop of borrowing stablecoins, buying more CRT, and staking it again. This multiplies your CRT exposure without needing additional external capital.

## How It Works
1. **Stake** your initial CRT.  
2. **Borrow** stablecoins against your staked CRT.  
3. **Buy More CRT** with those borrowed stables.  
4. **Stake the Newly Acquired CRT** to boost your total staked amount.  
5. Optionally, repeat for multiple loops as long as LTV constraints allow.

## Why Use Carrot Boost?
- **Multiply Yield**: If the staking yield exceeds the borrowing rate, leveraging can enhance total returns.  
- **No Liquidations**: Because CRT is stable-backed and the protocol design doesn’t rely on volatile price feeds, positions are not liquidated in the traditional sense.  
- **Efficient Use of Capital**: You preserve your initial CRT plus gain additional yield from the newly staked CRT.

## Risks & Considerations
- **Borrowing Costs**: If the weekly fixed borrow rate spikes or treasury yield drops, your spread narrows.  
- **Protocol Parameters**: The protocol enforces an LTV (Loan-to-Value) cap to keep positions safe.  
- **Exit Plan**: Eventually, borrowed stablecoins must be repaid before you can fully withdraw staked CRT.
