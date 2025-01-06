
# Conclusion

  

### Key Findings from EDA

- The target variable has a very long tail and is really skwed to the right, I decided to apply a `log transformation` to it.
- I investigated the possibility of having outliers in the Target Variable.
- The higher the temperature, the slightly higher the demand.
- `temp` and `atemp` are linearly correlated with each other which can cause problem for models similar to `LinearRegression`
-----------
- Categorical Features:
	1. By Season, 1 = spring, 2 = summer, 3 = fall, 4 = winter
	    - Demand is higher in summer and fall, and lower in winter, it is the lowest in spring.

	2. By Holiday, 0 = no holiday, 1 = holiday
	    - No noticeable difference in demand between holidays and non-holidays.

	3. By Workingday, 0 = non-working day, 1 = working day
	    - No noticeable difference in demand between working days and non-working days.

	4. By Weather
		1. Clear, Few clouds, Partly cloudy, Partly cloudy (Sunny)
		2. Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist (Foggy)
		3. Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain + Scattered clouds (Rainy)
		4. Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog (Heavy Rain)

		    - Demand is the highest in Sunny and Foggy weather, and the lowest in Rainy. It's weird that it's higher in Heavy Rain than in Light Rain.
  
--------

- Hour:
	- During morning demand is highest around 8am, probably people going to work.

	- Demand is highest in the afternoon around 4pm to 7pm, probably a combination of people going home from work, and people going out for a ride in the sweet afternoon.
-----------
- Correlation Analysis:

	- Again, temp and atemp are almost perfectly correlated, we'll need to remove one of them.

	- Demand is slightly linearly correlated with temp, atemp, and hour.

	- Demand is not linearly correlated windspeed, season, holiday, workingday, or weather.

	- Demand is slightly negatively correlated with humidity.
	- ---------------
#### 1. The First Model with some Feature Engineering:

- Metrics:
	* MAE: 112.1736
	* RMSE: 163.3219
	* R^2: 0.1070

- Residual Statistics:
	* Mean Residual: 53.7632
	* Residual Variance: 23794.4698


#### 2. The Second Model without outliers
- Metrics:
	* MAE: 106.6959
	* RMSE: 151.1721
	* R^2: 0.0614
	* 
- Residual Statistics:
	* Mean Residual: 58.8030
	* Residual Variance: 19404.3771
  

#### 3. The Third Model without Feature Engineering

- Metrics:
	* MAE: 112.1916
	* RMSE: 167.5386
	* R^2: 0.1088

- Residual Statistics:
	* Mean Residual: 58.6880
	* Residual Variance: 24636.2219
  
---------------

  Based on the metrics and residual statistics:

1.  **Model 2 without outliers**  performs the best overall:
    
    -   It has the  **lowest MAE (106.6959)**  and  **lowest RMSE (151.1721)**, indicating better prediction accuracy and fewer large errors.
        
    -   It also has the  **lowest residual variance (19404.3771)**, suggesting more consistent predictions.
        
    -   Although its  **R² (0.0614)**  is lower than the other models, the improvement in MAE and RMSE makes it the preferred choice.
        
2.  **Model 1 with feature engineering**  and  **Model 3 without feature engineering**  perform similarly:
    
    -   Both have comparable MAE, RMSE, and R² values, but Model 1 has a slightly lower mean residual (53.7632 vs. 58.6880), indicating less bias.
        
    -   However, neither outperforms Model 2 without outliers.
