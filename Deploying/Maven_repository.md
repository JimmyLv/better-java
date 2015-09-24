## Maven repository Maven仓库

You need a place to put your JARs, WARs, and EARs that you make, so you'll
need a repository.

你需要一个地方来存放你所创造的JARs、WARs和EARs，所以你就需要一个仓库。

Common choices are [Artifactory][artifactory] and [Nexus][nexus]. Both work,
and have their own [pros and cons][mavenrepo].

常见的一些选择是[Artifactory][artifactory]和[Nexus][nexus]。它们都可以工作，并且有自己的[pros and cons][mavenrepo]。

You should have your own Artifactory/Nexus installation and
[mirror your dependencies][artifactorymirror] onto it. This will stop your
build from breaking because some upstream Maven repository went down.

你应该要有自己的Artifactory/Nexus设置，用于存放[依赖镜像][artifactorymirror]。这可以让你的build在Maven上游仓库挂掉的时候免于崩溃。

[nexus]: http://www.sonatype.com/nexus
[artifactory]: http://www.jfrog.com/
[mavenrepo]: http://stackoverflow.com/questions/364775/should-we-use-nexus-or-artifactory-for-a-maven-repo
[artifactorymirror]: http://www.jfrog.com/confluence/display/RTF/Configuring+Artifacts+Resolution
