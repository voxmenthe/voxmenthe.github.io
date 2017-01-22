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
<style>
  .mytable 
  {
  background-color: #eee;
  border: 1px solid #999;
  display: block;
  padding: 20px;
  }
  .mytable .comment {
    padding-right: 30px 
    background-color: #ffccff;
    font-family: Arial,Courier,sans-serif;
    font-style: italic;
    font-color: yellow;
    font-size: 8; }
  .mytable .code {
    padding-right: 10px 
    background-color: #ffccff;
    font-family:Consolas,Monaco,Liberation Mono,DejaVu Sans Mono,Bitstream Vera Sans Mono;
    font-weight: bold;
    font-style: italic;
    font-color: black;
    font-size: 18; }
</style>


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

#### First I used the following code to test things out:

<table class="mytable">
<tr> <td class="comment"># Import the geocoding functionality from pygeocoder</td> </tr>
<tr> <td>from pygeocoder import Geocoder</td> </tr>
<tr><td></td></tr>
<tr> <td class="comment">#Feed in a latitude and longitude to see what we get</td> </tr>
<tr><td>mylocation = Geocoder.reverse_geocode(df.loc[0,'latitude'],df.loc[0,'longitude']</td></tr>
<tr></tr>
<tr> <td class="comment">#This returns a geocoder object with the info inside it</td> </tr>
<tr> <td>mylocation</td> </tr>
</table>

<pygeolib.GeocoderResult at 0x7fabd87b9320>

<table class="mytable">
<tr> <td class="comment">#To see ALL of the information encoded inside</td> </tr>
<tr> <td class="comment">#Use the <strong>raw</strong> attribute</td> </tr>
<tr> <td>mylocation.raw</td> </tr>
</table>

[{
    'address_components': [{'long_name': '603-609',
    'short_name': '603-609',
    'types': ['street_number']},
   {'long_name': 'West 52nd Street',
    'short_name': 'W 52nd St',
    'types': ['route']},
   {'long_name': 'New York County',
    'short_name': 'New York County',
    'types': ['administrative_area_level_2', 'political']},
   {'long_name': 'New York',
    'short_name': 'NY',
    'types': ['administrative_area_level_1', 'political']},
   {'long_name': 'United States',
    'short_name': 'US',
    'types': ['country', 'political']},
   {'long_name': '10019', 'short_name': '10019', 'types': ['postal_code']}],
  'formatted_address': '603-609 W 52nd St, New York, NY 10019, USA',
  'geometry': {'bounds': {'northeast': {'lat': 40.7676057, 'lng': -73.9938645}
  
  etc.
  
  ]}]

#### We can then access specific attributes as follows:

<table class="mytable">
<tr> <td class="comment">#Get the postal code:</td> </tr>
<tr>mylocation.postal_code</tr>
</table>

'10019'

<table class="mytable">
<tr> <td class="comment">#Get the street address:</td> </tr>
<tr>mylocation.street_address</tr>
</table>

''

#### There was nothing in that field, but in this instance, I had an alternative field:

<table class="mytable">
<tr> <td class="comment">#Get the street address using a different field:</td> </tr>
<tr>mylocation.formatted_address</tr>
</table>

'603-609 W 52nd St, New York, NY 10019, USA'

#### And then set up a function to apply to my pandas dataframe:

`def geofunc(lat,lon):`
    `result = Geocoder.reverse_geocode(lat,lon).formatted_address`



#### One thing to bear in mind is that the Google Maps API only allows 2500 geolocation requests per day, though you can pay for more.