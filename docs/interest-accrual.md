# Greenhouse Lending: Interest Accrual Model

## Summary
Greenhouse uses a **compounding interest** approach for tracking borrowed funds on a per-Reserve basis. Each Reserve has a **cumulative borrow rate** stored in high-precision (WAD, or 10^18). Whenever the Reserve is “refreshed,” it applies the time-elapsed since the last update to compound the rate and update outstanding borrows accordingly.

---

## Key Points

1. **Cumulative Borrow Rate (WAD)**  
   - Each Reserve tracks a multiplier called `cumulative_borrow_rate_wads`.  
   - Starts at `1e18` (which we treat as 1.0).  
   - Grows to reflect accrued interest based on an annual borrow rate (in basis points).

2. **Time-Based Compounding**  
   - The annual rate is converted into a per-second rate.  
   - The protocol calculates how many seconds have elapsed since the Reserve’s `last_borrow_update`.  
   - It then uses integer exponentiation to compound the rate for those elapsed seconds.  
   - This effectively simulates continuous compounding each second, but does so in one bulk calculation whenever we refresh.

3. **Borrowed Amount Updates**  
   - After computing the new cumulative rate, the code multiplies the current borrowed amount by **(new_rate / old_rate)** to reflect newly accrued interest.  
   - This difference is then added to the borrowed principal.

4. **Reserve Fee**  
   - Part of the newly accrued interest goes to a “reserve fee” (configured via `reserve_fee_bps`).  
   - This fee accumulates inside the Reserve account to benefit the lender (or protocol).

5. **Borrow / Repay Flow**  
   - **Borrow**: When a new borrow occurs, we first refresh the Reserve so it’s up-to-date, then add the borrowed principal.  
   - **Repay**: Similarly, on repayment, the Reserve is refreshed to include the most recent interest before reducing the outstanding borrowed amount.

6. **Practical Outcome**  
   - Even if a Reserve is only refreshed once every few minutes (or less frequently), the single refresh accounts for all the compounding that would have happened second by second in that period.  
   - Borrowers see their owed principal grow at an effectively continuous rate—lenders capture that interest in proportion to the time elapsed.

---

## Why This Matters
- **Accurate Interest**  
  Ensures the outstanding borrowed amount reflects continuous growth for time that’s actually passed.  
- **No Constant On-Chain Updates**  
  Reduces overhead by applying interest only upon certain actions (borrow, repay, refresh).  
- **Fee Distribution**  
  Lender fees are automatically calculated and added to the Reserve’s fee pool, simplifying reward distribution.

---

## Additional Details
- **Precision**  
  - Internally uses 1e18 WAD arithmetic to maintain consistent high precision.  
  - The integer exponentiation for `(1 + rate_per_second)^(seconds_elapsed)` runs with minimal rounding error.  
- **Borrow Rate Configuration**  
  - Defined per Reserve in basis points (bps).  
  - Updatable by the lender authority as needed for market changes.

---

**In essence, Greenhouse’s model applies second-by-second compounding during each refresh, capturing all accrued interest in a single transaction while preserving accuracy and minimizing on-chain load.**