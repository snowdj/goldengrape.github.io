<!--
.. title: ResNet编写注意事项
.. slug: ResNet-note
.. date: 2017-12-28 15:00:22 UTC+08:00
.. tags:
.. category:
.. link:
.. description:
.. type: text
-->

Deeplearning.ai 第4门课程<[卷积神经网络](https://www.coursera.org/learn/convolutional-neural-networks/home/welcome)>,  终于开始讲解"现代"的深度神经网络了. 第二周也迅速开始使用Keras进行神经网络的编写.

虽然Keras已经抽象程度很高了, 只需要设定基本的参数, 就可以建立网络层, 不至于在实现细节中迷失,  但是仍然会有些小坑容易踩.

下面是一些经验:
<!-- TEASER_END -->

# 务必小心各种默认值.

第一次用函数之前, 一定要先看文档说明, 如果自己的要求明确, 比如是否使用激活函数, pedding的方法等等,  就在函数调用时把这些要求都写出来, 哪怕已经有默认值规定.

比如:
* tensorflow中, 设定好卷积层之后最后几层往往还是全连阶层, 设定全连阶层的函数[tf.contrib.layers.fully_connected](https://www.tensorflow.org/api_docs/python/tf/contrib/layers/fully_connected)有个默认激活函数是ReLU, 如果你根本不想要激活函数, 或者后续还要设定其他的激活函数, 那么最好把activation_fn=None
* keras中CONV2D默认padding是valid, 我简直可以预见到自己日后一定会踩此坑. 而且不止一次.

# 维度一致
主路径和捷径的结果要相加, 必须维度一致. 如果主路径的filters分别是F1, F2, F3, 捷径的filter就应当是F3. 应当与最后一个filter#相同.

如果主路径中有padding=valid, 捷径中也需要相应缩小.
复习一下维度的变化, 一个(N, N)的图像, 经过二维卷积, 如果卷积的大小是(f,f), padding是(p,p), strip是(s, s), 那么卷积以后的尺寸变成了
floor( (N+2p-f)/s+1 )

# 作用函数一致
首先ResNet中两个卷积层的输出结果不能简单的使用+, 而应当使用Add( )函数.
Keras函数的返回值仍然是函数, 因此Add函数, 不能写成Add([X,X_shortcut]), 而要写成Add( )([X,X_s]).

在分路径时, 不同路径上在把函数作用到变量时, 要注意统一
* 主路径中一直是X=CONV2d(...)(X),
* 捷径中一直是X_shortcut=CONV2d(...)(X_shortcut), 不要在随手复制粘贴时搞成了X_shortcut=CONV2d(...)(X)

这种bug有时候停难找的, 特别是后端用tensorflow的时候, 感觉用tensforflow比较难debug, 因为是先建立静态的计算图, 最后才喂给数据, 以前编程时插入断点跟踪数据等debug的经验就很难用上.  [@ailurus1991](https://twitter.com/ailurus1991) 提到了tensorflow专用的debug工具https://www.tensorflow.org/programmers_guide/debugger 还不知道是否好用.
