## Testing

Testing is critical to your software. These packages help make it easier.

测试对于软件来说非常重要，这些包可以使之变得更加容易。

### jUnit 4

[jUnit][junit] needs no introduction. It's the standard tool for unit testing
in Java.

[jUnit][junit]无需再做介绍，它已经是Java中的标准单元测试工具了。

But you're probably not using jUnit to its full potential. jUnit supports
[parametrized tests][junitparam], [rules][junitrules] to stop you from writing
so much boilerplate, [theories][junittheories] to randomly test certain code,
and [assumptions][junitassume].

但是你有可能发挥出jUnit的全部潜能。jUnit支持[参数化的测试]][junitparam]、让你免于编写过多的样板文件的[规则][junitrules]、随机测试确定代码的[理论][junittheories]，以及[假设]][junittheories]

### jMock

If you've done your dependency injection, this is where it pays off: mocking
out code which has side effects (like talking to a REST server) and still
asserting behavior of code that calls it.

如果你已经完成了依赖注入，那么这里就有一个陷阱（-。-）：Mock出具有副作用的代码（就像REST服务里所说的那样）和依然判断所调用代码的行为。

[jMock][jmock] is the standard mocking tool for Java. It looks like this:

[jMock][jmock]是用于Java的标准Mock工具，像这样：

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

这里通过[jMock][jmock]设置了一个*FooWidgetDependency*，然后添加了一些预期行为。我们期望*dep*的*call*方法就会和字符串一样至少被调用一次，*dep*的*optionalCall*方法则可以被调用0次或者更多次。

If you have to set up the same dependency over and over, you should probably
put that in a [test fixture][junitfixture] and put *assertIsSatisfied* in an
*@After* fixture.

如果你不得不反复设置同样的依赖，也许你就可以讲它放到一个[测试fixture][junitfixture]，然后将*assertIsSatisfied*放到一个*@After*fixture里。

### AssertJ

Do you ever do this with jUnit?

你真的会用jUnit这样做？

```java
final List<String> result = some.testMethod();
assertEquals(4, result.size());
assertTrue(result.contains("some result"));
assertTrue(result.contains("some other result"));
assertFalse(result.contains("shouldn't be here"));
```

This is just annoying boilerplate. [AssertJ][assertj] solves this. You can
transform the same code into this:

这就是非常讨厌的一种样板，[AssertJ][assertj]可以解决它，你可以将同样的代码改成这样：

```java
assertThat(some.testMethod()).hasSize(4)
                             .contains("some result", "some other result")
                             .doesNotContain("shouldn't be here");
```

This fluent interface makes your tests more readable. What more could you want?

流畅的接口可以让你的测试更具有可读性，夫复何求？

[junit]: http://junit.org/
[junitparam]: https://github.com/junit-team/junit/wiki/Parameterized-tests
[junitrules]: https://github.com/junit-team/junit/wiki/Rules
[junittheories]: https://github.com/junit-team/junit/wiki/Theories
[junitassume]: https://github.com/junit-team/junit/wiki/Assumptions-with-assume
[jmock]: http://jmock.org/
[junitfixture]: https://github.com/junit-team/junit/wiki/Test-fixtures
[assertj]: http://joel-costigliola.github.io/assertj/index.html
