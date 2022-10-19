---
layout:     post
title:      Markdown语法和Atom文本编辑器
subtitle:
date:       2022-10-17
author:     Yongsheng Yu
header-img: img/
catalog: true
tags:
    - paper writing tools
---
## Markdown概念
<font color=red>Notice: CSDN博客集成了富文本编辑器和Markdown文本编辑器。其中，Markdown编辑器比Atom好用，因为它有可视化和快捷键工具。</font>
## Markdown文本编辑语法

### 标题
    # 一级标题
    ## 二级标题
    ### 三级标题
    #### 四级标题
    ##### 五级标题
    ###### 六级标题

### 换行
两个空格，表示本行结束，另起一行  
两个空格+return，实现段内换行  
\，转义符号能截断引用块

### 引用块
四个空格，或两个tab  

    引用块 <-- 两个tab  

### 字体
    <font face="黑体">我是黑体字</font>
<font face="黑体">我是黑体字</font>
### 字号
    <font size=5>字体、字号和颜色</font>
<font size=5>字体、字号和颜色</font>

### 颜色
    <font color=red>想变成红色的内容</font>  

<font color=red>想变成红色的内容</font>  

    <font color=#0099ff size=5 face="黑体">color=#0099ff size=5 face="黑体"</font>
<font color=#0099ff size=5 face="黑体">color=#0099ff size=5 face="黑体"</font>

### 高亮

    <mark color=red>高亮文本</mark>  
    <table><tr><td bgcolor=green>背景色</td></tr></table>
<mark>高亮文本</mark>
<table><tr><td bgcolor=green>背景色</td></tr></table>

### 加粗和斜体
一对\*号是 --> 斜体  
一对\*\*好是 --> 加粗  

    *斜体*  
    **加粗**
\
    *斜体*  
    **加粗**

### 列表序号

#### 无序列表
无序列表只需在行前加+/-/*符号 + 空格即可  

    + 无序列表
    * bullet list 1
    * bullet list 2   
      * sub item 1
      * sub item 2
* bullet list 1
* bullet list 2   
    * sub item 1
    * sub item 2

#### 有序列表
有序列表则在行前加1.等序号 + 空格即可  

    1. 有序列表  

#### 列表内容
列表内容加入[ ]或[x]来标识待办事项  

    * [x] 待办1
    1. [ ] 待办2  
    2. [x] 待办3  

* [x] 待办1
1. [ ] 待办2
  2. [x] 待办3  

### 引用
md中使用>来标识一个段落的引用，引用可以使用多个>进行嵌套  

    >这里是引用的段落
    >>这里是一层嵌套的引用
    >>>这里是两层嵌套的引用  

>这里是引用的段落
>>这里是一层嵌套的引用
>>>这里是两层嵌套的引用  

### 分割线

    ***  
    ---  
    ___  

### 链接
在md中想要插入某个外链，有两种方式：  

    md语法：[百度](http://www.baidu.com/ "百度一下")  
    html<a>标签：<a href="http://www.baidu.com/" target="_blank">百度</a>

md语法：[百度](http://www.baidu.com/ "百度一下")  
html<a>标签：<a href="http://www.baidu.com/" target="_blank">百度</a>

## 代码块
用反引号``,不是正引号'', e.g. python代码段  

    ```python
    import numpy

    df = np.read_excel(data_path)

    ```

```python
import numpy

df = np.read_excel(data_path)

```

## 表格
md支持了表格的简单形式，使用方式即使用|和-符号进行组合  

    |   表头一   |   表头二   |
    | --------- | --------- |
    | 表格内容一 | 表格内容二 |
    | 表格内容三 | 表格内容四 |  

|   表头一   |   表头二   |
| --------- | --------- |
| 表格内容一 | 表格内容二 |
| 表格内容三 | 表格内容四 |

## 图片
### 直接粘贴图片
安装了 markdown-image-paste 插件，就可以使用 Ctrl + V 快捷键粘贴图片了。不过这个图片必须处于编辑状态，比如通过 QQ 截图，然后直接粘贴就可以。

### 插入网络图片
图片的使用方式有些类似链接，在链接的格式前方加!即可，即![图片名](图片地址)  

    ![github头像](https://github.com/fluidicon.png)
\
![github头像](https://github.com/fluidicon.png)  

## 编辑Latex公式
Latex公式编辑参考：http://www.domuse.com/markdown-and-latex-equation-handbook.html  

$$\vec{x} \stackrel{\mathrm{def}}{=}(x_1,\dots,x_n)$$

    LaTex 语法是独立，本来和 Markdown 语法没有半毛钱关系。  
    但是我们经常要用到数学公式，这时就需要有个支持 Markdown + LaTex 双语法的插件。
    我们的 markdown-preview-plus 巧好满足这样的需求，
    在 File -> Settings -> Packages 中找到 markdown-preview-plus 这个插件，
    点击这个插件的 Settings ，设置插件：  

将这个支持 Latex 数学公式的 Enable Math Rendering By Default 选项勾选上，这样就支持数学公式了（需要重启一下 Atom 编辑器）。当然也要看一下keybindings功能是否打开，如果没有打开则打开快捷键功能，将下面 Enable 勾选上就可以了：  

    $$ S = \int_{a}^b f(x) \mathrm{d}x = F(b) - F(a) $$  

$$ S = \int_{a}^b f(x) \mathrm{d}x = F(b) - F(a) $$

## Atom文本编辑器

### 生成pdf文件
Markdown 生成 PDF 比较简单，如果你安装了 markdown-pdf 插件，鼠标放在目标 Markdown 编辑区域，按下 Shift + Ctrl + C 快捷键即可，过一会就会在当前文件夹目录下生成 PDF 文件了。


## Reference
1. [MarkDown使用教程(In Atom) ](https://www.cnblogs.com/hwb04160011/p/13960499.html)
2. [05_Github编辑器Atom之：Markdown + Latex 公式 + 离线插件安装 + Markdown生成PDF](https://www.jianshu.com/p/6b54e2eb9ae2)
