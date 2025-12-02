# Econometric Analysis of Asset Pricing: Fama-French Factor Modeling and Performance Attribution

## Project Overview

This project applies the renowned **Fama-French 3-Factor (FF3)** and **5-Factor (FF5)** asset pricing models to analyze and predict the excess monthly returns of a single stock (AAPL). It is a rigorous application of classical financial econometrics, leveraging the Ordinary Least Squares (OLS) regression framework to attribute stock performance to systematic market risk and key non-market factors (Size, Value, Profitability, and Investment). The core objective is to compare the explanatory power and predictive accuracy of the FF3 versus FF5 models.

## Phenomenon and Background

### The Evolution of Asset Pricing Theory

This project is grounded in the evolution of asset pricing theory, beginning with the **Capital Asset Pricing Model (CAPM)**.

  * **CAPM (Old Theory):** CAPM posited that an asset's expected return ($R_a$) was solely dependent on the **Market Risk Premium** ($\text{Market Return} - \text{Risk-Free Rate}$), scaled by the stock's sensitivity to the market ($\beta_a$).

    $$
    R_a = R_{rf} + [\beta_a \times (R_m – R_{rf})]
    $$

      * **Limitation:** This theory failed to fully explain stock returns, as many stocks with similar market risk ($\beta$) provided significantly different returns.

  * **Fama-French Three-Factor Model (1992):** The FF3 model was developed to address CAPM's limitations. Fama and French found that two additional factors—**Size** and **Value**—systematically influence stock returns. This model helps **segregate investment skill from simple exposure** to these known factor premiums.

### Key Factor Definitions

The Fama-French factors are constructed using portfolio returns to isolate the premium associated with a specific characteristic:

| Factor | Definition | Underlying Concept |
| :--- | :--- | :--- |
| **Mkt-RF** | **Market Risk Premium** | The excess return of the broad market over the risk-free rate. |
| **SMB** | **Small Minus Big (Size Factor)** | Historical excess returns of small-cap companies over large-cap companies (small firms have higher growth potential). |
| **HML** | **High Minus Low (Value Factor)** | Historical excess returns of **Value Stocks** (high book-to-market ratio) over **Growth Stocks** (low book-to-market ratio). |
| **RMW** | **Robust Minus Weak (Profitability Factor)** | Excess return of companies with high profitability over those with low profitability. |
| **CMA** | **Conservative Minus Aggressive (Investment Factor)** | Excess return of companies with conservative investment policies over aggressive ones. |

**Value/Growth Interpretation:** A **High Book-to-Market (BTM) Ratio** (Book Value \> Market Value) indicates a potentially undervalued stock (a Value stock), which often provides a higher historical excess return (the Value Effect).

## 🛠️ Technical Workflow & Methodology

The solution involves sophisticated financial data extraction, transformation, and statistical modeling:

#### 1\. Data Acquisition and Transformation

  * **Stock Data:** Historical daily price data for AAPL (2020-2025) was extracted using the `yfinance` API. Adjusted Close prices were used to account for stock splits and dividends, reflecting true investment performance.

  * **Factor Data:** Fama-French factor data was retrieved directly from the **Kenneth French Library** using `pandas-datareader`, providing prepackaged, cleaned historical US stock returns.

  * **Time-Series Alignment:** Daily stock returns were resampled and aggregated to **monthly returns** to align with the monthly frequency of the Fama-French factors.

  * **Excess Return Calculation:** Calculated the dependent variable: **Excess Return** ($R_a - R_{rf}$).

#### 2\. Regression Analysis (FF3 Model)

The FF3 regression is used to estimate the factor sensitivities ($\beta$):

$$
R_a - R_{rf} = \alpha + \beta_{Mkt}(Mkt-RF) + \beta_{S}(SMB) + \beta_{V}(HML) + \epsilon
$$

  * **Model Implementation:** Implemented OLS regression using `statsmodels`. The **alpha ($\alpha$) term** is the intercept, representing the asset's return that is **unexplained** by the systematic factors (i.e., the stock's abnormal return).

  * **Diagnostics:** Performed model diagnostics including residual vs. fitted plots and partial regression plots to check OLS assumptions.

#### 3\. Regression Analysis (FF5 Model)

The FF5 model expands the equation by including the Profitability (RMW) and Investment (CMA) factors.

$$
R_a - R_{rf} = \alpha + \beta_{Mkt}(Mkt-RF) + \beta_{S}(SMB) + \beta_{V}(HML) + \beta_{R}(RMW) + \beta_{C}(CMA) + \epsilon
$$

  * **Implementation:** Followed the same OLS methodology, analyzing if the two additional factors provide a significant explanatory lift.

#### 4\. Model Comparison and Validation

  * **Validation:** Used a temporal train-test split (80/20) to evaluate out-of-sample prediction performance.

  * **Metrics:** Used $R^2$ and **Root Mean Squared Error (RMSE)** to quantitatively compare the explanatory and predictive power of the FF3 and FF5 models.

## Dependencies and Setup

| Package | Purpose |
| :--- | :--- |
| **`pandas` / `numpy`** | Data wrangling, aggregation, and statistical computing. |
| **`yfinance`** | Financial data extraction (stock prices). |
| **`pandas_datareader`** | Direct retrieval of Fama-French factor data from Kenneth French's library. |
| **`statsmodels`** | Econometric OLS regression and statistical diagnostics (Summary, Partial Regression Plots). |
| **`scikit-learn`** | Train-test split, model fitting, and performance metric calculation (MSE, $R^2$). |
| **`matplotlib` / `plotly`** | Data visualization and diagnostic plots. |

You can install the dependencies using the following:

```
pip install pandas numpy yfinance statsmodels pandas-datareader scikit-learn plotly
```
