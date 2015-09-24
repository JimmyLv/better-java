# Libraries

Probably the best feature about Java is the extensive amount of libraries it
has. This is a small collection of libraries that are likely to be applicable
to the largest group of people.

## Missing Features

Java's standard library, once an amazing step forward, now looks like it's
missing several key features.

### Apache Commons

[The Apache Commons project][apachecommons] has a bunch of useful libraries.

**Commons Codec** has many useful encoding/decoding methods for Base64 and hex
strings. Don't waste your time rewriting those.

**Commons Lang** is the go-to library for String manipulation and creation,
    character sets, and a bunch of miscellaneous utility methods.

**Commons IO** has all the File related methods you could ever want. It has
[FileUtils.copyDirectory][copydir], [FileUtils.writeStringToFile][writestring],
[IOUtils.readLines][readlines] and much more.

### Guava

[Guava][guava] is Google's excellent here's-what-Java-is-missing library. It's
almost hard to distill everything that I like about this library, but I'm
going to try.

**Cache** is a simple way to get an in-memory cache that can be used to cache
network access, disk access, memoize functions, or anything really. Just
implement a [CacheBuilder][cachebuilder] which tells Guava how to build your
cache and you're all set!

**Immutable** collections. There's a bunch of these: [ImmutableMap][immutablemap],
[ImmutableList][immutablelist], or even [ImmutableSortedMultiSet][immutablesorted]
 if that's your style.

I also like writing mutable collections the Guava way:

```java
// Instead of
final Map<String, Widget> map = new HashMap<>();

// You can use
final Map<String, Widget> map = Maps.newHashMap();
```

There are static classes for [Lists][lists], [Maps][maps], [Sets][sets] and
more. They're cleaner and easier to read.

If you're stuck with Java 6 or 7, you can use the [Collections2][collections2]
class, which has methods like filter and transform. They allow you to write
fluent code without [Java 8][java8]'s stream support.


Guava has simple things too, like a **Joiner** that joins strings on
separators and a [class to handle interrupts][uninterrupt] by ignoring them.

### Gson

Google's [Gson][gson] library is a simple and fast JSON parsing library. It
works like this:

```java
final Gson gson = new Gson();
final String json = gson.toJson(fooWidget);

final FooWidget newFooWidget = gson.fromJson(json, FooWidget.class);
```

It's really easy and a pleasure to work with. The [Gson user guide][gsonguide]
has many more examples.

### Java Tuples

One of my on going annoyances with Java is that it doesn't have tuples built
into the standard library. Luckily, the [Java tuples][javatuples] project fixes
that.

It's simple to use and works great:

```java
Pair<String, Integer> func(String input) {
    // something...
    return Pair.with(stringResult, intResult);
}
```

### Joda-Time

[Joda-Time][joda] is easily the best time library I've ever used. Simple,
straightforward, easy to test. What else can you ask for?

You only need this if you're not yet on Java 8, as that has its own new
[time][java8datetime] library that doesn't suck.

### Lombok

[Lombok][lombok] is an interesting library. Through annotations, it allows you
to reduce the boilerplate that Java suffers from so badly.

Want setters and getters for your class variables? Simple:

```java
public class Foo {
    @Getter @Setter private int var;
}
```

Now you can do this:

```java
final Foo foo = new Foo();
foo.setVar(5);
```

And there's [so much more][lombokguide]. I haven't used Lombok in production
yet, but I can't wait to.

### Play framework

**Good alternatives**: [Jersey][jersey] or [Spark][spark]

There are two main camps for doing RESTful web services in Java:
[JAX-RS][jaxrs] and everything else.

JAX-RS is the traditional way. You combine annotations with interfaces and
implementations to form the web service using something like [Jersey][jersey].
What's nice about this is you can easily make clients out of just the
interface class.

The [Play framework][play] is a radically different take on web services on
the JVM: you have a routes file and then you write the classes referenced in
those routes. It's actually an [entire MVC framework][playdoc], but you can
easily use it for just REST web services.

It's available for both Java and Scala. It suffers slightly from being
Scala-first, but it's still good to use in Java.

If you're used to micro-frameworks like Flask in Python, [Spark][spark] will
be very familiar. It works especially well with Java 8.

### SLF4J

There are a lot of Java logging solutions out there. My favorite is
[SLF4J][slf4j] because it's extremely pluggable and can combine logs from many
different logging frameworks at the same time. Have a weird project that uses
java.util.logging, JCL, and log4j? SLF4J is for you.

The [two-page manual][slf4jmanual] is pretty much all you'll need to get
started.

### jOOQ

I dislike heavy ORM frameworks because I like SQL. So I wrote a lot of
[JDBC templates][jdbc] and it was sort of hard to maintain. [jOOQ][jooq] is a
much better solution.

It lets you write SQL in Java in a type safe way:

```java
// Typesafely execute the SQL statement directly with jOOQ
Result<Record3<String, String, String>> result =
create.select(BOOK.TITLE, AUTHOR.FIRST_NAME, AUTHOR.LAST_NAME)
    .from(BOOK)
    .join(AUTHOR)
    .on(BOOK.AUTHOR_ID.equal(AUTHOR.ID))
    .where(BOOK.PUBLISHED_IN.equal(1948))
    .fetch();
```

Using this and the [DAO][dao] pattern, you can make database access a breeze.

## Testing

Testing is critical to your software. These packages help make it easier.

### jUnit 4

[jUnit][junit] needs no introduction. It's the standard tool for unit testing
in Java.

But you're probably not using jUnit to its full potential. jUnit supports
[parametrized tests][junitparam], [rules][junitrules] to stop you from writing
so much boilerplate, [theories][junittheories] to randomly test certain code,
and [assumptions][junitassume].

### jMock

If you've done your dependency injection, this is where it pays off: mocking
out code which has side effects (like talking to a REST server) and still
asserting behavior of code that calls it.

[jMock][jmock] is the standard mocking tool for Java. It looks like this:

```java
public class FooWidgetTest {
    private Mockery context = new Mockery();

    @Test
    public void basicTest() {
        final FooWidgetDependency dep = context.mock(FooWidgetDependency.class);

        context.checking(new Expectations() {{
            oneOf(dep).call(with(any(String.class)));
            atLeast(0).of(dep).optionalCall();
        }});

        final FooWidget foo = new FooWidget(dep);

        Assert.assertTrue(foo.doThing());
        context.assertIsSatisfied();
    }
}
```

This sets up a *FooWidgetDependency* via jMock and then adds expectations. We
expect that *dep*'s *call* method will be called once with some String and that
*dep*'s *optionalCall* method will be called zero or more times.

If you have to set up the same dependency over and over, you should probably
put that in a [test fixture][junitfixture] and put *assertIsSatisfied* in an
*@After* fixture.

### AssertJ

Do you ever do this with jUnit?

```java
final List<String> result = some.testMethod();
assertEquals(4, result.size());
assertTrue(result.contains("some result"));
assertTrue(result.contains("some other result"));
assertFalse(result.contains("shouldn't be here"));
```

This is just annoying boilerplate. [AssertJ][assertj] solves this. You can
transform the same code into this:

```java
assertThat(some.testMethod()).hasSize(4)
                             .contains("some result", "some other result")
                             .doesNotContain("shouldn't be here");
```

This fluent interface makes your tests more readable. What more could you want?

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

