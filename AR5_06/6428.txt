The PIGETTE processor is used to: 
o   create bootstrap diskettes for remote Front End Processors (FEP) connected 
    to a CP-6 host.  This is the primary purpose of PIGETTE. 
o   transfer data from a diskette to a keyed file on the CP-6 host. 
To obtain more HELP information, see: 
HELP (PIGETTE) TOPICS         Displays available topics. 
HELP (PIGETTE) COMMANDS       Displays a list of commands. 
HELP (PIGETTE) command PARAM  Displays parameters associated 
                              with a particular command. 
HELP (PIGETTE) command DESC   Displays a description 
                              associated with a particular 
                              command. 
?                             Displays next level of HELP 
                              messages. 
??                            Displays all levels of HELP 
                              messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
Format: 
            [{ON  }                         ] 
BU[ILD] id1 [{OVER} {F[EP] } id2 [D[RIVE] m]] 
            [{INTO} {N[ODE]}                ] 
            [{TO  }                         ] 
Parameters: 
id1    specifies the node number or name of the remote FEP that will 
eventually receive the boot diskette. 
id2    specifies the node number or name of the FEP that will be used to 
create the boot diskette.  The FEP can be local or remote.  The default is the 
FEP and DRIVE last accessed by this PIGETTE session. 
m    specifies the diskette drive (0-3) loaded with the diskette on which the 
boot image is built.  If no drive is specified, drive 0 is used.  Drive 0 is 
the lowest addressed diskette drive and is usually at X'400' for remote FEPs. 
Drive 1 is the next highest diskette drive.  Drive 0 is standard on CP-6 FEPs; 
drive 1-3 are optional. 
Description: 
This command creates a boot image for a remote FEP.  Note that PIGETTE builds 
a boot image based on information contained in the :NETCON file 
Usage Notes: 
To create a boot image for a remote FEP: 
o   The NETCON processor DEFINE command must be used first to define the 
    remote FEP. 
o   The PIGETTE processor is then invoked.  When it is, the VOLINIT command 
    must be used first to initialize the boot diskette. 
o   Then, the PIGETTE processor BUILD command can be used to build the boot 
    image on the diskette. 
Examples: 
Oink:VOLINIT FEP 1 DRIVE 1 (TYPE=RFEP) 
Oink:BUILD 12 OVER FEP 1 DRIVE 1 
These commands load and initialize a diskette in drive 1 of FEP 1, and create 
a boot diskette that will eventually be used in FEP 12. 
00002
00004
00001
00003
Format: 
CERTIFY {F[EP] } id [D[RIVE] m] [(TY[PE]=typecode|option[,option]...)] 
        {N[ODE]} 
Parameters: 
id    specifies the node number or name of the FEP on which the diskette is 
loaded. 
m    specifies the diskette drive (0-3) loaded with the diskette that is to be 
certified.  If no drive is specified, drive 0 is used.  Drive 0 is the lowest 
addressed diskette drive and is usually at X'400' for remote FEPs.  Drive 1 is 
the next highest diskette drive.  Drive 0 is standard on CP-6 FEPs; drives 1-3 
are optional.  The CHECK command can be used to determine the actual 
configuration. 
typecode    specifies a code (see HELP (PIGETTE) TYPECODE_PARAMETER) that 
identifies a default set of diskette parameters that are to be used.  The 
default is RFEP. 
option    specifies one of the following: 
  Option                   Description                            Default 
SE[CTORS] [=] n[-m]      Specifies the sector ID number(s)      0-15 
                         to be VOLINITed on to the disk. 
SI[DES] [=] n[-m]        Specifies which side (0-1) of a        0-1 
                         double-sided diskette is to be 
                         VOLINITed (n-m specifies both). 
SS[IZE] [=] n            Indicates the size (in bytes)          256 
                         of each sector on the diskette. 
                         Either 128 or 256 may be 
                         specified. 
TR[ACKS] [=] n[-m]       Specifies the number(s) of the         0-79 
                         track(s) to be VOLINITed. 
Description: 
This command initializes and tests a diskette.  CERTIFY performs a 
considerable amount of writing and reading of the diskette to obtain an 
indication of the quality of the diskette surface. 
Example: 
Oink:CERTIFY NODE 2 DRIVE 1 (MSSSD) 
This command initializes and tests the single-sided, single-density, mini 
diskette loaded in drive 1 of node 2. 
00002
00003
00001
Format: 
CH[ECK] [{F[EP] } id] 
       [{N[ODE]}   ] 
Parameters: 
id    specifies the node number or name of the FEP to be checked.  The default 
is the last one used. 
Description: 
This command displays the type and status of the drives in the indicated or 
last used FEP. 
00002
00001
Format: 
CL[ONE] {F[EP] } id [D[RIVE] m1] [(TY[PE]=typecode|option[,option] ...)] 
        {N[ODE]} 
     {TO|ON|OVER|INTO} D[RIVE] m2 
Parameters: 
id    specifies the node number or name of the FEP on which the diskette is 
loaded. 
m1    specifies the diskette drive (0-3) loaded with the diskette that is to 
be cloned.  If no drive is specified, drive 0 is used.  Drive 0 is the lowest 
addressed diskette drive and is usually at X'400' for remote FEPs.  Drive 1 is 
the next highest diskette drive.  Drive 0 is standard on CP-6 FEPs; drive 1-3 
are optional. 
typecode    specifies a code (see HELP (PIGETTE) TYPECODE_PARAMETER) that 
identifies a default set of diskette parameters that are to be used. 
option    specifies one of the options listed in the following table. 
m2    specifies the number of the drive in which the destination diskette is 
loaded. 
  Option                          Description                   Default 
AN[NOUNCE] [=] n                Specifies that a message      None 
                                is to be sent when the 
                                operation is n% 
                                complete. 
DIAGNOSTIC                      Specifies that actual         None 
                                diskette I/O is to be 
                                done in diagnostic 
                                mode. 
SE[CTORS] [=] n[-m]             Specifies the number(s)       1-26 
                                of the sector(s) to be 
                                copied. 
SI[DES] [=] n[-m]               Specifies which side (0       0 
                                or 1) of double-sided 
                                diskette is to be used 
                                (n-m specifies both). 
SS[IZE] [=] n                   Indicates the size            128 
                                (in bytes) of each sector 
                                on the diskette.  Either 
                                128 or 256 may be 
                                specified. 
TR[ACKS] [=] n[-m]              Specifies the number(s)       0-76 
                                of the track(s) to be 
                                copied. 
VS[ECTOR] [=] n[-m]             Specifies the logical         1-diskette 
                                sector numbers (1-disk-       size 
                                ette size) of the portion 
                                to be copied. 
WAIT                            Specifies wait for            None 
                                conformation before 
                                proceeding. 
     {ALL                 }     Specifies whether to          ALL 
WARN {DISK[ETTE]          }     report errors accessing 
     {NONE                }     the data. 
     {V[IRTUAL] D[ISKETTE]} 
Description: 
This command performs a sector-by-sector copy from one diskette to another one 
in the same FEP.  Use of the CLONE command requires two identical drives in 
the FEP.  The CLONE command copy operation is considerably faster than the 
copy operations performed by the BUILD and MOVE commands, since the CLONE copy 
operation is performed entirely in the FEP. 
Example: 
Oink:CL NODE 2 DR 1 TO D O 
copies all the information of FEP 2, drive 1 to an identical diskette on drive 
0. 
00002
00003
00001
The PIGETTE commands are:  BUILD, CERTIFY, CHECK, CLONE, DATE, DIRECTORY, DO, 
DUMP, END, ENTER, ERASE, EXIT, HELP, LIST, MOVE, OUTPUT, PRINT, QUIT, TIME, 
USE and VOLINIT. 
For a one-line summary of these commands, enter: ?. 
For complete HELP for each command, enter: 
HELP (PIGETTE) command. 
  Command     Description 
BUILD       Create a boot-image for a remote FEP. 
CERTIFY     Performs exhaustive surface test of a diskette. 
CHECK       Displays drive types and status. 
CLONE       Duplicates a diskette (requires 2 identical drives in 
            one FEP). 
{DATE|TIME} Displays the current time and data. 
{DIRECTORY|DIR} 
            Changes the default account and packset. 
{DO|!}      Enables IBEX command execution. 
{DUMP}      Create ANLZable dumpfile from the dump information deposited 
            on a pair of RFEP diskettes by a crash in the RFEP. 
{END|EXIT|QUIT} 
            Exit PIGETTE. 
ENTER 
            Invokes a CP-6 ADAPT dialog from within this processor. 
ERASE       Deletes accumulated output for logical devices. 
HELP        Displays information on PIGETTE processor and other 
            processors. 
LIST        Retrieve information about a specific boot diskette; for 
            example, creation date, destination FEP, etc. 
MOVE        Move data between the actual diskette in an FEP drive and 
            the virtual diskette in a CP-6 keyed file. 
OUTPUT      Directs processor output to a destination. 
PRINT       Directs that output accumulated for logical devices be sent 
            to destinations immediately. 
USE         Manage loading in a FEP of the FPRG for handling diskettes. 
VOLINIT     Initialize a diskette. 
For HELP on specific commands, see:  HELP (PIGETTE) command 
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format 
for the display is: 
mmm dd 'yy hh:mm   (month)(day)(year)(hours)(minutes) 
Examples: 
Oink:DATE 
requests a display of the current date and time.  A sample display is: 
AUG 02  '88  11:03 
00001
00002
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
Oink:DIRECTORY .SYSLIB 
This command directs that subsequent fids that do not include an account are 
to default to the .SYSLIB account and the packset associated with that 
account. 
Oink:DIRECTORY DP#UTIL.Y 
This command specifies that subsequent fids that do not include an account are 
to default to the Y account on the packset named UTIL. 
Oink:DIRECTORY RESET 
This command re-establishes the running account and its associated packset as 
the default. 
00002
00003
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
Oink:DO DI 
means display the current system status 
Oink:!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00003
00001
Format: 
[UN]DU[MP] {F[EP] } id1 [D[RIVE] m1] [F[OR] {F[EP] } id2] 
           {N[ODE]}                         {N[ODE]} 
Parameters: 
id1    specifies the node number or name of the fep on which the diskette is 
loaded. 
m1    specifies the diskette drive (0-3) loaded with the diskette that 
contains the dump information.  If no drive is specified, drive 0 is used. 
Drive 0 is the lowest addressed diskette drive and is usually at X'400' for 
remote feps.  Drive 1 is the next highest diskette drive.  Drive 0 is standard 
on CP-6 FEPs; drives 1-3 are optional. 
id2    specifies the node on which the diskette or dump file originated. 
Description: 
The DUMP command creates an ANLZable dumpfile from the dump information 
deposited on a pair of RFEP diskettes by a crash in the RFEP.  It is useful to 
use the DUMP command to analyze problems getting the RFEP to connect to the 
network.  If the local FEP does not have two drives, the DUMP command allows 
you to replace the first diskette in the middle of the command execution to 
complete the dumping process. If id2 is not specified, the nodename for which 
the RFEP diskette was built is used (id1 of the BUILD command), unless that 
node is not defined on the current system, in which case the dump will be 
created for node 100. 
00002
00001
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
This command causes exit from the PIGETTE processor. 
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
Oink:ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
00001
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
  BUILD Command - 
      HELP BUILD 
C 
  CERTIFY Command - 
      HELP CERTIFY 
  CHECK Command - 
      HELP CHECK 
  CLONE Command - 
      HELP CLONE 
D 
  DATE Command - 
      HELP DATE 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DO Command - 
      HELP DO 
  DUMP Command - 
      HELP DUMP 
E 
  END Command - 
      HELP END 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
F 
  Files Created by PIGETTE - 
      HELP RELATED_FILES 
H 
  HELP Command - 
      HELP HELP 
I 
  Invoking PIGETTE - 
      HELP INVOKING_PIGETTE 
L 
  LIST Command - 
      HELP LIST 
  LIST Command (PIGETTE) - 
      HELP LIST FORMAT: 
M 
  MOVE Command - 
      HELP MOVE 
O 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PIGETTE -   
    BUILD Command - 
      HELP BUILD FORMAT: 
    CERTIFY Command - 
      HELP CERTIFY FORMAT: 
    CHECK Command - 
      HELP CHECK FORMAT: 
    CLONE Command - 
      HELP CLONE FORMAT: 
    D0 Command - 
      HELP DO 
    DATE Command - 
      HELP DATE 
    DIRECTORY Command - 
      HELP DIRECTORY 
    DUMP Command - 
      HELP DUMP FORMAT: 
    END Command - 
      HELP END 
    ENTER Command - 
      HELP ENTER 
    ERASE Command - 
      HELP ERASE 
    EXIT Command - 
      HELP END 
    HELP Command - 
      HELP HELP 
    LIST Command - 
      HELP LIST FORMAT: 
    MOVE Command - 
      HELP MOVE FORMAT: 
    OUTPUT Command - 
      HELP OUTPUT 
    PRINT Command - 
      HELP PRINT 
    QUIT Command - 
      HELP END 
    TIME Command - 
      HELP DATE 
    USE Command - 
      HELP USE 
    VOLINIT Command - 
      HELP VOLINIT FORMAT: 
  PRINT Command - 
      HELP PRINT 
  Privileges for Use of PIGETTE - 
      HELP PRIVILEGES 
S 
  Sample PIGETTE Run - 
      HELP SAMPLE_RUN 
T 
  typecode Parameter - 
      HELP TYPECODE_PARAMETER 
U 
  USE Command - 
      HELP USE 
V 
  virtual diskettes - 
      HELP MOVE PARAMETERS: 
  VOLINIT Command - 
      HELP VOLINIT 
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
HELP_INDEX
PIGETTE operates in the host CP-6 system and in a Front End Processor (FEP) 
that is booted and fully operational.  Actual diskette access is provided by a 
FPRG running in the specified FEP. 
PIGETTE may be run either as an on-line or batch job.  It is invoked by the 
command !PIGETTE.  The DCBs used by PIGETTE are: 
o  M$SI for input 
o  M$LO for normal output 
o  M$DO for output of error messages. 
When run on-line, PIGETTE solicits commands with the prompt Oink:.  The 
<BREAK> key can be used to monitor PIGETTE operations.  (See the HELP topic 
SAMPLE_RUN.) 
To run PIGETTE as a batch job, a !PIGETTE command is submitted, followed by a 
series of PIGETTE commands.  Only one command can be submitted per record. 
Format: 
L[IST] [{F[EP] } id [D[RIVE] m]] 
       [{N[ODE]}               ] 
Parameters: 
id    specifies the node number or name of the FEP to be listed.  The default 
is the last one used. 
m    specifies the diskette drive (0-3) loaded with the diskette that are to 
be listed.  If no drive is specified, drive 0 is used.  Drive 0 is the lowest 
addressed diskette drive and is usually at X'400' for remote FEPs.  Drive 1 is 
the next highest diskette drive.  Drive 0 is standard on CP-6 FEPs; drives 1-3 
are optional. 
Description: 
This command lists information about the boot image contained on the specified 
diskette. 
Examples: 
Oink:LIST FEP 7 DRIVE 3 
This command lists information concerning the diskette loaded in drive 3 of 
FEP 7. 
00002
00003
00001
Format: 
       {fid                   } 
M[OVE] {F[EP] id [D[RIVE] m1] } [(TY[PE]=typecode|option[,option] ...)] 
       {N[ODE] id [D[RIVE] m1]} 
                    {fid                   } 
  {TO|ON|OVER|INTO} {F[EP] id [D[RIVE] m2] } 
                    {N[ODE] id [D[RIVE] m2]} 
                    {D[RIVE] m2            } 
Parameters: 
fid    specifies the file identifier for the CP-6 virtual diskette. 
id    specifies the node number or name of the FEP on which the diskette is 
loaded. 
m    specifies the diskette drive (0-3) loaded with the diskette that is to be 
moved.  If no drive is specified, drive 0 is used.  Drive 0 is the lowest 
addressed diskette drive and is usually at X'400' for remote FEPs.  Drive 1 is 
the next highest diskette drive.  Drive 0 is standard on CP-6 FEPs; drives 1-3 
are optional. 
typecode    specifies a code (see HELP (PIGETTE) TYPECODE_PARAMETER) that 
identifies a default set of diskette parameters that are to be used. 
option    specifies one of the options listed in the following table. 
m2    specifies the number of the drive in which the destination diskette is 
loaded. 
  Option                          Description                   Default 
AN[NOUNCE] [=] n                Specifies that a message      None 
                                is to be sent when the 
                                operation is n% 
                                complete. 
DIAGNOSTIC                      Specifies that actual         None 
                                diskette I/O is to be 
                                done in diagnostic 
                                mode. 
SE[CTORS] [=] n[-m]             Specifies the number(s)       1-26 
                                of the sector(s) to be 
                                copied. 
SI[DES] [=] n[-m]               Specifies which side (0       0 
                                or 1) of double-sided 
                                diskette is to be used 
                                (n-m specifies both). 
SS[IZE] [=] n                   Indicates the size            128 
                                (in bytes) of each sector 
                                on the diskette.  Either 
                                128 or 256 may be 
                                specified. 
TR[ACKS] [=] n[-m]              Specifies the number(s)       0-76 
                                of the track(s) to be 
                                copied. 
VS[ECTOR] [=] n[-m]             Specifies the logical         1-diskette 
                                sector numbers (1-disk-       size 
                                ette size) of the portion 
                                to be copied. 
WAIT                            Specifies wait for            None 
                                conformation before 
                                proceeding. 
     {ALL                 }     Specifies whether to          ALL 
WARN {DISK[ETTE]          }     report errors accessing 
     {NONE                }     the data. 
     {V[IRTUAL] D[ISKETTE]} 
Description: 
MOVE moves data between an actual diskette in a FEP drive and a virtual 
diskette stored in a CP-6 keyed file.  The same command is used to transfer 
data from an actual diskette to a virtual diskette, or from a virtual diskette 
to an actual diskette:  either the source or the destination can specify an 
actual diskette in a FEP or remote FEP, or a virtual diskette stored as a CP-6 
keyed file in the host.  If both specify actual diskette(s) then only the 
DRIVE specification is allowed for the destination. 
Examples: 
Oink:MOVE FEP 2 DRIVE 1 (TYPE=RFEP) TO AHOY.MATES 
copies all the information on FEP 2, drive 1 to a file called AHOY.MATES. 
Specifying the TYPE=RFEP option effectively sets the diskette parameters as 
follows:  Track 0-79, Sector 0-15, Side 0-1, Ssize 256. 
00002
00003
00001
Format: 
         [[OVER] LP[@location]] 
OUT[PUT] [[INTO] fid          ] [(option[,option...][)]] 
         [[ON  ] ME           ] 
         [[TO  ]              ] 
Parameters: 
fid    any valid CP-6 file identifier. 
ON or TO    indicates to only honor the OUTPUT command if the file does not 
already exist. 
OVER    indicates to honor the OUTPUT command whether or not the file exists. 
INTO    indicates to merge the result of the OUTPUT command into the file if 
it exists, or to create a new one if it does not. 
LP    directs output to the default line printer; @location specifies a 
specific line printer. 
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
Oink:PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
00002
00003
00001
The user must have authorization to start the handler that accesses the 
diskette.  The user must have both a logon authorization for FPRG handler mode 
and a host logon with FEMFPRG>0. 
To write diskettes, the user must have MFEP privileges or the PPRIV PIGETTE. 
To read diskettes, the user must have CFEP privilege, MFEP privilege, or the 
PPRIV PIGETTE. 
END
The PIGETTE processor uses records in the :NETCON file to describe the boot 
image for the PIGETTE command BUILD, and uses the contents of the files 
referenced therein as part of the boot image. 
The PIGETTE MOVE command builds and reads virtual disk files, keyed CP-6 files 
that contain images of diskettes.  Each record in a virtual disk file 
represents one physical sector on the physical diskette so that the records in 
the virtual file can be accessed by track and sector. 
 !PIGETTE 
   PIGETTE E04 here at 16:40:43.01, 08/22/94. 
 Oink:CHECK FEP10 
  Drive 0 on channel 0600:  type = 2017, status = 0080. 
  Drive 1 on channel 0680:  type = 2017, status = 8000. 
 Oink:LIST 
  Diskette on FEP: 10 Drive: 0 
  Created on WED, 05/16/90, at 12:05:45.07. 
  Built for node L6X      of site C01519 
  Patch level 519 , CP-6 release LADC L 
  Free area starts on VSECTOR 1957. 
 Oink:BUILD FEP12 ON DRIVE 1 
 *** FEP number is out of range or bad node name. 
 Oink:BUILD FEP 12 
 ***  Incorrect input at <?>: 'BUILD FEP <?>12'. 
      Type a "?" for details. 
 Oink:BUILD 12 ON DRIVE 1 
 *** Drive selected is not ready! Check diskette and/or drive 
     while no diskette activity was going on 
 Oink:BU 12 
   ...Copying (73 tracks) 
 >BREAK<                         <--- Note that <BREAK> can be 
                                      used to track progress. 
      while writing Track 2 Side 0 Sector 6 on FEP 10 Drive 0 
 >BREAK< 
      while writing Track 6 Side 1 Sector 12 on FEP 10 Drive 0 
 >BREAK< 
      while writing Track 11 Side 1 Sector 12 on FEP 10 Drive 0 
 >BREAK< 
      while writing Track 22 Side 1 Sector 6 on FEP 10 Drive 0 
 >BREAK< 
      while writing Track 36 Side 0 Sector 12 on FEP 10 Drive 0 
 >BREAK< 
      while writing Track 66 Side 0 Sector 6 on FEP 10 Drive 0 
   Copy complete. 
 Oink:L 
  Diskette on FEP: 10 Drive: 0 
  Created on WED, 08/22/90, at 16:46:11.54. 
  Built for node L6XII    of site LADC L66B 
  Patch level 533 , CP-6 release C01533 
  Free area starts on VSECTOR 2357. 
 Oink:END 
   PIGETTE exiting. 
DATE
The following table lists the mini and standard size diskettes that can be 
loaded into a CP-6 FEP.  The table also indicates the attributes and a 
typecode for each diskette type.  The default diskette type is RFEP.  If the 
diskette is not a RFEP type diskette, then the diskette type must be 
specified. 
The diskette attributes for a non-RFEP type diskettes must be specified in the 
CERTIFY, CLONE, MOVE and VOLINIT commands.  The typecode parameter simplifies 
the specification of diskette attributes by identifying a default set of 
diskette parameters.  Using typecode to specify the diskette attributes will 
avoid failure resulting from incorrect specification of the diskette 
attributes.  (Such failure will often occur without indication as to the cause 
of failure.) 
       Diskette Size/                               Sector 
Code   Description      Sides   Density   Sectors   Bytes     Tracks 
----   --------------   -----   -------   -------   ------    ------ 
MDSDD  Mini             Double  Double    1-16       256       0-79 
MDSSD  Mini             Double  Single    1-16       128       0-79 
MSSDD  Mini             Single  Double    1-16       256       0-79 
MSSSD  Mini             Single  Single    1-16       128       0-79 
RFEP   Mini. CP-6       Double  Double    0-15       256       0-79 
       remote FEP 
       boot diskette 
SDSDD  Standard         Double  Double    1-26       256       0-76 
SDSSD  Standard. Cor-   Double  Single    1-26       128       0-76 
       responds in 
       format, but 
       not necessarily 
       data with IBM 
       diskette type 2. 
SSSDD  Standard         Single  Double    1-26       256       0-76 
SSSSD  Standard. Cor-   Single  Single    1-26       128       0-76 
       responds in 
       format but not 
       necessarily data 
       with IBM disk- 
       ette type 1. 
Note: Mini-size=5 1/4 inches 
      Standard size=8 inches 
DUMP
Format: 
USE [{F[EP] } id] 
    [{N[ODE]}   ] 
Parameters: 
id    specifies a node number or name for the FEP. 
Description: 
This command causes the PIGETTE front end program (FPRG) that handles diskette 
processing at the FEP to be loaded and to remain loaded until another USE 
command is issued, the PIGETTE session ends, or the FEP crashes or is 
disconnected.  This is not different than normal operation, except the 
commands referencing a different FEP are disallowed. 
Usage Notes: 
Only one FEP may be active at a time.  When the USE command is issued, the FEP 
identified in the succeeding PIGETTE diskette commands must be the same as the 
FEP specified in the USE command. 
Once a USE command is issued, succeeding USE commands are used to: 
o   change the FEP for which succeeding operations are to be performed. 
o   cancel a USE command.  Issuing the USE command without a FEP id parameter 
    cancels the previously issued USE command. 
Example: 
Oink:USE FEP 7 
00002
00004
00001
00003
Format: 
VOLINIT {F[EP] } id [D[RIVE] m] [(TY[PE]=typecode|option[,option] ...)] 
        {N[ODE]} 
Parameters: 
id    specifies the node number or name of the FEP on which the diskette is 
loaded. 
m    specifies the diskette drive (0-3) loaded with the diskette that is to be 
initialized.  If no drive is specified, drive 0 is used.  Drive 0 is the 
lowest addressed diskette drive and is usually at X'400' for remote FEPs. 
Drive 1 is the next highest diskette drive.  Drive 0 is standard on CP-6 FEPs; 
drives 1-3 are optional. 
typecode    specifies a code (see HELP (PIGETTE) TYPECODE_PARAMETER) that 
identifies a default set of diskette parameters that are to be used. 
option    specifies one of the following: 
  Option                   Description                            Default 
SE[CTORS] [=] n[-m]      Specifies the sector ID                1-15 
                         number(s) to be VOLINITED 
                         on to the disk. 
SI[DES] [=] n[-m]        Specifies which side (0                0-1 
                         -1) of double-sided 
                         diskette is to be VOLINITED 
                         (n-m specifies both). 
SS[IZE] [=] n            Indicates the size                     256 
                         (in bytes) of each sector 
                         on the diskette.  Either 
                         128 or 256 may be 
                         specified. 
TR[ACKS] [=] n[-m]       Specifies the number(s)                0-76 
                         of the track(s) to be 
                         VOLINITED. 
Description: 
This command initializes a diskette.  Track and sector headers are written on 
the diskette; all data blocks on the diskette are overwritten with zeros. 
Example: 
Oink:VOLINIT FEP 2 (TYPE=RFEP) 
This command initializes the diskette loaded in drive 0 of FEP 2, suitable for 
use as a remote FEP boot diskette. 
00002
00003
00001
