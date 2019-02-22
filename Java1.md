---
title: Java教程1---Java8特性1
date: 2018-01-28 14:37:03
tags: Java
categories: Java教程
thumbnail: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1517576446704&di=fec11781d6709c0abfdc441d3d8f06bb&imgtype=0&src=http%3A%2F%2F5b0988e595225.cdn.sohucs.com%2Fimages%2F20170731%2F10bfc5ca926b46c4ab04734be177ebc6.jpeg
---
### 虽然Java9都出来很久了，但是企业用的最多的基本还是Java7，所以Java8还是有必要了解的。  
RXJava是个非常火的框架，但我刚开始学的时候对他的链式表达式不是很了解，尤其是 **map、filter**等操作符特别不理解，因为 **map**关键字在Java中是一个集合，是键值对呀，因为当时还没学过Java8和kotlin，所以很难理解，现在Java8中就有这样的表达式，所以先从Java8学起，学完之后再去看RXJava就会觉得so easy。

## Java8新特性1---StreamApi  

操作步骤（必须有创建和终止两步，没有终止的话中间操作是不会执行的）  
一、创建 Stream  
用一个数据源（如： 集合、数组）来创建获取一个流，有四种创建方式
1. 集合提供了两个方法  stream() 与 parallelStream()
```java
List<String> list = new ArrayList<>();
Stream<String> stream = list.stream(); //获取一个顺序流、串行流
Stream<String> parallelStream = list.parallelStream(); //获取一个并行流
```
		
2. 通过 Arrays 中的 静态方法stream() 获取一个数组流
```java
Integer[] nums = new Integer[10];
Stream<Integer> stream1 = Arrays.stream(nums);
```
3. 通过 Stream 类中静态方法 of()
```java
Stream<Integer> stream2 = Stream.of(1,2,3,4,5,6);
```
4. 用函数创建无限流
```java
//迭代
Stream<Integer> stream3 = Stream.iterate(0, (x) -> x + 2).li(10);
stream3.forEach(System.out::println);
//生成
Stream<Double> stream4 = Stream.generate(Math::random).limit(2);
stream4.forEach(System.out::println);
```
二、中间操作  
一个中间操作链，对数据源的数据进行处理。中间操作这些都属于链式操作，返回的还是stream对象。
1. 筛选与切片
```java
	filter(p)——接收 Lambda ， 从流中排除某些元素。
	limit(n)——截断流，获取前n个
	skip(n) ——跳过元素，返回一个扔掉了前 n 个元素的流。若流中元素不足 n 个，则返回一个空流。与 limit(n) 互补
	distinct——筛选，通过流所生成元素的 hashCode() 和 equals() 去除重复元素
```
2. 映射（转换）尤其要注意参数的类型和返回值类型。具体的转换规则就由函数实现。
```java
map(Function<? super T, ? extends R> mapper);//接收一个函数（或lambda表达式）作为参数，该函数会被应用到每个元素上，并将其映射成一个新的元素。
flatMap(Function<? super T, ? extends Stream<? extends R>> mapper);//功能就是降维。三维集合降成二维集合，二维降成一维。
//如：
ArrayList<ArrayList<String>> list = new ArrayList();//list是一个二维集合
list.stream().flatMap(list2->list2.stream()).forEach(System.out::print);//经过flatMap后会得到一个一维集合list2.
mapToInt(ToIntFunction<? super T> mapper)
mapToLong(ToLongFunction<? super T> mapper);
mapToDouble(ToDoubleFunction<? super T> mapper);
```
3. 排序
```java
sorted();//自然顺序排，字典顺序
sorted(Comparator comp)//按比较器的规则排
```
4. 并行流、串行流
```java
parallel()//并行流，相当于多线程执行，效率非常高。底层采用的是fork-join模式。fork-join就是采用了窃取任务的多线程
sequential()//串行流
```
三、终止操作(终端操作)  
一个终止操作，执行中间操作链，并产生结果
```java
forEach//遍历
allMatch//检查是否匹配所有元素
anyMatch//检查是否至少匹配一个元素
noneMatch//检查是否没有匹配的元素
findFirst//返回第一个元素
findAny//返回当前流中的任意元素
count//返回流中元素的总个数
max//返回流中最大值
min//返回流中最小值
reduce//归约。可以将流中元素反复结合起来，得到一个值。可以结合从1加到100
collect//收集。将流中的某个数据收集起来，再返回一个集合或Optional。参数是Collector接口的实现，用于给Stream中元素做汇总的方法，通常用 Collectors 工具类创建。
```
* 总结  
StreamApi就三个步骤：
    1. 根据数组或集合创建流
    2. 对流进行中间操作
    3. 对流进行终止操作  

其实RXJava也就是这样做的。后面会写一篇博客来讲RXJava。
