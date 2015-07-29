---
layout: default
overview: true
title: Learning Data Frames in R
---

#Data Frames - most frequented data in R
This is where whatever we have learnt culminates. That is..
+ data types
+ vectors
+ matrix
+ lists

A data frame is collection of vectors of equal length. Lets see how it gets defined. It's type is different than ``list``. We have to use ``data.frame()`` to define a variable.

Example:
```
> cdg = c(23.5, 12,2,40,45)
> ndls = c(12,20,0, 35, 20)
> rainfall = data.frame(cdg, ndls)
> rainfall
   cdg ndls
1 23.5   12
2 12.0   20
3  2.0    0
4 40.0   35
5 45.0   20
> #note here the name of the variables is caught by data.frame
> month = c("Jan", "Feb", "Mar", "Apr", "May")
> month
[1] "Jan" "Feb" "Mar" "Apr" "May"
> cbind(rainfall, month)
   cdg ndls month
1 23.5   12   Jan
2 12.0   20   Feb
3  2.0    0   Mar
4 40.0   35   Apr
5 45.0   20   May
> row.names(rainfall) =  c("Jan", "Feb", "Mar", "Apr", "May")
> rainfall
     cdg ndls
Jan 23.5   12
Feb 12.0   20
Mar  2.0    0
Apr 40.0   35
May 45.0   20
# checkout every row has got a label
```

Further, like in list, one can assign values as:
```
> country = data.frame(states=c("Andhra Pradesh", "Uttar Pradesh", "Punjab"), capital=c("Hyderabad", "Lucknow", "Chandigarh"))
> country
          states    capital
1 Andhra Pradesh  Hyderabad
2  Uttar Pradesh    Lucknow
3         Punjab Chandigarh
> # here we see column names/labels are used like an associative array
```

## Helpers for data.frame
+ nrow() - returns number of rows
+ ncol() - returns number of columns
+ head() - returns top 3 rows of the frame
+ tail() - returns last 3 rows of the frame

## Accessing its members
It is same way as we do it for lists. That is use of ``[[]]``.
```
> rainfall[[2]]
[1] 12 20  0 35 20
> rainfall[["ndls"]]
[1] 12 20  0 35 20
> rainfall[,"ndls"]
[1] 12 20  0 35 20
> rainfall[,1:2]
     cdg ndls
Jan 23.5   12
Feb 12.0   20
Mar  2.0    0
Apr 40.0   35
May 45.0   20
> rainfall[,c("ndls", "cdg")]
    ndls  cdg
Jan   12 23.5
Feb   20 12.0
Mar    0  2.0
Apr   35 40.0
May   20 45.0
> rainfall[c(TRUE, TRUE, FALSE, FALSE, FALSE),]
     cdg ndls
Jan 23.5   12
Feb 12.0   20
> rainfall[c(2,5), ]
    cdg ndls
Feb  12   20
May  45   20
> 
```

Lets learn a simple trick here:
```
> rainfall$cdg
[1] 23.5 12.0  2.0 40.0 45.0
> rainy = rainfall$cdg > 10
> rainy
[1]  TRUE  TRUE FALSE  TRUE  TRUE
> rainfall[rainy,]
     cdg ndls
Jan 23.5   12
Feb 12.0   20
Apr 40.0   35
May 45.0   20
> typeof(rainy)
> [1] "logical"
```

We used logical operation here applied over all members of a vector.

##Loading data from files
Different packages within R support multiple data file formats. Lets see their mapping below:

Format, Package/Library, Function used

+ Excel sheets: gdata; read.xls
+ Excel sheets: XLConnect; loadWorkbook, loadWorksheet
+ MiniTab: foreign; read.mtp
+ SPSS:  foreign; read.spss
+ Text File with Spaces: ; read.table
+ CSV: ; read.csv

Set up the current working directory to different location where the data files are lying:
```
setcwd("/home/vineet/R/data")
getwd()
[1] "/home/vineet/R/data"
```
