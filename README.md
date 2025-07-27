# DeFi Wallet Risk Scoring Project

This project provides a framework for assessing the risk profile of blockchain wallets using their on-chain activity, specifically in relation to the Compound V2 lending protocol. By analyzing wallet-level behavior such as supply and borrow transactions, the system assigns each wallet a transparent, explainable risk score ranging from 0 to 1000.

---

## Table of Contents

- [Overview](#overview)
- [Project Goals](#project-goals)
- [Risk Scoring Pipeline](#risk-scoring-pipeline)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Output](#output)
- [Methodology Summary](#methodology-summary)
- [Contribution](#contribution)
- [License](#license)
- [Contact](#contact)

---

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

## Risk Scoring Pipeline

The end-to-end workflow of the project is summarized below:

```mermaid
graph TD
    A[Start: Wallet Addresses] --> B[Data Fetching: Compound V2 Subgraph]
    B --> C[Raw On-Chain Data]
    C --> D[Feature Extraction: Supplied, Borrowed, Ratios]
    D --> E[Feature Scaling and Normalization]
    E --> F[Risk Scoring Logic: Weighted Feature Contributions]
    F --> G[Final Risk Score (0 - 1000)]
    G --> H[Output: 104_wallet_risk_scores.csv]

    style A fill:#f2f2f2,stroke:#333,stroke-width:1.5px
    style B fill:#dce6f1,stroke:#333,stroke-width:1.5px
    style C fill:#e8f0fe,stroke:#333,stroke-width:1.5px
    style D fill:#dce6f1,stroke:#333,stroke-width:1.5px
    style E fill:#dce6f1,stroke:#333,stroke-width:1.5px
    style F fill:#dce6f1,stroke:#333,stroke-width:1.5px
    style G fill:#b3d9ff,stroke:#333,stroke-width:1.5px
    style H fill:#fbe5f1,stroke:#333,stroke-width:1.5px
