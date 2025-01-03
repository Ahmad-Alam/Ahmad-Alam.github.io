---
layout: post
title: Building a CLI Journaling System for ADHD-Friendly Self-Reflection
date: 2025-01-03
description: How I created a minimal, data-driven journaling system to overcome ADHD challenges and track personal growth
tags: programming personal-project cli bash goals
categories: projects
---

As a data scientist with ADHD, I've always been fascinated by the idea of journaling. The thought of looking back on my past thoughts and experiences, understanding my patterns, and tracking my personal growth has always appealed to me. Yet, like many others with ADHD, the actual practice of consistent journaling felt like an insurmountable task – another item on the endless to-do list that would eventually be forgotten or procrastinated away.

This tension between wanting to journal and struggling to maintain the habit led me to create [Daily Journal CLI](https://github.com/Ahmad-Alam/daily-journal-cli), a minimalist, markdown-based journaling system designed specifically for people who find traditional journaling overwhelming.

## The Problem with Traditional Journaling

The classic approach to journaling – sitting down with a blank page and pouring out your thoughts – can be particularly challenging for people with ADHD or attention difficulties. The lack of structure can be paralyzing, and the open-ended nature of the task often leads to:

- Analysis paralysis when facing a blank page
- Forgetting to journal regularly
- Inconsistent entries that make it hard to track patterns
- Difficulty maintaining the habit long-term

## A Data Scientist's Solution

Given my background in data science, I wanted to create a system that would not only make journaling more accessible but also generate meaningful data that I could analyze over time. The solution I developed combines several key elements:

1. **Structured Templates**: Instead of facing a blank page, each journal entry comes with pre-defined sections and prompting questions
2. **Quantifiable Metrics**: Daily ratings for focus, energy, mood, and productivity that can be tracked over time
3. **Easy Access**: A keyboard shortcut (Super+Shift+N) that instantly opens today's journal entry
4. **Automatic Organization**: Entries automatically organized by year and date
5. **Data-Driven Insights**: Monthly tracking sections that help identify patterns in focus, productivity, and health habits

## The Technical Implementation

The system is built using bash scripts and integrates seamlessly with the i3 window manager. Here's a look at the core structure:

```bash
~/journal/
├── YYYY/
│   ├── YYYY-MM-DD.md
│   └── ...
└── template.md
```

Each day's entry is created from a template that includes sections for:

- Daily metrics (1-5 scale ratings)
- Personal check-ins
- Achievement tracking
- Health monitoring
- Social connections
- Monthly trends
- Free writing
- Quick todos

## Making Data Collection Fun

One of my favorite aspects of this system is how it turns self-reflection into a data collection opportunity. Each entry captures metrics like:

- Focus Rating (1-5)
- Energy Level (1-5)
- Mood Start and End (1-5)
- Productivity Score (1-5)
- Sleep Quality (1-5)
- Exercise Duration
- Screen Time
- Water Intake

These data points can be analyzed at the end of each month to identify patterns and trends in personal well-being and productivity.

## The Human Element

While the system is data-driven, I made sure to include sections that capture the more nuanced, emotional aspects of daily life:

- "What made me smile today?"
- "What frustrated me most?"
- "Did I feel overwhelmed? When?"
- "What helped me feel calm/centered?"

These questions help preserve the sentimental value of traditional journaling while maintaining the structure that makes it ADHD-friendly.

## Looking Forward

This project is personal – it's my attempt to bridge the gap between wanting to preserve my thoughts and struggles with maintaining consistent habits. By combining data science principles with personal reflection, I've created a system that feels both meaningful and manageable.

The code is open-source and available on GitHub, and I welcome contributions from others who might want to adapt it to their own journaling needs. After all, everyone's journey with personal reflection is different, and the tools we use should be as unique as we are.

Will I stick with it? Only time (and my monthly data analysis) will tell. But by building a system that works with my brain rather than against it, I've given myself the best chance of maintaining this valuable practice.

## Try It Yourself

If you're interested in trying this journaling system, check out the [GitHub repository](https://github.com/Ahmad-Alam/daily-journal-cli) for installation instructions and documentation. The system is particularly well-suited for Linux users who use the i3 window manager, but the concepts can be adapted for other environments as well.

Remember, the goal isn't perfect consistency – it's about making self-reflection more accessible and gathering interesting data along the way. Sometimes, that's all we need to build a sustainable habit.
