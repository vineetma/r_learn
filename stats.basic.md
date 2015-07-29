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

