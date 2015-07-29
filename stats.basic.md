---
layout: default
overview: true
title: Learning Statistics Basics in R
---

#Statistics - Basic
Lets get started with some of the basic quantitative stats. These are frequency, cummulative frequency, mean, median, mode, standard deviation.

Lets pick up some data available out of the box.

{% highlight R %}
length(z)
[1] 6
> 
{% endhighlight %}


{% highlight R %}
 > library(MASS)
 > painters
                Composition Drawing Colour Expression School
 Da Udine                 10       8     16          3      A
 Da Vinci                 15      16      4         14      A
 Del Piombo                8      13     16          7      A
 Del Sarto                12      16      9          8      A
 Fr. Penni                 0      15      8          0      A
 .....
 ...
{% endhighlight %}

##Frequency Distribution
Lets find out categories in School column

{% highlight R %}
> levels(painters$School)
[1] "A" "B" "C" "D" "E" "F" "G" "H"
{% endhighlight %}

Also, checkout values stored in school, as a variable
{% highlight R %}
> painters$School
> [1] A A A A A A A A A A B B B B B B C C C C C C D D D D D D D D D D E E E E E E
[39] E F F F F G G G G G G G H H H H
{% endhighlight %}

To find occurence of all levels

{% highlight R %}
> table(painters$School)

 A  B  C  D  E  F  G  H 
10  6  6 10  7  4  7  4 
> 
{% endhighlight %}

``table`` command summarizes the levels within data.
##Relative Frequency
How much as a percentage a particular level occurs amongst all data points.

{% highlight R %}
> table(painters$School) / length(painters$School)

         A          B          C          D          E          F          G 
0.18518519 0.11111111 0.11111111 0.18518519 0.12962963 0.07407407 0.12962963 
         H 
0.07407407 
> 
{% endhighlight %}
To limit the digits in result, we can
{% highlight R %}
> options(digits=2)
> table(painters$School) / length(painters$School)

    A     B     C     D     E     F     G     H 
0.185 0.111 0.111 0.185 0.130 0.074 0.130 0.074 
> 
{% endhighlight %}

##Bar Graph
We can plot the above frequency table.

{% highlight R %}
> barplot(table(painters$School))
> #adding colors
> barplot(table(painters$School), col=c("red", "yellow"))
{% endhighlight %}

Both the graphs are given below side by side.

![bar graph](images/barplot_1.jpg)
![bar graph](images/barplot_2.jpg)

##Pie Chart
Similarly we can plot pie chart using ``pie()`` function

{% highlight R %}
> pie(table(painters$School), col=c("red", "blue"))
{% endhighlight %}
![pie chart](images/pie_1.jpg)

##Finding mean of every level (use of: tapply)
**``tapply``** can be used to apply different stats function data corresponding to every level. It is a worker provided for every category.

{% highlight R %}
> tapply(painters$Composition, painters$School, mean)
   A    B    C    D    E    F    G    H 
10.4 12.2 13.2  9.1 13.6  7.2 13.9 14.0 
> barplot(tapply(painters$Composition, painters$School, mean), col=c("red", "yellow"))
> 
{% highlight %}

![bar plot](images/barplot_3.jpg)

##Working with continous data
In above example, what we got as mean is an example of such information. Variable does not take any discrete values. Here variable is the mean and not the "Composition". For such types, how to calculate frequency distribution.

Lets use data frame ``faithful`` here

{% highlight R %}
> faithful
> head(faithful)
  eruptions waiting
1       3.6      79
2       1.8      54
3       3.3      74
4       2.3      62
{% endhighlight %}

Here both eruptions and waiting may be classified as continous data.

To find range in which the variable varies, use function **``range()``**

{% highlight R %}
> range(faithful$eruptions)
[1] 1.6 5.1
> range(faithful$waiting)
[1] 43 96
> 
{% endhighlight %}

Lets create an vector with equi-distant points between the range retrieved in previous example
{% highlight R %}
> breaks = seq(range(faithful$eruptions)[1]-0.5, range(faithful$eruptions)[2]+.5, by=0.5)
> breaks
 [1] 1.1 1.6 2.1 2.6 3.1 3.6 4.1 4.6 5.1 5.6
> 
{% endhighlight %}

One can create variable to store ``range(faithful$eruptions)[1]`` and that of upper limit, then reuse it (more readable).

Now, lets use this category sequence (vector), to split data range for eruptions, using **``cut()``**

{% highlight R %}
> eruptions.cat = cut(faithful$eruptions, breaks, right=FALSE)
> eruptions.cat
  [1] [3.6,4.1) [1.6,2.1) [3.1,3.6) [2.1,2.6) [4.1,4.6) [2.6,3.1) [4.6,5.1)
  [8] [3.6,4.1) [1.6,2.1) [4.1,4.6) [1.6,2.1) [3.6,4.1) [4.1,4.6) [1.6,2.1)
 [15] [4.6,5.1) [2.1,2.6) [1.6,2.1) [4.6,5.1) [1.6,2.1) [4.1,4.6) [1.6,2.1)
  ...
  ..
9 Levels: [1.1,1.6) [1.6,2.1) [2.1,2.6) [2.6,3.1) [3.1,3.6) ... [5.1,5.6)
> 
{% endhighlight %}

Now, every data point belongs to at least one of the 7 levels (category). Using the tapply, we can calculate the mean
{% highlight R %}
> tapply(faithful$eruptions, eruptions.cat, mean)
[1.1,1.6) [1.6,2.1) [2.1,2.6) [2.6,3.1) [3.1,3.6) [3.6,4.1) [4.1,4.6) [4.6,5.1) 
       NA       1.9       2.3       2.8       3.4       3.9       4.4       4.8 
[5.1,5.6) 
      5.1 
{% endhighlight  %}

To calculate freq??

{% highlight R %}
> cbind(table(eruptions.cat))
          [,1]
[1.1,1.6)    0
[1.6,2.1)   63
[2.1,2.6)   29
[2.6,3.1)    6
[3.1,3.6)   10
[3.6,4.1)   42
[4.1,4.6)   79
[4.6,5.1)   42
[5.1,5.6)    1
# we used here cbind to combine empty table with column representation of the output
> barplot(table(eruptions.cat), xlab="Duration minutes", ylab="Frequency", main="Faithful Eruptions")
# note here we remove cbind here, otherwise it would have created horizontal bars
# also note here additional arguments given to decorate chart
{% endhighlight %}

###Bar plot for eruptions

![bar plot](images/barplot_4.jpg)

This is equivalent to histogram available from R out of the box, using function **``hist``**

{% highlight R %}
> hist(faithful$eruptions, right=FALSE)
{% endhighlight %}

###Histogram of eruptions

![histogram](images/hist_1.jpg)

Notice here the similarity between the barplot and histogram.

###Relative Distribution
In similar fashion, we can calculate relative distribution as well, as we got eruptions.cat vector mapping to every row of eruptions.

{% highlight R %}
> table(eruptions.cat) / length(eruptions.cat)
eruptions.cat
[1.1,1.6) [1.6,2.1) [2.1,2.6) [2.6,3.1) [3.1,3.6) [3.6,4.1) [4.1,4.6) [4.6,5.1) 
   0.0000    0.2316    0.1066    0.0221    0.0368    0.1544    0.2904    0.1544 
[5.1,5.6) 
   0.0037 
> 
{% endhighlight %}

which again can be plotted. Would be similar.

### Putting things together
Lets put together eruptions, category, frequency, relative frequency

{% highlight R %}
> cbind(eruptions.cat, as.data.frame(faithful$eruptions))
> #now check if you do without coercing the data type
> cbind(eruptions.cat, faithful$eruptions)
> #this is simple matrix. In previous command, frame takes care of display factor label
> # you may check the str(), typeof() for both the results
> t1 <- cbind(eruptions.cat, as.data.frame(faithful$eruptions))
> str(t1)
'data.frame':   272 obs. of  2 variables:
 $ eruptions.cat     : Factor w/ 9 levels "[1.1,1.6)","[1.6,2.1)",..: 6 2 5 3 7 4 8 6 2 7 ...
 $ faithful$eruptions: num  3.6 1.8 3.33 2.28 4.53 ...
> typeof(t1)
[1] "list"
#note that this is of type list 
> t1 <- cbind(eruptions.cat, faithful$eruptions)
> str(t1)
 num [1:272, 1:2] 6 2 5 3 7 4 8 6 2 7 ...
 - attr(*, "dimnames")=List of 2
  ..$ : NULL
  ..$ : chr [1:2] "eruptions.cat" ""
# since this does not point to any useful information
# we can try typeof()
> typeof(t1)
> [1] "double"
{% endhighlight  %}

##Cummulative Frequency
For this, first we have to follow the old steps as :
+ Create breaks in the range including both ends of it
+ Cut data using these breaks
+ Table it to get distribution of data across these breaks

Now for cummulative, we need to do
+ use **``cumsum()``** function on the distribution table

{% highlight R %}
> cumsum(table(eruptions.cat))
[1.1,1.6) [1.6,2.1) [2.1,2.6) [2.6,3.1) [3.1,3.6) [3.6,4.1) [4.1,4.6) [4.6,5.1) 
        0        63        92        98       108       150       229       271 
[5.1,5.6) 
      272 
> 
{% endhighlight %}

### Lets plot the line graph

{% highlight R %}
g = c(0, cumsum(table(eruptions.cat)))
plot(breaks, g)
> lines(breaks, g)
{% endhighlight %}

Line graph
![line graph](images/line_1.jpg)

### Cummulative frequency using ``ecdf()``

{% highlight R %}
> f = ecdf(faithful$eruptions)
> plot(f)
{% endhighlight %}

Plot using interpolating function

![Interpolated graph](images/plot_1.jpg)

##Scatter Plot
It is same as ``plot()``. Lets do this between two dimensions - waiting, eruptions.

{% highlight R %}
plot(faithful$eruptions, faithful$waiting)
{% endhighlight %}

**Scatter plot graph**
![scatter plot](images/plot_2.jpg)
