---
Title: "Car Pricing Data Collection (DC) "
Author: Mary Nydegger
Description: The aim of this project is to compile datasets related to automobiles. This involves gathering information on car prices (MSRP - Manufacturer's Suggested Retail Price) and mapping each car brand to its respective country of origin. How does the country of origin influence car pricing and market preferences?
Layout: post

date: 2023-11-17 17:50:00

---

### Table of Contents 
- [Overview](#overview)
- [Data Collection](#data-collection)
- [Data Cleaning](#data-cleaning)
- [Data Building](#data-building)
- [Conclusion](#conclusion)
- [Ethical Considerations](#ethical-considerations)


### Overview

Cars, more than just machines, carry stories that go beyond their wheels. In this project, I aim to gather data about car prices (MSRP - Manufacturer's Suggested Retail Price) and connect each car brand to where it comes from. 

I am preparing to sell my car this summer, so I have been thinking about the pricing of cars and how it is determined. Throughout these thoughts and studying up about different cars, the biggest question that formed in my mind was **how does where a car is made affect how much it costs and what people prefer?**

I did this by first collecting info on car prices and trying to understand how each car brand has a different price tag and what that entails. From there, I mapped out where each car brand hails from. I linked brands to their home country to see if that had impact on what people like or how much they are willing to pay. 


### Data Collection

My data collection journey was a blend of online searches across various platforms like Wikipedia, Kaggle, and other specialized websites. I searched through these sources, sifting through numerous datasets to find the specific information I needed for my car-related project.

There are many datasets that contain data about cars and their prices, so it wasn't super difficult to find everything. But it did take time going through everything and deciding which datasets would be the most meaningful.


Data was downloaded and scraped from these locations
1. [Car Features and MSRP](https://www.kaggle.com/datasets/CooperUnion/cardataset/)
2. [What Country Does My Car Come From?](https://www.canstarblue.com.au/vehicles/car-country-of-origin/)

The Kaggle dataset was previously scraped from Edmund and Twitter. This dataset sought to analyze questions about the effects of car features on the price, brand effects on the price, and price vs. popularity. This went directly along with what I was seeking with this project. 

In the second dataset, I scraped the list of car brands and countries from what was listed and made a new dataframe. It was pretty straightforward, and this was the code that I ran to do it. 

``` py
# Web scraping to get the countries of origin for the different listed car brands

url = 'https://www.canstarblue.com.au/vehicles/car-country-of-origin/'

response = requests.get(url)
if response.status_code == 200:
    soup = BeautifulSoup(response.content, 'html.parser')
else:
    print("Failed to retrieve the page. Status code:", response.status_code)

table = soup.find('h2', text='Car Brands – Country of Origin').find_next('table')

data = []
for row in table.find_all('tr')[1:]:
    columns = row.find_all('td')
    row_data = [col.get_text(strip=True) for col in columns]
    data.append(row_data)

df = pd.DataFrame(data, columns=['Car Brand', 'Country of Origin'])
```

There were a few datasets I found on wikipedia that listed similar features to what was found in Kaggle, but I chose the Kaggle dataset over the others becauase it had so many more observations, so it would bring better results, and be hopefully more accurate. I also chose it because I liked that it was previosuly scrapewd from Twitter so it could have some interesting findings from that. I chose the next dataset about countries mainly because it was so simple and didn't require extensive scraping. A few others I found had many more columns, or didn't have super consistent models listed. But this current one was simple and easier to use. 

### Data Cleaning

Upon gathering the data, the next step involved examining the datasets. 

Ideally, my dataset would basically be the one from Kaggle with an extra column that had the country of origin for each brand. 

I started by focused on aligning the columns and ensuring the correct formatting, which is always a crucial step in preparing the datasets for merging. 

One of the focal points during this stage was identifying and ensuring consistency in the columns containing car brand information. This was essential for my subsequent exploration into the origins of these car brands. 

I originally was using data from [List of automobile manufacturers of the United States](https://en.wikipedia.org/wiki/List_of_automobile_manufacturers_of_the_United_States) on Wikipedia. It had a lot of extra data that I wasn't necessarily looking for, so after putting time into merging these tables, I backtracked and used the other dataset which I was more pleased with. 

### Data Building 

Once the dataframes had columns that were clean and could be merged, it was a simple merge with this code.

``` py
merged_df = pd.merge(MSRP, df, how='left', left_on='Make', right_on='Car Brand')
merged_df.to_csv('merged_df', index = False)
merged_df
```

From here, I switched the variable type of the MSRP column so I could view the numbers and get ready for the EDA portion (See my [next blog post](https://marynydegger.github.io/my-blog/2023/11/16/Car-Analysis-EDA.html) if you are interested in the further analysis).

#### Final Output

After building the ascribed variables to analyze scripture data in greater detail, the dataset looks as follows:

![Dataset1](/assets/images/Dataset1.png)
![Dataset2](/assets/images/Dataset2.png)


## Conclusion 
As mentioned previously, you can see the actual result of my EDA in my next blog post [Car Analysis EDA](https://marynydegger.github.io/my-blog/2023/11/16/Car-Analysis-EDA.html). The preparation for constructing this dataset was carefully completed. Exploring these car features in this part of my project as well as the EDA portion broadened my knowledge within the automotive landscape and gave me a deeper understanding of consumer behavior and industry dynamics. 

If you are interested in checking out my code and the data I used, you can find it in my [github repository](https://github.com/MaryNydegger/386-EDA-Project.git). 


### Ethical Considerations

1. Data Privacy and Legality: I ensured that the data I scraped and collected from various sources was legally and ethically obtained, and I respected the terms of use of the websites I accessed.
2. Bias and Fair Representation: I recognize that the Kaggle dataset could potentially have some biases in there as data was originally scraped from twitter. A next step would be doing this same project with a larger features table that I put together myself, with 100% confidence that it was unbiased and compare the results.
3. Data Accuracy: I ensured that the data I collected was factual and up to date - specifically from the country of origins table.
4. Avoiding Misinterpretation: As I have put together numbers (more specifically on the EDA page), I have been careful to highlight correlation, not causation. 

These measures ensured responsible and respectful data extraction while upholding website integrity.

