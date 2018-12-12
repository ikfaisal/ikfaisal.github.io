---
title:  "Statistical Features"
categories: generalassembly statsitics boxplot
tags: statistics
---

# Statistical Features

Statistical features is probably the most used statistics concept in data science. It’s often the first stats technique we need to apply when exploring a dataset and includes things like bias, variance, mean, median, percentiles, and many others. It’s all fairly easy to understand and implement in code!

Check out the graphic below for an illustration.

![](/img/1_8noddM5HrclQmqUU9U_dUw.gif)

A box plot perfectly illustrates what we can do with basic statistical features:

- When the box plot is **short** it implies that much of our **data points are similar**, since there are many values in a small range
- When the box plot is **tall** it implies that much of our **data points are quite different**, since the values are spread over a wide range
- If the median value is **closer to the bottom** then we know that most of the data has lower values. If the median value is closer to the top then we know that most of the data has higher values. Basically, if the median line is not in the middle of the box then it is an indication of **skewed data**.
- Are the whiskers very long? That means your data has a high standard deviation and variance i.e the values are spread out and highly varying. If you have long whiskers on one side of the box but not the other, then your data may be highly varying only in one direction.
