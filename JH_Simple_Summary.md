

# NIST官方评价 #
(以下文档包含对所有进入ROUND2的算法的评价，主要是为什么能够进入ROUND2的评价）
http://csrc.nist.gov/groups/ST/hash/sha-3/Round1/documents/sha3_NISTIR7620.pdf

# 李宇骞 #
JH算法首先将Message用课上的加一个1，若干个0，再加上一个表示长度的二进制数得到一个512n位的初始信息，然后分成n个512位的段，进行HASH。HASH过程非常简单，主要就用到了一个F8函数，将512位的信息段和一个1024位的HASH值计算得到一个1024位的新HASH值。算法开始时首先通过长度生成一个初始值H0，然后对n个512位的信息段M1, M2等分别用F8函数获得H1，H2...最后得到的Hn就是结果。如果最终需要得到的HASH值应该是m位，那么就将Hn的最后m位提取出来即可。

文章主要就是对F8做了具体的解释：F8是简单的通过E8得来的，E8是通过很多轮的`R8`和一次`R8*`得来了，`R8`是通过S，L，P等简单的模块计算得到了。中间的具体过程文章中写的非常清晰易懂。唯一让我琢磨不透的是L函数，虽然文中有具体的L计算公式，但是我不是很能理解L到底是干什么的。像SBox，Permutation这种模块由于在DES中已经出现过，所以比较清楚。

# 刘之方 #
  1. Summary of the Algorithm

> The algorithm`[1]` makes use of many ideas from existed algorithm, which makes
> the algorithm easy to understand.

  1. 1 The main hash algorithm

> The main hash ﬁrst pad the message to be a multiple of 512 bits, in which the
> length of the message is padded to the message. After padding, the message is
> split into blocks of 512 bits.
> Then, starting from an initial hash value H (0) (1024-bit), the algorithm itera-
> tively uses a compression function F8 to compress each block, resulting in a ﬁnal
> hash value H (N ) . Finally H (N ) is truncated into message digest of designated
> length.

  1. 2 The compression function

> The construction of the compression function uses a block cipher, and also
> borrows some ideas from AES methodology.
> Like AES, JH uses S-Boxes and P-Boxes as building blocks. Besides, a
> MDS (Maximum Distance Separable) code is used, which further contributes to
> diﬀusion by making the hash value more evenly distributed.

> References
`[1]` Hongjun Wu. The hash function jh. Submission to NIST (updated), 2009.

## JH中Differential Cryptanalysis的分析报告 ##
http://march2010.googlecode.com/files/JH_differential_analysis.pdf

# 刘洋 #
JH算法中所使用的函数都是一些常见的用于Hash的处理过程。JH通过两个S-boxes、若干Permutation及线性变换来完成对定长数据的压缩（F\_d）。给定一个输入后，JH先进行 一般的Padding和分块处理，然后根据数据摘要的长度计算出一个初始的H^(0)，然后用F\_d函数进行若干轮计算后得到最终的Hash值。
总的来说，JH的算法比较简单和常见。我认为，JH在数据处理方面并没有什么创新，它的安全性主要是通过合理地设计各个子过程的执行步骤以及增加块长度和增加加密轮数来实现的。但是，正因为JH所使用的算法非常“大众化“，所以恰好方便了我们对其安全性和运行效率进行分析。

# 李照楠 #

## 9 Security Analysis of JH ##

我主要针对文章的第9部分做了相关阅读和调查。以期了解对加密算法进行安全性分析的常用方法。

文章首先简要展示了几种不同位数的Hash算法所出现的碰撞、原像、第二原像的个数。以说明大部分情况下，此Hash算法是可以抵挡Preimage attack和birthday attack的。之后主要从三个方面进行了密码学分析：

  * 一，Differential cryptanalysis。这种分析旨在研究：对于一个HashFunction，输入值的变化会对输出值的变化造成多大的影响。通过这种分析，可能可以找到一些特殊位置，在这些位置HashFunction是不具有随机行为的。通过寻找这种位置，可以恢复一个HashFunction的密钥。paper首先通过分析active SBoxes的最小个数来讨论此Hash算法的加密特性。在最保守的情况下，active Sboxes的个数叶然在600左右。这说明JH算法是非常强壮的。

  * 二， Truncated differential cryptanalysis。这一分析主要是考虑结果中的一个元素是不是active的，而不是考虑其值是否是不同的。所以，文章考虑了与linear transformation L相邻的四个Sboxes。其前后两个Sboxes的活跃个数会依照不同的概率发生变化。如果之后Sboxes的活跃个数变少了，我们则称这是一个shrinking事件。最终评判truncated differential characteristic的方式，是统计shrinking事件的个数与最后一层的活跃Sboxes个数之和。

  * 三， algebraic attack，这种攻击可以通过解非线性方程对key或者message进行恢复。如果压缩算法的代数方程非常弱，这种攻击在密码分析学中可以被用于寻找冲突、第二原像或者原像。由于message被多padding了一个block，恢复一个message需要考虑至少36个SBoxes。由于Sbox的维度是3，所以要恢复message，需要进行的运算是非常巨大的。所以JH算法是安全的。

  * 四，之后，文章分析了其他常见的attacks，以说明JH算法的安全性。这些攻击方法包括Pseudo-collision, Collision resistance, preimage resistance以及Second preimage resistance。最后，作者说明了padding操作对于算法安全性的影响。


# MIT学生作业——对几个候选hash函数的分析（包括JH） #
http://courses.csail.mit.edu/6.857/2009/sha3/group7.pdf