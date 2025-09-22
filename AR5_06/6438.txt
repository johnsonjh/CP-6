The CP-6 Socket Library provides a collection of C-callable functions and 
PL6-callable procedures to permit CP-6 applications to communicate with other 
applications over a LAN. 
A socket is an endpoint for communication.  On CP-6 systems, a socket consists 
of a DCB and some context.  The Host Socket Library provides facilities to 
create and name sockets, to initiate outgoing connections and await incoming 
connections, to send and receive data, to check for the presence of incoming 
data or exceptional conditions, and to terminate connections. 
Other facilities of the library include getting and setting socket options, 
obtaining information about the sockets at each end of a connection, 
converting data between network and CP-6 formats, converting addresses between 
network and character string formats, and obtaining information from 
configuration files that reside in the :SYS account. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
The following changes were made for the A00 release of the Socket Library. 
o New C functions: bcmp(), bcopy(), bzero(). 
o New C functions: sendmsg(), recvmsg(), writev(), readv(). 
o New C structures: iovec, msghdr, xsl_sockinit. 
o New PL6 procedures: XSL$SENDMSG, XSL$RECVMSG, XSL$WRITEV, XSL$READV. 
o New PL6 structures: XSL$IOVEC, XSL$MSGHDR, XSL_SOCKINIT. 
o Added support for 'raw' socket type. 
o Added support for datagrams of up to 9000 bytes. 
o Added provisions for automatically contacting a name server. 
o Fixed send(), recv(), sendto(), recvfrom() to set errno only on errors. 
o Fixed send(), sendto(), write() to honor advantageous throttling. 
o Fixed some unusual situations to report ENOTBOUND. 
o Fixed asynchronous error reporting. 
o Fixed inet_addr(), inet_lnaof(), inet_netof(), inet_network() prototypes. 
o Modified CRAWDAD commands for new features and documented them. 
o Modified defaults for XSL_SOCKINIT. 
o Added information to accept_srvr() and XSL$ACCEPT_SRVR help topics. 
o Added information on errors to select() and XSL$SELECT help topics. 
o Added ERRORS help topic with discussion of asynchronous error reporting. 
o Added XSL_SOCKINIT and xsl_sockinit help topics. 
o Added DEBUGGING help topic. 
o Added XSL$CHAM help topic. 
o Fixed numerous grammatical and typographical errors in help topics. 
The CP-6 Socket Library dynamically allocates and releases socket DCBs as 
needed, without application intervention.  The DCBs used by the library are 
named F$XSLnn, where nn is an internal table index.  One DCB is required for 
each socket in use or awaiting an incoming connection. 
There is also one permanent DCB used for accessing the file etc:routes.:SYS 
and, if necessary, four permanent DCBs for accessing the files etc:hosts, 
etc:networks, etc:protocols, and etc:services, all in .:SYS. 
Application DCBs are neither used nor modified. 
Following is a description of several commands available to debug Socket 
Library applications under DELTA and ANLZ.  This is not a general debugging 
tutorial, nor is much information provided about the internals of Socket 
Library operation. 
The debugging commands are \XSL$SOCKHD, \XSL$SOCKINFO, \XSL$DATABUF, and 
\XSL$EVLOG.  They are implemented as CRAWDAD strings, so the system 
administrator will need to have installed them as part of the general TCP/IP 
installation at your site. 
The general format for usage of the commands is: 
        command offset [USING user#] 
Under ANLZ, the user number of the user running the Socket Library application 
to be debugged will need to be specified.  Under either DELTA or ANLZ, the 
symbol table of the running application needs to be loaded.  The whole process 
goes something like this: 
        !" example of DELTA debugging session follows.. 
        !UNDER DELTA 
        !run-unit-fid 
        ... 
        >command offset         " issue command 
        (repeat as needed) 
        ... 
        >QUIT 
        !" example of ANLZ debugging session follows.. 
        !ANLZ 
        -SPY A=account          " identify the user to be debugged 
        -SYM run-unit-fid       " load the correct symbol table 
        ... 
        -command offset U user# " issue command referring to user 
        (repeat as needed) 
        ... 
        -QUIT 
These commands can be used to debug either a currently running application or 
one that has been SNAPped with SNAP.X.  For later use, invoke ANLZ specifying 
the name of the SNAP dumpfile. 
The most common errors in using the commands are (1) forgetting to load the 
correct symbol table before use, and (2) using the incorrect offset. 
Rudimentary error checking is performed by the commands to help diagnose these 
errors. 
Following are brief descriptions of the command. 
\XSL$DATABUF 
     The \XSL$DATABUF command provides information about a specific NoWait 
     data buffer.  The offset parameter is a word offset into the Socket 
     Library data segment (obtained from one of the other commands). 
     The output from the \XSL$DATABUF command contains the following values: 
         bufx=hexnum         " offset of data buffer 
         nxt=hexnum          " offset of next data buffer in chain 
         sock=hexnum         " (pending buf) offset of owning socket 
         start=hexnum        " (active buf) byte offset to unread data 
         len=decnum          " (active buf) number of bytes of unread data 
         flags set:[ string ]... " currently set buffer status flags 
         key=hexnum...       " contents of KEY for M$READ or M$WRITE 
         key.msgcode=string  " decoded contents of KEY.MSGCODE 
     The data in a data buffer is not displayed, due to its potential size. 
     The DU or DUA commands can be used to dump the data manually.  (The data 
     region starts ten words higher than bufx.) 
\XSL$EVLOG 
     The \XSL$EVLOG command provides a human-readable dump of the Socket 
     Library's internal event log.  The offset parameter must be given as 
     zero. 
     The output from the \XSL$EVLOG command contains the following values: 
         XSL_EVENTIDX=hexnum   " index of next available event log entry 
         XSL_EVENTLOG$=address " address of event log in data segment 
     At this point in the display, the Socket Library's event log is dumped. 
     Each entry in the log occupies one or two words, and each word occupies 
     one line of the display.  Time increases downward in the display.  The 
     display wraps from last entry to first.  There is an indication of where 
     the next available entry is located.  If an entry indicates some sort of 
     monitor error, the error itself occupies the next entry. 
     Following is an example of an event log dump. 
         GP .044706  get sockptr from XSL$LISTEN+.22 
         GB .006114  get buffer .6114 
         NW .006114  nowait read on buffer .6114 
         WT .000006  M$WAIT on sock .6 
         EV .006114  event on buffer .6114 
         RB .006114  release buffer .6114 
         GP .037161  get sockptr from XSL$ACCEPT+.25 
         GT .000032  M$GETDCB on sock .32 
         OP .000032  M$OPEN on sock .32 
         RQ .000032  space available on sock .32 
         WR .000032  M$WRITE on sock .32 
         RD .000032  M$READ on sock .32 
         WR .000032  M$WRITE on sock .32 
         GB .006114  get buffer .6114 
         NW .006114  nowait read on buffer .6114 
         WT .000006  M$WAIT on sock .6 
         >>> next event goes here <<< 
\XSL$SOCKHD 
     The \XSL$SOCKHD command provides general information about the Socket 
     Library data segment.  The offset parameter must be given as zero. 
     The output from the \XSL$SOCKHD command contains the following values: 
         XSL_SOCK$$=hexnum   " base address of data segment 
         segsize=hexnum      " size of data segment in words 
         maxbuf=decnum       " default value of MAXBUF 
         maxrds=decnum       " default value of MAXRDS 
         maxsock=decnum      " number of sockets defined 
         evnt$=address       " address of application's event handler 
         sock(0)=hexnum, sock(1)=hexnum, etc. " socket offset array 
         bufhd=hexnum, buftl=hexnum, " head and tail of free buffer chain 
         hexnum [ >> hexnum ]... >> .0 " chain of free buffer offsets 
\XSL$SOCKINFO 
     The \XSL$SOCKINFO command provides information about a specific socket. 
     The offset parameter is a word offset into the Socket Library data 
     segment (obtained from the \XSL$SOCKHD display). 
     The output from the \XSL$SOCKINFO command contains the following values: 
         sock#=decnum        " socket number 
         dcbn=decnum         " DCBNUM of the socket's DCB 
         dcb=string          " name of the socket's DCB 
         af=decnum           " socket address family 
         type=string         " socket type 
         protocol=decnum     " socket protocol 
         flags set:[ string ]... " currently set socket status flags 
         sockname=decnum/decnum/string " sock family/port/inet-address 
         peername=decnum/decnum/string " peer family/port/inet-address 
         sernum=string       " name of FEP socket is bound to 
         rcrbytsiz=decnum    " maximum data chunk size host to/from FEP 
         feperror=decnum     " asynchronous error to be reported 
         maxbuf=decnum       " socket's current MAXBUF 
         maxrds=decnum       " socket's current MAXRDS 
         bufpnd#=decnum      " current number of pending buffers 
         oob#=decnum         " current number of active oob buffers 
         dat#=decnum         " current number of active data buffers 
         bufhd=hexnum, buftl=hexnum " head and tail of socket's active buffers 
     At this point in the display the socket's buffer chain is dumped.  See 
     the description of the \XSL$DATABUF command for more information on the 
     buffer display. 
Most of the Socket Library functions will return an error indication programs; 
the error names in PL-6 programs are preceded by E$ rather than E (for 
example, E$FAILURE instead of EFAILURE). 
    Error:  ESUCCESS 
    Message:  The operation succeeded. 
    Error:  EACCES 
    Message:  Permission denied. 
    Error:  EADDRINUSE 
    Message:  Address already in use. 
    Error:  EADDRNOTAVAIL 
    Message:  Can't assign requested address. 
    Error:  EAFNOSUPPORT 
    Message:  Address family not supported. 
    Error:  EALREADY 
    Message:  Operation already in progress. 
    Error:  EBADF 
    Message:  Bad file number. 
    Error:  ECONNABORTED 
    Message:  Software caused connection abort. 
    Error:  ECONNREFUSED 
    Message:  Connection refused. 
    Error:  ECONNRESET 
    Message:  Connection reset by peer. 
    Error:  EDESTADDRREQ 
    Message:  Destination address required. 
    Error:  EFAULT 
    Message:  Bad address. 
    Error:  EHOSTDOWN 
    Message:  Host is down. 
    Error:  EHOSTUNREACH 
    Message:  No route to host. 
    Error:  EINPROGRESS 
    Message:  Operation now in progress. 
    Error:  EINTR 
    Message:  Interrupted system call. 
    Error:  EINVAL 
    Message:  Invalid argument. 
    Error:  EIO 
    Message:  Indeterminate FEP I/O error. 
    Error:  EISCONN 
    Message:  Socket is already connected. 
    Error:  ELOOP 
    Message:  Too many levels of symbolic links. 
    Error:  EMFILE 
    Message:  Too many links, or not enough socket slots. 
    Error:  EMSGSIZE 
    Message:  Message too long. 
    Error:  ENAMETOOLONG 
    Message:  Name too long. 
    Error:  ENETDOWN 
    Message:  Network is down. 
    Error:  ENETRESET 
    Message:  Network dropped connection on reset. 
    Error:  ENETUNREACH 
    Message:  Network is unreachable. 
    Error:  ENOBUFFS 
    Message:  No buffer space is available. 
    Error:  ENOENT 
    Message:  Host, network, protocol, or service not found. 
    Error:  ENOPROTOOPT 
    Message:  Protocol not available. 
    Error:  ENOTBOUND 
    Message:  Socket is not bound to a FEP. 
    Error:  ENOTCONN 
    Message:  Socket is not connected. 
    Error:  ENOTSOCK 
    Message:  Socket operation on non-socket. 
    Error:  EOPNOTSUPP 
    Message:  Operation not supported on socket. 
    Error:  EPERM 
    Message:  Not owner. 
    Error:  EPFNOSUPPORT 
    Message:  Protocol family not supported. 
    Error:  EPROTONOSUPPORT 
    Message:  Protocol not supported. 
    Error:  EPROTOTYPE 
    Message:  Protocol wrong type for socket. 
    Error:  ESHUTDOWN 
    Message:  Can't send after socket shutdown. 
    Error:  ESOCKTNOSUPPORT 
    Message:  Socket type not supported. 
    Error:  ETIMEDOUT 
    Message:  Connection timed out. 
    Error:  ETOOMANYREFS 
    Message:  Too many references: can't splice. 
    Error:  EWOULDBLOCK 
    Message:  Operation would block. 
A 
  accept() and XSL$ACCEPT  --  Accept an Incoming Connection Request - 
      HELP accept 
  accept_srvr() and XSL$ACCEPT_SRVR  --  Accept from INETD - 
      HELP accept_srvr 
  Application Debugging - 
      HELP DEBUGGING 
B 
  bcmp()  --  Bytestring Comparison - 
      HELP bcmp 
  bcopy()  --  Bytestring Copy - 
      HELP bcopy 
  bind() and XSL$BIND  --  Bind Name to Socket - 
      HELP bind 
  blocking - 
      HELP accept DESCRIPTION: 
      HELP accept_srvr DESCRIPTION: 
  Bytestring Comparison - 
      HELP bcmp 
  Bytestring Copy - 
      HELP bcopy 
  Bytestring Zero - 
      HELP bzero 
  bzero()  --  Bytestring Zero - 
      HELP bzero 
C 
  close() and XSL$CLOSE  --  Close Socket - 
      HELP close 
  connect() and XSL$CONNECT  --  Initiate Connection Request - 
      HELP connect 
D 
  datagram socket - 
      HELP connect DESCRIPTION: 
  dot notation, conversion from - 
      HELP inet_network PURPOSE: 
  dot notation, conversion to - 
      HELP inet_ntoa DESCRIPTION: 
E 
  endhostent() and XSL$ENDHOSTENT  --  End Host Entry - 
      HELP endhostent 
  endnetent() and XSL$ENDNETENT  --  End Network Entry - 
      HELP endnetent 
  endprotoent() and XSL$ENDPROTOENT  --  End Protocol Entry - 
      HELP endprotoent 
  endservent() and XSL$ENDSERVENT  --  End Service Entry - 
      HELP endservent 
  etc:hosts file, related structure - 
      HELP hostent 
  etc:networks file, related structure - 
      HELP netent 
  etc:protocols file, related structure - 
      HELP protoent 
  etc:services file, related structure - 
      HELP servent 
F 
  fcntl() and XSL$FCNTL  --  File Control - 
      HELP fcntl 
G 
  gethostbyaddr() and XSL$GETHOSTBYADDR  --  Look Up Host by Address - 
      HELP gethostbyaddr 
  gethostbyname() and XSL$GETHOSTBYNAME  --  Look Up Host by Name - 
      HELP gethostbyname 
  gethostent() and XSL$GETHOSTENT  --  Get Host Entry - 
      HELP gethostent 
  gethostname() and XSL$GETHOSTNAME  --  Get Current Host Name - 
      HELP gethostname 
  getnetbyaddr() and XSL$GETNETBYADDR  --  Look Up Network by Address - 
      HELP getnetbyaddr 
  getnetbyname() and XSL$GETNETBYNAME  --  Look Up Network by Name - 
      HELP getnetbyname 
  getnetent() and XSL$GETNETENT  --  Get Network Entry - 
      HELP getnetent 
  getpeername() and XSL$GETPEERNAME  --  Get Socket Peer Name - 
      HELP getpeername 
  getprotobyname() and XSL$GETPROTOBYNAME  --  Look Up Protocol by Name - 
      HELP getprotobyname 
  getprotobynumber() and XSL$GETPROTOBYNUMBER  --  Look Up Protocol by Number 
     - 
      HELP getprotobynumber 
  getprotoent() and XSL$GETPROTOENT  --  Get Protocol Entry - 
      HELP getprotoent 
  getservbyname() and XSL$GETSERVBYNAME  --  Look Up Service by Name - 
      HELP getservbyname 
  getservbyport() and XSL$GETSERVBYPORT  --  Look Up Service by Port - 
      HELP getservbyport 
  getservent() and XSL$GETSERVENT  --  Get Service Entry - 
      HELP getservent 
  getsockname() and XSL$GETSOCKNAME  --  Get Socket Name - 
      HELP getsockname 
  getsockopt() and XSL$GETSOCKOPT  --  Get Socket Option - 
      HELP getsockopt 
H 
  Host Socket Library - 
      HELP HOST_SOCKET_LIBRARY 
  Host Socket Library DCB Usage - 
      HELP DCB 
  Host Socket Library Error Reporting - 
      HELP ERRORS 
  Host Socket Library Include Files - 
      HELP INCLUDE_FILES 
  Host Socket Library Linking Information - 
      HELP LINKING_INFO 
  Host Socket Library Services - 
      HELP SUMMARY 
  hostent - 
      HELP hostent 
  hostent Structure - 
      HELP hostent 
  htonl() and XSL$HTONL  --  Convert Host to Network Long Integer - 
      HELP htonl 
  htons() and XSL$HTONS  --  Convert Host to Network Short Integer - 
      HELP htons 
I 
  INETD - 
      HELP accept_srvr DESCRIPTION: 
  inet_addr() and XSL$INET_ADDR  --  Convert String to Inet Address - 
      HELP inet_addr 
  inet_lnaof() and XSL$INET_LNAOF  --  Get Local Address from Internet Address 
     - 
      HELP inet_lnaof 
  inet_makeaddr() and XSL$INET_MAKEADDR  --  Make Internet Address - 
      HELP inet_makeaddr 
  inet_netof() and XSL$INET_NETOF  --  Get Network from Internet Address - 
      HELP inet_netof 
  inet_network() and XSL$INET_NETWORK  --  Convert String to Network - 
      HELP inet_network 
  inet_ntoa() and XSL$INET_NTOA  --  Convert Inet Address to String - 
      HELP inet_ntoa 
  Initialize Socket Library - 
      HELP XSL$SOCKINIT 
  Internet Address Representation - 
      HELP INTERNET_ADDRESS 
  in_addr - 
      HELP sockaddr_in 
      HELP XSL$SOCKADDR_IN 
  ioctl() and XSL$IOCTL  --  I/O Control - 
      HELP ioctl 
  iovec - 
      HELP iovec 
  iovec Structure - 
      HELP iovec 
L 
  listen() and XSL$LISTEN  --  Listen for Incoming Connections - 
      HELP listen 
M 
  msghdr - 
      HELP msghdr 
  msghdr Structure - 
      HELP msghdr 
N 
  netent - 
      HELP netent 
  netent Structure - 
      HELP netent 
  non-blocking - 
      HELP accept DESCRIPTION: 
      HELP accept_srvr DESCRIPTION: 
      HELP fcntl DESCRIPTION: 
  ntohl() and XSL$NTOHL  --  Convert Network to Host Long Integer - 
      HELP ntohl 
  ntohs() and XSL$NTOHS  --  Convert Network to Host Short Integer - 
      HELP ntohs 
P 
  protoent - 
      HELP protoent 
  protoent Structure - 
      HELP protoent 
R 
  read() and XSL$READ  --  Read Data - 
      HELP read 
  readv() and XSL$READV  --  Read Scattered Data - 
      HELP readv 
  recv() and XSL$RECV  --  Read Data With Options - 
      HELP recv 
  recvfrom() and XSL$RECVFROM  --  Read Data With Options and Address - 
      HELP recvfrom 
  recvmsg() and XSL$RECVMSG  --  Read Scattered Data With Options and Address 
     - 
      HELP recvmsg 
  Representation - 
      HELP INTERNET_ADDRESS 
S 
  select() and XSL$SELECT  --  Select for Read, Write, or Exceptions - 
      HELP select 
  send() and XSL$SEND  --  Write Data With Options - 
      HELP send 
  sendmsg() and XSL$SENDMSG  --  Write Gathered Data With Options And Address 
     - 
      HELP sendmsg 
  sendto() and XSL$SENDTO  --  Write Data With Options And Address - 
      HELP sendto 
  servent - 
      HELP servent 
  servent Structure - 
      HELP servent 
  sethostent() and XSL$SETHOSTENT  --  Set Host Entry - 
      HELP sethostent 
  setnetent() and XSL$SETNETENT  --  Set Network Entry - 
      HELP setnetent 
  setprotoent() and XSL$SETPROTOENT  --  Set Protocol Entry - 
      HELP setprotoent 
  setservent() and XSL$SETSERVENT  --  Set Service Entry - 
      HELP setservent 
  setsockopt() and XSL$SETSOCKOPT  --  Set Socket Option - 
      HELP setsockopt 
  shutdown() and XSL$SHUTDOWN  --  Inhibit Data Transfer - 
      HELP shutdown 
  sockaddr - 
      HELP sockaddr 
  sockaddr Structure - 
      HELP sockaddr 
  sockaddr_in - 
      HELP sockaddr_in 
  sockaddr_in Structure - 
      HELP sockaddr_in 
  socket library - 
      HELP HOST_SOCKET_LIBRARY 
  socket() and XSL$SOCKET  --  Create Socket - 
      HELP socket 
  socket, definition of - 
      HELP HOST_SOCKET_LIBRARY 
  stream socket - 
      HELP connect DESCRIPTION: 
W 
  write() and XSL$WRITE  --  Write Data - 
      HELP write 
  writev() and XSL$WRITEV  --  Write Gathered Data - 
      HELP writev 
X 
  XSL$ACCEPT -- Accept an Incoming Connection Request - 
      HELP accept 
  XSL$ACCEPT_SRVR -- Accept from INETD - 
      HELP accept_srvr 
  XSL$BIND -- Bind Name to Socket - 
      HELP bind 
  XSL$CHAM - 
      HELP XSL$CHAM 
  XSL$CLOSE -- Close Socket - 
      HELP close 
  XSL$CONNECT -- Initiate Connection Request - 
      HELP connect 
  XSL$ENDHOSTENT -- End Host Entry - 
      HELP endhostent 
  XSL$ENDNETENT -- End Network Entry - 
      HELP endnetent 
  XSL$ENDPROTOENT -- End Protocol Entry - 
      HELP endprotoent 
  XSL$ENDSERVENT -- End Service Entry - 
      HELP endservent 
  XSL$FCNTL -- File Control - 
      HELP fcntl 
  XSL$GETHOSTBYADDR -- Look Up Host by Address - 
      HELP gethostbyaddr 
  XSL$GETHOSTBYNAME -- Look Up Host by Name - 
      HELP gethostbyname 
  XSL$GETHOSTENT -- Get Host Entry - 
      HELP gethostent 
  XSL$GETHOSTNAME -- Get Current Host Name - 
      HELP gethostname 
  XSL$GETNETBYADDR -- Look Up Network by Address - 
      HELP getnetbyaddr 
  XSL$GETNETBYNAME -- Look Up Network by Name - 
      HELP getnetbyname 
  XSL$GETNETENT -- Get Network Entry - 
      HELP getnetent 
  XSL$GETPEERNAME -- Get Socket Peer Name - 
      HELP getpeername 
  XSL$GETPROTOBYNAME -- Look Up Protocol by Name - 
      HELP getprotobyname 
  XSL$GETPROTOBYNUMBER -- Look Up Protocol by Number - 
      HELP getprotobynumber 
  XSL$GETPROTOENT -- Get Protocol Entry - 
      HELP getprotoent 
  XSL$GETSERVBYNAME -- Look Up Service by Name - 
      HELP getservbyname 
  XSL$GETSERVBYPORT -- Look Up Service by Port - 
      HELP getservbyport 
  XSL$GETSERVENT -- Get Service Entry - 
      HELP getservent 
  XSL$GETSOCKNAME -- Get Socket Name - 
      HELP getsockname 
  XSL$GETSOCKOPT -- Get Socket Option - 
      HELP getsockopt 
  XSL$HOSTENT - 
      HELP XSL$HOSTENT 
  XSL$HOSTENT Structure - 
      HELP XSL$HOSTENT 
  XSL$HTONL -- Convert Host to Network Long - 
      HELP htonl 
  XSL$HTONS -- Convert Host to Network Short - 
      HELP htons 
  XSL$INET_ADDR -- Convert String to Inet Address - 
      HELP inet_addr 
  XSL$INET_LNAOF -- Get Local Address from Internet - 
      HELP inet_lnaof 
  XSL$INET_MAKEADDR -- Make Internet Address - 
      HELP inet_makeaddr 
  XSL$INET_NETOF -- Get Network from Internet Address - 
      HELP inet_netof 
  XSL$INET_NETWORK -- Convert String to Network - 
      HELP inet_network 
  XSL$INET_NTOA -- Convert Inet Address to String - 
      HELP inet_ntoa 
  XSL$IOCTL -- I/O Control - 
      HELP ioctl 
  XSL$IOVEC - 
      HELP XSL$IOVEC 
  XSL$IOVEC Structure - 
      HELP XSL$IOVEC 
  XSL$LISTEN -- Listen for Incoming Connections - 
      HELP listen 
  XSL$MSGHDR - 
      HELP XSL$MSGHDR 
  XSL$MSGHDR Structure - 
      HELP XSL$MSGHDR 
  XSL$NETENT - 
      HELP XSL$NETENT 
  XSL$NETENT Structure - 
      HELP XSL$NETENT 
  XSL$NTOHL -- Convert Network to Host Long - 
      HELP ntohl 
  XSL$NTOHS -- Convert Network to Host Short - 
      HELP ntohs 
  XSL$PROTOENT - 
      HELP XSL$PROTOENT 
  XSL$PROTOENT Structure - 
      HELP XSL$PROTOENT 
  XSL$READ -- Read Data - 
      HELP read 
  XSL$READV -- Read Scattered Data - 
      HELP readv 
  XSL$RECV -- Read Data With Options - 
      HELP recv 
  XSL$RECVFROM -- Read Data With Options and - 
      HELP recvfrom 
  XSL$RECVMSG -- Read Scattered Data With Options - 
      HELP recvmsg 
  XSL$SELECT -- Select for Read, Write, or - 
      HELP select 
  XSL$SEND -- Write Data With Options - 
      HELP send 
  XSL$SENDMSG -- Write Gathered Data With Options - 
      HELP sendmsg 
  XSL$SENDTO -- Write Data With Options And - 
      HELP sendto 
  XSL$SERVENT - 
      HELP XSL$SERVENT 
  XSL$SERVENT Structure - 
      HELP XSL$SERVENT 
  XSL$SETHOSTENT -- Set Host Entry - 
      HELP sethostent 
  XSL$SETNETENT -- Set Network Entry - 
      HELP setnetent 
  XSL$SETPROTOENT -- Set Protocol Entry - 
      HELP setprotoent 
  XSL$SETSERVENT -- Set Service Entry - 
      HELP setservent 
  XSL$SETSOCKOPT -- Set Socket Option - 
      HELP setsockopt 
  XSL$SHUTDOWN -- Inhibit Data Transfer - 
      HELP shutdown 
  XSL$SOCKADDR - 
      HELP XSL$SOCKADDR 
  XSL$SOCKADDR Structure - 
      HELP XSL$SOCKADDR 
  XSL$SOCKADDR_IN - 
      HELP XSL$SOCKADDR_IN 
  XSL$SOCKADDR_IN Structure - 
      HELP XSL$SOCKADDR_IN 
  XSL$SOCKET -- Create Socket - 
      HELP socket 
  XSL$SOCKINIT -- Initialize Socket Library - 
      HELP XSL$SOCKINIT 
  XSL$WRITE -- Write Data - 
      HELP write 
  XSL$WRITEV -- Write Gathered Data - 
      HELP writev 
  XSL_CHAM - 
      HELP XSL$CHAM 
  xsl_sockinit - 
      HELP xsl_sockinit 
      HELP XSL_SOCKINIT 
  xsl_sockinit Structure - 
      HELP xsl_sockinit 
      HELP XSL_SOCKINIT 
00001
00002
00003
00004
00005
00006
00007
00008
00009
00010
00011
00012
00013
00014
00015
00016
HELP_INDEX

All of the include files necessary to make use of the Host Socket Library are 
located in the :LIBRARY account.  The include files are listed below. 
XSL_PERR_C 
        PL6 include file containing EQUs for error conditions. 
XSL_SOCKET_E 
        PL6 include file containing EQUs for general usage of the socket 
        library.  PL6 equivalents of the various C defines in the xsl_? 
        include files are found here. 
XSL_SOCKET_M 
        PL6 include file containing MACROs for general usage of the socket 
        library.  PL6 equivalents of the various C structures in the xsl_? 
        include files are found here. 
xsl_errno:h 
        C include file containing defines for error conditions. 
xsl_in:h 
        C include file containing defines for Internet addressing. 
xsl_netdb:h 
        C include file containing defines for the hosts, networks, protocols, 
        and services file manipulation functions. 
xsl_select:h 
        C include file containing defines for the select() function. 
xsl_socket:h 
        C include file containing defines for general usage of the socket 
        library. 
The term "Internet address" is used throughout the discussion of Host Socket 
Library services.  On 32-bit systems, an Internet address consists of four 
consecutive bytes of 8 bits each.  On CP-6 systems, an Internet address 
consists of four consecutive bytes ignoring the high-order bit of each byte. 
An Internet address is commonly represented in text as a "character string in 
dot notation", i.e., each of four bytes as a decimal number, separated by 
dots.  For example, 128.35.0.0 and 192.9.200.2 are Internet addresses. 
An Internet address consists of two parts, sometimes called "netid" and 
"hostid".  The netid identifies the network; the hostid identifies the host on 
that network.  The netid field can be 1, 2, or 3 bytes long in a Class A, B, 
or C address, respectively, leaving 3, 2 or 1 bytes for the hostid.  The 
lengths of the netid and the hostid are determined by inspecting the 
high-order bits of the Internet address. 
The CP-6 Internet addresses shown below illustrate the settings of the 
high-order bits for addresses with a 1, 2, or 3 byte netid.  For each bit 
position shown, the letter n denotes a netid bit, the letter h denotes a 
hostid bit, and the character ? denotes an unused (don't care) bit. 
Class A address: 
#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-# 
|? 0 n n n n n n n ? h h h h h h h h ? h h h h h h h h ? h h h h h h h h| 
#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-# 
Internet addresses 0.0.0.0 through 127.255.255.255 allow 126 networks with up 
to 16777214 hosts each. 
Class B address: 
#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-# 
|? 1 0 n n n n n n ? n n n n n n n n ? h h h h h h h h ? h h h h h h h h| 
#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-# 
Internet addresses 128.0.0.0 through 191.255.255.255 allow 16382 networks with 
up to 65534 hosts each. 
Class C address: 
#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-# 
|? 1 1 0 n n n n n ? n n n n n n n n ? n n n n n n n n ? h h h h h h h h| 
#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-#-+-+-+-+-+-+-+-+-# 
Internet addresses 192.0.0.0 through 223.255.255.255 allow 2097150 networks 
with up to 254 hosts each. 
In practice, Class A and Class B networks are commonly divided up into 
subnets, using a "subnet mask" which is ANDed with the Internet address to 
specify which bits define the netid. 
Note:  A netid or hostid value of all binary zeros or all binary ones is not 
permitted.  (All binary zeros is reserved to mean the local network or the 
local host; all binary ones is reserved to mean broadcast to all networks or 
broadcast to all hosts.) 
The CP-6 Socket Library exists as an unshared LEMUR library in the file 
:ETC_SOCKET.:SYS.  The library contains both C and PL6 interfaces.  Routines 
from the library are included in an application by linking the application 
with the option UNSAT=:ETC_SOCKET.:SYS. 
The services available in the library are listed in the following table. 
CATEGORY                    SERVICE 
Create and Name Sockets     socket() and XSL$SOCKET 
                            bind() and XSL$BIND 
Initiating Connections      listen() and XSL$LISTEN 
                            accept() and XSL$ACCEPT 
                            accept_srvr() and XSL$ACCEPT_SRVR 
                            connect() and XSL$CONNECT 
Transferring Data           send() and XSL$SEND 
                            recv() and XSL$RECV 
                            sendto() and XSL$SENDTO 
                            recvfrom() and XSL$RECVFROM 
                            sendmsg() and XSL$SENDMSG 
                            recvmsg() and XSL$RECVMSG 
                            write() and XSL$WRITE 
                            read() and XSL$READ 
                            writev() and XSL$WRITEV 
                            readv() and XSL$READV 
I/O Multiplexing            select() and XSL$SELECT 
Terminating Connections     shutdown() and XSL$SHUTDOWN 
                            close() and XSL$CLOSE 
Host, Socket, User Info     gethostname() and XSL$GETHOSTNAME 
                            getpeername() and XSL$GETPEERNAME 
                            getsockname() and XSL$GETSOCKNAME 
                            getsockopt() and XSL$GETSOCKOPT 
                            setsockopt() and XSL$SETSOCKOPT 
                            fcntl() and XSL$FCNTL 
                            ioctl() and XSL$IOCTL 
                            XSL$SOCKINIT 
                            XSL$CHAM 
Data Conversion             htonl() and XSL$HTONL 
                            htons() and XSL$HTONS 
                            ntohl() and XSL$NTOHL 
                            ntohs() and XSL$NTOHS 
Data Manipulation           bcmp() 
                            bcopy() 
                            bzero() 
Internet Address Usage      inet_addr() and XSL$INET_ADDR 
                            inet_lnaof() and XSL$INET_LNAOF 
                            inet_makeaddr() and XSL$INET_MAKEADDR 
                            inet_netof() and XSL$INET_NETOF 
                            inet_network() and XSL$INET_NETWORK 
                            inet_ntoa() and XSL$INET_NTOA 
"hosts" File Usage          gethostbyaddr() and XSL$GETHOSTBYADDR 
                            gethostbyname() and XSL$GETHOSTBYNAME 
                            gethostent() and XSL$GETHOSTENT 
                            sethostent() and XSL$SETHOSTENT 
                            endhostent() and XSL$ENDHOSTENT 
"networks" File Usage       getnetbyaddr() and XSL$GETNETBYADDR 
                            getnetbyname() and XSL$GETNETBYNAME 
                            getnetent() and XSL$GETNETENT 
                            setnetent() and XSL$SETNETENT 
                            endnetent() and XSL$ENDNETENT 
"protocols" File Usage      getprotobyname() and XSL$GETPROTOBYNAME 
                            getprotobynumber() and XSL$GETPROTOBYNUMBER 
                            getprotoent() and XSL$GETPROTOENT 
                            setprotoent() and XSL$SETPROTOENT 
                            endprotoent() and XSL$ENDPROTOENT 
"services" File Usage       getservbyname() and XSL$GETSERVBYNAME 
                            getservbyport() and XSL$GETSERVBYPORT 
                            getservent() and XSL$GETSERVENT 
                            setservent() and XSL$SETSERVENT 
                            endservent() and XSL$ENDSERVENT 
accept
accept_srvr
bind
DESCRIPTION: The XSL$CHAM library routine is an adaptation of the code in CP-6 
LOGIN that provides user verification and environment establishment.  It is 
useful to programs like communications servers that need to appear to be 
running on behalf of a different user authorization than that with which they 
were started.  MEMORY resources are not affected by this service.  It is 
called with two parameters, as follows: 
CALL SET_USER_ID (or XSL$CHAM) (XSL_CHAM, buffer) ALTRET(location); 
where "XSL_CHAM" is an FPT described by the XSL_CHAM macro, and "buffer" is a 
buffer large enough to contain a :USERS record (one page is recommended).  The 
ALTRETURN is taken unless the indicated user id is authorized to use the 
system. 
The parameters for XSL_CHAM except NAME and STCLASS are described below: 
ACCN = VALUE-CHAR(8) specifies the account portion of the desired user id. 
BADPW = {YES|NO} specifies that after a missing password response 
     (RESPONSE=1), no password will be supplied.  XSL$CHAM should log the 
     logon failure if required and possibly update :USERS in the failed logon 
     count. 
CHECKPW = {YES|NO} specifies whether password checking should be done by 
     XSL$CHAM.  This is intended to be used in cases where the password in not 
     provided by the application-level protocol, as is the case with some UNIX 
     network applications.  The default is YES. 
DO_ACCOUNTING = {YES|NO} specifies that accounting for the current environment 
     is to be done before reinitializing the accounting parameters in B$JIT 
     from the :USERS record for the new user id.  This option is not currently 
     implemented. 
FULL_STUFF = {YES|NO} specifies whether *S is to be updated with default LIMIT 
     information.  Since this is impossible to do from a user program, it is 
     not currently implemented.  Perhaps this option might have other uses. 
L = VALUE-DEC(1-20) must be set at runtime to eight plus the number of 
     significant characters in USER. 
PASS = VALUE-CHAR(8) specifies the password portion of the desired user ID. 
     This parameter is REDEFed as PSWB, an array of nine BIT-8 items which 
     should be cleared to zero to indicate that no password is specified. 
RESPONSE = VALUE-DEC(0-2) indicates the level of success of the call to 
     XSL$CHAM.  Zero indicates full success and the call returns normally. 
     Otherwise, the call altreturns and makes no change to the environment. 
     One indicates that an attempt to access a passworded authorization was 
     made without specifying one.  Two indicates failure, either because the 
     user ID was not authorized or because XSL$CHAM couldn't do its job.  It 
     needs read access to :HLP and :USERS in :SYS, and the rununit in which it 
     is running must have JIT privilege. 
SCRAMBLED = {YES|NO} specifies whether the PASS parameter is already 
     scrambled.  It is set by XSL$CHAM after scrambling FPT.PSWB if it wasn't 
     set and FPT.PSWB is nonzero. 
STUFF_JIT = {YES|NO} specifies whether the environment for the new user id is 
     to be set up in B$JIT from the :USERS record.  The default is YES.  All 
     JIT items currently set up by CP-6 LOGON are also set up by XSL$CHAM, 
     using the :USERS information for the mode of the running running program, 
     except CL resources and CPROC.  Note that the mode used is likely to be 
     ghost.  The user must be a time-sharing one, but access for the current 
     mode is not required. 
USER = VALUE-CHAR(12) specifies the username portion of the desired user id. 
                                   XSL_CHAM 
   .0-1-0 ACCN=' ' 
   .5-1-4 BADPW='0'B 
            NO='0'B 
            YES='1'B 
   .5-1-5 CHECKPW='1'B 
            NO='0'B 
            YES='1'B 
   .5-1-0 DO_ACCOUNTING='0'B 
            NO='0'B 
            YES='1'B 
   .5-1-3 FULL_STUFF='0'B 
            NO='0'B 
            YES='1'B 
    ..... NAME=XSL_CHAM 
   .6-0-0 PASS=' ' 
   .5-1-2 SCRAMBLED='0'B 
            NO='0'B 
            YES='1'B 
    ..... STCLASS=STATIC 
   .5-1-1 STUFF_JIT='1'B 
            NO='0'B 
            YES='1'B 
   .2-1-0 USER=' ' 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 NAME STCLASS ALIGNED, 
   .0 |uuu|   |   |   |   2 L              UBIN BYTE CALIGNED INIT(0), 
   .0 |   |ccc|ccc|ccc|   2 ACCN           CHAR(8) INIT(ACCN), 
   .1 |ccc|ccc|ccc|ccc| 
   .2 |ccc|   |   |   | 
   .2 |   |ccc|ccc|ccc|   2 USER           CHAR(12) INIT(USER), 
   .3 |ccc|ccc|ccc|ccc| 
   .4 |ccc|ccc|ccc|ccc| 
   .5 |ccc|   |   |   | 
   .5 |   |   |   |   |   2 FLAGS, 
   .5 |   |   |   |   |     3 DO_ACCOUNTING 
   .5 |   |4  |   |   |                    BIT(1) INIT(DO_ACCOUNTING), 
   .5 |   |2  |   |   |     3 STUFF_JIT    BIT(1) INIT(STUFF_JIT), 
   .5 |   |1  |   |   |     3 SCRAMBLED    BIT(1) INIT(SCRAMBLED), 
   .5 |   | 4 |   |   |     3 FULL_STUFF   BIT(1) INIT(FULL_STUFF), 
   .5 |   | 2 |   |   |     3 BADPW        BIT(1) INIT(BADPW), 
   .5 |   | 1 |   |   |     3 CHECKPW      BIT(1) INIT(CHECKPW), 
   .5 |   |  7|   |   |     3 *            BIT(3) INIT('0'B), 
   .5 |   |   |uuu|uuu|   2 RESPONSE       UBIN HALF CALIGNED INIT(0), 
   .6 |ccc|ccc|ccc|ccc|   2 PASS           CHAR(8) INIT(PASS), 
   .7 |ccc|ccc|ccc|ccc| 
   .6 |   |   |   |   |   2 PSWB(0:8) REDEF PASS 
   .6 |776|   |   |   |                    BIT(8); 
      Z   Z   Z   Z   Z 
      +---+---+---+---+ 
        0   1   2   3    .10-0-0 total length 
close
connect
endhostent
endnetent
endprotoent
endservent
fcntl
gethostbyaddr
gethostbyname
gethostent
gethostname
getnetbyaddr
getnetbyname
getnetent
getpeername
getprotobyname
getprotobynumber
getprotoent
getservbyname
getservbyport
getservent
getsockname
getsockopt
The XSL$HOSTENT structure is a template for the information returned by the 
Socket Library functions that deal with the etc:hosts.:SYS file. 
H_ADDRTYPE - INTEGER 
     Specifies the address family of the address pointed at by the address 
     pointer.  It is always %XSL_AF_INET. 
H_ADDR_LIST$ - PTR 
     Points at a buffer within the Socket Library containing the Internet 
     address(es) of the host.  Each address is a 32-bit integer unpacked into 
     the lower eight bits of four successive bytes.  The buffer is terminated 
     by a NULL pointer. 
H_ALIASES$ - PTR 
     Points at an array of pointers to character strings.  Each character 
     string contains an alias of the host name, and is terminated by a NUL 
     byte.  The array of pointers is terminated by a NULL pointer. 
H_LENGTH - INTEGER 
     Specifies the length of the address pointed at by the address pointer. 
     It is always 4. 
H_NAME$ - PTR 
     Points at a character string containing the host name.  The string is 
     terminated by a NUL byte. 
                                 XSL$HOSTENT 
    ..... FPTN=XSL$HOSTENT 
    ..... LAST=";" 
    ..... LVL=1 
    ..... STCLASS=BASED 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 FPTN STCLASS ALIGNED, 
   .0 |ppp|ppp|ppp|ppp|   2 H_NAME$        PTR INIT(ADDR(NIL)), 
   .1 |ppp|ppp|ppp|ppp|   2 H_ALIASES$     PTR INIT(ADDR(NIL)), 
   .2 |sss|sss|sss|sss|   2 H_ADDRTYPE     SBIN INIT(0), 
   .3 |sss|sss|sss|sss|   2 H_LENGTH       SBIN INIT(0), 
   .4 |ppp|ppp|ppp|ppp|   2 H_ADDR_LIST$   PTR INIT(ADDR(NIL)); 
      +---+---+---+---+ 
        0   1   2   3     .5-0-0 total length 
htonl
htons
inet_addr
inet_lnaof
inet_makeaddr
inet_netof
inet_network
inet_ntoa
ioctl
The XSL$IOVEC structure frames an area of memory to be used as an I/O buffer 
in the XSL$READV, XSL$WRITEV, XSL$RECVMSG, and XSL$SENDMSG procedures. 
IOV_BASE$ - PTR 
     Points at a buffer in application memory to be used for I/O. 
IOV_LEN - SBIN 
     Specifies how large the I/O buffer is, in bytes. 
                                  XSL$IOVEC 
    ..... FPTN=XSL$IOVEC 
    ..... LAST=";" 
    ..... LVL=1 
    ..... STCLASS=BASED 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 FPTN STCLASS ALIGNED, 
   .0 |ppp|ppp|ppp|ppp|   2 IOV_BASE$      PTR INIT(ADDR(NIL)), 
   .1 |sss|sss|sss|sss|   2 IOV_LEN        SBIN INIT(0) ALIGNED; 
      +---+---+---+---+ 
        0   1   2   3     .2-0-0 total length 
listen
The XSL$MSGHDR structure collects together various parameters needed by the 
XSL$SENDMSG and XSL$RECVMSG procedures. 
MSG_ACCRIGHTS$ - PTR 
     This item is not currently supported and must be coded as ADDR( NIL). 
MSG_ACCRIGHTSLEN - SBIN 
     This item is not currently supported and must be coded as 0. 
MSG_IOV$ - PTR 
     Points at an array of XSL$IOVEC structures framing one or more areas of 
     application memory to use for I/O buffers. 
MSG_IOVLEN - SBIN 
     Specifies how many XSL$IOVEC structures are valid at the memory address 
     specified by MSG_IOV$. 
MSG_NAME$ - PTR 
     Points at a buffer containing a network address.  For XSL$SENDMSG, the 
     buffer contains the address of the host to which the message is to be 
     sent.  For XSL$RECVMSG, the buffer contains the address of the host from 
     which the message was received. 
MSG_NAMELEN - SBIN 
     Specifies how large the MSG_NAME$ buffer is, in bytes.  It must be 
     specified for both XSL$SENDMSG and XSL$RECVMSG.  For the latter, it will 
     be modified to contain the length of the address of the host from which 
     the message was received. 
                                  XSL$MSGHDR 
    ..... FPTN=XSL$MSGHDR 
    ..... LAST=";" 
    ..... LVL=1 
    ..... STCLASS=BASED 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 FPTN STCLASS ALIGNED, 
   .0 |ppp|ppp|ppp|ppp|   2 MSG_NAME$      PTR INIT(ADDR(NIL)), 
   .1 |sss|sss|sss|sss|   2 MSG_NAMELEN    SBIN INIT(0) ALIGNED, 
   .2 |ppp|ppp|ppp|ppp|   2 MSG_IOV$       PTR INIT(ADDR(NIL)), 
   .3 |sss|sss|sss|sss|   2 MSG_IOVLEN     SBIN INIT(0) ALIGNED, 
   .4 |ppp|ppp|ppp|ppp|   2 MSG_ACCRIGHTS$ PTR INIT(ADDR(NIL)), 
   .5 |   |   |   |   |   2 MSG_ACCRIGHTSLEN 
   .5 |sss|sss|sss|sss|                    SBIN INIT(0) ALIGNED; 
      +---+---+---+---+ 
        0   1   2   3     .6-0-0 total length 
The XSL$NETENT structures is a template for the information returned by the 
Socket Library functions that deal with the etc:networks.:SYS file. 
N_ADDRTYPE - INTEGER 
     Specifies the address family of the addresses used on this network.  It 
     is always %XSL_AF_INET. 
N_ALIASES$ - PTR 
     Points at an array of pointers to character strings.  Each character 
     string contains an alias of the network name, and is terminated by a NUL 
     byte.  The array of pointers is terminated by a NULL pointer. 
N_NAME$ - PTR 
     Points at a character string containing the network name.  The string is 
     terminated by a NUL byte. 
N_NET - INTEGER 
     Specifies the network number for this network. 
                                  XSL$NETENT 
    ..... FPTN=XSL$NETENT 
    ..... LAST=";" 
    ..... LVL=1 
    ..... STCLASS=BASED 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 FPTN STCLASS ALIGNED, 
   .0 |ppp|ppp|ppp|ppp|   2 N_NAME$        PTR INIT(ADDR(NIL)), 
   .1 |ppp|ppp|ppp|ppp|   2 N_ALIASES$     PTR INIT(ADDR(NIL)), 
   .2 |sss|sss|sss|sss|   2 N_ADDRTYPE     SBIN INIT(0), 
   .3 |sss|sss|sss|sss|   2 N_NET          SBIN INIT(0); 
      +---+---+---+---+ 
        0   1   2   3     .4-0-0 total length 
ntohl
ntohs
The XSL$PROTOENT structure is a template for the information returned by the 
Socket Library functions that deal with the etc:protocols.:SYS file. 
P_ALIASES$ - PTR 
     Points at an array of pointers to character strings.  Each character 
     string contains an alias of the protocol name, and is terminated by a NUL 
     byte.  The array of pointers is terminated by a NULL pointer. 
P_NAME$ - PTR 
     Points at a character string containing the protocol name.  The string is 
     terminated by a NUL byte. 
P_PROTO - INTEGER 
     Specifies the protocol number for this protocol. 
                                 XSL$PROTOENT 
    ..... FPTN=XSL$PROTOENT 
    ..... LAST=";" 
    ..... LVL=1 
    ..... STCLASS=BASED 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 FPTN STCLASS ALIGNED, 
   .0 |ppp|ppp|ppp|ppp|   2 P_NAME$        PTR INIT(ADDR(NIL)), 
   .1 |ppp|ppp|ppp|ppp|   2 P_ALIASES$     PTR INIT(ADDR(NIL)), 
   .2 |sss|sss|sss|sss|   2 P_PROTO        SBIN INIT(0); 
      +---+---+---+---+ 
        0   1   2   3     .3-0-0 total length 
read
readv
recv
recvfrom
recvmsg
select
send
sendmsg
sendto
The XSL$SERVENT structure is a template for the information returned by the 
Socket Library functions that deal with the etc:services.:SYS file. 
S_ALIASES$ - PTR 
     Points at an array of pointers to character strings.  Each character 
     string contains an alias of the service name, and is terminated by a NUL 
     byte.  The array of pointers is terminated by a NULL pointer. 
S_NAME$ - PTR 
     Points at a character string containing the service name.  The string is 
     terminated by a NUL byte. 
S_PORT - INTEGER 
     Specifies the port at which this service is accessed. 
S_PROTO$ - PTR 
     Points at a character string containing the name of the protocol used to 
     access this service.  The character string is terminated by a NUL byte. 
                                 XSL$SERVENT 
    ..... FPTN=XSL$SERVENT 
    ..... LAST=";" 
    ..... LVL=1 
    ..... STCLASS=BASED 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 FPTN STCLASS ALIGNED, 
   .0 |ppp|ppp|ppp|ppp|   2 S_NAME$        PTR INIT(ADDR(NIL)), 
   .1 |ppp|ppp|ppp|ppp|   2 S_ALIASES$     PTR INIT(ADDR(NIL)), 
   .2 |sss|sss|sss|sss|   2 S_PORT         SBIN INIT(0), 
   .3 |ppp|ppp|ppp|ppp|   2 S_PROTO$       PTR INIT(ADDR(NIL)); 
      +---+---+---+---+ 
        0   1   2   3     .4-0-0 total length 
sethostent
setnetent
setprotoent
setservent
setsockopt
shutdown
The XSL$SOCKADDR structure is a generic address template for Socket Library 
applications.  The two parts of the generic address are the family and data. 
The specific value in the family part determines how to interpret the data 
part.  One family in particular (AF_INET) is used so widely that a separate 
structure is defined for it:  XSL$SOCKADDR_IN. 
SA_DATA - BYTE ARRAY 
     Specifies the individual bytes of an address.  The meaning of the bytes 
     is determined by the 'family' item of the structure.  Up to 16 bytes can 
     be specified. 
SA_FAMILY - INTEGER 
     Specifies the address family that this address belongs to.  The value 
     determines how the 'data' item is to be interpreted.  Equates for the 
     possible values can be found in XSL_SOCKET_E for the PL6 source and 
     <xsl_socket.h> for the C source. 
                                 XSL$SOCKADDR 
    ..... FPTN=XSL$SOCKADDR 
    ..... LAST=";" 
    ..... LVL=1 
    ..... STCLASS=BASED 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 FPTN STCLASS ALIGNED, 
   .0 |uuu|uuu|uuu|uuu|   2 SA_FAMILY      UBIN INIT(0), 
   .1 |uuu|   |   |   |   2 SA_DATA(0:15)  UBIN BYTE INIT(0*0) CALIGNED; 
      Z   Z   Z   Z   Z 
      +---+---+---+---+ 
        0   1   2   3     .5-0-0 total length 
The XSL$SOCKADDR_IN structure is an instance of the XSL$SOCKADDR structure 
useful for addresses in the AF_INET (Internet) family.  This family of 
addresses is used so frequently that it deserves its own address structure. 
SA_FAMILY - INTEGER 
     Specifies the address family that this address belongs to.  Addresses in 
     the Internet family specify the value AF_INET or %XSL_AF_INET in C or PL6 
     source, respectively.  Equates for the possible values can be found in 
     XSL_SOCKET_E.  <xsl_socket.h> or XSL_SOCKET_E for C or PL6 source 
     respectively. 
S_ADDR - INTEGER 
     Specifies the Internet address.  It is a 32-bit integer unpacked into the 
     lower eight bits of four successive bytes.  For more information about 
     Internet addresses, please refer to the topic INTERNET_ADDRESS. 
     The in_addr structure is used to store the IP address in network byte 
     order. 
         struct in_addr { 
         unsigned long s_addr; 
         }; 
S_PORT - INTEGER 
     Specifies the port within a specific host through which some application 
     can be accessed.  Equates for the so-called 'well-known' ports can be 
     found in etc:services.:SYS.  User applications can make use of any 
     non-conflicting port number; port numbers below 1024 are reserved for 
     system applications. 
                               XSL$SOCKADDR_IN 
    ..... FPTN=XSL$SOCKADDR_IN 
    ..... LAST=";" 
    ..... LVL=1 
    ..... STCLASS=BASED 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 FPTN STCLASS ALIGNED, 
   .0 |uuu|uuu|uuu|uuu|   2 SA_FAMILY      UBIN INIT(0), 
   .1 |uuu|uuu|uuu|uuu|   2 S_PORT         UBIN INIT(0), 
   .2 |uuu|uuu|uuu|uuu|   2 S_ADDR         UBIN INIT(0), 
   .3 |uuu|   |   |   |   2 *(0:5)         UBIN BYTE INIT(0*0) CALIGNED; 
      Z   Z   Z   Z   Z 
   .4 |   |   |...|...| 
      +---+---+---+---+ 
        0   1   2   3     .5-0-0 total length 
socket
Purpose: 
    Initializes the Socket Library using given parameters. 
C Usage: 
    XSL$SOCKINIT( &parms ); 
PL6 Usage: 
    CALL XSL$SOCKINIT( parms ); 
Parameter: 
    parms       XSL_SOCKINIT parameter structure 
Description: 
The XSL$SOCKINIT procedure initializes the Socket Library using the parameters 
passed in an XSL_SOCKINIT structure.  An application may wish to invoke 
XSL$SOCKINIT to specify the use or non-use of NoWait I/O, to reserve memory 
space for I/O buffers, or to set up a linkage to handle the arrival of 
application-specific events. 
The parms parameter contains information used in Socket Library 
initialization.  In C source, it is an xsl_sockinit structure found in 
<xsl_socket.h>.  In PL6 source, it is an XSL_SOCKINIT structure found in 
XSL_SOCKET_M. 
The default values for the use of XSL_SOCKINIT currently are MAXSOCK=2, 
NWSOCKS=-1, BUFSIZE=512, MEM=NIL, EVNT=NIL, MAXRDS=2, MAXBUF=0. 
The defaults provided by XSL_SOCKINIT are adequate for simple applications. 
For applications with special requirements, you will want to choose more 
appropriate values, such as larger BUFSIZE or MAXSOCK. 
00001
00004
00003
00002
write
writev
The XSL_SOCKINIT structure collects together various parameters that are used 
to initialize the Socket Library.  If no special action is taken by the 
application, defaults are used for initialization at the first use of socket() 
or XSL$SOCKET.  To override the defaults, the application calls XSL$SOCKINIT, 
passing an XSL_SOCKINIT structure with new parameters.  To have any effect, 
the call to XSL$SOCKINIT must precede any call to socket() or XSL$SOCKET. 
BUFSIZE - UBIN 
     Specifies the number of bytes of memory to reserve for each NoWait I/O 
     buffer.  Valid values are 1 to 4096.  The larger the buffer size, the 
     better.  Larger than 4096 is pointless because that is the limiting size 
     for data transfers between FEP and host.  I/O buffers are allocated at 
     Socket Library initialization and are shared among all NoWait sockets, 
     subject to each socket's current MAXRDS and MAXBUF values. 
EVNT$ - EPTR 
     Specifies the address of a PL6 PROC to handle non-Socket Library events 
     received by the Socket Library.  The named procedure should be coded as a 
     normal PROC (not PROC ASYNC) that receives one parameter, a B$EXCFR 
     structure. 
MAXBUF - UBIN HALF 
     Specifies the number of additional buffers to allocate to each NoWait 
     socket.  Valid values are 0 to 262143.  If nonzero, the value specifies 
     how many I/O buffers, above those in use by pending NoWait reads, should 
     be reserved for each socket.  This parameter is inherited by each socket 
     on creation.  A socket's copy of MAXBUF can be modified by using 
     XSL$SETSOCKOPT, specifying option XSL_SO_NWBUFFS.  (C programmers can use 
     setsockopt() with option SO_NWBUFFS.) 
     MAXBUF buffers may be useful in situations where the application needs to 
     be responsive to the network but cannot process incoming data as it 
     arrives.  It provides more buffering than possible with MAXRDS alone. 
MAXRDS - UBIN HALF 
     Specifies the maximum number of NoWait reads allowed on each socket. 
     Valid values are 0 to 3.  0 specifies that NoWait I/O is not to be used. 
     If nonzero, the value specifies how many I/O buffers to reserve for 
     pending NoWait reads, as well as how many simultaneous NoWait reads to 
     issue when the application requests data from the network.  This 
     parameter is inherited by each socket on creation.  A socket's copy of 
     MAXRDS can be modified by using XSL$SETSOCKOPT specifying option 
     XSL_SO_NWREADS.  (C programmers can use setsockopt() with option 
     SO_NWREADS.) 
     Converting a socket from NoWait-capable to non-NoWait-capable is possible 
     by setting the socket's MAXRDS value to zero.  The inverse operation is 
     not possible because the value of MAXRDS is used when the socket DCB is 
     opened to determine whether B$COMIO events should be delivered to the 
     library for that socket.  However, it is always possible to adjust a 
     socket's MAXRDS value from one nonzero value to another nonzero value. 
MAXSOCK - UBIN 
     Specifies the maximum number of sockets that will be in use at any one 
     time.  Valid values are 1 to 36.  The CP-6 LINK option DCBSLOTS may need 
     to be used to reserve space for DCBs associated with the sockets.  One 
     DCB is required for each socket in use. 
MEM$ - PTR 
     Points at an area of application-managed memory that the Socket Library 
     will use for its socket context.  If not specified, the library will 
     allocate space out of the next available data segment.  The number of 
     words of memory space required can be computed as shown below in 
     pseudo-code. 
     TOTAL = 68;  // for segment head and event log 
     TOTAL = TOTAL + 21*MAXSOCK;  // add pointer array and sockets 
     TOTAL = TOTAL + 1+B$ROSEG.NUMDCBS;  // add DCBNUM-to-socket map 
     IF NWSOCKS ~= 0 THEN DO; 
        // add NoWait I/O buffers as requested 
        IF NWSOCKS = -1 THEN 
            TMP = MAXSOCK; 
        ELSE 
            TMP = NWSOCKS; 
        TOTAL = TOTAL + (10+(BUFSIZE+3)/4) * (1+TMP*(MAXRDS+MAXBUF)); 
        END; 
NWSOCKS - SBIN 
     Specifies the maximum number of sockets capable of NoWait I/O.  Valid 
     values are -1 to MAXSOCK.  -1 specifies that all sockets are capable of 
     NoWait I/O.  0 specifies that none are capable.  The CP-6 LINK option TCB 
     may need to be used to reserve space for events arriving as the result of 
     NoWait I/O.  One TCB frame is required for each NoWait event on arrival, 
     so the worst case requirement is NWSOCKS*MAXRDS. 
                                 XSL_SOCKINIT 
   .2-0-0 BUFSIZE=512 
   .4-0-0 EVNT=NIL 
    ..... FPTN=XSL_SOCKINIT 
    ..... LAST=";" 
    ..... LVL=1 
   .5-2-0 MAXBUF=0 
   .5-0-0 MAXRDS=2 
   .0-0-0 MAXSOCK=2 
   .3-0-0 MEM=NIL 
   .1-0-0 NWSOCKS=-1 
    ..... STCLASS=STATIC 
        0   1   2   3 
      +---+---+---+---+ DCL 
   .0 |   |   |   |   | 1 FPTN STCLASS ALIGNED, 
   .0 |uuu|uuu|uuu|uuu|   2 MAXSOCK        UBIN ALIGNED INIT(MAXSOCK), 
   .1 |sss|sss|sss|sss|   2 NWSOCKS        SBIN ALIGNED INIT(NWSOCKS), 
   .2 |uuu|uuu|uuu|uuu|   2 BUFSIZE        UBIN INIT(BUFSIZE), 
   .3 |ppp|ppp|ppp|ppp|   2 MEM$           PTR ALIGNED INIT(ADDR(MEM)), 
   .4 |eee|eee|eee|eee|   2 EVNT$          EPTR INIT(ENTADDR(EVNT)), 
   .5 |   |   |   |   |   2 MAXRDS         UBIN HALF INIT(MAXRDS) 
   .5 |uuu|uuu|   |   |                    HALIGNED, 
   .5 |   |   |   |   |   2 MAXBUF         UBIN HALF INIT(MAXBUF) 
   .5 |   |   |uuu|uuu|                    HALIGNED; 
      +---+---+---+---+ 
        0   1   2   3     .6-0-0 total length 
Purpose: 
    Accepts an incoming connection request from another socket elsewhere in 
    the network. 
C Usage: 
    status = accept( s, &name, &namelen ); 
PL6 Usage: 
    CALL XSL$ACCEPT( status, s, name, namelen ); 
Parameters: 
    s           integer socket descriptor 
    name        sockaddr structure 
    namelen     integer size of name in characters 
Results: 
    status      integer new socket descriptor or error code 
    name        sockaddr structure 
    namelen     integer number of significant characters in name 
Description: 
The accept() function takes the first item on the queue of pending connection 
requests, allocates a new socket for it with the same attributes as socket s, 
and returns the new descriptor. 
The s parameter specifies the descriptor of the socket on which to accept. 
The name parameter specifies an application-defined buffer to receive the 
address of the socket that initiated the connection. 
The namelen parameter specifies how large the name buffer is, expressed as the 
number of characters it can hold. 
If the accept() function is successful, the status result contains the 
descriptor of the new socket allocated for the new connection.  The descriptor 
is a small non-negative integer, equivalent to the DCBNUM of the DCB allocated 
for the new socket.  The name and namelen parameters are modified to identify 
the initiator of the connection request. 
If the accept() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$ACCEPT procedure additionally 
ALTRETURNs if it is unsuccessful; it is otherwise identical to the accept() 
function. 
If no connection requests are pending when accept() is invoked, the action 
taken depends on the socket mode.  The mode of a socket is defined to be 
either "blocking" or "nonblocking".  If the socket is blocking (which is the 
default mode) the application is blocked (i.e., suspended) until an incoming 
connection request is received from the network.  If the socket is 
nonblocking, the condition is treated as an EWOULDBLOCK error. 
The mode of a socket can be changed with either fcntl() or ioctl(). 
The accept() function applies only to "stream" sockets. 
Errors: 
Following are the possible error conditions reported when the accept() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is inappropriate to identify a socket. 
EINVAL                  E$INVAL 
The listen() function has not been invoked for this socket. 
EMFILE                  E$MFILE 
M$GETDCB failed.  Unable to allocate DCB for new socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
EOPNOTSUPP              E$OPNOTSUPP 
This is not a "stream" socket. 
EWOULDBLOCK             E$WOULDBLOCK 
No connections are pending for this nonblocking socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Accepts from the INETD Ghost an incoming connection request from another 
    socket elsewhere in the network. 
C Usage: 
    status = accept_srvr( name, &namelen ); 
PL6 Usage: 
    CALL XSL$ACCEPT_SRVR( status, name, namelen ); 
Parameters: 
    name        sockaddr structure 
    namelen     integer size of name in characters 
Results: 
    status      integer new socket descriptor or error code 
    name        sockaddr structure 
    namelen     integer number of significant characters in name 
Description: 
The accept_srvr() function performs the "second half" of incoming connection 
setup when the INETD Ghost has performed the "first half" for the application. 
On systems such as UNIX where INETD can pass its environment to subprocesses, 
this function is not needed.  The subprocess inherits socket descriptors from 
INETD. 
On CP-6 systems, however, subprocesses are totally independent of INETD. 
INETD takes care of socket(), bind(), listen(), and the initial work of 
accept().  When an incoming connection request arrives, INETD starts up the 
application as a Ghost job, and the application issues accept_srvr() to 
complete the connection setup.  To avoid the overhead of starting a new ghost 
for every request, the application can use close() to end each request, and 
then accept_srvr() to wait for the next request.  The INETD STATUS command 
will display such waiting servers in state 1.  If a request arrives when the 
server is between accept_srvr() calls, a new ghost will be started.  If INETD 
is restarted while a server is in accept_srvr(), the server will abort (M$XXX 
in XSL$ACCEPT_SRVR). 
The name parameter specifies an application-defined buffer to receive the 
address of the socket that initiated the connection. 
The namelen parameter specifies how large the name buffer is, expressed as the 
number of characters it can hold. 
If the accept_srvr() function is successful, the status result contains the 
descriptor of the new socket allocated for the new connection.  The descriptor 
is a small non-negative integer, equivalent to the DCBNUM of the DCB allocated 
for the new socket.  The name and namelen parameters are modified to identify 
the initiator of the connection request. 
If the accept_srvr() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE.  The XSL$ACCEPT_SRVR procedure additionally ALTRETURNs 
if it is unsuccessful; it is otherwise identical to the accept_srvr() 
function. 
If no connection requests are pending when accept_srvr() is invoked, the 
action taken depends on the socket mode.  The mode of a socket is defined to 
be either "blocking" or "nonblocking".  If the socket is blocking (which is 
the default mode) the application is blocked (i.e., suspended) until an 
incoming connection request is received from the network.  If the socket is 
nonblocking, the condition is treated as an EWOULDBLOCK error. 
The mode of a socket can be changed with either fcntl() or ioctl(). 
The accept_srvr() function applies only to "stream" sockets. 
Errors: 
Following are the possible error conditions reported when the accept_srvr() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is inappropriate to identify a socket. 
EINVAL                  E$INVAL 
The listen() function has not been invoked for this socket. 
EMFILE                  E$MFILE 
M$GETDCB failed.  Unable to allocate DCB for new socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
EOPNOTSUPP              E$OPNOTSUPP 
This is not a "stream" socket. 
EWOULDBLOCK             E$WOULDBLOCK 
No connections are pending for this nonblocking socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Compares two strings of bytes and returns status. 
C Usage: 
    status = bcmp( ptr1, ptr2, len ); 
Parameters: 
    ptr1        address of first bytestring in memory 
    ptr2        address of second bytestring in memory 
    len         integer number of bytes to compare 
Result: 
    status      integer status of comparison 
Description: 
The bcmp() function compares two strings of bytes and returns zero if they are 
identical, otherwise returns a nonzero value.  Both strings are assumed to be 
len bytes long.  If len is zero then bcmp() returns zero. 
Errors: 
No error checking is performed by the bcmp() function. 
00001
00004
00005
00002
00003
Purpose: 
    Copies a string of bytes from one memory address to another. 
C Usage: 
    bcopy( ptr1, ptr2, len ); 
Parameters: 
    ptr1        address of source bytestring in memory 
    ptr2        address of destination bytestring in memory 
    len         integer number of bytes to copy 
Result: 
The result of the bcopy() function is undefined. 
Description: 
The bcopy() function copies len bytes starting at ptr1 to the address given by 
ptr2.  Overlap of source and destination has an undefined result. 
Errors: 
No error checking is performed by the bcopy() function. 
00001
00004
00005
00002
00003
Purpose: 
    Binds an address to a socket, so the socket can be addressed by other 
    sockets elsewhere in the network. 
C Usage: 
    status = bind( s, &name, namelen ); 
PL6 Usage: 
    CALL XSL$BIND( status, s, name, namelen ); 
Parameters: 
    s           integer socket descriptor 
    name        sockaddr structure 
    namelen     integer number of significant characters in name 
Result: 
    status      integer error code 
Description: 
The bind() function assigns an address to an existing socket.  When a socket 
is allocated with the socket() function, it has no associated address.  In 
order for other sockets in the network to identify the new socket, it must 
have an address bound to it. 
The s parameter specifies the descriptor of the socket to be bound. 
The name parameter specifies the address to bind to the socket.  In C source, 
it is a sockaddr structure.  In PL6 source, it is an XSL$SOCKADDR structure. 
The namelen parameter specifies the number of significant characters in name. 
If the bind() function is successful, the status result contains ESUCCESS or 
E$SUCCESS. 
If the bind() function is unsuccessful, the status result contains EFAILURE or 
E$FAILURE and the application must inspect errno or XSL_ERRNO to determine the 
specific error condition.  The XSL$BIND procedure additionally ALTRETURNs if 
it is unsuccessful; it is otherwise identical to the bind() function. 
Errors: 
Following are the possible error conditions reported when the bind() function 
is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EACCES                  E$ACCES 
Permission is denied to perform the function requested. 
EADDRINUSE              E$ADDRINUSE 
The specified address is already in use. 
EADDRNOTAVAIL           E$ADDRNOTAVAIL 
The specified address is not available. 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
EFAULT                  E$FAULT 
The namelen parameter is invalid (less than or equal to zero). 
EINVAL                  E$INVAL 
Either connect() or bind() has already been issued on this socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Zeroes a string of bytes in memory. 
C Usage: 
    bzero( ptr, len ); 
Parameters: 
    ptr         address of bytestring to be zeroed 
    len         integer number of bytes to be zeroed 
Result: 
The result of the bzero() function is undefined. 
Description: 
The bzero() function zeroes len bytes of a string in memory. 
Errors: 
No error checking is performed by the bzero() function. 
00001
00004
00005
00002
00003
Purpose: 
    Closes the socket and releases any context associated with it. 
C Usage: 
    status = close( s ); 
PL6 Usage: 
    CALL XSL$CLOSE( status, s ); 
Parameters: 
    s           integer socket descriptor 
Result: 
    status      integer error code 
Description: 
The close() function terminates any data transfer in progress through the 
socket, closes the underlying connection (if any), and releases any internal 
context associated with the socket. 
The s parameter specifies the descriptor of the socket to close. 
If the close() function is successful, the status result contains ESUCCESS or 
E$SUCCESS. 
If the close() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$CLOSE procedure additionally ALTRETURNs 
if it is unsuccessful; it is otherwise identical to the close() function. 
Once a socket has been closed, it cannot be used for other socket operations. 
Errors: 
Following are the possible error conditions reported when the close() function 
is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Initiates a connection request to another socket elsewhere in the network. 
C Usage: 
    status = connect( s, &name, namelen ); 
PL6 Usage: 
    CALL XSL$CONNECT( status, s, name, namelen ); 
Parameters: 
    s           integer socket descriptor 
    name        sockaddr structure 
    namelen     integer size of name in characters 
Result: 
    status      integer error code 
Description: 
The connect() function, when invoked on a "stream" socket, initiates a 
connection request to the remote socket named by name and namelen.  When 
invoked on a "datagram" socket, connect() specifies the remote socket that 
datagrams are to be sent to and received from. 
The s parameter specifies the descriptor of the socket on which to initiate 
the connection. 
The name parameter specifies the address of the remote socket.  In C source, 
it is a sockaddr structure.  In PL6 source, it is an XSL$SOCKADDR structure. 
The namelen parameter specifies the number of significant characters in name. 
If the connect() function is successful, the status result contains ESUCCESS 
or E$SUCCESS. 
If the connect() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$CONNECT procedure additionally 
ALTRETURNs if it is unsuccessful; otherwise it is identical to the connect() 
function. 
The application need not wait while a connection attempt is made.  If the mode 
of the socket has been set to "nonblocking" by either fcntl() or ioctl(), 
connect() initiates the connection attempt and reports the error EINPROGRESS. 
Subsequent invocations of connect() report the error EALREADY as long as the 
connection is still being attempted.  Eventually either ESUCCESS or EFAILURE 
is reported as above. 
Errors: 
Following are the possible error conditions reported when the connect() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EADDRINUSE              E$ADDRINUSE 
The specified address is already in use. 
EADDRNOTAVAIL           E$ADDRNOTAVAIL 
The specified address is not available. 
EAFNOSUPPORT            E$AFNOSUPPORT 
Addresses in the specified family cannot be used with this socket. 
EALREADY                E$ALREADY 
A connection attempt is already in progress on this socket. 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ECONNREFUSED            E$CONNREFUSED 
Connection request refused at remote end. 
EFAULT                  E$FAULT 
The namelen parameter is invalid (less than or equal to zero). 
EINPROGRESS             E$INPROGRESS 
A connection attempt is now in progress on this socket. 
EINVAL                  E$INVAL 
Either listen() or connect() has already been invoked on this socket. 
EISCONN                 E$ISCONN 
The socket is already connected. 
ENETUNREACH             E$NETUNREACH 
The specified network is unreachable. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
ETIMEDOUT               E$TIMEDOUT 
Connection establishment timed out. 
EWOULDBLOCK             E$WOULDBLOCK 
The connection cannot be immediately completed. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Closes the etc:hosts file. 
C Usage: 
    ptr = endhostent(); 
PL6 Usage: 
    CALL XSL$ENDHOSTENT( ptr ); 
Parameters: 
    (none) 
Result: 
    ptr         pointer to arbitrary location 
Description: 
The endhostent() function closes the etc:hosts file. 
If the endhostent() function is successful, the ptr result contains an 
arbitrary non-NULL value. 
If the endhostent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while closing the hosts file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Closes the etc:networks file. 
C Usage: 
    ptr = endnetent(); 
PL6 Usage: 
    CALL XSL$ENDNETENT( ptr ); 
Parameters: 
    (none) 
Result: 
    ptr         pointer to arbitrary location 
Description: 
The endnetent() function closes the etc:networks file. 
If the endnetent() function is successful, the ptr result contains an 
arbitrary non-NULL value. 
If the endnetent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while closing the etc:networks 
file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Closes the etc:protocols file. 
C Usage: 
    ptr = endprotoent(); 
PL6 Usage: 
    CALL XSL$ENDPROTOENT( ptr ); 
Parameters: 
    (none) 
Result: 
    ptr         pointer to arbitrary location 
Description: 
The endprotoent() function closes the etc:protocols file. 
If the endprotoent() function is successful, the ptr result contains an 
arbitrary non-NULL value. 
If the endprotoent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while closing the etc:protocols 
file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Closes the etc:services file. 
C Usage: 
    ptr = endservent(); 
PL6 Usage: 
    CALL XSL$ENDSERVENT( ptr ); 
Parameters: 
    (none) 
Result: 
    ptr         pointer to arbitrary location 
Description: 
The endservent() function closes the etc:services file. 
If the endservent() function is successful, the ptr result contains an 
arbitrary non-NULL value. 
If the endservent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while closing the etc:services 
file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Sets or obtains file control information for a file descriptor. 
C Usage: 
    status = fcntl( f, cmd, flags ); 
PL6 Usage: 
    CALL XSL$FCNTL( status, f, cmd, flags ); 
Parameters: 
    f           integer file descriptor 
    cmd         integer command code 
    flags       sum of integer command flags 
Result: 
    status      integer current setting or error code 
Description: 
The fcntl() function provides a subset of the corresponding function available 
on other systems.  On CP-6 systems, it is used only to set the mode of a 
socket to "nonblocking", or to get the current setting of the mode. 
The f parameter specifies the descriptor of the socket whose mode is 
to be queried or modified. 
The cmd parameter specifies the command to be issued.  Equates for the 
possible values can be found in <fcntl.h> or XSL_SOCKET_E. Only the 
"get status flags" and "set status flags" commands are currently 
supported.  "Get status flags" is selected by coding F_GETFL or %XSL_F_GETFL 
in C or PL6 source, respectively.  "Set status flags" is selected by coding 
F_SETFL or %XSL_F_SETFL in C or PL6 source, respectively. 
The flags parameter specifies the particular flags to be queried or modified. 
Equates for the possible values can be found in <fcntl.h> or XSL_SOCKET_E. 
Only the "ndelay" flag is currently supported.  This is selected by coding 
O_NDELAY or %XSL_O_NDELAY in C or PL6 source, respectively. 
If the fcntl() function is successful, the status result depends on the 
command issued.  If the command is "get status flags", status contains 
the value of the select status flags.  If the command is "set status flags", 
status contains ESUCCESS or E$SUCCESS. 
If the fcntl() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE and the application must inspect errno or XSL_ERRNO 
to determine the specific error condition.  The XSL$FCNTL procedure 
additionally ALTRETURNs if it is unsuccessful; it is otherwise identical 
to the fcntl() function. 
If the command is other than "get status flags" or "set status flags" the 
error EINVAL is reported.  If command is "get status flags" or "set status 
flags" and flags other than "ndelay" are specified, they are ignored. 
If the command is "set status flags" and one of the flags is "ndelay", the 
socket mode is set to "non-blocking"; otherwise it is set to "blocking". 
Modifications to the socket mode are processed by the Socket Library and, 
if the socket is bound to a FEP, modifications to the socket mode are 
processed by that FEP. 
Errors: 
Following are the possible error conditions reported when the fcntl() function 
is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor f is not appropriate to identify a socket. 
EINVAL                  E$INVAL 
The command is neither get status flags nor set status flags. 
ENOTSOCK                E$NOTSOCK 
The descriptor f is no longer valid to identify a socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Searches the etc:hosts file for an entry whose address matches that 
    specified. 
C Usage: 
    ptr = gethostbyaddr( addr, len, type ); 
PL6 Usage: 
    CALL XSL$GETHOSTBYADDR( ptr, addr, len, type ); 
Parameters: 
    addr        character array containing address 
    len         integer number of significant characters in addr 
    type        integer address type 
Result: 
    ptr         pointer to static buffer containing a host entry 
Description: 
The gethostbyaddr() function sequentially searches the etc:hosts file for the 
first entry whose address matches the specified address.  This entry is parsed 
into a hostent structure in a static buffer within the socket library, and a 
pointer to this buffer is returned. 
The addr parameter specifies an application-defined buffer containing the 
address of the host to be looked up. 
The len parameter specifies the number of significant characters in addr. 
The type parameter specifies the address format.  Equates for the possible 
values can be found in <xsl_socket.h> or XSL_SOCKET_E.  Only the "DARPA 
Internet" address format is currently supported; it is selected by coding 
AF_INET or %XSL_AF_INET in C or PL6 source, respectively. 
If the gethostbyaddr() function is successful, the ptr result contains a 
pointer to a static buffer within the socket library containing a hostent 
structure for the matching entry. 
If the gethostbyaddr() function is unsuccessful, the ptr result contains a 
NULL pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:hosts 
file, including reaching the end of the file without matching the address. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Searches the etc:hosts file for an entry whose name matches that 
    specified. 
C Usage: 
    ptr = gethostbyname( name ); 
PL6 Usage: 
    CALL XSL$GETHOSTBYNAME( ptr, name ); 
Parameters: 
    name        character array containing a host name to look up 
Result: 
    ptr         pointer to static buffer containing a host entry 
Description: 
The gethostbyname() function sequentially searches the etc:hosts file for the 
first entry whose name matches the specified name.  This entry is parsed into 
a hostent structure in a static buffer within the socket library, and a 
pointer to this buffer is returned. 
The name parameter specifies an application-defined buffer containing the name 
of the host to be looked up. 
If the gethostbyname() function is successful, the ptr result contains a 
pointer to a static buffer within the socket library containing a hostent 
structure for the matching entry. 
If the gethostbyname() function is unsuccessful, the ptr result contains a 
NULL pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:hosts 
file, including reaching the end of the file without matching the name. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Reads the next entry of the etc:hosts file into an internal buffer. 
C Usage: 
    ptr = gethostent(); 
PL6 Usage: 
    CALL XSL$GETHOSTENT( ptr ); 
Parameters: 
    (none) 
Result: 
    ptr         pointer to static buffer containing a host entry 
Description: 
The gethostent() function opens the etc:hosts file, if it is not already open, 
and reads the next entry and parses it into a hostent structure in a static 
buffer within the socket library.  A pointer to this buffer is returned. 
If the gethostent() function is successful, the ptr result contains a pointer 
to a static buffer within the socket library containing a hostent structure 
for the entry read. 
If the gethostent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:hosts 
file, including reaching the end of the file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Obtains the name of the host system. 
C Usage: 
    status = gethostname( name, namelen ); 
PL6 Usage: 
    CALL XSL$GETHOSTNAME( status, name, namelen ); 
Parameters: 
    name        character array buffer 
    namelen     integer size of name in characters 
Result: 
    status      integer error code 
Description: 
The gethostname() function returns the name of the system on which the 
function was invoked.  The name is found by looking up the alias "localhost" 
in the etc:hosts file and returning the system name associated with it. 
The name parameter specifies an application-defined buffer to receive the host 
name. 
The namelen parameter specifies how large the buffer is, expressed as the 
number of characters it can hold. 
If the gethostname() function is successful, the status result contains 
ESUCCESS or E$SUCCESS. 
If the gethostname() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE and the application must inspect errno or XSL_ERRNO to 
determine the specific error condition.  The XSL$GETHOSTNAME procedure 
additionally ALTRETURNs if it is unsuccessful; it is otherwise identical to 
the gethostname() function. 
Errors: 
Following are the possible error conditions reported when the gethostname() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
ENOENT                  E$NOENT 
The hosts file does not exist. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Searches the etc:networks file for an entry whose address matches that 
    specified. 
C Usage: 
    ptr = getnetbyaddr( netnum, type ); 
PL6 Usage: 
    CALL XSL$GETNETBYADDR( ptr, netnum, type ); 
Parameters: 
    netnum      integer network number 
    type        integer address type 
Result: 
    ptr         pointer to static buffer containing a network entry 
Description: 
The getnetbyaddr() function sequentially searches the etc:networks file for 
the first entry whose network number matches the specified network number. 
This entry is parsed into a netent structure in a static buffer within the 
socket library, and a pointer to this buffer is returned. 
The netnum parameter specifies the network number of interest. 
The type parameter specifies the address format.  Equates for the possible 
values can be found in <xsl_socket.h> or XSL_SOCKET_E.  Only the "DARPA 
Internet" address format is currently supported; it is selected by coding 
AF_INET or %XSL_AF_INET in C or PL6 source, respectively. 
If the getnetbyaddr() function is successful, the ptr result contains a 
pointer to a static buffer within the socket library containing a netent 
structure for the matching entry. 
If the getnetbyaddr() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:networks 
file, including reaching the end of the file without matching the network 
number. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Searches the etc:networks file for an entry whose name matches that 
    specified. 
C Usage: 
    ptr = getnetbyname( name ); 
PL6 Usage: 
    CALL XSL$GETNETBYNAME( ptr, name ); 
Parameters: 
    name        character array containing a network name to look up 
Result: 
    ptr         pointer to static buffer containing a network entry 
Description: 
The getnetbyname() function sequentially searches the etc:networks file for 
the first entry whose name matches the specified name.  This entry is parsed 
into a netent structure in a static buffer within the socket library, and a 
pointer to this buffer is returned. 
The name parameter specifies an application-defined buffer containing the name 
of the network to be looked up. 
If the getnetbyname() function is successful, the ptr result contains a 
pointer to a static buffer within the socket library containing a netent 
structure for the matching entry. 
If the getnetbyname() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:networks 
file, including reaching the end of the file without matching the name. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Reads the next entry of the etc:networks file into an internal buffer. 
C Usage: 
    ptr = getnetent(); 
PL6 Usage: 
    CALL XSL$GETNETENT( ptr ); 
Parameters: 
    (none) 
Result: 
    ptr         pointer to static buffer containing a network entry 
Description: 
The getnetent() function opens the etc:networks file, if it is not already 
open, and reads the next entry and parses it into a netent structure in a 
static buffer within the socket library.  A pointer to this buffer is 
returned. 
If the getnetent() function is successful, the ptr result contains a pointer 
to a static buffer within the socket library containing a netent structure for 
the entry read. 
If the getnetent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:networks 
file, including reaching the end of the file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Obtains the name of the socket at the remote end of a connection. 
C Usage: 
    status = getpeername( s, &name, &namelen ); 
PL6 Usage: 
    CALL XSL$GETPEERNAME( status, s, name, namelen ); 
Parameters: 
    s           integer socket descriptor 
    name        sockaddr structure 
    namelen     integer size of name in characters 
Results: 
    status      integer error code 
    name        sockaddr structure 
    namelen     integer number of significant characters in name 
Description: 
The getpeername() function obtains the name of the socket at the remote end of 
a connection with one of the application's sockets. 
The s parameter specifies the descriptor of the socket or communication end 
point. 
The name parameter specifies an application-defined buffer to receive the 
remote socket's name. 
The namelen parameter specifies how large the name buffer is, expressed as the 
number of characters it can hold. 
If the getpeername() function is successful, the status result contains 
ESUCCESS or E$SUCCESS.  The name and namelen parameters are modified to 
identify the name of the remote socket. 
If the getpeername() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE and the application must inspect errno or XSL_ERRNO to 
determine the specific error condition.  The XSL$GETPEERNAME procedure 
additionally ALTRETURNs if it is unsuccessful; it is otherwise identical to 
the getpeername() function. 
Errors: 
Following are the possible error conditions reported when the getpeername() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Searches the etc:protocols file for an entry whose name matches that 
    specified. 
C Usage: 
    ptr = getprotobyname( name ); 
PL6 Usage: 
    CALL XSL$GETPROTOBYNAME( ptr, name ); 
Parameters: 
    name        character array containing a protocol name to look up 
Result: 
    ptr         pointer to static buffer containing a protocol entry 
Description: 
The getprotobyname() function sequentially searches the etc:protocols file for 
the first entry whose name matches the specified name.  This entry is parsed 
into a protoent structure in a static buffer within the socket library, and a 
pointer to this buffer is returned. 
The name parameter specifies an application-defined buffer containing the name 
of the protocol to be looked up. 
If the getprotobyname() function is successful, the ptr result contains a 
pointer to a static buffer within the socket library containing a protoent 
structure for the matching entry. 
If the getprotobyname() function is unsuccessful, the ptr result contains a 
NULL pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:protocols 
file, including reaching the end of the file without matching the name. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Searches the etc:protocols file for an entry whose number matches that 
    specified. 
C Usage: 
    ptr = getprotobynumber( proto ); 
PL6 Usage: 
    CALL XSL$GETPROTOBYNUMBER( ptr, proto ); 
Parameters: 
    proto       integer protocol number 
Result: 
    ptr         pointer to static buffer containing a protocol entry 
Description: 
The getprotobynumber() function sequentially searches the etc:protocols file 
for the first entry whose number matches the specified number.  This entry is 
parsed into a protoent structure in a static buffer within the socket library, 
and a pointer to this buffer is returned. 
The proto parameter specifies the number of the protocol of interest. 
If the getprotobynumber() function is successful, the ptr result contains a 
pointer to a static buffer within the socket library containing a protoent 
structure for the matching entry. 
If the getprotobyaddr() function is unsuccessful, the ptr result contains a 
NULL pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:protocols 
file, including reaching the end of the file without matching the address. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Reads the next entry of the etc:protocols file into an internal buffer. 
C Usage: 
    ptr = getprotoent(); 
PL6 Usage: 
    CALL XSL$GETPROTOENT( ptr ); 
Parameters: 
    (none) 
Result: 
    ptr         pointer to static buffer containing a protocol entry 
Description: 
The getprotoent() function opens the etc:protocols file, if it is not already 
open, and reads the next entry and parses it into a protoent structure in a 
static buffer within the socket library.  A pointer to this buffer is 
returned. 
If the getprotoent() function is successful, the ptr result contains a pointer 
to a static buffer within the socket library containing a protoent structure 
for the entry read. 
If the getprotoent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:protocols 
file, including reaching the end of the file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Searches the etc:services file for an entry whose name matches that 
    specified. 
C Usage: 
    ptr = getservbyname( name, proto ); 
PL6 Usage: 
    CALL XSL$GETSERVBYNAME( ptr, name, proto ); 
Parameters: 
    name        character array containing a service name to look up 
    proto       character array containing a protocol name 
Result: 
    ptr         pointer to static buffer containing a service entry 
Description: 
The getservbyname() function sequentially searches the etc:services file for 
the first entry whose name matches the specified name.  This entry is parsed 
into a servent structure in a static buffer within the socket library, and a 
pointer to this buffer is returned.  If the optional proto parameter is 
non-NULL, searches must also match the specified protocol name. 
The name parameter specifies an application-defined buffer containing the name 
of the service to be looked up. 
The proto parameter specifies an application-defined buffer containing the 
name of the protocol. Specifying the proto parameter is optional and can be 
coded as NULL or zero. 
If the getservbyname() function is successful, the ptr result contains a 
pointer to a static buffer within the socket library containing a servent 
structure for the matching entry. 
If the getservbyname() function is unsuccessful, the ptr result contains a 
NULL pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:services 
file, including reaching the end of the file without matching the name. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Searches the etc:services file for an entry whose port number matches that 
    specified. 
C Usage: 
    ptr = getservbyport( port, proto ); 
PL6 Usage: 
    CALL XSL$GETSERVBYPORT( ptr, port, proto ); 
Parameters: 
    port        integer port number 
    proto       character array containing protocol name 
Result: 
    ptr         pointer to static buffer containing a service entry 
Description: 
The getservbyport() function sequentially searches the etc:services file for 
the first entry whose port number matches the specified number.  This entry is 
parsed into a servent structure in a static buffer within the socket library, 
and a pointer to this buffer is returned. 
The port parameter specifies the port number of the service of interest. 
The proto parameter specifies an application-defined buffer containing the 
name of the protocol. Specifying the proto parameter is optional and can be 
coded as NULL or zero. 
If the getservbyport() function is successful, the ptr result contains a 
pointer to a static buffer within the socket library containing a servent 
structure for the matching entry. 
If the getservbyport() function is unsuccessful, the ptr result contains a 
NULL pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:services 
file, including reaching the end of the file without matching the port number. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Reads the next entry of the etc:services file into an internal buffer. 
C Usage: 
    ptr = getservent(); 
PL6 Usage: 
    CALL XSL$GETSERVENT( ptr ); 
Parameters: 
    (none) 
Result: 
    ptr         pointer to static buffer containing a service entry 
Description: 
The getservent() function opens the etc:services file, if it is not already 
open, and reads the next entry and parses it into a servent structure in a 
static buffer within the socket library.  A pointer to this buffer is 
returned. 
If the getservent() function is successful, the ptr result contains a pointer 
to a static buffer within the socket library containing a servent structure 
for the entry read. 
If the getservent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while reading the etc:services 
file, including reaching the end of the file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Obtains the name of a socket. 
C Usage: 
    status = getsockname( s, &name, &namelen ); 
PL6 Usage: 
    CALL XSL$GETSOCKNAME( status, s, name, namelen ); 
Parameters: 
    s           integer socket descriptor 
    name        sockaddr structure 
    namelen     integer size of name in characters 
Results: 
    status      integer error code 
    name        sockaddr structure 
    namelen     integer number of significant characters in name 
Description: 
The getsockname() function obtains the name of the specified socket. 
The name parameter specifies an application-defined buffer to receive the 
socket's name. 
The s parameter specifies the descriptor of the socket or communication end 
point. 
The namelen parameter specifies how large the name buffer is, expressed as the 
number of characters it can hold. 
If the getsockname() function is successful, the status result contains 
ESUCCESS or E$SUCCESS.  The name and namelen parameters are modified to 
identify the name of the socket. 
If the getsockname() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE and the application must inspect errno or XSL_ERRNO to 
determine the specific error condition.  The XSL$GETSOCKNAME procedure 
additionally ALTRETURNs if it is unsuccessful; it is otherwise identical to 
the getsockname() function. 
Errors: 
Following are the possible error conditions reported when the getsockname() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Obtains the current setting of an option at one of the internal protocol 
    levels supporting a socket. 
C Usage: 
    status = getsockopt( s, level, optname, &optval, &optlen ); 
PL6 Usage: 
    CALL XSL$GETSOCKOPT( status, s, level, optname, optval, optlen ); 
Parameters: 
    s           integer socket descriptor 
    level       integer protocol number 
    optname     integer option name 
    optval      character array buffer for option value 
    optlen      integer size of optval in characters 
Results: 
    status      integer error code 
    optval      current option value 
    optlen      integer number of significant characters in optval 
Description: 
The getsockopt() function obtains the current setting of any option at any 
internal protocol level supporting an existing socket. 
The s parameter specifies the descriptor of the socket of interest. 
The level parameter specifies the protocol level managing the option of 
interest.  "Socket" level is specified by coding SOL_SOCKET or %XSL_SOL_SOCKET 
in C or PL6 source, respectively.  Other levels are specified by using a 
protocol number from the include files <xsl_socket.h> or XSL_SOCKET_E, 
respectively.  "Socket" is the only level implemented at this time. 
The optname parameter specifies the option of interest.  For "socket" level 
this is coded using one of the SO_ #defines or %XSL_SO_ equates which are 
defined in the include file <xsl_socket.h> or XSL_SOCKET_E.  These options are 
listed in the following table. 
  C #define        PL6 %EQU               Meaning 
SO_ACCEPTCONN    XSL_SO_ACCEPTCONN      Socket has had listen(). 
SO_BLOCKING      XSL_SO_BLOCKING        Blocking option. 
SO_BROADCAST     XSL_SO_BROADCAST       Allow broadcast messages. 
SO_DEBUG         XSL_SO_DEBUG           Record debugging information. 
SO_DONTROUTE     XSL_SO_DONTROUTE       Just use Interface address. 
SO_ERROR         XSL_SO_ERROR           Get error status and clear. 
SO_IMASOCKET     XSL_SO_IMASOCKET       Reserved for DPX/2-300 Kernel. 
SO_KEEPALIVE     XSL_SO_KEEPALIVE       Keep connections alive. 
SO_LINGER        XSL_SO_LINGER          Linger on close if data present. 
SO_NWREADS       XSL_SO_NWREADS         Max pending NoWait read count. 
SO_NWBUFFS       XSL_SO_NWBUFFS         Max pending buffer count. 
SO_OOBINLINE     XSL_SO_OOBINLINE       Leave received OOB data in line. 
SO_ORDREL        XSL_SO_ORDREL          Perform orderly release. 
SO_RCVBUF        XSL_SO_RCVBUF          Receive buffer size. 
SO_RCVLOWAT      XSL_SO_RCVLOWAT        Receive low-water mark. 
SO_RCVTIMEO      XSL_SO_RCVTIMEO        Receive timeout value. 
SO_REUSEADDR     XSL_SO_REUSEADDR       Allow local address reuse. 
SO_SNDBUF        XSL_SO_SNDBUF          Send buffer size. 
SO_SNDLOWAT      XSL_SO_SNDLOWAT        Send low-water mark. 
SO_SNDTIMEO      XSL_SO_SNDTIMEO        Send timeout value. 
SO_TYPE          XSL_SO_TYPE            Get socket type. 
SO_USELOOPBACK   XSL_SO_USELOOPBACK     Bypass hardware when possible. 
The optval parameter specifies an application-defined buffer to receive the 
current setting of the option. 
The optlen parameter specifies how large the optval buffer is, expressed as 
the number of characters it can hold. 
If the getsockopt() function is successful, the status result contains 
ESUCCESS or E$SUCCESS.  The optval and optlen parameters are modified to 
contain the current value of the selected option. 
If the getsockopt() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE and the application must inspect errno or XSL_ERRNO to 
determine the specific error condition.  The XSL$GETSOCKOPT procedure 
additionally ALTRETURNs if it is unsuccessful; it is otherwise identical to 
the getsockopt() function. 
If level is SOL_SOCKET and optname is one of SO_NWBUFFS, SO_NWREADS, 
SO_OOBINLINE, or SO_TYPE, the Socket Library provides the result.  For any 
other combination of level and optname, the socket must already be bound to a 
FEP and the result is provided by that FEP. 
Errors: 
Following are the possible error conditions reported when the getsockopt() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOPROTOOPT             E$NOPROTOOPT 
The option specified in optname is not recognized by protocol level. 
ENOTBOUND               E$NOTBOUND 
Socket is not bound to a FEP. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
00001
00005
00006
00003
00002
00004
     The hostent structure is a template for the information returned by the 
     Socket Library functions that deal with the etc:hosts.:SYS file. 
h_addr_list - (char **) 
     Points at a buffer within the Socket Library containing the Internet 
     address(es) of the host.  Each address is a 32-bit integer unpacked into 
     the lower eight bits of four successive bytes.  The buffer is terminated 
     by a NULL pointer. 
h_addrtype - (int) 
     Specifies the address family of the address pointed at by the address 
     pointer.  It is always AF_INET. 
h_aliases - (char **) 
     Points at an array of pointers to character strings.  Each character 
     string contains an alias of the host name, and is terminated by a NUL 
     byte.  The array of pointers is terminated by a NULL pointer. 
h_length - (int) 
     Specifies the length of the address pointed at by the address pointer. 
     It is always 4. 
h_name - (char *) 
     Points at a character string containing the host name.  The string is 
     terminated by a NUL byte. 
                                   hostent 
        0   1   2   3 
      +---+---+---+---+ 
   .0 |   |   |   |   | struct hostent { 
   .0 |ppp|ppp|ppp|ppp|   char *h_name; 
   .1 |ppp|ppp|ppp|ppp|   char **h_aliases; 
   .2 |sss|sss|sss|sss|   int h_addrtype; 
   .3 |sss|sss|sss|sss|   int h_length; 
   .4 |ppp|ppp|ppp|ppp|   char **h_addr_list; 
      +---+---+---+---+   }; 
        0   1   2   3     .5-0-0 total length 
Purpose: 
    Converts a 36-bit unsigned integer to an unpacked 32-bit unsigned integer. 
C Usage: 
    netlong = htonl( hostlong ); 
PL6 Usage: 
    CALL XSL$HTONL( netlong, hostlong ); 
Parameters: 
    hostlong    36-bit unsigned integer 
Result: 
    netlong     unpacked 32-bit unsigned integer 
Description: 
The htonl() function converts a long integer from host to network formats.  On 
CP-6 systems, this means taking the low order 32 bits of the number and 
unpacking them into the low 8 bits of 4 successive 9-bit bytes. 
The hostlong parameter specifies the long integer to be converted.  If the 
number is too large to be converted, it is truncated without warning. 
Errors: 
The htonl() function is always successful.  There are no errors reported. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Converts a 18-bit unsigned integer to an unpacked 16-bit unsigned integer. 
C Usage: 
    netshort = htons( hostshort ); 
PL6 Usage: 
    CALL XSL$HTONS( netshort, hostshort ); 
Parameters: 
    hostshort   18-bit unsigned integer 
Result: 
    netshort    unpacked 16-bit unsigned integer 
Description: 
The htons() function converts a short integer from host to network formats. 
On CP-6 systems, this means taking the low order 16 bits of the number and 
unpacking them into the low 8 bits of 2 successive 9-bit bytes. 
The hostshort parameter specifies the short integer to be converted.  If the 
number is too large to be converted, it is truncated without warning. 
Errors: 
The htons() function is always successful.  There are no errors reported. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Converts a character string in "dot notation" to an Internet address. 
C Usage: 
    status = inet_addr( cp ); 
PL6 Usage: 
    CALL XSL$INET_ADDR( status, cp ); 
Parameters: 
    cp          pointer to character array 
Result: 
    status      Internet address or error code stored in an unsigned integer. 
Description: 
The inet_addr() function takes a character string representation of an 
Internet address and converts it to its binary representation suitable for use 
with other socket library functions. 
The cp parameter specifies the address of the character string to convert. 
The string must contain an Internet address in "dot notation", i.e., a 
sequence of one to four numeric values separated by dots.  Each numeric value 
can be in either hexadecimal, octal, or decimal notation.  A leading '0x' or 
'0X' implies hexadecimal; a leading '0' implies octal; otherwise decimal is 
implied. 
If four values are given, they are assigned to the four bytes of result. 
If three values are given, the last value is treated as a 16-bit number 
unpacked into the last two bytes of result. 
If two values are given, the last value is treated as a 24-bit number unpacked 
into the last three bytes of result. 
If one value is given, it is treated as a 32-bit number and unpacked into the 
four bytes of result. 
If the inet_addr() function is successful, the status result contains the 
converted Internet address suitable for use by other socket library functions. 
If the inet_addr() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE.  The XSL$INET_ADDR procedure additionally ALTRETURNs if 
it is unsuccessful; it is otherwise identical to the inet_addr() function. 
Errors: 
The status result contains EFAILURE or E$FAILURE if the conversion could not 
be performed. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Extracts the local network address from an Internet address. 
C Usage: 
    lnaddr = inet_lnaof( inaddr ); 
PL6 Usage: 
    CALL XSL$INET_LNAOF( lnaddr, inaddr ); 
Parameters: 
    inaddr      Internet address 
Result: 
    lnaddr      integer local network address 
Description: 
The inet_lnaof() function extracts the local network address from an Internet 
address. 
The inaddr parameter specifies the Internet address to process. 
On return from the inet_lnaof() function, the lnaddr result contains the 
extracted local network address. 
Errors: 
The inet_lnaof() function always succeeds.  There are no error conditions. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Combines a network number and local network address into an Internet 
    address. 
C Usage: 
    inaddr = inet_makeaddr( netnum, lnaddr ); 
PL6 Usage: 
    CALL XSL$INET_MAKEADDR( inaddr, netnum, lnaddr ); 
Parameters: 
    netnum      integer network number 
    lnaddr      integer local network address 
Result: 
    inaddr      Internet address 
Description: 
The inet_makeaddr() function combines a network number and a local network 
address to make an Internet address. 
The netnum parameter specifies the network number. 
The lnaddr parameter specifies the local network address. 
On return from the inet_makeaddr() function, the inaddr result contains the 
constructed Internet address. 
Errors: 
The inet_makeaddr() function always succeeds.  There are no error conditions. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Extracts the network number from an Internet address. 
C Usage: 
    netnum = inet_netof( inaddr ); 
PL6 Usage: 
    CALL XSL$INET_NETOF( netnum, inaddr ); 
Parameters: 
    inaddr      Internet address 
Result: 
    netnum      integer network number 
Description: 
The inet_netof() function extracts the network number from an Internet 
address. 
The inaddr parameter specifies the Internet address to process. 
On return from the inet_netof() function, the netnum result contains the 
extracted network number. 
Errors: 
The inet_netof() function always succeeds.  There are no error conditions. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Converts a character string in "dot notation" to a network number. 
C Usage: 
    status = inet_network( cp ); 
PL6 Usage: 
    CALL XSL$INET_NETWORK( status, cp ); 
Parameters: 
    cp          pointer to character array 
Result: 
    status      integer network number or error code 
Description: 
The inet_network() function takes a character string representation of an 
Internet address and extracts the network number from it. 
The cp parameter specifies the address of the character string to process. 
The string must contain an Internet address in "dot notation", i.e., a 
sequence of one to four numeric values separated by dots.  Each numeric value 
can be in either hexadecimal, octal, or decimal notation.  A leading '0x' or 
'0X' implies hexadecimal; a leading '0' implies octal; otherwise decimal is 
implied. 
If the inet_network() function is successful, the status result contains the 
extracted network number suitable for use by other socket library functions. 
If the inet_network() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE.  The XSL$INET_NETWORK procedure additionally ALTRETURNs 
if it is unsuccessful; it is otherwise identical to the inet_network() 
function. 
Errors: 
The status result contains EFAILURE or E$FAILURE if the conversion could not 
be performed. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Converts an Internet address from binary representation to a character 
    string. 
C Usage: 
    cp = inet_ntoa( inaddr ); 
PL6 Usage: 
    CALL XSL$INET_NTOA( cp, inaddr ); 
Parameters: 
    inaddr      Internet address 
Result: 
    cp          pointer to character array 
Description: 
The inet_ntoa() function converts an Internet address in binary to its 
character representation, which is a sequence of one to four decimal numbers 
separated by dots. 
The inaddr parameter specifies the Internet address to convert. 
On return from the inet_ntoa() function, the cp result points to a static 
buffer within the socket library that contains the converted string. 
Errors: 
The inet_ntoa() function always succeeds.  There are no error conditions. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Sets or obtains I/O control information for a file descriptor. 
C Usage: 
    status = ioctl( f, cmd, &parm ); 
PL6 Usage: 
    CALL XSL$IOCTL( status, f, cmd, parm ); 
Parameters: 
    f           integer file descriptor 
    cmd         integer command code 
    parm        address of parameter buffer 
Results: 
    status      integer error code 
    parm        optionally modified parameter buffer 
Description: 
The ioctl() function provides a subset of the corresponding function available 
on other systems. 
The f parameter specifies the descriptor of the socket for which the command 
is to be issued. 
The cmd parameter specifies the command to be issued.  Equates for the 
possible values can be found in <ioctl.h> or XSL_SOCKET_M.  If the latter 
include file is used, the macro XSL_IOCTLS must be invoked to establish the 
equates.  The available commands are listed in the following table. 
  C #define        PL6 %EQU               Meaning 
FIOCLEX          XSL_FIOCLEX            Set exclusive fd use. 
FIONCLEX         XSL_FIONCLEX           Remove exclusive fd use. 
FIONREAD         XSL_FIONREAD           Number of bytes available. 
FIONBIO          XSL_FIONBIO            Set/Clear nonblocking I/O. 
FIOASYNC         XSL_FIOASYNC           Set/Clear async I/O. 
FIOSETOWN        XSL_FIOSETOWN          Set owner. 
FIOGETOWN        XSL_FIOGETOWN          Get owner. 
SIOCSHIWAT       XSL_SIOCSHIWAT         Set high water mark. 
SIOCGHIWAT       XSL_SIOCGHIWAT         Get high water mark. 
SIOCSLOWAT       XSL_SIOCSLOWAT         Set low water mark. 
SIOCGLOWAT       XSL_SIOCGLOWAT         Get low water mark. 
SIOCATMARK       XSL_SIOCATMARK         At out-of-band mark? 
SIOCSPGRP        XSL_SIOCSPGRP          Set process group. 
SIOCGPGRP        XSL_SIOCGPGRP          Get process group. 
The parm parameter specifies an application-defined buffer containing 
information appropriate to the command. 
If the ioctl() function is successful, the status result contains ESUCCESS or 
E$SUCCESS.  The parm parameter may be modified by some commands. 
If the ioctl() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$IOCTL procedure additionally ALTRETURNs 
if it is unsuccessful; it is otherwise identical to the ioctl() function. 
All ioctl() commands require the socket to be bound to a FEP, otherwise the 
error ENOTBOUND is reported.  The command FIONBIO is processed by the Socket 
Library and the FEP.  The commands FIONREAD and SIOCATMARK are processed 
either by the Socket Library or the FEP, depending on whether the socket is 
currently conditioned for NoWait I/O.  The commands FIOCLEX, FIONCLEX, 
FIOASYNC, FIOSETOWN, FIOGETOWN, SIOCSPGRP, and SIOCGPGRP are currently not 
implemented, and report the error EINVAL.  All other commands are processed by 
the FEP. 
Errors: 
Following are the possible error conditions reported when the ioctl() function 
is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor f is not appropriate to identify a socket. 
EINVAL                  E$INVAL 
The command is not supported. 
ENOTSOCK                E$NOTSOCK 
The descriptor f is no longer valid to identify a socket. 
00001
00005
00006
00003
00002
00004
The iovec structure frames an area of memory to be used as an I/O buffer in 
the readv(), writev(), recvmsg(), and sendmsg() functions. 
iov_base - (char *) 
     Points at a buffer in application memory to be used for I/O. 
iov_len - (int) 
     Specifies how large the I/O buffer is, in bytes. 
                                    iovec 
        0   1   2   3 
      +---+---+---+---+ 
   .0 |   |   |   |   | struct iovec { 
   .0 |ppp|ppp|ppp|ppp|   char *iov_base; 
   .1 |sss|sss|sss|sss|   int iov_len; 
      +---+---+---+---+   }; 
        0   1   2   3     .2-0-0 total length 
Purpose: 
    Listens for incoming connections to an existing socket. 
C Usage: 
    status = listen( s, backlog ); 
PL6 Usage: 
    CALL XSL$LISTEN( status, s, backlog ); 
Parameters: 
    s           integer socket descriptor 
    backlog     integer pending connect queue length 
Result: 
    status      integer error code 
Description: 
The listen() function prepares the socket to wait until an incoming connection 
request is delivered by the network.  The wait itself is requested with the 
accept() function. 
The s parameter specifies the descriptor of the socket on which to listen. 
The backlog parameter specifies how many pending connection requests can be 
queued while the application is processing another connection request. 
If the listen() function is successful, the status result contains ESUCCESS or 
E$SUCCESS. 
If the listen() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$LISTEN procedure additionally 
ALTRETURNs if it is unsuccessful; it is otherwise identical to the listen() 
function. 
The listen() function applies only to "stream" sockets. 
If an incoming connection arrives when the listen queue is full, the initiator 
of the connection request receives the error ECONNREFUSED. 
Errors: 
Following are the possible error conditions reported when the listen() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
EFAULT                  E$FAULT 
The backlog parameter is invalid (less than or equal to zero). 
EINVAL                  E$INVAL 
Either bind() has not been issued on this socket, or listen() has already been 
issued on this socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
EOPNOTSUPP              E$OPNOTSUPP 
This is not a "stream" socket. 
00001
00005
00006
00003
00002
00004
The msghdr structure collects together various parameters needed by the 
sendmsg() and recvmsg() functions. 
msg_accrights - (char *) 
     This item is not currently supported and must be coded as ADDR( NIL). 
msg_accrightslen - (int) 
     This item is not currently supported and must be coded as 0. 
msg_iov - (struct iovec *) 
     Points at an array of XSL$IOVEC structures framing one or more areas of 
     application memory to use for I/O buffers. 
msg_iovlen - (int) 
     Specifies how many XSL$IOVEC structures are valid at the memory address 
     specified by MSG_IOV$. 
msg_name - (char *) 
     Points at a buffer containing a network address.  For XSL$SENDMSG, the 
     buffer contains the address of the host to which the message is to be 
     sent.  For XSL$RECVMSG, the buffer contains the address of the host from 
     which the message was received. 
msg_namelen - (int) 
     Specifies how large the MSG_NAME$ buffer is, in bytes.  It must be 
     specified for both XSL$SENDMSG and XSL$RECVMSG.  For the latter, it will 
     be modified to contain the length of the address of the host from which 
     the message was received. 
                                    msghdr 
        0   1   2   3 
      +---+---+---+---+ 
   .0 |   |   |   |   | struct msghdr { 
   .0 |ppp|ppp|ppp|ppp|   char *msg_name; 
   .1 |sss|sss|sss|sss|   int msg_namelen; 
   .2 |ppp|ppp|ppp|ppp|   struct iovec *msg_iov; 
   .3 |sss|sss|sss|sss|   int msg_iovlen; 
   .4 |ppp|ppp|ppp|ppp|   char *msg_accrights; 
   .5 |sss|sss|sss|sss|   int msg_accrightslen; 
      +---+---+---+---+   }; 
        0   1   2   3     .6-0-0 total length 
The netent structures is a template for the information returned by the Socket 
Library functions that deal with the etc:networks.:SYS file. 
n_addrtype - (int) 
     Specifies the address family of the addresses used on this network.  It 
     is always AF_INET. 
n_aliases - (char **) 
     Points at an array of pointers to character strings.  Each character 
     string contains an alias of the network name, and is terminated by a NUL 
     byte.  The array of pointers is terminated by a NULL pointer. 
n_name - (char *) 
     Points at a character string containing the network name.  The string is 
     terminated by a NUL byte. 
n_net - (unsigned long) 
     Specifies the network number for this network. 
                                    netent 
        0   1   2   3 
      +---+---+---+---+ 
   .0 |   |   |   |   | struct netent { 
   .0 |ppp|ppp|ppp|ppp|   char *n_name; 
   .1 |ppp|ppp|ppp|ppp|   char **n_aliases; 
   .2 |sss|sss|sss|sss|   int n_addrtype; 
   .3 |uuu|uuu|uuu|uuu|   unsigned long n_net; 
      +---+---+---+---+   }; 
        0   1   2   3     .4-0-0 total length 
Purpose: 
    Converts an unpacked 32-bit unsigned integer to a 36-bit unsigned integer. 
C Usage: 
    hostlong = ntohl( netlong ); 
PL6 Usage: 
    CALL XSL$NTOHL( hostlong, netlong ); 
Parameters: 
    netlong     unpacked 32-bit unsigned integer 
Result: 
    hostlong    36-bit unsigned integer 
Description: 
The ntohl() function converts a long integer from network to host formats.  On 
CP-6 systems, this means taking the low 8 bits of 4 successive 9-bit bytes and 
packing them into the low order 32 bits of a word. 
The netlong parameter specifies the unpacked long integer to be converted. 
Errors: 
The htonl() function is always successful.  There are no errors reported. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Converts an unpacked 16-bit unsigned integer to a 18-bit unsigned integer. 
C Usage: 
    hostshort = ntohs( netshort ); 
PL6 Usage: 
    CALL XSL$NTOHS( hostshort, netshort ); 
Parameters: 
    netshort    unpacked 16-bit unsigned integer 
Result: 
    hostshort   18-bit unsigned integer 
Description: 
The ntohs() function converts a short integer from network to host formats. 
On CP-6 systems, this means taking the low 8 bits of 2 successive 9-bit bytes 
and packing them into the low order 16 bits of a word. 
The netshort parameter specifies the unpacked short integer to be converted. 
Errors: 
The htons() function is always successful.  There are no errors reported. 
00001
00005
00006
00003
00002
00004
The protoent structure is a template for the information returned by the 
Socket Library functions that deal with the etc:protocols.:SYS file. 
p_aliases - (char **) 
     Points at an array of pointers to character strings.  Each character 
     string contains an alias of the protocol name, and is terminated by a NUL 
     byte.  The array of pointers is terminated by a NULL pointer. 
p_name - (char *) 
     Points at a character string containing the protocol name.  The string is 
     terminated by a NUL byte. 
p_proto - (int) 
     Specifies the protocol number for this protocol. 
                                   protoent 
        0   1   2   3 
      +---+---+---+---+ 
   .0 |   |   |   |   | struct protoent { 
   .0 |ppp|ppp|ppp|ppp|   char *p_name; 
   .1 |ppp|ppp|ppp|ppp|   char **p_aliases; 
   .2 |sss|sss|sss|sss|   int p_proto; 
      +---+---+---+---+   }; 
        0   1   2   3     .3-0-0 total length 
Purpose: 
    Reads data from a socket into an application-specified buffer. 
C Usage: 
    status = read( s, buf, len ); 
PL6 Usage: 
    CALL XSL$READ( status, s, buf, len ); 
Parameters: 
    s           integer socket descriptor 
    buf         character array buffer 
    len         integer size of buf in characters 
Results: 
    status      integer number of characters read or error code 
    buf         character array buffer 
Description: 
The read() function reads any available data from the socket into the buffer 
specified. 
The s parameter specifies the descriptor of the socket to be read from. 
The buf parameter specifies an application-defined buffer to receive the data 
to be read from the socket. 
The len parameter specifies how large the buffer is, expressed as the number 
of characters it can hold. 
If the read() function is successful, the status result contains the number of 
characters read into buf.  This number is non-negative.  A successful read() 
returns all data available, up to the size of buf.  On datagram sockets, if 
the buffer is not large enough to receive the entire datagram, the excess will 
be discarded. 
If the read() function is unsuccessful, the status result contains EFAILURE or 
E$FAILURE and the application must inspect errno or XSL_ERRNO to determine the 
specific error condition.  The XSL$READ procedure additionally ALTRETURNs if 
it is unsuccessful; it is otherwise identical to the read() function. 
If no data is available from a socket when read() is invoked, the action taken 
depends on the socket mode.  The mode of a socket is defined to be either 
"blocking" or "nonblocking".  If the socket is blocking (which is the default 
mode) the application is blocked (i.e., suspended) until data is received from 
the network.  If the socket is nonblocking, the condition is treated as an 
EWOULDBLOCK error. 
The mode of a socket can be changed with either fcntl() or ioctl(). 
If shutdown() has been invoked for this socket to inhibit reception of data, 
or if the peer is no longer connected, all read() operations are treated as if 
zero bytes of data were read. 
Errors: 
Following are the possible error conditions reported when the read() function 
is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C or PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOTCONN                E$NOTCONN 
The socket is not currently connected.  connect() has not been invoked. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
EWOULDBLOCK             E$WOULDBLOCK 
There is no data available from this nonblocking socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Reads data from a socket into multiple application-specified buffers. 
C Usage: 
    status = readv( s, &iovec[0], count ); 
PL6 Usage: 
    CALL XSL$READV( status, s, iovec, count ); 
Parameters: 
    s           integer socket descriptor 
    iovec       array of iovec structures 
    count       number of structures in iovec 
Results: 
    status      integer number of characters read or error code 
    iovec       array of iovec structures 
Description: 
The readv() function reads any available data from the socket into the 
specified buffers. 
The s parameter specifies the descriptor of the socket to be read from. 
The iovec parameter specifies an array of iovec or XSL$IOVEC structures 
framing the data buffers to receive the data to be read from the socket. 
The count parameter specifies the number of structures in the iovec array. 
If the readv() function is successful, the status result contains the number 
of characters read into the iovec buffers.  This number is non-negative.  A 
successful readv() returns all data available, up to the total size of the 
iovec buffers.  On datagram sockets, if the buffers are not large enough to 
receive the entire datagram, the excess will be discarded. 
If the readv() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$READV procedure additionally ALTRETURNs 
if it is unsuccessful; it is otherwise identical to the readv() function. 
If no data is available from a socket when readv() is invoked, the action 
taken depends on the socket mode.  The mode of a socket is defined to be 
either "blocking" or "nonblocking".  If the socket is blocking (which is the 
default mode) the application is blocked (i.e., suspended) until data is 
received from the network.  If the socket is nonblocking, the condition is 
treated as an EWOULDBLOCK error. 
The mode of a socket can be changed with either fcntl() or ioctl(). 
If shutdown() has been invoked for this socket to inhibit reception of data, 
or if the peer is no longer connected, all readv() operations are treated as 
if zero bytes of data were read. 
Errors: 
Following are the possible error conditions reported when the writev() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C or PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOTCONN                E$NOTCONN 
The socket is not currently connected.  connect() has not been invoked. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
EWOULDBLOCK             E$WOULDBLOCK 
There is no data available from this nonblocking socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Receives a message from a connected socket into an application-specified 
    buffer. 
C Usage: 
    status = recv( s, buf, len, flags ); 
PL6 Usage: 
    CALL XSL$RECV( status, s, buf, len, flags ); 
Parameters: 
    s           integer socket descriptor 
    buf         character array buffer 
    len         integer size of buf in characters 
    flags       integer bitflags of recv options 
Results: 
    status      integer number of characters received or error code 
    buf         character array buffer 
Description: 
The recv() function receives a message from a connected socket and places it 
in the buffer specified. 
The s parameter specifies the descriptor of the socket on which to receive. 
The buf parameter specifies an application-defined buffer to hold the message 
received from the socket. 
The len parameter specifies how large the buffer is, expressed as the number 
of characters it can hold. 
The flags parameter specifies recv options.  The desired options are 'OR-ed' 
together when coding the invocation.  The only options currently implemented 
are "out-of-band" and "peek".  The out-of-band option receives any message 
that was sent on the out-of-band data path if the socket supports it.  It is 
selected by coding MSG_OOB or %XSL_MSG_OOB in C or PL6 source, respectively. 
The peek option copies a message into the buffer, but additionally leaves it 
in the recv() queue so subsequent recv() invocations see the same message. It 
is selected by coding MSG_PEEK or %XSL_MSG_PEEK in C or PL6 source, 
respectively. 
If the recv() function is successful, the status result contains the number of 
characters received.  This number is non-negative.  On datagram sockets, if 
the buffer is not large enough to receive the entire message, the excess will 
be discarded. 
If the recv() function is unsuccessful, the status result contains EFAILURE or 
E$FAILURE and the application must inspect errno or XSL_ERRNO to determine the 
specific error condition.  The XSL$RECV procedure additionally ALTRETURNs if 
it is unsuccessful; it is otherwise identical to the recv() function. 
If no data is available from a socket when recv() is invoked, the action taken 
depends on the socket mode.  The mode of a socket is defined to be either 
"blocking" or "nonblocking".  If the socket is blocking (which is the default 
mode) the application is blocked (i.e., suspended) until a message is received 
from the network.  If the socket is nonblocking, the condition is treated as 
an EWOULDBLOCK error. 
The mode of a socket can be changed with either fcntl() or ioctl(). 
Recv() may be used only on sockets that have had connect() invoked. 
If shutdown() has been invoked for this socket to inhibit reception of data, 
or if the peer is no longer connected, all recv() operations are treated as if 
zero bytes of data were read. 
Errors: 
Following are the possible error conditions reported when the recv() function 
is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOTCONN                E$NOTCONN 
The connect() function has not been invoked for this socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
EWOULDBLOCK             E$WOULDBLOCK 
There is no data available from this nonblocking socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Receives a message from a socket into an application-specified buffer, 
    along with the address of the message's sender. 
C Usage: 
    status = recvfrom( s, buf, len, flags, from, fromlen ); 
PL6 Usage: 
    CALL XSL$RECVFROM( status, s, buf, len, flags, from, fromlen ); 
Parameters: 
    s           integer socket descriptor 
    buf         character array buffer 
    len         integer size of buf in characters 
    flags       integer bitflags of recvfrom options 
    from        sockaddr structure 
    fromlen     integer size of from in characters 
Results: 
    status      integer number of characters received or error code 
    buf         character array buffer 
    from        sockaddr structure with address of message's sender 
    fromlen     integer number of significant characters in from 
Description: 
The recvfrom() function receives a message from a connected socket and places 
it in the buffer specified.  Additionally, the network address of the 
message's sender is provided. 
The s parameter specifies the descriptor of the socket on which to receive. 
The buf parameter specifies an application-defined buffer to hold the message 
received from the socket. 
The len parameter specifies how large the buffer is, expressed as the number 
of characters it can hold. 
The flags parameter specifies recvfrom options.  The desired options are 
'ORed' together when coding the invocation.  The only options currently 
implemented are "out-of-band" and "peek".  The out-of-band option receives any 
message that was sent on the out-of-band data path if the socket supports it. 
It is selected by coding MSG_OOB or %XSL_MSG_OOB in C or PL6 source, 
respectively.  The peek option copies a message into the buffer, but 
additionally leaves it in the recvfrom() queue so subsequent recvfrom() 
invocations see the same message. It is selected by coding MSG_PEEK or 
%XSL_MSG_PEEK in C or PL6 source, respectively. 
The from parameter specifies an address buffer into which is placed the 
network address of the message's sender. 
The fromlen parameter specifies how large from is, expressed as the number of 
characters it can hold. 
If the recvfrom() function is successful, the status result contains the 
number of characters received.  This number is non-negative.  On datagram 
sockets, if the buffer is not large enough to receive the entire message, the 
excess will be discarded.  The network address of the message's sender is 
placed into from, and fromlen is set to the number of significant characters 
in from. 
If the recvfrom() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE and the application must inspect errno or XSL_ERRNO to 
determine the specific error condition.  The XSL$RECVFROM procedure 
additionally ALTRETURNs if it is unsuccessful; it is otherwise identical to 
the recvfrom() function. 
If no data is available from a socket when recvfrom() is invoked, the action 
taken depends on the socket mode.  The mode of a socket is defined to be 
either "blocking" or "nonblocking".  If the socket is blocking (which is the 
default mode) the application is blocked (i.e., suspended) until a message is 
received from the network.  If the socket is nonblocking, the condition is 
treated as an EWOULDBLOCK error. 
The mode of a socket can be changed with either fcntl() or ioctl(). 
Recvfrom() may be used on sockets regardless of whether connect() has been 
issued. 
If shutdown() has been invoked for this socket to inhibit reception of data, 
or if the peer is no longer connected, all recvfrom() operations are treated 
as if zero bytes of data were read. 
Errors: 
Following are the possible error conditions reported when the recvfrom() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
EWOULDBLOCK             E$WOULDBLOCK 
There is no data available from this nonblocking socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Receives a message from a socket into multiple application-specified 
    buffers, along with the address of the message's sender. 
C Usage: 
    status = recvmsg( s, msghdr, flags ); 
PL6 Usage: 
    CALL XSL$RECVMSG( status, s, msghdr, flags ); 
Parameters: 
    s           integer socket descriptor 
    msghdr      msghdr structure 
    flags       integer bitflags of recvmsg options 
Results: 
    status      integer number of characters received or error code 
    msghdr      msghdr structure 
Description: 
The recvmsg() function receives a message from a connected socket and places 
it in the buffers specified in the iovec array within msghdr.  Additionally, 
the network address of the message's sender is provided in msghdr. 
The s parameter specifies the descriptor of the socket on which to receive. 
The msghdr parameter specifies a msghdr or XSL$MSGHDR structure containing 
information specific to this invocation. 
The flags parameter specifies recvmsg options.  The desired options are 'ORed' 
together when coding the invocation.  The only options currently implemented 
are "out-of-band" and "peek".  The out-of-band option receives any message 
that was sent on the out-of-band data path if the socket supports it.  It is 
selected by coding MSG_OOB or %XSL_MSG_OOB in C or PL6 source, respectively. 
The peek option copies a message into the buffers, but additionally leaves it 
in the queue so subsequent recvmsg() invocations see the same message.  It is 
selected by coding MSG_PEEK or %XSL_MSG_PEEK in C or PL6 source, respectively. 
If the recvmsg() function is successful, the status result contains the number 
of characters received into the iovec buffers within msghdr.  This number is 
non-negative.  On datagram sockets, if the buffers are not large enough to 
receive the entire message, the excess will be discarded.  The network address 
of the message's sender is placed into the msg_name item within msghdr, and 
msg_namelen is set to the number of significant characters in msg_name. 
If the recvmsg() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$RECVMSG procedure additionally 
ALTRETURNs if it is unsuccessful; it is otherwise identical to the recvmsg() 
function. 
If no data is available from a socket when recvmsg() is invoked, the action 
taken depends on the socket mode.  The mode of a socket is defined to be 
either "blocking" or "nonblocking".  If the socket is blocking (which is the 
default mode) the application is blocked (i.e., suspended) until data is 
received from the network.  If the socket is nonblocking, the condition is 
treated as an EWOULDBLOCK error. 
The mode of a socket can be changed with either fcntl() or ioctl(). 
If shutdown() has been invoked for this socket to inhibit reception of data, 
or if the peer is no longer connected, all recvmsg() operations are treated as 
if zero bytes of data were read. 
Errors: 
Following are the possible error conditions reported when the recvmsg() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C or PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
EWOULDBLOCK             E$WOULDBLOCK 
There is no data available from this nonblocking socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    For specified sets of sockets, determines whether data is available for 
    reading, whether space is available for writing data, or whether an 
    exceptional condition is pending. 
C Usage: 
    status = select( numbits, rmask, wmask, emask, &timeout ); 
PL6 Usage: 
    CALL XSL$SELECT( status, numbits, rmask, wmask, emask, timeout ); 
Parameters: 
    numbits     integer number of significant bits in each mask 
    rmask       bit array of sockets to be checked for data available 
    wmask       bit array of sockets to be checked for space available 
    emask       bit array of sockets to be checked for exceptions 
    timeout     structure specifying time to delay before checking 
Results: 
    status      integer number of sockets selected by any mask 
    rmask       bit array of sockets with data available 
    wmask       bit array of sockets with space available 
    emask       bit array of sockets with pending exceptions 
Description: 
The numbits parameter specifies the number of significant bits in the three 
mask parameters rmask, wmask, and emask.  Each mask is a bit array whose bits 
correspond one to one with the application's DCBs.  Since sockets are DCBs 
(plus other context), the masks can be used to specify which sockets are to be 
checked for the various conditions.  Any mask bits that correspond to DCBs not 
currently in use as sockets are ignored.  Also note that since bits in the 
masks are numbered from zero, numbits must be one plus the highest-numbered 
DCB specified in any mask. 
It is not necessary to specify all three masks.  Coding zero for any mask 
effectively causes it to be unspecified.  In PL6 source, omitting a mask from 
the argument list has the same effect. 
Application programmers using C can make use of the following macros to help 
with bitmask manipulation.  The number of bits allowed in a bitmask is given 
by FD_SETSIZE. 
FD_ZERO( &bitmask ) 
   Initializes a bitmask to all zeroes. 
FD_CLR( bit, &bitmask ) 
   Clears the specified bit in the bitmask. 
FD_SET( bit, &bitmask ) 
   Sets the specified bit in the bitmask. 
FD_ISSET( bit, &bitmask ) 
   Returns true if the specified bit is set in the bitmask. 
The optional rmask parameter specifies which sockets are to be checked for 
available data.  On return from select(), only bits of rmask that correspond 
to sockets that have data available are set to 1.  If data is available for a 
given socket, then a read() of the socket is guaranteed not to block. 
The optional wmask parameter specifies which sockets are to be checked for 
space available to write data.  On return from select(), only bits of wmask 
that correspond to sockets with space available are set to 1.  If space is 
available for a given socket, then a write() to the socket is guaranteed not 
to block, so far as CP-6 Host to FEP throttling allows. 
The optional emask parameter specifies which sockets are to be checked for an 
exceptional condition.  On return from select(), only bits of emask that 
correspond to sockets that have an exceptional condition are set to 1. 
The optional timeout parameter specifies how long to delay before checking for 
the selected conditions.  If specified, timeout is a structure with two 
elements: an integer number of seconds from 0 to 32767 and an integer number 
of microseconds.  If timeout is not specified, a delay of 86399 seconds (one 
second short of a day) is performed.  The delay is terminated if the condition 
of any of the selected sockets changes, and the result masks are set 
appropriately. 
The timeout parameter is regarded as unspecified in C source by coding NULL in 
its place.  In PL6 source it can simply be omitted from the argument list. 
If the select() function is successful, the status result is the number of 
sockets with any of the selected conditions. 
If the select() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE.  The XSL$SELECT procedure additionally ALTRETURNs if it is 
unsuccessful; it is otherwise identical to the select() function. 
In the case of unsuccessful select(), the mask parameters are unchanged. 
Errors: 
Any error conditions reported by select() can be assumed to be the result of 
earlier socket operations.  The select() function does not diagnose any error 
conditions itself. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Sends a message from an application-specified buffer to a connected 
    socket. 
C Usage: 
    status = send( s, msg, len, flags ); 
PL6 Usage: 
    CALL XSL$SEND( status, s, msg, len, flags ); 
Parameters: 
    s           integer socket descriptor 
    msg         character array containing message to be sent 
    len         integer number of significant characters in msg 
    flags       integer bitflags of send options 
Result: 
    status      integer number of characters sent or error code 
Description: 
The send() function sends a message from an application-defined buffer to a 
socket.  On datagram sockets the message is sent atomically; if this is not 
possible then the error EMSGSIZE is reported. 
The s parameter specifies the descriptor of the socket to be written to. 
The msg parameter specifies an application-defined buffer containing the 
message to be sent to the socket. 
The len parameter specifies the number of characters to be sent. 
The flags parameter specifies send options.  The only option currently 
implemented is "out-of-band", which causes the message to be sent on the 
out-of-band data path if the socket supports it.  This is selected by coding 
SOF_OOB or %XSL_SOF_OOB in C or PL6 source, respectively. 
If the send() function is successful, the status result contains the number of 
characters sent to the socket.  This number is non-negative.  A successful 
result does not guarantee that the message was delivered, but only that it was 
sent to the FEP for network transmission.  The status value may be less than 
the len value if the socket is nonblocking and no more data could be 
immediately sent. 
If the send() function is unsuccessful, the status result contains EFAILURE or 
E$FAILURE and the application must inspect errno or XSL_ERRNO to determine the 
specific error condition.  The XSL$SEND procedure additionally ALTRETURNs if 
it is unsuccessful; it is otherwise identical to the send() function. 
Send() may be used only on sockets that have had connect() invoked. 
If shutdown() has been invoked for this socket to inhibit transmission of 
data, all send() operations report the error ESHUTDOWN. 
Errors: 
Following are the possible error conditions reported when the send() function 
is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
EMSGSIZE                E$MSGSIZE 
The specified message is too long to send atomically. 
ENOTBOUND               E$NOTBOUND 
The socket is not bound to a FEP. 
ENOTCONN                E$NOTCONN 
The connect() function has not been invoked for this socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
ESHUTDOWN               E$SHUTDOWN 
Can't send after socket shutdown. 
EWOULDBLOCK             E$WOULDBLOCK 
The message cannot be immediately sent. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Sends a message from multiple application-specified buffers to a socket. 
    This function is typically used when the destination socket changes from 
    invocation to invocation. 
C Usage: 
    status = sendmsg( s, &msghdr, flags ); 
PL6 Usage: 
    CALL XSL$SENDMSG( status, s, msghdr, flags ); 
Parameters: 
    s           integer socket descriptor 
    msghdr      msghdr structure 
    flags       integer bitflags of sendmsg options 
Result: 
    status      integer number of characters sent or error code 
Description: 
The sendmsg() function sends a message from multiple application-defined 
buffers to a socket.  On datagram sockets the message is sent atomically; if 
this is not possible then the error EMSGSIZE is reported. 
The s parameter specifies the descriptor of the socket to be written to. 
The msghdr parameter specifies a msghdr or XSL$MSGHDR structure containing 
information specific to this invocation. 
The flags parameter specifies sendmsg options.  The only option currently 
implemented is "out-of-band", which causes the message to be sent on the 
out-of-band data path if the socket supports it.  This is selected by coding 
MSG_OOB or %XSL_MSG_OOB in C or PL6 source, respectively. 
If the sendmsg() function is successful, the status result contains the number 
of characters sent to the socket.  This number is non-negative.  A successful 
result does not guarantee that the message was delivered, but only that it was 
sent to the FEP for network transmission.  The status value may be less than 
the total number of characters in the iovec buffers within msghdr if the 
socket is nonblocking and no more data could be immediately sent. 
If the sendmsg() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$SENDMSG procedure additionally 
ALTRETURNs if it is unsuccessful; it is otherwise identical to the sendmsg() 
function. 
Sendmsg() may be used on sockets regardless of whether connect() has been 
issued. 
If shutdown() has been invoked for this socket to inhibit transmission of 
data, all sendmsg() operations report the error ESHUTDOWN. 
Errors: 
Following are the possible error conditions reported when the sendmsg() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C or PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
EMSGSIZE                E$MSGSIZE 
The specified buffers are too long to send atomically. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
ESHUTDOWN               E$SHUTDOWN 
Can't send after socket shutdown. 
EWOULDBLOCK             E$WOULDBLOCK 
The data cannot be immediately sent. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Sends a message from an application-specified buffer to a socket.  This 
    function is typically used when the destination socket changes from 
    invocation to invocation. 
C Usage: 
    status = sendto( s, msg, len, flags, to, tolen ); 
PL6 Usage: 
    CALL XSL$SENDTO( status, s, msg, len, flags, to, tolen ); 
Parameters: 
    s           integer socket descriptor 
    msg         character array containing message to be sent 
    len         integer number of significant characters in msg 
    flags       integer bitflags of sendto options 
    to          sockaddr structure 
    tolen       integer size of to in characters 
Result: 
    status      integer number of characters sent or error code 
Description: 
The sendto() function sends a message from an application-defined buffer to a 
socket.  On datagram sockets the message is sent atomically; if this is not 
possible then the error EMSGSIZE is reported. 
The s parameter specifies the descriptor of the socket to be written to. 
The msg parameter specifies an application-defined buffer containing the 
message to be sent to the socket. 
The len parameter specifies the number of characters to be sent. 
The flags parameter specifies sendto options.  The only option currently 
implemented is "out-of-band", which causes the message to be sent on the 
out-of-band data path if the socket supports it.  This is selected by coding 
SOF_OOB or %XSL_SOF_OOB in C or PL6 source, respectively. 
The to parameter specifies the address of the remote socket to receive the 
message.  In C source, it is a sockaddr structure.  In PL6 source, it is an 
XSL$SOCKADDR structure. 
The tolen parameter specifies the number of significant characters in to. 
If the sendto() function is successful, the status result contains the number 
of characters sent to the socket.  This number is non-negative.  A successful 
result does not guarantee that the message was delivered, but only that it was 
sent to the FEP for network transmission.  The status value may be less than 
the len value if the socket is nonblocking and no more data could be 
immediately sent. 
If the sendto() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$SENDTO procedure additionally 
ALTRETURNs if it is unsuccessful; it is otherwise identical to the sendto() 
function. 
Sendto() may be used on sockets regardless of whether connect() has been 
issued. 
If shutdown() has been invoked for this socket to inhibit transmission of 
data, all sendto() operations report the error ESHUTDOWN. 
Errors: 
Following are the possible error conditions reported when the sendto() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
EMSGSIZE                E$MSGSIZE 
The message is too long to send atomically. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
ESHUTDOWN               E$SHUTDOWN 
Can't send after socket shutdown. 
EWOULDBLOCK             E$WOULDBLOCK 
The message cannot be immediately sent. 
00001
00005
00006
00003
00002
00004
The servent structure is a template for the information returned by the Socket 
Library functions that deal with the etc:services.:SYS file. 
s_aliases - (char **) 
     Points at an array of pointers to character strings.  Each character 
     string contains an alias of the service name, and is terminated by a NUL 
     byte.  The array of pointers is terminated by a NULL pointer. 
s_name - (char *) 
     Points at a character string containing the service name.  The string is 
     terminated by a NUL byte. 
s_port - (int) 
     Specifies the port at which this service is accessed. 
s_proto - (char *) 
     Points at a character string containing the name of the protocol used to 
     access this service.  The character string is terminated by a NUL byte. 
                                   servent 
        0   1   2   3 
      +---+---+---+---+ 
   .0 |   |   |   |   | struct servent { 
   .0 |ppp|ppp|ppp|ppp|   char *s_name; 
   .1 |ppp|ppp|ppp|ppp|   char **s_aliases; 
   .2 |sss|sss|sss|sss|   int s_port; 
   .3 |ppp|ppp|ppp|ppp|   char *s_proto; 
      +---+---+---+---+   }; 
        0   1   2   3     .4-0-0 total length 
Purpose: 
    Opens or positions the etc:hosts file and initializes a stay-open flag. 
C Usage: 
    ptr = sethostent( flag ); 
PL6 Usage: 
    CALL XSL$SETHOSTENT( ptr, flag ); 
Parameters: 
    flag        integer flag 
Result: 
    ptr         pointer to arbitrary location 
Description: 
The sethostent() function opens the etc:hosts file, if it is not already open, 
and positions it to the beginning.  A flag internal to the socket library is 
initialized from the flag parameter. 
The flag parameter specifies whether the etc:hosts file is to remain open 
after use by any of the hosts file manipulation functions.  If the flag is 
nonzero the file will be kept open. 
If the sethostent() function is successful, the ptr result contains an 
arbitrary non-NULL value. 
If the sethostent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while opening or positioning 
the etc:hosts file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Opens or positions the etc:networks file and initializes a stay-open flag. 
C Usage: 
    ptr = setnetent( flag ); 
PL6 Usage: 
    CALL XSL$SETNETENT( ptr, flag ); 
Parameters: 
    flag        integer flag 
Result: 
    ptr         pointer to arbitrary location 
Description: 
The setnetent() function opens the etc:networks file, if it is not already 
open, and positions it to the beginning.  A flag internal to the socket 
library is initialized from the flag parameter. 
The flag parameter specifies whether the etc:networks file is to remain open 
after use by any of the networks file manipulation functions.  If the flag is 
nonzero the file will be kept open. 
If the setnetent() function is successful, the ptr result contains an 
arbitrary non-NULL value. 
If the setnetent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while opening or positioning 
the etc:networks file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Opens or positions the etc:protocols file and initializes a stay-open 
    flag. 
C Usage: 
    ptr = setprotoent( flag ); 
PL6 Usage: 
    CALL XSL$SETPROTOENT( ptr, flag ); 
Parameters: 
    flag        integer flag 
Result: 
    ptr         pointer to arbitrary location 
Description: 
The setprotoent() function opens the etc:protocols file, if it is not already 
open, and positions it to the beginning.  A flag internal to the socket 
library is initialized from the flag parameter. 
The flag parameter specifies whether the etc:protocols file is to remain open 
after use by any of the protocols file manipulation functions.  If the flag is 
nonzero the file will be kept open. 
If the setprotoent() function is successful, the ptr result contains an 
arbitrary non-NULL value. 
If the setprotoent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while opening or positioning 
the etc:protocols file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Opens or positions the etc:services file and initializes a stay-open flag. 
C Usage: 
    ptr = setservent( flag ); 
PL6 Usage: 
    CALL XSL$SETSERVENT( ptr, flag ); 
Parameters: 
    flag        integer flag 
Result: 
    ptr         pointer to arbitrary location 
Description: 
The setservent() function opens the etc:services file, if it is not already 
open, and positions it to the beginning.  A flag internal to the socket 
library is initialized from the flag parameter. 
The flag parameter specifies whether the etc:services file is to remain open 
after use by any of the services file manipulation functions.  If the flag is 
nonzero the file will be kept open. 
If the setservent() function is successful, the ptr result contains an 
arbitrary non-NULL value. 
If the setservent() function is unsuccessful, the ptr result contains a NULL 
pointer. 
Errors: 
A NULL pointer is returned if any error occurs while opening or positioning 
the etc:services file. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Modifies the current setting of an option at one of the internal protocol 
    levels supporting a socket. 
C Usage: 
    status = setsockopt( s, level, optname, &optval, optlen ); 
PL6 Usage: 
    CALL XSL$SETSOCKOPT( status, s, level, optname, optval, optlen ); 
Parameters: 
    s           integer socket descriptor 
    level       integer protocol number 
    optname     integer option name 
    optval      address of option value 
    optlen      integer number of significant characters in optval 
Result: 
    status      integer error code 
Description: 
The setsockopt() function modifies the current setting of any option at any 
internal protocol level supporting an existing socket. 
The s parameter specifies the descriptor of the socket of interest. 
The level parameter specifies the protocol level managing the option of 
interest.  "Socket" level is specified by coding SOL_SOCKET or %XSL_SOL_SOCKET 
in C or PL6 source, respectively.  Other levels are specified by using a 
protocol number from the include files <xsl_socket.h> or XSL_SOCKET_E, 
respectively. 
The optname parameter specifies the option of interest.  For "socket" level 
this is coded using one of the SO_ #defines or %XSL_SO_ equates which are 
defined in the include file <xsl_socket.h> or XSL_SOCKET_E.  These options are 
listed in the following table. 
  C #define        PL6 %EQU               Meaning 
SO_ACCEPTCONN    XSL_SO_ACCEPTCONN      Socket has had listen(). 
SO_BLOCKING      XSL_SO_BLOCKING        Blocking option. 
SO_BROADCAST     XSL_SO_BROADCAST       Allow broadcast messages. 
SO_DEBUG         XSL_SO_DEBUG           Record debugging information. 
SO_DONTROUTE     XSL_SO_DONTROUTE       Just use Interface address. 
SO_ERROR         XSL_SO_ERROR           Get error status and clear. 
SO_IMASOCKET     XSL_SO_IMASOCKET       Reserved for DPX/2-300 Kernel. 
SO_KEEPALIVE     XSL_SO_KEEPALIVE       Keep connections alive. 
SO_LINGER        XSL_SO_LINGER          Linger on close if data present. 
SO_NWREADS       XSL_SO_NWREADS         Max pending NoWait read count. 
SO_NWBUFFS       XSL_SO_NWBUFFS         Max pending buffer count. 
SO_OOBINLINE     XSL_SO_OOBINLINE       Leave received OOB data in line. 
SO_ORDREL        XSL_SO_ORDREL          Perform orderly release. 
SO_RCVBUF        XSL_SO_RCVBUF          Receive buffer size. 
SO_RCVLOWAT      XSL_SO_RCVLOWAT        Receive low-water mark. 
SO_RCVTIMEO      XSL_SO_RCVTIMEO        Receive timeout value. 
SO_REUSEADDR     XSL_SO_REUSEADDR       Allow local address reuse. 
SO_SNDBUF        XSL_SO_SNDBUF          Send buffer size. 
SO_SNDLOWAT      XSL_SO_SNDLOWAT        Send low-water mark. 
SO_SNDTIMEO      XSL_SO_SNDTIMEO        Send timeout value. 
SO_TYPE          XSL_SO_TYPE            Get socket type. 
SO_USELOOPBACK   XSL_SO_USELOOPBACK     Bypass hardware when possible. 
The optval parameter specifies an application-defined buffer containing the 
new setting of the option. 
The optlen parameter specifies the number of significant characters in optval. 
If the setsockopt() function is successful, the status result contains 
ESUCCESS or E$SUCCESS. 
If the setsockopt() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE and the application must inspect errno or XSL_ERRNO to 
determine the specific error condition.  The XSL$SETSOCKOPT procedure 
additionally ALTRETURNs if it is unsuccessful; it is otherwise identical to 
the setsockopt() function. 
If the socket is not bound to a FEP, only level SOL_SOCKET and optname 
SO_REUSEADDR can be specified.  If the socket is bound to a FEP, then level 
SOL_SOCKET and optnames SO_NWBUFFS, SO_NWREADS, and SO_OOBINLINE are processed 
by the Socket Library; all other combinations of level and optname are 
processed by the FEP. 
Errors: 
Following are the possible error conditions reported when the setsockopt() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
ENOPROTOOPT             E$NOPROTOOPT 
The option specified in optname is not recognized by protocol level. 
ENOTBOUND               E$NOTBOUND 
Socket is not bound to a FEP. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Inhibits either or both the sending and receiving of data through a 
    socket. 
C Usage: 
    status = shutdown( s, how ); 
PL6 Usage: 
    CALL XSL$SHUTDOWN( status, s, how ); 
Parameters: 
    s           integer socket descriptor 
    how         integer shutdown type 
Result: 
    status      integer error code 
Description: 
The shutdown() function provides for the inhibiting of data reception or data 
transmission, or both, for the specified socket. 
The s parameter specifies the descriptor of the socket to be modified. 
The how parameter specifies how the socket is to be modified.  If how is 0, 
reception is inhibited.  If how is 1, transmission is inhibited.  If how is 2, 
both reception and transmission are inhibited. 
If the shutdown() function is successful, the status result contains ESUCCESS 
or E$SUCCESS. 
If the shutdown() function is unsuccessful, the status result contains 
EFAILURE or E$FAILURE and the application must inspect errno or XSL_ERRNO to 
determine the specific error condition.  The XSL$SHUTDOWN procedure 
additionally ALTRETURNs if it is unsuccessful; it is otherwise identical to 
the shutdown() function. 
There is no facility to re-enable data reception or transmission once they 
have been inhibited by shutdown(). 
If data reception has been inhibited, all subsequent invocations of read(), 
recv(), and recvfrom() on the selected socket act as if zero bytes of data 
were received. 
If data transmission has been inhibited, all subsequent invocations of 
write(), send(), and sendto() on the selected socket report the error 
ESHUTDOWN. 
Errors: 
Following are the possible error conditions reported when the shutdown() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
EFAULT                  E$FAULT 
The how parameter is invalid (not 0, 1, or 2). 
ENOTCONN                E$NOTCONN 
The connect() function has not been invoked on this socket. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
00001
00005
00006
00003
00002
00004
The sockaddr structure is a generic address template for Socket Library 
applications.  The two parts of the generic address are the family and data. 
The specific value in the family part determines how to interpret the data 
part.  One family in particular (AF_INET) is used so widely that a separate 
structure is defined for it:  sockaddr_in. 
sa_data - (char) 
     Specifies the individual bytes of an address.  The meaning of the bytes 
     is determined by the 'family' item of the structure.  Up to 16 bytes can 
     be specified. 
sa_family - (unsigned short) 
     Specifies the address family that this address belongs to.  The value 
     determines how the 'data' item is to be interpreted.  Equates for the 
     possible values can be found in <xsl_socket.h>. 
                                   sockaddr 
        0   1   2   3 
      +---+---+---+---+ 
   .0 |   |   |   |   | struct sockaddr { 
   .0 |uuu|uuu|uuu|uuu|   unsigned short sa_family; 
   .1 |ccc|   |   |   |   char sa_data[16]; 
      Z   Z   Z   Z   Z 
      +---+---+---+---+   }; 
        0   1   2   3     .5-0-0 total length 
The sockaddr_in structure is an instance of the sockaddr structure useful for 
addresses in the AF_INET (Internet) family.  This family of addresses is used 
so frequently that it deserves its own address structure. 
sin_addr - (struct in_addr) 
     Specifies the Internet address.  It is a 32-bit integer unpacked into the 
     lower eight bits of four successive bytes.  For more information about 
     Internet addresses, please refer to the topic INTERNET_ADDRESS. 
     The in_addr structure is used to store the IP address in network byte 
     order. 
         struct in_addr { 
         unsigned long s_addr; 
         }; 
sin_family - (short) 
     Specifies the address family that this address belongs to.  Addresses in 
     the Internet family specify the value AF_INET or %XSL_AF_INET in C or PL6 
     source, respectively.  Addresses in the Internet family specify the value 
     AF_INET for this item. 
sin_port - (unsigned short) 
     Specifies the port within a specific host through which some application 
     can be accessed.  Equates for the so-called 'well-known' ports can be 
     found in etc:services.:SYS.  User applications can make use of any 
     non-conflicting port number; port numbers below 1024 are reserved for 
     system applications. 
                                 sockaddr_in 
        0   1   2   3 
      +---+---+---+---+ 
   .0 |   |   |   |   | struct sockaddr_in { 
   .0 |sss|sss|sss|sss|   short sin_family; 
   .1 |uuu|uuu|uuu|uuu|   unsigned short sin_port; 
   .2 |bbb|bbb|bbb|bbb|   struct in_addr sin_addr; 
   .3 |ccc|   |   |   |   char sin_zero[8]; 
      Z   Z   Z   Z   Z 
   .4 |   |   |...|...| 
      +---+---+---+---+   }; 
        0   1   2   3     .5-0-0 total length 
Purpose: 
    Creates a new socket, to allow communication with another socket elsewhere 
    in a network. 
C Usage: 
    s = socket( af, type, protocol ); 
PL6 Usage: 
    CALL XSL$SOCKET( s, af, type, protocol ); 
Parameters: 
    af          integer address format 
    type        integer socket type 
    protocol    integer protocol number 
Result: 
    s           integer socket descriptor or error code 
Description: 
The socket() function creates an endpoint for communication, and returns a 
descriptor used by other socket library functions for this communication. 
The af parameter specifies the address format to use when processing network 
addresses in later operations on this socket.  Equates for the possible values 
can be found in <xsl_socket.h> or XSL_SOCKET_E.  Only the "Internet" address 
format is currently supported; it is selected by coding AF_INET or 
%XSL_AF_INET in C or PL6 source, respectively.  The complete list of possible 
address formats is shown below. 
  C #define        PL6 %EQU          Meaning 
AF_APPLETALK     XSL_AF_APPLETALK  AppleTalk. 
AF_CCITT         XSL_AF_CCITT      CCITT protocols, X.25, etc. 
AF_CHAOS         XSL_AF_CHAOS      MIT CHAOS protocols. 
AF_DATAKIT       XSL_AF_DATAKIT    Datakit protocols. 
AF_DECnet        XSL_AF_DECNET     DECnet. 
AF_DLI           XSL_AF_DLI        Direct data link interface. 
AF_ECMA          XSL_AF_ECMA       European Comp. Manufacturers Assoc. 
AF_HYLINK        XSL_AF_HYLINK     NSC Hyperchannel. 
AF_IMPLINK       XSL_AF_IMPLINK    Arpanet IMP address. 
AF_INET          XSL_AF_INET       Internet:  UDP, TCP, etc. 
AF_LAT           XSL_AF_LAT        Local Area Transport (LAT). 
AF_NBS           XSL_AF_NBS        NBS protocols. 
AF_NS            XSL_AF_NS         XEROX NS protocols. 
AF_PUP           XSL_AF_PUP        PUP protocols, e.g., BSP. 
AF_SNA           XSL_AF_SNA        IBM SNA. 
AF_UNIX          XSL_AF_UNIX       Local to UNIX host (pipes, portals). 
The type parameter specifies how communication is to be performed for this 
socket.  Equates for the possible values can be found in <xsl_socket.h> or 
XSL_SOCKET_E.  Only "stream", "datagram", and "raw" socket types are currently 
supported.  Stream type is selected by coding SOCK_STREAM or %XSL_SOCK_STREAM 
in C or PL6 source, respectively.  Datagram type is selected by coding 
SOCK_DGRAM or %XSL_SOCK_DGRAM in C or PL6 source, respectively.  Raw type is 
selected by coding SOCK_RAW or %XSL_SOCK_RAW in C or PL6 source, respectively. 
The complete list of possible types is shown in the table below. 
  C #define        PL6 %EQU               Meaning 
SOCK_DGRAM       XSL_SOCK_DGRAM         Datagram socket. 
SOCK_RAW         XSL_SOCK_RAW           Raw protocol interface. 
SOCK_RDM         XSL_SOCK_RDM           Reliably-delivered message. 
SOCK_SEQPACKET   XSL_SOCK_SEQPACKET     Sequenced packet stream. 
SOCK_STREAM      XSL_SOCK_STREAM        Stream socket. 
The protocol parameter specifies which protocol family to use for 
communication on this socket.  There are potentially many protocol families 
available for each address format selected.  Equates for the possible values 
can be found in <xsl_socket.h> or XSL_SOCKET_E.  Only "Internet" protocol is 
currently supported; it is selected by coding PF_INET or %XSL_PF_INET in C or 
PL6 source, respectively.  The value 0 is also permitted; it specifies use of 
the default protocol for the selected address format.  The complete list of 
possible protocol families is shown below. 
  C #define        PL6 %EQU          Meaning 
PF_APPLETALK     XSL_PF_APPLETALK  AppleTalk. 
PF_CCITT         XSL_PF_CCITT      CCITT protocols, X.25, etc. 
PF_CHAOS         XSL_PF_CHAOS      MIT CHAOS protocols. 
PF_DATAKIT       XSL_PF_DATAKIT    Datakit protocols. 
PF_DECnet        XSL_PF_DECNET     DECnet. 
PF_DLI           XSL_PF_DLI        Direct data link interface. 
PF_ECMA          XSL_PF_ECMA       European Comp. Manufacturers Assoc. 
PF_HYLINK        XSL_PF_HYLINK     NSC Hyperchannel. 
PF_IMPLINK       XSL_PF_IMPLINK    Arpanet IMP address. 
PF_INET          XSL_PF_INET       Internet:  UDP, TCP, etc. 
PF_LAT           XSL_PF_LAT        Local Area Transport (LAT). 
PF_NBS           XSL_PF_NBS        NBS protocols. 
PF_NS            XSL_PF_NS         XEROX NS protocols. 
PF_PUP           XSL_PF_PUP        PUP protocols, e.g., BSP. 
PF_SNA           XSL_PF_SNA        IBM SNA. 
PF_UNIX          XSL_PF_UNIX       Local to UNIX host (pipes, portals). 
If the socket() function is successful, the s result contains the descriptor 
for a new socket with the selected attributes.  The descriptor is a small 
non-negative integer, equivalent to the DCBNUM of the DCB allocated for this 
socket. 
If the socket() function is unsuccessful, the s result contains EFAILURE or 
E$FAILURE and the application must inspect errno or XSL_ERRNO to determine the 
specific error condition.  The XSL$SOCKET procedure additionally ALTRETURNs if 
it is unsuccessful; it is otherwise identical to the socket() function. 
Errors: 
Following are the possible error conditions reported when the socket() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C and PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EAFNOSUPPORT            E$AFNOSUPPORT 
The selected address format is not currently supported. 
EMFILE                  E$MFILE 
M$GETDCB failed.  Unable to allocate DCB for this socket. 
ENOBUFFS                E$NOBUFFS 
No buffer space is available. 
EPROTONOSUPPORT         E$PROTONOSUPPORT 
The selected protocol family is not currently supported. 
ESOCKTNOSUPPORT         E$SOCKTNOSUPPORT 
The selected socket type is not currently supported. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Writes data from an application-specified buffer to a socket. 
C Usage: 
    status = write( s, buf, len ); 
PL6 Usage: 
    CALL XSL$WRITE( status, s, buf, len ); 
Parameters: 
    s           integer socket descriptor 
    buf         character array buffer 
    len         integer number of significant characters in buf 
Result: 
    status      integer number of characters written or error code 
Description: 
The write() function writes data from the specified buffer to the socket.  On 
datagram sockets the data is written atomically; if this is not possible then 
the error EMSGSIZE is reported. 
The s parameter specifies the descriptor of the socket to be written to. 
The buf parameter specifies an application-defined buffer containing the data 
to be written to the socket. 
The len parameter specifies the number of characters to be written. 
If the write() function is successful, the status result contains the number 
of characters written to the socket.  This number is non-negative.  A 
successful result does not guarantee that the data was delivered, but only 
that it was sent to the FEP for network transmission.  The status value may be 
less than the len value if the socket is nonblocking and no more data could be 
immediately sent. 
If the write() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$WRITE procedure additionally ALTRETURNs 
if it is unsuccessful; it is otherwise identical to the write() function. 
Write() may be used only on sockets that have had connect() invoked. 
If shutdown() has been invoked for this socket to inhibit transmission of 
data, all write() operations report the error ESHUTDOWN. 
Errors: 
Following are the possible error conditions reported when the write() function 
is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C or PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
EMSGSIZE                E$MSGSIZE 
The specified buffer is too long to send atomically. 
ENOTBOUND               E$NOTBOUND 
The socket is not bound to a FEP. 
ENOTCONN                E$NOTCONN 
The socket is not currently connected.  connect() has not been invoked. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
ESHUTDOWN               E$SHUTDOWN 
Can't send after socket shutdown. 
EWOULDBLOCK             E$WOULDBLOCK 
The data cannot be immediately sent. 
00001
00005
00006
00003
00002
00004
Purpose: 
    Writes data from multiple application-specified buffers to a socket. 
C Usage: 
    status = writev( s, &iovec[0], count ); 
PL6 Usage: 
    CALL XSL$WRITEV( status, s, iovec, count ); 
Parameters: 
    s           integer socket descriptor 
    iovec       array of iovec structures 
    count       number of structures in iovec 
Result: 
    status      integer number of characters written or error code 
Description: 
The writev() function writes data from the specified buffers to the socket. 
On datagram sockets the data is written atomically; if this is not possible 
then the error EMSGSIZE is reported. 
The s parameter specifies the descriptor of the socket to be written to. 
The iovec parameter specifies an array of iovec or XSL$IOVEC structures 
framing the data buffers to be written to the socket. 
The count parameter specifies the number of structures in the iovec array. 
If the writev() function is successful, the status result contains the number 
of characters written to the socket.  This number is non-negative.  A 
successful result does not guarantee that the data was delivered, but only 
that it was sent to the FEP for network transmission.  The status value may be 
less than the total number of characters in the iovec buffers if the socket is 
nonblocking and no more data could be immediately sent. 
If the writev() function is unsuccessful, the status result contains EFAILURE 
or E$FAILURE and the application must inspect errno or XSL_ERRNO to determine 
the specific error condition.  The XSL$WRITEV procedure additionally 
ALTRETURNs if it is unsuccessful; it is otherwise identical to the writev() 
function. 
Writev() may be used only on sockets that have had connect() invoked. 
If shutdown() has been invoked for this socket to inhibit transmission of 
data, all writev() operations report the error ESHUTDOWN. 
Errors: 
Following are the possible error conditions reported when the writev() 
function is unsuccessful.  Equates for the possible values can be found in 
<xsl_errno.h> or XSL_PERR_C for C or PL6 source, respectively. 
C #define               PL6 %EQU 
----------------------- ----------------------- 
EBADF                   E$BADF 
The descriptor s is not appropriate to identify a socket. 
EMSGSIZE                E$MSGSIZE 
The specified buffers are too long to send atomically. 
ENOTBOUND               E$NOTBOUND 
The socket is not bound to a FEP. 
ENOTCONN                E$NOTCONN 
The socket is not currently connected.  connect() has not been invoked. 
ENOTSOCK                E$NOTSOCK 
The descriptor s is no longer valid to identify a socket. 
ESHUTDOWN               E$SHUTDOWN 
Can't send after socket shutdown. 
EWOULDBLOCK             E$WOULDBLOCK 
The data cannot be immediately sent. 
00001
00005
00006
00003
00002
00004
The xsl_sockinit structure collects together various parameters that are used 
to initialize the Socket Library.  If no special action is taken by the 
application (see below), defaults are used for initialization at the first use 
of socket() or XSL$SOCKET.  To override the defaults, the application calls 
XSL$SOCKINIT passing a xsl_sockinit structure with new parameters.  To have 
any effect, the call to XSL$SOCKINIT must precede any call to socket() or 
XSL$SOCKET. 
bufsize - (unsigned long) 
     Specifies the number of bytes of memory to reserve for each NoWait I/O 
     buffer.  Valid values are 1 to 4096.  The larger the buffer size, the 
     better.  Larger than 4096 is pointless because that is the limiting size 
     for data transfers between FEP and host.  I/O buffers are allocated at 
     Socket Library initialization and are shared among all NoWait sockets, 
     subject to each socket's current MAXRDS and MAXBUF values. 
evnt$ - (void *)() 
     Specifies the address of a PL6 PROC to handle non-Socket Library events 
     received by the Socket Library.  The named procedure should be coded as a 
     normal PROC (not PROC ASYNC) that receives one parameter, a B$EXCFR 
     structure. 
maxbuf - (unsigned :18) 
     Specifies the number of additional buffers to allocate to each NoWait 
     socket.  Valid values are 0 to 262143.  If nonzero, the value specifies 
     how many I/O buffers, above those in use by pending NoWait reads, should 
     be reserved for each socket.  This parameter is inherited by each socket 
     on creation.  A socket's copy of MAXBUF can be modified by using 
     XSL$SETSOCKOPT, specifying option XSL_SO_NWBUFFS.  (C programmers can use 
     setsockopt() with option SO_NWBUFFS.) 
     MAXBUF buffers may be useful in situations where the application needs to 
     be responsive to the network but cannot process incoming data as it 
     arrives.  It provides more buffering than possible with MAXRDS alone. 
maxrds - (unsigned :18) 
     Specifies the maximum number of NoWait reads allowed on each socket. 
     Valid values are 0 to 3.  0 specifies that NoWait I/O is not to be used. 
     If nonzero, the value specifies how many I/O buffers to reserve for 
     pending NoWait reads, as well as how many simultaneous NoWait reads to 
     issue when the application requests data from the network.  This 
     parameter is inherited by each socket on creation.  A socket's copy of 
     MAXRDS can be modified by using XSL$SETSOCKOPT specifying option 
     XSL_SO_NWREADS.  (C programmers can use setsockopt() with option 
     SO_NWREADS.) 
     Converting a socket from NoWait-capable to non-NoWait-capable is possible 
     by setting the socket's MAXRDS value to zero.  The inverse operation is 
     not possible because the value of MAXRDS is used when the socket DCB is 
     opened to determine whether B$COMIO events should be delivered to the 
     library for that socket.  However, it is always possible to adjust a 
     socket's MAXRDS value from one nonzero value to another nonzero value. 
maxsock - (unsigned long) 
     Specifies the maximum number of sockets that will be in use at any one 
     time.  Valid values are 1 to 36.  The CP-6 LINK option DCBSLOTS may need 
     to be used to reserve space for DCBs associated with the sockets.  One 
     DCB is required for each socket in use. 
mem$ - (void *) 
     Points at an area of application-managed memory that the Socket Library 
     will use for its socket context.  If not specified, the library will 
     allocate space out of the next available data segment.  The number of 
     words of memory space required can be computed as shown below in 
     pseudo-code. 
     TOTAL = 68;  // for segment head and event log 
     TOTAL = TOTAL + 21*MAXSOCK;  // add pointer array and sockets 
     TOTAL = TOTAL + 1+B$ROSEG.NUMDCBS;  // add DCBNUM-to-socket map 
     IF NWSOCKS ~= 0 THEN DO; 
        // add NoWait I/O buffers as requested 
        IF NWSOCKS = -1 THEN 
            TMP = MAXSOCK; 
        ELSE 
            TMP = NWSOCKS; 
        TOTAL = TOTAL + (10+(BUFSIZE+3)/4) * (1+TMP*(MAXRDS+MAXBUF)); 
        END; 
nwsocks - (long) 
     Specifies the maximum number of sockets capable of NoWait I/O.  Valid 
     values are -1 to MAXSOCK.  -1 specifies that all sockets are capable of 
     NoWait I/O.  0 specifies that none are capable.  The CP-6 LINK option TCB 
     may need to be used to reserve space for events arriving as the result of 
     NoWait I/O.  One TCB frame is required for each NoWait event on arrival, 
     so the worst case requirement is NWSOCKS*MAXRDS. 
                                 xsl_sockinit 
        0   1   2   3 
      +---+---+---+---+ 
   .0 |   |   |   |   | struct xsl_sockinit { 
   .0 |uuu|uuu|uuu|uuu|   unsigned long maxsock; 
   .1 |sss|sss|sss|sss|   long nwsocks; 
   .2 |uuu|uuu|uuu|uuu|   unsigned long bufsize; 
   .3 |ppp|ppp|ppp|ppp|   void *mem$; 
   .4 |eee|eee|eee|eee|   void (*evnt$)(void *); 
   .5 |uuu|uuu|   |   |   unsigned maxrds :18; 
   .5 |   |   |uuu|uuu|   unsigned maxbuf :18; 
      +---+---+---+---+   }; 
        0   1   2   3     .6-0-0 total length 
