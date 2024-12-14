---
layout: page
title: Lahore Property Market Analysis
description: A comprehensive analysis of Lahore's rental property market using data analytics and geospatial visualization
importance: 1
category: work
toc:
  sidebar: left
---

## Overview

An in-depth analysis of Lahore's rental property market using Python and data science techniques. This project combines traditional statistical analysis with geospatial visualization to uncover patterns in property pricing and location-based trends.

### Key Technologies
- **Data Analysis**: Python, Pandas, NumPy
- **Visualization**: Matplotlib, Seaborn
- **Geospatial Analysis**: Google Maps API
- **Statistical Methods**: Outlier Detection, Correlation Analysis

## Methodology

### Data Collection & Preprocessing
- Dataset taken from [Kaggle](https://www.kaggle.com/datasets/sherafgunmetla/lahore-property-rents) 
- Implemented geocoding using Google Maps API
- Standardized price and area measurements
- Applied IQR-based outlier detection

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
{% include figure.liquid path="assets/img/projects/location-heatmap-lahore.png" class="img-fluid rounded z-depth-1" zoomable=true %}
- Premium pricing clusters in specific neighborhoods
- Distance from city center shows moderate price correlation
- Suburban areas demonstrate varied pricing patterns

### Price Analysis
{% include figure.liquid path="assets/img/projects/price-distribution.png" class="img-fluid rounded z-depth-1" zoomable=true %}
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

## Resources

- [GitHub Repository](https://github.com/Ahmad-Alam/lahore-rent-2022-eda)
- [Data Source](https://www.kaggle.com/datasets/sherafgunmetla/lahore-property-rents)


