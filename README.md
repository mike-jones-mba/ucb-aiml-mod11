# ucb-aiml-mod11
# readme.md



## SUMMARY 

Salespeople in the pre-owned automobile markets are interested in pricing dynamics.  
The study below investigates these dynamics based on data found in the vehicles 
data set. The broad conclusion is that year and odometer are two most significant 
factors in estimating/predicting price.  Further investigation to determine 
profitibility is also suggested as a follow on study.

The CRISP-DM methodology was followed to produce this analysis and report. The 
basic outline is as follows:

    [1] BUSINESS UNDERSTANDING 
    [2] DATA UNDERSTANDING 
    [3] DATA PREPARATION 
    [4] MODELING 
    [5] EVALUATION 
    [6] DEPLOYMENT

Futher details for each step in the process are given in the section below. 



## DETAILS 

### BUSINESS UNDERSTANDING 

The vehicles data set was examined for the purpose of understanding the factors 
which impact used car sales pricing.  The clients are a consortium of Car Dealers 
who have contracted with Analytics Services for the purpose gaining insights 
into their business. This study considers which underlying factors drive sales 
performance. The resuling knowledge can be used to increase sales.  The highest 
average sales prices tend to occur with the most recently built cars that have 
the lowest milage.

The analysis and the report below is an initial survey which gives a first pass
glimpse into the data.  Next actions and ideas for follow on analysis are given 
at the end, and suggest future directions regarding additional data to collect 
as well as further areas to investigate for more insight and discovery.



### DATA UNDERSTANDING & DATA PREPARATION 

The input data file contains several columns with multiple ids, region, and 
vehicle characteristcs such as manufacturer, model, year, condition, odometer,
paint color & etc. 


BoxPlots were used to look at effect on price of other characteristics (such 
as make, model, paint_color, etc), however none of these seemed to have much
analytic value that was immediately apparent. As such these features were 
dropped from the analysis in order to focus on year, odometer & condition.  
These boxplots themselves weren't included in the final jupyter notebook
file. 

Exploratory Data Analysis (EDA) included looking at the data using Excel, 
Pandas DataFrames and SQL. The data was understood from many different
directions prior to modeling. 

The predominant features effecting sale price are a car's production year 
and odometer reading, so these as well as condition (excellent, good, fair, 
poor, salvage) were used. The analysis was limited to year, odometer & condition
as inputs.

The influence of outliers in these features was avoided by simply removing 
odometer readings greater than 400,000 (and sometimes as low as 200,000) 
as well as pricing above $200k USD (sometimes as low as $100k). These values 
were adjusted throughout the course of analysis. All years were kept. 
Note that values for condition where missing for a large number of cases 
(>25% of the data). The condition feature was given as text values. These were
tranformed into one-hot columns.

### MODELING 

The EDA included preliminary modeling with both Polynomial Regression and LOWESS.

The polynomial regression appeared to only be relevant toward the main mass of
data (i.e. high/recent year or low odometer). As one moved toward the extremities 
and further from the center, the relevance of the polynomial regression estimates 
decreased significantly to the point of becoming unusable. For years > 1995, the 
polynomial regression  estimates are pretty good, however in the years less 
than 1995 estimates are off by quite a bit.

LOWESS also gave promising estimates for pricing based on both odometer 
and year. I was able to apply LOWESS on one dimension at a time (i.e. pricing 
vs odometer or pricing vs year). 

Two additional models were also applied with multple features as input. The Year, 
odometer, and vehicle-condition were the used to make predictions via:

    SequentialFeatureSelector with LinearRegression and Lasso estimators, and 
    Grid Search with Ridge Regression.

2-D plots were made for year vs price  as well as odometer vs price. 
These were given with both actual price and Grid Search Ridge Regression estimates. 
Additionally, a 3-D plot for actual price vs year & odomoter, was given along 
with the predicted pricing. 

See the Notebook for details related to Mean Square Error (MSE) measures comparing 
estimates with predicted values. 

Futher work can be done to analyze model prediction feasibility via MSE as well 
as tuning and refining the models. Further graphical work to display the results 
for visual inspection is also advised.



### EVALUATION & FINDINGS 

Broadly speaking, the four models applied to odometer, year and condition 
all predict prices that support the following conclusion:

    Lower odometer readings as well as a more recent model-year production 
    dates lead to higher unit sales prices for the automobiles under 
    consideration. 

Although the four models differ in their specific predicted estimates at any 
given point, the overall trend is clear and appropriate for the purpose of 
business decion making.

No data was collected regarding the vehicle purchase pricing, cost of sales, 
marketing or vehicular improvement costs (or inventory holding costs & etc). 
Without costing information, it is not possible to assess which vehicle 
characteristics (and which combinations) are the most profitable. That said,
the magnitude of sale price is a good first start indication of the percieved
value in the marketplace from the standpoint of the customer. 

It is suggested to collect such costing data so as to determine net profit on
a per-unit basis. 


### DEPLOYMENT

The jupyter notebook is deployed to Github along with this readme and the 
vehicles data set for further analyisis and/or distribution.





