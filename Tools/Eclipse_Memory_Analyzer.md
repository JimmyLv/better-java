## Eclipse Memory Analyzer Eclipse内存分析器

Memory leaks happen, even in Java. Luckily, there are tools for that. The best
tool I've used to fix these is the [Eclipse Memory Analyzer][mat]. It takes a
heap dump and lets you find the problem.

哪怕在Java中也可能发生内存泄漏。幸运的是，这儿有些工具来检查。我曾用过的最好的解决工具就是[Eclipse Memory Analyzer][mat]。它可以获取堆内存信息来让你寻找问题所在。

There's a few ways to get a heap dump for a JVM process, but I use
[jmap][jmap]:

又不少方式来从JVM进程中获取对内存信息，但是我选择[jmap][jmap]：

```bash
$ jmap -dump:live,format=b,file=heapdump.hprof -F 8152
Attaching to process ID 8152, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 23.25-b01
Dumping heap to heapdump.hprof ...
... snip ...
Heap dump file created
```

Then you can open the *heapdump.hprof* file with the Memory Analyzer and see
what's going on fast.

然后你就可以通过打开内存分析器打开*heapdump.hprof*文件，迅速查看发生了什么。

[mat]: http://www.eclipse.org/mat/
[jmap]: http://docs.oracle.com/javase/7/docs/technotes/tools/share/jmap.html
