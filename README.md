# CMPE_258 : Assignment 2

Below details covers the list of different things explored in addition to mandatory requirements of assignment.

## Part 1

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


## Part 2

### Automl vision and timeseries forecasting models
* For LSTM model, changed the model to SGD and adadelta and explored the results.
* Also, CNN and stacked LSTM are tried to evaluate the working approach of the model.
* The core parameters of ARIMA model i.e p,d and q are tweaked with different values to know it’s impact on the model output.
* Number of seasons under seasonal_order values was changed.
* Optimizer, filter and kernel_size for CNN model are changed with different values.
* Replacing weights for Ensemble ML and Statistical models.

### E2E deployment of vision model to mobile device




If we run the example, we get the following output:
```
We found errors in the data:

CompletenessConstraint(Completeness(productName)): Value: 0.8 does not meet the requirement!
PatternConstraint(containsURL(description)): Value: 0.4 does not meet the requirement!
```
The test found that our assumptions are violated! Only 4 out of 5 (80%) of the values of the `productName` attribute are non-null and only 2 out of 5 (40%) values of the `description` attribute contained a url. Fortunately, we ran a test and found the errors, somebody should immediately fix the data :)

## More examples

Our library contains much more functionaliy than what we showed in the basic example. We are in the process of adding [more examples](src/main/scala/com/amazon/deequ/examples/) for its advanced features. So far, we showcase the following functionality:

 * [Persistence and querying of computed metrics of the data with a MetricsRepository](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/metrics_repository_example.md)
 * [Data profiling](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/data_profiling_example.md) of large data sets
 * [Anomaly detection](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/anomaly_detection_example.md) on data quality metrics over time
 * [Automatic suggestion of constraints](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/constraint_suggestion_example.md) for large datasets
 * [Incremental metrics computation on growing data and metric updates on partitioned data](https://github.com/awslabs/deequ/blob/master/src/main/scala/com/amazon/deequ/examples/algebraic_states_example.md) (advanced)
