

```python
# Import the Pandas library
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import os
from sklearn import preprocessing #Used for Normalized calculations
```


```python
# Create a reference for the desired JSON file
json_path = "purchase_data.json"

# Read the JSON into a Pandas DataFrame
heroes_df = pd.read_json(json_path)

# Print the first five rows of data to the screen - just to be sure we have imported the JSON correctly
heroes_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Export imported JSON File (in Pandas Dataframe) as a CSV, without the Pandas index, but with the header
heroes_df.to_csv("heroes_tushaar.csv", index=False, header=True)
# This is just so that I can use excel to 'view' the spreadsheet for additional verifications
# This is pretty cool - with just a couple of lines of code I can easily convert a JSON to a CSV
```


```python
# Check to see if there are any rows with missing data
heroes_df.count()
# This is very important method...to check the sanity of our imported table
```




    Age          780
    Gender       780
    Item ID      780
    Item Name    780
    Price        780
    SN           780
    dtype: int64




```python
# Display the data types for each column of our data frame - just to understand the data types for future calculations
heroes_df_dtype = heroes_df.dtypes
heroes_df_dtype
```




    Age            int64
    Gender        object
    Item ID        int64
    Item Name     object
    Price        float64
    SN            object
    dtype: object




```python
# Code for the Player Count Section
```


```python
# Count the number of 'unique' players in the SN column
unique_player_counts = heroes_df ["SN"].value_counts() #using the value_counts() to return all the unique values totals pf 'SN'
```


```python
# Calculating the total number of players
total_player_counts = unique_player_counts.count() # using the count() function to return total number of values
print("Total Number of Players: " + str(total_player_counts)) # simple print statement to output the results
Player_Count_Df = pd.DataFrame({"Total Players": [total_player_counts]}) # Create the dataframe for desired output format
Player_Count_Df

```

    Total Number of Players: 573





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Print the first five rows of our dataframe to the screen
heroes_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Code for the Purchase Analysis Section
```


```python
# Count the number of 'unique' items in the "Item ID" column
unique_item_ID_counts = heroes_df ["Item ID"].value_counts() # using value_counts() function will return totals of each unique value
unique_item_ID_counts # return output
total_unique_items_count = unique_item_ID_counts.count() # using count() function to return total number of items
print ("Total Number of Unique Items are: " + str(total_unique_items_count)) # print the output
```

    Total Number of Unique Items are: 183



```python
# Count the total number of purchases - these are same as 'total number of enteries' of the Price column
total_number_of_purchases = heroes_df ["Price"].count() # using count() function to return total number of items for Price column
total_number_of_purchases
print("Total Number of Purchases are: " + str(total_number_of_purchases)) #print the output
```

    Total Number of Purchases are: 780



```python
# Count the total revenue - it is the sum of all the prices in the price column
total_revenue = heroes_df ["Price"].sum() # Basic sum() function to return totals of the Price column. This will give the total revenue
print("Total revenue is: " + str(total_revenue)) #print the output
```

    Total revenue is: 2286.33



```python
# Calculate the average purchase price - this is basically the average of ALL values of the price column
average_purchase_price = round((heroes_df ["Price"].mean()),2) # simple mean() function, rounded off to 2 decimals
print("Average Purchase Price is: " + str(average_purchase_price))
```

    Average Purchase Price is: 2.93



```python
# Creating Purchase Analysis Dataframe with all the values calculated earlier - this will be used for formatting the desired output
Purchase_Analysis_Df = pd.DataFrame({"Number of Unique Items": [total_unique_items_count],
                                     "Average Price": [average_purchase_price],
                                     "Number of Purchases": [total_number_of_purchases],
                                     "Total Revenue": [total_revenue]})
```


```python
# Organizing the columns of our dataframe. This could have been done in earlier step as well by adding the columns delimmter in the dataframe definition
organized_Purchase_Analysis_Df = Purchase_Analysis_Df[["Number of Unique Items","Average Price","Number of Purchases","Total Revenue"]]

#formatting the coloumns to add $ signs
organized_Purchase_Analysis_Df["Average Price"] = organized_Purchase_Analysis_Df["Average Price"].map("${:.2f}".format)
organized_Purchase_Analysis_Df["Total Revenue"] = organized_Purchase_Analysis_Df["Total Revenue"].map("${:,}".format)

organized_Purchase_Analysis_Df #return the output of our final dataframe for the Homework specification
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>$2.93</td>
      <td>780</td>
      <td>$2,286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Code for Gender Demographics Section
```


```python
# Collect a list of all the unique values in "Gender"
heroes_df["Gender"].unique()
```




    array(['Male', 'Female', 'Other / Non-Disclosed'], dtype=object)




```python
# Now creating a new dataframe for male players
male_players_df = heroes_df.loc[heroes_df["Gender"] == "Male", :] #using Loc method to return all Males records
male_players_df.head() #display our new dataframe
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Doublechecking to make sure that our new male player dataframe is accurately showing only Males in the Gender column
male_players_df["Gender"].unique()
```




    array(['Male'], dtype=object)




```python
# Now that we have the male players dataframe, our next task is to find out the 'unique' male players
unique_male_players = male_players_df["SN"].value_counts() #As explained earlier above in the code, value_counts() returns unique values totals
total_unique_male_players = unique_male_players.count() # capturing the total value
print ("Total Number of Male Players are: " + str(total_unique_male_players)) #printing the output
```

    Total Number of Male Players are: 465



```python
# Now creating a new dataframe for female players. Exact same logic and comments as above
female_players_df = heroes_df.loc[heroes_df["Gender"] == "Female", :]
female_players_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
    </tr>
    <tr>
      <th>16</th>
      <td>22</td>
      <td>Female</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Sundista85</td>
    </tr>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
    </tr>
    <tr>
      <th>22</th>
      <td>11</td>
      <td>Female</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Deural48</td>
    </tr>
    <tr>
      <th>29</th>
      <td>16</td>
      <td>Female</td>
      <td>45</td>
      <td>Glinting Glass Edge</td>
      <td>2.46</td>
      <td>Phaedai25</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Doublechecking to make sure that our new female player dataframe is accurately showing only Females in the Gender column
female_players_df["Gender"].unique()
```




    array(['Female'], dtype=object)




```python
# Now that we have the female players dataframe, our next task is to find out the 'unique' female players
unique_female_players = female_players_df["SN"].value_counts() # capturing totals of unique values using value_counts
total_unique_female_players = unique_female_players.count() # capturing the total value
print ("Total Number of Female Players are: " + str(total_unique_female_players)) #printing the output
```

    Total Number of Female Players are: 100



```python
# Now creating a new dataframe for Other / Non-Disclosed players - same exact logic as Males and Females above
nogender_players_df = heroes_df.loc[heroes_df["Gender"] == "Other / Non-Disclosed", :]
nogender_players_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>177</th>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
    </tr>
    <tr>
      <th>209</th>
      <td>33</td>
      <td>Other / Non-Disclosed</td>
      <td>157</td>
      <td>Spada, Etcher of Hatred</td>
      <td>2.21</td>
      <td>Frichistasta59</td>
    </tr>
    <tr>
      <th>244</th>
      <td>21</td>
      <td>Other / Non-Disclosed</td>
      <td>183</td>
      <td>Dragon's Greatsword</td>
      <td>2.36</td>
      <td>Tyaerith73</td>
    </tr>
    <tr>
      <th>267</th>
      <td>33</td>
      <td>Other / Non-Disclosed</td>
      <td>65</td>
      <td>Conqueror Adamantite Mace</td>
      <td>1.96</td>
      <td>Frichistasta59</td>
    </tr>
    <tr>
      <th>276</th>
      <td>12</td>
      <td>Other / Non-Disclosed</td>
      <td>128</td>
      <td>Blazeguard, Reach of Eternity</td>
      <td>4.00</td>
      <td>Aillycal84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Doublechecking to make sure that our new non-disclosed gender player dataframe is accurately showing only Females in the Gender column
nogender_players_df["Gender"].unique()
```




    array(['Other / Non-Disclosed'], dtype=object)




```python
# Now that we have the non-disclosed players dataframe, our next task is to find out the 'unique' non-disclosed players
unique_nogender_players = nogender_players_df["SN"].value_counts()# capturing totals of unique values using value_counts
total_unique_nogender_players = unique_nogender_players.count() # capturing the total value
print ("Total Number of Other/Non-Disclosed Players are: " + str(total_unique_nogender_players))
```

    Total Number of Other/Non-Disclosed Players are: 8



```python
# Calculating the percentage males, femails and non-disclosed populations and rounding it off to 2 decimal places
Male_Player_Percentage = round (((total_unique_male_players / total_player_counts) * 100),2)
Female_Player_Percentage = round(((total_unique_female_players / total_player_counts) * 100),2)
Nogender_Player_Percentage = round(((total_unique_nogender_players/ total_player_counts) * 100),2)
print ("Percentage of Male Players is: " + str (Male_Player_Percentage))
print ("Percentage of Female Players is: " + str (Female_Player_Percentage))
print ("Percentage of Other/ Non-Disclosed Players is: " + str (Nogender_Player_Percentage))
```

    Percentage of Male Players is: 81.15
    Percentage of Female Players is: 17.45
    Percentage of Other/ Non-Disclosed Players is: 1.4



```python
#Creating Gender Demographics dataframe to return the desired output needed in the homework
Gender_Demographics_Df = pd.DataFrame ({"Gender": ["Male", "Female", "Other"],
                                        "Percentage of Players": [Male_Player_Percentage, Female_Player_Percentage, Nogender_Player_Percentage],
                                        "Total Count": [total_unique_male_players, total_unique_female_players, total_unique_nogender_players]
                                        })

#Formatting the Percentage of Players column to add the percentage sign and 2 decimal places
Gender_Demographics_Df["Percentage of Players"] = Gender_Demographics_Df["Percentage of Players"].map("{:.2f}%".format)
Gender_Demographics_Df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>81.15%</td>
      <td>465</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>17.45%</td>
      <td>100</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other</td>
      <td>1.40%</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Code for Purchase Analysis (Gender)
```


```python
# Starting the calculations for the Male Players Dataframe

# Count the total number of purchases
total_number_of_purchases_male = male_players_df ["Price"].count()
total_number_of_purchases_male
print("Total Number of Purchases by Male players are: " + str(total_number_of_purchases_male))


# Count the total revenue
total_purchase_value_male = male_players_df ["Price"].sum()
print("Total Purchase Value for Male Players is: " + str(total_purchase_value_male))

# Calculate the average purchase price
average_purchase_price_male = round((male_players_df ["Price"].mean()),2)
print("Average Purchase Price for Male Players is: " + str(average_purchase_price_male))
```

    Total Number of Purchases by Male players are: 633
    Total Purchase Value for Male Players is: 1867.68
    Average Purchase Price for Male Players is: 2.95



```python
# Starting the calculations for the Female Players Dataframe

# Count the total number of purchases
total_number_of_purchases_female = female_players_df ["Price"].count()
total_number_of_purchases_female
print("Total Number of Purchases by Female players are: " + str(total_number_of_purchases_female))


# Count the total revenue
total_purchase_value_female = round((female_players_df ["Price"].sum()),2)
print("Total Purchase Value for Female Players is: " + str(total_purchase_value_female))

# Calculate the average purchase price
average_purchase_price_female = round((female_players_df ["Price"].mean()),2)
print("Average Purchase Price for Female Players is: " + str(average_purchase_price_female))
```

    Total Number of Purchases by Female players are: 136
    Total Purchase Value for Female Players is: 382.91
    Average Purchase Price for Female Players is: 2.82



```python
# Starting the calculations for the Other/Non-Disclosed Players Dataframe

# Count the total number of purchases
total_number_of_purchases_nogender = nogender_players_df ["Price"].count()
total_number_of_purchases_nogender
print("Total Number of Purchases by Other/Non-Disclosed players are: " + str(total_number_of_purchases_nogender))


# Count the total revenue
total_purchase_value_nogender = round((nogender_players_df ["Price"].sum()),2)
print("Total Purchase Value for Other/Non-Disclosed Players is: " + str(total_purchase_value_nogender))

# Calculate the average purchase price
average_purchase_price_nogender = round((nogender_players_df ["Price"].mean()),2)
print("Average Purchase Price for Other/Non-Disclosed Players is: " + str(average_purchase_price_nogender))
```

    Total Number of Purchases by Other/Non-Disclosed players are: 11
    Total Purchase Value for Other/Non-Disclosed Players is: 35.74
    Average Purchase Price for Other/Non-Disclosed Players is: 3.25



```python
# Create Normalized Values - this will be done after we create a dataframe for the above information

Purchase_Analysis_Gender_Df = pd.DataFrame({"Gender": ["Female", "Male", "Other/Non-Disclosed"],
                                            "Purchase Count": [total_number_of_purchases_female, total_number_of_purchases_male, total_number_of_purchases_nogender],
                                            "Average Purchase Price": [average_purchase_price_female, average_purchase_price_male, average_purchase_price_nogender],
                                            "Total Purchase Value": [total_purchase_value_female, total_purchase_value_male, total_purchase_value_nogender],
                                            })

# Creating Normalized Values for the Total Purchases Column

# Create x, where x the 'Total Purchase Value' column's values as floats
x = Purchase_Analysis_Gender_Df[["Total Purchase Value"]].values.astype(float)
# Create a minimum and maximum processor object
min_max_scaler = preprocessing.MinMaxScaler()
# Create an object to transform the data to fit minmax processor
x_scaled = min_max_scaler.fit_transform(x)
# print(x_scaled)


# Now adding Normalized Totals and creating a brand new Dataframe
# We can also add Normalized Totals as a 'new column' in the existing Purchase_Analysis_Gender_Df Dataframe as well

Purchase_Analysis_Gender_Df = pd.DataFrame({"Gender": ["Female", "Male", "Other/Non-Disclosed"],
                                            "Purchase Count": [total_number_of_purchases_female, total_number_of_purchases_male, total_number_of_purchases_nogender],
                                            "Average Purchase Price": [average_purchase_price_female, average_purchase_price_male, average_purchase_price_nogender],
                                            "Total Purchase Value": [total_purchase_value_female, total_purchase_value_male, total_purchase_value_nogender],
                                            "Normalized Totals": [x_scaled[0], x_scaled[1], x_scaled[2] ]
                                            })


# Formatting the dataframe columns to add $ signs
Purchase_Analysis_Gender_Df["Average Purchase Price"] = Purchase_Analysis_Gender_Df["Average Purchase Price"].map("${:.2f}".format)
Purchase_Analysis_Gender_Df["Total Purchase Value"] = Purchase_Analysis_Gender_Df["Total Purchase Value"].map("${:.2f}".format)

```


```python
#Organizing the dataframe to re-order the coloumns in the desired format
organized_Purchase_Analysis_Gender_Df = Purchase_Analysis_Gender_Df[["Gender", "Purchase Count", "Average Purchase Price", "Total Purchase Value", "Normalized Totals"]]
organized_Purchase_Analysis_Gender_Df #This produces the output as specified in the Homework
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>136</td>
      <td>$2.82</td>
      <td>$382.91</td>
      <td>[0.18950948175158572]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>633</td>
      <td>$2.95</td>
      <td>$1867.68</td>
      <td>[1.0]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other/Non-Disclosed</td>
      <td>11</td>
      <td>$3.25</td>
      <td>$35.74</td>
      <td>[0.0]</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Code for Age Demographics
```


```python
heroes_df.head(10) #return top 10 records of our original imported Dataframe from the JSON file
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20</td>
      <td>Male</td>
      <td>10</td>
      <td>Sleepwalker</td>
      <td>1.73</td>
      <td>Tanimnya91</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20</td>
      <td>Male</td>
      <td>153</td>
      <td>Mercenary Sabre</td>
      <td>4.57</td>
      <td>Undjaskla97</td>
    </tr>
    <tr>
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>Male</td>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>2.77</td>
      <td>Sondenasta63</td>
    </tr>
    <tr>
      <th>9</th>
      <td>31</td>
      <td>Male</td>
      <td>99</td>
      <td>Expiration, Warscythe Of Lost Worlds</td>
      <td>4.53</td>
      <td>Hilaerin92</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create the logic for Binning
max_age = heroes_df["Age"].max() # Calculating the minimum age of our players in our JSON file
min_age = heroes_df["Age"].min() # Calculating the maximum age of our players in our JSON file

# Create the bins in which Data will be held
# Bins are 0 to 9, 10 to 14, 15 to 19, 20+
bins = [0, 9, 14, 19, max_age]

# Create the names for the four bins
group_names = ['<10', '10-14', '15-19', '20+']

# Using the Bin function to split our data by "Age Demogrpahics" 4 bins as defined earlier
heroes_df["Age Demographics"] = pd.cut(heroes_df["Age"], bins, labels=group_names)
heroes_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Demographics</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20+</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Defining new dataframes by each of the 4 Age Demographics partitions

heroes_10_demographics_df = heroes_df.loc[heroes_df["Age Demographics"] == "<10", :] # Data Frame for less than 10 years age group
heroes_14_demographics_df = heroes_df.loc[heroes_df["Age Demographics"] == "10-14", :] # Data Frame for 10-14 years age group
heroes_19_demographics_df = heroes_df.loc[heroes_df["Age Demographics"] == "15-19", :] # Data Frame for 15-19 years age group
heroes_20_demographics_df = heroes_df.loc[heroes_df["Age Demographics"] == "20+", :] # Data Frame for greater than 20 years age group

# Getting total unique player counts for each player falling in our above age demographics
Player_count_10 = len(heroes_10_demographics_df["SN"].unique()) # Player count for less than 10 years demographics
Player_count_14 = len(heroes_14_demographics_df["SN"].unique()) # Player count for l0-14 years demographics
Player_count_19 = len(heroes_19_demographics_df["SN"].unique()) # Player count for 15-19 years demographics
Player_count_20 = len(heroes_20_demographics_df["SN"].unique()) # Player count for greater than 20 years demographics

# Calculating the percentage of each player in each age demographics, rounded off to 2 decimal places
Player_10_Percentage = round (((Player_count_10 / total_player_counts) * 100),2)
Player_14_Percentage = round (((Player_count_14 / total_player_counts) * 100),2)
Player_19_Percentage = round (((Player_count_19 / total_player_counts) * 100),2)
Player_20_Percentage = round (((Player_count_20 / total_player_counts) * 100),2)


# Creating our DataFrame to produce output as desired in the Homework
Age_Demographics_Counts_Df = pd.DataFrame({"Age Demographics": ["<10", "10-14", "15-19", "20+"],
                                            "Percentage of Players": [Player_10_Percentage,Player_14_Percentage,Player_19_Percentage,Player_20_Percentage],
                                            "Total Count": [Player_count_10, Player_count_14, Player_count_19, Player_count_20]
                                          })

# Formatting the Percentage of Players column to return % sign and 2 decimal places
Age_Demographics_Counts_Df["Percentage of Players"] = Age_Demographics_Counts_Df["Percentage of Players"].map("{:.2f}%".format)

Age_Demographics_Counts_Df # Display the desired output as specified in the homework
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Demographics</th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>3.32%</td>
      <td>19</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>4.01%</td>
      <td>23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>17.45%</td>
      <td>100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20+</td>
      <td>75.22%</td>
      <td>431</td>
    </tr>
  </tbody>
</table>
</div>




```python

# Count the total number of purchases for each age demogrpahics
total_number_of_purchases_10 = heroes_10_demographics_df ["Price"].count()
total_number_of_purchases_14 = heroes_14_demographics_df ["Price"].count()
total_number_of_purchases_19 = heroes_19_demographics_df ["Price"].count()
total_number_of_purchases_20 = heroes_20_demographics_df ["Price"].count()

# Count the total revenue for each age demogrpahics
total_purchase_value_10 = round((heroes_10_demographics_df["Price"].sum()),2)
total_purchase_value_14 = round((heroes_14_demographics_df["Price"].sum()),2)
total_purchase_value_19 = round((heroes_19_demographics_df["Price"].sum()),2)
total_purchase_value_20 = round((heroes_20_demographics_df["Price"].sum()),2)


# Calculate the average purchase price for each age demographics
average_purchase_price_10 = round((heroes_10_demographics_df ["Price"].mean()),2)
average_purchase_price_14 = round((heroes_14_demographics_df ["Price"].mean()),2)
average_purchase_price_19 = round((heroes_19_demographics_df ["Price"].mean()),2)
average_purchase_price_20 = round((heroes_20_demographics_df ["Price"].mean()),2)

```


```python
# Create Normalized Values - this will be done after we create a dataframe for the above information

Age_Demographics_Df = pd.DataFrame({"Age Demographics": ["<10", "10-14", "15-19", "20+"],
                                    "Purchase Count": [total_number_of_purchases_10, total_number_of_purchases_14, total_number_of_purchases_19,total_number_of_purchases_20],
                                    "Average Purchase Price": [average_purchase_price_10, average_purchase_price_14, average_purchase_price_19, average_purchase_price_20],
                                    "Total Purchase Value": [total_purchase_value_10,total_purchase_value_14,total_purchase_value_19,total_purchase_value_20]
                                                                    
                                   })


# Creating Normalized Values for the Total Purchases Column

# Create x, where x the 'Total Purchase Value' column's values as floats
x = Age_Demographics_Df[["Total Purchase Value"]].values.astype(float)
# Create a minimum and maximum processor object
min_max_scaler = preprocessing.MinMaxScaler()
# Create an object to transform the data to fit minmax processor
x_scaled = min_max_scaler.fit_transform(x)
# print(x_scaled)


# Create our Dataframe for the output, this dataframe includes the normalized values column as well
Age_Demographics_Df = pd.DataFrame({"Age Demographics": ["<10", "10-14", "15-19", "20+"],
                                    "Purchase Count": [total_number_of_purchases_10, total_number_of_purchases_14, total_number_of_purchases_19,total_number_of_purchases_20],
                                    "Average Purchase Price": [average_purchase_price_10, average_purchase_price_14, average_purchase_price_19, average_purchase_price_20],
                                    "Total Purchase Value": [total_purchase_value_10,total_purchase_value_14,total_purchase_value_19,total_purchase_value_20],
                                    "Normalized Totals": [x_scaled[0], x_scaled[1], x_scaled[2], x_scaled[3]]                              
                                   })

Organized_Age_Demographics_Df = Age_Demographics_Df[["Age Demographics", "Purchase Count", "Average Purchase Price", "Total Purchase Value", "Normalized Totals"]]

# Format the columns to get $ signs and 2 decimal places
Organized_Age_Demographics_Df["Average Purchase Price"] = Organized_Age_Demographics_Df["Average Purchase Price"].map("${:.2f}".format)
Organized_Age_Demographics_Df["Total Purchase Value"] =  Organized_Age_Demographics_Df["Total Purchase Value"].map("${:.2f}".format)


# Display the final output dataframe as specified in the homework
Organized_Age_Demographics_Df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Demographics</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>28</td>
      <td>$2.98</td>
      <td>$83.46</td>
      <td>[0.0]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>35</td>
      <td>$2.77</td>
      <td>$96.95</td>
      <td>[0.008245519669445735]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>133</td>
      <td>$2.91</td>
      <td>$386.42</td>
      <td>[0.1851788464829711]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20+</td>
      <td>584</td>
      <td>$2.94</td>
      <td>$1719.50</td>
      <td>[1.0000000000000002]</td>
    </tr>
  </tbody>
</table>
</div>




```python
heroes_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Demographics</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20+</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Code Logic for Top 5 Spenders
# Over here - we will use the group by function. This is much simpler and cleaner way to process the next set of calculations
# We could have easily used 'groupby' function for earlier calculations for Age Demographics as well - but I wanted to try out different methods for practice

SN_grouped_heroes_df = heroes_df.groupby('SN') # Group our dataframe by 'SN' column
# Perform the Price calculations of Count, Mean and Sum on the newly grouped dataframe
Spenders_Price_Count_df = SN_grouped_heroes_df["Price"].count()
Spenders_Price_Average_df = SN_grouped_heroes_df["Price"].mean()
Spenders_Price_Total_df = SN_grouped_heroes_df["Price"].sum()

#Create a new dataframe view for producing our output
Spenders_df = pd.DataFrame({"Purchase Count":Spenders_Price_Count_df,
                                "Average Purchase Price": Spenders_Price_Average_df,
                               "Total Purchase Value": Spenders_Price_Total_df},
                               columns =["Purchase Count","Average Purchase Price","Total Purchase Value"])

# Sort the dataframe with highest values for "Total Purchase Value" -> this will return us top spenders
Top_Spenders_df = Spenders_df.sort_values("Total Purchase Value", ascending = False)

# Format the coloumns to add $ sign and 2 decimal places
Top_Spenders_df["Average Purchase Price"] = Top_Spenders_df["Average Purchase Price"].map("${:.2f}".format)
Top_Spenders_df["Total Purchase Value"] = Top_Spenders_df["Total Purchase Value"].map("${:.2f}".format)

# Return the top 5 records - which is same as top 5 spenders in our newly sorted dataframe
Top_Spenders_df.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>3</td>
      <td>$4.24</td>
      <td>$12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>3</td>
      <td>$3.86</td>
      <td>$11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
heroes_df.head() # Returning our orignal dataframe - just for reference
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Demographics</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20+</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20+</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Code Logic for top 5 most popular items

# Over here - we will again use the group by function. This time we will group by 2 columns -> Item ID and Item Name
Items_grouped_heroes_df = heroes_df.groupby(["Item ID","Item Name"])

# Perform the Price calculations of Count, Mean and Sum on the newly grouped dataframe
Items_Purchase_Count_df = Items_grouped_heroes_df["Price"].count()
Items_Purchase_Value_df = Items_grouped_heroes_df["Price"].sum()
Items_Purchase_Price_df = Items_grouped_heroes_df["Price"].unique()


# Perform the Price calculations of Count, Mean and Sum on the newly grouped dataframe
Items_df = pd.DataFrame({"Purchase Count": Items_Purchase_Count_df,
                         "Item Price": Items_Purchase_Price_df,
                         "Total Purchase Value": Items_Purchase_Value_df},
                        columns =["Purchase Count","Item Price","Total Purchase Value"])

# Sort the dataframe with highest values for "Purchase Count"-> this will return us top popular items
Top_Items_df = Items_df.sort_values("Purchase Count", ascending = False)
# format the coloumn for $ sign and 2 decimal values
Top_Items_df["Total Purchase Value"] = Top_Items_df["Total Purchase Value"].map("${:.2f}".format)
Top_Items_df.head()


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>[2.35]</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>[2.23]</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>[2.07]</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>9</td>
      <td>[1.24]</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>[1.49]</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Now, you will see that in the above dataframe the "Item Price" is not in a good format. The below code will fix it
Top_Items_Price = Top_Items_df["Item Price"].values.astype(float) # Create new column with Float values for item price
Top_Items_df["New Item Price"] = Top_Items_Price # Add that column to our dataframe as New Item Price

#Code to fix the Item Price
New_Top_Items_df = Top_Items_df[["Purchase Count", "New Item Price", "Total Purchase Value"]]
renamed_Top_Items_df = New_Top_Items_df.rename(columns={"New Item Price":"Item Price"})
renamed_Top_Items_df["Item Price"] = renamed_Top_Items_df["Item Price"].map("${:.2f}".format)
renamed_Top_Items_df.head() # and Viola! We have item price fixed :)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>$2.23</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>$2.07</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>9</td>
      <td>$1.24</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Code Logic for Most Profitable Items

# Sort the original Dataframe by Purchase Value
Most_profitable_items_df = Items_df.sort_values("Total Purchase Value", ascending = False)

# Now, you will see that in the above dataframe the "Item Price" is not in a good format. The below code will fix it
Profitable_Items_Price = Most_profitable_items_df["Item Price"].values.astype(float) # Create new column with Float values for item price
Most_profitable_items_df["New Item Price"] = Profitable_Items_Price # Add that column to our dataframe as New Item Price

#Code to fix the Item Price - same exact logic and next steps as explaiend above in the earlier section
New_Most_profitable_items_df = Most_profitable_items_df[["Purchase Count", "New Item Price", "Total Purchase Value"]]
renamed_Most_profitable_items_df = New_Most_profitable_items_df.rename(columns={"New Item Price":"Item Price"})
renamed_Most_profitable_items_df["Item Price"] = renamed_Most_profitable_items_df["Item Price"].map("${:.2f}".format)
renamed_Most_profitable_items_df["Total Purchase Value"] = renamed_Most_profitable_items_df["Total Purchase Value"].map("${:.2f}".format)

renamed_Most_profitable_items_df.head() # and Viola! We have item price fixed :)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>7</td>
      <td>$4.25</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>6</td>
      <td>$4.95</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>6</td>
      <td>$4.87</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>8</td>
      <td>$3.61</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>


