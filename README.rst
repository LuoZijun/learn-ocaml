Learn OCaml
====================


:Author: Luo Zijun
:Date: 2014-06-04
:Category: book,doc,OCaml,language
:Copyright: Open


.. contents::


OCaml语言简介
-----------------------------
`OCaml <http://en.wikipedia.org/wiki/OCaml>`_  语言是一门多范式（指令式，函数式，面向对象）类型的语言，由作者 `INRIA <http://zh.wikipedia.org/wiki/INRIA>`_ 发行于1996年，目前最新版本为4.00.1/2012-10-05。

官网：`OCaml <http://ocaml.org/>`_

官方文档：`OCaml Docs <http://ocaml.org/docs/>`_    `Tutorials <http://ocaml.org/learn/tutorials>`_  ` OCaml Manual <http://caml.inria.fr/pub/docs/manual-ocaml/>`_


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
*   value names (syntactic class value-name),
*   value constructors and exception constructors (class constr-name),
*   labels (label-name, defined in section 6.1),
*   polymorphic variant tags (tag-name),
*   type constructors (typeconstr-name),
*   record fields (field-name),
*   class names (class-name),
*   method names (method-name),
*   instance variable names (inst-var-name),
*   module names (module-name),
*   module type names (modtype-name).

赋值(Values)
^^^^^^^^^^^^^^

.. code:: ocaml
    
    let sum = 10;;

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

    val

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

.. code:: ocaml
    

    (* 定义类 stack_of_ints *)
    class stack_of_ints =
        object (self)
        val mutable the_list = ( [] : int list ) 
        method push x =                        (* push 方法 *)
            the_list <- x :: the_list
        method pop =                           (* pop 方法 *)
            let result = List.hd the_list in
            the_list <- List.tl the_list;
            result
        method peek =                          (* peek 方法 *)
            List.hd the_list
        method size =                          (* size 方法 *)
            List.length the_list
        end;;

    (* 实例 *)
    let s = new stack_of_ints;;

    (*  迭代 *)
    for i = 1 to 10 do
        s#push i
        done;;
    (* 循环 *)
    while s#size > 0 do
        Printf.printf "Popped %d off the stack.\n" s#pop
        done;;

对象(Object)
^^^^^^^^^^^^



OCaml语言执行效率
---------------------------------------
博客阅读：`浅谈代码的执行效率（2）：编译器的威力 <http://www.cnblogs.com/JeffreyZhao/archive/2010/01/08/talk-about-code-performance-2-compiler.html>`_   作者： `赵劼 <http://www.cnblogs.com/JeffreyZhao/>`_

**以下为原文引用：**

编译器的优化并非在空谈。例如Core Java 2中阐述了这样一个现象，便是JDK中的BitSet集合效率比C++的性能高。当然，文章里承认，这是由于Borland C++编译器的BitSet模板实现不佳导致的性能底下。不过这篇文章的数据也已经旧了，据某大牛的可靠消息，Core Java 7中表示，BitSet的效率已经打败了g++的编译成果，感兴趣的朋友们可以翻阅一下，如果我找到了网上的引用资料也会及时更新。这也是编译器的优化效果，因为对于BitSet这种纯算术操作，Java比C/C++这种静态编译的语言快很正常，因为JIT可以找到更多在运行时期可以做的特殊优化方式。

最后再举一个例子，便是Google工程师Mark Chu-Carroll在3年多前写的一篇文章《The “C is Efficient” Language Fallacy》，其中表示C/C++只是“最贴近CPU的语言”，但并非是进行科学计算时最高效的语言——甚至它们几乎不可能成为最高效的语言。这也是编译器的缘故，且看Mark列举了一小段代码：

.. code:: c++

    for (int i=0; i < 20000) {
        for (int j=0; j < 20000) {
            x[i][j] = y[i-2][j+1] * y[i+1][j-2];
        }
    }


这段代码进行的是两个数组的计算。此时C++编译器便会遇到一个叫做“别名检测（alias detection）”的问题，那就是C++编译器无法得知x和y两个数组的关系（试想如果它们是一个函数的两个参数，也就是说没有任何其他上下文信息），例如它们是不是同一个数组？是不是有重叠？要知道C++的数组访问只是基于下标地址配合偏移量的计算，因此x和y的内容完全可能出现重叠现象。于是C++编译器只能老老实实地按照高级代码的写法生成机器码，优化的余地并不大——这里由于语言特性而导致编译器无法进行更高级的优化，可谓是一个“硬伤”。

Mark表示，Fortran-77可以区分x和y两者是否相同，Fortran-98可以由程序员指名两者并无重叠（如果我没有理解错原文的话），而一个由Lawrence Livermore实验室发明实验性语言Sisal比Fortran更有20%的性能提高。此外Mark还提出了他经历过的一个实际案例：几年前他要写一个复杂的算法来求出两个数组中“最长相同子串”，当时他不知道哪种语言合适，便使用多种语言各实现了一遍。最后他使用两个长为2000的数组进行测试的结果为：

*   C：0.8秒。
*   C++：2.3秒。
*   OCaml：解释执行花费0.6秒，完全编译后执行耗费0.3秒。
*   Java：1分20秒。
*   Python：超过5分钟。

一年以后它使用最新的Java运行时，改进后的JIT只用了0.7秒便执行完了——当然还有额外的1秒用于启动JVM。在评论中Mark补充到，他是个严肃的C/C++程序员，并且已经尽他最大的努力来对C代码进行了优化。而当时他从来没有用过OCaml写过程序，更别说对OCaml代码进行一些取巧的优化方式了。至于OCaml高效的原因，他只是简单的提了一句，我也没有完全理解，便直接引用，不作翻译了::

    The results were extremely surprising to me, and I did spend some time profiling to try to figure out just why the OCaml was so much faster. The specific reason was that the Caml code did some really clever stuff - it basically did something like local constant propagation that were based on be able to identify relations between subscripts used to access different arrays, and having done that, it could do some dramatic code rewriting that made it possible to merge loops, and hoist some local constants out of the restructured merged loop.

事实上，OCaml似乎的确是门了不起的语言，您可以在搜索引擎上使用“C++ OCaml Performance”作为关键字进行查找，可以找到很多性能比较的结果，以及OCaml编译优化方面的资料。自然，这些是题外话，您可以把它们作为扩展阅读用于“开阔视野”。我列举这个例子也不是为了说明C/C++的性能不够好，我这里谈的一切都是想说明一个问题：代码的执行效率并非能从字面上得出结论，更不是“简短”两个字能说明问题的。少一些赋值，少一些判断并非提高性能的正确做法，甚至您的手动优化会让编译器无法理解您的意图，进而无法进行有效的优化。如果您真想在细节上进行优化，还是进行Profiling之后，针对热点进行有效地优化吧。

OCaml语言的应用
----------------------------------
用OCaml写成的程序 `列表 <http://zh.wikipedia.org/wiki/OCaml#.E7.94.A8OCaml.E5.86.99.E6.88.90.E7.9A.84.E7.A8.8B.E5.BA.8F>`_ ：

**一般用途**

*   `MLDonkey <http://zh.wikipedia.org/wiki/MLDonkey>`_  - a multi-network P2P program
*   Unison - a file synchronizer

**教育**

*   `GeoProof <http://home.gna.org/geoproof/>`_  - a dynamic geometry software
*   `MinCaml <http://min-caml.sourceforge.net/index-e.html>`_  - a small tutorial compiler written in OCaml.

**工程**

*   `Confluence <http://www.confluent.org/>`_  is a language for synchronous reactive system design. A Confluence program can generate digital logic for an FPGA or ASIC platform, or C code for hard real-time software.

**娱乐**

*   Index of `toys and examples <http://caml.inria.fr/cgi-bin/hump.en.cgi?sort=0&browse=19>`_  on the Caml hump.
*   Several International Conference on Functional Programming Contest winners
*   `Gravity simulator <http://handhelds.freshmeat.net/projects/planets/>`_

**科学**

*   `Coq <http://coq.inria.fr/>`_  is a proof assistant.
*   `Orpie <http://www.eecs.umich.edu/~pelzlpj/orpie/>`_  - a fullscreen RPN calculator for the console. Its operation is similar to that of modern HP calculators.
*   `FFTW <http://www.fftw.org/>`_  - C FFT library, most of whose performance-critical code is generated by a program written in OCaml.

