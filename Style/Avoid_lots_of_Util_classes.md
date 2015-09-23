## Avoid lots of Util classes 避免大量工具类

Be careful if you find yourself adding a lot of methods to a Util class.

如果你在为Util类添加大量方法的时候，就要开始小心了。

```java
public class MiscUtil {
    public static String frobnicateString(String base, int times) {
        // ... etc
    }

    public static void throwIfCondition(boolean condition, String msg) {
        // ... etc
    }
}
```

These classes, at first, seem attractive because the methods that go in them
don't really belong in any one place. So you throw them all in here in the
name of code reuse.

这些类起初看起来很诱人，因为在这些方法里面，真的可以不属于任何一个地方。所以你就以代码重用的名义把他们全部扔到了这里。

The cure is worse than the disease. Put these classes where they belong, or
if you must have common methods like this, consider [Java 8][java8]'s default
methods on interfaces. Then you could lump common actions into interfaces.
And, since they're interfaces, you can implement multiple of them.

这属于饮鸠止渴。把这些类放回他们该在的地方，或者如果你不得不有一些这样的公共方法，考虑一下[Java 8][java8]的接口默认方法。然后你把共同行为并到一起放进接口。而且，因为接口的好处，你可以有不同的具体实现。

```java
public interface Thrower {
    default void throwIfCondition(boolean condition, String msg) {
        // ...
    }

    default void throwAorB(Throwable a, Throwable b, boolean throwA) {
        // ...
    }
}
```

Then every class which needs it can simply implement this interface.

然后每个类就可以很轻易地实现这个接口所需要的东西。

[java8]: http://www.java8.org/