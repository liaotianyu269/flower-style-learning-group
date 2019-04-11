<details><summary>torch.Tensor</summary>
  
- 创建
  - torch.Tensor(rows,cols)  
  - torch.ones/torch.zeros/torch.eye(rows,cols)  
  - torch.arange(s,e,step)/torch.linspace(s,e,num)  
  - torch.rand/torch.randn(rows,cols) //0-1均匀分布，-1--1标准分布  
  - torch.normal(means,std,out)  //有问题,创建不了  
  - torch.randperm(n)//随机排列  
  - torch.is_tensor  
  - torch.set_default_tensor_type  
  - torch.numel  
  - tensor.size()/tensor.shape //尺寸  
  - tensor.dtype/tensor.type()//数据类型  
  - tensor.numel()//元素个数  
- 数据类型  
  - 8位 torch.CharTensor/torch.ByteTensor  
  - 16位 torch.ShortTensor  
  - 32位 torch.IntTensor/torch.FloatTensor  
  - 64位 torch.LongTensor/torch.DoubleTensor  
  - 类型转换 tensor.type()/tensor.type_as(tensor)  
- 常用操作  
  **从存储角度看，对tensor的操作分为两类：函数名以_结尾的是inplace方式, 即会修改调用者自己的数据。**  
  - tensor.view()//修改尺寸，保持元素不变，浅复制  
  - tensor.unsqueeze(n)//扩展维度，在n-1后插入新维度  
  - tensor.squeeze(n)//压缩第N维，N维维度必须是1  
  - tensor.squeeze()//压缩所有维度为1的维  
  - tensor.resize()//修改尺寸，尺寸比原来大，会分配新空间，比原来小，旧数据仍保存  
  - 索引操作  
    - 坐标 tensor[,],tensor[[],[],[]]    
    - 切片 tensor[:,:]  
    - 大切片 tensor[:,...]  
    - mask tensor[真值表]  
  - torch.cat(tensor,dimension=0,1)//拼接  
  - torch.gather(tensor,dim,index,out)//将tensor按dim维通过index索引的值聚合后，输出   
  - tensor.scatter_(dim,index,inputtensor)//按dim维通过index索引将inputtensor的值放入tensor  
  - tensor.gather(dim,index)//gather和scatter_是一对逆操作  
  - torch.index_select(input,dim,index)//按index和dim选取行或列  
  - torch.masked_select(input,mask)//根据mask选取  
  - torch.nonzero(input)//返回非零元素坐标  
  - torch.split(input,size,dim)//按dim分割，每块大小为size，不能整除，则最后一块小于size  
  - torch.stack(tensors,dim)//按dim堆叠tensors  
  - torch.t()/torch.transpose()//转置，浅复制  
  - torch.chunk(tensor,chunks,dim)//类似split,按dim分割，分成chunks块  
  - torch.unbind(tensor,dim)//按dim，每行或列为一个tensor，组成一个元组，并返回  
- 数学运算  
  - torch.sum
  - torch.mean
  - torch.std
  - torch.clamp
  - torch.max
  - torch.min
  - torch.ceil,torch.floor,torch.round  
  - torch.pow  
  - torch.sqrt  
  - torch.prod
  - torch.eq,torch.ne,torch.gt,torch.ge,torch.lt,torch.le    
  - torch.equal  
  - +-/\*，均是element-wise，按元素运算方式  
  - 内积,tensor.dot(tensor)/torch.dot(tensor,tensor)//tensor必须是一维  
  - 矩阵乘法,tensor.mm(tensor)/torch.mm(tensor,tensor)//按线性代数矩阵乘法运算规则   
- tensor和numpy的转换  
  - torch.from_numpy(ndarray)  
  - torch.Tensor(ndarry)  
  - tensor.numpy()  
</details>

<details><summary>torch.save,torch.load,torch.nn.Module.load_state_dict</summary>
  

</details>

<details><summary>向量化</summary>
  

</details>

<details><summary>torch.utils.data</summary>
  
- torch.utils.data.Dataset
- torch.utils.data.DataLoarder

</details>
