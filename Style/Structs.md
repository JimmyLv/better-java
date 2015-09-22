## Structs 结构体

One of the simplest things we as programmers do is pass around data. The
traditional way to do this is to define a JavaBean:

我们作为程序员做的最简单的事情之一就是传输数据，通过传统的方式来做的话就是定义一个JavaBean：

```java
public class DataHolder {
    private String data;

    public DataHolder() {
    }

    public void setData(String data) {
        this.data = data;
    }

    public String getData() {
        return this.data;
    }
}
```

This is verbose and wasteful. Even if your IDE automatically generated this
code, it's a waste. So, [don't do this][dontbean].

这非常啰嗦和浪费。尽管你的IDE可以自动生成这些代码，但还是太浪费了。所以说[不要这样做][dontbean]。

Instead, I prefer the C struct style of writing classes that merely hold data:

取而代之的是，我更喜欢这种C结构的风格，仅仅是写一个类用来包含数据。

```java
public class DataHolder {
    public final String data;

    public DataHolder(String data) {
        this.data = data;
    }
}
```

This is a reduction in number of lines of code by a half. Further, this class
is immutable unless you extend it, so we can reason about it easier as we know
that it can't be changed.

这使得代码行数减少了一半。此外，这个类是不可变的，除非你扩展它，所以我们可以更容易进行推理，因为我们知道它不能被改变。

If you're storing objects like Map or List that can be modified easily, you
should instead use ImmutableMap or ImmutableList, which is discussed in the
section about immutability.

如果你正在存储Map或者List这样可以被轻易修改的类，你应该使用ImmutableMap或者ImmutableList，这将会在immutability部分进行讨论。

### The Builder Pattern 建造者模式

If you have a rather complicated object that you want to build a struct for,
consider the Builder pattern.

如果你有一个比较复杂的对象想要构造的话，试试Builder模式。

You make a subclass in your object which will construct your object. It uses
mutable state, but as soon as you call build, it will emit an immutable
object.

你可以在对象中创建一个用来构造对象的子类。它可以使用可变状态，但只要你调用创建函数，你就会给出一个不可变对象。

Imagine we had a more complicated *DataHolder*. The builder for it might look
like:

想象一下我们有一个比较复杂的*DataHolder*，构造它的builder可能就像这样：

```java
public class ComplicatedDataHolder {
    public final String data;
    public final int num;
    // lots more fields and a constructor

    public static class Builder {
        private String data;
        private int num;

        public Builder data(String data) {
            this.data = data;
            return this;
        }

        public Builder num(int num) {
            this.num = num;
            return this;
        }

        public ComplicatedDataHolder build() {
            return new ComplicatedDataHolder(data, num); // etc
        }
    }
}
```

Then to use it:

然后使用它：

```java
final ComplicatedDataHolder cdh = new ComplicatedDataHolder.Builder()
    .data("set this")
    .num(523)
    .build();
```

There are [better examples of Builders elsewhere][builderex] but this should
give you a taste for what it's like. This ends up with a lot of the boilerplate
we were trying to avoid, but it gets you immutable objects and a very fluent
interface.

这里有其他的[更好的Builder例子][builderex]，可以给你一些该有的味道。这就彻底解决了一些我们曾经试图避免的样板文件，但它可以让你使用不可变对象以及一个非常流畅的接口。
