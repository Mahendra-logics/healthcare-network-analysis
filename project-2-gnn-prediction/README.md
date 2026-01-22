# Phase 2: Graph Neural Network Framework for Multimorbidity Risk Stratification

## Executive Summary

This study develops a Graph Neural Network (GNN) framework for predicting multimorbidity risk by modeling Electronic Health Record (EHR) data as patient similarity networks. By representing patients as nodes connected through shared chronic conditions, we trained five state-of-the-art GNN architectures achieving up to 97.45% AUC in binary risk classification. Beyond prediction, we developed a collaborative filtering-based care recommendation system that identifies preventive care gaps by analyzing utilization patterns across clinically similar patient cohorts.

## Research Objectives

### Primary Research Questions

**RQ1: Predictive Value of Graph Structure**  
Can patient-patient similarity networks improve multimorbidity risk prediction compared to baseline demographic and clinical features alone?

**RQ2: Actionable Care Recommendations**  
Can the learned graph structure identify care gaps—specifically, recommending preventive care facilities that high-risk patients should utilize based on similar peers' utilization patterns?

### Hypothesis

Models designed to capture complex graph topology (GIN, GAT) will outperform simpler aggregation methods (GCN) by learning to distinguish subtle structural patterns in patient similarity networks.

## Methodology

### Dataset Construction

**Source**: EHRShot dataset - de-identified hospital network EHR data  
**Population**: 1,162 patients with chronic disease diagnoses  
**Disease Coverage**: Diabetes Mellitus, Cardiovascular Disease, Cancer, Chronic Kidney Disease  
**Data Quality**: Filtered for complete demographics, minimum 1-month follow-up

### Patient Similarity Graph Construction

**Graph Topology**:
- **Nodes**: Individual patients (1,162 nodes)
- **Edges**: Shared chronic condition relationships
- **Edge Criterion**: Minimum 1 shared chronic diagnosis
- **Edge Weights**: Count of shared diagnoses (1-4 scale)

**Node Features** (6 dimensions):
- **Demographics**: Age (continuous), Gender (binary), Race/Ethnicity (categorical)
- **Behavioral**: Degree centrality (network embeddedness), Care site variety (clinical complexity proxy)

**Target Variable**:
- **Class 0 (Low Risk)**: 0-1 chronic conditions (58% of cohort)
- **Class 1 (High Risk)**: ≥2 chronic conditions - clinical multimorbidity threshold (42% of cohort)

**Data Split**: 80% training, 10% validation, 10% test (stratified, fixed seed)

### Graph Neural Network Architectures

We implemented and compared five architectures representing distinct design philosophies:

#### 1. Graph Convolutional Network (GCN)
- **Mechanism**: Spectral graph convolutions with symmetric normalization
- **Architecture**: 2 layers × 64 hidden units, ReLU activation, 0.5 dropout
- **Rationale**: Baseline for homophilic graphs where similar nodes connect

#### 2. GraphSAGE (SAmple and aggreGatE)
- **Mechanism**: Inductive learning via fixed-size neighborhood sampling
- **Architecture**: 2 layers, 25 neighbors/hop, mean aggregation
- **Rationale**: Scalability and generalization to unseen patients

#### 3. Graph Attention Network (GAT)
- **Mechanism**: Multi-head attention for weighted neighbor aggregation
- **Architecture**: 2 layers, 8 attention heads, 64 hidden units
- **Rationale**: Learn importance of different clinical neighbors

#### 4. Graph Isomorphism Network (GIN)
- **Mechanism**: MLP-based aggregation with maximal expressive power
- **Architecture**: 2 layers, 64-unit MLPs per layer
- **Rationale**: Theoretical guarantee of Weisfeiler-Lehman expressiveness

#### 5. APPNP (Approximate Personalized PageRank)
- **Mechanism**: Decoupled feature transformation and graph propagation
- **Architecture**: 2-layer MLP + 10-step PageRank (α=0.1)
- **Rationale**: Prevent over-smoothing while leveraging graph structure

### Training Configuration

**Optimization**: Adam optimizer (lr=0.01, weight decay=5e-4)  
**Loss Function**: Cross-entropy on labeled training nodes  
**Epochs**: 150 (early convergence observed)  
**Hardware**: Google Colab Tesla T4 GPU  
**Framework**: PyTorch Geometric 2.0

### Care Recommendation System

**Logic**: Collaborative filtering on learned patient embeddings

1. **Neighborhood Retrieval**: For high-risk patient, extract k-nearest neighbors in learned embedding space
2. **Utilization Comparison**: Identify care sites frequented by neighbors but not visited by target patient
3. **Gap Scoring**: Rank unvisited sites by frequency among similar peers

**Output**: Top-N care facility recommendations with peer utilization rates

## Results

### Model Performance Comparison

| Model | AUC-ROC | AUPRC | F1-Score | Accuracy | Precision | Recall |
|-------|---------|-------|----------|----------|-----------|--------|
| **GCN** | **0.9745** | **0.9973** | **0.9810** | **0.9650** | 0.9678 | 0.9945 |
| **GIN** | 0.9734 | 0.9971 | 0.9730 | 0.9500 | 0.9525 | 0.9945 |
| **GraphSAGE** | 0.8965 | 0.9827 | **0.9795** | **0.9625** | **0.9703** | 0.9890 |
| **GAT** | 0.9429 | 0.9929 | 0.9602 | 0.9250 | 0.9258 | 0.9890 |
| **APPNP** | 0.9360 | 0.9933 | 0.9589 | 0.9225 | 0.9235 | **0.9972** |

**Key Findings**:
- GCN achieved highest ranking performance (AUC=0.9745), demonstrating spectral convolution effectiveness on homophilic patient networks
- GraphSAGE demonstrated superior precision (0.9703), optimal for clinical deployment where false positives are costly
- APPNP achieved highest recall (0.9972), suitable for screening scenarios minimizing missed high-risk patients

### Ablation Studies

#### Experiment A: Node Feature Contribution
- **Demographics Only**: AUC ≈ 0.91-0.93
- **Behavioral Only**: AUC ≈ 0.92-0.94
- **Full Features**: AUC ≈ 0.93-0.97
- **Conclusion**: Behavioral features (degree centrality, care site variety) are more predictive than demographics alone

#### Experiment B: Edge Weight Impact
- **Binary Edges (unweighted)**: AUC ≈ 0.91-0.98
- **Weighted Edges**: AUC ≈ 0.93-0.99 (+1-2% improvement)
- **Conclusion**: Weighting by shared condition count provides modest but consistent improvement

#### Experiment C: Data Efficiency (Learning Curves)
- **10% training data**: AUC ≈ 0.90-0.97
- **30% training data**: AUC ≈ 0.90-0.97 (94% of maximum)
- **50% training data**: AUC ≈ 0.86-0.97 (plateau reached)
- **Conclusion**: Semi-supervised learning achieves near-optimal performance with 30% labeled data

#### Experiment D: Network Robustness
- **0% edge deletion**: AUC ≈ 0.90-0.98 (baseline)
- **25% edge deletion**: AUC ≈ 0.89-0.97
- **50% edge deletion**: AUC ≈ 0.91-0.97
- **75% edge deletion**: AUC ≈ 0.91-0.97
- **Conclusion**: Graceful degradation demonstrates network redundancy and node feature sufficiency

### Care Recommendation System Validation

**Test Case Example**:
- **Target Patient**: High-risk, visits 3/16 sites used by similar peers
- **Recommendation**: Site #32845 (visited by 310/310 similar neighbors, 100% utilization)
- **Clinical Interpretation**: Likely represents preventive care facility (e.g., ophthalmology for diabetic retinopathy screening)

## Clinical and Operational Implications

### 1. Risk Stratification Deployment
GNN-based risk scores can stratify patient populations for:
- **Proactive outreach**: Target high-risk patients before acute events
- **Resource allocation**: Prioritize care management program enrollment
- **Population health**: Monitor cohort-level risk trends

### 2. Care Gap Identification
Recommendation system identifies:
- **Missed preventive services**: Screenings not completed by high-risk patients
- **Underutilized specialists**: Facilities that peers access but patient does not
- **Care coordination opportunities**: Referrals to complete care pathways

### 3. Scalability Considerations
- **Inductive models (GraphSAGE, GIN)**: Generalize to new patients without retraining
- **Transductive models (GCN, GAT)**: Require periodic retraining but achieve higher accuracy
- **Recommendation tradeoff**: Real-time inference vs. batch prediction based on operational needs

## Technical Implementation

### Environment
- **Python**: 3.8+
- **Deep Learning**: PyTorch 1.12, PyTorch Geometric 2.0
- **Graph Analysis**: NetworkX 2.8
- **ML Utilities**: scikit-learn 1.0, NumPy, Pandas
- **Visualization**: Matplotlib, Plotly

### Code Structure
```
project-2-gnn-prediction/
├── data_preprocessing/      # Patient similarity graph construction
├── models/                  # GNN architecture implementations
├── training/               # Training loops and optimization
├── evaluation/             # Performance metrics and ablation studies
├── recommendation/         # Care site recommendation system
└── notebooks/             # Jupyter notebooks with full pipeline
```

### Reproducibility
All experiments use fixed random seeds (seed=42). Training configuration, hyperparameters, and data splits are version-controlled for full reproducibility.

## Limitations and Future Directions

### Current Limitations
1. **Single healthcare system**: Results may not generalize to different EHR systems or patient populations
2. **Static snapshots**: Current graphs do not model temporal disease progression
3. **Fairness**: Demographic subgroup performance not systematically audited
4. **Causality**: Observational data precludes causal inference

### Future Research Directions

**1. Temporal Graph Neural Networks**
- Model disease progression as dynamic graphs
- Predict risk trajectories rather than static snapshots
- Incorporate visit timestamps for temporal patterns

**2. Heterogeneous Graph Learning**
- Multi-node-type graphs (patients, diagnoses, medications, providers)
- Capture richer EHR relationships beyond patient similarity
- Relation-aware message passing (e.g., R-GCN, HGT)

**3. Transfer Learning**
- Pre-train on large multi-site EHR databases
- Fine-tune for specific hospital systems
- Accelerate deployment in data-scarce settings

**4. Fairness and Interpretability**
- Subgroup performance analysis (age, race, gender)
- Attention visualization for risk prediction explanation
- Counterfactual analysis for model decision transparency

**5. Prospective Clinical Validation**
- Deploy in real clinical workflows
- Measure impact on patient outcomes (readmissions, ER visits)
- A/B testing vs. standard care protocols

## Conclusions

This study demonstrates that Graph Neural Networks effectively leverage patient similarity network structure to predict multimorbidity risk with high accuracy (AUC>0.97). The semi-supervised learning paradigm achieves strong performance with limited labeled data, addressing a key challenge in healthcare ML where labels are expensive. 

The integration of predictive modeling with a care recommendation system bridges the gap between risk assessment and actionable clinical intervention, transforming abstract risk scores into concrete care gap identification. The demonstrated robustness to missing data and graceful performance degradation suggest practical viability for real-world deployment.

GNN-based patient network analysis represents a promising direction for EHR-based prediction, particularly for tasks where relationships between patients or medical entities encode clinically meaningful information. As healthcare systems increasingly prioritize population health management and value-based care, graph-based methods offer a principled framework for modeling complex care delivery ecosystems.

## References

Full methodology, results, and analysis detailed in research report (see `/reports` directory).

## Acknowledgments

Research conducted as part of Machine Learning and Network Analysis coursework at University of South Florida, Department of Computer Science.

## Citation

If you use this work, please cite:
```
Moturi Karthikeya, Pothabathula Bala Mahendra, Chimmana Gowtham Sai (2025). 
A Graph Neural Network Framework for Multimorbidity Risk Stratification 
and Patient-Peer Care Site Recommendation. 
University of South Florida, Department of Computer Science.
```
