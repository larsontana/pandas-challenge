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
                         
                     

