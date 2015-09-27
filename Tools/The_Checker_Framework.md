## The Checker Framework Checker框架

Java's type system is pretty weak. It doesn't differentiate between Strings
and Strings that are actually regular expressions, nor does it do any
[taint checking][taint]. However, [the Checker Framework][checker]
does this and more.

Java的类型系统非常脆弱。它不能区分字符串和字符串正则表达式，也不可以做任何的[污染检查][taint]。然而，[Checker框架]可以用来做这个。

It uses annotations like *@Nullable* to check types. You can even define
[your own annotations][customchecker] to make the static analysis done even
more powerful.

使用类似于*@Nullable*这样的注解来检查类型。你甚至可以定义[自己的注解][customchecker]来加强静态分析。

[taint]: http://en.wikipedia.org/wiki/Taint_checking
[checker]: http://types.cs.washington.edu/checker-framework/
[customchecker]: http://types.cs.washington.edu/checker-framework/tutorial/webpages/encryption-checker-cmd.html

