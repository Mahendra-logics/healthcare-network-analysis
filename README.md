# Healthcare Network Analysis & Machine Learning

**A comprehensive two-phase study combining network science and deep learning to analyze patient care pathways in chronic disease management**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![NetworkX](https://img.shields.io/badge/NetworkX-2.8-orange.svg)](https://networkx.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-Geometric-red.svg)](https://pytorch-geometric.readthedocs.io/)

---

## 🎯 Project Overview

This repository presents a complete analysis of Electronic Health Record (EHR) data for chronic disease management, structured in two complementary research phases:

**Phase 1** applies **network analysis** to identify critical healthcare infrastructure and care coordination patterns.

**Phase 2** leverages **Graph Neural Networks** to predict multimorbidity risk and recommend preventive care interventions.

### Diseases Analyzed
- Diabetes Mellitus
- Cardiovascular Disease (Heart Disease)
- Cancer
- Chronic Kidney Disease (CKD)

---

## 📊 Phase 1: Network Analysis of Healthcare Infrastructure

> *Identifying universal hubs, bridges, and community structures in patient care networks*

### Key Results
- Analyzed **262,833 patient transitions** across **120 care facilities**
- Identified **8 universal hub sites** handling **83.7%** of all transitions
- Detected **23 functional communities** (modularity Q=0.67)
- Quantified **34 bridge facilities** critical for care coordination

### Methods & Tech Stack
`NetworkX` `PageRank` `Betweenness Centrality` `Louvain Algorithm` `Plotly` `Interactive Visualizations`

### 📂 [Explore Phase 1 →](./project-1-network-analysis/)

---

## 🧠 Phase 2: Graph Neural Network Risk Prediction

> *Predicting multimorbidity risk using patient similarity networks and deep learning*

### Key Results

| Model | AUC-ROC | Accuracy | F1-Score |
|-------|---------|----------|----------|
| **GCN** | **0.9745** | 96.50% | 0.9810 |
| **GIN** | 0.9734 | 95.00% | 0.9730 |
| **GraphSAGE** | 0.8965 | 96.25% | 0.9795 |

### Innovation
- Built **patient-patient similarity graphs** from 1,162 patients
- Trained **5 GNN architectures** (GCN, GraphSAGE, GAT, GIN, APPNP)
- Developed **care recommendation system** identifying preventive care gaps
- Achieved **94% performance with only 30% labeled data**

### Methods & Tech Stack
`PyTorch Geometric` `Graph Neural Networks` `Semi-Supervised Learning` `Collaborative Filtering` `Ablation Studies`

### 📂 [Explore Phase 2 →](./project-2-gnn-prediction/)

---

## 🛠️ Complete Tech Stack

| Category | Technologies |
|----------|-------------|
| **Languages** | Python 3.8+ |
| **Data Processing** | Pandas, NumPy, SQL |
| **Network Analysis** | NetworkX 2.8 |
| **Deep Learning** | PyTorch 1.12, PyTorch Geometric 2.0 |
| **Machine Learning** | scikit-learn |
| **Visualization** | Plotly, Matplotlib, Pyvis |
| **Algorithms** | PageRank, Betweenness Centrality, Louvain, GCN, GraphSAGE, GAT, GIN, APPNP |

---

## 📁 Repository Structure
```
healthcare-network-analysis/
│
├── README.md                          ← You are here
│
├── project-1-network-analysis/        ← Phase 1: Network Analysis
│   ├── README.md
│   ├── Network_Analysis_CODE.ipynb
│   ├── Cancer_Graph.html
│   ├── Diabetes_Graph.html
│   ├── HeartDisease_Graph.html
│   ├── Chronic_Kidney_Disease_Graph.html
│   ├── Multi_Disease_Interactive_Graph.html
│   └── Network_Communities.html
│
└── project-2-gnn-prediction/          ← Phase 2: GNN Prediction
    ├── README.md
    ├── GNN_Multimorbidity_Prediction.ipynb
    └── visualizations/
        ├── ROC_Curves_Model_Comparison.png
        ├── Feature_Ablation_Study.png
        ├── TSNE_Embedding_Visualization.png
        └── ...
```

---

## 🚀 Quick Start

### Clone the Repository
```bash
git clone https://github.com/Mahendra-logics/healthcare-network-analysis.git
cd healthcare-network-analysis
```

### Phase 1: Network Analysis
```bash
cd project-1-network-analysis
pip install pandas numpy networkx plotly pyvis
jupyter notebook Network_Analysis_CODE.ipynb
```

### Phase 2: GNN Prediction
```bash
cd project-2-gnn-prediction
pip install torch torch-geometric networkx scikit-learn pandas numpy
jupyter notebook GNN_Multimorbidity_Prediction.ipynb
```

---

## 📈 Research Impact & Applications

### Healthcare System Optimization
1. **Capacity Planning**: Strategic resource allocation at universal hub facilities
2. **Care Coordination**: Targeted interventions at bridge sites connecting communities
3. **Comorbidity Management**: Integrated care clinics for overlapping disease networks

### Predictive Analytics
1. **Risk Stratification**: Proactive identification of high-risk multimorbidity patients
2. **Care Gap Analysis**: Preventive service recommendations based on peer utilization
3. **Population Health**: Scalable risk assessment for large patient cohorts

### Technical Contributions
1. **Novel Methodology**: Patient-patient similarity network construction from EHR data
2. **Comparative Analysis**: Systematic evaluation of 5 GNN architectures for healthcare
3. **Semi-Supervised Learning**: High accuracy with limited labeled data
4. **Interpretability**: Comprehensive ablation studies revealing feature importance

---

## 🎓 Key Findings Summary

### Phase 1 Insights
- **Hub Infrastructure**: 8 universal sites form the backbone of multi-disease care delivery
- **Disease Patterns**: CKD patients navigate most complex pathways (16.1 avg sites/patient)
- **Community Structure**: Strong modularity (Q=0.67) indicates functional specialization
- **Bridge Sites**: 34 critical connectors vulnerable to bottlenecks

### Phase 2 Insights
- **Model Performance**: GCN achieves 97.45% AUC for multimorbidity prediction
- **Feature Importance**: Behavioral features (network position, care utilization) outperform demographics
- **Data Efficiency**: 30% labeled data sufficient for 94% of maximum performance
- **Network Robustness**: Models maintain 85%+ AUC even with 75% missing edges
- **Clinical Utility**: Care recommendation system identifies specific preventive gaps

---

## 👥 Authors

**Bala Mahendra Pothabathula**  
M.S. Computer Science | University of South Florida  
[LinkedIn](#) | [Email](mailto:pothabathula@usf.edu)

**Collaborators:**  
- Karthikeya Moturi  
- Gowtham Sai Chimmana

*This research was conducted as part of CIS 4930/CAI 5155 (Network Analysis & Machine Learning with Graphs) at the University of South Florida, Department of Computer Science.*

---

## 📜 License

This project is for educational and research purposes. Please cite appropriately if referencing this work.

---

## 🔗 Navigation

- **[Phase 1: Network Analysis](./project-1-network-analysis/)** - Critical infrastructure identification
- **[Phase 2: GNN Prediction](./project-2-gnn-prediction/)** - Deep learning risk prediction

---

## 📧 Contact

For questions, collaborations, or further information about this research:

**Email**: pothabathula@usf.edu  
**LinkedIn**: [linkedin.com/in/bala-mp] 
**GitHub**: [@Mahendra-logics](https://github.com/Mahendra-logics)

---

**⭐ If you find this work useful, please consider starring this repository!**
```

---

## 📝 **How to Add This Main README**

### **Step 1: Go to your main repository**
```
https://github.com/Mahendra-logics/healthcare-network-analysis
```

### **Step 2: Create new README file**
Click **"Add file"** → **"Create new file"**

### **Step 3: Name the file**
In the "Name your file..." box, type:
```
README.md
