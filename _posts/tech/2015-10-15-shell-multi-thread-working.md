---
layout: post
title: shell多进程控制脚本实现
city: 北京
tags: [tech,shell]
---


shell脚本多进程控制实现
====================




shell多进程实现方式
-----------------------------


+ 代码级别实现
	
	:::code 
	
		{
			#to do code 	
		} & 



+ 多进程控制实现
	
	:::code
		
		task_id="`date '+%Y%m%d%H%M%S'`".${RANDOM}
		THREAD_COUNT=3
		rm ".{task_id}*running_flag"
		for task in `cat ${task_file}`;do
			{
				_runing_flag=
				touch ".{task_id}.${RANDOM}.`date '+%Y%m%d%H%M%S'`.running_flag"
				# to do code
				rm 
				
			}&
		 	while [ `ls .${task_id}*running_flag` -ge  ${THREAD_COUNT} ];do
				sleep 10
			done 
		done


+ 上述代码解释
	+ 只是为了对shell进程数目进行控制，另，有些地方需要判断返回值；
	+ running_flag建立，如果加入时间戳方式最好，通过判断时间戳进行抛弃（进程最大容忍时间，避免程序报错后，没有删除running_flag问题）