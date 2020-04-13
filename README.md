# **Data Analysis Case Study: Changes in Fine Particule Air Pollution in the U.S.**
We are gonna walk through a nine step process of data analysis in analysing the dataset. This step by step process is gonna helpfull to any beginner in the data analysis cluster of study. The nine steps are:
1. Formulate your question
2. Read in your data
3. Check the packaging
4. Run str()
5. Look at the top and the bottom of your data
6. Check your “n”s
7. Validate with at least one external data source
8. Try the easy solution first
9. Challenge your solution
10. Follow up

**Step 01:  Formulate your question**
First thing is that, we have to know what we are looking for from a dataset!  What things we are gonna find! It may come as a hypotheis or as a question. Better to formulate a sharpe question rather than moving here and there and find particularly what you are looking for. 

We are gonna look at the air pollution dataset which comes from US environmental protection agency (EPA). This is a monitored data of Fine Particulate matter in the air. Fine particulate matter is just a fancy way of saying dust in the airwhich is sometimes called PM2.5. When these types of data comes we generally want to know about "Is the air pollution reduced compared to before or increased?" 

So we are gonna formulate question as "Is the air pollution reduced from 1999 to 2012?"

**Step 02:  Read in your data**
We are gonna download data from [EPA website](https://www3.epa.gov/ttn/airs/airsaqs/detaildata/downloadaqsdata.htm). In the directory, lets look at the daownloaded files,
```
> list.files()
[1] "RD_501_88101_1999-0.txt" "RD_501_88101_2012-0.txt"
```
So, the is 2 .txt files. One conains data of 1999 and other contains data of 2012. Now, let's read the data with usual `read.table()`.
```
> pm0<- read.table("RD_501_88101_1999-0.txt")
> str(pm0)
'data.frame':	117421 obs. of  1 variable:
 $ V1: Factor w/ 117421 levels "RD|I|01|027|0001|88101|1|7|105|120|19990103|00:00||AS|3|||||||||||||",..: 1 2 3 4 5 6 7 8 9 10 ...
> head(pm0)
                                                                       V1
1    RD|I|01|027|0001|88101|1|7|105|120|19990103|00:00||AS|3|||||||||||||
2    RD|I|01|027|0001|88101|1|7|105|120|19990106|00:00||AS|3|||||||||||||
3    RD|I|01|027|0001|88101|1|7|105|120|19990109|00:00||AS|3|||||||||||||
4 RD|I|01|027|0001|88101|1|7|105|120|19990112|00:00|8.841||3|||||||||||||
5 RD|I|01|027|0001|88101|1|7|105|120|19990115|00:00|14.92||3|||||||||||||
6 RD|I|01|027|0001|88101|1|7|105|120|19990118|00:00|3.878||3|||||||||||||
```
Here, we can see, its kinda messy data. We need to organize them as our need. First of all, they are not clear to understand and there is an extra column named V1. Lets correct these things. If we set the argument `header= F`, value is then determined from file format. We determine the sperator as `|` and missing values as blank strings.
```
 > pm0<- read.table("RD_501_88101_1999-0.txt", comment.char= "#", header = F, sep = "|", na.strings = "")
 > head(pm0)
  V1 V2 V3 V4 V5    V6 V7 V8  V9 V10      V11   V12    V13  V14 V15 V16  V17 V18 V19 V20 V21 V22 V23
1 RD  I  1 27  1 88101  1  7 105 120 19990103 00:00     NA   AS   3  NA <NA>  NA  NA  NA  NA  NA  NA
2 RD  I  1 27  1 88101  1  7 105 120 19990106 00:00     NA   AS   3  NA <NA>  NA  NA  NA  NA  NA  NA
3 RD  I  1 27  1 88101  1  7 105 120 19990109 00:00     NA   AS   3  NA <NA>  NA  NA  NA  NA  NA  NA
4 RD  I  1 27  1 88101  1  7 105 120 19990112 00:00  8.841 <NA>   3  NA <NA>  NA  NA  NA  NA  NA  NA
5 RD  I  1 27  1 88101  1  7 105 120 19990115 00:00 14.920 <NA>   3  NA <NA>  NA  NA  NA  NA  NA  NA
6 RD  I  1 27  1 88101  1  7 105 120 19990118 00:00  3.878 <NA>   3  NA <NA>  NA  NA  NA  NA  NA  NA
  V24 V25 V26 V27 V28
1  NA  NA  NA  NA  NA
2  NA  NA  NA  NA  NA
3  NA  NA  NA  NA  NA
4  NA  NA  NA  NA  NA
5  NA  NA  NA  NA  NA
6  NA  NA  NA  NA  NA
 ```
 **Step 03:  Check the packaging**
 Have you ever gotten a present before the time when you were allowed to open it? Sure,
we all have. The problem is that the present is wrapped, but you desperately want to
know what’s inside. What’s a person to do in those circumstances? Well, you can shake
the box a bit, maybe knock it with your knuckle to see if it makes a hollow sound, or even
weigh it to see how heavy it is. This is how you should think about your dataset before
you start analyzing it for real.
Assuming you don’t get any warnings or errors when reading in the dataset, you should
now have an object in your workspace named pm0. It’s usually a good idea to poke at
that object a little bit before we break open the wrapping paper.
For example, you can check the number of rows and columns.
```
> nrow(pm0)
[1] 117421
> ncol(pm0)
[1] 28
```
Remember when I said there were 117421 rows in the file? How does that match up
with what we’ve read in? This dataset also has relatively few columns, so you might be
able to check the original text file to see if the number of columns printed out (28) here
matches the number of columns you see in the original file. Another is just to run `dim()`
```
> dim(pm0)
[1] 117421     28
```
 **Step 04:  Run str()**
 Another thing you can do is run str() on the dataset. This is usually a safe operation in
the sense that even with a very large dataset, running str() shouldn’t take too long.
```
> str(pm0)
'data.frame':	117421 obs. of  28 variables:
 $ V1 : Factor w/ 1 level "RD": 1 1 1 1 1 1 1 1 1 1 ...
 $ V2 : Factor w/ 1 level "I": 1 1 1 1 1 1 1 1 1 1 ...
 $ V3 : int  1 1 1 1 1 1 1 1 1 1 ...
 $ V4 : int  27 27 27 27 27 27 27 27 27 27 ...
 $ V5 : int  1 1 1 1 1 1 1 1 1 1 ...
 $ V6 : int  88101 88101 88101 88101 88101 88101 88101 88101 88101 88101 ...
 $ V7 : int  1 1 1 1 1 1 1 1 1 1 ...
 $ V8 : int  7 7 7 7 7 7 7 7 7 7 ...
 $ V9 : int  105 105 105 105 105 105 105 105 105 105 ...
 $ V10: int  120 120 120 120 120 120 120 120 120 120 ...
 $ V11: int  19990103 19990106 19990109 19990112 19990115 19990118 19990121 19990124 19990127 19990130 ...
 $ V12: Factor w/ 11 levels "00:00","01:00",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ V13: num  NA NA NA 8.84 14.92 ...
 $ V14: Factor w/ 32 levels "AA","AB","AC",..: 19 19 19 NA NA NA NA NA NA NA ...
 $ V15: int  3 3 3 3 3 3 3 3 3 3 ...
 $ V16: logi  NA NA NA NA NA NA ...
 $ V17: Factor w/ 21 levels "1","2","3","4",..: NA NA NA NA NA NA NA NA NA NA ...
 $ V18: logi  NA NA NA NA NA NA ...
 $ V19: logi  NA NA NA NA NA NA ...
 $ V20: logi  NA NA NA NA NA NA ...
 $ V21: logi  NA NA NA NA NA NA ...
 $ V22: logi  NA NA NA NA NA NA ...
 $ V23: logi  NA NA NA NA NA NA ...
 $ V24: logi  NA NA NA NA NA NA ...
 $ V25: logi  NA NA NA NA NA NA ...
 $ V26: logi  NA NA NA NA NA NA ...
 $ V27: logi  NA NA NA NA NA NA ...
 $ V28: logi  NA NA NA NA NA NA ...
 ```
 **Step 05: Look at the top and the bottom of your data**
I find it useful to look at the “beginning” and “end” of a dataset right after I check the packaging. This lets me know if the data were read in properly, things are properly formatted, and that everthing is there. If your data are time series data, then make sure
the dates at the beginning and end of the dataset match what you expect the beginning
and ending time period to be.
You can peek at the top and bottom of the data with the head() and tail() functions.
```
> head(pm0)
  V1 V2 V3 V4 V5    V6 V7 V8  V9 V10      V11   V12    V13  V14 V15 V16  V17 V18 V19 V20 V21 V22 V23
1 RD  I  1 27  1 88101  1  7 105 120 19990103 00:00     NA   AS   3  NA <NA>  NA  NA  NA  NA  NA  NA
2 RD  I  1 27  1 88101  1  7 105 120 19990106 00:00     NA   AS   3  NA <NA>  NA  NA  NA  NA  NA  NA
3 RD  I  1 27  1 88101  1  7 105 120 19990109 00:00     NA   AS   3  NA <NA>  NA  NA  NA  NA  NA  NA
4 RD  I  1 27  1 88101  1  7 105 120 19990112 00:00  8.841 <NA>   3  NA <NA>  NA  NA  NA  NA  NA  NA
5 RD  I  1 27  1 88101  1  7 105 120 19990115 00:00 14.920 <NA>   3  NA <NA>  NA  NA  NA  NA  NA  NA
6 RD  I  1 27  1 88101  1  7 105 120 19990118 00:00  3.878 <NA>   3  NA <NA>  NA  NA  NA  NA  NA  NA
  V24 V25 V26 V27 V28
1  NA  NA  NA  NA  NA
2  NA  NA  NA  NA  NA
3  NA  NA  NA  NA  NA
4  NA  NA  NA  NA  NA
5  NA  NA  NA  NA  NA
6  NA  NA  NA  NA  NA
> tail(pm0)
       V1 V2 V3 V4 V5    V6 V7 V8  V9 V10      V11   V12 V13  V14 V15 V16  V17 V18 V19 V20 V21 V22
117416 RD  I 78 10 12 88101  1  7 105 116 19991126 00:00  NA   AO   6  NA <NA>  NA  NA  NA  NA  NA
117417 RD  I 78 10 12 88101  1  7 105 116 19991202 00:00  NA   AO   6  NA <NA>  NA  NA  NA  NA  NA
117418 RD  I 78 10 12 88101  1  7 105 116 19991208 00:00 5.5 <NA>   6  NA <NA>  NA  NA  NA  NA  NA
117419 RD  I 78 10 12 88101  1  7 105 116 19991214 00:00  NA   AM   6  NA <NA>  NA  NA  NA  NA  NA
117420 RD  I 78 10 12 88101  1  7 105 116 19991220 00:00  NA   AM   6  NA <NA>  NA  NA  NA  NA  NA
117421 RD  I 78 10 12 88101  1  7 105 116 19991226 00:00 4.9 <NA>   6  NA <NA>  NA  NA  NA  NA  NA
       V23 V24 V25 V26 V27 V28
117416  NA  NA  NA  NA  NA  NA
117417  NA  NA  NA  NA  NA  NA
117418  NA  NA  NA  NA  NA  NA
117419  NA  NA  NA  NA  NA  NA
117420  NA  NA  NA  NA  NA  NA
117421  NA  NA  NA  NA  NA  NA
```
 **Step 05: Check your “n”s**
 Now, we want the column names. Referring them with just V1, v2 etc can be dillisional. Wa want their real names which was storoed in the 1st column we rejected while reading with `header= F`. I was wea are gonna just read 1st line.
 ```
 > cnames<- readLines("RD_501_88101_1999-0.txt", 1)
> cnames
[1] "# RD|Action Code|State Code|County Code|Site ID|Parameter|POC|Sample Duration|Unit|Method|Date|Start Time|Sample Value|Null Data Code|Sampling Frequency|Monitor Protocol (MP) ID|Qualifier - 1|Qualifier - 2|Qualifier - 3|Qualifier - 4|Qualifier - 5|Qualifier - 6|Qualifier - 7|Qualifier - 8|Qualifier - 9|Qualifier - 10|Alternate Method Detectable Limit|Uncertainty"
```
When we print this out, we will see there is only string. Because, we just read the lines directly not the tables. So, we need to split all the columns.
```
> cnames<- strsplit(cnames, "|", fixed = T)
> cnames
[[1]]
 [1] "# RD"                              "Action Code"                      
 [3] "State Code"                        "County Code"                      
 [5] "Site ID"                           "Parameter"                        
 [7] "POC"                               "Sample Duration"                  
 [9] "Unit"                              "Method"                           
[11] "Date"                              "Start Time"                       
[13] "Sample Value"                      "Null Data Code"                   
[15] "Sampling Frequency"                "Monitor Protocol (MP) ID"         
[17] "Qualifier - 1"                     "Qualifier - 2"                    
[19] "Qualifier - 3"                     "Qualifier - 4"                    
[21] "Qualifier - 5"                     "Qualifier - 6"                    
[23] "Qualifier - 7"                     "Qualifier - 8"                    
[25] "Qualifier - 9"                     "Qualifier - 10"                   
[27] "Alternate Method Detectable Limit" "Uncertainty"  
```
We splitted it with | as not a reglar expression but fixed so set the fixed argument as true. Now if we look at cnames it is organized. Strsplit actually returns a list back. Now lets combne the names with the dataframe.
```
> names(pm0)<- cnames[[1]]
> head(pm0)
  # RD Action Code State Code County Code Site ID Parameter POC Sample Duration Unit Method     Date
1   RD           I          1          27       1     88101   1               7  105    120 19990103
2   RD           I          1          27       1     88101   1               7  105    120 19990106
3   RD           I          1          27       1     88101   1               7  105    120 19990109
4   RD           I          1          27       1     88101   1               7  105    120 19990112
5   RD           I          1          27       1     88101   1               7  105    120 19990115
6   RD           I          1          27       1     88101   1               7  105    120 19990118
  Start Time Sample Value Null Data Code Sampling Frequency Monitor Protocol (MP) ID Qualifier - 1
1      00:00           NA             AS                  3                       NA          <NA>
2      00:00           NA             AS                  3                       NA          <NA>
3      00:00           NA             AS                  3                       NA          <NA>
4      00:00        8.841           <NA>                  3                       NA          <NA>
5      00:00       14.920           <NA>                  3                       NA          <NA>
6      00:00        3.878           <NA>                  3                       NA          <NA>
  Qualifier - 2 Qualifier - 3 Qualifier - 4 Qualifier - 5 Qualifier - 6 Qualifier - 7 Qualifier - 8
1            NA            NA            NA            NA            NA            NA            NA
2            NA            NA            NA            NA            NA            NA            NA
3            NA            NA            NA            NA            NA            NA            NA
4            NA            NA            NA            NA            NA            NA            NA
5            NA            NA            NA            NA            NA            NA            NA
6            NA            NA            NA            NA            NA            NA            NA
  Qualifier - 9 Qualifier - 10 Alternate Method Detectable Limit Uncertainty
1            NA             NA                                NA          NA
2            NA             NA                                NA          NA
3            NA             NA                                NA          NA
4            NA             NA                                NA          NA
5            NA             NA                                NA          NA
6            NA             NA                                NA          NA
```
But the column names are separated by spcaes in between. Lets fix that.
```
> names(pm0)<- make.names(cnames[[1]])
> head(pm0)
  X..RD Action.Code State.Code County.Code Site.ID Parameter POC Sample.Duration Unit Method     Date
1    RD           I          1          27       1     88101   1               7  105    120 19990103
2    RD           I          1          27       1     88101   1               7  105    120 19990106
3    RD           I          1          27       1     88101   1               7  105    120 19990109
4    RD           I          1          27       1     88101   1               7  105    120 19990112
5    RD           I          1          27       1     88101   1               7  105    120 19990115
6    RD           I          1          27       1     88101   1               7  105    120 19990118
  Start.Time Sample.Value Null.Data.Code Sampling.Frequency Monitor.Protocol..MP..ID Qualifier...1
1      00:00           NA             AS                  3                       NA          <NA>
2      00:00           NA             AS                  3                       NA          <NA>
3      00:00           NA             AS                  3                       NA          <NA>
4      00:00        8.841           <NA>                  3                       NA          <NA>
5      00:00       14.920           <NA>                  3                       NA          <NA>
6      00:00        3.878           <NA>                  3                       NA          <NA>
  Qualifier...2 Qualifier...3 Qualifier...4 Qualifier...5 Qualifier...6 Qualifier...7 Qualifier...8
1            NA            NA            NA            NA            NA            NA            NA
2            NA            NA            NA            NA            NA            NA            NA
3            NA            NA            NA            NA            NA            NA            NA
4            NA            NA            NA            NA            NA            NA            NA
5            NA            NA            NA            NA            NA            NA            NA
6            NA            NA            NA            NA            NA            NA            NA
  Qualifier...9 Qualifier...10 Alternate.Method.Detectable.Limit Uncertainty
1            NA             NA                                NA          NA
2            NA             NA                                NA          NA
3            NA             NA                                NA          NA
4            NA             NA                                NA          NA
5            NA             NA                                NA          NA
6            NA             NA                                NA          NA
```
make.names usually takes the strings and assign the column names correctly while sperating them default (.) value.
 **Step 07: Validate with at least one external data source**
Making sure your data matches something outside of the dataset is very important. It
allows you to ensure that the measurements are roughly in line with what they should
be and it serves as a check on what other things might be wrong in your dataset. External
validation can often be as simple as checking your data against a single number, as we
will do here. We are gonna do that kwith summary values here.
```
> summary(pm0)
 X..RD       Action.Code   State.Code     County.Code        Site.ID         Parameter    
 RD:117421   I:117421    Min.   : 1.00   Min.   :  1.00   Min.   :   1.0   Min.   :88101  
                         1st Qu.:13.00   1st Qu.: 27.00   1st Qu.:   7.0   1st Qu.:88101  
                         Median :30.00   Median : 61.00   Median :  22.0   Median :88101  
                         Mean   :29.16   Mean   : 78.72   Mean   : 658.3   Mean   :88101  
                         3rd Qu.:42.00   3rd Qu.:101.00   3rd Qu.:1001.0   3rd Qu.:88101  
                         Max.   :78.00   Max.   :810.00   Max.   :9997.0   Max.   :88101  
                                                                                          
      POC       Sample.Duration      Unit         Method           Date            Start.Time    
 Min.   :1.00   Min.   :7       Min.   :105   Min.   :116.0   Min.   :19990101   00:00  :117370  
 1st Qu.:1.00   1st Qu.:7       1st Qu.:105   1st Qu.:118.0   1st Qu.:19990424   11:00  :    13  
 Median :1.00   Median :7       Median :105   Median :118.0   Median :19990723   12:00  :    13  
 Mean   :1.06   Mean   :7       Mean   :105   Mean   :118.6   Mean   :19990719   10:00  :     7  
 3rd Qu.:1.00   3rd Qu.:7       3rd Qu.:105   3rd Qu.:120.0   3rd Qu.:19991015   01:00  :     5  
 Max.   :2.00   Max.   :7       Max.   :105   Max.   :120.0   Max.   :19991231   09:00  :     5  
                                                                                 (Other):     8  
  Sample.Value    Null.Data.Code   Sampling.Frequency Monitor.Protocol..MP..ID Qualifier...1   
 Min.   :  0.00   AN     :  5020   Min.   :0.000      Mode:logical             1      :  5425  
 1st Qu.:  7.20   AQ     :  1148   1st Qu.:1.000      NA's:117421              2      :  3759  
 Median : 11.50   AR     :   912   Median :3.000                               T      :  2528  
 Mean   : 13.74   AM     :   889   Mean   :2.619                               X      :  2290  
 3rd Qu.: 17.90   AS     :   845   3rd Qu.:3.000                               V      :  1321  
 Max.   :157.10   (Other):  4403   Max.   :9.000                               (Other):  1772  
 NA's   :13217    NA's   :104204   NA's   :9575                                NA's   :100326  
 Qualifier...2  Qualifier...3  Qualifier...4  Qualifier...5  Qualifier...6  Qualifier...7 
 Mode:logical   Mode:logical   Mode:logical   Mode:logical   Mode:logical   Mode:logical  
 NA's:117421    NA's:117421    NA's:117421    NA's:117421    NA's:117421    NA's:117421   
                                                                                          
                                                                                          
                                                                                          
                                                                                          
                                                                                          
 Qualifier...8  Qualifier...9  Qualifier...10 Alternate.Method.Detectable.Limit Uncertainty   
 Mode:logical   Mode:logical   Mode:logical   Mode:logical                      Mode:logical  
 NA's:117421    NA's:117421    NA's:117421    NA's:117421                       NA's:117421   
```
 **Step 10: Follow up**
 for now, i am gonna skip to the step 10. We will discuss 2 steps later. 
  now, we are gonna just bring out the values of PM2.5 which are the values in sample values. 
  ```
  > x0<- pm0$Sample.Value
> class(x0)
[1] "numeric"
```
Here we can see it is numeric. Lets run a str() on it
```
> str(x0)
 num [1:117421] NA NA NA 8.84 14.92 ...
 ```
 So, we have 117421 values on it including NA values. Lets see the summary now. 
 ```
 > summary(x0)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
   0.00    7.20   11.50   13.74   17.90  157.10   13217 
   ```
   So, we can see median is 11.50 kg/m^3 and maximum is 157.10 which is quit a large value for a daily basis. We can also see there is 13217 missing values. That can be a problem if we just do not count them. Lets what parcentage it is? Can it be a problem?
   ```
   > mean(is.na(x0))
[1] 0.1125608
```
so, about 11% is missing. So, it can make a big difference in the analysis. But missing values are not always a problem it depends on what type of question are you trying to answer.

Now lets load the data for 2012.
```
> pm1<- read.table("RD_501_88101_2012-0.txt", header = F, sep = "|", na.strings = "")
> dim(pm1)
[1] 1304287      28
```
SO, there is 1304287 number of observations. Now, lets fix the column names:
```
> names(pm1)<- make.names(cnames[[1]])
> head(pm1)
  X..RD Action.Code State.Code County.Code Site.ID Parameter POC Sample.Duration Unit Method     Date
1    RD           I          1           3      10     88101   1               7  105    118 20120101
2    RD           I          1           3      10     88101   1               7  105    118 20120104
3    RD           I          1           3      10     88101   1               7  105    118 20120107
4    RD           I          1           3      10     88101   1               7  105    118 20120110
5    RD           I          1           3      10     88101   1               7  105    118 20120113
6    RD           I          1           3      10     88101   1               7  105    118 20120116
  Start.Time Sample.Value Null.Data.Code Sampling.Frequency Monitor.Protocol..MP..ID Qualifier...1
1      00:00          6.7           <NA>                  3                       NA          <NA>
2      00:00          9.0           <NA>                  3                       NA          <NA>
3      00:00          6.5           <NA>                  3                       NA          <NA>
4      00:00          7.0           <NA>                  3                       NA          <NA>
5      00:00          5.8           <NA>                  3                       NA          <NA>
6      00:00          8.0           <NA>                  3                       NA          <NA>
  Qualifier...2 Qualifier...3 Qualifier...4 Qualifier...5 Qualifier...6 Qualifier...7 Qualifier...8
1          <NA>          <NA>            NA            NA            NA            NA            NA
2          <NA>          <NA>            NA            NA            NA            NA            NA
3          <NA>          <NA>            NA            NA            NA            NA            NA
4          <NA>          <NA>            NA            NA            NA            NA            NA
5          <NA>          <NA>            NA            NA            NA            NA            NA
6          <NA>          <NA>            NA            NA            NA            NA            NA
  Qualifier...9 Qualifier...10 Alternate.Method.Detectable.Limit Uncertainty
1            NA             NA                                NA          NA
2            NA             NA                                NA          NA
3            NA             NA                                NA          NA
4            NA             NA                                NA          NA
5            NA             NA                                NA          NA
6            NA             NA                                NA          NA
```
Now, lets grab the pm2.5 values from here.
```
> x1<- pm1$Sample.Value
> head(x1)
[1] 6.7 9.0 6.5 7.0 5.8 8.0
```
Now, lets have a quick view on data on 199 and 2012 by viewing the summary.
```
> summary(x0)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
   0.00    7.20   11.50   13.74   17.90  157.10   13217 
> summary(x1)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
 -10.00    4.00    7.63    9.14   12.00  908.97   73133 
 ```
 So, we can see the meadiam has plummeted to 7.63 in 2012. It's a good news. Lets visualize some data.
```
> boxplot(x0,x1)
```
![text](https://github.com/khaledhasanzami/Data-Analysis-Case-Study-Changes-in-Fine-Particule-Air-Pollution-in-the-U.S./blob/master/Rplot.png)

The plot is kind of messy right now. Because data is kind of skewed. Lets fix this boxplot using log.
```
> boxplot(log10(x0),log10(x1))
```

![text](https://github.com/khaledhasanzami/Data-Analysis-Case-Study-Changes-in-Fine-Particule-Air-Pollution-in-the-U.S./blob/master/Rplot01.png)
Here, we can say that, average levl has gone down but the spread has increased. 

Data is coolected in a way that, a sucker is used to suck the air and a mask collects the dust in the air. Mask collected dust is counted to measesure how much data was in there. 

