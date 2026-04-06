# stock-direction-ml-comparison
This project compares ML and deep learning models for predicting next-day stock direction using historical price data and technical indicators. Models are evaluated with classification metrics and a simulated trading test. Sentiment features via FinBERT are also tested to see if they meaningfully improve results.

---

# Project Proposal
## Comparing Traditional Machine Learning Models and Deep Learning Models for Predicting Short-Term Stock Direction
Adam Fischer, Eric Fode & Adam Booth <br>
University of Guelph <br>
CIS*4780 - Computational Intelligence <br>
Dr. Rozita Dara <br>
March 1, 2026 <br>

### 1. Short Description
Our project investigates the effectiveness of traditional machine learning and deep
learning models for predicting short-term stock price direction. Specifically, we have framed the
problem as a next-day binary classification task using historical daily stock data and technical
indicators. We compare linear models, feedforward neural networks, and sequential deep
learning models to evaluate whether architectures capable of modelling temporal dependencies
outperform simpler approaches in financial time-series forecasting. To evaluate the model's
performance, we will use standard machine learning metrics, along with performance-based
capital testing, in which we assign each model's simulated capital to trade day by day against
real market performance. Prior research has shown that while deep learning models such as
LSTMs and hybrid CNN-LSTM architectures can capture nonlinear and sequential patterns in
financial data, performance gains over traditional models are often modest and sensitive to
overfitting, particularly in noisy market environments (Gholami et al., 2025).
    In addition, we incorporate financial news sentiment as an external feature to examine
whether sentiment-enhanced models improve predictive performance. Sentiment scores will be
extracted from timestamped financial headlines using the domain-specific transformer model
FinBERT and aggregated at the daily level before being aligned with market data. Recent
studies in deep neural network-based stock sentiment analysis demonstrate that combining
textual sentiment with numerical indicators can enhance classification accuracy. However, it is
important to use careful evaluation methods and metrics beyond accuracy, given model bias
and class imbalance. Our project extends this comparative framework by systematically
evaluating model families with and without sentiment features under a unified experimental
setup. (Correia et al., 2022)

### 2. Motivation for the Project
**_Modeling Motivation_**
    Financial time-series data are noisy, and the datasets are small compared to those used
in common deep learning applications (e.g., image classification). This makes short-term
forecasting difficult. Therefore, it is beneficial to determine whether more complex models yield
more accurate predictions while avoiding overfitting. Traditional financial forecasting models
also rely heavily on quantitative features such as historical prices, returns, and volatility (Maung
& Swanson, 2025). However, sentiment data extracted from social media and news narratives
may influence how investors make decisions.


### 3. Analytics Objectives and Sub-Objectives
**_Main Objective:_**
    The main objective of the project is to determine which machine learning model performs
best at predicting future stock performance by training on historical stock performance.
**_Sub-Objectives:_**
    The sub-objectives are to determine:
       If models can accurately predict stock movement (higher or lower start to end of
       day price)
       Whether deep learning models are more accurate than traditional modelling
       approaches
       If sentiment features improve predictive performance
### 4. Data and Application Information
**_Data Availability:_**
    Historical daily stock price data, including Open, High, Low, Close, and Volume, will be
obtained from Yahoo Finance covering the period 2009-2020.
    Financial News headlines are obtained from Benzinga (via a Kaggle dataset),
timestamped and stock-specific.
**_Data Generation Explanation:_**
    Sentiment Scores are computed using finBERT and aggregated daily
    The target variable is generated as the next-day directional movement
**_Citations:_**
    Sentimental news dataset: Daily Financial News for 6000+ Stocks
    Yahoo Finance: Download market data from Yahoo! Finance's API

### 5. Proposed Solution and Methodology
**_Algorithms:_**
    Layer 1: Traditional Models → Logistic Regression & MLP Classifier
       MLP here only gets input for a single day at a time
    Layer 2: Time-Series Models → Windowed MLP & LSTM
       MLP here gets a window of data from the flattened input (ex: gets 5 days of info)
    Layer 3: With Sentiment → {Logistic, MLP, LSTM} with sentiment
**_Evaluation Methods_**
    Accuracy: Test how often our model is correct in predicting whether a stock moves up or
down


Precision: When our model says a stock is going to go up (When our model tells us to
buy), how often does the stock actually close higher than its open
Recall: Of the stocks in our data that went up that day, how many did we catch
F1: Overall performance of our model
All of these evaluation methods will be used to assess how well the models simply guess
whether stock prices rise or fall. However, they miss important context for financial stock
models, mainly predicting that a stock will rise, only for it to fall disastrously, in which 1 trade
may lose more than all the gains on a day. To test for this, we will also use
Return: Test over a given period if we gave the model the ability to purchase its most
certain winners, how much money we would be up or down
Sharpe Ratio: Tests the average return of the models predicted trades over how volatile,
or how much risk you take by following the models predictions

### 6. Expected Outcomes, Deliverables, and Findings
**_Expected Outcomes:_**
    We expect the Long-Short Term Memory model with the added sentiment data to be the
best at predicting future stock performance. LSTMs are the best of the models we are testing at
predicting sequential signals. That being said, it will also be the most computationally intensive,
and simpler models may perform competitively on much less compute.
**_Deliverables:_**
    Formal written research report
    Code repository containing implementations of each selected model
    Tables and visualizations highlighting model performance
    A live demonstration comparing model performance, with and without sentiment features
### 7. Resources of Completion:
Language: Python 3.12.
    Environment: Jupyter Notebook & Git
    Libraries:
       Pandas, Numpy, datetime
       yfinance, newsapi-python
       Scikit-learn, PyTorch, transformers, matplotlib, huggingface
    Data Generation:
       Market Data: derived from Yahoo Finance
       Sentiment Data: derived from kaggle dataset


### 8. Work Division Between Team Members
We will each train a model while working together to find the best way to concentrate our
dataset to maximize predictive performance. We will then work together to set up a prediction
environment in which we give the models some simulated capital to trade with, so they can
compute the return and Sharpe ratio for each model.


**References**
Correia, F., Madureira, A. M., & Bernardino, J. (2022). Deep Neural Networks Applied to Stock
Market Sentiment Analysis. _Sensors (Basel, Switzerland)_ , _22_ (12), 4409.
https://doi.org/10.3390/s
Gholami, M.T., Shahabi A. (2025). Comparison of deep learning methods with traditional
financial time series models for forecasting the TEPIX index in the Tehran Stock
Exchange. _Systems and Soft Computing_ , 7, Article 200395.
https://doi.org/10.1016/j.sasc.2025.200395.
Maung, K., & Swanson, N. R. (2025). A survey of models and methods used for forecasting
when investing in financial markets. _International Journal of Forecasting, 41_ (4).
https://doi.org/10.1016/j.ijforecast.2025.03.

