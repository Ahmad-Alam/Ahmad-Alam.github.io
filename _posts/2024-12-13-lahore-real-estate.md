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
    },
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.264358, 31.431199]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.258648, 31.456696]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.286887, 31.443183]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.308071, 31.447469]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.259748, 31.443262]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.176841, 31.369488]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.232511, 31.368900]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.283953, 31.420537]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.348483, 31.431384]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.380779, 31.467638]}},
    {"type": "Feature", "properties": {"popupContent": "Property Location"}, "geometry": {"type": "Point", "coordinates": [74.202524, 31.452773]}}
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

