# Pass2Formation: Multi-Receiver, Full-Team Next-Location Forecasting from Short Event Sequences in Soccer Games

## Overview

This repository contains the code and resources for the research paper titled **"Pass2Formation: Multi-Receiver, Full-Team Next-Location Forecasting from Short Event Sequences in Soccer Games"** , submitted to the MIT Sloan Sports Analytics Conference (SSAC). The paper introduces a novel lightweight LSTM-based model that predicts the post-pass locations of all 22 players on the soccer pitch using only four prior events. This enables tactical analysis, counterfactual scenario evaluation (e.g., "what-if" different receivers), and integration into soccer simulation systems like video games.

The model is trained on the PFF FC's 2022 World Cup dataset, with a baseline model trained on general matches and fine-tuned versions for specific teams (Argentina, Croatia, England, France, Morocco) to capture team-specific tactics. Key contributions include:
- Accurate prediction of full-team formations (MAE around ~5.8 m ).
- Support for multi-receiver counterfactuals.
- Detailed analysis of prediction errors across player roles, pass features, game dynamics, and pitch locations.

The repository includes Jupyter notebooks for model training, fine-tuning, evaluation, and result generation, along with figures from the paper.

For the full details, see the paper PDF in the root directory: (`Pass2Formation MITSloanFullPaper.pdf`).

## Repository Structure

The repo is organized into folders for different phases of the project:

1. **Abstract_1st_phase**: Contains codes and results from the initial abstract submission phase (1st phase of the conference process).
   
2. **Baseline_Model**: Jupyter notebook (`Pass2Formation_LSTM_Baseline_Model.ipynb`) for training and evaluating the generic baseline model .

3. **Argentina_Model**: Jupyter notebook (`Pass2Formation_LSTM_Baseline_Model_Fine_Tunned_on_Argentina.ipynb`) for fine-tuning the baseline model on Argentina's data and evaluating it on other datasets (cross-team evaluation).

4. **Croatia_Model**: Similar to Argentina_Model, but for Croatia (`Pass2Formation_LSTM_Baseline_Model_Fine_Tunned_on_Croatia.ipynb`).

5. **England_Model**: Similar, for England (`Pass2Formation_LSTM_Baseline_Model_Fine_Tunned_on_England.ipynb`).

6. **France_Model**: Similar, for France (`Pass2Formation_LSTM_Baseline_Model_Fine_Tunned_on_France.ipynb`).

7. **Morocco_Model**: Similar, for Morocco (`Pass2Formation_LSTM_Baseline_Model_Fine_Tunned_on_Morocco.ipynb`).

8. **Pass2Formation_Results**: Jupyter notebooks for analyzing results and generating figures/tables from the paper. Includes codes for MAE calculations, R² metrics, heatmaps, correlations (e.g., vs. player dispersion/movement), and visualizations across teams, periods, pass features, etc.

9. **Results_Figures**: Contains all figures generated from the analysis codes. Figures are named by their numbers in the paper (e.g., `Figure1.png` for the data processing workflow, `Figure2.png` for MAE results, etc.).

10. **Pass2Formation MITSloanFullPaper.pdf**: The full PDF of the submitted paper.

## Requirements

To run the code:
- Python 3.8+
- Libraries: 
  - TensorFlow/Keras (for LSTM model)
  - Pandas, NumPy (for data processing)
  - Matplotlib/Seaborn (for visualizations)
  - Scikit-learn (for metrics like MAE and R²)

Install dependencies via:
```
pip install tensorflow pandas numpy matplotlib seaborn scikit-learn
```

The dataset used is the publicly available PFF FC 2022 World Cup dataset (JSON event files). Download it from the official source and place it in a `data/` folder (not included in this repo due to size). The code assumes a relational database setup (e.g., via SQL) for efficient querying, as described in Section 2.1 of the paper. 

The processed data that we used is uploaded in our Google Drive folder and is publicly shared (view-only): [FIFA 2022 Data](https://drive.google.com/drive/folders/1QmnNRFq8CGiphT8okvOTOK8zBPUM4kFJ).

Additionally, the processed data for the first model version submitted in the abstract 1st phase is available here: [Abstract Phase Data](https://drive.google.com/drive/folders/1H8gdohJ2YYnpLNmVtPIgYbxe5_ZjbBot).


## How to Use

1. **Setup Dataset**:
   - Organize the JSON event files into a relational database with tables for possession events, player locations, ball locations, and metadata (as per Section 2.1).
   - Normalize positions to pitch dimensions and unify offense direction.
   
   - You can run the code on Google Colab. The data input paths in the code point to the shared Drive folder [FIFA 2022 Data](https://drive.google.com/drive/folders/1QmnNRFq8CGiphT8okvOTOK8zBPUM4kFJ), so you can access it directly if you mount your Drive, or download the files to your own Drive/local setup. Change output paths in the code to your preferred location.
2. **Run Baseline Model**:
   - Open `Baseline_Model/Pass2Formation_LSTM_Baseline_Model.ipynb`.
   - Load Group B data (non-reserved teams).
   - Train the model (LSTM with 5-event sequences).
   - Evaluate MAE on test sets.

3. **Fine-Tune Team-Specific Models**:
   - For each team (e.g., Argentina), open the corresponding notebook (e.g., `Argentina_Model/argentina_model.ipynb`).
   - Load team-specific data from Group A.
   - Fine-tune the baseline weights with reduced learning rate.
   - Perform within-team and cross-team evaluations.

4. **Generate Results and Figures**:
   - Open notebooks in `Pass2Formation_Results/`.
   - Run analyses for MAE/R² across factors (e.g., player positions, pass types, periods).
   - Outputs will save figures to `Results_Figures/` (named by paper figure numbers).

5. **Reproduce Paper Figures**:
   - Figures are pre-generated in `Results_Figures/`, but you can regenerate them via the results notebooks.

Note: All models use Adam optimizer, MSE loss (masked), batch size 64, and early stopping. Hyperparameters are detailed in Section 2.2.

## Authors and Contributors

- Authors: [ Mikhail Daoud ] [ Tamer Bashsa ].

For questions or collaborations, contact [ m.daoud@eng.cu.edu.eg  , tamer.bashsa@eng1.cu.edu.eg ] or open an issue.

## Citation

If you use this code or paper, please cite:

```
@article{pass2formation2025,
  title = {Pass2Formation: Multi-Receiver, Full-Team Next-Location Forecasting from Short Event Sequences in Soccer Games},
  author = {[ Mikhail Daoud , Tamer Basha ]},
  journal = {MIT Sloan Sports Analytics Conference},
  year = {2026},
  note = {Paper ID: 163}
}
```

## License

This project is licensed under the MIT License . The code is provided for educational and research purposes. The 2022 World Cup dataset is subject to its own licensing terms from PFF FC.
