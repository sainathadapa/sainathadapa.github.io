---
layout: post
title: "Cyclones in The Bay of Bengal"
description: "Visualizing cyclone paths, intensity and landfall locations"
tag:
  - rstats
  - ggplot
---

Thanks to Gaston Sanchez for a very informative Rpub, [Visualizing Hurricane Trajectories](http://rpubs.com/gaston/hurricanes). His post has led me to the data set and consequently to creating this post.

# Source code
Keeping the length of the post in mind, I am not including the code that was used to generate the plots here. The data, code and the generated images are available at [github.com/sainathadapa/plotting-cyclones](https://github.com/sainathadapa/plotting-cyclones). Please feel free to create an issue at the github repo or comment here if any part of the code is unclear.

# Path of a cyclone
Shown below is the path of the [HudHud cyclone](https://en.wikipedia.org/wiki/Cyclone_Hudhud) that devastated Visakhapatnam in 2014.

<a href="/images/hudhud-static-large.png" target="_blank"><img src="/images/hudhud-static-small.png" alt="image"></a>

# Cyclone landfall locations
Finding the cyclone landfall locations turned out to be little tricky since the data set didn't have that information. With a little help from the _sp_ and the _maps_ packages, I was able to find the intersections between the cyclone paths and the coast.

<a href="/images/landfall-locations-large.png" target="_blank"><img src="/images/landfall-locations-small.png" alt="image"></a>

# Cyclone intensity along the east coast
I needed a way to visualize the cyclone intensity and the landfall locations. One way to represent this is to use size of the point as an indication of the Wind speed. (Assuming Wind speed is a good indicator of a cyclone intensity.)

<a href="/images/cyclone-intensity-on-map-large.png" target="_blank"><img src="/images/cyclone-intensity-on-map-small.png" alt="image"></a>

This doesn't look like a optimal way of showing this information. And it is harder to make inferences from the above plot. A bar plot fits better. Translating geo-locations onto a single axis is difficult though. After approximating the east coast into a series of line segments and calculating the distance to each landfall point from the southern most tip, this is what I finally ended up with.

<a href="/images/cyclone-intensity-large.png" target="_blank"><img src="/images/cyclone-intensity-small.png" alt="image"></a>

# Trajectories of all the cyclones

And finally, an animation of paths of all the cyclones in the Bay of Bengal from the data set. Watch in 1080p to avoid the blurry video.

<iframe width="560" height="310" src="https://www.youtube.com/embed/cLx7uf2PM3s" frameborder="0" allowfullscreen></iframe>


_Note: This is an update to my previous post at [Rpubs - Visualizing trajectories of Cyclones in Indian Ocean Basin](http://rpubs.com/sainathadapa/indian-ocean-cyclones)._

