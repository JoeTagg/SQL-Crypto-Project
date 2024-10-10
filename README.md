# SQL-Crypto-Project

## Introduction/Overview
In this project, I set about using SQL to analyse historical price data for the cryptocurrencies:

- Bitcoin
- Ethereum
- Solana
- Dogecoin
- Binance Coin

The datasets for this were taken from Kaggle ([here](https://www.kaggle.com/datasets/sudalairajkumar/cryptocurrencypricehistory)), and covered the period 2013-2021. This was very much a 101 ‘primer’ in SQL, incorporating foundational syntax, operators, commands, clauses etc. 

I used the in-browser data tool (https://www.csvfiddle.io), which was fantastically slick. I’ll link to my workspace at the bottom of the article, and the GitHub project folder can be found via the URL top of profile, in case anyone wants to explore.

Onwards!

## Step 1: Dataset Exploration and Basic Queries
Goal: To get a basic understanding of the data by retrieving key financial metrics like prices and market capitalisation for the selected cryptocurrencies.

#### SQL Syntax Focus:

- SELECT
- AS
- WHERE
- LIMIT

Before beginning the analysis, I wanted to get familiar with the dataset. I used a basic SELECT * FROM and LIMIT statement to return the first 30 rows of data.

![1728539370021](https://github.com/user-attachments/assets/aca875ce-fd74-4da9-b3ff-7a6f6ac7c471)

![1728539388990](https://github.com/user-attachments/assets/bf196482-e059-4750-b9f7-50cae4bb4847)

I also wanted a quick view of the names of the columns only, so wrote a query to return the headers.

![1728539768574](https://github.com/user-attachments/assets/016454d1-574f-4c8a-bd55-75da3576205e)

![1728540748256](https://github.com/user-attachments/assets/6e700104-22ab-493b-83ce-9d5d80f8a76d)

With more knowledge of what the dataset included, I planned to first use SELECT to retrieve specific columns like Date, Open, Marketcap, etc. I would then create alias columns using AS for clarity and presentation. The results could then be filtered using WHERE for specific currencies and time periods. And finally, as there were a large number of records, I would limit the number of rows displayed with LIMIT.

For the first query, I chose Bitcoin as the currency. I wanted to get a sense of its scale/performance, so filtered to records for the whole of January 2021. I chose it’s Open price for a bit of variation.

![1728539863914](https://github.com/user-attachments/assets/4ce6b4d8-65c5-432a-824f-ad05edee48eb)

![1728539876003](https://github.com/user-attachments/assets/6b74e878-c885-4f97-8625-6fb26d12c4f0)

It’s interesting to see a not-insignificant fluctuation in open price and marketcap around the 10-15th Jan.

The next query focused on Ethereum, filtering for only the last 7 days of transactions available in the dataset. This now looked at the High and Low prices for each day. I introduced the clause ORDER BY to sort the Dates by most recent first. On average, the price appears to fluctuate around $150-200.

![1728539898202](https://github.com/user-attachments/assets/45bf5ffe-e88c-4211-a65c-1e2c0a333489)

![1728539910957](https://github.com/user-attachments/assets/6bcb002a-563d-49fe-8549-d3ef4bcf63b6)

## Step 2: Summarise Cryptocurrency Data with Aggregation
Goal: To summarise key metrics like total trading volume, average prices, and total market cap over specific periods for each cryptocurrency.

#### SQL Syntax Focus:

- GROUP BY
- SUM
- AVG
- COUNT

I planned to make use of SUM, AVG, and COUNT to calculate total volume, average price, and count of records. I would then apply GROUP BY to aggregate data for each cryptocurrency, month, or year. Finally, I aimed to track trends over time using grouped data (e.g., monthly averages, yearly totals).

The first query used SUM to find the total trading volume for Bitcoin in a given year. The result: a ridiculous volume of shares, more than I can comprehend.

![1728539945392](https://github.com/user-attachments/assets/e21173c7-2191-41e6-a80c-40e8f305240d)

![1728539959260](https://github.com/user-attachments/assets/d1b86e4a-d66d-433c-8894-957f21062dcd)

The next query switched to finding the average closing price for Ethereum for each month of 2020. This was achieved using aggregate function AVG, which I also enclosed in the rounding command ROUND, to remove the decimal points.

The GROUP BY was finally used to aggregate the results by the month data found in the Date column. Small fluctuations across the year, but overall, a huge increase. Approx. 300% in 12 months?!

![1728539983694](https://github.com/user-attachments/assets/827ae55f-5140-474c-97cb-72967b51ba71)

![1728539995589](https://github.com/user-attachments/assets/c4a5d2d5-1460-4495-bdc3-941259b8f3d0)

And the final aggregate function used was COUNT, where I totalled the number of recorded trading days for each currency in 2018.

Unsurprisingly, most came back as 365. I was curious about Binance coin only showing 159. Sure enough, a quick Google search reveals that it had its IPO in 2017, becoming a stablecoin in 2018. I suspect this might explain at least some of the lack of recorded trading data.

![1728540017400](https://github.com/user-attachments/assets/610be745-2572-4bb9-9f04-1efb733057a0)

![1728540029265](https://github.com/user-attachments/assets/45901f3a-7984-4cc4-8ec0-e13f0b28ce54)

## Step 3: Analyse Cryptocurrency Price Movements Using Conditions
Goal: To use logical operators to filter data based on conditions like significant price movements, market cap thresholds, and trading volumes.

#### SQL Syntax Focus:

- WHERE
- AND
- OR
- NOT

I aimed to use logical operators like AND, OR, and NOT to combine multiple conditions in the WHERE clause. I would then filter for significant price movements (e.g., closing price greater than opening price). And finally, set thresholds for volume or market cap to focus on days with substantial trading activity.

Knowing only that Bitcoin was the major/most valuable cryptocurrency, I wanted to get a sense of the scale of it. The first query looks to find days where its close price was over $50k AND market cap over $1tr. The result: many, many days in this (limited) data set where that criteria was met…insane sums of money!

![1728540062934](https://github.com/user-attachments/assets/e73cd56a-b912-4287-bace-c106f15631f2)

![1728540072634](https://github.com/user-attachments/assets/cfab54dd-6208-4507-a877-e80b42a1a866)

Next up was to look at Solana, a decidedly lower value currency by compariso. Now I wanted to use inequality symbols (<>), in conjunction with AND (within WHERE), to see the days where its close price was lower than its open. In other words, a price drop.

![1728540092116](https://github.com/user-attachments/assets/c8da8675-191e-42cc-a6b6-d84cd9843462)

![1728540104748](https://github.com/user-attachments/assets/a55ed8f7-59ae-41fe-9d6d-e2c37d01a2a7)

And the final query explored Dogecoin (woof woof), and its trading volume. I used the inequality symbol < in combination with the operators AND NOT. I suppose > 10000 would have worked to an extent, but I don’t think it’d pick up a volume of 10000 exactly. It would have to be > 9999 to capture everything. So AND NOT (as I understand it) effectively means rows where the Volume is greater than or equal to 10000.

It looks like the coin launched in 2013. I suspect the apparent lack of $ values in the Open/Close columns (despite obvious trading volume) means the value was less than $0.00 for quite a while.

![1728540125789](https://github.com/user-attachments/assets/51620719-9586-4948-ad76-ed81f32ce761)

![1728540137333](https://github.com/user-attachments/assets/3d793d6f-52de-40f0-9b1a-23229e2e74de)

## Step 4: Rank and Compare Cryptocurrencies
Goal: To rank the cryptocurrencies based on metrics like total trading volume, average price, or market capitalisation. Using ORDER BY, MAX and LIMIT to highlight the top-performing cryptocurrencies.

#### SQL Syntax Focus:

- ORDER BY
- MAX
- LIMIT

I would use ORDER BY to sort cryptocurrencies by total market cap, highest closing price, and other metrics. I’d incorporate LIMIT to focus on the top performers within a certain metric (e.g., highest market cap or price). And a spot of aggregation (MAX, SUM) and sorting to generate rankings.

This first query aimed to return the top 3 currencies by total marketcap in 2019. I applied the SUM aggregate function to Marketcap, GROUP BY to the currency Name, and then ORDER BY DESC, to rank them highest to lowest. Whilst they are all absolutely massive numbers, note Bitcoin still has an extra digit on the others!

![1728540170728](https://github.com/user-attachments/assets/2f625d39-7322-43e0-85aa-86e1abd773b4)

![1728540180982](https://github.com/user-attachments/assets/e306d10d-6759-4f44-b988-5da96c865b44)

I went more specific with the next query, ranking the 5 currencies by their highest closing price for the first half of 2021. The MAX aggregate function was used against the close price, and the WHERE start/end dates were set with BETWEEN coupled with AND. The results were then ranked (ORDER BY) highest (MAX) to lowest closing price.

![1728540203516](https://github.com/user-attachments/assets/d05ebe49-68fe-49d7-8c1b-91f47fd94fcd)

![1728540216390](https://github.com/user-attachments/assets/49276bfc-25de-4f7a-a1c1-51475de5501a)

## Step 5: Full Cryptocurrency Analysis and Reporting
Goal: To perform a more comprehensive analysis that investigates cryptocurrency trends, price changes, market cap growth, and volatility for the five selected cryptocurrencies.

#### SQL Syntax Focus:

- Combine all clauses (SELECT, WHERE, GROUP BY, ORDER BY, LIMIT, etc.)

The aim was to now do some big picture analysis, looking at how the cryptocurrencies performed against one another. I would apply all aggregate functions to multiple columns, before using extended grouping and ordering to make sense of the results.

In this first query, I utilised SUM, AVG, and MAX/MIN functions. MAX/MIN were used against the High/Low price columns to establish volatility: how much the price of a coin has moved up or down over time.

![1728540259113](https://github.com/user-attachments/assets/e1e6c7c3-f633-4883-bfed-c55e8b0f0582)

We can see that Bitcoin has the highest volatility. With a bit more Googling, I’m sure I’d find a way to plot Volatility against the Average Closing Price, to compare the relationship between the two for each currency. Coefficient of Variation, maybe? Regardless, “Win Big, Lose Big with Bitcoin” I think is the main takeaway.

![1728540301815](https://github.com/user-attachments/assets/be1e49f7-64d4-463e-88c6-a52e8f902020)

And for the grand finale, I wanted to see Average Closing Price and Total Market Cap changes, for each currency, grouped by year. Using GROUP BY and ORDER BY for both the Name and Year column helped turn the mass of data into a very neat table.

![1728540319805](https://github.com/user-attachments/assets/dc38f065-57c7-4990-916b-7b1a3483c40e)

From this it looks like Binance coin made a great leap in value/marketcap from 2020 to 2021. Bitcoin escalated in both metrics at a ridiculous pace, especially in the final 3 years of data. Interestingly, there seems to have been a dip from 2014 to 2015. More investigation could reveal that curious anomaly. Dogecoin total marketcap showed strong growth, but appears to have never broken the $1 closing price. (Postscript: it still hasn’t.) Not pictured, Ethereum fluctuated for the first few years, before making a big jump in closing price in 2021. And Solana, only being launched early 2020, had a small amount of recorded data, but made a (relatively speaking) big jump from 2020 to 2021 as well.

![1728540338627](https://github.com/user-attachments/assets/86780bfe-cafc-4dbb-b3fb-af30f6a54c06)

Overall, the data would suggest a considerable uplift in investor interest in cryptocurrencies in  the last two years of data. Prior to this, almost all currencies displayed high volatility. Analysing price volatility change over time could reveal whether this has settled as the currencies become/became more established.

## Conclusion

Despite the data being a few years old now, one big takeaway was the sheer scale of trading volume and amounts of money we’re talking about. Of course, it’s clear too that this type of trading asset comes with a huge level of risk and uncertainty.

This was a very satisfying tour of SQL’s fundamental syntax, and will be a great springboard into another (more involved) project.

The link to csvfiddle.io workspace is: here. The .csv file and project information can be found on GitHub (URL top of profile). You’d need to upload CSV file as ‘New Table’ in csvfiddle to explore fully. And finally, forgive my inconsistent use of upper/lower case SQL syntax. It’s quite painful to see in retrospect…

This was a very satisfying tour of SQL’s fundamental syntax, and will be a great springboard into another (more involved) project.

The link to csvfiddle.io workspace and project information can are also included in this repo. You’d need to upload CSV file as ‘New Table’ in csvfiddle to explore fully. And finally, forgive my inconsistent use of upper/lower case SQL syntax. It’s quite painful to see in retrospect…
