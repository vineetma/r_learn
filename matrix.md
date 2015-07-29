#Matrix
Recall, school days, when we used to multiply vector and get confused between rows and columns. It has been an hit question during programming interviews as well. Here is the language that has this capability built in. It is about 2-dimensional organization of members. Kind of vector with added dimension.

We shall used vector learned so far to create them.

```
> b = c(23,12,14,20)
> b2 = c(12, 10, 9, 15)
> myt = matrix(c(b, b2), nrow=2, ncol=4, byrow=TRUE)
> myt
     [,1] [,2] [,3] [,4]
[1,]   23   12   14   20
[2,]   12   10    9   15
```

Now, we can use additional dimension, which was not valid while using with vectors. For example:
```
> myt[1,3]
[1] 14
> 
```

With partial index, we can view all elements in a particular row, or all in that of a column.
```
> myt[1,]
[1] 23 12 14 20
> 
```
all elements of row ``1``

```
> myt[,2]
[1] 12 10
> 
```
all elements in column ``2``

Just like we did in vectors, we can use vectors in place of single index values to access members. By doing so, we can access multiple members.
```
> myt[,c(2,4)]
     [,1] [,2]
[1,]   12   20
[2,]   10   15
> 
```

##Giving names to dimensions
Vector naming concept is further extended here. Here instead of ``names``, ``dimnames`` is used. Checkout the usage here:
```
> vineet = c("Vineet", "Maheshwari", 5.5, "Gurgaon")
> rakesh = c("Rakesh", "Sharma", 6.0, "Gurgaon")
> team = matrix(c(vineet, rakesh), nrow=2, ncol=4, byrow=TRUE)
> team
     [,1]     [,2]         [,3]  [,4]     
[1,] "Vineet" "Maheshwari" "5.5" "Gurgaon"
[2,] "Rakesh" "Sharma"     "6"   "Gurgaon"
> dimnames(team) = list(c("Vineet", "Rakesh"), 
+ c("First Name", "Last Name", "Height", "City"))
> team
       First Name Last Name    Height City     
Vineet "Vineet"   "Maheshwari" "5.5"  "Gurgaon"
Rakesh "Rakesh"   "Sharma"     "6"    "Gurgaon"
> 
```
Now we can access members using names. Example..
```
> team[,c("Height","City")]
       Height City     
Vineet "5.5"  "Gurgaon"
Rakesh "6"    "Gurgaon"
> 
```
## Playing with Matrix, basic operations
### Transposing
It is very simple, just invoke function ``t()``. Exmaple:
```
> t(team)
           Vineet       Rakesh   
First Name "Vineet"     "Rakesh" 
Last Name  "Maheshwari" "Sharma" 
Height     "5.5"        "6"      
City       "Gurgaon"    "Gurgaon"
> 
```
### Adding
It is as simple as adding numbers:
```
> a = c(1,2,3,4)
> b = c(4,3,2,1)
> a = matrix(a, nrow=2, ncol=2)
> b = matrix(b, nrow=2, ncol=2)
> a
     [,1] [,2]
[1,]    1    3
[2,]    2    4
> b
     [,1] [,2]
[1,]    4    2
[2,]    3    1
> a+b
     [,1] [,2]
[1,]    5    5
[2,]    5    5
> 
```
### Multiplication
This is interesting. It is not done the way we have been taught. It multiplies element by element and creates new matrix. Example:
```
> a*b
     [,1] [,2]
[1,]    4    6
[2,]    6    4
> 
```

Ideally it should have been
```
13   5
20  30
```
Leaving it to the way it is implemented and will be useful to arrive at desired implementation.

### Combining
It can be done to add rows of data or to add columns of data. It can be done using two functions

+ cbind -- for column additions
+ rbind -- for row additions

Examples:
```
> gender = c("Male", "Male")
> gender = matrix(gender, nrow=2, ncol=1)
> gender
     [,1]  
[1,] "Male"
[2,] "Male"
> dimnames(gender) = list(c("Vineet", "Rakesh"), c("Gender"))
> gender
       Gender
Vineet "Male"
Rakesh "Male"
> cbind(team, gender)
       First Name Last Name    Height City      Gender
Vineet "Vineet"   "Maheshwari" "5.5"  "Gurgaon" "Male"
Rakesh "Rakesh"   "Sharma"     "6"    "Gurgaon" "Male"
> 
```

It would be interesting to see if we would have kept the row labels for gender out of order, would R have sorted it correctly?
### Converting back to vector single dimension
Just do ``c(matrix)``. Example
```
> c(team)
[1] "Vineet"     "Rakesh"     "Maheshwari" "Sharma"     "5.5"       
[6] "6"          "Gurgaon"    "Gurgaon"   
> 
```

