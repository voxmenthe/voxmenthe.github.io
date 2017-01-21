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

#### My data began like this as a pandas dataframe:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-yw4l"></th>
    <th class="tg-yw4l">latitude</th>
    <th class="tg-yw4l">longitude</th>
  </tr>
  <tr>
    <td class="tg-yw4l">0</td>
    <td class="tg-yw4l">40.767272159966524</td>
    <td class="tg-yw4l">-73.99392887997085</td>
  </tr>
  <tr>
    <td class="tg-yw4l">1</td>
    <td class="tg-yw4l">40.71911551996054</td>
    <td class="tg-yw4l">-74.0066666100157</td>
  </tr>
  <tr>
    <td class="tg-yw4l">2</td>
    <td class="tg-yw4l">40.71117416000734</td>
    <td class="tg-yw4l">-74.00016544998859</td>
  </tr>
  <tr>
    <td class="tg-yw4l">3</td>
    <td class="tg-yw4l">40.68382604000925</td>
    <td class="tg-yw4l">-73.97632328001441</td>
  </tr>
  <tr>
    <td class="tg-yw4l">4</td>
    <td class="tg-yw4l">40.74177603003744</td>
    <td class="tg-yw4l">-74.00149745986825</td>
  </tr>
</table>

#### Install pygeocoder:

`pip install pygeocoder`

#### Import the geocoding functionality from pygeocoder:

####`from pygeocoder import Geocoder`
**`test`**


#### And then set up a function to apply to my pandas dataframe:

`def geofunc(lat,lon):`
`   result = Geocoder.reverse_geocode(lat,lon).formatted_address`
