# Case-Study-Sales-Data-Analysis
Sales data analysis for a made up company.

## Data Sourcing
The data sourced for this repository/data analysis comes from a youtube video for practicing applicable analysis skills. In the description of the youtube video is the zipped file containing the sales data. The data is free use and not from a real company. Click this ![link](https://www.youtube.com/watch?v=eMOA1pPVUc4&t=4464s&ab_channel=KeithGalli) to find the aforementioned Youtube video.

## Business Question
The team at Imagine Airy Electronics needs highlevel analysis done on their most trending products. Their goal is to gain insights that could increase the amount of people purchasing their product, and changing pricing based on quantity of product sold. In order to accomplish this task, we've been asked to answer 5 subquestions in order to generate the needed insights for business development.
* Sub Question 1: What was the best month for sales?
* Sub Question 2: What city sold the most product?
* Sub Question 3: What time should we display advertisements to maximize the likelyhood of customers buying the product?
* Sub Question 4: What products are most often sold together?
* Sub Question 5: What product sold the most?

## Data Cleaning/Analysis

#### Data Structure
The data inside of the csv files are structured as follows:
* Order ID ; String
* Product ; String
* Quantity ; String
* Price Each ; String
* Order Date ; String
* Purchase Address ; String

#### Processing Plan:
Looking at the structure of the data we can see that many of the columns are strings, this will make it difficult to manipulate when we go answer the questions posed by the business. Firstly, we need to check and clean every column for Null values or other blank cells that may disturb out analysis. Afterwards we need to convert the data type of the applicable columns to numbers so that we can manipulate them later in the analysis. Once all the cleaning is done then we can proceed to the analysis. Once the analysis is complete I plan to export the answers to the business questions to separate csv files to make loading the data into Tableau.

##### Documentation of Cleaning Data
1. To start the cleaning off, we have to first merge the data together from 12 files down to one master file, and once we have the data merged into one CSV file we can then name a dataframe using the data stored inside the aggregated file as the source.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Clean1.JPG)

2. After merging all the files into one dataframe, we can begin the cleaning process by first checking for any Null values, and then removing the null values if there are any by using the pandas dropna method. We specify the parameter 'all' for how to remove all instances of any null values there may be in the dataframe. Removing these nulls is important so that we can create calculated columns without any problems.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Clean2.JPG)

3. Once all the Nan values have been cleaned we can then move onto the data preprocessing portions whereby we set up the columns we will need in order to do the analysis and visualization later on. While this step is completely a preference I prefer to have all my variables ready before starting analysis. To start off, we simply create a new column in the dataframe called 'Month' whereby we take the first 2 indexes in the 'Order Date' column to get the month's number. Furthermore in this step while I was looking through the data, I noticed that there was a mistake that the scaping tool had made in that there were rows of data tha had 'Or" inside the cell. Removing these values would be necessary in order to be able to calulate revenue and perform other numerical transformations without running into any issues. There are many ways 
