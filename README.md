# Task3-Exploratory-Data-Analysis---Retails
In [2]:
import pandas as pd 
import numpy as np 
import matplotlib.pyplot as plt
import sklearn
import seaborn as sns
In [3]:
store_df=pd.read_csv("SampleSuperstore.csv")
store_df.head()
Out[3]:
Ship Mode	Segment	Country	City	State	Postal Code	Region	Category	Sub-Category	Sales	Quantity	Discount	Profit
0	Second Class	Consumer	United States	Henderson	Kentucky	42420	South	Furniture	Bookcases	261.9600	2	0.00	41.9136
1	Second Class	Consumer	United States	Henderson	Kentucky	42420	South	Furniture	Chairs	731.9400	3	0.00	219.5820
2	Second Class	Corporate	United States	Los Angeles	California	90036	West	Office Supplies	Labels	14.6200	2	0.00	6.8714
3	Standard Class	Consumer	United States	Fort Lauderdale	Florida	33311	South	Furniture	Tables	957.5775	5	0.45	-383.0310
4	Standard Class	Consumer	United States	Fort Lauderdale	Florida	33311	South	Office Supplies	Storage	22.3680	2	0.20	2.5164
In [4]:
store_df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 9994 entries, 0 to 9993
Data columns (total 13 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   Ship Mode     9994 non-null   object 
 1   Segment       9994 non-null   object 
 2   Country       9994 non-null   object 
 3   City          9994 non-null   object 
 4   State         9994 non-null   object 
 5   Postal Code   9994 non-null   int64  
 6   Region        9994 non-null   object 
 7   Category      9994 non-null   object 
 8   Sub-Category  9994 non-null   object 
 9   Sales         9994 non-null   float64
 10  Quantity      9994 non-null   int64  
 11  Discount      9994 non-null   float64
 12  Profit        9994 non-null   float64
dtypes: float64(3), int64(2), object(8)
memory usage: 1015.1+ KB
In [7]:
st = pd.value_counts(store_df['State'])
st1 = pd.Series({'numunique': len(st), 'unique values': st.index.tolist()})
st.append(st1)
Out[7]:
California                                                           2001
New York                                                             1128
Texas                                                                 985
Pennsylvania                                                          587
Washington                                                            506
Illinois                                                              492
Ohio                                                                  469
Florida                                                               383
Michigan                                                              255
North Carolina                                                        249
Arizona                                                               224
Virginia                                                              224
Georgia                                                               184
Tennessee                                                             183
Colorado                                                              182
Indiana                                                               149
Kentucky                                                              139
Massachusetts                                                         135
New Jersey                                                            130
Oregon                                                                124
Wisconsin                                                             110
Maryland                                                              105
Delaware                                                               96
Minnesota                                                              89
Connecticut                                                            82
Missouri                                                               66
Oklahoma                                                               66
Alabama                                                                61
Arkansas                                                               60
Rhode Island                                                           56
Mississippi                                                            53
Utah                                                                   53
South Carolina                                                         42
Louisiana                                                              42
Nevada                                                                 39
Nebraska                                                               38
New Mexico                                                             37
Iowa                                                                   30
New Hampshire                                                          27
Kansas                                                                 24
Idaho                                                                  21
Montana                                                                15
South Dakota                                                           12
Vermont                                                                11
District of Columbia                                                   10
Maine                                                                   8
North Dakota                                                            7
West Virginia                                                           4
Wyoming                                                                 1
numunique                                                              49
unique values           [California, New York, Texas, Pennsylvania, Wa...
dtype: object
In [8]:
plt.figure(figsize= (10,16))
store_df.groupby('Category')['Profit','Sales'].agg(['sum']).plot.bar()
plt.ylabel('profit')
plt.show()
<ipython-input-8-523feadc89b7>:2: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
  store_df.groupby('Category')['Profit','Sales'].agg(['sum']).plot.bar()
<Figure size 720x1152 with 0 Axes>

In [9]:
plt.figure(figsize= (10,16))
store_df.groupby('Sub-Category')['Profit','Sales'].agg(['sum']).plot.bar()
plt.ylabel('profit')
plt.show()
<ipython-input-9-c060b103e239>:2: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
  store_df.groupby('Sub-Category')['Profit','Sales'].agg(['sum']).plot.bar()
<Figure size 720x1152 with 0 Axes>

In [10]:
plt.figure(figsize= (10,16))
store_df.groupby('Segment')['Profit','Sales'].agg(['sum']).plot.bar()
plt.ylabel('profit')
plt.show()
<ipython-input-10-7b710e93d812>:2: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
  store_df.groupby('Segment')['Profit','Sales'].agg(['sum']).plot.bar()
<Figure size 720x1152 with 0 Axes>

In [11]:
plt.figure(figsize= (10,16))
store_df.groupby('State')['Profit','Sales'].agg(['sum']).plot.bar()
plt.ylabel('profit')
plt.show()
<ipython-input-11-f8ecda6aa859>:2: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
  store_df.groupby('State')['Profit','Sales'].agg(['sum']).plot.bar()
<Figure size 720x1152 with 0 Axes>

In [12]:
plt.figure(figsize= (10,16))
store_df.groupby('Region')['Profit','Sales'].agg(['sum']).plot.bar()
plt.ylabel('profit')
plt.show()
<ipython-input-12-1cfd200b6950>:2: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
  store_df.groupby('Region')['Profit','Sales'].agg(['sum']).plot.bar()
<Figure size 720x1152 with 0 Axes>

In [13]:
plt.figure(figsize= (10,16))
store_df.groupby('Discount')['Profit','Sales'].agg(['sum']).plot.bar()
plt.ylabel('profit')
plt.show()
<ipython-input-13-67d46ad82c25>:2: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
  store_df.groupby('Discount')['Profit','Sales'].agg(['sum']).plot.bar()
<Figure size 720x1152 with 0 Axes>

In [14]:
plt.figure(figsize= (10,16))
store_df.groupby('Sub-Category')['Profit','Discount'].agg(['sum']).plot.bar()
plt.ylabel('profit')
plt.show()
<ipython-input-14-96b9e91f6efb>:2: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
  store_df.groupby('Sub-Category')['Profit','Discount'].agg(['sum']).plot.bar()
<Figure size 720x1152 with 0 Axes>

In [15]:
plt.figure(figsize=[4,4])
sns.heatmap(store_df.corr(), annot=True)
Out[15]:
<AxesSubplot:>
