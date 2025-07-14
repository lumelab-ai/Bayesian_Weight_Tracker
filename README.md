![pandas](https://img.shields.io/badge/-pandas-blue?logo=pandas)
![numpy](https://img.shields.io/badge/-numpy-blue?logo=numpy)
![scipy](https://img.shields.io/badge/-scipy-blue?logo=scipy)
![tensorflow](https://img.shields.io/badge/-tensorflow-blue?logo=tensorflow)
![tensorflow_probability](https://img.shields.io/badge/-tensorflow--probability-blue?logo=tensorflow)
![keras](https://img.shields.io/badge/-keras-blue?logo=keras)
![tf_keras](https://img.shields.io/badge/-tf__keras-blue?logo=tensorflow)
![statsmodels](https://img.shields.io/badge/-statsmodels-blue)
![pyarrow](https://img.shields.io/badge/-pyarrow-blue?logo=apache)
![openpyxl](https://img.shields.io/badge/-openpyxl-blue)
![tqdm](https://img.shields.io/badge/-tqdm-blue?logo=python)
![ipython](https://img.shields.io/badge/-ipython-blue?logo=jupyter)
![matplotlib](https://img.shields.io/badge/-matplotlib-blue)
![seaborn](https://img.shields.io/badge/-seaborn-blue)
![networkx](https://img.shields.io/badge/-networkx-blue)

---

> ⚠️ **Status: Pre-Release**
>
> This project is still under active development and has **not yet reached version 1.0**.
> It’s progressing well and already provides meaningful results, but some parts may evolve.
>
> 🧪 The full analysis is implemented in a **Jupyter Notebook**, designed for transparency, experimentation, and reproducibility.
>
> 🤝 **Contributions are welcome** — whether it's feature ideas, bug fixes, or feedback.

# 🧠 **Project Overview**
Wearables, smart scales, and nutrition-tracking apps generate an immense volume of health-related data — from physical activity and sleep to nutrition and hydration. Yet the real value of this data often remains locked within the platforms that collect it, serving mostly as vanity metrics or for social sharing. This project aims to change that by creating an analytical tool that puts this data to work **for the user**.

Our goal is to deliver a deep, personalized analysis of how different aspects of your daily habits — such as sleep quality, activity level, and dietary intake — influence **changes in your body weight** over time, whether your goal is to **lose**, **gain**, or **maintain** it. The model not only identifies these relationships but also **quantifies their impact**, offering **actionable insights** to help users make smarter health and wellness decisions.

At the core of the system is a **Bayesian Structural Time Series (BSTS)** model, built with **TensorFlow Probability**. BSTS is a class of probabilistic time series models that decomposes an observed variable (here, body weight) into latent components such as:

* **A local linear trend**, capturing long-term directional changes, and
* **A regression component with exogenous variables**, modeling how daily behaviors influence that trend.

This framework enables the estimation of **time-varying effects**, the use of **flexible priors** based on domain knowledge, and the generation of **credible intervals** to express uncertainty. Unlike standard models, BSTS produces full **posterior distributions** — allowing for risk-aware forecasts that reflect the true variability in individual trajectories.

Users can analyze how their habits affect weight over time and share these insights with healthcare professionals — such as nutritionists, sports physicians, or coaches — who can then design **personalized, data-driven wellness plans** based on real behavioral evidence.

---

# 🔍 **Technical Highlights and Innovations**

This project demonstrates the application of advanced data science methods to a real-world health problem, with key technical elements including:

* **Bayesian Structural Time Series (BSTS) Modeling:** Uses TensorFlow Probability’s BSTS to model weight variation, combining a latent trend component with exogenous regressors representing user behavior. This supports both interpretability and robust forecasting.

* **Hierarchical Priors and Uncertainty Calibration:** Applies structured hierarchical priors to regression coefficients by grouping features conceptually (e.g., body composition, activity, nutrition). This reduces parameter uncertainty and improves generalization. A custom `HalfNormal` prior is used for observation noise (`σ_obs`) to align the model's uncertainty scale with the empirical variance.

* **Variational Inference (VI):** Enables scalable posterior approximation, producing full distributions over model parameters and forecasts — essential for understanding prediction uncertainty and communicating risk.

* **Robust Data Processing and Feature Engineering:** Includes validation routines, outlier treatment (winsorization at p5–p95), and computation of 15 key behavioral indicators derived from raw health logs (e.g., sleep, steps, calories, hydration).

* **Sliding Window Construction:** Converts daily data into rolling 91-day windows. For each window, it aggregates metrics (mean, median, standard deviation) and computes the weekly slope of weight change (kg/week) as the prediction target.

* **Advanced Collinearity Filtering:** Uses a graph-based approach (NetworkX) to detect highly correlated features. Within each correlated cluster, the most representative variable is selected based on average correlation with both other features and the target.

* **Calibrated Walk-Forward Validation:** Implements sequential forecasting to mimic real deployment scenarios. Prediction intervals are empirically calibrated to achieve actual coverage between 90% and 95%, ensuring alignment between forecast uncertainty and observed outcomes.

* **Comprehensive Model Diagnostics:** Provides tools to evaluate convergence, residual structure, feature normality, and predictive calibration (PIT histograms, reliability diagrams). Also includes prior sensitivity analysis, forecast degradation monitoring, and posterior predictive checks (PPC) via HMC on synthetic data.

* **Cross-Validation with Temporal Blocking:** Adds a robust alternative validation method by splitting the dataset into time-based blocks. This tests the model’s generalization across periods and minimizes temporal leakage.

* **Interpretability and Scenario Projections:** Extracts time-varying feature weights in stable windows, generates interpretability visuals (e.g., heatmaps of top features, diverging bar plots), and runs multi-step-ahead simulations to estimate the probability of reaching specific weight goals under behavioral adjustments.

---

# 🌱 **Why This Project Matters**

This project is more than a technical showcase — it’s a user-focused, data-informed response to a widespread challenge: understanding how daily behaviors affect long-term body weight.

* **Empowering the Individual:** Transforms passive self-tracking into active insight. Instead of relying on generic advice, users can see which specific behaviors correlate most with their personal weight patterns.

* **Supporting Evidence-Based Interventions:** Enables professionals (nutritionists, physicians, coaches) to craft tailored plans based on rich behavioral data, improving precision and long-term effectiveness.

* **End-to-End Data Science Practice:** Demonstrates a complete pipeline — from raw data handling and feature engineering to Bayesian modeling, posterior inference, diagnostic validation, and interpretability. This reflects how real-world data science is done.

* **Uncertainty as a First-Class Citizen:** Forecasts are delivered with uncertainty baked in — not as afterthoughts. This allows better communication of confidence, avoids false precision, and promotes informed, cautious decision-making.

* **Applied to Real, Noisy Data:** Unlike toy datasets or competitions, this pipeline deals with real-world imperfections: gaps, behavioral noise, uneven sampling. It extracts meaning despite the mess, producing outputs that are both interpretable and useful.

* **Open and Extendable:** The system is modular, documented, and open-source — enabling others to reproduce, extend, or repurpose it for different health and behavior modeling contexts.

---

# 🧭 **Getting Started & Documentation**

Technical documentation is maintained in the **[Wiki](../../wiki)**, including:

* Setup instructions and environment configuration
* Data format and preprocessing details
* Step-by-step guidance for running the pipeline
* Model assumptions and design decisions
* Evaluation metrics and interpretability tools
* Contribution guidelines and roadmap

Whether you're exploring, adapting, or contributing — the Wiki is the best place to begin.

---

# 🔓 **Open-Source License**

This project is licensed under the **GNU General Public License v3.0 (GPLv3)**.

You're free to:

* Use, modify, and redistribute the code
* Incorporate it into commercial or non-commercial projects
* Build derivative works

As long as you:

* Distribute derivative work under the same GPLv3 license
* Attribute the original project appropriately
* Keep the source code open and share your modifications with the community

See the [`LICENSE`](./LICENSE) file for complete terms.

---

# 👤 About Me
My name is Lucas Pereira. I'm a UX and Conversational Designer with a strong foundation in Data Science. My work bridges human-centered design and statistical modeling, with a focus on creating AI-powered tools that are both technically rigorous and meaningful to real users. I’m especially interested in applying Bayesian methods to behavior-driven data.
