The EDIT processor is entered from IBEX by the following command: 
{E|EDIT} [fid] 
EDIT responds by printing: 
EDIT D00 HERE 
* 
The asterisk (*) is a prompt indicating that EDIT is prepared to receive 
commands. 
If a fid (file identifier) is specified, EDIT searches for the specified disk 
file; if it exists, the file is opened.  A user may be restricted in the ways 
that the opened file can be altered.  If the user is not permitted to update 
the file, it is opened for reading only.  If no fid is specified, EDIT is 
entered, but a file is not opened.  EDIT commands fall into three groups: 
o   File commands build, copy, merge, and delete files; open files for 
    examination or editing; determine editing conditions; and provide status 
    information. 
o   Record commands print, insert, delete, reorder, alter, search records, and 
    determine which records will be modified by subsequent intrarecord 
    commands. 
o   Intrarecord commands manipulate strings within records, set up conditional 
    execution of other intrarecord commands, and provide miscellaneous 
    functions. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
Syntax: 
{k1|[j]/string1/}A{k2|/string2/} 
Parameters: 
j   -   is a positive integer specifying the occurrence of the string to be 
searched for (and shifted). 
string1   -   is the string whose first character marks the column to be 
shifted. 
k1   -   is the column to be shifted.  If k=0, the last column in the record 
is assumed. 
string2   -   is the string whose first column marks the target column for the 
shift. 
k2   -   is the target column for the shift. 
Description: 
The A (Align) command aligns two columns.  A functions like an R command if 
the shift is to the right, and like an L command if to the left.  A is always 
an intrarecord command. 
Examples: 
*15A25 
means shift column 15 to column 25. 
*/FISH/A30 
means shift the portion of the record beginning with the string FISH to column 
30. 
*30A/FISH/ 
means shift column 30 to the portion of the record that begins with string 
FISH. 
*/FISH/A/UNICORPUS/ 
means shift the portion of the record that begins with FISH to the column 
marked by the first U in UNICORPUS. 
Related Commands: 
R, L 
00002
00003
00001
00004
Syntax: 
AD [n1[-n2]] 
Parameters: 
n1   -   is the key of the first record to be printed. 
n2   -   is the key of the final record to be printed.  If omitted, only 
record n1 is processed. 
If neither n1 nor n2 is specified, the records satisfying the current 
selection criteria are printed. 
Description: 
The AD (ADd) command prints a record or range of records, stopping at the end 
of each record to allow the user to add text.  No editing of the existing 
contents is permitted.  AD can be a record command (if any parameters are 
included) or an intrarecord command (if parameters are omitted). 
Examples: 
*AD 1-10 
means print records 1 through 10, stop at the end of each record and permit 
text to be added. 
Related Commands: 
RR 
00002
00003
00001
00004
Syntax: 
AP [i] 
Parameters: 
i   -   is the increment for successively inserted lines.  The default is 1 or 
the last-issued increment in a previous command. 
Description: 
The AP (APpend) command appends records to the end of a file currently open 
for editing.  When AP is issued, the increment is added to the highest 
numbered record in the file, and the resulting key is printed as a prompt. 
Successive insertions are also incremented by i.  Insertion is terminated when 
any of the following events takes place: 
1.  A null line (an unaccompanied carriage return) is entered. 
2.  An attempt is made to insert a record having a key larger the 99999.999; 
    in this case an error message is printed. 
AP is always a record command. 
Examples: 
*AP 10 
means add 10 to the highest numbered record and begin inserting records, 
incrementing by 10 
Related Commands: 
BUILD, IN, IP 
00002
00003
00001
00004
BUILD
Syntax: 
BP {ON|OFF} 
Parameters: 
ON   -   specifies that blank fields are to be preserved.  The default is ON. 
OFF   -   specifies that the column positions of non-blank characters in a 
record are to be maintained at the cost of blank fields. 
Description: 
The BP (Blank Preserve) command determines the handling of blanks during 
intrarecord editing BP is usually set to OFF when editing a source program 
file where commands or statements must be maintained in certain positions to 
be meaningful.  When BP is OFF, a field of blanks will be truncated or 
expanded as necessary to accommodate the positioning of non-blank characters. 
However, no blank field will be truncated to less than a single blank.  This 
facilitates editing of the various parts of a column-oriented file. 
When BP is ON, blank fields are maintained.  When a string is inserted or 
replaced in a manner that forces a change in the number of characters in the 
records, strings are moved to preserve the number of blanks separating them. 
The BP and RP commands interact to determine the handling of blanks and record 
lengths during intrarecord editing.  BP is always a file command. 
Examples: 
*BP OFF 
means that blank fields can flex in size to accommodate changes in the 
contents of records. 
Related Commands: 
RP 
00002
00003
00001
00004
In on-line operation, the BREAK key always causes an immediate interruption in 
any EDIT activity, and any partially completed input and output. 
If a command that produces no display is interrupted, the point of 
interruption is reported to the user with a message starting the sequence 
number(s) of the record(s) being processed at the time of the interrupt.  The 
following message is printed: 
*ENTER 'C' TO CONTINUE 
and a prompt is issued.  If an unaccompanied upper or lowercase c is typed, 
immediately followed by a carriage return, the operation runs to completion; 
any other response will be processed as an EDIT input. 
If a new command is issued, it is put into operation. 
If a command is interrupted during an I/O operation on a single record, the 
operation is completed and a prompt is printed. 
When a BREAK interrupts the processing of a record or intrarecord command (or 
an informational command), the currently open file remains open, and the 
current selection criteria are not changed.  If a file command is interrupted 
and then aborted, all files are closed. 
Syntax: 
{B|BUILD} fid[,[n][,i][,tc]] 
Parameters: 
fid   -   is the identifier of the file to be created. 
n   -   is the key at which the new file is to start.  The default is 1. 
i   -   is the increment for the keys of the new file.  The default is 1 or 
the last-issued increment in a previous command. 
tc   -   specifies a two character file type code for the file.  The default 
is SE (Source Edit).  File types are defined by processors at file creation. 
Users can define their own file types to aid in associating groups of selected 
files. 
Description: 
BUILD creates a newly-named keyed disk file and causes EDIT to print keys as 
prompts for the assignment of records.  A null line (an unaccompanied carriage 
return or line feed) terminates the operation.  When issued from EDIT, the 
null line returns control to EDIT, and the newly-created file remains open for 
editing.  When issued from IBEX, the null line returns control to IBEX, and 
the file is closed.  An error message is printed if an attempt is made to 
create a file that already exists.  BUILD is always a file command. 
Examples: 
*BUILD LEMEGETON 
means create a new file called LEMEGETON, prompt with key 1.000, and continue 
adding to the file (next record 2.000, next 3.000, etc.)  until a null line is 
entered. 
*BUILD CONSCIOUSNESS..COSMIC,100,.001 
means create new file CONSCIOUSNESS with password COSMIC, prompt with key 
100.000, and continue adding to the file (next key 100.001, next 100.002, 
etc.). 
*BUILD :DATA,,GJ 
means create new file :DATA, and give it user-defined file code GJ. 
Related Commands: 
COPY, MERGE, EXAMINE, EDIT 
00002
00003
00001
00004
COPY
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
Syntax: 
CI [n][,i] 
Parameters: 
n   -   is the first record in the target range.  The default is the last key 
specified in a prior CI or CP command. 
i   -   is the increment for multiple record operations.  The default is 1 or 
the last increment specified on a previous CI or CP command. 
Description: 
The CI (Copy Interlacing) command causes the record(s) in the selection range 
to be copied to another position in the file.  The original record(s) is not 
deleted.  CI differs from CP in that existing records can be overwritten, and 
records can be interlaced among existing records.  CI is always an intrarecord 
command. 
Examples: 
*SE1-5;CI 100.1,.001 
means copy records 1 through 5 to record 100.1, with incremented records of 
100.101, 100.102, etc. 
Related Commands: 
CP, CL 
00002
00003
00001
00004
Syntax: 
CL c3[,c4] 
Parameters: 
c3   -   is the lower limit of the range of columns to be edited. 
c4   -   is the upper limit for the range of columns to be edited.  The 
default is 256. 
Description: 
The CL (CoLumn) command defines a column range for editing that is separate 
from the column range used for string selection searches.  This allows the 
editing of portions of a record that are not included in the range of selected 
columns.  Once a record has been selected for editing (via a record command 
that may or may not specify a range of columns for the sse search), 
intrarecord commands operate only upon columns c3 through c4 as specified in 
the latest CL command.  Note that CL does not alter the selection criteria in 
any way.  CL is always an intrarecord command. 
Examples: 
*SE1-5,/*/,1,5;CL10,20;/*/S/#/ 
means limit editing to all records between 1 and 5 that contain an asterisk 
between columns 1 and 5.  Within records so selected, change the first 
asterisk in columns 10 through 20 to pound signs (#). 
Related Commands: 
CI, CP 
00002
00003
00001
00004
Syntax: 
CM n,c1[,c2] 
Parameters: 
n   -   is the key of the first record to be assigned text. 
c1   -   is the starting column for text insertion. 
c2   -   is the last column to be assigned text.  The default is 256. 
Description: 
The CM (CoMentary) command inserts text (typically commentary) into a column 
range.  CM prints key n as a prompt; text entered in response is assigned to 
columns c1 through c2 of that record.  The key next larger than n is then 
printed, and so on.  The insertion process is terminated when a blank line is 
typed in response to a prompt.  The inserted text is blank filled to the right 
through column c2.  If more data is entered than will fit between the two 
columns, the input is truncated on the right.  CM is always a record command. 
Examples: 
*CM 5,32,64 
means start at record 5 and insert commentary in columns 32 to 64 inclusive. 
Related Commands: 
CT 
00002
00003
00001
00004
COPY
The EDIT commands, by groups, are: 
File Commands:  BP, BUILD, COPY, CR, CRPT, DELETE, DIRECTORY, EDIT, END, 
EXAMINE, HELP, LIST, MERGE, READ, RP, STATUS, TA, TABC, TABX, TYPE, VE, X. 
Record Commands:  AD, AP, CM, CT, DE, FD, FS, FT, IA, IB, IN, IP, IS, MD, MK, 
OL, RN, RR, SE, SS, ST, TC, TN, TP, TS, TY. 
Intrarecord Commands:  A, CI, CL, CP, D, E, EI, EL, F, IF, JU, L, NO, O, P, 
QR, R, RF, RL, RO, S, TX. 
Information about these commands can be obtained by typing: 
HELP command 
    The following components are used in many EDIT commands: 
    Component                             Meaning 
    --------                              ------- 
    FID                                   File Identifier 
    STRING                                Character String 
    WILDCARD                              Template Character String 
    SSE                                   String Selection Expression 
    The following concepts are essential to a complete understanding of CP-6 
    EDIT. 
    CONCEPT                             MEANING 
    -------                             ------- 
    FILE COMMANDS                       Commands that manipulate files 
    RECORD COMMANDS                     Commands that alter records 
    INTRARECORD COMMANDS                Commands that alter strings, etc. 
    SELECTION CRITERIA                  Rules for editing 
    KEY FORMATS                         Standard edit keys 
    FILE ORGANIZATION                   Edit support of files 
    DATA CONTROL BLOCKS                 Assignable DCBs in EDIT 
    LINEFEED FUNCTION                   Special function key 
    UP ARROW FUNCTION                   Special function key 
    BREAK FUNCTION                      Special function key 
    = SUBSTITUITION                     FID name used in place of = 
    XUG SERVICES                        EDIT recognizes DO(!) commands 
Control-D is synonymous with the up-arrow function. 
Control-J is synonymous with linefeed. 
Syntax: 
C[OPY] fid1 [{ON|TO|OVER} fid2][,[n][,i][,tc]] 
Parameters: 
fid1   -   is the file to be copied. 
fid2   -   is the target file.  If n, i, or tc are not specified, the original 
keys and file type are retained.  If fid2 is not specified, the file is copied 
over itself. 
ON   -   specifies that fid2 must not be a previously existing file. 
TO   -   is a synonym for ON. 
OVER   -   specifies that any existing fid2 is to be replaced. 
n   -   is the initial key in the target file.  The default is 1. 
i   -   is the increment for the target file.  The default is 1 or the 
last-issued increment in a previous command. 
tc   -   is a two character file type code.  Standard file type codes are 
listed under the TYPE command. 
Description: 
COPY creates an EDIT keyed file.  The file to be copied may be either an EDIT 
keyed file, or a file of some other organization type; in any case, the target 
file is keyed.  On completion of a COPY operation, the target file remains 
open for editing.  COPY is always a file command. 
If file type code is not specified, the TYPE field will be the same as it was 
before the copy of the file was made.  If COPY builds a new file, and the file 
type code was not specified in the COPY command, the new file will have the 
same file type as the input file for the COPY command. 
NOTE:  Do not confuse the COPY command in EDIT with the COPY command in PCL or 
LEMUR; all three have similar functions, but provide different capabilities. 
Examples: 
*COPY QBL TO LSHILL 
means copy file QBL to file LSHILL, which will be keyed. 
*COPY DELPHI..FOSNIGHT OVER FLINT 
means copy file DELPHI with password FOSNIGHT to file FLINT (no password); 
replace any already existing file FLINT. 
*COPY ENOCHIAN,19,30,JD 
means copy file ENOCHIAN over itself, start with key 19 and increment each 
record by 30.  The new ENOCHIAN will be file type JD. 
Related Commands: 
BUILD, MERGE, EXAMINE, EDIT 
00002
00003
00001
00004
Syntax: 
CP [n][,i] 
Parameters: 
n   -   is the first record in the target range.  The command aborts if this 
record already exists.  The default is the last key specified in a prior CI or 
CP command. 
i   -   is the increment for multiple record operations.  The default is 1 or 
the last increment specified on a previous CI or CP command. 
Description: 
The CP (Copy Protected) command causes the record(s) currently open for 
editing to be copied to another position in the file.  The original record(s) 
is not deleted.  CP terminates if an attempt is made to write a record and a 
record exists between the last destination record and the current destination 
record. 
Examples: 
*SE20;CP35 
means reproduce record 20 at record 35. 
Related Commands: 
CI 
00002
00003
00001
00004
Syntax: 
CR {ON|OFF} 
Parameters: 
OFF   -   specifies the carriage return is to be excluded.  The default is 
OFF. 
ON   -   specifies that the carriage return is to be included. 
Description: 
The CR (Carriage Return) command controls the inclusion of the carriage return 
character on any records written to the file.  The carriage return is not 
normally needed at the end of a record, as the system provides this function 
automatically.  However, in certain cases (as when reproducing a file on cards 
or tape), it may be desirable to have this information included.  Note that a 
COPY command issued while CR is ON includes a carriage return at the end of 
every record in the target file. 
The presence of a carriage return at the end of a record has no effect on the 
printing of records.  CR is always a file command. 
Examples: 
*CR ON 
means include the carriage return character at the end of all newly-created 
lines. 
Related Commands: 
COPY 
00002
00003
00001
00004
    A record or a portion of a record must be included within the current 
    selection criteria before it can be altered.  The current selection 
    criteria consist of the following factors: 
1.  A range of selected records that define which records are open for 
    intrarecord editing. 
2.  A range of selected columns that define which areas of the selected 
    records are open for intrarecord editing. 
3.  A string selection expression limiting availability to records that 
    satisfy 1 and 2 and contain (or omit) specified character strings. 
When a file is opened or created, the selection criteria are set to the 
default, i.e., all columns of all records in the file, with no string 
selection expression.  Record commands alter this all-inclusive default. 
Rules: 
The following set of rules govern the modification of the selection criteria: 
1.  A record command that explicitly specifies a record or group of records 
    sets the range of selected records to that record or group of records. 
    Example: 
    *TY1-100 
    The selection criteria is now records 1 to 100 inclusive. 
2.  A record command that causes sequential access of records in the file (AD, 
    RR, CM, CT, IN, IP, IS, IA, IB, and AP) sets the range of selected records 
    to the last record altered or created by the user.  Examples: 
    *IN 100,.1 
    If the user inserts records 100 and 100.1, the selection criteria is now 
    record 100.1 (and not 100). 
3.  A record command that explicitly specifies a column as an upper or lower 
    limit sets the range of selected columns to the new limit.  Example: 
    *TY1-100,5,10 
    The selection criteria is now columns 5 through 10 inclusive, of records 1 
    through 100 inclusive. 
4.  A record command that explicitly specifies a string selection expression 
    limits all editing to records that satisfy the expression within the range 
    of selected records and columns.  Example: 
    *FT1-100,/FISH/,5,10 
    The selection criteria is now all records between 1 and 100 inclusive that 
    contain the string FISH within columns 5 through 10 inclusive. 
5.  A record command that alters a factor of the selection criteria sets the 
    other factors to their defaults, unless those factors are also explicitly 
    altered by the command.  Example: 
    *FT0-99,/SERPENT/ 
    *TY 3 
    *SE 
    The FT command sets selection criteria to all records between 0 and 99 
    that contain the string SERPENT.  The TY command sets selection criteria 
    to record 3 (with no string selection expression).  The SE command resets 
    the selection criteria to the default values, i.e., all columns of all 
    records with no string selection expression. 
00001
Syntax: 
CRPT [seed] 
Parameters: 
seed   -   is an octal integer in the range of 1 to 777777777777.  If the seed 
is omitted from the command, data encryption and decryption do not occur. 
Description: 
The CRPT (enCRyPTion) command sets the data encryption seed, a value that will 
scramble and unscramble all data read from and written to any record accessed 
by EDIT.  A record's data encryption seed must be remembered by the user; if 
forgotten, it is likely that the contents of the record will, in time, become 
mysterious.  Although separate seeds can be set for separate records in a 
file, it is advisable to use only one seed for an entire file.  CRPT is always 
a file command. 
Examples: 
*CRPT 1234 
means all newly-created records are to be encrypted with the seed 1234, and 
all records printed are to be decrypted with the seed 1234. 
Related Commands: 
None. 
00002
00003
00001
00004
Syntax: 
CT n,c1[,c2] 
Parameters: 
n   -   is the key of the first record to be assigned text. 
c1   -   is the starting column for text insertion. 
c2   -   is the last column to be assigned text.  The default is 256. 
Description: 
The CT (Commentary and Type) command inserts text (typically commentary) into 
a column range.  CT prints the record n up to column c1 as a prompt; text 
entered in response is assigned to columns c1 through c2 of that record.  The 
next record in the file is then printed (up to column c1), and so on.  The 
insertion process is terminated when a null line is typed. 
The inserted text is blank filled to the right through column c2.  If more 
data is entered than will fit between the two columns, the input is truncated 
on the right.  CT is always a record command. 
Examples: 
*CT 30,40 
means print columns 1 through 40 of record 30, allow commentary to be added, 
starting at column 40 and ending at column 256 (the default). 
Related Commands: 
None 
00002
00003
00001
00004
Syntax: 
[j]/string/D 
Parameters: 
j   -   is a non-negative integer specifying the occurrence in the record of 
the string to be deleted.  If j=0, then all occurrences are deleted.  The 
default is 1. 
string   -   is the string to be deleted.  See the STRINGS Option for a 
complete description of the string construct. 
Description: 
The D (Delete string) command locates and deletes strings within a record or 
records. D is always an intrarecord command. 
Examples: 
*se3;5/FISH/D 
means delete the fifth occurrence of the string FISH in record 3. 
Related Commands: 
S 
00002
00003
00001
00004
Data Control Blocks (DCBs) are "paths" through which EDIT accepts input and 
prints output.  Generally in EDIT the DCBs are user-transparent; for special 
processing, three of the DCBs that EDIT uses can be reassigned via the IBEX 
command SET.  These DCBs and their default assignments are: 
M$SI - All input. 
M$DO - All diagnostic output, including HELP and error messages. 
M$ME - All printed output. 
Syntax: 
DE [n1[-n2]] 
Parameters: 
n1   -   is the key of the first record in the range of records to be deleted. 
n2   -   is the key of the last record in the range of records to be deleted. 
If omitted, and n1 is specified, only n1 is deleted. 
Description: 
The DE (DElete record) command deletes records.  If no parameters are 
specified, all records in the current selection criteria are deleted, i.e., if 
DE is used without parameters following any command that specifies a range of 
records (such as SE, SS, ST, TY, TS, etc.), the entire range of records 
specified is deleted.  Note also that certain EDIT commands that specify a 
range of records have a default range when the range is left unspecified.  For 
example, if the SE, SS, ST, TY, or TS commands (among others) are used, and no 
selection criteria is specified, the default range is 0 to 99999.999.  In such 
a case, the use of the DE command without parameters results in the deletion 
of the entire default range of records. 
NOTE:  At completion of a DE operation, the selection criteria are set to the 
deleted records. 
DE is a record command if parameters are specified, and an intrarecord command 
if parameters are omitted. 
Examples: 
*DE 
means delete all records in the current selection criteria. 
*DE 5-10 
means delete records 5 through 10. 
Related Commands: 
MD, FD 
00002
00003
00001
00004
Syntax: 
{DEL|DELETE} fid 
Parameters: 
fid   -   is the disk file to be deleted. 
Description: 
The DELETE (DELETE file) command erases a file from disk storage.  DELETE is 
always a file command. 
Examples: 
*DELETE OSBORN 
means delete file OSBORN. 
Related Commands: 
None. 
00002
00003
00001
00004
Syntax: 
{DIR|DIRECTORY} [{fid|R[ESET]}] 
Parameters: 
fid   -   specifies the new default account fid, and may consist of an account 
or a pack set name and an account.  If neither fid nor RESET is specified, the 
current directory account is displayed. 
RESET   -   specifies that the default account is to be reset to the running 
account. 
Description: 
DIRECTORY changes the default account and pack set.  The default account and 
set are the account and associated pack set that are selected if an account is 
not supplied as part of a disk file fid specification. 
Examples: 
*DIRECTORY .SYSLIB 
This command directs the subsequent fids that do not include an account are to 
default to the SYSLIB account and the pack set associated with that account. 
*DIRECTORY RESET 
This command establishes the running account and its associated pack set. 
Related Commands: 
None 
00002
00003
00001
00004
Syntax: 
[j]/string1/E/string2/    or    kE/string2/ 
Parameters: 
j   -   is a positive integer specifying the occurrence of string1 to be 
located in the record.  The j=0 option is invalid for this command.  The 
default is 1. 
string1   -   is a string whose first character marks the column at which 
string2 is to overwrite; string1 must lie within the range of columns in the 
selection criteria.  See the STRING component for a complete description of 
the string construct. 
string2   -   is the string that is to overwrite the specified area in the 
record. 
k   -   is the start column for the overwriting by string2; i.e., the first 
character of string2 will lie in column k.  This column must lie within the 
range of columns in the selection criteria.  If k=0, the last column in the 
record is assumed. 
Description: 
The E (Extend) command replaces a section of a record with a specified string; 
all columns to the right of the new string are extended (filled) with blanks. 
E is always an intrarecord command. 
Examples: 
*SE1;/ABRACADABRA/E/PRESTO/ 
means overwrite the string PRESTO at the beginning of string ABRACADABRA.  All 
columns to the right of the O in PRESTO will be filled with blanks. 
*SE100-200;10E/$/ 
means put a dollar sign ($) in column 10 of records 100 through 200.  Any 
character already in column 10 is replaced; columns 11 through 256 will be 
filled with blanks. 
Related Commands: 
O 
00002
00003
00001
00004
Syntax: 
{E|EDIT} fid 
Parameters: 
fid   -   is the disk file to be opened. 
Description: 
EDIT opens a previously-created disk file for editing.  The EDIT processor is 
designed to edit keyed disk files.  Any attempt to open any other file 
organization results in a message describing the restrictions applied to 
editing or examining that file.  An error message is printed if the file does 
not exist, or if the user is not permitted to access the file.  EDIT is always 
a file command. 
Examples: 
*EDIT LEMEGETON 
means open file LEMEGETON for editing. 
*EDIT RELFILE 
means open the file RELFILE for editing. 
Related Commands: 
BUILD, COPY, EXAMINE, MERGE 
00002
00003
00001
00004
Syntax: 
...;EI[;...] 
Parameters: 
None. 
Description: 
The EI (End If) command terminates an IF block.  EI is always an intrarecord 
command. 
Examples: 
*SE1-10;IF 2/WAGTAIL/;DE;EI;TY 
means search records 1 through 10.  If a record contains at least two 
WAGTAILs, delete it.  Print records 1 through 10. 
*SE1-10;IF/FISHY/;TY;IF/WISHY/;DE;EI;EI 
means search records 1 through 10.  If a record contains the string FISHY, 
print it; if such a record also contains string WISHY, delete the record. 
Related Commands: 
EL, IF 
00002
00003
00001
00004
Syntax: 
...;EL [sse[,c1[,c2]];...] 
Parameters: 
sse   -   is the string selection expression.  See the SSE component for a 
complete description.  The basic format of the sse is: 
[NOT][j]string1[{AND|OR|EOR}[,NOT][j]string2]... 
c1   -   is the start column for the string selection search.  The default is 
1. 
c2   -   is the ending column for the string selection search.  The default is 
256. 
Description: 
The EL (ELse) command ends an IF block, and sets up commands that will be 
executed should the IF command obtain a false result.  Should the IF obtain a 
true result, the commands following the EL command are ignored.  EL is always 
an intrarecord command. 
Examples: 
*SE10-20;IF/GRYPHON/;TY;EL;RR;EI 
means search records 10 through 20.  Print all records containing the string 
GRYPHON.  Reread all other records in the range. 
*SE10-20;IF/CHIMERA/;DE;EL/COCKATRICE/;TY;EI 
means search records 10 through 20.  Delete all records containing the string 
CHIMERA and print all records containing the string COCKATRICE.  Records 
containing neither are ignored. 
Related Commands: 
IF, EI 
00002
00003
00001
00004
Syntax: 
{E|END|Q|X} 
Parameters: 
None. 
Description: 
END (with variant forms E, X, and Q) closes all active files and returns 
control to processor from which EDIT was called (usually IBEX).  END is always 
a file command. 
Examples: 
*END 
means exit EDIT and return to IBEX. 
Related Commands: 
EDIT, BUILD, DELETE 
00002
00003
00001
00004
The '='(equal sign) can be used in place of the filename to specify the 
current file you are editing. 
The rules for use of the = feature are as follows: 
1)  the '=' is legal only in the COPY, EDIT, EXAMINE, and MERGE commands. The 
    DELETE command has been purposely excluded because of the problems DELETE 
    = might cause. 
2)  the '=' is legal only in the "file-name" part of an input fid. 
3)  the '=' always refers to the "open file before the command began 
    execution". 
4)  Here are the rules to determine what is picked up from the open file. 
    A.  PSN will be picked up only if the user doesn't specify an Account or a 
        PSN. 
    B.  Account will be picked up only if the user doesn't specify an Account 
        or a PSN. 
    C.  Password will be picked up only if the user specifies just the '=' 
        (current file). 
    D.  Filename will always be picked up. 
        Examples: 
        =                => current file. 
        =..              => pick up PSN, Filename, and Account 
                            from open file, and don't use the 
                            open file's password. 
        =..Pass          => pick up PSN, Filename, and Account 
                            from open file, and use user supplied 
                            password. 
        =.               => pick up Filename from the open file, 
                            and use the current FMA account and 
                            packset name. 
        =.ACCOUNT        => pick up filename from the open file, and 
                            use user supplied PSN and Account. 
        =.ACCOUNT.       => pick up Filename from the open file, and 
                            use the user supplied PSN and Account. 
        =.ACCOUNT.PASS   => pick up Filename from the open file, 
                            and use user supplied Account, password 
                            and PSN. 
5)  Whenever EDIT performs the file-matching substitution for you, it prints 
    out what it built so that you can tell exactly what EDIT did and where 
    your data went. 
Current File Usage: 
    !EDIT  file 
    *C =                     REKEY the current file 
    *EX =                    Toggle to EXAMINE mode 
    *E =                     Toggle to EDIT mode 
    *MERGE file1 into =,10   MERGE file1 into the current file 
    *MERGE = into file2,10   MERGE the current file into file2 
Usage Specifying Other Accounts: 
    !EDIT file.:acctSI 
    *MERGE  =,10-20  INTO   =.acctUI,10,.001 
       (MERGE the current file, lines 10-20 into a UI file for 
       creating an update packet.) 
    *EX =.acctLS 
       (Examine a file of this name in another account.) 
    !EDIT file2.acct1 
    *MERGE  =.acct2,10-20  ON  =.acct3,10.01,.01 
       (Notice that only the filename will be picked up on this 
       MERGE because the account names have been specified on both 
       sides.) 
6)  Some people would like to avoid retyping a partial or full filename that 
    they've already typed on a MERGE command.  If we accept the basic rules of 
    the use of '=', then we can extend them a bit to recognize '==', as 
    performing the exact same function as the '=', but only in the SECOND fid 
    position of a command. The '==' will pick up the appropriate pieces from 
    the FIRST fid position of a command. 
    For example: 
    !E file3.:XSI 
    *M file4.:XSI,1-12 INTO ==.:XTUI,1.1,.1 
    * file4.:XTUI used for file2 
    Note that the "currently open file" is not used. 
Syntax: 
EX[AMINE] fid 
Parameters: 
fid   -   is the disk file to be opened for reading. 
Description: 
EXAMINE opens a disk file for reading; no updating is permitted. 
Examples: 
*EXAMINE CONCEPT 
means open the file CONCEPT for reading. 
Related Commands: 
BUILD, COPY, EDIT, MERGE 
00002
00003
00001
00004
Syntax: 
[j]/string1/F/string2/    or    kF/string2/ 
Parameters: 
j   -   is a non-negative integer specifying the occurrence of string1 to be 
located in the record.  If j=0, all occurrences are located.  The default is 
1. 
string1   -   is a string whose last character marks the column before the one 
at which string2 is to be inserted; string1 must lie within the range of 
columns in the section criteria.  See the STRING component for a complete 
description of the string construct. 
string 2   -   is the string to be inserted. 
k   -   is the start column for the insertion of string2; i.e., the first 
character of string2 will lie immediately to the right of column k.  This 
column must lie within the range of columns in the selection criteria.  If 
k=0, the last column in the record is assumed. 
Description: 
The F (Follow string) command inserts a string at a specified column or 
following a specified string.  F is always an intrarecord command. 
Examples: 
*SE1;/FISH/F/WIFE/ 
means locate the string FISH in record 1 and follow it with the string WIFE, 
forming FISHWIFE.  The W in Wife lies in the column following the H in FISH. 
The portion of the record that originally followed after FISH is shifted to 
the right. 
*SE;0F#015 
means put a carriage return (octal 15) at the end of every record. 
Related Commands: 
P, S 
00002
00003
00001
00004
Syntax: 
FD n1[-n2],sse[,c1[,c2]] 
Parameters: 
n1   -   is the starting key of the range of records to be searched. 
n2   -   is the ending key of the range of records to be searched.  If 
omitted, only record n1 is searched. 
sse   -   is the string selection expression.  See the SSE component for a 
complete description.  The basic format of the sse is: 
[NOT][j]string1[{AND|OR|EOR}[,NOT][j]string2]... 
c1   -   is the starting column for the search.  The default is 1. 
c2   -   is the ending column for the search.  The default is 256. 
Only columns c1 through c2 of records n1 through n2 are searched for the sse. 
Partial matches are not recognized. 
Description: 
The FD (Find and Delete) command searches a range of records and columns for 
specified string constructions.  Records satisfying the string selection 
expression are deleted. 
NOTE:  At the completion of an FD operating selection criteria is set to the 
deleted records. 
FD is always a record command. 
Examples: 
*FD200-5000,/GOODELF/EOR/SARUTAN/ means search records 200 through 5000 for 
the strings GOODELF and SARUTAN.  Delete any records that contain either 
string, but retain records that contain neither or both. 
*FD1-10,/Q/,1,1 
means delete all records between 1 and 10 inclusive that begin with the 
character Q. 
Related Commands: 
FS, FT, DE, MD 
00002
00003
00001
00004
Format: 
name[.[account][.password]] 
Parameters: 
name   -   is a string of 1 to 31 characters that assigns an identifying name 
to a file.  The valid characters for this parameter are A through Z, a through 
z, the digits 0 through 9, and the following characters:  $, _, :, -.  The * 
character is used as a first character to identify temporary star files. 
Temporary star files are automatically deleted at job-end or log-off.  They 
cannot be renamed except as another star file. 
account   -   is a string of 1 to 8 characters that identifies a file 
directory.  The valid characters for the account parameter are the same as 
those for the name parameter. Accounts are created by the system manager.  If 
unspecified, the user's default file management account is assumed. 
password   -   is a string of 1 to 8 characters that provides a 
user-controlled security check for file access.  The password parameter can 
consist of any ASCII characters (including non-printing characters and control 
sequences).  The user must include the password if the file is password 
protected. 
Description: 
EDIT fids may only be disk files. 
Examples: 
*EDIT PITHECUS 
means open the file named PITHECUS. 
*EDIT FIG.COSMIC 
means open the file FIG in account COSMIC 
*EDIT GAIUS.JULIUS.CAESAR 
means open the file GAIUS, the account JULIUS, with password CAESAR. 
Usage Note: 
The FID component is used with File Manipulation Commands.  EDIT does not 
support tape or device input or output (except the OL command, which prints at 
the line printer). 
00002
00003
00001
00004
    File commands may be classified into the following categories: 
    File Manipulation                         Session Attribute 
    BUILD     - Create new file.              BP   - Set blank preservation. 
    COPY      - Copy a file.                  CRPT - Set data encryption seed. 
    DELETE    - Delete a file.                CR   - Set carriage return. 
    DIRECTORY - Sets directory account.       RP   - Set record preservation. 
    EDIT      - Open file for updating.       TA   - Set tab stops. 
    END       - Exit EDIT.                    TABC - Set tab compression. 
    EXAMINE   - Open file for reading.        TABX - Set tab expansion. 
    MERGE     - Merge a file into another.    TYPE - Set filetype code. 
    READ      - Read command file.            VE   - Set verification mode. 
    Information 
    HELP    - Supply information. 
    LIST    - List files. 
    STATUS  - Display EDIT status. 
Rules: 
1.  File commands can be issued at any time while the user is in EDIT. 
2.  File manipulation commands create, open, close, copy, delete, merge, and 
    execute files. 
3.  When a file manipulation command is issued, any open file is closed prior 
    to execution of the command.  When this takes place, the following message 
    is printed: 
    *   EDIT STOPPED 
4.  Informational commands supply information about EDIT, the current status 
    of the editing session, and the current state of disk storage. 
5.  Session attribute commands determine the characteristics of the editing 
    session. 
00001
EDIT can access file organizations other than keyed.  The following 
restrictions apply: 
Relative files can be updated in EDIT, but record lengths must be maintained. 
Relative files are assumed to have relative keys; i.e., the first record is 
1.000, the second 2.000, etc. 
Consecutive, Unit Record, and Indexed files can be opened for examination via 
the EDIT or EXAMINE command.  These files can be updated via EDIT, with the 
restriction that record length cannot be extended, and records may not be 
deleted.  These files should be copied (via the EDIT COPY command) in EDIT 
keyed format if extensive updating is to be performed. 
When EDIT builds a new file, the type is SE unless the EDIT TYPE command is 
used to specify a file type.  For the EDIT COPY command, unless the TYPE CODE 
is used, the TYPE field is not touched, i.e., it is the same as it was before 
a replacement type COPY.  If the COPY builds a new file, and the TYPE CODE was 
not used in the COPY command, the new file will have the same TYPE as the 
input file for the COPY command. 
Syntax: 
FS n1[-n2],sse[,c1[,c2]] 
Parameters: 
n1   -   is the starting key of the range of records to be searched. 
n2   -   is the ending key of the range of records to be searched.  If 
omitted, only record n1 is searched. 
sse   -   is the string selection expression.  See the SSE component for a 
complete description.  The basic format of the sse is: 
[NOT][j]string1[{AND|OR|EOR}[,NOT][j]string2]... 
c1   -   is the starting column for the search.  The default is 1. 
c2   -   is the ending column for the search.  The default is 256. 
Only columns c1 through c2 of records n1 through n2 are searched for the sse. 
Partial matches are not recognized. 
Description: 
The FS (Find String) command searches a range of records and columns for 
specified string constructions.  The keys of records satisfying the string 
selection expression are printed.  FS is always a record command. 
Examples: 
*FS 41,/BALTOH/ 
means search record 41 for the string BALTOH, print the key if it does so. 
*FS1-5,/HERMES/AND/TRISTEMEGUS/ 
means search records 1 through 5 for the strings HERMES and TRISTEMEGUS. 
Print the keys of any records that contain both. 
Related Commands: 
FD, FT, TY 
00002
00003
00001
00004
Syntax: 
FT n1[-n2],sse[,c1[,c2]] 
Parameters: 
n1   -   is the starting key of the range of records to be searched. 
n2   -   is the ending key of the range of records to be searched.  If 
omitted, only record n1 is searched. 
sse   -   is the string selection expression.  See the SSE component for a 
complete description.  The basic format of the sse is: 
[NOT][j]string1[{AND|OR|EOR}[,NOT][j]string2]... 
c1   -   is the starting column for the search.  The default is 1. 
c2   -   is the ending column for the search.  The default is 256. 
Only columns c1 through c2 of the records n1 through n2 are searched for the 
sse.  Partial matches are not recognized. 
Description: 
The FT (Find and Type) command searches a range of records and columns for 
specified string constructions.  Records satisfying the string selection 
expression are printed.  FT is always a record command. 
Examples: 
*FT137-1341,/OXEX/ 
means search records 137 through 1341 for the string OXEX.  Print the records 
that satisfy the search. 
*FT1-100,/QQQ/OR/PPP/,1,10 
means search columns 1 through 10 of records 1 through 100 for the strings QQQ 
or PPP.  Print all records that contain either or both string. 
Related Commands: 
TY, TS, FS, FD 
00002
00003
00001
00004
Syntax: 
HELP [(fid)] [TOPICS] [keyword1] [-] [keyword2] 
Note:  The following elements can be specified in any order: 
         fid 
         TOPICS 
         [keyword1] [-] [keyword2] 
For example, HELP (fid) keyword1 - keyword2 TOPICS is acceptable. 
Parameters: 
fid    specifies the processor name (for example, PCL).  If fid is omitted, 
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
*HELP BUILD 
means print the syntax of the BUILD command, prompt for more information. 
*HELP BUILD SYNTAX 
means the same as the above example. 
*HELP MERGE EXAMP 
means print an example(s) of the MERGE command. 
*HELP TOPICS 
means print all topic names in the EDIT help file. 
*HELP TOPICS C - D 
means print all concept topic names between C and D in the EDIT help file. 
*HELP TOPICS C - 
means print all command topic names from C to Z in the EDIT help file. 
*HELP TA - TABX 
means print the entire messages for commands TA, TABC, and TABX. 
*HELP BUILD - BUILD 
means print the entire BUILD message. 
Related Commands: 
STATUS 
00002
00003
00001
00004
A 
  AD Command - 
      HELP AD 
  AP Command - 
      HELP AP 
B 
  BP Command - 
      HELP BP 
  BREAK Key Function - 
      HELP BREAK 
  BUILD Command -   
    EDIT - 
      HELP BUILD SYNTAX: 
  BUILD Command - 
      HELP BUILD 
C 
  CI Command - 
      HELP CI 
  CL Command - 
      HELP CL 
  CM Command - 
      HELP CM 
  A Command - 
      HELP  A 
  components, EDIT - 
      HELP COMPONENTS 
  CONTROL-D Function - 
      HELP CONTROL_D 
  CONTROL-J Function - 
      HELP CONTROL_J 
  COPY Command -   
    EDIT - 
      HELP COPY SYNTAX: 
  COPY Command - 
      HELP COPY 
  CP Command - 
      HELP CP 
  CR Command - 
      HELP CR 
  CRPT Command - 
      HELP CRPT 
  CT Command - 
      HELP CT 
D 
  D Command - 
      HELP D 
  Data Control Blocks - 
      HELP DCBS 
  Data Control Blocks (DCBs) -   
    EDIT - 
      HELP DCBS 
  DE Command - 
      HELP DE 
  DELETE Command -   
    EDIT - 
      HELP DELETE PARAMETERS: 
  DELETE Command - 
      HELP DELETE 
  DIRECTORY Command -   
    EDIT - 
      HELP DIRECTORY SYNTAX: 
  DIRECTORY Command - 
      HELP DIRECTORY 
E 
  E Command - 
      HELP E 
  EDIT -   
    Add command - 
      HELP AD DESCRIPTION: 
    Align command - 
      HELP  A DESCRIPTION: 
    Append command - 
      HELP AP DESCRIPTION: 
    Blank preserve command - 
      HELP BP DESCRIPTION: 
    carriage return command - 
      HELP CR DESCRIPTION: 
    column command - 
      HELP CL DESCRIPTION: 
    commentary and type command - 
      HELP CT DESCRIPTION: 
    commentary command - 
      HELP CM DESCRIPTION: 
    Copy interlacing command - 
      HELP CI DESCRIPTION: 
    copy protected command - 
      HELP CP PARAMETERS: 
    data encryption command - 
      HELP CRPT DESCRIPTION: 
    default account - 
      HELP DIRECTORY DESCRIPTION: 
    delete record command - 
      HELP DE DESCRIPTION: 
    delete string command - 
      HELP D DESCRIPTION: 
    End If command - 
      HELP EI DESCRIPTION: 
    extend command - 
      HELP E DESCRIPTION: 
    file type - 
      HELP FILE_TYPES 
      HELP COPY DESCRIPTION: 
    file type command - 
      HELP TYPE DESCRIPTION: 
    find and delete command - 
      HELP FD DESCRIPTION: 
    Find and Type command - 
      HELP FT DESCRIPTION: 
    Find String command - 
      HELP FS DESCRIPTION: 
    Insert After command - 
      HELP IA PARAMETERS: 
    Insert Before command - 
      HELP IB DESCRIPTION: 
    insert Preceding command - 
      HELP P DESCRIPTION: 
    Insert Protected command - 
      HELP IP DESCRIPTION: 
    Insert Suppress command - 
      HELP IS DESCRIPTION: 
    Jump command - 
      HELP JU DESCRIPTION: 
    locating a string - 
      HELP FS DESCRIPTION: 
      HELP FT DESCRIPTION: 
      HELP S DESCRIPTION: 
    Move and Delete command - 
      HELP MD PARAMETERS: 
    Move and Keep command - 
      HELP MK DESCRIPTION: 
    Output to lineprinter command - 
      HELP OL DESCRIPTION: 
    Overwrite string command - 
      HELP O DESCRIPTION: 
    Quit Record command - 
      HELP QR DESCRIPTION: 
    record length preserve command - 
      HELP RP DESCRIPTION: 
    renumber command - 
      HELP RN DESCRIPTION: 
    review record command - 
      HELP RR DESCRIPTION: 
    rounding command - 
      HELP ROUNDING DESCRIPTION: 
    searching for a string - 
      HELP FS DESCRIPTION: 
      HELP FT DESCRIPTION: 
      HELP S DESCRIPTION: 
    Select editing range command - 
      HELP SE DESCRIPTION: 
    setting tabs - 
      HELP TA DESCRIPTION: 
    Shift Left command - 
      HELP L DESCRIPTION: 
    shift Right command - 
      HELP  R DESCRIPTION: 
    Substitute command - 
      HELP S DESCRIPTION: 
    tab characters command - 
      HELP TABC DESCRIPTION: 
    tab command - 
      HELP TA DESCRIPTION: 
    tab exchange command - 
      HELP TABX DESCRIPTION: 
    type changed commands - 
      HELP TX DESCRIPTION: 
    type command - 
      HELP TY DESCRIPTION: 
    type compressed command - 
      HELP TC DESCRIPTION: 
    type next command - 
      HELP TN DESCRIPTION: 
    type previous - 
      HELP TP DESCRIPTION: 
    type suppressed - 
      HELP TS DESCRIPTION: 
    Verify command - 
      HELP VE DESCRIPTION: 
  EDIT Command -   
    EDIT - 
      HELP EDIT SYNTAX: 
  EDIT Command - 
      HELP EDIT 
  EDIT Commands - 
      HELP COMMANDS 
  EDIT Components - 
      HELP COMPONENTS 
  EDIT Concepts - 
      HELP CONCEPTS 
  EI Command - 
      HELP EI 
  EL Command - 
      HELP EL 
  END Command -   
    EDIT - 
      HELP END SYNTAX: 
  END Command - 
      HELP END 
  =(equal sign) Substitution - 
      HELP EQUAL 
  EXAMINE Command -   
    EDIT - 
      HELP EXAMINE SYNTAX: 
  EXAMINE Command - 
      HELP EXAMINE 
F 
  F Command - 
      HELP F 
  FD Command - 
      HELP FD 
  FID Component - 
      HELP FID 
  File Commands - 
      HELP FILE_COMMANDS 
  File Organization, EDIT - 
      HELP FILE_ORGS 
  File Types - 
      HELP FILE_TYPES 
      HELP TYPE SYNTAX: 
  FS Command - 
      HELP FS 
  FT Command - 
      HELP FT 
H 
  HELP Command - 
      HELP HELP 
I 
  IA Command - 
      HELP IA 
  IB Command - 
      HELP IB 
  IF Command -   
    EDIT - 
      HELP IF PARAMETERS: 
  IF Command - 
      HELP IF 
  IN Command - 
      HELP IN 
  Intrarecord Commands - 
      HELP INTRARECORD_COMMANDS 
  IP Command - 
      HELP IP 
  IS Command - 
      HELP IS 
J 
  JU Command - 
      HELP JU 
K 
  Key Formats - 
      HELP KEY_FORMATS 
L 
  L Command - 
      HELP L 
  Linefeed Function - 
      HELP LINEFEED 
  LIST Command -   
    EDIT - 
      HELP LIST PARAMETERS: 
  LIST Command - 
      HELP LIST 
M 
  MD Command - 
      HELP MD 
  MERGE Command - 
      HELP MERGE 
  MK Command - 
      HELP MK 
N 
  NO Command - 
      HELP NO 
O 
  O Command - 
      HELP O 
  OL Command - 
      HELP OL 
  Organization of Files - 
      HELP FILE_ORGS 
P 
  P Command - 
      HELP P 
Q 
  QR Command - 
      HELP QR 
R 
  R Command - 
      HELP  R 
  READ Command -   
    EDIT - 
      HELP READ SYNTAX: 
  READ Command - 
      HELP READ 
  Record Commands - 
      HELP RECORD_COMMANDS 
  RF Command - 
      HELP RF 
  RL Command - 
      HELP RL 
  RN Command - 
      HELP RN 
  ROUNDING Command - 
      HELP ROUNDING 
  RP Command - 
      HELP RP 
  RR Command - 
      HELP RR 
S 
  S Command - 
      HELP S 
  SE Command - 
      HELP SE 
  Selection Criteria - 
      HELP CRITERIA 
  SS Command - 
      HELP SS 
  SSE Component - 
      HELP SSE 
  ST Command - 
      HELP ST 
  STATUS Command -   
    EDIT - 
      HELP STATUS SYNTAX: 
  STATUS Command - 
      HELP STATUS 
  STRING Component - 
      HELP STRING 
T 
  TA Command - 
      HELP TA 
  TABC Command - 
      HELP TABC 
  TABX Command - 
      HELP TABX 
  TC Command - 
      HELP TC 
  TN Command - 
      HELP TN 
  TP Command - 
      HELP TP 
  TS Command - 
      HELP TS 
  TX Command -   
    EDIT - 
      HELP TX SYNTAX: 
  TX Command - 
      HELP TX 
  TY Command - 
      HELP TY 
  TYPE Command - 
      HELP TYPE 
U 
  Up Arrow Function - 
      HELP UP_ARROW 
V 
  VE Command - 
      HELP VE 
W 
  WILDCARD Component - 
      HELP WILDCARD 
X 
  XUG Services - 
      HELP XUG_SERVICES 
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
HELP_INDEX
Syntax: 
IA [n][,i] 
Parameters: 
n   -   specifies the key after which insertion is to take place.  The default 
is the highest key in the selection criteria. 
i   -   specifies the increment for insertions.  The default is 1 or the 
last-issued increment in a previous command. 
Description: 
The IA (Insert After) command inserts records following a specified key.  The 
increment i is added to key n, and the resulting key is printed as a prompt. 
Successive insertions are incremented by i.  IA does not permit the 
replacement of existing records.  Record insertion is terminated when any of 
the following events takes place: 
1.  A null line (an unaccompanied carriage return) is entered. 
2.  A record exists whose key is greater than the key of the last inserted 
    record, and is less than the incremented key. 
3.  An attempt is made to insert a record having a key larger than 99999.999; 
    in this case, an error message is printed. 
Examples: 
*IA 50,.1 
means insert record 50.1, then 50.2, then 50.3, etc. 
Related Commands: 
IB, IN, IP, IS 
00002
00003
00001
00004
Syntax: 
IB [n][,i] 
Parameters: 
n   -   specifies the key previous to which insertion is to take place.  The 
default is the lowest key in the selection criteria. 
i   -   specifies the increment that determines the key of each successive 
record to be inserted.  The default is 1 or the last issued increment in a 
previous command. 
Description: 
The IB (Insert Before) command inserts records before a specified record.  The 
increment i is added to the key immediately preceding key n.  Successive 
insertions are incremented by i.  IB does not allow the replacement of 
records.  Record insertion is terminated when any of the following events 
takes placed: 
1.  A null line (an unaccompanied carriage return) is entered. 
2.  A record exists whose key is greater than the key of the last inserted 
    record, and is less than the incremented key. 
3.  An attempt is made to insert a record having a key larger than 99999.999; 
    in this case, an error message is printed. 
IB is always a record command. 
Examples: 
*IB10,.5 
means locate the record immediately before record 10 (e.g., record 8) add .5 
and continue insertions, with .5 as an increment. 
Related Commands: 
IA, IN, IP, IS 
00002
00003
00001
00004
Syntax: 
[...;]IF sse[,c1[,c2]];... 
Parameters: 
sse   -   is the string selection expression.  See the SSE component for a 
complete description.  The basic format of the sse is: 
[NOT][j]string1[{AND|OR|EOR}[,NOT][j]string2]... 
c1   -   is the start column for the string selection search.  The default is 
1. 
c2   -   is the ending column for the string selection search.  The default is 
256. 
Description: 
IF evaluates a string selection expression.  If the sse proves true, the 
intrarecord commands immediately following the IF on the command line are 
executed.  If the sse proves false, command execution begins at the next EL or 
EI command at the same nesting level as the IF.  IF is always an intrarecord 
command. 
Examples: 
*IF/*/,1,1;DE;EI 
means delete all records that have an asterisk in column one. 
Related Commands: 
EI, EL, QR, RL 
00002
00003
00001
00004
Syntax: 
IN [n][,i] 
Parameters: 
n   -   specifies the key of the first record to be inserted.  If omitted, the 
increment is added to the highest record in the selection criteria to obtain a 
value for n. 
i   -   specifies the increment that determines the key of each successive 
record to be inserted (following n).  The default is 1 or the last-specified 
increment in a previous command. 
Description: 
IN inserts records into a file.  If record n already exists, it is replaced, 
unless a null line is typed in response to the prompt for n, in which case the 
original record is retained.  Record insertion is terminated when any of the 
following events takes place: 
1.  A null line (an unaccompanied carriage return) is entered. 
2.  A record exists whose key is greater than the key of the last inserted 
    record, and is less than the incremented key. 
3.  An attempt is made to insert a record having a key larger than 99999.999; 
    in this case, an error message is printed. 
IN is always a record command. 
IN acts like AP if the whole file is selected in that it will find the last 
key in the file and INsert after that key, not 99999.999 as it previously did. 
IN now works for Consecutive files. If no start is specified, IN will act just 
like AP. If a start is specified, it must be passed the last record in the 
file. If not, an error will occur. Also, an increment is now allowed on the IN 
command; if this increment is anything other than 1, a warning message will 
inform you that EDIT is assuming an increment of 1. 
Examples: 
*IN5 
means replace record 5 (if it exists) and use the default increment for 
successive insertions. 
*IN,.01 
means add .01 to the highest numbered record in the selection criteria, and 
then increment by .01 for successive insertions. 
Related Commands: 
IA, IB, IP, IS 
00002
00003
00001
00004
Intrarecord commands can be classified into the following categories: 
String Manipulation                          Miscellaneous 
A  - Align columns.                          CI - Copy interlacing. 
D  - Delete string.                          CL - Define editing range. 
E  - Overwrite string, blank fill.           CP - Copy protected. 
F  - Insert string, following.               JU - Jump to new sequence. 
L  - Shift image left.                       NO - No change. 
O  - Overwrite string.                       RF - Reverse blank preservation. 
P  - Insert string, preceding.               TX - Print changed records. 
R  - Shift image right. 
S  - Substitute string. 
Conditional Execution 
EI - End conditional command area. 
EL - Else conditional command area. 
IF - Conditional command execution. 
QR - Quit processing current record. 
RL - Return to beginning of command line. 
Rules: 
1.  Intrarecord commands operate only upon records that satisfy the current 
    selection criteria.  They never alter the selection criteria. 
2.  Intrarecord commands can be linked together on a single line through the 
    use of a semicolon (;).  For example, the command sequence 
    *SE 98-100 
    *TY 
    *0/TEMP/S/PMET/ 
    sets the selection criteria to all columns of records 98-100, prints the 
    records (TY), and then changes all occurrences of string TEMP to string 
    PMET.  This sequence could also have been entered as: 
    *SE98-100;TY;0/TEMP/S/PMET/ 
    In this case, the TY and the S command operate upon each record in 
    sequence; i.e., a record is printed, then altered, the next is printed, 
    then altered, etc.  When entered on separate lines, the entire range is 
    printed, and then the entire range is altered. 
    Note that the SE command can be included in a multicommand line, but only 
    if it is the first command on the line.  The TY, TS, TC, DE, AD, and RR 
    commands, when issued without parameters, function as intrarecord 
    commands; they do not change the selection criteria when so issued. 
3.  If a string manipulation command alters a single string, the asterisk 
    prompt is printed, and further commands can be issued.  If no strings or 
    more than one string is altered a message is printed declaring the number 
    of strings that were altered.  The asterisk prompt is then printed. 
4.  Conditional execution commands are used in sophisticated word 
    manipulations using multicommand lines of intrarecord commands that are 
    executed only if certain conditions are satisfied.  When used with the 
    READ command, entire word-processing programs can be constructed that 
    analyze and alter text and data. 
5.  The CP and CI commands move records from one place to another without 
    altering the current selection criteria.  The CL command defines an 
    editing range of columns that can differ from the range used for record 
    selection.  The RF command temporarily reverses the blank preservation 
    mode.  The TX command is a special command that prints a record if it is 
    altered.  The NO and JU commands are only used in operations initiated by 
    the SS and ST commands. 
00001
Syntax: 
IP [n][,i] 
Parameters: 
n   -   specifies the key of the first record to be inserted.  If omitted, the 
increment is added to the highest record in the selection criteria to obtain a 
value for n.  An error message is issued if record n exists. 
i   -   specifies the increment that determines the key of each successive 
record to be inserted (following n).  The default is 1 or the last-specified 
increment in a previous command. 
Description: 
The IP (Insert Protected) command inserts records into a file, but does not 
permit the replacement of existing records.  Record insertion is terminated 
when any of the following events takes place: 
1.  A null line (an unaccompanied carriage return) is entered. 
2.  A record exists whose key is greater than the key of the last inserted 
    record, and is less than the incremented key. 
3.  An attempt is made to insert a record having a key larger than 99999.999; 
    in this case, an error message is printed. 
4.  A record with key equal to n exists (as stated above). 
IP is always a record command. 
Examples: 
*IP5 
means insert record 5 (if it doesn't already exist) and use the default 
increment for successive insertions. 
*IP,.01 
means add .01 to the highest numbered record in the selection criteria, and 
then increment by .01 for successive insertions. 
Related Commands: 
IS, IA, IB, IN 
00002
00003
00001
00004
Syntax: 
IS [n][,i] 
Parameters: 
n   -   specifies the key of the first record to be inserted.  If omitted, the 
increment is added to the highest record in the selection criteria to obtain a 
value for n. 
i   -   specifies the increment that determines the key of each successive 
record to be inserted (following n).  The default is 1 or the last-specified 
increment in a previous command. 
Description: 
The IS (Insert Suppress) command inserts records into a file, but suppreses 
the record key, prompting each record with a period (.)  rather than with a 
key. 
If record n already exists, it is replaced, unless a null line is typed in 
response to the prompt for n, in which case the original record is retained. 
Record insertion is terminated when any of the following events takes place: 
1.  A null line (an unaccompanied carriage return) is entered. 
2.  A record exists whose key is greater than the key of the last inserted 
    record, and is less than the incremented key. 
3.  An attempt is made to insert a record having a key larger than 99999.999; 
    in this case, an error message is printed. 
IS is always a record command 
IS now works for Consecutive files. If no start is specified, IS will act just 
like AP. If a start is specified, it must be passed the last record in the 
file. If not, an error will occur. Also, an increment is now allowed on the IS 
command; if this increment is anything other than 1, a warning message will 
inform you that EDIT is assuming an increment of 1. 
Examples: 
*IS5,.1 
means insert at line 5, increment successive inserts by .1, prompt with 
periods. 
Related Commands: 
IA, IB, IN, IP 
00002
00003
00001
00004
Syntax: 
JU n 
Parameters: 
n   -   specifies the record to which stepping is to be transferred.  This 
must lie within the range of records in the selection criteria. 
Description: 
The JU (JUmp) command can only be issued during set and step operations, which 
are initiated by the SS and ST commands.  JU allows the user to jump forwards 
and backwards among the records being accessed.  JU can be issued on a line by 
itself, or as the last command on a multiple command line. 
JU is always an intrarecord command. 
Examples: 
**JU5 
means, during set and step, jump to record 5. 
Related Commands: 
NO, ST, SS 
00002
00003
00001
00004
EDIT builds keyed files.  Each record in an EDIT keyed file is represented by 
a sequence number of the format: 
nnnnn.nnn 
where n represents a decimal digit.  When referencing EDIT keys, only 
significant digits need be typed.  For example: 
    550    implies    00550.000 
    5.5    implies    00005.500 
   .055    implies    00000.055 
EDIT creates variable length records that range from 1 to 256 characters in 
length.  Trailing blanks are not written into records unless the RP command 
enables record preservation. 
Syntax: 
[j]/string/Ls    or    kLs 
Parameters: 
j   -   is a positive integer specifying the occurrence of the string to be 
shifted.  The j=0 option is invalid for this command.  The default is 1. 
string   -   is a string whose first character marks the column in the record 
that is to be shifted to the left.  See the STRING component for a description 
of the string construct. 
s   -   is a positive integer indicating the number of column positions for 
the shift to the left. 
k   -   is the column that is to be shifted to the left.  If k=0, the last 
column in the record is assumed. 
Description: 
The L (shift Left) command shifts a portion of a record to the left. 
If BP is ON, the entire record to the left of k (or the first character in the 
string) is shifted to the left.  If BP is OFF, blank fields to the left of k 
will be compressed, if possible, to a single blank to accommodate the shift; a 
field of blanks is created on the right of the shifted portion of the record. 
Characters to the left of k are overwritten as required to shift s number of 
columns. 
L is always an intrarecord command. 
Examples: 
*SE10;2/SSSS/L10 
means locate the second occurrence of the string SSSS in record 10, and shift 
the column (marked by the first S) 10 column positions to the left. 
*20L10 
means shift column 20 of all records in the current selection criteria 10 
columns to the left. 
Related Commands: 
A, R 
00002
00003
00001
00004
LIST
If a single linefeed character is entered in response to the asterisk prompt, 
the selection criteria range (i.e., the SE range) is set to all columns of the 
next record following the upper limit of the current range.  That record is 
then printed in the format specified by the last issued TY, TS, TC, or RR 
command.  The default is TY.  The linefeed key is also used in set and step 
operations to obtain the next record. 
Syntax: 
L[IST][(A)][filename][.[account]] 
Parameters: 
A   -   means list the files with their attributes.  If unspecified, only the 
names of the files are listed, except if filename is specified, in which case 
the default is listing with attributes. 
filename   -   indicates to list the requested disk file with attributes. 
account   -   specifies the account whose files are to be listed.  If 
unspecified, the user's directory account is the default.  The specified 
account should be one to which the user has authorized access. 
See PCL LIST command for the complete syntax. 
Description: 
LIST calls the PCL processor to list the files in an account.  List is always 
a file command. 
Examples: 
*LIST .DEE 
means list the names of the files in account DEE. 
*L JOHN.DEE 
means list, with attributes, file JOHN in account DEE. 
*LIST (A) .DEE 
means list, with attributes, all the files in account DEE. 
Related Commands: 
EDIT, BUILD, COPY, MERGE 
00002
00003
00001
00004
MERGE
Syntax: 
MD[P] n1[-n2],n3[-n4][,i] 
Parameters: 
P   -   specifies that the range n3 to n4 must not contain any existing 
records; otherwise the command aborts. 
n1   -   is the starting key of the range of records to be moved. 
n2   -   is the final key of the range of records to be moved.  If omitted, 
only record n1 is moved. 
n3   -   is the string key for the target range of records. 
n4   -   is the ending key of the target range of records.  If omitted, the 
move is halted when a previously existing record is encountered. 
i   -   is the increment to be used for renumbering the moved records.  The 
default is 1 or the last issued increment in a previous command. 
Description: 
The MD (Move and Delete) command transfers a range of records from one part of 
a file to another.  The original records are deleted. 
The ranges n1 through n2 and n3 through n4 cannot overlap.  If the ranges do 
overlap, the command will still work provided that by the time EDIT gets 
around to reusing a key that overlaps, the data that used to occupy that space 
has been moved (see example below).  If the MDP form is used, the range n3 
through n4 must not contain any records.  With MD, the range n3 through n4 is 
deleted prior to the move.  If the renumbered records reach a previously 
existing record, the command aborts, and a message is printed specifying the 
last record moved from n1 through n2, and the total number of records moved. 
Records not successfully transferred are not deleted from their original 
position. 
MD is always a record command. 
Examples: 
*MD5-10,20-30 
means delete records 20 through 30 and move records 5 through 10 to the 
vacated area, incrementing with the default increment.  Records 5 through 10 
are deleted from the file. 
*MDP100-200,50,.01 
means move records 100-200 to line 50; the first record is 50, the second 
50.01, the third 50.02, etc.  The operation halts when an existing record is 
encountered. 
*MD 1-200,.5,.5 
This overlap of ranges will work since by the time EDIT gets to reuse KEY 
1.000, it will have moved the old 1.000 to .500; thus, no data is lost. 
Related Commands: 
MK, DE, RN 
00002
00003
00001
00004
Syntax: 
{M|ERGE} fid1[,n1[-n2]] {ON|TO|OVER|INTO} fid2,n3[-n4][,i] 
Parameters: 
fid1   -   is the file containing the records to be transferred, i.e., the 
merge file. 
n1   -   is the key of the first record in the range to be transferred.  If 
omitted, the entire file is transferred. 
n2   -   is the key of the final record in the range to be transferred.  If 
omitted, only record n1 is transferred. 
fid2   -   is the file to which the records are transferred, i.e., the target 
file.  If fid2 does not exist, a new file is created. 
n3   -   is the key of the first record in the target range of records.  If it 
exists in the target file, it is deleted. 
n4   -   is the key of the last record in the target range of records.  If 
specified, the range n3 to n4 is deleted from the target file. 
i   -   specifies the increment for the sequencing of records in the target 
file.  The default is 1 or the last-issued increment in a previous command. 
Description: 
MERGE transfers records from one keyed file to another. 
If the range n3 to n4 is not sufficiently large to contain the merged records 
(as incremented by i), the operation is halted and a message is printed: 
**   Cutoff at n5 (n6) 
where 
n5   -   is the last key assigned in fid2. 
n6   -   is the key of the last record moved from fid1. 
At completion, fid2 is open for editing.  An error results if fid1 does not 
exist, or if fid2 is not keyed. 
MERGE is always a file command. 
Examples: 
*MERGE LEMEGETON INTO QBL,1-22,1 
means delete records 1 through 22 in file QBL, and insert the file LEMEGETON 
in the area vacated, beginning with record 1 and incrementing by 1. 
*MERGE O_G_D,1-5 INTO O_T_A,333 
means take records 1 through 5 from file O_G_D and move them to file O_T_A, 
begin sequencing at key 333.  It replaces 333 if it exists. 
Related Commands: 
COPY, BUILD, EXAMINE, EDIT 
00002
00003
00001
00004
Syntax: 
MK[P] n1[-n2],n3[-n4][,i] 
Parameters: 
P   -   specifies that the range n3 to n4 must not contain any existing 
records; otherwise the command aborts. 
n1   -   is the starting key of the range of records to be moved. 
n2   -   is the final key of the range of records to be moved.  If omitted, 
only record n1 is moved. 
n3   -   is the starting key for the target range of records. 
n4   -   is the ending key of the target range of records.  If omitted, the 
move is halted when a previously existing record is encountered. 
i   -   is the increment to be used for renumbering the moved records.  The 
default is 1 or the last issued increment in a previous command. 
Description: 
The MK (Move and Keep) command transfers a range of records from one part of a 
file to another.  The original records are retained. 
The ranges n1 through n2 and n3 through n4 cannot overlap.  If the MKP form is 
used, the range n3 through n4 must not contain any records.  With MK, the 
range n3 through n4 is deleted prior to the move.  If the renumbered records 
reach a previously existing record, the command aborts, and a message is 
printed specifying the last record moved from n1 through n2, and the total 
number of records moved from their original position. 
Examples: 
*MK5-10,20-30 
means delete records 20 through 30 and move records 5 through 10 to the 
vacated area, incrementing with the default increment.  Records 5 through 10 
are retained in the file. 
*MKP100-200,50,.01 
means move records 100 to 200 to line 50; the first record is 50, the second 
50.01, the third 50.02, etc.  The operation halts when a existing record is 
encountered. 
Related Commands: 
MD, RN 
00002
00003
00001
00004
Syntax: 
NO 
Parameters: 
None. 
Description: 
NO specifies that the currently accessed record should not be altered.  If 
used during set and step operations (initiated by the SS and ST commands), NO 
means skip to the next selected record. 
NO is always an intrarecord command. 
Examples: 
**NO 
means, during set and step, skip to the next record. 
IF /B/,2,2;NO;EL;/A/S/X/ 
means if a B is in column 2, then the record is not changed.  Otherwise, 
change the first occurrence of A to X. 
NOTE:  Because the NO command suppresses record updating, it may be used for 
testing the effects of complex edit commands non-destructively.  See example 
below: 
!E SOMEFILE 
*TY 
1.000 THIS IS RECORD ONE 
2.000 THIS IS RECORD TWO 
3.000 THIS IS record THREE 
4.000 THIS IS RECORD FOUR 
* EOF hit after 4.000 
*/record/s/RECORD/;tx;NO 
3.000 THIS IS RECORD THREE 
* EOF hit after 4.000 
* 1 strings changed 
*TY 
1.000 THIS IS RECORD ONE 
2.000 THIS IS RECORD TWO 
3.000 THIS IS record THREE 
4.000 THIS IS RECORD FOUR 
* EOF hit after 4.000 
* END 
Notice that the records have not changed. 
Related Commands: 
SS, ST, JU 
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
Syntax: 
[j]/string1/O/string2/    or kO/string2/ 
Parameters: 
where 
j   -   is a non-negative integer specifying the occurrence of string1 to be 
located in the record.  If j=0, all occurrences are located.  The default is 
1. 
string 1   -   is a string whose first character marks the column at which 
string2 is to overwrite; string1 must lie within the range of columns in the 
selection criteria.  See the STRING component in the introduction to this 
section for a complete description of the string construct. 
string2   -   is the string that is to overwrite the specified area in the 
record. 
k   -   is the start column for the overwriting by string2; i.e., the first 
character of string2 will lie in column k.  This column must lie within the 
range of columns in the selection criteria.  If k=0, the last column in the 
record is assumed. 
Description: 
The O (Overwrite string) command replaces a section of a record with a 
specified string; all columns not overwritten remain unchanged. 
O is always an intrarecord command. 
Examples: 
*SE1;/ABRACADABRA/O/PRESTO/ 
means overwrite the string PRESTO at the beginning of string ABRACADABRA.  The 
resulting string is PRESTODABRA. 
*SE100-200;10O/$/ 
means put a dollar sign ($) in column 10 of records 100 through 200.  Any 
character already in column 10 is replaced; the remainder of the record is not 
altered in any way. 
Related Commands: 
E 
00002
00003
00001
00004
Syntax: 
OL [n1[-n2]] 
Parameters: 
n1   -   specifies the first record to be printed. 
n2   -   specifies the last record to be printed.  If unspecified, only record 
n1 is printed. 
Description: 
The OL (Output to Lineprinter) command prints records at the line-printer. 
If no parameters are specified, the records satisfying the current selection 
criteria are printed. 
OL is always a record command. 
NOTE:  The line-printer device at which the file is printed will be the user's 
default line-printer. 
Examples: 
*OL 
means print the currently open file at the line printer.  Since no parameters 
are specified, the records satisfying the current selection criteria will be 
printed. 
Related Commands: 
TY 
00002
00003
00001
00004
Syntax: 
[j]/string1/P/string2/    or    kP/string2/ 
Parameters: 
j   -   is a non-negative integer specifying the occurrence of string1 to be 
located in the record.  If j=0, all occurrences are located.  The default is 
1. 
string 1   -   is a string whose first character marks the column for the 
insertion of string2; string1 must lie within the range of columns in the 
selection criteria.  See the STRING component for a complete description of 
the string construct. 
string2   -   is the string to be inserted in the record. 
k   -   is the start column for the insertion of string2; i.e., the first 
character of string2 will lie in column k.  This column must lie within the 
range of columns in the selection criteria.  If k=0, the last column in the 
record is assumed. 
Description: 
The P (insert Preceding) command inserts a string preceding a specified column 
or string. 
P is always an intrarecord command. 
Examples: 
*SE3;/POSE/P/PRO/ 
means locate the string POSE in record 3 and precede it with the string PRO, 
forming PROPOSE.  The P in PRO lies in the column where the P in POSE was 
located. 
*SE1-100;1P/!/ 
means place an exclamation point (!) in column 1 of records 1 through 100. 
The record shifts to the right to accommodate the additional character. 
Related Commands: 
F, R, L 
00002
00003
00001
00004
CP-6 EDIT is a source program and data file editor that builds, manipulates, 
and maintains files of ASCII text. 
END
Syntax: 
 ...;QR[;...] 
Parameters: 
None. 
Description: 
The QR (Quit Record) command causes an unconditional skip to the end of the 
command line.  The next record in the records being searched is then 
processed. 
QR is always an intrarecord command. 
Examples: 
*SE20-30,5;IF/LESLY/;QR;EI;DE 
means search records 20 through 30, delete all records that don't contain the 
string LESLY. 
Related Commands: 
EI, IF, EL 
00002
00003
00001
00004
Syntax: 
[j]/string/Rs    or    kRs 
Parameters: 
j   -   is a positive integer specifying the occurrence of the string to be 
shifted.  The j=0 option is invalid for this command.  The default is 1. 
string   -   is a string whose first character marks the column in the record 
that is to be shifted to the right.  See the STRING component for a 
description of the string construct. 
s   -   is a positive integer indicating the number of column positions to be 
shifted to the right. 
k   -   is the column to be shifted to the right.  If k=0, the last column in 
the record is assumed. 
Description: 
The R (shift Right) command shifts a portion of a record to the right. 
If BP is ON, the entire record to the right of k (or the first character in 
the string) is shifted to the right.  If BP is OFF, blank fields to the right 
of k will be compressed, if possible, to a single blank to accommodate the 
shift.  In either case, a field of blanks is created on the left of the 
shifted portion of the record.  If a shift causes characters to exceed 256 
columns, excessive characters are truncated from the end of the record. 
R is always an intrarecord command. 
Examples: 
*SE10;2/SSSS/R10 
means locate the second occurrence of the string SSSS in record 10, and shift 
the column (marked by the first S) 10 column positions to the right. 
*10R20 
means shift column 10 of all records in the current selection criteria 20 
columns to the right. 
Related Commands: 
A, L 
00002
00003
00001
00004
Syntax: 
READ {fid|lname} 
Parameters: 
fid   -   is a disk file containing one EDIT command input line per record. 
The asterisk prompt should not be included. 
lname   -   may be ME or UC.  This is a unit record special name (see Unit 
Record Special Names in Section 2.) 
Description: 
The READ command reads and executes a file of EDIT commands. 
An EDIT command file that includes READ UC accepts input from the user's 
terminal when that command is processed; an EDIT command file that includes 
READ ME accepts input from the current command stream (on-line terminal, or 
the job stream) when that command is processed. 
Note that READ does not necessarily open or close files. 
READ is always a file command. 
Examples: 
*READ COMFILE 
means read the EDIT commands contained in file COMFILE. 
*READ UC 
means read EDIT commands from my terminal. 
Related Commands: 
See the IBEX XEQ command. 
00002
00003
00001
00004
    Record commands may be classified into the following categories: 
    Print Record                           Alter Record 
    OL - Output to the line printer.       AD - Add to the record's end. 
    TC - Type records, compressed.         CM - Insert commentary. 
    TN - Type next records.                CT - Type and insert commentary. 
    TP - Type previous records.            RR - Reread Record. 
    TS - Type records without key. 
    TY - Type records with key. 
    Insert/Delete Record                   Search Record 
    AP - Append to file.                   FD - Find and delete. 
    DE - Delete record.                    FS - Find and type key. 
    IA - Insert records after record.      FT - Find and type record. 
    IB - Insert records before record. 
    IN - Insert records. 
    IP - Insert records, protected. 
    IS - Insert record, period prompt. 
    Reorder Record                         Select Record 
    MD - Move and delete.                  SE - Set selection criteria. 
    MK - Move and keep.                    SS - Select, set, and step. 
    RN - Renumber record.                  ST - Select, set, step, and type. 
Rules: 
Record commands act upon one record or a group of records within a file, and 
can only be issued after a file has been opened for editing via a file 
manipulation command. 
00001
Syntax: 
[...;]RF;... 
Parameters: 
None. 
Description: 
The RF (Reverse Flag) command temporarily reverses the current flag setting 
for blank preservation. 
Commands following the RF command on a multicommand line are executed as if 
the BP setting were reversed.  Blank preservation is restored to its initial 
setting when a new prompt is issued. 
RF is always an intrarecord command. 
Examples: 
*/aa/D;RF;/aa/D 
means delete the string aa, reverse BP mode, and delete the next occurrence of 
aa. 
Related Commands: 
BP 
00002
00003
00001
00004
Syntax: 
...;RL[;...] 
Parameters: 
None. 
Description: 
RL causes a return to the beginning of the command line, and causes the 
current line to be reprocessed, if any changes have been made on the current 
line. 
RL is always an intrarecord command. 
Examples: 
*SE30-40;IF/ /,1,1;/ /D;EI;RL 
means search records 30 through 40; delete all leading blanks. 
Related Commands: 
IF, EL, EI, QR 
00002
00003
00001
00004
Syntax: 
RN n1,n2 
Parameters: 
n1   -   specifies the original key of the record to be renumbered. 
n2   -   specifies the target key. 
Description: 
The RN (ReNumber) command renumbers a single record. 
An error message is printed if key n2 already exists. 
RN is always a record command. 
Examples: 
*RN3,10 
means renumber the record presently numbered 3 so that it is numbered 10. 
Related Commands: 
MK, MD 
00002
00003
00001
00004
Syntax: 
RO[UNDING] {OFF|ON} 
Parameters: 
OFF   -   specifies no KEY rounding will occur. This is the default. 
ON   -   specifies that AP and IN will now round the line number of the next 
line inserted to be a multiple of the INCR. 
Description: 
The RO (ROUNDING) command determines how the next KEY number will be decided. 
If RO ON then the KEY of the next line inserted must be a multiple of INCR. 
Examples: 
*ROUNDING OFF *IN 5.3,1 
     5.300 this is some text you entered 
     6.300 because ROUNDING OFF, key is 6.300 
     7.300 
*ROUNDING ON 
*IN 5.3,1 
     5.300 this is some text you entered 
     6.000 because ROUNDING ON, key is 6.000 (ie. multiple of 1.000) 
     7.000 
Related Commands: 
None. 
00002
00003
00001
00004
Syntax: 
RP {OFF|ON} 
Parameters: 
OFF   -   specifies that record lengths are to be variable.  This is the 
default. 
ON   -   specifies that record lengths are to be maintained. 
Description: 
The RP (Record length Preserve) command determines the handling of record size 
when a file is edited.  If RP is ON, all records are maintained at the current 
record size.  Trailing blanks are not truncated.  Strings added or moved to 
the right are truncated.  Strings deleted or shifted to the left cause blanks 
to be inserted at the end of the record.  Records that are replaced entirely 
take the length of the replacement records. 
If RP is OFF, records are shortened or lengthened as necessary.  Blanks typed 
at the end of records are deleted. 
RP is always a file command. 
Examples: 
*RP ON 
means maintain current record lengths. 
Related Commands: 
BP 
00002
00003
00001
00004
Syntax: 
RR [n1[-n2]] [,col] 
Parameters: 
n1   -   specifies the key of the first record in the range of records to be 
accessed. 
n2   -   is the key of the final record in the range of records to be 
accessed.  If omitted, only record n1 is reread. 
col   -   is the column position on the line being accessed. 
Description: 
The RR (Review Record) command prints records, stopping at the end of each 
record to allow the modification of the record using CP-6 terminal editing 
features. 
If neither n1 nor n2 is specified, the records in the current selection 
criteria are reread. 
The default for col is 0, which is the end of the line.  A positive number 
will be the absolute column number, while a negative number will be the number 
of positions back from the end of the line. 
The maximum length record that can be reread is 255 characters in length. 
NOTE:  The RR command is not meaningful in batch operations. 
RR is a record command if parameters are specified, an intrarecord command if 
parameters are omitted. 
Examples: 
*RR5-6 
means reread records 5 through 6, stop at the end of each printed record and 
allow modification via input editing. 
(the '_' is the cursor position in the next examples) 
RR 1.000 this is the rest of your life_ RR ,1 1.000 _his is the rest of your 
life RR ,0 1.000 this is the rest of your life_ RR ,-5 1.000 this is the rest 
of your_life 
Related Commands: 
AD 
00002
00003
00001
00004
Syntax: 
[j]/string1/S/string2/ 
Parameters: 
j   -   is a non-negative integer specifying the occurrence of string1 that is 
to be located in the record.  If j=0, all occurrences are located and 
replaced.  The default is 1. 
string1   -   is the string to be replaced.  See STRING component for a 
complete description of this construct. 
string2   -   is the replacement string. 
Description: 
The S (Substitute) command locates a string and replaces it with a second 
string.  When j=0, attempts at multiple replacement may cause occurrences of 
string1 to exceed the upper range of columns, if string2 is larger than 
string1. 
S is always an intrarecord command. 
Examples: 
*SE5;/COSMIC/S/UNIVERSAL/ 
means search record 5, and change the first occurrence of string COSMIC to 
string UNIVERSAL. 
*SE3,5,10;2/Q/S/Z/ 
means search columns 5 through 10 of record 3, and change the second Q to a Z. 
Related Commands: 
D 
00002
00003
00001
00004
Syntax: 
SE [n1[-n2][,sse][,c1[,c2]]] 
Parameters: 
n1   -   is the starting key of the range of records.  The default is record 
0. 
n2   -   is the ending key of the range of records.  If n1 is specified, and 
n2 is omitted, only record n1 is selected.  If neither n1 nor n2 are 
specified, the default for n2 is record 99999.999 
sse   -   is the string selection expression.  See the SSE component for a 
complete description.  The basic format of the sse is: 
[NOT][j]string1[{AND|OR|EOR}[,NOT][j]string2]... 
c1   -   is the starting column for range of columns.  The default is 1. 
c2   -   is the ending column for the range of columns.  The default is 256. 
Description: 
The SE (SElect) command sets selection criteria. 
The synonym CH can be substituted for the verb SE.  If no parameters are 
specified, selection criteria are set to the defaults, i.e., all columns of 
all records with no string selection expression. 
Only columns c1 through c2 of records n1 through n2 are searched for the 
string selection expression.  The column settings are ignored if subsequent TY 
or RR commands are entered without parameters. 
All records satisfying the criteria defined become available for intrarecord 
editing. 
SE is always a record command. 
Examples: 
SE1-5 
means set selection criteria to records 1 through 5. 
SE5-10,/PIXIE/ 
means set selection criteria to all records between 5 and 10 inclusive that 
contain the string PIXIE. 
Related Commands: 
SS, ST 
00002
00003
00001
00004
CRITERIA
Syntax: 
SS n1[-n2][,sse][,c1[,c2]] 
Parameters: 
n1   -   is the starting key of the range of records.  The default is record 
0.  If n1 is specified, and n2 is omitted, only record n1 is selected, but the 
default selection range is set from n1 to record 99999.999. 
n2   -   is the ending key of the range of records.  The default is record 
99999.999.  If neither n1 or n2 are specified, the default selection range is 
set from record 0 to 99999.999. 
sse   -   is the string selection expression.  See the SSE component for a 
complete description.  The basic format of the sse is: 
[NOT][j]string1[{AND|OR|EOR}[,NOT][j]string2]... 
c1   -   is the starting column for range of columns.  The default is 1. 
c2   -   is the ending column for the range of columns.  The default is 256. 
Description: 
The SS (Set and Step) command defines the selection criteria, consecutively 
accesses each record in that criteria, prints the key as a prompt, and then 
accepts one line of intrarecord commands to update that record. 
As SS accesses each record, the key followed by two asterisks is printed as a 
prompt.  A single intrarecord command line can then be entered.  Also, DE can 
be entered to delete that one record.  Typing NO and then carriage return 
skips to the next record.  The JU command skips forwards and backwards among 
the selected records.  Linefeed may also be used to obtain the next record. 
Typing just a carriage return terminates the operation, as indicated by a 
single asterisk prompt, but the selection range of records (or default range) 
remains in effect until subsequently reset.  For this reason, the DE command 
at this point will result in the deletion of the entire selection range of 
records. 
SS is always a record command. 
Examples: 
*SS100-200,/TWAIN/ 
means step through all records between 100 and 200 inclusive that contain the 
string TWAIN. 
Related Commands: 
ST, JU, NO 
00002
00003
00001
00004
Format: 
[NOT][j]/string1/[{AND|OR|EOR}[,NOT][j]/string2/]... 
Parameters: 
/string/   -   proves true if the string is entirely present in the range of 
columns being searched.  This is the simplest form of the SSE, and at least 
one string must be present in an SEE. 
NOT/string/   -   proves true if the string is absent in the range of columns 
being searched. 
j/string/   -   proves true if the string occurs at least j times in the range 
of columns being searched.  The default is 1.  The j parameter must be a 
positive integer. 
NOTj/string/   -   proves true if and only if string appears less than j times 
in the range of columns being searched. 
AND   -   indicates that both string selection operators must prove true. 
OR   -   indicates that either string selection operator must prove true. 
EOR   -   indicates that either but not both string selection operators must 
prove true. 
Description: 
When an SSE is specified, the search is satisfied if and only if the SSE 
yields a logical true result.  EDIT performs a linear, left to right search 
when evaluating a record for selection.  If, at the end of this search, the 
expression proves true, the record is selected.  Note that only the selected 
range of columns are searched. 
Examples: 
Using the FT command, the following examples illustrate string selection 
expressions: 
COMMAND                     FIND AND TYPE 
FT1-10,/FISH/               Records 1 to 10 that contain string FISH. 
FT1-10,NOT/FISH/            Records 1 to 10 that don't contain FISH. 
FT1-10,2/FISH/              Records 1 to 10 that contain at least two FISHs. 
FT1-10,NOT5/FROG/           Records 1 to 10 that contain less than five FROGs. 
FT1-10,/FISH/,1,5           Records 1 to 10 that contain FISH in columns 1-5. 
FT1-10,/FROG/AND/FISH/      Records 1 to 10 that contain a FROG and a FISH. 
FT1-10,/FROG/OR/FISH/       Records 1 to 10 that contain FROG or FISH. 
FT1-10,/FISH/AND,NOT/FROG/  Records 1 to 10 that contain FISH, but not FROG. 
FT1-10,/FISH/EOR/SERPENT/   Records 1 to 10 with either FISH or SERPENT, 
                            but not FISH and SERPENT in the same record. 
Usage Note: 
The TY, FT, FS, FD, SE, ST, SS, IF, and EL commands utilize string selection 
expressions. 
00002
00003
00001
00004
Syntax: 
ST n1[-n2][,sse][,c1[,c2]] 
Parameters: 
n1   -   is the starting key of the range of records.  The default is record 
0.  If n1 is specified, and n2 is omitted, only record n1 is selected, but the 
default selection range is set from n1 to record 99999.999. 
n2   -   is the ending key of the range of records.  The default is record 
99999.999.  If neither n1 or n2 are specified, the default selection range is 
set from record 0 to 99999.999. 
sse   -   is the string selection expression.  See the SSE component for a 
complete description.  The basic format of the sse is: 
[NOT][j]string1[{AND|OR|EOR}[,NOT][j]string2]... 
c1   -   is the starting column for range of columns.  The default is 1. 
c2   -   is the ending column for the range of columns.  The default is 256. 
Description: 
The ST (Set, step and Type) command ST defines the selection criteria, 
consecutively accesses each record in that criteria, prints the record, and 
then accepts one line of intrarecord commands to update that record. 
As ST accesses each record, the record is printed, followed by two asterisks 
issued as a prompt.  A single intrarecord command line can then be entered. 
Also, DE can be entered to delete that one record.  Typing NO and then 
carriage return skips to the next record.  The JU command skips forwards and 
backwards among the selected records.  Linefeed may also be used to obtain the 
next record.  Typing just a carriage return terminates the operation, as 
indicated by a single asterisk prompt, but the selection range of records (or 
default range) remains in effect until subsequently reset.  For this reason 
the DE command at this point will result in the deletion of the entire 
selection range of records. 
ST is always a record command. 
Examples: 
*ST300-301,/SQUIRE ALLWORTHY/,100,250 
means step through all records between records 300 to 301 inclusive that 
contain the string SQUIRE ALLWORTHY between columns 100-250 inclusive. 
Related Commands: 
JU, NO, SS 
00002
00003
00001
00004
Syntax: 
(STAT/US | SH/OW) [optionlist] 
Parameters: 
Optionlist is the list of options you want displayed separated by commas. 
Options are FILE/NAME, SE, CL, TA/BS, DIR/ECTORY, MODE, BP, CR, RP, TABX, 
TABC, VE, and RO/OUNDING. 
Description: 
STATUS displays information about the current status of EDIT. 
The first line gives the name of the currently open file; if none, NO FILE 
OPEN is printed.  The next line indicates what is the setting of the current 
selection criteria.  This is followed by the remaining options, with all FLAG 
displays on a single line. 
Examples: 
*STATUS 
FILENAME = QP.MYACCT 
SE   190.000-  210.000,0001,1024 
NO TABS SET 
DIRECTORY: .MYACCT 
EDIT MODE, BP ON, CR OFF, RP OFF, TABX OFF, TABC OFF, VE ON, ROUND ON 
Related Commands: 
None. 
00002
00003
00001
00004
Format: 
/characters/   -   specifies the characters enclosed by the slashes.  A single 
slash may be included in the string by typing two successive slashes. 
'characters'   -   specifies the characters enclosed by the apostrophes.  A 
single apostrophe may be included in the string by typing two successive 
apostrophes. 
#ooo[#ooo]...   -   specifies a series of octal values representing ASCII 
characters. 
Parameters: 
None. 
Description: 
A string is a series of characters. 
Examples: 
Each of the following examples describes the string ABCD: 
/ABCD/ 
'ABCD' 
#101#102#103#104 
Usage Note: 
Strings are used in string selection expression and in many intrarecord 
commands.  Also see the WILDCARD component. 
00002
00003
00001
00004
NOTATION
Syntax: 
TA {F|C|A}    or    TA n1[,n2]...[nn] 
Parameters: 
F   -   sets tabs for FORTRAN at columns 7, 16, and 34. 
C   -   sets tabs for COBOL at columns 8, 12, and 36. 
A   -   sets tabs for Assembly Language (GMAP) at columns 8, 16, and 32. 
n1[n2]...   -   specify column positions (in ascending order) at which tab 
stops are to be set. 
The default is no tab stops. 
Description: 
The TA (TAb) command sets terminal tab stops.  Unlike the tabbing mechanism on 
typewriters, the tab key for a terminal simulates tabbing action.  If no tab 
stops are set via the TA command or the IBEX command TABS, pressing the tab 
key generates a single blank character.  When editing text that contains tab 
characters, tabs must be set for EDIT to insert the proper number of blanks 
for each tab character. 
The TA command interacts with the TABX and TABC commands. 
NOTE:  The performance of tab characters is highly dependent upon the physical 
characteristics of the terminal device. 
TA is always a file command. 
Examples: 
*TA C 
means set tab stops at columns 8, 12, and 36. 
*TA 8,12,36 
means the same as the first example. 
Related Commands: 
TABC, TABX 
00002
00003
00001
00004
Syntax: 
TABC {OFF|ON} 
Parameters: 
OFF   -   specifies blank compression is not to take place.  The default is 
OFF. 
ON   -   specifies that blank compression is to take place. 
Description: 
The TABC (TAB Characters) command determines whether to treat blank fields as 
tab characters, based upon the current tab settings.  If TABC is ON, any 
strings of blanks in a data record written to a file are converted (if 
convenient tab stops have been set) to tab characters; this occurs regardless 
of the TABX setting. 
NOTE:  The performance of tab characters is highly dependent upon the physical 
characteristics of the terminal device. 
TABC is always a file command. 
Examples: 
*TABC ON 
means that blanks are to be converted to tab characters. 
Related Commands: 
TABX, TA 
00002
00003
00001
00004
Syntax: 
TABX {ON|OFF} 
Parameters: 
ON   -   specifies that tab characters are to generate blank fields.  The 
default is ON. 
OFF   -   specifies that tab characters are to be preserved in the files. 
Description: 
The TABX (TAB eXchange) command determines (during read operations) whether to 
treat tab characters literally or to replace them with an appropriate number 
of blanks. 
NOTE:  The performance of tab characters is highly dependent upon the physical 
characteristics of the terminal device. 
TABX is always a file command. 
Examples: 
*TABX OFF 
means preserve tab characters in the file. 
Related Commands: 
TA, TABC 
00002
00003
00001
00004
Syntax: 
TC [n1[-n2][,c1][,c2]]] 
Parameters: 
n1   -   specifies the starting key of the range of records to be printed. 
n2   -   specifies the ending key of the range of records to be printed.  If 
omitted, only record n1 is printed. 
c1   -   specifies the starting column of the range of columns for the 
selection criteria.  The default is 1. 
c2   -   specifies the ending column of the range of columns for the selection 
criteria.  The default is 256. 
Description: 
The TC (Type Compressed) command prints a range of records with keys, 
compressing all strings of blanks into a single blank.  This compression 
affects only printed output-- the records themselves are not altered. 
TC is a record command if parameters are specified, and an intrarecord command 
if parameters are omitted. 
Examples: 
*TC100-200 
means print records 100 through 200, but compress all strings of blanks to a 
single blank. 
Related Commands: 
TY, TS, TN, TP 
00002
00003
00001
00004
Syntax: 
TN n 
Parameters: 
n   -   specifies the number of records to be printed. 
Description: 
The TN (Type Next) command prints records following the highest numbered 
record in the current selection criteria.  It will use the last TY/TS/TC 
format for displaying these records. 
At completion, selection criteria are set to all columns of the printed 
records. 
TN is always a record command. 
Examples: 
*TN 10 
means print the next 10 records following the highest numbered selected 
record. 
Related Commands: 
TP, TY, TC, TS 
00002
00003
00001
00004
Syntax: 
TP n 
Parameters: 
n   -   specifies the number of records to be printed. 
Description: 
The TP (Type Previous) command prints records preceding the lowest numbered 
selected record.  At completion, selection criteria are set to all columns of 
the printed records.  TP is always a record command. 
TP will use the last TY/TS/TC format for displaying the selected records. 
Examples: 
*TP 10 
means print the 10 records preceding the lowest numbered selected record. 
Related Commands: 
TN, TY, TS, TC 
00002
00003
00001
00004
Syntax: 
TS [n1[-n2][,c1][,c2]]] 
Parameters: 
n1   -   specifies the starting key of the range of records to be printed. 
n2   -   specifies the ending key of the range of records to be printed.  If 
omitted, only record n1 is printed. 
c1   -   specifies the starting column of the range of columns for the 
selection criteria.  The default is 1. 
c2   -   specifies the ending column of the range of columns for the selection 
criteria.  The default is 256. 
Description: 
The TS (Type Suppressed) command prints a range of records without keys, i.e., 
the keys are suppressed. 
TS is a record command if parameters are specified, an intrarecord command if 
parameters are omitted. 
Examples: 
*TS 9-100 
means print (without keys) records 9 through 100. 
Related Commands: 
TN, TP, TC, TY 
00002
00003
00001
00004
Syntax: 
...;TX[;...] 
Parameters: 
None. 
Description: 
The TX (Type eXchanged) command prints records that have been changed by the 
command preceding the TX command on the same multicommand line. 
TX is always an intrarecord command. 
Examples: 
*/twerple/D;tx 
means type all lines changed by deleting the string twerple. 
Related Commands: 
TY, TC, TS 
00002
00003
00001
00004
Syntax: 
TY [n1[-n2][,c1][,c2]]] 
Parameters: 
n1   -   specifies the starting key of the range of records to be printed. 
n2   -   specifies the ending key of the range of records to be printed.  If 
omitted, only record n1 is printed. 
c1   -   specifies the starting column of the range of columns for the 
selection criteria.  The default is 1. 
c2   -   specifies the ending column of the range of columns for the selection 
criteria.  The default is 256. 
Description: 
The TY (TYpe records) command prints a range of records and columns, with 
keys. 
NOTE:  A string selection expression can also be specified as part of the TY 
command; in this case the syntax is the same as for the FT command (except TY 
replaces FT as the command verb). 
TY is a record command if parameters are specified, an intrarecord command if 
parameters are omitted. 
Examples: 
*TY1-100 
means print records 1 to 100 inclusive, with keys. 
*TY1-100,100,200 
means print records 1 to 100, set criteria to columns 100 through 200. 
Related Commands: 
TN, TP, TC, FT 
00002
00003
00001
00004
Syntax: 
TYPE [']code['] 
Parameters: 
code   -   is either a two character file type, or a two-character quote 
string denoting file type. 
Description: 
The TYPE command sets the two character filetype to be assigned to files 
created by subsequent BUILD, COPY, or MERGE commands. 
File types may be defined by the user and used as a file sorting and 
management aid. 
TYPE is always a file command. 
Examples: 
*TYPE SF  or 
*TYPE 'SF' 
means assign the file type SF (Source FORTRAN) to all subsequently created 
files. 
Related Commands: 
BUILD, COPY, MERGE 
00002
00003
00001
00004
If a single up-arrow character (&) followed by a carriage return is entered in 
response to the asterisk prompt, the selection criteria is set to all columns 
of the first record before the lower limit of the current criteria.  That 
record is then printed in the format specified by the last issued TY, TS, TC, 
or RR command.  The default is TY. 
Syntax: 
VE {TY|TC|TS|TX|OFF} 
Parameters: 
TY, TC, TS, or TX designates the command to implicitly follow each intrarecord 
command. 
The default is OFF. 
Description: 
The VE (VErify) command causes EDIT to automatically assume that TY, TC, TS, 
or TX command follows any intrarecord command line. 
VE is always a file command. 
Examples: 
*VE TY 
means automatically assume that a TY command follows each intrarecord command. 
Related Commands: 
TY, TC, TS, TX 
00002
00003
00001
00004
Format: 
string ?[x] string 
Parameters: 
string   -   can be a character string or the null string ('' or //). 
x   -   is a decimal integer specifying the length of the template field.  If 
unspecified, the string can be of any length. 
Description: 
Wildcard strings define template fields within character strings. 
NOTE:  A special form of the wildcard string applies to intrarecord commands 
that perform string substitution (S, P, F, O, E, and A).  This form is always 
located to the right of the command verb and refers not to the length of the 
template field, but to the corresponding wildcard string located left of the 
command verb.  For example, //?/A/?//S//?2// matches the ?2 with the second 
wildcard in the command. 
Examples: 
/A/?/C/    could refer to AAC,AABWQC, A$$C, etc. 
#101?#103  has the identical meaning to the wildcard string above. 
/A/?2/C/   could refer to AQRC, A!$C, but not AZC or APOIC. 
//?//      refers to any string whatever, including the null string. 
/A/?//     could refer to A, AB, ABC, A!!$#%, etc. 
Usage Note: 
Wildcards are used in string selection expressions, and in many intrarecord 
commands.  Also see the STRING component. 
00002
00003
00001
00004
END
    XUG Services have been added to EDIT for Command entry only.  This allows 
    you to use DO(!) commands at the '*' prompt level.  It also allows you to 
    use XUG built-in commands such as OUTPUT, PRINT and ERASE.  Two nice uses 
    of this feature are the ability to use !DEL to allow wildcarded deletes 
    (don't delete the file you are EDITing) and !PERUSE.X to check word 
    spelling. 
