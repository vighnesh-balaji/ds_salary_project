# ds_salary_proj

## Data Science Salary Estimator: Project Overview
- Created a tool that estimates data science salaries (MAE ~ $ 11K) to help data scientists negotiate their income when they get a job.
- Scraped over 1000 job descriptions from glassdoor using python and selenium
- Engineered features from the text of each job description to quantify the value companies put on python, excel, aws, and spark.
- Optimized Linear, Lasso, and Random Forest Regressors using GridsearchCV to reach the best model.
- Built a client facing API using flask

## Code and Resources Used
Python Version: 3.9
Packages: pandas, numpy, sklearn, matplotlib, seaborn, selenium, flask, json, pickle
For Web Framework Requirements: pip install -r requirements.txt
Scraper Github: https://github.com/arapfaik/scraping-glassdoor-selenium
Scraper Article: https://towardsdatascience.com/selenium-tutorial-scraping-glassdoor-com-in-10-minutes-3d0915c6d905
Flask productionization: https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2

## Web Scraping
Tweaked the web scraper github repo (above) to scrape 1000 job postings from glassdoor.com. With each job, I got the following:

- Job title
- Salary Estimate
- Job Description
- Rating
- Company
- Location
- Company Headquarters
- Company Size
- Company Founded Date
- Type of Ownership
- Industry
- Sector
- Revenue
- Competitors
- Data Cleaning

After scraping the data, I needed to clean it up to make it usable for our model. I made the following changes and created the following variables:

Parsed numeric data out of salary
Made columns for employer-provided salary and hourly wages
Removed rows without salary
Parsed rating out of company text
Made a new column for the company state
Added a column for if the job was at the company’s headquarters
Transformed the founded date into age of company
Made columns for if different skills were listed in the job description:
- Python
- Excel
- AWS
- Spark
- Column for simplified job title and Seniority
- Column for description length


## EDA
I looked at the distributions of the data and the value counts for the various categorical variables. Below are a few highlights from the pivot tables.

![positions_by_state](https://github.com/vighnesh-balaji/ds_salary_project/assets/39007695/4c41e44c-62de-4e3f-9c1d-b82af8fc0023)
![correlation_visual](https://github.com/vighnesh-balaji/ds_salary_project/assets/39007695/7450b69c-e72f-4f17-a0ea-79712d5c257e)
![salary_by_job_title](https://github.com/vighnesh-balaji/ds_salary_project/assets/39007695/76fb5aa9-32e6-47af-9e6a-ae0ff685ce5c)


## Model Building
First, I transformed the categorical variables into dummy variables. I also split the data into train and test sets with a test size of 20%.

I tried three different models and evaluated them using Mean Absolute Error. I chose MAE because it is relatively easy to interpret and outliers aren’t particularly bad for this type of model.

I tried three different models:

- Multiple Linear Regression – Baseline for the model
- Lasso Regression – I thought a normalized regression like lasso would be practical because of the sparse data from the many categorical variables.
- Random Forest – Again, with the sparsity associated with the data, I thought that this would be a good fit.


## Model performance
The Random Forest model far outperformed the other approaches on the test and validation sets.

- Random Forest: MAE = 11.22
- Linear Regression: MAE = 18.86
- Ridge Regression: MAE = 19.67


## Productionization
In this step, I built a flask API endpoint that was hosted on a local webserver by following along with the TDS tutorial in the reference section above. The API endpoint takes in a request with a list of values from a job listing and returns an estimated salary.
