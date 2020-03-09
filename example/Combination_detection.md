# 重组检测
## 例1
* 在首次对新冠病毒测序后，我们得知新冠病毒属于乙型冠状病毒属，因此如果可以的话，我们将会使用乙型冠状病毒属里的所有序列，但是序列越多，计算量越大。在这里我们按照学者David在Virological发表的帖子“[nCoV’s relationship to bat coronaviruses & recombination signals (no snakes)](http://virological.org/t/ncovs-relationship-to-bat-coronaviruses-recombination-signals-no-snakes-no-evidence-the-2019-ncov-lineage-is-recombinant/331)”所使用的序列来简单重复一次关于重组检测的步骤。所需序列我存放在了data文件夹的sequences.fasta里，该文件可以通过NCBI的[Batch Entrez](https://www.ncbi.nlm.nih.gov/sites/batchentrez)**批量**下载序列的fasta文件，列表文件为accessions_list.seq。
	* ***++思考： 在第一次获得某种新的病毒序列时，进行重组检测的数据集应该是怎么选择？++***
* 数据文件：**data/simplot_example2.fasta**

* 所需软件：[**RDP5**](http://web.cbio.uct.ac.za/~darren/rdp.html)

* RDP5：
	* 打开对齐后的fasta文件，在这里我们可以看到fasta的序列以及序列相似度的信息;
	* 进入选项卡，Run->Auto RDP
