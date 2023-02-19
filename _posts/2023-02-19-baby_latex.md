---
layout:     post
title:      "不精通但是优雅使用LaTeX"
subtitle:   ""
date:       2023-02-20 0:30:00
author:     "Gfssfa"
header-img: "img/bg-post-2023-02-20.jpg"
catalog: true
tags:
    - baby
    - LaTeX

---

倒腾毕设翻译任务后小小总结一下

编辑器和编译器是TeXtsudio+texlive2022。textlive2022是整个官网ios下的完整版本。TeXstudio会自动搜索编译器或者在选项-设置TeXstudio中手动添加编译器。

## 1.数学公式

有一些工具：

**Mathpix** 

支持扫描ocr识别公式并导出。一个免费账号每个月有一定额度，用完可以换个账号或者tb。

![](https://gfssfa-github.oss-cn-shanghai.aliyuncs.com/posts/baby_latex/mathpix.JPG)



**在线工具 latexlive**

 https://www.latexlive.com/ 可以看成在线版的Mathpix。但是多了一些预设的功能操作更方便。![latexlive](https://gfssfa-github.oss-cn-shanghai.aliyuncs.com/posts/baby_latex/latexlive.JPG)

```latex
\begin{equation}
	your equation
\end{equation}
```

需要注意的是，一些特殊数学符号字体需要我们添加额外的包如：

拉丁字母加粗用的`boldsymbol{}`和黑板粗体`mathbb{}`。

```latex
\usepackage{amsmath}%\boldsymbol{}
\usepackage{amssymb} %\mathbb{}
```

## 2.表格

overleaf上有一些参考示例：https://www.overleaf.com/learn/latex/Tables

在线表格生成器

https://www.tablesgenerator.com/

可以自己生成表格，把表格数据打进去，或者根据文件导入。支持一定的单元格编辑（分裂单元格、合并单元格、对齐方式、加粗倾斜字号等），但是表格划线功能比较呆板，需要后续加工。

有趣的是，它导出的再导入却不能正确识别哈哈哈。但是导出的倒都是正确的。

## 4.图片

```
\usepackage{graphicx}

\begin{figure}[t]
	\centering
	\includegraphics[width=7in]{picture/fig.JPG}
	\caption{}
	\label{}
\end{figure}
```

width控制图片缩放大小，或者查阅文档制定图片长宽。

## 3.公式图标编号与引用

```
\begin{table/figure/equation}[htbp]
\caption{}
\label{Labelxxx}
\end{table/figure/equation}
```

注意label要紧跟在caption后面，否则编号会有问题

htpd表示插入的位置：here top bottom page

引用的时候用命令`\ref{Labelxxx}`

## 4.其他

参考文献`\cite{label1,label2}`

修改页边距

```
\usepackage{geometry} 
\geometry{left=25mm,right=20mm,top=25mm,bottom=25mm}
```

首页标题上方留空太大，缩小留空

```
\title{\vspace{-4cm}YOUR TITLE}
```

