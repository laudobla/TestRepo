# Vectors

## Filling a vector with random numbers
Creating a vector containing 10 draws from a standard normal distribution
```
> y <- rnorm(10)
> y
[1] -0.57935818 -0.36375595 -0.35751602 -0.33473711 -0.30893615 -0.59938428 -0.38637783
[8] -0.57089700  0.59948705 -0.08282902
```

## Filling a vector with repeated values
#### rep()
To create a vector with a repited value
```
> rep(0, times= 10)
 [1] 0 0 0 0 0 0 0 0 0 0
```
It works not only with values:
```
> rep( c(0,1,2), times= 10)
 [1] 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2
```
Otra opción interesante
```
> rep(c(0, 1, 2), each = 10)
 [1] 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2
```

## Logical vectors
Comparisons
```
> num_vect <- c(0.5, 55, -10, 6)

> tf <- num_vect < 1
> tf
[1]  TRUE FALSE  TRUE FALSE

> tf <- num_vect != 55
> tf
[1]  TRUE FALSE  TRUE  TRUE
```

## Character vectors
 ```
> my_char <- c("My", "name", "is")

> my_char
[1] "My"   "name" "is"
```


To concatenate:
```
> my_char
[1] "My"   "name" "is"

> my_name <- c(my_char, "Laura")

> my_name
[1] "My"    "name"  "is"    "Laura"

> paste(my_name, collapse = " ")
[1] "My name is Laura"
```

Using paste():
```
> my_char <- c("My", "name", "is")

> paste(my_char, collapse = " ")
[1] "My name is"

> paste("Hello", "world!", sep = " ")
[1] "Hello world!"

> paste(1:3, c("X", "Y", "Z"), sep = "")
[1] "1X" "2Y" "3Z"
```

Pasting vectors of different length
(*LETTERS* is a predefined variable in R containing a character vector of all 26 letters in the English alphabet)
```
> paste(LETTERS, 1:4, sep = "-")
 [1] "A-1" "B-2" "C-3" "D-4" "E-1" "F-2" "G-3" "H-4" "I-1" "J-2" "K-3" "L-4" "M-1" "N-2"
[15] "O-3" "P-4" "Q-1" "R-2" "S-3" "T-4" "U-1" "V-2" "W-3" "X-4" "Y-1" "Z-2"
```
