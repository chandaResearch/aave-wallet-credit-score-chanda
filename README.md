# Aave V2 Wallet Credit Scoring System

This project builds a machine learning-inspired rule-based system to assign credit scores (0–1000) to wallets based on their transaction history on the Aave V2 protocol.

## 📊 Goal

To detect risky vs. responsible behavior in DeFi by assigning wallet credit scores using behavioral indicators from `deposit`, `borrow`, `repay`, `redeemunderlying`, and `liquidationcall` actions.

---

## 🛠️ Methodology

1. **Data Loading**: Parsed 100K+ records from `user_transactions.json`.
2. **Feature Engineering**: Extracted wallet-level metrics:
   - Action counts (`deposit`, `borrow`, etc.)
   - Ratios: `repay/borrow`, `redeem/deposit`
   - Active span in days
3. **Scoring Logic**:
   - +100 if `repay > 0`
   - +100 if `repay/borrow > 1`
   - +50 if `redeem/deposit > 1`
   - +50 if wallet active for >30 days
   - −100 if no repayment but borrowed
   - −200 if `liquidationcall > 0`
   - Score bounded between 0–1000
4. **Export**: Saved final scores to `wallet_scores.csv`

---

## 🧾 Files

- `notebook.ipynb` — Main analysis
- `wallet_scores.csv` — Final scores
- `score_distribution.png` — Score histogram
- `analysis.md` — Score interpretation

---

## 📈 Score Interpretation

| Score Range | Behavior Description                  |
|-------------|----------------------------------------|
| 0–300       | Highly risky, liquidated, no repayment |
| 300–600     | Moderate usage, missing repayments     |
| 600–800     | Mostly safe, good ratios               |
| 800–1000    | Very reliable, strong repayment habits |

---
