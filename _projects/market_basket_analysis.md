---
layout: page
title: Retail Market Basket Analysis
description: Association rule mining for product recommendations using Apriori algorithm
img: assets/img/projects/price-distribution.jpg
importance: 4
category: fun
github: https://github.com/Ahmad-Alam/retail-market-basket-analysis
---

This project applies association rule mining to an online retail dataset containing nearly 400,000 transaction items across 18,536 invoices. Using the Apriori algorithm, the analysis discovers which products are frequently purchased together, generating actionable insights for cross-selling strategies and product placement optimization.

The analysis pipeline begins with data cleaning and transformation, converting transaction records into a one-hot encoded product matrix suitable for frequent pattern mining. The Apriori algorithm identifies 243 frequent itemsets meeting a minimum 2% support threshold, from which 32 association rules are generated with at least 50% confidence.

The strongest associations involve complementary products like Regency Teacup sets, where purchasing one variant strongly predicts buying another—these rules achieve lift values up to 24x, indicating correlations far exceeding random chance. Average metrics across all rules show 2.41% support, 64.1% confidence, and 14.47x lift, demonstrating meaningful purchase patterns in the data.

The project spans four Jupyter notebooks covering data cleaning, customer segmentation, product performance analysis, and the core market basket analysis. Multiple evaluation metrics—support, confidence, lift, leverage, and conviction—provide comprehensive rule assessment. These findings directly translate to business applications: product bundling, shelf layout optimization, targeted promotions, and inventory management decisions.
