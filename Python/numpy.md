import numpy as np  
  矩阵创建方法  
  np.ones((rows,cols),dtype=' ')  
  np.zeros((rows,cols),dtype=' ')  
  np.empty((rows,cols),dtype=' ')  
  
  np.ones_like(array,dtype='')  
  np.zeros_like(array,dtype='')  
  np.empty_like(array,dtype='')  
  
  np.random.rand(rows,cols)  
  np.random.randn(rows,cols)  
  
  np.fromfunction(f,(rows,cols),dtype)  
  
  np.arange(s,e,stride)  
  np.linspace(s,e,num)  
  
  np.array([初始化矩阵],dtype)   
  
  矩阵属性  
  np.shape  返回矩阵的尺寸rows x cols  
  np.dtype  返回矩阵数据类型  
  np.size   返回矩阵元素个数  
  np.ndim   返回矩阵维度  
  np.itemsize  返回矩阵元素存储占用的字节数  
  
  索引、切片  
  array[rows-1,cols-1]   获取rows行cols列的元素  
  array[row,:]           获取row-1行的所有元素  
  array[:,col]           获取col-1列的所有元素  
  array[a:b,c:d]         获取a-b行，c-d列的矩形范围的元素  
  array[a,...]           获取某一维的所有元素  
  
  基础运算  
  + np.add  
  -
  /
  *             element-wise product  
  @             matrix product  
  np.dot        matrix product  
  np.sum()        
  np.max()        
  np.min()        
  np.cumsum()
  np.exp()  
  np.sqrt()  
  np.average()  
  np.mean()  
  np.std()  
  np.floor()
  
  其他操作  
  np.reshape(rows,cols)   重塑矩阵尺寸  
  np.resize(rows,cols)    in-place操作  
  np.concatenate((np.array A,np.array B),axis=0,1)  
  np.hstack((a,b))  
  np.vstack((a,b))  
  np.nonzero()  返回矩阵不为零的索引  
  np.where(condition)  只返回结果为true的索引  
  np.where(condition,true result,false result)   类似条件表达式 ? :  
  np.transpose()  np.T  转置  
  np.flat   集合所有元素的迭代器  
  np.ravel()  重塑为1维矩阵  
  np.hsplit(array,(n,...))  纵向分割  
  np.vsplit(array,(n,...))  横向分割  
  id(array)  矩阵id  
  np.copy()  深复制  
