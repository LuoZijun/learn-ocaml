网络套接字(socket)
========================

:Author: Luo Zijun
:Date: 2014/06/07

.. contents::



OCaml Socket code snippets : http://pleac.sourceforge.net/pleac_ocaml/sockets.html

介绍
---------------------------
OCaml 网络套接字 接口模块（并非库(Lib)）为Unix。
在ubuntu下位于 /usr/lib/ocaml/ ，文件名为：unix.cma 。
在你的代码中导入该模块：

.. code:: ocaml
    
    (* 导入Unix Interface *)
    #   load "unix.cma" ;; (* 载入unix接口文件 *)
    open Unix ;;                 (* 打开Unix 模块，类似于 perl 中的 USE . *)

OCaml中的 unix接口模块是一个 包含了一些 unix* 特有特性的库。其中不仅仅提供了对于INET Socket 和 Unix Socket 的操作支持，还提供了对 Unix* 系统的一些操作。比如 getppid,nice,stdout,stdin,openfile,rename,time……等等。
它更像是python下面的 os 和 sys 以及 socket 库的结合（个人感觉还是有点大杂烩的味道:P ）。


创建套接字连接
-------------------------------------

以基本的TCP协议建立HTTP通讯例子：

.. code:: ocaml
    
    (* 加载unix 库 *)
    #   load "unix.cma" ;;
    open Unix ;;
    
    (* 向网络套接字发送讯息 *)
    let sock_send sock str =
        let len = String.length str in
            Unix.send sock str 0 len []

    (* 接收来自网络套接字的讯息 *)
    let sock_recv sock maxlen =
        let str = String.create maxlen in
        let recvlen = recv sock str 0 maxlen [] in
        String.sub str 0 recvlen
        
    (* TCP Client *)
    let host = Unix.gethostbyname "www.badu.com" in
        let packed_ip = host.h_addr_list.(0) in
            let sock = Unix.socket Unix.PF_INET Unix.SOCK_STREAM 0 in 
                (** socket 接受 三个参数:  
                 
                 
                type socket_domain =
                    PF_UNIX                     (** Unix domain *)
                | PF_INET                     (** Internet domain (IPv4) *)
                | PF_INET6                    (** Internet domain (IPv6) *)
                (** The type of socket domains.  Not all platforms support
                    IPv6 sockets (type [PF_INET6]). *)
                 
                type socket_type =
                    SOCK_STREAM                 (** Stream socket *)
                | SOCK_DGRAM                  (** Datagram socket *)
                | SOCK_RAW                    (** Raw socket *)
                | SOCK_SEQPACKET              (** Sequenced packets socket *)
                (** The type of socket kinds, specifying the semantics of
                communications. *)

                type sockaddr =
                    ADDR_UNIX of string
                | ADDR_INET of inet_addr * int
                (** The type of socket addresses. [ADDR_UNIX name] is a socket
                address in the Unix domain; [name] is a file name in the file
                system. [ADDR_INET(addr,port)] is a socket address in the Internet
                domain; [addr] is the Internet address of the machine, and
                [port] is the port number. *)
                
                
                (* socket 参数 ： *)
                val socket : socket_domain -> socket_type -> int -> file_descr
                (** Create a new socket in the given domain, and with the
                given kind. The third argument is the protocol type; 0 selects
                the default protocol for that kind of sockets. *)
                **)
                
                
                (* 建立连接TCP  *)
                Unix.connect sock (Unix.ADDR_INET (packed_ip,80) ) ;
                (* 发送HTTP协议请求讯息 *)
                sock_send sock "GET / HTTP1.0\r\nHOST:127.0.0.1\r\n" ;
                (* 接收服务器端返回数据 *)
                sock_recv sock 2048;


建立TCP监听
~~~~~~~~~~~~~~~~~~~

.. code:: ocaml

    let server_address = hostinfo.Unix.h_addr_list.(0) in
            ignore (Unix.bind socket (Unix.ADDR_INET (server_address, port)));
            Unix.listen socket 10;
            while true do 
                let (fd, _) = Unix.accept socket in
                let _ = set_nonblock fd in 
                let ins = readall fd in
                    ignore (writeall fd (fn ins));
                    Unix.close fd
            done