# vmd-lstm
Time-series forecasting using VMD-LSTM model architecture
Inspiration article: https://arxiv.org/abs/2212.14687

Introduction:
- The idea of the article which uses mainly forecasting of each separate IMF and the sum up the results into reconstructed y_pred and was only taken as inspiration. Experimenting with LSTM and single dataset of IMFs were used in the following project.
- Starting the research for the regression problem with boston housing dataset target variable only. Finishing it with Standard and Poor's 500 ETF closing prices transformed into detrended percentage changes time-series. The model pipeline consist of Variational mode decomposition (VMD) part which creates dataset with n-amount of derivative features (IMFs). Input data for the modeling part of the algorithm consist only of IMFs with batch lengths of t-21 to t-0 for the features and t+1 for the target created with tf.TimeseriesGenerator(). Afterwards in the process of verification of the results simulation was created and a few mistakes in the process were detected.

Content:
- vmd-lstm: the initial research using boston housing data
- vmd-lstm_findata: using the previous research knowledge, organized into a class of methods for ease of use with SPY log(returns) data.
- vmd_verify: containing the final results and development of stepwise simulation with build up of the previous knowledge of how to forecast t+1 using tf.TimeseriesGenerator()

Notes:
- Decomposing before splitting the data into train/test sets is leaking the target in the test set which makes test results unvalid.
- Decomposing with Python vmdpy requires even amount of examples in the data that is used to be decomposed.
- Searching for the best vmdpy.VMD() parameters was done by reconstructing the IMFs and substracting the original input in order to analyze the error in terms of RMSE and MAPE. The results with lowest RMSE and MAPE in the reconstruction error were picked. It was assumed that reconstruction error do not have to follow normal distribution.
- Using tf.TimeseriesGenerator() there were a few constrains about it. First the horizon for the target slicing is restricted to only one value per batch. Second probably because of extra measures in order to not leak future data into the training process the developers that wrote the code restricted you from predicting t+1 and in order to to that you should pad np.zeros(len(IMFs)) as last row in order to go to t+1 prediction.
- Nothing about the model architecture went through parameter search. Adam optimizer with loss function mean squared error.

Conclution:
- Using only price data with mode decomposition technique and LSTM model won't produce any meaningful results and will only support the efficient market hypothesis. The model outcome is that the best prediction of t+1 is the yesterday price. Result plots can be seen in the file vmd_verify.ipynb at the bottom of the notebook simulation results.


Contacts:
- dminchev66@gmail.com
- https://www.linkedin.com/in/daniel-minchev-b1556a156/