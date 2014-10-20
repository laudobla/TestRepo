# Missing values

## Operations with missing values
Any operation involving NA generally yields NA as the result.
```
> x <- c(44, NA, 5, NA)

> x * 3
[1] 132  NA  15  NA
```

## An experiment with NAs
Creating a vector containing 1000 draws from a standard normal distribution
```
 > y <- rnorm(1000)
```
Then we create a vector containing 1000 NAs
```
> z <- rep(NA, 1000)
```
Finally, we select 100 elements at random from these 2000 values (combining y and z) such that we don't know how many NAs we'll wind up with or what positions they'll have
```
> my_data <- sample(c(y, z), 100)

> my_na <- is.na(my_data)
> my_na
  [1]  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE
 [15]  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE
 [29]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE FALSE  TRUE FALSE  TRUE
 [43]  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE FALSE
 [57] FALSE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
 [71]  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE
 [85]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE
 [99]  TRUE  TRUE
```



*my_na* has a TRUE for every
| NA and FALSE for every numeric value, we can compute the total number of NAs in our data.



## Option seq()
Used to a sequence from a to b

```
> seq(1,20)

 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
```

Used to a sequence in increments other than 1:
```
 > seq(0,10, by=0.5)
 [1]  0.0  0.5  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5  7.0  7.5  8.0
[18]  8.5  9.0  9.5 10.0
```

Used to a sequence from a to b divided in a size:
```
> seq(5, 10, length=30)
 [1]  5.000000  5.172414  5.344828  5.517241  5.689655  5.862069  6.034483  6.206897
 [9]  6.379310  6.551724  6.724138  6.896552  7.068966  7.241379  7.413793  7.586207
[17]  7.758621  7.931034  8.103448  8.275862  8.448276  8.620690  8.793103  8.965517
[25]  9.137931  9.310345  9.482759  9.655172  9.827586 10.000000
```

An experiment:
```
> my_seq<-seq(5, 10, length=30)

> length(my_seq)
[1] 30

> 1:length(my_seq)
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
[30] 30
```

A sequence in increments of 1 to the size of a vector
```
> seq(along.with = my_seq)
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
[30] 30
```

## Option seq_along()
A stablished function for doing the last thing
```
> seq_along(my_seq)
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
[30] 30
```

## rep()
To create a vector with a repited value
```
> rep(0, times= 40)
 [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
```
It works not only with values:
```
> rep( c(0,1,2), times= 10)
 [1] 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2

> rep(c(0, 1, 2), each = 10)
 [1] 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2
```
