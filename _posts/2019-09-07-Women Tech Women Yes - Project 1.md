### Introduction
This project was about helping an organization called Women Tech Women Yes. The company is organizing a gala (festival) and they want to sign up people to attend to this gala. So they decided to send some of their employees to subway stations to collect sign ups from people. 
We have been asked to help the company with their decision. And our role will be to tell the company which station they should put their employees in. and since most of the stations are large and they contain many units, we will tell the company also where exactly their employees should be at. And most importantly when they should send their employees. So to recap our role, we will tell the company what is the best place and when is the best time to send their employees to collect the sign ups from the subway stations. 

### Strategy
So we stated the project by defining the targeting strategy. And based on the data that we had and delivery time of the project we decided that we want to target as many people as possible to increase the chances of sign ups. So we are going to look for the busiest stations at the busiest times. 

### Approach
---
#### Collecting the data
we collected the data from the [Metropolitan Transportation Authority](http://web.mta.info/developers/turnstile.html) website. It is free for everyone to look at. The figure below shows an the first four rows in the data set. 
![Image test]({{ site.url }}/images/head4.png)

#### Understanding the data
In this step we started building the domain knowledge needed for this project. And most importantly understanding what the meaning of each column in our data set. And after some filtering of the columns that we don’t need. We ended up with a data set that contains the following columns (station name, unit, subunit channel position, date, time, entries and exits).  

#### Analyzing the data
In this step we cleaned the data and then analyzed it to get the busiest stations at the busiest times. It is important to note that we were determining if a station is busy or not by seeing the total flow of the station (number of entries + number of exits) 

Here we can see the top 5 busiest stations 
![Image test]({{ site.url }}/images/Picture1.png)

Here we can see the busiest units in the one of the stations
![Image test]({{ site.url }}/images/Picture2.png)

### Results
We got the results for the busiest stations and their busiest times. Lets take the busiest station (according to our results) as an example

Station | Unit | Day | Hours
------------ | -------------| -------------| ------------- 
34 ST-PENN STA | R012 | Tuesday, Monday, Wednsday and Thursday | 8:00 AM, 12:00 PM, 4:00 PM

Finally, we solved all the business problems except one. which is how will the organization distribute their employees between the stations. So we did a final analysis on the top 5 stations, and we calculated their importance by percentage. So we would recommend to take this final analysis into consideration when the workers are distributed. The figure below shows the top 5 stations importance percentages.
![Image test]({{ site.url }}/images/piechart.png)

