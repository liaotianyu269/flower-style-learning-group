
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
