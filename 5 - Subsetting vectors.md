# Subsetting vectors

Let's start with a vextor x:
```
> x
 [1]  1.0428869 -1.0260351         NA         NA  2.2039688  0.6416555  1.1068159         NA
 [9]  0.4944852 -0.4234192         NA -0.6139127         NA -0.1045116         NA         NA
[17]  0.9135576 -0.7034776  1.0019940 -1.0478699         NA         NA -2.5261136         NA
[25]         NA         NA         NA  0.5367543         NA  0.3534117         NA         NA
[33]         NA  0.2460981         NA  0.5827928         NA         NA  0.3489496 -1.8315955
```

## Indexing using []

```
> x[1:10]
 [1]  1.0428869 -1.0260351         NA         NA  2.2039688  0.6416555  1.1068159         NA
 [9]  0.4944852 -0.4234192
```

## Indexing with logical vectors
First, we create the logical vector. For instance, is.na() to get out all the NAs
```
> is.na(x)
 [1] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE  TRUE FALSE
[15]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE FALSE
[29]  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE FALSE FALSE
```

Then, to take out all the NAs:
```
> x[is.na(x)]
 [1] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA

> y <- x[!is.na(x)]
> y
 [1]  1.0428869 -1.0260351  2.2039688  0.6416555  1.1068159  0.4944852 -0.4234192 -0.6139127
 [9] -0.1045116  0.9135576 -0.7034776  1.0019940 -1.0478699 -2.5261136  0.5367543  0.3534117
[17]  0.2460981  0.5827928  0.3489496 -1.8315955
```

To get all the positive values of a vector:
```
> y[y > 0]
 [1] 1.0428869 2.2039688 0.6416555 1.1068159 0.4944852 0.9135576 1.0019940 0.5367543
 [9] 0.3534117 0.2460981 0.5827928 0.3489496
```

The same excercise with missing values:
```
> x[x > 0]
 [1] 1.0428869        NA        NA 2.2039688 0.6416555 1.1068159        NA 0.4944852
 [9]        NA        NA        NA        NA 0.9135576 1.0019940        NA        NA
[17]        NA        NA        NA        NA 0.5367543        NA 0.3534117        NA
[25]        NA        NA 0.2460981        NA 0.5827928        NA        NA 0.3489496
```

To exclude both missing and negative values:
```
> x[!is.na(x) & x > 0]
 [1] 1.0428869 2.2039688 0.6416555 1.1068159 0.4944852 0.9135576 1.0019940 0.5367543
 [9] 0.3534117 0.2460981 0.5827928 0.3489496
```


## Indexing using c()

To subset the 3rd, 5th, and 7th elements of x:
```
> x[c(3,5,7)]
[1]       NA 2.203969 1.106816
```

Using negative values: R gives us all elements of x EXCEPT for the negative ones:
```
> x[c(-2, -10)]
 [1]  1.0428869         NA         NA  2.2039688  0.6416555  1.1068159         NA  0.4944852
 [9]         NA -0.6139127         NA -0.1045116         NA         NA  0.9135576 -0.7034776
[17]  1.0019940 -1.0478699         NA         NA -2.5261136         NA         NA         NA
[25]         NA  0.5367543         NA  0.3534117         NA         NA         NA  0.2460981
[33]         NA  0.5827928         NA         NA  0.3489496 -1.8315955
```

A shorter way to do this is to put the negative sign outside the c() function:
```
> x[-c(2, 10)]
 [1]  1.0428869         NA         NA  2.2039688  0.6416555  1.1068159         NA  0.4944852
 [9]         NA -0.6139127         NA -0.1045116         NA         NA  0.9135576 -0.7034776
[17]  1.0019940 -1.0478699         NA         NA -2.5261136         NA         NA         NA
[25]         NA  0.5367543         NA  0.3534117         NA         NA         NA  0.2460981
[33]         NA  0.5827928         NA         NA  0.3489496 -1.8315955
```


## Indexing using Named Elements

First we create a vector with named elements:
```
> vect <- c(foo = 11, bar = 2, norf= NA)
> vect
 foo  bar norf
  11    2   NA

## Another way:
> names(vect) <- c("foo", "bar", "norf")
> names(vect)
[1] "foo"  "bar"  "norf"
```

Now, to obtain an element by name:
```
> vect["bar"]
bar
  2
```

We also can specify a vector of names with c():
```
> vect[c("foo", "bar")]
foo bar
 11   2
```