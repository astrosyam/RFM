# RFM Analysis (Recency, Frequency and Monetary)

RFM is frequently employed in customer analytics and tools like SPSS have built in functions to perform it. This repository is an effort to make a similar package for R.

<b> Sample data set : "sales" </b>
<i> Fictional dataset containing customer names, date of purchase and amount of purchase. </i>


```r
library(RFM)
head(sales)
```

```
##                  customer       date amount
## 1           Bunting, Dana 2015-03-15     13
## 2              Lee, David 2015-10-31     54
## 3 Williams Taylor, Joshua 2015-06-01      7
## 4         Ospina, Brenden 2015-09-13      9
## 5       Jimenez, Victoria 2015-02-22     65
## 6       Jimenez, Victoria 2015-05-30     72
```

<b> Perform simple RFM analysis on the data </b>


```r
rfm(sales)
```

```
##                   customer Recency Frequency Monetary RFM_Score
## 1            Bunting, Dana      53        13      669       555
## 10 Williams Taylor, Joshua      68         5      194       511
## 2            Hester, Sarah      71        15      842       455
## 4      Kusi-Mensah, Victor      73        11      546       433
## 3        Jimenez, Victoria      74        10      662       334
## 8       Thatcher, Angelica      78         8      546       323
## 7          Ospina, Brenden     107        15      528       252
## 5               Lee, David     115         6      379       212
## 6         Martinez, Daijah     122        12      581       144
## 9              Verde, Noah     173         5      303       111
```

By default, Recency is calculated from the current date.
This behaviour can be altered by specifying Analysis date.


```r
#RFM with analysis date as 20th of Jan 2016
rfm(sales,analysisDate = "2016/01/20")
```

```
##                   customer Recency Frequency Monetary RFM_Score
## 1            Bunting, Dana      19        13      669       555
## 10 Williams Taylor, Joshua      34         5      194       511
## 2            Hester, Sarah      37        15      842       455
## 4      Kusi-Mensah, Victor      39        11      546       433
## 3        Jimenez, Victoria      40        10      662       334
## 8       Thatcher, Angelica      44         8      546       323
## 7          Ospina, Brenden      73        15      528       252
## 5               Lee, David      81         6      379       212
## 6         Martinez, Daijah      88        12      581       144
## 9              Verde, Noah     139         5      303       111
```

Note the dates have to be in "yyyy/mm/dd" format. eg : 2016/12/23.

By default, the function looks for "customer", "date" and "amount" columns.

Custom column names may be specified:


```r
#Creating  sales data  set with customer, billDate and revenue as column names
newsales = sales
names(newsales) = c("customer", "billDate", "revenue")
rfm(newsales,analysisDate = "2016/01/20", customer = "customer", date = "billDate", revenue = "revenue")
```

```
##                   customer Recency Frequency Monetary RFM_Score
## 1            Bunting, Dana      19        13      669       555
## 10 Williams Taylor, Joshua      34         5      194       511
## 2            Hester, Sarah      37        15      842       455
## 4      Kusi-Mensah, Victor      39        11      546       433
## 3        Jimenez, Victoria      40        10      662       334
## 8       Thatcher, Angelica      44         8      546       323
## 7          Ospina, Brenden      73        15      528       252
## 5               Lee, David      81         6      379       212
## 6         Martinez, Daijah      88        12      581       144
## 9              Verde, Noah     139         5      303       111
```

<b>Installation</b>


```r
#Uncomment block below
#install.packages("devtools")
#library(devtools)
#install_github("astrosyam/RFM")
```

<i>Disclaimer:
This is an initial commit and is therefore limited to basic RFM.
The code is currently not optimized or bug free.</i>

<b> Wishlist </b>

Future commits will add the following functionalities:

1. Custom weightage of components, for eg. MFR, where Monetary has a higher preference than Recency while scoring.

2. Specify custom bins for scoring

3. Customer purchase latency
