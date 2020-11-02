# mode_mate
通过集成学习做帕金森人脸评分

该项目是处于探索阶段的一个项目，通过计算机视觉对帕金森的面部进行评分

### 人脸识别文献调研

特征脸法（Eigenface）
特征脸技术是近期发展起来的用于人脸或者一般性刚体识别以及其它涉及到人脸处理的一种方法。使用特征脸进行人脸识别的方法首先由Sirovich和Kirby（1987）提出（《Low-dimensional procedure forthe characterization of human faces》），并由Matthew Turk和Alex Pentland用于人脸分类（《Eigenfaces for recognition》）。首先把一批人脸图像转换成一个特征向量集，称为“Eigenfaces”，即“特征脸”，它们是最初训练图像集的基本组件。识别的过程是把一副新的图像投影到特征脸子空间，并通过它的投影点在子空间的位置以及投影线的长度来进行判定和识别。

将图像变换到另一个空间后，同一个类别的图像会聚到一起，不同类别的图像会聚力比较远，在原像素空间中不同类别的图像在分布上很难用简单的线或者面切分，变换到另一个空间，就可以很好的把他们分开了。
Eigenfaces选择的空间变换方法是PCA（主成分分析），利用PCA得到人脸分布的主要成分，具体实现是对训练集中所有人脸图像的协方差矩阵进行本征值分解，得到对应的本征向量，这些本征向量就是“特征脸”。每个特征向量或者特征脸相当于捕捉或者描述人脸之间的一种变化或者特性。这就意味着每个人脸都可以表示为这些特征脸的线性组合。
局部二值模式（Local Binary Patterns，LBP）
局部二值模式（Local binary patterns LBP）是计算机视觉领域里用于分类的视觉算子。LBP，一种用来描述图像纹理特征的算子，该算子由芬兰奥卢大学的T.Ojala等人在1996年提出（《A comparative study of texturemeasures with classification based on featured distributions》）。2002年，T.Ojala等人在PAMI上又发表了一篇关于LBP的文章（《Multiresolution gray-scale androtation invariant texture classification with local binary patterns》）。这一文章非常清楚的阐述了多分辨率、灰度尺度不变和旋转不变、等价模式的改进的LBP特征。LBP的核心思想就是：以中心像素的灰度值作为阈值，与他的领域相比较得到相对应的二进制码来表示局部纹理特征。

LBP是提取局部特征作为判别依据的。LBP方法显著的优点是对光照不敏感，但是依然没有解决姿态和表情的问题。不过相比于特征脸方法，LBP的识别率已经有了很大的提升。
Fisherface
线性鉴别分析在降维的同时考虑类别信息，由统计学家Sir R. A.Fisher1936年发明（《The useof multiple measurements in taxonomic problems》）。为了找到一种特征组合方式，达到最大的类间离散度和最小的类内离散度。这个想法很简单：在低维表示下，相同的类应该紧紧的聚在一起，而不同的类别尽量距离越远。1997年，Belhumer成功将Fisher判别准则应用于人脸分类，提出了基于线性判别分析的Fisherface方法（《Eigenfaces vs. fisherfaces:Recognition using class specific linear projection》）

来自 <https://www.sohu.com/a/258863246_651893> 

- 最终选择了dlib人脸识别模型

### 特征提取

对眼睛的纵横比进行时序提取，然后再次提取数学特征

