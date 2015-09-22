## Formatting 格式化

Formatting is so much less important than most programmers make it out to be.
Does consistency show that you care about your craft and does it help others
read? Absolutely. But let's not waste a day adding spaces to if blocks so that
it "matches".

大多数程序员都觉得格式化是那么地不重要。（-。-）保持一致性表明了你对技术的在乎以及帮助他人阅读代码吗？当然。但是让我们不再浪费一整天时间去添加空格，以便于代码块可以「匹配」。

If you absolutely need a code formatting guide, I highly recommend
[Google's Java Style][googlestyle] guide. The best part of that guide is the
[Programming Practices][googlepractices] section. Definitely worth a read.

如果你极其想要一个代码格式化手册，我强烈推荐[Google的Java代码风格][googlestyle]指南。该指南最好的部分就是[编程实践][googlepractices]那一节，非常值得一读。

### Javadoc Java文档

Documenting your user facing code is important. And this means
[using examples][javadocex] and using sensible descriptions of variables,
methods, and classes.

文档化你的用户使用代码是非常重要的。这意味着[使用例子][javadocex]和使用恰当的变量、方法和类的描述。

The corollary of this is to not document what doesn't need documenting. If you
don't have anything to say about what an argument is, or if it's obvious,
don't document it. Boilerplate documentation is worse than no documentation at
all, as it tricks your users into thinking that there is documentation.

这样做的结果不是说要将本来不必要的内容也文档化。如果你对于这个变量没有任何内容想说的，或者它非常明显，那就不要文档化。样板式的文档比完全没有文档更加糟糕，因为这对你的用户来说会误以为这有个文档。
