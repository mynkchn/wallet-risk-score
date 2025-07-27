# Comprehensive Report: DeFi Wallet Risk Scoring

This report outlines the methodology, logic, and key insights behind our credit scoring system for wallets interacting with the Compound V2 protocol. Our model assigns a risk score between 0 and 1000, where higher scores indicate higher financial risk.

## 1. Data Collection Strategy

We used The Graph Protocol to query Compound V2’s blockchain data. The data was collected using a GraphQL-based Subgraph endpoint.

### Wallets Analyzed:
- 104 Ethereum wallet addresses

### Data Fetched Per Wallet:
- `supplyBalanceUnderlying`
- `borrowBalanceUnderlying`

### Query Used (GraphQL):

```graphql
query GetAccountBalances($walletId: ID!) {
  account(id: $walletId) {
    id
    tokens {
      symbol
      supplyBalanceUnderlying
      borrowBalanceUnderlying
    }
  }
}
```

## 2. Features Selected for Risk Evaluation

| Feature           | Description                                                   | Risk Contribution        |
|-------------------|---------------------------------------------------------------|--------------------------|
| `total_supplied`  | USD value of total supplied assets                            | Higher = Lower Risk      |
| `total_borrowed`  | USD value of total borrowed assets                            | Higher = Higher Risk     |
| `net_borrow_ratio`| total_borrowed / total_supplied (leverage ratio)              | Higher = Higher Risk     |

All features are normalized between 0 and 1 before risk computation.

## 3. Risk Scoring Methodology

We use a weighted sum of normalized features to calculate a risk score out of 1000.

### Risk Score Formula:

```python
scaled_supply = min(total_supplied, 10000) / 10000
scaled_borrow = min(total_borrowed, 10000) / 10000
ratio = min(total_borrowed / (total_supplied + 1), 1)

risk_score = round(min(
    400 * (1 - scaled_supply) +  # More supply = safer
    300 * ratio +                # High leverage = more risky
    300 * scaled_borrow,         # More borrowing = more risky
    1000
))
```

### Scoring Breakdown:
- Supply Risk (Max 400): More collateral reduces risk.
- Borrow Risk (Max 300): Higher borrow values increase risk.
- Leverage Risk (Max 300): High borrow-to-supply ratio increases risk.

## 4. Handling Missing or Inactive Wallets

Many wallets had no activity in Compound V2 at the time of querying. For those, we defaulted their values:

```python
total_supplied = 0
total_borrowed = 0
ratio = 0
```

Leading to:

```text
risk_score = 400 * (1 - 0) + 300 * 0 + 300 * 0 = 400
```

### Interpretation:
- A score of 400 is a default neutral score for wallets without any protocol activity.
- It does not imply high risk, but insufficient data for scoring.

## 5. Insights from Results

- Majority of wallets scored 400 due to inactivity or data absence.
- High scores (>700) were observed for highly leveraged wallets with small supply and large borrow.
- Low scores (<300) typically belonged to wallets with large supply and no borrowing activity.

## 6. Potential Improvements

### Feature Engineering:
- Include liquidation history, collateral types, and interaction frequency.
- Analyze wallet behavior over time (longitudinal risk).

### Broader Coverage:
- Expand to other DeFi protocols (Aave, MakerDAO, etc.).
- Use wallet clustering to identify user profiles.

### Risk Categorization:
Define buckets:
- 0–300: Low Risk  
- 301–600: Moderate Risk  
- 601–1000: High Risk

## Summary

| Step                    | Details                                                                       |
|-------------------------|--------------------------------------------------------------------------------|
| Wallets Queried         | 104                                                                            |
| Data Source             | Compound V2 Subgraph (via The Graph)                                           |
| Features Used           | Total Supplied, Total Borrowed, Borrow Ratio                                   |
| Scoring Method          | Weighted sum: Supply (400), Ratio (300), Borrow (300)                          |
| Default Score           | 400 if no data                                                                 |
| High Risk Indicator     | High borrow, high leverage, low collateral                                     |
| Low Risk Indicator      | High collateral, low borrow, low leverage                                      |

## Files in Repository

| File Name                     | Description                                    |
|------------------------------|------------------------------------------------|
| `compound_wallets.csv`       | List of wallets with their risk scores         |
| `risk_scoring_notebook.ipynb`| Jupyter Notebook for fetching & scoring wallets|
| `REPORT.md`                  | This detailed technical report                 |
| `requirements.txt`           | Python dependencies                            |

## Author

- Mayank Chouhan  
  Data Science Enthusiast, Python Developer, DeFi Analyst  
  LinkedIn: [https://www.linkedin.com/in/maynkchn](https://www.linkedin.com/in/maynkchn)
