## Title

911 Call Analysis for Crime Hotspots Prediction and Response Optimization

## Team

Mansi Gopani - mansigopani
Heet Gala - heetgala
Hemanth Chowdary - ThammineniHemanthChowdary
Kunal Ahirrao - kuunnnaaaalllll

## Overview

By addressing Heilmeier's catechism, we can provide insight into the following:
Question 1 - What are you trying to do?
The project aims to improve emergency response systems and enhance public safety in New York City by analyzing NYPD call data. By
examining historical records, we aim to uncover insights that can help emergency services respond more effectively to critical situations.
Additionally, we aim to develop a model that can predict crime incidents in specific areas. This proactive approach can enable law
enforcement agencies to allocate resources more effectively, contributing to a safer and more secure environment for residents and
visitors alike.
Question 2 - What is new in your approach and why do you think it will be successful?
Our approach to analyzing NYPD call data for improving emergency response and predicting crime in New York City is unique in its
thoroughness and methodology. By focusing on detailed data points such as incident timing, location, and call nature, we aim to extract
meaningful insights. Through advanced data analysis and machine learning techniques, we intend to develop a predictive model. This
model can help identify crime-prone areas and optimize resource allocation. Overall, our approach has the potential to significantly
enhance public safety in the city.
Question 3 - Who cares? If you are successful, what difference will it make?
If our project succeeds, it could greatly improve emergency response systems and enhance public safety in New York City. This would directly benefit law enforcement agencies, key stakeholders, by allowing them to use resources more efficiently and respond more effectively to emergencies, possibly leading to lower crime rates. Additionally, government agencies and city officials would be interested in the results to improve how they make policies and allocate resources. Ultimately, the general public, who are indirect stakeholders, in New York City would benefit from safer communities and better emergency services.

We are focused on predicting the response time of law enforcement and emergency medical units  

## Data

Dataset is taken from : https://data.cityofnewyork.us/Public-Safety/NYPD-Calls-for-Service-Year-to-Date-/n2zq-pubd/about_data

The following image shows the number of incidents reported based on the location.
![my image](location.png)

The following image shows the number of incidents reported based on the location.

## Preprocessing

The steps included in preprocessing of data are as follows:

The time difference in minutes between 'ARRIVD_TS' and 'DISP_TS' columns was calculated and stored in the 'Time_Difference_Minutes' column in the 'nypd_data' DataFrame. Rows where the time difference was less than 0 were filtered out to ensure valid time durations for analysis. And the outliers where filtered out based on the confidence interval.

code: 
Q1 = nypd_data['Time_Difference_Minutes'].quantile(0.25)
Q3 = nypd_data['Time_Difference_Minutes'].quantile(0.75)

# Calculate the interquartile range (IQR)
IQR = Q3 - Q1

# Define the lower and upper bounds to identify outliers
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Filter the DataFrame to remove outliers
nypd_data_no_outliers = nypd_data[(nypd_data['Time_Difference_Minutes'] >= lower_bound) & (nypd_data['Time_Difference_Minutes'] <= upper_bound)]

The columns 'CAD_EVNT_ID', 'GEO_CD_X', and 'GEO_CD_Y' were dropped from the 'merged_data' DataFrame as they were deemed unnecessary for the analysis.

The 'BORO_NM' column in the 'merged_data' DataFrame was encoded using LabelEncoder, which converts categorical labels into numerical representations. The mapping of original values to encoded values in the 'BORO_NM' column was printed to understand how the encoding was performed.

from sklearn.preprocessing import LabelEncoder
# Initialize LabelEncoder
label_encoder = LabelEncoder()

# Fit and transform the 'BORO_NM' column
merged_data['BORO_NM_encoded'] = label_encoder.fit_transform(merged_data['BORO_NM'])

# Print the mapping of original values to encoded values
print("Mapping of original values to encoded values:")
for original, encoded in zip(label_encoder.classes_, label_encoder.transform(label_encoder.classes_)):
    print(f"{original}: {encoded}")

## Modeling

The MAE of 1.35 minutes indicates that, on average, the model's predictions differ from the actual values by about 1.35 minutes.
This initial modeling provides a baseline performance metric that can be used to assess the model's improvement in future iterations.

## Problems & Challenges

We are yet to find the baseline for our modelling technique and how to go about it. We are going to try different techniques to fnd the best solution and predict the response time of the units.

## Next steps

Procceed with the modelling - 04/06/2024 - 04/13/2024
Test the model - 04/14/2024 - 04/21/2024

