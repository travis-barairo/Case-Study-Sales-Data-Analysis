# Case-Study-Sales-Data-Analysis
Sales data analysis for a made up company.

## Data Sourcing
The data sourced for this repository/data analysis comes from a youtube video for practicing applicable analysis skills. In the description of the youtube video is the zipped file containing the sales data. The data is free use and not from a real company. Click this ![link](https://www.youtube.com/watch?v=eMOA1pPVUc4&t=4464s&ab_channel=KeithGalli) to find the aforementioned Youtube video.

## Business Question
The team at Imagine Airy Electronics needs high level analysis done on their most trending products. Their goal is to gain insights that could increase the amount of people purchasing their product, and changing pricing based on quantity of product sold. In order to accomplish this task, we've been asked to answer 5 subquestions in order to generate the needed insights for business development.
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

3. Moving on to Question 3, What time should we display advertisements to maximize the likelyhood of customer's buying the product, we can simply create a new column named Purchase hour, and pass in the str method along with the index of 0:2 to take the hour of the purchase. After this we can then group the dataframe by the Purchase Hour and compare it to the sum of the Sales Revenue to get that 7 PM or 19 UTC was the highest amount of sales. We then created a csv to help load into Tableau later on.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Analysis3.JPG)

4. Question 4 is where it gets a bit tricky. The question asks, "What products are most often sold together?" Although it may seem simple the solution was quite difficult to come accross. First, we have to create a new dataframe identifying duplicate Order ID's. What this does for us is shows us which transactions were under the same order id and what products were sold in these transactions.
5. After creating this new data frame we have to create a Grouped Products column to show the products that were bought together. We do this by grouping the dataframe by Order ID and passing the Product column into the transform method which allows us to, depending on the set delimiter and for every item in the column join the two products on the delimiter. 
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Analysis4.JPG)
6. Lastly, for this step atleast, we drop the duplicate orders that were already accounted for by using the drop_duplicates method with a criteria of Order ID and Products Grouped.
7. After creating the new data frame with the grouped products, we can then use the counter method inside of the collections library and combinations from the itertools library to create a for loop that will, for every row in Products Grouped, split the row on the comma, and then update the counter by counting the split combinations that resulted from the row_list by pairs. Once this for loop is done, we can then use the count function and pass in the 10 most_common combinations to see the top 10 items purchased together.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Analysis5.JPG)
8. Finally after much deliberation, we can then turn the count.most_common(10) into a DataFrame to then export as a CSV using the to_csv method.

![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Analysis6.JPG)

9. Lastly Question 5 asks us what product sold the most and to postulate as to why? To answer the first part is fairly straight forward. All we have to do is group the data frame by Product and compare it with the sum of values, which we can do after we export it to a CSV and visualize in Tableau.

![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Analysis7.JPG)

So far we've been able to uncover and answer the five questions posed for us. Now all there's left to do is to put it into visual format so that it is easier for us to understand the insights that we've discovered.

## Data Visualization
*Click this [link](https://public.tableau.com/app/profile/travis.miguel.barairo/viz/Project2SalesDataAnalysis/SalesAnalysisDashboard) to view the dashboard and any specific details on Tableau!*

### Question 1: What was the best month for sales, and how much was sold that month?
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Vis1.JPG)
Seeing from the graph above, the largest month for sales was in December generating over $4,613,443. This can be attributed to many factors such as Christmas Season being in December. Interestingly as well is that we see a large spike in sales starting in the last quarter of the year, which is unsuprising since this season has events such as Black Friday, Cyber Monday, Christmas, and Thanksgiving that can be a large driver of spending.

### Question 2: What city sold the most product?
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Vis2.JPG)

According to my visualization, we can see that the city in which our company's products sold the most in was San Francisco, California which generated $8,262,204 worth of revenue, a whopping 65% more than the next highest city Los Angeles which is only at $5,452,571.

### Question 3: What time should we display advertisements to maximize the likelyhood of customers buying the product?
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Vis3.JPG)

According to the amount of quantity ordered by hour, we should be advertising our products at 19 UTC or 7 PM. Additionally, in order to increase customer's likelyhood of purchasing our products we should also consider showing advertisements around 12 UTC which will account for both peaks of purchasing activity within a customer's day.

### Question 4: What products are most often sold together?
The top 10 products that are most sold together are as shows:
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Vis4.JPG)

Although, the top 10 is shown, we can see that the majority of combinations is for customers to purchase a highly branded phone and their respective charging cable. Going down the list we can see the custmers purchasing different sorts of Wireless headphones and wired headphones.

### Question 5: What product sold the most? Why?
To answer this question, I decided to plot all the available products the company sells and compare their total Quantity Sold versus the total Revenue Generated.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Vis5.JPG)
Looking at the most ordered product, we can see that AAA batteries, AA batteries, USB-C charging cords, and Lightning charging cords make up the largest quantity of orders. Although they make up the majority of orders from our company, interestingly enough, most of the revenue generation is driven by the higher ticket items.
![](https://github.com/travis-barairo/Case-Study-Sales-Data-Analysis/blob/main/Images/Vis6.JPG)
From this chart, its plain to see that the largest drivers of revenue are the Macbook pro laptop, the ThinkPad laptop, iPhone, and Google phone. Notice that in the previous chart, the Batteries and lightning cords made up the bulk of the orders, but according to revenue they are nowhere near the amount generated by the big ticket electronics the company keeps in stock.

In terms of quantity ordered, it makes sense that things such as batteries are sold the most because they are used outside of just charging electronics. They are a normal household product that most people will keep in stock. Interestingly enough the next two highest in terms of quantity ordered were the lightning cables and chargers. This can be attributed to the fact that the chargers are relatively fragile and may break easier or get lost which influences the user to buy more.

When looking at the revenue generated however, it makes sense that the more valuable electronic items drive most of the revenue generation, due to their higher price point. Although they make up only 15% of the amount of orders that both battery types combined had, the Macbook pro laptop and the ThinkPad laptop made 98% more revenue than the batteries.

## Reccomendations:
To increase the amount of people purchasing their products, and as well as to grow their business even further, Imagine Airy Electronics should:
* Start advertising heavily starting in September, this is due to the fact that there is a large spike of sales during the last 3 months of the year, and promoting products before this time will only increase sales greatly.
* Furthermore, the company should focus on advertising heavily in San Francisco, Los Angeles, New York, and Boston as these four cities make the majority of where their products are being purchased from. Having more advertising in these areas will be more cost effective as we can see from the data that the people in these cities are more willing to buy the product, so a little advertising may push them to buy even more.
* As for when they should advertise on a daily basis, Imagine Airy should advertise more during the hours 9 am - 1 pm and then again later at night starting at 5 pm - 9 pm. By aiming advertisements to release during these times, Imagine Airy can influence the most amounts of people to purchase their products.
* Outside of advertising, Imagine Airy can sell bundles for most bought items. These bundles are given for the most sold pairs, and can be at a discounted rate. If these bundles are offered, the amount of purchases will increase drastically due to consumer perception of a lower price, thus driving more revenue for the company. The items the company should bundle together are: the iPhone and Lightning charging cable, the Google Phone and the USB-C charging cable, the iPhone and Wired Headphones, and the Google Phone and Wired Headphones.
* In terms of stocking and pricing, I reccomend that Imagine Airy Electronics sells Macbooks, iPhones, and ThinkPads at a discounted rate of 10% off. By doing this it will incentivize customers to purchase more of these items, and seeing as how these three products are the main drivers of revenue generation, having more people ordering these electronics will drive our profits even higher.

