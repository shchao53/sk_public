I did my Insight project with a startup, Fleetr*. Fleetr delivers rental cars. A customer can book a car through their mobile app and they will have an agent deliver the car directly to the customer at the given time and location. They are more like a mobility provider. They don’t own cars. They partner with local car rental companies to server their customers. 

*This is a fake name. The company wants to remain anonymous. 


# The problem 

The biggest challenge they are facing right now is to predict the demand at a given time, which is extremely important to the ground logistics of an on-demand company like Fleetr. This is a very challenging problem considering how many factors could affect the demand, and how those factors vary from region to region. Currently, they don’t have any prediction system working. They get the cars from their partner companies according to the booking requests. If they don’t have enough in their parking lot, they will try to get more from their partners. This is where I can help them – making a predictive model. Anything is better than nothing!  


# The data
Fleetr gave me their booking data since Feb 2016. They changed their target customers and local operation dramatically in late May. This change of business was clearly reflected in the booking data. Therefore, I used the data after the change for model building. The data contains the delivery time and location for each booking, along with other information like the model of the car, the price, the booking time, customer ID, etc. 


## Data cleaning 
As many other data scientists, I spent more than half of my time cleaning the data and transforming the data into the right format for later model training. There were some noises in the data I removed beforehand. For example, unlike the majority of customers requested for sedans, occasionally there were people renting trucks or 15 seaters. I removed these booking records as noises.     

## Regional segmentation
Most of Fleetr’s bookings came from their biggest market – Los Angeles. They have total 3 local hubs in LA. Hubs are parking facilities in which they store cars rented from partner rental companies in advance. At the requested delivery time, Fleetr delivers a car from the nearest hub to wherever the delivery location of the booking is. Based on this operation rule, I first separated the data into three subsets, according to the distance between the delivery location and the hub location, as shown in the figure below. The distance was driving distance calculated using Google Distance Matrix API.  

  By looking at the geographical distribution of the delivery locations, along with the domain knowledge of Los Angeles, one can easily point out the difference of booking between three hubs. Hub1 is close to downtown LA. Hub2 covers Hollywood, where had a lot of delivery records. Hub3 covers Santa Monica and LAX airport.  


## The daily booking number
I grouped the data by date to get the daily booking data. The data shows a clear seasonality, which corresponds to the weekly booking pattern. Usually, the booking number increases over the weekend. Friday is the busiest day of a week. I didn’t see a clear monthly trend. 

The three hubs also showed slightly different booking trends. Hub1 had less booking comparing to hub2 and hub3. Hub3 had a more apparent seasonality and higher spikes during the holiday weekends, which was attributed to traveler customers. 
 

# The model 
From the time series data, I generated N features, which includes day of week, week of month, prior-day price, etc. I also introduced external signals like holiday information and local weather. I then trained three linear regression models separately for three hubs. 

 

# Summary
To sum up, I used the above pipeline to build predictive models for Fleetr to predict the booking demand in their hubs in LA, using the historical booking data since late May. The biggest limitation I had is the problem of “small data” – I had only three months of data. There was no data covering the same season that I can validate. Training data on the summer season was especially risky, since summer is when students go home and lots of tourists visiting popular tourist spots like Hollywood. 

I delivered the model to Fleetr and they are about to test it. They can also re-train the model once they have more data in the following months. Hopefully that can help improve the model performance further. There were two other recommendations I gave Fleetr, which could potentially be future data science project they can work on: 1) Adapt surge pricing model to compensate the underestimation of demand sometimes, especially over the weekend; 2) Log more customer information when on-boarding for customer segmentation. For example, age could be a good indicator of students, or locals and travelers could be separate by billing addresses, etc. For now, there is no luxury in terms of data points to the build in such a granular way, but these are all fun projects to work on in the future. ☺
 
---
I used Pandas for data mugging, Google Distance Matrix API for distance calculation, scikit-learn and StatsModel for model building, and Folium for mapping.
