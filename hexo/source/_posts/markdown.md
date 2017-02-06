---
title: markdown简明语法  
date: 2017-01-18 10:50:03  
tags: markdown  
---
# markdown简明语法
Markdown是一种极简的『标记语言』，将文本转为HTML，通常为我大码农所用。其不追求大而全，简洁至上，正所谓不求最贵，只求最好！

本文介绍Markdown基本语法，内容很少，一行语法一行示例，学会后可轻松写出高大上的文档，再也不需要各种编辑器去调文章格式。另外，网上有各平台下的Markdown工具可用，也有在线的，我直接使用sublime搞定，Markdown本来就是为了追求简洁，弄个工具岂不多此一举。  
## 强调
星号与下划线都可以，单是斜体，双是粗体，符号可跨行，符号可加空格  
格式：  
<pre>  
**一个人来到田纳西**  
__毫无疑问__  
*我做的馅饼  
是全天下*  
_最好吃的_ 
</pre>

显示效果：  
**一个人来到田纳西**  
__毫无疑问__  
*我做的馅饼  
是全天下*  
_最好吃的_

---  

## 分割线  
三个或更多\-\_\*，必须单独一行，可含空格  
格式：  
<pre>  
&#175;&#175;&#175;
</pre>

显示效果：  
  
---

## 空格,换行
半方大的空格&amp;ensp;或&amp;#8194 ;  
全方大的空格&amp;emsp ;或&amp;#8195 ;  
不断行的空格&amp;nbsp ;或&amp;#160 ;  
2个空格，&amp;emsp;   
换行，连续按2个以上空格，然后回车

---

## 引用 
格式：  
<pre>
> 引用 
</pre>

显示效果：  
> 引用 

内层符号前的空格必须要  
格式：  
<pre> 
>引用  
&emsp;>>引用中的引用 
</pre>


显示效果：   
 >引用
 >>引用中的引用  

---
 
##  标题
格式：  
<pre> 
# 一级标题  
## 二级标题  
### 三级标题  
#### 四级标题  
##### 五级标题  
###### 六级标题   
</pre>

---

## 无序列表
符号之后的空格不能少，\-\+\*效果一样，但不能混合使用，因混合是嵌套列表，内容可超长  
格式：   
<pre>
- 无序列表  
+ 无序列表  
* 无序列表  
- 无序列表：我很长。我也很长！那比一比啊？比就比！我有这么长，你有我长吗？我有这么这么长！好吧，你赢了！ 
</pre>

显示效果：   
- 无序列表
+ 无序列表
* 无序列表
- 无序列表：我很长。我也很长！那比一比啊？比就比！我有这么长，你有我长吗？我有这么这么长！好吧，你赢了！  

---

## 有序列表

数字不能省略但可无序，点号之后的空格不能少  
1. 有序列表
2. 有序列表
3. 有序列表
4. 有序列表 

--- 

## 嵌套列表
\-\+\*可循环使用，但符号之后的空格不能少，符号之前的空格也不能少   
格式：    
<pre>
- 嵌套列表  
&emsp;+ 嵌套列表  
&emsp;+ 嵌套列表  
&emsp;&emsp;- 嵌套列表  
&emsp;&emsp;&emsp;* 嵌套列表  
- 嵌套列表  
</pre>

显示效果：   
- 嵌套列表
  + 嵌套列表
  + 嵌套列表
    - 嵌套列表
      * 嵌套列表
- 嵌套列表  

---

## 文字超链：Inline方式
格式：  
<pre>  
[博客](https://mingdaa.github.io/)  
</pre>

显示效果：    
[博客](https://mingdaa.github.io/ "mingdaa的博客")


## 图片超链
格式：  
<pre>
![image](http://图片地址)
</pre>

显示效果：   
![image](https://avatars0.githubusercontent.com/u/19933368?v=3&u=28da34f8cb1f2fea2eecfba93ed15a5909abaf02&s=400)  

--- 

## 索引超链：Reference方式
索引，1 2可以是任意字符    
格式：  
<pre>
[我的博客][1]  
![图片][2]  

[1]:https://mingdaa.github.io/  
[2]:https://图片地址 
</pre>


显示效果：   
[我的博客][1]  
![图片][2]

[1]:https://mingdaa.github.io/  
[2]:https://avatars0.githubusercontent.com/u/19933368?v=3&u=28da34f8cb1f2fea2eecfba93ed15a5909abaf02&s=400  

---

## 自动链接
尖括号    
格式：  
<pre>
&lt;https://mingdaa.github.io&gt;   
</pre>

显示效果：   
<https://mingdaa.github.io/>

---

## 代码
格式：
<pre>
&#39;&#39;&#39; 
class    
{  
&emsp;&emsp;public static void main(String[] args)   
&emsp;&emsp;{  
&emsp;&emsp;&emsp;&emsp;System.out.println("Hello World!");  
&emsp;&emsp;}  
}  
&#39;&#39;&#39;  
</pre>

显示效果：  
```
class  
{
	public static void main(String[] args) 
	{
		System.out.println("Hello World!");
	}
}
```

---

## 注释
可以使用html的注释，不会在HTML中显示  
格式：  
<pre>
&lt;!-- 注释 --&gt;
</pre>

## 转义字符
Markdown中的转义字符为\，需要转义的有：  
\\ 反斜杠  
\` 反引号  
\* 星号  
\_ 下划线  
\{\} 大括号  
\[\] 中括号  
\(\) 小括号  
\# 井号  
\+ 加号  
\- 减号  
\. 英文句号  
\! 感叹号  


## 表格
格式：  
<pre> 
表头1 | 表头2 <br/>
---|---  <br/>
左上 | 右上  <br/>
左下 | 右下   <br/>
</pre>

显示效果：
   
表头1 | 表头2
---|---
左上 | 右上  
左下 | 右下

---

## HTML 中有用的字符实体
显示结果|描述|实体名称|实体编号
---|---|---|----
&nbsp;|空格|&amp;nbsp;|&amp;#160;
&#60;|小于号|&amp;lt;|&amp;#60;  
&gt;|大于号|&amp;gt;|&amp;#62;   
&amp;|和号|&amp;amp;|&amp;#38;   
&quot;|引号|&amp;quot;|&amp;#34;   
'|撇号&nbsp;|&amp;apos; (IE不支持)|&amp;#39;
￠|分（cent）|&amp;cent;|&amp;#162;    
&pound;|镑（pound）|&amp;pound;|&amp;#163;  
&yen;|元（yen）|&amp;yen;|&amp;#165;    
&euro;|欧元（euro）|&amp;euro;|&amp;#8364;
§|小节|&amp;sect;|&amp;#167;
&copy;|版权（copyright）|&amp;copy;|&amp;#169;
&#174;|注册商标|&amp;reg;|&amp;#174;
&trade;|商标|&amp;trade;|&amp;#8482;
×|乘号|&amp;times;|&amp;#215;
÷|除号|&amp;divide;|&amp;#247;

---

## 其它
文本中可直接用html标签，但是要前后加上空行。
