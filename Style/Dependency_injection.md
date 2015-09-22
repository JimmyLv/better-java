## Dependency injection 依赖注入

This is more of a software engineering section than a Java section, but one of
the best ways to write testable software is to use [dependency injection][di]
(DI). Because Java strongly encourages OO design, to make testable software,
you need to use DI.

这部分更像是谈论软件工程而不仅仅是Java，但是编写可测试软件的最佳方法之一就是使用[依赖注入][di]（DI）。因为Java非常推崇面向对象设计来保持软件的可测试性，你需要使用DI。

In Java, this is typically done with the [Spring Framework][spring]. It has a
either code-based wiring or XML configuration-based wiring. If you use the XML
configuration, it's important that you [don't overuse Spring][springso] because
of its XML-based configuration format.  There should be absolutely no logic or
control structures in XML. It should only inject dependencies.

在Java里，实现DI的典型例子就是[Spring框架](spring)。它既可以基于代码来装配，也可以基于XML文件来进行配置。如果使用XML配置的话，非常重要的一点就是[不要滥用Spring][springso]，因为基于XML配置的格式问题。很显然不能够在XML里面放有任何逻辑或者控制结构，它仅仅用于注入依赖。

Good alternatives to using Spring is Google and Square's [Dagger][dagger]
library or Google's [Guice][guice]. They don't use Spring's XML
configuration file format, and instead they put the injection logic in
annotations and in code.

使用Spring的另一种选择是Google和Square的[Dagger][dagger]库或者是Google的[Guice][guice]。他们不会使用Spring的XML配置文件格式，而是将注入逻辑放在代码的注解里面。
