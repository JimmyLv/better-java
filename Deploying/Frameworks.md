## Frameworks

Because deploying Java isn't easy, frameworks have been made which can help.
Two of the best are [Dropwizard][dropwizard] and [Spring Boot][springboot].
The [Play framework][play] can also be considered one of these deployment
frameworks as well.

由于部署Java不是那么容易，框架就被开发出来用于协助。其中最好的两个框架就是[Dropwizard][dropwizard]和[Spring Boot][springboot]，还有[Play框架][play]也可以被当做一种部署框架。

All of them try to lower the barrier to getting your code out the door.
They're especially helpful if you're new to Java or if you need to get things
done fast. Single JAR deployments are just easier than complicated WAR or EAR
deployments.

他们都尝试降低门槛，以便于你家的「代码」得以出嫁。它们对Java新手尤其有用，或者是你需要快速完成目标。单个JAR的部署确实会比复杂的WAR或者EAR部署更加容易。

However, they can be somewhat inflexible and are rather opinionated, so if
your project doesn't fit with the choices the developers of your framework
made, you'll have to migrate to a more hand-rolled configuration.

然而，他们也会有点儿不够灵活，更准确地说很死板，所以如果你的项目跟框架作者的选择不一致的话，你就不得不转移到更多的手动配置上去。

[dropwizard]: https://dropwizard.github.io/dropwizard/
[springboot]: http://projects.spring.io/spring-boot/
[play]: http://www.playframework.com/
