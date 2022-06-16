# Thesis
Here you can find the results of the experiments I made for my thesis, which is about energy demand forecasting under a federated learning setting.

Until now, I experimented with:

  - Centralized Forecasting
  - Vanilla FedAVG
  - FedAVG with Hierarchical Clustering
  - IFCA

I still need to refine the experiments above with more clever features, in addition to removing trend&seasonality from the data.

The dataset I used is energy demand measurement data of households located in London. For centralized learning setting, I have added the corresponding weather data for all the households. This is due to the fact that my HPC credits are getting too low for doing the same with federated learning experiments.

