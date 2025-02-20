# CRT Protocol: Staking Mechanics Overview

## Core Concept
The CRT staking system uses a liquid staking token (LST) model where users receive share tokens representing their proportion of the staking pool. These shares automatically capture yield and value accrual through their relationship with the underlying collateral.

## Key Components

### Share Tokens
- Users receive share tokens when they stake collateral
- Share tokens represent proportional ownership of the staking pool
- The ratio between total collateral and total shares determines the value per share
- Share value automatically increases as the pool accrues yield

### Collateral Management
- All staked collateral is held in a central reserve
- The protocol tracks the total amount of shares and total collateral
- Effective collateral per share = Total Collateral / Total Shares
- This ratio naturally increases as yield accrues to the pool

## Staking Flow

### Staking Process
1. User deposits collateral into the pool
2. System calculates shares based on current collateral/share ratio
3. User receives share tokens representing their stake
4. Share tokens can be used for other protocol features (e.g., borrowing)

### Unstaking Process
1. User initiates unstake request
2. Request starts unstaking period countdown
3. During unstaking period:
   - Funds remain in pool
   - User can cancel request and return to staked status
4. After period completion:
   - User can execute unstake
   - Shares are burned
   - Equivalent collateral (including accrued yield) is returned

## Value Accrual

### Automatic Yield Distribution
- As the pool generates yield, total collateral increases
- Share token value rises proportionally
- No explicit distribution or claim process needed
- All stakers benefit proportionally to their share

### Share Value Calculation
- Current Value Per Share = Total Pool Collateral / Total Share Supply
- User's Claimable Collateral = User's Shares × Current Value Per Share
- Value automatically compounds as yield accrues

## Safety Features

### Unstaking Period
- Required waiting period between request and withdrawal
- Helps protect protocol stability
- Allows for orderly liquidation of positions
- Can be cancelled if user changes their mind
- Never earn when unstaking, even if cancelled

### Pool Management
- All collateral held in secure reserve
- Share minting/burning strictly controlled
- Automatic yield distribution removes complexity
- Mathematical precision in share calculations

## Benefits

### For Users
- Liquid representation of staked position
- Automatic yield capture
- No manual claiming required
- Flexibility to cancel unstaking

### For Protocol
- Predictable liquidity management
- Protected against rapid withdrawals
- Efficient yield distribution
