RATES and SUPER are the two processors through which the system manager 
controls the accounting process.  RATES defines the charges for 
o   System resources such as 
    CPU time 
    Connect time 
    Memory pages 
    Tape drives 
    Service requests 
    Installation-defined transactions, etc. 
o   Forms mounting and media consumed by the user. 
These charges are stored in the RATE and FORM tables, respectively. 
For each RATE table containing user resource charges, the system manager also 
defines one or more SCHEDULE or PROCESSOR tables to be used to reference the 
RATE table. 
An LCP-6 RATE table and a (host) RATE table with the same name are in fact the 
same table sharing values for all identical options.  In addition, the LCP-6 
option, MCLS, shares a value with the PMMES option, and the LCP-6 option, 
HACCESS, shares a value with the OACCESS option.  (The LCP-6 option, 
INTERRUPTS, has no host counterpart.  All the other LCP-6 options have exact 
host duplicates.) 
To obtain more HELP information, see 
HELP (RATES) TOPICS               Displays available topics. 
HELP (RATES) COMMANDS             Displays list of RATES commands. 
HELP (RATES) command PARAM        Displays parameters associated 
                                  with a particular command. 
HELP (RATES) command DESCRIPTION  Displays description associated 
                                  with a particular command. 
?                                 Displays next level of HELP. 
??                                Displays all levels of HELP 
                                  messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
Format: 
                                 {base     } 
B[UILD] F[ORM] {name     } [FROM {SCR[ATCH]}] 
               {DEF[AULT]}       {DEF[AULT]} 
Parameters: 
name    is the name of the form table to be built, and may be up to 6 
characters long. 
DEFAULT    refers to the table is the default form table.  The name of the 
default table is 0. 
base    is the name of the base table. 
SCRATCH    indicates that the table is to be built from scratch. 
Description: 
The BUILD FORM command creates a FORM table containing charges to be applied 
for forms mounting and usage.  The user may specify that the table be created 
from scratch or as a modification of an already existing base table.  If the 
base is not specified, the table is created from scratch.  If created from 
scratch, the table is initialized with zeros, then loaded with the data 
specified with options to this command.  To access these BUILD FORM command 
options, type HELP (RATES) BUILD_FORM_OPTS. 
00002
00001
BUILD_FORM_OPTS
A list of BUILD FORM command options can be accessed by typing a ? or a ??. 
To access individual options, type 
HELP (RATES) BUILD_FORM_OPTS option 
where option is FORM or FMOUNT. 
  Option         Description 
  FO[RM]=value 
                 value is the charge per form (page or card). 
  FM[OUNT]=value 
                 value is the charge for mounting the form. 
00002
00001
Format: 
               {name     } [, {P[ERCENT]}] [     {base     }] 
B[UILD] L[CP6] {DEF[AULT]} [, {%        }] [FROM {SCR[ATCH]}] 
                                           [     {DEF[AULT]}] 
Parameters: 
name    is the name of the RATE table to be built, and may be up to 6 
characters long. 
DEFAULT    indicates that the table is the default rate table.  The name of 
the default table is 0. 
PERCENT or %    indicates that the rate table will contain percentage values 
to be used for processor charging.  This type of table enables an installation 
to establish a surcharge for processor usage. 
base    is the name of the base table. 
SCRATCH    indicates that the table is to be built from scratch. 
Description: 
The BUILD LCP-6 command creates a RATE table containing cost multipliers 
applied to accumulated system service usage data.  The user may specify that 
the table be created from scratch or be created as a modification of an 
already existing base table.  If the base is not specified, the table is 
created from scratch.  If created from scratch, the table is initialized with 
zeroes and then loaded with the data specified with options to this command. 
To access these BUILD LCP-6 command options, type HELP (RATES) BUILD_LCP6_OPTS 
00002
00001
BUILD_LCP6_OPTS
A list of BUILD LCP-6 command options can be accessed by typing a ? or a ??. 
To access individual options, type 
HELP (RATES) BUILD_LCP6_OPTS option 
where option is CMULTIPLIER, CONNECT, HACCESS, INTERRUPTS, JSTEPS, JUNIT, 
MCLS, PEXECUTION, PMEMORY, PSTIME, SUNIT, TINTERACTION, UEXECUTION, UMEMORY, 
and USTIME. 
  Option         Description 
  CM[ULTIPLIER]=value 
                 value    is a charge multiplier applied to charge units 
                 before being output to the user or accounting record. 
  CO[NNECT]=value 
                 value    specifies a charge per clock minute of connect time 
                 for LCP-6 users. 
  H[ACCESS]=value 
                 value    specifies a charge per host access. 
  I[NTERRUPTS]=value 
                 value    specifies a charge per connected interrupt level. 
  J[STEPS]=value 
                 value    specifies a charge per job-step. 
  J[UNIT]n[=value][, name] 
                 n    specifies the number of the job-unit for which a value 
                 from 1 to 4 is specified. 
                 value    is a charge associated with the word n of job-unit 
                 charges in the LCP-6 user's JIT. 
                 name    specifies an installation name associated with 
                 job-unit n and may be up to sixteen characters in length. 
                 Note:  JUNIT may be used by site-specific FPRGs.  Some CP-6 
                 products may also make use of JUNIT.  The programs define the 
                 transaction internally and use monitor service requests 
                 (M$CHGUNIT) to increment the counters.  Programs utilizing 
                 the transaction counters should be execute-only run units to 
                 prevent circumvention by DELTA or other means. 
  M[CLS]=value 
                 value    specifies a charge per monitor service call, MCL. 
  PE[XECUTION]=value 
                 value    specifies a charge per minute of processor execution 
                 (CPU) time. 
  PM[EMORY]=value 
                 value    specifies a charge per CPU page-minute of processor 
                 memory. 
  PS[TIME]=value 
                 value    specifies a charge per minute of monitor service 
                 (CPU) time for processors. 
  S[UNIT]n[=value][, name] 
                 n    specifies the number of the step-unit for which a value 
                 1 to 4 is specified. 
                 value    is a charge associated with the word n of step-unit 
                 charges in the LCP-6 user's JIT. 
                 name    specifies an installation name associated with 
                 step-unit n and may be up to 16 characters in length. 
                 Note:  SUNIT may be used by site-specific programs.  Some 
                 CP-6 products may also make use of SUNIT.  The programs 
                 define the transaction internally and use monitor service 
                 requests (M$CHGUNIT) to increment the counters.  Programs 
                 utilizing the transaction counters should be execute-only run 
                 units to prevent circumvention by DELTA or other means. 
  T[INTERACTION]=value 
                 value    specifies a charge per terminal access. 
  UE[XECUTION]=value 
                 value    specifies a charge per minute of user execution 
                 (CPU) time. 
  UM[EMORY]=value 
                 value    specifies a charge per CPU page-minute of user 
                 memory. 
  US[TIME]=value 
                 value    specifies a charge per minute of monitor service 
                 (CPU) time for users. 
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
Format: 
                                       {base     } 
B[UILD] P[ROCESSOR] {name     } [FROM  {SCR[ATCH]} ] 
                    {DEF[AULT]}        {DEF[AULT]} 
Parameters: 
name    is the name of the processor table to be built, and may be up to 31 
characters long.  This is the name which corresponds to a processor for which 
proprietary accounting is to be performed. 
DEFAULT    indicates that the table is the default processor table.  The name 
of the default processor table is 0. 
base    is the name of the processor table to be used as a base. 
SCRATCH    indicates that the table is to be built from scratch. 
Description: 
This command creates a table indicating which rate table should be applied for 
additional charges for using a given processor.  The user may specify that the 
table be created from scratch or as a modification of an already existing base 
table.  If the base is not specified, the table is created from scratch.  If 
created from scratch, the table is initialized to point to the default RATE 
table (0), and is then loaded with the data specified with options to this 
command. 
The options that may be appended to the BUILD PROCESSOR command, after the 
double-dash prompt, are: 
I[NFO]n=info 
where n is 1-3, and info is a 1-16 character informational string (used for 
any purpose). 
R[TABLE]=name 
where name specifies the rate table to which this processor table points.  Up 
to 6 characters are permitted. 
00002
00001
Format: 
               {name     } [, {P[ERCENT]}] [     {base     }] 
B[UILD] R[ATE] {DEF[AULT]} [, {%        }] [FROM {SCR[ATCH]}] 
                                           [     {DEF[AULT]}] 
Parameters: 
name    is the name of the rate table to be built, and may be up to 6 
characters long. 
DEFAULT    indicates that the table is the default rate table.  The name of 
the default table is 0. 
PERCENT or %    indicates that the rate table will contain percentage values 
to be used for processor charging.  This type of table enables an installation 
to establish a surcharge for processor usage. 
base    is the name of the base table. 
SCRATCH    indicates that the table is to be built from scratch. 
Description: 
The BUILD RATE command creates a rate table containing cost multipliers 
applied to accumulated system service usage data.  The user may specify that 
the table be created from scratch or be created as a modification of an 
already existing base table.  If the base is not specified, the table is 
created from scratch.  If created from scratch, the table is initialized with 
zeros and then loaded with the data specified with options to this command. 
To access these BUILD RATE command options, type HELP (RATES) BUILD_RATE_OPTS. 
00002
00001
BUILD_RATE_OPTS
To list BUILD RATE command options and their definitions, type a ? or a ??. 
To list individual options, type 
HELP (RATES) BUILD_RATE_OPTS option 
where option may be one of the following: 
CMULTIPLIER, CONNECT, FACCESS, FCLOCK, FCPU, FMOUNT, HACCESS, INTERRUPTS, 
JSTEPS, JUNIT, MCLS, OACCESS, OCLOCK, OCPU, OMOUNT, PEXECUTION, PMEMORY, 
PMMES, PSTIME, SUNIT, TACCESS, TCLOCK, TCPU, TINTERACTIONS, TMOUNT, TPACK, 
UEXECUTION, UMEMORY, USTIME. 
  Option         Description 
  CM[ULTIPLIER]=value 
                 value is a charge multiplier applied to charge units before 
                 being output to the user or accounting record. 
  CO[NNECT]=value 
                 value specifies a charge per clock minute of connect time for 
                 on-line users. 
  FA[CCESS]=value 
                 value specifies a charge per file access. 
  FCL[OCK]=value 
                 value specifies a charge per clock resource-minute for 
                 allocated disk spindles. 
  FCP[U]=value 
                 value specifies a charge per CPU resource-minute for 
                 allocated (private) disk spindles. 
  FM[OUNT]=value 
                 value specifies a charge per (private) disk pack mount. 
  H[ACCESS]=value 
                 value specifies a charge per host access.  IF OACCESS is 
                 specified also, the last specified of the two options will 
                 set the rate for both. 
  I[NTERRUPTS]=value 
                 value specifies a charge per connected interrupt level.  This 
                 option is meaningful only when the table is used for FEP 
                 accounting. 
  J[STEPS]=value 
                 value specifies a charge per job-step. 
  J[UNIT]n[=value][, name] 
                 n specifies the number of the job-unit for which a value from 
                 1 to 4 is specified. 
                 value is a charge associated with the word n of job-unit 
                 charges in the JIT. 
                 name specifies an installation name associated with job-unit 
                 n and may be up to sixteen characters in length.  The name 
                 will appear in the accounting record and on the printed 
                 accounting log for the job. 
                 Note:  JUNIT may be used by site-specific programs.  Some 
                 CP-6 products may also make use of JUNIT.  The programs 
                 define the transaction internally and use monitor service 
                 requests (M$CHGUNIT) to increment the counters.  Programs 
                 utilizing the transaction counters should be execute-only run 
                 units to prevent circumvention by DELTA or other means. 
  M[CLS]=value 
                 value specifies a charge per monitor service call (MCL).  If 
                 PMMES is specified also, the last specified of the two 
                 options will set the value for both. 
  OA[CCESS]=value 
                 value specifies a charge per non-tape, non-file access.  If 
                 HACCESS is specified also, the last specified of the two 
                 options will set the value for both. 
  OCL[OCK]=value 
                 value specifies a charge per clock resource-minute for 
                 allocated non-disk, non-tape resources. 
  OCP[U]=value 
                 value specifies a charge per CPU resource-minute for 
                 allocated non-disk, non-tape resources. 
  OM[OUNT]=value 
                 value specifies a charge per non-pack, non-tape mount. 
  PE[XECUTION]=value 
                 value specifies a charge per minute of processor execution 
                 (CPU) time for shared processors. 
  PM[EMORY]=value 
                 value specifies a charge per CPU page-minute of processor 
                 memory. 
  PMM[ES]=value 
                 value specifies a charge per monitor service call, PMME.  If 
                 MCLS is specified also, the last specified of the two options 
                 will set the value for both. 
  PS[TIME]=value 
                 value specifies a charge per minute of monitor service (CPU) 
                 time for shared processors. 
  S[UNIT]n[=value][, name] 
                 n specifies the number of the step-unit for which a value 1 
                 to 4 is specified. 
                 value is a charge associated with the word n of step-unit 
                 charges in the JIT. 
                 name specifies an installation name associated with step-unit 
                 n and may be up to 16 characters in length.  The name will 
                 appear in the step or proprietary accounting record and on 
                 the printed accounting log if step reporting is specified. 
                 Note:  SUNIT may be used by site-specific programs.  Some 
                 CP-6 products may also make use of SUNIT.  The programs 
                 define the transaction internally and use monitor service 
                 requests (M$CHGUNIT) to increment the counters.  Programs 
                 utilizing the transaction counters should be execute-only run 
                 units to prevent circumvention by DELTA or other means. 
  TA[CCESS]=value 
                 value specifies a charge per tape access. 
  TCL[OCK]=value 
                 value specifies a charge per clock resource-minute for tape 
                 drives. 
  TCP[U]=value 
                 value specifies a charge per CPU resource-minute for 
                 allocated tape drives. 
  TI[NTERACTIONS]=value 
                 value specifies a charge per terminal interaction. 
  TM[OUNT]=value 
                 value specifies a charge per tape mount. 
  TP[ACK]=value 
                 value specifies a charge per clock page-minute of temporary 
                 disk pack storage. 
  UE[XECUTION]=value 
                 value specifies a charge per minute of user execution (CPU) 
                 time. 
  UM[EMORY]=value 
                 value specifies a charge per CPU page-minute of user memory. 
  US[TIME]=value 
                 value specifies a charge per minute of monitor service (CPU) 
                 time for other than shared processors. 
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
00005
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
Format: 
                                      {base     } 
B[UILD] S[CHEDULE] {name     } [FROM  {SCR[ATCH]} ] 
                   {DEF[AULT]}        {DEF[AULT]} 
Parameters: 
name    is the name of the schedule table to be built, and may be up to six 
characters long.  This is the name which corresponds to the BILLING fields 
specified for a user in SUPER. 
DEFAULT    indicates that the table is the default schedule table.  The name 
of the default is 0. 
base    is the name of the schedule table to be used as a base. 
SCRATCH    indicates that the table is to be built from scratch. 
Description: 
The BUILD SCHEDULE command creates a table indicating which rate table should 
be applied for charges incurred by a given user.  The user may specify that 
the table be created from scratch or as a modification of an already existing 
base table.  If the base is not specified, the table is created from scratch. 
If created from scratch, the table is initialized to point to the default RATE 
table (0) and is then loaded with the data specified with options to this 
command. 
The options that may be appended to the BUILD SCHEDULE command, after the 
double-dash prompt, are: 
I[NFO]n=info 
where n is 1-3, and info is a 1-6 character informational string (used for any 
purpose). 
R[TABLE]=name 
where name specifies the rate table to which this schedule table points.  Up 
to six characters are permitted. 
00002
00001
BUILD_FORM
BUILD_LCP6
BUILD_PROCESSOR
BUILD_RATE
BUILD_SCHEDULE
To list RATES commands and their definitions, type a ? or a ??.  To list 
individual commands, type 
HELP (RATES) COMMANDS command 
where command is any of the following: 
BUILD_FORM, BUILD_LCP6, BUILD_PROCESSOR, BUILD_RATE, BUILD_SCHEDULE, DELETE, 
END, HELP, LIST, and MODIFY. 
  Command        Description 
  BUILD FORM 
                 Creates a table containing charges to be applied for forms 
                 mounting and usage. 
  BUILD LCP6 
                 Creates a LCP-6 rate table containing cost multipliers 
                 applied to accumulated FEP system service usage data. 
  BUILD PROCESSOR 
                 Creates a table indicating which rate table should be applied 
                 for additional charges for using a given processor. 
  BUILD RATE 
                 Creates a table containing cost multipliers applied to 
                 accumulated host system service usage data. 
  BUILD SCHEDULE 
                 Creates a table indicating which rate table should be applied 
                 for charges incurred by a given user. 
  {DATE|TIME} 
                 Displays the current time and date. 
  DELETE 
                 Deletes the specified table(s). 
  {DIRECTORY|DIR} 
                 Changes the default account and packset. 
  {DO|!} 
                 Enables IBEX command execution. 
  {END|EXIT|QUIT} 
                 Terminates the RATES processor. 
  ENTER 
                 Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
                 Deletes accumulated output for logical devices. 
  HELP 
                 Provides  information about RATES and other processors. 
  LIST 
                 Lists the specified tables. 
  MODIFY 
                 Modifies an existing rate, schedule, processor or forms 
                 table. 
  OUTPUT 
                 Directs processor output to a destination. 
  PRINT 
                 Directs that output accumulated for logical devices be sent 
                 to destinations immediately. 
Any RATE/LCP-6 table can be listed, deleted, or modified, individually as 
either a RATE or LCP-6 table.  Note that: 
o   The LIST ALL command will only list tables created in the same mode (RATE 
    or LCP-6) as the LIST command specifies. 
o   The DELETE ALL command deletes all RATE/LCP-6 tables, regardless of their 
    creation mode or the command mode. 
Also, when BUILD and MODIFY operations are performed on a (Host) RATE table, 
all options, even the three that pertain only to FEP accounting, may be 
specified.  However, the value for INTERRUPTS is only displayed when the table 
is listed as an LCP-6 table. 
00009
00001
00002
00003
00004
00005
00001
00002
00003
00004
00005
00007
00006
00007
00008
00009
00010
00011
00012
00010
00013
00014
00015
00016
00017
00010
00006
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm (month)(day)(year)(hours)(minutes) 
Examples: 
-DATE 
requests a display of the current date and time.  A sample display is: 
AUG 02  '88  11:03 
00001
00002
Format: 
         {A[LL]      } 
         {F[ORM]     } {ALL      } 
DEL[ETE] {L[CP6]     } {name     } 
         {P[ROCESSOR]} {DEF[AULT]} 
         {R[ATE]     } 
         {S[CHEDULE] } 
Parameters: 
ALL    denotes that all tables or all tables of a specified type are to be 
deleted. 
FORM, LCP-6, PROCESSOR, RATE, and SCHEDULE    denote the table or tables to be 
deleted. 
name    is the name of the table to be deleted. 
DEFAULT    indicates that the DEFAULT table of the specified type is to be 
deleted. 
Description: 
The DELETE command instructs the system to delete the specified table or 
tables. 
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
{DO|!} IBEX-command 
Parameters: 
IBEX-command    any legal IBEX command.  (See the CP-6 Programmer Reference 
Manual (CE40).) 
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
{E[ND]|E[XIT]|Q[UIT]} 
Description: 
The END command (or its synonyms EXIT or QUIT) instructs the system to 
terminate the RATES processor and return control to the command processor. 
Before returning control to the command processor, RATES checks the tables 
defined for internal consistency; two conditions will be reported: 
o   Schedule tables and processor tables which reference a non-existent rate 
    table will be displayed. 
o   Rate tables which are not referenced by a schedule table or processor 
    table will be displayed. 
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
B 
  BUILD FORM Command - 
      HELP BUILD_FORM 
  BUILD LCP-6 Command - 
      HELP BUILD_LCP6 
  BUILD PROCESSOR Command - 
      HELP BUILD_PROCESSOR 
  BUILD RATE Command - 
      HELP BUILD_RATE 
  BUILD SCHEDULE Command - 
      HELP BUILD_SCHEDULE 
D 
  DATE Command - 
      HELP DATE 
  DELETE Command -   
    RATES - 
      HELP DELETE FORMAT: 
  DELETE Command - 
      HELP DELETE 
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
F 
  Files Created by RATES - 
      HELP RELATED_FILES 
H 
  HELP Command - 
      HELP HELP 
I 
  Invoking RATES - 
      HELP INVOKING_RATES 
J 
  JUNIT - 
      HELP BUILD_RATE_OPTS JUNIT 
L 
  LIST Command -   
    RATES - 
      HELP LIST FORMAT: 
  LIST Command - 
      HELP LIST 
M 
  MODIFY Command -   
    RATES - 
      HELP MODIFY FORMAT: 
  MODIFY Command - 
      HELP MODIFY 
O 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PRINT Command - 
      HELP PRINT 
  Privileges for Use of RATES - 
      HELP PRIVILEGES 
  Proprietary Accounting - 
      HELP PROPRIETARY_ACCOUNTING 
R 
  RATES -   
    BUILD FORM Command - 
      HELP BUILD_FORM FORMAT: 
    BUILD PROCESSOR Command - 
      HELP BUILD_PROCESSOR FORMAT: 
    BUILD RATE Command - 
      HELP BUILD_RATE FORMAT: 
    BUILD SCHEDULE Command - 
      HELP BUILD_SCHEDULE FORMAT: 
    DELETE Command - 
      HELP DELETE FORMAT: 
    DIRECTORY Command - 
      HELP DIRECTORY FORMAT: 
    DO Command - 
      HELP DO FORMAT: 
    END Command - 
      HELP END FORMAT: 
    ERASE Command - 
      HELP ERASE FORMAT: 
    EXIT Command - 
      HELP END FORMAT: 
    HELP Command - 
      HELP HELP FORMAT: 
    LIST Command - 
      HELP LIST FORMAT: 
    MODIFY Command - 
      HELP MODIFY FORMAT: 
    QUIT Command - 
      HELP END FORMAT: 
S 
  SUNIT - 
      HELP BUILD_RATE_OPTS SUNIT 
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
The RATES processor may be executed on-line, in batch, or as a GHOST.  When 
executed on-line, RATES prompts for a command by typing a single dash (-). 
Options for RATES are entered following the options prompt which is a double 
dash (--).  Each option is followed by an equal sign(=) and the value that is 
to appear in the record.  An END command must be entered after the double-dash 
prompt to terminate options processing. 
Example: 
!RATES 
-command 
--options 
--END 
-END 
00001
Format: 
       {A[LL]      } 
       {F[ORM]     } {ALL      } 
L[IST] {L[CP6]     } {name     } 
       {P[ROCESSOR]} {DEF[AULT]} 
       {R[ATE]     } 
       {S[CHEDULE] } 
Parameters: 
ALL    denotes that all tables or all tables of a specified type are to be 
listed. 
FORM, LCP-6, PROCESSOR, RATE, and SCHEDULE    denote the table or tables to be 
listed. 
name    is the name of the table to be listed. 
DEFAULT    indicates that the DEFAULT table of the specified type is to be 
listed. 
Description: 
The LIST command instructs the system to list the specified table or tables. 
00002
00001
Format: 
         {F[ORM]     } 
         {L[CP6]     } {name     } 
M[ODIFY] {P[ROCESSOR]} {DEF[AULT]} 
         {R[ATE]     } 
         {S[CHEDULE] } 
Parameters: 
FORM, LCP-6, PROCESSOR, RATE, and SCHEDULE    denote the table or tables to be 
modified. 
name    is the name of the table to be modified. 
DEFAULT    indicates that the default table is to be modified. 
Description: 
The MODIFY command instructs the system to modify an existing table in 
accordance with the data supplied in MODIFY options. 
The options that may be appended to the MODIFY command, after the double-dash 
prompt, are the same as those for the BUILD command. 
00002
00001
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
printer. 
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
-PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
00002
00003
00001
Use of RATES requires that the user have the RATES processor privilege or the 
FMSEC privilege. 
The proprietary accounting process is similar to the process for charging 
users.  PROCESSOR tables are defined for processors for which proprietary 
accounting is to be performed.  Instead of building a SCHEDULE table which in 
turn points to a RATE table, a PROCESSOR table is built which in turn points 
to a RATE table.  The items which may be charged for are the same as for 
users.  Proprietary accounting is performed only for software which has 
proprietary accounting turned on.  This can be established when a program is 
created, via the SURCHARGE option of the LINK command, or by the system 
manager via the CONTROL processor. 
END
RATES maintains tables for accounting control in a file called :RATES in the 
system account.  This file is accessed by command processors in order to do 
accounting. 
DATE
