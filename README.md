# Database-Homework

[![](https://img.shields.io/badge/Homework-@lyc0930-informational.svg?style=flat)](https://github.com/lyc0930) ![](https://img.shields.io/badge/USTC-2020Spring-green.svg?style=flat)

Homework assignments of **An Introduction to Database System**

## [Homework 1](https://github.com/lyc0930/Database-Homework/tree/master/Homework1)

2020.3.3

-   关系数据模型
-   完整性规则

## [Homework 2（有误）](https://github.com/lyc0930/Database-Homework/tree/master/Homework2)

3.10

-   关系代数

## [Homework 3](https://github.com/lyc0930/Database-Homework/tree/master/Homework3)

3.25

-   SQL 查询

## [Homework 4（有误）](https://github.com/lyc0930/Database-Homework/tree/master/Homework4)

4.8

-   关系模式

## [Homework 5](https://github.com/lyc0930/Database-Homework/tree/master/Homework5)

4.22

-   ER 模型实例
-   **TikZ ER 模型图**

## [Homework 6](https://github.com/lyc0930/Database-Homework/tree/master/Homework6)

4.26

-   数据库数据结构
    -   B+ 树
    -   [个人完成的用以绘制 B+ 树的 TikZ 包](https://github.com/lyc0930/Database-Homework/tree/master/tikz-B+Tree/tikz-B+Tree.sty)，[用法](#tikz-btree-包)
    -   可扩展 Hash

## [Homework 7](https://github.com/lyc0930/Database-Homework/tree/master/Homework7)

5.5

-   事务处理

## [Homework 8](https://github.com/lyc0930/Database-Homework/tree/master/Homework8)

5.19

-   事务调度

---

## tikz-B+Tree 包

一个简单的用于绘制 3-4 B+ 树结点的 TikZ 包

1. 引用

```latex
\usepackage{tikz-B+Tree}
```

2. 提供

-   `node style` `B+node`
    -   `anchor`
        -   `ptr1`
        -   `ptr2`
        -   `ptr3`
        -   `ptr4`
        -   `proc`
-   `path style` `Pointer`
-   `alias` `\B+{#1|#2|#3}`

3. 实例

```latex
\documentclass{standalone}
\usepackage{tikz-B+Tree}
\begin{document}
\begin{tikzpicture}[every node/.style = {B+node, draw}, every path/.style = {Pointer}]

    \node at(  0  ,   0  ) (A1) {\B+(13|{\color{blue}37}|)};
    \node at(-12em,  -6em) (B1) {\B+(7||)};
    \node at(  0em,  -6em) (B2) {\B+({\color{blue}23}|{\color{blue}31}|)};
    \node at( 12em,  -6em) (B3) {\B+({\color{blue}43}||)};
    \node at(-18em, -12em) (C1) {\B+(2|3|5)};
    \node at(-12em, -12em) (C2) {\B+(7|11|)};
    \node at( -6em, -12em) (C3) {\B+(13|17|19)};
    \node at(  0em, -12em) (C4) {\B+(23|29|)};
    \node at(  6em, -12em) (C5) {\B+({\color{blue}31}|{\color{red}36}|)};
    \node at( 12em, -12em) (C6) {\B+({\color{blue}37}|{\color{blue}41}|)};
    \node at( 18em, -12em) (C7) {\B+(43|47|)};

    \foreach \i in {1, 2, 3}
        \draw (A1.ptr\i) to (B\i);
    \foreach \i in {1, 2}
        \draw (B1.ptr\i) to (C\i);
    \foreach \i [evaluate=\i as \j using int(\i+2)] in {1, ..., 3}
        \draw (B2.ptr\i) to (C\j);
    \foreach \i [evaluate=\i as \j using int(\i+5)] in {1, 2}
        \draw (B3.ptr\i) to (C\j);
    \foreach \i/\j in {1/1, 1/2, 1/3, 2/1, 2/2, 3/1, 3/2, 3/3, 4/1, 4/2, 5/1, 5/2, 6/1, 6/2, 7/1, 7/2}
        \draw (C\i.ptr\j) -- +(0, -1);
    \foreach \i [evaluate=\i as \j using int(\i+1)] in {1, ..., 6}
        \draw (C\i.ptr4) to[out = 0, in = 180] (C\j.proc);

    \draw [blue] (C5.ptr4) to[out = 0, in = 180] (C6.proc);

\end{tikzpicture}
\end{document}
```

![example](https://github.com/lyc0930/Database-Homework/blob/master/tikz-B+Tree/example.png)
