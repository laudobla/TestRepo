# Looking at Data

## class()
Let's start with an already defined dataframe called plants. To see its class:
```
> class(plants)
[1] "data.frame"
```

## seeing its dimensions
We can see the size of a data frame with these functions
```
> dim(plants)
[1] 5166   10

> nrow(plants)
[1] 5166

> ncol(plants)
[1] 10

> object.size(plants)
644232 bytes
```

## names()
To show the names of a dataframe
```
> names(plants)
 [1] "Scientific_Name"      "Duration"             "Active_Growth_Period"
 [4] "Foliage_Color"        "pH_Min"               "pH_Max"              
 [7] "Precip_Min"           "Precip_Max"           "Shade_Tolerance"
[10] "Temp_Min_F"
```

## head()
To take a peek of the first rows. By default, it shows only the first 6 rows:
```
> head(plants)
               Scientific_Name          Duration Active_Growth_Period Foliage_Color pH_Min
1                  Abelmoschus              <NA>                 <NA>          <NA>     NA
2       Abelmoschus esculentus Annual, Perennial                 <NA>          <NA>     NA
3                        Abies              <NA>                 <NA>          <NA>     NA
4               Abies balsamea         Perennial    Spring and Summer         Green      4
5 Abies balsamea var. balsamea         Perennial                 <NA>          <NA>     NA
6                     Abutilon              <NA>                 <NA>          <NA>     NA
  pH_Max Precip_Min Precip_Max Shade_Tolerance Temp_Min_F
1     NA         NA         NA            <NA>         NA
2     NA         NA         NA            <NA>         NA
3     NA         NA         NA            <NA>         NA
4      6         13         60        Tolerant        -43
5     NA         NA         NA            <NA>         NA
6     NA         NA         NA            <NA>         NA
```

To show a different number of observations
```
> head(plants,3)
                     Scientific_Name          Duration Active_Growth_Period Foliage_Color
1                        Abelmoschus              <NA>                 <NA>          <NA>
2             Abelmoschus esculentus Annual, Perennial                 <NA>          <NA>
3                              Abies              <NA>                 <NA>          <NA>

   pH_Min pH_Max Precip_Min Precip_Max Shade_Tolerance Temp_Min_F
1      NA     NA         NA         NA            <NA>         NA
2      NA     NA         NA         NA            <NA>         NA
3      NA     NA         NA         NA            <NA>         NA
```

## tail()
To take a peek of the last rows. By default, it shows only the last 6 rows:
```
> tail(plants)
      Scientific_Name  Duration Active_Growth_Period Foliage_Color pH_Min pH_Max Precip_Min
5161      Zizia aurea Perennial                 <NA>          <NA>     NA     NA         NA
5162 Zizia trifoliata Perennial                 <NA>          <NA>     NA     NA         NA
5163          Zostera      <NA>                 <NA>          <NA>     NA     NA         NA
5164   Zostera marina Perennial                 <NA>          <NA>     NA     NA         NA
5165           Zoysia      <NA>                 <NA>          <NA>     NA     NA         NA
5166  Zoysia japonica Perennial                 <NA>          <NA>     NA     NA         NA
     Precip_Max Shade_Tolerance Temp_Min_F
5161         NA            <NA>         NA
5162         NA            <NA>         NA
5163         NA            <NA>         NA
5164         NA            <NA>         NA
5165         NA            <NA>         NA
5166         NA            <NA>         NA
```

## summary()
It provides different output for each variable, depending on its class. For numeric data such as Precip_Min, summary() displays the minimum, 1st quartile, median, mean, 3rd quartile, and maximum. These values help us understand how the data are distributed.
For categorical variables (called 'factor' variables in R), summary() displays the number of times each value (or 'level') occurs in the data.
```
> summary(plants)
                     Scientific_Name              Duration   
 Abelmoschus                 :   1   Perennial        :3031  
 Abelmoschus esculentus      :   1   Annual           : 682  
 Abies                       :   1   Annual, Perennial: 179  
 Abies balsamea              :   1   Annual, Biennial :  95  
 Abies balsamea var. balsamea:   1   Biennial         :  57  
 Abutilon                    :   1   (Other)          :  92  
 (Other)                     :5160   NA's             :1030  
           Active_Growth_Period      Foliage_Color      pH_Min          pH_Max      
 Spring and Summer   : 447      Dark Green  :  82   Min.   :3.000   Min.   : 5.100  
 Spring              : 144      Gray-Green  :  25   1st Qu.:4.500   1st Qu.: 7.000  
 Spring, Summer, Fall:  95      Green       : 692   Median :5.000   Median : 7.300  
 Summer              :  92      Red         :   4   Mean   :4.997   Mean   : 7.344  
 Summer and Fall     :  24      White-Gray  :   9   3rd Qu.:5.500   3rd Qu.: 7.800  
 (Other)             :  30      Yellow-Green:  20   Max.   :7.000   Max.   :10.000  
 NA's                :4334      NA's        :4334   NA's   :4327    NA's   :4327    
   Precip_Min      Precip_Max         Shade_Tolerance   Temp_Min_F    
 Min.   : 4.00   Min.   : 16.00   Intermediate: 242   Min.   :-79.00  
 1st Qu.:16.75   1st Qu.: 55.00   Intolerant  : 349   1st Qu.:-38.00  
 Median :28.00   Median : 60.00   Tolerant    : 246   Median :-33.00  
 Mean   :25.57   Mean   : 58.73   NA's        :4329   Mean   :-22.53  
 3rd Qu.:32.00   3rd Qu.: 60.00                       3rd Qu.:-18.00  
 Max.   :60.00   Max.   :200.00                       Max.   : 52.00  
 NA's   :4338    NA's   :4338                         NA's   :4328    
```

## table()
R truncates the summary for Active_Growth_Period by including a catch-all category called 'Other'. Since it is a categorical/factor variable, we can see how many times each value actually occurs in the data with the function table()
```
> table(plants$Active_Growth_Period)

Fall, Winter and Spring                  Spring         Spring and Fall 
                     15                     144                      10 
      Spring and Summer    Spring, Summer, Fall                  Summer 
                    447                      95                      92 
        Summer and Fall              Year Round 
                     24                       5 
```

## str()
str() combines many of the features of the other functions
in a concise and readable format. At the very top, it tells us that the class of plants is 'data.frame' and that it has 5166 observations and 10 variables. It then gives us the name and class of each variable, as well as a preview of its contents.

It is a very general function that you can use on most objects in R. Any time you want to understand the structure of something (a dataset, function, etc.), str() is a good place to start.

```
> str(plants)
'data.frame':	5166 obs. of  10 variables:
 $ Scientific_Name     : Factor w/ 5166 levels "Abelmoschus",..: 1 2 3 4 5 6 7 8 9 10 ...
 $ Duration            : Factor w/ 8 levels "Annual","Annual, Biennial",..: NA 4 NA 7 7 NA 1 NA 7 7 ...
 $ Active_Growth_Period: Factor w/ 8 levels "Fall, Winter and Spring",..: NA NA NA 4 NA NA NA NA 4 NA ...
 $ Foliage_Color       : Factor w/ 6 levels "Dark Green","Gray-Green",..: NA NA NA 3 NA NA NA NA 3 NA ...
 $ pH_Min              : num  NA NA NA 4 NA NA NA NA 7 NA ...
 $ pH_Max              : num  NA NA NA 6 NA NA NA NA 8.5 NA ...
 $ Precip_Min          : int  NA NA NA 13 NA NA NA NA 4 NA ...
 $ Precip_Max          : int  NA NA NA 60 NA NA NA NA 20 NA ...
 $ Shade_Tolerance     : Factor w/ 3 levels "Intermediate",..: NA NA NA 3 NA NA NA NA 2 NA ...
 $ Temp_Min_F          : int  NA NA NA -43 NA NA NA NA -13 NA ...
```








