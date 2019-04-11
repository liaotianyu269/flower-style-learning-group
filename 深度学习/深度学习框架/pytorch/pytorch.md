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

<details><summary>torch.autograd.Variable</summary>
  
- Variable数据结构：
  - 包含成员data，grad，grad_fn  
  - data:就是一个tensor  
  - grad:是一个variable,形状与data一致  
  - grad_fn:记录variable的来源操作，即variable是通过grad_fn记录的操作产生的，如果为None则说明是手动创建的  
            同时grad_fn也表示此variable的反向传播函数，如AddBackwardl,AcummulateGrad,None  
  - grad_fn.next_functions 前几个元素的grad_fn  
- Variable的创建  
  - Variable(tensor,requires_grad=True/False,volatile=True/False)  
  - requires_grad:bool值，指示需不需要求导此variable   
  - volatile:bool值，指示是否禁止求导此variable,优先级大于requires_grad  
    **注：新版本好像不用volatile了，用torch.no_grad**  
- Variable自动求导功能  
  - Variable.backward(grad_varialbes,retain_graph):根据计算图求出直至源头的梯度，**注：计算图是理解自动求导的重要概念**  
  - grad_variables即目标函数对此variable的梯度  
  - retain_graph：bool值，指示是否清空中间变量的梯度缓存  
    所以求导类似于
    ```python
    z.backward()
    y.backward(torch.autograd.grad(z.y))//两种方法是同一个意思，从z开始求导，和从y开始求导  
    ```
    backward计算完梯度后，用于临时存储中间变量的grad的变量即被释放，所以用variable.grad查不到中间变量的grad  
    可用`torch.autograd.grad(x,y)`手动计算，即x对y的grad  
    或用torch.autograd.Variable.register_hook(func(grad))函数返回一个句柄，func(grad)是关于此variable的gra的函数  
    每次在backward时，调用register_hook  
    ```python
    def variable_hook(grad):
      print('y的梯度： \r\n',grad)
    x = V(t.ones(3), requires_grad=True)
    w = V(t.rand(3), requires_grad=True)
    y = x * w
    hook_handle = y.register_hook(variable_hook)
    z = y.sum()
    z.backward()
    hook_handle.remove()
    ```
 - 若遇到不能通过autograd自动求导的情况，可通过手动写function来进行前向传播和后向传播  
   **待了解** 
</details>

<details><summary>torch.utils.data</summary>
  
- torch.utils.data.Dataset  
- torch.utils.data.DataLoarder  

</details>
