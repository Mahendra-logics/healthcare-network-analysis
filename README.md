# Healthcare Network Analysis: Multi-Disease Patient Care Pathways

Uncovering critical infrastructure in healthcare networks through analysis of Electronic Health Record (EHR) data.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![NetworkX](https://img.shields.io/badge/NetworkX-Graph%20Analysis-orange.svg)
![Status](https://img.shields.io/badge/Status-Completed-green.svg)

---

## Overview

This project analyzes **262,833 patient care transitions** across **120 healthcare facilities** to understand how patients with chronic diseases navigate through the healthcare system. By applying network analysis techniques to EHR data, we identify critical hub facilities and care coordination patterns.

**Diseases Analyzed:**
- Diabetes
- Heart Disease
- Cancer
- Chronic Kidney Disease (CKD)

---

##  Research Question

*"How do patient care pathways and network structures differ across chronic diseases, and what are the critical infrastructure elements—universal hubs, bridges, and communities—that support multi-disease care coordination?"*

---

## Tech Stack

| Category | Tools |
|----------|-------|
| **Language** | Python |
| **Data Processing** | Pandas, NumPy, SQL |
| **Network Analysis** | NetworkX |
| **Visualization** | Plotly, Pyvis (Interactive HTML) |
| **Algorithms** | PageRank, Betweenness Centrality, Louvain Community Detection |

---

## Key Findings

- Identified **universal hub facilities** that serve all four disease cohorts
- Discovered **modular community structures** revealing distinct care pathways
- Quantified facility importance using **PageRank** and **Betweenness Centrality**
- Uncovered **hub-dependent architecture** critical for care coordination

---

## Project Structure
```
├── Network_Analysis_CODE.ipynb    # Main analysis notebook
├── Cancer_Graph.html
├── Chronic_Kidney_Disease_Graph.html
├── Diabetes_Graph.html
├── HeartDisease_Graph.html
├── Multi_Disease_Interactive_Graph.html
├── Network_Communities.html
└── README.md
```

---

## How to Run

1. Clone the repository:
```bash
   git clone https://github.com/Mahendra-logics/healthcare-network-analysis.git
```

2. Install dependencies:
```bash
   pip install pandas numpy networkx plotly pyvis
```

3. Open the Jupyter notebook:
```bash
   jupyter notebook Network_Analysis_CODE.ipynb
```

4. View interactive visualizations by opening the HTML files in any web browser

---

## Interactive Visualizations

The interactive HTML visualizations allow exploration of:
- Disease-specific care networks
- Multi-disease network overlay
- Community structures and hub facilities

*Open the HTML files in any web browser to interact with the network graphs.*

---

## Future Work (Part 2 - In Progress)

Extending this analysis with **Graph Neural Networks (GNNs)** for predictive modeling:
- Implementing GCN, GraphSAGE, GAT models
- Predicting patient readmission risk
- Disease progression modeling

---

## 👤 Author

**Bala Mahendra Pothabathula**  
M.S. Computer Science | University of South Florida  
[LinkedIn](https://www.linkedin.com/in/bala-mp) | [Email](mailto:bala29mahendra@gmail.com)

*This project was completed as part of CIS 4930/CAI 5155 (Network Analysis & ML with Graphs) at USF.*  
*Collaborators: Karthikeya Moturi, Gowtham Sai Chimmana*

---

## 📄 License

This project is for educational purposes. Please cite appropriately if referencing this work.
