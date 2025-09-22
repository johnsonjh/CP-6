The REPLAY processor extracts any or all information from the console history 
file(s) and formats that information in human-readable form for display and 
review.  REPLAY selects the appropriate information based on: 
o   Time/date 
o   Console logon-id 
o   Console attribute 
o   Console workstation 
o   Console name 
To obtain more HELP information, see 
HELP (REPLAY) TOPICS                Displays available topics. 
HELP (REPLAY) COMMANDS              Displays a list of REPLAY 
                                    commands. 
HELP (REPLAY) command PARAM         Displays parameters associated 
                                    with a particular command. 
HELP (REPLAY) command DESCRIPTION   Displays description associated 
                                    with a particular command. 
?                                   Displays next level of HELP 
                                    messages. 
??                                  Displays all levels of HELP 
                                    messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
A list of REPLAY commands and their definitions can be accessed by typing a ? 
or ??.  To obtain definitions of individual commands, type 
HELP (REPLAY) COMMANDS command 
where command is any of the following: 
CONSOLE_REPORT, DATE, DIRECTORY, DISPLAY, DO, END, ENTER, 
ERASE, EXIT, HELP, LOGON_REPORT, OUTPUT, PRINT, QUIT, 
REPORT, RESET, SELECT, SPAN, TIME, TIME_RANGE, X 
  Command        Description 
  CONSOLE REPORT 
                 Specifies that a subsequent REPLAY report is to be limited to 
                 a summary of keyins entered. 
  {DATE|TIME} 
                 Displays the current time and date. 
  {DIRECTORY|DIR} 
                 Changes the default account and packset. 
  DISPLAY 
                 Displays the current settings of the SELECT options. 
  {DO|!} 
                 Enable IBEX command execution. 
  {END|EXIT|QUIT} 
                 Terminates REPLAY. 
  ENTER 
                 Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
                 Deletes accumulated output for logical devices. 
  HELP 
                 Displays documentation on processors and commands. 
  LOGON REPORT 
                 Specifies that a subsequent REPLAY report is to be limited to 
                 a summary of console logon/logoff activity. 
  OUTPUT 
                 Sends subsequent output to the specified file. 
  PRINT 
                 Directs that output accumulated for logical devices be sent 
                 to destinations immediately. 
  REPORT 
                 Generates a formatted playback of the console history. 
  RESET 
                 Resets to defaults the criteria for a subsequent REPLAY 
                 report. 
  SELECT 
                 Selects categories of information to be included in a 
                 subsequent REPLAY report. 
  {SPAN|TIME} 
                 Sets time span for a subsequent REPLAY report. 
00005
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
00006
00013
00014
00015
00016
00002
00016
00006
Format: 
CONS[OLE] RE[PORT] 
Description: 
This command specifies that a subsequent report is to be limited to a summary 
of keyins.  This can be helpful in monitoring the use of and strategically 
locating consoles.  The consoles will be identified in the report by logon (if 
any) and console station.  Only those consoles that had keyins entered on them 
during the current time span will be displayed.  In addition, the number of 
keyins done on each console and the percent of the total are displayed. 
Usage Note: 
The CONSOLE REPORT and LOGON REPORT commands are mutually exclusive. 
Specifying CONSOLE REPORT resets a request for LOGON REPORT and vice versa. 
00001
00002
CONSOLE_REPORT
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm    (month)(day)(year)(hours)(minutes) 
Examples: 
:DATE 
requests a display of the current date and time.  A sample display is: 
AUG 02  '88  11:03 
00001
00002
DISPLAY
Format: 
{DIR|DIRECTORY} [fid|R[ESET]] 
Parameters: 
fid    specifies the new default account fid, and may consist of an account or 
a packset name and an account. 
RESET    specifies that the default account is to be reset to the running 
account. 
Description: 
DIRECTORY changes the default account and packset.  The default account and 
packset are the account and associated packset that are selected if an account 
is not supplied as part of a disk file fid specification.  Initially, the 
default account is the logon or running account and the packset name is nil. 
When used without parameters, DIRECTORY displays the current directory 
pointer. 
Examples: 
:DIRECTORY .SYSLIB 
This command directs that subsequent fids that do not include an account are 
to default to the .SYSLIB account and the packset associated with that 
account. 
:DIRECTORY DP#UTIL.Y 
This command specifies that subsequent fids that do not include an account are 
to default to the Y account on the packset named UTIL. 
:DIRECTORY RESET 
This command re-establishes the running account and its associated packset as 
the default. 
00002
00003
00001
Format: 
DI[SPLAY] 
Description: 
This command displays the current settings of the SELECT options. 
The user will receive a list resembling the following: 
Console = SC01@LOCAL 
Logon = ? 
Workstation = ? 
Attribute type = ? 
Logon Report = NO 
Console Report = NO 
Wildcarding = NO 
00001
Format: 
{DO|!} IBEX-command 
Parameters: 
IBEX-command    any legal IBEX command.  See the CP-6 Programmer Reference 
Manual (CE40). 
Description: 
The DO command allows the user to execute an IBEX command without exiting the 
current processor. 
Note:  The ! (exclamation point) may be used instead of the word DO.  It 
should be noted however that if the ! is used in an XEQ file, it will 
terminate the current processor session unless preceded by at least one blank, 
or by a double ! (!!). 
Examples: 
:DO DI 
means display the current system status 
:!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00003
00001
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
These commands provide normal termination of REPLAY. 
00001
Format: 
ENTER [script_fid] [,frame_name] [initial_input] 
Parameters: 
script_fid    is the file identifier for the script to be executed. 
frame_name    is the first frame of the script to execute. 
initial_input    supplies responses to the initial prompts for the dialog. 
Description: 
The ENTER command invokes a CP-6 ADAPT dialog that permits use of precompiled, 
menu-driven user interfaces called compiled scripts.  script_fid identifies 
the file containing the compiled script for the dialog.  See the CP-6 ADAPT 
Reference Manual (HA12) for more information on using ADAPT dialogs. 
00002
00001
Format: 
ERASE [ALL|ldevlist] 
Parameters: 
ALL    specifies that the accumulated output for all logical devices is to be 
deleted.  This is the default. 
ldevlist    specifies that the accumulated output for the specified logical 
device or devices is to be deleted.  The list is entered in the format 
ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
ERASE deletes the accumulated output for logical devices. 
Examples: 
:ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
00001
END
Format: 
HELP [(processor)] [TOPICS] [keyword1] [-] [keyword2] 
Note:  The elements 
    [(processor)] 
    [TOPICS] 
    [keyword1] [-] [keyword2] 
can be entered in any sequence. 
Parameters: 
For IBEX HELP, type:  !HELP HELP PARAMETERS 
Description: 
For IBEX HELP, type:  !HELP HELP DESCRIPTION 
Examples: 
For IBEX HELP, type:  !HELP HELP EXAMPLES 
00002
00003
00001
C 
  CONSOLE REPORT Command - 
      HELP CONSOLE_REPORT 
D 
  DATE Command - 
      HELP DATE 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DISPLAY Command - 
      HELP DISPLAY 
  DISPLAY Command (REPLAY) - 
      HELP DISPLAY FORMAT: 
  DO Command - 
      HELP DO 
E 
  END Command - 
      HELP END 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
F 
  Files Created by REPLAY - 
      HELP RELATED_FILES 
H 
  HELP Command - 
      HELP HELP 
  History file - 
      HELP INVOKING_REPLAY 
I 
  Invoking REPLAY - 
      HELP INVOKING_REPLAY 
L 
  LOGON REPORT Command - 
      HELP LOGON_REPORT 
O 
  :OCHIST files - 
      HELP RELATED_FILES 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  POSTRANGE - 
      HELP LOGON_REPORT DESCRIPTION: 
  PRERANGE - 
      HELP LOGON_REPORT DESCRIPTION: 
  PRINT Command - 
      HELP PRINT 
  Privileges for Use of REPLAY - 
      HELP PRIVILEGES 
R 
  REPLAY -   
    CONSOLE REPORT Command - 
      HELP CONSOLE_REPORT FORMAT: 
    DISPLAY Command - 
      HELP DISPLAY FORMAT: 
    HELP Command - 
      HELP HELP FORMAT: 
    LOGON REPORT Command - 
      HELP LOGON_REPORT FORMAT: 
    REPORT Command - 
      HELP REPORT FORMAT: 
    RESET Command - 
      HELP RESET FORMAT: 
    SELECT Command - 
      HELP SELECT FORMAT: 
    SPAN/TIME Command - 
      HELP SPAN FORMAT: 
  REPLAY files - 
      HELP RELATED_FILES 
  REPLAY Output - 
      HELP MESSAGE_OUTPUT 
  REPORT Command - 
      HELP REPORT 
  REPORT Command (REPLAY) - 
      HELP REPORT FORMAT: 
  RESET Command - 
      HELP RESET 
  RESET Command (REPLAY) - 
      HELP RESET FORMAT: 
S 
  SELECT Command - 
      HELP SELECT 
  SELECT Command (REPLAY) - 
      HELP SELECT FORMAT: 
  SPAN|TIME Command - 
      HELP SPAN 
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
REPLAY can be run as a batch or on-line job.  It is invoked by the command: 
!REPLAY [specific-history-file] 
where 
specific-history-file    names the history file to be searched.  If no name is 
given, REPLAY searches the file :OCHIST.:SYSTAC and any file with a name of 
the form :OCHISTyyyymmdd.:SYSTAC, if it is part of the chain originating from 
:OCHIST.  Each of these files points to the previous history file, permitting 
REPLAY to search until it finds the appropriate console history or the end of 
the chain of files.  When examining a broken history file, REPLAY is able to 
search to the end of valid data.  Specifying specific-history-file is useful 
in the case that a history file not in the chain is to be searched; this could 
be the case for a history file stored on tape and later read back into 
:SYSTAC. 
The DCBs used by REPLAY are: 
o   M$SI for input 
o   M$LO for display output 
o   M$DO for diagnostic output 
When run as an on-line job, REPLAY solicits commands with the :  character. 
Commands can be written on multiple lines, using the semicolon to indicate 
line continuation. 
Format: 
LOG[ON] RE[PORT] 
Description: 
This command specifies that a subsequent report is to be limited to console 
logon/logoff activity.  Any consoles that logged on or off during the time 
span are reflected in the report (unless excluded by SELECT command options). 
The consoles are identified by logon (if any) and station.  If a console 
logged on prior to the span, the logon time is displayed as PRERANGE.  If a 
console logged on during the time span but logged off after the time span, the 
logoff time is displayed as POSTRANGE.  Multiple logons of the same console 
with logoff times of POSTRANGE indicate that either history logging was turned 
off and then turned back on, the console was disconnected, or the system 
crashed during the time span. 
Usage Note: 
The CONSOLE REPORT and LOGON REPORT commands are mutually exclusive. 
Specifying CONSOLE REPORT resets a request for LOGON REPORT and vice versa. 
00001
00002
LOGON_REPORT
The output generated by REPLAY appears as follows: 
1.  Operator keyins will be displayed in the form: 
    FROM device_name@terminal !keyin 
2.  Direct output messages will be displayed in the form: 
    TO device_name@terminal message 
3.  General output messages will be displayed in one of these formats: 
    TO console_type@wsn      message 
    TO console_type@terminal message 
    TO console_type          message 
    where console_type is of the following: 
    o   Device console 
    o   Administrative console 
    o   Communications console 
    o   System console 
    o   Administrative and Communications console 
    o   TP console 
Note:  Output is only preceded by TO or FROM if CONSOLE, LOGON, TYPE, or WSN 
is not selected.  Once a particular selection is made, the user is assumed to 
know where the messages are being sent and who is entering the keyins. 
Format: 
         [[ON  ] LP[@location]] 
OU[TPUT] [[OVER] fid          ] [(option[,option]...[)]] 
         [[INTO] ME           ] 
         [[TO  ]              ] 
Parameters: 
{ON|TO|OVER|INTO}    directs file output processing.  OVER causes an existing 
file to be overwritten.  INTO causes file extension.  ON and TO are synonyms 
used to create a new file.  If the file exists, an error will occur.  The 
default is ON. 
LP    directs output to the default line printer; @location specifies a 
particular workstation. 
fid    identifies the file to receive the output.  Output can be directed to 
any valid fid. 
ME    returns the output destination to the user's terminal. 
option    is one of the following: 
    F[ORM]={formname|'formname'}    Applies to unit record files and unit 
    record devices and specifies the name of a form to be mounted on a unit 
    record device.  formname is a 1-6 character string, which can be quoted. 
    The name must have been defined to the system by the system manager (via 
    the Form Definition File).  The default is blank, which means the default 
    form for a unit record device and form 'STDLP' for unit record files. 
    I[XTNSIZE]=value    Specifies an initial disk storage allocation (in 
    blocks) for the output file.  value must be in the range of 1 through 
    134217727.  The default is 2. 
    O[RGANIZATION={C[ONSECUTIVE]|U[NIT]R[ECORD]}    Specifies the organization 
    of the output file as either CONSECUTIVE or UNIT RECORD.  If this option 
    is not specified, the output file is created as a UR file. 
    X[TNSIZE]=value    Use of this option causes an automatic M$EXTEND when 
    needed.  value specifies a secondary disk storage allocation (in blocks) 
    for the output file, and must be in the range 1 through 32000.  The 
    default is 2. 
Description: 
This command sends subsequent output to a destination.  OUTPUT with no options 
redirects output to the original output destination. 
Examples: 
:OUTPUT ON OUTPUTFILE 
:OUTPUT ON ME 
00002
00003
00001
Format: 
PRINT [ALL|ldevlist] 
Parameters: 
ALL    specifies that the accumulated output for all logical devices is to be 
sent to destination(s) immediately.  This is the default. 
ldevlist    specifies that the accumulated output for the specified logical 
device or devices is to be sent to destination(s) immediately.  The list is 
entered in the format 
ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
PRINT directs that output accumulated for logical devices be sent to 
destination(s) immediately. 
Examples: 
:PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
00002
00003
00001
The user must have REPLAY PPRIV privilege to invoke REPLAY and examine console 
history files.  However, any user with appropriate account access controls has 
access to the REPLAY display files created in that account. 
END
REPORT
REPLAY obtains its information from the :OCHIST files created by the KEYIN 
ghost and placed in the :SYSTAC account.  REPLAY will create files whose 
contents are REPLAY displays.  These files are user-requested and user-named. 
Format: 
R[EPORT] [{ON  }]  {ME } 
         [{OVER}]  {LP } 
                   {fid} 
Parameters: 
ME    directs the replay to the operator initiating the REPLAY.  This is the 
default. 
LP    directs the replay to the line printer. 
fid    directs the replay to a specified file. 
Description: 
This command generates a formatted playback of the console history. 
00002
00001
Format: 
RES[ET] [{S[PAN]|T[IME]}   ] 
        [CONS[OLE]         ] 
        [WSN               ] 
        [LOG[ON]           ] 
        [TYP[E]            ] 
        [LOG[ON] RE[PORT]  ] 
        [CON[SOLE] RE[PORT]] 
        [WILD[CARDING]     ] 
Parameters: 
{S[PAN]|T[IME]}    resets time span default as described for the TIME/SPAN 
command. 
CONS[OLE] 
WSN 
LOG[ON] 
TYPE    resets this criterion to the default as described for the SELECT 
command. 
LOG[ON] RE[PORT]    cancels a request for a summary of console logons. 
CON[SOLE] RE[PORT]    cancels a request for a summary of keyins. 
WILD[CARDING]    cancels a request to wildcard. 
Description: 
This command resets the specified option to its default value.  If no options 
are specified, all options are reset to their defaults. 
00002
00001
Format: 
SEL[ECT] [option] 
Parameters: 
option    is any of the options that can be displayed by typing HELP (REPLAY) 
SELECT_OPTS 
Description: 
This command selects the information to be formatted and displayed.  The user 
may select both keyins and console messages for a specified WSN or CONSOLE 
(via the WSN, LOGON, or CONSOLE options), may select system generated console 
messages for a specified console attribute (via the TYPE option), or may 
select wildcarded strings in the file (via the PATTERN option). 
Example: 
SEL[ECT] C[ONSOLE]=?@? 
SEL[ECT] WSN      =? 
00002
00003
00001
A list of SELECT command options and their definitions can be accessed by 
typing a ? or ??.  To display a particular option, type 
HELP (REPLAY) SELECT_OPTS option 
where options is CONSOLE, LOGON, PATTERN, TYPE, or WSN. 
  Option         Description 
  C[ONSOLE]=console_name @station_name 
                 Replays console activity for a particular console. 
                 console_name    specifies a console (4 characters maximum). 
                 station_name    is a legal terminal or station, as defined by 
                 SUPER. 
  LOG[ON]=logon_string 
                 Replays console activity for a specific logon identification. 
                 logon_string    is a legal console identifier.  The default 
                 is all logons. 
  P[ATTERN]=[?]search_pattern[?] 
                 Replays console activity containing the string specified by 
                 search_pattern.  If search_pattern contains blanks, the 
                 request must be delimited by single quotes (e.g., SEL P 
                 '?WJPTEST on ?'). 
  T[YPE]={SYS[TEM]|{DEV[ICE]@TWSN}|{ADM[IN]@WSN}|{COM[M]}|{TP} 
                 Replays system generated console messages (but not keyins) 
                 for the specified consoles. 
                 SYSTEM    prints all messages sent to system consoles. 
                 DEVICE@TWSN    prints all messages sent to a device console 
                 at a particular TERMINAL. 
                 ADMIN@WSN    prints all messages sent to an ADMINistrative 
                 console at a chosen WSN. 
                 COMM    prints all messages sent to communications consoles. 
                 TP    prints all messages sent to TP consoles. 
  W[SN]=wsn_name 
                 Replays console activity for a specific workstation (WSN). 
                 wsn_name    is a valid name.  The default is all 
                 workstations. 
00001
00002
00003
00004
00005
Format: 
{S[PAN]|T[IME]} [=] {start [-stop]} 
                    {-stop        } 
Parameters: 
start and stop    specify any of the following: 
    hh:mm 
    mm/dd/yy 
    hh:mm,mm/dd/yy 
    hh:mm mm/dd/yy 
    mm/dd/yy,hh:mm 
    mm/dd/yy hh:mm 
The default for start is 00:00 of the present day, and for stop is 23:59 of 
the present day. 
Description: 
This command specifies a time span for using REPLAY without regard to specific 
files.  When a range reflects a beginning time prior to the present history 
file (:OCHIST.:SYSTAC), REPLAY can follow a chain of backward pointers through 
previous history files.  The chain will be traversed until the time request 
can be satisfied, or until the chain is broken.  If the former condition 
occurs, REPLAY proceeds forward until the requested ending time is satisfied; 
otherwise the user will receive a warning message and REPLAY will proceed 
forward with whatever history files it was able to find, trying to satisfy as 
much of the specified time span as possible. 
Usage Notes: 
1.  From 1 to 4 of the above options may be entered. 
2.  Dates and times may be interchangeable (for example, the beginning of the 
    range could be entered hh:mm, mm/dd/yy). 
3.  The end of the range may be entered before the beginning of the range by 
    preceding the end with the necessary dash (-). 
4.  If the user enters a beginning time (without specifying a date), REPLAY 
    assumes the current date, not the beginning date of the file. 
00002
00001
00003
DATE
SPAN
END
