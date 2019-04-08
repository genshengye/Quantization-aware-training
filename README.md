# Quantization-aware-training
Tensorflow Quantization-aware training

[官方介绍](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/contrib/quantize?spm=a2c4e.11153940.blogcont680747.5.6c18652aeauOJ0)

#### 一、需要创建两个graph：

##### 1、一个只用来training，在这个graph上使用create_training_graph(). 

##### 2、另一个graph，只用来inference，在这个graph上使用create_eval_graph(). 

##### 3、最后，Freeze这个用来inference的graph，再把它传给toco。

#### 二、[谷歌现成的例子](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/speech_commands)

##### 1、train.py，第157行（create_training_graph）

##### 2、freeze.py，第133行(create_eval_graph)

#### 三、注意事项

##### 1、create_training_graph，要出现在cross_entropy之后，tf.train.GradientDescentOptimizer之前。

##### 2、create_eval_graph则是出现在创建完inference graph之后，load checkpoint之前。

##### 3、load checkpoint之后是freeze graph，freeze graph 用的是graph_util.convert_variables_to_constants（）