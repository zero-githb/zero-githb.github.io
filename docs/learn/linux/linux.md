+ ##### linux只有一个目录 / 根目录，在Linux世界中，一切皆文件


	bin 目录 存放指令集
	dev 目录 设备管理
	etc 目录 配置文件
	home 家目录
	lib 动态库
	mnt 挂载
	opt 软件目录
	usr 用户文件夹，安装目录

+ #### vi and vim

 + vi  或者 vim ####

  + o，i 进入编辑模式

  + ：，/ 进入命令行模式

  + wq、q、q!，表示保存退出、退出、强制退出，，！表示强制

  + ##### 快捷键（都是在正常模式下）

  	+ p 粘贴

  	+ yy 拷贝当前行，3yy 拷贝当前行向下的3行

  	+ dd 删除当前行

  	+ /### 查找     n 查找下一个

  	+ set nu 显示行号、、、、set nonu 取消显示行号

  	+ g 到达文档的末行，、， gg 到达文档的首行

  	+ u 撤销

  	+ ##### 移动到指定行号

        		 1、显示行号	2、输入要移动的行号	3、按下 shift + g

+ ##### 开机&重启命令

	+ shutdown 
		+ shutdown -h now : 表示立即关机
		+ shutdown -h 1 : 表示 1 分钟后关机
		+ shutdown -r now : 立即重启
	+ halt    直接关机
	+ reboot    重启系统
	+ sync 把未保存的数据报存

+ #### 用户管理
	+ ##### 添加用户 ：useradd 用户名
	+ 将用户添加到指定目录  ： useradd -d /home/### 用户名.
	
	+  
	
	+ ##### 删除用户 ：userdel  用户名
	
	+ 删除用户，但是保留该用户家目录 ： userdel  用户名
	
	+ 彻底删除 ：  userdel -r 用户名
	
+ #### 查询用户信息

     + id 用户名
     + 显示： 用户id号   所在组id   组名

+ #### 用户组管理

	+ 创建组  ：  groupadd 组名
	+ 删除组  ：  groupdel 组名
	+ 创建用户是指定所在的组  ：  useradd -g  组名   用户名  （组名要提前创建）
	+ 修改用户组  ：usermod -g  组名   用户名  （组名要提前创建）

+ #### 用户和组的相关文件

	+ ##### /etc/passwd       用户配置文件

		+ 每行含义 ： 用户名：密码：用户标识号：组标识号：注释性描述：主目录：登陆shell

	+ ##### /etc/group        组配置文件

		+ 组名：口令：组标识号（id）：组内用户列表

	+ ##### /etc/shadow        口令配置文件（密码，登陆信息等，加密的）

		+ 登录名： 加密口令：最后修改时间：最小间隔：最大间隔：警告时间：不活动时间：失效时间：标志
	
+ ### 实用指令

     + ##### 运行级别

          + 1.   0：关机
               2.   1：单用户（找回丢失 密码）
               3.   2：多用户无网络服务
               4.   3：多用户有网络服务
               5.   4：保留
               6.   5：图形界面
               7.   6：重启系统
          + 常用的是 3 和5 
          + 运行级别配置文件： /etc/inittab
          + 切换级别 ：init  【012356】   （输入其中一个指定切换级别）

     + #### 文件目录类

     	+ ##### pwd         显示当前目录的绝对路径

     	+ ##### ls  [选项]  [目录或者文件]

     		+ 常用选项 
     			1. -a，，显示当前目录的所有文件夹。包括隐藏文件
     			2. -l，，以列表的方式显示信息

     	+ ##### cd    切换目录

     		+ cd ~  或者 cd      回到家目录
     		+ cd..    回到上级目录

     	+ ##### mkdir  [选项]  要创建文件目录

     		+ 选项：    -p    一次创建多级目录

     	+ ##### rmdir    删除空白目录（如目录下有内容则无法删除）

     		+ rndir  [选项]  要删除的空白目录

     	+ ##### touch    创建空文件

     	+ ##### cp    拷贝

     		+ cp  [选项]  source  dest    （source：源文件，dest:拷贝路径）
     			+ cp aaa.txt bbb/   (当前目录的aaa.txt拷贝到bbb目录)
     		+ 常用选项    -r    递归复制整个文件夹
     			+ cp -r test/ bbb/    (把test文件夹拷贝到bbb)
     		+ 强制覆盖 ： \cp -r test/ bbb/

     	+ ##### rm    删除文件或目录

     		+ rm [选项]  目标文件夹

     		+ -r  : 递归删除整个**文件夹**

     			-f  :  强制删除不提示

     		+ rm -f aaa.txt        删除文件

     		+ rm -rf /*

     	+ ##### mv    移动文件与目录(剪切)或者重命名

     		+ 重命名：mv oldFileName  newFlieName
     			+ mv aaa.txt  bbb.txt
     		+ 移动文件： mv  文件名   要移动到的目录的路径     （在当前目录下）
     			+ mv aaa.txt  /root/ 

     	+ ##### cat  查看文件内容  （只能浏览不能修改）

     		+ cat [选项]  要查看的文件
     		+ -n      显示行号
     		+ cat -n 文件 | more     以cat指令打开文件，并分页显示

     	+ ##### more

     		+ more  文件
     		+ 一全屏的方式按页显示文本文件的内容
     			1. 空格    向下翻页
     			2. 回车    下行一行
     			3. q          离开more，不再显示该文本内容
     			4. ctrl + f   向下滚动一屏
     			5. Ctrl + b  返回上一屏
     			6. =            输出当前的行号
     			7. :f            输出文件名和当前的行号

     	+ ##### less

     		+ 与more类似，对于显示大型文件有较高的
     			1. 空格键    向下翻动一页
     			2. pgup       向上翻动一页
     			3. pudn         向下翻动一页
     			4. /字符串      向下搜索字符串，n向下查找，N向上查找
     			5. q       离开less
     	
     	+ ##### 输出重定向&追加
     	
     		+ ls -l > 文件    （列表内容**覆盖**写入文件中）
     		+ ls -l >> 文件    （列表内容**追加**到文件的末尾）
     		+ cat  文件1 > 文件2     （将文件1的内容**覆盖**到文件2中）
     		+ echo "内容" >> 文件     （将“内容”追加到文件中）
     	
     	+ ##### echo  ： 输出内容到控制台
     	
     		+ echo [选项] [输出内容]
     		+ 输出环境变量的路径： echo SPATH
     	
     	+ ##### head  显示文件的开头部分内容（默认前10行）
     	
     		+ head  文件   （查看文件头10行内容）
     		+ head -n 5  文件  （查看文件头5行，5可以为其他数字）
     	
     	+ ##### tall 显示文件末尾部分（与head相反）
     	
     		+ tall 文件
     		+ tall -n 5 文件
     		+ tall -f 文件  （实时追踪该文档的所有更新）
     			+ 监控文件有无变化，若有变化，就能看到
     	
     	+ ##### ln   软链接（快捷方式）
     	
     		+ ln -s 目标文件目录  软连接名称
     		+ 删除软链接，rm -rf 软连接名称（名称后不要有 / , 否则可能会删除源目录）
     	
     	+ ##### history     查看执行过的历史命令
     	
     		+ history       显示所有的历史指令
     		+ history  10   显示历史指令的最后10个
     		+ !10       执行历史编号为 10 的指令
     	
     + #### 时间日期类

          + ##### date    显示当前日期

          	+ date      显示当前时间

          	+ date+%Y    显示当前年份

          	+ date+%m   显示当前月份

          	+ date+%d    显示当前日期

          	+ date“+%Y-%m-%d %H%:M:%S“      显示年月日时分秒

          	+ ##### 设置日期(把时间设置为)

          		+ date -s "2020-4-18 14:07:00"  

          + ##### cal  查看日历

          	+ cal [选项]         显示当前月的日历
          	+ cal  2020           显示2020年一年的日历

     + #### 搜索查找类

          + ##### find 从指定目录范围（支持正则）

               + find [搜索范围] [选项]  文件名
               	1. -name   按照名字搜索
               	
               		+ find /home -name hallo.txt
               	2. -user 按照拥有者(用户)查询    -user后接用户名
               	
               		+ find  /opt  -user  root
               	3. -size      查找大于指定大小的文件
               	
          		+ find  /  -size  +20M      在根目录下查找大于20m的文件
               		+ find  /  -size   -20M      在根目录下查找小于20m的文件
          		+ find  /  -size    20M      在根目录下查找等于20m的文件
     
          + ##### locate   快速定位文件路径
     
               + locate 搜索文件
          + 先updatedb  创建数据库，然后在搜索
            
          + ##### grep 和 |  管道符
     
               + grep  过滤查找        |   表示 前一个命令的处理结果传递给后面的命令处理
               + grep [选项] 查找内容 源文件
                    1.  -n  显示匹配行及行号
               2.  -i     忽略字母大小写
               + cat hello.txt | grep yes
          + 可以用来查找文件内容
     
+ #### 压缩与解压缩
  
          + ##### gzip/gunzip    gzip用于压缩，gunzip解压缩    压缩的文件后缀： .gz
    
               + gzip/gunzip 要压缩/解压的文件
               + 不会保留源文件
          
          + ##### zip/unzip        后缀：zip       会保留压缩的源文件
          
               + zip [选项]  压缩文件名称   压缩文件目录     
          
                    unzip [选项] 文件
          
               + zip[选项]     -r  xxx.zip   递归压缩文件目录   
          
               + unzip[选项]     -d  指定解压缩目录  xxx.zip
          
               + zip  -r  mypackage.zip  /home/*
          
               + unzip -d /opt/tmp/ mypackage.zip
          
          + ##### tar   可以压缩也可以解压
          
               + tar [选项] xxx.tar.gz  打包的内容       后缀：tar.gz
                    1. -c  产生 .tar 文件
                    2.  -v  显示详细信息
                    3.  -f   指定压缩文件名
                    4.  -z   打包同时压缩
                    5. -x    解压缩  .tar文件
               + tar  -zcvf  a.tar.gz  a.txt a2.txt          打包多个文件
               + tar  -zcvf  myhome.tar.gz  /home/     打包指定目录下的全部文件
               + tar -zxvf  a.tar.gz       解压到当前目录
               + tar -zxvf  a.tar.gz  -C /opt/           指定解压目录必需存在
     
+ ### 组管理和权限管理

     + ##### 文件/目录的所有者

          + ls  -ahl         查看文件所有者

          + chown  用户名  文件名      **修改文件所有者**

     + ##### 组的创建

          + groupadd  组名

     + ##### 修改文件所在组

          + chgrp  组名  文件名

     + #### 改变用户所在组

          + usermod  -g  组名   用户名
          + usermod  -d  目录名  用户名          改变该用户登陆的初始目录

+ ### 权限

  + 文件类型：    -rw-r--r-- 1 zero zero 246 4月  14 10:01 utools.desktop

  	1. -：普通文件
  	2. d :   目录文件
  	3. l :  软连接
  	4. c ： 字符设备[键盘，鼠标]
  	5. b  :  块文件，硬盘

  	+ r : 读    w: 写
  	+ rw : 表示文件所有者的权限是rw
  	+ r-- : 文件所在组的用户的权限r--,只有读的权限
  	+ r--(第二个)：文件其他组的用户的权限r--,
  	+ 1：如果是文件，表示硬链接的个数，，如果是目录，则表示该目录的子目录个数
  	+ zero ：用户的拥有者
  	+ zero（第二个）：文件所在的用户组
  	+ 246 ：文件的大小（bit），如果是目录则显示4096
  	+ 4月~~：最后修改时间

  + #### rwx权限

    + ##### rwx权限作用到文件

    	+ r : read，可以读取，查看
    	+ w：write，可以修改，但是不代表可以修改文件
    	+ 删除一个文件的前提条件是对该文件所在的目录有写的权限，才可以删除
    	+ x：execute，可以被执行

    + ##### rwx权限作用到目录

    	+ r：可以读取，ls查看目录内容
    	+ w：可以修改，目录内创建，删除，重命名目录
    	+ x：可执行，可以进入改目录

    + ##### 修改权限

    	- ##### chmod     	修改文件或者目录权限	
    	  
    	  - +、-、=  变更权限
    	    
    	    u : 所有者，g：所在组，o：其他人，a：所有人
    	    
    	    1. chmod u=rwx,g=rx,o=x  文件目录名
    	    2. chmod o+w  文件目录名
    	    3. chmod a-x     文件目录名
    	  - ##### 通过数字变更权限
    	    
    	    1. r =4 ,w=2,x= 1,,,,,,,,rwx=4+2+1=7
    	    2. chmod u=rwx,g=rx,o=x  文件目录名     相当与 chmod 751   文件目录名

    	+ #### chown  修改文件所有者

    		> ##### chown newowner  file    改变文件所有者
    		>
    		> ##### chown newowner：newgroup  file    改变文件所有者和所有组
    		>
    		> ##### -R  如果是目录则递归修该目录的文件
    	
    + #### crond 任务调度

    	+ ##### crontab [选项]

    		> -e ：编辑crontab定时任务
    		>
    		> -l ：查询crontab定时任务
    		>
    		> -r  ：删除当前用户所有的crontab任务

    	+ 只是简单的任务，可以直接加入任务中，不用写脚本

    	+ > [* / * * * *] ls -l /etc >/tmp/to.txt     (  []  不要 )
    		>
    		> 1. 第一个 * ：一个小时的第几分钟    0~59
    		> 2. 第二个 * ：一天当中的第几个小时   0~23
    		> 3. 第三个 * ：一个月当中的第几天     1~~31
    		> 4. 第四个 * ：一年的第几个月       1~~12
    		> 5. 第五个 * ：一周中的星期几  0~~7  （0和7都代表周日）

    
    
    
    + ##### 网络配置
    
    	+ #### 指定linux的ip
    	
    		+ ##### vim /etc/sysconfig/network-scripts/ifcfg-eth0
    	
    			> onboot = yes
    			>
    			> bootproto =  static      (static  静态)
    			>
    			> ipaddr =   192.168.1.20 (以静态的方式获取ip)
    			>
    			> gateway    网关
    			>
    			> dns1    dns和网关保持一致
  
+ #### 进程管理

     + ps  [选项]  查看进程

          > -a ：显示当前终端的所有信息
          >
          > -u ：一用户的格式显示进程信息
          >
          > -x  ：显示后台进程运行参数

     + ##### 终止进程

     	+ kill  [选项]  进程id

     		> -9          强制杀掉

     	+ killall 进程名称            (终止多个进程)

     + ##### pstree 查看进程树

     	+ pstree [选项] 

     		> -p ：显示进程pid
     		>
     		> -u：显示进程所属用户

     + ##### 服务管理

     	+ setup      查看服务
     	
     + ##### 监控网络状态

          + ##### 查看系统网络情况

               + ##### netstat [选项]

                    > -an     按一定顺序排列输出
                    >
                    > -p        显示那个进程在调用
          
               + ##### netstat -anp | more

                    + 查看所有网络服务

               + ##### netstat -anp | grep  xxx
          
                    + 查看某（xxx）一项服务
          
          + ##### 动态监控进程
          
               + top [选项]
          
                    > -d   秒数      每隔几秒刷新
                    >
                    > -i     使top不显示闲置或者僵死进程
                    >
                    > -p    通过指定进程id来监控某一个进程的状态
                    
               + 进入top后，
               
                    > N     按照pid排序
                    >
                    > M      以内存使用率排序
                    >
                    > P 		以cpu使用率排序，默认就是此项
                    >
                    > Q		退出top
     
+ ### rpm &  yum

     + ##### rpm 包          类似win的setup.exe

          + ##### rpm -qa | grep xxxx      查询已安装的rpm列表

     + #### yum 包

     	+ ##### yum  list | grep xxx

     	+ ##### yum install xxxx

     

