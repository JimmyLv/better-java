## Missing Features 遗失的特性

Java's standard library, once an amazing step forward, now looks like it's
missing several key features.

Java的标准库曾经有过非常大的进步，但是现在看起来缺失了一些核心特性。

### Apache Commons

[The Apache Commons project][apachecommons] has a bunch of useful libraries.

Apache Commons项目现在有了非常可观的有用的库。

**Commons Codec** has many useful encoding/decoding methods for Base64 and hex
strings. Don't waste your time rewriting those.

Apache Commons包括了基于Base64和hex字符串的编码/解码函数，不要浪费时间去「造轮子」了。

**Commons Lang** is the go-to library for String manipulation and creation, character sets, and a bunch of miscellaneous utility methods.

**Commons Lang**是一个用于字符串操作和创建，字符集以及拥有各种丰富的工具方法的go-to库。

**Commons IO** has all the File related methods you could ever want. It has
[FileUtils.copyDirectory][copydir], [FileUtils.writeStringToFile][writestring],
[IOUtils.readLines][readlines] and much more.

**Commons IO**包含了你可能想要的所有文件操作方法，其中有[FileUtils.copyDirectory][copydir]、[FileUtils.writeStringToFile][writestring]、
[IOUtils.readLines][readlines]以及非常多其他的。

### Guava

[Guava][guava] is Google's excellent here's-what-Java-is-missing library. It's
almost hard to distill everything that I like about this library, but I'm
going to try.

[Guava][guava]是谷歌的一个非常棒的「Java本该有的」库，很难说清楚我喜欢这个库的所有东西，但是我会尝试的。

**Cache** is a simple way to get an in-memory cache that can be used to cache
network access, disk access, memorize functions, or anything really. Just
implement a [CacheBuilder][cachebuilder] which tells Guava how to build your
cache and you're all set!

**Cache**是获取内存缓存的一种简单方式，可以被用于缓存网络存取、硬盘存取、存储函数，或者其他任何事情。只需要实现一个[CacheBuilder][cachebuilder]，就可以告诉Guava你要如何实现缓存就可以了。

**Immutable** collections. There's a bunch of these: [ImmutableMap][immutablemap],
[ImmutableList][immutablelist], or even [ImmutableSortedMultiSet][immutablesorted]
 if that's your style.

**Immutable**集合，这儿也有一些可能合你胃口的：[ImmutableMap][immutablemap]、
[ImmutableList][immutablelist]、甚至于[ImmutableSortedMultiSet][immutablesorted]。

I also like writing mutable collections the Guava way:

我也喜欢以Guava的方式来写可变集合：

```java
// Instead of
final Map<String, Widget> map = new HashMap<>();

// You can use
final Map<String, Widget> map = Maps.newHashMap();
```

There are static classes for [Lists][lists], [Maps][maps], [Sets][sets] and
more. They're cleaner and easier to read.

这儿有一些用于[Lists][lists]、[Maps][maps]、[Sets][sets]等等的静态类，非常清晰、易于阅读。

If you're stuck with Java 6 or 7, you can use the [Collections2][collections2]
class, which has methods like filter and transform. They allow you to write
fluent code without [Java 8][java8]'s stream support.

如果你被迫使用Java 6或者7，你可以使用[Collections2][collections2]类，拥有一些方法比如说filter和transform。他们可以让你哪怕没有[Java 8][java8]的stream支持也可以写出流畅的代码。

Guava has simple things too, like a **Joiner** that joins strings on
separators and a [class to handle interrupts][uninterrupt] by ignoring them.

Guava也有一些简单的东西，比如说**Joiner**可以通过分隔符的方式连接字符串，通过忽略它们，还有[一个类可以处理中断][uninterrupt]。

### Gson

Google's [Gson][gson] library is a simple and fast JSON parsing library. It
works like this:

Google的[Gson][gson]库是一个非常简单和高效的JSON解析库，它可以这样：

```java
final Gson gson = new Gson();
final String json = gson.toJson(fooWidget);

final FooWidget newFooWidget = gson.fromJson(json, FooWidget.class);
```

It's really easy and a pleasure to work with. The [Gson user guide][gsonguide]
has many more examples.

这样做真的非常简单和令人满意，[Gson用户指南][gsonguide]中更多更好的例子。

### Java Tuples Java元组

One of my on going annoyances with Java is that it doesn't have tuples built
into the standard library. Luckily, the [Java tuples][javatuples] project fixes
that.

我对Java非常不满的一点就是，它竟然也没用把元组加入到标准库中。幸运的是，[Java tuples][javatuples]项目拯救了我。

It's simple to use and works great:

使用起来很简单，也很棒：

```java
Pair<String, Integer> func(String input) {
    // something...
    return Pair.with(stringResult, intResult);
}
```

### Joda-Time

[Joda-Time][joda] is easily the best time library I've ever used. Simple,
straightforward, easy to test. What else can you ask for?

[Joda-Time][joda]肯定就是我使用过的最好的time库。很简单，坦率的讲，是非常容易测试。你还能奢求什么呢？

You only need this if you're not yet on Java 8, as that has its own new
[time][java8datetime] library that doesn't suck.

如果你还没有使用Java 8的话，你就只需要[Joda-Time][joda]，因为Java 8有了一个自己的新[time][java8datetime]库，而且没有那么令人讨厌。

### Lombok

[Lombok][lombok] is an interesting library. Through annotations, it allows you
to reduce the boilerplate that Java suffers from so badly.

[Lombok][lombok]是一个非常有趣的库。可以让你通过注解的方式，减少Java的样本文件，Java已经深受其害非常严重了。

Want setters and getters for your class variables? Simple:

想为你的类变量添加setters和getters方法？很简单：

```java
public class Foo {
    @Getter @Setter private int var;
}
```

Now you can do this:

然后可以这样：

```java
final Foo foo = new Foo();
foo.setVar(5);
```

And there's [so much more][lombokguide]. I haven't used Lombok in production
yet, but I can't wait to.

更多详情请看[这里][lombokguide]。目前为止，我还没有在产品环境中使用过Lombok，但是早就跃跃欲试了。

### Play framework

**Good alternatives**: [Jersey][jersey] or [Spark][spark]

**优秀替代品**：[Jersey][jersey]或者[Spark][spark]

There are two main camps for doing RESTful web services in Java:
[JAX-RS][jaxrs] and everything else.

使用Java实现RESTful的Web服务主要分为两大阵营：[JAX-RS][jaxrs]和其他。

JAX-RS is the traditional way. You combine annotations with interfaces and
implementations to form the web service using something like [Jersey][jersey].
What's nice about this is you can easily make clients out of just the
interface class.

[JAX-RS][jaxrs]是传统的一种方式，你可以将注解和接口结合起来，使用[Jersey][jersey]等搭建的web服务来实现。很棒的就是，你可以很轻易地将客户端和接口类分离。

The [Play framework][play] is a radically different take on web services on
the JVM: you have a routes file and then you write the classes referenced in
those routes. It's actually an [entire MVC framework][playdoc], but you can
easily use it for just REST web services.

[Play框架][play]是在JVM上完全不同的一种web服务实现：通过路由文件，然后编写在路由中制定的类。这里有一个[完整的Play MVC 框架][playdoc]，但是你可以使用它轻松创建一个REST web服务。

It's available for both Java and Scala. It suffers slightly from being
Scala-first, but it's still good to use in Java.

对Java和Scala来说都是可行的，虽然稍微优先用于Scala，但是在Java使用起来也是很棒的。

If you're used to micro-frameworks like Flask in Python, [Spark][spark] will
be very familiar. It works especially well with Java 8.

如果你习惯于在Python里面使用Flask这样的微框架，[Spark][spark]就会非常容易上手，尤其适用于Java 8。

### SLF4J

There are a lot of Java logging solutions out there. My favorite is
[SLF4J][slf4j] because it's extremely pluggable and can combine logs from many
different logging frameworks at the same time. Have a weird project that uses
java.util.logging, JCL, and log4j? SLF4J is for you.

这儿也有很多Java的logging解决方案。我最喜欢的就是[SLF4J][slf4j]，因为它非常具有可插拔性，也可以同时从其他logging框架中集成记录。有一个使用java.util.logging、JCL和log4j的奇怪项目？SLF4J就是为你准备的。

The [two-page manual][slf4jmanual] is pretty much all you'll need to get
started.

[two-page手册][slf4jmanual]非常不错，你可以用来入门。

### jOOQ

I dislike heavy ORM frameworks because I like SQL. So I wrote a lot of
[JDBC templates][jdbc] and it was sort of hard to maintain. [jOOQ][jooq] is a
much better solution.

我不喜欢重量级的ORM框架，因为我喜欢SQL。所以我写了大量的[JDBC模板][jdbc]，然而维护起来非常困难。[jOOQ][jooq]远远好于我的解决方案。

It lets you write SQL in Java in a type safe way:

它可以让你在Java中以一种类型安全的方式编写SQL：

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

使用jOOQ和[jOOQ][jooq]模式，你就可以轻松操作数据库了。

[apachecommons]: http://commons.apache.org/
[copydir]: http://commons.apache.org/proper/commons-io/javadocs/api-release/org/apache/commons/io/FileUtils.html#copyDirectory(java.io.File,%20java.io.File)
[writestring]: http://commons.apache.org/proper/commons-io/javadocs/api-release/org/apache/commons/io/FileUtils.html#writeStringToFile(java.io.File,%20java.lang.String)
[readlines]: http://commons.apache.org/proper/commons-io/javadocs/api-release/org/apache/commons/io/IOUtils.html#readLines(java.io.InputStream)
[guava]: https://github.com/google/guava
[cachebuilder]: http://docs.guava-libraries.googlecode.com/git-history/release/javadoc/com/google/common/cache/CacheBuilder.html
[immutablesorted]: http://docs.guava-libraries.googlecode.com/git-history/release/javadoc/com/google/common/collect/ImmutableSortedMultiset.html
[immutablemap]: http://docs.guava-libraries.googlecode.com/git/javadoc/com/google/common/collect/ImmutableMap.html
[immutableset]: http://docs.guava-libraries.googlecode.com/git/javadoc/com/google/common/collect/ImmutableSet.html
[lists]: http://docs.guava-libraries.googlecode.com/git-history/release/javadoc/com/google/common/collect/Lists.html
[maps]: http://docs.guava-libraries.googlecode.com/git-history/release/javadoc/com/google/common/collect/Maps.html
[sets]: http://docs.guava-libraries.googlecode.com/git-history/release/javadoc/com/google/common/collect/Sets.html
[java8]: http://www.java8.org/
[uninterrupt]: http://docs.guava-libraries.googlecode.com/git-history/release/javadoc/com/google/common/util/concurrent/Uninterruptibles.html
[collections2]: http://docs.guava-libraries.googlecode.com/git-history/release/javadoc/com/google/common/collect/Collections2.html
[gson]: https://code.google.com/p/google-gson/
[gsonguide]: https://sites.google.com/site/gson/gson-user-guide
[joda]: http://www.joda.org/joda-time/
[lombokguide]: http://jnb.ociweb.com/jnb/jnbJan2010.html
[java8datetime]: http://www.oracle.com/technetwork/articles/java/jf14-date-time-2125367.html
[jersey]: https://jersey.java.net/
[spark]: http://www.sparkjava.com/
[jaxrs]: http://en.wikipedia.org/wiki/Java_API_for_RESTful_Web_Services
[playdoc]: http://www.playframework.com/documentation/2.3.x/Anatomy
[play]: http://www.playframework.com/
[slf4j]: http://www.slf4j.org/
[slf4jmanual]: http://www.slf4j.org/manual.html
[jdbc]: http://docs.spring.io/spring/docs/4.0.3.RELEASE/javadoc-api/org/springframework/jdbc/core/JdbcTemplate.html
[jooq]: http://www.jooq.org/
[dao]: http://www.javapractices.com/topic/TopicAction.do?Id=66
[javatuples]: http://www.javatuples.org/
