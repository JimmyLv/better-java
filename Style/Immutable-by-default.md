## Immutable-by-default 默认不可变

Unless you have a good reason to make them otherwise, variables, classes, and
collections should be immutable.

除非你理由充分，不然的话就保持变量、类和集合数据不可变。

Variable references can be made immutable with *final*:

变量引用可以被*final*修饰成不可变的。

```java
final FooWidget fooWidget;
if (condition()) {
    fooWidget = getWidget();
} else {
    try {
        fooWidget = cachedFooWidget.get();
    } catch (CachingException e) {
        log.error("Couldn't get cached value", e);
        throw e;
    }
}
// fooWidget is guaranteed to be set here
```

Now you can be sure that fooWidget won't be accidentally reassigned. The *final*
keyword works with if/else blocks and with try/catch blocks. Of course, if the
*fooWidget* itself isn't immutable you could easily mutate it.

现在你可以确定的是fooWidget不会被意外的重新赋值。*final*关键字将会和if/else以及try/catch代码块共同作用。当然，如果*fooWidget*不是不可变的话，你可以轻松得改变它。

Collections should, whenever possible, use the Guava [ImmutableMap][immutablemap],
[ImmutableList][immutablelist], or [ImmutableSet][immutableset] classes. These
have builders so that you can build them up dynamically and then mark them
immutable by calling the build method.

集合类都应该尽一切可能地使用Guava的[ImmutableMap][immutablemap]、
[ImmutableList][immutablelist]或者[ImmutableSet][immutableset]。他们都有builder模式以便于你可以动态得构建他们，然后通过调用build方法来使之保持不可变。

Classes should be made immutable by declaring fields immutable (via *final*)
and by using immutable collections. Optionally, you can make the class itself
*final* so that it can't be extended and made mutable.

类都应该通过声明不可变字段的方式（使用 *final*）被构造成不可变的，以及使用不可变集合。可选的是，你也可以将这个类声明为*final*，所以它就不可能被继承和被改变。
