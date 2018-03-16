---
layout: post
title: jQuery一些使用经验
city: 杭州 
tags: [web]
---



引用
---------
```html 
<script src="jquery.min.js" type="text/javascript"></script>
```

声明类
-------
```js
var someClass = {
    someVar:null,// 定义一个变量
    functionName:function(){
        var a = 1; // 定义函数局部变量
        //<div id="J_SomeId" value="5">
        // css selector语法
        var collections = jQuery("#J_SomeId").attr("value");
        // value = 5 , # -> id 
        // <div id="J_TextChange">hello world!</div>
        jQuery('#J_TextChange').text("Hello world!");
        // <div id="J_TextChange">Hello world!</div>
        jQuery.post("someUrl",{"param1":"test"},function(data){
            data = JSON.parse(data); // 如果返回数据是json 
        });
        // map 词典
        jQuery.each(map,function(k,v){
            // do something
        });
        // 找到多选框中被选择item
        var multiOpinionSelected = jQuery("#J_Option option:selected");
        // 移除item中某个attr
        jQuery("css selector 语句").removeAttr("某个attr 名称")
        //<input type="text" placeHolder="没有任何输入的时候显示的文字" id="J_Input">
        jQuery("#J_Input").val("设置的文字")
        // 在浏览器中断点调试
        debugger
        // 浏览器中监听点击事件，并且命中css selector
        jQuery(document).on("click","css selector",function(){
            var t = jQuery(this);// 获得jQuery点击对象本身
            var attr = t.attr("attrName");// 获得点击组件属性
            // do something
        }); 
        // 增加table表格 ; 更新表格内容 
        var tr = jQuery('<tr id="J_'+trId+'"></tr>')
        tr.append(jQuery(<td>一个表格位置</td>))
        tbody.append(tr)
        // 发出警告信息，可以使用alter
        alter("this is alter!");
    },
    alterHtml:function(){
        //<div id="J_Alter"></div>
        jQuery("#J_Alter").html("some html")
    }
}
```
