# Single-Lender, Multiple-Borrower Lending Protocol

This documentation provides an **overview** of the architecture and flow for a Solana‐based lending protocol in which there is **one lender** and potentially **many borrowers**. The system lets the lender supply liquidity (tokens) into a **reserve**, and borrowers collateralize their own tokens to borrow from that reserve. Borrowers accrue interest on their borrowed amounts over time, while the lender’s balance grows by that accrued interest.

- **Single Lender**: A single authority provides liquidity to a **reserve** for lending.  
- **Multiple Borrowers**: Each borrower can staker their own collateral in a pool, then take out a loan against that collateral.  
- **Interest Accrual**: Over time, interest accumulates on all outstanding borrows. The interest earned goes to the lender’s pool.  

In this system, a **Market** represents a unique configuration of lending parameters for a specific pool. Within each Market, there may be multiple **Reserves**, each referencing a different token that can be borrowed. A borrower’s **Obligation** tracks which reserves they have borrowed from and how much they owe.
