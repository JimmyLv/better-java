## Continuous Integration 持续集成

Obviously you need some kind of continuous integration server which is going
to continuously build your SNAPSHOT versions and tag builds based on git tags.

很显然，你需要集中持续集成服务，用来持续构建你的SNAPSHOT版本，并且基于git标签进行构建。

[Jenkins][jenkins] and [Travis-CI][travis] are natural choices.

[Jenkins][jenkins]和[Travis-CI][travis]就是非常适合的选择。

Code coverage is useful, and [Cobertura][cobertura] has
[a good Maven plugin][coberturamaven] and CI support. There are other code
coverage tools for Java, but I've used Cobertura.

测试覆盖率非常有用，[Cobertura][cobertura]就有一个非常好的[Maven插件][coberturamaven]和CI支持。当然也有其他的Java测试覆盖率工具，但是我一直在用Cobertura。

[jenkins]: http://jenkins-ci.org/
[travis]: https://travis-ci.org/
[cobertura]: http://cobertura.github.io/cobertura/
[coberturamaven]: http://mojo.codehaus.org/cobertura-maven-plugin/usage.html