# 使用unidbg去ollvm虚假分支反混淆

我们的 OLLVM 的在虚假分支混淆的时候，会得到的大量的判断， 但是大量的判断其实从出生的那一刻都没有被真正的被调用过，他只是想消耗你的生命，所以思路也很简单，就是跟汇编代码，跟着真实的情况走一遍。看看哪些汇编代码块是真的被调用了，并且记录下对应的地址，那么就是真实的目标代码， 而其它的代码，直接 nop 掉，然后再反汇编，就是去掉混淆之后的结果

注意：如果你的 so 当中已经有一个

