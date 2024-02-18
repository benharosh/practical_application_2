# Practical-App-11
**OVERVIEW**

In this application, you will explore a dataset from kaggle. The original dataset contained information on 3 million used cars. The provided dataset contains information on 426K cars to ensure speed of processing.  Your goal is to understand what factors make a car more or less expensive.  As a result of your analysis, you should provide clear recommendations to your client -- a used car dealership -- as to what consumers value in a used car.

#### Business Understanding

From a business perspective, we are tasked with identifying key drivers for used car prices.  In the CRISP-DM overview, we are asked to convert this business framing to a data problem definition.  Using a few sentences, reframe the task as a data task with the appropriate technical vocabulary.

 Business Objectives:
 * Dealerships want identify what features in used cars will drive the price of the car up.
 * Dealerships want to have good understanding of what price should they pay for a certain car with certain features, in order to maximize their ability to make profit by buying cars under market value and making profit.
 * Dealerships want to identify which used cars they should stay away from.

 
### Data Understanding

After considering the business understanding, we want to get familiar with our data.  Write down some steps that you would take to get to know the dataset and identify any quality issues within.  Take time to get to know the dataset and explore what information it contains and how this could be used to inform your business understanding.

* Data has 426K records
* Data has 3 numerical and 13 categorical columns
* Data contain many rows with NaN values. 7 columns are missing moire than 20% of their values
* Over 90% of cars are prices between `500` to `100,000` USD
* `price` data is skewed and we might want to work with the price log that shows a better uniform distribution
* There are many `price` outliers - over 35K records with price=0 and some cars with prices ober 1 billion dollar
* There are some `odometer` outliers - cars with over 500K miles, some of them with 10 million miles
* There are many duplicate records (almost 200,000) - cars that has the same `VIN ` number with the same odometer, price, mode and  manufactor
* `cylinders` and `condition ` categorical columns can show ordinallity when ranking their unique values

### Data Cleaning 
* I dropped the `id` column since it's holding a unique identifier that has no predictive meaning. 
* I dropped the `size` column since it's missing more than `70%` of its data.
* I dropped over 199K duplicated records, most of them related to cars with the same `VIN` number that had the same features as `price`, `odometer` and `year`
* I dropped the `VIN` column after cleaning the dulicates, since it's just holding a unique identifier that has no predictive meaning. 
* I remove `odometer` outliers and focused on cars with `odometer` which is less than 400K miles that captured most  (`98.5%`) of the data set.
* I remove `price` outliers and focused on cars with `price` between 500 and 100,000 USD that captured most (`91.05%`) of the data set.
* I removed all `title_status` besides `clean` in order to focus on predicting cars with clean titles. I did it since `clean` title status captures `93.77%` of the data set.
* I removed rows that were missing more than 4 values out of the coluns that showed the highest missing values - `condition`, `paint_color`, `drive`, `cylinders` and `type` columns
* I removed rows that contained `other` value and treated it as a missing value (NaN)
* I removed NaN values for colums with less than 4% of missing values `year`, `odometer`, `manufacturer`, `fuel`, `transmission` . For `year`, `odometer` it made a very good sense because these columns were very highly correlated to the price and it didn't make sense to randomly impute them.
* I imputed the missing data for the remained NaNs with `RandomSampleImputer`. I chose this imputer because it's fast and keeping the same distribution of data before and after imputation, which is very important when imputing 20-30% of missing data.
* After cleaning, and NaNs imputation, we were left with ~146K rows - `34.4%` of the original data set.

### Modelling:


### Findings
