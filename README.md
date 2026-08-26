# Soil_habitability_scoring4

Can dirt from space grow plants? This project builds a machine learning pipeline to score the plant-growth suitability of soil and regolith (Earth, Moon, Mars) from chemical composition data alone.

Growing food in space is a real problem for long-term missions. Before spending months physically growing plants in a soil sample, it would be useful to quickly screen a soil's chemistry and estimate whether plants could survive in it at all.

<img width="1161" height="222" alt="image" src="https://github.com/user-attachments/assets/3193c9ea-4a82-482c-ab6b-52a5c5d79126" />

## Results

The model correctly ranked all 3 real soils — matching the actual experimental outcomes from Wamelink et al. (2014):

Soil	Model score	Real avg biomass	Real ranking
Mars simulant	0.848	131 mg	1st, Earth soil	0.396	62 mg	2nd, Moon simulant	0.188	36 mg	3rd

Model accuracy on held-out synthetic test set:

R² = 0.9997
MAE = 0.0034 (on a 0–1 scale)

## data sources
### Primary dataset:
Wamelink et al. (2014). Can Plants Grow on Mars and the Moon: A Growth Experiment on Mars and Moon Soil Simulants.
PLOS ONE. https://doi.org/10.1371/journal.pone.0103138
(open access — free to use)

soil_composition.csv — Table 2 from this paper (real measured chemistry for Earth, Moon, Mars simulants)
pone_0103138_s002.xlsx — Supplementary Table S2 (840-pot per-plant biomass and germination results, the ground truth)

Supporting literature reviewed:

Caporale et al. (2020, 2022) — independent replication using MMS-1/LHS-1 simulants confirming Mars simulant outperforms Lunar simulant for plant growth
Paul et al. (2022) — perchlorate toxicity in real Mars regolith

## How to run
### 1. clone the repo
git clone https://github.com/skan06-md/Soil_habitability_scoring
cd Soil_habitability_scoring

### 2. install dependencies
pip install pandas numpy matplotlib scikit-learn xgboost openpyxl jupyter

### 3. run the notebooks in order
jupyter notebook

## Limitations
There are some important limitations to our model. Knowing these limitations makes our project more honest and credible.

Perchlorate was not included: Real Mars soil contains a toxic chemical called perchlorate. The Mars soil used in the study did not include it, so our model may make Mars soil look more suitable for plants than it really is.
Phosphorus was not used: All the soil samples had very little phosphorus. Since there was not enough difference between the soils, we kept the information for transparency but did not use phosphorus in the model.
Nitrogen and potassium limits are estimates: We could not find exact limits for nitrogen and potassium for this type of soil. The values we used are reasonable estimates, but they have not been officially validated.
Only three soils were tested: We tested the model using Earth, Moon, and Mars soils. Getting all three correct is encouraging, but three examples are not enough to prove that the model will always work.
The model follows the rubric: Our model is designed to follow the scoring rubric. This means it can score new soil samples, but it cannot consider factors that are not included in the rubric.
Water retention was not included: Moon soil does not hold water very well, which can affect plant growth. However, the original data did not include water-retention measurements, so we could not include this factor in our model.

Honest Scope of the Model

Our model predicts how suitable different volcanic-rock-based soil simulants are for plant growth. It uses factors such as pH, nitrogen, and potassium.

However, it does not predict exactly what would happen to plants on the real surface of Mars or the Moon, because real regolith contains other factors that are not included in our model.

Possible Next Steps
Add perchlorate: Include perchlorate as a factor because it can be toxic to plants.
Test more soils: Use more soil samples to make the model more reliable.
Create a web interface: Build a simple website where users can enter soil values and get a score immediately.
Test with more experiments: Compare the model's results with results from other independent plant-growth experiments.
