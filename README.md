# pandas-challenge
Pandas homework. 
# setup, set up the pandas lib and also numpy

import pandas as pd
import numpy as np

# pd means pandas like import the pandas
# np means num py like import the numpy. numpy is a library for scientific computing
# a numpy array is a grid of all values all of the same tpe . the number of dimensions is the rank
# numpy provides a large set of numeric datatypes that you can use to contruct arrays 

# load file

file_to_load = "Resources/purchase_data.csv"

#read the file to download data

purchase_data = pd.read_csv(file_to_load)

# TOTAL NUM OF PLAYERS

total_players = len(purchase_data["SN"].value_counts())
# total players is the length of the amount of screen names in purchase data

player_count = pd.DataFrame({"Total Players":[total_players]})
player_count

# essentially put the amount of players in a variable and then display it as a data frame which is from the pandas libary

# NUM OF UNIQUE ITEMS, AVG PRICE, PURCHASE COUNT, REVENUE 

num_unique_items = len((purchase_data:["Item ID"]).unique())

# so the number of unique items is gonna be in the purchase data obvi, under the column item id and then it has to be unique so add the unique one which i believe comes from the pandas
# len is the number of items in an object so like the number of characters in the string of items cuase its unique

average_price = purchase_data:["Price"]).mean()

# essentially go into the purch data and find price then take the mean of it which is a

number_of_purchases = purchase_data:["Purchase ID"]).count()
total_revenue = purchase_data:["Price"]).sum()

# Make it a data frame

summary_df = pd.DataFrame({"Number of Unique Items":[number_of_unique_items], "Avg Price":[average_price],"Number of Purchases":[number_of_purchases],"Total Revenue":[total_revenue]})

# format with currency style

summary_df.style.format({'Average Price':"${:,.2f}",
                         'Total Revenue': '${:,.2f}'})
                        
# GENDER DEMOGRAPHICS
# group female, male, other
gender_stats = purchase_data.groupby("Gender")

# count the screen names by gender in the gender stats object and only the unique ones 

total_count_gender = gender_stats.nunique()["SN"]

# find the percentage of players, so divide the values above by the total count of players

percentage_of_players = total_count_gender / total_players * 100

# make df of this

gender_demographics = pd.DataFrame({"Percentage of Players": percentage_of_players, "Total Count": total_count_gender})

# format data frame to not have index name in the corner (not sure why we do this tbh but its ugly without it

gender_demographics.index.name = None

# format values sorted by total count 

gender_demographics.sort_values(["Total Count"], ascending = False).style.format({Percentage of Players":"{:.2f}"})

# Purchase Analysis

# Count the total number of purchases by gender 
# essentially counting the purchases by gender

purchase_count = gender_stats["Purchase ID"].count()

# average purchases by gender 

avg_purchase_price = gender_stats["Price"].mean()

# average purchase total by gender

avg_purchase_price = gender_stats["Price"].sum()

# average purchase total by gender divided by purchases of unique players

average_purchase_per_person = avg_purchase_total/total_count_gender

# data frame 

gender_demographics = pd.DataFrame({"Purchase Count": purchase_count, 
                                    "Average Purchase Price": avg_purchase_price,
                                    "Average Purchase Value":avg_purchase_total,
                                    "Avg Purchase Total per Person": avg_purchase_per_person})
                                    
# format

gender_demographics.index.name = "Gender"

# add currency

gender_demographics.style.format({"Average Purchase Value":"${:,.2f}",
                                  "Average Purchase Price":"${:,.2f}",
                                  "Avg Purchase Total per Person":"${:,.2f}"})
                                  
# AGE DEMOGRAPHICS
# Making the bins
# Seperate the different bins using commas
age_bins = [0, 9.90, 14.90, 19.90, 24.90, 29.90, 34.90, 39.90, 99999]

# Name the bins

group_names = ["<10", "10-14","15-19","20-24","25-29", "30-34", "35-39", "40+"]

# Segment and sort age values into bins established above 
# Use cut when you need to segment and sort data values into bins. This function is also useful for going from a continuous variable to a categorical variable. For example, cut could convert ages to groups of age ranges. Supports binning into an equal number of bins, or a pre-specified array of bins.
# So essentially what is happening is we are saying take all of this data and make a variable by age group using bins of ages. The cut function allows the age column to be seperated in bins with the labels established in the group_names object

purchase_data["Age Group"] = pd.cut(purchase_data["Age"], age_bins, labels = group_names)purchase_data

# Create new data frame with age group 

age_grouped = purchase_data.groupby("Age Group")

# Count total players by age category

total_count_age = age_grouped["SN"].nunique()

# Create data frame with obtained values

age_demographics = pd.DataFrame({"Percentage of Players": percentage_by_age, "Total Count": total_count_age})

# Format the data frame with no index name in the corner

age_demographics.index.name = None

# Format percentage with two decimal places 

age_demographics.style.format({"Percentage of Players":"{:,.2f}"})

# PURCHASE ANALYSIS
