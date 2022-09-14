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

3. Once all the Nan values have been cleaned we can then move onto the data preprocessing portions whereby we set up the columns we will need in order to do the analysis and visualization later on. While this step is completely a preference I prefer to have all my variables ready before starting analysis. To start off, we simply create a new column in the dataframe called 'Month' whereby we take the first 2 indexes in the 'Order Date' column to get the month's number. Furthermore in this step while I was looking through the data, I noticed that there was a mistake that the scaping tool had made in that there were rows of data tha had 'Or" inside the cell. Removing these values would be necessary in order to be able to calulate revenue and perform other numerical transformations without running into any issues.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Clean3.JPG)
There are many ways of approaching getting rid of the 'Or' cells but I chose to just create a filter that includes all the data that != to 'Or' and recreated a dataframe that doesn't have the value inside of it.

4. Once we've removed the Or cells, we are now able to convert our Mont, Quantity Ordered, and Price Each columns to numeric values from string objects. To do this, we call upon the pandas method to_numeric.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Clean4.JPG)

5. Once the columns are converted to an intiger or float value, we are able to then create a calculated column for Sales revenue by multiplying the price each column and quantity ordered column together.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Clean5.JPG)

6. Next, we needed to split the Purchase address column into a more useable format. To do this we used the str.split method to split the column using a delimiter of ',' and then putting the out put into its own column by defining a dictionary and having expand = True written.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Clean6.JPG)

7. Now that we have the three columns for street, city, and state and zip, we must make sure that there aren't any extra spaces at the beginning or the tail of the string so that when we use the split funciton later, we will have the right character index. In order to do this we simply use the str.strip method to get rid of any unwanted spaces.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Clean7.JPG)

8. For question 2 they ask what city sold the most product. Thinking ahead, when we analyze the products sold by city how are sure that the cities listed aren't unique values. Take for example, Portland Oregon, and Portland Maine. When we do the analysis later we must be sure to account for citis in different states that have the same names. To account for this, we need to access the state portion of the State and zip column only, and drop any unnecessary columns in the process.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Clean8.JPG)

9. Lastly, we need to access the time products were purchased, and so to do this we simply use the str method to specify what part of the string to pull into a new column for purchase time.

![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Clean9.JPG)

##### Documentation of Analyzing Cleaned Data

1. To Answer Question 1, what was the best month for sales? How much was earned in that month? We simply just had to group the dataframe by month and take the sum of the sales revenue. After running this and printing our new variable, we find that December was the highest sales month at $4,613,443.34. Then we take the completed table and export it into a csv to use for visualization later.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Analysis1.JPG)

2. Similarly, the next question, Question 2, asks what city sold the most product. In order to find this we can use a similar method as the first question. First we create a new column called City State which takes into account the Portland Oregon versus Portland Maine hurdle I mentioned earlier. Then after creating this column, we will simply group the data frame by the City State and take the sum of all values, including products sold. After printing the answer you'll be able to see that San Francisco CA sold the most product. Finally we exported it to a csv file to use for further visualization later.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Analysis2.JPG)

3. 
