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
Getting number of *Null* vallues in each column
```Python
# Number of Null Values in data:
hotel_bookings.isna().sum()
```
There seems that `country` attribute has *488* null values and `children` attribute has *4* null values. Other than that, attribute `agent` and `company` has *16340* and *112593* null values respectively.

Now, replacing null values in `children` attribute with `0` because average of the same column is nearly `0`.
```python
hotel_bookings['children'].fillna(0,inplace=True)
```
Replacing `Null` values in `country` attribute with `Unknown` text for each of analysis.
```Python
hotel_bookings['country'].fillna('Unknown',inplace=True)
```
As the dataframe size is huge, a step is taken here to convert the data-types of each column to *Category* to reduce the dataframe size. The main motive of this step is to reduce the processing time for the data cleaning.
```Python
hotel_bookings['hotel']=hotel_bookings['hotel'].astype('category')
hotel_bookings['is_canceled']=hotel_bookings['is_canceled'].astype('category')
hotel_bookings['meal']=hotel_bookings['meal'].astype('category')
hotel_bookings['country']=hotel_bookings['country'].astype('category')
hotel_bookings['market_segment']=hotel_bookings['market_segment'].astype('category')
hotel_bookings['distribution_channel']=hotel_bookings['distribution_channel'].astype('category')
hotel_bookings['is_repeated_guest']=hotel_bookings['is_repeated_guest'].astype('category')
hotel_bookings['reserved_room_type']=hotel_bookings['reserved_room_type'].astype('category')
hotel_bookings['deposit_type']=hotel_bookings['deposit_type'].astype('category')
hotel_bookings['customer_type']=hotel_bookings['customer_type'].astype('category')
hotel_bookings['required_car_parking_spaces']=hotel_bookings['required_car_parking_spaces'].astype('category')
hotel_bookings['total_of_special_requests']=hotel_bookings['total_of_special_requests'].astype('category')
hotel_bookings['reservation_status']=hotel_bookings['reservation_status'].astype('category')
hotel_bookings['reservation_status_date']=hotel_bookings['reservation_status_date'].astype('datetime64[ns]')
hotel_bookings['children']=hotel_bookings['children'].astype('int64')
hotel_bookings['stays_in_weekend_nights']=hotel_bookings['stays_in_weekend_nights'].astype('category')
hotel_bookings['stays_in_week_nights']=hotel_bookings['stays_in_week_nights'].astype('category')
hotel_bookings['assigned_room_type']=hotel_bookings['assigned_room_type'].astype('category')
hotel_bookings['arrival_date_month']=hotel_bookings['arrival_date_month'].astype('category')
```
During this preprocessing, we found that there are some rows with `children`, `adults` and `babies` = 0, in short with no guests in the booking. This is a false booking and not needed in the further analysis. So we decided to remove all these rows.
``` Python
hotel_bookings=hotel_bookings.drop(hotel_bookings[(hotel_bookings['children']==0) & (hotel_bookings['adults']==0) & (hotel_bookings['babies']==0)].index)
```
Converting Day, Month, Year into a single arrival date for ease of analysis.
```Python
month_number={'January':1,
             'February':2,
             'March':3,
             'April':4,
             'May':5,
             'June':6,
             'July':7,
             'August':8,
             'September':9,
             'October':10,
             'November':11,
             'December':12}

hotel_bookings['arrival_date_month_number']=hotel_bookings['arrival_date_month'].apply(lambda x:month_number[x])
hotel_bookings['arrival_date_month_number']=hotel_bookings['arrival_date_month_number'].astype('category')

hotel_bookings['date_of_arrival']=pd.to_datetime(hotel_bookings['arrival_date_year'].astype(str)+hotel_bookings['arrival_date_month_number'].astype(str)+hotel_bookings['arrival_date_day_of_month'].astype(str),format="%Y%m%d")
```
This above convertion made us realize that there are one day stays too!!! which we have found below:
```Python
# Number of one day stays
hotel_bookings[(hotel_bookings['stays_in_week_nights']==0) & (hotel_bookings['stays_in_weekend_nights']==0)]['hotel'].count()
```
The number of one day stays came out to be *645*.

There are some bookings which has no date for `day_of_leaving`, it means that there is no checkout for the booking and it has either been *Cancelled** or there is *No Show*. So we have replaced `None` in `day_of_leaving` for all these bookings.
```Python
hotel_bookings.loc[hotel_bookings['reservation_status']!='Check-Out','day_of_leaving']=None
```
For the ease of analysis, we decided to create two more attributes to the data.
* `total_night_stays`: this attribute signifies the number of night stays for a booking. It is of integer data-type. This column is calculated by adding data of two other attributes i.e. `stays_in_week_nights` and `stays_in_weekend_nigts`.
```Python
hotel_bookings['total_night_stays']=hotel_bookings['stays_in_week_nights'].astype(int)+hotel_bookings['stays_in_weekend_nights'].astype(int)
```
* `one_day_stay`: this attribute is created to handle one day stays. It is a binary attribute with two values either *Yes* or *No*
```Python
hotel_bookings.loc[(hotel_bookings['reservation_status']=='Check-Out')&(hotel_bookings['total_night_stays']==0),'One_day_stay']='Yes'
hotel_bookings['One_day_stay']=hotel_bookings['One_day_stay'].astype('category')
```
