# vapply and tapply

vapply() and tapply(), each of which serves a very specific purpose within the Split-Apply-Combine methodology. For consistency, we'll use the same dataset we used in the 'lapply and sapply' lesson.

We will start with data stored in a variable called flags. We see what is inside it.
```
> dim(flags)
[1] 194  30

> class(flags)
[1] "data.frame"

> head(flags)
            name landmass zone area population language religion bars stripes colours red
1    Afghanistan        5    1  648         16       10        2    0       3       5   1
2        Albania        3    1   29          3        6        6    0       0       3   1
3        Algeria        4    1 2388         20        8        2    2       0       3   1
4 American-Samoa        6    3    0          0        1        1    0       0       5   1
5        Andorra        3    1    0          0        6        0    3       0       3   1
6         Angola        4    2 1247          7       10        5    0       2       3   1
  green blue gold white black orange mainhue circles crosses saltires quarters sunstars
1     1    0    1     1     1      0   green       0       0        0        0        1
2     0    0    1     0     1      0     red       0       0        0        0        1
3     1    0    0     1     0      0   green       0       0        0        0        1
4     0    1    1     1     0      1    blue       0       0        0        0        0
5     0    1    1     0     0      0    gold       0       0        0        0        0
6     0    0    1     0     1      0     red       0       0        0        0        1
  crescent triangle icon animate text topleft botright
1        0        0    1       0    0   black    green
2        0        0    0       1    0     red      red
3        1        0    0       0    0   green    white
4        0        1    1       1    0    blue      red
5        0        0    0       0    0    blue      red
6        0        0    1       0    0     red    black
```

## vapply()
When given a vector, the unique() function returns a vector with all duplicate elements removed. In other words, unique() returns a vector of only the 'unique' elements. If you use sapply(flags, unique) to apply the unique function to each column of flags, you will fail to simplify the result, thus obtaining the same result as with lapplay(). (see *lapply and sapply* lesson for more info on this)

Whereas sapply() tries to 'guess' the correct format of the result, vapply() allows you to specify it explicitly. If the result doesn't match the format you specify, vapply() will throw an error, causing the operation to stop. This can prevent significant problems in your code that might be caused by getting unexpected return values from sapply().

If we try vapply(flags, unique, numeric(1)), it says that you expect each element of the result to be a numeric vector of length 1. Since this is NOT actually the case, YOU WILL GET AN ERROR.
```
> vapply(flags, unique, numeric(1))
Error in vapply(flags, unique, numeric(1)) : values must be length 1,
 but FUN(X[[1]]) result is length 194
```

sapply(flags, class) will return a character vector containing the class of each column in the dataset.
```
> sapply(flags, class)
      name   landmass       zone       area population   language   religion 
  "factor"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer" 
      bars    stripes    colours        red      green       blue       gold 
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer" 
     white      black     orange    mainhue    circles    crosses   saltires 
 "integer"  "integer"  "integer"   "factor"  "integer"  "integer"  "integer" 
  quarters   sunstars   crescent   triangle       icon    animate       text 
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer" 
   topleft   botright 
  "factor"   "factor" 
```

If we wish to be explicit about the format of the result we expect, we can use vapply(flags, class, character(1)). The 'character(1)' argument tells R that we expect the class function to return a character vector of length 1 when applied.
```
> vapply(flags, class, character(1))
      name   landmass       zone       area population   language   religion 
  "factor"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer" 
      bars    stripes    colours        red      green       blue       gold 
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer" 
     white      black     orange    mainhue    circles    crosses   saltires 
 "integer"  "integer"  "integer"   "factor"  "integer"  "integer"  "integer" 
  quarters   sunstars   crescent   triangle       icon    animate       text 
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer" 
   topleft   botright 
  "factor"   "factor" 
```

 You might think of vapply() as being 'safer' than sapply(), since it requires you to specify the format of the output in advance, instead of just allowing R to 'guess' what you wanted. In addition, vapply() may perform faster than sapply() for large datasets.


## tapply()
As a data analyst, you'll often wish to split your data up into groups based on the value of some variable, then apply a function to the members of each group. The next function we'll look at, tapply(), does exactly that.

The 'landmass' variable in our dataset takes on integer values between 1 and 6, each of which represents a different part of the world. Using table to count how many observations of each part of the world tehre are:
```
> table(flags$landmass)

 1  2  3  4  5  6 
31 17 35 52 39 20 
```

The 'animate' variable in our dataset takes the value 1 if a country's flag contains an animate image (e.g. an eagle, a tree, a human hand) and 0 otherwise.
```
> table(flags$animate)

  0   1 
155  39 
```

 If you take the arithmetic mean of a bunch of 0s and 1s, you get the proportion of 1s. Use tapply(flags$animate, flags$landmass, mean) to apply the mean function to the 'animate' variable separately for each of the six landmass
groups, thus giving us the proportion of flags containing an animate image WITHIN each landmass group.
```
> tapply(flags$animate, flags$landmass, mean)
        1         2         3         4         5         6 
0.4193548 0.1764706 0.1142857 0.1346154 0.1538462 0.3000000 
```


Similarly, we can look at a summary of population values (in round millions) for countries with and without the color red on their flag.
```
> tapply(flags$population, flags$red, summary)
$`0`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   0.00    0.00    3.00   27.63    9.00  684.00 

$`1`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    0.0     0.0     4.0    22.1    15.0  1008.0 
```

From this, the median population (in millions) for counties *without* the color red on their flag is 3.

Using the same approach to look at a summary of population values for each of the six landmasses:
```
> tapply(flags$population, flags$landmass, summary)
$`1`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   0.00    0.00    0.00   12.29    4.50  231.00 

$`2`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   0.00    1.00    6.00   15.71   15.00  119.00 

$`3`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   0.00    0.00    8.00   13.86   16.00   61.00 

$`4`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  0.000   1.000   5.000   8.788   9.750  56.000 

$`5`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   0.00    2.00   10.00   69.18   39.00 1008.00 

$`6`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   0.00    0.00    0.00   11.30    1.25  157.00 
```
From this, the maximum population (in millions) for the fourth landmass group (Africa)is 56