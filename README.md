# vmd-lstm
Time-series forecasting using VMD-LSTM model architecture
(inspired from: https://arxiv.org/abs/2212.14687)

Using only 1d target data that is decomposed into many IMFs which are used as feature dataset.
Target is financial market data returns with daily interval for the last 5 years of Standart and Poor's 500 ETF Closing prices.
Model is based on Keras.

Notes: There was a challange with understanding VMD pre-processing part of the model. Leaking data with first decomposing all the data was a problem in the vmd-lstm.ipynb and vmd-lstm_findata.ipynb. After that there is vmd_verify.ipynb which fix the problem with leaking future target data into the test set by not using simulation iterative algorithm rather than just decomposing all at the begining. 
