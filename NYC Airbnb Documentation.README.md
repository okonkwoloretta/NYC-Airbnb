# Project Documentation: NYC Airbnb Data Analysis

![Picture1](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/586c9410-8612-4937-8d18-bb785eb233c1)


New York City (NYC), one of the most-visited cities in the world. As a result, there are many [Airbnb](https://www.airbnb.com/) listings to meet the high demand for temporary lodging for anywhere between a few nights to many months.

1. ## Introduction:

The NYC Airbnb Data Analysis project focuses on exploring and analyzing three datasets related to Airbnb listings in New York City. The main objectives are to convert untidy data into appropriate formats and provide insights by answering key questions related to pricing, room types, and borough-based comparisons.

2. ## Data Sources:

The project utilizes three datasets:

a) *datasets/airbnb_price.csv*: Contains information about pricing details for Airbnb listings in NYC, including listing ID, room type, neighborhood, price, minimum nights, and availability.

b) *datasets/airbnb_room_type.xlsx*: An Excel file with data about different room types offered by Airbnb hosts in NYC.

c) *datasets/airbnb_last_review.tsv*: A tab-separated values (tsv) file containing details about the last review received by each Airbnb listing in NYC.

3. ##  Data Analysis Goals:

The main goals of the analysis are to:

Find the average price per night for an Airbnb listing in NYC.

Compare the average monthly price of an Airbnb listing with the private rental market.

Determine the number of advertisements for private rooms.

Analyze Airbnb listing prices across the five boroughs of NYC.

4. ## Data Processing and Cleaning:

The project performs various data processing tasks to prepare the datasets for analysis. Key data processing steps include:

Loading the datasets using Pandas' read_csv() and ExcelFile() functions for CSV and Excel files, respectively.

Parsing the first sheet from the Excel file using xls.parse(0).

Converting the "price" column in the "prices" DataFrame to a numeric data type by removing non-numeric characters and converting it using pd.to_numeric().

Handling missing values by dropping them from the "airbnb_merged" DataFrame using dropna().

Converting the "room_type" column in the "room_types" DataFrame to lowercase and changing its data type to "category" using str.lower() and astype() methods, respectively.

Converting the "last_review" column in the "reviews" DataFrame to a datetime data type using pd.to_datetime().

``` python
# import libraries
import pandas as pd
import numpy as np
import datetime as dt

# Load airbnb_price.csv, prices
prices = pd.read_csv("C:/Users/LORA/Documents/Project NYC Airbnb Data Analysis/datasets/airbnb_price.csv")

# Load airbnb_room_type.xlsx, xls
xls = pd.ExcelFile("C:/Users/LORA/Documents/Project NYC Airbnb Data Analysis/datasets/airbnb_room_type.xlsx")

# Parse the first sheet from xls, room_types
room_types = xls.parse(0)

# Load airbnb_last_review.tsv, reviews
reviews = pd.read_csv("C:/Users/LORA/Documents/Project NYC Airbnb Data Analysis/datasets/airbnb_last_review.tsv", sep="\t")

# Print the first five rows of each DataFrame
print(prices.head(), "\n", room_types.head(), "\n", reviews.head())
```
## Explanation:

Importing necessary libraries: pandas, numpy, and datetime. These libraries are commonly used for data manipulation, numerical operations, and date/time handling in Python.

The pd.read_csv() function is used to read the "airbnb_price.csv" file, which contains Airbnb listing prices, and load it into a pandas DataFrame called prices.

The pd.ExcelFile() function is used to open the "airbnb_room_type.xlsx" file, which contains room type information, and assign it to the variable xls.

The xls.parse(0) method is used to parse the first sheet (index 0) from the Excel file xls, and the data is loaded into the DataFrame room_types.

The pd.read_csv() function is used again to read the "airbnb_last_review.tsv" file, which contains information about the last reviews for each listing, and load it into the DataFrame reviews. The parameter sep="\t" indicates that the file is tab-separated.

Finally, the code prints the first five rows of each DataFrame (prices, room_types, and reviews) using the head() method. This is done to get a glimpse of the data and verify that it was loaded correctly.

Note: The file paths used in the pd.read_csv() and pd.ExcelFile() functions contain absolute paths, which may cause issues when the code is run on different machines. It's recommended to use relative paths or other methods to handle file locations more robustly.

## Output:

![import data 1](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/1837f23e-7d79-4d4b-aa19-63455a4ea01f)


```python
# Remove whitespace and string characters from prices column
prices["price"] = prices["price"].str.replace(" dollars", "")

# Convert prices column to numeric datatype
prices["price"] = pd.to_numeric(prices["price"])

# Print descriptive statistics for the price column
print(prices["price"].describe())
```
## Explanation:

Performing data cleaning and data type conversion operations on the "price" column of the prices DataFrame.

prices["price"].str.replace(" dollars", ""): This line of code removes the string " dollars" from each value in the "price" column. This step is necessary because the values in the "price" column may contain the string " dollars" as part of their representation.

pd.to_numeric(prices["price"]): This line converts the "price" column to a numeric data type. After removing the " dollars" string, the column contains numerical values, but they might still be stored as strings. Converting them to a numeric data type (e.g., float or integer) allows for mathematical operations and more effective data analysis.

print(prices["price"].describe()): This line of code prints the descriptive statistics for the "price" column. The describe() method computes summary statistics for the numerical column, including the count, mean, standard deviation, minimum value, 25th percentile (Q1), median (50th percentile or Q2), 75th percentile (Q3), and maximum value.

By printing the descriptive statistics, you can quickly get an overview of the basic distribution and central tendency of the "price" column, such as the average price, the spread of prices, and the range of values.

## Output:

![2](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/9764e499-00bb-4caf-9329-0121ac6bbe9b)


5. ## Data Analysis and Results:

The analysis includes calculating various summary statistics, grouping data, and answering the key questions.

## Average Price per Night: 

The project calculates the average price per night for an Airbnb listing in NYC using the "prices" DataFrame and prints the result.

```python

# Subset prices for listings costing $0, free_listings
free_listings = prices["price"] == 0

# Update prices by removing all free listings from prices
prices = prices.loc[~free_listings]

# Calculate the average price, avg_price
avg_price = round(prices["price"].mean(), 2)

# Print the average price
print("The average price per night for an Airbnb listing in NYC is ${}.".format(avg_price))

```
## Explanation:

handling listings with a price of $0 and calculating the average price for the remaining Airbnb listings in NYC.

free_listings = prices["price"] == 0: This line creates a boolean mask called free_listings. It checks each row in the "price" column of the prices DataFrame to see if the price is equal to 0. The result is a boolean Series where True indicates a listing with a price of $0, and False indicates a listing with a non-zero price.

prices.loc[~free_listings]: This line updates the prices DataFrame by excluding the rows where free_listings is True, meaning listings with a price of $0. The ~ symbol is the "not" operator, which inverts the boolean values in free_listings. So, ~free_listings returns True for non-free listings, and False for free listings. By using this as a filter with loc, you keep only the non-free listings in the prices DataFrame.

round(prices["price"].mean(), 2): After removing the free listings, this line calculates the average price per night for the remaining Airbnb listings in NYC. The mean() method calculates the arithmetic mean of the "price" column, representing the average price. The round() function is used to round the result to two decimal places for better readability.

print("The average price per night for an Airbnb listing in NYC is ${}.".format(avg_price)): This line prints the average price calculated in the previous step. The average price is inserted into the string using the .format() method and displayed as part of the output message.

## Output:

![3](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/cda84470-9480-43b6-acf8-10586945f5b0)


## Monthly Price Comparison: 

The average monthly price of an Airbnb listing is computed by multiplying the daily price by 365 and dividing by 12. The comparison with the private rental market reveals the average Airbnb monthly cost and the corresponding private market cost.

```python
# Add a new column to the prices DataFrame, price_per_month
prices["price_per_month"] = prices["price"] * 365 / 12

# Calculate average_price_per_month
average_price_per_month = round(prices["price_per_month"].mean(), 2)

# Compare Airbnb and rental market
print("Airbnb monthly costs are ${}, while in the private market you would pay {}.".format(average_price_per_month, "$3,100.00"))
```
## Explanation:

Performing calculations related to the monthly cost of Airbnb listings and comparing it to the private rental market.

prices["price_per_month"] = prices["price"] * 365 / 12: This line adds a new column called "price_per_month" to the prices DataFrame. It calculates the monthly cost for each Airbnb listing by multiplying the nightly price (in the "price" column) by 365 (days in a year) and then dividing by 12 (months in a year). This assumes that the price remains constant throughout the year, which may not always be the case.

average_price_per_month = round(prices["price_per_month"].mean(), 2): After adding the "price_per_month" column, this line calculates the average monthly cost for all Airbnb listings in NYC. It computes the mean of the "price_per_month" column, rounding the result to two decimal places for readability.

print("Airbnb monthly costs are ${}, while in the private market you would pay {}.".format(average_price_per_month, "$3,100.00")): This line prints a comparison between the average monthly cost of an Airbnb listing in NYC and a hypothetical cost in the private rental market. The output message shows the average monthly cost for Airbnb listings and the assumed cost in the private market (represented as "$3,100.00"). The values are inserted into the string using the .format() method.

## Output:

![4](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/15071464-a280-4b75-aaa3-a959339fca8f)


## Room Type Frequency: 

The number of advertisements for private rooms is determined by calculating the frequency of each room type in the "room_types" DataFrame.

```python
# Convert the room_type column to lowercase
room_types["room_type"] = room_types["room_type"].str.lower()

# Update the room_type column to category data type
room_types["room_type"] = room_types["room_type"].astype("category")

# Create the variable room_frequencies
room_frequencies = room_types["room_type"].value_counts()

# Print room_frequencies
print(room_frequencies)
```
## Explanation:

Preparing the "room_type" data for analysis by converting it to lowercase, changing the data type to a categorical variable, and calculating the frequency of each room type.

room_types["room_type"].str.lower(): This line converts all the values in the "room_type" column to lowercase. It ensures that the room type categories are consistent and makes it easier to handle variations in capitalization (e.g., "Private room" and "private room" will be treated as the same category).

room_types["room_type"] = room_types["room_type"].astype("category"): After converting the room types to lowercase, this line updates the "room_type" column in the room_types DataFrame to be of the categorical data type. Categorical data type is used to represent data that has a fixed and limited set of unique values, which is suitable for the room type categories (e.g., "Private room," "Entire home/apt," "Shared room").

room_frequencies = room_types["room_type"].value_counts(): This line calculates the frequency of each unique room type in the "room_type" column. The value_counts() method counts the occurrences of each category and returns a new Series with room type categories as the index and their respective frequencies as values.

print(room_frequencies): Finally, this line prints the frequencies of each room type in the room_types DataFrame. The output will display the room type categories along with the corresponding count of occurrences for each category.

## Output:

![5](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/17ea65c2-68f4-44a0-8e43-a654f6e828e1)

```python
# Change the data type of the last_review column to datetime
reviews["last_review"] = pd.to_datetime(reviews["last_review"])

# Create first_reviewed, the earliest review date
first_reviewed = reviews["last_review"].dt.date.min()

# Create last_reviewed, the most recent review date
last_reviewed = reviews["last_review"].dt.date.max()

# Print the oldest and newest reviews from the DataFrame
print("The earliest Airbnb review is {}, the latest review is {}".format(first_reviewed, last_reviewed))
```
## Explanation:

Preparing the "last_review" data for analysis by converting it to datetime format and then finding the earliest and latest review dates.

reviews["last_review"] = pd.to_datetime(reviews["last_review"]): This line converts the "last_review" column in the reviews DataFrame to datetime format. The pd.to_datetime() function is used to parse the dates in the column and convert them to the datetime data type. This allows for easier manipulation and comparison of dates.

first_reviewed = reviews["last_review"].dt.date.min(): After converting the "last_review" column to datetime, this line calculates the earliest review date in the dataset. The .dt.date attribute is used to extract only the date component from the datetime objects, and then the .min() method is used to find the minimum (earliest) date among all the reviews.

last_reviewed = reviews["last_review"].dt.date.max(): Similarly, this line calculates the latest review date in the dataset. The .dt.date attribute extracts only the date component from the datetime objects, and the .max() method finds the maximum (latest) date among all the reviews.

print("The earliest Airbnb review is {}, the latest review is {}".format(first_reviewed, last_reviewed)): Finally, this line prints the earliest and latest review dates in a human-readable format. The output message will display the earliest review date and the latest review date extracted from the dataset.

Output:

![6](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/a85868dc-7169-46c7-9757-a75bd4aee8d1)

```python
# Merge prices and room_types to create rooms_and_prices
rooms_and_prices = prices.merge(room_types, how="outer", on="listing_id")

# Merge rooms_and_prices with the reviews DataFrame to create airbnb_merged
airbnb_merged = rooms_and_prices.merge(reviews, how="outer", on="listing_id")

# Drop missing values from airbnb_merged
airbnb_merged.dropna(inplace=True)

# Check if there are any duplicate values
print("There are {} duplicates in the DataFrame.".format(airbnb_merged.duplicated().sum()))
```
## Explanation:

merging multiple DataFrames to combine the relevant information and create a consolidated DataFrame for further analysis.

rooms_and_prices = prices.merge(room_types, how="outer", on="listing_id"): This line merges the prices DataFrame and the room_types DataFrame based on a common column, "listing_id". The merge() function is used to combine the two DataFrames. The "outer" merge is performed, meaning that all rows from both DataFrames are included in the resulting DataFrame, and matching rows are merged based on the "listing_id" column.

airbnb_merged = rooms_and_prices.merge(reviews, how="outer", on="listing_id"): After merging the prices and room_types DataFrames, this line further merges the resulting DataFrame (rooms_and_prices) with the reviews DataFrame based on the "listing_id" column. The "outer" merge is again used to include all rows from both DataFrames and merge matching rows based on the "listing_id" column.

airbnb_merged.dropna(inplace=True): This line drops any rows containing missing values (NaN) from the airbnb_merged DataFrame. The dropna() function is used with inplace=True to modify the DataFrame directly.

print("There are {} duplicates in the DataFrame.".format(airbnb_merged.duplicated().sum())): Finally, this line checks if there are any duplicate rows in the airbnb_merged DataFrame. The .duplicated() method identifies duplicate rows, and the .sum() method counts the total number of duplicates. The output message will display the count of duplicate rows in the DataFrame.

## Output:

![7](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/339f530d-fae4-4dd0-bba6-7d9fc451250c)


Borough-wise Comparison: Data from the "airbnb_merged" DataFrame is grouped by borough, and summary statistics (sum, mean, median, and count) for the listing prices are computed. The boroughs are sorted in descending order of mean price.


```python
# Extract information from the nbhood_full column and store as a new column, borough
airbnb_merged["borough"] = airbnb_merged["nbhood_full"].str.partition(",")[0]

# Group by borough and calculate summary statistics
boroughs = airbnb_merged.groupby("borough")["price"].agg(["sum", "mean", "median", "count"])

# Round boroughs to 2 decimal places, and sort by mean in descending order
boroughs = boroughs.round(2).sort_values("mean", ascending=False)

# Print boroughs
print(boroughs)
```
## Explanation:

Performing grouping and aggregation, and then printing the summary statistics based on the extracted information.

airbnb_merged["borough"] = airbnb_merged["nbhood_full"].str.partition(",")[0]: This line creates a new column called "borough" in the airbnb_merged DataFrame. The values for this column are extracted from the "nbhood_full" column using the .str.partition(",")[0] method. It splits each value in the "nbhood_full" column at the comma (",") and selects the first part, which represents the borough. This allows you to extract the borough information from the original column and store it in a separate column.

boroughs = airbnb_merged.groupby("borough")["price"].agg(["sum", "mean", "median", "count"]): After creating the "borough" column, this line groups the airbnb_merged DataFrame by the "borough" column. Then, the .agg() method is used to calculate multiple summary statistics (sum, mean, median, and count) for the "price" column within each borough group. The result is a new DataFrame called boroughs that contains the summary statistics for each borough.

boroughs = boroughs.round(2).sort_values("mean", ascending=False): This line rounds the values in the boroughs DataFrame to 2 decimal places using the .round() method. It specifically rounds the values to 2 decimal places. Then, the DataFrame is sorted in descending order based on the "mean" column using the .sort_values() method. The ascending=False parameter ensures that the DataFrame is sorted in descending order.

print(boroughs): Finally, this line prints the boroughs DataFrame, which contains the summary statistics for each borough. The output will display the borough names, along with the corresponding sum, mean, median, and count values for the "price" column.

## Output:

![8](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/27c56d5f-57be-46c2-b7a9-009109a1adbe)


## Price Range Labels: 

The "price" column in the "airbnb_merged" DataFrame is segmented into four price range labels ("Budget," "Average," "Expensive," and "Extravagant"). The occurrence frequencies of each label in each borough are calculated and printed.

```python
# Create labels for the price range, label_names
label_names = ["Budget", "Average", "Expensive", "Extravagant"]

# Create the label ranges, ranges
ranges = [0, 69, 175, 350, np.inf]

# Insert new column, price_range, into DataFrame
airbnb_merged["price_range"] = pd.cut(airbnb_merged["price"], bins=ranges, labels=label_names)

# Calculate occurence frequencies for each label, prices_by_borough
prices_by_borough = airbnb_merged.groupby(["borough", "price_range"])["price_range"].count()
print(prices_by_borough)
```
## Explanation:

creating price ranges and assigning labels to each range for the "price" column in the airbnb_merged DataFrame. Then, you calculate the occurrence frequencies for each label within each borough.

label_names = ["Budget", "Average", "Expensive", "Extravagant"]: This line creates a list called label_names, containing the labels for the price ranges. The labels are "Budget", "Average", "Expensive", and "Extravagant," and they represent different price categories.

ranges = [0, 69, 175, 350, np.inf]: This line creates a list called ranges, defining the price ranges for each category. The ranges list contains four elements that represent the upper bounds for each price category. The elements are 0, 69, 175, 350, and np.inf (numpy's representation of positive infinity).

airbnb_merged["price_range"] = pd.cut(airbnb_merged["price"], bins=ranges, labels=label_names): This line adds a new column called "price_range" to the airbnb_merged DataFrame. The values in this column are determined based on the "price" column. The pd.cut() function is used to bin the "price" values into the specified ranges using the ranges list. The labels for the bins are assigned based on the label_names list. This operation categorizes each "price" value into one of the specified price ranges and assigns the corresponding label to it in the "price_range" column.

prices_by_borough = airbnb_merged.groupby(["borough", "price_range"])["price_range"].count(): This line groups the airbnb_merged DataFrame by both the "borough" and "price_range" columns. Then, it counts the occurrences of each price range label within each borough using the .count() method. The result is a Series called prices_by_borough, with a multi-level index representing the "borough" and "price_range" combinations, and the values representing the occurrence frequencies.

print(prices_by_borough): Finally, this line prints the prices_by_borough Series, displaying the occurrence frequencies for each label within each borough. The output will show how many listings fall into each price range for each borough.

## Output:

![9](https://github.com/okonkwoloretta/NYC-Airbnb/assets/116097143/109f5859-6c4e-4a09-b0d7-257e9a450235)


6. ## Conclusion:

The NYC Airbnb Data Analysis project provides valuable insights into the pricing trends, room types, and borough-wise comparisons for Airbnb listings in New York City. The analysis offers essential information for both hosts and travelers to make informed decisions when engaging with the Airbnb platform in NYC.

7. ## Future Scope:

The project can be extended to include more sophisticated data visualization, predictive modeling, and further exploration of external datasets related to tourist attractions, transportation, or seasonal trends. Additionally, creating interactive visualizations and an accessible dashboard would enhance the usability and presentation of the analysis.
