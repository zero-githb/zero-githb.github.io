+ ### shell 编程

  + ##### shell 是命令解释器

    > 以 #!/bin/bash  打头
    >
    > 1. 脚本需要可执行权限	
    >
    > 	+ chmod 744 xxx（文件路径）
    > 2. 指定sh解释器执行
    >
    > 	+ sh   xxx（文件路径）

+ #### hello world

	```shell
	#!/bin/bash
	echo “hello world”
	```

+ #### shell 变量

  + ##### 系统变量

  	+ > $HOME
  		>
  		> $PWD
  		>
  		> $SHELL
  		>
  		> $UER
  		>
  		> 等等

  	+ ##### 显示当前shell的所有变量     set

  + ##### 自定义变量

  	```shell
  	A=100			# = 两侧不能有空格哦
  	echo "A=$A"		#引用变量A，引用时要加 $
  	unset			#撤销变量A
  	echo “A=$A”
  	```
  	
  	> 上代码输出结果：
  	>
  	> A=100
  	>
  	> A=
  	
  	+ ##### 静态变量
  	
  		+ 静态变量用 readonly ,,,,,,静态变量不能  unset
  	
  	+ ##### 把命令的结果返回给变量
  	
  		```shell
  		A=`ls -la`  # ` `,运行里面的命令，把结果返回给变量
  		A=$(ls -la)   #等价于第一个
  		```
  	
  		```shell
  		RES=`ls -l /home`
  		echo $RES			#输出home的目录
  		echo ""				#输出空行
  		MY_DATE=$(date)		# `date`,输出当前时间，
  		echo "date=$MY_DATE"
  		```

  + #### 设置环境变量

   +    vim /etc/profile    配置环境变量

        + > 基本语法：

        	>
        	> 1. export  变量名=变量值	# 将shell变量输出为环境变量
        	> 2. source 配置文件               #让修改的配置信息立即生效，刷新配置文件
        	> 3. echo  $变量名    #查询环境变量的值

  + ##### 多行注释

  	> :<!					!

  + ##### 位置参数变量

   +    将外部参数传的程序内部

        	> $n ：n为数字，n为0时代表命令本身，n=1~9代表一到九个参数，十以上的		用{ } 包住
        	>
        	> $* ：代表命令行中的所有参数，把命令行中的所有参数看成一个**整体**
        	>
        	> $@：代表命令行中的所有参数，把每一个参数区分对待
        	>
        	> $#：代表命令行中所有参数的个数
        	
        	```shell
        	#!/bin/bash
        	echo "$0 $1 $2"
        	echo "$*"
        	echo "$@"
        	echo "$#"
        	```


        ​	

  + #### 预定义变量

    + ##### shell中预先设置好的变量

    	> $$ ：当前进程的进程号（pid）
    	>
    	> $! ：后台最后一个进程的pid
    	>
    	> $?：最后一次执行命令的返回状态，若是0，则表示上一个命令执行正确；若不是0，则证明上一个命令执行不正确。

    + 实例：

    	```shell
    	#!/bin/bash
    	echo "当前进程号：$$"
    	#后台运行脚本
    	./myshell.sh &
    	echo "最后的进程号（pid）:$!"
    	echo "执行的值：$?"
    	```

+ #### 运算符

  + ##### 基本语法

  	1. > $((运算式))   或者   
  	
  	> $[运算式]
  	
  	2. > expr m + n
  	
  		>
  		> 注意：expr运算符间要有空格
  		>
  		> expr m - n
  	>
  		> expr  \*,/,%      乘，除，取余
  	
  	```shell 
  	#计算（2+3）*4
  	#!/bin/bash
  	#第一种方法
  	RESULT1=$(((2+3)*4))
  	echo "result1=$RESULT1"
  	#第二种方式
  	RESULT2=$[(2+3)*4]
  	#使用expr
  	temp=`expr 2 + 3`
  	RESULT3=`expr &temp \* 4`
  	echo "result3=$RESULT3"
  	#求两数之和，，，命令行参数
  	SUM=$[$1+$2]
  	echo "SUM=$SUM"
  	```
  
+ #### 条件判断

	+ ##### 基本语句

		> [ condition ]   (condition**前后**要有**空格**)
		>
		> 非空返回true，，，，用&？验证，0为true，非0为false

	+ ##### 常用判断条件

		1. 两个整数的比较
	
			> = ：字符串比较
			>
			> -lt：小于
			>
			> -le：小于等于
			>
			> -eq：等于
			>
			> -gt：大于
			>
			> -ge：大于等于
			>
			> -ne：不等于
	
		2. 按照文件权限进行判断
	
			> -r ：有读的权限
			>
			> -w：有写的权限
			>
			> -x：有执行的权限
	
		3. 按照文件类型进行判断
	
			> -f：文件存在并且是一个常规的文件
			>
			> -e：文件存在
			>
			> -d：文件存在并且是一个目录
	
		```shell
		#!/bin/bash
		#案例1:“ok”是否等于“ok”
		if [ "ok" = "ok" ]
		then				#如果等于就输出 等于
			echo "deng yu"
		fi
		#案例2:23是否大于等于22？
		if [ 23 -gt 22 ]
		fi
		#案例3：判断文件是否存在
		if [ -e /home/aaa.txt ]
		fi
		```

+ ### 流程控制

  + #### if 判断

  	+ 基本语法

  		```shell 
  		if [ 条件判断式 ];then
  			程序
  		fi
  		#########或者##########
  		if [ 条件判断式 ]
  		then
  			程序
  		elif [ 条件判断式 ]
  		then
  			程序
  		fi
  		```
	
  		```shell
  		#!/bin/bash
  		if [ $1 -ge 60 ]	#大于或等于60
  		then 
  			echo "及格了！！！"
  		elif [ $1 -lt 60 ]	#小于60
  		then
  			echo "不及格"
  		fi
  		```
  	
  + #### case语句

  	+ 基本语法

  		```shell 
  		case 变量名 in
  		"值1"）
  			程序
  		;;
  		"值2"）
  			程序
  		;;
  		esac
  		## 如果变量的值没有上述的，则程序就不执行
  		```

  + #### for循环

  	+ 基本语法

  		```shell
  		for 变量 in 值1 值2 值3
  		do
  			程序
  		done
  		#类似python的for循环
  		#######语法2 ##############
  		for（（初始值；循环控制条件；变化变量））
  		do
  			程序
  		done
  		```
	
  		```shell
  		#!/bin/bash
  		SUM=0
  		for((i=1;i<=100;i++))
  		do
  			SUM=$[$SUM+$i]
  		done
  		echo "sum=$SUM"
  		#1加到100，，，，5050
  		```

  + #### while循环

  	+ 基本语法

  		```shell
  		while [ 条件判断式 ]
  		do
  			程序
  		done
  		```
	
  		```shell
  		#!bin/bash
  		sum=0
  		i=0
  		while [ $i -le $1 ]
  		do
  			sum=$[$SUM+$i]
  			i=$i+1
  		done
  		echo "sum=$sum"
  		```

+ #### read读取控制台输入

	+ read [选项] [参数]

		> -p : 指定读取时的提示信息
		>
		> -t: 指定读取的等待时间
	
		```shell
		#!/bin/bash
		read -p "请输入：" num
		echo "你输入的是：$num"
		
		#指定时间内输入，10s
		read -t 10 -p "请输入：" num	#10s内输入，否则就不等待了
		echo "你输入的是：$num"
		```

+ ### 函数

	+ #### 系统函数

		+ ##### basename 基本语法
	
			+ ##### basename [pathname] [后缀]
	
			+ ##### 功能：返回完整路径最后  /  的部分，用于获取文件名
	
			```shell
			#!/bin/bash		#可以在终端使用
			#返回/home/aaa/teas.txt
			basename /home/aaa/teas.txt      #返回结果：teas.txt 
			basename /home/aaa/teas.txt .txt      #返回结果：teas
			```
	
		+ ##### dirname 基本语法
	
			+ 功能：和basename相反，获取完整路径最后 /  前的部分
			+ dirname 文件的绝对路径

	+ #### 自定义函数

		```shell
		function funname[()]
		{
			sum=$[$n1+$n2]
			echo "和：$sum"
		}
		read -p "输入" n1
		read -p "输入" n2
		#调用
		funname $n1 $n2
		```

	
​	
	

	

	

	

	
	

