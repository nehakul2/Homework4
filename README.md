

```python
import pandas as pd
import os
import numpy as np
```


```python
#data = pd.read_json('purchase_data.json')
file_name = os.path.join("purchase_data.json")
print(file_name)
json_pd = pd.read_json(file_name)
json_pd.head()

```

    purchase_data.json





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
#Player Count
#Total Number of Players
total_player_cnt = json_pd.count()
total_cnt =  (total_player_cnt[0])
print("Total number of players : " ,total_cnt)
```

    Total number of players :  780



```python
#Purchasing Analysis (Total)
#Number of Unique Items
unq_items=len(json_pd["Item Name"].value_counts())
print("Number of Unique Items : " ,unq_items)
```

    Number of Unique Items :  179



```python
#lets calculate Average Purchase Price
avg_price = json_pd["Price"].mean()
print("Average Purchase Price : " , avg_price)
```

    Average Purchase Price :  2.931192307692303



```python
#Total Number of Purchases
num_pur = json_pd["Price"].count()
print("Total Number of Purchases : " ,num_pur)
```

    Total Number of Purchases :  780



```python
#lets calculate Total Revenue
total_rev = json_pd["Price"].sum()
print("Total Revenue  :" , total_rev)
```

    Total Revenue  : 2286.33



```python
#lets get the number by gender
knt = json_pd.groupby(["Gender"]).count()
knt
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
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>136</td>
      <td>136</td>
      <td>136</td>
      <td>136</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>633</td>
      <td>633</td>
      <td>633</td>
      <td>633</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#gender demographics
#Percentage and Count of Male Players

knt= json_pd.groupby('Gender').count()
#(knt)

per_male = knt.iloc[1,0]/total_cnt *100

print("Percentage and Count of Male Players" , per_male ,"," ,knt.iloc[1,0])
```

    Percentage and Count of Male Players 81.1538461538 , 633



```python
#Percentage and Count of Female Players
#knt= json_pd.groupby('Gender').count()
#print(knt)
per_female = knt.iloc[0,0]/total_cnt *100

print("Percentage and Count of Female Players" , per_female ,"," ,knt.iloc[0,0])
```

    Percentage and Count of Female Players 17.4358974359 , 136



```python
#Percentage and Count of Other / Non-Disclosed
per_other = knt.iloc[2,0]/total_cnt *100

print("Percentage and Count of Other / Non-Disclosed" , per_other ,"," ,knt.iloc[2,0])
```

    Percentage and Count of Other / Non-Disclosed 1.41025641026 , 11



```python
#Purchasing Analysis (Gender)
#The below each broken by gender
#Purchase Count
grouped_purchase_val = json_pd.groupby(["Gender"]).count()["Price"]
print ("Purchase Count by Gender : " ,grouped_purchase_val)

```

    Purchase Count by Gender :  Gender
    Female                   136
    Male                     633
    Other / Non-Disclosed     11
    Name: Price, dtype: int64



```python
#Average Purchase Price
avg_price = json_pd.groupby(["Gender"]).mean()["Price"]
print("Average Price by Gender : " ,avg_price)
```

    Average Price by Gender :  Gender
    Female                   2.815515
    Male                     2.950521
    Other / Non-Disclosed    3.249091
    Name: Price, dtype: float64



```python
#Total Purchase Value

tot_pur_price =json_pd.groupby(["Gender"]).sum()["Price"]
print("Total Purchase Value by Gender : " , tot_pur_price)
```

    Total Purchase Value by Gender :  Gender
    Female                    382.91
    Male                     1867.68
    Other / Non-Disclosed      35.74
    Name: Price, dtype: float64



```python
#Normalized Totals (normalizing for the # of people in each gender group)
```


```python
#lets start with Purchasing Analysis (Total)
gnd_knt = json_pd["Gender"].value_counts()
gnd_knt.head()

grouped = json_pd.groupby('Gender')
print (grouped['Price'].agg(np.sum))


grouped = json_pd.groupby('Gender')
print (grouped['Price'].agg([np.sum, np.mean]))
```

    Gender
    Female                    382.91
    Male                     1867.68
    Other / Non-Disclosed      35.74
    Name: Price, dtype: float64
                               sum      mean
    Gender                                  
    Female                  382.91  2.815515
    Male                   1867.68  2.950521
    Other / Non-Disclosed    35.74  3.249091



```python
#Age Demographics
#The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
#Purchase Count
age_bins = [0, 9, 14, 19, 24, 29, 34, 39, 100]
age_labels = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+" ]

pd.cut(json_pd["Age"], age_bins, labels=age_labels)
```




    0      35-39
    1      20-24
    2      30-34
    3      20-24
    4      20-24
    5      20-24
    6      20-24
    7      25-29
    8      25-29
    9      30-34
    10     20-24
    11     20-24
    12     30-34
    13     20-24
    14       40+
    15     20-24
    16     20-24
    17     20-24
    18     25-29
    19     30-34
    20     20-24
    21     15-19
    22     10-14
    23     15-19
    24     10-14
    25     20-24
    26     25-29
    27     30-34
    28     15-19
    29     15-19
           ...  
    750    20-24
    751    25-29
    752    15-19
    753    20-24
    754    30-34
    755    20-24
    756    20-24
    757    35-39
    758    20-24
    759    15-19
    760    25-29
    761    25-29
    762    35-39
    763    25-29
    764    25-29
    765    15-19
    766    20-24
    767    20-24
    768    20-24
    769    20-24
    770    20-24
    771    20-24
    772    15-19
    773    20-24
    774    20-24
    775    20-24
    776    10-14
    777    20-24
    778    20-24
    779    20-24
    Name: Age, Length: 780, dtype: category
    Categories (8, object): [<10 < 10-14 < 15-19 < 20-24 < 25-29 < 30-34 < 35-39 < 40+]




```python
#Purchase Count
#Average Purchase Price
#Total Purchase Value
#Normalized Totals (normalizing for the # of people in each age group

json_pd["Age_Category"] = pd.cut(json_pd["Age"], age_bins, labels=age_labels)
json_pd.head()

# #tried this to fix the sequence
#age_grouped= json_pd.groupby("Age_Category")
#age_grouped.head()
#total_purchase_val = age_grouped["Price" ].sum() 

total_purchase_val = json_pd.groupby("Age_Category").sum()["Price"]
# Create a DataFrame using the Series
df = pd.DataFrame({"Total Purchase Value": total_purchase_val})
# Sort the DataFrame by descending
df.sort_values("Total Purchase Value")
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
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Age_Category</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>40+</th>
      <td>53.75</td>
    </tr>
    <tr>
      <th>&lt;10</th>
      <td>83.46</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>96.95</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>119.40</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>197.25</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>370.33</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>978.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# This gives us the count of all the bins in categorized
#Average Purchase Price
purchase_count = age_grouped["Gender"].value_counts() # saving in variables
p1 = purchase_count.loc['<10'].sum()
p2 = purchase_count.loc['10-14'].sum()
p3 = purchase_count.loc['15-19'].sum()
p4 = purchase_count.loc['20-24'].sum()
p5 = purchase_count.loc['25-29'].sum()
p6 = purchase_count.loc['30-34'].sum()
p7 = purchase_count.loc['35-39'].sum()
p8 = purchase_count.loc['40+'].sum()

```


```python
# Normalized Totals for Age demographics
# Total Purchase Value/# of people each group
normalized1 = total_purchase_val.iloc[0]/p1
normalized2 = total_purchase_val.iloc[1]/p2
normalized3 = total_purchase_val.iloc[2]/p3
normalized4 = total_purchase_val.iloc[3]/p4
normalized5 = total_purchase_val.iloc[4]/p5
normalized6 = total_purchase_val.iloc[5]/p6
normalized7 = total_purchase_val.iloc[6]/p7
normalized8 = total_purchase_val.iloc[7]/p8
 
```


```python
# Average purchase price (Total Purchase value/purchase count) 
avg_purchase1 = total_purchase_val.iloc[0]/purchase_count.iloc[0]
avg_purchase2 = total_purchase_val.iloc[1]/purchase_count.iloc[1]
avg_purchase3 = total_purchase_val.iloc[2]/purchase_count.iloc[2]
avg_purchase4 = total_purchase_val.iloc[3]/purchase_count.iloc[3]
avg_purchase5 = total_purchase_val.iloc[4]/purchase_count.iloc[4]
avg_purchase6 = total_purchase_val.iloc[5]/purchase_count.iloc[5]
avg_purchase7 = total_purchase_val.iloc[6]/purchase_count.iloc[6]
avg_purchase8 = total_purchase_val.iloc[7]/purchase_count.iloc[7]
```


```python
# Creating a new dataframe for Purchasing Analysis (Age)
purchasing_analysis_Age_dic = {"Age": ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"],
                                  "Average Purchase Price": [avg_purchase1,
                                                             avg_purchase2,
                                                             avg_purchase3,
                                                             avg_purchase4,
                                                             avg_purchase5,
                                                             avg_purchase6,
                                                             avg_purchase7,
                                                             avg_purchase8],
                                  "Total Purchase Value": [total_purchase_val.iloc[0],
                                                           total_purchase_val.iloc[1],
                                                           total_purchase_val.iloc[2],
                                                           total_purchase_val.iloc[3],
                                                           total_purchase_val.iloc[4],
                                                           total_purchase_val.iloc[5],
                                                           total_purchase_val.iloc[6],
                                                           total_purchase_val.iloc[7]],
                                  "Normalized Totals": [normalized1,
                                                        normalized2,
                                                        normalized3,
                                                        normalized4,
                                                        normalized5,
                                                        normalized6,
                                                        normalized7,
                                                        normalized8],
                                  "Purchase Count": [purchase_count.iloc[0],
                                                     purchase_count.iloc[1],
                                                     purchase_count.iloc[2],
                                                     purchase_count.iloc[3],
                                                     purchase_count.iloc[4],
                                                     purchase_count.iloc[5],
                                                     purchase_count.iloc[6],
                                                     purchase_count.iloc[7]],
                                    "# people each group": [p1,
                                                               p2,
                                                               p3,
                                                               p4,
                                                               p5,
                                                               p6,
                                                               p7,
                                                               p8]}

purchasing_analysis_Age_df = pd.DataFrame(purchasing_analysis_Age_dic) # Set the row index to be "Age"

purchasing_analysis_Age_df

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
      <th># people each group</th>
      <th>Age</th>
      <th>Average Purchase Price</th>
      <th>Normalized Totals</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>&lt;10</td>
      <td>16.692000</td>
      <td>16.692000</td>
      <td>5</td>
      <td>83.46</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>10-14</td>
      <td>96.950000</td>
      <td>32.316667</td>
      <td>1</td>
      <td>96.95</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11</td>
      <td>15-19</td>
      <td>386.420000</td>
      <td>35.129091</td>
      <td>1</td>
      <td>386.42</td>
    </tr>
    <tr>
      <th>3</th>
      <td>36</td>
      <td>20-24</td>
      <td>978.770000</td>
      <td>27.188056</td>
      <td>1</td>
      <td>978.77</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>25-29</td>
      <td>41.147778</td>
      <td>41.147778</td>
      <td>9</td>
      <td>370.33</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7</td>
      <td>30-34</td>
      <td>98.625000</td>
      <td>28.178571</td>
      <td>2</td>
      <td>197.25</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>35-39</td>
      <td>4.117241</td>
      <td>19.900000</td>
      <td>29</td>
      <td>119.40</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>40+</td>
      <td>7.678571</td>
      <td>53.750000</td>
      <td>7</td>
      <td>53.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Lets start working n the top 5 spenders
```


```python
#Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
#SN
#Purchase Count
#Average Purchase Price
#Total Purchase Value
#Index(['Age', 'Gender', 'Item ID', 'Item Name', 'Price', 'SN'], dtype='object')

# Series for Total Purchase Value
total_purchase_val = json_pd.groupby(["SN"]).sum()["Price"]
# Create a DataFrame using the Series
df = pd.DataFrame({"Total Purchase Value": total_purchase_val})
# Sort the DataFrame by descending
df.sort_values("Total Purchase Value", ascending=False).head()

#crearting a new df for top spenders to store all the results
spenders_df = pd.DataFrame(total_purchase_val)
spenders_df.head()

#lets rename the column for Price as Total Purchase Value
spenders_df.rename(columns={'Price': 'Total Purchase Value'}, inplace=True)
spenders_df.head()
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
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
#now lets calculate
#Purchase Count
#Average Purchase Price

# lets get the players for each category

spenders_df['Purchase Count'] = players_by_category = json_pd.groupby(["SN"])['Age'].count()
spenders_df['Average Purchase Price'] = spenders_df['Total Purchase Value'].div(spenders_df['Purchase Count'])
spenders_df
#grouped_purchase_val = json_pd.groupby(["Gender"]).count()["Price"]
#print ("Purchase Count by Gender : " ,grouped_purchase_val)

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
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
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
      <th>Adairialis76</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
      <td>3</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
      <td>3</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
      <td>1</td>
      <td>1.270000</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <td>5.06</td>
      <td>2</td>
      <td>2.530000</td>
    </tr>
    <tr>
      <th>Aelin32</th>
      <td>3.14</td>
      <td>1</td>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Aeliriam77</th>
      <td>6.72</td>
      <td>2</td>
      <td>3.360000</td>
    </tr>
    <tr>
      <th>Aeliriarin93</th>
      <td>2.04</td>
      <td>1</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Aeliru63</th>
      <td>8.98</td>
      <td>2</td>
      <td>4.490000</td>
    </tr>
    <tr>
      <th>Aellyria80</th>
      <td>4.32</td>
      <td>1</td>
      <td>4.320000</td>
    </tr>
    <tr>
      <th>Aellyrialis39</th>
      <td>3.15</td>
      <td>1</td>
      <td>3.150000</td>
    </tr>
    <tr>
      <th>Aellysup38</th>
      <td>3.61</td>
      <td>1</td>
      <td>3.610000</td>
    </tr>
    <tr>
      <th>Aelollo59</th>
      <td>1.55</td>
      <td>1</td>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Aenarap34</th>
      <td>1.65</td>
      <td>1</td>
      <td>1.650000</td>
    </tr>
    <tr>
      <th>Aenasu69</th>
      <td>3.27</td>
      <td>1</td>
      <td>3.270000</td>
    </tr>
    <tr>
      <th>Aeral43</th>
      <td>2.72</td>
      <td>1</td>
      <td>2.720000</td>
    </tr>
    <tr>
      <th>Aeral85</th>
      <td>4.25</td>
      <td>1</td>
      <td>4.250000</td>
    </tr>
    <tr>
      <th>Aeral97</th>
      <td>2.35</td>
      <td>1</td>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Aeri84</th>
      <td>6.60</td>
      <td>2</td>
      <td>3.300000</td>
    </tr>
    <tr>
      <th>Aerillorin70</th>
      <td>1.88</td>
      <td>1</td>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>10.45</td>
      <td>3</td>
      <td>3.483333</td>
    </tr>
    <tr>
      <th>Aerithnucal56</th>
      <td>3.18</td>
      <td>2</td>
      <td>1.590000</td>
    </tr>
    <tr>
      <th>Aerithnuphos61</th>
      <td>1.69</td>
      <td>1</td>
      <td>1.690000</td>
    </tr>
    <tr>
      <th>Aerithriaphos45</th>
      <td>2.38</td>
      <td>1</td>
      <td>2.380000</td>
    </tr>
    <tr>
      <th>Aesty51</th>
      <td>1.82</td>
      <td>1</td>
      <td>1.820000</td>
    </tr>
    <tr>
      <th>Aesur96</th>
      <td>4.66</td>
      <td>1</td>
      <td>4.660000</td>
    </tr>
    <tr>
      <th>Aethe80</th>
      <td>2.32</td>
      <td>1</td>
      <td>2.320000</td>
    </tr>
    <tr>
      <th>Aethedru70</th>
      <td>2.97</td>
      <td>1</td>
      <td>2.970000</td>
    </tr>
    <tr>
      <th>Aidain51</th>
      <td>6.84</td>
      <td>2</td>
      <td>3.420000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Undjaskla97</th>
      <td>4.57</td>
      <td>1</td>
      <td>4.570000</td>
    </tr>
    <tr>
      <th>Undjasksya56</th>
      <td>4.53</td>
      <td>1</td>
      <td>4.530000</td>
    </tr>
    <tr>
      <th>Undotesta33</th>
      <td>3.90</td>
      <td>1</td>
      <td>3.900000</td>
    </tr>
    <tr>
      <th>Wailin72</th>
      <td>2.04</td>
      <td>1</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Whaestysu86</th>
      <td>4.08</td>
      <td>1</td>
      <td>4.080000</td>
    </tr>
    <tr>
      <th>Yadacal26</th>
      <td>1.93</td>
      <td>1</td>
      <td>1.930000</td>
    </tr>
    <tr>
      <th>Yadaisuir65</th>
      <td>8.56</td>
      <td>2</td>
      <td>4.280000</td>
    </tr>
    <tr>
      <th>Yadanun74</th>
      <td>9.09</td>
      <td>3</td>
      <td>3.030000</td>
    </tr>
    <tr>
      <th>Yalaeria91</th>
      <td>1.88</td>
      <td>1</td>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Yaliru88</th>
      <td>3.71</td>
      <td>1</td>
      <td>3.710000</td>
    </tr>
    <tr>
      <th>Yalo71</th>
      <td>2.41</td>
      <td>1</td>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Yalostiphos68</th>
      <td>2.37</td>
      <td>1</td>
      <td>2.370000</td>
    </tr>
    <tr>
      <th>Yaralnura48</th>
      <td>4.19</td>
      <td>2</td>
      <td>2.095000</td>
    </tr>
    <tr>
      <th>Yararmol43</th>
      <td>1.55</td>
      <td>1</td>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Yarirarn35</th>
      <td>2.88</td>
      <td>1</td>
      <td>2.880000</td>
    </tr>
    <tr>
      <th>Yaristi64</th>
      <td>1.24</td>
      <td>1</td>
      <td>1.240000</td>
    </tr>
    <tr>
      <th>Yarithllodeu72</th>
      <td>2.19</td>
      <td>1</td>
      <td>2.190000</td>
    </tr>
    <tr>
      <th>Yarithphos28</th>
      <td>2.35</td>
      <td>1</td>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Yarithsurgue62</th>
      <td>4.81</td>
      <td>2</td>
      <td>2.405000</td>
    </tr>
    <tr>
      <th>Yarmol79</th>
      <td>2.91</td>
      <td>1</td>
      <td>2.910000</td>
    </tr>
    <tr>
      <th>Yarolwen77</th>
      <td>6.98</td>
      <td>2</td>
      <td>3.490000</td>
    </tr>
    <tr>
      <th>Yasriphos60</th>
      <td>10.40</td>
      <td>3</td>
      <td>3.466667</td>
    </tr>
    <tr>
      <th>Yasrisu92</th>
      <td>2.60</td>
      <td>1</td>
      <td>2.600000</td>
    </tr>
    <tr>
      <th>Yasur35</th>
      <td>2.78</td>
      <td>1</td>
      <td>2.780000</td>
    </tr>
    <tr>
      <th>Yasur85</th>
      <td>2.04</td>
      <td>1</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Yasurra52</th>
      <td>3.14</td>
      <td>1</td>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Yathecal72</th>
      <td>7.77</td>
      <td>2</td>
      <td>3.885000</td>
    </tr>
    <tr>
      <th>Yathecal82</th>
      <td>2.41</td>
      <td>1</td>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Zhisrisu83</th>
      <td>2.46</td>
      <td>2</td>
      <td>1.230000</td>
    </tr>
    <tr>
      <th>Zontibe81</th>
      <td>3.71</td>
      <td>1</td>
      <td>3.710000</td>
    </tr>
  </tbody>
</table>
<p>573 rows × 3 columns</p>
</div>




```python
#lets sort the df to list the top 5 spenders
# Sorting in the highest values of top 5 player purchases
sorted_top_spenders_df =spenders_df.sort_values("Total Purchase Value", ascending=False) 
sorted_top_spenders_df.head()
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
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
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
      <td>17.06</td>
      <td>5</td>
      <td>3.412000</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>13.56</td>
      <td>4</td>
      <td>3.390000</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>12.74</td>
      <td>4</td>
      <td>3.185000</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>12.73</td>
      <td>3</td>
      <td>4.243333</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>11.58</td>
      <td>3</td>
      <td>3.860000</td>
    </tr>
  </tbody>
</table>
</div>




```python
### Now lets start to work on the top 5 popular items purchase section
```


```python
#Identify the 5 most popular items by purchase count, then list (in a table):
#Item ID
#Item Name
#Purchase Count
#Item Price
#Total Purchase Value
# Series for Total Purchase Value
# To get the count of the players for each category

```


```python
# to get the top 5 popular items lets change  index to item name
json_new_idx_df= json_pd.set_index('Item Name')
json_new_idx_df.head()
json_new_idx_df.index
```




    Index(['Bone Crushing Silver Skewer',
           'Stormbringer, Dark Blade of Ending Misery', 'Primitive Blade',
           'Final Critic', 'Stormfury Mace', 'Sleepwalker', 'Mercenary Sabre',
           'Interrogator, Blood Blade of the Queen',
           'Ghost Reaver, Longsword of Magic',
           'Expiration, Warscythe Of Lost Worlds',
           ...
           'Persuasion', 'Hero Cane', 'Trickster', 'Bonecarvin Battle Axe',
           'Twilight's Carver', 'Deadline, Voice Of Subtlety',
           'Gladiator's Glaive', 'Heartstriker, Legacy of the Light',
           'Brutality Ivory Warmace', 'Splitter, Foe Of Subtlety'],
          dtype='object', name='Item Name', length=780)




```python
# create a Dataframe by grouping Item ID and Item Name
grp_item_name_id_df = json_pd.groupby(["Item ID", "Item Name"])

grp_item_name_id_df.sum()

most_popular_df = pd.DataFrame(grp_item_name_id_df.sum())
most_popular_df.head()

#total_purchase_count = json_pd.groupby(["SN"]).count()["Age"]
#Create a DataFrame using the Series
#df = pd.DataFrame({"Total Purchase Count": total_purchase_count})
#Sort the DataFrame by descending
#df.sort_values("Total Purchase Count", ascending=False).head()
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
      <th>Age</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <th>Splinter</th>
      <td>30</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <th>Crucifer</th>
      <td>89</td>
      <td>9.12</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Verdict</th>
      <td>15</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <th>Phantomlight</th>
      <td>15</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Bloodlord's Fetish</th>
      <td>20</td>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
# adding new column  to existing dataframe
most_popular_df['Purchase Count'] = json_pd.groupby(["Item ID", "Item Name"])["Item Name"].count()
most_popular_df.head()
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
      <th>Age</th>
      <th>Price</th>
      <th>Purchase Count</th>
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
      <th>0</th>
      <th>Splinter</th>
      <td>30</td>
      <td>1.82</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <th>Crucifer</th>
      <td>89</td>
      <td>9.12</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Verdict</th>
      <td>15</td>
      <td>3.40</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <th>Phantomlight</th>
      <td>15</td>
      <td>1.79</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Bloodlord's Fetish</th>
      <td>20</td>
      <td>2.28</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#  Rename column 'Item Price'of Price dataframe 
most_popular_df = most_popular_df.rename(columns={'Price': 'Item Price' })
most_popular_df.head()
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
      <th>Age</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
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
      <th>0</th>
      <th>Splinter</th>
      <td>30</td>
      <td>1.82</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <th>Crucifer</th>
      <td>89</td>
      <td>9.12</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Verdict</th>
      <td>15</td>
      <td>3.40</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <th>Phantomlight</th>
      <td>15</td>
      <td>1.79</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Bloodlord's Fetish</th>
      <td>20</td>
      <td>2.28</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Total Purchase Value calculations
most_popular_df['Total Purchase Value'] = most_popular_df['Purchase Count'].mul(most_popular_df['Item Price'])
most_popular_df.head()
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
      <th>Age</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <th>Splinter</th>
      <td>30</td>
      <td>1.82</td>
      <td>1</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <th>Crucifer</th>
      <td>89</td>
      <td>9.12</td>
      <td>4</td>
      <td>36.48</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Verdict</th>
      <td>15</td>
      <td>3.40</td>
      <td>1</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <th>Phantomlight</th>
      <td>15</td>
      <td>1.79</td>
      <td>1</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Bloodlord's Fetish</th>
      <td>20</td>
      <td>2.28</td>
      <td>1</td>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sorting in the highest values of top 5  purchase count

df.sort_values("Total Purchase Value")
sorted_most_popular_df = most_popular_df.sort_values("Purchase Count", ascending=False) 
sorted_most_popular_df.head()
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
      <th>Age</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>233</td>
      <td>25.85</td>
      <td>11</td>
      <td>284.35</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>243</td>
      <td>24.53</td>
      <td>11</td>
      <td>269.83</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>232</td>
      <td>18.63</td>
      <td>9</td>
      <td>167.67</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>192</td>
      <td>11.16</td>
      <td>9</td>
      <td>100.44</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>184</td>
      <td>13.41</td>
      <td>9</td>
      <td>120.69</td>
    </tr>
  </tbody>
</table>
</div>




```python
# lets start working on the Most profitable items
```


```python
#Most Profitable Items
#Identify the 5 most profitable items by total purchase value, then list (in a table):
#Item ID
#Item Name
#Purchase Count
#Item Price
#Total Purchase Value

# Sorting in the highest values of top 5 Most Profitable Items
sorted_top_purchase_df = most_popular_df.sort_values("Total Purchase Value", ascending=False) 
sorted_top_purchase_df.head()
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
      <th>Age</th>
      <th>Item Price</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>234</td>
      <td>37.26</td>
      <td>9</td>
      <td>335.34</td>
    </tr>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>233</td>
      <td>25.85</td>
      <td>11</td>
      <td>284.35</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>243</td>
      <td>24.53</td>
      <td>11</td>
      <td>269.83</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>199</td>
      <td>28.88</td>
      <td>8</td>
      <td>231.04</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>154</td>
      <td>29.75</td>
      <td>7</td>
      <td>208.25</td>
    </tr>
  </tbody>
</table>
</div>


