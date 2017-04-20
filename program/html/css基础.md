# html
```
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>无标题文档</title>
<link href="style/style.css" rel="stylesheet"/><!--样式表-->
</head>
<body>
<a name="m2"></a>
<h1>相亲</h1>
<h2>相亲</h2>
<p class="p1">啦啦啦啦!</p><br/>
<p class="p2">啦啦啦啦!</p><br/>
<p id="p3">啦啦啦啦!</p><br/>
<div>
    <div id="son1">
        <div>
        好神奇啊1.
        </div>
    </div>
    <div id="son2">
        <div>
        好神奇啊2.
        </div>
    </div>
    <div id="son3">
        <div>
        好神奇啊3.
        </div>
    </div>
    <div id="son4">
        <div>
        好神奇啊4.
        </div>
    </div>
    <div id="son5">
        <div>
        好神奇啊5.
        </div>
    </div>
    <div id="son6">
    </div>
    <div id="son7">
    </div>
</div>
<br/>
<div id="float">
	<div id="float1" class="squre">
    
	</div>
    <div id="float2" class="squre">
        <div id="float21" class="squre2">
        	
        </div>
        <div id="float22" class="squre2">
	
		</div>
	</div>
    <div id="float3" class="squre">
	
	</div>
    <div id="float4" class="squre">
		<a  href="#m2" style=" height:150px; width=300px; color:#000; display:block;">返回顶部</a>
	</div>
</div>
<br/>
<img src="images/2.jpg"  height="50%" width="50%" style="margin:0 auto; display:block;"/><!--内联标签转为块标签,可以居中-->
<a href="#m1">查看下个图片</a><!--第二种锚点-->
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<a name="m1"></a>
<img src="images/3.jpg" height="50%" width="50%" style="margin:0 auto; display:block;"/>
</body>
</html>

```
# style
```
@charset "utf-8";
/* CSS Document */


h1,h2,h3{text-align:center;color:#726363;}/*群组选择器，可以包含以下三种选择器*/
p{color:#FF0000;}/*标签选择器*/
p.p2{color:#FF7F00;}/*class选择器*/
#p3{color:#FFFF00;}/*id选择器*/
/*div div{width:200px;height:200px}标签选择器*/
div #son1 div{color:#C00;}/*伪类选择器,空格是进入*/
div #son2 div:hover{ background:red;}/*鼠标经过，背景变色*/
#son3 div{ background:blue;}
#son4 div{ background:green;margin-top:50px;margin-left:50px;}
#son5{ width:200px;height:200px;background:green;margin:50px auto;
		border:5px solid black;}
#son6{width:200px;height:200px;background:green;margin-top:100px;
		border-top:20px solid #0000FF;border-bottom:20px solid black;border-left:10px solid red;border-right:10px solid yellow;}
#son7{ width:0px;height:0px;margin-top:100px;
		border-top:20px solid #0000FF;border-left:10px solid transparent;border-right:10px solid transparent;}
#float div{display:inline-block;float:left;}/*行内块元素*/	
#float1{background:#F9D6BB;}
#float2{background:#F58788;position:relative;left:20px; top:10px;}/*position:relative相对自己本身的位置*/
#float3{background:#F85053;}
#float4{background:#F85053;position:fixed;left:10px; bottom:10px;}
/*默认static为没有定位；position:fixed相对屏幕的位置;absolute是网页左上角起的绝对
位置(父级容器relative的情况以父级左上角位置起)栗子如下;*/
#float21{background:green;position:absolute;left:30px; top:0px;}
#float22{background:blue;position:absolute;left:30px; top:20px;}
.squre{width:50px;height:50px;}/*正方形类*/
.squre2{width:20px;height:20px;}/*正方形类*/
.clearfix{clear:both;}/*清除浮动类*/
```

