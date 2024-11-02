# Energy_Demand-_Forecasting
 An Advanced Data Analytics Approach to Discover Trends and Patterns in Energy Consumption, Demand, and Actual Demand, and Predicting Actual Demand with Forecast Uncertainties

### In recent years the photovoltaic (PV) industry has proliferated and the scale of grid-connected PV continues to increase.
### The random and fluctuating nature of PV power output is a major issue concerning power systems' safe and stable operation (Rafique et al., 2022).
### Accurate actual demand prediction including the contribution of PV-generated power in smart grids helps to reasonably arrange the power system scheduling plan and realise the real-time balance of power generation and power consumption, to ensure that the power system can operate reliably, safely, and stably(Hongyang et al., 2023, Hosna, et al., 2022).
### Because of the intermittent and uncontrollable nature of renewables (including solar energy) it is crucial for utilities to quantify the uncertainty in the predicted future generation and demand(Chengiliang et al., 2023).

Consumption; is the cumulative amount of electricity used over a period of time (in MWh).
Demand: demand refers to the immediate rate at which the energy is used (in MW).
As the consumption is the total amount of energy consumed over a specific period of time, 
the demand will be calculated by dividing consumption over the period of time. Since the Meter Point 
Enumeration is Half_Hourly, in order to calculate the demand from consumption one needs to divide the 
consumption by 0.5(h);
			Energy (MWh) = Power (MW) x Time(Hours) 
	As a result:                    Demand(MW) = Consumption(MWh) / 0.5 

Actual Demand: The difference between Demand and PV power

In smart grids, the integration of renewable energies including solar energy (PV-generated) incorporates fluctuations in the power supply. As a result, it is crucial to forecast the actual demand as the difference between the demand and the PV generated to ensure that smart grids can operate reliably, safely, and stably.

This way actual demand is defined as :     

			Actual Demand = Demand(MW) - PV(MW)

1) Weather data set including the time series of temperature; (synth_weather.csv): `region`, `mpe_time`, `observation_value`. Represents temperature values at different time points and observation_value represents Temperature in Celsius. 
 PV-generated dataset including the time series for the PV power and the; (synth_pv): This file contains PV generation. `region`, `mpe_date`, `mpe_time`, `PV`. Represents PV generation in MW. 
The demand(consumption) dataset having the half-hourly measured consumption; Data (synth_actual.csv): `region`, `mpe_date`, `mpe_hh`, `mpe_time`, `unit`, `demand`. Please note that demand here represents energy consumption (in MWH). mpe_hh here represents the half hour of day ranging from 1 to 48. 

* The is no null value in the observations.
* There is no duplicated observation in the datasets.
* All data is collected from the same region.
* The datasets are merged with left joined on demand data .
* The merged data frame has 52511 rows (observations).

  ## Feature Engineering
* Demand (as the consumption) is converted to demand_MW as the average half_hour rate by multiplying consumption by two.
* Actual demand is calculated by calculating the difference between demand_MW and PV(MW).
* Since the time columns include the date, the date columns are removed, and date-time columns are created(parsing data).
* The temporal features are extracted from data-time column creating hour, day of week, and month columns.



# Results and Conclusions
* The Simple Linear Regression model served as a baseline, yielding an MAE of 790.02 and RMSE of 1021.03, with an 𝑹^𝟐 of 0.2007. While offering a straightforward approach, this model struggled to capture the complexity in the data.

* The XGBoost model significantly improved performance with an MAE of 479.99, RMSE of 612.31, and 𝑹^𝟐 of 0.7125, demonstrating that more sophisticated machine learning methods, particularly those capable of capturing non-linear relationships, are better suited to this type of forecasting problem.

* The Quantile Regression model, providing a 90% coverage of the forecast intervals, effectively captured the range of possible outcomes, offering valuable insights into uncertainty.
  
* The coefficients for features like PV generation, temperature, and hour_sin show that these variables significantly influence the actual demand prediction. The higher the temperature and the hour of day, the more variation in demand is observed, with weekend days contributing to reduced demand.

## Uncertainities Calculated and Visualised!

![image](https://github.com/user-attachments/assets/6ded744f-b7f7-4b87-92b6-fb5a1c07899e)

![image](https://github.com/user-attachments/assets/9af3c7c0-d014-4b9b-9d34-f55c33dbf5ea)







