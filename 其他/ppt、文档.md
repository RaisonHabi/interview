## How：

1.  呈现事实，提炼观点：突出重点，清晰讲述

2.  扬长避短：不提未做的

3.  按照目标职级要求，来证明

4.  突出理解、思考业务问题的过程

5.  突出重点工作过程

6.  呈现主要业绩贡献

7.  Ppt配色、图形的选择，重要内容深色

8.  表述流畅、清晰，最好能吸引人

9.  白话讲演，把不了解的人说懂

&nbsp;
## 
```
TensorFlow - Google发布的开源深度学习框架
OP - Operation缩写，TensorFlow算子
PS - Parameter Server 参数服务器
WDL -Wide & Deep Learning，Google发布的用于推荐场景的深度学习算法模型
AFO - AI Framework on YARN的简称 - 基于YARN开发的深度学习调度框架，支持TensorFlow，MXNet等深度学习框架
```


零售金融风控
利润=成本（万五，年化18%）-资金（7-8%）-风险-运营（1-2%）

&nbsp;
## 
Q1:无人行(优：节约查人行成本、增加用户借款意向)（去掉人行数据，放宽了门槛，更多的人通过：3倍；第二阶段再加上人行，通过率为40%）为什么同一个评分体系，先去人行再加人行结果不相等（3*40%>1?），不应该是等于1吗？换句话说，无人行的初衷是不是：不用人行数据的评分结果尽量接近用人行数据的结果，即第一阶段应该尽量接近1倍？

Q2：embedding是哪种embedding（word2vec/glove/elmo/bert）;用embedding（降维度、求语意相似度）的目的是什么，有对比过不用embedding吗？
在维度较小且不关注语意相似度时，为什么不用one-hot？





https://blog.csdn.net/zhaojc1995/article/details/80572098

RNN（Recurrent Neural Network）是一类用于处理序列数据的神经网络。首先我们要明确什么是序列数据，摘取百度百科词条：时间序列数据是指在不同时间点上收集到的数据，这类数据反映了某一事物、现象等随时间的变化状态或程度。这是时间序列数据的定义，当然这里也可以不是时间，比如文字序列，

但总归序列数据有一个特点——后面的数据跟前面的数据有关系。







https://blog.csdn.net/jack_jmsking/article/details/82465019

Tensorflow 之 embedding：word2vec







https://www.cnblogs.com/hellojamest/p/11623085.html

Graph Embedding
早期影响力较大的graph embedding方法是2014年提出的DeepWalk，它的主要思想是在由物品组成的图结构上进行随机游走，产生大量物品序列，然后将这些物品序列作为训练样本输入word2vec进行训练，最大化随机游走序列的似然概率，并使用最终随机梯度下降学习参数,得到物品的embedding。其目标函数为：
实际上，也是word2vec的目标函数。







