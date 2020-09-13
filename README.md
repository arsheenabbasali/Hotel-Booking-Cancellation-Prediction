# Overview

## [Data Cleaning and Preparation](Data_Cleaning/Data_Cleaning.md)

## [Data Exploration](Data_Exploration/Data_Exploration.md)

## [Feature Selection](Feature_Selection/Feature_Selection.md)

## [Models and Pipeline](Pipeline.md)

## [Deep Learning](Deep_Learning/Deep_Learning.md)

### Introduction
The rate of cancellation for bookings in the hospitality industry is quite high in the competitive market offering no deposit bookings. Once the booking has been cancelled, there is almost nothing to be done at the end of hotel. This kind of setting creates discomfort and monetary losses for many hotels and creates a demand to take prior precautions for high number of cancellations. Therefore, predicting bookings that can be cancelled and preventing these cancellations will create value for hospitality industry. 
With the help of this project, we will try to explain how future cancelled hotel bookings can be predicted in advance with the help of machine learning methods. Also, what measures and steps can be implemented for reducing their impact on industry’s revenue.

### Research Problem Statement
In this proposed project, we will be predicting whether a booking made in a hotel can be cancelled in future or not. For this, we have developed models that will identify and flag bookings with high cancellation probability by understanding the trends and features associated with it. Thus, hotels can act on these booking to contain the associated revenue losses. 
This kind of prediction will help in producing better net demand forecasts, improve overbooking/cancellation policies, and have more assertive pricing and inventory allocation strategies. This analysis can also be used by hotels to identify their loyal customers who never cancel their booking and can provide loyalty benefits. 

### Data Acquisition
For this project, we are using **[Hotel Booking Demand](https://www.kaggle.com/jessemostipak/hotel-booking-demand)** from Kaggle. This data set contains booking information for a city hotel and a resort hotel and includes information such as when the booking was made, length of stay, the number of adults, children, and/or babies, and the number of available parking spaces, among other things. All personally identifying information has been removed from the data. 
The data is originally from the article *Hotel Booking Demand Datasets*, written by Nuno Antonio, Ana Almeida, and Luis Nunes for Data in Brief, Volume 22, February 2019.

### References
* Zeytinci, E. (2019, December 30). Predicting Hotel Cancellations with Machine Learning [online](https://towardsdatascience.com/predicting-hotelcancellations-with-machine-learning-fa669f93e794)
* Antonio, N., Almeida, A. D., & Nunes, L. (2019). Hotel booking demand datasets. Data in Brief, 22, 41–49. doi: 10.1016/j.dib.2018.11.126 
* Mostipak, J. (2020, February 13). Hotel booking demand [online](https://www.kaggle.com/jessemostipak/hotel-booking-demand) 
* Marcuswingen. (2020, March 6). EDA of bookings and ML to predict cancelations [Online](https://www.kaggle.com/marcuswingen/eda-of-bookings-and-ml-topredict-cancelations) 

#### Libraries Used
`Python`
* [Python Standard Library](https://docs.python.org/2/library/): Built in python modules.
* [Numpy](http://www.numpy.org/): Scientific computing with python.
* [Pandas](http://pandas.pydata.org/): Data analysis tools.
* [matplotlib](https://matplotlib.org/): Static, animated, and interactive visualizations.
* [Seaborn](https://seaborn.pydata.org/): Python data visualization library.
* [Pyspark](https://spark.apache.org/docs/latest/api/python/pyspark.html): PySpark is the Python API for Spark.
