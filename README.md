# Project Name
> Multiple Linear Regression Model for the prediction of demand for shared bikes

## Table of Contents
* [Problem Statement](#Problem-Statement)
* [Data Understanding](#data-understandin)
* [Data Cleaning](#data-cleaning)
* [Analysis](#analysis)
* [Conclusions](#conclusions)

<!-- You can include any other section that is pertinent to your problem -->

## Problem Statement
- A US bike-sharing provider BoomBikes has recently suffered considerable dips in their revenues due to the ongoing Corona pandemic. The company is finding it very difficult to sustain in the current market scenario. So, it has decided to come up with a mindful business plan to be able to accelerate its revenue as soon as the ongoing lockdown comes to an end, and 		the economy restores to a healthy state. 
- Based on various meteorological surveys and people's styles, the service provider firm has gathered a large dataset on daily bike demands across the American market based on some factors. The company wants to know:

  - Which variables are significant in predicting the demand for shared bikes.
  - How well those variables describe the bike demands

## Data Understanding
- day.csv have the following fields:
	- instant: record index
	- dteday : date
	- season : season (1:spring, 2:summer, 3:fall, 4:winter)
	- yr : year (0: 2018, 1:2019)
	- mnth : month ( 1 to 12)
	- holiday : weather day is a holiday or not (extracted from http://dchr.dc.gov/page/holiday-schedule)
	- weekday : day of the week
	- workingday : if day is neither weekend nor holiday is 1, otherwise is 0.
	+ weathersit : 
		- 1: Clear, Few clouds, Partly cloudy, Partly cloudy
		- 2: Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist
		- 3: Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain + Scattered clouds
		- 4: Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog
	- temp : temperature in Celsius
	- atemp: feeling temperature in Celsius
	- hum: humidity
	- windspeed: wind speed
	- casual: count of casual users
	- registered: count of registered users
	- cnt: count of total rental bikes including both casual and registered
- It contains 730 rows and 16 columns

## Data Cleaning and preparation
- No Null values found.
- Keeping cnt column and removing registered and casual columns as they are directly related
- Dummy variables are created for season, month, weekday and weather
- Data is split with train size of 0.7
- 'cnt','hum','temp','windspeed' are normalized using MinMaxScaler

## Analysis
- 2019 has seen an increase in total rentals.
- 2018 has peak rental counts in May,June,July where as 2019 has seen spike in August, September,October
- 2018 has almost same distribution of rental counts through out the week where as 2019 has seen little spike during Friday and Saturday
- OLS regression model showed 21 columns with high values of VIF. Took RFE approach to eliminate columns with high values of multicollinearity
- Columns dropped for multicollinearity - 'April', 'December', 'February', 'Friday', 'Heavy rain', 'July', 'June','March', 'May', 'November', 'Saturday', 'Thursday', 'Tuesday','Wednesday'
- RSquare score after RFE - 0.8475442609382655
  
## Conclusions
- Test set RSquare shows that the model is generalized enough even with high train RSquare and F-Statistic
  - Train Set
    - RSquare : 0.85
      F - Statistic : 196.6
    - Test Set
      RSquare : 0.82
      Variation with test set - 3 %
- Equation of best fit line from model is
  𝑐𝑛𝑡=0.0557∗𝐴𝑢𝑔𝑢𝑠𝑡−0.247∗(𝐿𝑖𝑔ℎ𝑡𝑆𝑛𝑜𝑤)−0.0568∗𝑀𝑖𝑠𝑡+0.0385∗𝑂𝑐𝑡𝑜𝑏𝑒𝑟+0.125∗𝑆𝑒𝑝𝑡𝑒𝑚𝑏𝑒𝑟−0.0557∗𝐻𝑜𝑙𝑖𝑑𝑎𝑦−0.17∗ℎ𝑢𝑚+0.1049∗𝑠𝑢𝑚𝑚𝑒𝑟+0.53∗𝑡𝑒𝑚𝑝−0.185∗𝑤𝑖𝑛𝑑𝑠𝑝𝑒𝑒𝑑+0.135∗𝑤𝑖𝑛𝑡𝑒𝑟+0.0442∗𝑤𝑜𝑟𝑘𝑖𝑛𝑔𝑑𝑎𝑦+0.229∗𝑦𝑟

- Features having positive coefficients
    - August,October,September,Sunday,Summer,temp,winter,working day, year
- Features having negative coefficients
- Light snow, Mist, holiday,hu, windspeed


## Technologies Used
- numpy - version 1.19.2
- pandas - version 1.1.3
- matplotlib - version 3.3.2
- seaborn - version 0.11.0


## Contact
Created by [@SuryaGopasana] - feel free to contact me!
