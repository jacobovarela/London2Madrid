
<img src="https://image.freepik.com/free-icon/airplane-shape_318-75671.jpg" style="float: right; margin: 10px; height: 10px; width: 10px">

# London to Madrid
Exploring flight prices and building models to predict them

---

I am currently living in London, but I am constantly trying to visit Madrid to see my friends and family. Whenever I am looking to book a flight to go back home, I am always faced with the same questions:
1. How much is it going to cost me? How much should it cost me?
2. When is the right time to book a flight? When is the best time to fly?
3. From where should I fly? Which airport combination is the best?
4. Is it possible to predict the prices?

The aim of this project is to solve these questions, using the scraped data from flight aggregators such as Adioso.

Questions 1 to 3 can be answered by performing exploratory data analysis, using GroupBy functions as queries, or visualisation software Tableau.

Question 4 on the other hand is a Machine Learning problem, which will be answered by using simple regression models such as Linear, Ridge and Lasso.

---

### Scraping the data

I created a script that runs on the terminal, which accepts 2 variables:
- Airport code (LHR, STN, LGW, etc.)
- Month (1, 2 ,3, etc.)

The script then goes on to scrape flight information data from each day of a given month, from a given London airport, to Madrid. It uses the 3 APIs that Adioso.com uses, and employs BeautifulSoup to extract information. The script puts together every individual flight into a DataFrame, with its flight number, date, time and price, and it returns a csv file.

---

### Tableau visualisation

I used Tableau to answer the following questions:
- Cheapest airport?
- Cheapest month?
- Cheapest day of the month?
- Cheapest day of the week?
- Cheapest airline?
- What is a deal?

For more information on the results, please refer to the slides document in this repository.

---

### Modelling

I tried out numerous models, but I only included 2 approaches in my final presentation:

1. Predict the price for a specific flight number (for example a morning Iberia flight from LHR) based on features such as the day of the month, day of the week, and other flight prices for the same day.
  - This approach turned out to be a failure and I could not get a proper positive score using models such as Linear Regression, Lasso, Ridge, Elastic Net, or Random Forest Regressor. The reason for this could be that the feature space was too large and non-correlated to the flight price, which is the target.


2. Predict the cheapest price for a given airline in a given day (Air Europa) given the cheapest prices for other airlines.
  - This approach was a result of noticing that Air Europa does not publish prices beyond 6 months (in contrast with the almost 12 months of other airlines). The goal was to predict how Air Europa would price the following 6 months by building a model that uses just the prices of other airlines.
  - This time I had more success, and I managed to get a score over 0.6 for Lasso and Ridge regression.

---

### Next steps

One thing that I did not look into was to cross validate my models (which I thought that was not  possible to do with time series data).


As far as evolving the project and diving into more complex modelling, I think it would be interesting to consider ARIMA models and look into seasonal decomposition.


Another thing that I would love to do is to scrape past price data and try to explain flight price fluctuation, to understand when is the best time to book a flight in advance.
