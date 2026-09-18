# Pension-Fund-Risk-Modeling-GARCH-Copula-Simulation-of-Public-Plan-Funded-Ratios
Built an end-to-end stochastic risk model for public pension funds using the Public Plans Data dataset, simulating funded ratio distributions across 2017–2024 under both volatility-clustering and constant-variance regimes to quantify tail risk in underfunded systems.

Methods & Technical Work:
	•	Constructed an expanding-window GARCH(1,1) pipeline with skewed Student-t innovations across four asset classes (equities, fixed income, real estate, private equity), re-fitting each year on data through XX-1 to simulate year XX out-of-sample
	•	Validated GARCH fits via Ljung-Box tests on standardized residuals and squared residuals — all assets passed across all years; tracked α and β stability across windows to detect structural breaks
	•	Modeled cross-asset dependence using a 4-dimensional Student-t copula fit to GARCH-filtered uniform marginals via maximum likelihood, capturing tail co-movement that Gaussian copulas miss; tracked correlation evolution (e.g., EQ-FI: −0.28 → −0.10 over 2017–2024)
	•	Simulated 10,000 annual portfolio paths per year by chaining 12 monthly GARCH returns with copula-correlated innovations; applied duration-based liability revaluation (D_liab = 13) driven by simulated FI returns, linking asset and liability dynamics
	•	Computed VaR(5%) and CVaR(5%) on funded ratio distributions; GARCH-Copula produced systematically lower tail estimates than constant variance (mean VaR gap: 4.8 pp, mean CVaR gap: 7.4 pp, max CVaR gap: 12 pp), indicating that volatility clustering materially concentrates left-tail risk

Tools: R (rugarch, copula, quantmod, ggplot2), Monte Carlo simulation, duration-based liability modeling

Key Finding: Constant-variance models structurally understate pension tail risk. Volatility clustering — especially around 2020 and 2022 shock periods — compresses the funded ratio distribution’s left tail in ways that matter for actuarial stress testing and contribution policy design.
