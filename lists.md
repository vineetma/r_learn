---
layout: default
overview: true
title: Learning Lists in R
---

#Lists
Lists are very much similar to associative arrays. It comes very close in similarity to a PHP programmer.

Lets see
##Definition
Just declare a variable using ``list()`` function. Note that list has a property to hold objects of different class/types. Lets do the same example of two students and their attributes
{% highlight R %}
>team = list(c("Vineet", "Maheshwari", 5.6, "Gurgaon"), c("Rakesh", "Sharma", 6.0, "Gurgaon"))
> team
[[1]]
[1] "Vineet"     "Maheshwari" "5.6"        "Gurgaon"   

[[2]]
[1] "Rakesh"  "Sharma"  "6"       "Gurgaon"
> 
> 
{% endhighlight %}

Lets name them
{% highlight R %}
team = list(Vineet = c("Vineet", "Maheshwari", 5.6, "Gurgaon"), Rakesh = c("Rakesh", "Sharma", 6.0, "Gurgaon"))
> team
$Vineet
[1] "Vineet"     "Maheshwari" "5.6"        "Gurgaon"   

$Rakesh
[1] "Rakesh"  "Sharma"  "6"       "Gurgaon"

> 
{% endhighlight %}

Note ``[[]]`` brackets and use of ``$`` in front of the label while capturing the content of list member. These are used to access members of the list.

## Accessing them

{% highlight R %}
> team["Vineet"]
$Vineet
[1] "Vineet"     "Maheshwari" "5.6"        "Gurgaon"   

> team$Vineet
[1] "Vineet"     "Maheshwari" "5.6"        "Gurgaon"   
> 
> team[[1]]
[1] "Vineet"     "Maheshwari" "5.6"        "Gurgaon"   
>
> team[["Vineet"]]
[1] "Vineet"     "Maheshwari" "5.6"        "Gurgaon"   

{% endhighlight %}

Note here four ways to access. Use of ``$`` and Use of square brackets - both single and double.

Answer to the difference lies in following example.

{% highlight R %}
> team[1][3]
$<NA>
NULL

> team[[1]][3]
[1] "5.6"
> 
{% endhighlight %}

Note that though we can access the list member by using ``team[1]``, but we can't access the member of a member. On the other hand using ``[[]]``, we are able to access. So also, we can modify.

Lets check the type of ``team[1]``

{% highlight R %}
> class(team[1])
[1] "list"
> class(team[[1]])
[1] "character"
> 
{% endhighlight %}
It is again a list, though we had inserted a character type.

##Attach and detach with lists
This is new concept. Something similar was there in VBA, where one selects and object and there is no need to repeat that name in the enclosing block. Similarly, ``attach(team)`` shall eliminate the need for repeating ``team`` list name. After this statement, list members within itself are available for direct access.

{% highlight R %}
> attach(team)
> Vineet
[1] "Vineet"     "Maheshwari" "5.6"        "Gurgaon"   
> detach(team)
> Vineet
Error: object 'Vineet' not found
> 
{% endhighlight %}
