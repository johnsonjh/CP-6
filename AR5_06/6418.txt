LEMUR is invoked with the following IBEX command: 
!LEMUR 
When invoked, LEMUR identifies itself and prompts with a hyphen (-) character. 
LEMUR uses the following Data Control Blocks (DCBs): 
M$SI    Command Input 
M$LO    Listing Output 
M$DO    Diagnostic Output 
DCBs can be reassigned via the IBEX SET command. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
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
COPY
The commands for LEMUR are: 
COPY 
DEFINE 
DELETE 
DROP 
EXTRACT 
END 
LIST 
To obtain HELP information, type: 
HELP command 
Syntax: 
C[OPY] fid-entry-list {ON|TO|INTO|ADDTO|OVER} lib-fid[(optionlist)] 
Parameters: 
fid-entry-list   -   specifies one or more object or library files accompanied 
by optional object unit names.  The format of a fid-entry-list is: 
obj-fid[(obj-unit[,obj-unit]...)][,obj-fid[(obj-unit[,obj-unit]...)]... 
    where 
    obj-fid   -   specifies a disk or labeled tape file containing a library 
    or an object file. 
    obj-unit   -   specifies the name of an object unit contained in the 
    obj-fid file.  If unspecified, the entire file is considered a single 
    object unit.  Object unit names are user-created identifiers from 1 to 27 
    characters in length, and can consist of any combination of the following 
    characters: 
    A-Z   a-z   1-9 
    $     #     - (dash) 
    *     /     _ (underscore) 
    :     @     . (period) 
ON   -   specifies the creation of a new library file.  The command aborts if 
lib-fid already exists. 
TO   -   is a synonym for ON. 
INTO   -   specifies that, if lib-fid already exists, merge the input 
material, and overwrite where appropriate.  In effect, this allows the 
replacement of obsolete object units in a library file.  If INTO is used, and 
lib-fid does not exist, INTO functions identically to ON or TO. 
ADDTO   -   specifies that, if lib-fid already exists, merge the input 
material, but do not overwrite.  In most cases this appends new object units 
to a previously existing library file.  If ADDTO is used, and lib-fid does not 
exist, ADDTO functions identically to ON or TO. 
OVER   -   specifies that the new library file is to replace any previous file 
with the same fid.  If lib-fid does not already exist, it becomes a 
newly-created library file. 
lib-fid   -   specifies the library file to be created, modified, or replaced. 
This may be any valid CP-6 disk or labeled tape fid. 
optionlist   -   specifies one or more COPY options, separated by commas: 
D[UPLICATE]={INQUIRE|OVERWRITE|ERROR} 
M[AP]=(attachmentlist) 
N[ODEBUG] 
S[EVERITY]=decimal value 
SR[CH](.account1[,.account2]...) 
Description: 
COPY creates or modifies a library file, using one or more library or object 
files as sources.  A file created or modified by this command is automatically 
assigned the file type designator LE. 
Examples: 
!LEMUR 
LEMUR D00 here 
-COPY TEST_OU INTO TEST_LIBRARY 
means copy object unit TEST_OU INTO TEST_LIBRARY 
-COPY MY_OBJECT TO MY_LIBRARY 
means copy all object units in MY_OBJECT to MY_LIBRARY, which cannot 
previously exist. 
-COPY NEW_OBJECT(A_UNIT,B_UNIT) ADDTO MY_LIBRARY 
means copy object units A_UNIT and B_UNIT in NEW_OBJECT to MY_LIBRARY, which 
must not already contain an A_UNIT or a B_UNIT. 
-COPY NEXT_OBJECT(A_UNIT,C_UNIT) INTO MY_LIBRARY(NODEBUG,SEVERITY=6) 
means copy object units A_UNIT and C_UNIT in NEXT_OBJECT into MY_LIBRARY.  If 
the object units already exist in MY_LIBRARY, they are replaced.  No debugging 
information is copied, and a severity level of 6 is to be tolerated. 
When the PCL L command is used (either from PCL or directly from IBEX), the 
listing displays LE as the file type designator for files created or modified 
by the LEMUR COPY command: 
!L TEST_LIBRARY 
ORG TY   GRAN   NGAV      REC   LAST MOFIFIED   NAME 
KEY LE      1      0       26 11:37 FEB 21 '86  TEST_LIBRARY 
Related Commands: 
DELETE, LIST, EXTRACT 
00002
00003
00001
00004
The options for the COPY and LIST commands are:  DUPLICATE, MAP, NODEBUG, 
SEVERITY, and SRCH 
To obtain HELP messages, type: 
HELP (LEMUR) C_OPS option 
The options are described according to the following structure. 
  Option   Meaning 
  D[UPLICATE]={INQUIRE|OVERWRITE|ERROR} 
           When updating an existing library or creating a new library, it is 
           possible for more than one instance of an entry definition name to 
           occur.  These occurrences, which will define the entry definition 
           to object unit relationship, must be on a one-to-one 
           correspondence.  Ambiguity results when more than one of these 
           relationships is attempted.  The DUPLICATE option controls the 
           processing of duplicate relationships: 
           INQUIRE   -   directs LEMUR to prompt the user for a decision on a 
           case by case basis.  This is only valid for on-line operations.  If 
           INQUIRE is specified during batch operations, it is interpreted as 
           ERROR. 
           OVERWRITE   -   directs LEMUR to overwrite existing relationships 
           with subsequent occurrences. 
           ERROR   -   directs LEMUR to issue a diagnostic message regarding 
           any conflict and to not overwrite any existing relationships. 
           The default for on-line operations is INQUIRE; for batch 
           operations, ERROR. 
  M[AP]=(attachmentlist) 
           Produce a sorted listing by name according to list of attachments 
           separated by commas.  Valid attachments are: 
           DE[F]    List by name entry, data, and segment definitions. 
           ED[EF]   List by name entry definitions. 
           DD[EF]   List by name data definitions. 
           SD[EF]   List by name segment definitions. 
           R[EF]    List by name entry, data, and segment definitions. 
           ER[EF]   List by name entry references. 
           DR[EF]   List by name data references. 
           SR[EF]   List by name segment references. 
  NODEBUG 
           Specifies that any debug records in the fid-entry-list are not to 
           be copied to the library file. 
  S[EVERITY]=decimal value 
           Specifies the maximum severity tolerable in performing the 
           function.  If the severity level as obtained from the object unit 
           is greater than the value specified, then LEMUR skips that object 
           unit.  The object unit is not processed and a diagnostic message is 
           printed.  The default is 4. 
  SR[CH](account1[,account2]...) 
           Specifies the accounts the COPY command can access when searching 
           for an object or library file.  If the SRCH option is specified, 
           and a file is encountered in the COPY command that does not contain 
           an account, then COPY will search for the file in the accounts 
           given in the SRCH option.  The search is performed in the order 
           specified in the SRCH option, from left to right. 
00001
00002
00003
00004
00005
COPY_OPTIONS
DROP
Syntax: 
DEF[INE] entry-name[,entry-name]... IN lib-fid(obj-unit) 
Parameters: 
entry-name   -   specifies the entry name to be entered in the 
cross-reference. 
lib-fid   -   specifies the library file containing the desired object unit. 
obj-unit   -   specifies the object unit to be cross-referenced by the 
entry-name. 
Description: 
DEFINE enters an entry name in the cross-reference for the object unit in a 
specified library file. 
Examples: 
DEFINE ENTER,SIDE_DOOR IN MY_LIBRARY(A_UNIT) 
means insert the entry names ENTER and SIDE_DOOR in the cross-reference for 
the object unit A_UNIT in library file MY_LIBRARY. 
Related Commands: 
DROP 
00002
00003
00001
00004
Syntax: 
DEL[ETE] fid-entry-list 
Parameters: 
fid-entry-list   -   specifies one or more object or library files accompanied 
by optional object unit names.  The format of a fid-entry-list is: 
obj-fid[(obj-unit[,obj-unit]...)][,obj-fid[(obj-unit[,obj-unit]...)]... 
obj-fid   -   specifies a disk or labeled tape file containing a library file. 
obj-unit   -   specifies the name of an object unit contained in the obj-fid 
file.  If unspecified, the entire file is considered a single object unit. 
Object unit names are user-created identifiers from 1 to 27 characters in 
length, and can consist of any combination of the following characters: 
A-Z   a-z   1-9 
$     #     - (dash) 
*     /     _ (underscore) 
:     @     . (period) 
Description: 
DELETE deletes library files, object files, or object units within library or 
object files. 
Examples: 
DELETE MY_LIBRARY(C_UNIT) 
means delete only object unit C_UNIT from MY_LIBRARY. 
DELETE NEW_OBJECT(A_UNIT),NEXT_OBJECT 
means delete object unit A_UNIT from the object file NEW_OBJECT, and delete 
the entire file NEXT_OBJECT. 
Related Commands: 
COPY, LIST, EXTRACT 
00002
00003
00001
00004
Syntax: 
D[ROP] entry-name[,entry-name]... IN lib-fid(obj-unit) 
Parameters: 
entry-name   -   specifies the entry name to be deleted from the 
cross-reference. 
lib-fid   -   specifies the library file containing the object unit. 
obj-unit   -   specifies the object unit containing the entry-name to be 
dropped. 
Description: 
DROP removes cross-referenced items for entry names in an object unit 
contained in a library file. 
Examples: 
DROP SIDE_DOOR IN MY_LIBRARY(A_UNIT) 
means remove the entry name SIDE_DOOR from the cross-reference index for 
object unit A_UNIT in library file MY_LIBRARY. 
Related Commands: 
DEFINE 
00002
00003
00001
00004
Syntax: 
{EN[D]|X|Q[UIT]} 
Parameters: 
NONE 
Description: 
END terminates LEMUR processing and returns the user to IBEX. 
Examples: 
-END 
means exit LEMUR, return to IBEX. 
Related Commands: 
NONE 
00002
00003
00001
00004
Syntax: 
EX[TRACT] fid-entry-list {ON|TO|INTO|ADDTO|OVER} lib-fid 
Parameters: 
fid-entry-list   -   specifies one or more object or library files accompanied 
by optional object unit names.  The format of a fid-entry-list is: 
obj-fid[(obj-unit[,obj-unit]...)][,obj-fid[(obj-unit[,obj-unit]...)]... 
    where 
    obj-fid   -   specifies a disk or labeled tape file containing a library 
    or an object file. 
    obj-unit   -   specifies the name of an object unit contained in the 
    obj-fid file.  If unspecified, the entire file is considered a single 
    object unit.  Object unit names are user-created identifiers from 1 to 27 
    characters in length, and can consist of any combination of the following 
    characters: 
    A-Z   a-z   1-9 
    $     #     - (dash) 
    *     /     _ (underscore) 
    :     @     . (period) 
ON   -   specifies the creation of a new library file.  The command aborts if 
lib-fid already exists. 
TO   -   is a synonym for ON. 
INTO   -   specifies that, if lib-fid already exists, merge the input 
material, and overwrite where appropriate.  In effect, this allows the 
replacement of obsolete object units in a library file.  If INTO is used, and 
lib-fid does not exist, INTO functions identically to ON or TO. 
ADDTO   -   specifies that, if lib-fid already exists, merge the input 
material, but do not overwrite.  In most cases this appends new object units 
to a previously existing library file.  If ADDTO is used, and lib-fid does not 
exist, ADDTO functions identically to ON or TO. 
OVER   -   specifies that the new library file is to replace any previous file 
with the same fid.  If lib-fid does not already exist, it becomes a 
newly-created library file. 
lib-fid   -   specifies the library file to be created, modified, or replaced. 
This may be any valid CP-6 disk of labeled tape fid. 
Description: 
EXTRACT copies object units within library or object files to an object file. 
The cross-reference index is not copied. 
Examples: 
EXTRACT MY_LIBRARY(A_UNIT) OVER NEXT_OBJECT 
means only object unit A_UNIT is copied over object file NEXT_OBJECT.  The 
cross-reference index is not copied, and NEXT_OBJECT is not a library file. 
EXTRACT NEW_OBJECT,MY_LIBRARY(B_UNIT) INTO NEXT_OBJECT 
means the entire file NEW_OBJECT is copied into object file NEXT_OBJECT, 
replacing any identically named object units.  In addition, the object unit 
B_UNIT in MY_LIBRARY is copied (with replacement, if required) to NEXT_OBJECT. 
Related Commands: 
DELETE, COPY, LIST 
00002
00003
00001
00004
C 
  COPY Command -   
    LEMUR - 
      HELP COPY SYNTAX: 
  COPY Command - 
      HELP COPY 
  COPY Options (LEMUR) - 
      HELP COPY_OPTIONS 
D 
  DEFINE Command - 
      HELP DEFINE 
  DELETE Command -   
    LEMUR - 
      HELP DELETE SYNTAX: 
  DELETE Command - 
      HELP DELETE 
  DROP Command - 
      HELP DROP 
E 
  END Command -   
    LEMUR - 
      HELP END SYNTAX: 
  END Command - 
      HELP END 
  EXTRACT Command - 
      HELP EXTRACT 
L 
  LEMUR Commands - 
      HELP COMMANDS 
  LEMUR COPY Options - 
      HELP COPY_OPTIONS 
  LEMUR Example - 
      HELP LEMUR_EXAMPLE 
  LIST Command -   
    LEMUR - 
      HELP LIST SYNTAX: 
  LIST Command - 
      HELP LIST 
  LIST Options (LEMUR) - 
      HELP COPY_OPTIONS 
00001
00002
00003
HELP_INDEX
LIST
The following example illustrates how LEMUR is used to create a library file: 
!B TEST 
EDIT D00 HERE 
    1.000 A:PROC; 
    2.000 DCL B UBIN; 
    3.000 DCL C UBIN; 
    4.000        B = 1; 
    5.000        C = B; 
    6.000 END A; 
    7.000 %EOD; 
    8.000 B:PROC; 
    9.000 DCL D UBIN; 
   10.000 DCL E UBIN; 
   11.000        D= E; 
   12.000 END B; 
   13.000 
                    A PL6 program is written containing two procedures, A and 
                    B. 
!PL6 TEST OVER TEST_OU (NLS) 
PL6 D00 here at 15:16 FEB 21 '86 
                    The program is compiled and object unit TEST_OU is 
                    created. 
--  Include file information  -- 
         . 
      No diagnostics issued in procedure A 
         . 
         . 
         . 
      No diagnostics issued in procedure B 
         . 
    No errors detected in file TEST.YOURACCT 
                    The PL6 listing indicates that two procedures, A and B, 
                    have been compiled without error. 
!L TEST_OU 
ORG TY  GRAN  NGAV     REC   LAST MODIFIED   NAME 
KEY O6     1     0      24 15:16 FEB 21 '86  TEST_OU 
!LEMUR 
LEMUR D00 here 
-L TEST_OU 
DBG SEV COMPILER     LIBRARY FILE       COMPILE TIME    OBJECT UNIT NAME 
 Y  0   PL6   D00        NO           15:16 FEB 21 '86  A 
 Y  0   PL6   D00        NO           15:16 FEB 21 '86  B 
                    LEMUR is invoked and the LEMUR LIST command is used to 
                    list TEST_OU.  The listing indicates the two object units 
                    within the file, A and B.  The files are not library 
                    files. 
-C TEST_OU INTO TEST_LIBRARY 
  ... COPYing 
                    The COPY command of the LEMUR processor is used to copy 
                    TEST_OU into TEST_LIBRARY. 
-L TEST_LIBRARY 
DBG SEV COMPILER     LIBRARY FILE       COMPILE TIME    OBJECT UNIT NAME 
 Y  0   PL6   D00        YES          15:16 FEB 21 '86  A 
 Y  0   PL6   D00        YES          15:16 FEB 21 '86  B 
-END 
                    The LEMUR LIST command is used to list TEST_LIBRARY, which 
                    indicates that both object units are now library files. 
!L TEST_OU 
ORG TY  GRAN  NGAV     REC   LAST MODIFIED   NAME 
KEY O6     1     0      24 15:16 FEB 21 '86  TEST_OU 
!L TEST_LIBRARY 
ORG TY  GRAN  NGAV     REC   LAST MODIFIED   NAME 
KEY LE     1     0      26 15:18 FEB 21 '86  TEST_LIBRARY 
                    The PCL L command is used (from IBEX) to list TEST_OU and 
                    TEST_LIBRARY.  The file type designator for TEST_LIBRARY 
                    is LE, indicating that LEMUR has been used to create or 
                    modify the file. 
Syntax: 
L[IST] fid-entry-list[(MAP=(attachmentlist)] 
Parameters: 
fid-entry-list   -   specifies one or more object or library files accompanied 
by optional object unit names.  The format of a fid-entry-list is: 
obj-fid[(obj-unit[,obj-unit]...)][,obj-fid[(obj-unit[,obj-unit]...)]... 
    where 
    obj-fid   -   specifies a disk or labeled tape file containing a library 
    or an object file. 
    obj-unit   -   specifies the name of an object unit contained in the 
    obj-fid file.  If unspecified, the entire file is considered a single 
    object unit.  Object unit names are user-created identifiers from 1 to 27 
    characters in length, and can consist of any combination of the following 
    characters: 
    A-Z   a-z   1-9 
    $     #     - (dash) 
    *     /     _ (underscore) 
    :     @     . (period) 
MAP=(attachment list)   -    
Description: 
LIST lists the object units within library or object files.  The following 
information is listed: 
1.  The presence or absence of debugging information (signified by Y for YES 
    and N for NO). 
2.  The severity as defined at creation via the SEVERITY option. 
3.  The compiler which produced this object unit, along with its version 
    number. 
4.  Whether or not the listed file is a library file (YES or NO). 
5.  The time at which the object unit was created by the compiler. 
6.  The object unit name. 
Examples: 
!LEMUR 
-LIST MY_LIBRARY 
DBG SEV COMPILER      LIBRARY FILE    COMPILE TIME      OBJECT UNIT NAME 
 Y  0   PL6   D00         YES         11:48 FEB 16 '86  A_UNIT 
 Y  0   PL6   D00         YES         11:48 FEB 16 '86  B_UNIT 
The object units in MY_LIBRARY are listed.  Two object units are in 
MY_LIBRARY: A_UNIT and B_UNIT.  Both were compiled by PL6 (compiler version 
D00) on February 16, 1986 at 11:48 A.M.  They have debugging information 
included and a 0 severity level associated. 
-LIST NEW_OBJECT 
DBG SEV COMPILER      LIBRARY FILE    COMPILE TIME      OBJECT UNIT NAME 
Y    0   PL6  D00          NO          11:48 FEB 16 '86   A_UNIT 
Y    0   PL6  D00          NO          11:49 FEB 16 '86   C_UNIT 
The object units in NEW_OBJECT are A_UNIT and C_UNIT.  Both have debugging 
information and a severity level of 0.  They were compiled February 16, 1986 
at 11:48 A.M. and 11:49 A.M. respectively.  They are not library files. 
Related Commands: 
DELETE, COPY, EXTRACT 
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
LEMUR (Library Editor and Maintenance Utility Routine) is a processor that 
builds and manipulates library files of object units.  The libraries thus 
built are accessed by the LINK processor when constructing user programs (run 
units) that require library routines. 
A library file is a repository for commonly-used routines; it is similar to an 
object file, except that it includes an index of entry definitions.  When 
constructing a run-unit, the programmer tells LINK which library file to 
search for unsatisfied references; LINK includes only those object unit pieces 
that are required to complete the construction of the run unit. 
LEMUR performs the following tasks: 
1.  Construct a library file from one or more object units reading in one or 
    more object files. 
2.  Delete a library file or delete specific object units along with their 
    cross-references from a library file. 
3.  Replace an existing library file with another library file, or replace an 
    existing object unit along with its cross-references with another object 
    unit. 
4.  Copy a library file to another library file. 
5.  Extract one or more object units from one or more library files (without 
    their cross-references) into one object file. 
6.  List the object units contained within a library file. 
7.  Define a symbol in the cross-reference for a particular object unit in the 
    library file. 
8.  Drop a symbol in the cross-reference for a particular object unit in the 
    library file. 
END
NOTATION
END
