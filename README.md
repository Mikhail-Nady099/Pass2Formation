# Pass2Formation: Multi-Receiver, Full-Team Next-Location Forecasting from Short Event Sequences in Soccer Games

## Introduction

Predicting how all players reposition after a pass is critical for tactical analysis in soccer and underpins the mechanics of popular games like “Score! Hero”, yet existing models focus on receiver choice [], pass outcomes [], event likelihoods [], or distributional output [] rather than full next-state forecasting. In this work, we propose a model that predicts all 22 player locations after a candidate pass, especially across real and alternative receiver scenarios, from only five prior events. This work fills the gap between discrete event prediction (Seq2Event) [] and value maps (EPV) [], enabling detailed counterfactual tactical evaluations, essential for coaches, analysts, and simulation-driven game developers.

## Methods

**Dataset:** We trained, validated, and tested our proposed model on the seven France matches available in the. The seven matches were curated into 5,502 sequences of five consecutive pass events. Each pass event has 59 features: x and y coordinates of the 22 players’ locations, ball coordinates (x,y,z), and 12 pass contextual variables (passer id, receiver id, receiver location, pass type, pass outcome, pass pressure, etc.). All Positions were normalized to the pitch dimensions and a unified offense direction.

**Model Design and Training:** Our proposed model was developed as a sequence-to-next-state two-layers LSTM prediction model (128, 64 units), batch normalization, dropout (30%), and a linear output layer. Input is 5×59 feature tensor per sequence, and output is a vector of the next-event (post-pass) x and y positions for all 22 players, not including ball coordinates. We trained with Adam optimizer (lr=0.001), MSE loss masked on alternatives [], batch size 64, early stopping, for up to 100 epochs. We split stratified by sequence into 80% train, 10% validation, 10% test sets.

## Results

Figure 1 shows examples of the different scenarios our model can predict for the same players locations but with different passing decisions. Quantitively, on the held-out test set, our model achieved MAE of 6.4m, RMSE of 9.5m, and R²=0.74 for next-state players positions. This positional accuracy compares favorably to multi-agent trajectory imputation models (≈6–7m MAE) trained on far more data [;). Unlike earlier approaches predicting only ball outcomes [], discrete events [], pass values [], or single-receiver choices [], our model simulates the entire post-pass team configuration for every plausible receiver, supporting granular scenario ranking and interpretation. Figure 2 shows the prediction error across different players and when tested on different team other than the team it was trained on.

## Conclusion

Pass2Formation is the first practical, identity-anchored pipeline to forecast full next-state spatial configurations and systematically generate multi-receiver counterfactuals from open-play contexts. Its compact architecture and strong positional accuracy make it immediately deployable for team-shape analysis, tactical decision support, and what-if scenario ranking—bridging the gap between value-only models and heavyweight simulators and benefitting both the professional analytics community and game/simulators developers.

![Figure 1](Figure%201.jpg)  
*Figure 1. Example of counterfactual tactical scenarios evaluations using the proposed model. The upper row shows the five steps, i.e. prior events, of an arbitrary sequence from the testing sequences. The lower row shows players positions directly after the next event/pass. The actual pass that occurred in the game is on the most left side, followed by four predictions for four different passes.*

![Figure 2](Figure%202.jpg)  
*Figure 2. Model prediction error per player when testing on the players of team France (to the left), and when testing on the player of a different team (to the right). The prediction error changes significantly within the different players’ (mostly based on the player tactical positions). Moreover, being trained on the seven games of France, the model exhibits lower error for the French team compared to the other team (Overall MAE 6.4m vs. 16.94m).*
