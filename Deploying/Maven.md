## Maven

**Good alternative**: [Gradle][gradle].

更好的选择：[Gradle][gradle]。

Maven is still the standard tool to build, package, and run your tests. There
are alternatives, like Gradle, but they don't have the same adoption that Maven
has. If you're new to Maven, you should start with
[Maven by Example][mavenexample].

Maven依旧是用于构建、打包和运行测试的标准工具。这儿也有些替代品，比如Gradle，但是他们不像Maven被采用得那样广泛。如果你是一个Maven新手，可以从[Maven by Example][mavenexample]开始。

I like to have a root POM with all of the external dependencies you want to
use. It will look something [like this][rootpom]. This root POM has only one
external dependency, but if your product is big enough, you'll have dozens.
Your root POM should be a project on its own: in version control and released
like any other Java project.

我喜欢让所有想要使用的外部依赖继承自一个根POM，就像[这样][rootpom]。根POM只有一个外部依赖，但是如果你的项目足够大，你也可以有很多。你的根POM应该有一个项目的样子：就像其他Java项目那样通过版本控制和发布。

If you think that tagging your root POM for every external dependency change
is too much, you haven't wasted a week tracking down cross project dependency
errors.

如果你觉得每个外部依赖都对你的根POM标注产生太多改变了，你就还没有过浪费一周的时间用来跟踪跨项目间依赖错误的经历。「too young too native？」

All of your Maven projects will include your root POM and all of its version
information.  This way, you get your company's selected version of each
external dependency, and all of the correct Maven plugins. If you need to pull
in external dependencies, it works just like this:

所有Maven项目将会包括你的根POM以及自己的版本信息。这样的话，你就可以为每个外部依赖指定公司所选择的版本，以及所有的Maven插件。如果你需要引入外部依赖，这样就可以了：

```xml
<dependencies>
    <dependency>
        <groupId>org.third.party</groupId>
        <artifactId>some-artifact</artifactId>
    </dependency>
</dependencies>
```

If you want internal dependencies, that should be managed by each individual
project's **<dependencyManagement>** section. Otherwise it would be difficult
to keep the root POM version number sane.

如果你想要内部依赖，也可以通过每个独立项目的**<dependencyManagement>**部分来管理。否则将会让维护POM版本号变得非常困难。

### Dependency Convergence 依赖收敛

One of the best parts about Java is the massive amount of third party
libraries which do everything. Essentially every API or toolkit has a Java SDK
and it's easy to pull it in with Maven.

Java最好的一部分就是拥有大量无所不能的第三方库。本质上每个API或者工具包都有一套Java SDK，而且通过Maven可以非常容易引入。

And those Java libraries themselves depend on specific versions of other
libraries. If you pull in enough libraries, you'll get version conflicts, that
is, something like this:

这些Java库都依赖于其他特定版本的库。如果你引入了一定量的库之后，就会发现一些版本冲突，先这样：

    Foo library depends on Bar library v1.0
    Widget library depends on Bar library v0.9

Which version will get pulled into your project?

那么到底哪个版本会引入到项目之中呢？

With the [Maven dependency convergence plugin][depconverge], the build will
error if your dependencies don't use the same version. Then, you have two
options for solving the conflict:

通过Maven的依赖收敛插件，如果你的依赖可以使用正确的版本的话build就会报错。然后，你有两种选择可以解决冲突：

1. Explicitly pick a version for Bar in your *dependencyManagement* section
2. Exclude Bar from either Foo or Widget

1. 在*dependencyManagement*部分为你的Bar明确指定一个版本。
2. 从Foo或者Widget中排除掉Bar。

The choice of which to choose depends on your situation: if you want to track
one project's version, then exclude makes sense. On the other hand, if you
want to be explicit about it, you can pick a version, although you'll need to
update it when you update the other dependencies.

至于到底选择那种取决于你的具体情况：如果你想要追踪项目的版本，排除它会比较有意义。而另一方面，如果你需要明确指定对这个库的版本，你就可以挑选一个版本，不过当你升级其他依赖的时候就需要亲自更新它。


[gradle]: http://www.gradle.org/
[mavenexample]: http://books.sonatype.com/mvnex-book/reference/index.html
[depconverge]: https://maven.apache.org/enforcer/enforcer-rules/dependencyConvergence.html
[rootpom]: https://gist.github.com/cxxr/10787344
