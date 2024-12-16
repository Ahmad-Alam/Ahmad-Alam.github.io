---
layout: post
title: Uncovering Lahore's Property Market Patterns 
date: 2024-12-13
description: How data science revealed hidden patterns in Lahore's rental market
tags: data-science property-analysis pakistan
categories: projects
toc:
  beginning: true
related_papers: true
bibliography: papers.bib
map: true
---

# Beyond the Numbers: Understanding Lahore's Real Estate Landscape

The real estate market in Lahore tells a fascinating story of urban development, cultural preferences, and economic patterns. After diving deep into data from over 17,500 property listings, I've uncovered some surprising insights about Pakistan's second-largest city and its housing market. For those interested in the technical details of this analysis, including the complete code and methodology, you can find the detailed project documentation [here](https://ahmad-alam.github.io/projects/lahore-property-analysis/).

## The Heart of Lahore's Housing Culture

One of the most striking things about Lahore's real estate market is how it reflects the city's strong family-oriented culture. The overwhelming preference for 3-bedroom, 3-bathroom homes isn't just about square footage – it's a reflection of the multigenerational living arrangements that are deeply woven into Pakistani society. These homes often accommodate extended families, with spaces that can be both private and communal.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/bedrooms.png" title="Distribution of Rooms" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Distribution of bedrooms and bathrooms across properties in Lahore
</div>

Houses dominate the market, but what's particularly interesting is the thriving market for "portions" – upper and lower sections of houses that are rented out separately. This unique feature of Lahore's real estate landscape speaks to both the entrepreneurial spirit of homeowners and the practical solutions that have evolved to address housing demands in a growing city.

## Geospatial Analysis and Price Distribution

Inspired by the innovative approach of Truong et al. {% cite TRUONG2020433 %} in their housing price prediction study, I implemented a geospatial analysis of Lahore's property market. Using Google's Geocoding API, I mapped each property's location to its corresponding latitude and longitude coordinates. This allowed me to create a comprehensive visualization of price distributions across the city.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/location-heatmap-lahore.png" title="Property Price Distribution" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Geospatial distribution of property prices across Lahore. Color intensity indicates price levels.
</div>

## Geographical Distribution of Properties

The interactive map below shows the distribution of all property listings across Lahore. Each blue marker represents a property location, while the red star marks the city center. This visualization helps illustrate both the spread of properties across different neighborhoods and the relationship between location and property concentration.

```geojson

    {
      "type": "FeatureCollection",
      "features": [
        {
          "type": "Feature",
          "properties": {
            "name": "City Center",
            "popupContent": "Lahore City Center",
            "marker-symbol": "star",
            "marker-color": "#ff0000"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3087, 31.5204]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.26435819999999, 31.4311985]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.258648, 31.456696]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.28688679999999, 31.4431825]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.30807089999999, 31.4474685]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2597483, 31.4432618]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1768412, 31.3694884]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2325105, 31.3689001]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.28395309999999, 31.42053739999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3484833, 31.431384]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3807788, 31.4676379]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2025244, 31.4527726]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4540282, 31.5948421]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2193999, 31.3623068]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2170853, 31.4639288]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2421428, 31.4605393]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.36607839999999, 31.5004073]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2487451, 31.4328323]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.41665480000002, 31.5032221]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3357285, 31.5388622]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4554936, 31.5296195]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4256343, 31.5202806]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2648567, 31.5388036]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.388925, 31.5196113]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4034624, 31.3190793]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3369345, 31.5616533]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3239342, 31.4804642]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4192199, 31.4990163]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2756066, 31.3837953]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2051202, 31.3388255]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3499496, 31.5164883]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.24067560000002, 31.4269467]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3836719, 31.4942473]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2111003, 31.3181216]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3851379, 31.3202919]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4209234, 31.5603503]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.27284610000001, 31.469693]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.27808550000002, 31.4448646]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2777188, 31.4841409]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3044879, 31.4760114]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.25603570000001, 31.403247]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2685504, 31.4555022]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3015563, 31.4562075]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3264869, 31.5525146]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2546136, 31.4781106]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.17390569999999, 31.3886132]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2319637, 31.396232]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.20912799999999, 31.4153247]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3217207, 31.4632019]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2844714, 31.512412]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3297094, 31.5651475]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3394299, 31.5572673]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4137129, 31.5622136]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.40877560000001, 31.4865895]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.25718100000002, 31.5017412]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.29422079999999, 31.4065037]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2751517, 31.4082952]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.28688679999999, 31.4292593]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2700521, 31.5208886]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.35874729999999, 31.5203696]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.39539979999999, 31.551378]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2370076, 31.4230055]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2990459, 31.4761573]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4403969, 31.5906928]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2105955, 31.4391744]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.32978659999999, 31.5303194]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4679495, 31.5777864]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4481662, 31.5802017]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4738108, 31.5840788]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.36701579999999, 31.4157845]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.298621, 31.5643252]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2627904, 31.4858849]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.50164939999999, 31.5944836]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.360282, 31.4075498]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3748754, 31.4597379]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.26928389999999, 31.4159153]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2546136, 31.4196459]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.289087, 31.4497229]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3602136, 31.3910577]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4019965, 31.4429184]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3228206, 31.5193603]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3763319, 31.3776311]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.239942, 31.37045669999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3550817, 31.42454639999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4041953, 31.5469071]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3219132, 31.51108799999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3501562, 31.5442078]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2678169, 31.3669851]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1445487, 31.4071838]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.14673379999999, 31.3437498]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2487451, 31.4523212]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2981226, 31.4504213]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1922515, 31.4278172]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.415463, 31.479745]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2524129, 31.42424299999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2142641, 31.4041362]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.415922, 31.5734116]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4413685, 31.4581407]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4231202, 31.5549053]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4126156, 31.55555859999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3191314, 31.515509]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2354641, 31.3582862]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4071271, 31.5611865]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.17912299999999, 31.4191919]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.281448, 31.4183615]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4657515, 31.5823839]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.25718100000002, 31.44816]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1918846, 31.424639]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.38784439999999, 31.33785499999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4598899, 31.5204202]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4041953, 31.571952]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4104252, 31.4846973]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.40822639999999, 31.5769754]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3308864, 31.5377616]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.42618209999999, 31.576079]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3639904, 31.4843016]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4045618, 31.4930181]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.26928389999999, 31.4883017]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3136912, 31.3869679]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4210521, 31.4800999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.37560839999999, 31.491155]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.24801149999999, 31.4932844]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3924679, 31.492558]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3543485, 31.543476]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2956875, 31.5695206]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3683804, 31.4545853]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2686164, 31.5787137]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2458108, 31.4686549]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.240955, 31.3232557]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.298797, 31.5335676]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2612154, 31.3849627]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.415922, 31.4453442]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.41005870000001, 31.4557579]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3949536, 31.4497314]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2487451, 31.4634563]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.310303, 31.432799]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3748754, 31.5849905]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2663499, 31.4433937]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4188535, 31.543164]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4107916, 31.5553811]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3532488, 31.4337188]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3492165, 31.434957]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2891727, 31.4331344]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4089594, 31.4879959]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2656164, 31.4022266]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3163689, 31.5557956]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3719431, 31.3423507]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3126152, 31.5414168]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3157437, 31.5476458]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3183222, 31.5313323]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2924791, 31.4511418]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.28688679999999, 31.5350339]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4804046, 31.5897658]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.18481249999999, 31.4030625]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4759378, 31.5866955]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4691639, 31.588605]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2558105, 31.5120353]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3653453, 31.552501]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.23847479999999, 31.49139]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1841796, 31.41636]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.28762019999999, 31.5274743]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4766288, 31.4356663]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.49070309999999, 31.5962697]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.29348740000002, 31.4447049]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.25277969999999, 31.4462157]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3790915, 31.3575636]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.28468649999999, 31.4255029]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2729513, 31.3920038]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2881702, 31.4271573]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.258648, 31.4525201]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3061465, 31.5350998]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3815609, 31.4275659]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2289376, 31.3516641]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2820224, 31.4476958]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3333144, 31.542855]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2920596, 31.5632362]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.31591089999999, 31.5495447]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.37707449999999, 31.49412169999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3634835, 31.4953739]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3439001, 31.5584083]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2392084, 31.4030926]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3148653, 31.5115584]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.26703359999999, 31.53898329999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2964892, 31.507615]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3422513, 31.4539312]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2971543, 31.4263668]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4979866, 31.5808112]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2469112, 31.5094946]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.24801149999999, 31.5085895]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4729941, 31.5892888]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2977074, 31.482463]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2795524, 31.552197]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3939759, 31.4469315]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4171413, 31.4931571]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.354708, 31.5475527]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2606095, 31.3274135]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.355674, 31.4514756]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3715766, 31.4951767]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3396851, 31.6000644]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2487451, 31.4133402]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2257995, 31.319271]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3222162, 31.4618905]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.35861489999999, 31.56896489999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3106478, 31.522172]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.448899, 31.5726401]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4103575, 31.5203274]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.238617, 31.4636698]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1606956, 31.3911245]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3657119, 31.321713]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3624129, 31.4783737]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2891329, 31.5658174]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.35881669999999, 31.5203906]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3459172, 31.4745762]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4950564, 31.40498179999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.37890709999999, 31.4884336]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3991619, 31.5531315]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2916539, 31.4420389]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4008971, 31.5885826]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3701104, 31.492906]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.20497, 31.4485309]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.28992219999999, 31.5326833]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3811117, 31.5729711]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4086362, 31.5542211]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3457135, 31.5958449]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.45966229999999, 31.5853731]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3052953, 31.4507887]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3866039, 31.5864535]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.36167979999999, 31.6014236]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.16730079999999, 31.4093598]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3653453, 31.4216463]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.46316449999999, 31.58746439999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4244466, 31.5578355]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3774411, 31.35871329999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3112722, 31.5543622]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3137526, 31.5596506]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4401057, 31.5715482]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2603081, 31.5120945]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2566804, 31.4596003]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3022099, 31.5961844]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3917349, 31.4486065]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.363146, 31.4471372]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4258157, 31.4719883]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3019212, 31.5205709]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2634159, 31.5070462]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2144268, 31.5921767]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4950564, 31.4384243]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.378559, 31.3464041]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3460927, 31.5805609]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3016, 31.5282166]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.29825439999999, 31.5590635]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3682777, 31.4846732]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3067577, 31.5430024]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3254565, 31.5547009]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.26928389999999, 31.685744]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2894537, 31.4264477]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3697439, 31.5029521]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.298621, 31.5893578]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.34811669999999, 31.4992105]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.172438, 31.4037431]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.413082, 31.5670582]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3653198, 31.4398298]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2923873, 31.4546605]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3453638, 31.3590768]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2812828, 31.3996]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.246738, 31.475959]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.297246, 31.4738]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3543485, 31.4571805]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3217207, 31.4701624]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2553471, 31.4580217]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4705139, 31.5951485]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3283201, 31.4695949]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2516794, 31.491658]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3958799, 31.5821591]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4121079, 31.4874987]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2823662, 31.6211127]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3338194, 31.5882051]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.42618209999999, 31.4870025]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4181206, 31.5813369]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.43241119999999, 31.5674616]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3625962, 31.4253084]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3697439, 31.42915799999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.44450239999999, 31.5693113]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3884364, 31.5800746]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.48919579999999, 31.58250619999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4012635, 31.5743694]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2667167, 31.4952853]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2924213, 31.5278658]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.292754, 31.5357696]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3906354, 31.5803487]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.22233469999999, 31.4406511]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1983209, 31.4405053]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.20802739999999, 31.44685449999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3121879, 31.551768]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2928457, 31.5440408]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2662369, 31.5050411]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2080991, 31.5824419]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3521688, 31.5583539]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4063941, 31.4058538]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2370076, 31.4090823]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2817528, 31.4863862]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3983317, 31.5573088]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2429653, 31.4495086]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4063941, 31.5548339]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.24654439999999, 31.4764014]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.36167979999999, 31.5902975]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3277188, 31.5664484]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4133773, 31.5982732]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3653453, 31.5817145]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.38440489999999, 31.4268036]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2656164, 31.49271209999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3242797, 31.5232582]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2401239, 31.48169189999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.31211820000001, 31.5252694]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3684062, 31.5933829]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3206208, 31.6018492]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.34563299999999, 31.343036]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.31842089999999, 31.52159289999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2764265, 31.5359429]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.21499779999999, 31.3715035]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.5220933, 31.5526181]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2657912, 31.6137439]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3524375, 31.45168749999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3200761, 31.5699659]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4263125, 31.5811875]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3245103, 31.5592663]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.30040269999999, 31.6294287]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.302463, 31.5825142]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.35604909999999, 31.5780616]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.30466129999999, 31.5540012]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.31201539999999, 31.5698132]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3426179, 31.58930579999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2333395, 31.4148873]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.42618209999999, 31.5983374]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.23945619999999, 31.4558061]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2887203, 31.5300469]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4005306, 31.494257]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3051963, 31.5540119]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3267112, 31.5684148]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.06966729999999, 31.3016316]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3536663, 31.3981516]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3791746, 31.6049401]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.22160099999999, 31.4537818]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3074213, 31.5153461]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3658952, 31.4828102]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3697439, 31.486248]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2582813, 31.5794245]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.316571, 31.585949]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4107916, 31.581816]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3260855, 31.547696]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.38440489999999, 31.5827018]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3344882, 31.2948237]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3013978, 31.4724895]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3355082, 31.5692686]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3594805, 31.4585164]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3137831, 31.5749202]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3063213, 31.5287744]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2887203, 31.5502177]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3637405, 31.4622103]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3851379, 31.604352]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4983285, 31.5835547]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4629237, 31.577631]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3198175, 31.5486133]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4149371, 31.4826256]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2834956, 31.5610851]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4166404, 31.5668817]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3550817, 31.4969479]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3589306, 31.5511786]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3193705, 31.5273336]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.411891, 31.4834872]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2477256, 31.48870579999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2879739, 31.4155565]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.30375459999999, 31.5489727]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2222877, 31.6260411]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3382187, 31.5428522]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3594805, 31.5809821]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3066423, 31.5860261]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2488383, 31.4500237]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3233763, 31.5544623]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3675446, 31.373857]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3008211, 31.5819854]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1716658, 31.4178134]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2975625, 31.5900625]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1949221, 31.4388468]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2395634, 31.4531907]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3067741, 31.5911183]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.1899333, 31.641105]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2426906, 31.4482544]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.359847, 31.4999782]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3650795, 31.5477496]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.24801149999999, 31.398627]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2979541, 31.5280175]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4071271, 31.6001386]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3609467, 31.543604]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3873369, 31.475909]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3484833, 31.4258132]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2131976, 31.4524434]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.363146, 31.4916899]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3356524, 31.4698146]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2529172, 31.4471465]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.156292, 31.3529722]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2197668, 31.3863776]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3602136, 31.4746191]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3859939, 31.59656129999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2962376, 31.4803722]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3322407, 31.5486639]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.32208729999999, 31.5728287]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3308864, 31.46260659999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3330861, 31.467754]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.183807, 31.5592287]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3651505, 31.4604455]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.32611469999999, 31.4321785]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4768835, 31.5714681]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3683829, 31.4873858]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3634059, 31.4012285]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.4321166, 31.5555906]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.41665480000002, 31.5867191]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [73.1279532, 33.5687889]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.39320090000001, 31.5810162]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2905248, 31.4507857]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.363146, 31.42764009999999]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2874368, 31.4281098]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.30996, 31.5505262]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2956875, 31.5528302]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3074791, 31.5657387]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.2553471, 31.5081199]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3961328, 31.5744259]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.37029369999999, 31.5717257]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.26708339999999, 31.5095936]
          }
        ,
        {
          "type": "Feature",
          "properties": {
            "popupContent": "Property Location",
            "marker-color": "#3388ff"
          },
          "geometry": {
            "type": "Point",
            "coordinates": [74.3781741, 31.4834698]
          }
        
      ]
    }
    
```

## The Price Paradox

Perhaps the most intriguing finding is what I call the "suburban premium paradox." Conventional wisdom suggests that properties closest to the city center should command the highest prices. While this holds true for properties very close to the center (averaging PKR 86,700), there's an unexpected twist: properties far from the center actually command higher prices than those moderately close to it.

This pattern reveals the emergence of high-end suburban developments in Lahore. Areas that might have once been considered "too far" are now becoming prestigious addresses, complete with modern amenities and planned communities. It's a sign of how Lahore is growing not just outward, but upward in terms of luxury and desirability.

## The Value Game

What really drives property values in Lahore? While location matters, the data reveals that Lahoris place a premium on bathrooms and bedrooms almost equally. This makes sense when you consider the local lifestyle – large family gatherings are common, and having adequate facilities is often as important as having enough bedrooms.

Farm houses, while representing a small segment of the market, tell an interesting story about luxury living in Lahore. With an average size of 22.5 Marlas, these properties are massive compared to standard homes. Yet their pricing doesn't always reflect their size, suggesting they serve as weekend retreats or status symbols rather than primary residences.

## The Evolution of Urban Living

The significant presence of flats in the market (over 2,000 listings) signals a gradual shift in Lahore's urban landscape. While traditionally a city of houses, the growing acceptance of apartment living suggests a modernizing mindset, particularly among younger residents. However, the price points of flats (median of PKR 42,000) indicate they're positioned as middle-market options rather than luxury choices.

## Reading Between the Numbers

What makes this analysis particularly fascinating is how it reveals the intersection of tradition and transformation in Lahore. The property market isn't just responding to supply and demand – it's adapting to changing family structures, evolving lifestyle preferences, and the city's rapid expansion.

For investors and homebuyers, understanding these patterns is crucial. The sweet spot in Lahore's market isn't just about finding the right price point – it's about understanding the social and cultural factors that drive value. A property's worth isn't just in its square footage or location, but in how well it serves the unique needs of Lahori families and their way of life.

## Looking Forward

As Lahore continues to grow and evolve, these patterns will likely shift. The rise of suburban premium areas suggests a city that's reimagining its boundaries. The steady demand for family-sized homes indicates the enduring strength of traditional living arrangements. And the emerging apartment market hints at new possibilities for urban living.

The story of Lahore's real estate market is, in many ways, the story of Lahore itself – a city balancing tradition with transformation, family values with modern aspirations, and organic growth with planned development. For anyone interested in understanding urban development in South Asia, Lahore offers a fascinating case study of how housing markets adapt to and reflect social change.

Note: This analysis was conducted using Python and pandas, examining a dataset of over 17,500 property listings across Lahore. All prices are in Pakistani Rupees (PKR). The geospatial analysis methodology was inspired by the work of Truong et al. {% cite TRUONG2020433 %}. For the complete technical analysis, including code and methodology, please visit the [project documentation](https://ahmad-alam.github.io/projects/lahore-property-analysis/)._

## References

{% bibliography --cited %}

