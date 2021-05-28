# TextClassification_CNN2

数据源过大，无法上传，所以存在了网盘里。<br>
链接：https://pan.baidu.com/s/1SvRR37harMQwpOAKE5ePbA 
提取码：o7ns 
复制这段内容后打开百度网盘手机App，操作更方便哦

## 赛题背景
新闻发展越来越快，每天各种各样的新闻令人目不暇接，对新闻进行科学的分类既能够方便不同的阅读群体根据需求快速选取自身感兴趣的新闻，也能够有效满足对海量的新闻素材提供科学的检索需求。

## 赛题描述
赛题以新闻数据为赛题数据，整合划分出如下候选分类类别：体育，财经，房产，家居，教育，科技，时尚，时政，游戏，娱乐共十类的新闻文本数据。选手根据新闻内容，进行分类。

## 预期效果
输入为新闻的内容，输出为新闻的分类。

输入新闻：<br>
![](https://img-blog.csdnimg.cn/20210528145424562.png)<br>
![](https://img-blog.csdnimg.cn/20210528145455338.png)

输出分类：游戏     科技

## 数据源
数据集选取自中文文本分类数据集THUCNews。THUCNews是根据新浪新闻RSS订阅频道2005~2011年间的历史数据筛选过滤生成，又在原始新浪新闻分类体系的基础上，重新整合划分出14个候选分类类别：财经、彩票、房产、股票、家居、教育、科技、社会、时尚、时政、体育、星座、游戏、娱乐。

本次训练选用了其中的10个分类。
类别如下：体育、财经、房产、家居、教育、科技、时尚、时政、游戏、娱乐。

数据集划分如下：

* 训练集: 50000；<br>
* 验证集: 5000；<br>
* 测试集: 10000。<br>

## 数据处理
* 读取已选用的数据文件，并根据此文件构建词汇表。<br>
* 给词汇表中的每一字符编号，并据此将数据文件的新闻内容用编号表示。<br>
* 将选用的十个新闻分类类别的标签用one-hot表示。<br>

## 卷积神经网络（CNN）
卷积神经网络（CNN）广泛应用于图像分析识别上，其核心是通过滤波器在图像目标上的平滑移动，通过卷积得到目标的特征图并作为下一层神经元的输入，最终建立起问题到目标的一个映射关系。

CNN的主要性质是：

* 局部连接；<br>
* 权值共享。<br>
![](https://img-blog.csdn.net/20170430161936244?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3htc2Ni/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## TextCNN
TextCNN的模型结构跟CNN差别不大，只是针对输入层做了变型，将词向量作为输入。<br>
![](https://img-blog.csdnimg.cn/2019070616562550.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzM3Nzg4MzA4,size_16,color_FFFFFF,t_70)

## CNN配置参数

![](https://img-blog.csdnimg.cn/20210528150027501.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ4MTg4ODMw,size_16,color_FFFFFF,t_70)

## 模型要点

* Dropout：在训练中忽略掉一半的特征值，以减少过拟合现象。<br>
* ReLU激活：选用非线性修正函数ReLU作为激活函数。
* SoftMax：根据全连接层的输出结果得到对应标签种类的概率分布，确定所属新闻类别。
* 交叉熵：损失函数选用交叉熵函数，便于衡量概率分布之间的差异情况。
* 优化器：优化器选用Adam算法，Adam等自适应学习率算法对于稀疏数据具有优势，且收敛速度很快。

## 训练结果

![](https://img-blog.csdnimg.cn/20210528150057292.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ4MTg4ODMw,size_16,color_FFFFFF,t_70)

由图可知，在验证集上最好的效果是95.58%，并且只经历了4轮迭代就停止了。

## 模型评定

准确率、召回率、F1值是主流的文本分类评价指标。<br>

图为模型在测试集上的分类实现效果。<br>

准确率（precision）：也叫作查准率。即真正正确的占所有预测为正的比例；<br>

召回率 （recall）：也叫作查全率。即真正正确的占所有实际为正的比例；<br>

F-Measure是Precision和Recall加权调和平均。<br>

![](https://img-blog.csdnimg.cn/20210528150104728.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ4MTg4ODMw,size_16,color_FFFFFF,t_70)

![](https://img-blog.csdnimg.cn/2021052815152594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ4MTg4ODMw,size_16,color_FFFFFF,t_70)

可以看出，准确率、召回率以及F1值基本都在0.9以上，说明模型还是可以的。
