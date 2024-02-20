# COMAP MCM/ICM Notes

## USEFUL WEBSITES :link:
- [Image to Latex](https://mathpix.com/image-to-latex)
- [Grammarly for final grammar checking](https://www.grammarly.com/)
- [ChatGPT for poetic title Inspirations](https://chat.openai.com/)
- [Detection tool for GPT writing](https://gptzero.me/)
- [Stronger Detector](https://contentatscale.ai/?fpr=home23&gclid=CjwKCAiAk9itBhASEiwA1my_69BJTeH6OwEUoFWRDcC15zgR6Z0Cn4mO6x6Ca8QhPl91aAr2sizvTxoCVPQQAvD_BwE)
- [Alternative](https://originality.ai/blog/contentatscale-ai-content-detection-review)

### USEFUL TOOLS

- [Color map references](https://matplotlib.org/stable/gallery/color/colormap_reference.html)
- [Time Series Histogram](https://matplotlib.org/stable/gallery/statistics/time_series_histogram.html)

## CHECKLIST :white_check_mark:

&#x2610; Set colour palatte based on the given problem
- Choose the best palatte fit for the concept/theme of the problem

&#x2610; Check Final Formatting
- &#x2610; content page and summary sheet
- &#x2610; section and subsection content
- &#x2610; grammar and use of vocabulary
- &#x2610; page count
- &#x2610; font and font sizes
- &#x2610; bold and italic letters
- &#x2610; all notations
- &#x2610; all related figures
- &#x2610; PDF output

## USEFUL TERMS

- ACF: Autocorrelation Function
- PACF: Partial Autocorrelation Function
- Augmented Dickey-Fuller Test (ADF): Test Hypothesis
- differencing

## Interpretting ACF and PACF Plots

### [Kaggle Reference](https://www.kaggle.com/code/iamleonie/time-series-interpreting-acf-and-pacf/notebook#Fundamentals)

Autocorrelation Function and Partial Autocorrelation Function plots modelled using ARMA (in our case, ARIMA) is crucial to **analyze patterns, seasonality and randomness.** Fundamentally, ACF and PACF plots are used to figure out the order of **AR (Auto-Regressive), MA (Moving Average) and ARMA models.** 

- seasonality: predictable changes that occur over a one-year period in a business or economy based on calendar or commercial seasons

### AR Model 

$\hat{y_t} = \alpha_1y_{t-1}+...+\alpha_py_{t-p}$

This equation assumes that the current value ($y_t$) is **dependent on previous values** ($y_{t-p}$) to build a linear regression model. **PACF is used to figure out the order of AR.**

### MA Model

$\hat{y_t} = \beta_1y_{t-1}+...+\beta_py_{t-p}$

On the other hand, MA model assumes that the current value ($y_t$) is **dependent on the error terms** including current error ($\epsilon_t, ... , \epsilon _{t-q}$). Since the error terms are completely random, there is no linear relationship between current value and error terms. **ACF is used instead.**

| AR | MA |
| - | - |
| PACF | ACF |
| previous terms | error terms|
| $\hat{y_t} = \alpha_1y_{t-1}+...+\alpha_py_{t-p}$ | $\hat{y_t} = \beta_1y_{t-1}+...+\beta_py_{t-p}$ |

## Stationarity

### ACF and PACF assume stationarity of the underlying time series. This can be checked by performing Augmented Dickey-Fuller Test (ADF): Test Hypothesis

- p-value > 0.05: Fail to reject the null hypothesis (H0), the data has a unit root and is non-stationary.
- p-value <= 0.05: Reject the null hypothesis (H0), the data does not have a unit root and is stationary.

To achieve stationary time series, apply differencing. **Stationary ACF plots will drop to zero relatively quickly by observation while non-stationary plots decreases slowly.**

- differencing: compute differences between consecutive observations

## Definitions and Characteristics of ACF and PACF

**ACF**

Correlation between time series with a lagged version of itself. The correlation between the observation at the current time spot and the observations at previous time spots.The autocorrelation function starts a lag 0, which is the correlation of the time series with itself and therefore results in a correlation of 1.

The ACF plot can provide answers to the following questions:

- Is the observed time series white noise / random?
- Is an observation related to an adjacent observation, an observation twice-removed, and so on?
- Can the observed time series be modeled with an MA model? If yes, what is the order?

**PACF**

Additional correlation explained by each successive lagged term. The correlation between pbservations at two time spots given that we consider both observations are correlated to observations at other time spots:

> The partial correlation at lag k is the autocorrelation between $X_t$ and $X_{t-k}$ that is not accounted for by lags 1 through $k-1$.

The PACF plot can provide answers to the following questions:

- Can the observed time series be modeled with an AR model? If yes, what is the order?

**Both the ACF and PACF start with a lag of 0, which is the correlation of the time series with itself and therefore results in a correlation of 1.**

**The difference between ACF and PACF is the inclusion or exclusion of indirect correlations in the calculation.**

**Furthermore, you will see a blue area in the ACF and PACF plots, which depicts the 95% confidence interval and is in indicator for the significance threshold. That means, anything within the blue area is statistically close to zero and anything outside the blue area is statistically non-zero.**

## Order of AR, MA and ARMA Model

To determine model:

| | AR(p) | MA(q) | ARMA |
| - | - | - | - |
| ACF | Tails off (Geometric Decay) | Significant at lag q / Cuts off after lag q | Tails off (Geometric decay) |
| PACF | Significant at lag p / Cuts off after lag p | Tails off (Geometric decay) | Tails off (Geometric decay) |

ARMA identification:

| | ACF | PACF |
| - | - | - |
| AR(p) | Damped exponential and/or sine functions | $\phi_{kk} = 0$ for $k > p$ |
| MA(q) | $\rho(k) = 0$ for $k < q$ | Dominated by damped exponential and/or sine functions |
| ARMA(p, q) | Damped exponential and/or sine functions after lag $max(0, q-p)$ | ominated by damped exponential and/or sine functions after lag $max(0, p-q)$ |

