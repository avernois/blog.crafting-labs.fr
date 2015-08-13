---
layout: post
title: "Diamond Kata"

categories:
---
[![By kubotake [CC BY 2.0 (http://creativecommons.org/licenses/by/2.0)], via Wikimedia Commons](https://upload.wikimedia.org/wikipedia/commons/thumb/5/55/Kubotake_-_Diamond_ring_on_22_Jul._2009_%28by%29.jpg/320px-Kubotake_-_Diamond_ring_on_22_Jul._2009_%28by%29.jpg)](https://commons.wikimedia.org/wiki/File:Kubotake_-_Diamond_ring_on_22_Jul._2009_%28by%29.jpg){: .left-image}

## the problem: the diamond kata
I use Seb Rose description as it is simple and efficient.

>Given a letter, print a diamond starting with ‘A’ with the supplied letter at the widest point.

> For example: print-diamond ‘C’ prints

      A
     B B
    C   C
     B B
      A


I heard a lot about this kata. Recently[^1], it was the main subject of a two hours workshop at the awesome [NCrafts](http://ncrafts.io) conference.
So long time after the initial battle[^2], I decided to give it a try.

## my solution

### the idea

Well, as usual, when I'm told that something is difficult or impossible, I just don't care and do it as I will have if no one told me anything.
So I apply TDD as I usually do: red, green, refactor. And that's all. 

Write a test, make it pass, clean the code. One step at a time.

### the first test
So let's start with the first test.

{% highlight java %}
public class DiamondTest {
    @Test public void 
    should_draw_diamond_A() {
        assertEquals("A", Diamond.create('A'));
    }
}
{% endhighlight %}

Test is Red, it's time to make it go to green :

{% highlight java %}

public class Diamond {

    public static String create(Character c) {
        return "A";
    }   
}
{% endhighlight %}

Yep, that's a stupid implementation. But it works :)

And quite clean by itself. So let's add another test.

### a second test

{% highlight java %}
    @Test public void 
    should_draw_diamond_B() {
        assertEquals(" A \nB B\n A ", Diamond.create('B'));
    }
{% endhighlight %}

And make it pass stupidly.

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

And it's green, so it's time to refactor. 
But I can't see duplication yet. 

Well, there are twice the same " A " line in the 'B' diamond. But I can't give a meaning to it. I probably don't have enough data.

So, I'll keep things like that for now, and add a third test.

# and the third

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

As I try to be coherent, my way to make it green won't differ from the previous one :)

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

Yep, again that is a stupid implementation. 
Because at this moment I don't care being clever, doing nice, clean things. At this moment I just want to be sure that the test I wrote is the one I intended to write.

By making it goes green with a simple solution, there are very few risks I introduced a mistake in the implementation. So when I see the test goes from red to green, I can be confident on my test.

That's my way to test my tests.

So now, I may have enough materials to see if I can make some interesting things appear.

### time to start refactoring
There should be some logic in the letters and spaces distribution. 
As I don't understand it yet, I will artificially separate them. Yes, I'm going to create kind of artificial duplication.

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

Now I can notice that first and last lines are `z spaces - A - z spaces`.
If a diamond 'A' has a size of 1, 'B' of 2, 'C' 3 and so on, then `z = (size - 1)`

Great, lets put that logic in a method.

{% highlight java %}
public static String create(Character c) {
    int size = c - 'A' + 1;

    if (c.equals('C')) {
        return diamondTip(size) + "\n"
             +  " " + "B" +  " "  + "B" + " "  + "\n"
             +   "" + "C" + "   " + "C" + ""   + "\n"
             +  " " + "B" +  " "  + "B" + " "  + "\n"
             + diamondTip(size);
    }
    
    if (c.equals('B')) {
        return diamondTip(size) + "\n"
             + "B" + " " + "B" + "\n"
             + diamondTip(size);
    }
    
    return "A";
}

private static String diamondTip(int size) {
    return manySpaces(size -1) + "A" + manySpaces(size - 1);
}

private static String manySpaces(int nbSpaces) {
    StringBuilder builder = new StringBuilder();
    
    for (int i = 0; i < nbSpaces; i++) {
        builder.append(" ");
    }
    return builder.toString();
}

{% endhighlight %}

I also notice that other lines follow the same pattern : `x spaces - a char - y spaces - same char - x spaces`
So lets make that appear in the code.

{% highlight java %}
public static String create(Character c) {
    ...
    if (c.equals('C')) {
        return diamondTip(size) + "\n"
             +  manySpaces(1) + "B" + manySpaces(1) + "B" + manySpaces(1) + "\n"
             +  manySpaces(0) + "C" + manySpaces(3) + "C" + manySpaces(0) + "\n"
             +  manySpaces(1) + "B" + manySpaces(1) + "B" + manySpaces(1) + "\n"
             + diamondTip(size);
    }

    if (c.equals('B')) {
        return diamondTip(size) + "\n"
             + "B" + manySpaces(1) + "B" + "\n"
             + diamondTip(size);
    }
    ...
}
{% endhighlight %}

There is definitely something that tie everything, but i don't see it yet.

### a fourth test
Let's add the D diamond. I won't show you the test, it the same than previous but with a D diamond.
Make it pass by adding this in our current solution.

{% highlight java %}
public static String create(Character c) {
    ...
    if (c.equals('D')) {
        return diamondTip(size) + "\n"
                + manySpaces(2) + "B" + manySpaces(1) + "B" + manySpaces(2) + "\n"
                + manySpaces(1) + "C" + manySpaces(3) + "C" + manySpaces(1) + "\n"
                + manySpaces(0) + "D" + manySpaces(5) + "D" + manySpaces(0) + "\n"
                + manySpaces(1) + "C" + manySpaces(3) + "C" + manySpaces(1) + "\n"
                + manySpaces(2) + "B" + manySpaces(1) + "B" + manySpaces(2) + "\n"
                + diamondTip(size);
    }
    ...
}
{% endhighlight %}

From now, I will only show you the refactoring on the D diamond.

All those integers must have some kind of relationship. Maybe we can figure it by rearranging them.

Let's introduce the `width` of the diamond: it's the
I draw some diamond on a paper and manage to figure quite rapidly that the `width` is `size * 2 - 1`

{% highlight java %}
public static String create(Character c) {
    int size = c - 'A' + 1;
    int width = size * 2 - 1;
    
    if (c.equals('D')) {
        return diamondTip(size) + "\n"
            + manySpaces(2) + "B" + manySpaces(width - 2*3) + "B" + manySpaces(2) + "\n"
            + manySpaces(1) + "C" + manySpaces(width - 2*2) + "C" + manySpaces(1) + "\n"
            + manySpaces(0) + "D" + manySpaces(width - 2*1) + "D" + manySpaces(0) + "\n"
            + manySpaces(1) + "C" + manySpaces(width - 2*2) + "C" + manySpaces(1) + "\n"
            + manySpaces(2) + "B" + manySpaces(width - 2*3) + "B" + manySpaces(2) + "\n"
            + diamondTip(size);
     }
     ...
}
{% endhighlight %}


Well, I think I got it. Let make appear a floor level.

{% highlight java %}
public static String create(Character c) {
    ...
    if (c.equals('D')) {
        String diamond = diamondTip(size) + "\n";

        int floor = 3;
        diamond += manySpaces(floor - 1) + "B" + manySpaces(width - 2*floor) + "B" + manySpaces(floor - 1) + "\n";
        floor = 2;
        diamond += manySpaces(floor - 1) + "C" + manySpaces(width - 2*floor) + "C" + manySpaces(floor - 1) + "\n";
        floor = 1;
        diamond += manySpaces(floor - 1) + "D" + manySpaces(width - 2*floor) + "D" + manySpaces(floor - 1) + "\n";
        floor = 2;
        diamond += manySpaces(floor - 1) + "C" + manySpaces(width - 2*floor) + "C" + manySpaces(floor - 1) + "\n";
        floor = 3;
        diamond += manySpaces(floor - 1) + "B" + manySpaces(width - 2*floor) + "B" + manySpaces(floor - 1) + "\n";

        diamond += diamondTip(size);
                
        return diamond;
    }
    ...
}
{% endhighlight %}
Yes, every lines really look like the same now, we can give it a name.

{% highlight java %}
public static String create(Character c) {
    ...
    if (c.equals('D')) {
        String diamond = diamondTip(size) + "\n";
        diamond += diamondWall(size, 3, "B") + "\n";
        diamond += diamondWall(size, 2, "C") + "\n";
        diamond += diamondWall(size, 1, "D") + "\n";
        diamond += diamondWall(size, 2, "C") + "\n";
        diamond += diamondWall(size, 3, "B") + "\n";
        diamond += diamondTip(size);
                                     
        return diamond;
    }

    ...
}

private static String diamondWall(int size, int floor, String wall) {
    int width = size * 2 - 1;
    return manySpaces(floor - 1) + wall + manySpaces(width - 2*floor) + wall + manySpaces(floor - 1);
}
{% endhighlight %}

That's better, but we are not done yet.
There is a pattern in these calls. Let's see what append if we renumber floors so they become a sequence, from `+size` to `-size`

{% highlight java %}
public static String create(Character c) {
    ...
    if (c.equals('D')) {
        String diamond = diamondTip(size) + "\n";
        diamond += diamondWall(size, 2, "B") + "\n";
        diamond += diamondWall(size, 1, "C") + "\n";
        diamond += diamondWall(size, 0, "D") + "\n";
        diamond += diamondWall(size, -1, "C") + "\n";
        diamond += diamondWall(size, -2, "B") + "\n";
        diamond += diamondTip(size);
                             
        return diamond;
    }
    ...
}

private static String diamondWall(int size, int floor, String wall) {
    int width = size * 2 - 1;
    int absoluteFloor = Math.abs(floor);

    return manySpaces(absoluteFloor) + wall + manySpaces(width - 2*(absoluteFloor + 1)) + wall + manySpaces(absoluteFloor);
}
{% endhighlight %}

Well, there seems to have a loop hidden there. The problem to introduce it are those characters in the parameters of diamondWall call.
But we can easily get ride of them as the character used in a floor can be compute from the size of the diamond and the current floor.


{% highlight java %}
private static String diamondWall(int size, int floor) {
    int width = size * 2 - 1;
    int absoluteFloor = Math.abs(floor);
        
    Character wall = Character.toChars('A' + size - absoluteFloor -1)[0]; 

    return manySpaces(absoluteFloor) + wall + manySpaces(width - 2*(absoluteFloor + 1)) + wall + manySpaces(absoluteFloor);
}

public static String create(Character c) {
    ...

    if (c.equals('D')) {
        String diamond = diamondTip(size) + "\n";
        diamond += diamondWall(size, 2)  + "\n";
        diamond += diamondWall(size, 1)  + "\n";
        diamond += diamondWall(size, 0)  + "\n";
        diamond += diamondWall(size, -1) + "\n";
        diamond += diamondWall(size, -2) + "\n";
        diamond += diamondTip(size);
                             
        return diamond;
    }
    ...
}
{% endhighlight %}

and finally

{% highlight java %}
public static String create(Character c) {
    int size = sizeOfDiamond(c);
    
    if(size == 1) return "A";
    
    String diamond = diamondTip(size) + "\n";
    
    for (int floor = size - 2; floor >= -(size - 2) ; floor --) {
        diamond += diamondWall(size, floor)  + "\n";
    }
    
    diamond += diamondTip(size);
    
    return diamond;
}
{% endhighlight %}

## thoughts

My [first attempt on that kata](https://github.com/avernois/kata-diamond_java/tree/2015.05.23-first_attempt) took me around 2hours in a train[^6].

As I usually do I've made things with very small steps in order to keep my test green all the time.
I tried to let the algorithm emerge from the refactoring, and not the opposite.

Of course, it did not emerge by itself. With that kind of problem, I had in mind that there will be some kind of loop in the solution. So my refactorings aimed to make that loop appears: introducing deliberate duplication so that each line looks the same, then unifying indices.

Introducing one change at a time allow my test to be very efficient in helping me to find the errors I've made[^7].

The full code is available on [my github](https://github.com/avernois/kata-diamond_java). Look in the branches :)[^8]

## next
Once there, if it was real code, I will probably give name to `size -2` and `-(size - 2)`. Maybe attic and cellar to stick with the building metaphore. And `size` should probably become `height`.

I also don't really like the use of a `Character` everywhere will in fact it is a kind of diamond. So i'll introduce a `DiamondKind` class to hold the `Character` and `size`[^3], `width` calculation. Maybe other `Character` operations too[^4].

Maybe a `Floor` class too[^5].

The "A" diamond would probably become a constant with a name.

------
image : By kubotake [CC BY 2.0](http://creativecommons.org/licenses/by/2.0), via Wikimedia Commons. During a solar eclipse, in french, the third contact is also called "Effet diamant" or diamond effect.



[^1]: well, it was recent when I started write that post.
[^2]: started I think with this post [Recycling test in TDD](http://claysnow.co.uk/recycling-tests-in-tdd/) by Seb Rose.
[^3]: or height
[^4]: like a `charForFloor`
[^5]: but currently the use of `floor` is an implementation detail, not sure if it's a good idea to give its own class that will become public.
[^6]: on my way home from the awesome [Ncrafts](http://ncrafts.io) conference.
[^7]: and I made a lot of them. +1/-1 shifts are my personal hell :)
[^8]: in the [branch 2015.05.23-step_by_step](https://github.com/avernois/kata-diamond_java/tree/2015.05.23-step_by_step), I made a commit at each step with some explanation of the purpose of that step. Mostly, it is what you find in this post.