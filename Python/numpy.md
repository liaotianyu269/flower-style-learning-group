import numpy as np  
#常用的创建矩阵的方法  
  np.ones((rows,cols),np.datatype)  
  np.zeros((rows,cols),np.datatype)  #如np.int32  
  
  np.array([初始化矩阵],np.datatype)  
  
  np.shape  返回矩阵的尺寸rows x cols  
  np.dtype  返回矩阵数据类型  
  
  array[rows-1,cols-1]   获取rows行cols列的元素  
  array[row,:]           获取row-1行的所有元素  
  array[:,col]           获取col-1列的所有元素  
  array[a:b,c:d]         获取a-b行，c-d列的矩形范围的元素  
  以上类似于python中list列表的元素访问机制，切片和某个元素的访问  
  
  np.concatenate((np.array A,np.array B),axis=0,1)
