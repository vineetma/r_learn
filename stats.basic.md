---
layout: default
overview: true
title: Learning Statistics Basics in R
---

#Statistics - Basic
Lets get started with some of the basic quantitative stats. These are frequency, cummulative frequency, mean, median, mode, standard deviation.

Lets pick up some data available out of the box.

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
{% endhighlight %}

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
