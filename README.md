# DeFi Wallet Risk Scoring Project

This project provides a framework for assessing the risk profile of blockchain wallets using their on-chain activity, specifically in relation to the Compound V2 lending protocol. By analyzing wallet-level behavior such as supply and borrow transactions, the system assigns each wallet a transparent, explainable risk score ranging from 0 to 1000.

## Overview

In decentralized finance (DeFi), wallet behavior is an important signal for:

- Assessing protocol-level risks
- Making informed decisions in credit delegation or lending
- Monitoring borrowing behaviors and liquidation risks

This project introduces a fully transparent and reproducible risk scoring pipeline that processes wallet-level transaction data from Compound V2 and outputs a standardized risk score.

---

## Project Goals

1. **Fetch On-Chain Wallet Data**  
   Retrieve relevant wallet interactions from Compound V2 using its public GraphQL subgraph endpoint.

2. **Feature Engineering**  
   Derive interpretable wallet metrics such as supply amount, borrow amount, and their ratios.

3. **Risk Scoring**  
   Implement a scoring algorithm to assign normalized risk scores to each wallet.

4. **Reporting and Output**  
   Export the results into a CSV file and explain the methodology in a separate technical report.

---


The end-to-end workflow of the project is summarized below:
graph TD
    A[Start: Wallet Addresses] --> B[Data Fetching from Compound V2 Subgraph]
    B --> C[Raw On-Chain Data]
    C --> D[Feature Extraction: Supplied, Borrowed, Ratios]
    D --> E[Feature Scaling and Normalization]
    E --> F[Risk Scoring Logic: Weighted Contributions]
    F --> G[Final Risk Score (0 - 1000)]
    G --> H[Output: 104_wallet_risk_scores.csv]

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#bbf,stroke:#333,stroke-width:2px
    style C fill:#ccf,stroke:#333,stroke-width:2px
    style D fill:#bbf,stroke:#333,stroke-width:2px
    style E fill:#bbf,stroke:#333,stroke-width:2px
    style F fill:#bbf,stroke:#333,stroke-width:2px
    style G fill:#9cf,stroke:#333,stroke-width:2px
    style H fill:#fcf,stroke:#333,stroke-width:2px

