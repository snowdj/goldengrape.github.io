<!--
.. title: 机器学习的战略(0)--基础概念
.. slug: ji-qi-xue-xi-de-zhan-lue-0-ji-chu-gai-nian
.. date: 2017-12-19 01:22:18 UTC+08:00
.. tags: ML, 教程, 现代眼科医生知识扩展包
.. category: tutorial
.. link:
.. description:
.. type: text
-->

这是deeplearning.ai系列课程的第三门课[Structuring Machine Learning Projects](https://www.coursera.org/learn/machine-learning-projects/).  我觉得这门课非常适合甲方\导师\研发团队头目\产品经理.

这是一门即时战略类课程, 讲述如何评估模型如何挑选改进方向, 所需基础知识不多, 对机器学习知道基本概念即可.
<!-- TEASER_END -->

但是这门课里面涉及到的概念和经验很多, 未来我可能需要借助一个笔记时常参考. 这个笔记也可以帮助其他未选这门课的人了解其中的梗概.

# 一些基础的概念
虽然我认为这门课所需要的基础知识并不多, 但也还是需要知道一些机器学习的基本概念, 需要量还是要比"朋友圈公众号科普"多一些.

## 机器学习 Machine Learning
这里讲的是有监督学习的任务, 比如给一张照片, 判定这张照片是不是一只猫. 所谓有监督的学习, 就是已知有很多照片, 已经被人工标记过是猫还是非猫了, 这些叫做数据集**dataset**, 数据集中通常是一个对应的结构, 一个输入x, 对应一个输出y.  x ->y, 比如一张照片就是x, 是猫的照片y=1, 不是猫的照片 y=0

Machine Learning就是利用大量的dataset, 自动从里面去总结出一种从x映射到y的规律.

最简单的, 比如线性拟合就可以视为一种简单的ML, 有一堆数据点(x,y), 用一条直线去拟合它们. 求解y=kx+b, 有了y=kx+b的公式以后, 你就可以代入一些新的x, 求出y值.

y=kx+b这个训练出来的公式通常叫做"模型", 当然你的数据也可能不是符合y=kx+b的, 而是符合y=ax^2+bx+c, 甚至于更加复杂的函数关系以至于很难写出表达式. 去找到k, b这样的参数的过程叫做"训练"模型.

除了拟合, 更常见的Machine Learning问题是分类, 其实也类似, 比如相当于看是否 y=kx+b>0

在deeplearning.ai课程中的[第一门课](https://www.coursera.org/learn/neural-networks-deep-learning/home)就是讲基本的ML方法----神经网络.

## dataset
有标记的数据集x->y, 就是dataset. 现代的机器学习已经开始使用非常庞大的数据集了, 比如1,000,000张标记好的照片甚至更多. 

在训练模型时, 需要把dataset分成几个部分, 一般而言是分成3个, train set / develop set / test set.

### train set
train set是用来训练当前这个模型用的, 比如假定模型是y=kx+b, 求解k和b这两个参数的过程就是用train set.

不严格的说, 相当于上课时老师用的例题.

### develop set
develop set, 在课程中常写作dev set 是说你可能有多个候选的模型, 或者说要"develop"模型的时候, 用来测试各个模型的. 比如你的候选模型除了y=kx+b, 可能还有y=ax^2+bx+c, 可能还有y=ax^3+bx^2+cx+d... 这时候就要分别用同一个train set去训练各个模型, 求得各自最佳的参数, 然后再用dev set中的数据代入, 看看各个模型的误差是怎样的.

不严格的说, 相当于家庭作业.  

### test set
test set, 顾名思义, 就是用来测验考试的. 考试题里不能是老师上课用过的例题, 也不能是做过的作业, 需要是考生(模型)从来没见过的题目.

## bias 和 variance
我觉得这两个词语的中文翻译并不准确, 所以干脆不翻译了.

* bias过高, 是指拟合的函数不够准确, 比如本来数据是符合y=a^x+bx+c这样一条二次曲线的, 结果只用了y=kx+b一条直线去拟合, 直的适应不了弯的, 于是可能在一小段还比较符合, 在其他区域预测的准确率就很差. 通常认为bias过高, 是拟合不足, 欠拟合的. under fitting. [插图]

* variance过高, 是指拟合过度了, over fitting. 一条弯弯曲曲的曲线穿过所有的数据点, 这样虽然误差很小, 但是预测能力就很差, 而我们进行机器学习当然目的是为了评估哪些未知的数据. 真正需要的是预测能力.[插图]

如果模型过于简单, bias就容易很高, 如果模型过于复杂, variance就容易很高.

在deeplearning.ai系列课程的[第二门](https://www.coursera.org/learn/deep-neural-network/home/welcome)就是在讲各种奇技淫巧去调整模型来降低bias和variance, 相当于改善模型表现的战术方法.

我个人觉得理解上面这些概念就可以开始ML strategy这门课程的学习了. 但是我已经学过了第一门和第二门课, 有可能存在"因为我知道所以我不知道你是否需要知道"这样的知识诅咒. 所以万一在学MLstrategy这门课程时觉得吃力, 还是去补习一下基础比较好. 暂时没必要去学更复杂的卷积神经网络什么的.

----
# 参考资料:
* 机器学习的战略合集目录:

0. [基础概念](http://www.jianshu.com/p/605bb2d6da5e)
1. [目标设置](http://www.jianshu.com/p/e5f2d53493ff)
2. [错误率](http://www.jianshu.com/p/9ec8e8c7b58c)
3. [误差分析](http://www.jianshu.com/p/b841fc1f7c40)
4. [面对分布不同](http://www.jianshu.com/p/4e1ad322deb5)
5. [迁移学习](http://www.jianshu.com/p/e2993f594767)
6. [end-to-end](http://www.jianshu.com/p/92bf4af48804)

* 课程链接:
[Structuring Machine Learning Projects](https://www.coursera.org/learn/machine-learning-projects/home/welcome)

* 参考视频:
莫烦的"[有趣的机器学习](https://morvanzhou.github.io/tutorials/machine-learning/ML-intro/)"系列科普视频, 制作精良讲解清晰, 非常推荐.  
