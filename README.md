# dongbei - 东北方言编程语言

* [引言](#引言)
* [系统要求](#系统要求)
* [安装](#安装)
* [你好，世界](#你好世界)
* [语言定义](#语言定义)
  * [词法](#词法)
    * [字符串常量](#字符串常量)
    * [注释](#注释)
    * [分词](#分词)
    * [名字](#名字)
    * [常数](#常数)
  * [语句](#语句)
  * [变量](#变量)
    * [定义变量](#定义变量)
    * [给变量赋值](#给变量赋值)
    * [增减变量](#增减变量)
    * [引用变量](#引用变量)
  * [输出](#输出)
  * [字符串运算](#字符串运算)
  * [算术运算](#算术运算)
  * [比大小](#比大小)
  * [循环](#循环)
  * [讲条件](#讲条件)
  * [组合拳](#组合拳)
  * [套路](#套路)
    * [定义套路](#定义套路)
    * [使用套路](#使用套路)
    * [带参数的套路](#带参数的套路)
    * [从套路返回值](#从套路返回值)
    * [自推](#自推)
  
## 引言

dongbei是啥？它是一门*以东北方言词汇为基本关键字的以人为本的编程语言。*

这玩意儿可是填补了世界方言编程地图上的一大片儿空地啊！
这么说吧，谁要是看了 dongbei 程序能忍住了不笑，我敬他是纯爷们儿！

那它有啥特点咧？多了去了：

*  简单啊！小学文化程度就行。您能看懂春晚不？能？那就没问题。
*  好读啊！看着看着包您不由自主地念出声儿来。
*  开心啊！呃，做人嘛，最重要的是要开心。
*  开源啊！不但不要钱，而且不要脸 -- 随时随地欢迎东北话高手打脸指正。

dongbei 编程语言的开发采用了业界领先的 **TDD（TreeNewBee-Driven Development）** 方式。
具体地说，就是每个功能都是先把文案写好，八字没一撇牛皮就吹起来了，然后根据牛皮写测试案例，最后再实现功能让牛皮不被吹破。
这样做有两大好处：第一每个功能都是有的放矢，不值得 tree new bee 的功能一概没有。
第二确保了每个功能都有文案负责吹嘘，开发者的辛劳绝对不会被埋没。

不扯犊子了。翠花，上酸菜～～～

## 系统要求

dongbei 语言是基于 Python 3 二次开发的。
只要能跑 Python 3 的旮旯儿都能跑。
像 Mac OS 啦、Windows 啦、Linux 啦，等等等等，都成！

## 安装

甭麻烦了！直接跑 src/dongbei.py 就成。

不过，要是你的系统没有python3呢，那得先装一个，免费！

比如，你要是用 Mac 的话，就按 https://docs.python-guide.org/starting/install3/osx/ 做。

## 你好，世界

创建一个名字叫 hello-world.dongbei 的文本文件，内容如下：

```
唠唠：“这旮旯儿嗷嗷美好哇！”。
```

用 utf-8 编码保存。
要是编辑器因为编码错误埋汰你，那就把文件内容改成

```
# -*- coding: utf-8 -*-

唠唠：“这旮旯儿嗷嗷美好哇！”。
```

再试，应该就成了。

然后在命令行窗口运行：

```
src/dongbei.py hello-world.dongbei
```

你应该看到执行结果：

```
这旮旯儿嗷嗷美好哇！
```

## 语言定义

学习一门语言，先得了解它的**词法**（怎么从一串串的字符组成词），然后是**语法**（怎么把词组成句子）和**语义**（这些句子都啥意思啊？）。
所以，咱们先讲讲 dongbei 语言词汇的构成。

### 词法

#### 字符串常量

一行代码当中，要是出现配对的中文全角双引号，比如

```
...“我是一个字符串”...
```

那么引号当中的内容（*我是一个字符串*）会被当成一个字符串常量。

#### 注释

一行代码当中，如果在字符串常量*外面*出现 **#** 字符，所有从 # 开始的字符都会被当成注释被忽略掉。
比如

```
唠唠：  # 我是一个注释。
    “嘎哈#？”。  # 我还是一个注释。
```
跟
```
唠唠：“嘎哈#？”。
```
是一样一样的。

#### 分词

大部分的西方语言在书写的时候要用空白字符或者标点把单词隔开，要不就会产生歧义。
比如 therapist（理疗师）和 the rapist（强X犯）就有很大的不同！

所以，西人开发的编程语言也一样啰嗦，动不动就要加空格，忒麻烦了。

dongbei 语言以人为本，适应华人的书写习惯，*加不加空格换行都无所谓。*
反正加了也白加（除非加在一个字符串常量的内部）。
所以对 dongbei 来说，

```
唠
  唠
    ：
      “嘎哈？”
        。
```
跟
```
唠唠：“嘎哈？”。
```
是一样一样的。

#### 名字

代码里面除了各种有特俗意义的关键词（keyword），还会有各种用户定义的**名字**（变量名、函数名、类型名，等等）。
在 dongbei 语言里面，除了关键词、标点符号和常数，剩下的都是名字。
比如，在“张三乘李四”这个 dongbei 语言表达式里，“乘”是一个关键词，“张三”和“李四”是两个不同的名字，

那么问题来了：dongbei 语言是不尿空格的，名字和关键词之间没有明显的隔离。
要是名字里包含关键词怎么办？
比如，我们知道“乘”是一个关键词，那还能用“阶乘”做套路名吗？
系统会不会把它理解成名字“阶”和关键词“乘”？

不要方！
dongbei 语言允许你用中文全角方括号【】把一串字符标注为名字。
比方说，“【阶乘】”就明明白白地是一个叫“阶乘”的名字，绝对不会被当成是名字“阶”加关键词“乘”。

#### 常数

除了用阿拉伯数字表示的十进制整数（比如 2、42、250，等等），0 到 10 的常数也可以用中文表达：

```
零一二三四五六七八九十
```

其中 `二` 也可以写成 `两`。

比如，
```
五加二
```
的意思就是 5 + 2。

### 语句

一个 dongbei 程序是由一串**语句**组成的。
每个语句以句号（。）结束。
为了表达程序员炽热的感情，也可以用感叹号（！）结束，意思和句号是一样一样的。
请大家根据自己的心情任选使用。

### 变量

dongbei 语言允许使用任何字符串做变量名。只要记住两点：

1. 变量名里所有的空白字符都会被忽略。
2. 有歧义的时候要把变量名用【】括起来。

#### 定义变量

dongbei 是一门以人为本的语言。
我们知道东北人都是活雷锋。
所以，要定义一个叫 XX 的变量，我们要写......

```
XX是活雷锋。
```

比如：
```
老王是活雷锋。
```

当然，热情洋溢的
```
老王是活雷锋！
```
也是可以的。

#### 给变量赋值

dongbei 语言不整“赋值”这种文绉绉的词儿。
咱们叫“装”。
比如：
```
老王装二。
```
可以理解为 C 语言的
```
lao_wang = 2;
```

#### 增减变量

活雷锋除了会装，加加减减也是常见的操作。
按没病走两步的规矩，这些操作的名字叫做：**走走**、**退退**、**走X步**、**退X步**。
比如：
```
老张装二。  # 现在老张等于2
老张走走。  # 现在老张等于3
老张走两步。  # 现在老张等于5
老张退退。  # 现在老张等于4
老张退五步。  # 现在老张等于-1
```

#### 引用变量

变量，呃，活雷锋定义以后就可以引用了。
引用的方法很简单：把活雷锋的名字写出来就成。
比如：
```
老张是活雷锋。
老王是活雷锋。
老张装250。
老王装老张加13。
```
定义了两个活雷锋：老张和老王。
老张值250。
老王值263。

### 输出

要输出信息，咱们得说“唠唠”。假定要说的信息是 YY，就得写
```
唠唠：YY。
```

比如说，活雷锋老王的当前值是263，那么
```
唠唠：老王。
```
的结果就是打印
```
263
```

唠的内容也可以是中文全角双引号括起来的字符串常量，像
```
唠唠：“诶呀妈呀！”。
```
的结果就是打印出
```
诶呀妈呀！
```

### 字符串运算

**顿号（、）** 操作符可以把两个值当成字符串拼接起来。
假定活雷锋老王的当前值是字符串“NB”，那么表达式
```
老王、“A”
```
的值就是字符串 `NBA`。而

```
“老王”、665加一
```
的值是 `老王666`。

### 算术运算

基本的四则运算 dongbei 都是支持的。举例说明：

表达式 | 含义
------|----
老王加老张 | 老王 + 老张
老王减老张 | 老王 - 老张
老王乘老张 | 老王 * 老张
老王除以老张 | 老王 / 老张

注意除法运算叫“除以”，不叫“除”。
问问你小学数学老师就知道，“A除B”的意思其实是“B除以A”，也就是说“B/A“。
所以，要是你说“6除2”，数学老师会以为你在说3分之1，而不是3。
你要是跟他讲“6除2得3”，信不信他削你？

跟小学学过的一样，乘除的优先级比加减高。
相同优先级的情况下，运算从左到右。比如说：
```
3加2乘5
```
的结果是13，不是25。

括号也是可以的：
```
唠唠：(五减（四减三）)乘二。
```
得
```
8
```

### 比大小

dongbei 人讲究分寸，长幼有序。

假定老王装的是5，老张装的是6。
那么
```
唠唠：老王 比 老张 大。
唠唠：老王 比 老张 小。
唠唠：老王 跟 老张 一样一样的。
唠唠：老王 跟 老张 不是一样一样的。
```
的结果就是
```
错
对
错
对
```

### 循环

所谓循环，就是一遍一遍磨叽。
所以，在 dongbei 语言里循环的写法是：
```
变量名 从 X 到 Y 磨叽：
  ...  # 需要重复做的事
磨叽完了。
```

举例说明：
```
老王从一到五磨叽：  # 老王从1走到5。
  唠唠：老王！  # 打印老王的当前值。
磨叽完了！  # 循环结束。
```
运行的结果是：
```
1
2
3
4
5
```

磨叽是可以嵌套的。比如：
```
老张从一到二磨叽：
  唠唠：“老张：”、老张。
  老王从老张到四磨叽：  # 内层磨叽可以引用外层磨叽变量
    唠唠：“老王：”、老王。
  磨叽完了。  # 内层磨叽结束。
磨叽完了。  # 外层磨叽结束。
```
运行出来是这样的：
```
老张：1
老王：1
老王：2
老王：3
老王：4
老张：2
老王：2
老王：3
老王：4
```

### 讲条件

虽然 dongbei 人都是活雷锋，干活的时候该讲条件还是要讲条件的。
**瞅瞅** 是一项很有用的技能！

一般来讲，要是俺们有件事情（不妨叫做 XXX）只想在某个条件（不妨叫 CCC）成立的时候再做，就写：
```
瞅瞅： CCC 吗？
要行咧就 XXX
```

要是 CCC 不成立的时候俺们有另外一件事情 YYY 要做，那就写：
```
瞅瞅： CCC 吗？
要行咧就 XXX
要不行咧就 YYY
```

比如说吧，要是俺们瞅着老王比老张大就想夸夸老王，那就这么写：

```
瞅瞅：老王比老张大吗？
要行咧就唠唠：“老王比较牛叉！”。
```

再复杂一点的：

```
瞅瞅：老王比老张大吗？
要行咧就唠唠：“老王比较牛叉！”。
要不行咧就瞅瞅：老张比老王大吗？
要行咧就唠唠：“老张比较牛叉！”。
要不行咧就唠唠：“老王老张共同牛叉。”。
```

看懂了？要是老王是3老张是2，那么这段代码就会打印
```
老王比较牛叉！
```
要是老王2老张3咧，就会打印
```
老张比较牛叉！
```
要是老王老张都2咧，打印的就是
```
老王老张共同牛叉。
```

### 组合拳

你有没有想过：要是俺们在某个条件成立的时候想做两件事而不是一件事，该咋办咧？
要是写
```
瞅瞅：CCC 吗？
要行咧就
   XXX。
   YYY。
```
成嘛？

不成。

前面俺们说过咧，dongbei 语言里面字符串常量外边儿的空白是不作数的。
写了也瞎掰活。
所以，按上面这种写法，XXX 倒是只有 CCC 成立的时候才会做，可 YYY 是无论如何都会做的。
相当于：
```
# 先讲条件：
瞅瞅：CCC 吗？
要行咧就XXX。

# 这个不讲条件。
YYY。
```

要解决这个问题，咱得上 **组合拳**：把一串操作整合成一个操作。
组合拳的写法是：
```
开整：
  XXX。
  YYY。
  ...
  ZZZ。
整完了。
```

尽管整了一串，在 dongbei 语言看来这是一个操作。
所以，
```
瞅瞅：CCC 吗？
要行咧就开整：
   XXX。
   YYY。
整完了。
```
就能达到俺们的目的了！

### 套路

“套路”这名字听着吓人，其实就是给一串常用的组合拳取一个名字，然后吧需要做这些操作的时候提一下这个名字就OK了。

#### 定义套路

要定义一个套路，用这个格式：
```
套路名字 咋整：
  ...  # 要做的操作
整完了。
```

还是举例说明：
```
写九九表咋整：  # 定义套路 写九九表。
  老王从1到9磨叽：
    老张从老王到9磨叽：
      唠唠：老王、“*”、老张、“=”、老王乘老张。  # 打印 X*Y=Z
    磨叽完了。
    唠唠：“”。  # 空一行。
  磨叽完了。
整完了。  # 结束套路定义。
```
定义了一个叫“写九九表”的套路。
注意定义套路本身不会让这个套路真的跑起来。
所以上面这段程序跑的结果是啥也不做。

#### 使用套路

要把一个套路代表的操作跑一遍，得写：
```
整 套路名。
```

比如说，上面这个“写九九表”的套路定义好了过后，你只要写：
```
整写九九表。
```
就可以打印出一份浓眉大眼的九九表了：
```
1*1=1
1*2=2
1*3=3
...

8*8=64
8*9=72

9*9=81
```
#### 带参数的套路

有的时候，我们希望通过一个参数去控制一个套路的行为。
比如，我们要教会电脑算一个数的阶乘（就是1*2*3*... 一直乘到这个数）。
在定义这个“阶乘”套路的时候，我们并不知道以后会用它来算哪个数的阶乘。
所以，我们要把这个数定义成这个套路的一个参数。

那就要这样写：
```
套路名（参数名）咋整：
  ...  # 爱做的事
整完了。
```

具体到这个“阶乘”套路，就是这样的：
```
【阶乘】（几）咋整：  # 定义套路 阶乘，有一个参数 几
  ...  # 阶乘的操作步骤
整完了。  # 定义结束。
```

注意这里我们把套路名“阶乘”用方括号【】括起来，因为“乘”本身是个关键词，不括起来容易引起误会。

这个套路有一个参数，名字加做“几”。
“【阶乘】（几）”就是算几的阶乘。

要是一个套路有多个参数，那就得把它们一个一个列出来，中间用逗号隔开：
```
求和（甲，乙）咋整：
  滚犊子吧 甲加乙。
整完了。
```

调用这种套路的时候咧，相应地要把参数的值一个一个列出来：
```
唠唠：整求和（五，七）。
```
会打印出 12。

#### 从套路返回值

在“写九九表”这个例子里，套路本身是不返回任何值的。
它要做的事都通过“唠唠”打印出来了。

而对于“阶乘”来说，我们并不想打印这个阶乘的结果。
我们只想把结果返回给整这个套路的人，爱咋用咋用。

在 dongbei 里边儿，从套路里返回一个值X，得说“滚犊子吧X。”

这个阶乘的完整定义，可以是这样的：
```
【阶乘】（几）咋整：  # 定义套路 阶乘，有一个参数 几
  老王是活雷锋。
  老王装一。
  老李从一到几磨叽：
    老王装老王乘老李。
  磨叽完了。
  滚犊子吧老王！  # 返回值。
整完了。  # 定义结束。
```

写完这个，再来一句
```
唠唠：整【阶乘】（五）。
```
就可以看到打印结果
```
120
```
了！

#### 自推

每个程序员在学习编程的时候都要翻一个坎儿，这就是 **递归** 。

在 dongbei 语言里面，咱不整这些虚头八脑的概念。
咱就叫“自推”。

啥意思？
就是说在做一个操作的时候调用这个操作自己。
有点循环定义的意思。

其实这就是俺们中学老师讲过的数学归纳法：欲求 f(n)，先求 f(n-1)。
然后如果从 f(n-1) 的值可以推算出 f(n) 的值，不就搞定了吗？
当然，前提是这个自推不能无穷无尽地整下去，到某一步得停下来。

举个例子。
求 n 的阶乘 f(n) 可以这么搞：
要是 n 是 0 的话，结果就是 1。
要是 n 比 0 大的话，就给就是 n * f(n-1)。

这里，在算 f(n) 的时候，我们先算 f(n-1)，再从 f(n-1) 算出 f(n)。
这就是自推大法的精髓。

把上面的思路用 dongbei 语言写出来，就是：

```
【阶乘】（几）咋整：  # 定义套路 阶乘，有一个参数 几。
  瞅瞅：几比一小吗？ # 需要自推吗？
  要行咧就 滚犊子吧 一。  # 不需要。
  要不行咧就 滚犊子吧 几乘整【阶乘】（几减一）。  # 需要。自推吧。
整完了。  # 定义结束。
```