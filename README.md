# Time_Series_Darts

### Environment Setup

###### Python Version ---> 3.7.11

###### Environment Yaml Files ---> The yaml file for environment can be found [here](https://github.com/Ashwinikumar1/Time_Series_Darts/tree/main/environment_variables)

### Methodology 

We are provided 4 Timeseries i.e. ["req_ThunB2B_AA", "req_ThunB2B_PP", "req_ThunB2B_Sorter", "req_ThunB2C"] and for all of them we are also provided Benchmark Forcasts from the client i.e. ["BOL_B2B AA Thun", "BOL_B2B P&P Thun", 
"BOL_B2B Sorter Thun", "BOL_B2C Thun"]. The objective of this project are as follows:

1. Try multiple DARTS model to find out which model beats the benchmark Model. Mean Absolute Error (MAE) is used to evaluate the model. Data Before '2021-01-04’  is used as training data and after this as test data
2. For the best models for each time Series Hyperparameter Tune the best model to see if it beats the becnhmark. 
3. Create Useful pipeline so it can be replicated across datasets

### Objective 1 : Trial Out different models to see which model works best. 
The code used for this excercise can be found [here](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Codes/All_Model_Trial.ipynb). We do two trials first on Raw Time Series Data and second on Filtered Time Series. Filtered Time Series Gives better results. 

##### Why Filter Time Series
Our Data is very noisy with sudden Peaks and Troughs. This type of time series is very difficult to handle by any forcasting models. Filtering helped us to control 
these peaks while keeping the data as it is. Thus model performs better. The plot of Noisy Time Series v/s Filtered timeseries for Req_thun_B2B_Sorter can be found below, it clearly shows that filtering helps to control peaks

![image](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Insights/filtered_data.PNG)

## Summary Objective 1 : Best model summary of all variables

Summary of all best performing models based on MAE & model learning from data is as follows :

| Variable Name |model |	loss_benchmark|	loss_model|Plot Models Prediction |
|------|------| ------- | -------| ------ |
| Sum of all variables(Total Thun) |Prophet	| 51986 |	47985 | ![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Sum_All_Variablesfiltered/Prophet.png)|
| req_ThunB2B_AA |Theta(2)|	23509.7	|16320.1| ![Theta Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/Theta.png)|
| req_ThunB2B_PP |NBEATSModel |	11758.0	 |11494.8 | ![N beats Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered/NBEATSModel.png) |
| req_ThunB2B_Sorter |Prophet|	33980.2	|38167.9 |![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_Sorterfiltered/Prophet.png) |
| req_ThunB2C |Auto-ARIMA	| 4775 |	5456 | ![Arima Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2Cfiltered/AutoARIMA.png)|

### Detailed Analysis for each Variable

##### 1. Sum of all variables(Total Thun): Prophet Model beats the benchmark model by a margin of 4k. All other models perform worse than the benchmark model

|model |	loss_benchmark|	loss_model|Plot Models Prediction |
|------| ------- | -------| ------ |
|Prophet	| 51986 |	47985 | ![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Sum_All_Variablesfiltered/Prophet.png)|
|TCN Model |	51986 |	63071 |![TCN Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Sum_All_Variablesfiltered/TCNModel.png) |
|N Beats Model |	51986 |	73559 |![N Beats Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Sum_All_Variablesfiltered/NBEATSModel.png) |

Complete output for this trial can be found at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Sum_All_Variablesfiltered)

##### 2. req_ThunB2B_AA : Multiple Models are able to beat the benchmark model with comfortable margin. The list of models are as follows :

|model| loss_benchmark |	loss_model | Plot Models Prediction |
|------| ------- | -------| ------ |
|Theta(2)|	23509.7	|16320.1| ![Theta Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/Theta.png)|
|TCNModel 	|23509.7|	17404.3| ![TCN Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/TCNModel.png)|
|Auto-ARIMA	|23509.7|	17649.3| ![Arima Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/AutoARIMA.png)|
|NBEATSModel| 	23509.7|	18466.6| ![NBeats Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/NBEATSModel.png)|
|Prophet	|23509.7|	18683.2| ![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/Prophet.png) |

But though many models beat the Time Series by comfortable margin, we should be looking at N beats Model as its curve looks best fit. Complete output for this trial
can be found at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered)

##### 3. req_ThunB2B_PP : Only 4 models i.e. TCNModel,Theta,Auto-ARIMA and NBEATSModel beat the benchmark model.But if you look at the curve N beats model gives you the best curve.

|model |	loss_benchmark |	loss_model |Plot Models Prediction |
|------| ------- | -------| ------ |
|TCNModel | 	11758.0	|9843.7 | ![TCN Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered/TCNModel.png) |
|Theta(2) |	11758.0	|10560.3 | ![Theta Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered/Theta.png) |
|Auto-ARIMA |	11758.0	|10705.8 | ![Arima Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered/AutoARIMA.png) |
|NBEATSModel |	11758.0	 |11494.8 | ![N beats Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered/NBEATSModel.png) |

But though many models beat the Time Series by comfortable margin, we should be looking at N beats Model as its curve looks best fit. Complete output for this trial
can be found at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered)

##### 4. req_ThunB2B_Sorter : No Models beats the benchmark model. The best performing model is prophet which has MAE - 4k more than the benchmark. We will tune the parameters for this model

|model |	loss_benchmark	|loss_model | Plot Models Prediction |
|------| ------- | -------| ------ |
|Prophet|	33980.2	|38167.9 |![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_Sorterfiltered/Prophet.png) |
|Theta(2)|	33980.2	|42468.7 |![Theta Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_Sorterfiltered/Theta.png) |
|ExponentialSmoothing |	33980.2 |	48377.8 |![Exponential Smoothing Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_Sorterfiltered/ExponentialSmoothing.png) |

Complete output for this trial can be found at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_Sorterfiltered)

##### 5. req_ThunB2C : No Models beats the benchmark model. The best performing model is prophet which has MAE - 4k more than the benchmark.

|model |	loss_benchmark|	loss_model|Plot Models Prediction |
|------| ------- | -------| ------ |
|Auto-ARIMA	| 4775 |	5456 | ![Arima Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2Cfiltered/AutoARIMA.png)|
|FFT |	4775 |	6892 |![FFT Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2Cfiltered/FFT.png) |
|Prophet |	4775 |	6929 |![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2Cfiltered/Prophet.png) |

Complete output for this trial can be found at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2Cfiltered)

### Objective 2 : For req_ThunB2B_Sorter & req_ThunB2C do hyperparameter tuning.

##### Hyperparam Tuning : req_ThunB2B_Sorter

After doing multiple trials and experimentation, we have been able to reach MAE of 35630 as compared to benchmark error of 33980. Before Tuning it was 38167.This has been achieved using Prophet model with below hyperparams. The Grid Search was done on following hyperparams:


####       "seasonality_mode" : {"values":['additive','multiplicative']},
####       "n_changepoints" : {"values" : [5,10,20,30,40,50,60,70,80]},
####       "changepoint_range" : {"values" : [0.5,0.6,0.7,0.8,0.9]},
####       "seasonality_prior_scale" : {"values" :[5,10,20,30,40,50]

Grid Search Resulted in best hyperparams as follows :

  |changepoint_range| n_changepoints |	seasonality_mode |	seasonality_prior_scale |
  |------| ------- | -------| ------ |
  | 0.8 |	30	| additive |	30 |
 
Few Trials which did not work are as follows :

  1. Interpolation of Covid 2020 when demand was very less with 2019 observations
  2. Ensembling Prophet with ExponentialSmoothing model and FFT() as they are second best model
  3. Ignoring the covid period

The results of hyperparam are documented in this [csv](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Hyperparam_tuning/req_ThunB2B_Sorter-hyperparms_tuning.csv)


##### Hyperparam Tuning : req_ThunB2B_Sorter

By hyperparameter tuning, we beat the benchmark model. Our model MAE is 4038 as compared to 4774 from benchmark Before hyperparam tuning it was around 6000. The best model is exponential smoothing. The Grid Search was done on following hyperparams:

####   "trend" : {"values" :[ModelMode.ADDITIVE, ModelMode.MULTIPLICATIVE,ModelMode.NONE]},
####  "damped" :{"values" : [True,False]},
####   "seasonal":{"values" :[SeasonalityMode.ADDITIVE, SeasonalityMode.MULTIPLICATIVE, SeasonalityMode.NONE]},
####   "seasonal_periods" :{"values":[4,8,16,24,32,52,53,56,60,72]}

Grid Search Resulted in best hyperparams as follows :

 |trend| damped |	seasonal |	seasonal_periods |
 |------| ------- | -------| ------ |
 | ModelMode.ADDITIVE |	TRUE	| SeasonalityMode.ADDITIVE |	52 |

The code used for hyperparam tuning is placed at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Codes/TimeSeries_Experimentation-Req_ThunB2c.ipynb)

### Modelling Using Past Covariates

After further analysis, we created new variables called Sales Order Quantity for 4 different periods. We will use these variables as Past Covariates and compare with model without past covariates to see if past covariates. 

We created four different models and use it predict 4 different periods:

| Variable Name | Start Date | End Date | # of Weeks |
| -------| ------ | -------| ------ |
| SO_QTY_20210315 | 2021-03-22 | 2021-06-07 | 12 |
| SO_QTY_20210607 | 2021-06-14 | 2021-08-30 | 12 |
| SO_QTY_20210830 | 2021-09-06 | 2021-11-22 | 12 |
| SO_QTY_20211122 | 2021-11-29 | 2022-01-31 | 10 |

|                  | SO\_QTY\_20210315 |                         |                 | SO\_QTY\_20210607 |                         |                 | SO\_QTY\_20210830 |                         |                 | SO\_QTY\_20211122 |                         |                 |
| ---------------- | ----------------- | ----------------------- | --------------- | ----------------- | ----------------------- | --------------- | ----------------- | ----------------------- | --------------- | ----------------- | ----------------------- | --------------- |
| Models           | Model\_Loss       | Model\_Loss\_Covariates | loss\_benchmark | Model\_Loss       | Model\_Loss\_Covariates | loss\_benchmark | Model\_Loss       | Model\_Loss\_Covariates | loss\_benchmark | Model\_Loss       | Model\_Loss\_Covariates | loss\_benchmark |
| NBEATSModel      | 30325.7           | 26818.5                 | 73494.5         | 113385.3          | 29018.7                 | 41794.7         | 153271.0          | 138060.4                | 58756.5         | 104097.1          | 42380.9                 | 48203.2         |
| BlockRNNModel    | 183724.4          | 183654.2                | 73494.5         | 160021.4          | 159951.2                | 41794.7         | 249280.5          | 249210.3                | 58756.5         | 218586.8          | 218516.5                | 48203.2         |
| LinearRegression | 23482.4           | 23347.5                 | 73494.5         | 26744.6           | 26737.7                 | 41794.7         | 42084.5           | 41696.6                 | 58756.5         | 30778.4           | 29069.3                 | 48203.2         |
| RandomForest     | 37304.9           | 37266.0                 | 73494.5         | 53048.8           | 54403.5                 | 41794.7         | 95228.3           | 97509.2                 | 58756.5         | 92189.4           | 88316.2                 | 48203.2         |
| TCNModel         | 54464.1           | 42427.5                 | 73494.5         | 47941.3           | 60461.0                 | 41794.7         | 130264.8          | 133425.2                | 58756.5         | 91607.0           | 83487.6                 | 48203.2         |
| TransformerModel | 183546.5          | 180871.4                | 73494.5         | 159443.3          | 156036.6                | 41794.7         | 248105.7          | 243976.0                | 58756.5         | 216624.4          | 211777.5                | 48203.2         |
