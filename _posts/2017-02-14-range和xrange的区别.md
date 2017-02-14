---
layout: post
title: "python学习之 range 和 xrange 的区别"
date: 2017-02-14 
description: "python、基础、笔试面试"
tag: python
---  

## 序列中的数字序列range类型
便捷的range()函数  
range 也是一种类型（type），它是一个数字的序列（sequence of numbers），而且是不可变的，通常用在for循环中。  

    class range(stop)
    class range(start, stop [, step])

对于第一种构造方式，start默认值为0，step默认值为1。  
当step为正时，一个range的元素值为r[i] = start + i * step 且 r[i] < stop； step为负时，r[i] > stop。  

    >>> range(6)
    [0, 1, 2, 3, 4, 5]
    >>> tuple(range(0,-10,-2))
    (0, -2, -4, -6, -8)
    >>> 

使用python的人都知道range()函数很方便，下面再介绍一些用法。  

    >>> range(1,5) #代表从1到5(不包含5)
    [1, 2, 3, 4]
    >>> range(1,5,2) #代表从1到5，间隔2(不包含5)
    [1, 3]
    >>> range(5) #代表从0到5(不包含5)
    [0, 1, 2, 3, 4]

再回顾一下，看看list的操作：  

    array = [1, 2, 5, 3, 6, 8, 4]
    #其实这里的顺序标识是
    [1, 2, 5, 3, 6, 8, 4]
    (0，1，2，3，4，5，6)
    (-7,-6,-5,-4,-3,-2,-1)
     
    >>> array[0:] #列出0以后的
    [1, 2, 5, 3, 6, 8, 4]
    >>> array[1:] #列出1以后的
    [2, 5, 3, 6, 8, 4]
    >>> array[:-1] #列出-1之前的
    [1, 2, 5, 3, 6, 8]
    >>> array[3:-3] #列出3到-3之间的
    [3]

那么两个[::]会是什么样子呢？  

    >>> array[::2] #o以后隔1个取一个
    [1, 5, 6, 4]
    >>> array[2::] #列出2以后的
    [5, 3, 6, 8, 4]
    >>> array[::3] #o以后隔2个取一个
    [1, 3, 4]
    >>> array[::4] #o以后隔3个取一个
    [1, 6] 
    如果想让他们颠倒形成reverse函数的效果
    >>> array[::-1]
    [4, 8, 6, 3, 5, 2, 1]
    >>> array[::-2]
    [4, 6, 5, 1]

差不多了解的话，再试图了解用 Python 实现冒泡排序吧（循环）：  

    array = [1, 2, 5, 3, 6, 8, 4]
    for i in range(len(array) - 1, 0, -1):
        print i
        for j in range(0, i):
            print j
            if array[j] > array[j + 1]:
                array[j], array[j + 1] = array[j + 1], array[j]
    print array

1.line 1：array = [1, 2, 5, 3, 6, 8, 4]一个乱序的list没什么好解释的  

2.line 2：for i in range(len(array) - 1, 0, -1):这就是上边给的例子的第二条，我们替换下就成为range(6,1,-1)，意思是从6到1间隔-1,也就是倒序的range(2,7,1),随后把这些值循环赋给i，那么i的值将会是[6, 5, 4, 3, 2]  

3.line 3：for j in range(0, i):这是一个循环赋值给j，j的值将会是[0, 1, 2, 3, 4, 5][0, 1, 2, 3, 4][0, 1, 2, 3][0, 1, 2][0, 1]  

4.那么上边两个循环嵌套起来将会是  

    i----6
    j----0,j----1,j----2,j----3,j----4,j----5
    i----5
    j----0,j----1,j----2,j----3,j----4
    i----4
    j----0,j----1,j----2,j----3
    i----3
    j----0,j----1,j----2
    i----2
    j----0,j----1

5.line 4：if array[j] > array[j + 1]:  

    >>> array = [1, 2, 5, 3, 6, 8, 4]
    >>> array[0]
    1
    >>> array[1]
    2
    >>> array[2]
    5
    >>> array[3]
    3
    >>> array[4]
    6
    >>> array[5]
    8
    >>> array[6]
    4

其实就是使用这个把这个没有顺序的array = [1, 2, 5, 3, 6, 8, 4]排序。  

6.line 5：array[j], array[j + 1] = array[j + 1], array[j] 替换赋值  
7.line 6：打印出来

## Python xrange与range的区别  
返回的结果不一样
range 前面小节已经说明了，range([start,] stop[, step])，根据start与stop指定的范围以及step设定的步长，生成一个序列。  
    比如：

    >>> range(5) 
    [0, 1, 2, 3, 4] 
    >>> range(1,5) 
    [1, 2, 3, 4] 
    >>> range(0,6,2)
    [0, 2, 4]

**xrange 用法与 range 完全相同，所不同的是生成的不是一个list对象，而是一个生成器。**  

    >>> xrange(5)
    xrange(5)
    >>> list(xrange(5))
    [0, 1, 2, 3, 4]
    >>> xrange(1,5)
    xrange(1, 5)
    >>> list(xrange(1,5))
    [1, 2, 3, 4]
    >>> xrange(0,6,2)
    xrange(0, 6, 2)
    >>> list(xrange(0,6,2))
    [0, 2, 4]

由上面的示例可以知道：要生成很大的数字序列的时候，用xrange会比range性能优很多，因为不需要一上来就开辟一块很大的内存空间。  

xrange 和 range 这两个基本上都是在循环的时候用。  

    for i in range(0, 100): 
        print i 

    for i in xrange(0, 100): 
        print i 

这两个输出的结果都是一样的，实际上有很多不同，range会直接生成一个list对象：  

    a = range(0,100) 
    print type(a) 
    print a 
    print a[0], a[1] 

输出结果：

    <type 'list'>
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
    0 1

而xrange则不会直接生成一个list，而是每次调用返回其中的一个值：  

    a = xrange(0,100) 
    print type(a) 
    print a 
    print a[0], a[1] 

输出结果：  

    <type 'xrange'>
    xrange(100)
    0 1

所以xrange做循环的性能比range好，尤其是返回很大的时候。尽量用xrange吧，除非你是要返回一个列表。  

总结一下：  

1、range()返回整个list。  

2、xrange()返回的是一个xrange object，且这个对象是个iterable。  

3、两者都用与for循环。  

4、xrange()占用更少的内存空间，因为循环时xrange()只生成当前的元素，不像range()一开始就成生成完整的list。  

这就是在Python 2里range和xrange的相同点和区别。

那么在Python 3里，我们在前面提到了range()被移除了，xrange()被重新命名成了range()。它们之间有区别吗？  

range object在Python里增加了新的attributes，'count', 'index', 'start', 'step', 'stop'，
且能支持slicing。Python 3的range()在xrange()的基础上变得更强大了。具体可见[【Python那些事儿之十】range()和xrange()](http://www.360doc.com/content/17/0214/10/40331896_628878577.shtml)或者查看官方文档







