字符串(String)
======================

:Author: Luo Zijun
:Date: 2014-06-06


.. contents::
    
官方API：http://caml.inria.fr/pub/docs/manual-ocaml/libref/String.html
OCaml博客（非官方）：http://roscidus.com/blog/blog/2014/02/13/ocaml-what-you-gain/


大小写转换
----------------------

.. code:: ocaml
    
    (* 大小 *)
    let s = String.uppercase ("Hello World.") ;;
    (* val s : string = "HELLO WORLD." *)
    (* 小写 *)
    let s = String.lowercase ("Hello World.") ;;
    (* val s : string = "hello world." *)

字符串转整数
----------------------------

.. code:: ocaml
    
    let s = int_of_string "1" ;;   (* 字符串转换整数 *)
    (* val s : int = 1 *)
    
    let s = int_of_char '1' ;;      
    (* val s : int = 49  *)
    
    (* 警告：int_of_bool 是不存在的方法函数。 *)


字符串连接
------------------------------

字符串使用符号"^"来进行前后连接。

.. code:: ocaml
    
    let s = "hello "^"world.\n";; (* 输出结果：hello world.\n *)
    

数学运算符
---------------------------

整数算术操作符::

    + : 加
    - : 减
    * : 乘
    / : 除
    mod : 取模

浮点操作符::

    +. : 加
    -. : 减
    *. : 乘
    /. : 除
    ** : 幂

转换整数到浮点：float_of_int n
转换浮点到整数：int_of_float n


模块代码编译
------------------------------
Link : http://www.java123.net/v/353972-6.html

模块详解：http://www.cnblogs.com/ntest/archive/2013/02/28/2936907.html


struct … end 中的语句。

接口文件a.mli(可选)是一组声明，和 sig … end 类似。

令一个编译单元B就像访问结构一样访问A，通过点记法A.x或直接open A。我 们假定源文件为:a.ml, a.mli, b.ml。

没有B的接口文件。编译过程描述如 下::

    命令  编译  创建文件
    ocamlc -c a.mli A的接口    a.cmi
    ocamlc -c a.ml  A的实现    a.cmo
    ocamlc -c b.ml  B的实现    b.cmi(生成默认接口文件,推导出的接口) b.cmo
    ocamlc -o myprog.exe a.cmo b.cmo    链接  myprog.exe

这个程序和下面的代码是相同的:

.. code:: ocaml

    module A : sig(* a.mli的内容 *)end = struct(* a.ml的内容 *)endmodule B = struct(* b.ml的内容 *)end

模块定义的顺序和链接命令行上的.cmo对象文件顺序是一致的。

参数化的模块
-------------------------

一个函子，写为 functor (S:T) -> M ，是一个从模块到模块的函数。

.. code:: ocaml

    module type T =  sig    type t    val x : t    val g : t -> t  end;;  module M = functor (X : T) ->  struct    type u = X.t * X.t    let y = X.g (X.x)  endmodule S1 =  struct    type t = int    let x 


