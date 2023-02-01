# Monte Carlo Simulation to determine the Optimal Portfolio Weights
In this project, I use monte-carlo simulations to select the optimal portfolio weights in a basket of securities that yields the highest risk-adjusted return.
There are two key classes: **Security** and **Portfolio**.  Securities are individual assets for which we can gather historic prices using the [Alphavantage](https://www.alphavantage.co/) API.  Portfolios consist of baskets of securities with their associated weights.  The appendix contains details on the attributes and methods used in each class

We can calculate the mean return, risk, and covariance between each security in the portfolio


## Security Prices
![image](https://user-images.githubusercontent.com/1649676/215936189-a17f9410-1bc5-4f7e-a7c0-63912f9bdfea.png)
![image](https://user-images.githubusercontent.com/1649676/215936252-53c6971d-ecd0-43c5-b9f4-a51713f9e08f.png)


## Efficient Frontier 

![image](https://user-images.githubusercontent.com/1649676/215935779-b0dfb918-84ea-48d7-be5b-2283c42873ba.png)



### Most Efficient Weights
![image](https://user-images.githubusercontent.com/1649676/215935819-b8f1c4d2-ce73-4f5e-a314-5f453cce8891.png)



## Monte Carlo Simulation: Expected Risk, Return and Sharpe-Ratio

### Simulation Paths
![image](https://user-images.githubusercontent.com/1649676/215935877-7b226d6d-ae27-426f-b4d2-e2457db5a178.png)


### Return/Risk Distributions
![image](https://user-images.githubusercontent.com/1649676/215935930-476ef8bc-76f0-46be-b2ce-83136ebcd6a5.png)



### Expected Portfolo Value after 10 Years
![image](https://user-images.githubusercontent.com/1649676/215936001-fc8fb706-6e68-4d74-afb4-7907f1f7c063.png)



## Appendix

#### Security Attributes
+ name = security name
+ identifier (used to query alphavantage for prices)
+ mu (mean return)
+ sigma (mean standard deviation of returns)
#### Security Methods
+ generate_returns(self.mu, self.sigma, self.n). This function simulates returns from the normal distribution based on mu and sigma

#### Portfolio Attributes
A portfolio holds securities at specific weights
+ name = portfolio name
+ securities = a list of securities
+ target_weights = a list of weights associated with each security 
+ portfolio_value = starting value of the portfolio
+ rf = risk free rate (decimal format)
+ cov = covariance matrix of the returns of each security in the portfolio
+ simulation_results = A dictionary of various outputs from the monte carlo simulation
+ mean_return = Mean return of the portfolio. Calculated by the simulation
+ mean_volatility = Mean standard deviation of returns of the portfolio - calculated by the simulation
+ sharpe_ratio = sharpe ratio of the portfolio - calculated by the simulation
+ expected_values = expected values of the portfolio - calculated by the simulation
#### Portfolio Methods
+ calc_sharpe_ratio(self): Calculate the sharpe-ratio of the portfolio
+ calc_covariance(self): Calculate the covariance between security returns
+ convert_from_annual(self,metric,freq,measure): convert from annual to another frequency (return, risk)
+ convert_to_annual(self,ret,vol,freq,periods): convert return/risk to annual from another frequency
+ get_security_prices(self,yr, key, plot=False,requests_per_min=5): get security prices from alpha vantage
+ run_simulation(self,simulations, years, frequency,robust=False): run the monte carlo simulation
+ get_expected_values(self): get the expected values from the simulation
+ weight_combinations(self, total_portfolio_wt, min_security_wt, max_security_wt, weight_increment): get all possible portfolio weight combinations
+ build_efficient_frontier(self, total_portfolio_wt, min_security_wt, max_security_wt, weight_increment, num_sims, years, frequency, verbose=0): Build the efficient frontier
+ get_optimal_portfolios(self, top_n): get the optimal portfolio from the efficient frontier
+ plot_boxplots(self): plot return/risk in boxplots
+ plot_histograms(self): plot return/risk in histograms
+ plot_portfolio_simulations(self): plot the simulation results
+ plot_efficient_frontier(self): plot the efficient frontier






