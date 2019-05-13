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
  - 16位 torch.ShortTensor/torch.cuda.HalfTensor  
  - 32位 torch.IntTensor/torch.FloatTensor  
  - 64位 torch.LongTensor/torch.DoubleTensor  
  - 类型转换 tensor.type()/tensor.type_as(tensor)  
- 常用操作  
  **从存储角度看，对tensor的操作分为两类：函数名以_结尾的是inplace方式, 即会修改调用者自己的数据。**  
  - tensor.view()//修改尺寸，保持元素不变，浅复制  
  - tensor.unsqueeze(n)//扩展维度，在n-1后插入新维度  
  - tensor.expand(dim1,dim2,dim3)//扩展维度为dim1,dim2,dim3  
  - tensor.expand_as(tensor)//扩展维度与后一tensor一致  
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

<details><summary>torch.nn</summary>
  
- torch.nn.Module类的属性  
  **torch.nn.Module是torch.nn的核心数据结构，表示一个网络，可以是单层或多层，可以包含子网络。**    
  - self.\_parameters=OrderedDict()   //此网络中的Parameters，子网络的Parameters不在这里  
  - self.\_modules=OrderedDict()    //存储包含的子网络,子网络的子网络不在这里    
  - self.training=True      //模型是否训练模式的标志，默认为True  
  - self.\_buffers=OrderedDict()    //以下三个属性是在网络前向传播和后向传播中会利用到的    
                                      获取中间网络层的参数的函数类似之前提到的Variable hook技术  
                                      Variable.register_hook(fun(grad))  
                                      Module.register_backward_hook(fun(model,inut,output))  
  - self.\_forward_hooks=OrderedDict()  
  - self.\_backward_hooks=OrderedDict()  
  - torch.nn.Module.\_\_dict\_\_.get('属性')//返回属性，但是在self.\_parameters和self.\_modules中已有的属性  
                                              不会出现在torch.nn.Module.\_\_dict\_\_中  
                                              三者加起来是所有的parameters,和modules  
                                              modules.parameters() or modules.modules()  
- 创建网络
  ```python
  自定义简单网络模型示例,全连接层FClayer  
  class myFCNet(nn.Module):
    def __init__(self,in_features,out_features):
        super(myFCNet,self).__init__()    //也可以nn.Module.__init__(self)
        self.w=nn.Parameter(torch.randn(in_features,out_features))  
        self.b=nn.Parameter(torch.randn(out_features))

    def forward(self,x):
        x=x.mm(self.w)
        x=x+self.b.expand_as(x)
        return x
   ```
  - torch.nn.Module.parameters(),torch.nn.Module.named_parameters()//返回所有网络参数，返回所有网络参数名称和参数  
  - torch.nn.modules(),torch.nn.named_modules()//返回子网络  
  - torch.nn.Parameter(Variable)  //Parameter,Variable,tensor都是矩阵  
    tensor是纯数字只运用于计算，不能用于自动求导  
    variable是对tensor的封装，记录有梯度相关信息，可用于自动求导  
    Parameter是对Variable的子类，默认requires_grad是True(因Parameter是学习的参数肯定要求导)  
    另Parameter在用于Module中时，Module可以根据Parameter的属性进行自动识别等.Variable不行因为缺少这些属性  
  ```python
  自定义含有子网络的网络模型示例,多层感知机MLP  
  def myMLP(nn.Module):
      def __init__.(self,in_features,hidden_features,out_features):
          super(myMLP,self).__init__()
          self.layer1=myFCNet(in_features,hidden_features)
          self.layer2=myFCNet(hidden_layers,out_features)

      def forward(self,x):
          x=self.layer1(x)
          x=self.layer2(x)
          return x
  ```
  - torch.nn.Sequential
    是一类特殊的Module,不用再写forward函数，规定了网络结构后，默认一层一层往下传递  
    ```python
    Sequentila示例  
    net=torch.nn.Sequential(
        torch.nn.Conv2d(3,3,3),
        torch.nn.BatchNorm2d(3),
        torch.nn.Relu()
        )
    net.add_module('fc1',torch.nn.Linear(3,3))
    input=torch.randn(3,3)
    net(input)//自动一层一层传递  
    ```
  - torch.nn.ModuleList  
    也是一个Module，包含了一层或多层子网络的Module,但是不能依次进行传播  
    ```python
    ModuleList示例
    net=torch.nn.ModuleList([torch.nn.Linear(3,3),torch.nn.Linear(3,2),torch.nn.Dropout(0.5)])  
    input=torch.randn(3,3)
    net(input)//这样是错误的，因为不能一层一层传递会报错  
    for model in net:
        input=model(input)//正确  
    ```
- 常用的神经网络层，标准接口  
  - torch.nn.Conv2d  
  - torch.nn.Linear  
  - torch.nn.Dropout
  - torch.nn.MaxPool2d
- 激活函数  
  **激活函数也是基于Module实现，保存在torch.nn中**
  - torch.nn.Relu  
- loss损失函数torch.nn  
  **也是一类特殊的Module，保存在torch.nn中**  
  - 常用的loss损失函数  
    - torch.nn.CrossEntropyLoss()  
    - torch.nn.MSELoss()  
- optimizer优化器  
  **保存在torch.nn.optim中**  
  - 常用的优化器  
    - torch.optim.SGD()  
- torch.nn.functional纯函数    
  某些torch.nn.Module的功能在torch.nn.functional中也有相应接口，比如不需要参数学习的Module就可以使用functional  
  - torch.nn.functional.relu()  
  - torch.nn.functional.max_pool2d()  
- torch.nn.init初始化策略  
  - torch.nn.init.xavier_normal(Parameter)  
- torch.save,torch.load模型保存和加载  
  - torch.save(module.state_dict(),'xx.pth')//只保存参数  
  - torch.load('xx.pth')//加载参数  
  - module.load_state_dict(torch.load('xx.pth'),strict=True)//将加载的参数添加到模型中,strict默认为True  
                                    strict=False时，非严格加载参数，属性对应则加载，不对应不加载，保持原样  
- cpu与gpu加载时相互转换  
  torch.load(path,map_location=lambda storage,loc:storage)  
  torch.load(path,map_location=lambda storage,loc:storage.cuda(0))  
  torch.load(path,map_location={'cuda:0':'cuda:1'}  
</details>

<details><summary>torch.utils</summary>
  
- **数据抽象**torch.utils.data.Dataset  
  **将数据源整理成像列表一样的数据结构,元素内容可以(文件路径，label，特征点，图片数据...)**  
  主要是定义\_\_init\_\_,\_\_getitem\_\_,\_\_len\_\_三个函数  
  ```python
  简单数据加载定义示例  
  class myData(torch.utils.data.Dataset):
      def __init__(self,root,transforms=None):    //root目录下包含图片，图片命名分别包含'cat'，'dog'  
          self.imgpath=[os.path.join(root,path) for path in os.listdir(root)]  
          
      def __getitem__(self,index):
          img=self.imagepath[index]
          if 'cat' in img.split('/')[-1]:
              label=0
          else:
              label=1
          if transforms:
              img=PIL.Image.open(img)
              img=transform(img)
          return img,label
          
      def __len__(self):
         return len(self.imgpath)
  dataset=myData('./liaodi')
  dataset[0]                  //可以想使用list一样使用dataset，很方便  
  for path,label in dataset:
      print(path,label)
  ```
  **注:**
  - 高负载的操作放在__getitem__中，如加载图片等。
  - dataset中应尽量只包含只读对象，避免修改任何可变对象，利用多线程进行操作。
  ```
  第一点是因为多进程会并行的调用__getitem__函数，将负载高的放在__getitem__函数中能够实现并行加速。
  第二点是因为dataloader使用多进程加载，如果在 Dataset实现中使用了可变对象，可能会有意想不到的冲突。
  在多线程/多进程中，修改一个可变对象，需要加锁，但是dataloader的设计使得其很难加锁(在实际使用中也应尽量避免锁的存在)
  因此最好避免在dataset中修改可变对象。
  例如下面就是一个不好的例子，在多进程处理中self.num可能与预期不符，这种问题不会报错，因此难以发现。
  如果一定要修改可变对象，建议使用Python标准库Queue中的相关数据结构。

  class BadDataset(Dataset):
      def __init__(self):
          self.datas = range(100)
          self.num = 0 # 取数据的次数
      def __getitem__(self, index):
          self.num += 1
          return self.datas[index]
  ```
- **数据抽取**torch.utils.data.DataLoader  
  - DataLoader(dataset, batch_size=1, shuffle=False, sampler=None, num_workers=0, collate_fn=default_collate,   
    pin_memory=False,drop_last=False)  
    - dataset：加载的数据集(Dataset对象)  
    - batch_size：batch size  
    - shuffle:：是否将数据打乱  
    - sampler： 样本抽样，后续会详细介绍  
    - num_workers：使用多进程加载的进程数，0代表不使用多进程  
    - collate_fn： 如何将多个样本数据拼接成一个batch，一般使用默认的拼接方式即可  
    - pin_memory：是否将数据保存在pin memory区，pin memory中的数据转到GPU会快一些  
    - drop_last：dataset中的数据个数可能不是batch_size的整数倍，drop_last为True会将多出来不足一个batch的数据丢弃  
- torch.utils.data.sampler  
  在DataLoader中shuffle是sampler的一种，默认的sampler是SequentialSampler顺序采样即一个接一个采样  
  常用的还有：WeightedRandomSampler(weights,num_samplers,replacement=True)  
  当DataLoader中指定了sampler后，shuffle参数失效  
  - weights:样本的权重，越大选取几率越大  
  - num_samplers:总采样的数目//当采样数目==样本数目，且replacement=False时，意味样本每一个采一次都会采到  
                              那么WeightedRandSampler将失去意义。  
  - replacement:是否可重复选取                                                                                               
  
</details>

<details><summary>Visualization可视化</summary>
  
- Visdom类似matplotlib的画图工具  
  ```python
  import visdom
  vis=visdom.Visdom(env='test')
  vis.line(X,Y,Win='',name='')//横纵坐标，窗口名字，线的名字，重复两次，win命名相同，新图覆盖旧图    
  vis.line(X,Y,Win='',update='append',name'')//设置update方式为apend，数据更新，不覆盖原图  
  vis.updateTrace(X,Y,Win='',name='')//在同一个窗口上画一条新线    
  vis.image(ndarray，Win='')//接收一个numpy array的数据，并可视化为图片      
  vis.images(ndarray,Win='',nrow=)//接收一个batch的ndarray数据，并可视化图片，nrow指定有多少行  
  vis.text(''' ''',Win='')//支持html语法<br>换行<hl>标题<b>加粗之类的          
  ```
</details>

<details><summary>GPU加速</summary>
  
- torch.cuda.is_available()     gpu是否可用
- torch.backends.cudnn.benchmark   设为True有助加速训练  
- torch.nn.DataParallel(model,device_id=[])  这是一个类，将model从原始GPU上复制到其他GPU上，在minibatch运行时，均分到每个model副本上，所以minibatch数量最好是 device_ids数量的整数倍。 最终，反向梯度传播会汇聚到原始model上。  
- Tensor,Variable,Module都有.cuda()方法，但是有区别：
  - Tensor，Variable的.cuda()以后，返回新的变量为GPU版本，原来的变量没有变化  
  - Module的.cuda()以后，是inplace方式，Module自身变为GPU版本  

- .cuda(device=)  
  - device:应用哪一块GPU  
- is_cuda  
  - 是否在GPU上  
- get_device()返回使用的GPU是哪一块  
- 损失函数也是一种运算可放在GPU上  
- torch.cuda.device()设置默认使用的GPU  
- torch.cuda.set_device()指定使用某一块GPU  
- CUDA_VISIBLE_DEVICE来指定使用多块GPU
  - 命令行格式 python main.py CUDA_VISIBLE_DEVICE 0,1  
  - import方式 import os ,os.environ["CUDA_VISIBLE_DEVICE"]="0,1"  
  - 使用指定的某几块物理GPU  
  - 在逻辑使用上，还是按0,1，2 的顺序使用，虽然可能使用的是第2,4,5块物理GPU  
  - 在数据处理，训练，测试时涉及到很多运算，1. 什么样的运算可以在GPU上加速 2. 这些运算在GPU上实现加速的原理或机制 3. 合理设计GPU加速机制  
 
</details>

<details><summary>向量化</summary>
  

</details>

<details><summary>torch.optim.lr_scheduler</summary>
  
 - torch.optim.lr_scheduler.StepLR(optimizer,stepsize,gamma=0.1,last_epoch=-1) //每stepsize个epoch后，lr变为原来的0.1,直到最后一个epoch时，lr变为初始大小。  
 </details>
