---
layout: post
title: Geocoding in Python
modified:
categories: blog/
excerpt:
tags: [python, data wrangling, geocoding, pandas]
image:
  feature:
date: 2017-01-21T12:44:00-00:00
---



#### I recently had to extract zip codes from a set of points described by latitude and longitude to be able to analyze intra-borough traffic in New York. I also recently had to extract latitudes and longitudes from some street addresses to allow me to map the points in a visualization.


#### Python has a few different options. Initially I started with geopy using the Nominatim geocoder, which worked fine for one or two points, but ended up timing out or otherwise not working when I tried to feed in more than 10 points or so, even when I introduced significant wait time between queries.

#### I then switched to pygeocoder, which is a wrapper for Google's geo-API, which just seemed to work a lot better, and seemed a little faster as well, though I haven't formally measured it.

#### My data began like this:

| latitude            | longitude           |
|-------------------- |-------------------- |
| 40.767272159966524  | -73.99392887997085  |
| 40.71911551996054   | -74.0066666100157   |
| 40.71117416000734   | -74.00016544998859  |
| 40.68382604000925   | -73.97632328001441  |

#### After putting it into a pandas dataframe, I just did:

`pip install pygeocoder`

`from pygeocoder import Geocoder`

#### And then set up a function to apply to my pandas dataframe:

`def geofunc(lat,lon):
    result = Geocoder.reverse_geocode(lat,lon).formatted_address`
