---
layout: post
title: 前端组件
city: 杭州 
tags: [web]
---


前端组件
=========
+ [JQClound 词云标签](https://github.com/lucaong/jQCloud)
	
		
		
		<!DOCTYPE html>
		<html>
		  <head>
		    <title>jQCloud Example</title>
		    <link rel="stylesheet" type="text/css" href="jqcloud.css" />
		    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.min.js"></script>
		    <script type="text/javascript" src="jqcloud-1.0.4.js"></script>
		    <script type="text/javascript">
		      /*!
		       * Create an array of word objects, each representing a word in the cloud
		       */
		      var word_array = [
		          {text: "Lorem", weight: 15},
		          {text: "Ipsum", weight: 9, link: "http://jquery.com/"},
		          {text: "Dolor", weight: 6, html: {title: "I can haz any html attribute"}},
		          {text: "Sit", weight: 7},
		          {text: "Amet", weight: 5}
		          // ...as many words as you want
		      ];
		
		      $(function() {
		        // When DOM is ready, select the container element and call the jQCloud method, passing the array of words as the first argument.
		        $("#example").jQCloud(word_array);
		      });
		    </script>
		  </head>
		  <body>
		    <!-- You should explicitly specify the dimensions of the container element -->
		    <div id="example" style="width: 550px; height: 350px;"></div>
		  </body>
		</html>



+ [Chosen selector超帅利器](https://github.com/harvesthq/chosen)			
     + [下载地址](https://github.com/harvesthq/chosen/releases/)  



		
		 
		
		<select id="J_Selector" class="chosen-select" style="width: 30%;">


		  <script type="text/javascript">
				// 单选初始化
				jQuery("#J_Selector").chosen({no_results_txt:"没有结果的时候提示信息!"})
				// 多选初始化	
				jQuery("#J_Selector").chosen({})
				// 更新 
                $("#J_Selector").trigger("chosen:updated");
		  </script>




+ [echart.js 图形可视化](https://github.com/ecomfe/echarts)
