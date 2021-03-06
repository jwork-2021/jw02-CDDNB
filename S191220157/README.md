# W02

## 任务一

### 1.1 example类图和时序图

类图：![image](https://github.com/jwork-2021/jw02-CDDNB/blob/master/S191220157/example_class.png)

时序图：![image](https://github.com/jwork-2021/jw02-CDDNB/blob/master/S191220157/example_time.png)

### 1.2 example设计理念分析

#### 单例类Geezer：

​	1、用静态私有的成员对象和私有构造函数确保只能创建一个对象爷爷；

​	2、Geezer有私有的Sorter成员对象。采取这样的设计而非Geezer和Sorter相互发送消息的设计，使得排序行为是Geezer发起，并且排序过程的每一步都是Geezer从Sorter处获取信息再发送给葫芦娃Gourd，体现了爷爷对葫芦娃排序的“指挥”性，理解上更为自然。

#### 采用Linable接口的枚举类Gourd：

​	1、储存自身颜色、位置信息，用final关键字修饰颜色信息保证不能更改；

​	2、采用Linable接口，实现对Gourd方法甚至对象的抽象，便于其他涉及位置和值的对象被使用时复用其他代码。这是为了作业任务二三部分妖怪排序而做的考虑，对任务一只涉及葫芦娃一种对象的情况并无裨益;

​	3、Gourd有方法swapposition，但个人认为换位不是单个Gourd对象应该负责的事，放在Line里更自然。

#### 类Line与类Position：

​	1、Line中定义了一个内置类Position，并用私有Position数组记录Line的每个单位的位次，确保安全性。一开始只觉得把Posiotion作为Line的内置类是符合自然逻辑的，后来发现这样的设计在重写Matrix的时候极为方便，只需替换一个文件，实际上完成了非常良好的封装。

​	2、Position有私有成员对象Linable指示该位置的单位，而Gourd也有私有的Position成员对象记录该单位的位置，每次发生位置交换时两者都要完成更改。第一眼觉得这很合理，因为两次修改是分别针对位置和单位（葫芦娃）的，但后来觉得这是由于Line的存在而带来的冗余。Line对应葫芦娃的队伍，但并不是一个具体的“东西”也不是一个实际的“方法”，既然在排序时仍需在Geezer中用int型数组代替位次来排序，那Line的作用看起来就比较微小了，个人感觉有为了面向对象而抽象之嫌。

#### 接口Sorter与类BubbleSorter：

​	1、Sorter是具体排序方法的抽象接口，可以对需要使用排序功能的类和对象屏蔽排序方法的实现细节，也便于替换/选择不同的排序方法；

​	2、它不能直接改变Gourd的位次信息（包括向Gourd对象发送消息以实现这一点），而是给出一个代表位次信息的int型数组的排序方法。一方面可以理解这是为了方便输出log排序步骤信息，而另一方面效果上不如让Sorter对所需排序的一类对象的抽象进行操作（既完成实际排序，又较大程度满足抽象要求）。



## 任务二

类图：![image](https://github.com/jwork-2021/jw02-CDDNB/blob/master/S191220157/my_line.png)

排序1视频：https://github.com/jwork-2021/jw02-CDDNB/blob/master/S191220157/SelectSorter_64.mov

排序2视频：https://github.com/jwork-2021/jw02-CDDNB/blob/master/S191220157/QuickSorter_64.mov

· 做任务二的时候才体会到示例代码中linable和position，以及Sorter写plan再在Geezer中根据plan排序的看似繁琐的设计在自然逻辑中的对应。是我太年轻了。

## 任务三

类上并未做修改，类图同任务二。

排序1视频：https://github.com/jwork-2021/jw02-CDDNB/blob/master/S191220157/SelectSorter_8_8.mov

排序2视频：https://github.com/jwork-2021/jw02-CDDNB/blob/master/S191220157/QuickSorter_8_8.mov

