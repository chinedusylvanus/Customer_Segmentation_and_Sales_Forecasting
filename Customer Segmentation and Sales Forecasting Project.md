```python
#import libraries
```


```python
import pandas as pd
```


```python
import numpy as np 
```


```python
import matplotlib.pyplot as plt
```


```python
import seaborn as sns
```


```python
from datetime import datetime
```


```python
Sheet_one = pd.read_excel(r'C:\Users\Chinedu\Downloads\online_retail_II.xlsx', sheet_name='Year 2009-2010')
```


```python
Sheet_two = pd.read_excel(r'C:\Users\Chinedu\Downloads\online_retail_II.xlsx', sheet_name='Year 2010-2011')
```


```python
#Combine the two sheets
```


```python
data = pd.concat([Sheet_one, Sheet_two], ignore_index=True)
```


```python
#Quickly understand my data structure
```


```python
data.head(10)
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
      <th>Invoice</th>
      <th>StockCode</th>
      <th>Description</th>
      <th>Quantity</th>
      <th>InvoiceDate</th>
      <th>Price</th>
      <th>Customer ID</th>
      <th>Country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>489434</td>
      <td>85048</td>
      <td>15CM CHRISTMAS GLASS BALL 20 LIGHTS</td>
      <td>12</td>
      <td>2009-12-01 07:45:00</td>
      <td>6.95</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>1</th>
      <td>489434</td>
      <td>79323P</td>
      <td>PINK CHERRY LIGHTS</td>
      <td>12</td>
      <td>2009-12-01 07:45:00</td>
      <td>6.75</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>2</th>
      <td>489434</td>
      <td>79323W</td>
      <td>WHITE CHERRY LIGHTS</td>
      <td>12</td>
      <td>2009-12-01 07:45:00</td>
      <td>6.75</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>3</th>
      <td>489434</td>
      <td>22041</td>
      <td>RECORD FRAME 7" SINGLE SIZE</td>
      <td>48</td>
      <td>2009-12-01 07:45:00</td>
      <td>2.10</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>4</th>
      <td>489434</td>
      <td>21232</td>
      <td>STRAWBERRY CERAMIC TRINKET BOX</td>
      <td>24</td>
      <td>2009-12-01 07:45:00</td>
      <td>1.25</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>5</th>
      <td>489434</td>
      <td>22064</td>
      <td>PINK DOUGHNUT TRINKET POT</td>
      <td>24</td>
      <td>2009-12-01 07:45:00</td>
      <td>1.65</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>6</th>
      <td>489434</td>
      <td>21871</td>
      <td>SAVE THE PLANET MUG</td>
      <td>24</td>
      <td>2009-12-01 07:45:00</td>
      <td>1.25</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>7</th>
      <td>489434</td>
      <td>21523</td>
      <td>FANCY FONT HOME SWEET HOME DOORMAT</td>
      <td>10</td>
      <td>2009-12-01 07:45:00</td>
      <td>5.95</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>8</th>
      <td>489435</td>
      <td>22350</td>
      <td>CAT BOWL</td>
      <td>12</td>
      <td>2009-12-01 07:46:00</td>
      <td>2.55</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>9</th>
      <td>489435</td>
      <td>22349</td>
      <td>DOG BOWL , CHASING BALL DESIGN</td>
      <td>12</td>
      <td>2009-12-01 07:46:00</td>
      <td>3.75</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.shape
```




    (1067371, 8)




```python
data.dtypes
```




    Invoice                object
    StockCode              object
    Description            object
    Quantity                int64
    InvoiceDate    datetime64[ns]
    Price                 float64
    Customer ID           float64
    Country                object
    dtype: object




```python
#Drop Null values in the dataset
```


```python
data.isnull().sum()
```




    Invoice             0
    StockCode           0
    Description      4382
    Quantity            0
    InvoiceDate         0
    Price               0
    Customer ID    243007
    Country             0
    TotalPrice          0
    dtype: int64




```python
data = data.dropna()
```


```python
data.isnull().sum()
```




    Invoice        0
    StockCode      0
    Description    0
    Quantity       0
    InvoiceDate    0
    Price          0
    Customer ID    0
    Country        0
    TotalPrice     0
    dtype: int64




```python
data.shape
```




    (824364, 9)




```python
# Add new column Total Price (Quantity * Price)
```


```python
data['TotalSales'] = data['Quantity'] * data['Price']
```


```python
data.head(10)
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
      <th>Invoice</th>
      <th>StockCode</th>
      <th>Description</th>
      <th>Quantity</th>
      <th>InvoiceDate</th>
      <th>Price</th>
      <th>Customer ID</th>
      <th>Country</th>
      <th>TotalPrice</th>
      <th>TotalSales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>489434</td>
      <td>85048</td>
      <td>15CM CHRISTMAS GLASS BALL 20 LIGHTS</td>
      <td>12</td>
      <td>2009-12-01 07:45:00</td>
      <td>6.95</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>83.4</td>
      <td>83.4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>489434</td>
      <td>79323P</td>
      <td>PINK CHERRY LIGHTS</td>
      <td>12</td>
      <td>2009-12-01 07:45:00</td>
      <td>6.75</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>81.0</td>
      <td>81.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>489434</td>
      <td>79323W</td>
      <td>WHITE CHERRY LIGHTS</td>
      <td>12</td>
      <td>2009-12-01 07:45:00</td>
      <td>6.75</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>81.0</td>
      <td>81.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>489434</td>
      <td>22041</td>
      <td>RECORD FRAME 7" SINGLE SIZE</td>
      <td>48</td>
      <td>2009-12-01 07:45:00</td>
      <td>2.10</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>100.8</td>
      <td>100.8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>489434</td>
      <td>21232</td>
      <td>STRAWBERRY CERAMIC TRINKET BOX</td>
      <td>24</td>
      <td>2009-12-01 07:45:00</td>
      <td>1.25</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>30.0</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>489434</td>
      <td>22064</td>
      <td>PINK DOUGHNUT TRINKET POT</td>
      <td>24</td>
      <td>2009-12-01 07:45:00</td>
      <td>1.65</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>39.6</td>
      <td>39.6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>489434</td>
      <td>21871</td>
      <td>SAVE THE PLANET MUG</td>
      <td>24</td>
      <td>2009-12-01 07:45:00</td>
      <td>1.25</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>30.0</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>489434</td>
      <td>21523</td>
      <td>FANCY FONT HOME SWEET HOME DOORMAT</td>
      <td>10</td>
      <td>2009-12-01 07:45:00</td>
      <td>5.95</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>59.5</td>
      <td>59.5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>489435</td>
      <td>22350</td>
      <td>CAT BOWL</td>
      <td>12</td>
      <td>2009-12-01 07:46:00</td>
      <td>2.55</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>30.6</td>
      <td>30.6</td>
    </tr>
    <tr>
      <th>9</th>
      <td>489435</td>
      <td>22349</td>
      <td>DOG BOWL , CHASING BALL DESIGN</td>
      <td>12</td>
      <td>2009-12-01 07:46:00</td>
      <td>3.75</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>45.0</td>
      <td>45.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
## USING RFM TO DO A CUSTOMER SEGMENTATION ON THE SALES DATA
```


```python
# RFM Calculation (Recency, Frequency, Monetary)
```


```python
reference_date = data['InvoiceDate'].max() + pd.DateOffset(1)
```


```python
print(reference_date)
```

    2011-12-10 12:50:00
    


```python
rfm = data.groupby('Customer ID').agg({
    'InvoiceDate': lambda x: (reference_date - x.max()).days,
    'Invoice': 'nunique',
    'TotalPrice': 'sum'
})
```


```python
rfm.head(10)
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
      <th>InvoiceDate</th>
      <th>Invoice</th>
      <th>TotalPrice</th>
    </tr>
    <tr>
      <th>Customer ID</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>12346.0</th>
      <td>326</td>
      <td>17</td>
      <td>-64.68</td>
    </tr>
    <tr>
      <th>12347.0</th>
      <td>2</td>
      <td>8</td>
      <td>5633.32</td>
    </tr>
    <tr>
      <th>12348.0</th>
      <td>75</td>
      <td>5</td>
      <td>2019.40</td>
    </tr>
    <tr>
      <th>12349.0</th>
      <td>19</td>
      <td>5</td>
      <td>4404.54</td>
    </tr>
    <tr>
      <th>12350.0</th>
      <td>310</td>
      <td>1</td>
      <td>334.40</td>
    </tr>
    <tr>
      <th>12351.0</th>
      <td>375</td>
      <td>1</td>
      <td>300.93</td>
    </tr>
    <tr>
      <th>12352.0</th>
      <td>36</td>
      <td>13</td>
      <td>1889.21</td>
    </tr>
    <tr>
      <th>12353.0</th>
      <td>204</td>
      <td>2</td>
      <td>406.76</td>
    </tr>
    <tr>
      <th>12354.0</th>
      <td>232</td>
      <td>1</td>
      <td>1079.40</td>
    </tr>
    <tr>
      <th>12355.0</th>
      <td>214</td>
      <td>2</td>
      <td>947.61</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Rename the columns accordingly
```


```python
rfm.columns = ['Recency', 'Frequency', 'Monetary']
```


```python
#Consider only customers with postive monetary value
```


```python
rfm = rfm[rfm['Monetary'] > 0]
```


```python
# RFM Scoring
```


```python
rfm['R_Score'] = pd.qcut(rfm['Recency'], 5, labels=[5, 4, 3, 2, 1])
```


```python
rfm['F_Score'] = pd.qcut(rfm['Frequency'].rank(method='first'), 5, labels=[1, 2, 3, 4, 5])
```


```python
rfm['M_Score'] = pd.qcut(rfm['Monetary'], 5, labels=[1, 2, 3, 4, 5])
```


```python
rfm['RFM_Segment'] = rfm['R_Score'].astype(str) + rfm['F_Score'].astype(str) + rfm['M_Score'].astype(str)
```


```python
rfm['RFM_Score'] = rfm[['R_Score', 'F_Score', 'M_Score']].sum(axis=1)
```


```python
rfm.head(10)
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
      <th>Recency</th>
      <th>Frequency</th>
      <th>Monetary</th>
      <th>R_Score</th>
      <th>F_Score</th>
      <th>M_Score</th>
      <th>RFM_Segment</th>
      <th>RFM_Score</th>
    </tr>
    <tr>
      <th>Customer ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>12347.0</th>
      <td>2</td>
      <td>8</td>
      <td>5633.32</td>
      <td>5</td>
      <td>4</td>
      <td>5</td>
      <td>545</td>
      <td>14</td>
    </tr>
    <tr>
      <th>12348.0</th>
      <td>75</td>
      <td>5</td>
      <td>2019.40</td>
      <td>3</td>
      <td>3</td>
      <td>4</td>
      <td>334</td>
      <td>10</td>
    </tr>
    <tr>
      <th>12349.0</th>
      <td>19</td>
      <td>5</td>
      <td>4404.54</td>
      <td>4</td>
      <td>3</td>
      <td>5</td>
      <td>435</td>
      <td>12</td>
    </tr>
    <tr>
      <th>12350.0</th>
      <td>310</td>
      <td>1</td>
      <td>334.40</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>212</td>
      <td>5</td>
    </tr>
    <tr>
      <th>12351.0</th>
      <td>375</td>
      <td>1</td>
      <td>300.93</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>212</td>
      <td>5</td>
    </tr>
    <tr>
      <th>12352.0</th>
      <td>36</td>
      <td>13</td>
      <td>1889.21</td>
      <td>4</td>
      <td>5</td>
      <td>4</td>
      <td>454</td>
      <td>13</td>
    </tr>
    <tr>
      <th>12353.0</th>
      <td>204</td>
      <td>2</td>
      <td>406.76</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>222</td>
      <td>6</td>
    </tr>
    <tr>
      <th>12354.0</th>
      <td>232</td>
      <td>1</td>
      <td>1079.40</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>213</td>
      <td>6</td>
    </tr>
    <tr>
      <th>12355.0</th>
      <td>214</td>
      <td>2</td>
      <td>947.61</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>223</td>
      <td>7</td>
    </tr>
    <tr>
      <th>12356.0</th>
      <td>23</td>
      <td>6</td>
      <td>6373.68</td>
      <td>4</td>
      <td>4</td>
      <td>5</td>
      <td>445</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Segmentation
```


```python
def segment_customers(df):
    if df['RFM_Score'] == 15:
        return 'Platinum Customers'
    elif df['RFM_Score'] >= 12:
        return 'Gold Customers'
    elif df['RFM_Score'] >= 9:
        return 'Silver Customers'
    elif df['RFM_Score'] >= 6:
        return 'Bronze Customers'
    else:
        return 'Low-Value Customers'
```


```python
rfm['Customer_Segment'] = rfm.apply(segment_customers, axis=1)
```


```python
#Visualization
```


```python
segment_counts = rfm['Customer_Segment'].value_counts()
```


```python
print(segment_counts)
```

    Bronze Customers       1448
    Silver Customers       1423
    Low-Value Customers    1264
    Gold Customers         1223
    Platinum Customers      484
    Name: Customer_Segment, dtype: int64
    


```python
plt.figure(figsize=(10, 6))
sns.barplot(x=segment_counts.index, y=segment_counts.values)
plt.title('Customer Segments')
plt.xlabel('Segment')
plt.ylabel('Number of Customers')
plt.xticks(rotation=45)
```




    (array([0, 1, 2, 3, 4]),
     [Text(0, 0, 'Bronze Customers'),
      Text(1, 0, 'Silver Customers'),
      Text(2, 0, 'Low-Value Customers'),
      Text(3, 0, 'Gold Customers'),
      Text(4, 0, 'Platinum Customers')])




    
![png](output_45_1.png)
    



```python
## Performing sales forecasting using the ARIMA (AutoRegressive Integrated Moving Average) model
```


```python

```


```python
# install required libraries
```


```python
pip install statsmodels pmdarima
```


```python
from statsmodels.tsa.arima.model import ARIMA
```


```python
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
```


```python
from pmdarima import auto_arima
```


```python

```


```python
# Group by date to get daily/weekly/monthly sales. We'll use daily sales here:
```


```python
data.head()
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
      <th>Invoice</th>
      <th>StockCode</th>
      <th>Description</th>
      <th>Quantity</th>
      <th>InvoiceDate</th>
      <th>Price</th>
      <th>Customer ID</th>
      <th>Country</th>
      <th>TotalPrice</th>
      <th>TotalSales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>489434</td>
      <td>85048</td>
      <td>15CM CHRISTMAS GLASS BALL 20 LIGHTS</td>
      <td>12</td>
      <td>2009-12-01 07:45:00</td>
      <td>6.95</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>83.4</td>
      <td>83.4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>489434</td>
      <td>79323P</td>
      <td>PINK CHERRY LIGHTS</td>
      <td>12</td>
      <td>2009-12-01 07:45:00</td>
      <td>6.75</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>81.0</td>
      <td>81.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>489434</td>
      <td>79323W</td>
      <td>WHITE CHERRY LIGHTS</td>
      <td>12</td>
      <td>2009-12-01 07:45:00</td>
      <td>6.75</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>81.0</td>
      <td>81.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>489434</td>
      <td>22041</td>
      <td>RECORD FRAME 7" SINGLE SIZE</td>
      <td>48</td>
      <td>2009-12-01 07:45:00</td>
      <td>2.10</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>100.8</td>
      <td>100.8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>489434</td>
      <td>21232</td>
      <td>STRAWBERRY CERAMIC TRINKET BOX</td>
      <td>24</td>
      <td>2009-12-01 07:45:00</td>
      <td>1.25</td>
      <td>13085.0</td>
      <td>United Kingdom</td>
      <td>30.0</td>
      <td>30.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
daily_sales = data.groupby(data['InvoiceDate'].dt.date)['TotalSales'].sum().reset_index()
```


```python
daily_sales.head()

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
      <th>InvoiceDate</th>
      <th>TotalSales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2009-12-01</td>
      <td>42708.22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2009-12-02</td>
      <td>52578.19</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2009-12-03</td>
      <td>61534.22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2009-12-04</td>
      <td>33686.86</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2009-12-05</td>
      <td>9803.05</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Set 'InvoiceDate' as index for time series analysis
daily_sales['InvoiceDate'] = pd.to_datetime(daily_sales['InvoiceDate'])
```


```python
print(daily_sales.columns)
```

    Index(['InvoiceDate', 'TotalSales'], dtype='object')
    


```python
daily_sales.set_index('InvoiceDate', inplace=True)
```


```python
print(type(daily_sales.index))
```

    <class 'pandas.core.indexes.datetimes.DatetimeIndex'>
    


```python
daily_sales = daily_sales.asfreq('D')
```


```python
# Display the first few rows
```


```python
print(daily_sales.head())
```

                 TotalSales
    InvoiceDate            
    2009-12-01     42708.22
    2009-12-02     52578.19
    2009-12-03     61534.22
    2009-12-04     33686.86
    2009-12-05      9803.05
    


```python
#Visualize Time Series Data (To identify trends and seasonality in the time series)
```


```python
plt.figure(figsize=(10, 6))
```




    <Figure size 1000x600 with 0 Axes>




    <Figure size 1000x600 with 0 Axes>



```python
plt.figure(figsize=(10, 6))
plt.plot(daily_sales.index, daily_sales['TotalSales'], label='Daily Sales')
plt.title('Daily Sales Over Time')
plt.xlabel('Date')
plt.ylabel('Sales')
plt.legend()
plt.grid(True)
plt.show()
```


    
![png](output_67_0.png)
    



```python
#Decompose the Time Series (Check for Trend and Seasonality)
```


```python
from statsmodels.tsa.seasonal import seasonal_decompose
```


```python
# Perform seasonal decomposition
decomposition = seasonal_decompose(daily_sales['TotalSales'], model='additive', period=30)
```


```python
# Plot the decomposed components
decomposition.plot()
plt.show()
```


    
![png](output_71_0.png)
    



```python
##Trend: Shows whether there is an upward or downward movement in sales over time.
##Seasonality: Reflects recurring patterns in the data (e.g., daily, weekly, monthly).
##Residuals: The random noise component.
```


```python
## Make the Time Series Stationary
```


```python
from statsmodels.tsa.stattools import adfuller

# ADF test for stationarity
result = adfuller(daily_sales['TotalSales'])

print(f'ADF Statistic: {result[0]}')
print(f'p-value: {result[1]}')

# If the p-value is > 0.05, the series is not stationary, and we may need differencing
```

    ADF Statistic: -2.605429599866257
    p-value: 0.09188026413992395
    


```python
#Since the series is not stationary, apply differencing to remove the trend:
```


```python
# First-order differencing
daily_sales_diff = daily_sales['TotalSales'].diff().dropna()
```


```python
# Plot the differenced series
plt.figure(figsize=(10, 6))
plt.plot(daily_sales_diff)
plt.title('Differenced Sales Series')
plt.show()
```


    
![png](output_77_0.png)
    



```python
#Use the Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF) plots to determine the appropriate AR (p) and MA (q) parameters for ARIMA.
```


```python
# Plot ACF and PACF
plot_acf(daily_sales_diff)
plot_pacf(daily_sales_diff)
plt.show()
```


    
![png](output_79_0.png)
    



    
![png](output_79_1.png)
    



```python
##ACF: Helps identify the MA (Moving Average) term.
##PACF: Helps identify the AR (AutoRegressive) term.
```


```python
##use auto_arima from pmdarima to automatically select the best ARIMA model.
```


```python
# Use auto_arima to determine the best p, d, q values
auto_model = auto_arima(daily_sales['TotalSales'], seasonal=False, trace=True, stepwise=True)
print(auto_model.summary())
```

    Performing stepwise search to minimize aic
     ARIMA(2,1,2)(0,0,0)[0] intercept   : AIC=13157.929, Time=0.82 sec
     ARIMA(0,1,0)(0,0,0)[0] intercept   : AIC=13416.138, Time=0.02 sec
     ARIMA(1,1,0)(0,0,0)[0] intercept   : AIC=13310.916, Time=0.05 sec
     ARIMA(0,1,1)(0,0,0)[0] intercept   : AIC=13167.794, Time=0.06 sec
     ARIMA(0,1,0)(0,0,0)[0]             : AIC=13414.143, Time=0.02 sec
     ARIMA(1,1,2)(0,0,0)[0] intercept   : AIC=13157.975, Time=0.36 sec
     ARIMA(2,1,1)(0,0,0)[0] intercept   : AIC=13161.196, Time=0.34 sec
     ARIMA(3,1,2)(0,0,0)[0] intercept   : AIC=13158.750, Time=0.53 sec
     ARIMA(2,1,3)(0,0,0)[0] intercept   : AIC=13129.202, Time=0.79 sec
     ARIMA(1,1,3)(0,0,0)[0] intercept   : AIC=13157.014, Time=0.63 sec
     ARIMA(3,1,3)(0,0,0)[0] intercept   : AIC=13131.028, Time=1.12 sec
     ARIMA(2,1,4)(0,0,0)[0] intercept   : AIC=13131.296, Time=1.26 sec
     ARIMA(1,1,4)(0,0,0)[0] intercept   : AIC=13160.501, Time=0.38 sec
     ARIMA(3,1,4)(0,0,0)[0] intercept   : AIC=13131.156, Time=1.28 sec
     ARIMA(2,1,3)(0,0,0)[0]             : AIC=13127.032, Time=0.61 sec
     ARIMA(1,1,3)(0,0,0)[0]             : AIC=13155.037, Time=0.58 sec
     ARIMA(2,1,2)(0,0,0)[0]             : AIC=13157.905, Time=0.19 sec
     ARIMA(3,1,3)(0,0,0)[0]             : AIC=13132.404, Time=0.80 sec
     ARIMA(2,1,4)(0,0,0)[0]             : AIC=13129.300, Time=0.73 sec
     ARIMA(1,1,2)(0,0,0)[0]             : AIC=13155.697, Time=0.32 sec
     ARIMA(1,1,4)(0,0,0)[0]             : AIC=13158.534, Time=0.64 sec
     ARIMA(3,1,2)(0,0,0)[0]             : AIC=13156.543, Time=0.43 sec
     ARIMA(3,1,4)(0,0,0)[0]             : AIC=13129.176, Time=1.46 sec
    
    Best model:  ARIMA(2,1,3)(0,0,0)[0]          
    Total fit time: 13.420 seconds
                                   SARIMAX Results                                
    ==============================================================================
    Dep. Variable:                      y   No. Observations:                  604
    Model:               SARIMAX(2, 1, 3)   Log Likelihood               -6557.516
    Date:                Fri, 18 Oct 2024   AIC                          13127.032
    Time:                        11:47:47   BIC                          13153.443
    Sample:                             0   HQIC                         13137.311
                                    - 604                                         
    Covariance Type:                  opg                                         
    ==============================================================================
                     coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------
    ar.L1          0.9452      0.030     31.149      0.000       0.886       1.005
    ar.L2         -0.9365      0.028    -33.868      0.000      -0.991      -0.882
    ma.L1         -1.7093      0.047    -36.546      0.000      -1.801      -1.618
    ma.L2          1.5587      0.071     21.848      0.000       1.419       1.698
    ma.L3         -0.6720      0.040    -16.858      0.000      -0.750      -0.594
    sigma2      1.779e+08   3.82e-10   4.66e+17      0.000    1.78e+08    1.78e+08
    ===================================================================================
    Ljung-Box (L1) (Q):                   0.00   Jarque-Bera (JB):               720.01
    Prob(Q):                              0.98   Prob(JB):                         0.00
    Heteroskedasticity (H):               1.60   Skew:                             1.22
    Prob(H) (two-sided):                  0.00   Kurtosis:                         7.76
    ===================================================================================
    
    Warnings:
    [1] Covariance matrix calculated using the outer product of gradients (complex-step).
    [2] Covariance matrix is singular or near-singular, with condition number 1.27e+33. Standard errors may be unstable.
    


```python
##Build the ARIMA Model
```


```python
#order(p,d,q) where p is the AutoRegressive term (AR), d is Differencing term/Integrated part (I) and q is Moving Average term (MA)
```


```python
model = ARIMA(daily_sales['TotalSales'], order=(2, 1, 3))
```


```python
# Fit the model

```


```python
arima_result = model.fit()
```


```python
# Display the summary
print(arima_result.summary())
```

                                   SARIMAX Results                                
    ==============================================================================
    Dep. Variable:             TotalSales   No. Observations:                  739
    Model:                 ARIMA(2, 1, 3)   Log Likelihood               -6577.942
    Date:                Fri, 18 Oct 2024   AIC                          13167.884
    Time:                        16:18:02   BIC                          13195.508
    Sample:                    12-01-2009   HQIC                         13178.536
                             - 12-09-2011                                         
    Covariance Type:                  opg                                         
    ==============================================================================
                     coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------
    ar.L1          0.4364      0.224      1.945      0.052      -0.003       0.876
    ar.L2         -0.6313      0.175     -3.609      0.000      -0.974      -0.288
    ma.L1         -1.2012      0.215     -5.599      0.000      -1.622      -0.781
    ma.L2          0.9574      0.280      3.418      0.001       0.408       1.506
    ma.L3         -0.6288      0.135     -4.652      0.000      -0.894      -0.364
    sigma2      2.175e+08    9.8e-10   2.22e+17      0.000    2.17e+08    2.17e+08
    ===================================================================================
    Ljung-Box (L1) (Q):                   0.54   Jarque-Bera (JB):              1715.63
    Prob(Q):                              0.46   Prob(JB):                         0.00
    Heteroskedasticity (H):               1.77   Skew:                             1.40
    Prob(H) (two-sided):                  0.00   Kurtosis:                         9.93
    ===================================================================================
    
    Warnings:
    [1] Covariance matrix calculated using the outer product of gradients (complex-step).
    [2] Covariance matrix is singular or near-singular, with condition number 5.91e+32. Standard errors may be unstable.
    


```python
#Make Predictions and Plot the Forecast
```


```python
# Forecast future sales (e.g., next 30 days)
forecast = arima_result.forecast(steps=30)
```


```python
# Plot the actual and forecasted sales
```


```python
plt.figure(figsize=(10, 6))
plt.plot(daily_sales.index, daily_sales['TotalSales'], label='Actual Sales')
plt.plot(pd.date_range(start=daily_sales.index[-1], periods=30, freq='D'), forecast, label='Forecasted Sales', color='red')
plt.title('Actual vs Forecasted Sales')
plt.xlabel('Date')
plt.ylabel('Sales')
plt.legend()
plt.grid(True)
plt.show()
```


    
![png](output_92_0.png)
    



```python
forecast.head(30)
```




    2011-12-10    34496.040142
    2011-12-11    35069.667968
    2011-12-12    42381.763390
    2011-12-13    45210.487971
    2011-12-14    41828.665551
    2011-12-15    38567.088129
    2011-12-16    39278.786534
    2011-12-17    41648.436963
    2011-12-18    42233.203810
    2011-12-19    40992.392609
    2011-12-20    40081.754178
    2011-12-21    40467.709406
    2011-12-22    41211.031630
    2011-12-23    41291.744941
    2011-12-24    40857.697272
    2011-12-25    40617.331455
    2011-12-26    40786.460463
    2011-12-27    41012.011467
    2011-12-28    41003.664316
    2011-12-29    40857.628344
    2011-12-30    40799.170608
    2011-12-31    40865.855233
    2012-01-01    40931.860341
    2012-01-02    40918.564839
    2012-01-03    40871.093001
    2012-01-04    40858.770798
    2012-01-05    40883.363235
    2012-01-06    40901.874097
    2012-01-07    40894.426354
    2012-01-08    40879.490137
    Freq: D, Name: predicted_mean, dtype: float64




```python
##Use the time series trend and seasonality components to identify key periods of high and low sales.
#Forecast Accuracy: Review forecast accuracy to assess the reliability of the predictions.
#Recommendations: Provide management with insights such as:
#Expected increase/decrease in sales for future periods.
#Seasonal trends to consider when planning marketing or promotions.
#Potential areas for optimizing inventory and supply chain planning.
```


```python

```
