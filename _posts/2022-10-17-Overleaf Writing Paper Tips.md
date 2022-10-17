---
layout:     post
title:      Overleaf Writing Paper Tips
subtitle:
date:       2022-10-17
author:     Yongsheng Yu
header-img: img/
catalog: true
tags:
    - paper writing tools
---
## Overleaf 概念

简单讲,Overleaf是一个在线的LaTeX环境. 不需要在自己电脑上安装,通过网页访问即可编写LaTeX.

Overleaf website: https://www.overleaf.com/

## Overleaf基本布局
```
\documentclass{article}
\usepackage[utf8]{inputenc}

\title{test overleaf}
\author{Yongsheng Yu}
\date{October 2022}

\begin{document}

\maketitle

\section{Introduction}

\end{document}
```

## Overleaf 编辑文本
### 加粗
```
\textup{texts}
```
### 颜色
```
%% 首先导入颜色package
\usepackage{color}
\newcommand{\red}[1]{\textcolor{red}{#1}}
%% 标记文本颜色
\red{CNN}
```
### 斜体
```
意大利斜体： \textit{text}
slanted斜体： \textsl{text}
```
### 下划线
```
\underline{text}
```
## Overleaf 插入图片

```latex
%% 在文本开头导入图片package
\usepackage{graphicx}

%% 引用图片
Figure \ref{fig:frog}

%% 插入图片
\begin{figure}
\centering
\includegraphics[width=0.3\textwidth]{frog.jpg}
\caption{\label{fig:frog}This frog was uploaded via the project menu.}
\end{figure}
```
## Overleaf 绘制表格

```
%% 引用表格
\ref{tab:weights}

%% 插入表格
\begin{table}
\centering % 表格位置居中
\begin{tabular}{l|r} % l,r,c表示表格内容靠左、靠右、居中；|表示表格竖线
Item & Quantity \\\hline % |hline表示在表格中绘制横线
Widgets & 42 \\ % \\表示本行数据结束
Gadgets & 13
\end{tabular}
\caption{\label{tab:widgets}An example table.}
\end{table}
```

## Overleaf 文章模板: format and grammer
### main.tex
main.tex是Overleaf生成的论文主体。
```
\documentclass[a4paper]{article}

%% Language and font encodings
\usepackage[english]{babel}
\usepackage[T1]{fontenc}

%% Sets page size and margins
\usepackage[a4paper,top=3cm,bottom=2cm,left=3cm,right=3cm,marginparwidth=1.75cm]{geometry}

%% Useful packages
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage[colorinlistoftodos]{todonotes}
\usepackage[colorlinks=true, allcolors=blue]{hyperref}

\title{Your Paper}
\author{You}

\begin{document}
\maketitle

\begin{abstract}
Your abstract.
\end{abstract}

\section{Introduction}

Your introduction goes here! Some examples of commonly used commands and features are listed below, to help you get started. If you have a question, please use the Overleaf menu in the top left of the editor to see various project settings, and to view our help documentation.

\section{Some examples to get started}

\subsection{How to add Comments}

Comments can be added to your project by clicking on the Review menu in the toolbar above. To reply to a comment, simply click the reply button in the lower right corner of the comment, and you can close them when you're done.

\subsection{How to include Figures}

First you have to upload the image file from your computer using the upload link in the project menu. Then use the includegraphics command to include it in your document. Use the figure environment and the caption command to add a number and a caption to your figure. See the code for Figure \ref{fig:frog} in this section for an example.

\begin{figure}
\centering
\includegraphics[width=0.3\textwidth]{frog.jpg}
\caption{\label{fig:frog}This frog was uploaded via the project menu.}
\end{figure}

\subsection{How to add Tables}

Use the table and tabular commands for basic tables --- see Table~\ref{tab:widgets}, for example.

\begin{table}
\centering
\begin{tabular}{l|r}
Item & Quantity \\\hline
Widgets & 42 \\
Gadgets & 13
\end{tabular}
\caption{\label{tab:widgets}An example table.}
\end{table}

\subsection{How to write Mathematics}

\LaTeX{} is great at typesetting mathematics. Let $X_1, X_2, \ldots, X_n$ be a sequence of independent and identically distributed random variables with $\text{E}[X_i] = \mu$ and $\text{Var}[X_i] = \sigma^2 < \infty$, and let
\[S_n = \frac{X_1 + X_2 + \cdots + X_n}{n}
      = \frac{1}{n}\sum_{i}^{n} X_i\]
denote their mean. Then as $n$ approaches infinity, the random variables $\sqrt{n}(S_n - \mu)$ converge in distribution to a normal $\mathcal{N}(0, \sigma^2)$.


\subsection{How to create Sections and Subsections}

Use section and subsections to organize your document. Simply use the section and subsection buttons in the toolbar to create them, and we'll handle all the formatting and numbering automatically.

\subsection{How to add Lists}

You can make lists with automatic numbering \dots

\begin{enumerate}
\item Like this,
\item and like this.
\end{enumerate}
\dots or bullet points \dots
\begin{itemize}
\item Like this,
\item and like this.
\end{itemize}

\subsection{How to add Citations and a References List}

You can upload a \verb|.bib| file containing your BibTeX entries, created with JabRef; or import your \href{https://www.overleaf.com/blog/184}{Mendeley}, CiteULike or Zotero library as a \verb|.bib| file. You can then cite entries from it, like this: \cite{greenwade93}. Just remember to specify a bibliography style, as well as the filename of the \verb|.bib|.

You can find a \href{https://www.overleaf.com/help/97-how-to-include-a-bibliography-using-bibtex}{video tutorial here} to learn more about BibTeX.

We hope you find Overleaf useful, and please let us know if you have any feedback using the help menu --- or use the contact form at \url{https://www.overleaf.com/contact}!

\bibliographystyle{alpha}
\bibliography{sample}

\end{document}
```
### ref.bib
创建一个参考文献文件.bib，我喜欢取名为ref.bib。这里面是paper citation信息bibtex，bibtex引用信息可以从google scholar上获取，比如：
```
@article{greenwade93,
    author  = "George D. Greenwade",
    title   = "The {C}omprehensive {T}ex {A}rchive {N}etwork ({CTAN})",
    year    = "1993",
    journal = "TUGBoat",
    volume  = "14",
    number  = "3",
    pages   = "342--351"
}
```
### frog.jpg
frog.jpg是用于插入文章的图片。
