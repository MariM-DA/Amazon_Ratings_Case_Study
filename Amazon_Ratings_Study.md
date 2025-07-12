---
title: "Amazon Sales Case Study Project"
author: "Mari M."
date: "2025-07-10"
output: html_document
---
# Introductions

In this project, I will perform many real-life scenarios regarding data analysis such as cleaning, analyzing, visualizing and subsequently creating a presentation of the topic covered. The goal of this case study project is to create a fresh start to my brand new portfolio using my newfound skills.

### Scenario

I will assume to be a junior data analyst currently employed and in training at Amazon, a worldwide company behing the largest e-shop in the world. The CEO believes that expensive products equal to better ratings, due to the higher quality of the product, and has requested the data analytics team to perform an analysis on online sales in the year 2024 & subsequently create visualizations, to confirm whether this is true or not.






---

# The Questions and Goals of the Project

### The Business Goal

Use analysis insights to find whether discount frequency should be increased or decreased depending on the ratings of the products.

### The Questions

The stakeholder has put forward questions that they'd like answered with this project:

* 1. Does the price of the product correlate to the ratings of it?
* 2. Which sales categories are underperforming the most?

### Data Source

I will be using an open-source independent dataset from [Kaggle](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset).
This dataset contains product names, prices, discount prices, ratings and reviews from individuals, whose identity will be censored and anonymous.

---

# Data Preparation & Cleaning

On a quick overview of the dataset, we can see that it is not very large, so we will be doing the data cleaning in Spreadsheets/Excel. For our data analysis, some of the information in the columns will be irrelevant to our work, so we will remove the columns "about_product, user_id, user_name, review_id, review_title, review_content, img_link, product_link". 
Upon doing this, we will remove duplicate data via the remove duplicates feature.
![](https://i.ibb.co/5WBKs74P/image-png.png)

*As it turns out, there were quite many duplicates*

Next, I will use the filter feature to view data in every column and search for any possibles typo's or missing values. Upon finding (Blank) values, I will delete its' rows. We've also found that some rating counts are non-sensical, such as "1,79,641", in a real life scenario, we would turn to the source of the dataset for clarification, but for the project, we will assume the stakeholder told us that the review amounts are only supposed to be 5 characters at max. We will correct this by using the =RIGHT function and copy paste special. 
Every product category comes with a lengthy name, so we will divide every category into bigger categories, such as all Computer & Accessory | USB Cables products going into a "Computer & Accessory" category. To achieve this, I'll be using a combination of the filter by condition features and find & replace.

The currency of the dataset is in Indian Rupeés and we will convert it to US dollars ($) as it is the origin currency for the company. We will clarify with the stakeholders what conversion rate they'd prefer, since our data is from the year 2024, but in this project, we will use the current conversion rate of 0.012.
Now we will use a simple calculation of the currency times the conversion rate, which will result in the dollar price. And with a quick double checking, we conclude the cleaning process.

---

# Analysis 

With the data ready for analysis, we will export our .csv dataset file into r, as it's going to be our primary analysis & preliminary visualizations tool. 
As a start, we will load the dataset and all the packages we will be using for this analysis such as tidyverse, ggplot2 and dplyr. 

```{r}
library(tidyverse)
library(ggplot2)
library(dplyr)
library(readr)
amazon_products_cleaned <- read_csv("amazon_products_cleaned.csv")
head(amazon_products_cleaned)
```

Upon having a glimpse at the dataset, we can start making a visualization to view the correlations to answer the first question.

```{r eval=FALSE, include=FALSE}
ggplot(data = amazon_products_cleaned) + geom_point(mapping = aes(x = rating, y = actual_price_dollars, color = category)) + labs(title="Price vs Ratings")   

```

![](https://i.ibb.co/Dg5Lww5W/Price-VRatings.png)



*As we can see, the price of the product does not have a very big impact on the ratings of it. Expensive items tend to have good ratings by default, but most cheap/median items hover around the same rating too.*

---

```{r warning=FALSE}
ggplot(data = amazon_products_cleaned) + geom_col(mapping = aes(x = ratings_amount, y = category, color = category)) + labs(title="Category Performance", subtitle = "Electronics are overperforming by a large margin")   
```

![](https://i.ibb.co/C5xG44q5/Performance.png)

*Car & Motorbike section is the underperforming candidate in this case, it is the least popular and least profitting category due to the sheer scale of Electronics reviews, which we can attribute directly to sales.*

![](https://i.ibb.co/DHg5N1MR/Tableau-A-Sales.png)

Above is a preview of general category analysis. You can view the proper interactive graphs on [Tableau Public](https://public.tableau.com/app/profile/marco.minar.ik/viz/TableauA-Sales1/Dashboard1)

From general overview of the data, we come to the conclusion that the Electronics category is overperforming in every aspect. We can deduct that since the average price of Electronics is much higher than most other items, it is more of a hot item when discounts are applied.

---


# Recommendations

We conclude, that the best course of action would be focusing on the Electronics and Computers & Accessories category, applying discounts more often, yet decreasing the amount discounted, as we feel there's a lot of potential profit lost in this category, due to the consistent review ratings. On the contrary, we recommend increasing amounts discounted on the Toys & Games and Car & Motorbike, as they are underperforming by a large margin. 
We have also concluded there's no correlation between high price and quality of products, as most low priced items still have good ratings, though it can be argued there's a slight correlation.
