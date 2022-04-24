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



##### 1. req_ThunB2B_AA : Multiple Models are able to beat the benchmark model with comfortable margin. The list of models are as follows :

|model| loss_benchmark |	loss_model | Plot Models Prediction |
|------| ------- | -------| ------ |
|Theta(2)|	23509.7	|16320.1| ![Theta Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/Theta.png)|
|TCNModel 	|23509.7|	17404.3| ![TCN Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/TCNModel.png)|
|Auto-ARIMA	|23509.7|	17649.3| ![Arima Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/AutoARIMA.png)|
|NBEATSModel| 	23509.7|	18466.6| ![NBeats Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/NBEATSModel.png)|
|Prophet	|23509.7|	18683.2| ![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered/Prophet.png) |


But though many models beat the Time Series by comfortable margin, we should be looking at N beats Model as its curve looks best fit. Complete output for this trial
can be found at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_AAfiltered)

##### 2. req_ThunB2B_PP : Only 4 models i.e. TCNModel,Theta,Auto-ARIMA and NBEATSModel beat the benchmark model.But if you look at the curve N beats model gives you the best curve.

|model |	loss_benchmark |	loss_model |Plot Models Prediction |
|------| ------- | -------| ------ |
|TCNModel | 	11758.0	|9843.7 | ![TCN Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered/TCNModel.png) |
|Theta(2) |	11758.0	|10560.3 | ![Theta Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered/Theta.png) |
|Auto-ARIMA |	11758.0	|10705.8 | ![Arima Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered/AutoARIMA.png) |
|NBEATSModel |	11758.0	 |11494.8 | ![N beats Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered/NBEATSModel.png) |

But though many models beat the Time Series by comfortable margin, we should be looking at N beats Model as its curve looks best fit. Complete output for this trial
can be found at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_PPfiltered)

##### 3. req_ThunB2B_Sorter : No Models beats the benchmark model. The best performing model is prophet which has MAE - 4k more than the benchmark. We will tune the parameters for this model

|model |	loss_benchmark	|loss_model | Plot Models Prediction |
|------| ------- | -------| ------ |
|Prophet|	33980.2	|38167.9 |![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_Sorterfiltered/Prophet.png) |
|Theta(2)|	33980.2	|42468.7 |![Theta Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_Sorterfiltered/Theta.png) |
|ExponentialSmoothing |	33980.2 |	48377.8 |![Exponential Smoothing Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_Sorterfiltered/ExponentialSmoothing.png) |

Complete output for this trial can be found at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2B_Sorterfiltered)


##### 4. req_ThunB2C : No Models beats the benchmark model. The best performing model is prophet which has MAE - 4k more than the benchmark.

|model |	loss_benchmark|	loss_model|Plot Models Prediction |
|------| ------- | -------| ------ |
|Auto-ARIMA	| 4775 |	5456 | ![Arima Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2Cfiltered/AutoARIMA.png)|
|FFT |	4775 |	6892 |![FFT Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2Cfiltered/FFT.png) |
|Prophet |	4775 |	6929 |![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2Cfiltered/Prophet.png) |

Complete output for this trial can be found at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Before_Filtering/req_ThunB2Cfiltered)

##### 4. Sum of all variables: Prophet Model beats the benchmark model by a margin of 4k. All other models perform worse than the benchmark model

|model |	loss_benchmark|	loss_model|Plot Models Prediction |
|------| ------- | -------| ------ |
|Prophet	| 51986 |	47985 | ![Prophet Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Sum_All_Variablesfiltered/Prophet.png)|
|TCN Model |	51986 |	63071 |![TCN Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Sum_All_Variablesfiltered/TCNModel.png) |
|N Beats Model |	51986 |	73559 |![N Beats Plot](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Outputs/Sum_All_Variablesfiltered/NBEATSModel.png) |

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
####   "seasonal":{"values":[SeasonalityMode.ADDITIVE, SeasonalityMode.MULTIPLICATIVE, SeasonalityMode.NONE]},
####   "seasonal_periods" :{"values":[4,8,16,24,32,52,53,56,60,72]}

Grid Search Resulted in best hyperparams as follows :

 |trend| damped |	seasonal |	seasonal_periods |
 |------| ------- | -------| ------ |
 | ModelMode.ADDITIVE |	TRUE	| SeasonalityMode.ADDITIVE |	52 |

The code used for hyperparam tuning is placed at this [location](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Codes/TimeSeries_Experimentation-Req_ThunB2c.ipynb)


