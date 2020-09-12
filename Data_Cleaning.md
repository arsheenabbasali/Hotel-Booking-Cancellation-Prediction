## [Overview](README.md)

# Data Cleaning and Preparation

## Data Exploration

## Feature Selection

## Models and Pipelines

## Deep Learning

## Recommendations

In this section, we begin with loading the dataset and finding the number of *Null* values in each column of the dataset and replacing it with suitable alternative.

* So, Let's Begin!!!!!*

#### Loading Data
```Python
hotel_bookings=pd.read_csv("hotel_bookings.csv")                                        
hotel_bookings.head(10)
```
|hotel|	is_canceled	|lead_time|	arrival_date_year|	arrival_date_month|	arrival_date_week_number|	arrival_date_day_of_month|	stays_in_weekend_nights|	stays_in_week_nights|	adults|	...	deposit_type|	agent	|company|	days_in_waiting_list|	customer_type|	adr	|required_car_parking_spaces|	total_of_special_requests	|reservation_status	|reservation_status_date|
|--------------|-----|----------|----------|-----------|---------------|-----------|-----------|------------|------------|--------------|----------|--------|------------|----------|-----------|---------|-----------|------------|-------|
|Resort Hotel|	0	|342|	2015	|July	|27|	1|	0	|0|	2	|...	No Deposit|	NaN	|NaN|	0|	Transient|	0.0|	0	|0|	Check-Out	|2015-07-01|
|Resort Hotel|	0	|737|	2015	|July	|27|	1|	0|	0|	2|	...	No Deposit|	NaN|	NaN|	0|	Transient|	0.0|	0|	0|	Check-Out|	2015-07-01|
|Resort Hotel|	0	|7	|2015	|July	|27|	1|	0	|1|	1	|...	No Deposit|	NaN	|NaN|	0	|Transient|	75.0|	0	|0|	Check-Out|	2015-07-02|
|Resort Hotel|	0	|13	|2015	|July	|27|	1|	0	|1|	1	|...	No Deposit|	304.0|	NaN|	0|	Transient|	75.0|	0|	0	|Check-Out|	2015-07-02|
|Resort Hotel|	0	|14	|2015	|July	|27|	1|	0	|2|	2	|...	No Deposit|	240.0	|NaN|	0	|Transient	|98.0	|0|	1	|Check-Out|	2015-07-03|
5 rows × 32 columns
