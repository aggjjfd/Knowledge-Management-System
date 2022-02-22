# 谈谈数学里的构造主义（constructivism）、直觉主义（intuitionism）和数学基础

> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/22389755)

翻开数学史的书籍，构造主义仿佛是二十世纪初期的一股叛逆思潮。它曾经很酷，但是却缺乏主流数学家的关注，甚至遭到批判。本文试图梳理一下构造主义的脉络，始于构造主义，终于 univalence axiom (i. e. homotopy type theory).

## §-1. 构造主义和直觉主义

用过分简单的话讲，构造主义的核心就是 “要证明一个东西存在，必须把它构造出来”。这直接否定了人们熟悉的反证法。把反证法拿走，后果有多严重呢？

从某些层面上讲，它并没有人们想象的那么严重——只要澄清了一些概念并且做一些仔细地重新叙述，有些用反证法证明的命题其实并不需要反证法：比如欧几里得仔细选取的对 “素数有无穷个” 这个命题的陈述，本质上说的是

> 任意一个有限集合到素数的集合都存在一个单射。

完全避开了 “无穷” 的概念这一蹚浑水。（从欧几里得对平面几何第五公理的谨慎态度也可以理解，他绝对不会用 “素数有无穷个” 这种描述。）

$\sqrt 2$ 是无理数” 这个命题，也可以转化为

> 对任意的自然数 $m,n$, 我们有 $m^2>2n^2$ 或者 $m^2<2n^2$ .

并且可以构造性地证明（证明比一般的用反证法证明稍微冗长些）。

在另一些层面上，构造主义带来的困难则大得多——构造主义的一支，布劳威尔（L. E. J. Brouwer）的直觉主义直接要求 "there exists" 被解读为'there can be constructed', 也就是说'we can compute'. 这直接导致了了以下的 “神逻辑”:

> $(\star )$ 对于数列 $(a_n)$, 即使 “ $\forall n,a_n=0$ ” 这一命题不成立，我们也不能得出 $\exists n, a_n\neq 0$

因为——虽然在非直觉主义的意义下有这么一个 $n$, 但是这个 $n$ 并不是被构造出来的。没有 “算法” 告诉你怎么计算出这个$n$.

不能构造出来就不存在？没错，布劳威尔就像苹果公司一样，再一次定义了 “存在”！

## §0. 如何解读神逻辑

要理解这个神逻辑，不能拘泥于 “存在” 这两个字在自然语言中的字面意思，而是把 “$\exists$” 这个量词 (quantifier) 看做一个纯粹的符号，再接受布劳威尔对这个词的解读——换句话讲建构在直觉主义上的数学和逻辑，其实是我们熟悉的那套东西的一个兄弟，只是 “$\exists$” 这个基因发生了一点变异。

由于 “$\exists$” 的变异，直觉主义的数学发展相比迟缓。因为，$(\star )$直接否定了数学中一个常用的逻辑命题——排中律！排中律的陈述很简单：

> 对于任意的命题 $P$ , $P \lor \lnot P$ 成立。（也就是说， $P$ 或非 $P$ 总有一个成立。）

加上量词的版本更能体现排中律和 $(\star )$ 的不可调和之处——加上量词的排中律是这样的：

> $\lnot(\forall x. Px) \Rightarrow \exists x.(\lnot Px)$.

用直觉主义的方式来阐释 “ $\exists$ ”，显然无法接受排中律——即使我们否定了 “对任意的! $x$ , 都有 $Px$ ” 这一命题，我们也不能**算出**一个使得 $Px$ 不成立的! $x$ .

把排中律抽走，对直觉主义的数学影响有多大呢？很大：

（注：这里原文有误，已修改）由 Diaconescu's theorem 排中律是选择公理的推论，抽走排中律，选择公理也不能成立，这就抽走了很多现代数学里最重要的引理，动摇了很多比较现代的理论的基石——

1. 分析上，没有排中律，不能得出 $\forall x \in \mathbb{R},(x=0)\lor (|x|>0)$ （即使知道 $x=0$ 不成立也不能推出! $x$ 的绝对值大于 $0$).）类似地，也没有中值定理。
2. 代数上，没有选择公理，甚至不能证明任意一个环的存在极大理想！

这种限制对于很多数学家而言是万万不能接受的。实际上，没有排中律的话，甚至不能说一个实数要么是有理数，要么是无理数！（提示，设 $(a_n)$ 是一个取值在 $\{0,1\}$ 中的递减数列，考虑 $\sum\limits_{n=1}^{\infty}\dfrac{a_n}{n!}$ 的有理性和前面的神逻辑 $(\star )$ 的关系）

## §1. 一个有趣的观点

实际上，高中或者大学的某些数学之所以对一部分人困难，就是因为我们就放弃了构造主义！

首先，高中的数学和初中是很不一样的——并不是说初中研究了线性函数和二次函数，高中就研究三次四次函数，大学再研究五次六次函数。回头看来，两者最大的区别是，用的数学基础发生了重大变化——初中的数学，无所谓基础，所有的研究对象都是实数轴上的一次或者二次函数，所有的函数都可以在计算器上摁出来，其实在学生脑子里默默建构了构造主义的习惯。而高中开始，数学就慢慢地建立在集合论的基础上了。

集合论带来的，是非构造性。两个集合之间的映射，定义起来并不平凡：

> 给定集合 $X,Y$, 他们之间的一个映射是一个关系，对于任意的 $x\in X$, 有唯一的 $f(x) \in Y$, 这个关系记作 $f: X\rightarrow Y$.

换句话讲， $f: X\rightarrow Y$ 对应的是 $X \times Y$ 的一个满足如下条件的子集 $R$.

> $\forall x\in X, \exists! y\in Y$，（存在唯一的 $y \in Y$ 使得 $(x, y) \in R$

真正理解这个定义的人，难免[痛恨](http://mathoverflow.net/a/2367/82513) “一个映射 / 函数就是一个公式” 的常见误解（鄙人就曾经是痛恨者中的一员）。回过头来看，这种误解其实代表着构造主义和集合论的冲突。按照集合论的定义，实数轴上的实值函数，其实是 $\mathbb R \times \mathbb R$ 的一类的子集，对每个 $x \in \mathbb R$ “分配” 了一个值 $y \in \mathbb R$ ——有没有让人窥见选择公理的影子？大多数这样的函数，都是 “不可计算” 的。

就是这一点点非构造主义，以奇怪的形式把很多人绊倒在构造在集合论基础上的现代数学的门槛上。门槛本身在哪里并不重要——可能在集合论，也可能在数学分析，或者实变函数论，但归根结底都是那一点点非构造主义。

类似的例子还有抽象代数。很多人在初次学习的时候本能地拒绝 “一个群是一个集合加上一个满足某些条件的二元运算” 这样的抽象定义，但是能接受矩阵群的概念，本质上也是非构造主义在作祟。用面向对象编程的语言来说，矩阵和一个抽象的集合的元素的区别在于，矩阵群自带元素的 constructor 和 methods. 但是用抽象的集合给出的群，就好像只带着 virtual methods 的 object, 会被一些人脑子里的编译器拒绝。

## §2. 集合论与计算机，一个小故事

实际上，集合论以及上述的非构造主义，不光把一部分学生拦在了现代数学的门槛之外，还拦住了一个重要的角色——**计算机**。

这个 “拦住” 是实质性的：不是说囿于计算性能的门槛，计算机虽说可以理解集合论，但无法用于实际用途。而是由于某些原因，多数数学家接受的作为数学基础的 [ZFC 集合论](https://en.wikipedia.org/wiki/Zermelo–Fraenkel_set_theory)，实在无法让计算机接受。

实际上，在集合论的框架下，多数数学家也没办法从纯粹集合论的角度思考数学——比如实数的概念，只有在最严格的分析中才视作有理数的柯西序列的等价类，平时脑子里想象的都是实数轴上的点。数学基础和实践的这种巨大差异，才是计算机的最大绊脚石。

就算有办法把以 ZFC 集合论为基础的内容硬塞给计算机，其实还有下面这种风险：假设某一天计算机利用强大的计算能力，用纯粹的逻辑找到了黎曼猜想的证明，但人类仔细阅读计算机给出的证明的时候，发现在关键的一步，计算机说

> 因为 $0\in 2$, 所以...

等等， $0\in 2$ 是什么鬼？！计算机辩解道，根据定义，万物都是集合，首先有空集 $\varnothing$, 然后通过 $0=\varnothing ,1=\{0\},2=\{0,1\},\ldots$ 来定义自然数 $\mathbb N$ 嘛。人类数学家急了，这只是自然数的集合论**模型**之一啊！$0\in 2$ 这种依赖于模型的东西，怎么能用来证明这么重要的定理呢？这时候，另一台计算机，用另一个自然数的集合论模型，也找到了一个黎曼猜想的证明，但是这台计算机里，自然数的模型 $f\mathbb N$ 是通过 $0=\{\varnothing\},1=\{0\},2=\{1\},\ldots$ 来定义的。而在证明的关键一步，它用到了 $0\in 1, 1\in 2$ 我们甚至没法比较两台计算机给出的证明是否相同。

在人类看来，两个自然数的模型的选取，本来是无关紧要的东西，不管怎么说，任意两个模型都是同构的嘛。对重要命题的证明不应该依赖于模型的选取，这就好像对一个关于整数的结论的证明不应该依赖于整数的十进制表示一样显然。同构的话，对一个成立的命题，可以通过同构 “搬” 到另一个上，但显然，“可以搬动的性质” 并不包括 $0\in 2$ 这种**奇怪的东西**——这又是一个没法跟计算机解释的怪现象。

## §3. 从集合论到类型论 (type theory)

花开两朵，各表一枝。七十年代末，瑞典人 Martin-Löf 做出了一个重要的发现，即 algorithmic mathematics, 也就是计算机科学, 等价于只用直觉主义逻辑的数学。在 Martin-Löf 发展的构造性类型理论 (constructive type theory) 中，有以下的对应关系

![[Pasted image 20220208002715.png]]

熟悉集合论的读者应该能注意到上述表格的第一行的不寻常之处——在 Martin-Löf type theory 中，一个 “函数” 就是一个 “公式”！（只不过这个公式可以稍微复杂一点，写成一段代码或者算法而已。）这套观点完全丢弃了原来对函数的定义， $X \to Y$ 的函数不再是 $X\times Y$ 的一个特殊子集，而是从一个类型 $X$ 的输入到一个类型 $Y$ 的输出的一个计算的步骤 (procedure) !

实际上，尽管离学术界广泛接受还有一定距离，type theory 其实很有适用于数学基础的潜力，并且是一个**从诞生之初就适合计算机理解**的数学基础。

在类型论中，“集合” 的概念被 “类型” (type) 取代，自然数、整数、有理数，都有对应的类型。乍一看这和集合论 “万物都是集合” 没啥不同，只是把 “放在一起的一堆东西” 的名字从集合 (**set**) 改成了类型 (**type**), 并且把记号 $a\in A$ 改成了 $a:A$. 实际上，两者差了十万八千里——在集合论中，我们可以构造一个集合 $a$, 和另一个集合 $A$ （两者都是从空集 $\varnothing$ 出发，用 ZFC 集合论允许的运算进行构造得到的结果，比如$\{\varnothing, 0, 1, 3\} \times \{1,2\}$），再讨论

> $a\in A$ 是否成立？

这样的问题。而在 type theory（intensional type theory, 下同）中，没有办法 “给出” 一个不 “属于” 任何类型的 $a$ , 再去讨论它和别的类型有没有从属关系，只能一次性地给出判定 $a:A$ ——注意这里的用词， $a:A$ 是一个判定 (judgement)，而不是一个取值有可能真也有可能假的命题，一个判定从摆上纸面的那一刻就自动成立。在集合论中，如果 $a\in A$, $B$ 是一个满足 $A\subset B$ 的集合，则我们也有 $a\in B$. 类似的话在 type theory 中毫无意义。——实际上，type theory 的这种讨论方式，反倒**更接近现代数学实践**，因为没有人会真的拿两个不相干的东西 $a,A$ 再问 “ $a\in A$ 是否成立”，而通常是 “设 $X$ 是拓扑空间，$x\in X$ 是 $X$ 中的一个点”，从这个角度上说，这种做法更接近于给出判定 $X:\text{Top}, x : X$.

更有趣的一点是，类型论的法则自动地包含了基本的逻辑！一个命题，在类型论中可以写成一个类型 $P$ , 其证明则是构造那个类型中的一项 (term) $x:P$. 命题 $P\Rightarrow Q$ 则变成了一个新的 type $P\to Q$, 其 “证明” 则是在类型论的意义下构造 $P$ 到 $Q$ 的一个函数。对照之下，数理逻辑独立于集合论而存在。

集合论中最基本的 “命题”，$a\in A$ 在 type theory 中已经不能讨论。另一类命题，即对于 $x, y\in A$ 是否有 $x=y$, 则在 type theory 中有深远的推广。前面说了，任意一个命题，都有自己的类型, $x=y$ 这样的，也不例外——它对应的类型，叫 identity type, 记做 $x=_A y$. 相比之下，集合论中的命题，无非是两个元素的一个比较，相等，则 $x,y$ 只是同一对象的两个符号而已，可以互相置换（substitution, 等量代换是中学数学中最基本的操作）；不相等，则他们之间在集合论的意义下没有任何联系。$x=_A y$ 是个 type 这件事情，不仅仅是个记号，意味着 type theory 的任何构造，都可以对它进行。

## §4. 尾声：从 Extensionality 到 Univalence

两个集合什么时候相等呢？在 ZFC 集合论中，这是由一条叫做外延性 (extensionality) 的公理保证的：$\forall A, B, (\forall x, x\in A \iff x\in B) \Rightarrow (A=B)$. 也就是说，如果两个集合包含的元素一模一样，我们就说两个集合相等。

这个公理完全不能用在 type theory 中——根本没有 $\forall x$ 这个说法，要给出! $x$ , 必须以 $x:A$ 这样的方式，这时候 $x:B$ 就成了彻底的伪命题，没法讨论。

但是，在类型论中讨论两个类型的 equality, 还是有一定意义：实际上，任意两个 type $A,B$ 都是一个更大的 type, 即 universe $\mathcal U$ 中的项，所以给出两个类型其实是给定了 $A, B : \mathcal U$, 我们当然可以定义 identity type $A, B : \mathcal U$, 但是，怎么描述这个类型呢？

Voevodsky 在 2009 年给出了一个诱人的答案，即 univalence axiom.

从 $A =_{\mathcal U} B$ 这个类型到 $(A\to B)$ 这个类型，有个 map. 对于任意一个 $p:A=_{\mathcal U} B$, 我们都能得到一个 $p_*: A \to B$，这个 $p_*$ 有个特殊的性质，它（together with other data）实际上构成了 $A$ 到 $B$ 的一个 equivalence. ——熟悉范畴论的读者应该不会觉得奇怪。

Equivalence 的定义在这里恕不展开了，只能说任给 $A, B : \mathcal U$，可以定义 type of equivalences $A\simeq B$). 用不严格的符号说，前述的 map $p\mapsto p_*$ 实际上给出了 identity type 到 type of equivalences 的一个 map. Voevodsky 引入的 univalence 公理说，这个 map 是一个 equivalence.

引入 univalence 公理相当于把终极的外延性 (extensionality) 引入了 type theory。说到底，extensionality 是关于什么时候能判定两个结构在某种意义下 “相同” 的公理，对于集合来说，这是很简单的。但是在通常的数学中，有些熟悉例子，两个很一致的东西（即关键的性质可以像前面说的那样 “搬来搬去” (transport)），不能说他们相等。比如任意两个 $n$ 维线性空间，我们只能说他们 “同构” 而不能说他们相等，因为有太多种方式把他们等同起来（选取基以后任意的 $n\times n$ 可逆矩阵都给出同构）；对于两个范畴，甚至只能说他们 “等价” 而不能说他们同构（因为在集合层面并不是一一对应）。这些褶皱，都能用 univalence axiom 一一抚平。

更体现 univalence axiom 威力的地方在于，有了 univalence axiom, 能很好地对任意的自然数 $n$ 定义 $n\text{-groupoid}$ （ $n\text{-type}$ ）——定义 $n\text{-groupoid}$ 或者 $(\infty,1)\text{-groupoid}$ 其实是很有意义的，也很困难（比如通常的 algebraic stacks 也就是 $n=2$ 的情形而已）。Grothendieck 在 *Esquisse d'un Programme* (*[Sketch of a Programme](http://www.landsburg.com/grothendieck/EsquisseEng.pdf)*) 的第七节 Pursuing Stacks 描绘了用 homotopic algebra 来定义 $n-\text{stack}$ 的可能性。Univalence axiom 可以看做对 Grothendieck 描绘的蓝图的一个回应。

## §5. 注释

1. 用 “瑞典人” 来描述 Martin-Löf 的主要原因是他太神，没法用 “数学家” 这样的词简单概括，引用 Wikipedia 第一句做个注解：**Per Erik Rutger Martin-Löf** (born May 8, 1942) is a Swedish logician, philosopher, and mathematical statistician.（逻辑学家，哲学家和数理统计学家）
2. Type theory 其实最早是罗素提出来的。这里介绍的是 Martin-Löf type theory. Martin-Löf 发展的 type theory 其实有好几个版本, 参见 [Intuitionistic type theory#Martin-Löf_Type_Theories](https://en.wikipedia.org/wiki/Intuitionistic_type_theory#Martin-L.C3.B6f_Type_Theories). 我认为 identity type 是最大的创新之一。
3. 计算机证明黎曼猜想和自然数的定义那个故事是编的，但是很有必要定义一种数学基础使得所有的命题都可以 “搬来搬去”，则是一种共识。“It should be impossible to formulate a statement which is not invariant with respect to equivalences.” ——T. Coquand
4. 让计算机理解集合论并没有文中说的那么困难，参见 [Mizar system](https://en.wikipedia.org/wiki/Mizar_system) —— A proof assistant based on first-order logic, in a natural deduction style, and [Tarski–Grothendieck set theory](https://en.wikipedia.org/wiki/Tarski–Grothendieck_set_theory). (Tarski-Grothendieck set theory 是 ZFC 的一个 non-conservertive extension, 添加了 Tarski 公理: 对任意一个集合! $x$ 存在一个 [Grothendieck universe](https://en.wikipedia.org/wiki/Grothendieck_universe) $U$ 使得 $x\in U$.)
5. 可能有读者会问 type theory 里这套 Programming 和 Mathematics 的对应和所谓的 [Curry-Howard Isomorphism](https://en.wikipedia.org/wiki/Curry–Howard_isomorphism) 有什么区别和联系, 实际上上述对应相当于把 Curry-Howard isomorphism 扩展到了 dependent type theory. 相当于 Curry–Howard isomorphism 加上了谓词逻辑的的强化版。
6. 集合论的 extensionality 公理的推论之一是，对于两个集合之间的函数 $f, g: X\to Y$, $f = g \iff \forall x \in X, f(x) = g(x)$ ： 因为作为 $X\times Y$ 的子集，$f,g$ 的图像 $\Gamma _f,\Gamma _g$ 在函数值完全相当的时候完全重合，所以作为集合相等。
7. 用不严谨的话讲，加入了 univalence axiom 的 type theory, 叫 homotopy type theory. 我故意在正文里避开了这个词。
8. Jacob Lurie 以集合论为基础来定义 $(\infty,1)\text{-groupoid}$, 做了很重要的工作，但他的工作与 homotopy type theory 无关。窃认为 Jacob Lurie 工作的困难程度可以反过来说明 homotopy type theory 的重要性。

## §6. 参考

1. 关于构造主义的一个比较耐读的参考 (40 pp.): **[Constructive Mathematics in Theory and Programming Practice](http://www.cse.chalmers.se/~coquand/TRIESTE/BridgesReeves.pdf)**, Douglas BRIDGES and Steve REEVES
2. [Constructive Mathematics (Stanford Encyclopedia of Philosophy)](http://plato.stanford.edu/entries/mathematics-constructive/)
3. 有一定数学背景，且对 Homotopy type theory 有兴趣的读者很有必要看看这三个 slides:
	- <http://www.cse.chalmers.se/~coquand/leeds1.pdf>
	- <http://www.cse.chalmers.se/~coquand/leeds2.pdf>
	- <http://www.cse.chalmers.se/~coquand/leeds3.pdf>

（题图：Wikipedia [File:Logic.svg](https://en.wikipedia.org/wiki/File:Logic.svg)）
