Github Repository URL : https://github.com/ADA-SITE-ENCE-3503/team-project-team-project-team-43.git

Ali Hasanli - > 25% -> Built machine learning model to predict price
Elgun Atayev - > 25% -> Extracted initial data from HTML 
Farid Mikayilov - > 25% -> Processed initially scraped data
Fuad Orujov - > 25% -> Built visualizations from processed data


The project aims to gather building data on Azerbaijan and get insights from the current market situation.
For this, the first task is to gather the data from the most famous building seller website in Azerbaijan - bina.az.
First, we read their guidelines about legality. Based on their robots.txt, we had to wait at least 10 seconds pre-request.
Then we delve into the website frontend design to understand the style that the website is created, and find out which data is present and can be useful.
We discovered that per a single page, about 24 buildings' information can be extracted. This means that 5 or more pages of data would be enough for the scope of this project.
The important part of web scraping is finding the correct selectors. We carefully analyzed the HTML and had many test runs to gather all important data successfully.
Using Python's famous requests library, we send a request to bina.az, get back HTML, extract data from HTML, and after gathering all data in a data frame, store it into a CSV file.

In the next part, we processed data from multiple perspectives:
1) Extract post_id from href of post
2) Filled empty products_label with default
3) Extracted the numeric price from the price string
4) Extracted the numeric room_count from room_count string
5) Extracted floor_number of and total_floors from a single floor string
6) Extracted region and added_time from single city_and_added_time string
7) Processed added_time further with parsing it via process_added_time function
8) Processed area to get single float value
9) Lastly, moved post_id to be first column and dropped unnecessary columns (that were processed to create new columns)

Next, we tried to look for empty values, and thanks to successful data extraction, we got 0 results (products_label being default means regular users added their buildings data, so we gave it 'default' default value)
Then we saved the data into another CSV file.

However, we still wanted to visually see some aspects of our data
o we implemented the below graphs

1) Property price distribution to understand what ranges are most buildings
2) Location histogram to find out the most famous locations for buildings in Azerbaijan
3) Correlation map among numeric data - mostly to understand which variables have the highest relation with price
4) Outlier analysis to understand how many building data can be classified as outliers.

Lastly, we applied machine learning model to predict price of a building based on other variables that we thought to have impact - availability of bill of sales, mortgage and repair,
location, area, room count, floor number and total floors
Since location is not a numeric value, we just onehotencoder. For others that have numeric data, we use StandardScaler
We created our pipeline with random forest algorithm.
And with 80/20 data split on train and test, we got around 70% R^2 Score. 
To make it better, other models can be tested, or more pages can be scraped to acquired more stable data.
