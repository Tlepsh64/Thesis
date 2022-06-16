# Thesis

# Introduction
Here you can find the results of the experiments I made for my thesis, which is about energy demand forecasting under a federated learning setting.

Until now, I have experimented with:

  - Centralized Forecasting
  - Vanilla FedAVG
  - FedAVG with Hierarchical Clustering
  - IFCA


The dataset I used is energy demand measurement data of households located in London. For centralized learning setting, I have added the corresponding weather data and some datetime features for all the households. This is due to the fact that my HPC credits are getting too low for doing the same with federated learning experiments. 

Since I am running a single-machine simulation, the FL rounds are executed serially in the clients, thus the RAM usage goes out of the roof(hence I lose too much HPC credits with every FL experiment). Parallelizing the local trainings will get rid of this issue, but I don't know how to do it yet.

I still need to refine the experiments with more clever features, in addition to removing trend&seasonality from the data. The energy usage is really violent for some houses and inter-household variance seems to be quite high as well. Thus, counting on weather & energy data & datetime features are not sufficient to reduce the MSE values. In all experiment settings, the R2 value is negative which means the model is struggling a lot to capture the variance in the data.

# Technicalities

## Epochs
For all the FL settings, I tried 5, 20 and 30 epochs with early stopping(patience was 3). 
For the centralized setting, I set the max number of epochs to 200 and patience to 20. Nevertheless the training stabilizes around 30-40 epoch band and it never continued further than 70 epochs.

## FL Rounds & Client Size
To save from computation, I set the max number of rounds to 25 for all the FL experiments. The client number was 50 for both FL and CL. They were randomly selected from the dataset. I used all the clients at every round.

## Sample Size
For forecasting, I selected the data from 1 January to 2 July. This period corresponds to half of the maximum observations available(8760/2).

## LSTM Model
2 layers with 32 and 16 units each. Every layer had a dropout value of 0.1, and the learning rate was 0.002. Adam optimizer was used, and the loss function was MSE.

## Time Windows & Batch Size
The model uses past 12 observations to forecast the 13th one. The train batch size was 512 and test had a batch size of 1.

## Evaluation Metrics
I used three metrics; MSE, MAPE and R2. MAPE error is too high but that is due to some instability in its calculation, ie sometimes denominator gets too small of a value and mean absolute percentage error gets much bigger than it should be. MSE seems to be small with every experimental setting, but if you consider the energy demand values which themselves are also small(generally between 0 and 1 kwh), the MSE metric I'm getting is not good. R2 values prove this fact unfortunately.

## CFL Hyperparams
The hyperparameters about the Clustered FL algorithms will be added shortly. 

