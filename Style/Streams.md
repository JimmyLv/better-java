## Streams 流

[Java 8][java8] has a nice [stream][javastream] and lambda syntax. You could
write code like this:

[Java 8][java8]有了一个非常漂亮的[stream][javastream]和lambda语法。你可以这样编码了：

```java
final List<String> filtered = list.stream()
    .filter(s -> s.startsWith("s"))
    .map(s -> s.toUpperCase())
    .collect(Collectors.toList());
```

Instead of this:

而不是：

```java
final List<String> filtered = new ArrayList<>();
for (String str : list) {
    if (str.startsWith("s") {
        filtered.add(str.toUpperCase());
    }
}
```

This allows you to write more fluent code, which is more readable.

这可以让你写出更加流畅的代码，而且更加可读。

[java8]: http://www.java8.org/
[javastream]: http://blog.hartveld.com/2013/03/jdk-8-33-stream-api.html
