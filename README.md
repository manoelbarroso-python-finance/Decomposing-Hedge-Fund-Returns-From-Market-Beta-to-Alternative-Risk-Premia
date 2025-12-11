# Decomposing Hedge Fund Returns: From Market Beta to Alternative Risk Premia

**Author:** Manoel Barroso  
**Notebook:** `hedge_funds.ipynb`  

This project decomposes hedge-fund-like returns into traditional equity beta, style premia and latent risk factors, using a hedge-fund index ETF as a proxy.

**Quick navigation / interactive view**

For convenience, you can explore the notebook through the links below (static render or fully interactive in the browser):
- 👉 **nbviewer (static, fast navigation)**: https://nbviewer.org/github/manoelbarroso-python-finance/Decomposing-Hedge-Fund-Returns-From-Market-Beta-to-Alternative-Risk-Premia/blob/main/hedge_funds.ipynb  
- 🚀 **Google Colab (interactive, run the code online)**: https://colab.research.google.com/github/manoelbarroso-python-finance/Decomposing-Hedge-Fund-Returns-From-Market-Beta-to-Alternative-Risk-Premia/blob/main/hedge_funds.ipynb

The goal is to answer:

> How much of a hedge-fund-like return series can be explained by traditional equity beta, style factors and latent risk components (PCs), and how much is better seen as exposure to alternative risk premia or residual “true alpha”?

---

## 1. Methodology Overview

The analysis is organised in layers:

1. **Data & Returns**
   - Monthly total returns for a hedge-fund-like ETF (**HF_INDEX**).
   - Fama–French equity style factors + risk-free rate.
   - Fung–Hsieh-inspired style premia (credit, term, cross-asset trend).
   - VIX-based volatility / tail-risk factor.

2. **Layer 1 – CAPM baseline**
   - `HF_EXCESS ~ MKT_RF`
   - Evaluate basic fit (R², RMSE, MAE) and residual diagnostics.

3. **Layer 2 – Equity & style premia**
   - Extend with credit, term and trend premia.
   - Show how R² increases and CAPM “alpha” shrinks once style premia are added.

4. **Layer 3 – PCA on style premia (latent factors)**
   - Apply PCA to the extended factor set.
   - Build a PC-only model `HF_EXCESS ~ PC1–PC4`.
   - Compare performance vs the raw style-premia model.

5. **Layer 4 – PCs + VIX (volatility / tail-risk)**
   - Extend the PC model with a VIX-based factor.
   - Compare R², RMSE and MAE vs previous specifications.
   - Check whether the volatility factor is statistically significant and how it affects residual alpha and tail behaviour.

6. **Layer 5 – Shapash feature importance**
   - Use **Shapash** to compute and visualise **global feature importance** for the final `PCs + VIX` model.
   - Show that higher-order latent factors (PC3, PC4) are the main drivers of hedge-fund excess returns, with VIX playing a secondary regime-related role.

---

## 2. Key Takeaways

- A **single market factor (CAPM)** explains a large share of the variance, but leaves non-trivial residual risk and fat-tailed residuals.
- **Style premia (credit, term, trend)** improve the fit and reveal that the hedge-fund-like index loads on multiple sources of risk premia, not only equity beta.
- **PCA** compresses the factor universe into a small set of **latent components (PC1–PC4)** with almost the same explanatory power as the full style-premia model.
- The **PCs + VIX** specification shows that hedge-fund excess returns are driven mainly by **higher-order latent components** rather than the first, more “market-like” PC.
- Even though linear factor models are not ideal for fully capturing hedge-fund non-linear payoffs, they still **tell a useful story** about beta vs alternative risk premia and help frame what remains as potential “true alpha”.

---

## 3. Repository Structure

```text
hedge-funds/
│
├── hedge_funds.ipynb        # Main analysis notebook (CAPM → styles → PCA → PCs + VIX + Shapash)
├── data/
│   ├── hf_index.csv         # Hedge-fund-like ETF returns
│   ├── fama_french.csv      # Fama–French equity factors + RF
│   └── style_premia.csv     # Credit, term, trend premia (Fung-inspired)
│
├── README.md
├── LICENSE
├── requirements.txt
└── .gitignore
