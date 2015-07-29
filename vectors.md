#Data types in R-Language

Like any other language, R also provides with following data types:

+ Numeric (something similar to float)
+ Integer
+ Character (same as string and array of string)
+ Logical (same as boolean)

#Assignments of variables

There are two types:
+ One is the direct assignment, may also be called as primitives

``
x = 34
``

Such assignments always make numeric variable.
To check variable type, just write
class(x)

``
x = as.integer(3.4)
``

This will make 3.4 explicitly being treated as integer, therefore, .4 will be truncated

``
x = "Vineet Maheshwari"
``

Assigns character (or string in regular language)

One can coerce a variable into other type, typically required between integers and float. It can be done by:

``
x = 4
y = as.integer(x)
class(x)
class(y)
``

+ Another one is using the vector and making the variables it's components (or members in routine language). 'c' is the function call used, i understand, refers to "component", nevertheless, it is good to settle question on what "c" stands for.

``
x = c(23,TRUE, "Vineet")
class(x)
x
``

Note in the output of above following:
 + class outputs again type as "character"
 + x has coerced all components to "character"


