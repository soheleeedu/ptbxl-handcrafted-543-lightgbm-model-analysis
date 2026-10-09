# PTB-XL handcrafted-feature ECG classification (CPU-only)

Code and results for *Interpretable by construction: a CPU-only gradient-boosting pipeline with 543 handcrafted 12-lead ECG features for single- and multi-label classification on PTB-XL* (Miah, Hossain, Islam).

| Path | Purpose |
|---|---|
| `PTBXL_feature_extraction.ipynb` | Feature extraction. PTB-XL WFDB records to `ECG_MODEL_ready_FINAL_with_StratFold.csv` (543 features + ids + strat_fold + label columns). |
| `PTBXL_revision_experiments.ipynb` | All modelling and evaluation. 10-fold patient-level LightGBM, label-permutation and leave-out leakage tests, calibration (ECE), multi-label replication with Fmax and bootstrap CIs, SHAP with 10-fold rank stability, unambiguous-subset robustness, no-HRV and six-family ablations, per-fold SDs, figures. Checkpointed, resumable on Colab. |
| `Figure6_SHAP_only.ipynb` | Regenerates Figure 6 (SHAP, fold-10 model) only. |
| `results/analysis_state.json` | Every number reported in the paper, as produced by the experiments notebook (final run, 2026-10-09). |
| `results/feature_cols.csv` | The 543 feature names in matrix order. |
| `results/feature_family_map.csv` | Exact feature-to-family assignment used for Table 2 and the family ablation (Table 6, Supplementary Table S8). |
| `figures/` | Figures 1-10 and S1 as used in the manuscript. |
| `requirements.txt` | Pinned Python packages. |

## Reproduce
1. Download PTB-XL v1.0.3 from PhysioNet (`records500/`, `ptbxl_database.csv`, `scp_statements.csv`).
   Link: https://physionet.org/content/ptb-xl/1.0.3/records100/#files-panel
3. Open `PTBXL_feature_extraction.ipynb`, set the paths in the CONFIG cell, run all (about 2 h on a 2-core CPU).
4. Open `PTBXL_revision_experiments.ipynb`. It auto-detects the feature file, drops the seven label-derived columns, and runs every experiment with checkpoints in `_analysis_checkpoints/` (about 3 h in total on a 2-core CPU, resumable).

Fixed settings: LightGBM learning rate 0.05, up to 800 rounds, 63 leaves, min 40 samples per leaf, row subsample 0.9, column subsample 0.7, L2 5.0, seed 42, balanced class weights, early stopping patience 50 on the validation fold (fold 9, or fold 8 when the test fold is 9).

## Data
PTB-XL is distributed by PhysioNet under the Creative Commons Attribution 4.0 licence and is not redistributed here. No patient data are included in this repository.

## Licence
MIT (see `LICENSE`).
## File 
https://drive.google.com/file/d/1i7CIfcAu6rptyqFXxLtLRjRmFENj6QIw/view?usp=drive_link
