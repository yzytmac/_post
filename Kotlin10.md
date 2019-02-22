---
title: Kotlin教程10---集合和函数操作符
date: 2018-01-28 14:37:03
tags: Kotlin
categories: Kotlin教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517214609323&di=40d0cb3d0cacdcc718de20dccb81fa6d&imgtype=0&src=http%3A%2F%2Fimgup01.sj88.com%2F2017-06%2F30%2F01%2F1498755765289_0.jpg
---
集合和函数操作符
在我们这个项目我们已经使用过集合了,但是现在是时候展示它们结合函数操作符
之后有多强大了。关于函数式编程很不错的一点是我们不用去解释我们怎么去做,
而是直接说我想做什么。  
比如,如果我想去过滤一个list,不用去创建一个list,遍
历这个list的每一项,然后如果满足一定的条件则放到一个新的集合中,而是直接使
用filer函数并指明我想用的过滤器。用这种方式,我们可以节省大量的代码。
虽然我们可以直接用Java中的集合,但是Kotlin也提供了一些你希望用的本地的接口:
```kotlin
Iterable:父类。所有我们可以遍历一系列的都是实现这个接口。
MutableIterable:一个支持遍历的同时可以执行删除的Iterables。
Collection:这个类相是一个范性集合。我们通过函数访问可以返回集合的size、是否为空、是否包含一个或者一些item。这个集合的所有方法提供查询,因为connections是不可修改的。
MutableCollection:一个支持增加和删除item的Collection。它提供了额外的函数,比如add、remove、clear等等。
List:可能是最流行的集合类型。它是一个范性有序的集合。因为它的有序,我们可以使用get函数通过position来访问。
MutableList:一个支持增加和删除item的List。
Set:一个无序并不支持重复item的集合。
MutableSet:一个支持增加和删除item的Set。
Map:一个key-value对的collection。key在map中是唯一的,也就是说不能有两对key是一样的键值对存在于一个map中。
MutableMap:一个支持增加和删除item的map。
```
有很多不同集合可用的函数操作符。我想通过一个例子来展示给你看。知道有哪些可选的操作符是很有用的,因为这样会更容易分辨它们使用的时机。
```kotlin
//生成list操作符
    val list = listOf(1, 2, 3, 4, 5, 6)

//any
//如果至少有一个元素符合给出的判断条件,则返回true。
    list.any { it % 2 == 0 }
    list.any { it > 10 }
//all
//如果全部的元素符合给出的判断条件,则返回true。
    list.all { it < 10 }
    list.all { it % 2 == 0 }
//count
//返回符合给出判断条件的元素总数。
    list.count { it % 2 == 0 }
//fold
//在一个初始值的基础上从第一项到最后一项通过一个函数累计所有的元素。
    list.fold(4) { init, next -> init + next }//init就是4
//foldRight与fold一样,但是顺序是从最后一项到第一项。
    list.foldRight(4) { total, next -> total + next }
//forEach
//遍历所有元素,并执行给定的操作。
    list.forEach { println(it) }
//forEachIndexed与forEach一样,但是我们同时可以得到元素的index。
    list.forEachIndexed { index, value -> println("position	$index contains a $value") }
//max
//返回最大的一项,如果没有则返回null。
    list.max()
//maxBy
//根据给定的函数返回最大的一项,如果没有则返回null。
    list.maxBy { Math.abs(it) }//返回绝对值最大的
//min
//返回最小的一项,如果没有则返回null。
    list.min()
//114总数操作符
//minBy
//根据给定的函数返回最小的一项,如果没有则返回null。
//	The	element	whose	negative	is	smaller
    list.minBy{ Math.abs(it) }
//none
//如果没有任何元素与给定的函数匹配,则返回true。
    list.none { it % 7 == 0 }
//reduce与fold一样,但是没有一个初始值。通过一个函数从第一项到最后一项进行累计。
    list.reduce{ total, next -> total + next }
//reduceRight与reduce一样,但是顺序是从最后一项到第一项。
    list.reduceRight{total, next ->total + next }
//sumBy
//返回所有每一项通过函数转换之后的数据的总和。
    list.sumBy{ it % 2 }
//过滤操作符
//drop
//返回包含去掉前n个元素的所有元素的列表。
    list.drop(4)
//dropWhile
//返回根据给定函数从第一项开始去掉指定元素的列表。
    list.dropWhile{ it < 3 }
//dropLastWhile
//返回根据给定函数从最后一项开始去掉指定元素的列表。
    list.dropLastWhile{ it > 4 }
//filter
//过滤所有符合给定函数条件的元素。
    list.filter{ it % 2 == 0 }
//filterNot
//过滤所有不符合给定函数条件的元素。
    list.filterNot{ it % 2 == 0 }
//filterNotNull
//过滤所有元素中不是null的元素。
    list.filterNotNull()
//slice
//过滤一个list中指定index的元素。
    list.slice(listOf(1, 3, 4))
//take
//返回从第一个开始的n个元素。
    list.take(2)
//takeLast
//返回从最后一个开始的n个元素
    list.takeLast(2)
//takeWhile
//返回从第一个开始符合给定函数条件的元素。
    list.takeWhile{ it < 3 }
//映射操作符
//flatMap
//遍历所有的元素,为每一个创建一个集合,最后把所有的集合放在一个集合中。
    list.flatMap { listOf(it, it + 1) }
//groupBy
//返回一个根据给定函数分组后的map。
    list.groupBy{ if (it % 2 == 0) "even" else "odd" }
//map
//返回一个每一个元素根据给定的函数转换所组成的List。
    list.map    { it * 2 }
//mapIndexed
//返回一个每一个元素根据给定的包含元素index的函数转换所组成的List。
    list.mapIndexed{index, it->index*it}
//mapNotNull
//返回一个每一个非null元素根据给定的函数转换所组成的List。
    list.mapNotNull{it * 2 }
//120元素操作符
//元素操作符
//contains
//如果指定元素可以在集合中找到,则返回true。
    list.contains(2)
//elementAt
//返回给定index对应的元素,如果index数组越界则会抛 出 IndexOutOfBoundsException 。
    list.elementAt(1)
//elementAtOrElse
//返回给定index对应的元素,如果index数组越界则会根据给定函数返回默认值。
    list.elementAtOrElse(10,{ 2 * it })
//elementAtOrNull
//返回给定index对应的元素,如果index数组越界则会返回null。
    list.elementAtOrNull(10)
//first
//返回符合给定函数条件的第一个元素。
    list.first{ it % 2 == 0 }
//firstOrNull
//返回符合给定函数条件的第一个元素,如果没有符合则返回null。
    list.firstOrNull { it % 7 == 0 }
//indexOf
//返回指定元素的第一个index,如果不存在,则返回-1。
    list.indexOf(4)
//indexOfFirst
//返回第一个符合给定函数条件的元素的index,如果没有符合则返回-1。
    list.indexOfFirst{ it % 2 == 0 }
//indexOfLast
//返回最后一个符合给定函数条件的元素的index,如果没有符合则返回-1。
    list.indexOfLast{ it % 2 == 0 }
//last
//返回符合给定函数条件的最后一个元素。
    list.last{ it % 2 == 0 }
//lastIndexOf
//返回指定元素的最后一个index,如果不存在,则返回-1。
    list.lastIndexOf(1)
//lastOrNull
//返回符合给定函数条件的最后一个元素,如果没有符合则返回null。
    list.lastOrNull { it % 7 == 0 }
//single
//返回符合给定函数的单个元素,如果没有符合或者超过一个,则抛出异常。
    list.single{ it % 5 == 0 }
//singleOrNull
//返回符合给定函数的单个元素,如果没有符合或者超过一个,则返回null。
    list.singleOrNull { it % 7 == 0 }
//生产操作符
//merge
//把两个集合合并成一个新的,相同index的元素通过给定的函数进行合并成新的元素作为新的集合的一个元素,返回这个新的集合。新的集合的大小由最小的那个集合大小决定。
    val listRepeated = listOf(2, 2, 3, 4, 5, 5, 6)
//    list.merge(listRepeated){ it1, it2 -> it1 + it2 }
//partition
//把一个给定的集合分割成两个,第一个集合是由原集合每一项元素匹配给定函数条
//件返回true的元素组成,第二个集合是由原集合每一项元素匹配给定函数条件返回false的元素组成。
    list.partition { it % 2 == 0 }
//plus
//返回一个包含原集合和给定集合中所有元素的集合,因为函数的名字原因,我们可 以使用+操作符。
    list + listOf(7, 8)
//zip
//返回由pair组成的List,每个pair由两个集合中相同index的元素组成。这个返回的List的大小由最小的那个集合决定。
    list.zip(listOf(7, 8))
//unzip
//从包含pair的List中生成包含List的Pair。
    listOf(Pair(5, 7), Pair(6, 8)).unzip()
//顺序操作符
//reverse
//返回一个与指定list相反顺序的list。
    list.reversed()
//sort
//返回一个自然排序后的list。
    list.sorted()
//sortBy
//返回一个根据指定函数排序后的list。
    list.sortedBy { it % 3 }
//sortDescending
//返回一个降序排序后的List。
    list.sortedDescending()
//sortDescendingBy
//返回一个根据指定函数降序排序后的list。
    list.sortedByDescending { it % 3 }
```