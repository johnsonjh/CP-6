The PCL processor is invoked by the IBEX command: 
PCL [fid] 
where 
fid   -   specifies a file of PCL commands, one command per record 
(continuations via semicolon are permitted.)  PCL is automatically exited at 
the end of the file. 
If no fid is specified, PCL responds by printing the following message on the 
user's output device: 
PCL D00 here 
< 
The less-than sign (<) is the prompt indicating that PCL is prepared to 
receive commands.  Command input is through the M$SI DCB and defaults to the 
user's terminal for on-line operations and job stream for batch operations. 
Any command which may be entered from IBEX may also be entered in response to 
the PCL prompt.  This can be done by entering the IBEX bang (!) directly after 
the PCL prompt.  For all of these commands, with the exception of !XEQ, the 
user is returned to PCL after the command is executed. 
For HELP messages, type: 
HELP (PCL) COMMANDS      For a list and brief description of commands 
HELP (PCL) TOPICS        For a list of topics 
HELP (PCL) command       For the format of a specific command. 
                         Then type ? or ?? for more. 
HELP (PCL) command PARAM For parameter information for a 
                         specific command. 
HELP (PCL) command DESC  For the description of a specific 
                         command. 
?                        Displays next level of 
                         HELP messages. 
??                       Displays all levels of 
                         HELP messages. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
If a BREAK is issued while a COPY is active, the following message is printed: 
BREAK at xxx of yyy - kk.kkk (fid).  C to continue. 
where 
xxx   -   specifies the logical sequence number of the record in the output 
file where execution was halted. 
yyy   -   specifies total records in file. 
kk.kkk   -   specifies key of appropriate record in file, when applicable. 
If the user types C, the command is processed to completion; any other 
response aborts the command.  When the command is aborted, the output file is 
saved if the last issued ERRORS command specified SAVE; otherwise the output 
file is released.  For more information, press ? 
If a <BREAK> is issued while a COPYALL is active, the following message is 
printed: 
BREAK at xxx of yyy - kk.kkk (fid).  C to continue. 
where 
xxx   -   specifies the logical record number of the output file being copied. 
yyy   -   specifies total records in file. 
kk.kkk   -   specifies key of appropriate record in file, when applicable. 
If the user types anything except C, the copy operation is aborted and the 
file at which the interruption took place is saved if the last issued ERRORS 
command specified SAVE.  If the user types C, the file at which the 
interruption took place is copied to completion and a second message is 
printed: 
C to continue at end 
If the user types anything but C, the COPYALL is aborted.  For more 
information, press ? 
If <BREAK> is presed during a deletion, the file currently being deleted is 
deleted, and the following message is printed: 
Break! C to continue. 
If the user types anything except C, the delete operation is aborted.  If the 
user types C, the delete operation continues and a message is printed 
confirming the number of files deleted and the number of blocks freed. 
If <BREAK> is pressed during a LIST, REVIEW, MOD or MOUNT operation, the 
following message is printed: 
Break!  C to continue. 
If C is entered, step continues; otherwise the step is aborted. 
The <BREAK> key has no effect upon any other PCL commands.  These operations 
run to completion even if <BREAK> is pressed while they are active. 
COPY
COPYALL
Changes have been made to the following processors:  IBEX, EDIT, PLOVER and 
LEMUR.  No changes have been made to PCL, IMP AND LINK. 
For information on changes to a specific processor, type: 
HELP (processor) CHANGES processor 
For IBEX HELP changes, see also HELP CHANGES TERMINAL and HELP CHANGES VFC. 
  Processor    Changes 
  Section 1 - Manual Overview. 
               No changes. 
  Section 2 - File and I/O management concepts. 
  Section 3 - IBEX command language. 
               o  New options have been added to the $INPUT builtin 
                  function: 
                        REPLY_EXPRESSION - sets up a default reply. 
                        REREAD_POSITION - sets up the cursor within 
                                          the REPLY_EXPRESSION. 
               o  A new builtin function $CMDVAR_EXISTS (cmdvarname) 
                  returns 1 if specified command variable exists, else 
                  returns 0. 
               o  New TERMINAL suboptions have been added to the 
                  CHARSETNAME option: 
                        ASC8 - has slightly different functionality. 
                        ASC8I - has been added as a new type. 
               o  A new option has been added to SET/ADJUST/RESET: 
                        The COPIES option has been added for 
                        UR files and devices. 
               o  The SET option TYPE now allows a quote string. 
               o  DI BUDGET now displays more information. 
               o  CANCEL now has the same output as CHECK. 
               o  The CHECK command now accepts ~JOBID to allow deletion 
                  from the USE file. 
               o  DI PROFILES and VARS accept wildcards against which to 
                  match the output list. 
               o  The SET command now displays SET information if no SET 
                  options are specified. 
               o  XEQ/BATCH/XMIT now accept encrypted files via the CRPT 
                  option. 
               o  LET BANNERTEXTn now accepts IBEX expressions. 
               o  CHECK now allows accounts to be checked. 
               o  CANCEL now accepts most of the options of CHECK. 
               o  The option ORG=X364 has been added to the SET command. 
               o  The JOBNAME parameter (for JOB, FOLLOW, CHECK, CANCEL 
                  and UNHOLD) now accepts digits. 
               o  The IBEX CHECK command now allows a user to specify an 
                  output file. 
               o  The documentation has been corrected for the TERMINAL 
                  option HALFDUXPAPERTAPE. 
               o  The option ONESPACEEDIT has been added to the 6EDIT 
                  FORMAT command Esc-1-LF. 
  Section 4 - EDIT Processor. 
               o  A new topic EQUAL (or =) has been added to EDIT. 
                  The equal sign can now be used as a way of specifying 
                  the current file you are editing (in place of the 
                  filename). 
               o  A new topic XUG_SERVICES (or XUG) has been added to EDIT. 
                  XUG services allow you to use a DO (!) command at the * 
                  prompt. 
               o  The RF/MK/MD commands have been improved with minor bug 
                  fixes. 
               o  The MERGE command now allows 'ON'|'TO' and 'OVER'. 
               o  '==' is now allowed on the MERGE command as the second 
                  fid. 
               o  A new topic ROUNDING (or RO) has been added to EDIT. 
                  AP and IN will now round the next line number inserted 
                  to a multiple of INCR. 
               o  The IN command has been updated to act like AP if the 
                  whole file is selected. It has also been updated to 
                  work for consecutive files. 
               o  The IS command has been updated to work for consecutive 
                  files. 
               o  The RR command can now specify column positioning. 
               o  The STATUS command will now display MODE. The STATUS 
                  display has been rearranged by level of importance. 
                  STATUS now also allows options and has had the new 
                  synonym SHOW added to it. 
               o  The TP command now uses the last TY/TS/TC format when 
                  displaying the selected lines. 
  Section 5 - PCL processor. 
               No changes. 
  Section 6 - Terminal Editing Features. 
               o  The option ONESPACEEDIT has been added to the 6EDIT 
                  FORMAT command Esc-1-LF. 
  Section 7 - IMP processor. 
               No changes. 
  Section 8 - LINK processor. 
               No changes. 
  Section 9 - LEMUR processor. 
               o  Upon exit, LEMUR now sets the STEPCC to indicate 
                  whether any errors were found. 
  Section 10 - PLOVER processor. 
               o  The documentation for the EXTERNAL command has been 
                  clarified. 
  Appendix A - DELTA directives. 
               No Changes. 
  Appendix B - ASCII Character set. 
               No changes. 
  Appendix C - Device Format Control Characters. 
               No changes. 
  Appendix D - Monitor Error Messages. 
               No changes. 
  Appendix E - Making ANS and IBM-compatible Tapes. 
               No changes. 
  Appendix F - X3.64 Functions. 
               No changes. 
00012
00011
00004
00002
00016
00003
00007
00009
00008
00014
00001
00005
00010
00015
00006
00013
COPY
COPYALL
The commands in PCL are: 
File Copy:               COPY, COPYALL, COPYSTD 
Spooling File Control:   PRINT, ERASE 
Disk File Modification:  MODIFY, DELETERECORD 
Disk File Deletion:      DELETE, DELETESTD 
List and Review:         LIST, LISTSTD, REVIEW, REVIEWSTD 
Tape Control:            MOUNT, REWIND, SPF, SPE, SPR, SCAN, 
                         REMOVE, RELEASE, WEOF. 
Informational:           HELP, STATUS 
Miscellaneous:           DIRECTORY, END, ERRORS, 
                         LINK, READ, SEVERITY, TX. 
For information about individual commands, type    HELP command. 
Format: 
[device[#serial][(globaloptionlist)]][/(sourcelist)] 
Parameters: 
device   -   specifies a device (e.g. LT, DP, CR). 
#serial   -   specifies a tape serial number or a packset name (valid only for 
MT, FT, LT, or DP). 
globaloptionlist   -   specifies a set of input options that will be globally 
assigned to the sourcelist (if present).  If source list is absent, the input 
options apply to the specified device.  See INOPS 
sourcelist   -   is a list of single, ranged, or wildcard sources, separated 
by commas.  The parentheses are not required if only one such source is named. 
Description: 
The complex source component is a special form that allows device 
specification, combined with global option capability. 
Examples: 
LT#ABCD(VO=2)/(?X?) 
means all files on LT#ABCD whose names contain the character X, beginning with 
volume 2 of the labeled tape. 
DP(ORG=K)/A 
means file A on disk, organization KEYED.  Note that because only a single 
filename is specified, the area to the right of the slash need not be enclosed 
in parenthesis. 
LT#XYZ(TY=SA,PHY)/(M1>M2,DATAFILE(TY=DA)) 
means all files of file type SA (Source APL) that lie physically between files 
M1 and M2 (inclusive), and the file DATAFILE of filetype DA (Data APL), all on 
the labeled tape XYZ. 
Usage Note: 
Complex sources can be specified anywhere a source is permitted, except the 
DELETE RECORD command. 
00002
00003
00001
00004
The use of PCL components can be illustrated using the PCL COPY command, which 
contains components that are found in other PCL commands.  A simple form of 
the COPY command is: 
COPY source TO destination FROM fid 
In fact, the COPY command is somewhat more flexible than this, but for the 
purposes of the discussions, the following general definitions hold true: 
o   The source component is the file to be copied, or the device in which the 
    file is stored. 
o   The destination component is the "place" to which the file is to be copied 
    or to be stored. 
o   The FROM component is a set of fid elements that are globally associated 
    with the source parameters; i.e., they provide defaults for fids in the 
    source. 
To obtain information about PCL components insert:  HELP (PCL) component where 
'component' is one of the following: 
SINGLE_SOURCE 
Single Source Component         the simplest form of source, 
                                usually just a disk or tape file. 
RANGE_SOURCE 
Range Source Component          a range of sources, usually files 
                                in an alphabetic (ASCII) searching order. 
WILD_SOURCE 
Wildcard Source Component       selection of source files based upon 
                                the presence of specified strings in 
                                their filename. 
COMPLEX_SOURCE 
Complex Source Component        a powerful source selection component, 
                                usually used with tape devices. 
DESTINATION 
Single Destination Component    the simplest form of the destination 
                                component, typically a file to which 
                                the sources are copied. 
WILD_DESTINATION 
Wildcard Destination Component  selection of multiple destinations 
                                based upon specified strings; used 
                                only with wildcard sources. 
PREPOSITION 
Preposition Component           the TO, ON, OVER, and INTO part of 
                                COPY-like commands; TO and ON are file 
                                creation, OVER is file replacement, 
                                and INTO is file catenation. 
FROM 
FROM Component                  a  way of specifying global 
                                attributes for sources. 
COPY
COPYALL
COPYSTD
Syntax 
C[OPY] sourcelist[ {TO|ON|OVER|INTO} destination][ FROM fid] 
Parameters: 
sourcelist   -   specifies a list of sources with input options.  A maximum of 
ten input options is allowed.  See PCL INOPS.  The basic format of the source 
parameter is: 
fid[(option[,option]..)] 
TO   -   specifies file creation (see Preposition Component). 
ON   -   specifies file creation (see Preposition Component). 
OVER   -   specifies file replacement (see Preposition Component). 
INTO   -   specifies file extension (see Preposition Component). 
destination   -   specifies a single destination fid with output options and 
attributes that may replace or add to the attributes of the source fid.  The 
COPY command issued from IBEX always defaults to LP in batch and to ME online. 
The first time a COPY command is issued from PCL, the default is the same as 
it would be in IBEX.  Subsequent COPY commands issued inside PCL default to 
the last COPY destination.  The COPY command defaults INTO fid.  If an error 
condition occurs, the default is reset back to the original default. 
The basic format of the destination parameter is: 
fid[(option[,option]...)] 
FROM fid   -   specifies default values for parts of a fid not specified in 
the source parameters.  See SINGLE_SOURCE, DESTINATION, and FROM for more 
detailed information. 
Description: 
COPY copies a source or list of sources to a single specified destination. 
When a copying operation begins, a message "..COPYing" is printed. 
Examples: 
<COPY LESLIE 
means copy the file LESLIE to the default destination (the terminal in on-line 
operations, the line printer in batch if no previous COPY has been done in 
this session). 
<COPY LESLIE,HELEN TO FILEA 
means copy files LESLIE and HELEN to a new file FILEA. 
<COPY ?A? (OR=CON) TO FILEB(RD=ALL) 
means copy all files that contain the character "A" in their file name, and 
that are of consecutive file organization, into a new file FILEB giving READ 
access to all accounts. 
<COPY A>C TO FILEC 
means copy all files between A and C (using file range selection) to a new 
file FILEC. 
Related Commands: 
COPYALL, COPYSTD 
00002
00003
00001
00004
Syntax: 
C[OPY]A[LL] [sourcelist][ {TO|ON|OVER|INTO} destination][ FROM fid] 
Parameters: 
sourcelist   -   specifies a list of sources with input options.  If 
unspecified, all files in the user's account are assumed.  Input file 
selection is also dependent upon any input options included as part of a 
source parameter.  The basic format of the source parameter is: 
fid[(option[,option]...)] 
TO   -   specifies file creation (see Preposition Component). 
ON   -   specifies file creation (see Preposition Component). 
OVER   -   specifies file replacement (see Preposition Component). 
INTO   -   specifies file extension (see Preposition Component). 
destination   -   specifies a special fid with associated output options that 
define the characteristics of the output files.  This may be any valid fid, 
except that no file name can be included unless it is a wildcard file name. 
The default, if not specified, is the user's account directory. 
FROM fid   -   specifies default values for parts of a fid not specified in 
the source parameters (see FROM Component). 
See SINGLE_SOURCE, RANGE_SOURCE, WILD_SOURCE, COMPLEX_SOURCE, DESTINATION, and 
FROM for detailed syntactical information. 
Description: 
COPYALL copies a source or group of sources to a group of destinations, 
generally preserving any associated file names, but allowing the modification 
of other fid elements. 
COPYALL is primarily for multiple file transfers.  Unless a wildcarded fid is 
included as part of the destination parameter, the names of the input files in 
the source parameters are preserved in the output files.  The other fid 
elements of the input files are not retained; the destination parameter 
defines device type, account, password, etc. of the output files. 
WILDCARD CONSIDERATIONS:  If wildcarding is used recursion may occur.  If the 
output file name places the output file in the input selection range, the 
operation may be repeated on the output file.  To prevent recursion other 
input selection criteria may be added (such as DATEC < NOW). 
Examples: 
<COPYALL .MYACCOUNT 
DANIEL    HELEN     LESLIE    PAPPY 
     4 files,     32 granules copied 
< 
means copy all the files in the account .MYACCT into the user's account.  As 
each file is transferred, its file name is printed at the terminal. 
<COPYALL ?N? TO ?n? 
means copy all files that contain the character "N", creating new files that 
contain (in their file names) the character "n" in place of the character "N". 
As each file is copied, the source file name is printed with an "arrow" 
pointing to the new file. 
DANIEL -> DAnIEL    HELEN -> HELEn 
     2 files,     16 granules copied 
< 
<L  . 
DANIEL    DAnIEL    HELEN     HELEn     LESLIE    PAPPY 
     6 files listed 
< 
Note that only the first occurrence of the letter is changed.  However, 
recursion may occur if output file falls within the selection range. 
<CA  ?P? TO ?H? 
PAPPY -> HAPPY 
      1 file,        8 granules copied 
<COPYALL ?E? TO ?e? 
DANIEL -> DANIeL    DAnIEL -> DAnIeL    HELEN -> HeLEN 
HELEn -> HeLEn      HeLEN -> HeLeN      HeLEn -> HeLen 
LESLIE -> LeSLIE    LeSLIE -> LeSLIe 
      8 files,      32 granules copied 
<L . 
DANIEL    DANIeL    DAnIEL    DAnIeL    HAPPY     HELEN 
HELEn     HeLEN     HeLEn     HeLeN     HeLen     LESLIE 
LeSLIE    LeSLIe   PAPPY 
      7 files listed 
< 
Related Commands: 
COPY, COPYSTD, MODIFY 
00002
00003
00001
00004
Syntax: 
C[OPY]S[TD] stdfid[ {TO|ON|OVER|INTO} destination] [ FROM fid] 
Parameters: 
stdfid   -   specifies an STD file.  Each record of the STD file contains a 
sourcelist.  A source is defined as a fid or range of fids or wildcards with 
input options.  See INOPS.  The basic format of the source parameter is: 
fid[(option[,option]..)] 
TO   -   specifies file creation.  See PREPOSITION. 
ON   -   specifies file creation.  See PREPOSITION. 
OVER   -   specifies file replacement.  See PREPOSITION. 
INTO   -   specifies file extension.  See PREPOSITION. 
destination   -   specifies a set of fid elements with associated output 
options that define the characteristics of the output files.  See OUTOPS. 
This may be any valid fid, except that no file name can be included unless it 
is a wildcard file name.  The basic format of the destination parameter is: 
fid[(option[,option]...)] 
FROM fid   -   specifies default values for parts of a fid not specified in 
the source parameters.  See SINGLE_SOURCE, DESTINATION, and FROM for detailed 
syntactical information. 
Description: 
COPYSTD copies a source or list of sources as defined in a STD file. 
COPYSTD functions identically to the COPYALL command, except that the list of 
sources is obtained from a file rather than typed as part of the command.  The 
STD file is also copied to the specified destination. 
Examples: 
<COPYSTD STANDARD TO LP 
means copy all files (named in STANDARD) to the default lineprinter.  Note 
that the first file copied is the STD file itself. 
Related Commands: 
COPY, COPYALL 
00002
00003
00001
00004
COPYSTD
COPYSTD
The following Data Control Blocks (DCBs) may be set by the user prior to 
entering PCL: 
DCB              FUNCTION 
---              -------- 
M$ME             Writes all conversational and diagnostic output; if set, the 
                 file is opened for file extension.  This cannot be a keyed 
                 or indexed file. 
M$DO             Writes all diagnostic output; if set, the file is opened for 
                 file extension.  This cannot be a keyed or indexed file. 
M$SI             Reads all command input. 
M$EO             Writes all output from a COPY command. 
M$EO1            Writes all output from COPYALL, COPYSTD, LIST, and LISTSTD 
                 commands. 
The M$EO and M$EO1 DCBs, can only be successfully reassigned if the AMR 
(Assign Merge) output option is specified as part of the command. 
DELETE
DELETERECORD
Syntax: 
DEL[ETE] sourcelist[ FROM fid] 
Parameters: 
sourcelist   -   specifies a list of disk filenames, ranges of disk files, or 
wildcard filenames, with only OR, DATE, or TY input options permitted. 
FROM fid   -   specifies a default set of fid elements that are used when the 
source parameters are parsed. 
See the common parameter descriptions for SOURCE and FROM for detailed 
syntactical information. 
Description: 
DELETE deletes a file or range of files from disk storage. 
When a single file is deleted with DELETE, a message is printed that confirms 
the deletion and the number of granules that the file contained.  When 
multiple files are deleted with a DELETE command, a verification of the 
operation is requested.  The user must type YES$ in response to this 
verification, or the operation is aborted.  If the operation is not aborted, 
the name of each file is printed as it is deleted, and upon completion, a 
message is printed confirming the number of files deleted and the number of 
granules freed. 
When the DELETE command is used to delete multiple files in batch job 
execution or as part of an XEQ command file, verification is not requested. 
Examples: 
<DELETE FILEA,FILEB,FILEC 
means delete files FILEA, FILEB, and FILEC.  A message is printed that 
confirms the deletions. 
<DELETE ?Q.PIG FROM ..MAGIC 
means delete all files in account PIG where names end with a Q, that have a 
password MAGIC, or no password. 
Related Commands: 
DELETESTD 
00002
00003
00001
00004
Syntax: 
DEL[ETE]REC[ORD] sourcefid [FROM fid] 
Parameters: 
sourcefid   -   specifies a single disk file from which records are to be 
deleted.  Records to be deleted are specified by either relative record 
number/range or key number/range of the form n1[-[n2]].  If no record 
selection information is provided the command is aborted and the file is left 
unaltered. 
FROM fid   -   specifies a default fid whose elements are used when PCL parses 
the source parameter (See FROM Component). 
Description: 
DELETERECORD causes the specified records to be permanently removed from the 
input file.  The record selection range may be specified in any order, and may 
overlap one another.  PCL arranges the selections so that overlap is 
eliminated, and the specified records are deleted in descending order from the 
end of the file. 
Examples: 
<DELREC MYFILE(2,8,4-10,20-) FROM .THERE 
deletes records 20 through EOF, records 4 through 10 inclusive, and record 2 
from the file MYFILE.THERE.  The specification of record 8 is redundant. 
<DELREC MYEDITFILE(4.5-9.,3-9) 
deletes all records having EDIT-style keys from 4.5 through 9.0 inclusive and 
logical records 3 through 9. 
<DELETEREC MYKEYEDFILE(O'0'-'FRED') 
deletes all records having a key less than or equal to 'FRED'. 
00002
00003
00001
Syntax: 
D[ELETE]S[TD] stdfid [ FROM fid] 
Parameters: 
stdfid   -   specifies an STD file.  Each record of the file contains a 
sourcelist.  Each source must be either a disk filename, a range of disk 
files, or a wildcard filename. 
FROM fid   -   specifies a default set of fid elements that are used when the 
sources in the STD file are parsed. 
See the common parameter description for SOURCE and FROM for detailed 
syntactical information. 
Description: 
DELETESTD deletes disk files according to a list of sources defined in an STD 
file.  The STD file is not deleted. 
DELETESTD functions identically to a DELETE command, except that the list of 
sources is contained in a file rather than as part of the command.  Note that 
the STD file is not deleted, unless explicitly specified as an entry in the 
STD file.  Unlike the DELETE command, DELETESTD will not request confirmation 
when a wildcard or range is specified. 
Examples: 
<DELETESTD STANDARD 
means delete the files defined in the STD file STANDARD. 
Related Commands: 
DELETE 
00002
00003
00001
00004
DELETERECORD
DELETERECORD
DELETESTD
DELETESTD
Format: 
fid[(option[,option]...)] 
Parameters: 
fid   -   is any valid output fid. 
option   -   specifies an output option that provides information about the 
processing or final disposition of the destination.  See OUTOPS 
Description: 
The single destination component identifies and/or qualifies the storage 
medium to which sources are to be transferred.  The default is command 
dependent.  See LIST and COPY commands for specific defaults. 
Examples: 
LP@BOSTON(K) 
means line printer at workstation BOSTON; include file keys in printed output. 
MYFILE(ORG=K,ACC=(CP-6?,READ)) 
means keyed disk file, MYFILE; only accounts beginning with the characters 
CP-6 can read the file. 
FT#WXYZ(DE=6250) 
means free tape WXYZ; output at 6250 bytes per inch. 
DP#FRODO/GONDOR.ARAGORN(TY=WB) 
means disk file GONDOR of file type WB (Workspace BASIC) in account ARAGORN on 
packset FRODO. 
Usage Note: 
When output is directed to a logical device such as a printer, a PRINT command 
must be issued before the output is actually printed. 
00002
00003
00001
00004
Syntax: 
{DIR|DIRECTORY} [{fid|R[ESET]}] 
Parameters: 
fid   -   specifies the new default account fid, and may consist of an account 
or a pack set name and an account. 
RESET   -   specifies that the default account is to be reset to the running 
account. 
Description: 
DIRECTORY changes the default account and pack set.  The default account and 
set are the account and associated pack set that are selected if an account is 
not supplied as part of a disk file fid specification.  Initially, the default 
account is the log-on or running account and the pack set name is nil. 
DIRECTORY without the use of the parameter displays the current default 
account and set. 
Examples: 
<DIRECTORY .SYSLIB 
This command directs that subsequent fids that do not include an account are 
to default to the .SYSLIB account and the pack set associated with that 
account. 
<DIRECTORY DP#UTIL.Y 
This command specifies that subsequent fids that do not include an account are 
to default to the Y account on the pack set named UTIL. 
<DIRECTORY RESET 
This command re-establishes the running account and its associated pack set as 
the default. 
Related Commands: 
NONE 
00002
00003
00001
00004
DELETESTD
Syntax: 
{E[ND]|Q[UIT]|[E]X[IT]} 
Parameters: 
NONE 
Description: 
END (and the QUIT and EXIT synonyms) terminates PCL processing. 
The simplest forms of the END command are E, Q, and X. 
NOTE:  The END command should not be confused with the END response in the 
REVIEW command. 
Examples: 
<END 
means exit PCL. 
Related Commands: 
NONE 
00002
00003
00001
00004
ERRORS
Syntax: 
ERASE [fid[,fid]...] 
Parameters: 
fid   -   is a device stream fid.  If unspecified, all streams are deleted 
from the system. 
Description: 
ERASE causes spooling streams to be deleted from the system without being 
output. 
Examples: 
<COPY HELEN TO CP 
<ERASE 
means copy file HELEN to the card punch at the user's workstation.  The ERASE 
command cancels the output and the actual card punch device is not activated. 
Related Commands: 
PRINT 
00002
00003
00001
00004
Syntax: 
ER[RORS] {S[AVE]|R[ELEASE]} 
Parameters: 
SAVE   -   specifies that the output file or spooling stream is to be saved. 
RELEASE   -   specifies that the output file or spooling stream is to be 
deleted. 
The default is RELEASE. 
Description: 
ERRORS determines the handling of output files and spooling streams in the 
event of an error or break condition. 
Examples: 
<ERRORS SAVE 
means save the file or output stream if an error occurs. 
Related Commands: 
NONE 
00002
00003
00001
00004
END
Format: 
F[ROM] fid 
Parameters: 
fid   -   specifies any combination of name, account, packset, and/or password 
to be used as a default in the source parameters; this has the format of any 
valid CP-6 fid.  If a fid element is specified both in the source parameter 
and the FROM parameter, the FROM parameter's fid element is overridden.  The 
default directory account, when specified by a period following the file name 
in the source, is not replaced by the account in the FROM.  Wildcard names are 
permitted. 
Description: 
The FROM component defines default values for parts of fid not specified in 
the source parameters in a command. 
Examples: 
SOURCE                 FROM                  MEANING 
------                 ----                  ------- 
FISH>FROG              FROM LT#ABCD          LT#ABCD/FISH>FROG 
DP#MYSET,DP#OLSET      FROM ?_OV             DP#MYSET/?_OV,DP#OLSET/?_OV 
LT#ABCD/HELEN          FROM..REVOL           LT#ABCD/HELEN..REVOL 
ABBOT,DP#YOX/COSTELLO  FROM DP#FROG/..PASS   DP#FROG/ABBOT..PASS 
                                             DP#YOX/COSTELLO..PASS 
CHICKEN.,GOOSE         FROM .FARM            CHICKEN. 
                                             GOOSE.FARM 
MOOSE..HUNTER          FROM .URANUS          MOOSE..HUNTER 
00002
00003
00001
FROM
Syntax: 
HELP [(fid)] [TOPICS] [keyword1] [-] [keyword2] 
Note:  The following elements can be specified in any order: 
         fid 
         TOPICS 
         [keyword1] [-] [keyword2] 
For example, HELP (fid) keyword1 - keyword2 TOPICS is acceptable. 
Parameters: 
fid    specifies the processor name (for example, EDIT).  If fid is omitted, 
the current processor is assumed.  The processor name can be ? to request a 
listing of processors that have HELP facilities available. 
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
keyword1 and keyword2 may be abbreviated (by truncation).  keyword1 may 
include the wildcard (?) character as the rightmost character, if TOPICS is 
specified. 
Description: 
HELP displays information. 
HELP messages have levels.  Once the initial level has been displayed, 
entering a question mark displays the next level, usually containing greater 
detail.  Entering two question marks displays all the remaining levels. 
Examples: 
<HELP COPY 
means print the syntax of the COPY command. 
<HELP TOPICS 
means print the names of all available PCL HELP messages. 
<HELP INOPS 
means print a list of the input options. 
<HELP OUTPUT_OPTIONS RECS 
means print a description of the RECS output option. 
Related Commands: 
NONE 
00002
00003
00001
00004
A 
  access vehicles -   
    PCL - 
      HELP OUTPUT_OPS ACSVEHICLES 
B 
  BREAK Key Function -   
    PCL - 
      HELP BREAK_RESPONSE 
C 
  Complex Source Component - 
      HELP COMPLEX_SOURCE 
  concepts (PCL) - 
      HELP OPTIONS 
  COPY Command -   
    PCL - 
      HELP COPY SYNTAX 
  COPY Command - 
      HELP COPY 
  COPYALL Command - 
      HELP COPYALL 
  COPYSTD Command - 
      HELP COPYSTD 
D 
  Data Control Blocks (DCBs) -   
    PCL - 
      HELP DCBS 
  DCB assignments (PCL) - 
      HELP DCBS 
  DCBs -   
    PCL - 
      HELP DCBS 
  DCBs (Data Control Blocks) - 
      HELP DCBS 
  DELETE Command -   
    PCL - 
      HELP DELETE SYNTAX: 
  DELETE Command - 
      HELP DELETE 
  DELETERECORD Command - 
      HELP DELETERECORD 
  DELETESTD Command - 
      HELP DELETESTD 
  destination component (PCL) - 
      HELP DESTINATION FORMAT: 
  DIRECTORY Command -   
    PCL - 
      HELP DIRECTORY SYNTAX: 
  DIRECTORY Command - 
      HELP DIRECTORY 
E 
  END Command -   
    PCL - 
      HELP END SYNTAX: 
  END Command - 
      HELP END 
  ERASE Command -   
    PCL - 
      HELP ERASE SYNTAX: 
  ERASE Command - 
      HELP ERASE 
  ERRORS Command - 
      HELP ERRORS 
  EXIT Command -   
    PCL - 
      HELP END PARAMETERS: 
F 
  files -   
    ranges - 
      HELP RANGE_SOURCE DESCRIPTION: 
  FROM Component - 
      HELP FROM 
H 
  HELP Command - 
      HELP HELP_COMMAND 
I 
  IBEX Commands from PCL - 
      HELP IBEX_COMMANDS 
  Input Options - 
      HELP INPUT_OPS 
  IXTNSIZE - PCL option - 
      HELP OUTPUT_OPS IXTNSIZE 
L 
  LIST Command -   
    PCL - 
      HELP LIST PARAMETERS: 
  LIST Command - 
      HELP LIST 
  LISTSTD Command - 
      HELP LISTSTD 
M 
  MODIFY Command - 
      HELP MODIFY 
  MOUNT Command - 
      HELP MOUNT 
O 
  output options (PCL) - 
      HELP OUTPUT_OPS 
P 
  parameters, PCL - 
      HELP COMPONENTS 
  PCL BREAK Response - 
      HELP BREAK_RESPONSE 
  PCL Command Summary - 
      HELP COMMANDS 
  PCL Components - 
      HELP COMPONENTS 
  PCL Concepts - 
      HELP OPTIONS 
  PCL input options - 
      HELP INPUT_OPS 
  PCL input options summary - 
      HELP OPTIONS INPUT 
  PCL Output Options - 
      HELP OUTPUT_OPS 
      HELP OUTPUT_OPS 
  PCL parameters - 
      HELP COMPONENTS 
  Preposition Component - 
      HELP PREPOSITION 
  PRINT Command -   
    PCL - 
      HELP PRINT SYNTAX: 
  PRINT Command - 
      HELP PRINT 
Q 
  QUIT Command -   
    PCL - 
      HELP END SYNTAX: 
R 
  Range Source Component - 
      HELP RANGE_SOURCE 
  READ Command -   
    PCL - 
      HELP READ SYNTAX: 
  READ Command - 
      HELP READ 
  RELEASE Command -   
    PCL - 
      HELP RELEASE SYNTAX: 
  RELEASE Command - 
      HELP RELEASE 
  REMOVE Command - 
      HELP REMOVE 
  RENAME Command (see PCL MODIFY) - 
      HELP MODIFY 
  REVIEW Command - 
      HELP REVIEW 
  REVIEWSTD Command - 
      HELP REVIEWSTD 
  REWIND Command - 
      HELP REWIND 
S 
  SCAN Command - 
      HELP SCAN 
  SEVERITY Command - 
      HELP SEVERITY 
  Single Destination Component - 
      HELP DESTINATION 
  Single Source Component - 
      HELP SINGLE_SOURCE 
  SPE Command - 
      HELP SPE 
  SPF Command - 
      HELP SPF 
  SPR Command - 
      HELP SPR 
  STATUS Command -   
    PCL - 
      HELP STATUS SYNTAX: 
  STATUS Command - 
      HELP STATUS 
T 
  TX Command -   
    PCL - 
      HELP TX SYNTAX: 
  TX Command - 
      HELP TX 
V 
  Vehicle (Processor) Permission - 
      HELP OUTPUT_OPS ACSVEHICLES 
  vertical format control - 
      HELP OPTIONS VFC 
  VFC output option - 
      HELP OUTPUT_OPS VFC 
W 
  WEOF Command - 
      HELP WEOF 
  Wildcard Destination Component - 
      HELP WILD_DESTINATION 
  Wildcard Source Component - 
      HELP WILD_SOURCE 
X 
  XTNSIZE - PCL Option - 
      HELP OUTPUT_OPS XTNSIZE 
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
Any command which may be entered from IBEX may be entered following the PCL 
prompt by entering the IBEX bang (!) followed by the IBEX command.  For all of 
these commands, with the exception of !XEQ, the user is returned to PCL after 
the command is executed. 
INPUT_OPS
PCL recognizes the following input options.  A maximum of ten input options is 
permitted with any one command. 
ATTRIBUTES, BINARY, BLOCK, CLPOS, COLUMNS, CREATOR, CRITERIA, CRPT, DATE, 
DEOD, EATTRIBUTES, EBCDIC, FATTRIBUTES, FFID, FSN, FTORGANIZATION, HEAD, 
IGNOREFSN, IOERROK, n1-n2, NBINARY, NBLOCKED, NCNVRT, NHEAD, NSPANNED, 
ORGANIZATION, PHYSICAL, RECLENGTH, SHARED, SORTEDBY, TRANSPARENT, TYPE, 
VOLUME. 
To obtain a HELP message for an individual option, type: 
HELP INOPS option 
The options are displayed with the following structure: 
  Option     Meaning 
  A[TTRIBUTES] 
             List the file or range of files with associated attributes. 
  B[INARY] 
             Specifies that any read operation from a free tape (FT) or card 
             reader (CR) is to interpret data as binary.  The default is 
             NBINARY (see the NBINARY option). 
  BL[OCK]=value 
             Specifies the block length for input from free tape.  May also be 
             used to specify the block length for input from labeled tape 
             without HDR2 labels; in this case, the values specified should be 
             the same as those used to create the tape files. 
             NOTE:  For labeled tape with HDR2 labels, the values for BLOCK 
             will come from the HDR2 label. 
  CLPOS={BOT|BOF|EOF|NO[NE]} 
             Specifies input tape positioning on the CLOSE.  Valid only for 
             COPY from free tape. 
             BOT   -   Rewind the tape to its beginning. 
             BOF   -   Rewind the tape to the beginning of the file. 
             EOF   -   Space forward to the end of the file on the tape. 
             NONE   -   Specifies that the input tape is not re-positioned on 
             the CLOSE. 
             Default is NONE. 
  C[OLUMNS]=n 
             List the name(s) of the file or range of files in columns of n 
             characters in width; the meaning of this value varies depending 
             on the device used for output.  C=0 means one filename per line. 
  CRE[ATOR]{=|~=}{'account,username'|'ME'} 
             Selects only those files that were created by the specified user; 
             'username' is the same as that used in the logon procedure. 
             Arbitrary selection by CREATOR ('account,username') requires the 
             FMSEC privilege. 
  CRI[TERIA][=] (condition[,condition...]) 
             Establishes criteria for file search according to the 
             condition(s) specified.  For example, !L .(CRITERIA=(DELF)) 
             results in the listing of files deleted by the user, but still in 
             the file directory. 
             where 'condition' may be any of the following: 
             ANYF    specifies that the search include every entry in the file 
             directory, including deleted entries. 
             ARCHIVE    specifies that the search be directed for files that 
             are known to the archive system. 
             BAD    specifies a search for files with a file inconsistency. 
             BUF    specifies a search for files that are to be backed up. 
             DELF    specifies a search for deleted files that are still in 
             the file directory. 
             NOLIST    specifies a search for files with a 'no list' 
             attribute. 
             QS    specifies a search for files that are queued for stow. 
             REV    results in a search for a file or account directory in 
             reverse order. 
             NOTE:  Criteria is meaningless if used with single fid 
             definition. 
  CRPT=octal value 
             Specifies that the octal value is to be used as a decryption seed 
             when data is read.  If the input data was previously encrypted 
             with the same seed, the result will be decryption of data; if 
             not, the data is encrypted using the specified seed.  The value 
             can range from 0 to 777777777777, or be a one to four-character 
             string enclosed in single quotes.  The default is no encryption 
             (CRPT=0). 
  DA[TE] type relation date 
             Specifies file selection for COPY, LIST, MODIFY or DELETE 
             operations based on date of creation, last access, last 
             modification, or expiration.  Parameter options may be any 
             combination of one each of type, relation, and date: 
             type                Meaning 
             ----                ------- 
             A[CCESS]            date of last access 
             B[ACKUP]            date of last backup 
             C[REATE]            date of creation of file 
             E[XPIRE]            date of expiration 
             M[ODIFY]            date of last modification 
             S[TOWED]            date of last STOW 
             relation 
             -------- 
             <                   before 
             <=                  before or equal to 
             =                   equal to 
             ~=                  not equal to 
             >=                  after or equal to 
             >                   after 
             date 
             ---- 
             -ddd                number of days before today 
             [+]ddd              number of days after today 
             mm/dd/yy            specific day 
             TODAY               today 
             NEVER               Used with E[XPIRE] to indicate 
                                 that file never expires 
             NOTE:  If the action specified is a multiple file DELETE, PCL 
             will request confirmation before deleting each source 
             specification. 
             <DELETE .(DATE EXPIRE<TODAY) 
             deletes all files marked expired. 
  DEOD 
             Specifies that all files in an unmanaged free tape (FT) are to be 
             read until two consecutive end-of-data (EOD) characters are read. 
  EA[TTRIBUTES] 
             List the file or range of files with associated extended 
             attributes. 
  EB[CDIC] 
             Specifies that tape data read from free tape (FT) be translated 
             from EBCDIC to ASCII.  The default is no translation. 
  FA[TTRIBUTES] 
             List the file or range of files with associated full attributes. 
  F[SN]=(n[-m]) 
             Specifies that files n through m are to be read sequentially from 
             a tape.  The value of m must exceed the value of n, and both must 
             be between 1 and 32767.  FSN may not be specified if a filename 
             or range is included in the source parameter.  If m is omitted, 
             only file n is assumed. 
  FF[ID] 
             Causes the full fid to be printed.  May be specified as part of a 
             source specification and/or as a LIST option. 
  FT[ORGANIZATION]={[FREE]|UN[DEFINED]|F[IXED]|V[ARIABLE]} 
             Specifies the input file organization for free tape.  The default 
             is FREE. 
  H[EAD] 
             Specifies that the PCL header line for this source is to be 
             output regardless of the device type. 
  IGN[OREFSN] 
             This option is meaningful only for labelled tape files.  This 
             option can be used to read tapes with erroneous file sequence 
             numbers and erroneous section numbers. 
  IO[ERROK] 
             This option is meaningful only for labelled tape files.  With 
             this option, tape file management tries to recover from I/O 
             errors as completely as possible.  The action taken depends on 
             the operation in progress at the time of the error.  If tape 
             errors occur and IOERROK is specified, the errors will not be 
             reported, and some records may be missing or garbeled. 
  n1[-[n2]] 
             If the file is any organization other than KEYED or INDEXED, this 
             option specifies record selection by logical record position; 
             e.g., the first record in the file is 1, the second is 2, the 
             first through the third record is 1-3, etc. 
             If the file is INDEXED or KEYED, this option specifies record 
             selection by keys or logical record position.  Keys may be 
             decimal (an EDIT key format with period included), octal, or 
             string, or any combination.  If a decimal key omits the period, 
             it is interpreted as a logical record number.  An octal key is 
             represented in the following format: 
             O'nnn...' 
             A string key is represented in the following format: 
             'string' 
             A record selection specification may not mix keys and logical 
             record numbers. 
             In all cases, if key1 is specified alone, only key1 is selected, 
             and if the dash (-) character is included without key2, key2 is 
             assumed to be the end of the file. 
  NBIN[ARY] 
             Specifies that any read operation from a free tape (FT) or a card 
             reader (CR) is to interpret data as characters rather than as 
             binary.  The default is NBINARY.  (See the BINARY option.) 
  NBL[OCKED] 
             Specifies that the input free tape is not blocked.  The default 
             is blocked. 
  N[CNVRT] 
             Specifies EBCDIC data read from tapes with the EBCDIC option is 
             not to be translated into ASCII.  The default is translation. 
             This option is valid for managed tapes only. 
  NH[EAD] 
             Specifies that the PCL header line for this source is to be 
             suppressed regardless of the device type. 
  NS[PANNED] 
             Specifies that the input free tape is not spanned.  If 
             unspecified, it is assumed to be spanned. 
  OR[GANIZATION]{=|~=}(org[,org]...) 
             Specifies that only managed files of certain organizations are to 
             be selected.  Valid organizations are: 
             C[OM]G[ROUP] 
             C[ONSECUTIVE] 
             DBGCG 
             DBGDCB 
             DBGSYSID 
             F[IXED] 
             FO[RM] 
             F[ORMS]P[ROGRAM] 
             FR[EE] 
             HA[NDLER] 
             ID[S] 
             IN[DEXED] 
             I[NDEXED] R[ELATIONAL] 
             IR[E][L] 
             K[EYED] 
             RA[NDOM] 
             REL[ATIVE] 
             RES[TRICTED] 
             S[CREEN] E[DIT] 
             S[YMBIONT] 
             T[ERMINAL] 
             U[NIT]R[ECORD] 
             UN[DEFINED] 
             V[ARIABLE] 
             X364 
  PHY[SICAL] 
             Specifies that a range of file names in a source parameter is to 
             be interpreted physically; this only applies to labeled tape. 
             PCL positions to the first file in the range specification and 
             then consecutively accesses files until the second file in the 
             range specification is located and accessed.  If unspecified, all 
             files whose filenames are alphabetically between the two 
             filenames in the range specification are accessed. 
  R[ECLENGTH]=value 
             Specifies the maximum record length for input from free tape. 
             May also be used to specify the maximum record length for input 
             from labeled tape without HDR2 labels; in this case, the values 
             specified should be the same as those used to create the tape 
             files. 
             The  defaults are format dependent: 
             Format          Default         Maximum 
             ------          -------         ------- 
             C,X             BLOCK-4         32764 
             F,V,U           80              32764 
             D,S             80              9999 
             R,X             4096            28672 
             NOTE:  For labeled tape with HDR2 labels, the values for 
             RECLENGTH will come from the HDR2 label. 
  S[HARED] 
             Causes the input file or range of files to be opened in the 
             shared mode, allowing other users to update the file while PCL is 
             accessing it for input.  If unspecified, no other users may 
             update the file while PCL is accessing it. 
  SORT[EDBY]=([mode] criteria[,[mode] criteria]...) 
             Causes the selected input files to be processed in the order 
             specified by mode and criteria.  Valid modes are: 
             A[SCENDING]    Ascending sort is used. 
             DE[SCENDING]   Descending sort is used. 
             If no mode is specified, ASCENDING is used. 
             Valid criteria are: 
             DA[TE]type   (type is the same as for the DATE input option) 
             G[RANULES] 
             R[ECORDS] 
             T[TYPE] 
             Example: 
             L(A).(SORTEDBY=(DE G,DATEC)) 
             sorts by ascending creation date within descending granules. 
  TR[ANSPARENT] 
             Specifies input without translation.  Primarily useful for input 
             organizations which normally perform character translation. 
  TY[PE]{=|~=}(ty[,ty]...) 
             Specifies that only managed files of certain types are to be 
             selected.  A maximum of 10 types may be specified.  File types 
             are two character codes with the following meanings: 
             1st Character 
             D = Data 
             I = Database 
             O = Object Unit 
             R = Run Unit 
             S = Source 
             U = Update 
             W = Workspace 
             X = Work file 
             1 = schema for databases 
             2 = subschema for databases 
             * = file reserved for system use: can only be created 
                 by operating system; can be read or deleted by user. 
             blank = undefined 
             2nd character for processor object units: 
             A = APL 
             a = ARES 
             B = BASIC 
             C = COBOL 
             D = TP(TRADER) 
             E = EDIT 
             F = FORTRAN 
             f = FPL 
             G = GMAP 
             I = IDS 
             J = IMP 
             K = reserved 
             P = Performance Monitor or PARTRGE 
             Q = IDP 
             R = RPG 
             S = SORT 
             T = TEXT 
             1 = reserved 
             6 = PL-6 
             2nd character for data files: 
             A = ASCII 
             B = ASCII and single precision 
             D = Double precision 
             S = Single precision 
             a = APL data block attributes 
             c = APL component file 
             blank = undefined or unformatted 
  VO[LUME]=value 
             Specifies which volume of a tape set is to be accessed initially. 
             The value can range from 1 to 511. 
00001
00002
00003
00005
00004
00005
00006
00007
00008
00009
00010
00011
00012
00014
00013
00015
00014
00016
00017
00018
00019
00023
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
00020
00020
INPUT_OPS
PREPOSITION
INPUT_OPS
Syntax: 
L[IST][(listopt)][ sourcelist][ {TO|ON|OVER|INTO} destination][ FROM fid] 
Parameters: 
listopt   -   specifies either an A, C, CRE, CRI, DA, EA, FA, FF, OR, SORT, or 
TY listing format input option. 
sourcelist   -   specifies a list of disk or labeled tape fid with options. 
The only valid options are A, EA, C, CRIT, DATE, FA, FSN, OR, PHYS, TY, and 
VOL.  If a source has an A, EA, C, or FA input option, the request overrides 
the default listing format.  If an account is specified, it should be one to 
which the user has authorized access.  If unspecified, the user's directory 
account is assumed as a default source.  The basic format of the source 
parameter is: 
fid[(option[,option]...)] 
TO   -   specifies file creation (see Preposition Component). 
ON   -   specifies file creation (see Preposition Component). 
OVER   -   specifies file replacement (see Preposition Component). 
INTO   -   specifies file extension (see Preposition Component). 
destination   -   specifies the output for the listing operation.  This may be 
either a file, or a device stream.  The default is ME, which indicates the 
user's terminal (on-line) or the line printer (batch).  The CR, FA, LC, NCR, 
NFA, O, TX, VC, VF, X, FV, NV, and X1 are invalid output options for this 
command. 
FROM fid   -   specifies a default fid whose elements are used when PCL parses 
the source parameters (see FROM Component). 
The default list option for single file specifications is A; for multiple 
specifications, the default is C=12. 
See the common parameter descriptions for SOURCE, DESTINATION and FROM for 
detailed syntactical information. 
Description: 
LIST prints a summary of disk and labeled tape storage.  The A option causes 
files to be listed with file organization, the file type, the number of 
granules, the NGAV (number of excess granules), the number of records, the 
date the file was last modified, and the file name.  The EA option adds 
additional file management information.  The FA option includes the EA and 
also provides key, KEYL, and alternate key information for indexed files. 
Examples: 
<L(A) 
means list the files in the account with attributes. 
<LIST AGRIPPA 
means list the file AGRIPPA, with attributes. 
<LIST ?FORT.MYACCT 
means list the filenames of all files ending with FORT in account MYACCT. 
Related Commands: 
LISTSTD, REVIEW, REVIEWSTD 
00002
00003
00001
00004
LISTSTD
Syntax: 
L[IST]S[TD] [(listopt)] stdfid[ {TO|ON|OVER|INTO} destination][ FROM]fid] 
Parameters: 
listopt   -   specifies either an A, C, EA, or FA listing format input option. 
stdfid   -   specifies an STD file containing a sourcelist for each record. 
If a source has an A, EA, FA, or C input option, the request overrides the 
default listing format. 
TO   -   specifies file creation (see Preposition Component). 
ON   -   specifies file creation (see Preposition Component). 
OVER   -   specifies file replacement (see Preposition Component). 
INTO   -   specifies file extension (see Preposition Component). 
destination   -   specifies the output for the listing operation.  This may be 
either a file, or a device stream.  The default is ME, which indicates the 
user's terminal (on-line) or the line printer (batch).  The CR, FA, O, TY, VC, 
VF, X, FV, NV and X1 are not valid output options for this command. 
FROM fid   -   specifies a default set of elements used when PCL parses the 
source parameters (see FROM Component). 
The default list option for single file specifications is A; for multiple 
specifications, the default is C=12. 
See the component description for SOURCE, DESTINATION, and FROM for detailed 
syntactical information. 
Description: 
LISTSTD prints a summary of disk and labeled tape storage with the sources 
defined in an STD file. 
LISTSTD functions identically to the LIST command, except that the sources are 
contained in an STD file rather than included as part of the command.  Note 
that the STD file is also listed. 
Examples: 
<COPY ME TO STANDARD1 
 .HELEN 
 .LESLIE 
 .<F> 
<LISTSTD STANDARD1 
Org  TY    Gran       NGAV     Rec      Last Modified      Name 
CON           1          0       2   07:59 MAY 05 '86      STANDARD1 
Key  SE       2          0       3   12:00 MAY 03 '86      HELEN 
Key  SE       2          0       3   11:40 MAY 03 '86      LESLIE 
 ..     3 files,     5 granules,      8 records listed 
< 
The user issues a COPY command that creates a consecutive file.  PCL prompts 
with a period (.) for each line.  The user types the file names and then types 
<ESC><F>, which prints an "<F>" to end the file.  The user then issues a 
LISTSTD command that lists the stdfile and the two files that are named in the 
stdfile. 
Related Commands: 
REVIEW, REVIEWSTD, LIST 
00002
00003
00001
00004
LISTSTD
Syntax: 
{MOD[IFY]|REN[AME]} sourcelist..TO destination[,sourcelist TO destination]... 
Parameters: 
sourcelist   -   specifies a list of disk files or ranges of disk files, 
separated by commas.  The following input options may be used with this 
command:  CRI, DATE, ORG, S, and TY.  Wildcard filenames are permitted. 
destination   -   specifies a file name, password, and or the attributes and 
access controls that are to be assigned to the disk files specified in the 
source parameters.  The special format of the destination parameter for the 
MODIFY command is: 
[{fid|wild}][(outopt[,outopt]...)] 
where 
fid   -   specifies a name and/or password to be associated with each modified 
file. 
wild   -   specifies a wildcard filename. 
outopt   -   specifies one of the following output options:  ACC, ACS, BA, GH, 
LR, LS, NBA, NR, RD, REB, REL, SPAR, TYP, VRD, VWR, WR, and XTN. 
NOTE:  The following rules apply to the use of the ACC option: 
1.  If the command specifies a single ACC option, that option will replace 
    existing accesses. 
2.  If the command specifies more than one ACC option and the first does not 
    have a + or -, existing accesses will be replaced by it.  Subsequent ACC 
    options in the same command that do not have a + or - will be treated as 
    if they had a +. 
Description: 
MODIFY alters the attributes and access controls of specified disk files. 
Note that the source and destination fids for the MODIFY command differ 
substantially from the source and destination fids in other PCL commands. 
Examples: 
<MODIFY SHEEP TO GOATS 
means change only the name of the file from SHEEP to GOATS, without having to 
wait for its contents to be copied. 
<MOD SECRET TO (RD=SAMMY) 
means set file access controls such that the file named SECRET will be 
readable by the account named SAMMY, as well as the creating account. 
<MOD SECRET TO (ACC(?)) 
makes file unreadable by all other accounts. 
NOTE:  The incantation MOD SECRET TO (RD=ALL) authorizes reading by all 
accounts. 
<REN ?_FORT TO ?_SI (TY=SF) 
means change the name of all files ending in _FORT so that they end in _SI, 
with the file type to be set to SF (source FORTRAN).  As each file is 
modified, the old and new names are displayed. 
<RENAME PERCH TO FISH, CHICKEN TO FOWL 
means change the names of PERCH to FISH, and CHICKEN to FOWL, with one 
command. 
Related Commands: 
NONE 
00002
00003
00001
00004
Syntax: 
MOU[NT] fid {[DE[NSITY]{=n|(n)}][,{R[ING]|N[ORING]}] [,REEL=(reel[,reel]...)]} 
            {[REEL=(reel[,reel]...)                                         ]} 
Parameters: 
fid   -   is a CP-6 tape fid. 
DENSITY   -   specifies the tape density.  Meaningful only if the RING option 
is also specified. 
RING   -   specifies that the tape is to be mounted with a write ring. 
NORING   -   specifies that the tape is to be mounted without a write ring. 
This is the default setting. 
REEL=reel   -   specifies which physical reels are to be mounted.  If only one 
reel is specified, the parenthesis may be omitted.  The maximum number of 
reels is ten. 
Description: 
MOUNT requests that a certain tape be mounted on the system tape drives. 
When MOUNT is issued, the operator is informed of the request.  No further 
commands can be issued until the requested mount has taken place.  If the 
BREAK key is struck while a MOUNT request is active, the request is 
terminated, and a cancellation message is sent to the operator. 
Examples: 
<MOUNT FT#1234 REEL=3 
<MOUNT LT#ABCD 
means mount reel 3 of the free tape #1234 and the labeled tape #ABCD. 
Related Commands: 
REMOVE, RELEASE 
00002
00003
00001
00004
Notation conventions used in command specifications and examples are listed 
below. 
  Convention          Meaning 
  CAPITAL LETTERS 
                      Capital letters must be entered as shown for input, and 
                      will be printed as shown in output. 
  lowercase letters 
                      Lowercase letters identify an element that must be 
                      replaced with a user-selected value. 
                      AP i could be entered as AP 2. 
  Special Characters 
                      Numbers that appear on the line (i.e., not subscripts), 
                      special symbols, and underlines appear as shown in 
                      output messages and must be entered as shown when input. 
                      #xxx could be entered as #011. 
  Brackets 
                      An element inside brackets ([]) is optional.  If 
                      elements are stacked vertically within brackets, the 
                      elements may be omitted or one of them may be entered. 
                      For example, 
                          [DISK] 
                          [TAPE] 
                      means that the user may omit this entry, or may enter 
                      DISK, or may enter TAPE. 
                      Alternatively, the vertical OR bar is used to separate 
                      the possible choices: 
                          [DISK|TAPE] 
                      When used to enclose keywords, brackets signify that the 
                      bracketed portion may be omitted, or truncated at any 
                      point.  For example, the notation K[EY] means that the 
                      user may enter K, KE, or KEY. 
  Braces 
                      Elements placed inside a pair of braces ({}) identify a 
                      required choice.  If elements are stacked vertically 
                      within braces, one of them must be entered.  For 
                      example, 
                          {id } 
                          {ALL} 
                      means that either a value for id or the word ALL must be 
                      entered. 
                      Alternatively, the vertical OR bar is used to separate 
                      the choices: 
                          {id|ALL}. 
  Or Bar 
                      The Or bar also separates elements in a required choice. 
                      {A|id}   -   means that either the letter A or the value 
                      of id must be entered. 
  Ellipsis 
                      The horizontal ellipsis indicates that a previous 
                      bracketed element may be repeated, or that elements have 
                      been omitted. 
                      option[,option]...   -   means that one or more options 
                      may be entered, with a comma inserted between each 
                      variable. 
  Careted Letters 
                      Letters inside carets indicate the keys on a physical 
                      terminal device. 
                      <ESC> <BS>   -   means press the escape key and then the 
                      backspace key. 
                      <CNTL-B>   -   means hold the control key down while 
                      pressing the B. 
                      Note that the control key is similar to the shift key: 
                      it does nothing on its own, but changes the meaning of 
                      the keys that are pressed while it is held down. 
  Keywords 
                      Keywords can be typed in uppercase or lowercase or a 
                      combination of both.  In this manual, keywords are 
                      always shown in uppercase. 
  Parameters 
                      Single parameters are connected to keywords in one of 
                      three ways: 
                      KEYWORD=parameter 
                      KEYWORD(parameter) 
                      KEYWORD=(parameter) 
                      A list of more than one parameter is connected to a 
                      keyword in one of two ways: 
                      KEYWORD(parameter,parameter) 
                      KEYWORD=(parameter,parameter) 
                      In this manual, the following forms are used: 
                      Single parameters:    KEYWORD=parameter 
                      Multiple parameters:  KEYWORD=(parameter,parameter) 
                                                       or 
                                            KEYWORD=(parameterlist) 
                      Multiple parameters are often referred to as lists, e.g. 
                      an optionlist is a list of options, separated by commas. 
  Double Quotes 
                      Comments within command streams are denoted by being 
                      enclosed in double quotes marks ("). 
  Apostrophe 
                      Strings that contain delimiters must be enclosed by 
                      apostrophes ('); if an apostrophe is part of a string, 
                      it is denoted by adjacent apostrophes (''). 
  Semicolon 
                      The semicolon is a continuation indicator for multiple 
                      line commands and for multiple commands on a single 
                      line.  The semicolon cannot be used for continuation 
                      inside a keyword or text string. 
00012
00005
00004
00001
00008
00011
00007
00009
00002
00006
00010
00013
00003
NOTATION
PREPOSITION
OPTIONS
Summaries of PCL options can be obtained by issuing the following HELP calls: 
HELP OPTIONS INPUT    Summary of input options. 
HELP OPTIONS ACCESS   Summary of access control output options. 
HELP OPTIONS FILE     Summary of file attribute output options. 
HELP OPTIONS TAPE     Summary of tape control output options. 
HELP OPTIONS VFC      Summary of vertical format control output options. 
HELP OPTIONS RECORD   Summary of record modification output options. 
HELP OPTIONS DISK     Summary of disk storage output options. 
HELP OPTIONS DUMP     Summary of dump format output options. 
HELP OPTIONS MISC     Summary of miscellaneous output options. 
PCL recognizes the following input options: 
ATTRIBUTES            List with attributes. 
BINARY                Read binary from CR or FT. 
BLOCK                 Tape block length. 
CLPOS                 Tape position upon CLOSE. 
COLUMNS               List in columns of width n. 
CREATOR               File selection by creator. 
CRITERIA              Establishes criteria for file search. 
CRPT                  File decryption. 
DATE                  File selection by date. 
DEOD                  Read from FT until double tape mark. 
EATTRIBUTES           List with extended attributes. 
EBCDIC                Translate EBCDIC to ASCII from FT. 
FSN                   Read files numbered n to m from tape. 
FATTRIBUTES           List with full attributes. 
FTORGANIZATION        Free tape organization. 
HEAD                  Force output of PCL header line. 
IGNOREFSN             Don't check file sequence before tape file is opened. 
IOERROK               Try to recover from I/O errors if possible. 
n1-n2                 Record selection by key or record position. 
NBINARY               Read non-binary from CR or FT. 
NBLOCKED              Free tape is not blocked. 
NCNVRT                Don't translate EBCDIC to ASCII from tape. 
NHEAD                 Suppress output of PCL header line. 
NSPANNED              Free tape is not spanned. 
ORGANIZATION          File selection by organization. 
PHYSICAL              Interpret tape file range literally. 
RECLENGTH             Tape maximum record segment length. 
SHARED                Permit shared access of input files. 
SORTEDBY              Changes the order in which selected 
                      files are processed. 
TRANSPARENT           Input without translation. 
TYPE                  File selection by file type. 
VOLUME                Initial volume access. 
For syntactic information type:   HELP INOPS option 
The following output options control file access: 
ACCESS                Account(s) and their access control(s). 
ACSVEHICLES           Processor(s) and their access control(s). 
READ                  Read permission for account(s). 
VREAD                 Read permission for processor(s). 
VWRITE                Write permission for processor(s). 
WRITE                 Write permission for account(s). 
For syntactic information type:    HELP OUTOPS option 
The following output options control file attributes: 
BACKUP                Automatic file backup when modified. 
EXPIRE                File expiration date. 
GHSTACS               Pass function code to system access ghost 
                      before opening disk file DCB. 
KEYLENGTH             Number of columns for index key. 
KEYX                  Column position for index key. 
LN                    Concatenate producing an EDIT file. 
LRDL0                 Number of contiguous blocks. 
LSLIDE                Number of blocks. 
NBACKUP               Don't backup file when modified. 
NFATTRIBUTES          Transfer no file attributes. 
NLN                   Concatenate files into consecutive file. 
NLOAD                 Suppress loading of upper level indices. 
NUMRECORDS            Number of records in relative file. 
ORGANIZATION          File organization. 
RECLENGTH             Maximum record length. 
SPARE                 Spare space at end of index block. 
TYPE                  Two character file type. 
For syntactic information type:    HELP OUTOPS option 
The following output options control tape file handling: 
BLOCK                 Maximum block size for tape. 
DENSITY               Tape density. 
EBCDIC                Write tape in EBCDIC. 
IOERROK               Try to recover from I/O errors if possible. 
MAXVOL                Maximum number of tape volumes. 
NBLOCKED              Don't block tape output. 
NCNVRT                Don't translate data to EBCDIC. 
NSPANNED              Don't span records on LT. 
VOLACCESS             Tape volume protection:  ALL, NONE, or IN. 
VOLUME                Which reel to access initially. 
XTEND                 Write at end of labeled tape. 
For syntactic information type:    HELP OUTOPS option 
The following output options control vertical formatting on unit-record 
devices: 
DSP                   Double-space output. 
FVFC                  Translate FORTRAN VFC characters. 
NVFC                  Write without vertical format control. 
SSP                   Single-space output. 
SVFC                  Write without vertical format control, 
                        strip the VFC character. 
VFC                   Write with vertical format control. 
For syntactic information type:    HELP OUTOPS option 
The following output options control record modification. 
BINARY                Write binary. 
CR                    Retain carriage returns and line feeds. 
CRPT                  File encryption. 
CS                    Card sequencing. 
KEYS                  Write keys in output record. 
LC                    Translate upper case to lower case. 
NBINARY               Write non-binary. 
NBLANKS               Strip blanks from end of record. 
NCR                   Strip carriage return and linefeed. 
NCS                   Write blanks in columns 73 to 80. 
NTRANSPARENT          Output with translation. 
RECSIZE               Truncate or pad records to value size. 
TRANSPARENT           Output without translation. 
TX                    Tab expansion. 
UC                    Translate lower case to upper case. 
For syntactic information type:    HELP OUTOPS option 
The following output options control disk storage allocation: 
COMPRESSED            Write in compressed format. 
IXTNSIZE              Initial disk storage allocation. 
NCOMPRESSED           No compression on output. 
NRELEASE              Don't release excess disk storage. 
RELEASE               Release excess disk storage. 
XTNSIZE               Secondary disk storage allocation. 
For syntactic information type:    HELP OUTOPS option 
The following output options display files in octal and hexadecimal format: 
OCTAL                 Octal format dump. 
X                     X format hexadecimal dump. 
X1                    X1 format hexadecimal dump. 
For syntactic information type:    HELP OUTOPS option 
The following output options, though important, do not fall neatly into any 
category: 
AMR                   Use assign merge record. 
HEAD                  Force output of PCL header line. 
FORM                  Specifies form to be mounted on unit record device. 
NEWKEY                Prevent overwrite of existing keys. 
NHEAD                 Suppress PCL header line. 
NPAGE                 Suppress new page on file output. 
NSUMMARY              Suppress summary line in LIST command. 
NWRAP                 No wrapping on output. 
PAGE                  Force page eject for new files. 
REBUILD               Rebuild upper-level index structure. 
SAVE                  Cause output to be saved in case of interrupt. 
SHARED                Allow shared access of output file. 
SUMMARY               Force summary line upon LIST command. 
WIDTH                 Specifies width of output file. 
WRAP                  Determines wrapping method for output. 
For syntactic information type:    HELP OUTOPS option 
00002
00007
00008
00003
00001
00009
00006
00004
00005
OUTPUT_OPS
File Access Output Options:  ACCESS, ACSVEH, READ, VREAD, VWRITE, WRITE. 
File Attribute Output Options:  BACKUP, EXPIRE, GHSTACS, KEYLENGTH, KEYX, LN, 
LRDL0, LSLIDE, NBACKUP, NFATTRIBUTES, NLN, NLOAD, NUMRECORDS, ORGANIZATION, 
RECLENGTH, SPARE, TYPE. 
Tape File Output Options:  BLOCK, DENSITY, EBCDIC, IOERROK, MAXVOL, NBLOCKED, 
NCNVRT, NSPANNED, VOLACCESS, VOLUME, XTEND. 
Vertical Format Control Output Options:  DSP, FVFC, NVFC, SSP, SVFC, VFC. 
Record Modification Output Options:  BINARY, CR, CRPT, CS, KEYS, LC, NBINARY, 
NBLANKS, NCR, NCS, NTRANSPARENT, NWRAP, RECSIZE, TRANSPARENT, TX, UC, WIDTH, 
WRAP. 
Disk Storage Output Options:  COMPRESSED, IXTNSIZE, NCOMPRESSED, NRELEASE, 
RELEASE, XTNSIZE. 
Dump Format Output Options:  OCTAL, X, X1. 
Miscellaneous Output Options:  AMR, COPIES, FORM, HEAD, NEWKEY, NSUMMARY, 
NHEAD, NPAGE, PAGE, REBUILD, SAVE, SHARE, SUMMARY. 
To obtain HELP messages for these options, type: 
HELP OUTOPS option The options are described with the following structure: 
  Option        Meaning 
  ACC[ESS][{+|ADD|-|DELETE}]={ALL|((a[,a]...])[,c]...)} 
           Specifies which account(s) are permitted access to the file, and 
           what controls (c) apply to those accounts.  An account is defined 
           as any valid CP-6 account or the following special cases: 
           1.  If ALL is specified, all accounts on the system are controlled. 
           2.  Wildcarded accounts; these function identically to wildcard 
           file names. 
           The controls are listed below. 
           MNEMONIC        MEANING 
           --------        ------- 
           AU              Meaningful for comgroups only.  If set, this 
                           user is allowed to be the administrative user 
           AURD            Meaningful for comgroups only.  If set, this 
                           user is allowed to issue monitor services 
                           normally reserved for the administrative user 
                           that examine but do not change the comgroup. 
           DELF[ILE]       Permitted to delete file, change file name, 
                           password, ACCESS and ACSVEH. 
           DELR[ECORDS]    Permitted to delete records. 
           E[XECUTE]       Permitted to execute only; access to file 
                           depends on the process opening the file. 
           N[OLIST]        Forbidden to access the file in 
                           any way, even to know that it 
                           exists. 
           READ            Permitted to read records. 
           REAT[TRIBUTES]  Permitted to change file attributes with the 
                           exception of ACCESS and ACSVEH (see DELF above) 
           TCTL            Meaningful for comgroups only.  If set, this 
                           user is allowed to issue terminal control 
                           monitor services (such as M$PROMPT and 
                           M$STRMATTR).  For ORG=FPRG comgroups, M$SETFP 
                           is allowed. 
           U[PDATE]        Permitted to overwrite existing records. 
           W[NEW]          Permitted to write new records. 
           NOTE:  If only one account is specified, it need not be enclosed in 
           parentheses; the parentheses that enclose the entire field after 
           the "equal" sign are required. 
           3.  ADD or +    specifies that the file controls following are to 
           be added to the list of existing controls. 
           The addition operation searches the existing control list for a 
           matching account to be controlled.  If a match is found, the file 
           controls are added. 
           4.  DELETE or -    specifies that the file controls following are 
           to be deleted from the list of existing controls. 
           The delete operation searches the existing control list for a 
           matching account to be deleted.  If a match is found, the specified 
           options are deleted.  If no match is found, an error is reported. 
           NOTE:  All account access control options may be repeated as 
           desired to a maximum of 20 entries. 
  ACS[VEHICLES][{+|ADD|-|DELETE}]=((p[,p]...)[,c]...) 
           Specifies which processors (p) are permitted access to the file, 
           and which controls (c) apply to those processors.  A processor is 
           defined as any run unit with optional account specification.  If 
           the account is not specified, :SYS is assumed (BASIC, EDIT, etc.). 
           If a period (.) follows the name, but no account is specified, the 
           processor must exist in the same account as the file.  The controls 
           are described in the ACCESS option. 
           If only one processor is specified, it need not be enclosed in 
           parentheses; the parentheses that enclose the entire field after 
           the "equal" sign are required. 
           ADD or +    specifies that the file controls following are to be 
           added to the list of existing controls. 
           The addition operation searches the existing control list for a 
           matching processor to be controlled.  If a match is found, the file 
           controls are added. 
           DELETE or -    specifies that the file controls following are to be 
           deleted from the list of existing controls. 
           The delete operation searches the existing control list for a 
           matching processor to be deleted.  If a match is found, the 
           specified file controls are deleted.  If no match is found, an 
           error is reported. 
           NOTES: 
           1.  All access vehicle options may be repeated as desired to a 
               maximum of 200 bytes (where length of each entry is 
               LENGTH(p)+3). 
           2.  For name abbreviation as applied to ACSVEHICLES, only a 
               trailing question mark on the name portion is honored. 
           3.  In order to preclude file security problems, run units used as 
               access vehicles must reside in accounts which have been added 
               to the Master Account Directory (MAD), or the check for access 
               vehicles will not be performed when the file is opened, i.e., 
               file management will open the file as though it had no access 
               vehicle control list. 
  ALT[BLD] 
           For COPY, COPYALL, COPYSTD, and MODIFY operations on Indexed and 
           IREL disk files with alternate indexes, specifies that the 
           alternate indexes are to be built/rebuilt when the file is closed. 
           See CE74, Host Monitor Services Reference, under M$CLOSE, ALTBLD 
           parameter.  Default for copy operations is to build/rebuild the 
           alternate indexes unless the NLOAD output option is specified. 
           Default for MODIFY operations is not to build/rebuild the alternate 
           indexes. 
  AM[R] 
           Specifies that the assign-merge record for the output DCB is to be 
           used.  The M$EO DCB is used for the COPY command; the M$EO1 DCB is 
           used for the COPYALL, COPYSTD, LIST, and LISTSTD commands. 
  BA[CKUP] 
           Specifies that the file will be automatically backed up when 
           modified.  See the NBACKUP option.  The default is individually set 
           by account when each account is created. 
  BIN[ARY] 
           Specifies that all records are to be written as binary data.  The 
           default is for records to be written in the same form as they were 
           input. 
  BL[OCK]=value 
           Sets the maximum block size for files on tape.  The size is 
           expressed in number of bytes per block.  If BLOCK is not specified, 
           and NBLOCKED is not specified, a format-dependent default will be 
           supplied.  The maximum is also format dependent.  See Appendix E, 
           tables E-3 and E-4, for format-dependent defaults and maximum 
           values. 
  C[OMPRESSED] 
           Specifies that the output disk file is to be written in compressed 
           format. 
  COPIES=n 
           Specifies the number of copies of this file to be printed.  This 
           value is passed to M$OPEN as FPT_OPEN.V.COPIES#. 
  CR 
           Specifies that the activation characters carriage return and line 
           feed are to be retained at the end of each record.  This is the 
           default except in the case of terminal input.  See the NCR option. 
  CRPT=octal value 
           Specifies the encryption seed for the output file.  The value must 
           range from 0 through 777777777777, or be a one to four-character 
           string enclosed in single quotes.  The default is no encryption 
           (CRPT=0). 
  CS[=([id][,[n][,i]])] 
           Specifies that card sequencing is to take place in columns 73 to 80 
           of each record.  The id specifies up to 4 characters of 
           user-selected identifier that is written, left justified at column 
           73; if omitted no identifier is written.  In the remaining 4 or 
           more columns, ending in column 80, a sequence number is written, 
           beginning with value n with increments of i.  The default values 
           for n and i are 0 and 1. 
  DE[NSITY]=value 
           Specifies the tape recording density.  Valid densities are: 556, 
           800, 1600, or 6250. 
  DS[P] 
           Causes output to be double-spaced. 
  EB[CDIC] 
           Specifies that the labels on labeled tape are to be written in 
           EBCDIC; data will also be written in EBCDIC unless NCN is included 
           as one of the output options.  Valid only for labeled tape (LT) 
           file types V, F, and U and free tape (FT). 
  EXP[IRE]=date 
           Specifies the expiration date of the file.  The date may be either 
           an actual date of the form mm/dd/yy, a number of days from today in 
           the form nnn, NEVER, or TODAY. 
  FO[RM]='formname' 
           Specifies the name of a form to be mounted on a unit record device. 
           formname   -   is a quoted 1 to 6 character string.  The name must 
           have been defined to the system by the system manager (via the Form 
           Definition File).  The default is blank, which means default form 
           for the unit record devices and form 'STDLP' for unit record files. 
           FORM applies to unit record files and unit record devices. 
  F[VFC] 
           Causes any FORTRAN VFC characters on records built with VFC 
           specified, to be translated into their CP-6 equivalents as shown 
           below.  Will affect all records if VFC option is also used. 
           FORTRAN   STANDARD CP-6   FUNCTION 
           -------   -------------   -------- 
            +              `         No space. 
            0              b         Space twice before printing. 
            1              0         Skip to top of form before printing. 
            SP             a         Space once before printing. 
           All other VFC characters remain the same. 
  GH[STACS] = value 
           Specifies a function code to be passed to the system access ghost 
           prior to opening the DCB to a disk file.  The only currently 
           implemented code is JRNLOPN, which asks the ghost to open a 
           journal, either as the owner of this journal or to journal this 
           comgroup.  The value NONE may be used to reset to zero a previous 
           non-zero value (either in the DCB for M$OPEN, or in the file for 
           M$CLOSE).  The default causes this parameter to be ignored. 
  H[EAD] 
           Specifies that the PCL header line for this source is to be output 
           regardless of the device type. 
  IO[ERROK] 
           This option is meaningful only for labelled tape files.  With this 
           option, tape file management tries to recover from I/O errors as 
           completely as possible.  The action taken depends on the operation 
           in progress at the time of the error.  If tape errors occur and 
           IOERROK is specified, the errors will not be reported, and some 
           records may be missing or garbled. 
  I[XTNSIZE]=value 
           Specifies an initial disk storage allocation (in blocks) for the 
           output file.  Value must be in the range of 1 through 134217727; if 
           this option is not specified, a value of 2 is assigned. 
  KEYL[ENGTH]=value 
           Specifies the number of characters for the key in an indexed file. 
           The value can range from 1 to 255.  Default value is 1.  Used with 
           the KEYX option below. 
  K[EYS][=][opt|(opt[,opt[,...])] 
           Specifies that for each input record, the logical sequence number 
           (if known) and key (if one exists) are to be written as part of the 
           output record.  If the key can be represented as an EDIT key, the 
           logical sequence number and key are output, preceding the input 
           record.  This can be overridden with the ONDATA suboption. 
           If the key cannot be represented as an EDIT key, the key and 
           logical sequence number are written as a separate record preceding 
           the input record.  If KEYS is included among the output options for 
           a LIST or LISTSTD command, the output file's logical record number 
           precedes the list record. 
           opt     stands for sub-options which fall into the categories shown 
           below.  Defaults for all options are listed at the very end. 
           Key Formatting: 
           C[HARACTER]    The key is displayed as a string of characters. 
           E[DIT]    The key is displayed in the style of EDIT. 
           OCT[AL]    The key is displayed in octal. 
           ONDATA    Record attribute information appears on the same line as 
           the actual record.  This information includes key, sequence number, 
           DVBYTE, and record size. 
           NOONDATA    Record attributes are written as a separate record 
           preceding the input record.  ONDATA and NOONDATA are mutually 
           exclusive. 
           X    The key is displayed in hexadecimal format. 
           X1    The key is displayed in hexadecimal X1 format.  Eight out of 
           every nine bits are displayed in hex.  The high-order bit of each 
           byte is omitted. 
           S[EQUENCE] [NUMBER]    The record sequence number is displayed. 
           If any key-formatting option is not appropriate for a given record 
           it is ignored without printing an error message.  For example, for 
           the EDIT suboption, KEYs will not attempt to print an EDIT key if 
           the key is not three bytes long. 
           The user may request as many key formats as desired.  If one or 
           more of these options are selected, the specified set takes the 
           place of the default set. 
           DVBYTE Control: 
           N[O] DV[BYTE]    Suppresses the display of flags from the record's 
           DVBYTE. 
           DV[BYTE]    Requests the display of flags from the record's DVBYTE. 
           These options are mutually exclusive. 
           Record Size Display: 
           N[O] REC[SIZE]    Disables the printing of the record size. 
           REC[SIZE]    Requests that PCL print the record size.  These 
           options are mutually exclusive. 
           Defaults: 
           1.  If the OCTAL, X, or X1 PCL output dump options are specified, 
           the defaults are:  SEQUENCE NUMBER, EDIT, OCTAL, CHARACTER, DVBYTE, 
           RECSIZE, NOONDATA. 
           2.  IF K is specified without options, and the key is three bytes 
           long, the defaults are:  SEQUENCE NUMBER, EDIT, NO DVBYTE, 
           NO RECSIZE, ONDATA. 
           3.  IF K is specified without options, and the key is not three 
           bytes long, the defaults are:  SEQUENCE NUMBER, EDIT, OCTAL, 
           CHARACTER, DVBYTE, RECSIZE, NOONDATA. 
  KEYX=value 
           Specifies a character position at which the key for an indexed file 
           is to be located.  The value can range from 0 to 32767.  Used with 
           the KEYL option above. 
  LC 
           Specifies that all upper case letters are to be translated into 
           lower case.  The default is no translation. 
  LN[=(n[,i])] 
           Specifies that the input files are to be concatenated into an EDIT 
           keyed file with an initial key of n, and successive keys 
           incremented by i.  EDIT keys are described in Section 4.  The 
           default for both n and i is 1. 
  LR[DL0]=value 
           Specifies the number of contiguous blocks that can be added to the 
           KEYED or INDEXED disk file's level 0 index since the current 
           higher-level index structure was created.  If the specified number 
           is exceeded, the higher-level index structure is rebuilt when the 
           file is closed.  Values can range from 1 to 511.  A value of 511 
           means that the upper level will not be rebuilt.  The default is 3. 
  LS[LIDE]=value 
           Specifies the number of blocks that can be added to the KEYED or 
           INDEXED disk file's level 0 index since the current higher-level 
           index structure was created.  If the specified value is exceeded, 
           the higher-level index structure will be rebuilt when the file is 
           closed.  If a value of 511 is specified, the higher-level index 
           structure is not rebuilt.  Values can range from 1 to 511.  The 
           default value is 510. 
  M[AXVOL]=value 
           Specifies the maximum number of additional tape volumes that can be 
           accumulated as part of the volume set.  The value must be in the 
           range of 1 to 511.  The default is 511.  Valid only for labeled 
           tape. 
  NALT[BLD] 
           For COPY, COPYALL, COPYSTD, and MODIFY operations on Indexed and 
           IREL disk files with alternate indexes, specifies that the 
           alternate indexes are not to be built/rebuilt when the file is 
           closed.  See CE74, Host Monitor Services Reference, under M$CLOSE, 
           ALTBLD parameter. Default for copy operations is to build/rebuild 
           the alternate indexes unless the NLOAD output option is specified. 
           Default for MODIFY operations is not to build/rebuild the alternate 
           indexes. 
  NBA[CKUP] 
           Specifies that the file is not to be automatically backed up when 
           it is modified.  The default is individually set by account when 
           each account is created. 
  NBIN[ARY] 
           Specifies that all records are to be written as non-binary data. 
           The default is for records to be written in the same form as they 
           were input. 
  NB[LANKS] 
           Specifies that blanks are to be stripped from the end of each 
           record.  If both NB and NCR are included among the output options, 
           the stripping of carriage returns is accomplished before the 
           stripping of blanks.  If NBLANKS and RECSIZE are specified, RECSIZE 
           acts as a maximum record length.  Note that NB can remove a blank 
           in column 1. 
  NBLO[CKED] 
           Specifies that tape output is not to be blocked.  See the BLOCK 
           option. 
  NCN[VRT] 
           Specifies that data is not to be translated into EBCDIC format on 
           an EBCDIC labeled tape.  Valid only for labeled tape and only when 
           the EBCID option is included among the output options. 
  NCO[MPRESSED] 
           Specifies that the output to a disk file is to be written in a 
           decompressed format. 
  NCR 
           Specifies that the activation characters carriage return and line 
           feed are to be stripped from the end of each records.  This is the 
           default for terminal input. 
  NCS 
           Specifies that blanks are to be written in columns 73 to 80 of each 
           record. 
  NE[WKEY] 
           Causes an error condition if an attempt is made to overwrite a 
           record in a KEYED, INDEXED, IREL, or RELATIVE file.  If not 
           specified, a record in the output file is replaced by any record 
           with the same key. 
  NFA[TTRIBUTES] 
           Causes no file attributes to be transferred to the output file. 
           Normally, all file attributes are copied across (including file 
           password) unless NFA is specified. 
  NH[EAD] 
           Specifies that the PCL header line for this source is to be 
           suppressed regardless of the device type. 
  NLN 
           Specifies that the input files are to be concatenated into a 
           consecutive file.  Identical to OR=CONSECUTIVE.  See the 
           ORGANIZATION option. 
  NL[OAD] 
           Specifies that alternate indicies are to be built as the records 
           are written, rather than when the file is closed.  Valid for files 
           with alternate indices only. 
  NP[AGE] 
           Suppress page ejection between files on UR output regardless of 
           HEAD option. 
  NR[ELEASE] 
           Specifies that excess disk storage space is not to be released when 
           the output file is closed.  See the RELEASE option. 
  NS[PANNED] 
           Specifies that records are not to be spanned.  Spanned records may 
           be divided between physical tape records and may exceed the record 
           size specified in the RECLENGTH option.  Valid only for labeled 
           tape or managed free tape. 
  NSU[MMARY] 
           Specifies that on a LIST command the summary line is to be 
           suppressed. 
  NT[RANSPARENT] 
           If NTRANSPARENT is specified, the data is sent with the normal 
           translation, which is as follows.  For magnetic tape, translation 
           to EBCDIC occurs if EBCDIC=YES or CNVRT=YES was specified when the 
           file was opened.  For unit record devices, blanks replace any 
           non-printable characters.  For TERMINAL organization, the handler 
           performs translation appropriate to the terminal type. 
           NTRANSPARENT is the default; see TRANSPARENT option. 
  NUMR[ECORDS]=value 
           Specifies the number of records in a relative output file. 
  NV[FC] 
           Causes all output records to be written without vertical format 
           control applied, thus leaving PCL to generate records with VFC if 
           it wants.  The VFC character, if present, remains in the record. 
  NW[RAP] 
           Specifies that the output is not to be wrapped.  Default is NWRAP. 
  O[CTAL][{=dumpopt|[=](dumpopt[,dumpopt]...)}] 
           Causes the input files to be output in an octal format dump.  The 
           header describes the record number, length in bytes, and VFC, 
           BINARY, and/or TRANSPARENT attributes of the input record, if 
           applicable.  If NOTEXT is included, no textual representation is 
           included following the octal representation.  Dump formatting takes 
           place after other record modifications.  Dump records will be 
           flagged if the record was written in TRANSPARENT, BINARY, or VFC 
           modes. 
           dumpopt may be any of the following: 
           DU[PLICATES]    Suppresses compaction of repeated data. 
           NDU[PLICATES]    Compacts duplicate values to save space. 
           Compaction is marked by an asterisk (*) following the address 
           field. 
           TE[XT]    Text is included in the dump format.  ASCII characters SP 
           through "~" ('040'O through '176'O) are considered printable.  All 
           other characters are represented with a "." 
           N[OTEXT]    No textual representation is included following the 
           octal representation. 
           The defaults are TEXT and NDUPLICATES. 
  OR[GANIZATION]=org 
           Specifies the organization of the output file.  Valid organizations 
           are: 
           C[OM]G[ROUP] 
           C[ONSECUTIVE] 
           DBGCG 
           DBGDCB 
           DBGSYSID 
           F[IXED] 
           FO[RM] 
           F[ORMS]P[ROGRAM] 
           FR[EE] 
           HA[NDLER] 
           ID[S] 
           IN[DEXED] 
           I[NDEXED] R[ELATIONAL] 
           K[EYED] 
           RA[NDOM] 
           REL[ATIVE] 
           RES[TRICTED] 
           S[CREEN] E[DIT] 
           S[YMBIONT] 
           T[ERMINAL] 
           U[NIT]R[ECORD] 
           UN[DEFINED] 
           V[ARIABLE] 
           X364 
           NOTE:  ORG=KEYED causes the output file to be keyed with EDIT keys 
           and is a synonym for LN.  Similarly, ORG=IDS and ORG=RANDOM ignore 
           the input keys and write the records with consecutive output keys. 
  P[AGE] 
           Force a new page for each new output file in a copy to UR file 
           regardless of HEAD option. 
  {(RD|REA[D])}[{+|A[DD]|-|D[ELETE]}]={ALL|(a[,a]...)} 
           Specifies which accounts can read records from the file.  ALL 
           specifies that any account can read this file.  However, NONE is 
           considered a valid account.  The RD option is identical to 
           ACC=((a[,a]...),READ).  If only one account is specified, the 
           parentheses are optional. 
           ADD or + specifies that the file controls following are to be added 
           to the list of existing controls. 
           The addition (ADD or +) operation searches the existing control 
           list for a matching account to be controlled.  If a match is found, 
           the file controls are added. 
           DELETE or - specifies that the file controls following are to be 
           deleted from the list of existing controls. 
           The delete operation searches the existing control list for a 
           matching account to be deleted.  If a match is found, the specified 
           file controls are deleted.  If no match is found, an error is 
           reported. 
           NOTE:  All account control options may be repeated as desired to a 
           maximum of 20 entries. 
  REB[UILD] 
           Specifies in COPY type and MODIFY operations that the upper level 
           index structure is to be rebuilt.  In some circumstances, this may 
           result in an increase in granule size by one.  See HELP (HOSTMON) 
           M$CLOSE REBLD. 
  RECL[ENGTH]=value 
           For fixed record length formats such as RELATIVE and FIXED, the 
           RECL option is the maximum record length in bytes.  For variable 
           record length TAPE formats such as CONSEC, KEYED, and VARIABLE, the 
           RECL option is the maximum record segment length in bytes.  For 
           unspanned files, a record may not exceed the length of a record 
           segment.  Records exceeding this length are truncated. 
           All variable record length TAPE formats include control information 
           bytes with the data record; these require 4 bytes except for format 
           D (non-EBCDIC, SPANNED,VARIABLE) which requires 5 bytes.  For KEYED 
           tape files, the key is included with the record and must be 
           accounted for when choosing RECL.  If no record length is 
           specified, a format dependent default will be supplied.  The 
           maximum is also format dependent. 
           See Appendix E, tables E-3 and E-4, for format-dependent defaults 
           and maximum values. 
           For all TAPE format records which include control information bytes 
           with the record, the number of control bytes must be accounted for 
           in determining the record length.  For example, if 4 bytes are 
           required, a RECLENGTH=80 will accommodate a record of only 76 
           bytes. 
  RECS[IZE][=]{(min)|(min-)|(-max)|(min-max)} 
           Specifies that all records will be between the min and max bytes 
           long.  Records shorter than the min will be padded with blanks on 
           the right.  Records longer than the max are truncated.  Records 
           within the range are unaffected.  User may specify minimum size 
           (min-) or maximum size (-max) or force a specific size (min). 
           Valid values are 0 through 99999 and max must be equal to or larger 
           than min.  This action takes place before card sequencing (see the 
           CS option) and the addition of keys (see the KEYS option).  The 
           stripping of blanks (see NB option) occurs after tab expansion (see 
           TX option).  The default is not truncation or padding.  The VFC 
           character, if present in the record, is not counted as part of the 
           record. 
  REL[EASE] 
           Specifies that excess disk storage space is to be released.  The 
           default is RELEASE. 
  SA[VE] 
           Specifies that in the event of an error or break condition, the 
           output stream of the current command is saved.  Also causes the 
           stream to continue when minor errors occur on a COPYALL. 
  SH[ARED] 
           Specifies that other users can access the output disk file while it 
           is being written. 
  SPAR[E]=value 
           Specifies in words the amount of spare space to be left unused at 
           the end of each index block while a KEYED or INDEXED disk file is 
           being created or updated with sequential access.  The value 
           specified may not exceed 511 words.  This spare space is used so 
           that additional keys can be inserted in a minimum time when 
           updating the file with direct access (as in EDIT).  If the file 
           will never be updated with direct access, a spare value of 1 should 
           be specified. 
           The default (zero) means use the existing value in the DCB.  If a 
           DCB has never been opened by a program, the default is 1. 
  SS[P] 
           Causes output to be single-spaced. 
  SU[MMARY] 
           Specifies that the LIST command will produce a summary line 
           regardless of destination. 
  SV[FC] 
           Causes all output records to be written without vertical format 
           control applied, thus leaving PCL to generate records with VFC if 
           it wants.  The VFC character, if present, is stripped from the 
           record before the record is written. 
  TR[ANSPARENT] 
           Specifies output without translation.  Primarily useful for output 
           organizations which normally perform character translation. 
  TY[PE]=ty 
           Specifies the file type for the output file.  See input option TYPE 
           for type meanings. 
  TX 
           Specifies that tab expansion is to take place in writing tab 
           characters to the output file.  Tab stops in PCL are set via the TX 
           command.  If no TX command has been issued, the IBEX tab stops are 
           used.  If no tab stops are set, a blank is generated for each tab 
  UC 
           Specifies that all lower case letters are to be translated into 
           upper case.  The default is no translation. 
  VF[C] 
           Causes the output to be written with the first character of each 
           record as a vertical format control (VFC) character.  VFC 
           characters are described in Appendix C.  The default is that 
           records created with VFC are written with it; records created 
           without VFC are written without it. 
  {VRD|VREA[D]}[{+|A[DD]|-|D[ELETE]}]=(p[,p]...) 
           Specifies which processor can read records from the file.  The VRD 
           option is identical to ACS=((p[,p]...),READ).  If only one 
           processor is specified, the parentheses are optional. 
           ADD or + specifies that the file controls following are to be added 
           to the list of existing controls. 
           The additional (ADD or +) operation searches the existing control 
           list for a matching processor to be controlled.  If a match is 
           found, the file controls are added. 
           DELETE or - specifies that the file controls following are to be 
           deleted from the list of existing controls. 
           The delete operation searches the existing control list for a 
           matching processor or account to be deleted.  If a match is found, 
           the specified file controls are deleted.  If no match is found, an 
           error is reported. 
           NOTE:  All access vehicle options may be repeated as desired to a 
           maximum of 200 bytes (where length of each entry is LENGTH(p)+3). 
  VWR[ITE][{+|ADD|-|DELETE}]=(p[,p]...) 
           Specifies which processor can write records to the file.  The VWR 
           option is identical to 
           ACS=((p[,p]...),READ,DELR,WNEW,UPD,DEL,REATTR).  If only one 
           processor is specified, the parenthesis are optional. 
           ADD or + specifies that the file controls following are to be added 
           to the list of existing controls. 
           The addition operation searches the existing control list for a 
           matching processor to be controlled.  If a match is found, the file 
           controls are added. 
           DELETE or - specifies that the file controls following are to be 
           deleted from the list of existing controls. 
           The delete operation searches the existing control list for a 
           matching processor to be deleted.  If a match is found, the 
           specified file controls are deleted.  If no match is found, an 
           error is reported. 
           NOTE:  All access vehicle options may be repeated as desired to a 
           maximum of 200 bytes (where length of each entry is LENGTH(p)+3). 
  VOLA[CCESS]={A[LL]|N[ONE]|I[N]} 
           Specifies volume access mode: 
           IN   -   specifies that only the owner (creator, i.e. user who 
           wrote the first file on the volume set) can write to these volumes. 
           The system identifies the owner by account only, not account and 
           name. 
           NONE   -   specifies that only the owner can read from or write to 
           these volumes. 
           ALL   -   specifies that any account can read from or write to 
           these volumes.  The default is ALL. 
  VO[LUME]=value 
           Specifies which reel in a multivolume tape set is to be accessed 
           initially.  Valid only for labeled tape. 
  WI[DTH]=value 
           Specifies number of characters wide for output (destination). 
           Default is from the DCB. 
  WRA[P] 
           PCL wraps the output at the specified WIDTH.  The default is NWRAP, 
           unless the destination is a unit-record (UR) file or device, in 
           which case WRAP is the default. 
  WR[ITE][{+|A[DD]|-|D[ELETE]},]={ALL|(a[,a]...)} 
           Specifies which accounts can write records to the file.  ALL 
           specifies that any account can write to this file.  However, NONE 
           is considered a valid account.  The WR option is identical to 
           ACC=((a[,a]...), READ,DELR,WNEW,UPD,DELF,REATTR).  If only one 
           account is specified, the parentheses are optional. 
           ADD or + specifies that the file controls following are to be added 
           to the list of existing controls. 
           The addition (ADD or +) operation searches the existing control 
           list for a matching processor to be controlled.  If a match is 
           found, the file controls are added. 
           DELETE or - specifies that the file controls following are to be 
           deleted from the list of existing controls. 
           The delete operation searches the existing control list for a 
           matching processor to be deleted.  If a match is found, the 
           specified file controls are deleted.  If no match is found, an 
           error is reported. 
           NOTE:  All account control options may be repeated as desired to a 
           maximum of 20 entries for account control information. 
  XTE[ND] 
           Prevents overwrite of other files on the tape by writing the output 
           file at the end of the labeled tape.  If unspecified, the write 
           occurs at the current tape position.  Valid only for labeled tape. 
  X[{=dumpopt|[=](dumpopt[,dumpopt]...)}] 
           Specifies that the input files are to be output in an X format 
           hexadecimal dump.  The X format is 9 hexadecimal digits per 36 
           bits, with one ASCII character per eight bits.  The grouping and 
           counting is handled in 36-bit words.  The header describes the 
           record number, length in words, and VFC, BINARY, and/or TRANSPARENT 
           attributes of the input record, if applicable.  If NOTEXT is 
           included, no textual representation is included following the 
           hexadecimal representation.  Dump formatting takes place after 
           other record modifications.  Dump records will be flagged if the 
           record was written in TRANSPARENT, BINARY, or VFC modes. 
           dumpopt     may be any of the dumpopt suboptions listed under the 
           X1 option. 
  X1[{=dumpopt|[=](dumpopt[,dumpopt]...)}] 
           Specifies that the input files are to be output in an X1 format 
           hexadecimal dump.  The X1 format is a hexadecimal dump using the 
           lower eight bits of each nine, grouping and counting in units of 18 
           bits (which appear as 16 bits).  The header describes the record 
           number, length in words, and VFC, BINARY, and/or TRANSPARENT 
           attributes of the input record, if applicable.  If NOTEXT is 
           included, no textual representation is included following the 
           hexadecimal representation.  Dump formatting takes place after 
           other record modifications.  Dump records will be flagged if the 
           records was written in TRANSPARENT, BINARY, or VFC modes. 
           dumpopt may be any of the following: 
           DU[PLICATES]    Suppresses compaction of repeated data. 
           NDU[PLICATES]    Compacts duplicate values to save space. 
           Compaction is marked by an asterisk (*) following the address 
           field. 
           TE[XT]    Text is included in the dump format.  ASCII characters SP 
           through "~" ('040'O through '176'O) are considered printable.  All 
           other characters are represented with a "." 
           N[OTEXT]    No textual representation is included following the 
           octal representation.  The defaults are TEXT and NDUPLICATES. 
  XTN[SIZE]=value 
           For files other than RANDOM, IDS, and RELATIVE, this option 
           specifies a secondary disk storage allocation (in blocks) for the 
           output file; value must be in the range of 1 through 32000. 
           Default value for XTNSIZE is 2. 
           For RANDOM, IDS, and RELATIVE files, no extension will be performed 
           unless this option is specified with a valid value.  Use of this 
           option causes an automatic M$EXTEND when needed. 
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
00018
00017
00018
00019
00020
00022
00021
00022
00024
00023
00024
00025
00026
00027
00028
00029
00030
00031
00034
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
00044
00043
00044
00045
00046
00047
00048
00049
00050
00051
00052
00053
00054
00055
00056
00056
00057
00058
00059
00060
00061
00062
00063
00064
00065
00066
00067
00069
00068
00070
00071
00075
00074
00075
00072
00072
00073
00076
00078
00077
00078
00080
00081
00079
00082
OUTPUT_OPS
OUTPUT_OPS
PREPOSITION
PRINT
BREAK_RESPONSE
COMPONENTS
PRINT
Format: 
{ON|TO|OVER|INTO} 
Parameters: 
ON   -   file creation.  The source or list of sources is copied to a file 
defined by the fid portion of the destination component, which must not 
specify an already existing file. 
TO   -   file creation.  Synonym for ON. 
OVER   -   File replacement.  Functions identically to TO and ON, but allows 
the replacement of an already existing file. 
INTO   -   file extension.  If the fid specified in the destination parameter 
is an already existing file, the source or list of sources is added to that 
file.  If output file's organization is KEYED, only KEYED input files may be 
merged; input records may overwrite and may be interspersed among the output 
file's records.  If the output file's organization is anything else, except 
for INDEXED and IREL files, the input records are appended to the output file. 
For INDEXED and IREL files, any compatible input (keys are not necessary) 
works, and has the same effect as that described for KEYED files.  If the file 
does not already exist, or if the destination fid is a device, INTO functions 
identically to TO or ON. 
Description: 
One of the four preposition components always precedes the destination 
component.  This determines the type of file open that is to take place. 
Examples: 
<COPY STEVE TO CHARN 
means create a new file CHARN with identical contents of file STEVE.  Abort if 
the file STEVE already exists. 
<COPY ZORRO OVER MARKS 
means replace any existing file MARKS. 
<COPY LOIS INTO SUPERSTAR 
means merge file LOIS into file SUPERSTAR.  Create the file if it does not 
exist. 
Usage Note: 
The preposition component is used in the COPY, COPYALL, COPYSTD, LIST, LISTD, 
and MODIFY commands. 
00002
00003
00001
00004
PREPOSITION
Syntax: 
PRINT [fid[,fid]...] 
Parameters: 
fid   -   is a device stream fid.  If unspecified, all streams are output to 
their associated devices. 
Description: 
PRINT cause spooling streams to be output to the device with which they are 
associated. 
Files copied to devices that are not at the user's workstation cannot be 
cancelled by ERASE, and are activated without a PRINT command. 
Streams are automatically released for output when a user logs off. 
Examples: 
<COPY LESLIE TO LP 
<PRINT 
means copy file LESLIE to the line printer at the user's workstation.  PRINT 
causes the output to actually be printed on the device. 
Related Commands: 
ERASE 
00002
00003
00001
00004
CP-6 Peripheral Conversion Language (PCL) is a flexible and powerful utility 
processor that provides information movement between various sources and 
destinations in the CP-6 system or network.  Features include: 
o   Single, multiple, and conditional file selection 
o   Data encryption and conversion 
o   Modification of file attributes 
o   Support of ANS tape and file structures 
o   File backup and maintenance 
o   Comprehensive error messages and an extensive HELP facility 
END
RANGE_SOURCE
Format: 
name1[.[account][.password]]>name2[(option[,option]...)] 
Parameters: 
name1   -   specifies the name of the file at the beginning of the file range. 
account   -   specifies the account in which the file range is contained.  The 
default is the user's directory account. 
password   -   specifies a password for all the files in the file range.  If a 
password is not specified, any passworded files are not selected as part of 
the file range.  If a password is specified, only files that have that 
password (or no password) are selected. 
name2   -   specifies the name of the file at the end of the file range. 
option   -   is an input option that influences the processing or selection of 
files.  See INOPS. 
A dash (-) may be used instead of a greater-than sign (>) to delineate the 
range; however the dash must be enclosed by blanks. 
Description: 
The range source component is a special form of the source component that 
specifies a range of files on a single storage medium.  If used by itself, the 
single source is presumed to be a disk file.  If the single source is used in 
a complex source, the file will be found on the specified device. 
For disk storage, files whose names are alphabetically between name1 and name2 
(inclusive) are selected.  The same alphabetical sorting is true of labeled 
tape storage as well, unless PHYSICAL is specified as one of the input 
options.  In that case the files that live physically on the tape between 
name1 and name2 (inclusive) are selected.  Name1 must exist for the selection 
to be valid. 
NOTE:  Throughout this discussion, "alphabetically" refers to the ASCII 
collating sequence. 
Do not use wildcarding with range selection. 
A special convention exists to specify a range that ends at the "end" of the 
disk storage or labeled tape.  The format is: 
(name1[.[account][.password]]>) 
The "missing" ending filename before the closing parenthesis indicates that 
the range is "open-ended", terminating at the end of the disk file directory 
or the end of the tape. 
A special convention exists to specify range that starts at the "beginning" of 
the disk storage or labeled tape.  The format is: 
[.account][.password]>name 
Examples: 
FILEA>FILEZ 
means all disk files alphabetically between FILEA and FILEZ (inclusive). 
FISH>ABALONE(PHY) 
means all files located physically between FISH and ABALONE (inclusive). 
MOD1..QBL - MOD7 (ORG=K,TY=SB) 
means all keyed disk files of file type SB (Source Basic) between MOD1 and 
MOD7 with password QBL or no password. 
Usage Note: 
The range source component applies to both disk and tape storage media. 
00002
00003
00001
00004
Syntax: 
REA[D] fid 
Parameters: 
fid   -   is a file containing PCL commands, one per record.  Continuation via 
semicolon is permitted. 
Description: 
READ reads a disk file containing PCL commands. 
When the file runs to completion or is interrupted, PCL resumes normal command 
reading. 
Examples: 
<READ COMFILE 
means execute the commands contained in file COMFILE 
Related Commands: 
NONE 
00002
00003
00001
00004
Syntax: 
REL[EASE] fid 
Parameters: 
fid   -   is a CP-6 tape fid. 
Description: 
RELEASE releases a tape drive back to the system. 
Examples: 
<RELEASE LT#ABCD 
requests that the labeled tape be removed from the tape drive, releasing the 
tape drive so that other users can allocate it for their tasks. 
Related Commands: 
REMOVE, MOUNT 
00002
00003
00001
00004
Syntax: 
REM[OVE] fid 
Parameters: 
fid   -   is a CP-6 tape fid. 
Description: 
REMOVE requests that a certain tape be removed from the system tape drives. 
Examples: 
<REMOVE FT#1234 
requests that the free tape be removed from the tape drive. 
Related Commands: 
RELEASE, MOUNT 
00002
00003
00001
00004
MODIFY
Syntax: 
REV[IEW][(listopt)] sourcelist[ FROM fid] 
Parameters: 
listopt   -   specifies either an A, C, EA, or FA listing format input option. 
See INOPS. 
sourcelist   -   specifies a list of disk files or ranges of disk files with 
input options.  The only valid input options are A, C, CRPT, DATE, EA, FA, OR, 
or TY.  The default is the user's directory account. 
FROM fid   -   specifies a default set of fid elements to be used when PCL 
parses the list of sources. 
See the common parameter descriptions for SOURCE and FROM for detailed 
syntactical information. 
Description: 
REVIEW prints a summary of a specified portion of the user's disk storage, 
allowing the user to delete or copy the contents of the file. 
REVIEW is designed for on-line operation; in batch, REVIEW functions as a LIST 
command.  The list of sources determines which files are selected for review. 
Each selected file is listed according to the requested format.  If no list 
and review options are specified, only the file name is listed.  After each 
specified file is listed, a period is issued as a prompt.  The user may then 
perform several actions upon the file by entering one of the following 
responses: 
    A[TTRIBUTES]    Re-list the file with its attributes. 
    EA[TTRIBUTES]    Re-list the file with its extended attributes. 
    FA[TTRIBUTES]    Re-list the file with its full attributes. 
    J[UMP] [fid]    Continue the reviewing process at the next source 
    parameter (if fid is unspecified) or at or beyond the specified fid. 
    D[ELETE]    Delete the file from the user's account. 
    C[OPY] [n] [CRPT=seed]    Copy the first n records of the file to the 
    user's terminal and then relist the file.  The default for n is 1.  If 
    specified, the seed is used to decrypt the file. 
    [NEXT]    Proceed to the next file. 
    E[ND]    End the reviewing process, return to the PCL command level. 
When the REVIEW operation terminates, PCL prints a summary line showing the 
number of files and the number of granules taken up by files listed using "A" 
or "FA" options.  (Use of the JUMP response can distort both of these numbers 
by relisting one or more files.)  The summary also shows the number of files 
and granules deleted. 
Examples: 
<REV 
HELEN.A 
Org TY  Gran  NGAV     Rec   Last modified   Name 
Key       27     0    1483 14:42 MAR 29 '86  HELEN. 
LESLIE.EA 
Org TY  Gran  NGAV     Rec   Last modified   Name 
Key       35     0    2278 16:35 MAY 03 '86  LESLIE 
    Last access  08:41 MAY 04 '86 
    Backed up    23:54 MAY 04 '86  on  LT#A09B03 
    XTNsize =    2 
    FITsize =   54 
    Created      16:34 DEC 05 '85 
    Lslide  =  510    Slide   =    1 
    LRDL0   =    3    TDALVL  =    1    Spare   =    1 
    Backup.J MEMO 
MEMO.C 3 
Memo To: J. Turweiler 
Subject:  Clogged Drains 
It has come to our attention during the recent rain 
MEMO.J JANICE 
JANICE.D 
           ** Deleted ** 
JOPLIN.END 
 ..   5 files listed;    1 files,     1 granules deleted 
< 
The user reviews the files in the account: 
1.  The file name HELEN is printed; the user types "A" <CR> causing file HELEN 
    to be listed with it attributes.  The user presses RET. 
2.  The file name LESLIE is printed; the user types EA <CR>, causing file 
    LESLIE to be listed with its extended attributes.  The user types J MEMO 
    and presses RET . 
3.  The file name MEMO is printed; the user types C 3 <CR>, causing the first 
    three records of file MEMO to be printed. 
4.  The file name MEMO is printed again; the user types J JANICE <CR> causing 
    the review operation to skip to file JANICE. 
5.  The file name JANICE is printed, the user types <D> to delete the file. 
6.  The file name JOPLIN is printed, the user types END <CR> to end the review 
    process. 
Related Commands: 
REVIEWSTD 
00002
00003
00001
00004
Syntax: 
REV[IEW]S[TD] [(listopt)] stdfid [FROM fid] 
Parameters: 
listopt   -   specifies either an A, C, EA, or FA listing format input option. 
See INPUT_OPS. 
stdfid   -   specifies an STD file.  Each record of the STD file contains a 
sourcelist.  The only valid input options for this command are A, EA, FA, 
CRIT, CRPT, DATE, OR, and TY. 
FROM fid   -   specifies a default fid whose elements are to be used when PCL 
parses the list of sources. 
See the common parameter descriptions for SOURCE and FROM for detailed 
syntactical information. 
Description: 
REVIEWSTD prints a summary of a specified portion of the user's disk storage, 
allowing the user to delete or copy the contents of the file. 
REVIEWSTD functions identically to the REVIEW command, except that the sources 
are contained in an STD file rather than included as part of the command.  The 
first file reviewed is always the STD file itself.  If it is deleted, the 
sources it contained are still accessed. 
Examples: 
<REVIEWSTD STANDARD 
means review the files listed in STD file STANDARD. 
Related Commands: 
REVIEW 
00002
00003
00001
00004
REVIEWSTD
Syntax: 
REW[IND] fid 
Parameters: 
fid   -   is a CP-6 tape fid. 
Description: 
REWIND rewinds a tape to its beginning or load point. 
Examples: 
<REW FT#1234 
<REW LT#ABCD 
means rewind free tape #1234 then rewind the labeled tape #ABCD. 
Related Commands: 
MOUNT, REMOVE, SPE, SPF, SPR, RELEASE 
00002
00003
00001
00004
Syntax: 
SC[AN] fid [ {TO|ON|OVER|INTO} destination] 
Parameters: 
fid   -   is a free tape fid. 
TO   -   specifies file creation (see Preposition Component). 
ON   -    specifies file creation (see Preposition Component). 
OVER   -   specifies file replacement (see Preposition Component). 
INTO   -   specifies file extension (see Preposition Component). 
destination   -   specifies the output for the scan operation.  This may be 
either a file, or a device stream.  The default is ME, which indicates the 
user's terminal (on-line) or the line printer (batch). 
Description: 
SCAN searches a free tape from present position up to the first encountered 
double tape mark and reports the recording density of the tape, the number of 
records accessed and the length of the longest record in each file. 
Usage Notes: 
The CR, LC, NCR, NFA, O, TX, VC, VF, X, FV, NV, and X1 options are invalid for 
this command. 
Examples: 
<SCAN FT#1234 
means report list of files on free tape #1234. 
<SCAN FT#ABC ON *STEVE 
means produce file named *STEVE with a list of files on free tape #ABC. 
Related Commands: 
LIST, LISTSTD 
00002
00004
00001
00005
00003
Syntax: 
SE[VERITY] {A[BORT]E[RROR]|C[ONTINUE]} {S[TEPCC]|NS[TEPCC]} 
Parameters: 
ABORT   -   specifies that error conditions generate an M$XXX. 
ERROR   -   specifies that error conditions generate an M$ERR. 
CONTINUE   -   specifies the operation is to run to completion.  The default 
is CONTINUE. 
STEPCC   -   specifies STEPCC setting option ON.  Default is ON. 
NSTEPCC   -   specifies STEPCC setting option OFF. 
Description: 
SEVERITY determines whether an operation runs to completion in the event of an 
error condition. 
On exit, for STEPCC "ON", the STEPCC value becomes a code number indicating 
the highest severity encountered in the session: 
STEPCC     MEANING 
------     ------- 
0       No errors, all OK. 
1       A warning only message was issued, operation complete. 
2       Part of a command could not be performed, 
        remainder of command may have been OK. 
3       An entire command could not be performed, due to 
        syntax or other error. 
4       Fatal user error, PCL aborted. 
5       Fatal internal error, PCL aborted. 
Examples: 
<SEVERITY ABORT 
means abort operation if an error occurs. 
Related Commands: 
ERASE, PRINT 
00002
00003
00001
00004
DESTINATION
Syntax: 
name[.[account][.password]][(option[,option]...)] 
Parameters: 
name   -   is the file name. 
account   -   is the file account. 
password   -   is the file password. 
option   -   is an input option that influences the processing of the file 
identified by name.  See IN_OPS 
Description: 
If used by itself the single source is presumed to be a disk file.  If the 
single source is used in a complex source, the file will be found on the 
specified device.  The single source parameter identifies and/or qualifies the 
location of data to be transferred to the destination. 
Examples: 
FILEA..SECRET 
means disk file FILEA with password SECRET. 
FILEB(1-10) 
means records 1 through 10 of disk file FILEB. 
FILEC(CRPT=375) 
means file FILEC, encrypted with seed 375. 
Usage Note: 
The single source component is used in the COPY, COPYALL, COPYSTD, DELETE, 
DELETE RECORD, DELETESTD, LIST, LISTSTD, MODIFY, REVIEW, and REVIEWSTD 
commands. 
00002
00003
00001
00004
SINGLE_SOURCE
Syntax: 
SPE fid 
Parameters: 
fid   -   is a CP-6 tape fid. 
Description: 
SPE positions a tape just beyond the end of its last file. 
If the file specifies a free tape, the tape is positioned forwards until two 
adjacent tape marks are encountered.  It is then positioned between these two 
tape marks.  If the fid specifies a labeled tape, the tape is positioned after 
the last file. 
Examples: 
<SPE LT#ABCD 
means position the labeled tape to the end of the last file. 
Related Commands: 
SPF, REWIND, SPR 
00002
00003
00001
00004
Syntax: 
SPF fid [value] 
Parameters: 
fid   -   is a CP-6 tape fid. 
value   -   specifies the number of files forwards or backwards at which 
positioning is to take place.  Only integers are valid; positive integers 
position in the forward direction and negative integers position in the 
backwards direction.  The default is 0, which positions to the beginning of 
the current file. 
If the fid specifies a filename on a labeled tape, the specified file becomes 
the current file, and positioning takes place forwards and backwards from that 
file. 
Description: 
SPF positions a tape to a specified file. 
Examples: 
SPF LT#TOUPEE/JANICE 
means position the tape to the beginning of file JANICE. 
Related Commands: 
SPE, REWIND, SPR 
00002
00003
00001
00004
Syntax: 
SPR fid [value] 
Parameters: 
fid   -   is a free tape fid. 
value   -   specifies the number of records to space forwards or backwards. 
Only integers are valid:  The default is 1. 
Description: 
SPR positions a free tape forwards or backwards a specified number of records. 
SPR does not allow positioning beyond the tape marks.  If the positioning 
operation encounters a tape mark, the user is informed and the tape is 
positioned just inside the offending tape mark. 
Examples: 
<SPR FT#1234 100 
means position 100 records forwards on free tape #1234. 
Related Commands: 
SPE, SPF, REWIND 
00002
00003
00001
00004
Syntax: 
ST[ATUS] 
Parameters: 
NONE 
Description: 
STATUS displays information about the current session.  Display includes 
default COPY destination, setting of SEVERITY command, highest encountered 
severity in the session, and the ERRORS SAVE setting. 
Examples: 
<STATUS 
means display PCL status information. 
Related Commands: 
HELP 
00002
00003
00001
00004
NOTATION
TX
PREPOSITION
Syntax: 
T[X] {[?]|t[,t]...} 
Parameters: 
?   -   prints the current tab stops. 
t   -   specifies a column at which a tab stop is to be set.  If no stops are 
specified, or the ? parameter is included, all tab stops are displayed.  If 
the only stop specified is 0, then all tab stops are cleared.  When specified, 
tab stops must be in ascending order and cannot exceed 511. 
Description: 
TX sets the tab stops for copy operations. 
Under normal operation, PCL interprets tab characters literally; i.e., a tab 
character read from a source is written to a destination as a tab character. 
If the TX output option is included as part of the destination parameter, the 
PCL tab stops (if any have been set) or the IBEX tab stops (if no PCL tab 
stops have been set) are used for tab expansion; a tab character read from a 
source will cause PCL to expand the written record to the next tab stop before 
the character following the tab character is written. 
Examples: 
<TX 10 
means set a tab stop at column 10. 
<TX ? 
means print the current tab stops. 
Related Commands: 
NONE 
00002
00003
00001
00004
Syntax: 
W[EOF] fid 
Parameters: 
fid   -   is a free tape fid. 
Description: 
WEOF writes an end-of-file record to the specified tape.  If a WEOF is issued 
to a line printer, the printer skips to top-of-form; if to a card punch, a 
!EOD card is punched; if to a free tape, an end-of-file tape mark is written 
to the tape. 
Examples: 
<WEOF FT#52580 
means write an end-of-file record to free tape FT#52580. 
Related Commands: 
NONE 
00002
00003
00001
00004
WILD_SOURCE
WILD_DESTINATION
WILD_SOURCE
Format: 
[{DP|LT|MT}][#serial][{characters|?}]...[[.account][.password]] 
    [(option[,option]...)] 
Parameters: 
DP   -   specifies disk pack; LT specifies labeled tape; MT specifies magnetic 
tape. 
#serial   -   specifies a tape serial number or a packset name. 
characters   -   specifies a set of one or more matching characters that must 
exist in the file name if the file is to be selected. 
?   -   specifies variable field for output matching.  At least one question 
mark must be contained in a wildcard fid. 
account   -   specifies the account in which the file range is contained.  The 
default is the user's directory account. 
password   -   specifies a password for all the files in the file range.  If a 
password is not specified, any passworded files are not selected as part of 
the file range.  If a password is specified, only files that have that 
password (or no password) are selected. 
option   -   specifies an output option that provides information about the 
processing or final disposition of the destination.  See OUTOPS 
Description: 
Wildcard destinations are primarily used as matchings for wildcard sources. 
When the output name is built, the output template is followed like a menu. 
When a constant part is indicated, it is used.  When the Nth wild token is 
encountered, the text that matched the Nth token in the input template is 
used. 
If the input specification is a range of files, the complete name of the file 
in the range will be used as the first wild token in output name construction. 
If the output name construction runs out of wild parts from the file name, 
nulls are used.  Leftover input wild parts are not considered an error. 
An output file name may not evaluate to more than 31 characters.  If it does, 
the command is aborted. 
Usage Notes: 
1.  Wildcard destinations are used in the COPYALL, COPYSTD, and MODIFY 
    commands. 
2.  Caution must be used when wildcarding appears within a fid name.  This 
    could lead to repetitive renaming in the MODIFY command until the fid name 
    exceeds 31 characters or repetitive creation of files in the COPYSTD or 
    COPYALL commands until file space is exhausted. 
00002
00001
00003
Format: 
[{characters|?}]...[.[account][.password]][(option[,option]...)] 
Parameters: 
characters   -   specifies a set of one or more matching characters that must 
exist in the file name if the file is to be selected. 
?   -   specifies variable field for file selection matching.  At least one 
question mark must be contained in a wildcard fid. 
account   -   specifies the account in which the file range is contained.  The 
default is the user's directory account. 
password   -   specifies a password for all the files in the file range.  If a 
password is not specified, any passworded files are not selected as part of 
the file range.  If a password is specified, only files that have that 
password (or no password) are selected. 
option   -   is an input option that influences the processing or selection of 
files.  See INOPS 
Description: 
The wildcard source component performs file selection on the basis of matching 
strings in a template filename. 
If used by itself the single source is presumed to be a disk file.  If the 
single source is used in a complex source, the file will be found on the 
specified device. 
PCL compares the file name to the input template from left to right.  The 
constant part of the template must be exactly matched by the file name to 
select the file.  Any number of characters (even zero) will be considered a 
match for the wild token ('?'). 
On input, any number of adjacent wild tokens count as a single token.  The 
following are valid examples of input wildcards: 
<L ?_?_SI 
<REV SPEAKER?TO?ANIMALS 
<C COBOL?CODE,COBOL????CODE TO LP 
Note that the two source specifications in the last example are considered 
identical. 
Examples: 
?.SHAW(TY=SE) 
means all disk files of filetype SE (Source Edit) in account SHAW. 
LT#ABCD/A?Z..SECRET 
means all files whose names begin with the character A and end with the 
character Z on labeled tape ABCD, password SECRET. 
DP#MYSET/?Z?.ALPHA 
means all disk files whose names contain the character Z anywhere in the name, 
on packset MYSET in account ALPHA. 
Z?A?Z(ORG=KEYED) 
means all keyed disk files in the user's account whose names begin and end 
with the character Z, and contain at least one A. 
Usage Notes: 
1.  Wildcard source components are frequently used with destination sources in 
    the MODIFY and COPYALL commands. 
2.  Wildcard source components can not be used with range selection. 
3.  Wildcard source components may not be used with the DELETE RECORD command. 
00002
00003
00001
00004
END
