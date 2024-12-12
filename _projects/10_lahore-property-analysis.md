---
layout: page
title: Lahore Property Market Analysis
description: A comprehensive analysis of Lahore's rental property market using data analytics and geospatial visualization
img: assets/img/projects/lahore-property-heatmap.jpg
importance: 1
category: data-science
github_repo: lahore-property-analysis
toc:
  sidebar: left
---

## Overview

An in-depth analysis of Lahore's rental property market using Python and data science techniques. This project combines traditional statistical analysis with geospatial visualization to uncover patterns in property pricing, configuration preferences, and location-based trends.

### Key Technologies
- **Data Analysis**: Python, Pandas, NumPy
- **Visualization**: Matplotlib, Seaborn
- **Geospatial Analysis**: Google Maps API, Folium
- **Statistical Methods**: Outlier Detection, Correlation Analysis

## Methodology

### Data Collection & Preprocessing
- Gathered rental property data across Lahore
- Implemented geocoding using Google Maps API
- Standardized price and area measurements
- Applied IQR-based outlier detection
- Created derived metrics like price-per-marla

### Feature Engineering
- Standardized area measurements to Marla
- Created location-based metrics
- Developed property type categorization
- Generated price normalization factors

## Key Findings

### Market Segmentation
- 3-4 bedroom properties dominate the market (65%)
- Houses show highest median prices but largest variation
- Strong correlation between property size and price (r = 0.78)

### Geographical Patterns
{% include figure.liquid path="assets/img/projects/location-heatmap.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
- Premium pricing clusters in specific neighborhoods
- Distance from city center shows moderate price correlation
- Suburban areas demonstrate varied pricing patterns

### Price Analysis
{% include figure.liquid path="assets/img/projects/price-distribution.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
- Median rental price: PKR 45,000
- Price per Marla shows significant variation
- Property type strongly influences price distribution

## Technical Implementation

### Data Cleaning Process
```python
def extract_price(price_str):
    match = re.search(r'[\d\.]+', price_str)
    if match:
        num = float(match.group())
        if 'Lakh' in price_str:
            return num * 100000
        elif 'Thousand' in price_str:
            return num * 1000
    return None
```

### Geospatial Analysis
```python
# Calculate distance from city center
center_point = np.array([74.3587, 31.5204])
df['distance_from_center'] = df.apply(
    lambda row: np.linalg.norm(
        np.array([row['Lng'], row['Lat']]) - center_point
    ), axis=1
)
```

## Impact & Applications

### Market Insights
- Identified undervalued areas
- Revealed pricing inefficiencies
- Mapped development opportunities

### Practical Applications
- Property valuation guidance
- Investment strategy development
- Urban planning insights

## Future Developments

1. Time series analysis of price trends
2. Machine learning for price prediction
3. Integration with economic indicators
4. Enhanced geospatial visualization

## Resources

- [GitHub Repository](https://github.com/yourusername/lahore-property-analysis)
- [Interactive Dashboard](https://yourdashboard.com)
- [Data Source](https://datasource.com)

