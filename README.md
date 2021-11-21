# Capital Bikeshare Data Mining Project
Data mining process for a group project about the Capital Bikeshare data. Developed in Python using Jupyter Notebook.

# Overview
The purpose of this project was to process the data to build a model to predict bike availability for any station at any given time. The data was pulled from the Capital Bikeshare data repository.

# Data
Ride data from December 2018 to December 2019 with columns contained location, time, and user information.

# Challenges
There were many challenges that made this particular data cleaning process very difficult which were:
1. **Ride Data**: The data was structured so that every row was a particular ride, with information about their starting and ending location. Because the data needed to be organized per station, a lot of manipulation was required to transform the data into this form.
2. **Van reshuffling**: One of the biggest problems was the van reshuffling. Like any other rideshare comapny, there is a van that goes around to distribute bikes in the appropriate places. However, this information was not present in our data so the reshuffling had to be infered from missing data (aka if the start and end locations for a particular bike did not match).
3. **What is bike availability?**: Another challenge was defining bike availability since the number of arrivals did not accurately describe the number of bikes at any station. In the end, bike availability was defined as the net difference between arrivals and departures after accounting for the number of bikes in the previous hour.
4. **How many bikes were there to begin with?**: The calculation for bike availability relies on knowing the number of bikes in the immediate past or knowing the 'starting point'. Since the original starting point is unknown, the starting number of bikes was estimated using the past month. A whole month was required since some stations rarely have rides so a larger time period was needed to capture all the bikes/stations. Using the past month, the last location for every bike was calculated and deemed the starting point.
5. **Estimated starting points**: To calculate bike availability, the cumulative sum was utilized to keep track of the prior number of bikes. However, this cumulative sum was sometimes negative or very large since the starting number of bikes was an estimation. 
6. **Large events**: Occasionally, there were large spikes and dips in stations at random times. Further investigation found that Capital Bikeshare sometimes expands stations for large events to leverage large crowds. To account for the large events and estimate bike availability, the cumulative sum was capped to the capicity for a particular station and was limited to 0 if the sum was negative.
