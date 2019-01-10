---
layout:     post
title:      Making jar by hand, with dep
date:       2015-02-25 09:00:00
author:     Julien Diener
summary:    Back to the basic
categories: blog-post
thumbnail:  blog
tags:
 - java
---


I happened to have problem running a jar with dependencies, and I found my-self wondering: Do I really know how it works?

I don’t remember having ever done it manually, so I tried. It is a good thing to be sure of what we know. Here is the code, lets two classes A and B. A’s got the main and requires B:
	
{% highlight java %}
package one.pack;
 
import two.pack.B;
 
public class A{
    public static void main(String args[]){
        B b = new B();
        b.println("Hello world");
    }
}
{% endhighlight %}
	
{% highlight java %}
package two.pack;
 
public class B{
    public void println(String message){
        System.out.println("B says: "+message);
    }
}
{% endhighlight %}

Now, let’s compile everything

{% highlight bash %}
# compile B.java into B.jar
javac B.java -d .    # "-d .": automatically create folders two/pack/
jar -cf B.jar two/     
 
# compile A.java into A.jar
javac -cp B.jar A.java -d .   # include B.jar in the classpath
jar -cf A.jar one/
{% endhighlight %}

Finally, move A.jar and run it

{% highlight bash %}
mv A.jar /somewhere/else
java -cp /somewhere/else/A.jar:B.jar one.pack.A
{% endhighlight %}

Output: `B says: Hello world`

Conclusion, it is just as expected but now at least I’m sure of it :-)
