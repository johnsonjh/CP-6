The GOOSE processor provides for the automatic scheduling of functions on the 
CP-6 system.  These functions include a subset of operator commands, sending 
messages to consoles, and startup of ghost users.  GOOSE tasks are scheduled 
by placing commands in the control file GOOSE_EGG.:SYS, which may be prepared 
by using the EDIT processor. 
To obtain more HELP information, see 
HELP (GOOSE) TOPICS               Displays available topics. 
HELP (GOOSE) COMMANDS             Displays list of commands. 
HELP (GOOSE) command PARAM        Displays parameters 
                                  associated with a 
                                  particular command. 
HELP (GOOSE) command DESCRIPTION  Displays description 
                                  associated with a 
                                  particular command. 
?                                 Displays next level of 
                                  HELP messages. 
??                                Displays all levels of 
                                  HELP messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
Format: 
                  { ON            } 
                  { OFF           } 
AUTO S[CHEDULING] { M[ESSAGE] ON  } 
                  { M[ESSAGE] OFF } 
                  { U[PDATE]      } 
Parameters: 
ON    turns on auto-scheduling of commands stored in internal tables which 
were set from the GOOSE_EGG.:SYS file. 
OFF    turns off auto-scheduling of commands. 
MESSAGE ON    turns on reporting of commands to the system console. 
MESSAGE OFF    turns off reporting of commands to the system console. 
UPDATE    informs GOOSE that the GOOSE_EGG file has changed.  GOOSE then reads 
all records out of GOOSE_EGG and updates its internal tables. 
Description: 
This command allows the operator to control GOOSE by enabling or inhibiting 
the processing of commands in the GOOSE_EGG file. 
Usage Note: 
The AUTO SCHEDULING command may be used only as a direct GOOSE command. 
00002
00001
00003
AUTO_SCHEDULING
    The GOOSE commands are divided into two categories:  GOOSE commands for 
    GOOSE_EGG files and direct GOOSE commands.  A list of GOOSE commands and 
    their definitions can be accessed by typing a ? or ??.  To obtain 
    definitions of individual commands, type 
    HELP (GOOSE) COMMANDS command 
    where command is any of the following: 
    AUTO_SCHEDULING, AUTO_SCHEDULING_MESSAGE, AUTO_SCHEDULING_UPDATE, DATE, 
    DIRECTORY, DO, END, ENTER, ERASE, EVALUATE, EXIT, HELP, KEYIN, LIST, 
    MESSAGE, OUTPUT, PRINT, QUIT, START, TIME, UPDATE 
  Command        Description 
  AUTO SCHEDULING {ON|OFF} 
                 Turns on or off the auto-scheduling of commands. 
                 Category: Direct/Operator Keyin.       Privilege: MSYS. 
  AUTO SCHEDULING MESSAGE {ON|OFF} 
                 Turns on or off GOOSE's reporting of commands to system 
                 console. 
                 Category: Direct/Operator Keyin.       Privilege: MSYS. 
  AUTO SCHEDULING UPDATE 
                 Forces a wake up of the GOOSE ghost mode. 
                 Category: Direct/Operator Keyin.       Privilege: MSYS. 
  {DATE|TIME} 
                 Displays the current time and date. 
                 Category: Direct/Operator Keyin.       Privilege: None. 
  {DIRECTORY|DIR} 
                 Changes the default account and packset. 
                 Category: Direct/Operator Keyin.       Privilege: None. 
  {DO|!} 
                 Enables IBEX command execution. 
                 Category: Direct/Operator Keyin.       Privilege: None. 
  {END|EXIT|QUIT} 
                 Causes GOOSE to exit. 
                 Category: Direct/Operator Keyin.       Privilege: None. 
  ENTER 
                 Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
                 Deletes accumulated output for logical devices. 
                 Category: Direct/Operator Keyin.       Privilege: None. 
  EVALUATE 
                 Displays date differences and date intervals.  Translates 
                 Julian dates to Gregorian dates. 
                 Category: Direct/Operator Keyin.       Privilege: None. 
  HELP 
                 Displays information on the GOOSE processor and other 
                 processors. 
                 Category: Direct/Operator Keyin.       Privilege: None. 
  KEYIN 
                 Performs a specified KEYIN at an appropriate time. 
                 Category: GOOSE_EGG.                   Privilege: MSYS. 
  LIST 
                 Displays the current GOOSE_EGG. 
                 Category: Direct/Operator Keyin.       Privilege: MSYS. 
  MESSAGE 
                 Sends a message to the system console. 
                 Category: GOOSE_EGG.                   Privilege: MSYS. 
  OUTPUT 
                 Directs process or output to a destination. 
                 Category: Direct/Operator Keyin.       Privilege: None. 
  PRINT 
                 Directs that output accumulated for logical devices be sent 
                 to destinations immediately. 
                 Category: Direct/Operator Keyins.      Privilege: None. 
  START 
                 Starts a particular ghost job. 
                 Category: GOOSE_EGG for jobs to be Auto-scheduled, or 
                 Direct/Operator Keyin to submit job for one-time execution. 
                 Privilege: User authorization for ghost jobs required. 
  UPDATE 
                 Allows the user to update the GOOSE_EGG file. 
                 Category: Direct/Operator Keyin.       Privilege: MSYS. 
00006
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
00007
00011
00012
00013
00014
00015
00016
00007
00017
00004
00018
COMMANDS
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
    mmm dd 'yy hh:mm  (month)(day)(year)(hours)(minutes) 
Usage Note: 
The DATE and TIME commands may be used only as direct GOOSE commands. 
Examples: 
:DATE 
requests a display of the current date and time.  A sample display is: 
    MAR 02  '86  11:03 
00001
00003
00002
Format: 
{DIR|DIRECTORY} [fid|R[ESET]] 
Parameters: 
fid    specifies the new default account fid, and may consist of an account or 
a packset name and an account. 
RESET    specifies that the default account is to be reset to the running 
account. 
Description: 
DIRECTORY (and its synonym DIR) changes the default account and packset.  The 
default account and packset are the account and associated packset that are 
selected if an account is not supplied as part of a disk file fid 
specification.  Initially, the default account is the logon or running account 
and the packset name is nil.  When used without parameters, DIRECTORY displays 
the current directory pointer. 
Usage Note: 
The DIRECTORY and DIR commands may be used only as a direct GOOSE command. 
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
00004
00001
00003
Format: 
{DO|!} IBEX-command 
Parameters: 
IBEX-command    any legal IBEX command.  See the CP-6 Programmer Reference 
Manual (CE40). 
Description: 
The DO command allows the user to execute an IBEX command without exiting the 
current processor. 
Usage Notes: 
1.  The ! (exclamation point) may be used instead of the word DO.  It should 
    be noted however that if the ! is used in an XEQ file, it will terminate 
    the current processor session unless preceded by at least one blank, or by 
    a double ! (!!). 
2.  The DO command may be used only as a direct GOOSE command. 
Examples: 
:DO DI 
means display the current system status 
:!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00004
00001
00003
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
The END command (and its synonyms EXIT and QUIT) causes GOOSE to exit. 
Usage Note: 
The END, EXIT, and QUIT commands may be used only as a direct GOOSE command. 
00001
00002
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
ERASE deletes the accumulated outputs for logical devices. 
Usage Note: 
The ERASE command may be used only as a direct GOOSE command. 
Examples: 
:ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00004
00001
00003
Format: 
EV[ALUATE] {jjj/yyyy | mm/dd/yyyy}[{+|-}nnnn| 
    {jjj/yyyy|mm/dd/yyyy}[INT[ERVAL]=xx {MIN[UTES]|DAYS}]] 
Parameters: 
jjj/yyyy    is the Julian day and year. 
mm/dd/yyyy    is the specified month, day and year. 
nnnn    specifies the number of days to be added or subtracted. 
xx    specifies the interval at which the date range is to be evaluated. 
Description: 
The EVALUATE command is used as an aid in scheduling ghosts, keyins and 
messages.  This command allows the user to display the difference (in days) 
between two dates, add an arbitrary number (positive or negative) of days to 
any date and receive a breakdown of the resulting date, receive a breakdown on 
a specific date, and display the number of days or minute intervals between 
two dates. 
Usage Notes: 
1.  Only two digits are required for specifying the year, as the evaluator 
    defaults to the 20th century. 
2.  Week of month and week of year are determined by the number of Mondays in 
    the month and in the year.  Days preceding the first Monday in a year are 
    considered as week 0. 
3.  The EVALUATE command may be used only as a direct GOOSE command. 
Example: 
!GOOSE. 
Goose here 
:EV 8/30/84 
Thursday, August 30, 1984 
Julian day...............243 
Week of year.............35 
Week of month............4 
Leap year................Yes 
:EV 8/30/84 365/82 INT = 60 MIN 
Difference = 123 Days 
Intervals = 2952 
:END 
00002
00004
00001
00003
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
A 
  AUTO SCHEDULING Command - 
      HELP AUTO_SCHEDULING 
D 
  DATE Command - 
      HELP DATE 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DO Command - 
      HELP DO 
E 
  END Command - 
      HELP END 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
  EVALUATE Command - 
      HELP EVALUATE 
F 
  Files Created by GOOSE - 
      HELP RELATED_FILES 
G 
  GOOSE -   
    AUTO SCHEDULING Command - 
      HELP AUTO_SCHEDULING FORMAT: 
    END Command - 
      HELP END FORMAT: 
    ENTER Command - 
      HELP ENTER FORMAT: 
    ERASE Command - 
      HELP ERASE FORMAT: 
    EVALUATE Command - 
      HELP EVALUATE FORMAT: 
    KEYIN Command - 
      HELP KEYIN FORMAT: 
    LIST Command - 
      HELP LIST FORMAT: 
    MESSAGE Command - 
      HELP MESSAGE FORMAT: 
    START Command - 
      HELP START FORMAT: 
    UPDATE Command - 
      HELP UPDATE FORMAT: 
H 
  HELP Command - 
      HELP HELP 
K 
  KEYIN Command -   
    GOOSE - 
      HELP KEYIN FORMAT: 
  KEYIN Command - 
      HELP KEYIN 
L 
  LIST Command -   
    GOOSE - 
      HELP LIST FORMAT: 
  LIST Command - 
      HELP LIST 
M 
  MESSAGE Command - 
      HELP MESSAGE 
O 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PRINT Command - 
      HELP PRINT 
  Privileges for Use of GOOSE - 
      HELP PRIVILEGES 
S 
  START Command - 
      HELP START 
U 
  UPDATE Command - 
      HELP UPDATE 
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
HELP_INDEX
Format: 
KEYIN 
    {AT {hh:mm|S[TARTUP][+nn]}} 
    {EVERY x {H[OURS]|M[INUTES]}} 
    [FROM hh:mm] [UNTIL hh:mm] [ON day[,day]...           ] U[SING] keyin 
                               [ON DATE mm/dd/yy          ] 
                               [ON DATES mm/dd/yy-mm/dd/yy] 
Parameters: 
time and day or date specifications    are as described in START. 
nn    specifies a time offset (in minutes) from system startup. 
x    is an integer value (0-99999999). 
USING keyin    specifies the KEYIN to be performed.  The list below includes 
all valid keyins for GOOSE. 
@ TERMSEND                           ACCTLG 
AUTO SCHEDULE [UPDATE ] {ON|OFF}     LOCK DEVICE 
              [MESSAGE]              MSG 
BATCH {ON|OFF}                       MYREADACCT [RESET] 
BOOT FEP {FEPNAME|FEPNUM}            NETWORK ROUTE {FEPNAME|FEPNUM} 
BROADCAST                            NETWORK ROUTES 
CONSOLE STATUS                       NCTL 
DELE O                               NODE {FEPNAME|FEPNUM} 
DISABLE {FEPNAME|FEPNUM}             NODES 
DISCONNECT {FEPNAME|FEPNUM}          OCHIST 
DISMOUNT                             ON [BA|GH|TP|TS] 
DISPLAY [RUNNING]                    PRIO {INPUT|OUTPUT} 
        [DEFER  ]                    READ 
        [NORUN  ]                    READACCT [RESET] 
        [INPUT  ]                    READ$ {DEVICE|LOGON} 
        [OUTPUT ]                    RESTRICT DEVICE 
        [NSFORM ]                    ROUTE 
        [PRIO   ]                    SEND ALL 
        [ALL    ]                    SEND ALL FEP {FEPNAME|FEPNUM} 
ENABLE {FEPNAME|FEPNUM}              START {FEPNAME|FEPNUM} 
EXCLMOUNT                            START FEPS 
FEP {FEPNAME|FEPNUM}                 START TP/ 
FEPS                                 STOP {FEPNAME|FEPNUM} 
FLUSH                                STOP FEPS 
HEADER                               SWITCH OUTPUT 
HISTORY {ON|OFF}                     TELL 
HOSTS                                TP/ 
INFO                                 [DONT] TURN [ACCT|OCHIST|ALL] 
KILL {FEPNAME|FEPNUM}                UNRESERVE DEVICE 
LINK {FEPNAME|FEPNUM}                UNRESTRICT DEVICE 
LINKS                                UNROUTE 
Description: 
This command performs the specified KEYIN at the appropriate time. 
Usage Notes: 
1.  The KEYIN command may be used only in GOOSE_EGG.:SYS. 
2.  The maximum length of the USING phrase keyin string is 80 characters. 
Examples: 
KEYIN AT 23:00 USING !ACCTLG :ACCLG_900719_2300.:SYSTAC 
00002
00004
00001
00003
Format: 
L[IST] 
Description: 
This command displays the contents of the GOOSE_EGG file. 
Usage Note: 
The LIST command may be used only as a direct GOOSE command. 
00001
00002
Format: 
MESSAGE 
    {AT {hh:mm|S[TARTUP][+nn]}} 
    {EVERY x {H[OURS]|M[INUTES]}} 
    [FROM hh:mm] [UNTIL hh:mm] [ON day[,day]...           ] U[SING] message 
                               [ON DATE mm/dd/yy          ] 
                               [ON DATES mm/dd/yy-mm/dd/yy] 
Parameters: 
The time and day or date specifications are as described in START. 
nn    specifies a time offset (in minutes) from system startup. 
x    is an integer value (0-99999999). 
USING message    specifies the text of the message to be sent to consoles with 
the SYSTEM attribute. 
Description: 
This command sends the specified message text to consoles with the SYSTEM 
attribute. 
Usage Note: 
The MESSAGE command may be used only in GOOSE_EGG.:SYS. 
00002
00001
00003
Format: 
         [[OVER] LP[@location]] 
OUT[PUT] [[INTO] fid          ] [(option[,option]...[)]] 
         [[ON  ] ME           ] 
         [[TO  ]              ] 
Parameters: 
fid    any valid CP-6 file identifier. 
ON or TO    indicates to only honor the OUTPUT command if the file does not 
already exist. 
OVER    indicates to honor the OUTPUT command whether or not the file exists. 
INTO    indicates to merge the result of the OUTPUT command into the file if 
it exists, or to create a new one if it does not. 
LP    directs output to the default line printer; @location specifies a line 
printer at a workstation. 
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
The OUTPUT command is used to direct all processor output to a destination. 
OUTPUT with no options redirects output to the original output destination. 
Output can be directed to any valid file name (fid).  If none of ON, TO, OVER, 
or INTO is specified, ON will be assumed. 
00002
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
The privileges required to use the various GOOSE commands are listed under 
HELP (GOOSE) COMMANDS. 
END
The control file GOOSE_EGG may be created by use of the EDIT processor. 
However, if this file is not present in :SYS when the system comes around, it 
will be created by GOOSE.  The GOOSE processor recreates the GOOSE_EGG file 
when updates are successfully parsed (see UPDATE command). 
Format: 
Form 1 (Direct): 
STAR[T] [account, uname, password] [U[SING] command] 
Form 2 (For GOOSE_EGG.:SYS): 
STAR[T] account, uname, password 
    {AT {hh:mm|S[TARTUP][+nn]}} 
    {EVERY x {H[OURS]|M[INUTES]}} 
    [FROM hh:mm] [UNTIL hh:mm] [ON day[,day]...           ] [U[SING] command] 
                               [ON DATE mm/dd/yy          ] 
                               [ON DATES mm/dd/yy-mm/dd/yy] 
Parameters: 
account,uname,password    identify the logon account in which the ghost is to 
run.  In Form 1 if these parameters are omitted, the ghost is started in the 
account from which the command was issued. 
command    is an IBEX command to invoke the ghost job, typically XEQ 
ghost_jobname.  The default command is taken from the SETUP option for the 
logon record for the account in which the ghost is to run. 
AT hh:mm    specifies the hours and minutes when the ghost job will be 
started.  These can be wildcarded so that a time of '?:30' means the command 
is to be done at 00:30, 01:30, 02:30,...,23:30 and a time of '?:?5' will be 
done at 00:05, 00:15, 00:25..., 01:05, 01:15,..., 23:55.  The FROM time and 
UNTIL time give the range in which this command should be executed. 
AT STARTUP    specifies that the ghost job will be started at every system 
initialization (recovery, boot, etc.). 
nn    specifies a time offset (in minutes) from system startup. 
EVERY number    specifies the number of minutes or hours between doing the 
command.  If FROM and UNTIL are specified, the command will be executed within 
that range.  If FROM and UNTIL are not specified, the interval will begin at 
startup. 
ON day    specifies the day(s) of the week when the command will be executed 
(MON, TUE, WED, THU, FRI, SAT, SUN). 
ON DATE    specifies the month, day, and year when the command will be 
executed.  Any of them may be wildcarded so that the date ??/01/?? would 
indicate, for example, execution on the first of every month.  Note that 
unlike the hh:mm field, both the tens and ones columns are wildcarded. 
ON DATES    specifies a range of dates over which this command is to execute. 
Wildcarding is not permitted in either date value. 
USING command    specifies the command executed when the ghost job starts.  If 
no command is given, the default is the current command in the SUPER record 
for the specified logon. 
Description: 
This command starts a particular ghost job immediately if Form 1 is used, or 
at the specified time if Form 2 is used.  The ghost job will have: 
            Direct START                   START in GOOSE_EGG.:SYS 
Account:    current account or the         account specified by START 
            account specified by START 
User name:  current uname or the uname     uname specified by START 
            specified by START 
WSN:        current WSN                    LOCAL 
Privileges: none                           none 
Usage Notes: 
1.  Form 1 of the START command must be entered as a direct command to GOOSE; 
    Form 2 of the START command is permitted only in GOOSE_EGG.:SYS. 
2.  Ghost jobs are started without any privileges.  They can, however, be 
    given any privileges that SUPER has authorized for them once they have 
    been started. 
3.  The account in which a ghost runs is authorized via SUPER with ACCESS 
    G=YES, O=YES... , and optionally with SETUP G=command...  (which defines 
    the default first command). 
4.  Multiple ghosts may run in a single account with one exception.  Only one 
    TP ghost (instance) is permitted to run in an account at a given time. 
    Several non-TP ghosts, however, may run simultaneously in an account with 
    a TP ghost. 
5.  Maximum length of the USING phrase command string is 256 characters. 
Examples: 
START :FED,CSO,PASSWORD AT 08:00 ON MON USING !XEQ $XELAN_REPORT.:FED 
00002
00004
00001
00003
DATE
Format: 
UPDATE 
Description: 
This command allows the user to update the GOOSE_EGG file.  The UPDATE is 
accomplished by the following sequence: 
1.  GOOSE copies the GOOSE_EGG file to a temporary file (only one user at a 
    time). 
2.  GOOSE invokes EDIT. 
3.  The user makes the desired changes. 
4.  The user exits EDIT by typing an END command. 
5.  GOOSE reads and checks the syntax of the temporary file. 
6.  If no errors are found, GOOSE copies the temporary file over the GOOSE_EGG 
    file as a consecutive file. 
7.  GOOSE uses PCL to copy the GOOSE_EGG file over itself (to key it). 
Usage Notes: 
1.  The UPDATE command may be used only as a direct GOOSE command. 
2.  GOOSE is automatically informed of any GOOSE_EGG file changes after the 
    UPDATE command is finished. 
00001
00002
