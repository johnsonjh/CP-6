The CONTROL processor allows the system manager to set, modify, and display 
parameters in order to tune the system dynamically to meet the needs of a 
particular installation.  CONTROL is capable of modifying these major 
categories of parameters: 
EXCEPTIONAL, PARTITION, RESOURCE, RUN_UNIT, SYSTEM, TP. 
To obtain HELP for these topics, see: 
HELP (CONTROL) name_PARAMS 
To obtain more HELP information, see: 
HELP (CONTROL) TOPICS         Displays available topics. 
HELP (CONTROL) COMMANDS       Displays a list of commands. 
HELP (CONTROL) command PARAM  Displays parameters associated 
                              with a particular command. 
HELP (CONTROL) command DESC   Displays a description 
                              associated with a particular 
                              command. 
?                             Displays next level of HELP 
                              messages. 
??                            Displays all levels of HELP 
                              messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
Format: 
AD[D] [item[, item] ... ] 
Parameters: 
item    specifies any of the following: 
Item            Display Flag Description 
----            ------------------------ 
ALL             All parameters. 
ASL             Alternate Shared Library domain indicator 
B[ATCH]         Mode indicator for Batch 
CP              Command Program domain indicator 
DB              Debugger domain indicator 
EX[CEPTIONAL]   All parameters in the EXCEPTIONAL parameter category 
G[HOST]         Mode indicator for Ghost 
O[NLINE]        Mode indicator for On-line 
parameter       CONTROL parameter name without qualification. 
PART[#][n]      Partition number, range or list 
PART[ITION]     All parameters in the PARTITION parameter category 
RES[OURCE]      All parameters in the RESOURCE parameter category 
SYS[TEM]        All parameters in SYSTEM parameter category 
TP              Mode indicator for Transaction Processing 
TPC[AT]         All parameters in the TP parameter category 
U[SER]          User domain indicator 
               For more information on these items, see 
               the following HELP topics: MODE, DOMAIN, 
               EXCEPTIONAL_PARAMS, PARTITION_PARAMS, 
               PART#, RESOURCE_PARAMS, SYSTEM_PARAMS, and 
               TP_PARAMS. 
The default is ALL. 
Note:  For a qualifiable parameter to be printed by the DISPLAY command, two 
print flags must have been set: the flag for the parameter name and the flag 
for the qualifier (mode, partition, or domain).  The two print flags may have 
been set in one ADD command, or in separate ADD commands. 
Description: 
The ADD command turns on the display flags for specified CONTROL parameters. 
The parameters to be flagged may be specified individually or by category. 
The flags set by the ADD command determine what parameters are displayed in 
response to the DISPLAY command. 
00002
00001
Format: 
CL[EAR] 
Description: 
The CLEAR command removes any previously SET but not STOREd values from the 
Partition Definition Table (PDT).  See also the HELP topics HELP (CONTROL) SET 
and HELP (CONTROL) STORE. 
00001
A list of CONTROL commands and their definitions can be accessed by typing a ? 
or a ??.  To obtain definitions of individual parameters, type 
HELP (CONTROL) COMMANDS command 
where command is any of the following: 
ADD, CLEAR, DATE, DELETE, DIRECTORY, DISPLAY, DO, DROP, END, ERASE, 
ENTER, EXIT, HELP, LIST, OUTPUT, PRINT, QUIT, SET, TIME, STORE. 
  Command        Description 
  ADD 
                 Turns on display flags for specified CONTROL parameters. 
  CLEAR 
                 Erases values in CONTROL'S Partition Definition Table (PDT). 
  {DATE|TIME} 
                 Displays the current time and date. 
  DELETE 
                 Deletes TP instances previously defined via CONTROL. 
  {DIRECTORY|DIR} 
                 Changes the default account and packset. 
  DISPLAY 
                 Prints out values of selected CONTROL parameters. 
  {DO|!} 
                 Enable IBEX command execution. 
  DROP 
                 Turns off display flags for specified CONTROL parameters. 
  {END|EXIT|QUIT} 
                 Terminates execution of the CONTROL processor. 
  ENTER 
                 Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
                 Deletes accumulated output for logical devices. 
  HELP 
                 Displays information on the CONTROL and other processors. 
  LIST 
                 Outputs a list of CONTROL parameters and categories for which 
                 display flags are set. 
  OUTPUT 
                 Sends subsequent output to the specified file. 
  PRINT 
                 Directs that output accumulated for logical devices be sent 
                 to destinations immediately. 
  SET 
                 Assigns values to CONTROL parameters; updates options in a 
                 run unit head record. 
  STORE 
                 Stores values from CONTROL's Partition Definition Table (PDT) 
                 into monitor's partition tables. 
00007
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
00009
00012
00013
00014
00015
00009
00016
00017
00003
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm    (month)(day)(year)(hours)(minutes) 
Examples: 
-DATE 
requests a display of the current date and time.  A sample display is: 
AUG 02  '88  11:03 
00001
00002
Format: 
DEL[ETE] TPI[NSTANCE]=instance_list 
Parameters: 
instance_list    specifies the list of instance names, separated by commas. 
Description: 
The DELETE command deletes TP instances previously defined by CONTROL. 
Note:  An active TP instance may not be deleted; if an attempt is made to do 
so, an error message will be printed. 
00002
00001
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
-DIRECTORY .SYSLIB 
This command directs that subsequent fids that do not include an account are 
to default to the .SYSLIB account and the packset associated with that 
account. 
-DIRECTORY DP#UTIL.Y 
This command specifies that subsequent fids that do not include an account are 
to default to the Y account on the packset named UTIL. 
-DIRECTORY RESET 
This command re-establishes the running account and its associated packset as 
the default. 
00002
00003
00001
Format: 
Form 1: 
DI[SPLAY] 
Form 2: 
DI[SPLAY] [item[, item] ... ] 
Parameters: 
item    specifies any of the following: 
Item               Display Flag Description 
----               ------------------------ 
ALL                All parameters. 
EX[CEPTIONAL]      All parameters in the EXCEPTIONAL parameter category 
EXP[TIME] [(ALL)]  All types of EXPTIME System parameters. 
fid ru_list        Standard CP-6 file identifier followed by one or 
                   more RUN UNIT parameters.  If more than one is 
                   specified, options are separated by a comma.  ALL 
                   may be specified to display all RUN UNIT parameters. 
                   If requested, the 72-bit rununit lock is displayed 
                   in octal. 
IO[CACHE]          All types of EXPTIME and UPDLIMIT System parameters. 
parameter          CONTROL parameter name with or without qualification. 
PART[#][n]         Partition number, range or list 
PART[ITION]        All parameters in the PARTITION parameter category 
PDT                CONTROL's Partition Definition Table (PDT) 
RES[OURCE]         All parameters in the RESOURCE parameter category 
SEC[URITY]         All System parameters related to security, such 
                   as LOGFILEGRANT, LOGFILEDENY, PRIVMASK, SETPRIVMASK, 
                   etc. 
SYS[TEM]           All parameters in the SYSTEM parameter category 
TPC[AT]            All parameters in the TP parameter category 
UPD[LIMIT] [(ALL)] All types of UPDLIMIT System parameters. 
                   For more information on these items, see 
                   the following HELP topics: EXCEPTIONAL_PARAMS, 
                   PARTITION_PARAMS, PART#, RESOURCE_PARAMS, SET, 
                   SYSTEM_PARAMS and TP_PARAMS. 
Description: 
The DISPLAY command instructs the processor to print out the values of 
selected parameters.  Form 1 of the command will cause printing of the values 
of those parameters whose display flags have been set by the ADD command. 
Form 2 of the command will cause printing of the values of the parameters 
specified in the list of items. 
Examples: 
DISPLAY UM,PART#(3),MAXMT(B),EXCEPTION 
will display the following items (1) the values for the maximum number of 
users allowed for each mode, (2) a table of all parameters associated with 
partition 3, (3) the maximum tape drives allowed any batch job, (4) a table of 
all exceptional condition parameters. 
DROP 
ADD UM,BATCH,PARTITION,PART#(ALL) 
DISPLAY 
DROP resets all display flags; ADD sets specified flags; DISPLAY prints UM(B) 
and the partition table display. 
00002
00003
00001
DOMAIN
The EXCEPTIONAL parameters may be qualified by adding one or more domain 
indicators enclosed in parentheses.  The domain indicators are: 
    ASL         Alternate Shared Library domain 
    CP          Command Processor domain 
    DB          Debugger domain 
    U[SER]      User domain 
If no domain is specified, the parameter applies to all domains.  For example, 
the parameter shown as ETIME(dmn) may be entered as ETIME (U,DB,CP,ASL) or 
ETIME for execution time allowed for exceptional condition processing in all 
modes. 
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
-DO DI 
means display the current system status 
-!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00003
00001
Format: 
DR[OP] [item[, item] ... ] 
Parameters: 
item    specifies any of the following: 
Item            Display Flag Description 
----            ------------------------ 
ALL             All parameters. 
ASL             Alternate Shared Library domain indicator 
B[ATCH]         Mode indicator for Batch 
CP              Command Program domain indicator 
DB              Debugger domain indicator 
EX[CEPTIONAL]   All parameters in the EXCEPTIONAL parameter category 
G[HOST]         Mode indicator for Ghost 
O[NLINE]        Mode indicator for On-line 
parameter       CONTROL parameter name without qualification. 
PART[#][n]      Partition number, range or list 
PART[ITION]     All parameters in the PARTITION parameter category 
RES[OURCE]      All parameters in the RESOURCE parameter category 
SYS[TEM]        All parameters in SYSTEM parameter category 
TP              Mode indicator for Transaction Processing 
TPC[AT]         All parameters in the TP parameter category 
U[SER]          User domain indicator 
               For more information on these items, see 
               the following HELP topics: MODE, DOMAIN, 
               EXCEPTIONAL_PARAMS, PARTITION_PARAMS, 
               PART#, RESOURCE_PARAMS, SYSTEM_PARAMS, and 
               TP_PARAMS. 
The default is ALL. 
Description: 
The DROP command turns off the display flags for specified CONTROL parameters. 
The parameters may be specified individually or by category. 
00002
00001
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
The END command (and is synonyms EXIT and QUIT) terminates execution of the 
CONTROL processor. 
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
-ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
00001
A list of exceptional parameters and their definitions can be accessed by 
typing a ? or a ??.  To obtain definitions of individual parameters, type 
HELP (CONTROL) EXCEPTIONAL_PARAMS param 
where param is any of the following: 
ECPO, EDO, EPDISK, EPO, ETDISK, ETIME. 
For information on the domain (dmn) qualifier included in EXCEPTIONAL 
parameters, type HELP (CONTROL) DOMAIN. 
  Parameter      Explanation 
  ECPO[(dmn)]=n 
                 The number of cards of punched output allowed to a job after 
                 its limit is exceeded.  The defaults are 10 for ASL, 20 for 
                 CP, 15 for DB, 5 for user. 
                 Units: cards           Minimum: 0     Maximum: (2**17)-1 
  EDO[(dmn)]=n 
                 The number of pages of diagnostic output allowed to a job 
                 after its limit is exceeded.  The defaults are 10 for ASL, 20 
                 for CP, 15 for DB, 5 for user. 
                 Units: pages           Minimum: 0     Maximum: (2**17)-1 
  EPDISK[(dmn)]=n 
                 The amount of permanent disk storage allowed to a job after 
                 its limit is exceeded.  The defaults are 10 for ASL, 20 for 
                 CP, 15 for DB, 5 for user. 
                 Units: granules        Minimum: 0     Maximum: (2**35)-1 
  EPO[(dmn)]=n 
                 The number of pages of printed output allowed to a job after 
                 its limit is exceeded.  The defaults are 10 for ASL, 20 for 
                 CP, 15 for DB, 5 for user. 
                 Units: pages           Minimum: 0     Maximum: (2**17)-1 
  ETDISK[(dmn)]=n 
                 The amount of temporary disk storage allowed to a job after 
                 its limit is exceeded.  The defaults are 10 for ASL, 20 for 
                 CP, 15 for DB, 5 for user. 
                 Units: granules        Minimum: 0     Maximum: (2**35)-1 
  ETIME[(dmn)]=n 
                 Clean-up time allowed to a job after its time limit is 
                 exceeded.  The defaults are 9999 for ASL, 5 for CP, 5 for DB, 
                 5 for user. 
                 Units: seconds         Minimum: 0     Maximum: (2**35)-1 
00001
00002
00003
00004
00005
00006
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
  accounting, processor - 
      HELP RUN_UNIT_PARAMS PROCACC 
  ADD Command - 
      HELP ADD 
  AUTO priority - 
      HELP SYSTEM_PARAMS AUTO_PRIO 
  automatically shared procedure priority - 
      HELP SYSTEM_PARAMS AUTO_PRIO 
  AUTOSHARE - 
      HELP SYSTEM_PARAMS AUTOSHARE 
  AUTO_PRIO - 
      HELP SYSTEM_PARAMS AUTO_PRIO 
C 
  cache pages priority - 
      HELP SYSTEM_PARAMS CACHE_PRIO 
  CACHE priority - 
      HELP SYSTEM_PARAMS CACHE_PRIO 
  CACHE_PRIO - 
      HELP SYSTEM_PARAMS CACHE_PRIO 
  CG priority - 
      HELP SYSTEM_PARAMS CG_PRIO 
  CG_PRIO - 
      HELP SYSTEM_PARAMS CG_PRIO 
  CLEAR Command - 
      HELP CLEAR_COMMAND 
  :CNTRL file - 
      HELP RELATED_FILES 
  comgroup pages priority - 
      HELP SYSTEM_PARAMS CG_PRIO 
  CONTROL -   
    ADD Command - 
      HELP ADD FORMAT: 
    CLEAR Command - 
      HELP CLEAR_COMMAND FORMAT: 
    DELETE Command - 
      HELP DELETE_COMMAND FORMAT: 
    DISPLAY Command - 
      HELP DISPLAY_COMMAND FORMAT: 
    DROP Command - 
      HELP DROP_COMMAND FORMAT: 
    END Command - 
      HELP END_COMMAND FORMAT: 
    LIST Command - 
      HELP LIST_COMMAND FORMAT: 
    SET Command - 
      HELP SET_COMMAND FORMAT: 
    STORE Command - 
      HELP STORE_COMMAND FORMAT: 
  CONTROL job, running - 
      HELP INVOKING_CONTROL 
  CONTROL_S file - 
      HELP RELATED_FILES 
D 
  DATE Command - 
      HELP DATE_COMMAND 
  DELETE Command - 
      HELP DELETE_COMMAND 
  DELETE Command (CONTROL) - 
      HELP DELETE_COMMAND FORMAT: 
  DIRECTORY Command - 
      HELP DIRECTORY_COMMAND 
  DISPLAY Command - 
      HELP DISPLAY_COMMAND 
  DISPLAY Command (CONTROL) - 
      HELP DISPLAY_COMMAND FORMAT: 
  DO Command - 
      HELP DO_COMMAND 
  Domain indicators - 
      HELP DOMAIN 
  DROP Command - 
      HELP DROP_COMMAND 
E 
  END Command - 
      HELP END_COMMAND 
  END Command (CONTROL) - 
      HELP END_COMMAND FORMAT: 
  ENQ/DEQ maximum requests - 
      HELP SYSTEM_PARAMS MAXENQ 
  ENTER Command - 
      HELP ENTER_COMMAND 
  ERASE Command - 
      HELP ERASE_COMMAND 
F 
  Files Created and Used by CONTROL - 
      HELP RELATED_FILES 
  fully protected tape - 
      HELP SYSTEM_PARAMS ANSPROT 
G 
  granule update limit - 
      HELP SYSTEM_PARAMS UPDLIMIT 
H 
  HELP Command - 
      HELP HELP_COMMAND 
I 
  I/O cache pages priority - 
      HELP SYSTEM_PARAMS CACHE_PRIO 
  instance of TP - 
      HELP TP_PARAMS TPI 
  Invoking CONTROL - 
      HELP INVOKING_CONTROL 
J 
  :JOBSTATS - 
      HELP SYSTEM_PARAMS JOBSTATSAGE 
  :JOBSTATSAGE - 
      HELP SYSTEM_PARAMS JOBSTATSAGE 
L 
  limit, granule update - 
      HELP SYSTEM_PARAMS UPDLIMIT 
  LIST Command - 
      HELP LIST_COMMAND 
  LIST Command (CONTROL) - 
      HELP LIST_COMMAND FORMAT: 
M 
  memory saturation threshold - 
      HELP SYSTEM_PARAMS FREETHRESH 
O 
  OUTPUT Command - 
      HELP OUTPUT_COMMAND 
P 
  Partition Definition Table (PDT) - 
      HELP STORE_COMMAND DESCRIPTION: 
  partition lock - 
      HELP PARTITION_PARAMS PLOCK 
  PRINT Command - 
      HELP PRINT_COMMAND 
  priority, base execution - 
      HELP PARTITION_PARAMS PPRIO 
  priority, execution - 
      HELP SYSTEM_PARAMS PRIOB 
  priority, increment - 
      HELP SYSTEM_PARAMS PI 
      HELP SYSTEM_PARAMS PRIOB 
  Privileges for Use of CONTROL - 
      HELP PRIVILEGES 
  procedure priority - 
      HELP SYSTEM_PARAMS AUTO_PRIO 
  processor lock - 
      HELP RUN_UNIT_PARAMS WLOCK 
Q 
  quantum - 
      HELP SYSTEM_PARAMS QMIN 
S 
  Security Log - 
      HELP SYSTEM_PARAMS LOGMONSER 
  semi-protected tape - 
      HELP SYSTEM_PARAMS ANSPROT 
  SET Command - 
      HELP SET_COMMAND 
  SET Command (CONTROL) - 
      HELP SET_COMMAND FORMAT: 
  shareable program - 
      HELP RUN_UNIT_PARAMS SHAREABLE 
  shared procedure procedure - 
      HELP SYSTEM_PARAMS AUTO_PRIO 
  STORE Command - 
      HELP STORE_COMMAND 
  symbiont - 
      HELP SYSTEM_PARAMS GRANSCHED 
      HELP SYSTEM_PARAMS WATCH 
  System modes - 
      HELP MODE 
T 
  TIMEZONE -   
    setting - 
      HELP SYSTEM_PARAMS TIMEZONE 
  TP_CNTRL_D - 
      HELP RELATED_FILES 
U 
  unprotected tape - 
      HELP SYSTEM_PARAMS ANSPROT 
  update limit, granule - 
      HELP SYSTEM_PARAMS UPDLIMIT 
  user slots - 
      HELP SYSTEM_PARAMS MAXU 
  users, number in system - 
      HELP SYSTEM_PARAMS UM 
  users, number of TP - 
      HELP TP_PARAMS MAXTPU 
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
CONTROL may be run as a batch, ghost, or on-line job.  It is invoked by the 
!CONTROL command.  The DCBs used by CONTROL are: 
o   M$SI for input 
o   M$LO for normal output 
o   M$DO for output of error messages 
CONTROL commands are entered one per record. 
When run as an on-line job, CONTROL issues a hyphen (-) character to solicit 
commands. 
Format: 
LI[ST] 
Description: 
The LIST command instructs the processor to output a list of the CONTROL 
parameters and categories for which the display flags are set. 
00001
Some SYSTEM parameters may be qualified by adding one or more mode indicators 
enclosed in parentheses.  The mode indicators are: 
    B[ATCH]        Batch mode 
    G[HOST]        Ghost mode 
    O[NLINE]       On-line mode 
    TP             Transaction processing mode 
If no mode is specified, then the parameter applies to all modes.  For 
example, parameters shown as UM(mode) may be entered as UM(B,O,G,TP) or UM to 
set UM for all modes. 
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
-OUTPUT ON OUTPUTFILE 
-OUTPUT ON ME 
00002
00003
00001
Each PARTITION parameter may include a qualifier to designate the partition(s) 
affected.  (n) may specify a single partition number (1-16), a list of 
partition numbers, or a range of partition numbers.  The default for (n) is 
all partitions.  For example, PMINTI(1-16), PMINTI(1,2-16), and PMINTI all 
mean the same thing:  minimum execution time in all partitions. 
PART#
A list of partition parameters can be accessed by typing a ? or a ??.  To 
obtain definitions of individual parameters, type 
HELP (CONTROL) PARTITION_PARAMS param 
where param is any of the following: 
PJCTOT, PJCUR, PJMAX, PJTOT, PLOCK, PMAX, PMAXACCT, 
PMAXTI, PMIN, PMINTI, PPRIO, PQUAN. 
For information on the partition number (n) in PARTITION 
parameters, type HELP (CONTROL) PART#.  For information on 
resnm included in certain PARTITION parameters, type 
HELP (CONTROL) RESNM. 
  Parameter      Explanation 
  PJCTOT[(n)] 
                 The number of jobs run in partition n since its current 
                 definition was established.  The default is zero for each 
                 partition (1 through 16).  PJCTOT is a display only 
                 parameter. 
                 Units: jobs       Minimum: -          Maximum: - 
  PJCUR[(n)] 
                 The number of jobs currently executing in partition n.  The 
                 default is zero for each partition (1 through 16).  PJCUR is 
                 a display only parameter. 
                 Units: jobs       Minimum: -          Maximum: - 
  PJMAX[(n)]=n 
                 The maximum number of jobs allowed in partition n.  The 
                 defaults are 2 for partition 1, zero for partitions 2 through 
                 16. 
                 Units: jobs       Minimum: 0          Maximum: 511 
  PJTOT[(n)] 
                 The number of jobs run in this partition since system 
                 start-up.  The default is zero for each partition (1 through 
                 16).  PJTOT is a display only parameter. 
                 Units: jobs       Minimum: -          Maximum: - 
  PLOCK[(n)]={NO|YES} 
                 Partition lock control.  PLOCK(n) = YES means partition n is 
                 unavailable.  PLOCK(n) = NO means partition n available.  The 
                 default is NO for each partition (1 through 16). 
                 Units: -          Minimum: -          Maximum: - 
  PMAXresnm[(n)]=n 
                 The maximum value of the expected usage of the resource named 
                 resnm, as stated on the job's RESOURCE card.  The defaults 
                 for partition 1 are 256 for MM, 4 for DP, 4 for MT, 0 for OP. 
                 The default for partitions 2-16 is zero for each type. 
                 Units: resources  Minimum: PMINresnm  Maximum: TOTresnm 
  PMAXACCT[(n)]=n 
                 The number of jobs from the same account allowed to run 
                 concurrently in this partition.  The default is 511 for each 
                 partition (1 through 16). 
                 Units: job        Minimum: 1          Maximum: 511 
  PMAXTI[(n)]=n 
                 The maximum value of expected execution time, as stated on 
                 the job's LIMIT card.  The defaults are 9,999,999 for 
                 partition 1, zero for partition 2 through 16. 
                 Units: minutes    Minimum: PMINTI     Maximum: 2733169 
  PMINresnm[(n)]=n 
                 The minimum value of expected usage of the resource named 
                 resnm, as stated on the job's RESOURCE card.  The default is 
                 zero for each type for each partition (1 through 16). 
                 Units: resources  Minimum: 0          Maximum: PMAXresnm 
  PMINTI[(n)]=n 
                 The minimum value of expected execution time, as stated on 
                 the job's LIMIT card.  The defaults are zero for each 
                 partition (1 through 16). 
                 Units: minutes    Minimum: 0          Maximum: PMAXTI 
  PPRIO[(n)]=n 
                 The base execution priority assigned to a job running in this 
                 partition.  The default is one unit for each partition (1 
                 through 16). 
                 Note:  For efficient system operation, PPRIO should be set no 
                 higher than 3.  (See the SYSTEM parameter PRIOB.) 
                 Units: priority   Minimum: 1          Maximum: 511 
                        units 
  PQUAN[(n)]=n 
                 The quantum of time to be assigned to an execution period for 
                 a job in partition n.  The default is 500 for each partition 
                 (1 through 16). 
                 Units: milli-     Minimum: 20         Maximum: 511 
                        seconds 
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
-PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
00002
00003
00001
Use of CONTROL to examine the CONTROL parameters requires the CNTRLD processor 
privilege or the SPCLMM privilege; use of CONTROL to change these parameters 
requires the CNTRLC processor privilege or the EXMM privilege. 
The CONTROL_S.:SYS file is created by the user to contain CONTROL commands 
that set parameters at system initialization.  The file is read at tape boots 
(but not at disk boots or at recovery). 
CONTROL builds and maintains two files, :CNTRL and TP_CNTRL_D in :SYS. 
Current parameter values (set by CONTROL via ADD and SET commands) are always 
saved in a file named :CNTRL so that they survive across recoveries and disk 
boots.  (The system-initialized values that are installed on a system booted 
by tape can be examined through the CONTROL processor DISPLAY ALL command.) 
The file TP_CNTRL_D is created by CONTROL if a Transaction Processing 
environment is incorporated into a CP-6 system.  The TP_CNTRL_D file contains 
the TP control parameters required to define each TP instance. 
RESOURCE parameters are qualified by a resource type (resnm).  Standard 
designations are 
    DP      Disk drives 
    MM      Main memory 
    MT      Magnetic tape 
    OP      Unit record and other physical devices 
TIGR-defined pseudo resources can also be used as RESOURCE parameters. 
A list of resource parameters can be accessed by typing a ? or a ??.  To 
obtain definitions of individual parameters, type 
HELP (CONTROL) RESOURCE_PARAMS param 
where param is any of the following:  CUR, MAX, TOT 
For information on the resnm included in RESOURCE parameters, type 
HELP (CONTROL) RESNM.  For information on the (mode) included in certain 
RESOURCE parameters, type HELP (CONTROL) MODE. 
  Parameter      Explanation 
  CURresnm [(mode)] 
                 The current value of the usage of the resource named resnm. 
                 CURresnm is a display only parameter. 
                 Units: resources   Minimum: -        Maximum: - 
  MAXresnm [(mode)]=n 
                 The maximum permitted value of the resources named resnm. 
                 The defaults are 1,000,000 (words) for main memory for each 
                 mode and for all others either the values specified in the 
                 TIGR deck or calculated by TIGR at boot time. 
                 Units: resources   Minimum: 0        Maximum: TOTresnm 
  TOTresnm 
                 The total-available quantity of the resource named resnm. 
                 TOTresnm is a display-only parameter.  The displayed values 
                 are 7,000,000 (words) for main memory and, for all other 
                 displayed resources, either the values specified in the TIGR 
                 deck or the values calculated by TIGR at boot time. 
                 Units: resources   Minimum: -        Maximum: - 
00001
00002
00003
Type ? or ?? for a list of Run Unit parameters.  For individual parameter 
descriptions, type 
HELP (CONTROL) RU_PARAMS param 
Valid options for param are WLOCK, SLOCK, NOCHGPMEM, PROCACC, PROCSURCHG, 
PSEUDO, SHAREABLE, STATS. 
The primary purpose of a rununit pseudo resource is to limit simultaneous use 
of the run unit by authorizing the pseudo with a maximum value via a TIGR deck 
MON command.  For example: 
         . 
         . 
    RES (BIG=400),; 
         . 
         . 
After the system is booted, subsequent manipulation is accomplished using the 
CONTROL processor.  For example: 
    !CONTROL 
    -SETMAXBIG(0)=400 
    -SET SPSSX.:SYS PSEUDO=BIG,NUM=250 
    -SET COBOL.:SYS PSEUDO=BIG,NUM=100 
    -SET FORTRAN.:SYS PSEUDO=BIG,NUM=150 
    -END 
    ! 
With this setup, only one SPSSX user will be able to run online at a time. 
Four COBOL users will be able to run, or two COBOL users and one FORTRAN user. 
The point is to limit simultaneous large program execution. 
Note that the intention here is to control run unit use independently of SUPER 
user authorizations.  Authorizing users for the pseudo on-line defeats the 
purpose of setting up the CONTROL/TIGR aggregate limits. 
  Parameter      Description 
  {WLOCK|SLOCK}(n[-m][, n-[m]]...) 
                 Processor lock control. 
                 {WLOCK|SLOCK}    specifies either a WEAK or STRONG processor 
                 lock. 
                 n[-m]    are integers specifying which bit(s) in the lock to 
                 set or reset.  Legal values for n and m are 1 to 72, 
                 inclusive.  Only those bits specified will be assigned to 
                 that value.  Bits not specified remain unchanged. 
  NOCHGPMEM={YES|NO} 
                 Processor memory charge.  YES specifies there is to be no 
                 charge for processor memory if run from :SYS.  NO specifies 
                 there is to be a charge for processor memory run from :SYS. 
  PROCACC={YES|NO} 
                 Processor accounting (see HELP (RATES)).  YES specifies that 
                 processor accounting is to be used if run from :SYS.  NO 
                 specifies user accounting is to be used. 
  PROCSURCHG={YES|NO} 
                 Processor surcharge (see HELP (RATES)).  YES specifies there 
                 is to be a processor surcharge; YES can be specified only if 
                 the run unit is in :SYS.  PROCACC=YES will be assumed if 
                 PROCSURCHG=YES.  NO specifies no processor surcharge. 
  PSEUDO=resnm[,NUM=n] 
                 Sets the pseudo-resource requirement for starting a run unit. 
                 resnm    is a 1-8 character pseudo-resource name. 
                 n    is a decimal number that sets the number of 
                 pseudo-resources of type resnm that will be required by any 
                 user starting the run unit.  A value of zero indicates that 
                 NO pseudo-resources are required, and deletes the run unit's 
                 pseudo-resource information. 
  SHAREABLE={YES|NO} 
                 YES specifies the program is shareable.  NO specifies the 
                 program is not sharable.  For additional information see HELP 
                 (CONTROL) SYSTEM_PARAMS AUTOSHARE. 
  STATS={YES|NO} 
                 YES specifies statistics are to be collected for the run 
                 unit.  NO specifies statistics are not to be collected. 
00002
00003
00004
00005
00006
00001
00007
00001
RUN_UNIT_PARAMS
Format: 
Form 1: 
SE[T] item=value[, item=value] ... 
Form 2: 
SE[T] fid ru_list 
Parameters: 
item    may be any CONTROL parameter, with or without qualifier (e.g., (mode), 
(n), (type)).  For more information on these items, see the following HELP 
topics: MODE, DOMAIN, EXCEPTIONAL_PARAMS, PARTITION_PARAMS, PART#, 
RESOURCE_PARAMS, SYSTEM_PARAMS, and TP_PARAMS. 
value    may be a single value or a parameter list as described under the 
following HELP topics: MODE, DOMAIN, EXCEPTIONAL_PARAMS, PARTITION_PARAMS, 
PART#, RESOURCE_PARAMS, SYSTEM_PARAMS, and TP_PARAMS. 
ru_list    may be any RUN UNIT parameters and their values.  ru-list is 
formatted item=value[,item=value]... where item and value is as specified 
under the HELP topic RU_PARAMS. 
Description: 
Form 1 of the SET command assigns values to CONTROL parameters. 
Form 2 of the SET command updates options in a run unit head record (for 
accounting purposes). 
Form 1 of the SET command assigns values to the operating system tables in 
memory, with the exception of PARTITION parameters.  The PARTITION parameters 
are stored by the SET command in CONTROL's Partition Definition Table (PDT). 
(Values in the PDT can be moved to the monitor's PDT via the STORE command; 
values in CONTROL's PDT can be removed via the CLEAR command.) 
Note: If a PARTITION parameter is being SET, then the minimum and maximum 
limits for the value assigned to that parameter may come from two possible 
sources. 
1.  If a value is SET in the PDT for the parameter to be used as a limit, then 
    the value of that parameter in the PDT is used. 
2.  If the PDT holds no value for the limiting parameter, then the value 
    currently in the monitor's partition tables is used. 
Examples: 
PMAXTI is used to check the upper limit of PMINTI.  Suppose PMAXTI(1) = 20 in 
the Monitor's partition table, and that there is no value in the PDT for 
PMAXTI(1).  If the system manager wants to SET the time limits on partition 1 
to 40-60 minutes, the SET commands must be in the following order: 
SET PMAXTI(1) = 60 
SET PMINTI(1) = 40  40 is compared to the limit 60, found to be less 
                    than the limit, and accepted. 
If the order of the SET commands is: 
SET PMINTI(1) = 40 
SET PMAXTI(1) = 60 
When the check on 40 is done, and it is found that there is no value in the 
PDT for PMAXTI, the comparison value used is 20 from the Monitor's partition 
table.  Since 40 is greater than 20, this command will be rejected because of 
limit exceeded.  See also the following HELP topics: HELP (CONTROL) CLEAR and 
HELP (CONTROL) STORE. 
The following example displays current run unit parameters, sets a pseudo 
resource, and displays the run unit parameters again. 
-DI STATS.YOURLOG ALL 
STATS.YOURLOG: 
NOCHGPMEM=YES SHAREABLE=YES PROCASS=YES PROCSURCHG=NO STATS=NO 
PSEUDO=None defined WLOCK= 000000000000 000000000000 
-SET STATS.YOURLOG PSEUDO=ABC,NUM=2 
-DI STATS.YOURLOG ALL 
STATS.YOURLOG: 
NOCHGPMEM=YES SHAREABLE=YES PROCACC=YES PROCSURCHG=NO STATS=NO PSEUDO=ABC 
NUM=2 WLOCK= 000000000000 000000000000 
00002
00003
00001
Format: 
ST[ORE] 
Description: 
The STORE command stores the values of the PARTITION parameters resident in 
the CONTROL processor's Partition Definition Table into the monitor's 
partition tables.  STORE performs a CLEAR function after the values are 
stored.  See also the following HELP topics: HELP (CONTROL) CLEAR and HELP 
(CONTROL) SET. 
00001
A list of system parameters and their definitions can be accessed by typing a 
? or a ??.  To obtain definitions of individual parameters, type 
HELP (CONTROL) SYSTEM_PARAMS param 
where param is any of the following:  ANSPROT, AUTOSHARE, AUTO_PRIO, 
CACHE_PRIO, CG_PRIO, CLEARMEM, EXPTIME, FREETHRESH, GRANSCHED, HOLDEXPIRE, 
IOLEAPERS, IOTA, JOBSTATSAGE, LIMITU, LOGFILEDENY, LOGFILEGRANT, LOGMONSER, 
LOGPRIVCHNG, LOGSYSACCESS, LOGSYSEXIT, MAXACCT, MAXENQ, MAXU, MFBLK, MFUBL, 
MONSERTBL, NOUSTHRESH, NPART, PI, PRIOB, PRIVCHNGMASK, PRIVMASK, 
PROTECTSECLOG, QMIN, QUAN, RETIM, SECLOGSIZE, STEPPRIVMASK, TIMEZONE, TOTU, 
UC, UM, UTC_OFFSET, UPDLIMIT, WATCH. 
For information on the (mode) qualifier used in certain SYSTEM parameters, 
type HELP (CONTROL) MODE. 
  Parameter    Explanation 
  ANSPROT={FULL|PROTECTED|UNPROTECTED} 
               Level of ANS type protection in the system.  ANSPROT = 
               UNPROTECTED means unprotected system.  ANSPROT = SEMI means a 
               semi-protected system.  ANSPROT = FULL means a fully protected 
               system.  The default is UNPROTECTED. 
               Units: -             Minimum: -     Maximum: - 
  AUTOSHARE={ALL|NONE|RU} 
               The shareable/nonshareable character of a rununit.  That is, 
               whether the rununit is to be 1) determined by the 
               SHAREABLE/NSHAREABLE LINK option in the run units head record, 
               2) shareable, regardless of the LINK option, or 3) 
               nonshareable, regardless of the LINK option.  These three 
               choices are specified respectively by AUTOSHARE=RU, 
               AUTOSHARE=ALL, and AUTOSHARE=NONE.  The default is RU. 
               Units: -             Minimum: -     Maximum: - 
  AUTO_PRIO=n 
               The automatically shared procedure priority to be used in 
               calculating which type of unused memory to use.  (See the 
               CACHE_PRIO and the CG_PRIO parameters.)  The default is 20. 
               Units: Priounits     Minimum: 1     Maximum: 100 
  CACHE_PRIO=n 
               The I/O cache pages priority to be used in calculating which 
               type of unused memory to use.  (See the AUTO_PRIO and the 
               CG_PRIO parameters.)  The default is 10. 
               Units: Priounits     Minimum: 1     Maximum: 100 
  CG_PRIO=n 
               The comgroup pages priority to be used in calculating which 
               type of unused memory to use.  (See the AUTO_PRIO and the 
               CACHE_PRIO parameters.)  The default is 80. 
               Units: Priounits     Minimum: 1     Maximum: 100 
  CLEARMEM={YES|NO} 
               The Clear Memory parameter determines whether or not memory 
               clearing is to be performed.  YES specifies that memory 
               clearing is to be performed before memory is allocated.  Memory 
               is cleared to '----'.  NO specifies that memory clearing is not 
               to be performed.  The default is YES. 
               Unit: -              Minimum: -     Maximum: - 
  EXPTIME(type)=time 
               A relative priority to determine which granules remain in the 
               cache longest by specifying the amount of time a granule will 
               remain in the cache before it is expired.  Expired granules are 
               purged from the cache before unexpired granules.  (See the 
               UPDLIMIT parameter.) 
               type is any of the following: 
               Type       Description                        Default 
               ----       -----------                        ------- 
               CONSEC     Consecutive files                  50 
               DATA       Data granules for keyed files      50 
               FD         File Directory                     5000 
               FIT        File Information Table             1000 
               GP         Granule Pool                       10000 
               INDEX      Index granules for keyed files     100 
               MAD        Master Account Directory           5000 
               PAD        Packset Account Directory          5000 
               REL        Relative files                     50 
               UL         Upper level for keyed files        1000 
               time is an integer representing hundredths of a second. 
               Units: hundredths    Minimum: 0     Maximum: 9999999999 
                      of a second 
  FREETHRESH=n 
               A memory saturation threshold.  Memory saturation is reached 
               when the number of free pages on the system falls below this 
               value.  The default is 256 pages. 
               Units: Pages         Minimum: 0     Maximum: 1000 
  GRANSCHED={NO|YES} 
               OUTSYM (output symbiont) file priority assignment.  GRANSCHED = 
               YES means assign priorities by granule count.  GRANSCHED = NO 
               means assign priorities by submittal priority.  The default is 
               YES. 
               Units: -             Minimum: -     Maximum: - 
  HOLDEXPIRE=n 
               The time internally in hours for which the "HOLD" attribute for 
               symbiont output will be honored.  When this time runs out, 
               files being held will print.  (See M$LDEV in Monitor Services 
               Reference for a description of the HOLD attribute.)  The 
               default is 36 hours. 
               Unit:  Hours         Minimum: 0     Maximum: 511 
  IOLEAPERS=n 
               All disk i/o requests are queued in either the forward or 
               backward queue for that disk.  IOLEAPERS establishes a limit on 
               the number of queue entries that can be inserted in the queue 
               currently being processed.  Once the limit is reached, 
               additional queue entries will be inserted in the appropriate 
               spot in the waiting queue.  The default is (2**18)-1.  This 
               parameter is particularly useful on DPS 90 or DPS 8000 systems. 
               Because of the CPU speed in these systems, one user with a 
               large i/o requirement can lock out other users from disk 
               access.  In such cases, setting a low IOLEAPER limit (e.g., 5 
               or less) will even out user response.  However, be aware that 
               there is a tradeoff:  evening out user response impacts disk 
               efficiency. 
               Units: i/o requests  Minimum: 0     Maximum: (2**18)-1 
  IOTA[(mode)]=n 
               Quantum adjustment per I/O.  The IOTA value is subtracted from 
               QUAN on each I/O.  A lower value favors an I/O bound user.  The 
               defaults are 4 for each mode. 
               Units: milliseconds  Minimum: 0     Maximum: (2**35)-1 
  JOBSTATSAGE=n 
               The length of time completed job entries may remain in 
               JOBSTATS.  On the next system boot or recovery, any completed 
               job entries older than JOBSTATSAGE days old are deleted.  The 
               default is 3 days. 
               Units: days          Minimum: 1     Maximum: 511 
  LIMITU=n 
               The limit on the total number of concurrent users.  That is, 
               the total of UC(B) + UC(O) + UC(G) + UC(TP) may not exceed this 
               value.  The default is 128. 
               Units: users         Minimum: 0     Maximum: MAXU 
  LOGFILEDENY={YES|NO} 
               The Log Denied File Accesses parameter specifies whether to log 
               denied file access in the Security Log for any file on the 
               system.  YES specifies that all denied file accesses will be 
               logged.  NO specifies that no denied file accesses will be 
               logged.  The default is NO. 
               Units: -             Minimum: -     Maximum: - 
  LOGFILEGRANT={YES|NO} 
               The Log Granted File Access parameter specifies whether to log 
               granted file access in the Security Log for any file on the 
               system.  YES specifies that all granted file accesses will be 
               logged.  NO specified that no granted file accesses will be 
               logged.  Since the decision to log file accesses is only 
               available at the system level, file accesses will be logged 
               only if the user has sufficient active privileges to bypass 
               normal security checking.  The default is NO. 
               Units: -             Minimum: -     Maximum: - 
  LOGMONSER={ALL|DENIED|GRANTED|NONE} 
               The Log Monitor Services parameter indicates whether the use of 
               any monitor service specified in MONSERTBL will be logged in 
               the Security Log.  ALL specifies both granted and denied 
               attempts will be logged.  DENIED specifies only denied attempts 
               will be logged.  GRANTED specifies that only granted usage will 
               be logged.  NONE specifies that no monitor service usage will 
               be logged.  The default is NONE. 
               Unit: -              Minimum: -     Maximum: - 
  LOGPRIVCHNG={ALL|DENIED|GRANTED|NONE} 
               The Log Privilege Change parameter controls the use of 
               PRIVCHNGMASK.  LOGPRIVCHNG indicates whether requests to set 
               any privilege parameter specified in PRIVCHNGMASK will be 
               logged in the Security Log.  ALL specifies both granted and 
               denied requests will be logged.  DENIED specifies only denied 
               requests will be logged.  GRANTED specifies only granted 
               requests will be logged.  NONE specifies no privilege requests 
               will be logged.  The default is NONE.  Note that privileges 
               linked with processors run from :SYS will not cause logging to 
               occur when set active. 
               Unit: -              Minimum: -     Maximum: - 
  LOGSYSACCESS={ALL|FAILED|FAILEDPWNE|FAILEDPW|NONE} 
               The Log System Access parameter specifies which system accesses 
               or attempted accesses will be logged in the Security Log.  NONE 
               specifies that no system accesses will be logged.  FAILEDPW 
               specifies that only those accesses which fail the password 
               check will be logged.  FAILEDPWNE includes FAILEDPW and also 
               any access which specifies a possible logon which does not 
               actually exist (no entry in :HLP).  FAILED includes FAILEDPWNE 
               and any logon which was not formatted correctly.  ALL means 
               that all system accesses, successful or failed, will be logged. 
               The default is NONE. 
               Unit: -              Minimum: -     Maximum: - 
  LOGSYSEXIT={ALL|NONE} 
               The Log System Exit parameter specifies which system exits will 
               be logged in the Security Log.  ALL specifies that all system 
               exits will be logged, including those due to recovery.  NONE 
               means that no system exits will be logged.  The default is 
               NONE. 
               Unit: -              Minimum: -     Maximum: - 
  MAXACCT=n 
               The number of batch jobs from the same account that are allowed 
               to run concurrently.  The default is 511. 
               Units: jobs          Minimum: 1     Maximum: 511 
  MAXENQ=n 
               The system default for the maximum number of ENQ/DEQ requests 
               allowed to a user.  The default is overridden on an individual 
               user basis by using the SUPER MAXENQ user option.  The default 
               is 16. 
               Units: requests      Minimum: 2     Maximum: (2**18)-1 
  MAXU 
               The number of user slots.  MAXU is a display only parameter. 
               The actual maximum value is determined in the TIGR deck at 
               initialization. 
               Units: users         Minimum: -     Maximum: 511 
  MFBLK[(mode)]=n 
               The blocking point; that is, the maximum number of concurrent 
               I/Os that can occur before a user is blocked.  The defaults are 
               10 for each mode.  If MFBLK is exceeded, the user is placed in 
               the SIOMF scheduler state.  The user stays there until the 
               number of concurrent I/Os is < MFUBL. 
               Units: # IOs         Minimum: MFUBL  Maximum: 511 
  MFUBL[(mode)]=n 
               The unblocking threshold for concurrent I/Os.  The defaults are 
               4 for each mode. 
               Units: # IOs         Minimum: 0      Maximum: MFBLK 
  MONSERTBL={ALL|NONE|(monservlist)} 
               The Monitor Services Table parameter specifies a group of 
               sensitive monitor services, the use of which may be logged in 
               the Security Log.  These special services could allow ordinary 
               system security to be bypassed.  The special monitor services 
               that may be logged in the Security Log are: 
               M$BADPP         M$GOODPP         M$RUE          M$SYSCON 
               M$CVM           M$IOQ            M$SAD          M$TDCLOSE 
               M$FEBOOT        M$LIMIT          M$SCREECH      M$TDIO 
               M$FECTL         M$MADMUCK        M$SMOUSE       M$TDOPEN 
               M$FEDUMP        M$MPL            M$SMPRT        M$TDREQCPU 
               M$GBPL          M$OCMSG          M$SPRIV        M$UMPL 
               M$GETMOUSE      M$RDSYSLOG       M$SSC          M$WRSYSLOG 
               M$GETPM         M$RSPP           M$STLPP        M$XMOUSE 
               The use of MONSERTBL is determined by the value of LOGMONSER. 
               ALL specifies all monitor services listed above will be flagged 
               for possible logging.  NONE specifies no monitor services will 
               be flagged for logging.  MONSERTBL=(monser1,monser2, . . .) 
               selects from the monitor services listed above those that are 
               to be flagged for possible logging.  The default is NONE. 
               Unit: -              Minimum: -     Maximum: - 
  NOUSTHRESH=n 
               The new user threshold.  No new users are allowed when the 
               number of free pages on the system falls below this value.  The 
               default is 50 pages. 
               Units: Pages         Minimum: 0     Maximum: 1000 
  NPART=n 
               The highest-numbered partition available for scheduling: jobs 
               in partitions 1 through n are permitted to be scheduled.  The 
               default is 1. 
               Units: partitions    Minimum: 0     Maximum: 16 
  PI=n 
               The priority increment (see note) for bypassed batch jobs. 
               This parameter is relevant for batch mode only.  The default is 
               3. 
               Units: See note      Minimum: 0     Maximum: 511 
               Note:  The priority incrementation unit is 1/512 of a priority 
               advance.  For example, if PI is set to 8, each pass-over of a 
               job will advance its priority by 8/512 (i.e., 1/64); if 64 jobs 
               start before a particular job, its priority will be 1 greater. 
               The maximum priority to which a job can be incremented is 14. 
  PRIOB[(mode)]=n 
               The base execution priority.  The default is 1.  Specifying 
               PRIOB(B)=n has no effect.  This parameter is relevant for 
               non-system ghost and online mode only.  (See the PARTITION 
               parameter PPRIO.) 
               Units: Prio units,   Minimum: 0     Maximum: 511 
  PRIVCHNGMASK={ALL|NONE|(privlist)} 
               The Privilege Change Mask parameter specifies which privileges 
               (see PRIVMASK) may cause an entry to be made in the Security 
               Log when set active.  The use of PRIVCHNGMASK is determined by 
               the value of LOGPRIVCHNG.  ALL specifies that all privileges 
               will be flagged for possible logging.  NONE specifies that no 
               privileges will be flagged for logging. 
               PRIVCHNGMASK=(priv1,priv2,...) specifies a list of individual 
               privileges to be flagged for possible logging.  (See the 
               PRIVMASK parameter.)  The default is NONE. 
               Unit: -              Minimum: -     Maximum: - 
  PRIVMASK={ALL|NONE|(privlist)} 
               The Privilege Mask parameter specifies a set of privileges that 
               may normally be available but should not be set active at this 
               time. 
               ALL specifies that the use of all privileges will be 
               restricted.  NONE specifies that no usually available 
               privileges will be restricted. 
               PRIVMASK=(priv1,priv2,...) specifies a list of individual 
               privileges the use of which will be restricted.  Most of the 
               privileges that can be specified are described under the 
               PRIVILEGE and FEPPRIVILEGE options (see HELP (SUPER)) In 
               addition, the FMEFT and FMBLK privileges, which are and should 
               be used only by system processors and system ghosts (and which 
               may not be authorized via SUPER), can be specified.  FMEFT 
               privilege allows the manipulation of some areas of the FIT and 
               is necessary for certain system programs (e.g., EFT and OUTSYM) 
               to function properly.  FMBLK privilege allows special granule 
               access and is necessary for certain system programs (e.g., 
               ALTKEY and PIG) to function properly.  It will rarely be 
               advantageous to specify the FMEFT and FMBLK privileges.  In any 
               case, they should always be treated with respect and caution. 
               Only active user privileges are affected: PRC privileges (those 
               associated with processors run from :SYS that are usually set 
               active) are still allowed to be set active.  The currently 
               active privilege of a user will not be restricted as a result 
               of this parameter until the user again requests that a 
               privilege be set.  The default is NONE. 
               Units: -             Minimum: -     Maximum: - 
  PROTECTSECLOG=value 
               The Protect Security Log parameter specifies the number of days 
               (1-3650) any Security Log file (:SECLOGyymmdd.:SYS) will be 
               specially protected by file management since the time of its 
               creation.  During the interval, only the Security Logging 
               processor will be allowed to write to the file.  All others 
               will be restricted to read only status.  The default is 1 day. 
               Units: days          Minimum: 1     Maximum: 3650 
  QMIN[(mode)]=n 
               The minimum quantum.  The defaults are 60 for each mode. 
               Units: milliseconds  Minimum: 20    Maximum: (2**35)-1 
  QUAN=n 
               The quantum time.  The default is 200. 
               Units: milliseconds  Minimum: 20    Maximum: (2**35)-1 
  RETIM=n 
               The time after line disconnect during which the user's image 
               will be saved.  The default is 900. 
               Units: seconds       Minimum: 0     Maximum: (2**35)-1 
  SECLOGSIZE=n 
               A number of granules to which the current :SECLOGyymmdd may 
               grow before it is closed as :SECLOGyymmddhhmmss. 
               Setting SECLOGSIZE provides a way to alert the operator that 
               unusual numbers of security log entries have been generated. 
               The operator is notified when this limit is exceeded by the 
               message: 
                   :SECLOG size limit reached - automatic turnover performed. 
               The default is 262143. 
               Unit: granules       Minimum: 10    Maximum: 262143 
  STEPPRIVMASK={ALL|NONE|(privlist)} 
               The Step Privilege Mask parameter specifies a set of privileges 
               (see PRIVMASK) to be reset at job step termination.  ALL 
               specifies that all active privileges will be reset.  NONE 
               specifies that no active privileges will be reset. 
               STEPPRIVMASK=(priv1,priv2,...)  specifies a list of individual 
               privileges to be reset.  (See the PRIVMASK parameter.)  The 
               default is NONE. 
               Units: -             Minimum: -     Maximum: - 
  TIMEZONE={acronym|offset [acronym]} 
               The TIMEZONE parameter specifies the current local time zone in 
               effect at the location of the CP-6 system.  If a time zone 
               acronym is to be specified, it must be one of the acronyms 
               understood by the library routine XST$TIMEZONE (i.e. one of 
               CDT, CST, EDT, EST, GMT, MDT, MST, PDT, PST, or UTC). 
               Otherwise, the time zone must be specified as an offset from 
               UTC expressed as shhmm, where s indicates a sign, hh a number 
               of hours, and mm a number of minutes.  If an offset is 
               specified, it may optionally be followed by a blank and up to 
               four characters to specify a site-defined time zone acronym; if 
               the acronym is left off, the acronym field is left as blank. 
               Whenever the TIMEZONE parameter is updated, the UTC_OFFSET 
               parameter is also internally updated.  The default for acronym 
               is four blanks. 
               Units: -             Minimum: -     Maximum: - 
  TOTU 
               The total users regardless of mode.  TOTU is a display only 
               parameter. 
               Units: users         Minimum: -     Maximum: - 
  UC[(mode)] 
               The current users by mode.  UC is a display only parameter. 
               Units: users         Minimum: -     Maximum: - 
  UM[(mode)]=n 
               The maximum number of users, for each mode.  The defaults are 0 
               (batch users), 32 (ghost users), 32 (on-line users), and 0 (TP 
               users). 
               Units: users         Minimum: 0     Maximum: MAXU 
  UPDLIMIT(type)=limit 
               A limit on the number of times a granule will be updated before 
               it is written to disk.  This parameter applies only to granules 
               that have multiple users, such as in the case of shared files. 
               Granules are automatically written to disk if they have no 
               associated users.  (Refer to the EXPTIME parameter.) 
               type is only the following: 
               Type    Description                       Default 
               ----    -----------                       ------- 
               DATA    Data granules for key files       0 
               INDEX   Index granules for keyed files    0 
               REL     Relative files                    0 
               limit is an integer representing the number of times a granule 
               can be dated. 
               Units: occurrences   Minimum: 0     Maximum: 9999999999 
  UTC_OFFSET 
               The time difference between the current local time zone and UTC 
               (Coordinated Universal Time, formerly known as GMT), expressed 
               as a signed integer.  UTC_OFFSET is a display only parameter, 
               but is updated internally whenever TIMEZONE is updated.  The 
               default is 0. 
               Units: centiseconds  Minimum: -     Maximum: - 
  WATCH={NO|YES} 
               Device control message printing control parameter.  YES 
               specifies that a message is to be printed on the device console 
               when output of a symbiont file starts or stops.  NO suppresses 
               this printing.  The default is NO. 
               Units: -             Minimum: -     Maximum: - 
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
00030
00031
00032
00033
00034
00035
00036
00037
00038
00039
00040
00041
00042
00043
00044
00045
A list of TP parameters and their definitions can be accessed by typing a ? or 
a ??.  To obtain definitions of individual parameters, type 
HELP (CONTROL) TP_PARAMS param 
where param is MAXTPU or TPI 
  Parameter      Explanation 
  MAXTPU[(instance_name)]=n 
                 The maximum number of TP users per instance.  If 
                 instance_name is not specified, MAXTPU is set to the value 
                 specified for all instances of TP currently on the system. 
                 If MAXTPU is not specified, the default number of instances 
                 is 49. 
                 Units: TP Users        Minimum: 0     Maximum: (2**35)-1 
  TPHE[ADER] [(instance_name)]=message 
                 A message that is to be displayed when a user logs on to the 
                 instance of TP called instance_name.  If the instance name is 
                 not specified, TPHEADER is set to the message specified for 
                 all instances of TP currently defined.  If no message is 
                 specified the current message is deleted.  The maximum length 
                 of the message is 80 characters. 
                 Units: -               Minimum: -     Maximum: - 
  TPI[NSTANCE]=instance_name 
                 The name of an instance of TP on the system.  instance_name 
                 is limited to eight alphanumeric characters. 
                 Units: -               Minimum: -     Maximum: - 
00001
00002
00003
INVOKING_CONTROL
