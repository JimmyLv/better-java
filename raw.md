


# Tools

## IntelliJ IDEA

**Good alternatives**: [Eclipse][eclipse] and [Netbeans][netbeans]

The best Java IDE is [IntelliJ IDEA][intellij]. It has a ton of awesome
features, and is really the main thing that makes the verbosity of Java
bareable. Autocomplete is great,
[the inspections are top notch][intellijexample], and the refactoring
tools are really helpful.

The free community edition is good enough for me, but there are loads of great
features in the Ultimate edition like database tools, Spring Framework support
and Chronon.

### Chronon

One of my favorite features of GDB 7 was the ability to travel back in time
when debugging. This is possible with the [Chronon IntelliJ plugin][chronon]
when you get the Ultimate edition.

You get variable history, step backwards, method history and more. It's a
little strange to use the first time, but it can help debug some really
intricate bugs, Heisenbugs and the like.

## JRebel

Continuous integration is often a goal of software-as-a-service products. What
if you didn't even need to wait for the build to finish to see code changes
live?

That's what [JRebel][jrebel] does. Once you hook up your server to your JRebel
client, you can see changes on your server instantly. It's a huge time savings
when you want to experiment quickly.

## The Checker Framework

Java's type system is pretty weak. It doesn't differentiate between Strings
and Strings that are actually regular expressions, nor does it do any
[taint checking][taint]. However, [the Checker Framework][checker]
does this and more.

It uses annotations like *@Nullable* to check types. You can even define
[your own annotations][customchecker] to make the static analysis done even
more powerful.

## Eclipse Memory Analyzer

Memory leaks happen, even in Java. Luckily, there are tools for that. The best
tool I've used to fix these is the [Eclipse Memory Analyzer][mat]. It takes a
heap dump and lets you find the problem.

There's a few ways to get a heap dump for a JVM process, but I use
[jmap][jmap]:

```bash
$ jmap -dump:live,format=b,file=heapdump.hprof -F 8152
Attaching to process ID 8152, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 23.25-b01
Dumping heap to heapdump.hprof ...
... snip ...
Heap dump file created
```

Then you can open the *heapdump.hprof* file with the Memory Analyzer and see
what's going on fast.

# Resources

Resources to help you become a Java master.

## Books

* [Effective Java](http://www.amazon.com/Effective-Java-Edition-Joshua-Bloch/dp/0321356683)
* [Java Concurrency in Practice](http://www.amazon.com/Java-Concurrency-Practice-Brian-Goetz/dp/0321349601)

## Podcasts

* [The Java Posse](http://www.javaposse.com/)

