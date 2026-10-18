# Social-Media-Time-Series-Forecasting

# Social Media Time Series Forecasting

Forecasting social media activity on Instagram, Facebook and YouTube using three different time series methods: **ARIMA/SARIMA**, **Prophet** and a **GRU neural network**.

This was a group project for **BCO6008 Predictive Analytics** at Victoria University (group of three). It combines a short literature review with three hands-on forecasting projects.

## Key finding

No single forecasting model works best everywhere. The right model depends on the platform and the shape of its data:

| Platform | Model | Why it fits |
| --- | --- | --- |
| Instagram | ARIMA / SARIMA | Steady activity with slow, predictable changes |
| Facebook (post volume) | Prophet | Clear weekly and yearly seasonality, holiday dips |
| YouTube | GRU | Non-linear engagement with sudden viral spikes |

## My contribution: YouTube engagement forecasting (GRU)

I built the deep learning part of the project, forecasting YouTube engagement with a GRU network.

- **Data preparation:** Aggregated YouTube interaction logs into a daily time series and handled missing values from gaps in the data
- **Scaling:** Normalised values to the range [0, 1] with MinMax scaling
- **Raw, non-stationary input:** Kept the data undifferenced so the network could learn trends and spikes itself, unlike ARIMA, which needs differencing
- **Windowing and split:** Turned the history into sliding look-back windows (past *n* days predict the next day) and split by time, 80% train and 20% test, to prevent data leakage
- **Model:** One GRU layer with 64 hidden units, a dropout layer (rate 0.2) and a dense output layer for single-step regression
- **Training:** Mean Squared Error loss with the Adam optimiser
- **Evaluation:** MAE, RMSE and MAPE on the held-out test set

**Results:** [add your GRU test-set MAE / RMSE / MAPE here]

## Team projects

### Instagram: ARIMA / SARIMA
- 365 days of Instagram reach data, with seasonal decomposition (30-day period) and ACF/PACF analysis
- Compared AR(1), AR(2), MA(1), ARMA(1,1), ARIMA(1,1,1) and SARIMA(1,1,1)(1,1,1,30)
- SARIMA had the best fit (lowest AIC and BIC), but ARIMA(1,1,1) had the lowest forecast errors (MSE, MAE, RMSE)
- A model with the best fit is not always the one that forecasts best
- 30-day forecast: reach staying around 25,000 to 30,000

### Facebook Prophet: publishing volume
- Daily post counts from January 2015 to June 2017, aggregated to weekly to reveal the trend
- The baseline model struggled with changing variance over time, so a Box-Cox transformation was applied before training
- Test error (MAPE) came down to 11.7%
- Decomposition showed accelerating growth from late 2016, a weekday/weekend pattern, and a yearly low around Christmas

## Literature review

Five peer-reviewed papers on social media forecasting were reviewed. They showed that:
- Traditional models like ARIMA still work well on stable data
- Adding outside signals (news, events) improves forecasts
- Hashtag recommendation can raise engagement and reach

## Limitations and future work

- No formal stationarity test (ADF) was run before the ARIMA models
- Only the platform's own history was used, with no outside variables such as hashtags, posting frequency or ad campaigns
- Next step: add exogenous regressors (for example trending topic indicators) to all three models and test whether the platform-specific results still hold

## Repository contents

| File | Description |
| --- | --- |
| `Predictive Analytics.docx` | Full group report: literature review, the three forecasting projects and individual reflections |

## Tools

Python, pandas, Matplotlib, Statsmodels (ARIMA/SARIMA), Prophet, SciPy (Box-Cox), [add your deep learning library, for example TensorFlow/Keras or PyTorch]

## References and data sources

- [YouTube Engagement Forecasting (GRU, LSTM, Prophet, SARIMA)](https://github.com/abdullahhunjra/YouTube-Engagement-Forecasting-using-Deep-Learning-and-Time-Series-Models-FastAPI-Docker) by abdullahhunjra
- [Time series with Facebook Prophet](https://www.kaggle.com/code/kashnitsky/topic-9-part-2-time-series-with-facebook-prophet) by kashnitsky (Kaggle)
- [Instagram Time Series](https://www.kaggle.com/code/snehalkhandewale/instagram-time-series) by snehalkhandewale (Kaggle)

## Author

Joshua Wiliam Emor
Group project completed with two teammates. Academic work, Victoria University.
