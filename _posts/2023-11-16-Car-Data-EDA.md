---
Layout: post
Title: "EDA Semester Project"
Author: Mary Nydegger
Description: My EDA journey through car data showcased compelling visualizations, unraveling nuanced insights into pricing, correlations, fuel efficiency, and market trends, enriching the narrative of automobile dynamics.
Image: assets/images/Screen Shot 2023-11-16 at 1.47.53 PM.png
---


In my exploratory data analysis (EDA), I delved into the detailes of car data, utilizing Python libraries to craft visualizations that unraveled diverse insights. From understanding price distributions and correlations between car features to exploring fuel efficiency trends and market popularity, the EDA journey illuminated compelling patterns, enriching my understanding of the multifaceted world of automobiles.



### Questions to Explore
Before digging deeper into the analysis, I wanted to understand the data a bit more - specifically the distribution of prices from the data I have - I recognize that this may not contain everything or be completely up to date. 
###### The minimum car price is $2,000
###### The maximum car price is $2,065,902
###### The average car price is $40,594

#### 1. Car Price Distribution: What is the distribution of car prices in the dataset?


#### 2. Price Variation Across Countries: How do car prices vary across different countries of origin?
#### 3. Correlation Between Engine Size and Horsepower: Is there a relationship between engine size and horsepower?
#### 4. Fuel Efficiency Analysis: How does city MPG and highway MPG vary across different car brands?
#### 5. Market Popularity Trends: Which car brands are the most popular based on their market category?


Then, we're mapping out where each car brand hails from. This part is about linking brands to their home countries to see if that has any impact on what people like or how much they're willing to pay.



### The Big Question

The main thing we're curious about: Does knowing where a car comes from tell us anything about how much people are willing to pay for it? We're trying to figure out if a car's home country affects its price and whether it influences what people prefer. This project is our journey into discovering these connections within the world of cars.

### My Motivation

As I prepare to sell my car next semester, I've found myself deeply intrigued by the intricacies of car pricing. I've been delving into understanding why certain cars are given significantly higher prices than others in the market. This curiosity sparked a desire to compile data, seeking insights into the underlying factors that dictate these price variations. Exploring this not only satisfies my personal interest but also lays the groundwork for understanding the market dynamics that influence car values.

## Data
### Collection: 
My data collection journey was a blend of online searches across various platforms like Wikipedia, Kaggle, and other specialized websites. I searched through these sources, sifting through numerous datasets to find the specific information I needed for my car-related project.

Initially, I gathered multiple datasets from these sources, loading them into my environment for a comprehensive view. To enrich this dataset, I employed web scraping techniques to extract additional relevant information. This process ensured I had a wide array of data to analyze.

### Cleaning:
Upon gathering the data, the next step involved a meticulous examination of the datasets. I focused on aligning the columns and ensuring the correct formatting, a crucial step in preparing the datasets for merging. This standardization phase laid the groundwork for seamless merging and subsequent analysis.

One of the focal points during this stage was identifying and ensuring consistency in the columns containing car brand information. This was essential for my subsequent exploration into the origins of these car brands.

While the process seemed straightforward, it involved sharp attention to detail and a substantial amount of effort sifting through numerous websites to locate the most suitable and easily accessible data for web scraping.  

### Ethical Considerations

During web scraping, I prioritized ethical conduct by respecting website policies and terms of use. To prevent overloading servers, I implemented controlled scraping techniques, like rate limiting and request delays. I focused solely on gathering publicly available data relevant to the project's scope, ensuring no collection of sensitive or personal information. These measures ensured responsible and respectful data extraction while upholding website integrity.


## Conclusion 
You can see the actual result of my EDA in my next blog post (Cars)[]. Through the journey of compiling datasets, understanding pricing dynamics, and exploring the origins of car brands, this project has helped me build more connections within the automotive landscape. It has offered a deeper understanding of consumer behavior and industry dynamics.

The intertwined narratives discovered within the datasets not only shed light on the pricing disparities but also underscore the rich cultural and economic dimensions embedded within each car's origin. It has opened doors to further inquiries into market trends and consumer perceptions, laying the groundwork for future studies in automotive economics and consumer behavior.

If you are interested in checking out my code and the data I used, you can find it in my [github repository](https://github.com/MaryNydegger/386-EDA-Project.git)


