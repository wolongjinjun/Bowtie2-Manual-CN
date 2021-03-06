# Bowtie2-Manual-CN
Brief-简介

This is the Chinese translation of [Bowtie2's Manual](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml).
[Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml) is a very popular aligner for Next Generation Sequencing data. Since most of the Chinese tutorials are incomplete, we create this project to put the translation of official manual here. We are tring our best to finish it as good as we can and as soon as possible. Hope more people join us to make it better. Even one sentence sometimes makes a huge difference, like one single base dose.

这是[Bowtie2使用手册](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml)的中文翻译。
[Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml)是常用的第二代高通量测序数据比对软件。由于大多中文教程没能给大家一个完整的说明，我们创建了这个项目来翻译官网的使用说明。我们正在尽最大的努力翻译地更好、更快，希望有更多的朋友加入进来。就算只是一个句子，有时也会产生巨大的影响，就像单个碱基一样。

## Translation-译文

[Manual 使用手册](http://cncbi.github.io/Bowtie2-Manual-CN/)

###Getting started with Bowtie 2: Lambda phage example-从这里开始使用Bowtie2：λ噬菌体的例子
Bowtie2自带了一些入门级的示例文件，这些示例文件并不具有科学含义，我们用[λ噬菌体](https://en.wikipedia.org/wiki/Lambda_phage)的参考基因组只是因为它很短，并且例子里面的reads是由一个电脑程序生成的而不是测序的结果。但是，这些文件能让你立即开始运行Bowtie2和下游的程序。

首先按照[获取Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#obtaining-bowtie-2)的指导下载它。设置Bowtie2环境变量*BT2_HOME*，把它指向含有*bowtie2, bowtie2-build*和*bowtie2-inspect*二进制文件的新Bowtie2的文件夹。这一步很重要，因为在下面的命令当中，变量*BT2_HOME*被用来代表那个文件夹的位置。

#####Indexing a reference genome-对参考基因组建立索引
为了对Bowtie2内置的[λ噬菌体](https://en.wikipedia.org/wiki/Lambda_phage)的参考基因组建索引，先新建一个临时文件夹（建在哪里无所谓），进入那个文件夹，然后运行：
```bash
$BT2_HOME/bowtie2-build $BT2_HOME/example/reference/lambda_virus.fa lambda_virus
```
这条命令在结束前应该会打印很多行输出。当其运行完毕时，当前文件夹会产生4个新的文件，它们的文件名都以*lambda_virus*开始，分别以*.1.bt2, .2.bt2, .3.bt2, .4.bt2, .rev.1.bt2*和*.rev.2.bt2*结束。这些文件构成了索引————你完成了！

你可以使用*bowtie2-build*对一组任意来源的FASTA文件构建索引，包括像[UCSC](http://genome.ucsc.edu/cgi-bin/hgGateway)，[NCBI](http://www.ncbi.nlm.nih.gov/sites/genome)，和[Ensembl](http://www.ensembl.org/)这些站点。当对多个FASTA文件建立索引时，你要在指定所有的文件，并用逗号隔开。更多关于如何用bowtie2-build建立索引的信息，请查看[使用手册的建立索引部分](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#the-bowtie2-build-indexer)。你可能也会直接获取一个已经建好的索引，从而绕过这一步。[使用已建好的索引](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#using-a-pre-built-index)给出了例子。

#####Aligning example reads-比对示例reads
在上一步创建的文件夹中，现在含有lambda_virus的索引文件。接下来，运行：
```bash
$BT2_HOME/bowtie2 -x lambda_virus -U $BT2_HOME/example/reads/reads_1.fq -S eg1.sam
```
这个命令会运行Bowtie2的比对软件，它会使用上一步建立的索引，把一组非双端测序的reads比对到[λ噬菌体](https://en.wikipedia.org/wiki/Lambda_phage)的参考基因组上。这步比对的结果是SAM格式的，输出文件是*eg1.sam*，同时比对的总结会被输出到终端控制台。（事实上，总结是被写进了“standard error” 或 “stderr”，即标准错误句柄里面，通常它会被输出到终端。）

要查看SAM结果的前几行，运行：
```bash
head eg1.sam
```
你会看到类似于下面的东西：
```
@HD VN:1.0  SO:unsorted
@SQ SN:gi|9626243|ref|NC_001416.1|  LN:48502
@PG ID:bowtie2  PN:bowtie2  VN:2.0.1
r1  0   gi|9626243|ref|NC_001416.1| 18401   42  122M    *   0   0   TGAATGCGAACTCCGGGACGCTCAGTAATGTGACGATAGCTGAAAACTGTACGATAAACNGTACGCTGAGGGCAGAAAAAATCGTCGGGGACATTNTAAAGGCGGCGAGCGCGGCTTTTCCG  +"@6<:27(F&5)9)"B:%B+A-%5A?2$HCB0B+0=D<7E/<.03#!.F77@6B==?C"7>;))%;,3-$.A06+<-1/@@?,26">=?*@'0;$:;??G+:#+(A?9+10!8!?()?7C>  AS:i:-5 XN:i:0  XM:i:3  XO:i:0  XG:i:0  NM:i:3  MD:Z:59G13G21G26    YT:Z:UU
r2  0   gi|9626243|ref|NC_001416.1| 8886    42  275M    *   0   0   NTTNTGATGCGGGCTTGTGGAGTTCAGCCGATCTGACTTATGTCATTACCTATGAAATGTGAGGACGCTATGCCTGTACCAAATCCTACAATGCCGGTGAAAGGTGCCGGGATCACCCTGTGGGTTTATAAGGGGATCGGTGACCCCTACGCGAATCCGCTTTCAGACGTTGACTGGTCGCGTCTGGCAAAAGTTAAAGACCTGACGCCCGGCGAACTGACCGCTGAGNCCTATGACGACAGCTATCTCGATGATGAAGATGCAGACTGGACTGC (#!!'+!$""%+(+)'%)%!+!(&++)''"#"#&#"!'!("%'""("+&%$%*%%#$%#%#!)*'(#")(($&$'&%+&#%*)*#*%*')(%+!%%*"$%"#+)$&&+)&)*+!"*)!*!("&&"*#+"&"'(%)*("'!$*!!%$&&&$!!&&"(*"$&"#&!$%'%"#)$#+%*+)!&*)+(""#!)!%*#"*)*')&")($+*%%)!*)!('(%""+%"$##"#+(('!*(($*'!"*('"+)&%#&$+('**$$&+*&!#%)')'(+(!%+ AS:i:-14    XN:i:0  XM:i:8  XO:i:0  XG:i:0  NM:i:8  MD:Z:0A0C0G0A108C23G9T81T46 YT:Z:UU
r3  16  gi|9626243|ref|NC_001416.1| 11599   42  338M    *   0   0   GGGCGCGTTACTGGGATGATCGTGAAAAGGCCCGTCTTGCGCTTGAAGCCGCCCGAAAGAAGGCTGAGCAGCAGACTCAAGAGGAGAAAAATGCGCAGCAGCGGAGCGATACCGAAGCGTCACGGCTGAAATATACCGAAGAGGCGCAGAAGGCTNACGAACGGCTGCAGACGCCGCTGCAGAAATATACCGCCCGTCAGGAAGAACTGANCAAGGCACNGAAAGACGGGAAAATCCTGCAGGCGGATTACAACACGCTGATGGCGGCGGCGAAAAAGGATTATGAAGCGACGCTGTAAAAGCCGAAACAGTCCAGCGTGAAGGTGTCTGCGGGCGAT  7F$%6=$:9B@/F'>=?!D?@0(:A*)7/>9C>6#1<6:C(.CC;#.;>;2'$4D:?&B!>689?(0(G7+0=@37F)GG=>?958.D2E04C<E,*AD%G0.%$+A:'H;?8<72:88?E6((CF)6DF#.)=>B>D-="C'B080E'5BH"77':"@70#4%A5=6.2/1>;9"&-H6)=$/0;5E:<8G!@::1?2DC7C*;@*#.1C0.D>H/20,!"C-#,6@%<+<D(AG-).?&#0.00'@)/F8?B!&"170,)>:?<A7#1(A@0E#&A.*DC.E")AH"+.,5,2>5"2?:G,F"D0B8D-6$65D<D!A/38860.*4;4B<*31?6  AS:i:-22    XN:i:0  XM:i:8  XO:i:0  XG:i:0  NM:i:8  MD:Z:80C4C16A52T23G30A8T76A41   YT:Z:UU
r4  0   gi|9626243|ref|NC_001416.1| 40075   42  184M    *   0   0   GGGCCAATGCGCTTACTGATGCGGAATTACGCCGTAAGGCCGCAGATGAGCTTGTCCATATGACTGCGAGAATTAACNGTGGTGAGGCGATCCCTGAACCAGTAAAACAACTTCCTGTCATGGGCGGTAGACCTCTAAATCGTGCACAGGCTCTGGCGAAGATCGCAGAAATCAAAGCTAAGT(=8B)GD04*G%&4F,1'A>.C&7=F$,+#6!))43C,5/5+)?-/0>/D3=-,2/+.1?@->;)00!'3!7BH$G)HG+ADC'#-9F)7<7"$?&.>0)@5;4,!0-#C!15CF8&HB+B==H>7,/)C5)5*+(F5A%D,EA<(>G9E0>7&/E?4%;#'92)<5+@7:A.(BG@BG86@.G AS:i:-1 XN:i:0  XM:i:1  XO:i:0  XG:i:0  NM:i:1  MD:Z:77C106 YT:Z:UU
r5  0   gi|9626243|ref|NC_001416.1| 48010   42  138M    *   0   0   GTCAGGAAAGTGGTAAAACTGCAACTCAATTACTGCAATGCCCTCGTAATTAAGTGAATTTACAATATCGTCCTGTTCGGAGGGAAGAACGCGGGATGTTCATTCTTCATCACTTTTAATTGATGTATATGCTCTCTT  9''%<D)A03E1-*7=),:F/0!6,D9:H,<9D%:0B(%'E,(8EFG$E89B$27G8F*2+4,-!,0D5()&=(FGG:5;3*@/.0F-G#5#3->('FDFEG?)5.!)"AGADB3?6(@H(:B<>6!>;>6>G,."?%  AS:i:0  XN:i:0  XM:i:0  XO:i:0  XG:i:0  NM:i:0  MD:Z:138    YT:Z:UU
r6  16  gi|9626243|ref|NC_001416.1| 41607   42  72M2D119M   *   0   0   TCGATTTGCAAATACCGGAACATCTCGGTAACTGCATATTCTGCATTAAAAAATCAACGCAAAAAATCGGACGCCTGCAAAGATGAGGAGGGATTGCAGCGTGTTTTTAATGAGGTCATCACGGGATNCCATGTGCGTGACGGNCATCGGGAAACGCCAAAGGAGATTATGTACCGAGGAAGAATGTCGCT 1H#G;H"$E*E#&"*)2%66?=9/9'=;4)4/>@%+5#@#$4A*!<D=="8#1*A9BA=:(1+#C&.#(3#H=9E)AC*5,AC#E'536*2?)H14?>9'B=7(3H/B:+A:8%1-+#(E%&$$&14"76D?>7(&20H5%*&CF8!G5B+A4F$7(:"'?0$?G+$)B-?2<0<F=D!38BH,%=8&5@+ AS:i:-13    XN:i:0  XM:i:2  XO:i:1  XG:i:2  NM:i:4  MD:Z:72^TT55C15A47  YT:Z:UU
r7  16  gi|9626243|ref|NC_001416.1| 4692    42  143M    *   0   0   TCAGCCGGACGCGGGCGCTGCAGCCGTACTCGGGGATGACCGGTTACAACGGCATTATCGCCCGTCTGCAACAGGCTGCCAGCGATCCGATGGTGGACAGCATTCTGCTCGATATGGACANGCCCGGCGGGATGGTGGCGGGG -"/@*7A0)>2,AAH@&"%B)*5*23B/,)90.B@%=FE,E063C9?,:26$-0:,.,1849'4.;F>FA;76+5&$<C":$!A*,<B,<)@<'85D%C*:)30@85;?.B$05=@95DCDH<53!8G:F:B7/A.E':434> AS:i:-6 XN:i:0  XM:i:2  XO:i:0  XG:i:0  NM:i:2  MD:Z:98G21C22   YT:Z:UU
```
头几行（以@开始的）是SAM的头文件，余下的部分是SAM的比对结果，每行代表一个read或mate。更多细节，请查看[Bowtie2使用手册的SAM输出部分](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#sam-output)和[SAM格式标准](http://samtools.sourceforge.net/SAM1.pdf)。

#####Paired-end example-双端测序示例
要比对Bowtie2自带的双端测序reads，继续在同样的文件夹下，运行：
```bash
$BT2_HOME/bowtie2 -x lambda_virus -1 $BT2_HOME/example/reads/reads_1.fq -2 $BT2_HOME/example/reads/reads_2.fq -S eg2.sam
```
这个命令会比对一组双端测序的reads到参考基因组上，结果文件输出在了eg2.sam里面。

#####Local alignment example-局部对比示例
要使用[局部对比](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#end-to-end-alignment-versus-local-alignment)比对Bowtie2自带的一些更长的reads，继续在同样的文件夹下，运行：
```bash
$BT2_HOME/bowtie2 --local -x lambda_virus -U $BT2_HOME/example/reads/longreads.fq -S eg3.sam
```
这会使用局部比对，把长reads比对到参考基因组上，结果文件在eg3.sam里面。

#####Using SAMtools/BCFtools downstream-使用SAMtools/BCFtools做下游分析
[SAMtools](http://samtools.sourceforge.net/)是一个用来处理和分析SAM和BAM比对文件的集成工具包。[BCFtools](http://samtools.sourceforge.net/mpileup.shtml)是一个用来识别变异和处理VCF和BCF文件的集成工具包，通常它会被集成在SAMtools里面。把这些工具合起来使用，可以让你从SAM格式的比对文件中获取VCF格式中的被识别的变异。下面的例子假设你已经安装了*samtools*和*bcftools*，而且含有那些工具的二进制文件的文件夹地址已经在你的[PATH环境变量](http://en.wikipedia.org/wiki/PATH_(variable))里了。

运行双端测序的示例：
```bash
$BT2_HOME/bowtie2 -x $BT2_HOME/example/index/lambda_virus -1 $BT2_HOME/example/reads/reads_1.fq -2 $BT2_HOME/example/reads/reads_2.fq -S eg2.sam
```
使用*samtools view*把这个SAM文件转换成一个BAM文件。BAM是与SAM文字格式相对应的二进制格式。运行：
```bash
samtools view -bS eg2.sam > eg2.bam
```
使用*samtools sort*把这个BAM文件转换成排过序的BAM文件。
```bash
samtools sort eg2.bam eg2.sorted
```
现在我们有一个排过序的BAM文件了，它的名字是*eg2.sorted.bam*。排序后的BAM是一个有用的格式，因为这些比对都是（a）被压缩过的，这样有利于长期存储，（b）排过序的，这样有利于发现变异。要生成VCF格式的变异识别文件，运行：
```bash
samtools mpileup -uf $BT2_HOME/example/reference/lambda_virus.fa eg2.sorted.bam | bcftools view -bvcg - > eg2.raw.bcf
```
之后要查看这些变异，运行：
```bash
bcftools view eg2.raw.bcf
```
更多细节和这一流程的一些变化，请查阅SAMtools的官方指南：[用SAMtools/BCFtools识别SNPs/INDELs（单核苷酸多态/插入删除）](http://samtools.sourceforge.net/mpileup.shtml)。




###Other parts are being translated-其他部分正在翻译中
