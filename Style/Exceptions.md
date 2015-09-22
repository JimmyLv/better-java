## Exceptions 异常

[Checked exceptions][checkedex] should be used with caution, if at all. They 
force your users to add many try/catch blocks and wrap your exceptions in their 
own. Better is to make your exceptions extend RuntimeException instead. This 
allows your users to handle your exceptions in the way they would like, rather 
than forcing them to handle/declare that it throws every time, which pollutes 
the code.

One nitfy trick is to put RuntimeExceptions in your method's throws declaration.
This has no effect on the compiler, but will inform your users via documentation
that these exceptions can be thrown.

如果真的需要[检查异常][checkedex]，也应当谨慎使用。他们将强迫你的用户添加try/catch代码块去把你的异常包裹起来。更好的方式是将你的异常继承自RuntimeException。这可以允许你的用户可以使用他们喜欢的方式处理异常，而不是强迫他们去处理/声明每一次所抛出的异常，这简直就是污染代码。

另一个需要注意的小技巧就是将RuntimeExceptions放到你的函数抛出声明里（-。-）。这对编译器没有任何影响，但是却可以通知你的用户可以通过文档知道哪些异常可以被抛出。
