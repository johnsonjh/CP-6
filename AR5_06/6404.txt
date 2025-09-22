Format: 
FTP [host [[,] port]] 
Parameters: (optional) 
host     specifies a host by name or by Internet address (four numbers, 0-255, 
separated by periods). 
port     specifies a port number (0-65535). The default port number is 21. 
Description: 
FTP can be initiated with or without the hostname or host ip address.  If a 
hostname or host ip address is specified, the user has the option of 
specifying a port on the remote host.  For FTP to work with the port 
specified, the ftpd server on the remote host must be listening on the 
specified port. 
If FTP is entered without the optional hostname (address), it enters its 
command interpreter and awaits instructions from the user.  When FTP is 
awaiting commands from the user, the prompt "FTP:" is displayed. 
With CP-6 FTP, file transfer defaults to STREAM mode, FILE structure, and 
NONPRINT format.  To change these options, use the commands MODE, STRUCT, and 
PRINT to change the mode, structure and format, respectively.  These commands 
can be excecuted only after a connection to the remote machine has been made. 
Only the default options have been implemented. 
The two examples shown below illustrate the commands used to copy a file from 
a remote machine and to copy a file to a remote machine.  If step 1, in both 
examples, is entered with the hostname (address) specified, FTP enters the 
command interpreter and automatically issues an OPEN command to the specified 
host. This allows you to skip step 2 and connect to the foreign host in one 
less step. 
Examples: 
To copy from a remote machine to your host machine, follow these steps: 
1   At the IBEX prompt (!) type FTP to start the program. 
2   When you see the "FTP:" prompt, type OPEN followed by the machine name or 
    ip address of the remote machine. 
3   Wait for FTP to establish a connection. 
4   Type your user id on the REMOTE machine at the User Id prompt. 
5   Type your password on the REMOTE machine at the Password prompt. 
6   Wait for FTP to log you on to the remote machine. 
7   When you see the "FTP:" prompt, type GET followed by the file name of the 
    file on the other machine (use the absolute path-name or a CD command to 
    establish the path), and the destination fid where you want the file to 
    appear. 
8   When FTP notifies you that the transfer is complete, type QUIT to return 
    to IBEX. 
Below is an example of a transfer from a remote machine to the CP-6 Host. 
!FTP 
CP-6 FTP Version A00 
FTP: OPEN SATURN 
Connection Established 
220 saturn FTP server (SunOS 4.1) ready. 
User id:dd 
331 Password required for dd. 
Password: 
230 User dd logged in. 
FTP: GET zzz YYY 
227 Entering Passive Mode (192,94,226,50,8,86) 
ASCII data connection for zzz (192.94.226.59.1059)  (1055 bytes). 
226 ASCII Transfer complete. 
1055 bytes transferred in 0.1 seconds (10.6 Kbytes/s) 
FTP:QUIT 
221 Goodbye 
To copy from your host machine to a remote machine, follow these steps: 
1   At the IBEX prompt (!) type FTP to start the program. 
2   When you see the "FTP:" prompt, type OPEN followed by the machine name or 
    ip address of the remote machine. 
3   Wait for FTP to establish a connection. 
4   Type your user id on the REMOTE machine at the User Id prompt. 
5   Type your password on the REMOTE machine at the Password prompt. 
6   Wait for FTP to log you on to the remote machine. 
7   When you see the "FTP:" prompt, type PUT, followed by the CP-6 fid of the 
    file on your machine and the destination file name (absolute path-name or 
    a CD command to establish the path) where you want the file to appear. 
8   When FTP notifies you that the transfer is complete, type QUIT to close 
    the network connection. 
Below is an example of a transfer from the CP-6 Host to a remote machine. 
!FTP 
CP-6 FTP Version A00 
FTP: OPEN SATURN 
Connection Established 
220 saturn FTP server (SunOS 4.1) ready. 
User id:dd 
331 Password required for dd. 
Password: 
230 User dd logged in. 
FTP: PUT zzz YYY 
227 Entering Passive Mode (192,94,226,50,8,86) 
ASCII data connection for zzz (192.94.226.59.1059) 
226 ASCII Transfer complete. 
1055 bytes transferred in 0.1 seconds (10.6 Kbytes/s) 
FTP:QUIT 
221 Goodbye 
For a list of FTP commands available, enter 
    HELP (FTP) TOPICS 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
Format: 
AP[PEND] local-file [ remote-file ] 
Parameters: 
local-file    specifies a CP-6 fid. 
remote-file    specifies the name of a remote file. 
Description: 
This command appends a local file to a file on the remote machine.  If 
remote-file is not specified, the local file name is used in naming the remote 
file.  If the remote file does not exist, it is created.  The remote file's 
name will be the same as the local file's name, except that any dollar signs 
in the local file's name will be converted to periods in the remote file's 
name.  File transfer uses the current setting for TYPE. 
APPEND performs the same function as the PUT command with INTO specified. 
00002
00001
OPEN
Format: 
{ CD | RDIR | CWD } remote-directory 
Parameters: 
remote-directory    specifies the name of a remote directory.  A name 
containing a space character may be used by enclosing the name within single 
quotation marks. 
Description: 
This command changes the working directory on the remote machine to 
remote-directory. 
00002
00001
Format: 
CDUP 
Parameters: 
None. 
Description: 
This command changes the working directory on the remote machine to its parent 
directory. 
00002
00001
Format: 
CL[OSE] 
Parameters: 
None. 
Description: 
This command terminates the FTP session with the remote server, and returns to 
the command interpreter. 
00002
00001
OPEN
CD
Format: 
{ DATE | TIME } 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm   (month)(day)(year)(hours)(minutes) 
Examples: 
FTP:DATE 
requests a display of the current date and time.  A sample display is 
     AUG 02  '89  11:03 
00001
00002
Format: 
DEL[ETE] remote-file 
Parameters: 
remote-file    specifies the name of a remote file. 
Description: 
This command deletes the specified file on the remote machine. 
00002
00001
LIST
Format: 
DIRECTORY [ fid | R[ESET] ] 
Parameters: 
fid    specifies the new default account fid on the CP-6 host, and may consist 
of an account or a packset name and an account. 
R[ESET]    specifies that the default account is to be reset to the running 
account. 
Description: 
This command changes the default account and packset on the CP-6 host.  The 
default account and packset are the account and associated packset that are 
selected if an account is not supplied as part of a disk file fid 
specification.  Initially, the default account is the logon or running account 
and the packset name is nil.  When used without parameters, DIRECTORY displays 
the current directory pointer. 
Examples: 
FTP:DIRECTORY .SYSLIB 
directs that subsequent fids, that do not include an account, are to default 
to the .SYSLIB account and the packset associated with that account. 
FTP:DIRECTORY DP#UTIL.Y 
directs that subsequent fids, that do not include an account, are to default 
to the Y account on the packset named UTIL. 
FTP:DIRECTORY RESET 
re-establishes the running account and its associated packset as the default. 
00002
00003
00001
Format: 
{ DO | ! } IBEX-command 
Parameters: 
IBEX-command    any legal IBEX command. 
Description: 
The DO command allows the user to execute an IBEX command without exiting the 
current processor. 
Note:  The ! (exclamation point) may be used instead of the word DO.  It 
should be noted however that if the ! is used in an XEQ file, it will 
terminate the current processor session unless preceded by at least one blank, 
or by another ! (!!). 
Examples: 
FTP:DO DI 
FTP:! DI 
both examples display the current system status. 
Of particular usefulness is the !SET command for the F$FILE DCB, which is used 
by FTP in GET and PUT commands. 
00002
00003
00001
QUIT
Format: 
ERASE [ ALL | ldevlist ] 
Parameters: 
ALL    specifies that the accumulated output for all logical devices is to be 
deleted.  This is the default. 
ldevlist    specifies that the accumulated output for the specified logical 
device or devices is to be deleted.  The list is entered in the format 
     ldevname[,ldevname]... 
where ldevname is a logical device name established through the LDEV command. 
Description: 
The ERASE command deletes the accumulated output for logical devices. 
Examples: 
FTP:ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
00001
QUIT

Format: 
{ G[ET] | RECV } remote-file [ [TO|ON|OVER|INTO] local-file ] 
Parameters: 
remote-file    specifies the name of a remote file.  A name containing a space 
character may be used by enclosing the name within single quotation marks. 
{TO|ON|OVER|INTO}   directs destination file processing.  OVER causes an 
existing file to be overwritten.  INTO causes file extension.  TO (or ON) is 
used to create a new file; if the file exists, an error is reported.  The 
default is OVER. 
local-file    specifies a CP-6 fid. 
Description: 
Retrieves the remote-file and stores it on the local machine.  If the local 
file name is not specified, the file is given the same name as that of the 
file on the remote machine, except that any periods in the remote file's name 
will be converted to dollar signs in the local file's name.  The current 
setting for TYPE is used while transferring the file.  Destination file 
attributes may be specified via a !SET command for F$FILE.  If a !SET command 
is not specified, a consecutive file will be created.  For type=binary, RECL 
in a !SET command specifies the length of all records but the last. 
To interrupt the file transfer, use the BREAK key.  Depending on the server, 
the use of this key may also cause a disconnect. 
00002
00001
Format: 
HELP [ (fid) ] [ TOPICS ] [ keyword1 [-] [ keyword2 ]] 
Note:  The following elements can be specified in any order: 
     (fid) 
     TOPICS 
     [keyword1] [-] [keyword2] 
For example, HELP (fid) keyword1  - keyword2 TOPICS is acceptable. 
Parameters: 
(fid)    specifies the processor name (for example, PIG).  If (fid) is 
omitted, the current processor is assumed. 
TOPICS    requests a list of topic or subtopic names, rather than an 
information message. 
Form                                     Result 
HELP (fid) TOPICS                        Lists all topics 
HELP (fid) TOPICS keyword1 - keyword2    Lists all topics in the range 
                                         specified by keyword1 - keyword 2 
HELP (fid) TOPICS keyword1?              Lists all topics beginning with 
                                         the prefix specified by keyword1 
HELP (fid) TOPICS keyword1               Lists all subtopics for the 
                                         topic specified by keyword1 
keyword1 [- [keyword2]]    specifies a topic, a range of topics, or a topic 
and subtopic to identify what HELP information is requested. 
Form                                     Result 
HELP (fid) keyword1                      Displays the first level 
                                         information message for 
                                         the topic keyword1 
HELP (fid) keyword1 keyword2             Displays the information 
                                         message for keyword1, but only 
                                         the level identified by the 
                                         subtopic keyword2 
HELP (fid) TOPICS keyword1 [-] [keyword2]  Lists topic or subtopic 
                                         names. 
keyword1 may include the wildcard (?) character as the rightmost character, if 
TOPICS is specified. 
Description: 
HELP displays information. 
HELP messages have levels.  Once the initial level has been displayed, 
entering a question mark displays the next level, usually containing greater 
detail.  Entering two question marks, displays the remainder of information on 
that topic. 
Note:  In interactive mode, syntax help is also available when a syntactic 
error is made resulting in a diagnostic message.  If the user enters a ? after 
the diagnostic message is displayed, a list of acceptable items at the point 
of error will be displayed. 
00002
00001
A 
  APPEND Command - 
      HELP APPEND 
C 
  CD Command - 
      HELP CD 
  CDUP Command - 
      HELP CDUP 
  CLOSE Command - 
      HELP CLOSE 
D 
  DATE Command - 
      HELP DATE 
  DCB, F$FILE - 
      HELP DO EXAMPLES: 
      HELP GET DESCRIPTION: 
  DELETE Command - 
      HELP DELETE 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DO Command - 
      HELP DO 
E 
  ERASE Command - 
      HELP ERASE 
F 
  F$FILE DCB - 
      HELP DO EXAMPLES: 
      HELP GET DESCRIPTION: 
  FILE structure - 
      HELP FTP 
  File Transfer Services - 
      HELP FILE_TRANSFER_SERVICES 
  format, NONPRINT - 
      HELP FTP 
  FTP -   
    ! Command - 
      HELP DO 
    APPEND Command - 
      HELP APPEND 
    ASCII type - 
      HELP TYPE FORMAT: 
    BINARY type - 
      HELP TYPE FORMAT: 
    CD Command - 
      HELP CD FORMAT: 
    CDUP Command - 
      HELP CDUP 
    CLOSE Command - 
      HELP CLOSE 
    CONNECT Command - 
      HELP OPEN 
    CWD Command - 
      HELP CD FORMAT: 
    DATE Command - 
      HELP DATE 
    DELETE Command - 
      HELP DELETE 
    DIR Command - 
      HELP LIST 
    DIRECTORY Command - 
      HELP DIRECTORY 
    DO Command - 
      HELP DO 
    END Command - 
      HELP QUIT FORMAT: 
    ERASE Command - 
      HELP ERASE 
    EXIT Command - 
      HELP QUIT FORMAT: 
    GET Command - 
      HELP GET FORMAT: 
    HELP Command - 
      HELP HELP 
    IMAGE type - 
      HELP TYPE FORMAT: 
    LIST Command - 
      HELP LIST 
    LS Command - 
      HELP LS 
    MDELETE Command - 
      HELP MDELETE 
    MGET Command - 
      HELP MGET 
    MPUT Command - 
      HELP MPUT 
    OPEN Command - 
      HELP OPEN 
    OUTPUT Command - 
      HELP OUTPUT 
    PRINT Command - 
      HELP PRINT 
    PUT Command - 
      HELP PUT 
    PWD Command - 
      HELP PWD 
    QUIT Command - 
      HELP QUIT FORMAT: 
    QUOTE Command - 
      HELP QUOTE 
    RDIR Command - 
      HELP CD FORMAT: 
    RECV Command - 
      HELP GET FORMAT: 
    REMOTE HELP Command - 
      HELP REMOTEHELP 
    RENAME Command - 
      HELP RENAME 
    SEND Command - 
      HELP PUT 
    STATUS Command - 
      HELP STATUS 
    SYNCHRONIZE Command - 
      HELP SYNCHRONIZE 
    TIME Command - 
      HELP DATE 
    TOGGLE Command - 
      HELP TOGGLE 
    TYPE Command - 
      HELP TYPE FORMAT: 
    USER Command - 
      HELP USER 
  FTP - 
      HELP FTP 
  FTP - File Transfer Protocol - 
      HELP FTP 
G 
  GET Command - 
      HELP GET 
H 
  HELP Command - 
      HELP HELP 
L 
  LIST Command - 
      HELP LIST 
  LS Command - 
      HELP LS 
M 
  MDELETE Command - 
      HELP MDELETE 
  MGET Command - 
      HELP MGET 
  mode, STREAM - 
      HELP FTP 
  MPUT Command - 
      HELP MPUT 
N 
  NONPRINT format - 
      HELP FTP 
O 
  On-Line HELP Facilities for TCP/IP - 
      HELP TCPIP_HELP 
  OPEN Command - 
      HELP OPEN 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PRINT Command - 
      HELP PRINT 
  PUT Command - 
      HELP PUT 
  PWD Command - 
      HELP PWD 
Q 
  QUIT Command - 
      HELP QUIT 
  QUOTE Command - 
      HELP QUOTE 
R 
  REMOTEHELP Command - 
      HELP REMOTEHELP 
  RENAME Command - 
      HELP RENAME 
S 
  STATUS Command - 
      HELP STATUS 
  STREAM mode - 
      HELP FTP 
  structure, FILE - 
      HELP FTP 
  SYNCHRONIZE Command - 
      HELP SYNCHRONIZE 
T 
  TOGGLE Command - 
      HELP TOGGLE 
  TYPE Command - 
      HELP TYPE 
U 
  USER Command - 
      HELP USER 
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
Format: 
{ L[IST] | DIR } [ remote-files [[TO|ON|OVER|INTO] local-file ]] 
Parameters: 
remote-files    specifies the name of a remote directory, file, or wildcarded 
set of files to be listed.  A name containing a space character may be used by 
enclosing the name within single quotation marks. 
{TO|ON|OVER|INTO}    directs destination file processing.  OVER causes an 
existing file to be overwritten.  INTO causes file extension.  TO (or ON) is 
used to create a new file; if the file exists, an error is reported.  The 
default is OVER. 
local-file    specifies the name of the CP-6 file into which to list the 
remote file name(s). 
Description: 
This command prints a listing of the contents of the specified directory on 
the remote machine, and places the listing in local-file.  If no directory is 
specified, the current working directory on the remote machine is used.  If no 
local file is specified, output is displayed on the terminal. 
The difference between LIST and LS is that LIST gives the "long" 
display--i.e., "LS -L". 
00002
00001
Format: 
LS [ remote-files [[TO|ON|OVER|INTO] local-file ]] 
Parameters: 
remote-files    specifies the name of a remote directory, file, or wildcarded 
set of files to be listed.  A name containing a space character may be used by 
enclosing the name within single quotation marks. 
{TO|ON|OVER|INTO}    directs destination file processing.  OVER causes an 
existing file to be overwritten.  INTO causes file extension.  TO (or ON) is 
used to create a new file; if the file exists, an error is reported.  The 
default is OVER. 
local-file    specifies the name of the CP-6 file into which to list the 
remote file name(s). 
Description: 
This command prints a name-only listing of the contents of a directory on the 
remote machine, and places the listing in local-file.  If remote-directory is 
not specified, the current working directory is used.  If no local file is 
specified, output is displayed on the terminal. 
00002
00001
Format: 
MDEL[ETE] remote-files 
Parameters: 
remote-files    specifies the name of the directory, file, or wildcarded set 
of files to be deleted from the remote system.  (Only files in a directory are 
deleted -- not the directory itself.)  A name containing a space character may 
be used by enclosing the name within single quotation marks. 
Description: 
Removes the specified file or set of files from the remote machine. 
To interrupt the processing of this command use the BREAK key.  Depending on 
the server, the use of this key may also cause a disconnect. 
The PROMPT toggle can be used with the MDELETE command to prompt for 
filenames.  When PROMPT is toggled on, there will be prompts for each file 
that is about to be processed.  The user is given the option to skip the 
deletion of that file by selecting "n", or to abort the entire MDELETE command 
by typing "q". 
A typical example of MDELETE with PROMPT toggled on is illustrated below: 
    remote-filename   (n/q) 
00002
00001
Format: 
MG[ET] remote-files 
Parameters: 
remote-files    specifies the name of the directory, file, or wildcarded set 
of files to get from the remote system.  A name containing a space character 
may be used by enclosing the name within single quotation marks. 
Description: 
Retrieves the specified file or set of files from the remote machine and 
places it in the current local directory.  Files on the CP-6 host are given 
the same names as those of the remote files, except that any periods in the 
remote files' names are converted to dollar signs on the local CP-6 system. 
To interrupt the file transfer use the BREAK key.  Depending on the server, 
the use of this key may also cause a disconnect. 
The PROMPT toggle can be used with the MGET command to prompt for filenames. 
When PROMPT is toggled on, there will be prompts for each file that is about 
to be processed.  The user is given the option to skip the transfer of that 
file by selecting "n", to abort the entire MGET command by typing "q", or to 
supply the name the file will be given on the host. 
A typical example of MGET with PROMPT toggled on is illustrated below: 
    remote-filename   (n/q/newname) 
If the user enters a filename, the remote file will be stored on the CP-6 
machine under the filename specified.  If the user simply enters a carriage 
return, the default occurs: the filename used on the CP-6 machine will be the 
same as the filename used on the remote machine. 
00002
00001
Format: 
MP[UT] local-file 
Parameters: 
local-file    specifies the name of the file or wildcarded set of files to be 
transferred to the remote system. A name containing a space character may be 
used by enclosing the name within single quotation marks. 
Description: 
Transfers the specified file or set of files from the current local directory 
to the current working directory on the remote machine.  Files on the remote 
computer are given the same names as those of the local files, except that any 
dollar signs in local files' names are converted to periods on the remote 
system. 
To interrupt the file transfer use the BREAK key.  Depending on the server, 
the use of this key may also cause a disconnect. 
The PROMPT toggle can be used with the MPUT command to prompt for filenames. 
When PROMPT is toggled on, there will be prompts for each file that is about 
to be processed.  The user is given the option to skip the transfer of that 
file by selecting "n", to abort the entire MGET command by typing "q", or to 
supply the name the file will be given on the host. 
A typical example of the MPUT command with PROMPT toggled on is shown below: 
    local-filename (n/q/newname) 
If the user enters a filename, the file transferred will be stored on the 
remote host under the name specified. 
If the user simply enters a carriage return, the default occurs:  the file 
stored on the remote host will have the same name as the file on the local 
host. 
00002
00001
Format: 
{ O[PEN] | C[ONNECT] } host [ [,] port ] 
Parameters: 
host    specifies a host by name or by Internet address (four decimal numbers, 
0-255, separated by dots). 
port    specifies a port number (0-65535). The default port number is 21. 
Description: 
This command establishes a connection to the specified host ftpd server.  An 
optional port number may be supplied, in which case FTP attempts to contact an 
FTP server at that port.  Upon successfully connecting, FTP prompts for logon 
information for the remote host. 
00002
00001
Format: 
         [[ON  ] LP[@location]] 
OUT[PUT] [[OVER] fid          ] [ (option[,option]...[) ]] 
         [[INTO] ME           ] 
         [[TO  ]              ] 
Parameters: 
{ON|TO|OVER|INTO}    directs file output processing.  OVER causes an existing 
file to be overwritten.  INTO causes file extension.  ON and TO are synonyms 
used to create a new file.  If the file exists, an error will occur.  The 
default is ON. 
fid    any valid CP-6 file identifier. 
LP    directs output to the default line printer.  @location identifies a 
specific line printer. 
ME    redirects output to the user's terminal. 
option    is one of the following: 
    F[ORM]={formname|'formname'}    FORM applies to unit record files and unit 
    record devices; it specifies the name of a form to be mounted on a unit 
    record device. formname is a 1-6 character string, which can be enclosed 
    in quotes.  The name must have been defined to the system by the system 
    manager (via the Form Definition File).  The default is blank, which 
    specifies the default form for a unit record device, and the 'STDLP' form 
    for unit record files. 
    I[XTNSIZE]=value    Specifies an initial disk storage allocation (in 
    blocks) for the output file.  value must be in the range of 1 through 
    134217727.  The default is 2. 
    O[RGANIZATION]={C[ONSECUTIVE]|U[NIT]R[ECORD]}    Specifies the 
    organization of the output file as either CONSECUTIVE or UNIT RECORD (UR). 
    If this option is not specified, the output file is created as a UR file. 
    X[TNSIZE]=value    Use of this option causes an automatic M$EXTEND when 
    needed. value specifies a secondary disk storage allocation (in blocks) 
    for the output file, and must be in the range 1 through 32000.  The 
    default is 2. 
Description: 
This command sends subsequent output to the specified file or device.  If a ! 
or DO command is used in conjunction with OUTPUT, subsequent output will be 
directed to the terminal. 
Examples: 
FTP:OUTPUT ON OUTPUTFILE 
FTP:OUTPUT ON ME 
00002
00003
00001
PUT
Format: 
PRINT [ ALL | ldevlist ] 
Parameters: 
ALL    specifies that the accumulated outputs for all logical devices are to 
be sent to their destinations immediately.  This is the default. 
ldevlist    specifies that the accumulated outputs for the specified logical 
device or devices are to be sent to their destination(s) immediately.  The 
list is entered in the format 
     ldevname[,ldevname]... 
where ldevname is a logical device name established through the LDEV command. 
Description: 
The PRINT command directs that output accumulated for logical devices be sent 
to its destination immediately. 
Examples: 
FTP:PRINT LP01,LP02 
causes the accumulated output associated with logical devices LP01 and LP02 to 
be sent immediately to the associated destinations. 
00002
00003
00001
Format: 
{ P[UT] | SE[ND] } local-file [[ OVER|INTO ] remote-file ] 
Parameters: 
local-file    specifies a CP-6 fid. 
{ OVER|INTO }   directs file output processing.  OVER causes an existing file 
to be overwritten.  INTO causes file extension.  The default is OVER. 
remote-file    specifies the name of a remote file.  A name containing a space 
character may be used by enclosing the name within single quotation marks. 
Description: 
This command stores a local file on the remote machine.  If remote-file is not 
specified, the local file name is used in naming the remote file.  File 
transfer uses the current setting for TYPE. 
To interrupt the file transfer use the BREAK key. Depending on the server, the 
use of this key may also cause a disconnect. 
00002
00001
Format: 
PWD 
Parameters: 
None. 
Description: 
This command prints the name of the current working directory for the remote 
machine. 
00002
00001
Format: 
{ Q[UIT] | E[ND] | [E]X[IT] } 
Parameters: 
None. 
Description: 
This command terminates the FTP session with the remote ftpd server and exits 
FTP. 
00002
00001
Format: 
QUO[TE] command_text 
Parameters: 
command_text    specifies a collection of characters which should represent a 
command implemented on the ftpd server. If the command sent is not implemented 
on the ftpd server, an error message will be displayed. For a list of valid 
ftpd server commands, use the REMOTE HELP command. 
Description: 
This command sends command_text to the remote ftpd server and waits for a 
response. 
Examples: 
The QUOTE command could be used in an XEQ or BATCH file to send information 
that would otherwise provoke errors in the FTP client.  For example, 
    QUOTE USER longname,account 
could be used when communicating with CP-6 FTPD using an ftp client that will 
not accept a long enough user id at the prompt.  Also, 
    QUOTE !SET F$FILE ... 
could be used when communicating with the CP-6 FPTD server. 
00002
00003
00001
REMOTEHELP
CD
GET
Format: 
{ REM[OTEHELP] | R[EMOTE] H[ELP] } [command] 
Parameters: 
command    specifies a command name recognized by the ftpd server on the 
remote host. 
Description: 
Requests help from the remote ftpd server. If a command is not specified, a 
list of valid ftpd server commands is displayed. 
00002
00001
Format: 
REN[AME] from-file [TO] to-file 
Parameters: 
from-file    specifies the name of a file on the remote machine.  A name 
containing a space character may be used by enclosing the name within single 
quotation marks. 
to-file    specifies the new name for the file.  A name containing a space 
character may be used by enclosing the name within single quotation marks. 
Description: 
This command renames the file on the remote machine to the specified name. 
00002
00001
STATUS
PUT
Format: 
S[TATUS] 
Parameters: 
None. 
Description: 
This command displays the current status of FTP. 
00002
00001
Format: 
SY[NCHRONIZE] 
Parameter: 
None. 
Description: 
This command is used to restore useful dialog with servers that do not respond 
properly to interrupted GET or PUT commands.  If the server is sending 
responses that are out of sequence, SYNC will display a response without 
sending an FTP command.  Do not use this command if FTP is functioning 
properly because FTP will wait for a response that will never come.  Use TYPE 
commands in VERBOSE mode to establish whether a SYNCHRONIZE command is needed. 
00002
00001
TOGGLE
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
DATE
Format: 
[ T[OGGLE] ] {BE[LL]|DEB[UG]|HA[SH]|PA[SV]|PO[RT]|PR[OMPT]|V[ERBOSE]} 
Parameters: 
BE[LL]    concerns the sending of a bell character when a GET or PUT command 
completes. 
DEB[UG]    concerns the display on the user terminal of the commands sent to 
the remote server. 
HA[SH]    concerns the display of a hash mark (#) after each 4k bytes 
transferred during a GET or PUT command. 
PA[SV]    concerns the use of PASV commands.  When this option is toggled on, 
all data transfers will occur in a passive manner.  This means that, upon 
receiving a data transfer request, the server will initiate the data 
connection.  The advantage of using PASV commands is that only two, not three, 
CL resources are needed to run FTP. 
PO[RT]    concerns the use of the PORT command. When toggled ON, PORT allows 
FTP to specify the data port on which data will be transferred. This will 
prevent delays when doing multiple file transfers. If the PORT option is 
toggled OFF, then data transfer will occur only on FTP's default data port 
(20). 
PR[OMPT]    concerns the prompting for each file of a multi-file operation 
(MGET, MPUT or MDELETE). 
V[ERBOSE]    concerns the display of normal responses to commands. 
Note:  The initial state for all the parameters, except VERBOSE, is off. 
Description: 
This command toggles the state of various flags.  The current status of the 
flags can be seen with the STATUS command. 
00002
00001
Format: 
[ TYPE ] [ type-name ] 
Parameters: 
type-name    specifies one of the following: 
   A[SCII]              for network ASCII 
   B[INARY]             for binary image transfer 
   I[MAGE]              synonym for BINARY 
Description: 
This command sets the file transfer type.  If no type is specified, the 
current type is printed.  The default is network ASCII. 
00002
00001
Format: 
U[SER] [ user-id [ password [ account ]]] 
Parameters: 
user-id    specifies the logon id needed to access the remote host.  If 
user-id contains a space character, the name may be used by enclosing it in 
single quotation marks. 
password    specifies the password required to access the remote host.  If 
password contains a space character, the name may be used by enclosing it in 
single quotation marks. 
account    specifies the account to be accessed on the remote host.  If 
account contains a space character, the name may be used by enclosing it in 
single quotation marks. 
Description: 
This command identifies the user to the remote ftpd server.  If any parameters 
are omitted, FTP prompts the user for logon information required by the remote 
host (disabling local echo for entry of the password).  This process is done 
automatically on initial connection to the remote ftpd server during the OPEN 
command, unless input is from XEQ, BATCH, or a file, in which case the USER 
command will need to be used before any useful work can be done. 
00002
00001
QUIT
