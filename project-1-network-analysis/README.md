# Phase 1: Network Analysis of Healthcare Delivery Systems

## Executive Summary

This study applies computational network analysis to Electronic Health Records (EHR) data to identify critical infrastructure components in multi-disease healthcare delivery. Using graph-theoretic methods on 262,833 patient care transitions across 120 healthcare facilities, we quantified facility importance, detected care coordination bottlenecks, and revealed modular organizational structures.

## Research Objectives

1. **Hub Identification**: Quantify facility centrality using PageRank and betweenness metrics to identify universal coordination sites serving multiple chronic disease populations
2. **Care Pathway Analysis**: Characterize disease-specific patient journey patterns through visit frequency, pathway complexity, and care continuity metrics
3. **Community Detection**: Apply Louvain modularity optimization to uncover functional clustering and bridge sites connecting care subsystems

## Methodology

### Data Source
- **Dataset**: De-identified EHR data from hospital network
- **Population**: 1,017 patients with chronic conditions (Diabetes Mellitus, Cardiovascular Disease, Cancer, Chronic Kidney Disease)
- **Observation Period**: Multi-year longitudinal records
- **Care Transitions**: 262,833 documented patient visits across 120 distinct care facilities

### Network Construction
- **Nodes**: Healthcare facilities (care sites)
- **Edges**: Directed patient transitions between facilities
- **Edge Weights**: Frequency of patient transfers between site pairs
- **Temporal Window**: 365-day active care episode tracking

### Analytical Methods
- **PageRank Centrality**: Recursive importance scoring via referral patterns
- **Betweenness Centrality**: Bridge facility identification through shortest-path analysis
- **Louvain Algorithm**: Community detection via modularity optimization (Q=0.67)
- **Pathway Metrics**: Visit frequency, site diversity, inter-visit intervals

## Key Findings

### Universal Hub Infrastructure
- **8 universal hub sites** identified serving all four disease populations
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
- **23 functional communities** detected via Louvain algorithm
- **Modularity score Q = 0.67** indicating strong community organization
- **34 bridge sites** identified with high betweenness centrality (μ=0.082)
- Top bridges: Internal Medicine, Laboratory Services, Cardiology

## Clinical Implications

1. **Capacity Planning**: Universal hubs represent critical bottlenecks requiring strategic resource allocation
2. **Care Coordination**: Bridge sites are optimal intervention points for care navigator programs
3. **Comorbidity Management**: Network overlap between cardiac and renal communities suggests integrated care clinic opportunities

## Technical Implementation

### Technologies
- **Python 3.8+**: Primary programming environment
- **NetworkX 2.8**: Graph construction and analysis
- **Pandas**: Data preprocessing and manipulation
- **Plotly**: Interactive network visualizations
- **NumPy/SciPy**: Numerical computations

### Reproducibility
All analysis code is documented in Jupyter notebooks with inline explanations. Network visualizations are provided as standalone HTML files for interactive exploration.

## Outputs

- `Network_Analysis_CODE.ipynb`: Complete analysis pipeline with documentation
- Disease-specific network visualizations (HTML interactive graphs):
  - `Cancer_Graph.html`
  - `Chronic_Kidney_Disease_Graph.html`
  - `Diabetes_Graph.html`
  - `HeartDisease_Graph.html`
- `Multi_Disease_Interactive_Graph.html`: Integrated 120-site network with disease coverage overlay
- `Network_Communities.html`: Community structure visualization with bridge identification

## References

Full methodology and results documented in research report (see `/reports` directory).

## Author

Conducted as part of Network Analysis and Machine Learning coursework at University of South Florida, Department of Computer Science.
```
