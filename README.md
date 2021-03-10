# CMPE_258 : Assignment 2

Below details covers the list of different things explored in addition to mandatory requirements of assignment.

## PART 1

### Image Dataset:
New Image Dataset has been downloaded from Kaggle. This dataset comprises images of cats and dogs. AutoML has been executed on this dataset to get accurate results.

### Text Dataset
Based on current trends, dataset on discussion about COVID has been downloaded for models Text Classification Single Label and Sentiment Analysis.

### Video Dataset
Data split ratio for Training, Validation and Test has been explored with different values to know it's impact on the model output. Custom jar with pre-built cotainer has been tried instead of AutoML, however got stuck with an error.

### Custom Training
Model frameworks like scikit-learn and PyTorch has been evaluated instead of default Tensorflow model.

### Tabular Dataset
New dataset has been downloaded from Kaggle to evaluate this. Also, RMSLE error has been instead of RMSE. Chronological assignment was chosen in data split, since we want to control splitting the data.


## PART 2

### Automl vision and timeseries forecasting models

List of changes tried for different models are as follows:
* LSTM : 1) Changed the model to SGD and ADADELTA and explored the results. 2) CNN and stacked LSTM are tried to evaluate the working approach of the model.
* ARIMA : The core parameters i,e p,d and q are tweaked with different values to know it’s impact on the model output.
* SARIMAX : Number of seasons under seasonal_order values was changed.
* CNN: Optimizer, filter and kernel_size are tried with different values.
* Ensemble ML and Statistical models: Replacement of weights

### E2E deployment of vision model to mobile device
