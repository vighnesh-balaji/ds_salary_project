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

