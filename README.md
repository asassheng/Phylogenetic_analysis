<font size="5">**目录**</font>

[TOC]


<font size="5">**写在最前**</font>
这个文档记录了我学习的Phylogenetics analysis的内容，这些内容将随着不断的学习不断地更新，而更新的频率就得取决于当时的课业:pear:了。由于刚刚接触这个领域，仅凭刚看的一点内容，对于许多知识还是一知半解，有可能存在错误的地方以及不足，还请大家发现后多多体谅并及时在issue里提出来或者直接在文档里修改后commit。也正因为这个原因，结果分析部分作为一个方法的精髓部分，本文中基本还没有，建议还是先看原文中的作者是如何解释的，这样更加专业。分析部分会待我觉得搞透后再着手。最后，很乐意大家提出一些学术上的问题来一起探讨，在探讨中更加深刻地学习知识。:blush:

++ 注：该Repository中出现的代码均为在**Windows Subsystem for Linux (WSL) - Ubuntu 18.04 LTS**下使用的代码 ++

- - -

# 系统进化分析（Phylogenetics analysis）

* 系统发生学（Phylogenetics）是研究生物进化规律及物种间亲缘关系的学科。学科的基本原则是++产生相似性的原因是共同祖先的存在++。一般的，它根据不同物种、群体、个体或者基因间的差异特征来进而构建系统进化树（Phylogenetic tree）来反映之间可能的关系。经典的系统进化学通过形态学、解剖学、以及地质学（化石）等来反映差异。最经典的例子就是达尔文在加拉帕戈斯群岛在通过观察不同鸟类的形态进而推断其进化关系从而提出自然选择假说。

* 现在，随着电子信息以及生物实验技术的快速发展，我们能获得到以及处理生物分子数据的能力也大大增强，为进一步探索未知，分子进化分析学毋庸置疑成为了现在主流的研究领域。

* 下面，我将介绍一下系统进化分析里常用的操作以及两个系统进化分析的主要应用，并进行简单的重复。

## 基本概念
> **Under construction**

## 基本操作
### 多重序列比对(Multiple Sequence alignment)
* 根据序列的相似性将多个序列对齐。对齐的软件有许多，具体可以查看[Wikipedia](https://en.wikipedia.org/wiki/List_of_sequence_alignment_software)(非最新)。在这里我将介绍目前比较常见的3中序列对齐程序。
	- **[Clustalo](http://www.clustal.org/omega/):**
	Clustal Omega对于任何数量的序列对齐表现都比较快与精确
	使用：`clustalo -i input.fasta -o output.fas -v`

	- **[MAFFT](https://mafft.cbrc.jp/alignment/software/)：**
	MAFFT能够快速对齐大量的序列或相对较长的序列，MAFFT对于序列间同源性高的序列对齐表现优秀，对于序列间变异度高的序列建议使用其它软件
	使用：MAFFT在行命令里有类似GUI的界面，因此按照提示输入或调整参数即可

	- **[MUSCLE](http://www.drive5.com/muscle/)：**
	MUSCLE对于中大型的序列（几千个分类群）对齐表现良好
	使用：`muscle -in input.fasta -out output.fasta`

### 相似图/差异图(Similarity Plot / Devisity Plot)
* 得到对齐后的序列后，我们可以通过画出不同病毒序列之间的相似性，直观的看出哪些片段序列之间的关联性，比如亲缘关系的远近，是否有重组的可能等。
* [**例子**](./example/simplot.md)

### 系统进化树(Plylogenetic tree)
* 产生系统进化树主要有两类方法。第一种是表型(Phenetic)分类法，它不需要任何历史的关系模型，通过测量不同物种之间的“距离”进行层次聚类（Hierarchical cluster）直接产生树；另一种是谱系分支(Cladistic)分类法，通过考虑所有可能的进化过程，从而回推共同祖先节点上的特点，然后根据其选择的进化模型选择其中最优树。一般来说谱系分支分类法优于表型分类法。

* 表型分类法目前主要有：UPGMA(Unweighted pair group method with arithmetic mean)、Neighbour-joining，两者的区别是Neighbour-joining将不同的进化分支的进化速度进行了加权。

* 谱系分支分类法目前主要有：Maximun parsimony、Maximun likelihood，这两种方法只能用于序列数据。谱系分支分类法的需要考虑可能的进化树随着物种个数增加而指数增长，如果过多的的话将会得出个大概的结果。为了解决这个问题，就需要有检验方法来检验结果，比如Jackknifing和Bootstrapping，常用的是Bootstrap法。
	* ***++思考：进化树上共同的节点表示的是什么？++***


* [**例子**](./example/phylogenetic_tree.md)

### 可视化
#### 多重序列可视化
* 序列文件本质上一连串的字符构成的文本，但这样的文本直接在论文里表示是不美观的，因此我们可以使用序列的查看软件来进行美化，而这样的程序也是各种各样的。序列可视化的软件有许多，具体可以查看[Wikipedia](https://en.wikipedia.org/wiki/List_of_alignment_visualization_software)(非最新)。在例子里，我将选取一些我认为在展示病毒序列可以较好使用的软件。

* [**例子**](./example/visualization_1.md)

#### 系统进化树可视化
* 虽然MEGA能够将生成的系统进化树可视化，但是只具有简单的调整功能，如果需要添加有关树的注释信息则需要用到其它专门的可视化软件。在树的可视化里，最基础的是添加树的注释信息的静态图像，这些像**[Figtree](http://tree.bio.ed.ac.uk/software/figtree/)、[iTOL](https://itol.embl.de/)、[ggtree](https://bioconductor.org/packages/release/bioc/html/ggtree.html)**(R package)等可以轻易做到。而更高级的是现在流行的可交互式的可视化，能够将注释信息附加到其它元件，并于其它图形相互搭配，可交互式的图像一般是由JavaScript编写的，比如**[figtree.js](https://github.com/rambaut/figtree.js/blob/master/README.md)、[PhyD3](https://phyd3.bits.vib.be/documentation.html)**等。

* 树的表示类型主要有4种，分别为RECTANGULAR、RADIAL、UNROOTED、CLOCK，其中CLOCK需要有时间的注释才能完成

* [**例子**](./example/visualization_2.md)

## 动态系统进化学分析（Phylodynamic analysis）
* 动态系统进化学分析是研究流行病学、免疫学和进化过程等潜在的其它因素对于构建系统进化树的影响。通过动态系统进化学分析，我们可以推断病毒流行的起源时间、帮助构造更稳定的传播模型参数或者反映病毒的控制力度等。

* [**例子**](./example/phylodynamic.md)

## 重组检测（Recombination detection）
* 冠状病毒的遗传变异主要包括突变和重组两类，这与大多数病毒相同。重组发生在共用同一宿主细胞的病毒之间，对于RNA病毒来说，重组的发生机制是拷贝选择(Copy choice)，拷贝选择是指RNA复制酶在合成RNA时从一条模板链转换到了另一条链上。对于冠状病毒科的病毒，由于其通过不连续的转录来合成mRNA的机制导致了在复制RNA时更频繁的模板转换。此外，重组在病毒进化中往往会给病毒带来较大的表型变化，因此对于在人群之间之前从未出现过的新冠病毒，我们有理由先考虑新冠病毒是可能是由于其它病毒重组而来的。

* 方法
	* 现许多方法可以让我们检测到重组的发生，但总的来说，它们在序列之间高差异性性与高重组率的情况下才更加精确，因此，一般要求序列之间至少5%的差异度以及数个重组事件来保证一定的检验功效。

	* 种类：

	> **Under construction**


* 案例分析

> **[Under construction](./example/Combination_detection.md)**




## 学习资料
* [**Virological**](http://virological.org/)
* [**Lesk, Arthur M. - Introduction to bioinformatics-Oxford University Press (2014)**](https://www.amazon.com/Introduction-Bioinformatics-Arthur-Lesk/dp/0198794142/ref=asc_df_0198794142/?tag=hyprod-20&linkCode=df0&hvadid=343206877892&hvpos=&hvnetw=g&hvrand=13717546636249817292&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9004338&hvtargid=pla-777337192964&psc=1&tag=&ref=&adgrpid=66484627102&hvpone=&hvptwo=&hvadid=343206877892&hvpos=&hvnetw=g&hvrand=13717546636249817292&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9004338&hvtargid=pla-777337192964)
* [**一文读懂进化树**](https://www.sohu.com/a/196872269_675868)
* [**Virus Evolution and Genetics**](https://www.sciencedirect.com/science/article/pii/B9780128031094000088)
* [**Recombination in viruses**](https://www.sciencedirect.com/science/article/pii/S156713481400478X?via%3Dihub#f0005)
