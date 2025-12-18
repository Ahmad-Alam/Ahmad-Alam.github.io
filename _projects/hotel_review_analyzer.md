---
layout: page
title: Hotel Review Sentiment Analysis
description: NLP pipeline for sentiment analysis and hotel performance evaluation
img: assets/img/projects/wheel.jpg
importance: 3
category: fun
github: https://github.com/Ahmad-Alam/HotelReviewAnalyzer
---

This project implements an end-to-end NLP pipeline that processes hotel reviews to extract sentiment and evaluate hotel performance across multiple criteria. The system handles thousands of reviews, performing text preprocessing, sentiment classification, and comparative analysis to identify top and bottom performing hotels.

The text preprocessing pipeline applies standard NLP techniques: lowercasing, special character removal, tokenization using NLTK, stopword filtering, and Porter stemming for word normalization. Processed text is then classified into positive, negative, or neutral sentiment categories, with results visualized through word clouds that highlight the most frequent terms in each sentiment group.

Beyond sentiment analysis, the system evaluates hotels across seven criteria—service quality, cleanliness, overall satisfaction, value for money, location, sleep quality, and room condition. By merging review data with hotel offerings, the pipeline calculates average ratings per criterion and identifies which hotels excel or underperform in each area.

The modular architecture separates concerns across dedicated scripts: preprocessing handles text cleaning, sentiment labeling generates classifications and visualizations, and a best/worst module ranks hotels by performance. Results are exported to CSV files for further analysis, making the system practical for business intelligence applications in the hospitality industry.
