# Matrices and Data Frames

Let's start with a vextor:
```
> my_vector<-1:20
> my_vector
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
```

## length()
```
> length(my_vector)
[1] 20
```

## Using dim() to convert a vector into a matrix
For the fucntion dim() the first number is the number of rows and the second is the number of columns
```
> dim(my_vector) <- c(4, 5)
> dim(my_vector)
[1] 4 5

> attributes(my_vector)
$dim
[1] 4 5

> my_vector
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    5    9   13   17
[2,]    2    6   10   14   18
[3,]    3    7   11   15   19
[4,]    4    8   12   16   20

> class(my_vector)
[1] "matrix"
```

## matrix()
Then, to take out all the NAs:
```
> my_matrix2 <- matrix(data = 1:20 , nrow=4, ncol=5)
> my_matrix2
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    5    9   13   17
[2,]    2    6   10   14   18
[3,]    3    7   11   15   19
[4,]    4    8   12   16   20
```

## Adding names to a matrix
Using cbind(). Matrices can only contain ONE class of data, so everything will be converted to text (implicit coercion).
```
> patients <- c("Bill", "Gina", "Kelly", "Sean")
> cbind(patients,my_matrix)
     patients                       
[1,] "Bill"   "1" "5" "9"  "13" "17"
[2,] "Gina"   "2" "6" "10" "14" "18"
[3,] "Kelly"  "3" "7" "11" "15" "19"
[4,] "Sean"   "4" "8" "12" "16" "20"
```

## Dataframes
To add this name and keep the integers, we can use Dataframes
```
> my_data <- data.frame(patients, my_matrix)
> my_data
  patients X1 X2 X3 X4 X5
1     Bill  1  5  9 13 17
2     Gina  2  6 10 14 18
3    Kelly  3  7 11 15 19
4     Sean  4  8 12 16 20

> class(my_data)
[1] "data.frame"
```

Adding the names to the columns of the dataset
```
> cnames<- c("patient", "age", "weight", "bp", "rating", "test")

> colnames(my_data) <- cnames

> my_data
  patient age weight bp rating test
1    Bill   1      5  9     13   17
2    Gina   2      6 10     14   18
3   Kelly   3      7 11     15   19
4    Sean   4      8 12     16   20
```

```
```