Learn OCaml
====================


:Author: Luo Zijun
:Date: 2014-06-04
:Category: book,doc,OCaml,language

.. contents::


OCaml语言简介
-----------------------------
`OCaml <http://en.wikipedia.org/wiki/OCaml>`_  语言是一门多范式（指令式，函数式，面向对象）类型的语言，由作者 `INRIA <http://zh.wikipedia.org/wiki/INRIA>`_ 发行于1996年，目前最新版本为4.00.1/2012-10-05。

官网：`OCaml <http://ocaml.org/>`_

官方文档：`OCaml Docs <http://ocaml.org/docs/>`_    `Tutorials <http://ocaml.org/learn/tutorials>`_


在书籍资料方面，`京东（JD）书籍搜索 <http://search.jd.com/Search?keyword=ocaml&enc=utf-8>`_ 仅有三本该书的英文进口书籍，中文没有。所以打算学习此门语言的朋友要有阅读官方纯英文文档的准备（即便如此，官方文档也是极其简洁:P）。


OCaml语言翻译
-----------------------------------
首先，我必须声明，本人英文 **极其** 有限，用‘翻译’一词其实是不恰当的，更形象的说法应该是以我的理解来重新描述该语言的一些特性和语法。我的复述难免可能会有各种坑，理解错误等等，所以为避免误人子弟，我强烈建议大家前往官方站点下载 `原版文档阅读 <http://ocaml.org/learn/tutorials>`_ 。

OCaml语法篇
~~~~~~~~~~~~~~~~~~~~~
本章介绍将OCaml的语法。


语法规范
^^^^^^^^^^^

空格（Blanks）
###################
以下字符视为空格：空格符，制表符，回车，换行符和换页符。空格的作用被用作分开两个相邻的标识符，文字，关键字，除此之外，空格将被忽略。

注释（Comments）
####################
OCaml的注释以 '(*' 开始至 '*)' 结束。类似与C语言的 //comments... 与\/*comments...*\/。

OCaml 语言注释：

.. code:: ocaml

    (* OCaml 语言单行注释 *)
    
    (* 
     *OCaml 语言多行注释
     *
     *
     *)


C语言注释 ：

.. code:: c
    
    // C语言单行注释 
    /**
    * C语言
    * 多行
    * 注释
    **/
    

缩进（Identifiers）
###############


保留字(Name)
^^^^^^^^^^^^^^^^

赋值(Values)
^^^^^^^^^^^^^^

.. code:: ocaml
    
    # let sum = 10;;

变量(Variables)
^^^^^^^^^^^^^^^
引用： `Local "variables" <http://ocaml.org/learn/tutorials/structure_of_ocaml_programs.html>`_

C 语言变量：

.. code:: c
    
    double num = 10.12;

Python语言变量：

.. code:: python
    
    num = 10

OCaml语言变量：

.. code:: ocaml
    
    let num = 10;;
    (* val num : int = 10  解释器输出 *)



函数（Function）
^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: ocaml
    
    let sum a b = a + b;;                     (* 定义函数 sum *)
   (* val sum : int -> int -> int = <fun>    解释器输出 *)
    sum 10 20;;                                   (* 执行函数 sum  *)
    (* 运算结果： - : int = 30   *)                                        

.. code:: python
    
    def sum(a,b):                                      # 定于函数
        return a+b                                               
    sum(10,20)                                          # 执行函数
    # 运算结果 30                                                         


类(Class)
^^^^^^^^^^^^


对象(Object)
^^^^^^^^^^^^
