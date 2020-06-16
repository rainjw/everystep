# 关系数据库模型

关系数据库采用二维表来描述实体于实体间的俩西，而每个关系就是一张规范的二维表。

## 关系数据结构

1. 关系模式

关系模式，在每个关系中都存在，由一个关系名和它的所有属性组成。

通常也称关系名为关系模式。关系名用 R 表示，属性用 A/B/C 表示，而一个关系模式则可以用 R(A,B,C,D,E) 来表示。

关系就是一张二维表，表头每一类代表一个属性，而属性的个数称为**元数**。

一个条数据就是一个元组，元组的总个数称为**基数**，也就是这张表有多少条数据。

元组的集合称为 **关系** 或 **实例**。

关系是规范化的二维表，所以具备以下性质：
* 属性值是原子的，不可分解。
* 没有重复元组。
* 没有行序。
* 理论上没有列序，但是使用时一般都有列序。

2. 键

在关系数据库中存在着键。

键通常由**一个**或**多个**属性组成，有时候也称其为码或关键字。

键的作用是**唯一标识**一个元组。例如个人信息中的身份证，对于人来说是唯一存在的。

键有超键，候选键，主键，外键四种类型。

超键指能唯一标识元组的属性或属性组。例如学生记录中的学号 SNO，姓名 SNAME，这两个属性可以唯一标识一个学生。

候选键指一个属性组能够唯一标识一个元组，和超键不同的是超键可以含有多余的属性，而候选键不行，每一个元素都不是多余的。例如还是学生记录中的 学生可以重名的话，那么 SNAME 就是多余的。而 SNO 则是候选键。

如果候选键有多个，那么其中一个就是主键，可以理解为主键组成了候选键，每一个主键都可以唯一的标识一个元组。

外键的定义是：假如存在一个关系 R，其中包含有另一个关系 S 的主键所对应的属性组 F，则称 F 为 R 的外键，称关系 S 为参照关系，关系 R 为依赖关系。

我们知道一个关系是一张表，换句话说外键指的是存在于当前表中的属性是别的表中主键。

1. 关系模式，关系子模式和存储模式

关系模式是对关系的描述，例如对于学生信息而言，其关系模式为 S(SNO,SNAME,AGE,SDPET) 其中 S 为关系模式的模式名，而圆括号中的则是学生的数据结构。

多个关系模式组成了关系模式集，对于关系模式而言，其中的一个具体的关系称为实例。

关系子模式指数据不在当前的关系模式中而是通过外键链接到另外的关系模式中提取到的数据。

存储模式指数据具体在物理设备上的存储方式，因为关系模式键的存在，通常采用散列方法或索引方法实现。如果关系中元组数目较少（100以内）也会采用堆文件方式实现。除此之外还可以堆任意的属性建立辅助索引。

## 关系操作

关系的本质是集合，所以操作关系本质上是操作集合，其对象结果都是集合。

1. 基本的关系操作

基本的关系操作有查询，插入，删除和更新。

而查询又分为选择，投影，并，差，笛卡尔积，连接，除等。其中前五种为基本操作。其他的操作都可以通过基本操作实现。例如 $1 * 3$ 可以用 $1 + 1 + 1$ 来实现。

2. 关系操作的表示

关系操作分为关系代数和关系演算。前者是通过关系的运算来表达查询，而后者则是通过谓词来表达查询。

而 SQL 语言则是介于关系代数和关系演算之间的结构化查询语言。

## 关系完整性约束

由于数据库中数据是动态改变的，为了方便维护并且与现实世界一致需要对关系数据库加以约束。

随着时间的变化，数据时刻都遵守这些约束。

1. 域完整性约束

指属性必须遵守该关系中属性的规则，例如百分制的学生成绩不会出现 101 分的成绩，一旦出现就破坏了域完整性约束。是最基本的最简答的约束。

2. 实体完整性约束

现实世界中的实体是可以唯一标识的，一个属性或一组属性都可以标识一个实体。例如通过身份证来唯一标识一个人。现实世界中不会存在完全两个相同的实体。

而实体完整性则指能唯一标识一个实体的属性或属性组不能为空，如果为空就无法标识一个实体了，这与现实相矛盾。

3. 参照完整性约束

在现实世界中实体与实体之间都是存在练习的。

参照完整性指的是一个关系的外键必须是另一个关系的主键，而且外键取值要么为空或者取作为主键的关系中的有效值。

4. 用户定义完整性约束

所有的数据库都支持实体完整性和参照完整性。但是具体到实际上根据实际情况会有特定的约束。例如学生姓名不能为空值。

以上的这些约束是用户自定义的，也就是用户定义完整性约束。

# 关系代数基本理论

## 传统的集合运算

并运算，交运算，差运算，笛卡尔积运算。

## 专门的关系元

选择，投影，连接，除等。

# 关系数据库的规范化理论

这些理论是为了构建更好的，合适的关系模式出现的。

根据现实世界的数据依赖从而对关系模式进行规范化处理，主要是解决不合适的数据依赖问题，数据依赖指的是数据之间的各种联系。

## 关系模式规范化的必要性

如果没有关系模式规范化会出现很多问题。例如数据冗余，指同一个数据在系统中多次出现。

因为数据冗余还会导致操作异常，操作异常分为更新异常，插入异常，删除异常。也就是当变更某个数据时需要将涉及到的所有的表都变更一遍，一旦没有变更使得同一个数据在不同的表中的值不一致都会导致异常出现，而根据变更的方式出现了更新异常，插入异常，删除异常。

## 函数依赖

1. 什么是函数依赖

先看例子：在学生这个关系中，通过学号可以确定学生的姓名，那么就说明姓名依赖于学号或者说学号决定姓名，这就是函数依赖。

定义：假设 R(U) 是一个关系模式，U 是 R 的属性集合， X，Y 是 U 的两个属性子集。对于 R(U) 的任意一个可能的关系 r，r 中不可能存在两个元组在 X 上的属性级相等，而在 Y 上的属性值不等，则称 X 函数确定 Y 或 Y 函数依赖于 X，记做 $X \rightarrow Y$，称 x 为决定项，y 为依赖项。

其中入过 Y 是 X 的子集，也就是 $y \subseteq x$ 那么必有 $X \rightarrow Y$ ，这是平凡函数依赖，反之其他的都是非平凡函数依赖。

关于函数依赖的概念还要注意以下几点：

* 函数依赖不是指关系 R 的部分关系实例需要满足而是全部都需要满足。

* 函数依赖是语义层面的概念，具体情况具体分析。

* 数据库的设计者需要根据实际情况设计函数依赖避免在使用种出现错误，不符合函数依赖的数据就不能存入数据库中。

2. 完全函数依赖和部分函数依赖

例子:

定义：从函数依赖继续向下分析，在关系模式 R(U) 中如果 $X \rightarrow Y$ 而对于 X 中的任一个真子集 W ，都有 $W \rightarrow Y$ 不成立，那么称 Y 完全函数依赖，反之就是部分函数依赖。

如果 U 部分函数依赖于 X 那么 X 是 R 的一个超键，反之如果 U 完全函数依赖于 X ，那么 X 是 R 的一个候选码。也就是超键里面存在多余的属性而候选键里面没有多余的属性。

3. 传递函数依赖

定义：在关系模式 R(U) 中，有 X，Y，Z 三个子集，如果 $X \rightarrow Y$ 而 $Y \rightarrow Z$ 那么称 X 传递函数确定 Z。而 Z 传递函数依赖 X 。

4. Armstrong 推理

根据已知的函数依赖推导出另外的函数依赖需要一些规则的支撑，而 Armstrong 公理提供了这些规则。

Armstrong 有以下三条规则：
* 自反性：如果 $B \subseteq A$ 则 $A\rightarrow B$  
* 增广性：如果 $A \rightarrow B$ 则 $AC \rightarrow BC$
* 传递性：如果 $A \rightarrow B$ 并且 $B \rightarrow C$ 那么 $A \rightarrow C$

根据 Armstrong 可以得到以下推论：
* 合并性：如果 $A \rightarrow B$ 且 $A \rightarrow C$ 那么 $A \rightarrow BC$ 
* 分解性：如果 $A \rightarrow BC$ 那么 $A \rightarrow B$ 且 $A \rightarrow C$ 
* 伪传递性：如果 $A \rightarrow B$ ， $BC\rightarrow D$ 那么 $AC\rightarrow D$
* 复合性：如果 $A\rightarrow B,C\rightarrowD$ 那么 $AC\rightarrow BD$

对于关系模式而言可能存在多个函数依赖，这些函数依赖构成的集合称为 F。

如果两个函数依赖集 $F_{1} F_{2}$ 在 Armstrong 公理的推导下相同则称 $F_{1} F_{2}$ 对于 Armstrong 推理保持一致。 

## 关系的范式及规范化

如果数据库中的表（关系模式）设计不好是会存在很多问题的，例如数据冗余，操作异常。

但是设计出好的关系范式必须满足一定的约束条件，这些条件成就是关系模式的规范。

规范的严格程度分为多个级别，不同级别之间严格递进，其中而每一个级别都称为范式。

1. 第一范式

举个例子：在客户这个关系模式中，如果电话号码这个属性可以再分话，例如一个客户有两个电话号码。

那么必定需要存两条记录了，首先就破坏了主键约束，即主键唯一标识一条记录，也就是同一个客户存在两条记录。

除此之外会带来数据的冗余，插入删除更新等操作数据时更要避免数据出现异常。所以问题在于字段属性只能有一个含义，属性不可分解，原子级别。

定义：第一范式指关系模式中的属性不可再分，也就是原子级别的。

第一范式 (first normal form) 简称 1NF 。

2. 第二范式

定义：在关系模式 R 中，首先 R 属于 1NF，其次它的每一个非主属性都完全函数依赖与 R 的候选键，那么 R 属于第二范式，简称 $R\subseteq2NF$ 。

3. 第三范式

定义：如果关系模式 R 属于 1NF ，且每个非主属性都不传递依赖于 R 的候选键，那么称 R 属于第三范式，简记为 $R\subseteq3NF$

注意 满足 3NF 的前提是已经满足了 2NF ！

将关系模式分解到这种地步已经很大程度上的降低了数据冗余和操作异常。

4. BC 范式

定义：如果关系模式 R 是 1NF，且每个属性都不传递依赖于 R 的候选键，那么称 R 属于 BC范式，也就是 $R\subseteqBCNF$

BC 范式和第三范式的区别在于，前者既检查主属性，又检查非主属性。而后者只检查非主属性。

显然 BC 范式更为严格，并且满足 BC 范式的话一定满足第三范式。

如果一个数据库中关系模式都是 BC 范式的话，在函数依赖范围内已经实现了彻底的分离。

并且已经消除了插入和删除异常，3NF 的“不彻底性” 表现在可能存在主属性对键的部分依赖和传递依赖。


## 关系模式的分解

模式分解指的是将原有关系在不同属性上进行投影，从而将原有的一个关系多个属性分解成多个关系，其中的每个关系含有较少属性。

并且分解必须是可逆的，可逆意味着信息没有丢失，数据间的语义联系依旧存在。

1. 无损分解

指对新的关系进行自然连接后得到的元组集合与原关系完全一致，如果不一致则称为有损分解。

2. 保持函数依赖分解

指分解后的函数依赖对于 Armstrong 推理保持一致。

3. 关系模式分解原则

指保证数据等价和语义等价以及效率。

无损分解可以保证数据等价，也就是通过连接可以逆转，分解前后数据不会丢失。

函数依赖分解可以保证语义等价，分解前后语义不发生变化。

除此之外还要考虑效率问题，如果分解的太细做大量的连接运算会减低查询速度。

可以适当的增加数据冗余，以空间换时间。

4. 3NF 分解

理论上已经证明任何关系模式都可以无损分解为多个 3NF ，并且这会解决数据冗余和操作异常等问题。
