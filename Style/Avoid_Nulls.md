## Avoid Nulls 避免Null

Try to avoid using nulls when you can. Do not return null collections when you
should have instead returned an empty collection. If you're going to use null, 
consider the [@Nullable][nullable] annotation. [IntelliJ IDEA][intellij] has 
built-in support for the @Nullable annotation.

尽可能尝试避免使用Nulls。当你可以返回空集合的时候就不要返回null的集合对象。如果你要使用null的话，考虑一下[@Nullable][nullable]注解。[IntelliJ IDEA][intellij]已经内置支持了@Nullable注解。

If you're using [Java 8][java8], you can use the excellent new 
[Optional][optional] type. If a value may or may not be present, wrap it in
an *Optional* class like this:

如果你正在使用[Java 8][java8]，你可以使用这个非常棒的[Optional][optional]新类型。如果一个值不确定是否需要显示，就可以把它放到一个*Optional*类里边：

```java
public class FooWidget {
    private final String data;
    private final Optional<Bar> bar;

    public FooWidget(String data) {
        this(data, Optional.empty());
    }

    public FooWidget(String data, Optional<Bar> bar) {
        this.data = data;
        this.bar = bar;
    }

    public Optional<Bar> getBar() {
        return bar;
    }
}
```

So now it's clear that *data* will never be null, but *bar* may or may not be
present. *Optional* has methods like *isPresent*, which may make it feel like
not a lot is different from just checking *null*. But it allows you to write
statements like:

所以现在就很明确了，*data*永远不可能是null，但是*bar*可能显示出来也可能不显示。*Optional*有一些像*isPresent*的方法，可以让它感觉很大不同，就不只是检查*null*了。但是它也允许你写一些这样的语句：

```java
final Optional<FooWidget> fooWidget = maybeGetFooWidget();
final Baz baz = fooWidget.flatMap(FooWidget::getBar)
                         .flatMap(BarWidget::getBaz)
                         .orElse(defaultBaz);
```

Which is much better than chained if null checks. The only downside of using
Optional is that the standard library doesn't have good Optional support, so
dealing with nulls is still required there.

这比链式的null检查好多了。唯一的缺点是标准库还没有很好地支持Optional的使用，所以
处理空值依然是有必要的。