Format: 
TELNET [ host [, port ]] 
Parameters: 
host    specifies a host by name or by Internet address (four decimal numbers, 
0-255, separated by dots). 
port    specifies a port number (0-65535). The default port number is 23. 
Description: 
TELNET is used to open a connection to a specified host.  If no port number is 
specified, TELNET attempts to contact a TELNET server at the default port. 
The host specification may be either a host name or an Internet address 
specified in the dot notation. 
If no host is specified, TELNET enters its command mode and prompts for 
commands with the prompt "Telnet>". 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
OPEN
Format: 
CL[OSE] 
Parameters: 
None. 
Description: 
The CLOSE command terminates a TELNET connection and remains in command mode. 
00002
00001
OPEN
DISPLAY
Format: 
{ DATE | TIME } 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
     mmm dd 'yy hh:mm   (month)(day)(year)(hours)(minutes) 
Examples: 
TELNET>DATE 
requests a display of the current date and time.  A sample display is 
     AUG 02  '89  11:03 
00001
00002
Format: 
{ DIR | DIRECTORY } [ fid | R[ESET] ] 
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
TELNET>DIRECTORY .SYSLIB 
directs that subsequent fids, that do not include an account, are to default 
to the .SYSLIB account and the packset associated with that account. 
TELNET>DIRECTORY DP#UTIL.Y 
specifies that subsequent fids, that do not include an account, are to default 
to the Y account on the packset named UTIL. 
TELNET>DIRECTORY RESET 
re-establishes the running account and its associated packset as the default. 
00002
00003
00001
Format: 
D[ISPLAY] [ optlist ] 
Parameters: 
optlist    specifies the particular SET and TOGGLE values to be displayed. 
The list is entered in the form 
    option [,option] ... 
See SET_OPTIONS and TOGGLE_OPTIONS 
Description: 
The DISPLAY command displays all, or some, of the SET and TOGGLE values. 
00002
00001
Format: 
{ DO | ! } IBEX-command 
Parameters: 
IBEX-command    any legal IBEX command. 
Description: 
The DO command allows the user to execute an IBEX command without exiting the 
current processor. 
Note:  The ! (exclamation point) may be used instead of the word DO.  It 
should be noted, however, that if the ! is used in an XEQ file, it will 
terminate the current processor session unless preceded by at least one blank, 
or by another ! (!!). 
Examples: 
TELNET>DO DI 
or 
TELNET>! DI 
Both examples display the current system status. 
00002
00003
00001
QUIT
Format: 
ENTER [ script_fid ] [ ,frame_name ] [ initial_input ] 
Parameters: 
script_fid    is the file identifier for the script to be executed. 
frame_name    is the first frame of the script to execute. 
initial_input    supplies responses to the initial prompts for the dialog. 
Description: 
The ENTER command invokes a CP-6 ADAPT dialog that permits use of precompiled, 
menu-driven user interfaces called compiled scripts.  script_fid identifies 
the file containing the compiled script for the dialog.  Type 'HELP (ADAPT) 
DIALOG_MANAGER' for more information on using ADAPT dialogs. 
00002
00001
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
TELNET>ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
00001
QUIT
Format: 
H[ELP] [ (fid) ] [ TOPICS ] [ keyword1 [-] [ keyword2 ]] 
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
C 
  CLOSE Command - 
      HELP CLOSE 
  COMMAND MODE - 
      HELP TOGGLE_OPTIONS COMMAND_MODE 
  cp6 Command - 
      HELP cp6 
  cp6 Server - 
      HELP cp6_SERVER 
  cp6 Sever -   
    cp6 Command - 
      HELP cp6 
  cp6rfep Server - 
      HELP cp6rfep_SERVER 
D 
  DATE Command - 
      HELP DATE 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DISPLAY Command - 
      HELP DISPLAY 
  DO Command - 
      HELP DO 
E 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
H 
  HELP Command - 
      HELP HELP 
M 
  MODE Command - 
      HELP MODE 
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
Q 
  QUIT Command - 
      HELP QUIT 
R 
  READ Command - 
      HELP READ 
S 
  SEND Command - 
      HELP SEND 
  SET Command - 
      HELP SET 
  STATUS Command - 
      HELP STATUS 
T 
  TELNET -   
    ! Command - 
      HELP DO FORMAT: 
    ? and ?? Commands - 
      HELP ?_AND_??_COMMANDS 
    CLOSE Command - 
      HELP CLOSE FORMAT: 
    CONNECT Command - 
      HELP OPEN FORMAT: 
    DATE Command - 
      HELP DATE FORMAT: 
    DIRECTORY Command - 
      HELP DIRECTORY FORMAT: 
    DISPLAY Command - 
      HELP DISPLAY FORMAT: 
    DO Command - 
      HELP DO FORMAT: 
    END Command - 
      HELP QUIT FORMAT: 
    ENTER Command - 
      HELP ENTER FORMAT: 
    ERASE Command - 
      HELP ERASE FORMAT: 
    EXIT Command - 
      HELP QUIT FORMAT: 
    HELP Command - 
      HELP HELP FORMAT: 
    MODE Command - 
      HELP MODE FORMAT: 
    OPEN Command - 
      HELP OPEN FORMAT: 
    OUTPUT Command - 
      HELP OUTPUT FORMAT: 
    PRINT Command - 
      HELP PRINT FORMAT: 
    QUIT Command - 
      HELP QUIT FORMAT: 
    READ Command - 
      HELP READ 
    SEND Command - 
      HELP SEND FORMAT: 
    SEND Options - 
      HELP SEND_OPTIONS 
    SET Command - 
      HELP SET FORMAT: 
    SET Options - 
      HELP SET_OPTIONS 
    STATUS Command - 
      HELP STATUS FORMAT: 
    TIME Command - 
      HELP DATE FORMAT: 
    TOGGLE Command - 
      HELP TOGGLE FORMAT: 
    TOGGLE Options - 
      HELP TOGGLE_OPTIONS 
  TELNET Program - 
      HELP TELNET 
  telnetd Server - 
      HELP telnetd_SERVER 
  Terminal Access Services - 
      HELP TERMINAL_ACCESS_SERVICES 
  TOGGLE Command - 
      HELP TOGGLE 
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
HELP_INDEX
Format: 
M[ODE] type 
Parameters: 
type    specifies LINE, for line-by-line mode, or CHARACTER, for 
character-at-a-time mode. 
Description: 
The MODE command requests permission of the remote host to enter the requested 
mode.  If the remote host is capable of entering that mode, the requested mode 
will be entered. 
00002
00001
Format: 
{ O[PEN] | C[ONNECT] } host [ [,] port ] 
Parameters: 
host    specifies a host by name or by Internet address (four decimal numbers, 
0-255, separated by dots). 
port    specifies a port number (0-65535). The default port number is 23. 
Description: 
This command establishes a connection to the specified host.  If no port 
number is specified, TELNET will attempt to contact a TELNET server at the 
default port.  Upon successful connection, TELNET enters data mode, where 
input from the terminal is forwarded to the remote host, and output from the 
remote host is displayed on the terminal.  To return to command mode, the 
escape character must be entered (see the topic SET).  The TOGGLE command also 
affects the data mode behavior. 
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
    F[ORM]={formname|'formname'}    Applies to unit record files and unit 
    record devices, and specifies the name of a form to be mounted on a unit 
    record device.  formname is a 1-6 character string, which can be enclosed 
    in quotes.  The name must have been defined to the system by the system 
    manager (via the Form Definition File).  The default is blank, which 
    specifies the default form for a unit record device, and 'STDLP' form for 
    unit record files. 
    I[XTNSIZE]=value    Specifies an initial disk storage allocation (in 
    blocks) for the output file.  value must be in the range of 1 through 
    134217727.  The default is 2. 
    O[RGANIZATION]={C[ONSECUTIVE]|U[NIT]R[ECORD]}    Specifies the 
    organization of the output file as either CONSECUTIVE or UNIT RECORD (UR). 
    If this option is not specified, the output file is created as a UR file. 
    X[TNSIZE]=value    Use of this option causes an automatic M$EXTEND when 
    needed.  value specifies a secondary disk storage allocation (in blocks) 
    for the output file, and must be in the range 1 through 32000.  The 
    default is 2. 
Description: 
This command sends subsequent output to the specified file or device. 
Examples: 
TELNET>OUTPUT ON OUTPUTFILE 
TELNET>OUTPUT ON ME 
00002
00003
00001
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
TELNET>PRINT LP01,LP02 
causes the accumulated output associated with logical devices LP01 and LP02 to 
be sent immediately to the associated destinations. 
00002
00003
00001
Format: 
{ Q[UIT] | E[ND] | [E]X[IT] } 
Parameters: 
None. 
Description: 
This command terminates any open TELNET session and exits TELNET.  An 
end-of-file (in command mode) will also close a session and exit. 
00002
00001
Format: 
R[EAD] fid 
Parameters: 
fid     any valid CP-6 file identifier. 
Description: 
This command directs TELNET to read subsequent commands from the indicated 
file.  When the end of the file is reached, an error message is displayed 
before input reverts to ME.  Input reverts also when any other errors are 
encountered while READing.  READ ME should be used to terminate a file of 
TELNET commands to avoid the error message. 
00002
00001
Format: 
Form 1: 
S[END] optlist 
Form 2: 
S[END] 'string1' [, CR ] [ A[FTER] 'string2' ] 
Parameters: 
optlist    specifies one or more special character sequence options.  The 
option list is entered in the form 
    option [,option] ... 
The options are listed under the topic SEND_OPTIONS. 
string1    specifies a string of characters to be sent. 
string2    specifies a string of characters expected to be received. 
Description: 
The SEND command sends one or more special character sequences to the remote 
host.  Form 2 of the SEND command sends string1 (possibly followed by an 
end-of-line) to the remote host, possibly after first waiting for string2 to 
be received from the the remote host.  Form 2 makes it possible and convenient 
to place TELNET sessions in XEQ files. 
Example: 
The example below is an XEQ file that will log on to a UNIX system. 
!telnet 
tog command 
con dpx2 
mode line 
send 'dolly', cr af 'gin:' 
send 'password', cr after 'rd:' 
tog command 
line 1 of the XEQ program gives the instruction to invoke the telnet program. 
line 2 toggles the command mode on the telnet program.  This instructs telnet 
    to remain in command mode and control will still reside on the CP-6 host 
    even after a connection is open to the UNIX side. 
line 3 sends an open connection request to the UNIX system DPX2.  Control 
    still resides with the CP-6 host telnet because of the "tog command" 
    instruction on line 2. 
line 4 informs the UNIX system that each TCP/IP packet received will be one 
    line of information delimited by a carriage return. 
line 5 instructs telnet to send the string 'dolly' followed by a carriage 
    return only after reciving the string 'gin:'.  The string 'gin:' is a 
    substring of the UNIX logon prompt 'login:'. 
line 6 instructs telnet to send the string 'password' followed by a carriage 
    return, after receiving the string 'rd:'.  The string 'rd:' is a substring 
    of the UNIX password prompt 'password:'. 
line 7 instructs telnet to exit command mode and commence data mode.  Control 
    is then transferred to the UNIX system.  The user will then be logged on 
    to the UNIX system. 
00002
00003
00001
Enter ? or ?? to see options in 2-column tabular format, as follows: 
  Option               Meaning 
  {AO|F[LUSHOUTPUT]} 
                       Sends the TELNET AO (Abort Output) sequence, which 
                       should cause the remote system to flush all output from 
                       the remote system to the user's terminal. 
  AY[T] 
                       Sends the TELNET AYT (Are You There) sequence, to which 
                       the remote system may or may not choose to respond. 
  {B[REAK]|BRK} 
                       Sends the TELNET BRK (Break) sequence, which may have 
                       significance to the remote system. 
  {DM|S[YNC]} 
                       Sends the TELNET SYNCH sequence.  This sequence causes 
                       the remote system to discard all previously typed (but 
                       not yet read) input.  This sequence is sent as TCP 
                       urgent data and may not work if the remote system is a 
                       4.2 BSD system.  (If it does not work, a lowercase 'r' 
                       may be echoed on the terminal.) 
  {EC|ER[ASE]} 
                       Sends the TELNET EC (Erase Character) sequence which 
                       should cause the remote system to erase the last 
                       character entered. 
  {EL|K[ILL]} 
                       Sends the TELNET EL (Erase Line) sequence, which should 
                       cause the remote system to erase the line currently 
                       being entered. 
  ES[CAPE] 
                       Sends the current TELNET escape character (default is 
                       BREAK), which otherwise cannot be sent. 
  GA 
                       Sends the TELNET GA (Go Ahead) sequence, which has no 
                       significance to the remote system. 
  {IP|I[NTERRUPT]} 
                       Sends the TELNET IP (Interrupt Process) sequence, which 
                       should cause the remote system to abort the currently 
                       running process. 
  N[OP] 
                       Sends the TELNET NOP (No OPeration) sequence. 
00001
00002
00003
00003
00004
00005
00006
00005
00007
00001
00008
00009
00009
00006
00010
00004
Format: 
SET option [[=] { c | BREAK | ^c | CNTL-c }] 
Parameters: 
option    specifies any one of a number of TELNET variables.  See SET_OPTIONS 
for a list of these variables. 
c    is any single character. 
^c or CNTL-c    indicate the control character formed by pressing the control 
key along with "c". 
Description: 
The SET command sets any one of a number of TELNET variables to a specific 
value.  Specifying no value resets the option to the undefined state.  The 
values of variables may be interrogated with the DISPLAY command. 
00002
00001
Enter ? or ?? to see options in 2-column tabular format, as follows: 
  Option               Meaning 
  {AO|F[LUSHOUTPUT]} 
                       If TELNET is in LOCALCHARS mode (see the TOGGLE 
                       LOCALCHARS option) and the FLUSHOUTPUT character is 
                       typed, a TELNET AO sequence (see the SEND AO option) is 
                       sent to the remote host.  The initial value for the 
                       FLUSH character is undefined. 
  {B[REAK]|BRK|Q[UIT]} 
                       If TELNET is in LOCALCHARS mode (see the TOGGLE option 
                       LOCALCHARS) and the QUIT character is typed, a TELNET 
                       BRK sequence (see the SEND BRK option) is sent to the 
                       remote host.  The initial value for the QUIT character 
                       is undefined. 
  {EL|K[ILL]} 
                       If TELNET is in LOCALCHARS mode (see the TOGGLE 
                       LOCALCHARS option) and if TELNET is operating in 
                       character-at-a-time mode, then when the EL character is 
                       typed, a TELNET EL sequence (see the SEND EL option) is 
                       sent to the remote system.  The initial value for the 
                       KILL character is CNTL-X. 
  EO[F] 
                       If TELNET is operating in line-by-line mode, entering 
                       the EOF character as the first character on a line will 
                       cause this character to be sent to the remote system. 
                       The initial value of the EOF character is CNTL-D. 
  {ER[ASE]|EC} 
                       If TELNET is in LOCALCHARS mode (see the TOGGLE 
                       LOCALCHARS option), and if TELNET is operating in 
                       character-at-a-time mode, then when the ERASE character 
                       is typed, a TELNET EC sequence (see the SEND EC option) 
                       is sent to the remote system.  The initial value for 
                       the erase character is DEL (CNTL-?). 
  ES[CAPE] 
                       This is the TELNET escape character (default is BREAK) 
                       which causes entry into TELNET command mode (when 
                       connected to a remote system). 
  {IP|I[NTERRUPT]} 
                       If TELNET is in LOCALCHARS mode (see TOGGLE LOCALCHARS) 
                       and the INTERRUPT character is typed, a TELNET IP 
                       sequence (see the SEND IP option) is sent to the remote 
                       host.  The initial value for the interrupt character is 
                       CNTL-Y. 
00001
00002
00002
00005
00003
00004
00005
00006
00001
00007
00007
00003
00002
Format: 
ST[ATUS] 
Parameters: 
None. 
Description: 
The STATUS command shows the current status of TELNET.  This information 
identifies the remote host the user is connected to, as well as the current 
mode and escape character. 
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
T[OGGLE] optlist 
Parameters: 
optlist    specifies one or more options.  The option list is entered in the 
form 
    option [,option] ...  The options are listed under the TOGGLE_OPTIONS 
topic. 
Description: 
The TOGGLE command toggles various flags that control how TELNET responds to 
events.  The state of these flags may be interrogated with the DISPLAY 
command. 
00002
00001
Enter ? or ?? to see options in 2-column tabular format, as follows: 
  Option               Meaning 
  AUTOF[LUSH] 
                       If AUTOFLUSH and LOCALCHARS are both true, then when 
                       the AO, IP, or QUIT characters are recognized (and 
                       transformed into TELNET sequences; see SET_OPTIONS for 
                       details), TELNET refuses to display any data on the 
                       user's terminal until the remote system acknowledges 
                       (via a TELNET Timing Mark option) that it has processed 
                       those TELNET sequences.  The initial value for this 
                       toggle is false. 
                       This option is not implemented. 
  AUTOS[YNC] 
                       If AUTOSYNC and LOCALCHARS are both true, then when 
                       either the IP or QUIT character is typed (see 
                       SET_OPTIONS for descriptions of IP and QUIT character), 
                       the resulting TELNET sequence is sent followed by the 
                       TELNET SYNCH sequence.  This procedure should cause the 
                       remote system to begin throwing away all previously 
                       typed input until both of the TELNET sequences have 
                       been read and acted upon.  The initial value of this 
                       toggle is false. 
                       This option is not implemented. 
  CO[MMAND MODE] 
                       When COMMAND MODE is true, after an OPEN command TELNET 
                       continues reading commands instead of entering data 
                       mode.  This option makes it possible and convenient to 
                       place TELNET sessions in XEQ files.  (See the example 
                       under the SEND topic.)  The initial value for this 
                       option is false. 
  C[RMOD] 
                       Toggles carriage return mode.  When this mode is 
                       enabled, most carriage return characters received from 
                       the remote host will be mapped into a carriage return 
                       followed by a line feed.  This mode does not affect 
                       those characters typed by the user, only those received 
                       from the remote host.  This mode is not very useful 
                       unless the remote host sends only carriage returns, and 
                       never line feeds.  The initial value for this toggle is 
                       false. 
                       This option is not implemented. 
  E[SCAPE] [D[ELAY]] 
                       The initial value of this option is ON.  This option 
                       delays the sending of the ESC character.  This is 
                       especially desirable when the user requires the use of 
                       the escape arrow keys sequences for cursor movement. 
  D[EBUG] 
                       Toggles socket level debugging (useful only to the 
                       SUPERuser).  The initial value for this flag is false. 
                       This option is not implemented. 
  L[OCALCHARS] 
                       If this flag is true, then the FLUSH, INTERRUPT, QUIT, 
                       ERASE, and KILL characters (see the SET options) are 
                       recognized locally, and transformed into appropriate 
                       TELNET control sequences:  AO, IP, BRK, EC, and EL, 
                       respectively.  (See SEND_OPTIONS.)  The initial value 
                       for this flag is false. 
  N[ETDATA] 
                       Toggles the display of all network data (in hexadecimal 
                       format).  The initial value for this toggle is false. 
  O[PTIONS] 
                       Toggles the display of some internal Telnet protocol 
                       processing (having to do with TELNET options).  The 
                       initial value for this flag is false. 
                       This option is not implemented. 
  S[TRIPPARITY] 
                       If STRIPPARITY is true, TELNET sends only the lower 7 
                       bits of each terminal input character to the remote 
                       host.  The initial value for this flag is true. 
00001
00002
00003
00004
00006
00005
00007
00008
00009
00010
QUIT
Format: 
cp6 [options] 
Options: 
The following options can be specified when you invoke the cp6 server: 
  -b bufsize 
  -c channel 
  -d mmrintchc 
  -h help 
  -l logon 
  -m memory 
  -p port 
  -t timeout 
where 
bufsize - sets the asynchronous buffer size (in bytes) for asynchronous (only) 
handlers.  Note that the actual buffer allocated in the FEP is rounded up, if 
necessary, to the next power of 2.  For example, BUFSIZE=100 results in 
allocation of the 128-byte buffer.  The maximum size that can be specified for 
n is 16384.  The default is -1, which means DC. 
channel - specifies the channel id, in hexadecimal, of a configuration to use 
(e.g., 4f80).  Note that the values are like those on LCP-6 so that NETCON 
does not get confused.  This option may be useful for specifying such things 
as automatic profiles, logons, line-speeds, etc.  The default is to use the 
next available unused and unconfigured channel, using the DEFAULT 
configuration for ASYNC. 
mmrintchc - specifies the debug flags (in hex) to be used while running the 
buddy-space manager.  The values are the same as for the ASYNC handler, except 
that a new flag (200 hex) has been added; 200 hex permits the buddy-space 
manager to expand the available space up to 16 times before aborting the 
session.  The default is 8200, specifying bitmap self-checking and space 
expansion. 
help - displays the meaning of all the options provided by the server. 
logon - specifies a logon string to be sent to the CP-6 system. 
memory - specifies the initial memory allocation in decimal kilobytes.  The 
default is 16. 
port - specifies the decimal port number that cp6 is to listen on when invoked 
as a server.  Specifying this option invokes cp6 as a server.  A port value of 
zero is used when invoking cp6 as a server started by inetd. 
timeout - specifies the watchdog timer interval in decimal seconds.  If the 
cp6 process is unable to access the communications connections for this 
interval it will abort, producing a khd-1314 dump.  A value of zero disables 
this facility. 
Description: 
Invokes the cp6 server which runs on the UNIX FEP and is responsible for 
providing users on remote computers terminal access to the CP-6 host.  Its 
function is analogous to the function of the asynch handler on the LCP-6 FEP. 
For more information, enter ? 
00002
00001
The cp6 server runs on the UNIX FEP. This rununit is the software that 
provides the connectivity to the CP-6 host by users on the network. There are 
four ways in which the cp6 server is invoked. The first way is via the super 
server, inetd. The second way is to start the server as a stand-alone server, 
specifying the port on which it should listen. The third way is for any user 
logged onto the UNIX FEP to interactively execute the "cp6" command. The 
fourth way is with the use of the telnetd server. 
Having invoked the cp6 server, you will, if not logged on automatically, be 
connected to the nodeadmin process in the DPX/2-300, which salutes much like a 
standard LCP-6 FEP.  Unlike on the LCP-6 FEP, <CNTL-Y> or <BREAK> will 
immediately terminate the logon process and exit from the cp6 process.  If you 
connected through Telnet, you will also exit from your Telnet client. 
Since the connection to your actual terminal is much farther removed from the 
cp6 process than it is from VDH in an LCP-6 FEP, certain output-controlling 
functions will work less responsively than with LCP-6; <ESC-H>, <CNTL-X>, and 
<BREAK> in particular will be affected.  The effect can be minimized by making 
sure that the line-speed you are using matches the actual character display 
speed on the terminal.  Use the IBEX TERMINAL command to adjust the speed, if 
necessary.  Flow control of the XON-XOFF variety will work properly only if it 
is being performed at the closest communications control service to the 
terminal: that usually means the UNIX computer you issued the telnet command 
from (use stty if necessary), or the terminal server to which you are more 
directly connected. 
Neither <BREAK> nor <DISCONNECT> is representable as an 8-bit character, so 
the cp6 process understands certain Telnet commands instead.  The IP command 
is interpreted as <BREAK>, and the BRK command as <DISCONNECT>.  You can 
probably configure your Telnet client or terminal server to send the IP 
command in response to the <BREAK> key on the terminal.  For Disconnect you 
will probably have to use a local command (usually "send brk").  Network 
disconnect is also interpreted as <DISCONNECT>, so the local command "quit" 
would have the same effect. 
FPRGs do not work; there is no LCP-6 operating system on the DPX/2-300 to 
support them. 
The cp6rfep rununit is a server on the UNIX FEP that allows other DPX and XPS 
systems on the network to act as remote FEPs.  When users on a remote UNIX FEP 
invoke the cp6 command, they will receive a connection to the nodeadmin 
process running on the remote FEP. 
The remote nodeadmin process on the remote FEP connects to the cp6rfep server 
running on the local FEP, which in turn connects to the nodeadmin running on 
the local FEP. This connection is then passed all the way up to the host. 
The cp6rfep server does not require as much processing overhead as the cp6 
server. It will, therefore, support more Telnet connections than two local 
FEPs. In addition, only one FEP will require a DIB. 
The telnetd server for the CP-6 implementation of TCP/IP has been modified to 
invoke the cp6 command. To do this, inetd calls the telnetd rununit, 
specifying the following options: 
     CP6@Telnet@Server/usr/bin/cp6 cp6@ -m32 
All beta versions of TCP/IP used the telnetd server to get terminal access to 
the CP-6 host. This method was limited by the number of ptys allowed on the 
system: each user connected to the CP-6 host used a psuedo terminal type 
(ptty). 
The A00 version of TCP/IP allows inetd to call the cp6 server directly. The 
overhead required for each connection is reduced and the ptty limitation is 
removed. 
