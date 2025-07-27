DeFi Wallet Risk Scoring Project
Welcome to the DeFi Wallet Risk Scoring Project! This initiative aims to assess the risk profile of blockchain wallets based on their on-chain interactions, particularly within lending protocols like Compound V2.

Understanding wallet behavior is crucial in the decentralized finance space for managing liquidity, identifying potential risks, and making informed decisions.

Project Goal
The core objective of this project is to:

Fetch Transaction History: Retrieve relevant on-chain data for a given set of wallet addresses from the Compound V2 protocol.

Data Preparation: Organize and preprocess this raw data into meaningful features.

Risk Scoring: Develop a transparent and justifiable scoring model that assigns each wallet a risk score from 0 to 1000.

Deliverables: Produce a CSV file containing wallet IDs and their corresponding risk scores, accompanied by a comprehensive report detailing the methodology and findings.

Our Approach: The Risk Scoring Pipeline
To achieve our goals, we follow a structured pipeline, ensuring each step contributes to a robust and interpretable risk assessment.

graph TD
    A[Start: Wallet Addresses] --&gt; B(Data Fetching: Compound V2 Subgraph);
    B --&gt; C{Raw On-Chain Data};
    C --&gt; D(Feature Extraction: Supplied, Borrowed, Ratio);
    D --&gt; E(Feature Scaling & Normalization);
    E --&gt; F(Risk Scoring Logic: Weighted Contributions);
    F --&gt; G(Final Risk Score: 0-1000);
    G --&gt; H[End: `104_wallet_risk_scores.csv`];

    style A fill:#f9f,stroke:#333,stroke-width:2px;
    style B fill:#bbf,stroke:#333,stroke-width:2px;
    style C fill:#ccf,stroke:#333,stroke-width:2px;
    style D fill:#bbf,stroke:#333,stroke-width:2px;
    style E fill:#bbf,stroke:#333,stroke-width:2px;
    style F fill:#bbf,stroke:#333,stroke-width:2px;
    style G fill:#9cf,stroke:#333,stroke-width:2px;
    style H fill:#fcf,stroke:#333,stroke-width:2px;

How to Navigate This Project
Jupyter/Colab Notebook: Dive into the jupyter_notebook_filename.ipynb (replace with your actual notebook file name if different) to explore the Python code implementation. This is where you can see the data fetching, processing, and scoring logic in action, and reproduce the results.

REPORT.md: For an in-depth understanding of the project, including the detailed rationale behind feature selection, the precise scoring methodology, and critical findings (such as why many scores might appear uniform), refer to the comprehensive REPORT.md file. It provides the narrative and justification for our technical choices.

104_wallet_risk_scores.csv: This CSV file contains the final output: the calculated risk scores for the 104 specified wallet addresses.

Getting Started (for the Notebook)
To run the analysis yourself:

Environment: Ensure you have Python and necessary libraries installed (pandas, requests). If using Google Colab, these are mostly pre-installed, or can be installed via !pip install.

Wallet List: The notebook contains the list of 104 wallet addresses directly embedded for convenience.

Execution: Simply run the cells in sequence. The notebook will automatically fetch data, process it, calculate scores, and generate the output CSV.

We believe this project provides a robust foundation for understanding and quantifying wallet risk in DeFi. Feel free to explore, scrutinize, and contribute!
