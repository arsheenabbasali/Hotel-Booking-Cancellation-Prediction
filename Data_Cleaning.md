## [Overview](README.md)

# Data Cleaning and Preparation

## Data Exploration

## Feature Selection

## Models and Pipelines

## Deep Learning

## Recommendations

In this section, we begin with loading the dataset and finding the number of *Null* values in each column of the dataset and replacing it with suitable alternative.

*So, Let's Begin!!!!!*

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

Total:5 rows × 32 columns

### Data Cleaning
```Python
# Number of Null Values in data:
hotel_bookings.isna().sum()
```
```{.python .output}
  
hotel                                  0
is_canceled                            0
lead_time                              0
arrival_date_year                      0
arrival_date_month                     0
arrival_date_week_number               0
arrival_date_day_of_month              0
stays_in_weekend_nights                0
stays_in_week_nights                   0
adults                                 0
children                               4
babies                                 0
meal                                   0
country                              488
market_segment                         0
distribution_channel                   0
is_repeated_guest                      0
previous_cancellations                 0
previous_bookings_not_canceled         0
reserved_room_type                     0
assigned_room_type                     0
booking_changes                        0
deposit_type                           0
agent                              16340
company                           112593
days_in_waiting_list                   0
customer_type                          0
adr                                    0
required_car_parking_spaces            0
total_of_special_requests              0
reservation_status                     0
reservation_status_date                0
dtype: int64
```


