---
title: "Note on Google Maps API polylines"
date: 2019-05-15T20:52:31-07:00
---

### I recently had occasion to use the Google Maps directions API. 
I needed a series of (lat, lon) points connecting two coordinates, which seemed like a perfect use case for the directions API. 
It was obvious that I'd get at least a few waypoints scattered throughout the trip. I thought I'd need to interpolate between the waypoints to get the series of points I needed. This was not necessary, as it turned out. 

### Polylines

The API response includes a polyline for every segment of the trip. With my GIS experience I knew that a polyline was precisely what I wanted, but the format of these polylines was not what I expected: 

~~~~
'polyline': {'points': 'gradGjz``NP@pETjBNtAH`CRlBPb@BZDlBPB?xBTTB~@JtAP`AJ|
BZvAR~@Lh@Jj@Jf@LVD~@VZJRFVHt@VZNd@Pr@Zt@`@FBd@Vv@d@x@h@l@b@ZVRNt@n@z@v@JHb@d@TT|
@`A`AlAlAbBlBnCl@z@n@~@j@z@~@pAl@|@|@pAn@|@l@z@p@~@l@v@`@f@p@x@p@v@`@b@PPbAfAjBdBhAbAvAlAfA|
@f@`@jBzAb@\\\\XFFhA~@hA|@zAnAv@n@fElDj@b@fBxAxAlA|AnAfA~@RNlFjEzAnAlB~Ar@j@d@`@d@^v@n@fA`APNf@d@'}
~~~~

This is a Google-optimized polyline encoding format. It is [pretty well documented](https://developers.google.com/maps/documentation/utilities/polylinealgorithm), and there is a polyline encoding/decoding utility maintained by Google on their [Maps developers page](https://developers.google.com/maps/documentation/utilities/polylineutility).

If you need to embed the decoding into an application, there are many options for many different programming languages. I used the Python package [`polyline`](https://pypi.org/project/polyline/), which implements the encoding/decoding algorithm. With a simple call to `polyline.decode()` I got a list of segment lists:
~~~
waypoints = [polyline.decode(loc['polyline']['points']) for loc in start_locs]
~~~
Which I then flattened to get a list of points:
~~~
flat_list = [item for sublist in waypoints for item in sublist]
~~~

I should be putting an end-to-end demo up on Github in the next couple of days.