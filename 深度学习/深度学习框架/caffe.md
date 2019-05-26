
Caffe的各层定义
Caffe层的定义由2部分组成：层属性与层参数，例如
{
name:"conv1"
type:CONVOLUTION
bottom:"data"
top:"conv1"
convolution_param{
    num_output:<span>20
    kernel_size:5
    stride:1
    weight_filler{
        type: "<span style="color: #c0504d;">xavier</span>"
    }
}
这段配置文件的前4行是层属性，定义了层名称、层类型以及层连接结构（输入blob和输出blob）；而后半部分是各种层参数。 

Blob
Blob是用以存储数据的4维数组，例如 

对于数据：Number*Channel*Height*Width
对于卷积权重：Output*Input*Height*Width
对于卷积偏置：Output*1*1*1

Caffe生成的数据分为2种格式：Lmdb和Leveldb
 
它们都是键/值对（Key/Value Pair）嵌入式数据库管理系统编程库。
虽然lmdb的内存消耗是leveldb的1.1倍，但是lmdb的速度比leveldb快10%至15%，更重要的是lmdb允许多种训练模型同时读取同一组数据集。
因此lmdb取代了leveldb成为Caffe默认的数据集生成格式。

Google Protocol Buffer的安装
Protocol Buffer是一种类似于XML的用于序列化数据的自动机制。

<details><summary>层类型及参数：</summary>
  
- type:"Data"  
```python
layer {  
  name: "cifar"  				//层名
  type: "Data"  				//类型
  top: "data"  					//输出之一
  top: "label"  				//输出之二
  include {  
    phase: TRAIN  				//训练时用
  }
  transform_param {
    mean_file: "examples/cifar10/mean.binaryproto"			//待了解
  }
  data_param {
    source: "examples/cifar10/cifar10_train_lmdb"			//数据源 LevelDB，LMDB格式数据
    batch_size: 100											//批量大小  
    backend: LMDB											//后端采用数据库
  }
}
```
- type: "Convolution"
```python
layer {
  name: "conv1"							//
  type: "Convolution"					//
  bottom: "data"						//
  top: "conv1"							//
  param {
    lr_mult: 1						//
    decay_mult: 1					//
  }
  param {
    lr_mult: 2						//如有两个lr_mult，则第一个表示权值w的学习率，第二个表示偏置项的学习率。												//一般偏置项的学习率是权值学习率的两倍
    decay_mult: 0					//
  }
  convolution_param {
    num_output: 96					//
    kernel_size: 11					//
    stride: 4						//
    pad: 2							//
    weight_filler {
      type: "gaussian"				//
      std: 0.01            			//标准差：distribution with stdev 0.01(default mean: 0)
    }
    bias_filler {
      type: "constant"				//
      value: 0						//
    }
  }
}
```
- type:"Pooling"
```python
layer {
  name: "pool1"
  type: "Pooling"
  bottom: "conv1"
  top: "pool1"
  pooling_param {
    pool: MAX				//
    kernel_size: 3			//
    stride: 2				//
  }
}        
```
- type:"img2col"
```python
```
- type:"InnerProduct"
```python
layers {
  name: "fc8"
  type: "InnerProduct"
  blobs_lr: 1          			# learning rate multiplier for the filters
  blobs_lr: 2          			# learning rate multiplier for the biases
  weight_decay: 1      			# weight decay multiplier for the filters
  weight_decay: 0      			# weight decay multiplier for the biases
  inner_product_param {
    num_output: 1000
    weight_filler {
      type: "gaussian"
      std: 0.01
    }
    bias_filler {
      type: "constant"
      value: 0
    }
  }
  bottom: "fc7"
  top: "fc8"
```
- type:"Accuracy"  
```python
layer {
  name: "accuracy"
  type: "Accuracy"
  bottom: "ip2"
  bottom: "label"
  top: "accuracy"
  include {
    phase: TEST				//accuracy只在test有，因此要设置include为TEST。输出分类（预测）的精确度。
  }
}
```
- type:"Reshape"  
```python
layer {
    name: "reshape"
    type: "Reshape"
    bottom: "input"
    top: "output"
    reshape_param {
      shape {
        dim: 0  			# copy the dimension from below
        dim: 2
        dim: 3
        dim: -1 			# infer it from the other dimensions
      }
    }
  }
```
- type:"Dropout"
```python
layer {
  name: "drop7"
  type: "Dropout"
  bottom: "fc7-conv"
  top: "fc7-conv"
  dropout_param {
    dropout_ratio: 0.5   #只需要设置一个dropout_ratio参数即可
  }
}
```
- type:"RELU"
```python
layers {
name: "relu1"
type: RELU
bottom: "conv1"
top: "conv1"
}
```
- type:"AbsVal"
```python
layer {
  name: "layer"
  bottom: "in"
  top: "out"
  type: "AbsVal"
}
```
- type:"Power"
```python
layer {
  name: "layer"
  bottom: "in"
  top: "out"
  type: "Power"
  power_param {
    power: 2
    scale: 1
    shift: 0
  }
}
```
- type:"SoftmaxWithLoss"
```python
layer {
  name: "loss"
  type: "SoftmaxWithLoss"
  bottom: "ip1"
  bottom: "label"
  top: "loss"
}
```
</details>

