After start-up, the TP administrator can monitor and direct activity of the 
instance of TP via TP commands entered on a Master Control Terminal, a 
privileged TP station, or a TP operator console.  For further HELP messages 
enter: 
HELP (TPA) TOPICS        For list of HELP topics 
HELP (TPA) COMMANDS      For summary of TP command types 
HELP (TPA) COMMAND_SUM   For summary of TP commands 
HELP (TPA) COMMAND_USAGE For summary of command usage restrictions 
HELP (TPA) NOTATION      For notation used to depict command formats 
For example, for HELP on the CHECK command, enter 
HELP (TPA) CHECK 
To obtain successive layers of information about the command, enter ? or ?? 
for all successive layers.  The layers of information are also accessible by 
specifying an additional subtopic such as PARAM in: 
HELP (TPA) CHECK PARAM 
to obtain the information on parameters.  Subtopics for commands include PARAM 
for Parameters, DESC for Description, NOTES for Usage Notes. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
Format: 
BEGIN [type[.password] [[BY] DEF[AULT]]] 
Parameters: 
type    specifies a Forms Program type (as defined in the TRADER CREATE FORM 
command). 
password    specifies the password associated with the Forms Program. 
Description: 
This command provides several options for invoking Forms Programs: 
o   With the type and optional password, it invokes the specified Forms 
    Program. 
o   With the type, optional password, and BY DEFAULT options, BEGIN invokes 
    the specified Forms Program and makes that program the default Forms 
    Program.  A user-supplied default Forms Program customizes the interface 
    between the end-user and the TP system by providing a choice of options 
    (i.e., a menu) and loading the appropriate user Forms Program based on the 
    end-user's option selection.  Once established as the default Forms 
    Program for a TP station, that program receives control whenever OTHER 
    user Forms Programs exit or abort.  When the default Forms Program exits 
    or if it should abort, the TP station is logged off the system. 
    NOTE:  The assignment of a default remains in effect until TP station 
    logoff or until entry of another BEGIN, rununit_command, or START command 
    specifying BY DEFAULT. 
o   Without options, BEGIN invokes the default Forms Program. 
If the end-user is not authorized to access the program requested or if the 
program is disabled, a message is returned to the TP station.  If the default 
Forms Program cannot be loaded for any reason, the TP station is logged off 
the system. 
Usage Notes: 
This command may be entered from a TP station after TP initialization. 
If no default Forms Program is specified, the Command Forms Program serves as 
the default Forms Program. 
Like other TP commands, BEGIN can be specified at station authorization via 
SUPER (i.e., the CMD option defining a first command to be executed on a 
behalf of a TP station at logon).  Specifying a default Forms Program in a 
station authorization is suitable for a stand-alone station or other TP 
station. 
A user-supplied default Forms Program may need to make provision for end-users 
to enter TP commands and to receive any messages sent to a TP station.  This 
can be accomplished in the default Forms Program by use of the FPL LOAD 
statement: 
    LOAD "COMMAND_FP.:SYS" BY NAME 
To return from Command state to the user-supplied default Forms Program, the 
end-user simply enters the BEGIN command without options. 
A BEGIN command must not appear in a file that is the subject of a BEGIN 
command. 
00002
00003
00001
00003
Format: 
{BYE|OFF} 
Description: 
This command logs the end-user off the CP-6 system.  Any data entry 
transactions submitted by this station and received by the host will be 
processed.  Any report transactions destined for this station by explicit 
identification of the terminal station name will be retained at the host until 
the station logs on later and invokes a Forms Program to receive them. 
Usage Notes: 
This command may be entered after TP initialization only. 
00001
00002
00002
Format: 
Form 1: 
                                   {type[.station]} 
         {R[EPORTS]              } {  id[.station]} 
CAN[CEL] {T[RANSACTIONS]         } {     .station]} 
Form 2: 
                                [type] 
CAN[CEL] H[ELD] [TRANSACTIONS]] [id  ] 
Parameters: 
R[EPORTS] 
T[RANSACTIONS] 
H[ELD] [T[RANSACTIONS]    specifies a class of transactions:  report, data 
entry and spawned, or data entry and spawned in "hold" status. 
type    specifies a transaction type.  type may include the wildcard (?) 
character.  If type is omitted when HELD is specified, the default is all 
transactions in "hold" status. 
station    if specified without type or id, .station identifies all data entry 
or spawned transactions associated with the named station.  If used together 
with type or id, .station specifies only the transactions of the type or id 
for the named station.  station may include the wildcard (?) character.  The 
default is the current station. 
id    specifies a transaction ID of a data entry or spawned transaction.  The 
form of id is n for a data entry transaction.  The form of id is n-m for a 
spawned transaction, where n identifies the data entry transaction which 
resulted in creation of spawned transaction m.  If id is omitted when HELD is 
specified, the default is all transactions in "hold" status. 
Description: 
This command eliminates from the comgroup the transaction(s) meeting the 
specified criteria provided that they are not already being processed by 
TPAPs. 
Usage Notes: 
Privilege is required to cancel another station's transactions. 
Entering CANCEL ?.? deletes all report transactions. 
00002
00003
00001
00003
Format: 
Form 1: 
                               {type[.station]} 
      [R[EPORTS]             ] {  id[.station]} 
CHECK [T[RANSACTIONS]        ] {     .station}} [SUM[MARY]] 
Form 2: 
                               [type] 
CHECK [H[ELD] [T[RANSACTIONS]] [id  ] [SUMMARY] 
Parameters: 
R[EPORTS] 
T[RANSACTIONS] 
H[ELD] [T[RANSACTIONS]    specifies a class of transactions:  report, data 
entry and spawned, or data entry and spawned transactions in "hold" status. 
The default is all three classes. 
type    specifies a transaction type.  Type may include the wildcard (?) 
character.  When HELD is specified and type is omitted, the default is all 
transactions in "hold" status. 
station    specifies an authorized TP station.  If specified without type or 
id, .station identifies all transactions associated with the named station. 
If used together with type or id, .station specifies only transactions of the 
type or id for the named station.  .station may include the wildcard (?) 
character.  The default is the current station. 
id    specifies a transaction ID of the form n[-m] where n specifies an 
integer assigned to a data entry transaction; -m is the additional integer 
that identifies transactions generated as a result of processing the data 
entry entry transaction.  If id is omitted when HELD is specified, the default 
is all transactions in "hold" status.  (n is available to the Forms Program as 
the ID variable defined in the Environment Division, File Control paragraph.) 
For example, if data entry transaction 5 is received and results in creation 
of a spawned transaction, the spawned transaction is assigned ID 5-1; if 
processing of the spawned transaction generates two report transactions, the 
first report transaction written to the comgroup is assigned ID 5-2; the 
second is assigned ID 5-3. 
Description: 
The CHECK command displays information about the specified transaction(s).  If 
SUMMARY is specified, a summary of all transactions meeting the specified 
criteria is displayed.  The summary is broken down and displayed by type for 
transactions, reports, and held transactions. 
Usage Notes: 
Privilege is required to check another station's transaction(s) or to use a 
wildcarded station name. 
00002
00003
00001
00003
The TP commands may be categorized as follows: 
Station Control Commands:  BEGIN, BYE|OFF, DATE, DEBUG, MESSAGE, PASSWORD, 
PRIORITY, PROFILE, Rununit Type, SPY, START, TIME, UNDER. 
Access Control Commands:  DISABLE, ENABLE, KILL. 
Scheduling and Administrative Control Commands:  CANCEL, CHECK, DISPLAY, 
ERSEND, HOLD, LET, READ, RELEASE, STATS, STOPTP!, SWITCH, TRANSACTION. 
For more information, type: 
HELP (TPA) COMMAND_S command   For a summary of a specific command 
HELP (TPA) COMMAND_S           For a summary of all commands 
To display a brief description of all commands, type ??.  To display a brief 
description of a specific command, type: 
HELP (TPA) COMMAND_S command 
Valid commands are BEGIN, BYE, CANCEL, CHECK, DATE, DEBUG, DISABLE, DISPLAY, 
ENABLE, ERSEND, HELP, HOLD, KILL, LET, MESSAGE, OFF, PASSWORD, PRIORITY, 
PROFILE, READ, RELEASE, SPY, START, STATS, STOPTP!, SWITCH, TIME, TRANSACTION. 
  Command        Description 
  BEGIN 
                 Invoke a specific Forms Program. 
  BYE|OFF 
                 Log this station off the TP system. 
  CANCEL 
                 Delete specified transaction(s) from the comgroup. 
  CHECK 
                 Check status of transactions. 
  DATE 
                 Requests a display of the current time and date. 
  DEBUG 
                 Invoke a specified Forms Program for debugging. 
  DISABLE 
                 Deny access to the TP system for specified station(s), or 
                 prevent invocation of specified Forms Program(s). 
  DISPLAY 
                 Display status of Forms Programs or stations, or LET options, 
                 or number of transactions of a given type waiting to be 
                 processed and in process by a TPAP, plus certain TRADER file 
                 information. 
  ENABLE 
                 Reverse the effect of DISABLE command for station(s) or Forms 
                 Program(s). 
  ERSEND 
                 Insert text into the TPA log. 
  HELP 
                 Obtain HELP messages on the specified processor. 
  HOLD 
                 Delay processing of specified transaction(s). 
  KILL 
                 Log off the specified station(s) or eliminate specified TP 
                 User(s). 
  LET 
                 Set any of a number of operating parameters for the instance 
                 of TP. 
  MESSAGE 
                 Send a text message to specified station(s) or operator 
                 console(s). 
  PASSWORD 
                 Change this station's logon password. 
  PRIORITY 
                 Change a station's priority. 
  PROFILE 
                 Select terminal profile. 
  READ 
                 Read and perform TP commands stored in a file. 
  RELEASE 
                 Remove specified transaction(s) from "hold" status. 
  Rununit Type 
                 Invoke a specific Forms Program. 
  SPY 
                 Display information pertaining to TP stations currently 
                 logged on to the instance of TP, or information pertaining to 
                 TPAPs. 
  START 
                 Invoke and/or debug a specified Forms Program. 
  STATS 
                 Display statistics on operation of the instance of TP. 
  STOPTP! 
                 Shut down the instance of TP. 
  SWITCH 
                 Change the destination of specified report transaction(s) to 
                 a specified station. 
  TIME 
                 Requests a display of the current time and date. 
  TRANSACTION 
                 Specify information on TPAP invocation for a transaction 
                 type.  Certain of the operating parameters override 
                 parameters supplied in the TRADER file or the start-up file. 
  UNDER 
                 Used in conjunction with the Rununit Type command, invokes a 
                 Forms Program under the control of DELTA, the debugger. 
For details on a specific command, enter: 
HELP (TPA) command_name        For command format.  Enter ? or ?? 
                               for more information. 
HELP (TPA) command_name PARAM  For a discussion of parameters 
HELP (TPA) command_name DESC   For the description of the command 
HELP (TPA) command_name NOTES  For usage notes on the command 
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
00002
00016
00017
00018
00019
00020
00021
00022
00023
00024
00025
00026
00027
00028
00029
------------------------------------------------------------------- 
|Command*      |User|MCT|Init|OC||Command*       |User|MCT|Init|OC| 
|-----------------------------------------------------------------| 
|BEGIN         |  x | x |    |  ||LET MEMWARN    |    |   |  x |  | 
|-----------------------------------------------------------------| 
|BYE           |  x | x |    |  ||LET NEWCG      |    |   |  x |  | 
|-----------------------------------------------------------------| 
|CANCEL        |  x | x |  x | x||LET POOLSIZE   |    |   |  x |  | 
|-----------------------------------------------------------------| 
|CHECK         |  x | x |  x | x||LET STATIONMAX |    | x |  x | x| 
|-----------------------------------------------------------------| 
|DATE          |  x | x |  x | x||LET TPUINITIAL |    |   |  x |  | 
|-----------------------------------------------------------------| 
|DEBUG         |  x | x |    |  ||LET XTNSIZE    |    | x |  x | x| 
|-----------------------------------------------------------------| 
|DISABLE       |    | x |  x | x||MESSAGE        | x  | x |  x | x| 
|-----------------------------------------------------------------| 
|DISPLAY       |    | x |  x | x||OFF            | x  | x |    | x| 
|-----------------------------------------------------------------| 
|ENABLE        |    | x |  x | x||PASSWORD       | x  | x |    |  | 
|-----------------------------------------------------------------| 
|ERSEND        |    | x |    | x||PRIORITY       | x  | x |  x | x| 
|-----------------------------------------------------------------| 
|HOLD          |  x | x |  x | x||PROFILE        | x  | x |    |  | 
|-----------------------------------------------------------------| 
|KILL          |    | x |    | x||READ           |    | x |  x | x| 
|-----------------------------------------------------------------| 
|LET ACCOUNTING|    | x |  x | x||RELEASE        | x  | x |  x | x| 
|-----------------------------------------------------------------| 
|LET CFPRU     |    |   |  x |  ||Rununit Type   | x  | x |    |  | 
|-----------------------------------------------------------------| 
|LET CGPAGEMAX |    |   |  x |  ||SPY            | x  | x |    | x| 
|-----------------------------------------------------------------| 
|LET CGPAGEMIN |    |   |  x |  ||START          | x  | x |    |  | 
|-----------------------------------------------------------------| 
|LET DCBCON    |    | x |  x | x||STATS          |    | x |    | x| 
|-----------------------------------------------------------------| 
|LET DISKWARN  |    |   |  x |  ||STOPTP!        |    | x |    | x| 
|-----------------------------------------------------------------| 
|LET IXTNSIZE  |    |   |  x |  ||SWITCH         | x  | x |  x | x| 
|-----------------------------------------------------------------| 
|LET JOURNAL   |    |   |  x |  ||TIME           | x  | x |  x | x| 
|-----------------------------------------------------------------| 
|LET LOG       |    |   |    | x||TRANSACTION    |    | x |  x | x| 
|-----------------------------------------------------------------| 
|LET MCTID     |    | x |  x | x||UNDER          | x  | x |    |  | 
------------------------------------------------------------------- 
  *User = a non-privileged station. 
   MCT = a Master Control Terminal (a station defined with SUPER's 
         option MCT=YES) or a station defined with SUPER's option 
         MCT=COMMANDS. 
   Init= TP start-up file used at TP initialization. 
         NOTE:  The LET commands may be used only once in the 
                start-up file. 
   OC = TP operator console or SYSTEM operator console. 
For details on a specific command, enter: 
HELP (TPA) command_name        For command format.  Enter ? or ?? 
                               for more information. 
HELP (TPA) command_name PARAM  For a discussion of parameters 
HELP (TPA) command_name DESC   For the description of the command 
HELP (TPA) command_name NOTES  For usage notes on the command 
Rununit
Format: 
DATE 
Description: 
Requests a display of the current time and date. 
00001
Format: 
DEBUG type[.password] 
Parameters: 
type    specifies a Forms Program type (as defined in the TRADER CREATE FORM 
command). 
password    specifies the password associated with the Forms Program. 
Description: 
This command invokes the Forms Program specified in the TRADER file and 
identified by type.  Instead of beginning execution immediately, the Forms 
Program is under control of DELTA, the debugger; a user at a time-sharing 
terminal communicates with DELTA to direct debugging activities.  If the 
end-user entering the DEBUG command is not authorized to access the program, 
if the program is disabled, or if debugging is prevented for the program, a 
message is returned and the station remains in Command state. 
Usage Notes: 
This command may be entered after TP initialization only. 
00002
00003
00001
00003
DISPLAY
Format: 
DISAB[LE] {FP type          } 
          {STAT[ION] station} 
Parameters: 
type    specifies the Forms Program to be disabled.  Type is the 1 to 8 
character name that an end-user enters in the BEGIN command, for example.  The 
type may include the wildcard (?) character. 
station    specifies a station name.  The station name may include the 
wildcard (?) character. 
Description: 
This command serves two purposes.  If STATION is specified, the named 
station(s) are denied access to the instance of TP.  Stations already logged 
on are not logged off by this command; a Master Control Terminal is not 
affected by this command and may subsequently log on even if its station name 
matches the station(s) that are disabled. 
If FP is specified, the named Forms Program cannot be invoked.  This command 
has no effect on Forms Programs already in use by stations.  The command 
prevents invocation of the named program in response to the BEGIN and DEBUG 
commands. 
The effect of the DISABLE command continues until an ENABLE command is entered 
to reverse it or until the instance of TP is shut down. 
Usage Notes: 
Privilege is required to use this command. 
00002
00003
00001
00003
Format: 
Form 1: 
DI[SPLAY] DISAB[LED] {FP     } 
                     {STATION} 
Form 2: 
DI[SPLAY] TYPE type 
Form 3: 
DI[SPLAY] PARAM[ETER] {option1[,option2]...} 
                      {ALL                 } 
Parameters: 
type    specifies a Forms Program type or a transaction type.  The type may 
include a trailing wildcard (?) character. 
option1,option2    specifies a LET option name for which the corresponding 
parameter is to be displayed. 
Description: 
Form 1 displays the Forms Programs that are currently disabled or TP stations 
that are currently disabled. 
Form 2 displays non-default options from the TRADER file for the transaction 
type specified.  In addition, it displays the following items: 
    Count      Number of transactions of this type waiting to be read by a 
               TPAP. 
    CurActive  Number of TPUs running on behalf of this transaction type. 
Form 3 displays the specified LET options or all LET options if the keyword 
ALL is specified. 
Usage Notes: 
Privilege is required to use this command. 
00002
00003
00001
00003
Format: 
ENAB[LE] {FP type          } 
         {STAT[ION] station} 
Parameters: 
type    specifies a disabled Forms Program.  The type may include the wildcard 
(?) character. 
station    specifies a disabled station.  The station name may include the 
wildcard (?) character. 
Description: 
This command reverses the effect of the DISABLE command.  If FP is specified, 
the named Forms Program(s) can be invoked.  If STATION is specified, the named 
station(s) can log on to the instance of TP. 
Usage Notes: 
Privilege is required to use this command. 
00002
00003
00001
00003
Format: 
ERSE[ND] message 
Parameters: 
message    is the text to be entered into the TPA log. 
Description: 
This command allows a TP administrator to insert text into the TPA log.  The 
message following the word 'ERSEND' will be written to the TPA log through 
M$DO. 
Usage Notes: 
Privilege is required to use this command. 
Example: 
ERSE Add this information to the TPA log. 
00002
00004
00001
00003
Format: 
HELP [(fid)] [TOPICS] [keyword1] [-] [keyword2] 
NOTE:  The following elements can be specified in any order: 
         (fid) 
         TOPICS 
         [keyword1] [-] [keyword2] 
For example, HELP (fid) keyword1 - keyword2 TOPICS is acceptable. 
Parameters: 
(fid)    specifies the processor name.  If (fid) is omitted, the current 
processor is assumed.  To obtain HELP for TP commands, enter TPA as the fid. 
TOPICS    requests a list of topic or subtopic names, rather than an 
information message. 
Form                                       Result 
----                                       ------ 
HELP (fid) TOPICS                          Lists all topics. 
HELP (fid) TOPICS keyword1 - keyword2      Lists all topics in the range 
                                           specified by keyword1 - keyword 2. 
HELP (fid) TOPICS keyword1?                Lists all topics beginning with 
                                           the prefix specified by keyword1. 
HELP (fid) TOPICS keyword1                 Lists all subtopics for the 
                                           topic specified by keyword1. 
keyword1 [- [keyword2]]    specifies a topic, a range of topics, or a topic 
and subtopic to identify what HELP information is requested. 
Form                                       Result 
----                                       ------ 
HELP (fid) keyword1                        Displays the first level 
                                           information message for 
                                           the topic keyword1. 
HELP (fid) keyword1 keyword2               Displays the information 
                                           message for keyword1, but 
                                           only the level identified 
                                           by the subtopic keyword2. 
HELP (fid) TOPICS keyword1 [-] [keyword2]  Lists topic or subtopic 
                                           names.  See TOPICS parameter. 
keyword1 may include the wildcard (?) character as the rightmost character, if 
TOPICS is specified. 
Description: 
HELP displays information. 
HELP messages have levels.  Once the initial level has been displayed, 
entering a question mark displays the next level, usually containing greater 
detail.  Entering two question marks displays all the remaining levels. 
Any processor with a standard HELP file can be read from IBEX, but is 
available only to users with sufficient privilege to use the processor itself. 
The HELP command can be used either within the processor or in IBEX. 
The HELP can be issued at the double-bang (!!) without losing the suspended 
activity.  Thus, one may exit a processor (such as EDIT) with a <CNTL-Y>, 
query for HELP information, and then issue GO to return to EDIT. 
Examples: 
HELP (TPA) HOLD 
means display the format of the HOLD command and prompt for the next entry. 
HELP (TPA) LET PARAM 
means display the discussion of parameters for the LET command, including a 
list of the attribute options. 
HELP (TPA) LET CGPAGEMAX 
means display only the discussion of the CGPAGEMAX attribute of the LET 
command. 
00002
00003
00001
B 
  BEGIN Command - 
      HELP BEGIN 
  BYE or OFF Command - 
      HELP BYE 
C 
  CANCEL Command - 
      HELP CANCEL 
  CHECK Command - 
      HELP CHECK 
D 
  DATE Command - 
      HELP DATE 
  DEBUG Command - 
      HELP DEBUG 
  DISABLE Command - 
      HELP DISABLE 
  DISPLAY Command - 
      HELP DISPLAY 
E 
  ENABLE Command - 
      HELP ENABLE 
  ERSEND Command - 
      HELP ERSEND 
H 
  HELP Command - 
      HELP HELP 
  HOLD Command - 
      HELP HOLD 
  hold status - 
      HELP CANCEL PARAMETERS: 
      HELP CHECK PARAMETERS: 
      HELP HOLD DESCRIPTION: 
I 
  Instance of TP Operation - 
      HELP INSTANCE_OF_TP_OPERATION 
J 
  JOURNAL - 
      HELP LET JOURNAL_ 
K 
  KILL Command - 
      HELP KILL 
L 
  LET Command - 
      HELP LET 
M 
  MESSAGE Command - 
      HELP MESSAGE 
N 
  NO DATA - 
      HELP RELEASE FORMAT: 
O 
  OFF - 
      HELP MESSAGE FORMAT: 
  Ordering - 
      HELP ORDERING_HOW_TO 
P 
  PASSWORD Command - 
      HELP PASSWORD 
  PRIORITY Command - 
      HELP PRIORITY 
  PROFILE Command - 
      HELP PROFILE 
  Publishing - 
      HELP PUBLISHING 
R 
  READ Command - 
      HELP READ 
  RELEASE Command - 
      HELP RELEASE 
  Rununit Type Command - 
      HELP Rununit 
S 
  SPY Command - 
      HELP SPY 
  START Command - 
      HELP START 
  Station priority - 
      HELP PRIORITY DESCRIPTION: 
  statistics - 
      HELP STATS DESCRIPTION: 
  STATS Command - 
      HELP STATS 
  STOPTP! Command - 
      HELP STOPTP 
  SWITCH Command - 
      HELP SWITCH 
T 
  TIME Command - 
      HELP TIME 
  TP Command - 
      HELP COMMANDS 
  TP Command Usage - 
      HELP COMMAND_USAGE 
  TP User - 
      HELP KILL DESCRIPTION: 
  TRANSACTION Command - 
      HELP TRANSACTION 
  transaction ID - 
      HELP HOLD FORMAT: 
  transaction type - 
      HELP TRANSACTION PARAMETERS: 
U 
  UNDER Command - 
      HELP UNDER 
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
     {type[.station]} 
HOLD {id[.station]  } 
     {.station      } 
Parameters: 
type    specifies a data entry or spawned transaction type.  type may include 
the wildcard (?) character. 
station    if specified without type or id, .station identifies all data entry 
or spawned transactions associated with the named station.  If used together 
with type or id, .station specifies only the transactions of the type or id 
for the named station.  station may include the wildcard (?) character.  The 
default is the current station. 
id    specifies a transaction ID of a data entry or spawned transaction.  The 
form of id is n for a data entry transaction.  The form of id is n-m for a 
spawned transaction, where n identifies the data entry transaction which 
resulted in creation of spawned transaction m. 
Description: 
This command delays processing for transactions currently in the comgroup that 
meet the specified criteria.  Those transactions are placed in "hold" status, 
i.e., in a part of the comgroup where they cannot be read by any TPAP. 
(Information on transactions in the "hold" status can be displayed via CHECK 
REPORTS specifying .HOLDSTA.)  The HOLD command affects only transactions 
currently in the comgroup, not transactions entering the comgroup after the 
command is executed. 
NOTE:  HOLD must be avoided for data entry transactions from a Forms Program 
that expects a response transaction and performs the FPL READ statement 
omitting the NO DATA phrase.  In that case, HOLD causes the Forms Program to 
wait indefinitely and prevents further use of the TP station (unless the TP 
station is powered off and logged on again). 
Usage Notes: 
Privilege is required to place another station's transaction(s) in "hold" 
status. 
00002
00003
00001
00003

Format: 
KILL {STAT[ION] station} 
     {DCB sysid [NOW!] } 
Parameters: 
station    is the same as for DISABLE.  The station name may include the 
wildcard (?) character. 
sysid    specifies the system ID (15-n) for the TP User that is to be 
eliminated.  The sysid for a TP User can be displayed via the SPY TPU command. 
Description: 
This command controls access to the comgroup, either by stations (via the 
STATION option) or by TP Users (via the DCB option). 
If STATION is specified, the named station(s) are immediately logged off the 
CP-6 system.  Any Forms Programs running on behalf of the stations are 
aborted.  Any TPAP processing a transaction on behalf of any station that is 
killed completes its processing; however, response transactions generated by 
that processing are discarded. 
If DCB is specified, the TP User named via its system ID is eliminated.  The 
NOW! option specifies that the TP User is to be eliminated immediately.  If 
NOW! is specified and a TPAP is operating as the TP User, the TPAP is aborted 
and the TP user is eliminated.  (If a Forms Program is waiting to satisfy a 
READ for a transaction that the TPAP creates, that Forms Program receives an 
I-O error status.)  If NOW! is omitted and a TPAP is operating in the TP User, 
the TPAP continues and transactions it creates can be delivered.  In this 
case, when the TPAP performs the next read of the comgroup, "end-of-file" 
status is returned and the TPAP should exit; when the TPAP does exit, the TP 
User is eliminated. 
Usage Notes: 
Privilege is required to use this command; it may be entered after TP 
initialization only. 
00002
00003
00001
00003
Format: 
LET option 
Parameters: 
option    specifies a LET option.  To obtain HELP messages for the LET 
options, enter HELP (TPA) LET option_name.  For example, 
HELP (TPA) LET CGPAGEMAX. 
Valid option are: 
ACC[OUNTING] [=] {ON|OFF}, CFP[RU] [=] fid CGPAGEMAX [=] n, CGPAGEMIN [=] n, 
DCBCON [=] {ON|OFF}, DISK[WARN] [=] n, IXTN[SIZE] [=] n, 
JOUR[NAL] [=] {ON|OFF}, LOG [=] {ON|OFF}, MCTID [=] station, MEM[WARN] [=] n, 
NEWCG [=] {YES|NO}, POOL[SIZE] [=] n, STATIONMAX [=] n, TPU[INITIAL] [=] n. 
XTN[SIZE] [=] n. 
Descriptions are in tabular form with two columns, as follows: 
  Options     Description 
  ACC[OUNTING] [=] {ON|OFF} 
              Specifies how accounting is to be performed for TPUs. 
              Regardless of how this option is specified, an accounting record 
              is always written to the accounting log when a TP user is 
              eliminated; it reflects the resources used by the TPU for the 
              duration of its existence.  If ON is specified, a Step 
              accounting record is also written to the system accounting log 
              whenever a TPAP exits.  Step accounting provides a finer record 
              of the resources used in processing different transaction types. 
              The default is ACCOUNTING=OFF, i.e., only TPU accounting is 
              performed. 
              Permitted at or after TP initialization. 
  CFP[RU] [=] fid 
              Specifies the Command Forms Program to be used for the purpose 
              of communicating to and from TPA where fid = 
              filename.account.password.  TPA will reject 
              DP#xxxxxx/filename.account.password.  The default fid is 
              COMMAND_FP.:SYS. 
              A sample Command Forms Program (written in PL-6 for non-hardcopy 
              devices only) is available in the .:XSI account for your use. 
              There is also a macro file, Q_MACRO_C.:LIBRARY from which to 
              obtain the structures needed to communicate with TPA.  For sites 
              wishing to split their screens between timesharing and TP, the 
              program, COMMANDFP2_SI61 is available in the .:XSI account. 
              Permitted at TP initialization only. 
  CGPAGEMAX [=] n 
              Specifies the maximum number (4-1000) of memory pages to use for 
              the comgroup.  (The CGPAGEMAX value must be no greater than the 
              CGMEM allocation specified via PIG.)  The default is 30. 
              Permitted at TP initialization only. 
  CGPAGEMIN [=] n 
              Specifies the minimum number (4-1000) of memory pages to use for 
              this comgroup.  (The CGPAGEMIN value must be no greater than the 
              CGMEM allocation specified via PIG.)  The default is 10. 
              Permitted at TP initialization only. 
  DCBCON [=] {ON|OFF} 
              Specifies if ON that DCBs can be connected to the comgroup for 
              TPAPs being debugged in non-TP mode.  The default is DCBCON=OFF. 
              Permitted at or after TP initialization. 
  DISK[WARN] [=] n 
              Sets the comgroup "free disk space" warning level in granules 
              (0-1000).  If the comgroup "free disk space" falls below this 
              level, a warning message is sent to the Master Control Terminal. 
              The default is 25 granules. 
              Permitted at TP initialization only. 
  IXTN[SIZE] [=] n 
              Specifies the initial extent size of the comgroup in granules. 
              This value (in the range 100 to 9999) is the initial number of 
              granules to allocate on disk for the comgroup.  The default 
              IXTNSIZE is suitable for the typical system to ensure that TPA 
              does not have to make frequent extensions to the comgroup on 
              disk.  Extending the comgroup disk granules can be more costly 
              than making a large initial allocation.  However, for a trivial 
              instance of TP in which applications do very little and the I/O 
              volume has no peaks, the IXTNSIZE may be reduced as appropriate. 
              The default is 400. 
              Permitted at TP initialization only. 
  JOUR[NAL] [=] {ON|OFF} 
              Specifies, if ON, that the journal specified via a SET command 
              in the start-up file is to be opened.  The default, JOURNAL=OFF, 
              means that the journal is not to be opened. 
              Permitted at TP initialization only. 
  LOG [=] {ON|OFF} 
              Specifies, if ON, that all status messages for the instance of 
              TP are to be sent to the operator console(s) with the TP 
              attribute in addition to sending them to Master Control 
              Terminal(s).  The LET LOG command is restricted to use only at 
              TP or system operator consoles.  The LET LOG command may be 
              issued via the KEYIN command: 
              KEYIN AT time USING TP/instance LET LOG=ON 
              This allows TP activity to appear in :OCHIST.  The default is 
              LOG=OFF. 
              Permitted after TP initialization only. 
  MCTID [=] station 
              Specifies that status messages for the instance of TP are to be 
              saved, if the station specified is not logged on, and those 
              messages are to be delivered to the station after it logs on to 
              the instance of TP.  The default is blanks, which means that a 
              Master Control Terminal only receives status messages occurring 
              while that MCT is logged on to the instance of TP. 
              Permitted at or after TP initialization. 
  MEM[WARN] [=] n 
              Sets the comgroup "free memory space" warning level in pages 
              (0-1000).  If the comgroup "free memory space" falls below this 
              level, a warning message is sent to the Master Control Terminal. 
              The default is 5 pages. 
              Permitted at TP initialization only. 
  NEWCG [=] {ON|OFF} 
              Specifies, if ON, that the comgroup queues are to be cleared 
              when the instance of TP is started.  The default is NEWCG=OFF. 
              Permitted at TP initialization only. 
  POOL[SIZE] [=] n 
              Specifies the size of the internal pool of TPA memory.  This 
              parameter need not be specified unless an error message is 
              displayed by TPA requesting a change.  The POOLSIZE value must 
              be in the range 2048 to 9999 words.  The default is 2048 words. 
              Permitted at TP initialization only.  See also LET_COMMAND 
              USAGE_NOTES 
  STATIONMAX [=] n 
              Specifies the maximum number of stations that can be logged on 
              to the instance of TP simultaneously.  If STATIONMAX is reached, 
              no new stations are permitted to log on.  The STATIONMAX value 
              must be in the range 0 to 9999.  The default is 9999. 
              Permitted at or after TP initialization. 
  TPUI[NITIAL] [=] n 
              Specifies the number (0-9999) of 'general' TP Users (TPUs) to 
              start during initialization.  A 'general' TPU is one that 
              processes any transaction type (i.e., can be used to invoke any 
              TPAP).  This number of TPUs is started regardless of any TPUs 
              started because of TRANSACTION commands with the PERM option. 
              (The TPUINITIAL value must be no greater than the MAXTPU value 
              specified via CONTROL.)  The default is 1. 
              Permitted at TP initialization only. 
  XTN[SIZE] [=] n 
              Specifies the number of granules by which to increment the size 
              of the comgroup if the comgroup runs out of disk space.  The 
              default is 20. 
              Permitted at or after TP initialization. 
Description: 
This command sets operating parameters for the instance of TP. 
Usage Notes: 
Privilege is required for all LET options.  For the devices from which 
specific LET commands may be entered, type HELP (TPA) COMMAND_USAGE.  The 
memory pool for TPA is contains several different types of information 
required by TPA.  The TP context for both stations and TPUs, the TP Events, 
and the TP command bufffer are stored in the memory pool.  The memory pool is 
also used as a scratch pad for several of the TPA functions. 
The following is a rough calculation of the poolsize: 
    TP Initialization/pool management          250 words 
     + TPU context                              19 words/TPU 
     + Station context (no CMD specified)       26 words/station 
     + Station context (CMD specified)          55 words/station 
     + Outstanding Events                       23 words/event 
     + Disabled station context                 14 words/disable station 
Please note this is an approximation of POOLSIZE.  It can not be computed 
exactly because TPA also uses this area for temporary storage. 
00002
00003
00004
00005
00006
00018
00007
00008
00009
00010
00011
00012
00013
00019
00001
00014
00015
00016
00019
00017
Format: 
          [(station )] 
M[ESSAGE] [(MAST[ER])] text 
          [(console )] 
Parameters: 
station    is a 1 to 8 character station name that may include the wildcard 
(?) character. 
MASTER    identifies the Master Control Terminal(s) for the instance of TP. 
The default is MASTER. 
console    specifies a particular console; i.e., SYS[TEM], ADMIN[ISTRATIVE], 
COMM[UNICATION], DEV[ICE], TP. 
text    specifies the 1 to 80 character message; continuation from one line to 
another is not permitted. 
Description: 
This command sends a text message to the Master Control Terminal(s), 
station(s), or console(s) specified.  Conditions for delivery of messages to 
stations are similar to those for report transactions.  That is, if the 
destination station is explicitly identified by its station name (or by MASTER 
if the LET option MCTID=station is in effect), the message is queued for 
delivery to that station even if the station is not currently logged on.  If 
the destination station is identified by a wildcarded station name, the 
message is queued for delivery only to the stations that match the wildcarded 
name and that are currently logged on.  In either case, if a station is not in 
Command state at the time the MESSAGE command is performed, the station can 
receive the message whenever it enters Command state. 
Usage Notes: 
Privilege is required to send a message to multiple stations by specifying a 
wildcarded station name. 
00002
00003
00001
00003
To list all syntax notation conventions, enter ??.  To list a specific 
convention, enter: 
HELP (processor) NOTATION name 
Valid names are LOWERCASE, UPPERCASE, SPECIAL_CHARACTERS, NUMERALS, BRACKETS, 
BRACES, OR_BAR, HORIZONTAL_ELLIPSIS. 
  Notation    Description 
  lowercase 
              Lowercase letters indicate that the element is a variable, to be 
              replaced with the desired value. 
  UPPERCASE 
              Uppercase letters indicate a literal, to be entered as shown. 
  special characters 
              Special characters are literals, to be entered as shown. 
  numerals 
              Numerals standing alone are literals, to be entered as shown. 
              Numerals embedded in or affixed to a string of capital letters 
              are also literals, to be entered as shown, for example, GHOST1. 
              Numerals embedded in or affixed to a string of lowercase letters 
              are part of the variable name to be replaced with a desired 
              value, for example, attribute1. 
  brackets 
              An element inside brackets ([]) is optional.  If elements are 
              stacked vertically within brackets, the elements may be omitted 
              or one of them may be entered.  For example, the notation 
                [DISK] 
                [TAPE]    means that the user may omit this entry, 
                          or may enter DISK, or may enter TAPE. 
              Alternatively, the vertical OR bar is used to separate the 
              possible choices, thus:  [DISK|TAPE] 
              When used to enclose keywords, brackets signify that the 
              bracketed portion may be omitted, or truncated at any point. 
              For example, the notation K[EY] means that the user may enter K, 
              KE, or KEY. 
  braces 
              Elements stacked inside a pair of braces ({}) identify a 
              required choice. 
                   {id } 
                   {ALL}    means that either a value for id or 
                            the word ALL must be entered. 
              Alternatively, the vertical OR bar is used to separate the 
              choices, thus:  {id|ALL}. 
  OR bar 
              The OR bar (|) separates elements in a list from which one 
              element may be, or must be, chosen.  For example, see the 
              description of the brackets convention and the braces 
              convention, above. 
  horizontal ellipsis 
              The horizontal ellipsis (...) indicates that a previous 
              bracketed element may be repeated, or that elements have been 
              omitted. 
                name [,name] ... 
                    or 
                name1[,name2] ... means that one or more name 
                                  values may be entered, with 
                                  commas inserted between the 
                                  name values. 
00006
00005
00008
00001
00004
00007
00003
00002
BYE
Format: 
PASS[WORD] {[OLD=oldvalue][,] [NEW=newvalue]} 
Parameters: 
oldvalue    specifies the 1 to 8 character password currently assigned to the 
end-user. 
newvalue    specifies the 1 to 8 character password to be assigned to this 
end-user. 
Description: 
This command changes the end-user's logon password.  If both OLD and NEW 
values are specified, the existing password is changed to the new value.  (In 
this case only, the comma is required.)  If NEW is specified and OLD is 
omitted, a password is created if a password did not exist previously.  If OLD 
is specified and NEW is omitted, the password is eliminated. 
Usage Notes: 
This command may be entered after TP initialization only.  After a password 
command has been successfully processed by TPA, the user will receive the 
message "Password change successful". 
00002
00003
00001
00003
Format: 
PRIO[RITY] station {DEF[AULT]} 
                   {[+|-]  n } 
Parameters: 
station    specifies a 1 to 8 character station name.  The name may include 
the wildcard (?) character. 
n    specifies an integer value used to increment (+) or decrement (-) the 
current station's priority, or specifies the priority value if the + or - is 
omitted. 
Description: 
This command changes a station's priority.  Station priority is a value 
between 1 and 500; 500 is the highest priority.  This command increments, 
decrements, or modifies this value, or returns it to the the default priority 
assigned via SUPER when this station was created. 
Both privileged and non-privileged stations may modify their own priority.  A 
non-privileged station cannot request priority greater than the default 
defined for this station via SUPER however.  Changes made to station priority 
are in effect until another PRIORITY command is entered, station priority is 
changed via SUPER, or the station logs off the system. 
NOTE:  If SUPER is run online while the instance of TP is operating and a 
change is made to the station priority, the change does not affect stations 
that are already logged on but does affect stations that log on subsequently. 
Usage Notes: 
Privilege is required to modify the station priority of another station. 
Privilege is also required to modify the station priority via a wildcarded 
station name and to request priority greater than the default defined for a 
station via SUPER. 
00002
00003
00001
00003
Format: 
PRO[FILE] profile (PERM) 
Parameters: 
profile    specifies a terminal type as represented by a profile name. 
Profiles are defined and supported by the system manager. 
PERM    specifies that the change should be permanent, i.e., used the next and 
subsequent times the end-user logs on. 
Description: 
This command sets the terminal profile for the Transaction Processing session. 
The PROFILE command can also be issued at logon using the PRO option.  The 
syntax is: 
    LOGON PLEASE:account,[uname],password PRO=profile 
Usage Notes: 
This command may be entered after TP initialization only. 
A list of system-supported profiles can be obtained via a DISPLAY PROFILE 
command entered at a time-sharing terminal. 
00002
00003
00001
00003
Format: 
READ fid 
Parameters: 
fid    specifies a CP-6 file identifier for a file that contains only TP 
commands. 
Description: 
This command reads and performs the TP commands contained in the specified 
file.  Execution and reporting of any errors are performed in the same way as 
for XEQ files. 
NOTE:  A READ command must not be appear in a file that is the subject of a 
READ command. 
Usage Notes: 
Privilege is required to execute this command. 
00002
00003
00001
00003
Format: 
          {type[.station]} 
REL[EASE] {id[.station]  } 
          {.station      } 
Parameters: 
type    specifies a data entry or spawned transaction type.  type may include 
the wildcard (?) character. 
station    if specified without type or id, .station identifies all data entry 
or spawned transactions associated with the named station.  If used together 
with type or id, .station specifies only the transactions of the type or id 
for the named station.  station may include the wildcard (?) character.  The 
default is the current station. 
id    specifies a transaction ID of a data entry or spawned transaction.  The 
form of id is n for a data entry transaction.  The form of id is n-m for a 
spawned transaction, where n identifies the data entry transaction which 
resulted in creation of spawned transaction m. 
Description: 
This command removes the specified transaction(s) from "hold" status. 
Transactions that are released are scheduled for processing as if they had 
just been received by the comgroup. 
Usage Notes: 
Privilege is required to release another station's held transaction(s). 
00002
00003
00001
00003
Format: 
type[.password] [[BY] DEF[AULT]] 
Parameters: 
type        specifies the Forms Program type. 
password    password associated with the Forms Program. 
Description: 
This command provides several options for invoking Forms Programs: 
1.  With the type, optional password, and no options specified, Rununit Type 
    invokes the specified Forms Program. 
2.  With the type, optional password, and BY DEFAULT options, Rununit Type 
    invokes the specified Forms Program and makes that program the default 
    Forms Program.  A user-specified default Forms Program customizes the 
    interface between the end-user and the TP system by providing a choice of 
    options (i.e., a menu) and loading the user Forms Program based on the 
    end-user's option selection.  Once established as the default Forms 
    Program for a TP station, that program receives control whenever other 
    user Forms Programs exit or abort.  When the default Forms Program exits 
    or if it should abort, the TP station is logged off the system. 
    Note:  The assignment of a default remains in effect until TP station 
    logoff or until entry of another BEGIN, Rununit Type, or START command 
    specifying BY DEFAULT. 
00002
00001
Format: 
    [TPU    ] 
SPY [station] 
Parameters: 
station    specifies a station name that may include the wildcard (?) 
character. 
Description: 
If station is specified, this command displays information about the specified 
station(s) if they are logged on.  If TPU is specified, it displays 
information about all TPAPs (which are currently operating in TP User slots). 
If no option is specified, it displays information about all TPAPs in TPUs and 
all stations currently logged on to the instance of TP. 
The display for TPAPs operating in TPUs includes the following: 
Station     Name of the DCB through which the TPAP is connected to the 
            comgroup. 
Time        Time of TPAP invocation. 
Type        TPU if the TPAP is operating as a TP User or STRANGER if the TPAP 
            is operating as a time-sharing user with the DCBCON=ON option. 
Msgtype     The data entry or spawned transaction type that the TPAP is 
            processing. 
Sysid       The system ID assigned to the TPAP. 
Disconnect  Indicates if the TPAP's DCB is in the process of being 
            disconnected from the comgroup. 
Timeout     The time period in minutes that the TPAP operating in a permanent 
            TPU is to leave a read pending to obtain the next incoming 
            transaction. 
Usage Notes: 
This command can be entered after TP initialization only. 
00002
00003
00001
00003
Format: 
START [type[.password]] {[[BY] DEF[AULT]]} 
                        {[U|UNDER] [debuggername]} 
Parameters: 
type    specifies the Forms Program type. 
password    password associated with the Forms Program. 
debuggername    DELTA or user specified debugger. 
Description: 
This command provides several options for invoking Forms Programs: 
1.  With the type, optional password, and no options specified, START invokes 
    the specified Forms Program. 
2.  With the type, optional password, and BY DEFAULT options, START invokes 
    the specified Forms Program and makes that program the default Forms 
    Program.  A user-supplied default Forms Program customizes the interface 
    between the end-user and the TP system by providing a choice of options 
    (i.e., a menu) and loading the user Forms Program based on the end-user's 
    option selection.  Once established as the default Forms Program for a TP 
    station, that program receives control whenever other user Forms Programs 
    exit or abort.  When the default Forms Program exits or if it should 
    abort, the TP station is logged off the system. 
    Note:  The assignment of a default remains in effect until TP station 
    logoff or until entry of another START, rununit_command, or BEGIN command 
    specifying BY DEFAULT. 
3.  With the type, optional password, and the UNDER debuggername option, START 
    invokes the specified Forms Program.  Instead of beginning execution 
    immediately, the Forms Program is under control of DELTA, the debugger (a 
    user at a time-sharing terminal communicates with DELTA to direct 
    debugging activities).  If the end-user entering DEBUG commands is not 
    authorized to access the program, if the program is disabled, or if 
    debugging is prevented for the program, a message is returned and the 
    station remains in Command state. 
00002
00001
Format: 
STATS [SNAP ] 
      [DELTA] 
Description: 
This command displays statistics pertaining to the operation of the instance 
of TP.  Statistics gathering occurs once every 60 seconds.  When SNAP is 
specified, the statistics displayed reflect values accumulated from start-up 
of the instance of TP.  When DELTA is specified, the statistics displayed 
reflect changes to the SNAP statistics within the last 60 seconds.  If neither 
SNAP nor DELTA is specified, the default is SNAP. 
The statistics displayed include the following: 
    Item                   Description 
    TPAP reads from CG     Number of DCB reads by TPAPs to the comgroup, 
                           including reads that result in the end-of-file 
                           status. 
    FP reads from CG       Number of reads to the comgroup by Forms Programs 
                           and number of Forms Program loads. 
    Msgs in CG to TPAPs    Number of data entry and spawned transactions in 
                           the comgroup. 
    DCBs opened to CG      Number of DCBs opened to the comgroup.  (One 
                           additional DCB per TPAP is used by the TP system.) 
    CG reads from disk     Number of times the comgroup read the disk queue 
                           for transactions or internal message data, i.e., 
                           the memory allocated to the comgroup was full and 
                           comgroup data written to disk was read. 
    CG pages * ms          A floating point number expressing the number of 
                           pages in use by the comgroup multiplied by the 
                           number of 10-millisecond increments the pages were 
                           in use. 
    FP loads               Number of Forms Program requests made via the BEGIN 
                           or DEBUG command or via an FPL LOAD statement. 
                           This statistic includes one for each time the 
                           default Forms Program is loaded (i.e., any time a 
                           Forms Program stops or aborts).  In addition if the 
                           default Forms Program is different from the Command 
                           Forms Program, one more count is added to 'FP 
                           loads' at logon of a station. 
    TPA events             Number of TP commands, Forms Program load requests, 
                           interactions with TPCP, administrative events 
                           (e.g., station disconnections), internal messages 
                           sent by TPCP, Forms Program aborts, occurrences of 
                           TP statistics collection. 
    TPAP writes to CG      Number of TPAP writes. 
    FP writes to CG        Number of writes to the comgroup by Forms Programs. 
    Msgs in CG to FPs      Number of transactions in the comgroup awaiting 
                           transmission to terminal stations. 
    Terminals on CG        Number of connected terminals. 
    CG data write->disk    Number of times the comgroup wrote transactions or 
                           internal message data to disk because data could 
                           not be accommodated in comgroup memory. 
    CG attrib wrt->disk    Number of times comgroup wrote the attributes for 
                           transactions and internal messages to disk because 
                           they could not be accommodated in comgroup memory. 
    TPUs active            Number of TPUs operating. 
    TP commands exec'd     Number of TP commands processed. 
00001
Format: 
STOPTP! [NOW!] 
Description: 
This command shuts down an instance of TP.  If NOW! is specified, shutdown 
occurs immediately; if NOW! is omitted current processing is completed.  See 
the KILL command for details. 
Usage Notes: 
Privilege is required to execute this command; this command may be entered 
after TP initialization only. 
00001
00002
00002
Format: 
       {type[.station]} 
SWITCH {  id[.station]} TO dest_station 
       {     .station } 
Parameters: 
type    specifies a report transaction type to be redirected.  Type may be 
wildcarded. 
station    if specified without type or id, .station specifies that all the 
report transactions associated with the station are to be redirected.  If 
specified with type or id, .station specifies only the transactions of the 
type or id for the named station.  The station name may include the wildcard 
(?) character. 
dest_station    specifies the station to receive the report transaction(s). 
The dest_station may not include the wildcard (?) character. 
id    specifies the transaction ID of the specific report transactions to be 
redirected.  The id is of the form n[-m] as explained in the discussion of 
CHECK. 
Description: 
This command redirects delivery of report transactions.  This command 
overrides the station(s) associated with the report transactions at the time 
they were written to the comgroup and instead delivers them to the station 
identified by dest_station.  This command affects only report transactions 
currently in the comgroup. 
Usage Notes: 
Privilege is required to change the destination of another station's report 
transactions. 
00002
00003
00001
00003
NOTATION
Format: 
TIME 
Description: 
Requests a display of the current time and date. 
00001
Format: 
TRANS[ACTION] TYPE = type, option1[,option2]... 
Parameters: 
type    specifies a transaction type.  Wildcarding can be used if the option 
specified for a data entry or spawned transaction is PERM or with the TIMEOUT 
option.  For example, the following is permitted: 
    TRANS TYPE=?,PERM=n,TIME=n 
option1,option2    specify any of the appropriate options.  To obtain HELP 
messages for the TRANSACTION options, enter HELP (TPA) TRA option_name, where 
option_name is one of the following: 
JOUR[NAL] = {ON|OFF}, MAXAC[TIVE] = n, NOW, ONE[REPORT] [=] {ON|OFF}, 
PERM[ANENT] = n, PRIO[RITY] = n, TIME[OUT] [=] n. 
Descriptions are in tabular format with two columns, as follows: 
  Option      Description 
  JOUR[NAL] [=] {ON|OFF} 
              Specifies, if ON, that this transaction type is to be written to 
              the common journal.  The default is JOURNAL=OFF. 
  MAXAC[TIVE] = n 
              Specifies the maximum number (0-9999) of TPUs that can be active 
              at one time for this transaction type.  (n is also constrained 
              by the total number of TPUs authorized for the instance of TP.) 
              This option overrides the MAXACTIVE parameter specified in the 
              TRADER file.  This option may be specified for data entry and 
              spawned transactions only. 
  NOW 
              Specifies that the TPAP associated with the named transaction 
              type is to be started immediately, if a TPU slot processing that 
              type is available.  (If a TPU slot is not available, an error 
              message is displayed.)  The NOW option overrides the normal 
              scheduling and priorities.  This option may be specified for 
              data entry and spawned transactions only, and must not be 
              specified for wildcarded transaction types. 
  ONE[REPORT] [=] {ON|OFF} 
              If ON, specifies that a group of related transactions created by 
              one TPAP is to be treated as a "logical report".  That is, if 
              two or more "logical reports" are ready for transmission to a 
              terminal station, consecutive reads by the Forms Program obtain 
              all report transactions of the complete logical report before 
              receiving any part of another logical report; in other words, 
              transactions of the different logical reports are not 
              interleaved.  This option pertains to report transactions only. 
              The default is ONEREPORT=OFF. 
  PERM[ANENT] = n 
              Specifies the number (0-9999) of permanent TPUs to devote to 
              this transaction type.  (n is also constrained by the total 
              number of TPUs authorized for the instance of TP.)  This option 
              must be used with care.  Increasing the number of permanent TPUs 
              for one transaction type can reduce the number of TPU slots 
              available to process other transaction types.  If n=0, all TPUs 
              for the specified transaction type are stopped.  Decreasing the 
              number of permanent TPUs for a transaction type causes the 
              TPAP(s) in the permanent slot(s) to be removed (i.e., it has the 
              same effect as the KILL DCB command without NOW!). 
              Specifying PERM for a wildcarded transaction type causes 
              start-up of the requested number of TPUs and reserves those TPUs 
              for any TPAP(s) that process the transactions that match the 
              wildcarded transaction type.  Specifying PERM for a 
              non-wildcarded transaction type causes start-up of the number of 
              TPUs requested and invokes the TPAP for that transaction type in 
              the TPU(s); the TPAP remains in operation in the TPU(s) 
              (overriding the SINGLE or AVAILABLE read-mode associated with 
              the TPAP), unless the TIMEOUT option is also specified. 
              This option may be specified for data entry and spawned 
              transactions only. 
              The PERM option cannot exceed the MAXACTIVE option of the 
              TRANSACTION command, or the CONTROL processor's MAXTPU option 
              for that instance. 
  PRIO[RITY] = n 
              Specifies the transaction priority (1-500), where 500 represents 
              the highest priority.  This option overrides the transaction 
              priority specified in the TRADER file.  This option may be 
              specified for data entry and spawned transactions only. 
  TIME[OUT} [=] n 
              Specifies the number (1-4000) of minutes that a read is to 
              remain pending for the specified transaction type.  This option 
              must be accompanied by the PERM option.  The timeout option 
              allows memory and other resources such as data files used by the 
              TPAP to be released if there are no transactions of the 
              specified type to be processed. 
Description: 
This command changes parameters that affect the processing of a specific type 
of transaction.  Changes made by this command are in effect until another 
TRANSACTION command for the same type is entered. 
The node, line, port, and controller information are included in the message 
to the TPA's DO file and the MCT upon receipt of unexpected disconnects of 
stations. 
NOTE:  If TRADER is run while the instance of TP is operating and a change is 
made to transaction PRIORITY, JOURNAL or MAXACTIVE, the changes do not affect 
current operation.  Those changes take affect after the next TP 
initialization.  However, the TRANSACTION command may be used to change these 
parameters while the instance of TP is operating. 
Usage Notes: 
Privilege is required to use this command. 
00009
00002
00003
00010
00004
00005
00001
00006
00007
00008
00010
Rununit
Format: 
U[NDER] [debuggername] 
Description: 
This command is used in conjunction with the Rununit Type command to invoke a 
Forms Program under the control of DELTA, the debugger.  A user at a 
time-sharing terminal communicates with DELTA to direct debugging activities. 
If the end-user entering DEBUG commands is not authorized to access the 
program, if the program is disabled, or if debugging is prevented for the 
program, a message is returned and the station remains in the Command state. 
Note: The Rununit Type command must immediately follow the UNDER command in 
the form type[.password]. 
00001
