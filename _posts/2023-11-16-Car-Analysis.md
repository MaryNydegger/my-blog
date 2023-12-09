---
Layout: post
Title: "EDA Semester Project"
Author: Mary Nydegger
Description: My EDA journey through car data showcased compelling visualizations, unraveling nuanced insights into pricing, correlations, fuel efficiency, and market trends, enriching the narrative of automobile dynamics.
Image: assets/images/Screen Shot 2023-11-16 at 1.47.53 PM.png
---

### Table of Contents
- [Synopsis](#synopsis)
- [Questions](#questions)
- [EDA](#eda)
    - [Car Price Distribution](#What-is-the-distribution-of-car-prices-in-the-dataset?)
    - [Price Variation Across Countries](#How-do-car-prices-vary-across-different-countries-of-origin?)
    - [Correlation Between Engine Size and Horsepower](#Is-there-a-relationship-between-engine-size-and-horsepower?)
    - [Fuel Efficiency Analysis](#How-does-fuel-efficiency-vary-across-different-car-sizes?)
    - [Market Popularity Trends](#Which-car-brands-are-the-most-popular-based-on-their-market-category?)
    - [Follow Up Questions](#Follow-Ups)
    - [Dashboard](#dashboard)
- [Conclusion](#conclusion)
- [Ethical Considerations](#ethical-considerations)

## Synopsis
In my exploratory data analysis (EDA), I delved into the details of car data, utilizing Python libraries to craft visualizations that unraveled diverse insights. From understanding price distributions and correlations between car features to exploring fuel efficiency trends and market popularity, the EDA journey illuminated compelling patterns, enriching my understanding of the multifaceted world of automobiles.



## Questions 

Before digging deeper into the analysis, I wanted to understand the data a bit more - specifically the distribution of prices from the data I have - I recognize that this may not contain everything or be completely up to date. 

#### The minimum car price is $2,000
#### The maximum car price is $2,065,902
#### The average car price is $40,594

From these numbers, these are the questions that I am curious about.

 1. Car Price Distribution: What is the distribution of car prices in the dataset?
 2. Price Variation Across Countries: How do car prices vary across different countries of origin?
 3. Correlation Between Engine Size and Horsepower: Is there a relationship between engine size and horsepower?
 4. Fuel Efficiency Analysis: How does fuel efficiency vary across different car sizes?
 5. Market Popularity Trends: Which car brands are the most popular based on their market category?

## EDA

### **What is the distribution of car prices in the dataset? **
To answer this first question, I created a histogram comparing the prices and the frequency. It was originally extremely right skewed (as seen in Graph 1.1). Assuming this was due to a few outlier prices among the whole distribution (as mentioned above, the maximum car price i over $2million), I filtered the data to zoom in on the prices that had a higher frequency. Graph 1.2 shows the frequency of prices less than $300,000, and it is much more readable.

#### Graph 1.1
![Graph1.1](/assets/images/Question1.png)

#### Graph 1.2
![Graph1.2](/assets/images/Question1b.png)

Most of the car's prices are below $50,000. The highest frequency of cars are around $30,000.

### **How do car prices vary across different countries of origin? **
To answer this second question, I built boxplots for each country and the prices that are present for each of their models.

#### Graph 2.1
![Graph2.1](/assets/images/prices-across-countries.png)

It was interesting to see how much higher the prices in France were compared to the other countries. When first running through the analysis, I assumed that it was because there are majorly higher prices in France, but it lead my to the follow up question of counting the number of car brands from each country, and this is what I found. 

#### Graph 2.2
![Graph2.2](/assets/images/CarModelNumbers.png)

From these numbers, it is clear that Japan, America, and Germany by far have the highest amount of car models, whereas France only has 3. Combining this understanding with what I saw in Graph 2.1, yes, France has the most expensive cars, but they also only have 3 car models that originate in France, which must be more expensive models. Whereas Japan, America, and Germany have thousands of car models, and much more variety, which would explain having very different prices among these models. 

Graph 2.1 shows us that the price ranges for all the models for Germany, America, and Japan are all smaller than France's as well. Germany at about $500,000, America at about $200,000, and Japan around $400,000. France's price ranges differ at more than $500,000. This makes sense because there are significantly more models in the prior 3 countries when compared to France, so there would be many more prices. 

### ** Is there a relationship between engine size and horsepower? **
In finding the answer to this question, I first ran this code to make a scatterplot. 

``` py
plt.figure(figsize = (8, 6))
sns.scatterplot(data = merged_df, x = 'Engine HP', y = 'Engine Cylinders')
sns.regplot(data=merged_df, x='Engine HP', y='Engine Cylinders', scatter=False, color='red', line_kws={'linewidth': 1})
plt.title('Correlation Between Engine Size and Horsepower')
plt.xlabel('Horsepower')
plt.ylabel('Engine Size')
plt.show()
```

This wasn't a super intuitive graph, however, because Engine Size is not a continuous variable, it is discrete. There was a noticeable trend that the higher horsepowers usually follow the higher engine size, but it still wasn't super clear, so instead, I created some boxplots that were more intuitive. 

#### Graph 3.1
![Graph3.1](/assets/images/HPvsEngineSize.png)

The results of the boxplots also show that the average engine size and horsepower are positively correlated. The maximum and minimum horsepowers are a bit more volatile and not as consistent of an increase. This is noticeable in cars though as you see that random car models with a certain engine size could be made to have better horsepower, whereas some super nice models may not have as high of a horsepower. These are more outlier cases though, but the averages follow the expected trend. 

### ** How does fuel efficiency vary across different car sizes? **
These features were something I was very interested in, because in the ideal world, I would want a car with the best fuel efficiency. My current car has good MPG, especially when compared with my dad's truck. But i was curious if this trend was statistically significant across many models of different sizes. 

There are so many different car models and sizes, that it was hard to view all the data without the visualization being very busy. However, I have decided to include it anyways because there are some helpful points to consider. 

#### Graph 4.1
![Graph4.1](/assets/images/FuelEfficiency.png)

It is helpful to see that there is not a significant difference in the MPG as the vehicle size chnges. There are some lower and higher gas mileages for each vehicle size, as shown in the outliers for certain models. This is expected because there are some certain car brands that make a car that meets criteria to give it a better gas mileage. They may not be the safest cars, but they do exist. This is good information, but it taught me that vehicle size isn't the only reason I should choose a certain type of car if I am looking for good gas mileage. 

### ** Which car brands are the most popular based on their market category? **
Similar to the previous question, I had a hard time making a good visualization for this because of the high number of car brands and market categories, so every visualization I made looked too busy. But a good thing this shows us is how there are some car brands that make more market categories. Like Chevrolet, a very common and popular car brand, has many more lines (representing the market categories) than Cadillac does. Some brands have a greater variety of products. 

#### Graph 5.1
![Graph5.1](/assets/images/TopCarBrands.png)

### ** Follow Ups **

**Fuel Efficiency Across Countries**
Question 4 about the fuel efficiency lead me to wonder about the fuel efficiency across the countries, so I made boxplots again to view these trends. 

#### Graph 6.1
![Graph6.1](/assets/images/FuelEfficiencyTrends.png)

I was hoping to see more drastic differences across each of the countries, but the average city MPG does not change very much across the countries. An interesting thing to note though (from the follow up in question 2 about the number of models originating in each country) is the amount of outliers for Germany, America, and Japan - who both have the highest number of car models originating there. Because there are so many models, if a new brand wants to gain traction among consumers, they need to improve the model in some way, so they could improve the feature of gas mileage to gain interest among the population of car buyers. 

**Performance Accross Country of Origin**
Finally, all of this lead me to look into the horse power and engine size by country. 

#### Graph 7.1
![Graph7.1](/assets/images/Grid.png)

I liked what I saw in this visualization, specifically the differences among the amount of engine cylinders per country. Germany has the widest spread between the minimum and maximum amount of cylinders, where France has the smallest range. 

## Dashboard
This streamlit dashboard makes it easy to look at the car features, car models, and countries of origin

[Streamlit]()

## Conclusion
In summary, this analysis through car data provided deep insights into pricing, correlations, fuel efficiency, and market trends. Exploring visualizations uncovered interesting patterns, enriching understanding across various aspects of the automotive world. For the most part, it confirmed what I had seen throughout my experience with driving and buying cars. This analysis did prompt me with further curiosity around fuel efficiency across countries and performance variations based on origin.


### Ethical Considerations

All data used was publicly made available. Part of the data was downloaded from Kaggle, and the other part from a website off of google. See my previous blog post about data collection to read further about the ethical considerations made. 


If you are interested in checking out my code and the data I used, you can find it in my [github repository](https://github.com/MaryNydegger/386-EDA-Project.git)


