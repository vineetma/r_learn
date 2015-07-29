---
layout: default
overview: true
title: Learning Vectors in R
---
#Data types in R-Language

Like any other language, R also provides with following data types:

+ Numeric (something similar to float)
+ Integer
+ Character (same as string and array of string)
+ Logical (same as boolean)
+ Complex (as we studied in school, a + ib)
+ Factors
+ List

#Assignments of variables

There are two types:
+ One is the direct assignment, may also be called as primitives

```
x = 34
```

Such assignments always make numeric variable.
To check variable type, just write
class(x)

```
x = as.integer(3.4)
```

This will make 3.4 explicitly being treated as integer, therefore, .4 will be truncated

```
x = "Vineet Maheshwari"
```

Assigns character (or string in regular language)

One can coerce a variable into other type, typically required between integers and float. It can be done by:

```
x = 4
y = as.integer(x)
class(x)
class(y)
```

+ Another one is using the vector and making the variables it's components (or members in routine language). 'c' is the function call used, i understand, refers to "component", nevertheless, it is good to settle question on what "c" stands for.

```
x = c(23,TRUE, "Vineet")
class(x)
x
```


Note in the output of above following:

a. class outputs again type as "character"

b. x has coerced all components to "character"

#Playing with vectors

## Combining them

We can combine them just like we created vector.

```
x = "Vineet"
y = c("Maheshwari", ",", 5.6, ",Gurgaon")
z = c(x, " ", y)
z

[1] "Vineet"     " "          "Maheshwari" ","          "5.6"       
[6] ",Gurgaon"
> 
```

You can measure the length of this vector to verify
```
length(z)
[1] 6
> 
```

Checkout coercion once again
```
> a = c(1,2,3)
> a
[1] 1 2 3
> b = c(a, "Vineet")
> b
[1] "1"      "2"      "3"      "Vineet"
```
Note here the way integer array is converted to array of strings. This means, R wants all members to be of same type

## Doing some maths
Same symbols ``+``, ``-``, ``*``, ``/`` are used to perform maths. However, if we operate to a vector, it follows following rules:
+ if it is single item, than it is operated upon all the members/components
+ if it is again a vector than it adds index by index
+ if it is unequal in size, than the elements from smaller one are reused
```
> a = c(1,2,3)
> a
[1] 1 2 3
> a + 2
[1] 3 4 5
> 
> b = c(3,3,10)
> b
> [1]  3  3 10
> a
[1] 1 2 3
> b+a
[1]  4  5 13
> b
[1]  3  3 10
> c = c(12,13)
> b+c
[1] 15 16 22
Warning message:
In b + c : longer object length is not a multiple of shorter object length
> 
```

Note 12 is added again to 10. This is also known as recycling.

##Accessing the members
Like arrays in C, one can do the same here. Also, it has adopted the convenience displayed in other languages like PHP, Python

```
> b
[1]  3  3 10
> b[3]
> 10
> 
```

Note that 0 is special index. It contains the type of the vector, in this case it is numeric.

Use can access members with pair of integer indexes separated by ``:``
```
> a
[1] 1 2 3
> a[2:3]
[1] 2 3
> 
```
###New ways
#### Use Negative Index
here is use of -ve index. It removes that indexed member which is stated like this.
```
> b[-2]
[1]  3 10
> 
```
Note: 2nd component removed.

#### Use list of indexes
Another one, instead of integer index, give another vector, with list of integer indexes. These index values can repeat. R shall return whatever is rquested from here.
```
> s = c("Ram", "Venkat", "Shree")
> s[c(1,1,1)]
[1] "Ram" "Ram" "Ram"
```

#### Use list of logical values
It is like a switch, placed on top of all members in given vector. If it is "True", i.e. "On", it will show up in final outcome, else not.
```
> a
[1] 1 2 3
> a[c(TRUE,FALSE,FALSE)]
[1] 1
>
```

#### Labelling vector members
Use ``names()`` function to create another array of labels for the given vector. Usage is as:
```
> person1 = c("Vineet", "Maheshwari", 5.5, "Gurgaon")
> names(person1) = c("First Name", "Last Name", "Height", "City")
> person1
  First Name    Last Name       Height         City 
    "Vineet" "Maheshwari"        "5.5"    "Gurgaon" 
> 
```
Note here, the function being used is on the LHS, with argument as the target vector.

