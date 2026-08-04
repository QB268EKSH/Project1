# Evaluating the Impact of Model Complexity on Stock Market Direction Prediction

## Executive Summary

This project investigates whether increasing model complexity improves next‑day stock market direction prediction using historical Yahoo Finance data. Three models were evaluated: a Dummy Baseline Classifier, Logistic Regression, and a Multi‑Layer Perceptron (MLP) Neural Network. Accuracy improved from **42.6% → 53.2% → 55.3%**, suggesting that complexity helps, although gains remain modest due to dataset limitations and market uncertainty.

---

## Introduction

Predicting stock market movements is challenging due to economic conditions, investor sentiment, and external events. Machine learning techniques can identify patterns within financial data that support forecasting and investment decisions. Logistic Regression offers interpretability, while Neural Networks can model more complex relationships.

This project tests the hypothesis that increasing model complexity improves out‑of‑sample stock market direction prediction compared with a simpler Logistic Regression approach.

---

## Data Collection

Historical stock market data was obtained from Yahoo Finance. The dataset included:

- Open  
- Close  
- High  
- Low  
- Adjusted Close  
- Volume  

These indicators represent volatility, momentum, and trading activity.

---

## Infrastructure Strengths, Constraints and Tool Selection

Python was selected due to its strong machine learning ecosystem (Scikit‑learn, Pandas, Matplotlib, Seaborn).  
Yahoo Finance provided accessible historical trading data but excluded broader influences such as:

- macroeconomic indicators  
- company fundamentals  
- interest rates  
- investor sentiment  

A production‑grade solution would require multiple data sources, automated pipelines, and ongoing model monitoring.

---

## Data Preparation

Data preparation steps included:

- converting date fields to datetime  
- ordering observations chronologically  
- removing missing engineered values  
- standardising numerical variables  

Standardisation ensures scale differences do not distort model behaviour.

---

## Feature Engineering

Additional features were engineered to capture market behaviour:

- **Daily Return** — percentage change in closing price  
- **MA5** — 5‑day moving average  
- **MA20** — 20‑day moving average  

These indicators capture short‑term momentum and longer‑term trends.

<!-- <p align="center"> -->
  <img src="/assets/figures/Project1-Fig1.png" alt="Price Movements and Moving Averages" width="600">
  <strong>Figure 1: Price Movements and Moving Averages</strong>
<!-- </p> -->
<br><br>
The target variable was defined as a binary outcome indicating whether the stock price increased or decreased on the following trading day.

---

## Modelling Approach and Evaluation

Three predictive models were evaluated:

- Dummy Baseline Classifier  
- Logistic Regression  
- MLP Neural Network  

Metrics used:

- Accuracy (primary)  
- Precision  
- Recall  
- F1‑score  
- Confusion matrices  

Temporal ordering was preserved using chronological train/test splits. Walk‑forward validation was used to assess robustness.

---

## Model Performance

<!-- <p align="center"> -->
  <img src="/assets/figures/Project1-Fig2.png" alt="Model Accuracy Comparison" width="600">
  <strong>Figure 2: Model Accuracy Comparison</strong>
<!-- </p> -->
<br><br>
Although the Neural Network delivered the strongest performance, the improvement over Logistic Regression was modest at <strong>2.1 percentage points</strong>.

---

## Model Limitations and Robustness

Walk‑forward validation results:

| Test Period | Baseline | Logistic Regression | Neural Network |
|-------------|----------|---------------------|----------------|
| Q2 2025 | 37.2% | 39.5% | 41.9% |
| Q3 2025 | 46.7% | 48.9% | 48.9% |
| Q4 2025 | 48.9% | 48.9% | 48.9% |
| Q1 2026 | 50.0% | 59.5% | 47.6% |
| Q2 2026 | 42.6% | 53.2% | 55.3% |
| Q3 2026 | 50.0% | 50.0% | 75.0% |

<strong>Table 1: Walk-Forward Validation Results Across Multiple Market Periods</strong>
<br><br>
<!-- <p align="center"> -->
  <img src="/assets/figures/Project1-Fig3.png" alt="Walk-Forward Validation" width="600">

  <strong>Figure 3: Walk-Forward Validation Accuracy Across Market Periods</strong>
<!-- </p> -->
<br><br>
Findings:

- Neural Network outperformed Logistic Regression in **3 of 6** periods  
- Logistic Regression outperformed the Neural Network in **Q1 2026**  
- Both models tied in **Q3/Q4 2025**  
- The **75%** result in Q3 2026 is likely inflated due to a short evaluation window  

Conclusion: **Neural Networks are not consistently superior.**

---

## Feature Analysis

Logistic Regression coefficients (rounded):

| Feature | Coefficient |
|---------|-------------|
| High | 0.714 |
| MA20 | 0.186 |
| Open | 0.107 |
| Return | 0.063 |
| Volume | -0.117 |
| MA5 | -0.301 |
| Close | -0.424 |
| Low | -0.444 |

<strong>Table 2: Coefficient Values</strong>
<br><br>
<!-- <p align="center"> -->
  <img src="/assets/figures/Project1-Fig4.png" alt="Coefficient Plot" width="600">
  <strong>Figure 4: Coefficient Plot</strong>
<!-- </p> -->
<br><br>
Interpretation:

- High and MA20 positively correlate with next‑day increases  
- Low and Close show negative coefficients (possible mean reversion)  
- Multicollinearity means coefficients should be interpreted cautiously  

---

## Visualisation Strategy

Visualisations used:

- moving average charts  
- correlation heatmaps  
- model comparison plots  
- coefficient bar charts  

These support interpretability and communication of findings.

---

## Discussion, Business Value and Future Recommendations

Key points:

- Neural Network gains were modest and inconsistent  
- Logistic Regression remains competitive and more explainable  
- Models could support decision‑making but not automated trading  
- Business value depends on transaction costs and market conditions  
- Governance stakeholders may prefer simpler models  

---

## Conclusion

Increasing model complexity **can** improve predictive performance, but gains are modest and inconsistent. Logistic Regression remains a strong baseline due to interpretability and stability.

Model selection should balance:

- predictive performance  
- explainability  
- governance  
- operational requirements  

---

## References

Akinrinola, O., Addy, W.A., Ajayi-Nifise, A.O., Odeyemi, O. and Falaiye, T. (2024)  
*Predicting stock market movements using neural networks: A review and application study.*  
GSC Advanced Research and Reviews, 18(2), pp. 297–311.  
https://doi.org/10.30574/gscarr.2024.18.2.0123

Khan, A.H., Shah, A., Ali, A., Shahid, R., Zahid, Z.U., Sharif, M.U. et al. (2023)  
*A performance comparison of machine learning models for stock market prediction with novel investment strategy.*  
PLoS ONE, 18(9), e0286362.  
https://doi.org/10.1371/journal.pone.0286362

Phan, J. and Chang, H.F. (2024)  
*Leveraging Fundamental Analysis for Stock Trend Prediction for Profit.*  
arXiv:2410.03913.  
https://arxiv.org/abs/2410.03913

Sriram, S. (2020)  
*Stock Market Prediction using Logistic Regression Analysis – A Pilot Study.*  
International Journal for Research in Applied Science and Engineering Technology, 8(10).  
https://doi.org/10.22214/ijraset.2020.31877

Usmani, S. and Shamsi, J.A. (2023)  
*LSTM based stock prediction using weighted and categorized financial news.*  
PLoS ONE, 18(3), e0282234.  
https://doi.org/10.1371/journal.pone.0282234
