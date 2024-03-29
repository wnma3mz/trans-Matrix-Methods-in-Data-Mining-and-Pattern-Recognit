第十一章

文本挖掘

通过文本挖掘，我们指的是从大量且通常是非结构化的文本集合中提取有用信息的方法。另一个密切相关的术语是信息检索。一个典型的应用是搜索科学论文摘要数据库。例如，在医学应用中，人们可能希望找到数据库中处理特定综合征的所有摘要。因此，我们将一个搜索短语，一个查询，以及与综合症相关的关键字放在一起。然后利用检索系统将查询结果与数据库中的文档进行匹配，并向用户展示相关的文档，并根据相关度进行排序。

例11.1。以下是医疗集合中搜索的典型查询

# 摘要：

9。在心脏外科、神经外科、头部损伤和传染病中使用诱导性低温。

这个查询是从一个名为medline的测试集合中获取的，我们将这个查询称为q9。

库目录是文本挖掘应用程序的另一个示例。

例11.2。为了说明信息检索中的一个问题，我们在linko–ping大学图书馆期刊目录中进行了搜索：

| 搜索短语       | 结果                        |
| -------------- | --------------------------- |
| 计算机科学工程 | 找不到任何东西              |
| 计算机科学工程 | IEEE：计算输入   科学与工程 |

当然，我们希望系统对用户的小错误不敏感。任何人都可以看到IEEE日志接近查询。从

一百二十九

这个例子我们得出结论，在许多情况下，直接的词匹配是不够好的。

Web搜索引擎是一个非常著名的文本挖掘领域，它的搜索短语通常很短，而且常常有许多相关文档，因此将它们全部呈现给用户是不可能的。在该应用程序中，搜索结果的排名对于搜索引擎的效率至关重要。我们将在第12章中讨论这个问题。

有关信息检索的概述，请参见，例如[43]。在本章中，我们将简要介绍一种最常用的文本挖掘方法，即向量空间模型[81]。本文简要介绍了向量空间模型和一些变体：使用termdocument矩阵的SVD的潜在语义索引（LSI）、基于聚类的方法、非负矩阵分解和lgk双向化。有关与向量空间模型相关的不同技术的更详细说明，请参见[12]。

11.1文件和查询的预处理

在本节中，我们将讨论在建立特定文档集合的向量空间模型之前对文本进行的预处理。

在信息检索中，携带有关文档内容信息的关键字称为术语。信息检索的基本步骤是创建文档集合中所有术语的列表，即所谓的索引。对于每个术语，将存储包含该特定术语的所有文档的列表。这被称为反向索引。

但是在建立索引之前，必须完成两个预处理步骤：清除所有停止词和词干。

停止词实际上可以在任何文档中找到。因此，在文档中出现这样一个词并不能将此文档与其他文档区分开来。以下是一个特定停止列表的开头：

a，a，ability，about，above，accordinate，across，actually，after，after，again，again s t，ain，all，allow，allow，allow，already，already，already，already，虽然，总是，在，在，在，在，在，一，和，另一，任何人，任何人，任何人，任何东西，无论如何，任何地方，apaRT，出现，欣赏，恰当，是，不是，周围，作为，旁白，问…。

词干化是将每个共轭词或词干有一个后缀的词还原的过程。显然，从信息检索的角度来看，在以下简化中不会丢失任何信息：


 

11.2.向量空间模型

### 可计算计算计算

公共域词干算法在互联网上可用。

表11.1.medline集合的索引的开头。使用波特-斯坦默和GTP解析器[38]。

| 无堵塞                   | 有堵塞 |
| ------------------------ | ------ |
| 行动                     | 行动   |
| 动作激活                 | 活性剂 |
| 积极主动活动活动实际行动 | 实际的 |
| 实际上敏锐               | 阿奎蒂 |
| 严重的                   | 阿库特 |
| 广告                     | 广告   |
| 适应                     | 适应   |
| 自适应添加               | 添加   |
| 附加附加                 | 栓剂   |

例11.3。我们分析了medline集合中的1063个文档（实际上是30个查询和1033个文档），不管是否有词干，在这两种情况下都删除了停止词。为了保持一致性，必须对停止列表执行相同的词干。在第一种情况下，术语数为5839，在第二种情况下为4281。我们在表11.1中列出了部分术语列表。

11.2矢量空间模型

向量空间模型的主要思想是创建一个术语文档矩阵，其中每个文档都由列向量表示。该列在与文档中可以找到的术语相对应的位置上有非零条目。因此，每一行代表一个术语，并且在与可以找到该术语的文档相对应的位置上具有非零条目；参见第11.1节中的倒排索引。

第1章给出了术语文档矩阵的简化示例。在这里，我们手动计算术语的频率。对于实际问题，我们使用文本解析器来创建术语文档矩阵。[38113]中描述了两个公共域解析器。除非另有说明，我们已经将[113]中的例子用于本章中更大的示例。用于信息检索的文本分析器通常包括词干分析器和删除停止词的选项。此外，还有一些过滤器，例如用于删除文档中的格式代码，例如HTML或XML。

通常，不仅要计算文档中出现的术语，还要应用术语加权方案，其中a的元素根据文档集合的特性进行加权。同样，通常会进行文档加权。在[12，第3.2.1节]中描述了许多方案。例如，可以通过定义

aij=fij对数（n/ni），（11.1）

其中fij是术语频率，术语i出现在文档j中的次数，ni是包含术语i的文档数（反向文档频率）。如果一个术语经常出现在少数几个文档中，那么这两个因素都很大。在这种情况下，该术语在不同的文档组之间有很好的区别，并且（11.1）中的日志因子在出现的文档中赋予了很大的权重。

通常，术语文档矩阵是稀疏的：大多数矩阵元素等于零。然后，当然，避免存储所有的零，而是使用稀疏矩阵存储方案；参见第15.7节。

例11.4。对于使用gtp[38]解析的stemmed medline集合，矩阵（包括30个查询列）为4163×1063，其中48263个非零元素，即约1%。矩阵的前500行和前500列如图11.1所示。

### 11.2.1查询匹配与性能建模

查询匹配是查找与特定查询q相关的文档的过程。这通常使用余弦距离度量来完成：如果查询q和aj之间的角度足够小，则认为文档aj是相关的。同样，如果

，

其中tol是一个预定义的公差。如果减小了公差，则返回更多的文档，其中许多文档可能与查询相关。但在

11.2.向量空间模型

​                                                  

图11.1.medline矩阵的前500行和列。每个点代表一个非零元素。

同时，存在这样的风险：当公差降低时，也会返回越来越多与之无关的文档。

例11.5。我们在stemmed medline集合中对查询q9进行了查询匹配。对于cosine测量，tol=0.19，只有文件409被认为是相关的。当公差降低到0.17时，还检索到文件415和467。

我们在与图11.2中的两个公差值匹配的查询中说明了不同类别的文档。当返回的两组文档与相关文档的交集尽可能大，返回的无关文档数较少时，查询匹配会产生良好的结果。对于高公差值，检索到的文件可能是相关的（图11.2中的小圆圈）。当余弦公差降低时，交集增加，但同时返回更多无关文档。

在信息检索的性能建模中，我们定义了以下度量：

精度：，（11.2）

其中dr是检索到的相关文档数，dt是总数

​                                                                                                                      



















图11.2.两个公差值的检索和相关文件。虚线圆圈表示为高余弦公差值检索到的文档。

检索到的文档数，以及

召回：，（11.3）

其中nr是数据库中相关文档的总数。由于cosine测量的tol值很大，因此我们希望具有较高的精度，但召回率较低。对于一个小的TOL值，我们将有高召回，但低精度。

在评估不同的信息检索方法和模型时，通常会使用一些查询。出于测试目的，所有文档都已由人工读取，并且与某个查询相关的文档都已标记。这使得绘制回忆与精确的图表成为可能，以说明某一信息检索方法的性能。

例11.6。我们使用cosine度量对medline集合（stemmed）中的查询q9进行了查询匹配。对于公差的特定值，我们从（11.2）和（11.3）中计算出相应的召回和精度。通过将公差从接近1变为0，我们得到了召回和精度的向量，这些向量给出了有关此查询的检索方法质量的信息。在不同方法的比较中，如图11.3所示，说明了绘制召回与精确图。理想情况下，一种方法在精度较高的同时具有较高的召回率。因此，曲线越靠近右上角，检索质量越高。

在本例和以下示例中，使用术语频率和反向文档频率加权（11.1）计算矩阵元素。

11.3.潜在语义索引

​                                                



​     

​     



​     

​     



​     

​     



​     



​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     



​     

​     

​     

​     

​     

​     













图11.3.使用向量空间方法查询Q9的匹配。回忆与精确。

11.3潜在语义索引

潜在语义索引（LSI）[28，9]是基于数据中存在一些潜在的潜在语义结构的假设。它被广泛使用的字所破坏，并且可以通过使用SVD将数据（术语文档矩阵和查询）投影到低维空间来发现和增强这种语义结构。

设a=u∑v t为术语文档矩阵的svd，并用秩k的矩阵进行近似：

| *A*               ≈ |      |
| ------------------- | ---- |
|                     |      |

.

UK列位于文档空间中，是我们用来近似文档的正交基础。根据列向量写出hk，hk=（h1，h2，…，hn）。从a≈ukhk我们得到a j≈ukhj，这意味着hk的j列在正交基上保持了j号文件的坐标。使用秩k近似，术语文档矩阵表示为ak=ukhk，在查询匹配中，我们计算qtak=qtukhk=（uktq）thk。因此，我们根据新的文档基础计算查询的坐标，并根据

（11.4）

这意味着查询匹配是在k维空间中执行的。

例11.7。我们在medline集合中对q9进行了查询匹配，使用秩100的截断SVD近似矩阵。

​                                                     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     

​     

​     

​     

​     

​     





​     

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        

​        









图11.4.查询Q9的匹配。全向量空间模型（实线）和秩100近似（虚线和菱形）的回忆与精度。

召回精度曲线如图11.4所示。可以看到，对于这个查询，LSI提高了检索性能。在图11.5中，我们还证明了许多术语文档矩阵所共有的一个事实：它是相当好的条件，并且在奇异值序列中没有间隙。因此，我们无法通过检验奇异值来找到合适的LSI近似等级，必须通过检索实验来确定。

另一个值得注意的事实是，当k=100时，矩阵近似中的近似误差，

，

是大的，而且我们仍然得到改进的检索性能。鉴于术语文档矩阵的截断SVD近似存在较大的近似误差，

11.3.潜在语义索引

   

图11.5.medline（stemmed）矩阵的前100个奇异值。矩阵列按欧几里得长度单位进行缩放。

人们可能会质疑“最佳”奇异向量是否构成表示术语文档矩阵的最佳基础。另一方面，由于我们得到了如此好的结果，一个更自然的结论可能是，frobenius规范不是术语文档矩阵中信息内容的良好度量。

同样有趣的是，看看数据中最重要的“方向”是什么。从定理6.6我们知道，前几个左奇异向量是文档空间中的主要方向，它们的最大分量应该指示这些方向是什么。matlab语句find（abs（u（：，k））>0.13）结合术语索引中的查找，得出k=1,2的以下结果：

| U（：，1） | U（：，2）          |
| ---------- | ------------------- |
| 细胞       | 案例                |
| 生长       | 细胞                |
| 激素       | 儿童                |
| 病人       | 缺陷DNA生长患者心室 |

在第13章中，我们将回到从文本中提取关键字的问题。

应该说，LSI并没有为medline集合中的所有查询提供显著更好的结果：有些LSI提供的结果与全向量模型相当，有些LSI提供的性能较差。然而，重要的往往是平均性能。

在[52]中对LSI的不同方面进行了系统研究。结果表明，LSI对降秩k的极小值具有较好的检索性能，同时相对矩阵逼近误差较大。很可能无法证明任何通用的结果来解释LSI可以以何种方式和为哪些数据改进检索性能。相反，我们给出了一个人工的例子（在[12]中使用类似的思想作为相应的例子构造），给出了部分解释。

例11.8。考虑示例1.1中的术语文档矩阵和查询“网页排名”。显然，文档1-4与查询相关，而文档5完全无关。但是，我们得到查询的余弦值和原始数据

，

表示文档5（足球文档）与查询的相关性与文档4相同。此外，由于文档1中没有查询词，因此此文档与查询是正交的。

然后我们计算术语文档矩阵的SVD，并使用秩2近似。投影到二维子空间后，根据（11.4）计算的余弦为：

.

原来，文档1被认为与原始表示形式中的查询完全无关，现在它具有高度相关性。此外，相关文件2-4的余弦值也得到了加强。同时，文件5的余弦值已显著降低。因此，在这个人工例子中，维度约简提高了检索性能。

在图11.6中，我们绘制了前两个左奇异向量坐标系中的五个文档和查询。显然，在这个表示中，第一个文档比文档5更接近查询。前两个左奇异向量是

，

奇异值是∑=diag（2.8546，1.8823，1.7321，1.2603，0.8483）。a中的前四列通过google、matrix等词进行强耦合，并且


 

11.4.聚类

​                                                     



​     

​     



​     

​     



​     

​     



​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     



​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     











​     

​     



















图11.6.五个文档和查询投影到前两个左奇异向量的坐标系中。

这些词是文档集的主要内容（参见单数值）。这显示在U1的组成中。因此，即使查询中没有一个词与文档1匹配，该文档也与主导方向紧密相关，因此它在简化表示中变得相关。

11.4聚类

在文档集合的情况下，很自然地假定存在内容相似的文档组。如果我们将文档看作是RM中的点，那么我们可以将组可视化为集群。通过平均值即质心来表示每个簇，我们可以根据质心来压缩数据。因此，例如，使用k-均值算法的聚类是术语文档矩阵的低阶近似的另一种方法。集群在信息检索中的应用在[30，76，77]中进行了描述。

与LSI类似，质心（归一化但非正交）的矩阵ck∈rm×k可作为“文档空间”中的一个近似基，查询匹配则需要在此基础上确定所有文档的坐标。这可以通过求解矩阵最小二乘问题来实现。

.

然而，首先对C的柱进行正交化比较方便，即计算C的二维分解。

ck=pkr，

解决


 

pk∈rm×k，r∈rk×k，


 

（11.5）

单独编写−pkgk的每一列，我们看到这个矩阵最小二乘问题等价于n个独立的标准最小二乘问题。

   

其中，gj是gk中的j列。由于pk有正态柱，我们得到gj=pktaj，（11.5）的解为

   

为了匹配查询q，我们计算产品

，

其中qk=pktq。因此，低维近似中的余弦是

.

例11.9。我们对medline集合的q9进行了查询匹配。在计算聚类之前，我们将列标准化为相等的欧几里得长度。我们使用正交归一化的质心将矩阵从一个聚类中近似为50个聚类。召回精度图如图11.7所示。我们发现，对于高回忆值，质心法和等级加倍的LSI法一样好；见图11.4。

对于等级50，质心法中的近似误差，

，

甚至比100级的LSI还要高。

改进后的性能可以用与LSI类似的方式来解释。作为集群的“平均文档”，质心捕获集群中主要文档之间的主要链接。通过用形心表达所有文档，强调了主要的链接。

当我们测试Medline集合中的所有30个查询时，我们发现秩等于50的质心方法与秩100的LSI具有相似的性能：有些查询的全向量空间模型更好，但也有一些查询的质心方法更好。好多了。

11.5.非负矩阵分解

​                                                     



​     

​     



​     

​     



​     

​     



​     

​     



​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     

​     

​     

​     

​     

​     





​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     









图11.7.查询Q9的匹配。全矢量空间模型（实线）和秩50质心近似（实线和圆）的回忆与精度。

11.5非负矩阵分解

假设我们已经计算出了术语文档矩阵的近似非负矩阵分解，

a≈w h，w≥0，h≥0，

式中，h的w∈rm×k和h∈rk×n。h的j列在由w列组成的近似非正交基中保持j文件的坐标。我们首先要通过求解最小二乘问题min来确定在同一基中查询向量q的表示。然后，在这里在此基础上，我们计算查询和所有文档向量之间的角度。考虑到w的薄qr分解，

W=qr，P∈Rm×K，R∈Rk×K，

缩减基础中的查询是

Q_=R−1qtq，

文件j的余弦是

.


 

​                                                     



​     

​     



​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     



​     

​     

​     

​     

​     

​     

​     





​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     

​     









图11.8.查询Q9的匹配。全向量空间模型（实线）和秩50非负矩阵近似（虚线和×）的回忆与精度。

例11.10。我们使用中描述的100次乘法算法迭代计算了medline termdocument矩阵的秩50近似值。

第9.2条相对近似误差约为0.89。查询q9的调用精度曲线如图11.8所示。

11.6 LGK标准化

到目前为止，在本章中，我们已经描述了三种改进信息检索向量空间方法的方法，即通过基于SVD、聚类和非负矩阵分解的低阶近似表示术语文档矩阵A。这三种方法有一个共同的缺点：当添加或删除新文档时，更新低阶近似值的成本很高。在第7章中，我们描述了一种计算与最小二乘问题有关的低阶近似值的方法，在lgk双向化中使用右手边作为起始向量。在这里，我们将把这种方法应用于文本挖掘问题，这样就可以为每个查询计算一个新的低阶近似值。因此，在更改文档收集时不需要额外的计算成本。另一方面，每个查询匹配的工作量会变大。本节的灵感来源于[16]。

给定一个查询向量Q，我们应用递归的LGK双向化算法（或PLS）。

11.6.LGK标准化

​             

### 查询Q的lgk bidialogization

​             

\1.    β1p1=q，z0=0

\2.    当i=1:kαizi=atpi−βizi−1βi+1pi+1=azi−αipi时

### 三。结束

确定系数αi−1和βi，以便

​             

向量pi和zi收集在矩阵中，并且

. 在这个过程的k个步骤之后，我们生成了一个k级

近似值；见（7.16）。我们在下面的命题中总结了推导过程。

提案11.11.让azk=pk+1bk+1是lgk的k步的结果。

递归，并让

   

是双矩阵bk+1的qr分解。那么我们有一个秩k近似值

，（11.6）

哪里

.

使用低秩近似（11.6）进行查询匹配的方法与LSI中使用SVD低秩近似的方法大致相同。然而，如果使用以下方法，结果表明[16]获得了更好的性能。

wk的列向量是接近查询q的文档的正交近似基础。我们现在选择根据该基础计算查询的投影，而不是根据该基础计算a的列的坐标：

.

然后我们用余弦度量

，（11.7）

   

图11.9.查询Q9的匹配。上图显示了相对残差，它是LGK双向化（实线和×）步骤数的函数。作为比较，给出了基于第一奇异向量（主成分回归）的残差（虚线）。在底图中，我们给出了全矢量空间模型（实线）的回忆与精度，以及两步（实线和+s）和八步（实线和s）的二元化。

也就是说，我们计算投影查询和原始文档之间角度的余弦。

例11.12。我们以q9作为起始向量进行了lgk双向化。结果表明，相对残差下降相当缓慢，略低于0.8；见图11.9。不过，经过两个步骤，该方法已经给出了

11.7.平均性能

比全矢量空间模型要好得多。也可以看出，八个步骤的双诊断结果更差。

实例11.12表明，由LGK双标准化得到的低阶近似在降噪方面具有与LSI和基于形心的方法相似的性质。值得注意的是，当查询向量用于影响第一个基向量时，较低的秩（在本例中为2）会给出几乎相同的检索结果。另一方面，当步数增加时，精度变差，接近全矢量空间模型。这是自然的，因为低阶近似逐渐变得更好，经过大约8个步骤后，它几乎代表了termdocument矩阵中与查询相关的所有信息，从全向量空间的意义上来说。

模型。

为了确定应该执行多少个递归步骤，可以监视最小二乘残差：在哪里

；

参见（7.14）。当残差范数大幅减少时，我们可以假设查询是由文档的线性组合来表示的。然后我们可以期望性能与全向量空间模型的性能大致相同。因此，为了比全向量空间模型有更好的性能，应该在残差曲线开始变平之前停止。

11.7平均性能

应在多个测试集上进行比较不同信息检索方法的实验。此外，一个人不仅应该使用一个查询，还应该使用一系列查询。

例11.13。我们测试了medline集合中的30个查询，并计算了本章介绍的五种方法的平均精度召回曲线。为了计算要比较的方法的平均精度，有必要

   

图11.10.查询匹配Medline集合中的所有30个查询。所采用的方法有：全矢量空间法（实线）、100阶LSI（虚线和菱形）、50阶形心近似（实线和圆）、50阶非负矩阵分解（虚线和×s）、LGK二级化（实线和＋s）。

以特定的召回值，比如5、10、15、…，90%对其进行评估。我们通过线性插值得到这些。

结果如图11.10所示。结果表明，与全向量空间模型相比，100阶LSI、50阶形心近似、非负矩阵因子分解和LGK二值化两个步骤的平均精度都有较大提高。

从示例11.13中我们看到，对于medline测试集合，基于术语文档矩阵的低阶近似的方法都比全向量空间模型表现得更好。当然，要支付的价格是更多的计算。在LSI、形心近似和非负矩阵分解的情况下，额外的计算可以离线进行，即与查询匹配分离。如果将文档添加到集合中，则必须重新计算近似值，这可能会很昂贵。另一方面，该方法基于LGK双向化，执行与查询匹配相关的额外计算。因此，它可以在术语文档矩阵经常发生变化的情况下有效地使用。

其他测试集合也得到了类似的结果；参见，例如[11]。然而，文本文档的结构起着作用。例如，在[52]中，表明LSI对医学文摘的性能比《时代》杂志的文章要好得多。


 