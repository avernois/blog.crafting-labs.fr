---
layout: post
title: "Diamond Kata"

categories:
---

I heard a lot about this kata.

So let's start with the first test.

{% highlight java %}

@Test public void 
should_draw_diamond_A() {
    assertEquals("A", Diamond.create('A'));
}

{% endhighlight %}

Test are Red, it's time to make them go to green :

{% highlight java %}

public class Diamond {

    public static String create(Character c) {
        return "A";
    }   
}
{% endhighlight %}

Yep, that's a stupid implementation :)

Let's add another test.

{% highlight java %}
@Test public void 
should_draw_diamond_B() {
    assertEquals(" A \nB B\n A ", Diamond.create('B'));
}
{% endhighlight %}

And make it pass.

{% highlight java %}
public static String create(Character c) {
    if (c.equals('B')) {
        return " A \n"
             + "B B\n"
             + " A ";
    }
    
    return "A";
}
        
{% endhighlight %}

And it's green. Time to refactor. But I can't see duplication yet. Well, there are twice the same " A " line in the 'B' diamond. But I can't give a meaning to it. So, let's keep it, and move to the third test.

{% highlight java %}
@Test public void 
should_draw_diamond_C() {
    assertEquals("  A  \n"
               + " B B \n"
               + "C   C\n"
               + " B B \n"
               + "  A  ", Diamond.create('C'));
}

{% endhighlight %}

As I try to be a coherent guy, my way to make it green won't differ from the previous one :)

{% highlight java %}
public static String create(Character c) {
    if (c.equals('C')) {
        return "  A  \n"
             + " B B \n"
             + "C   C\n"
             + " B B \n"
             + "  A  ";
    }

    if (c.equals('B')) {
        return " A \n"
             + "B B\n"
             + " A ";
    }
    
    return "A";
}
{% endhighlight %}

Yep, again that is a stupid implementation. But at this moment I don't care being clever, doing nice, clean thing. At this moment I just want to be sure that the test I wrote is the one I wanted to write.
By making it goes green with a simple solution, there are very few risk I introduce a mistake in the implementation. So when I see the test goes from red to green, I can be confident on my test.
That simple code is here to test my test.



{% highlight java %}
 public static String create(Character c) {
        if (c.equals('C')) {
            return "  " +        "A"  +       "  " + "\n"
                 +  " " + "B" +  " "  + "B" + " "  + "\n"
                 +   "" + "C" + "   " + "C" + ""   + "\n"
                 +  " " + "B" +  " "  + "B" + " "  + "\n"
                 + "  " +        "A"  +       "  ";
        }
        
        if (c.equals('B')) {
            return " " + "A" + " " + "\n"
                 + "B" + " " + "B" + "\n"
                 + " " + "A" + " ";
        }
        
        return "A";
    }

{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}
------

-- note : 

-- illustration : [2013.08 escala solidcrafters.0179 by Antoine Vernois](https://www.flickr.com/photos/antoinevernois/16448025843) en CC-BY-NC 2.0
