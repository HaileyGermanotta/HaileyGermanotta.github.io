# sicp 阅读笔记（一）

什么是 flexibility？

> The best systems are evolvable: they can be adapted to new situations with only minor modification. How can we design systems that are flexible in this way?

什么是 additive programming？

> One should not have to modify a working program. One should be able to add to it to implement new functionality or to adjust old functions for new requirements. We call this additive programming.

如何提高 flexibility？

> One strategy for enhancing flexibility, which should be familiar to many programmers, is generic dispatch.

看的时候觉得云里雾里，因为很多术语不熟悉，比如 DSL，additive programming, generic dispatch...

然后我去搜索了 DSL 相关，看到一篇讲关于前端 DSL 的。折腾了一番，我感觉我还是先看 sicp 吧。（sdff 里面用的是 scheme，scheme 和 lisp 的关系？）

sicp 里面用到的是 lisp 语言，所以我决定先学一下 lisp，然后我装了 lisp 的解释器 SBCL（因为它免费），一开始装的时候装错包了导致怎么运行都没有反应。装了解释器之后，一个 node 和 python 带来的习惯就是，直接运行某一个 lisp 脚本，那么要如何运行呢？

```shell
sbcl --script [filename].lisp
```

这样就可以运行 lisp 脚本了

```lisp
(+ 1 2)
(define size 2)
```
