# Phase 2: Graph Neural Network Framework for Multimorbidity Risk Prediction

Using patient similarity networks and deep learning to predict multimorbidity risk and identify preventive care gaps.

---

## 🎯 Overview

This project develops a **Graph Neural Network (GNN) framework** for predicting multimorbidity risk by modeling Electronic Health Record (EHR) data as patient similarity networks. By representing patients as nodes connected through shared chronic conditions, we trained **5 state-of-the-art GNN architectures** achieving up to **97.45% AUC** in binary risk classification.

Beyond prediction, we developed a **collaborative filtering-based care recommendation system** that identifies preventive care gaps by analyzing utilization patterns across clinically similar patient cohorts.

### Dataset
- **1,162 patients** with chronic disease diagnoses
- **Disease Coverage**: Diabetes Mellitus, Cardiovascular Disease, Cancer, Chronic Kidney Disease
- **Target**: Binary classification (Low Risk: 0-1 conditions | High Risk: ≥2 conditions)

---

## 🔬 Research Questions

**RQ1: Predictive Value of Graph Structure**  
Can patient-patient similarity networks improve multimorbidity risk prediction compared to baseline demographic features?

**RQ2: Actionable Care Recommendations**  
Can the learned graph structure identify care gaps—specifically, recommending preventive care facilities based on similar peers' utilization patterns?

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| **Language** | Python 3.8+ |
| **Deep Learning** | PyTorch 1.12, PyTorch Geometric 2.0 |
| **Graph Analysis** | NetworkX 2.8 |
| **Machine Learning** | scikit-learn, NumPy, Pandas |
| **Visualization** | Matplotlib, Plotly |
| **Models** | GCN, GraphSAGE, GAT, GIN, APPNP |

---

## 📊 Key Results

### Model Performance Comparison

| Model | AUC-ROC | Accuracy | F1-Score | Precision | Recall |
|-------|---------|----------|----------|-----------|--------|
| **GCN** | **0.9745** | **96.50%** | **0.9810** | 0.9678 | 0.9945 |
| **GIN** | 0.9734 | 95.00% | 0.9730 | 0.9525 | 0.9945 |
| **GraphSAGE** | 0.8965 | 96.25% | 0.9795 | **0.9703** | 0.9890 |
| **GAT** | 0.9429 | 92.50% | 0.9602 | 0.9258 | 0.9890 |
| **APPNP** | 0.9360 | 92.25% | 0.9589 | 0.9235 | **0.9972** |

**Key Insight**: GCN achieved highest overall performance, demonstrating that spectral convolution is highly effective for homophilic patient networks.

### Ablation Study Findings

#### Feature Contribution
- **Demographics Only**: AUC ≈ 0.91-0.93
- **Behavioral Features Only**: AUC ≈ 0.92-0.94
- **Full Features (Combined)**: AUC ≈ 0.93-0.97
- **Conclusion**: Behavioral features (degree centrality, care site variety) are more predictive than demographics alone

#### Data Efficiency
- **30% training data**: Achieved **94% of maximum performance**
- **Conclusion**: Semi-supervised learning is highly efficient for healthcare applications with limited labeled data

#### Network Robustness
- **75% edge deletion**: Models maintain **AUC > 0.85**
- **Conclusion**: Graceful degradation demonstrates network redundancy

### Care Recommendation System
- **Logic**: Collaborative filtering on learned patient embeddings
- **Output**: Identifies preventive care facilities visited by similar high-risk patients but not by target patient
- **Example**: Recommends ophthalmology visits for diabetic patients based on peer utilization patterns

---

## 📁 Project Structure
```
project-2-gnn-prediction/
├── README.md                                    # This file
├── GNN_Multimorbidity_Prediction.ipynb          # Main analysis notebook
└── visualizations/
    ├── ROC_Curves_Model_Comparison.png
    ├── Feature_Ablation_Study.png
    ├── Edge_Weight_Ablation.png
    ├── Data_Efficiency_Learning_Curves.png
    ├── Network_Robustness_Analysis.png
    ├── Care_Recommendation_System.png
    ├── Patient_Similarity_Network.png
    └── TSNE_Embedding_Visualization.png
```

---

## 🚀 How to Run

### 1. Clone the repository
```bash
git clone https://github.com/Mahendra-logics/healthcare-network-analysis.git
cd healthcare-network-analysis/project-2-gnn-prediction
```

### 2. Install dependencies
```bash
pip install torch torch-geometric networkx scikit-learn pandas numpy matplotlib plotly
```

### 3. Open the Jupyter notebook
```bash
jupyter notebook GNN_Multimorbidity_Prediction.ipynb
```

### 4. View visualizations
All model performance charts and ablation study results are saved in the `visualizations/` folder.

---

## 🧠 Methodology

### Graph Construction
- **Nodes**: Individual patients (1,162 nodes)
- **Edges**: Shared chronic condition relationships (minimum 1 shared diagnosis)
- **Edge Weights**: Count of shared diagnoses (1-4 scale)
- **Node Features**: Demographics (age, gender, race) + Behavioral (degree centrality, care site variety)

### GNN Architectures

**1. Graph Convolutional Network (GCN)**
- Spectral graph convolutions with symmetric normalization
- Best for homophilic graphs where similar nodes connect

**2. GraphSAGE (SAmple and aggreGatE)**
- Inductive learning via fixed-size neighborhood sampling
- Generalizes to new unseen patients

**3. Graph Attention Network (GAT)**
- Multi-head attention for weighted neighbor aggregation
- Learns importance of different clinical neighbors

**4. Graph Isomorphism Network (GIN)**
- MLP-based aggregation with maximal expressive power
- Theoretical guarantee of distinguishing graph structures

**5. APPNP (Approximate Personalized PageRank)**
- Decoupled feature transformation and graph propagation
- Prevents over-smoothing in deep architectures

### Training Configuration
- **Optimizer**: Adam (learning rate=0.01, weight decay=5e-4)
- **Loss**: Cross-entropy on labeled training nodes
- **Epochs**: 150 (early convergence observed)
- **Data Split**: 80% train, 10% validation, 10% test (stratified)
- **Hardware**: Google Colab Tesla T4 GPU

---

## 📈 Clinical Applications

### 1. Risk Stratification
- **Proactive outreach**: Target high-risk patients before acute events
- **Resource allocation**: Prioritize care management program enrollment
- **Population health**: Monitor cohort-level risk trends

### 2. Care Gap Identification
- **Missed preventive services**: Screenings not completed by high-risk patients
- **Underutilized specialists**: Facilities that peers access but patient does not
- **Care coordination**: Complete referrals to optimize care pathways

### 3. Scalability
- **Inductive models (GraphSAGE, GIN)**: Generalize to new patients without retraining
- **Real-time inference**: Deploy for production risk assessment

---

## 🎨 Visualizations

The `visualizations/` folder contains:
- **ROC Curves**: Comparative performance across all 5 models
- **Ablation Studies**: Feature contribution, edge weights, data efficiency, robustness
- **t-SNE Embeddings**: 2D projection showing risk class separation
- **Care Recommendation**: Visual explanation of collaborative filtering logic
- **Patient Networks**: Example similarity graphs with weighted edges

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

This project builds upon **Phase 1**, which analyzed patient care pathways using network science to identify critical healthcare infrastructure.

📂 [View Phase 1: Network Analysis →](../project-1-network-analysis/)

---

## 🔮 Future Directions

- **Temporal Graph Neural Networks**: Model disease progression as dynamic graphs
- **Heterogeneous Graphs**: Multi-node-type graphs (patients, diagnoses, medications, providers)
- **Transfer Learning**: Pre-train on large multi-site EHR databases
- **Fairness Auditing**: Subgroup performance analysis across demographics
- **Prospective Validation**: Deploy in real clinical workflows

---

## 📜 License

This project is for educational purposes. Please cite appropriately if referencing this work.

---

## 🔗 Links

- [Main Repository](../)
- [Phase 1: Network Analysis](../project-1-network-analysis/)
- [Full Research Report](../reports/)
