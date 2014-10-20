# Basic Building Blocks 

## To create a vector
Use function c()
```
> z <- c(1.1, 9, 3.14)
> z
[1] 1.10 9.00 3.14
```

A vector can contain vectors inside
```
> c(z,555,z)
[1]   1.10   9.00   3.14 555.00   1.10   9.00   3.14
```

Numeric vectors can be used in arithmetic expressions.
```
> z * 2 + 100
[1] 102.20 118.00 106.28
 ```

## Power and sqrt()
Where x^2 means 'x squared'.
```
> z^2
[1]  1.2100 81.0000  9.8596

> sqrt(z)
[1] 1.048809 3.000000 1.772005
```

## Operations with vectors
Con numbers
```
> x <- c(10,20,30)

> x + 5
[1] 15 25 35

> x / 5
[1] 2 4 6

> x ^ 2
[1] 100 400 900
```

With same sized vectors
```
> x <- c(10,20,30)
> y <- c(1,2,3)

> x + y
[1] 11 22 33

> x / y
[1] 10 10 10
```

With different sized vectors that dive evenly:
```
> c(1, 2, 3, 4) + c(0, 10)
[1]  1 12  3 14
```

With different sized vectors that not dived evenly R will still apply the 'recycling' method, but will throw a warning to let you know something fishy might be going on:
```
> c(1, 2, 3, 4) + c(0, 10, 100)
[1]   1  12 103   4
Warning message:
In c(1, 2, 3, 4) + c(0, 10, 100) :
  longer object length is not a multiple of shorter object length
```
