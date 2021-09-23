# AUC和ROC

## 1.AUC和ROC属于分类模型的评估指标

分类模型评估：

| 指标             | 描述            | Scikit-learn函数                             |
| ---------------- | --------------- | -------------------------------------------- |
| Precision        | 精准度          | from sklearn.metrics import precision_score  |
| Recall           | 召回率          | from sklearn.metrics import recall_score     |
| F1               | F1值            | from sklearn.metrics import f1_score         |
| Confusion Matrix | 混淆矩阵        | from sklearn.metrics import confusion_matrix |
| ROC              | ROC曲线         | from sklearn.metrics import roc              |
| AUC              | ROC曲线下的面积 | from sklearn.metrics import auc              |
| Kappa            | kappa系数       |                                              |

回归模型评估：

| 指标                          | 描述     | Scikit-learn函数                               |
| ----------------------------- | -------- | ---------------------------------------------- |
| Mean Square Error (MSE, RMSE) | 平均方差 | from sklearn.metrics import mean_squared_error |
| Recall                        | 绝对误差 | from sklearn.metrics import recall_score       |
| R-Squared                     | R平方值  | from sklearn.metrics import r2_score           |

## 2.定义

ROC全称是“受试者工作特征”（Receiver Operating Characteristic）。ROC用来评估分类器的效果。

ROC曲线的面积就是AUC（Area Under the Curve）。AUC用于衡量“二分类问题”机器学习算法性能（泛化能力）。

### 计算ROC需要知道的关键概念

首先，解释几个二分类问题中常用的概念：True Positive, False Positive, True Negative, False Negative。它们是根据真实类别与预测类别的组合来区分的。

假设有一批test样本，这些样本只有两种类别：正例和反例。机器学习算法预测类别如下图（左半部分预测类别为正例，右半部分预测类别为反例），而样本中真实的正例类别在上半部分，下半部分为真实的反例。

- 预测值为正例，记为P（Positive）
- 预测值为反例，记为N（Negative）
- 预测值与真实值相同，记为T（True）
- 预测值与真实值相反，记为F（False）

![这里写图片描述](https://img-blog.csdn.net/20170422190557868?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWJkZXNpcmU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

- TP：预测类别是P（正例），真实类别也是P
- FP：预测类别是P，真实类别是N（反例）
- TN：预测类别是N，真实类别也是N9
- FN：预测类别是N，真实类别是P

样本中的真实正例类别总数即TP+FN。**TPR**即True Positive Rate，TPR = TP/(TP+FN)。(召回率) 
同理，样本中的真实反例类别总数为FP+TN。**FPR**即False Positive Rate，FPR=FP/(TN+FP)。

还有一个概念叫”**截断点**”。机器学习算法对test样本进行预测后，可以输出各test样本对某个类别的相似度概率。比如t1是P类别的概率为0.3，一般我们认为概率低于0.5，t1就属于类别N。这里的0.5，就是”截断点”。 
**总结一下，对于计算ROC，最重要的三个概念就是TPR, FPR, 截断点**。

截断点取不同的值，TPR和FPR的计算结果也不同。将截断点不同取值下对应的TPR和FPR结果画于二维坐标系中得到的曲线，就是ROC曲线。横轴用FPR表示。

右上角的阈值最小，对应坐标点(1,1)；左下角阈值最大，对应坐标点为(0,0)。从左下角到右上角，随着阈值的逐渐变小，越来越多的实例被划分为正类，但是这些正类中同样也掺杂着真正的负实例，即TPR和FPR会同时增大。

最理想的分类器，就是对样本分类完全正确，即FP=0，FN=0。所以理想分类器TPR=1，FPR=0。

![img](https://pic2.zhimg.com/80/v2-66cc29b9e9f951de48c214d9ec34f4c5_720w.jpg)![img](https://pic2.zhimg.com/80/v2-10307b3a9d65af3f78aba218747599cd_720w.jpg)

理想目标：TPR=1，FPR=0，即图中(0,1)点，此时ROC曲线越靠拢(0,1)点，越偏离**45度对角线**越好。



AUC，（Area Under Curve），被定义为ROC曲线下的面积，显然这个面积小于1，又因为ROC曲线一般都处于y=x这条直线的上方，所以AUC一般在0.5到1之间。**使用AUC值作为评价标准是因为很多时候ROC曲线并不能清晰的说明哪个分类器的效果更好，而作为一个数值，对应AUC更大的分类器效果更好**

从AUC判断分类器（预测模型）优劣的标准：

- AUC = 1，是完美分类器，采用这个预测模型时，存在至少一个阈值能得出完美预测。绝大多数预测的场合，不存在完美分类器。
- 0.5 < AUC < 1，优于随机猜测。这个分类器（模型）妥善设定阈值的话，能有预测价值。
- AUC = 0.5，跟随机猜测一样（例：丢铜板），模型没有预测价值。
- AUC < 0.5，比随机猜测还差；但只要总是反预测而行，就优于随机猜测。

![img](https://pic3.zhimg.com/80/v2-0ec2fe6fb4bf120c59aa7b05037d9266_720w.jpg)

## 3.为什么使用ROC曲线？

既然已经这么多评价标准，为什么还要使用ROC和AUC呢？因为ROC曲线有个很好的特性：当测试集中的正负样本的分布变化的时候，ROC曲线能够保持不变。在实际的数据集中经常会出现类不平衡(class imbalance)现象，即负样本比正样本多很多(或者相反)，而且测试数据中的正负样本的分布也可能随着时间变化。下图是ROC曲线和[Precision-Recall](https://link.zhihu.com/?target=https%3A//en.wikipedia.org/wiki/Precision_and_recall)曲线的对比：

![img](https://pic2.zhimg.com/80/v2-a8ce55589ca9982426525493fec664b1_720w.jpg)

在上图中，(a)和(c)为ROC曲线，(b)和(d)为Precision-Recall曲线。(a)和(b)展示的是分类其在原始测试集(正负样本分布平衡)的结果，(c)和(d)是将测试集中负样本的数量增加到原来的10倍后，分类器的结果。可以明显的看出，ROC曲线基本保持原貌，而Precision-Recall曲线则变化较大。