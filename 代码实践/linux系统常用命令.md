常用快捷键：tab补全参数，包括路径和文件名；方向键上下，出现之前命令（少打相同的命令），Ctrl+c结束目前程序，Ctrl+z暂停程序，fg继续执行程序,clear清空终端显示内容    
- sudo apt-get install softname1   下载软件  
- sudo apt-get remove softname1    卸载软件  
- sudo apt-cache search softname1  搜索软件  
- cd  
  - cd /绝对路径  
  - cd ./相对路径  .代表当前目录  
  - cd .. 返回上级目录  
  - cd - 返回刚才打开的目录  
  - cd ~ 跳转到home directory  
  
- ls  
  - ls -a 显示所有文件，包含隐藏文件  
  - ls -r 级联显示文件  
  - ls -l 详细查询  
  - ls -lm 以人性化的显示形式，显示详细信息  

- touch  
  - touch new 创建文件  
  - touch new1 new2  同时创建多个文件  

- rm  
  - rm old  删除文件    
  - rm -r dir   -r表示递归删除此文件夹中的文件，即可理解为删除此文件夹      
  - rm -i old1 old2 old3 删除文件时，终端提示是否删除此文件  
  - rm -I old1 old2 old3 old4 删除文件时，文件数量大于3时，终端提示是否删除此文件   
  
- cp  
  - cp old new  old为文件，new为目标地址，文件支持正则表达式搜索  
  - cp -i old new  复制时增加确认流程，终端提示是否复制此文件  
  - cp -r old new  递归复制      
  - cp old1 old2 new 多文件同时复制  
  
- mv  
  - mv oldfile newfile 移动并重命名文件  
  - mv oldfile dstdir  移动文件至dstdir目录  
  
- mkdir  
  - mkdir dst 创建文件夹  
  - mkdir -p dst 创建多级文件夹  
  
- rmdir  
  - rmdir old old为空目录，如果不为空，则会报错    
  
- nano
  - nano filename 编辑文件，nano为文件编辑器    
  
- cat
  - cat filename 显示文件内容  
  - cat old > new 将old文件中的内容，移动到new文件中  
  - cat old1 old2 > new 将old1，old2文件中的内容合并到new文件中  
  - cat old1 >> old2  将old1的内容追加到old2中  
  
- chmod 
  - chmod 'ugoa' '+-' 'wrx' file  ugoa代表'user','group','others','all' +-代表增加或减少某样权限 wrx代表'write','read','execution'权限 file指定某个文件  
  `eg: chmod ug+wr file1 表示user和group在file1文件上增加了write和read的权限`  
  `#!/usr/bin/python3 在.py文件头添加此语句，表明使用python3来执行此文件`  
  `file1.py 即可执行`  
  `不需 python3 file1.py`  
  
- 用户管理，需在root用户下操作    
  - useradd 用户  
  - userdel 用户  
  - passwd  用户 为一个用户添加密码，注意linux里面密码不显示  
  - su 用户    注意不加用户名就默认为切换到root用户  
 
