# Phase 1: Network Analysis of Healthcare Delivery Systems

Uncovering critical infrastructure in healthcare networks through computational analysis of Electronic Health Record (EHR) data.

---

## 🎯 Overview

This project analyzes **262,833 patient care transitions** across **120 healthcare facilities** to understand how patients with chronic diseases navigate through the healthcare system. By applying network analysis techniques to EHR data, we identify critical hub facilities, care coordination patterns, and modular community structures.

### Diseases Analyzed
- **Diabetes Mellitus**
- **Cardiovascular Disease** (Heart Disease)
- **Cancer**
- **Chronic Kidney Disease (CKD)**

---

## 🔬 Research Question

> *"How do patient care pathways and network structures differ across chronic diseases, and what are the critical infrastructure elements—universal hubs, bridges, and communities—that support multi-disease care coordination?"*

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| **Language** | Python 3.8+ |
| **Data Processing** | Pandas, NumPy, SQL |
| **Network Analysis** | NetworkX 2.8 |
| **Visualization** | Plotly, Pyvis (Interactive HTML) |
| **Algorithms** | PageRank, Betweenness Centrality, Louvain Community Detection |

---

## 📊 Key Findings

### Universal Hub Infrastructure
- Identified **8 universal hub facilities** that serve all four disease cohorts
- These hubs handle **83.7% of inter-site patient transitions** despite representing only **6.7% of facilities**
- Hub sites: Primary Care, Internal Medicine, Cardiology, Cardiovascular Medicine, Laboratory Services

### Disease-Specific Patterns

| Disease | Avg Sites/Patient | Avg Inter-visit Interval | Network Density |
|---------|-------------------|-------------------------|-----------------|
| Chronic Kidney Disease | 16.1 | 8.2 days | 0.0194 |
| Heart Disease | 15.3 | 8.9 days | 0.0173 |
| Cancer | 14.2 | 7.9 days | 0.0194 |
| Diabetes | 13.8 | 10.2 days | 0.0180 |

### Community Structure
- Discovered **23 functional communities** via Louvain algorithm (modularity Q=0.67)
- Identified **34 bridge facilities** with high betweenness centrality (μ=0.082)
- Top bridges: Internal Medicine, Laboratory Services, Cardiology

### Clinical Implications
1. **Capacity Planning**: Universal hubs represent critical bottlenecks requiring strategic resource allocation
2. **Care Coordination**: Bridge sites are optimal intervention points for care navigator programs
3. **Comorbidity Management**: Network overlap between cardiac and renal communities suggests integrated care clinic opportunities

---

## 📁 Project Structure
```
project-1-network-analysis/
├── README.md                                # This file
├── Network_Analysis_CODE.ipynb              # Main analysis notebook
├── Cancer_Graph.html                        # Disease-specific visualizations
├── Chronic_Kidney_Disease_Graph.html
├── Diabetes_Graph.html
├── HeartDisease_Graph.html
├── Multi_Disease_Interactive_Graph.html     # Integrated network
└── Network_Communities.html                 # Community structure
```

---

## 🚀 How to Run

### 1. Clone the repository
```bash
git clone https://github.com/Mahendra-logics/healthcare-network-analysis.git
cd healthcare-network-analysis/project-1-network-analysis
```

### 2. Install dependencies
```bash
pip install pandas numpy networkx plotly pyvis
```

### 3. Open the Jupyter notebook
```bash
jupyter notebook Network_Analysis_CODE.ipynb
```

### 4. View interactive visualizations
Open the HTML files in any web browser to explore:
- Disease-specific care networks
- Multi-disease network overlay  
- Community structures and hub facilities

---

## 🎨 Interactive Visualizations

The interactive HTML visualizations allow exploration of:
- **Node sizes**: Proportional to patient traffic volume
- **Edge thickness**: Represents transition frequency
- **Colors**: Disease coverage (universal hubs vs. specialized facilities)
- **Communities**: Functional clustering patterns

Simply open any `.html` file in a web browser to interact with the network graphs.

---

## 📈 Methodology

### Data Source
- **Dataset**: De-identified EHR data from hospital network
- **Population**: 1,017 patients with chronic conditions
- **Observation Period**: Multi-year longitudinal records
- **Care Transitions**: 262,833 documented patient visits

### Network Construction
- **Nodes**: Healthcare facilities (care sites)
- **Edges**: Directed patient transitions between facilities
- **Edge Weights**: Frequency of patient transfers
- **Temporal Window**: 365-day active care episode tracking

### Analytical Methods
- **PageRank Centrality**: Recursive importance scoring via referral patterns
- **Betweenness Centrality**: Bridge facility identification through shortest-path analysis  
- **Louvain Algorithm**: Community detection via modularity optimization
- **Pathway Metrics**: Visit frequency, site diversity, inter-visit intervals

---

## 👥 Authors

**Bala Mahendra Pothabathula**  
M.S. Computer Science | University of South Florida  
[LinkedIn](#) | [Email](mailto:pothabathula@usf.edu)

**Collaborators:**  
- Karthikeya Moturi  
- Gowtham Sai Chimmana

*This project was completed as part of CIS 4930/CAI 5155 (Network Analysis & ML with Graphs) at USF.*

---

## 📄 Related Work

This analysis serves as the foundation for **Phase 2**, which applies Graph Neural Networks (GNNs) for multimorbidity risk prediction using patient similarity networks.

📂 [View Phase 2: GNN Prediction →](../project-2-gnn-prediction/)

---

## 📜 License

This project is for educational purposes. Please cite appropriately if referencing this work.

---

## 🔗 Links

- [Main Repository](../)
- [Phase 2: GNN Prediction](../project-2-gnn-prediction/)
- [Full Research Report](../reports/)
