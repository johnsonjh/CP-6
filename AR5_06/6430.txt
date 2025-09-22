PLOVER is a processor that applies RUM commands to object units.  The object 
unit can be in an object unit file or a library file.  PLOVER will accept the 
following RUM commands: 
    ALT VAR          ECHO            LET          STORE 
    COPY             FIND            MODIFY       SYNTAX 
    DEFINE           KILL            SCHEMA 
and the following EOM CHARS in the MODIFY mode: 
    NEXT, PREV, and *(indirect addressing). 
For information on these RUM commands, enter 
HELP (DELTA) directive. 
where directive is the individual RUM command. 
and HELP (DELTA) EOM_CHAR 
PLOVER checks only the first word of these commands for syntax correctness, 
and writes the records to the object unit with a special key.  PLOVER also 
writes a special record to the object unit to indicate the presence of PLOVER 
records in the object unit.  At LINK time, the LINKer will recognize the 
existence of the PLOVER records in the object unit by reading this special 
record, and will gather the PLOVER records into a star file.  When the run 
unit has been linked, the LINKer will ALIB to DELTA to apply the RUM commands 
to the run unit.  Plover will also count the patch space needed for the object 
unit and will write two fields (one for IPATCH and one for DPATCH) in this 
special record.  The Linker will add up all the patch space from the different 
object units before allocating the patch area in the run unit. 
In addition to the RUM commands that PLOVER will accept, there are PLOVER 
commands to list and delete PLOVER records, and some special commands used by 
LINK.  These commands are described under HELP (PLOVER) COMMANDS 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
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
The PLOVER commands are: 
    DELETE 
    DPATCH 
    ENTREF 
    EXTERNAL 
    IPATCH 
    LIST 
    READ 
    RESET 
    SYMDEF 
    For HELP, type HELP command 
Syntax: 
DEL[ETE]  [ object [ , UTS=date ] ] 
Parameters: 
object    is the name of an object unit in the file that is being PLOVERed. 
If an object unit name is not specified, the PLOVER records for all the object 
units in the file being PLOVERed will be deleted. 
UTS=date    specifies that only the PLOVER records for the specified date are 
to be deleted.  If a UTS is not specified, all the PLOVER records for the 
object unit will be deleted. 
Description: 
The DELETE command deletes the records which have been added to an object unit 
or library file by PLOVER. 
Example: 
>>DELETE  OU_NAME1 
00002
00003
00001
Syntax: 
DP[ATCH] = value 
Parameters: 
value   -   a decimal number. 
Description: 
Specifies the number of additional words to be reserved in the data patch 
space for this object unit when the linker processes the Plover records. 
Example: 
>>DPATCH = 100 
00002
00003
00001
Syntax: 
ENT[REF]  entref 
Parameters: 
entref    specifies the name of the ENTREF to be added to the object unit. 
Description: 
The ENTREF command adds an external procedure reference to the object unit 
being PLOVERed.  This command is useful when it is necessary to modify an 
instruction in a library object unit to transfer to an external procedure that 
was not referenced in the object unit.  The reason an ENTREF should be added 
to the library object unit is that the linker will include a library object 
unit in the run unit only if it has been referenced. 
Examples: 
>>PLOVER LIBRARY (OU=ENTRYNAME) 
>>ENTREF  X 
>>M ENTRYNAME+5 TSX1 X (TSX1 Y) 
00002
00003
00001
Syntax: 
                  { # } 
EXT[ERNAL]  name  { @ }, value 
Parameters: 
name    is the symbol to be defined. 
#    indicates a data patch area. 
@    indicates the instruction patch area. 
value    is the number of words of patch space to be reserved for the symbol. 
Description: 
The EXTERNAL command defines a symbol in either the data patch area or the 
instruction patch area and reserves 1 or more words of patch space for the 
symbol.  This command is useful when it is necessary for more than one library 
object unit to use the same data. 
NOTE:  The EXTERNAL command is implemented via a DELTA DEFINE, so a KILL DEFS 
command will remove the definition of this name.  For EXTERNAL to be useful, 
all patches to a library must KILL any DEFINEs they make by name. 
Examples: 
>>PLOVER LIBRARY (OU=ENTRYNAME1) 
>>EXTERNAL A #,2 
      . 
      . 
      . 
>>M @ STZ A 
      . 
      . 
      . 
>>PLOVER  (OU=ENTRYNAME2) 
      . 
      . 
      . 
>>M @ LDA A 
>>M @ TNZ ENTRTYNAME2+.1773 
00002
00003
00001
D 
  DELETE Command -   
    PLOVER - 
      HELP DELETE SYNTAX: 
  DELETE Command - 
      HELP DELETE 
  DPATCH Command - 
      HELP DPATCH 
E 
  ENTREF Command - 
      HELP ENTREF 
  EXTERNAL Command - 
      HELP EXTERNAL 
I 
  Invoking PLOVER - 
      HELP INVOKING_PLOVER 
  IPATCH Command - 
      HELP IPATCH 
L 
  LIST Command -   
    PLOVER - 
      HELP LIST SYNTAX: 
  LIST Command - 
      HELP LIST 
O 
  object units - 
      HELP NOTATION SEMICOLON 
P 
  PLOVER - 
      HELP NOTATION SEMICOLON 
  PLOVER Commands - 
      HELP COMMANDS 
R 
  READ Command -   
    PLOVER - 
      HELP READ SYNTAX: 
  READ Command - 
      HELP READ 
  RESET Command - 
      HELP RESET 
  RUM Command - 
      HELP NOTATION SEMICOLON 
S 
  SYMDEF Command - 
      HELP SYMDEF 
00001
00002
00003
00004
00005
00006
00007
HELP_INDEX
Syntax: 
PLOVER is invoked by the PLOVER command: 
PL[OVER]  [lib-fid] [,cmd-fid] [(optionlist)] 
Parameters: 
lib-fid    is the file identification of an object unit file or a library 
file. 
cmd-fid    is the file identification of the file from which subsequent PLOVER 
commands are to be read. 
optionlist   -   specifies one or more of the PLOVER options in the format 
(option[,option]...). 
Standard options are: 
    ou    is the name of the object unit with which subsequent PLOVER commands 
    will be associated. 
    UTS=date    specifies a date which must match the UTS of the object unit, 
    in the following format: 
        mm/dd/yy hh:mm:ss.hh 
        (month/day/year hours:minutes:seconds.hundredths) 
    For object units in object unit files, and for object units in library 
    files, this is the creation date. 
Description: 
The PLOVER command specifies the object unit that subsequent commands are to 
be associated with.  For HELP, type HELP COMMANDS 
Example: 
!PLOVER LIBRARY (OU=ENTRYNAME) 
00002
00003
00001
Syntax: 
IP[ATCH] = value 
Parameters: 
value   -   a decimal number. 
Description: 
Specifies the number of additional words to be reserved in the instruction 
patch space for this object unit when the linker processes the Plover records. 
Example: 
>>IPATCH = 50 
00002
00003
00001
Syntax: 
L[IST]  [ object [ , UTS=date ] ] 
Parameters: 
object    is the name of an object unit in the file that is being PLOVERed. 
If an object unit name is not specified, the PLOVER records for all the object 
units in the file being PLOVERed will be listed. 
UTS=date    specifies that only the PLOVER records for the specified date are 
to be listed.  If a UTS is not specified, all the PLOVER records for the 
object unit will be listed. 
Description: 
The LIST command lists the records which have been added to an object unit or 
library file by PLOVER. 
Example: 
>>LIST OU_NAME1 
00002
00003
00001
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
INVOKING_PLOVER
Syntax: 
R[EAD]  cmd-file 
Parameters: 
cmd-file    is the file identification for the file that subsequent PLOVER 
commands will be read from. 
Description: 
The READ command causes PLOVER to read subsequent commands from a file. 
Example: 
>>READ  CMDS 
00002
00003
00001
Syntax: 
RES[ET] [DP[ATCH]|IP[ATCH]] 
Parameters: 
DP[ATCH]    specifies that the data patch space is to be set to zero. 
IP[ATCH]    specifies that the instruction patch space is to be set to zero. 
Description: 
Specifies that the patch space needed for this object unit be set to zero.  If 
the DPATCH or IPATCH options are not present, both DP and IP are reset. 
Example: 
>>RESET IPATCH 
00002
00003
00001
Syntax: 
SYM[DEF]  symdef  section 
Parameters: 
symdef    specifies the name of the SYMDEF to be added to the object unit. 
section    specifies an entry number into the control section table for the 
object unit. 
Description: 
The SYMDEF command adds an external data definition to the object unit being 
PLOVERed.  This command is useful when it is necessary to modify static data 
in an object unit. 
Examples: 
>>PLOVER LIBRARY (OU=ENTRYNAME) 
>>SYMDEF ENTRYNAME_DATA1 1 
>>M ENTRYNAME_DATA1+.15  5 (4) 
00002
00003
00001
NOTATION
