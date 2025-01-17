---
layout: post
title: Notes from Day 1 - The Functional Art
date: 2025-01-17
description: My first day diving into Alberto Cairo's The Functional Art and what I learned about data visualization
tags: data-visualization books notes
categories: reading-notes
---

I started reading "The Functional Art" by Alberto Cairo today, primarily because I wanted to improve my data visualization skills. While there are countless online resources, I felt I needed a more structured understanding of what makes certain visualizations work better than others. I decided to take notes as I read, focusing on the key concepts that stood out to me.

One of the most interesting things I learned was about the fundamental purpose of data visualization. Cairo explains that the primary goal of any graphic or visualization is to be a tool for our eyes and brain to perceive what lies beyond their natural reach. This really shifted my perspective - instead of thinking about making pretty charts, I should be thinking about making effective tools.

The book introduced several fascinating concepts about how we should approach data visualization. There's a particular emphasis on the relationship between form and function, which isn't as straightforward as I initially thought. Cairo challenges the common "form follows function" principle through examples from evolution, like how feathers initially evolved for warmth but later became essential for flight. This made me think differently about how we repurpose visual elements in data visualization.

What really caught my attention was a section where Cairo presents a simple test for visualization effectiveness: can you answer specific questions about the data in under five seconds? He demonstrates this with an unemployment data visualization where a seemingly elegant map-based design actually made it difficult to extract basic information. This practical approach to evaluating visualizations is something I want to incorporate into my own work.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/unoptimized.png" title="Unemployment rates by region (unoptimized)" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The unoptimized infographic. 
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/optimized.png" title="Unemployment rates by region (optimized)" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The optimized infographic.
</div>

I've been keeping track of visualizations that caught my eye while reading. There was a particularly effective scatterplot (Figure 1.7 in the book) showing the relationship between education, wealth, and the fertility rate. What stood out was how it only labeled the outliers rather than every data point, which I found to be a clever way of focusing attention on the most important information. Also how easy it was to compare the two. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/fertility.png" title="Comparison of education and wealth against fertility rate" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    "The more educated and rich you are, the fewer children you'll have."
</div>

An interesting tidbit from the book: according to Eric Schmidt (former Google CEO), humanity produced about five exabytes of data from the beginning of time until 2003, but now we produce that same amount every two days. This really puts into perspective why effective data visualization is more crucial than ever.

I'm looking forward to reading more and expanding my visualization toolkit. The book has already challenged some of my assumptions about what makes a good visualization. Most importantly, I'm learning that before creating any visualization, I need to think carefully about what questions my readers will want to answer with it.

I'll be sharing more notes as I continue reading. 
