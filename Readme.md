# 🛡️ Wallet Risk Scoring (Compound Protocol) — Round 2 Assignment

This project calculates a **risk score (0–1000)** for 100 Ethereum wallet addresses based on their interaction with the **Compound V2 lending protocol**, using **on-chain transaction data** fetched from the Etherscan API.

---

## 📌 Objective

Given a list of Ethereum wallets, our goal is to:

1. **Fetch** each wallet’s transaction history related to Compound V2 using Etherscan API.
2. **Extract features** that reflect risk (e.g. borrowing volume, liquidations, activity).
3. **Normalize** and use a weighted scoring model to assign each wallet a **risk score** between 0 (low risk) and 1000 (high risk).
4. **Export** results to `wallet_scores.csv`.

---

## 📂 Files

| File | Description |
|------|-------------|
| `Wallet_id.csv` | Input file with 100 wallet addresses (`wallet_id` column) |
| `wallet_scores.csv` | Output file with `wallet_id` and risk `score` |
| `risk_scoring.ipynb` | Jupyter Notebook used to run and generate results |
| `README.md` | This file, describing the approach and usage |

---

## 🔍 Data Collection Method

- Used **Etherscan API** (`tokentx` endpoint) to fetch ERC-20 token transfer history.
- Filtered transactions to/from **Compound cToken contracts** (e.g., cDAI, cUSDC).
- Added a 0.25s delay per API call to prevent rate limiting.

---

## 🧠 Features Used

| Feature | Description |
|--------|-------------|
| `total_supply` | Total tokens supplied to Compound |
| `total_borrow` | Total tokens borrowed |
| `total_repay` | Repayments made |
| `net_balance` | Supply minus Borrow |
| `liquidation_count` | Proxy for liquidations (estimated from tx patterns) |
| `tx_count` | Number of transactions involving Compound |
| `active_days` | Unique days wallet interacted with protocol |

All features are normalized using **Min-Max Scaling**.

---

## 🧮 Risk Scoring Logic

We applied a custom weighted formula:

