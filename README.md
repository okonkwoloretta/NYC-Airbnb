

# NYC Airbnb Data Analysis

This project focuses on analyzing Airbnb data in New York City (NYC) to gain insights into pricing, room types, and reviews. The project involves working with three datasets: "airbnb_price.csv," "airbnb_room_type.xlsx," and "airbnb_last_review.tsv." The main goal is to convert the untidy data into appropriate formats for analysis and answer key questions related to pricing, room types, and borough comparisons.

## Key Questions

What is the average price, per night, of an Airbnb listing in NYC?

How does the average price of an Airbnb listing, per month, compare to the private rental market?

How many adverts are for private rooms?

How do Airbnb listing prices compare across the five NYC boroughs?

## Technologies Used

The following libraries were used for data manipulation and analysis:

Pandas: for data manipulation and analysis

NumPy: for numerical operations

DateTime: for date and time handling

## Code  and Output

The code provided in this project performs various tasks, including data loading, cleaning, merging, and analysis. Here are some highlights of the code:

Loading the datasets into pandas DataFrames.

Cleaning the "price" column by removing whitespace and converting it to a numeric data type.

Calculating the average price per night for NYC Airbnb listings.

Adding a new column for the price per month and comparing it with the private rental market.

Converting the "room_type" column to lowercase and categorizing it.

Extracting the borough information from the "nbhood_full" column.

Calculating summary statistics by borough.

Creating price ranges and assigning labels to categorize the listings.

Calculating occurrence frequencies for each label within each borough.

The [DOCUMENTATION](https://github.com/okonkwoloretta/NYC-Airbnb/blob/main/NYC%20Airbnb%20Documentation.README.md) provides a summary of the steps involved in the code, explanations of each section, and its corresponding output. For a detailed understanding of the code and analysis, please refer to the [code snippets](https://github.com/okonkwoloretta/NYC-Airbnb/blob/main/NYC%20Airbnb%20Data%20Analysis.ipynb) and explanations provided in this documentation.

Feel free to explore the code further and customize it according to your specific requirements.

Happy analyzing!
