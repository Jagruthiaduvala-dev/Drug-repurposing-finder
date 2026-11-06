# AI-Based Drug Discovery & Repurposing Platform

Ranks existing drugs for a disease (and diseases for a drug) using a knowledge graph and a graph neural network, with an evidence trail for every suggestion.

## Results (drugs never seen in training, 5-fold cold-drug test)
| Model | MRR |
|---|---|
| Boosting baseline | 0.203 |
| Graph neural network | 0.227 |
| Blend | 0.253 |
| Blend, 3 seeds averaged (final) | 0.269 |

Final model: true disease in the top 10 of 762 diseases 45.8% of the time, top 50 66.3%, median rank 14.

## Method
1. Load DRKG; remove every direct drug-disease edge and all ATC / drug-class data (no leakage).
2. Build sparse matrices: drug-gene, gene-disease, gene-gene (SciPy, NumPy).
3. Baseline: path counts + look-alike drugs, gradient boosting (scikit-learn).
4. Graph neural network in plain PyTorch (drug built from its genes, SVD gene features).
5. Blend both models and average 3 seeds.
6. Rank all drug-disease pairs and build the dashboard (single HTML file).

## Files
- `notebook.ipynb` - full Kaggle notebook (run top to bottom on a GPU)
- `dashboard.html` - the dashboard (open in any browser)

## How to run
Kaggle: attach the DRKG data, turn on GPU, Save & Run All.

## Data and licences
DRKG (Apache-2.0), Hetionet, MeSH, SIDER, DrugBank (CC BY-NC 4.0). Non-commercial academic project.

## Disclaimer
Research leads only, not medical advice.
