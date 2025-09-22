FTPD is the File Transfer Protocol Server.  It is the server portion of the 
client/server pair FTP/FTPD. 
FTPD is similar to most server applications in that it operates with the use 
of the INETD "superserver".  INETD continually listens on all ports associated 
with the service names specified in the file etc:inetd_conf.:SYS.  The 
association of port numbers with service names is made by the 
etc:services.:SYS file.  When INETD receives a connection request on the port 
for FTP service, it starts up FTPD as a separate CP-6 user.  FTPD inherits the 
connection from INETD and continues. 
The FTPD server will time out an inactive session after 15 minutes. 
Access to FTPD can be limited by the use of the file etc:ftpusers.:SYS. Any 
account name listed in etc:ftpusers is prevented from having access to FTPD. 
The format for entering account names is shown below: 
DONDUCK 
DAFDUCK 
The first eight characters of each line are used. Shorter lines are blank 
padded. 
For a summary of all FTPD requests, enter 
    HELP (FTPD) SUMMARY 
Information is available for a particular request by entering 
    HELP (FTPD) request_name 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
Syntax:  ACCT 
Specify account (ignored). 
Syntax:  ALLO 
Allocate storage (vacuously). 
Syntax:  APPE file-name 
Append to a file. 
Syntax:  CDUP 
Change to parent of current working directory. 
Syntax:  CWD [ directory-name ] 
Change working directory. 
Syntax:  DELE file-name 
Delete a file. 

Syntax:  HELP [ string ] 
Give help information; use '/' to separate options. 
F 
  FTPD -   
    FTP Requests - 
      HELP SUMMARY 
  FTPD - 
      HELP FTPD 
  FTPD - File Transfer Protocol Server - 
      HELP FTPD 
O 
  On-Line HELP Facilities for TCP/IP - 
      HELP TCPIP_HELP 
00001
HELP_INDEX
Syntax:  LIST [ path-name ] 
Give list files in a directory ('ls -l') (L(A)). 
Syntax:  NLST [ path-name ] 
Give name list of files in directory ('ls') (L(C=0)). 
Syntax:  NOOP 
Do nothing. 
Syntax:  PASS password 
Specify password. 
Syntax:  PASV 
Prepare for server-to-server transfer. 
Syntax:  PORT b0, b1, b2, b3, b4 
Specify data connection port. 
Syntax:  PWD 
Print the current working directory. 
Syntax:  QUIT 
Terminate session. 
Syntax:  RETR file-name 
Retrieve a file. 
Syntax:  RNFR file-name 
Specify rename-from file name. 
Syntax:  RNTO file-name 
Specify rename-to file name. 
Syntax:  !SET F$FILE fid, options 
Perform SET command; dcbname must be F$FILE. 
Syntax:  STOR file-name 
Store a file. 
The FTPD server currently supports the following FTP requests.  The requests 
can be typed in either upper or lower case. 
*  The FTP requests flagged with an asterisk are recognized, but not 
implemented. 
  Request     Description 
*ABOR       Abort previous command 
 ACCT       Specify account (ignored) 
 ALLO       Allocate storage (vacuously) 
 APPE       Append to a file 
 CDUP       Change to parent of current working directory 
 CWD        Change working directory 
 DELE       Delete a file 
 HELP       Give help information; use "/" to separate options 
 LIST       Give list of files in a directory ("ls -l") (L(A)) 
*MKD        Make a directory 
 MODE       Specify data transfer mode 
 NLST       Give name list of files in directory ("ls") (L(C=0)) 
 NOOP       Do nothing 
 PASS       Specify password 
 PASV       Prepare for server-to-server transfer 
 PORT       Specify data connection port 
 PWD        Print the current working directory 
 QUIT       Terminate session 
*REIN       Reinitialize context 
*REST       Restart transfer 
 RETR       Retrieve a file 
*RMD        Remove a directory 
 RNFR       Specify rename-from file name 
 RNTO       Specify rename-to file name 
*SITE       Give site information 
 STAT       Give status information 
 STOR       Store a file 
*STOU       Store a file with a unique name 
*STRU       Specify data transfer structure 
*SYST       Give system information 
 TYPE       Specify data transfer type 
 USER       Specify user name 
 XCUP       Change to parent of current working directory 
 XCWD       Change working directory 
*XMKD       Make a directory 
 XPWD       Print the current working directory 
*XRMD       Remove a directory 
 !SET       SET command; dcbname must be F$FILE 
FTPD authenticates users according to normal CP-6 rules.  The USER command 
specifies the account and name portion, separated by a comma.  Privilege is 
set to the online authorization. 
It is permissible to STOR to device FIDs like JF, JE, LP, etc.  Some of these 
are particularly useful. 
Use of the !SET command will most likely require your FTP client to support 
the QUOTE command, for example: 
    quote !set F$FILE x,recl=1024 
(Note that F$FILE must be in uppercase.) 
FTPD echoes commands and responses to LP, and produces an accounting of 
charges when the session ends (normally when a QUIT command is encountered, 
but possibly later if the JF destination is used).  If FTPD aborts, a PMD dump 
is also produced; this dump should be shown to your system administrator for 
possible STAR submission. 
CP-6 TCP/IP provides online HELP for the following facilities: FTP, FTPD, 
TELNET, INETD, and the Host Socket Library (SOCKETLIB).  HELP displays the 
syntax of commands and statements and related information.  For a list of the 
HELP topics available from the system command level (!), enter the following: 
    HELP (FTP) TOPICS 
    HELP (FTPD) TOPICS 
    HELP (TELNET) TOPICS 
    HELP (INETD) TOPICS 
    HELP (SOCKETLIB) TOPICS 
Note:  For the SOCKETLIB HELP facility, the topics for the services appear as 
the C service names.  The PL-6 service names may also be used to access the 
HELP facility.  For instance, 
    HELP (SOCKETLIB) accept 
and 
    HELP (SOCKETLIB) XSL$ACCEPT 
cause a display of the same information. 
Syntax:  TYPE [ A | E | I | L ] 
Specify data transfer type. 
Syntax:  USER username 
Specify user name. 
Syntax:  XCUP 
Change to parent of current working directory. 
Syntax:  XCWD 
Change working directory. 
Syntax:  XPWD 
Print the current working directory. 
