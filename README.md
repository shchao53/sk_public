I did my insight project with a startup, Fleetr*.
Fleetr delivers rental cars.
A customer can book a car through their mobile app and they will have an agent deliver the car directly to the customer at the given time and location.
They are more like a mobility provider. They don’t own cars. They partner with local car rental companies to server their customers. 

###### *a fake name becuase the company wants to remain anonymous

# The problem
The biggest challenge they are facing right now is to predict the demand at a given time, which is extremely important to the ground logistics of an on-demand company like Fleetr. This is a very challenging problem considering how many factors could affect the demand, and how those factors vary from region to region. Currently, they don’t have any prediction system working. They get the car from their partner companies according to the booking request. If they don’t have enough in their parking lot, they will try to get more from their partners. This is where I can help them – making a predictive model. Anything is better than nothing!

# The data
Fleetr gave me their booking data since Feb 2016. They changed their target customers and local operation dramatically in late May. This change of business was clearly reflected on the booking data. Therefore, I used the data after the change for model building. The data contains the delivery time and location for each booking, along with other information like the model of the car, the price, the booking time, customer ID, etc.

## Data cleaning
As many other data scientists, I spent more than half of my time cleaning the data and transform the data into right format for later model training.

## Regional segmentation
Most of Fleetr’s bookings came from their biggest market – Los Angeles. They have total 3 local ‘hubs’ in LA. Hubs are parking facilities in which they store cars from partner rental companies in advance. When receiving a booking, Fleetr delivers a car from the nearest hub to wherever the delivery location of the booking. Based on this operation rule, I first separated the data into three subsets, according to the distance between the delivery location and the hub location, as shown in the figure below. The distance was driving distance, which was calculated using Google Distance Matrix API.
