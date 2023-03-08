# Google DA Cyclistic Capstone
This is my Google Data Analytics Cyclistic Capstone Project

The raw data for my cyclistic capstone project is included in a url in the rmd file, remember to set the working directory accordingly and ensure that you have the required packages installed, (tidyverse, lubridate, and ggplot2)

All visualizations created are done using tableau, and can be accessed using the link in the powerpoint slide or via this link: https://public.tableau.com/views/GoogleCyclisticCapstone/Avgridelength?:language=en-US&:display_count=n&:origin=viz_share_link. 

Please start from the Cyclistic DA Capstone rmd file or the html file if RStudio is not installed, followed by the Cyclistic Capstone powerpoint.

Thanks for reading

![banner](assets/Credit_card_approval_banner.png)

![GitHub last commit](https://img.shields.io/github/last-commit/kennylam365/Google-DA-Cyclistic-Capstone)
![GitHub repo size](https://img.shields.io/github/repo-size/kennylam365/Google-DA-Cyclistic-Capstone)

Badge [source](https://shields.io/)

# Key findings: Annual and Casual members generally ride for different purposes; casual members for leisure, annual members for work.


## Authors

- [@kennylam365](https://www.github.com/kennylam365)

## Table of Contents

  - [Business problem](#business-problem)
  - [Data source](#data-source)
  - [Programs used](#programs-used)
  - [Data cleaning process](#data-cleaning-process)
  - [Quick glance at the results](#quick-glance-at-the-results)
  - [Lessons learned and recommendation](#lessons-learned-and-recommendation)
  - [Limitation and what can be improved](#limitation-and-what-can-be-improved)
  - [Run Locally](#run-locally)
  - [Explore the notebook](#explore-the-notebook)
  - [Deployment on streamlit](#deployment-on-streamlit)
  - [Repository structure](#repository-structure)
  - [Contribution](#contribution)
  - [Blog post](#blog-post)
  - [Project featuring](#project-featuring)
  - [License](#license)




## Business problem

You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. You are to find out how annual and causal riders use Cyclistic bikes differently and from your findings, design a new marketing strategy to convert casual riders into annual members.


## Data source

- [Cyclistic 2019 Q2 - 2020 Q1 Data](https://divvy-tripdata.s3.amazonaws.com/index.html)

## Programs used

- R studio (data cleaning; refer to requirement.txt for the packages used in this project)
- Tableau (data vizualisation)

## Data cleaning process
The dataset contained several missing values and outliers, which required cleaning before analysis. The following steps were taken to clean the data:

- Renaming and Reordering Columns: We renamed several columns in the dataset to make them more readable for analysis. We used the rename() function in tidyverse: dplyr library of R to accomplish this.

- Formatting Data: We also formatted several columns in the dataset to ensure consistency in the data. For example, we converted the ride_id and rideable_type column to the character using the mutate function in tidyverse library of R so that they can stack correctly.

- Removing excess data: We then identified the data which has been dropped in the beginning of 2020 and removed them from our 2019 data using the -c funtion

- Combining multiple files: We combined the files from Q2 2019 to Q1 2020 using the bind_rows function in R so the file we will be able to use the files in tableau for further analysis.

- Consolidating incosistent data: Before 2020, Cyclistic used different labels for these two types of riders, customer and subscriber, we will need to consolidate those 2 labels into the current updated casual and member labels. We used the mutate function in tidyverse library of R to accomplish this.

- Adding columns: The data can only be aggregated at the ride-level, which is too granular, we added more columns for date, month, year and day will allow us to aggregate ride data for each month, day, we formatted them into month, date, year and day of week using the as.Date function in R. "ride_length" column was also created as there is no "tripduration" column in Q1 2020 file. We added the column to the entire dataframe using the mutate function in tidyverse library of R to ensure consistency.

- Handling Outliers: We then identified the outliers in the dataset using a boxplot and decided to remove them. For example, we identified several rows where the ride_length was negative, which we deemed as outliers and removed them from the dataset. We used the !() function in R to accomplish this.


By following these steps, we were able to clean and prepare the dataset for analysis. The cleaned dataset is available in the cleaned_data.csv file, which is used in our analysis.

## Quick glance at the results

Correlation between the features.

![heatmap](assets/heatmap.png)

Confusion matrix of gradient boosting classifier.

![Confusion matrix](assets/confusion_matrix.png)

ROC curve of gradient boosting classifier.

![ROC curve](assets/roc.png)

Top 3 models (with default parameters)

| Model     	                | Recall score 	|
|-------------------	        |------------------	|
| Support vector machine     	| 88% 	            |
| Gradient boosting    	        | 90% 	            |
| Adaboost               	    | 79% 	            |



- **The final model used for this project: Gradient boosting**
- **Metrics used: Recall**
- **Why choose recall as metrics**:
  Since the objective of this problem is to minimize the risk of a credit default, the metrics to use depends on the current economic situation:

  - During a bull market (when the economy is expanding), people feel wealthy and are employed. Money is usually cheap, and the risk of default is low because of economic stability and low unemployment. The financial institution can handle the risk of default; therefore, it is not very strict about giving credit. The financial institution can handle some bad clients as long as most credit card owners are good clients (aka those who pay back their credit in time and in total).In this case, having a good recall (sensitivity) is ideal.

  - During a bear market (when the economy is contracting), people lose their jobs and money through the stock market and other investment venues. Many people struggle to meet their financial obligations. The financial institution, therefore, tends to be more conservative in giving out credit or loans. The financial institution can't afford to give out credit to many clients who won't be able to pay back their credit. The financial institution would rather have a smaller number of good clients, even if it means that some good clients are denied credit. In this case, having a good precision (specificity) is desirable.

    ***Note***: There is always a trade-off between precision and recall. Choosing the right metrics depends on the problem you are solving.

    ***Conclusion***: Since the time I worked on this project (beginning 2022), we were in the longest bull market (excluding March 2020 flash crash) ever recorded; we will use recall as our metric.


 **Lessons learned and recommendation**

- Based on this project's analysis, income, family member headcount, and employment length are the three most predictive features in determining whether an applicant will be approved for a credit card. Other features like age and working employment status are also helpful. The least useful features are the type of dwelling and car ownership.
- The recommendation would be to focus more on the most predictive features when looking at the applicant profile and pay less attention to the least predictive features.

## Limitation and what can be improved

- Combine this model with with a regression model to predict how much of a credit limit an applicant will be approved for.
- Hyperparameter tuning with grid search or random search.
- Better interpretation of the chi-square test
- Retrain the model without the least predictive features



## Run Locally
Initialize git

```bash
git init
```


Clone the project

```bash
git clone https://github.com/semasuka/Credit-card-approval-prediction-classification.git
```

enter the project directory

```bash
cd Credit-card-approval-prediction-classification
```

Create a conda virtual environment and install all the packages from the environment.yml (recommended)

```bash
conda env create --prefix <env_name> --file assets/environment.yml
```

Activate the conda environment

```bash
conda activate <env_name>
```

List all the packages installed

```bash
conda list
```

Start the streamlit server locally

```bash
streamlit run cc_approval_pred.py
```
If you are having issue with streamlit, please follow [this tutorial on how to set up streamlit](https://docs.streamlit.io/library/get-started/installation)

## Explore the notebook

To explore the notebook file [here](https://nbviewer.org/github/semasuka/Credit-card-approval-prediction-classification/blob/main/Credit_card_approval_prediction.ipynb)

## Deployment on streamlit

To deploy this project on streamlit share, follow these steps:

- first, make sure you upload your files on Github, including a requirements.txt file
- go to [streamlit share](https://share.streamlit.io/)
- login with Github, Google, etc.
- click on new app button
- select the Github repo name, branch, python file with the streamlit codes
- click advanced settings, select python version 3.9 and add the secret keys if your model is stored on AWS or GCP bucket
- then save and deploy!

## App deployed on Streamlit

![Streamlit GIF](assets/gif_streamlit.gif)

Video to gif [tool](https://ezgif.com/)
## Repository structure


```

├── assets
│   ├── confusion_matrix.png                      <- confusion matrix image used in the README.
│   ├── gif_streamlit.gif                         <- gif file used in the README.
│   ├── heatmap.png                               <- heatmap image used in the README.
│   ├── Credit_card_approval_banner.png           <- banner image used in the README.
│   ├── environment.yml                           <- list of all the dependencies with their versions(for conda environment).
│   ├── roc.png                                   <- ROC image used in the README.
│
├── datasets
│   ├── application_record.csv                    <- the dataset with profile information (without the target variable).
│   ├── credit_records.csv                        <- the dataset with account credit records (used to derive the target variable).
│   ├── test.csv                                  <- the test data (with target variable).
│   ├── train.csv                                 <- the train data (with target variable).
│
│
├── pandas_profile_file
│   ├── credit_pred_profile.html                  <- exported panda profile html file.
│
│
├── .gitignore                                    <- used to ignore certain folder and files that won't be commit to git.
│
│
├── Credit_card_approval_prediction.ipynb         <- main python notebook where all the analysis and modeling are done.
│
│
├── LICENSE                                       <- license file.
│
│
├── cc_approval_pred.py                           <- file with the model and streamlit component for rendering the interface.
│
│
├── README.md                                     <- this readme file.
│
│
├── requirements.txt                              <- list of all the dependencies with their versions(used for Streamlit).

```
## Contribution

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change or contribute.

## Blog post

The accompanying blog post for this project can be found [here](https://semasuka.github.io/blog/2022/10/12/credit-card-approval-prediction.html)
