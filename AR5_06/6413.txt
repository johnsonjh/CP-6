INETD is a ghost that listens for connections on Internet sockets and starts 
up the appropriate ghosts (FTPD, user-developed applications), as needed.  The 
/etc/inetd.conf file (or etc:inetd_conf.:SYS file on the CP-6 host) is a 
configuration file containing the list of services to be managed by the inetd 
ghost (or daemon on the UNIX system).  For more information on INETD, see the 
topics DEFINING_SERVERS and INSTALLING_INETD. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
The inetd super-server listens to service requests as instructed by the 
inetd.conf file.  When a request arrives, inetd starts a ghost job to process 
the request; then it returns to listening for service requests. 
Entries in the /etc/inetd.conf file are of the following form: 
  service[/hostname] type protocol [no]wait userid rununit 
     server_command 
An example of a single entry is as follows: 
  ftp stream tcp nowait root /usr/netbin/ftpd ftpd 
Entries in the etc:inetd_conf.:SYS file are of the following form: 
  service[/hostname] type protocol no[wait] userid server_command 
An example of a single entry is as follows: 
  cp6ftp/duck stream tcp nowait :SYSTAC,DON,xxx !FTPD 
In addition, entries in the etc:inetd_conf.:SYS file can be of the following 
form: 
  S[ERVICE]=service[/hostname] T[YPE]=type PROT[OCOL]=protocol [No]wait 
     U[SERID]=userid {CC[BUF]|C[OMMAND]|A[RGS]}=server_command 
An example of a single entry is as follows: 
  s=cp6ftp/duck T=stream PROT=tcp nowait u=:SYSTAC,DON,XXX c=!FTPD 
Note:  The CP-6 style format requires that the abbreviatable keywords, equals 
signs, and options be within a single record. 
where: 
    service    specifies a service defined in the services file or, in the 
    etc:inetd_conf file on the host only, a decimal port number.  Within the 
    etc:inetd_conf file only, "service" may be followed immediately by 
    "/hostname" to specify the name of the local TCP/IP FEP through which 
    incoming connections are expected.  The "/hostname" option is useful only 
    for systems with multiple TCP/IP FEPs, or when "localhost" is improperly 
    defined in etc:hosts.  The "/hostname" should match the name of the host 
    as defined in etc:hosts.:SYS. 
    type    specifies one of S[TREAM], D[ATA]GRAM, or R[AW].  This type is 
    used when opening socket connections. 
    protocol    specifies TCP or UDP. 
    [No]wait    is ignored.  This field is provided for compatibility with 
    UNIX standards. 
    userid    is a logon string that defines where to start the server as a 
    ghost job or daemon. 
    server_command    is the command provided to invoke the server as a ghost 
    job or daemon.  It can contain any string of characters. 
Note:  The spelling of service and protocol names must match the case of the 
corresponding definitions in etc:services and etc:protocols.  The rest may be 
entered in uppercase or lowercase. 
Note: As released, the INETD control file, etc:inetd_conf.:SYS, contains only 
the entry that configures the FTP server, FTPD.  That entry needs to be 
updated to contain a valid logon account in which FTPD is to run.  Other 
entries can be added to start other servers. 
A 
  account for INETD, FTPD - 
      HELP INSTALLING_INETD 
D 
  Define Servers in /etc/inetd.conf - 
      HELP DEFINING_SERVERS 
E 
  /etc/inetd.conf file - 
      HELP DEFINING_SERVERS 
  etc:inetd_conf file - 
      HELP DEFINING_SERVERS 
F 
  FTPD, server FTP ghost - 
      HELP INSTALLING_INETD 
I 
  Install INETD and Server FTP - 
      HELP INSTALLING_INETD 
O 
  On-Line HELP Facilities for TCP/IP - 
      HELP TCPIP_HELP 
S 
  server FTP - 
      HELP INSTALLING_INETD 
00001
00002
00003
00004
00005
00006
HELP_INDEX
First choose a CP-6 account from which to start a ghost job that runs INETD 
and from which to run the FTPD server when a connect occurs.  This account 
must have ghost user access and should match the AUACCOUNT specified for the 
TCP/IP CL resources defined in SUPER, unless only MSYS is being used to 
control privileged port access.  This account should be assigned as many CL 
resources as the server will need, unless the server uses JIT privilege to 
compensate.  Otherwise, it should probably be a low-privileged account, since 
servers that do not perform user authorization checks should not be allowed to 
do much damage, and those that do should provide specific privileges for 
themselves.  Note that the account must have execute access to FTPD.:SYS. 
Edit the etc:inetd_conf file from an account that can modify it in .:SYS. 
Because it has logon passwords in it, this file should not be easily visible. 
The file could be encrypted, by adding a SET command to the INETD GOOSE XEQ 
file.  It could also be passworded, because INETD uses FMSEC to see it. 
Note:  INETD normally gets configuration records from etc:inetd_conf.:SYS, but 
can be directed elsewhere through the M$SI DCB, either explicitly via a SET 
command, or implicitly on the command line. 
The following two lines have been added to the etc:services file (as released 
in .:SYS): 
    cp6ftp-data   18/tcp 
    cp6ftp        19/tcp 
The following line has been added to the etc:inetd_conf file in .:SYS: 
    cp6ftp   stream tcp nowait acct,name,pass  !FTPD 
You must change the "acct,name,pass" portion to specify the logon you have 
chosen for running the FTPD server.  The choice of service names (cp6ftp and 
cp6ftp-data) and port numbers (19 and 18) is arbitrary, but the data port must 
be one less than the service port, and both must be otherwise unused.  Be sure 
to check the /etc/services and /etc/inetd.conf files on the DPX/2-300 FEP for 
conflicts. 
Together, these entries will cause INETD to invoke the FTPD ghost when a 
connection is initiated to port 19.  Users wishing to use the server would 
issue the commands 
    !FTP 
    FTP:open unix_hostname,19 
from the CP-6 system, or 
    ftp unix_hostname 19 
from UNIX. 
If you would prefer to get to the CP-6 FTP server without having to specify a 
port in the ftp or open command, changes will have to be made in the services 
files on both the CP-6 and the DPX/2-300 systems.  In the etc:services file on 
the CP-6 host, exchange the port numbers for the ftp and cp6ftp, and exchange 
the port numbers for ftp-data and cp6ftp-data.  In the /etc/services file on 
the UNIX FEP, exchange the port number for cp6ftp and ftp.  An example of this 
is shown below. 
#etc:services          on CP-6 host 
   cp6ftp-data            20/tcp 
   cp6ftp                 21/tcp 
   ftp-data               18/tcp 
   ftp                    19/tcp 
#/etc/services          on UNIX FEP 
   cp6ftp                 21/tcp 
   ftp                    19/tcp 
Other desired servers can be conveniently implemented by using INETD to take 
care of the multiplexing problem.  For each such server, a line will need to 
be added to etc:inetd_conf.:SYS, and possibly to etc:services.:SYS, to define 
the correspondence between the port number and the server rununit and run 
account.  The description of "accept_srvr" in the SOCKETLIB HELP facility 
details the required interface for implementing such a server. 
The syntactical correctness of etc:inetd_conf.:SYS and its relation to 
etc:services.:SYS can be checked online by simply invoking INETD.  The 
configuration file will be processed, echoed, and any errors reported, but no 
network connections will be attempted.  If the configuration files are updated 
while INETD is already running as a ghost user, the INETD ghost can be caused 
to take note of the new configuration by running INETD online with the 
following command: 
    !INETD RESTART 
To verify the services provided by INETD, use the status command as follows: 
    !INETD STATUS 
The following is an example of what is displayed when invoking the status 
command: 
  Service         Host              Connects        Command 
     Sysid State   Ldctx  Rname        Errno        Client Address 
---------------------------------------------------------------------- 
  cp6ftp          dolly                    1        !FTPD 
  -  66942     2      11                   0        192.35.126.4,1622 
  printer         dolly                    0        !xeq $XLPD.:SYSTAC 
The display shows how the servers for cp6ftp and printer will be invoked by 
the INETD ghost. 
The display also shows the most recent instance of FTPD currently active: it 
has a sysid of 66942, it is in state 2, uses ldct 11 on the UNIX FEP, and the 
client address is 192.35.126.4,1622. 
To get pending line printer output from INETD on demand, use the PRINT 
command: 
    !INETD PRINT 
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
