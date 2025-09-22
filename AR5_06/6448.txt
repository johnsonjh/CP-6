The TRansaction-to-Application Definition Routine (TRADER) is a processor that 
the TP administrator invokes to create a TRADER file for an instance of TP. 
The TRADER file contains two types of records: 
o   Form record - contains the Forms Program file identifier (fid) and a 
    corresponding Forms Program type or report transaction type.  One Form 
    record is required for each Forms Program that is to be used by TP 
    stations in an instance of TP.  Form records for the report transaction 
    types are optional. 
o   Entry record - contains the TP Application Program (TPAP) file identifier 
    (fid) and a transaction type.  Every data entry or spawned transaction 
    type must be represented by an Entry record specifying the TPAP that is to 
    process it.  Every TPAP in the instance of TP must be referenced in an 
    Entry record. 
For further HELP messages, enter: 
HELP (TRADER) TOPICS        For a list of HELP topics 
HELP (TRADER) COMMANDS      For a list of commands available 
                            at the CMD and SET levels of TRADER 
HELP (TRADER) COMMAND_SUM   For a summary of TRADER commands 
HELP (TRADER) command_name  For details on a specific command 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
After invoking the processor, the first step in communicating with TRADER is 
selection of the file to be created or modified.  Then commands can be entered 
to create, modify, or list the contents of the file selected. 
The TRADER commands are categorized as Command (CMD) level and SET level. 
CMD-level commands may be entered immediately after invocation of TRADER. 
SET-level commands may be entered following a CREATE ENTRY or MODIFY ENTRY 
command specifying the SETS attribute. 
CMD-level commands:  COPY_ENTRY, COPY_FORM, CREATE_ENTRY, CREATE_FORM, 
DELETE_ENTRY, DELETE_FORM, END, LIST_ENTRY, LIST_FORM, MODIFY_ENTRY, 
MODIFY_FORM, QUIT, SELECT. 
Set-level commands:  END, QUIT, READS, REPORTS, RESET, RESPONDS, SET, SPAWNS. 
For further details on a specific command, enter:  HELP (TRADER) 
command_name       For the command format.  Enter 
                                 ? or ?? for more information 
HELP (TRADER) command_name PARAM For a discussion of parameters 
HELP (TRADER) command_name DESC  For the function of a command 
HELP (TRADER) command_name NOTES For usage notes on the command 
To obtain a brief description of all commands, type ??.  To obtain a brief 
description of a specific command, type: 
HELP (TRADER) COMMAND_S command 
Valid command names are COPY_ENTRY, COPY_FORM, CREATE_ENTRY, CREATE_FORM, 
DELETE_ENTRY, DELETE_FORM, END, LIST_ENTRY, LIST_FORM, MODIFY_ENTRY, 
MODIFY_FORM, QUIT, READS, REPORTS, RESET, RESPONDS, SELECT, SET, SPAWNS. 
  Command              Description 
  <carriage return> 
                       When entered at SET-command level, return to CMD-level 
                       of TRADER. 
  COPY ENTRY 
                       Copy an Entry record to another Entry record. 
  COPY FORM 
                       Copy a Form record to another Form record. 
  CREATE ENTRY 
                       Create an Entry record for a data entry or spawned 
                       transaction type. 
  CREATE FORM 
                       Create a Form record.  (A Form record describes a Forms 
                       Program or a report transaction sent to a Forms 
                       Program.) 
  DELETE ENTRY 
                       Delete an Entry record. 
  DELETE FORM 
                       Delete a Form record. 
  {END|QUIT} 
                       When entered at CMD-level, exit the TRADER processor. 
                       When entered at SET-level, return to CMD-level of 
                       TRADER. 
  LIST ENTRY 
                       Display an Entry record. 
  LIST FORM 
                       List a Form record. 
  MODIFY ENTRY 
                       Modify an Entry record.  (For details, see CREATE ENTRY 
                       command description.) 
  MODIFY FORM 
                       Modify a Form record.  (For details, see CREATE FORM 
                       command description.) 
  READS 
                       Specify information to enable the TPAP to read the 
                       comgroup via a Data Control Block. 
  REPORTS 
                       Specify information to enable the TPAP to write a 
                       report transaction to the comgroup via a Data Control 
                       Block. 
  RESET 
                       Cancel previous SET, READS, RESPONDS, REPORTS, SPAWNS 
                       command(s). 
  RESPONDS 
                       Specify information to enable the TPAP to write a 
                       response transaction to the comgroup via a Data Control 
                       Block. 
  SELECT 
                       Select a TRADER file to create or modify. 
  SET 
                       Specify information for a Data Control Block using the 
                       IBEX SET command format. 
  SPAWNS 
                       Specify information to enable the TPAP to write a 
                       spawned transaction to the comgroup via a Data Control 
                       Block. 
For further details on a specific command, enter:  HELP (TRADER) 
command_name       For the command format.  Enter 
                                 ? or ?? for more information 
HELP (TRADER) command_name PARAM For a discussion of parameters 
HELP (TRADER) command_name DESC  For the function of a command 
HELP (TRADER) command_name NOTES For usage notes on the command 
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
00008
00013
00014
00015
00016
00017
00018
00019
Format: 
C[OPY] E[NTRY] oldtype {TO  } newtype 
                       {OVER} 
Parameters: 
oldtype     specifies the type that identifies the Entry record to be copied. 
newtype    specifies the type that identifies the Entry record to be created 
or replaced. 
Description: 
This command creates a new Entry record from an existing record if TO is 
specified; it replaces an existing record if OVER is specified. 
00002
00001
Format: 
C[OPY] F[ORM] oldtype {TO  } newtype 
                      {OVER} 
Parameters: 
oldtype    specifies the type of the Form record to be copied. 
newtype    specifies the type of the Form record to be created or replaced. 
Description: 
This command creates a new Form record from an existing record if TO is 
specified; it replaces an existing record if OVER is specified. 
00002
00001
Format: 
{CR[EATE]} E[NTRY] type attribute1[,attribute2]... 
{MOD[IFY]} 
Parameters: 
type    specifies a data entry or spawned transaction type.  For a data entry 
transaction, the transaction type is contained in the TYPE variable when the 
Forms Program performs a WRITE to the transaction file.  For a spawned 
transaction, the transaction type is supplied in the DCB through which a 
spawned transaction is written to the comgroup (see the SPAWNS command).  Type 
must be a 1 to 8 character name containing at least one non-numeric character. 
Type may consist of any upper- or lower-case letters, the digits 0-9, or the 
dash, underscore, or dollar sign. 
attribute1,attribute2    specify attributes of the transaction type.  To 
obtain HELP messages on attributes, enter HELP CR_E attribute_name. 
Attributes are DEBUG[GER] = dname, JOUR[NAL] = {ON|OFF}, LOCK [=] {ON|OFF}, 
MAXAC[TIVE] = n, M[ESSAGE] [=] {ON|OFF}, PRIO[RITY] = n, SETS, TPAP = fid. 
Descriptions are in tabular form with two columns as follows: 
  Attribute      Description 
  DEBUG[GER]=dname 
                 Specifies the 1 to 11 character name of a debugger to 
                 associate with this TPAP when it is invoked.  The debugger 
                 must reside in account :SYS.  The default is blanks, which 
                 means not to associate any debugger when the TPAP is invoked. 
  JOUR[NAL] [=] {[ON]|OFF} 
                 If ON, specifies that transactions of the type specified are 
                 to be written to the common journal as soon as they are 
                 received by the comgroup.  Specifying only the keyword 
                 JOURNAL is interpreted to mean JOURNAL=ON.  The default is 
                 JOURNAL=OFF. 
  LOCK [=] {[ON]|OFF} 
                 Specifies whether or not VLP_STATION can be specified at a 
                 read or write of the comgroup.  By specifying LOCK=OFF, a 
                 TPAP can examine the terminal station name at a read or 
                 supply a terminal station name at a write.  See the CP-6 
                 Monitor Services Reference Manual (CE33) for further 
                 discussion of VLP_STATION.  Specifying only the keyword LOCK 
                 is interpreted to mean LOCK=ON.  The default is LOCK=ON, 
                 i.e., a VLP_STATION may not be used. 
  MAXAC[TIVE]=n 
                 Specifies the maximum number (0-9999) of transactions of this 
                 type that can be in process by the TPAP (in multiple TP User 
                 slots) at one time.  The default is 9999. 
  M[ESSAGE] [=] {[ON]|OFF} 
                 Specifies whether or not to send a message to the station 
                 that originated the transaction if the TP Application Program 
                 aborts.  Specifying only the keyword MESSAGE is interpreted 
                 to mean MESSAGE=ON.  The default is MESSAGE=OFF, i.e., a 
                 message is not sent. 
  PRIO[RITY]=n 
                 Specifies the transaction priority.  This number from 1 to 
                 500 is used by the comgroup in queueing the transaction and 
                 is one factor in determining when the transaction is 
                 processed.  The value 500 represents the highest priority. 
                 The default is 1. 
  SETS 
                 Specifies that the user wants to enter the SET level of 
                 TRADER.  If SETS is not specified, TRADER continues at the 
                 CMD level and prompts with the string CMD? 
  TPAP=fid 
                 Specifies the TP Application Program (TPAP) that is to 
                 process this transaction type.  The fid is the CP-6 file 
                 identifier of the run unit.  This attribute is required on 
                 the CREATE ENTRY command. 
Description: 
This command creates or modifies an Entry record that represents a data entry 
or spawned transaction and supplies information that is required to invoke a 
TP Application Program (TPAP) to process it. 
Usage Notes: 
If an Entry record is created or modified while the instance of TP is in 
operation, transaction processing in progress is not affected.  However, at 
subsequent invocation of the TPAP, those modifications take effect with the 
following exception.  Modifications to attributes that pertain to transactions 
(specifically, PRIORITY, JOURNAL, MAXACTIVE) do not take effect until the next 
TP initialization although changes are reflected in the TRADER Entry record. 
To modify for current operation PRIORITY, JOURNAL, or MAXACTIVE, the TP 
command TRANSACTION can be used. 
00002
00010
00003
00004
00006
00005
00006
00011
00001
00007
00008
00009
00011
Format: 
{CR[EATE]} F[ORM] type FP=fid [,attribute1[,attribute2]] 
{MOD[IFY]} 
Parameters: 
type    specifies a Forms Program type (i.e., the name used to invoke a Forms 
Program via the BEGIN or DEBUG command), or a report transaction type.  Type 
must be a 1 to 8 character name containing at least one non-numeric character. 
Type may consist of any upper- or lower-case letters, the digits 0-9, and the 
dash, underscore, or dollar sign. 
fid    specifies the CP-6 file identifier of the Forms Program interpretation 
unit.  The Forms Program interpretation unit is stored as a standard disk 
file. 
attribute    specifies an attribute which applies to report transaction types 
only.  To obtain HELP messages for the CREATE or MODIFY FORM options, enter 
HELP CR_F attribute_name. 
Attributes include JOUR[NAL] [=] {[ON]|OFF}, ONE[REPORT] [=] {[ON]|OFF}. 
Descriptions are in tabular form with two columns, as follows: 
  Attribute      Description 
  JOUR[NAL] [=] {[ON]|OFF} 
                 If ON, specifies that the report transaction is to be written 
                 to the journal as soon as it is unlatched.  Specifying only 
                 the keyword JOURNAL is interpreted to mean JOURNAL=ON.  The 
                 default is JOURNAL=OFF. 
  ONE[REPORT] [=] {[ON]|OFF} 
                 If ON, specifies that a group of related report transactions 
                 created by one TPAP is to be treated as a "logical report". 
                 That is, if two or more "logical reports" are ready for 
                 transmission to a terminal station, consecutive reads by the 
                 Forms Program obtain all report transactions of a complete 
                 logical report before receiving any part of another logical 
                 report; in other words, transactions of different logical 
                 reports are not interleaved.  Specifying only the keyword 
                 ONEREPORT is interpreted to mean ONEREPORT=ON.  The default 
                 is ONEREPORT=OFF. 
Description: 
This command creates or modifies a Form record in the TRADER file.  The Form 
record correlates the Forms Program as stored at the host system with the type 
used to invoke the program.  The Form record also allows the user to specify 
attributes for a report transaction type. 
Usage Notes: 
If a Forms Program type is added or a Forms Program fid is modified while the 
instance of TP is operating, forms processing in progress is not affected. 
However, subsequent attempts to load the Forms Program are affected by the 
modification.  If a report transaction attribute is added or modified while 
the instance of TP is in operation, the Form record is modified, but the 
modification does not take effect until the next TP initialization. 
00004
00002
00005
00003
00001
00005
CREATE_ENTRY
CREATE_FORM
COPY_ENTRY
COPY_FORM
Format: 
DEL[ETE] E[NTRY] type 
Parameters: 
type    is the same as for CREATE ENTRY. 
Description: 
This command deletes the specified Entry record, including any SET-level 
information entered for the transaction type. 
Usage Notes: 
If an Entry record is deleted while the instance of TP is in operation, any 
transaction processing in progress is unaffected.  However, any subsequent 
attempt to invoke the TPAP will fail. 
00002
00003
00001
00003
Format: 
DEL[ETE] F[ORM] type 
Parameters: 
type    same as for CREATE FORM. 
Description: 
This command deletes the specified Form record. 
Usage Notes: 
If a Forms Program record is deleted while the instance of TP is in operation, 
forms processing in progress is not affected.  However, subsequent attempts to 
load the Forms Program will fail. 
00002
00003
00001
00003
DELETE_ENTRY
DELETE_FORM
Format: 
{E[ND]|Q[UIT]} 
Description: 
This command causes the TRADER processor to exit from CMD level.  When entered 
at SET level, this command returns to CMD level. 
Usage Notes: 
Entering a carriage return or a blank line at the SET level also causes a 
return to the CMD level of TRADER. 
00001
00002
Format: 
HELP [(fid)] [TOPICS] [keyword1] [-] [keyword2] 
NOTE:  The following elements can be specified in any order: 
         (fid) 
         TOPICS 
         [keyword1] [-] [keyword2] 
For example, HELP (fid) keyword1 - keyword2 TOPICS is acceptable. 
Parameters: 
(fid)    specifies the processor name (for example, TRADER).  If (fid) is 
omitted, the current processor is assumed. 
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
HELP (TRADER) CR_E 
means display the format of the CREATE_ENTRY command and prompt for the next 
entry. 
HELP CR_E 
means the same as the above example, when the TRADER processor is in control. 
HELP MOD_E 
means the same as the above example; MOD_E, a synonym for MODIFY_ENTRY, is 
documented together with the CREATE_ENTRY command. 
HELP READS PARAM 
means display the discussion of parameters for the READS command. 
00002
00003
00001
C 
  COPY ENTRY Command - 
      HELP COPY_ENTRY 
  COPY FORM Command - 
      HELP COPY_FORM 
  CREATE or MODIFY ENTRY Command - 
      HELP CREATE_ENTRY 
  CREATE or MODIFY FORM Command - 
      HELP CREATE_FORM 
D 
  data entry transaction - 
      HELP READS PARAMETERS: 
  DCB - 
      HELP READS PARAMETERS: 
      HELP REPORTS PARAMETERS: 
      HELP RESET PARAMETERS: 
      HELP RESPONDS DESCRIPTION: 
      HELP SET DESCRIPTION: 
      HELP SPAWNS PARAMETERS: 
  DELETE ENTRY Command - 
      HELP DELETE_ENTRY 
  DELETE FORM Command - 
      HELP DELETE_FORM 
E 
  END or QUIT Command - 
      HELP END 
H 
  HELP Command - 
      HELP HELP 
J 
  JOURNAL - 
      HELP CREATE_ENTRY JOURNAL_ 
      HELP CREATE_FORM JOURNAL_ 
L 
  LIST ENTRY Command - 
      HELP LIST_ENTRY 
  LIST FORM Command - 
      HELP LIST_FORM 
M 
  MAXACTIVE - 
      HELP CREATE_ENTRY MAXACTIVE 
  MODIFY ENTRY - 
      HELP CREATE_ENTRY FORMAT: 
  MODIFY FORM - 
      HELP CREATE_FORM FORMAT: 
O 
  ONEREPORT - 
      HELP CREATE_FORM ONEREPORT_ 
      HELP REPORTS PARAMETERS: 
  Ordering - 
      HELP ORDERING_HOW_TO 
P 
  PRIO - 
      HELP CREATE_ENTRY PRIORITY 
  Publishing - 
      HELP PUBLISHING 
R 
  read-mode - 
      HELP READS DESCRIPTION: 
  READS Command - 
      HELP READS 
  report transaction - 
      HELP REPORTS PARAMETERS: 
  REPORTS Command - 
      HELP REPORTS 
  RESET Command - 
      HELP RESET 
  RESPONDS Command - 
      HELP RESPONDS 
  response transactions - 
      HELP RESPONDS DESCRIPTION: 
S 
  SELECT Command - 
      HELP SELECT 
  SET Command - 
      HELP SET 
  spawned transaction - 
      HELP SPAWNS PARAMETERS: 
  SPAWNS Command - 
      HELP SPAWNS 
T 
  TRADER - 
      HELP TRADER 
      HELP TRADER 
      HELP PROCESSOR 
  TRADER Commands - 
      HELP COMMANDS 
      HELP COMMANDS 
  TRADER file - 
      HELP TRADER 
  transaction type - 
      HELP CREATE_ENTRY PARAMETERS: 
  type - 
      HELP CREATE_ENTRY PARAMETERS: 
      HELP CREATE_FORM PARAMETERS: 
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
HELP_INDEX
Format: 
L[IST] E[NTRY] type [(A[TTRIBUTES])] 
Parameters: 
type    is the same as for CREATE ENTRY.  Type may include the wildcard (?) 
character. 
Description: 
This command displays the contents of the specified Entry record.  If (A) is 
specified, all attributes for the transaction types are included in the 
display. 
00002
00001
Format: 
L[IST] F[ORM] type [(A[TTRIBUTES])] 
Parameters: 
type    is the same as for CREATE FORM.  Type may include the wildcard (?) 
character. 
Description: 
This command displays the contents of the specified Form record.  If (A) is 
specified, attributes for the type are included in the display. 
00002
00001
LIST_FORM
LIST_ENTRY
LIST_FORM
CREATE_ENTRY
CREATE_FORM
CREATE_ENTRY
CREATE_FORM
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
The TP administrator runs TRADER as a batch or time-sharing job.  The DCBs 
used are M$SI for input, M$LO for normal output, and M$DO for output of error 
messages.  To run TRADER, a !TRADER command is submitted; that command is of 
the form: 
!TRADER [si_fid] [ON , lo_fid] 
Parameters: 
si_fid    specifies the fid of a file containing TRADER commands. 
lo_fid    specifies the fid to receive listing output. 
The TRADER commands are submitted with a maximum of one command per record.  A 
semicolon must be used to continue a command on the next line; commentary may 
be entered between quotation marks (" "). 
END
RESET
Format: 
READS type THRU dcb [MODE {AVAIL[ABLE]}] 
                    [     {SING[LE]   }] 
Parameters: 
type    must reflect the type entered for the current CREATE or MODIFY ENTRY 
command.  Type may include the wildcard (?) character. 
dcb    specifies the name of the DCB that is used to read this transaction 
type. 
{AVAIL[ABLE]|SING[LE]}    Specifies the "read-mode" for the TPAP.  AVAILABLE 
permits the TPAP to read the comgroup for the transaction it is to process; at 
any subsequent read of the comgroup, if another transaction of the same type 
just processed is in the comgroup, that transaction is read.  SINGLE permits 
the TPAP to read the comgroup once (for the transaction it is to process); at 
any subsequent read of the comgroup, "end-of-file" status is returned.  The 
default is AVAILABLE. 
NOTE:  The PERM option on the TRANSACTION command overrides SINGLE for 
transaction types that include the wildcard (?) character. 
Description: 
This command supplies parameters required at TPAP invocation.  These 
parameters are merged into the Data Control Block (DCB) when it is opened. 
Usage Notes: 
While the instance of TP is in operation, changes made to the DCB used to read 
the comgroup do not affect transaction processing in progress.  However, 
changes do affect subsequent invocations of the TPAP. 
The READS command simplifies the task of assigning DCBs and may be used in 
nearly all cases.  The exceptions to this rule are discussed under the SET 
command, Usage Notes. 
00002
00003
00001
00003
Format: 
REP[ORTS] type THRU dcb [TO station] [ONE[REPORT][=]{[ON]|OFF}] 
Parameters: 
type    specifies the report transaction type.  Type is defined by the Forms 
Program as the TYPE variable referenced in the FILE-CONTROL paragraph for the 
transaction file that receives the report transaction. 
dcb    specifies the name of a Data Control Block (DCB) that is used to write 
report transactions. 
station    specifies the 1 to 8 character name of the station that is to 
receive the report transaction.  The station name may include the wildcard (?) 
character in order to send the transaction to several stations.  The default 
is the station that submitted the transaction that caused generation of the 
report transaction. 
ONEREPORT    is the same as for the CREATE FORM command. 
Description: 
This command supplies the parameters for the DCB through which the report 
transaction type is written to the comgroup.  The parameters are merged into 
the DCB when it is opened. 
Usage Notes: 
While the instance of TP is in operation, changes made to the DCB used to 
write to the comgroup do not affect transaction processing in progress. 
However, changes do affect subsequent invocations of the TPAP. 
The REPORTS command simplifies the task of assigning DCBs and may be used in 
nearly all cases.  The exceptions to this rule are discussed under the SET 
command, Usage Notes.  Note also that READS, RESPONDS, REPORTS, and SPAWNS 
must not be used for the same DCB. 
00002
00003
00001
00003
Format: 
R[ESET] [dcb] 
Parameters: 
dcb    specifies the name of a Data Control Block previously specified in a 
SET, READS, RESPONDS, REPORTS, or SPAWNS command for this Entry record. 
Description: 
This command deletes from the Entry record the specified DCB assignment, or if 
no DCB is specified, deletes all DCB assignments for the Entry record. 
Usage Notes: 
While the instance of TP is in operation, changes made to the DCB specified 
via RESET do not affect transaction processing in progress.  However, changes 
do affect subsequent invocations of the TPAP. 
00002
00003
00001
00003
Format: 
RESP[ONDS] THRU dcb 
Parameters: 
dcb    specifies the name of the DCB that is used to write response 
transactions. 
Description: 
This command supplies the name of a Data Control Block (DCB) through which the 
TPAP writes response transactions to the comgroup.  Parameters are merged into 
this DCB when it is opened. 
NOTE:  A response transaction is always delivered to the terminal station that 
originated the transaction which caused the response transaction to be 
generated. 
Usage Notes: 
While the instance of TP is in operation, changes made to the DCB used to 
write to the comgroup do not affect transaction processing in progress. 
However, changes do affect subsequent invocations of the TPAP. 
The RESPONDS command simplifies the task of assigning DCBs and may be used in 
nearly all cases.  The exceptions to this rule are discussed under the SET 
command, Usage Notes.  Note also that READS, RESPONDS, REPORTS, and SPAWNS 
must not be used for the same DCB. 
00002
00003
00001
00003
Format: 
SEL[ECT] fid 
Parameters: 
fid    specifies a CP-6 file identifier. 
Description: 
This command selects the TRADER file which subsequent commands will create, 
modify, or display. 
00002
00001
Format: 
SET dcb [fid] [,optionlist] 
Description: 
This command provides the same options as the IBEX SET command which can be 
displayed by entering HELP (IBEX) SET_OPTIONS.  Typically the SET command is 
used to establish parameters for DCBs that are required to access data base 
files.  Parameters specified in a TRADER SET command are merged into the DCB 
when it is opened. 
Usage Notes: 
While the instance of TP is in operation, changes made to the DCB specified 
via SET do not affect transaction processing in progress.  However, changes do 
affect subsequent invocations of the TPAP. 
A SET command is required instead of a combination of READS, RESPONDS, 
REPORTS, or SPAWNS for a single DCB.  The case when a SET is required is as 
follows:  the DCB is used for reading and writing and the DCB is used to read 
a wildcarded transaction type or to read in SINGLE read-mode.  The READS, 
RESPONDS, REPORTS, and SPAWNS commands, although simpler to use, effectively 
cause a RESET before performing a SET with the specified options and assumed 
defaults.  The following sequence of commands illustrates the limitation: 
    READS AB? THRU XACTION 
    REPORTS ARPT THRU XACTION 
Performed in this sequence the commands have this effect:  when the READS 
command is processed, DCB XACTION is set to read type AB? (i.e., IMSGTYP=AB?), 
but when the REPORTS command is processed, the RESET function occurs deleting 
the wildcarded IMSGTYP and the DCB is set to write transaction type ARPT 
(i.e., OMSGTYP=ARPT).  When an attempt is made to read through DCB XACTION, 
the default transaction type is that taken from the previous CREATE ENTRY 
command (i.e., a transaction type that is not wildcarded).  Reversing the 
order of the READS and REPORTS command does not help, since the report 
transaction type would be similarly deleted.  Instead, this SET command should 
be used to provide a DCB that reads AB? and writes ARPT: 
    SET XACTION ME,IMSGTYP=AB?,OMSGTYP=ARPT,ILATCH,OLATCH, 
    SHARE=ALL,EXIST=OLDFILE 
00001
00002
00002
Format: 
SPAWNS type THRU dcb 
Parameters: 
type    specifies the spawned transaction type.  The TRADER file must include 
another Entry record that specifies this transaction type and the TPAP that 
will process it. 
dcb    specifies the name of a Data Control Block (DCB) that is used to write 
spawned transactions. 
Description: 
This command supplies the parameters used for the DCB through which the 
spawned transaction type is written to the comgroup.  The parameters are 
merged into the DCB when it is opened. 
Usage Notes: 
While the instance of TP is in operation, changes made to the DCB used to 
spawn transactions do not affect transaction processing in progress.  However, 
changes do affect subsequent invocations of the TPAP. 
The SPAWNS command simplifies the task of assigning DCBs and may be used in 
nearly all cases.  The exceptions to this rule are discussed under the SET 
command, Usage Notes.  Note also that READS, REPORTS, RESPONDS, and SPAWNS 
must not be used for the same DCB. 
00002
00003
00001
00003
NOTATION

