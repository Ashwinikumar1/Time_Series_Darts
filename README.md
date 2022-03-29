# Time_Series_Darts

### Environment Setup
[location](https://github.com/Ashwinikumar1/NLP-DL/tree/master/Spotify_Playlist_Creation_Using_Word2vec/Outputs)
Python Version ---> 3.7.11
Environment Yaml Files ---> The yaml file for environment can be found [here](https://github.com/Ashwinikumar1/Time_Series_Darts/tree/main/environment_variables)

### Methodology 

We are provided 4 Timeseries i.e. ["req_ThunB2B_AA", "req_ThunB2B_PP", "req_ThunB2B_Sorter", "req_ThunB2C"] and for all of them we are also provided Benchmark Forcasts from the client i.e. ["BOL_B2B AA Thun", "BOL_B2B P&P Thun", 
"BOL_B2B Sorter Thun", "BOL_B2C Thun"]. The objective of this project are as follows:

1. Try multiple DARTS model to find out which model beats the benchmark Model. Mean Absolute Error (MAE) is used to evaluate the model. Data Before '2021-01-04’  is used as training data and after this as test data
2. For the best models for each time Series Hyperparameter Tune the best model to see if it beats the becnhmark. 
3. Create Useful pipeline so it can be replicated across datasets

### Objective 1 : Trial Out different models to see which model works best. 
The code used for this excercise can be found [here](https://github.com/Ashwinikumar1/Time_Series_Darts/blob/main/Codes/All_Model_Trial.ipynb).We do two trials first on Raw Time Series Data and second on Filtered Time Series. Filtered Time Series Gives better results. 

#####


1. req_ThunB2B_AA : Multiple Models are able to beat the benchmark model with comfortable margin. The list of models are as follows :

model	loss_benchmark	loss_model
Theta(2)	23509.7	16320.1
TCNModel 	23509.7	17404.3
Auto-ARIMA	23509.7	17649.3
NBEATSModel 	23509.7	18466.6
Prophet	23509.7	18683.2
ExponentialSmoothing	23509.7	20888.5
FFT	23509.7	20926.7

    But though many models beat the Time Series by comfortable margin, we should be looking at N beats Model as its curve looks best fit

2. req_ThunB2B_PP : Only 4 models i.e. TCNModel,Theta,Auto-ARIMA and NBEATSModel beat the benchmark model.But if you look at the curve N beats model gives you the best curve.

req_ThunB2B_PP
model	loss_benchmark	loss_model
TCNModel 	11758.0	9843.7
Theta(2)	11758.0	10560.3
Auto-ARIMA	11758.0	10705.8
NBEATSModel 	11758.0	11494.8

3. req_ThunB2B_Sorter : No Models beats the benchmark model. The best performing model is prophet which has MAE - 4k more than the benchmark

req_ThunB2B_Sorter
model	loss_benchmark	loss_model
Prophet	33980.2	38167.9
Theta(2)	33980.2	42468.7
ExponentialSmoothing2	33980.2	48377.8
Auto-ARIMA	33980.2	50227.0
NBEATSModel	33980.2	53221.4

4. req_ThunB2C : No Models beats the benchmark model. The best performing model is prophet which has MAE - 4k more than the benchmark.
req_ThunB2C
model	loss_benchmark	loss_model
Auto-ARIMA	4775	5456
FFT	4775	6892
Prophet	4775	6929


