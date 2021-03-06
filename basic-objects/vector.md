

# Vector

A vector is a group of primitive values of the same type. It can be a group of numbers, true/false values, texts, and values of some other type. It is one of the building blocks of all R objects. 

There are several types of vectors in R. They distinct from each other in the type of entries they hold. Here we will see the most commonly used types of vectors including numeric vector, logical vector, character vector, and so on.


## Numeric vector

There are multiple ways to define a numeric vector.

A scalar number is the simplest numeric vector. It's special only because its length is one.


```r
> 1.5
```

```
[1] 1.5
```

To assign this value to a symbol, we can use `<-`.


```r
> x <- 1.5
```

Then the value is assigned to symbol `x` and we can use `x` to represent the value in later expressions.


```r
> x
```

```
[1] 1.5
```

We can call `numeric` function to create a zero numeric vector of a specific length.


```r
> numeric(10)
```

```
 [1] 0 0 0 0 0 0 0 0 0 0
```

We can also use `c` function to *combine* several vectors to be one vector.


```r
> c(1,2,3,4,5)
```

```
[1] 1 2 3 4 5
```

For example, we can combine several single-entry vectors with a multi-entry vector to obtain the previous vector.


```r
> c(1,2,c(3,4,5))
```

```
[1] 1 2 3 4 5
```

To define a series of consecutive numbers with step one, `:` operator will do the trick.


```r
> 1:5
```

```
[1] 1 2 3 4 5
```

A more general way to produce an integer sequence is to use `seq` function. For example, the following code produces a sequence from 1 to 10 with step 2.


```r
> seq(1,10,2)
```

```
[1] 1 3 5 7 9
```

A function like `seq` has many arguments. We can call a function by supplying all the arguments but it is in most cases not necessary. Most functions provide reasonable default values for some arguments, which makes it easier for us to call a function. In this case we only need to specify the argument we would like to modify from its default value.

For example, we can create another vector that starts from 3 with length 10 by specifying `length.out` argument.


```r
> seq(3,length.out = 10)
```

```
 [1]  3  4  5  6  7  8  9 10 11 12
```

A function call like the above uses named argument `length.out` so that other arguments are kept default and only this argument is modified.

There are many ways we can define numeric vectors, but we should always be careful when we use `:` to define a range of numbers.


```r
> 1+1:5
```

```
[1] 2 3 4 5 6
```

As the result shows, `1+1:5` does not mean a sequence from 2 to 5, but from 2 to 6. It is because `:` has higher priority than `+`, which results in evaluating `1:5` first and adding 1 to each entry, yielding the sequence you see in the result.

## Logical vector

In contrast with numeric vectors, a logical vector typically holds a group of `TRUE` or `FALSE` values. They are basically *yes* or *no* to denote the answers to a group of logical questions.

The simplest logical vector is `TRUE` or `FALSE` itself.


```r
> TRUE
```

```
[1] TRUE
```

A more usual way to obtain a logical vector is to ask logical questions about R objects. For example, we can ask R whether 1 is greater than 2.


```r
> 1 > 2
```

```
[1] FALSE
```

Its answer is correct. If we want to perform multiple comparisons at the same time, we can directly use numeric vectors.


```r
> c(1,2) > 2
```

```
[1] FALSE FALSE
```

R interprets this expression as the element-wise comparisons between the two entries.

Moreover, we can compare two multi-entry numeric vectors as long as the length of the longer vector is a multiple of that of the shorter one.


```r
> c(1,2) > c(2,1)
```

```
[1] FALSE  TRUE
```


```r
> c(2,3) > c(1,2,-1,3)
```

```
[1]  TRUE  TRUE  TRUE FALSE
```

The computing mechanism is asking the following questions iteratively: `1>2?`, `2>3?`, `-1>2?`, `3>3?`. In other words, the shorter vector will rotate to finish all the comparisons for each entry in the longer vector.

In R, several logical binary operators are defined, such as `==` to denote *equality*, `>` *greater-than*, `>=` *greater-or-equals-to*, `<` *less-than*, `<=` *less-than-or-equals-to*. Moreover, R provides some other additional logical operators like `%in%` to tell whether each entry in the left-hand side vector is contained by the right-hand side vector.


```r
> 1 %in% c(1,2,3)
```

```
[1] TRUE
```

```r
> c(1,4) %in% c(1,2,3)
```

```
[1]  TRUE FALSE
```


## Character vector

A character vector is a group of strings. Here a *character* does not mean literally a single letter or symbol in a language, but means a string like "*this is a string*".

A character vector is a group of strings. Both double-quotation mark and single-quotation mark can be used to define a character vector.


```r
> "hello, world!"
```

```
[1] "hello, world!"
```


```r
> 'hello, world!'
```

```
[1] "hello, world!"
```

We can also use combine function `c` to construct a multi-entry character vector.


```r
> c("Hello","World")
```

```
[1] "Hello" "World"
```

We can use `==` to tell whether two vectors have the same values, which applies to character vector too.


```r
> c("Hello","World") == c('Hello','World')
```

```
[1] TRUE TRUE
```

The character vectors are equal because `"` and `'` both work to define a string and do not affect its value.


```r
> c("Hello","World") == "Hello, World"
```

```
[1] FALSE FALSE
```

The previous expression yields both `FALSE` because neither `"Hello"` nor `"World"` equals `"Hello, World"`.

## Subsetting vectors

If we want to access some specific entries or a subset of a vector, we are *subsetting* the vector. Like many other operations, there are many ways to do it.

First we create a simple vector `v1`.


```r
> v1 <- c(1,2,3,4)
```

Each of the following lines gets a specific subset of `v1`.

Get the second entry:


```r
> v1[2]
```

```
[1] 2
```

Get the second to fourth entries:


```r
> v1[2:4]
```

```
[1] 2 3 4
```

Get all entries except the third one:


```r
> v1[-3]
```

```
[1] 1 2 4
```

The patterns are clear: we can put any numeric vector inside the square brackets after the vector to extract its corresponding subset.


```r
> a <- c(1,3)
> v1[a]
```

```
[1] 1 3
```

We can also supply an equal-length logical vector to determine whether each entry should be extracted.


```r
> v1[c(TRUE,FALSE,TRUE,FALSE)]
```

```
[1] 1 3
```

More than subsetting, we can overwrite a specific subset of a vector like this:


```r
> v1[2] <- 0
> v1[2:4] <- c(0,1,3)
```

Logical selector also allows overwriting.


```r
> v1[c(TRUE,FALSE,TRUE,FALSE)] <- c(3,2)
```

A useful implication of this operation is selecting entries by logical criterion. For example, this line picks out all entries that are no greater than 2.


```r
> v1[v1 <= 2]
```

```
[1] 0 2
```

This line picks out all entries that satisfy $x^2-x+1 \ge 0$.


```r
> v1[v1^2-v1+1>=0]
```

```
[1] 3 0 2 3
```

To replace all entries that satisfy $x \le 2$ with 0, we can call:


```r
> v1[v1 <= 2] <- 0
```

If we overwrite the vector at a non-existing entry, the vector will automatically expand with unassigned value kept `NA` as missing values.


```r
> v1[10] <- 8
> v1
```

```
 [1]  3  0  0  3 NA NA NA NA NA  8
```

## Named vectors

Named vector is not a specific type of vector parallel with numeric or logical vector. It is a vector with names assigned to its entries.


```r
> x <- c(a=1,b=2,c=3)
> x
```

```
a b c 
1 2 3 
```

Then we can access its entries with a single-valued character vector.


```r
> x["a"]
```

```
a 
1 
```

Or get multiple entries with a character vector


```r
> x[c("a","c")]
```

```
a c 
1 3 
```

In addition, all other operations to vector also perfectly work for named vectors.

We can get the names of a vector with `names` function.


```r
> names(x)
```

```
[1] "a" "b" "c"
```

Or we can change the names of a vector by assigning another character vector to its names.


```r
> names(x) <- c("x","y","z")
> x["z"]
```

```
z 
3 
```

Or we can simply cancel its names by assigning `NULL`.


```r
> names(x) <- NULL
> x
```

```
[1] 1 2 3
```

## Telling the type of vectors

Sometimes we need to tell the type of a vector before taking an action. `class` function will tell us the type of any R object.


```r
> class(c(1,2,3))
```

```
[1] "numeric"
```

```r
> class(c(TRUE,TRUE,FALSE))
```

```
[1] "logical"
```

```r
> class(c("Hello","World"))
```

```
[1] "character"
```

If we need to ensure an object is indeed a specific type of vector, we can use `is.numeric`, `is.logical`, `is.character` and many other similar functions.


```r
> is.numeric(c(1,2,3))
```

```
[1] TRUE
```

```r
> is.numeric(c(TRUE,TRUE,FALSE))
```

```
[1] FALSE
```

```r
> is.numeric(c("Hello","World"))
```

```
[1] FALSE
```

## Converting vectors

Different types of vectors can be coerced to a specific type of vector.


```r
> as.numeric(c("1","2","3","a"))
```

```
Warning: NAs introduced by coercion
```

```
[1]  1  2  3 NA
```

```r
> as.logical(c(-1,0,1,2))
```

```
[1]  TRUE FALSE  TRUE  TRUE
```

```r
> as.character(c(1,2,3))
```

```
[1] "1" "2" "3"
```

```r
> as.character(c(TRUE,FALSE))
```

```
[1] "TRUE"  "FALSE"
```

The conversion follows a set of rules. 

The first line converts the character vector to a numeric vector. The conversion is done except for the last one so a missing value is produced instead. 

As for converting numeric vector to logical vector, the rule is that only 0 corresponds to `FALSE` and all non-zero numbers will produce `TRUE`.

Each kind of vector can be converted to character vector since everything has a character representation. However, if a numeric vector or a logical vector is coerced to character vector, it cannot be directly involved in the arithmetic operations with other numeric or logical vectors unless it is converted back. That is why the following code does not work.


```r
> as.character(c(1,2)) + c(2,3)
```

```
Error in as.character(c(1, 2)) + c(2, 3): non-numeric argument to binary operator
```

## Arithmetic operators for numeric vectors

The arithmetic operations of numeric vectors are very simple. They basically follow two rules: Element-wise operation and rotating the shorter vector.


```r
> c(1,2,3,4) + 2
```

```
[1] 3 4 5 6
```

```r
> c(1,2,3) - c(2,3,4)
```

```
[1] -1 -1 -1
```

```r
> c(1,2,3) * c(2,3,4)
```

```
[1]  2  6 12
```

```r
> c(1,2,3) / c(2,3,4)
```

```
[1] 0.5000000 0.6666667 0.7500000
```

```r
> c(1,2,3) ^ 2
```

```
[1] 1 4 9
```

```r
> c(1,2,3) ^ c(2,3,4)
```

```
[1]  1  8 81
```

```r
> c(1,2,3,14) %% 2
```

```
[1] 1 0 1 0
```

The operations do not function with corresponding names. Only the names of the left-hand side vector will remain.


```r
> c(a=1,b=2,c=3) + c(b=2,c=3,d=4)
```

```
a b c 
3 5 7 
```

```r
> c(a=1,b=2,3) + c(b=2,c=3,d=4)
```

```
a b   
3 5 7 
```

