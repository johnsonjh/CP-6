To obtain more HELP information, see 
HELP (DEF) TOPICS                 Displays available topics. 
HELP (DEF) COMMANDS               Displays a list of DEF 
                                  commands. 
HELP (DEF) command PARA           Displays parameters 
                                  associated with 
                                  a particular command 
HELP (DEF) command DESC           Displays description 
                                  associated with a 
                                  particular command. 
?                                 Displays next level 
                                  of HELP messages. 
??                                Displays all levels 
                                  of HELP messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
Format: 
ACCOUNT [DP#psn].acct [(type[, type] ... )] 
Parameters: 
psn    specifies a packset name. 
acct    specifies an account. 
type    specifies a 2-character file type.  Refer to the M$OPEN monitor 
service in the publication "CP-6 Host Monitor Services Reference (Desc.)", 
CE74, for a list of file types. 
Description: 
The ACCOUNT command specifies that all files of a type designated in the type 
list be copied from the account specified.  A question mark may be used as a 
wildcard character. 
Usage Note: 
Multiple ACCOUNT commands may be entered. 
00002
00001
00001
00003
Format: 
BLOCK [MODE] 
Description: 
The BLOCK command causes the labeled portion of the PO tape to be written in 
block mode.  Block mode tapes may be written significantly faster by DEF and 
read significantly faster by GHOST1 than tapes that are not written in block 
mode.  The disadvantage is that files on the unlabeled portion of the block 
mode tape may not be accessed via PCL. 
Usage Notes: 
1.  The block mode format used by DEF is not the same as that used by EFT. 
    Thus, EFT may not be used to retrieve files from a block mode tape. 
2.  The PCL LIST command may be used to obtain the names of the files on a 
    block mode tape, but PCL cannot access the files either to copy them or 
    list with attributes. 
3.  The block mode files are written to the tape with an ORG of RESTRICT.  The 
    first block of each block mode file is the FIT of the file.  It will be 
    returned in the area specified by the FPARAM parameter to M$OPEN.  The 
    tape is read a block at a time into a 1024 word buffer with FULL=YES 
    specified in the M$READ FPT.  Word zero of each block contains the key 
    required to write the block to disk. 
    The FMBLK privilege is required for access to the block mode tape files 
    and for block mode access to disk files.  This privilege may not be 
    granted to users, but must be granted to processors residing in the :SYS 
    account. 
4.  On the labeled portion of a PO tape, files with any organization other 
    than RESTRICT are not in block mode and may be copied using PCL. 
00001
00002
Format: 
BOOTSTRAP {fid|NIL} 
Parameters: 
fid    specifies a CP-6 file identifier. 
NIL    specifies that the bootstrap program be omitted. 
Description: 
The BOOTSTRAP command specifies that a file other than AARDVARK (from the 
current file management account) is to be written to the unlabeled portion of 
the PO tape. 
00002
00001
00001
A list of DEF commands and their definitions can be accessed by typing a ? or 
a ??.  To obtain definitions of individual commands, type 
HELP (DEF) COMMANDS command 
where command is any of the following: 
ACCOUNT, BLOCK, BOOTSTRAP, DATE, DENSITY, DIRECTORY, DO, END, ENTER, ERASE, 
EXIT, FIRMWARE, G1HJIT, GHOST1, HELP, IGNORE, INCLUDE, INSTALL, MHJIT, 
MINI_ID, MON, NOBOOT, NOFILES, NOLIST, OUTPUT, PATCH, PO, PRINT, QUIT, 
SALUTATION, SCHEMA, SEARCH, SITEID, SITENAME, TIME, VERIFY, XDLT, XDLTLS 
  Command        Description 
  ACCOUNT 
                 Specifies the accounts whose files are to be written to the 
                 labeled portion of the PO tape. 
  BLOCK 
                 Causes the labeled portion of the PO tape to be written in 
                 block mode. 
  BOOTSTRAP 
                 Specifies the bootstrap program to write on the unlabeled 
                 portion of the PO tape. 
  {DATE|TIME} 
                 Displays the current time and date. 
  DENSITY 
                 Specifies the density at which the PO tape is to be written. 
  {DIRECTORY|DIR} 
                 Changes the default account and packset. 
  {DO|!} 
                 Enables IBEX command execution. 
  END 
                 Terminates DEF command streams and instructs DEF to begin 
                 writing the PO tapes. 
  ENTER 
                 Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
                 Deletes accumulated output for logical devices. 
  {EXIT|QUIT} 
                 Terminates DEF without writing the PO tapes. 
  FIRMWARE 
                 Specifies the MPC firmware to write on the unlabeled portion 
                 of the PO tape. 
  G1HJIT 
                 Specifies the GHOST1 HJIT run unit file to write to the 
                 unlabeled portion of the PO tape. 
  GHOST1 
                 Specifies the GHOST1 run unit to write on the unlabeled 
                 portion of the PO tape. 
  HELP 
                 Displays information about DEF and other processors. 
  IGNORE 
                 Supplies overrides to selection criteria specified via the 
                 ACCOUNT command. 
  INCLUDE 
                 Specifies files to write to the labeled portion of the PO 
                 tape. 
  INSTALL 
                 Specifies the file to write to the PO tape as $XINSTALL. 
  MHJIT 
                 Specifies the monitor HJIT run unit file to write on the 
                 unlabeled portion of the PO tape. 
  MINI_ID 
                 Specifies an identifier for the site, in addition to the site 
                 id. 
  MON 
                 Specifies the monitor run unit file to write to the unlabeled 
                 portion of the PO tape. 
  NOBOOT 
                 Bypasses writing of the unlabeled portion of the PO tape. 
  NOFILES 
                 Specifies that after writing of the unlabeled portion, a CVOL 
                 is to be performed, forcing the labeled portion to start on 
                 volume 2. 
  NOLIST 
                 Suppresses listing of patches as they are written on the 
                 unlabeled portion of the PO tape. 
  OUTPUT 
                 Directs processor output to a destination. 
  PATCH 
                 Specifies patch files (and TIGR commands) to write on the 
                 unlabeled portion of the PO tape. 
  PO 
                 Specifies the version for the PO tape being created. 
  PRINT 
                 Directs that output accumulated for logical devices be sent 
                 to destinations immediately. 
  SALUTATION 
                 Specifies the logon salutation. 
  SCHEMA 
                 Specifies the monitor debug schema be included on the 
                 unlabeled portion of the PO tape. 
  SEARCH 
                 Specifies a list of packset(s) and account(s) from which 
                 INCLUDE files are to be picked up and written to the labeled 
                 portion of the PO tape. 
  SITEID 
                 Specifies the site identifier. 
  SITENAME 
                 Specifies the site name to include in the greeting displayed 
                 to users following logon. 
  VERIFY 
                 Verifies the labeled portion of an existing PO tape set. 
  XDLT 
                 Specifies the file containing XDELTA to write to the 
                 unlabeled portion of the PO tape. 
  XDLTLS 
                 Specifies the XDELTA linkage segment to write to the 
                 unlabeled portion of the PO tape. 
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
00011
00029
00030
00031
00032
00033
00004
00034
00035
00036
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm (month)(day)(year)(hours)(minutes) 
Examples: 
:DATE 
requests a display of the current date and time.  A sample display is: 
AUG 02  '88  11:03 
00001
00002
Format: 
DENSITY {800|1600|6250} 
Parameters: 
800|1600|6250    specifies tape density bits per inch (bpi). 
Description: 
This command specifies the density at which the PO tape is to be written. 
00002
00001
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
:DO DI 
means display the current system status 
:!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00003
00001
Format: 
E[ND] 
Description: 
The END command terminates command input and instructs DEF to begin writing 
the PO tapes. 
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
Format: 
{EXIT|QUIT} 
Description: 
The EXIT command (or its synonym QUIT) terminates DEF without writing the PO 
tapes. 
00001
Format: 
FIRMWARE {fid|NIL} 
Parameters: 
fid    specifies a CP-6 file identifier. 
NIL    specifies that MPC firmware be omitted. 
Description: 
The FIRMWARE command specifies that a file other than FIRMWARE (from the 
current file management account) is to be written to the unlabeled portion of 
the PO tape. 
00002
00001
00001
Format: 
G1HJIT {fid|NIL} 
Parameters: 
fid    specifies a CP-6 file identifier. 
NIL    specifies the GHOST1 HJIT run unit be omitted. 
Description: 
The G1HJIT command specifies that a file other than G1HJIT (from the same 
account as GHOST1) is to be written to the unlabeled portion of the PO tape. 
00002
00001
00001
Format: 
GHOST1 {fid|NIL} 
Parameters: 
fid    specifies a CP-6 file identifier. 
NIL    specifies the GHOST1 be omitted. 
Description: 
The GHOST1 command specifies that a file other than GHOST1 (from the current 
file management account) is to be written to the unlabeled portion of the PO 
tape. 
00002
00001
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
A 
  ACCOUNT Command -   
    DEF - 
      HELP ACCOUNT FORMAT: 
  ACCOUNT Command - 
      HELP ACCOUNT 
B 
  BLOCK Command - 
      HELP BLOCK 
  BOOTSTRAP Command - 
      HELP BOOTSTRAP 
D 
  DATE Command - 
      HELP DATE 
  DEF -   
    ACCOUNT Command - 
      HELP ACCOUNT FORMAT: 
    BOOTSTRAP Command - 
      HELP BOOTSTRAP FORMAT: 
    DENSITY Command - 
      HELP DENSITY FORMAT: 
    END Command - 
      HELP END FORMAT: 
    FIRMWARE Command - 
      HELP FIRMWARE FORMAT: 
    G1HJIT Command - 
      HELP G1HJIT FORMAT: 
    GHOST1 Command - 
      HELP GHOST1 FORMAT: 
    IGNORE Command - 
      HELP IGNORE FORMAT: 
    INCLUDE Command - 
      HELP INCLUDE FORMAT: 
    INSTALL Command - 
      HELP INSTALL FORMAT: 
    MHJIT Command - 
      HELP MHJIT FORMAT: 
    MINI_ID Command - 
      HELP MINI_ID FORMAT: 
    MON Command - 
      HELP MON FORMAT: 
    NOBOOT Command - 
      HELP NOBOOT FORMAT: 
    NOFILES Command - 
      HELP NOFILES FORMAT: 
    NOLIST Command - 
      HELP NOLIST FORMAT: 
    PATCH Command - 
      HELP PATCH FORMAT: 
    PO Command - 
      HELP PO FORMAT: 
    SALUTATION Command - 
      HELP SALUTATION FORMAT: 
    SCHEMA Command - 
      HELP SCHEMA FORMAT: 
    SEARCH Command - 
      HELP SEARCH FORMAT: 
    SITEID Command - 
      HELP SITEID FORMAT: 
    SITENAME Command - 
      HELP SITENAME FORMAT: 
    VERIFY Command - 
      HELP VERIFY FORMAT: 
    XDLT Command - 
      HELP XDLT FORMAT: 
    XDLTLS Command - 
      HELP XDLTLS FORMAT: 
  DENSITY Command - 
      HELP DENSITY 
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
  EXIT Command - 
      HELP EXIT 
F 
  FIRMWARE Command - 
      HELP FIRMWARE 
G 
  G1HJIT Command - 
      HELP G1HJIT 
  GHOST1 Command - 
      HELP GHOST1 
H 
  HELP Command - 
      HELP HELP 
I 
  IGNORE Command - 
      HELP IGNORE 
  INCLUDE Command - 
      HELP INCLUDE 
  INSTALL Command -   
    DEF - 
      HELP INSTALL FORMAT: 
  INSTALL Command - 
      HELP INSTALL 
  Invoking DEF - 
      HELP INVOKING_DEF 
L 
  Labeled Portion of the PO Tape Set - 
      HELP LABELED 
M 
  MHJIT Command - 
      HELP MHJIT 
  MINI_ID Command - 
      HELP MINI_ID 
  MON Command -   
    DEF - 
      HELP MON FORMAT: 
  MON Command - 
      HELP MON 
N 
  NOBOOT Command - 
      HELP NOBOOT 
  NOFILES Command - 
      HELP NOFILES 
  NOLIST Command - 
      HELP NOLIST 
O 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PATCH Command - 
      HELP PATCH 
  PO Command - 
      HELP PO 
  PO Tape Set - 
      HELP PO_TAPE_SET 
  PRINT Command - 
      HELP PRINT 
  Privileges for Use of DEF - 
      HELP PRIVILEGES_FOR_USING_DEF 
Q 
  QUIT - 
      HELP EXIT DESCRIPTION: 
R 
  Required Files - 
      HELP RELATED_FILES 
S 
  SALUTATION Command - 
      HELP SALUTATION 
  SCHEMA Command - 
      HELP SCHEMA 
  SEARCH Command - 
      HELP SEARCH 
  SITEID Command - 
      HELP SITEID 
  SITENAME Command - 
      HELP SITENAME 
U 
  Unlabeled Portion of the PO Tape Set - 
      HELP UNLABELED 
V 
  VERIFY Command - 
      HELP VERIFY 
X 
  XDLT Command - 
      HELP XDLT 
  XDLTLS Command - 
      HELP XDLTLS 
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
HELP_INDEX
Format: 
IGNORE fid[, fid] ... 
Parameters: 
fid    specifies a CP-6 file identifier. 
Description: 
The IGNORE command overrides the ACCOUNT command with respect to the files 
named in the fid list.  A file in an account specified by an ACCOUNT command 
will not be copied if it is named in an IGNORE command.  If a fid specifies 
only an account name, files in that account are ignored.  If a fid specifies 
only a filename, that file is ignored whenever it is encountered. 
00002
00001
00001
Format: 
INCLUDE fid [AS filename] [, fid [AS filename]] ... 
Parameters: 
fid    specifies a CP-6 file identifier. 
filename    specifies the name to be assigned to the file when it is written 
to the tape. 
Description: 
The INCLUDE command specifies the file(s) to be included on the labeled 
portion of the PO tape.  If a fid does not contain an account, then the 
accounts specified on the SEARCH command are searched. 
Usage Note: 
Multiple INCLUDE commands may be entered. 
00002
00001
00001
00003
Format: 
INSTALL fid 
Parameters: 
fid    specifies a CP-6 file identifier. 
Description: 
The INSTALL command specifies that a file other than $XINSTALL (from the 
current file management account) is to be written to the PO tape. 
00002
00001
00001
DEF is invoked by the !DEF command directly from IBEX.  DEF may be run as a 
batch job, on-line job, or console ghost job.  DEF commands are read through 
the M$SI DCB.  DEF writes the PO tape through the M$PO DCB.  A free-form tape 
must be used for the PO tape.  The free-form specification may be accomplished 
by issuing an appropriate SET command for the M$PO DCB, or by means of 
parameters in the !DEF command. 
The format of the !DEF command is: 
!DEF [fid] [{ON|OVER|TO} {FT[#vsn]|MT[#vsn]}] 
where 
fid    is the file of DEF commands.  If no fid is given, DEF will look to the 
command stream for its commands. 
MT or FT    are alternative ways of indicating that a free-form tape must be 
used.  This specification may be omitted if the M$PO DCB has been SET to 
free-form tape. 
vsn    is the volume serial number of the tape to be used.  If a multivolume 
PO tape is created, subsequent volumes will have the serial numbers CP6PO2, 
CP6PO3,...,CP6PO9. 
The list of files that DEF is to write to the labeled portion of the PO tape 
is specified by a combination of INCLUDE, SEARCH, ACCOUNT, and IGNORE 
commands.  DEF contains a list of files that are required elements of the 
labeled portion of the PO tape.  Once the labeled portion of the PO tape is 
written, DEF prints out a list of any required files that were not found. 
(See Required Files below.) 
The labeled portion of the PO tape set is written in the order in which files 
are specified in the INCLUDE command(s).  ACCOUNT commands are processed 
first, followed by INCLUDE commands.  If two files of the same name are 
written to the tape, the last one on the tape will be the file written in 
:SYS. 
Format: 
MHJIT {fid|NIL} 
Parameters: 
fid    specifies a CP-6 file identifier. 
NIL    specifies the monitor HJIT be omitted. 
Description: 
The MHJIT command specifies that a file other than MHJIT (from the current 
file management account) is to be written to the unlabeled portion of the PO 
tape. 
00002
00001
00001
Format: 
MINI_ID {'xxx'|xxx} 
Parameters: 
{'xxx'|xxx}    specifies a three character identifier which is in addition to 
the version specified on the PO command. 
Description: 
The MINI_ID command sets the values for B_SITEINFO.MINI_ID#.  The MINI_ID is 
usually set to the 3-digit patch week of the PO tape being created (e.g., 
645). 
Usage Note: 
If this command is not present, MINI_ID will be set to blanks. 
00002
00001
00001
00003
Format: 
MON {fid|NIL} 
Parameters: 
fid    specifies a CP-6 file identifier. 
NIL    specifies the monitor run unit and monitor linkage segment be omitted. 
Description: 
The MON command specifies that a file other than M:MON (from the current file 
management account) is to be written to the unlabeled portion of the PO tape. 
00002
00001
00001
Format: 
NOBOOT 
Description: 
The NOBOOT command bypasses writing of the unlabeled portion of the PO tape. 
This command may be used to create standard tape sets. 
00001
Format: 
NOFILES 
Description: 
The NOFILES command writes the unlabeled portion and $XINSTALL on volume 1, 
and then performs a CVOL to force additional files onto volume 2. 
00001
Format: 
NOLIST 
Description: 
The NOLIST command suppresses the listing of the patches written on the 
unlabeled portion of the PO tape. 
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
PATCH fid[, fid]... 
Parameters: 
fid    specifies a CP-6 file identifier. 
Description: 
The PATCH command specifies the file(s) of patches and TIGR commands to be 
written on the unlabeled portion of the PO tape. 
Usage Note: 
Multiple PATCH commands may be entered. 
00002
00001
00001
00003
Format: 
PO version 
Parameters: 
version    specifies a 1 to 3 character version number. 
Description: 
The PO command specifies a version number different than the version of the 
CP-6 system under which DEF is running. 
00002
00001
00001
There are two distinct portions on this tape set:  the unlabeled portion and 
the labeled portion.  The unlabeled portion consists of all programs and data 
necessary to boot-load, patch and initialize the monitor, and to install the 
files from the labeled portion of the tape.  The labeled portion consists of 
CP-6 labeled tape format files which are to be copied into the :SYS account 
during the boot process.  The DEF process selects the files to be written, and 
permits the system manager to specify the selection criteria.  The tape set 
created by the DEF processor is known as the PO tape set.  The contents of the 
unlabeled portion of the PO tape set initialize the unmanaged system area of 
the system disk.  The contents of the labeled portion of the PO tape set 
initialize the :SYS account in the file-managed area of the system disk.  The 
contents of both portions of the PO tape are discussed in more detail below. 
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
While no specific privileges are required to use DEF, FMBLK must be active to 
write the tape in block mode. 
EXIT
The following files are required elements of the labeled portion of the PO 
tape: 
    :OCKEY                        JAYS 
    :OCMSG                        KEYIN 
    :SHARED_SYSTEM                LOGON 
    :SHARED_LCP6_SYSTEM           M:FEP 
    ASYNC                         NETCON 
    COUPLER                       NODEADMN 
    DELTA                         OUTSYM 
    DOG                           PIG 
    ELF                           PRESCAN 
    FROG                          RCVR2 
    GOOSE                         SLUG 
    IBEX                          SUPER 
    INSYM 
RELATED_FILES
Format: 
SALUTATION 'text_string' 
Parameters: 
'text_string'    specifies the first line of the logon solicitation. 
Description: 
The SALUTATION command specifies the logon salutation (text_string may contain 
a maximum of 43 characters). 
Usage Note: 
If the SALUTATION command is omitted, the salutation of the system on which 
DEF is run is the default. 
00002
00001
00001
00003
Format: 
SCHEMA fcg[, fcg] ... 
Parameters: 
fcg    specifies a 1 or 2 character functional code group. 
Description: 
The SCHEMA command specifies that instead of writing all monitor debug schema, 
only the schema for the specified functional code groups are to be written to 
the unlabeled portion of the PO tape. 
Usage Note: 
Multiple SCHEMA commands may be entered. 
00002
00001
00001
00003
Format: 
SEARCH [DP#psn].acct [, [DP#psn].acct] ... 
Parameters: 
psn    specifies a packset name. 
acct    specifies an account to be searched.  The current file management 
account may be specified by a single period. 
Description: 
The SEARCH command specifies accounts for which file directories are to be 
searched for files that were specified in the INCLUDE command only by file 
name.  If this command is present, the current account is not automatically 
searched; it is searched only if it is included in the SEARCH command's list. 
Accounts are searched in the order specified in the SEARCH command. 
Usage Notes: 
1.  If the SEARCH command is omitted, the current file management account is 
    searched. 
2.  Multiple SEARCH commands may be entered. 
00002
00001
00001
00003
Format: 
SITEID 'character_string' 
Parameters: 
'character_string'    specifies a 6-character site id. 
Description: 
The SITEID command specifies the site id to be placed in B_SITEINFO.SITE_ID#. 
(The default is the site id on which DEF is being run.) It should not be 
necessary to use this command for PO tapes DEFed on site. 
Usage Notes: 
1.  The site id is assigned by Bull marketing. 
00002
00001
00001
00003
Format: 
SITENAME 'text_string' 
Parameters: 
'text_string'    specifies the site name of usually no more than 20 
characters, although 139 characters are permitted. 
Description: 
The SITENAME command specifies the locally generated site name to be inserted 
in the greeting line issued to on-line users when they log on. 
Usage Note: 
If the SITENAME command is omitted, the site name on which DEF is being run is 
the default. 
00002
00001
00001
00003
DATE
DEF writes the following items to the unlabeled portion of the PO tape. 
o   AARDVARK (the bootstrap program) 
o   Firmware (procedure and data for the microprogrammed controllers (MPC)). 
o   XDELTA (system debugger) 
o   MONITOR (including the TIGR procedure) 
o   GHOST1 (system initialization ghost) 
o   Patches to the system components listed above, TIGR commands, processor 
    patches, and patches to the FEP software.  Writing of any of these patches 
    elements to the PO tape is optional, since they may alternatively be read 
    from the card reader or the operator's console. 
If all patches and TIGR commands are included on the tape, the system can be 
booted without using a card reader for these items. 
Format: 
VERIFY 
Description: 
The VERIFY command verifies the labeled portion of an existing PO set.  As 
each record is constructed to be written to the PO tape, instead of writing it 
to tape, the tape is read and the results are compared. 
00001
Format: 
XDLT {fid|NIL} 
Parameters: 
fid    specifies a CP-6 file identifier. 
NIL    specifies the file containing XDELTA be omitted. 
Description: 
The XDLT command specifies that a file other than XDELTA (from the current 
file management account) is to be written to the PO tape. 
00002
00001
00001
Format: 
XDLTLS {fid|NIL} 
Parameters: 
fid    specifies a CP-6 file identifier. 
NIL    specifies the XDELTA linkage segment be omitted. 
Description: 
The XDLTLS command specifies that a file other than XDELTAS (from the same 
account as XDELTA) is to be written to the PO tape. 
00002
00001
00001
