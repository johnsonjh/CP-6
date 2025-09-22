The CP-6 LINK Processor: 
o   Processes object files producing continuous sections of procedure, data 
    and DCBs. 
o   Satisfies references among the object files. 
o   Accesses library files to satisfy primary entry references. 
o   Builds a DCB pointer table for use by the Monitor and builds a Task 
    Control Block (TCB). 
o   Performs all necessary relocation for DELTA, adding records of debug 
    information to the run unit. 
o   Produces maps. 
The LINK processor is accessed through the LINK, MAP, and RUN commands.  These 
commands are entered directly from IBEX. 
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
L 
  Library Searches - 
      HELP LIBRARY_SEARCHES 
  LINK Command - 
      HELP LINK 
  LINK Options - 
      HELP OPTIONS 
M 
  MAP Command - 
      HELP MAP 
O 
  Object File Libraries - 
      HELP OBJECT_FILE_LIBRARIES 
  Overlay Structures - 
      HELP OVERLAYS 
P 
  Program Trees - 
      HELP PROGRAM_TREES 
R 
  Resolving Differences - 
      HELP OVERLAY_REFERENCES 
  RUN Command - 
      HELP RUN 
U 
  Using Overlays - 
      HELP USING_OVERLAYS 
00001
00002
00003
00004
00005
HELP_INDEX
LINK
The CP-6 system recognizes three types of libraries: 
o   Alternate Shared Library (for example, I-D-S/II) 
o   Shared Library (supplied with the CP-6 system or installation-defined.) 
o   Private Libraries (user-defined in LEMUR, or system-supplied) 
The LINK processor performs library searches as directed by the specifications 
on the LINK command.  By default, the LINK processor performs library searches 
as follows.  Information stored in the object unit itself specifies the shared 
library and alternate shared library (if any) to use.  Note: The definitions 
and references from the object file list are input on a node basis.  An 
attempt is made to satisfy all references within the node or within the 
private libraries before proceeding down the node path. 
1.  Associate (input) any definitions from the alternate shared library (only 
    data definitions). 
2.  Associate (input) any definitions from a shared library (both data and 
    entry definitions).  The appropriate shared library is determined by these 
    steps: 
    a.  If SHARELIB is specified, the named library is used.  If unsatisfied 
        primary entry references remain, proceed to step 3; otherwise, the 
        library search is complete.  If SHARELIB is not specified, proceed to 
        step 2b. 
    b.  If a non-standard shared library is identified within the object unit, 
        the named library is used.  If unsatisfied primary entry references 
        remain, proceed to step 3, otherwise, the library search is complete. 
        (Standard shared libraries are the system-supplied libraries, e.g., 
        :SHARED_COBOL.:SYS.)  If the object unit(s) identify a standard shared 
        library, proceed to step 2c. 
    c.  Associate the standard shared library that makes a match with the 
        information in the object unit.  Proceed to step 3.  If multiple 
        object units are included with different system-supplied libraries 
        specified, the LINK processor determines which library to use from 
        this priority list of libraries. 
3.  For primary entry references not satisfied in step 2c, search for and 
    associate the appropriate object unit(s) in the :LIB_xxx library with a 
    suffix matching the shared library.  Proceed to step 4 if there are 
    remaining unsatisfied references. 
4.  For primary entry references not satisfied in step 2c or 3, search for and 
    associate the appropriate object units from the :ETC_xxx library with the 
    suffix matching the shared library. 
5.  If any unsatisfied primary entry references remain the other :ETC_xxx 
    libraries in :SYS are searched. 
LINK's default behavior for library searches can be altered by various 
options: 
o   Step 1 can be altered by specifying ALTSHARELIB, or NOALTSHARELIB, or 
    both. 
o   Step 2 can be altered by specifying SHARELIB, or NOSHARELIB, or both. 
o   Additional private (user) library searches can be requested to occur 
    following step 2 via the UNSAT and LIBSRCH options. 
o   Steps 3, 4, and 5 can be inhibited by specifying NOSYSLIB (or NL). 
Syntax: 
{LINK|LOAD|LYNX} fid[,fid]...[,][tree] 
    [{ON|OVER} rununit[,listfid][(optionlist)]] 
Parameters: 
fid   -   specifies an object file, a run unit file, or a file of LINK 
commands.  If an object file is specified, all of the object units in the file 
are included.  If a run unit is specified, only information concerning defined 
symbols in the file is used; no procedure or data is extracted from the run 
unit file.  Using run unit files, the LINK Processor can satisfy references to 
symbols that are offsets from defined memory images.  See the discussion of 
overlaid programs later in this Section for information on how to specify 
input file lists for an overlaid program. 
tree   -   optionally specifies a tree structure. 
ON   -   specifies that if the value for rununit identifies a file that 
already exists, the existing file is not to be overwritten. 
OVER   -   specifies that if the value for rununit identifies a file that 
already exists, the existing file is to be overwritten. 
rununit   -   identifies the file to contain the run unit.  If rununit is not 
specified, the default is "OVER *L." 
listfid   -   identifies the file for listing output. 
optionlist   -   specifies valid LINK options in the form 
{option|(option[,option][,option]...)}.  Valid options are: 
ALT[SHARELIB]=libfid 
AS[LIB] 
B[REF]=value 
DB[IAS]=address 
DC[BSLOTS]=value 
{DCB1|SI[DCB]}=dcbname 
{DCB2|UI[DCB]}=dcbname 
{DCB3|OU[DCB]}=dcbname 
{DCB4|LO[DCB]}=dcbname 
DP[ATCH]=value 
DU[PLICATE] 
I[NCLUDE] ( (nodename,libfid,pen) [,(nodename,libfid,pen)...] ) 
IP[ATCH]=value 
IXT[NSIZE]=value 
LIBSR[CH](ac1[,ac2]...) 
LL[MU] 
LS[AU] 
M[AP]({N[AME]|V[ALUE]|L[DEF]|U[DEF]}[,{N[AME]|V[ALUE]|L[DEF]|U[DEF]}]...) 
NB[REF] 
{NDCB1|NSI[DCB]} 
{NDCB2|NUI[DCB]} 
{NDCB3|NOU[DCB]} 
{NDCB4|NLO[DCB]} 
NOALT[SHARELIB] 
NOC[HGPMEM] 
{NOD[EBUG]|ND} 
NOE[DITING] 
NOSH[ARELIB] 
{NOSY[SLIB]|NL} 
NPL[OVER] 
NWA[RN] 
OS[P] 
PB[IAS]=address 
PRI[VILEGES]{=priv|[=](priv[,priv]...)} 
PR[OCACC] 
PROMOTE 
PROMOTE_B[LANK] 
PROMOTE_L[ABEL] 
PSEUDO=(resnm[,decimal_number]) 
RE[PORT]=value 
SE[VERITY]=value 
{SHAREA[BLE]|NSHAREA[BLE]} 
SHAREL[IB]=libfid 
SL[IB] 
SLOCK(lock[,lock]...) 
SR[CH](ac1 [,ac2]...) 
ST[ART]=address 
STD[INVOC] 
SUR[CHARGE] 
SY[STEM] 
TC[B]=value 
UN[SAT]={libfid|(libfid,libfid[,libfid...])} 
V[ECTOR](option[,option]...) 
VER[SION]={version|(version)} 
WA[RN] 
WLOCK(lock[,lock]...) 
XT[NSIZE]=value 
Description: 
The LINK command (with synonyms LOAD and LYNX) creates an executable program 
(run unit) and, optionally, creates overlay programs. 
Examples: 
!LINK FIL.ACCT123.PAS OVER MOD (UNSAT=MY_LIB_FILE,SEVERITY=4,DBIAS=10000) 
In this example, the user specifies a library search list, a maximum severity 
level, and a bias: 
This command specifies: 
o   File FIL from account ACCT123 is the object unit to be retrieved. 
o   The library file MY_LIB_FILE is to be searched for external definitions 
    corresponding to unsatisfied primary references (if any exist after 
    linking has been accomplished from all other specified sources). 
o   The name MOD is to be associated with the run unit, which is to be a 
    permanent file in the user's account. 
o   Assuming that the user is authorized with a default read access of ALL, 
    any account may read the run unit, but none may write into it. 
o   Errors of severity level 4 are acceptable. 
o   A relocation bias of octal 10000 is to be used. 
o   No map is to be listed. 
Related Commands: 
RUN, MAP 
00002
00003
00001
00004
OPTIONS
OPTIONS
LINK
LINK
Syntax: 
MAP rununit[ {ON|OVER|INTO} listfid](optionlist) 
Parameters: 
rununit   -   identifies a run unit. 
ON   -   specifies listing onto a newly created file. 
OVER   -   specifies to replace any existing listing file. 
INTO   -   means append listing into existing listing file. 
listfid   -   specifies a file for LINK listing output. 
option   -   is any of the following values: 
    N[AME]   -   requests a map of defined symbols sorted by name. 
    V[ALUE]   -   requests a map of defined symbols sorted by value. 
    L[DEF]   -   requests that used library DEFs be included in the map. 
    U[DEF]   -   requests that all library DEFs (both used and unused) be 
    included in the map. 
Description: 
A map of an existing run unit is produced through the MAP command.  See the 
VECTOR option for differences in the map produced at link time and that 
produced when specifying MAP to IBEX. 
Examples: 
!MAP FIL.ACCT123.PAS (NAME,UDEF) 
Requests a map of run unit FIL.ACCT123.PAS containing defined symbols sorted 
by name and all library DEFs. 
Related Commands: 
RUN, LINK 
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
Program development involves the following three basic steps (modified as 
required to correct errors): 
1.  Compile or assemble a source program. 
2.  Create an executable program.  In the CP-6 system, the executable program 
    is called a run unit. 
3.  Execute the program.  In the CP-6 system, execution of a run unit can be 
    initiated through the LINK or RUN command, or by invoking the run unit by 
    name. 
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
Object files may be assembled into object file libraries using the LEMUR 
processor.  These library files may contain more than one object file.  If a 
library file is specified in the command that invokes the LINK Processor, LINK 
implicitly includes the object units in the run unit because asking for the 
library file causes a search to satisfy unresolved primary entry references. 
Only object units that are needed are included from the library file. 
The LINK and RUN commands recognize the following options: 
ALTSHARELIB, ASLIB, BREF, DBIAS, DCBSLOTS, DCB1, DCB2, DCB3, DCB4, DPATCH, 
DUPLICATE, INCLUDE, IPATCH, IXTNSIZE, LIBSRCH, LLMU, LSAU, MAP, NBREF, NDCB1, 
NDCB2, NDCB3, NDCB4, NOALTSHARELIB, NOCHGPMEM, NODEBUG, NOEDITING, NOSHARELIB, 
NOSYSLIB, NPLOVER, NWARN, OSP, PBIAS, PRIVILEGES, PROCACC, PROMOTE, 
PROMOTE_BLANK, PROMOTE_LABEL, PSEUDO, REPORT, SEVERITY, SHAREABLE, SHARELIB, 
SRCH, START, STDINVOC, SLIB, SLOCK, SURCHARGE, SYSTEM, TCB, UNSAT, VECTOR, 
VERSION, WARN, WLOCK, XTNSIZE. 
To obtain HELP messages about individual messages, type: 
HELP (LINK) OPTIONS option 
The options are displayed in the following format: 
  Opt        Meaning 
  ALT[SHARELIB]=libfid 
        Specifies the name of the alternate shared library to be associated 
        with the run unit.  Libfid can be any file (the account defaults to 
        :SYS if not specified), but the file must be installed as an alternate 
        shared library by SPIDER before the run unit is executed.  See HA21 
        CP-6 System Support Reference manual for a description of SPIDER.  The 
        ALTSHARELIB option inhibits any default alternate shared library 
        association established within any object files. 
  AS[LIB] 
        Specifies that the formed run unit is an alternate shared library. 
  B[REF]=value 
        Specifies that the branch reference mode is to be used to load 
        overlaid programs.  BREF has meaning only if the input object file 
        list specifies an overlaid program; otherwise, the option has no 
        effect.  In branch reference mode, the LINK Processor modifies code in 
        the run unit at the point of any branch from a level to a deeper level 
        in the program tree.  This modified code causes the branch-to node and 
        its complete backward path to be brought into memory from the run unit 
        file, if they are not already there. 
        The number is a decimal value that specifies the maximum number of 
        deeper branch references that can occur within a program.  Each entry 
        in the branch reference loading table requires 2 words.  The default 
        is the number of unique branch references. 
  DB[IAS]=address 
        Is an octal value that specifies the starting virtual address at which 
        data is to be bound.  The default is 0. 
  DC[BSLOTS]=value 
        Is a decimal value that specifies how many spare slots are to be 
        reserved in the DCB pointer list so that DCBs can be added dynamically 
        during program execution.  The default is 12. 
  {DCB1|SI[DCB]}=dcbname 
        Specifies which DCB in the run unit being formed is to be associated 
        with the positionally first or source-input file in the conventional 
        processor invocation syntax.  The default is M$SI. 
  {DCB2|UI[DCB]}=dcbname 
        Specifies which DCB in the run unit being formed is to be associated 
        with the positionally second or update-input file in the conventional 
        processor invocation syntax.  The default is M$UI. 
  {DCB3|OU[DCB]}=dcbname 
        Specifies which DCB in the run unit being formed is to be associated 
        with the positionally third or object-output file in the conventional 
        processor invocation syntax.  The default is M$OU. 
  {DCB4|LO[DCB]}=dcbname 
        Specifies which DCB is the run unit being formed is to be associated 
        with the positionally fourth or listing-output file in the 
        conventional processor invocation syntax.  The default is M$LO. 
  DP[ATCH]=value 
        Is a decimal value that specifies the number of words to be reserved 
        in the data patch space for the run unit.  The default is 0.  A 
        non-zero value enables the use of # modification in RUM. 
  DU[PLICATE] 
        Specifies that all duplicate definitions are to be reported regardless 
        of their origin.  Normally, the LINK Processor will not diagnose a 
        duplicate definition unless more than one of these definitions 
        originates from user-specified object files or user-specified LEMUR 
        library files.  This option removes the origin stipulation and the 
        LINK processor diagnoses duplicates regardless of their origin. 
   I[NCLUDE] ( (nodename,libfid,pen) [,(nodename,libfid,pen)...] ) 
        Includes the specified object units in the specified nodes.  Nodename 
        is the name of the node.  Libfid is the fid of a library file.  Pen is 
        the primary entry name of the object unit to be included.  For 
        example, 
            INCLUDE ( (A,MYLIB,START) ) 
        means the object unit with primary entry name START is in the library 
        file MYLIB and is to be included in the node A. 
  IP[ATCH]=value 
        Is a decimal value that specifies the number of words to be reserved 
        in the instruction patch space for the run unit.  The default is 0.  A 
        non-zero value enables use of @ modification in RUM. 
  IXT[NSIZE]=value 
        Specifies the initial extent of the run unit file. 
        value    is a decimal number from 1 to 2**35-1 (that is, any 
        reasonable size) that specifies the initial extent in the number of 
        granules.  The default is 10. 
  LL[MU] 
        Directs the LINK processor to write out a list of the library modules 
        (object units) used to build the run unit. 
  LS[AU] 
        Directs the LINK processor to write out a list of the object units 
        used along with the accounts these files were found in. 
  LIBSR[CH](ac1[,ac2]...) 
        Specifies the accounts the linker can access when searching for a 
        library file.  If the LIBSRCH option is specified and a library file 
        is encountered in the UNSAT option that does not contain an account, 
        then the linker will search for the file in the accounts given in the 
        LIBSRCH option.  The search is performed in the order specified on the 
        LIBSRCH option, from left to right. 
  M[AP]([{N[AME]|V[ALUE]|L[DEF]|U[DEF]} [,{N[AME]|V[ALUE]|L[DEF]|U[DEF]}]...]) 
        Directs the LINK Processor to write out a program map for the run unit 
        being linked as follows: 
        Map          Map 
        Option       Requested 
        ------       --------- 
        NAME         Defined symbols sorted by name. 
        VALUE        Defined symbols sorted by value. 
        LDEF         Used library DEFs are included in the map. 
        UDEF         All library DEFs (used and unused) are included 
                     in the map. 
        Any combination of these keyword options is allowed.  If both LDEF and 
        UDEF are specified, LDEF is ignored.  See the VECTOR option for 
        differences in the map produced at link time and that produced when 
        specifying MAP to IBEX. 
  NB[REF] 
        Specifies that the branch reference mode is NOT to be used to load 
        overlaid programs.  (Synonymous to BREF = 0).  This option must be 
        used when the program loads its own overlays via M$OLAY monitor 
        service. 
  {NDCB1|NSI[DCB]} 
        Specifies that no DCB should be associated with the positionally first 
        or source-input file in the conventional processor invocation syntax. 
  {NDCB2|NUI[DCB]} 
        Specifies that no DCB should be associated with the positionally 
        second or update-input file in the conventional processor invocation 
        syntax. 
  {NDCB3|NOU[DCB]} 
        Specifies that no DCB should be associated with the positionally third 
        or object-output file in the conventional processor invocation 
  {NDCB4|NLO[DCB]} 
        Specifies that no DCB should be associated with the positionally 
        fourth or listing-output file in the conventional processor invocation 
        syntax. 
  NOALT[SHARELIB] 
        Inhibits the automatic association of any alternate shared library. 
        If ALTSHARELIB is also specified, then only the alternate shared 
        library named in the ALTSHARELIB option will be associated. 
  NOC[HGPMEM] 
        If program resides in :SYS, then procedure pages will not be charged 
        regardless of whether the program is shared or not. 
  {NOD[EBUG]|ND} 
        Suppresses inclusion of debug information in the run unit file except 
        for the external symbol definitions, which are always included. 
        Without this debug information, the utility of DELTA for higher level 
        languages is extremely limited. 
  NOE[DITING] 
        Suppresses the inclusion of most of the system information in the run 
        unit, including the TCB, the tree tables, the read-only segment, the 
        association of shared and alternate shared libraries, the BREF loading 
        mode, the LINK defined pointers (B$JIT$, B$TCB$, B$ROS$), the 
        processor initialization area (PIA), the debugger work area, and the 
        user fault location.  This option will not generate a usable CP-6 
        rununit. 
  NOSH[ARELIB] 
        Inhibits the automatic association of any shared library.  If SHARELIB 
        is also specified, then only the shared library named in the SHARELIB 
        option will be associated. 
  {NOSY[SLIB]|NL} 
        Inhibits automatic inclusion of system library file(s) in the library 
        search list (see UNSAT). 
  NPL[OVER] 
        Suppresses the inclusion of PLOVER records in the run unit. 
  NWA[RN] 
        Suppresses the inclusion of all warning messages supplied by the 
        Linker.  (See WARN). 
  OS[P] 
        Specifies that all data COMMON control sections in an overlaid program 
        are to be forced to the root node. 
  PB[IAS]=address 
        Is an octal value that specifies the starting virtual page address at 
        which procedure is to be bound.  Unless a value is supplied for this 
        parameter, procedure is bound to the page following the last page of 
        the data.  If both DBIAS and PBIAS are specified, the user must ensure 
        that the data and procedure areas do not overlap. 
  PRI[VILEGES]{=priv|[=](priv[,priv]...)} 
        Specifies the special privileges that are to be associated with the 
        run unit.  Some of these privileges are only effective if the run unit 
        file is fetched from the system account (:SYS) that contains the 
        user-shared system libraries.  The privileges are: 
        AS[AVE]                FMR[EAD]            MF[EP] 
        CF[EP]                 FMS[EC]             PM 
        DI[SPJOB]              GP[P]               SP[CLMN] 
        EXM[M]                 IOQ                 SYSC[ON] 
        EXP[M]                 IOQW                SYSL[OG] 
        FMD[IAG]               JIT[M]              TN[D] 
                               MAX[M] 
        See the IBEX PRIV command for a description of these privileges. 
  PR[OCACC] 
        If program resides in :SYS, the program will be charged using 
        processor accounting and not user accounting. 
  PROMOTE 
        Specifies that both the PROMOTE_BLANK and PROMOTE_LABEL options are to 
        be in effect.  The default is not to PROMOTE. 
  PROMOTE_B[LANK] 
        Specifies that all instances of blank common must refer to the same 
        storage allocation.  The LINK processor may promote the allocation of 
        blank common to accomplish this request.  If the PROMOTE_BLANK option 
        is specified, the LINK processor will allocate only one area of blank 
        common so that all instances of blank common refer to the allocated 
        storage.  This may be accomplished by promoting allocation of blank 
        common to one of its ancestors.  In the case above, blank common will 
        be allocated in node B.  The default is not PROMOTE_BLANK. 
  PROMOTE_L[ABEL] 
        Specifies that all instances of labeled common with the same name must 
        refer to the same storage allocation.  The LINK processor may promote 
        the allocation of each and every uniquely named label common.  See 
        PROMOTE_BLANK above.  The default is not PROMOTE_LABEL. 
  PSEUDO=(resnm[,decimal_number]) 
        Specifies a pseudo resource to be associated with a run-unit, thereby 
        limiting the number of users of a specific processor. 
        resnm    is the name of a pseudo resource; it may be from 1 to 8 
        characters. 
        decimal_number    is the number (1-511) of resnm required; the default 
        is 1. 
  RE[PORT]=value 
        Is a decimal value directing the LINK processor to report any object 
        unit whose compilation or assembly error severity is greater than the 
        value specified.  The default is 0. 
  R[UN] 
        Specifies that execution of the run unit is to be initiated as soon as 
        linking is completed. 
  SE[VERITY]=value 
        Specifies an internal severity level which, if exceeded, sets the step 
        condition code to 4.  The default severity level is 11. 
  {SHAREA[BLE]|NSHAREA[BLE]} 
        Specifies that the run unit is shareable.  NSHAREABLE specifies that 
        the run in not shareable.  SHAREABLE is the default. 
  SHAREL[IB]=libfid 
        Specifies the name of the shared library to be associated with the run 
        unit.  Libfid can be any file (the account defaults to :SYS if not 
        specified), but the file must be installed as a shared library by 
        SPIDER before the run unit is executed.  See HA21 CP-6 System Support 
        Reference for a description of SPIDER.  The SHARELIB option inhibits 
        any default shared library association established within any object 
        files. 
  SL[IB] 
        Specifies that the formed run unit is a shared library. 
  SLOCK(lock[,lock]...) 
        Sets a strong series of "locks" or access controls to the run-unit.  A 
        lock is a decimal integer from 1 to 72.  Each user has a set of keys 
        as established by the system manager.  SLOCK specifies that the user 
        must have all the keys to access the run-unit.  See WLOCK. 
  SR[CH](ac1 [,ac2]...) 
        Specifies the accounts the Linker can access when searching for an 
        object unit file.  If the SRCH option is specified and a file is 
        encountered in the link command that does not contain an account, then 
        the linker will search for the file in the accounts given in the SRCH 
        option.  The search is performed in the order specified on the SRCH 
        option, from left to right. 
  ST[ART]=address 
        Is an octal value that specifies the program start address.  This 
        value overrides a start address specified in any of the object units. 
        If START is not specified, the start address is determined from the 
        relocatable code.  The LINK Processor resolves the start address at 
        the first object unit encoded that provides an implicit address.  This 
        address must be in the root node. 
  STD[INVOC] 
        Specifies that a standard invocation of the run unit is required.  If 
        set, IBEX will flag as an error any invocation that does not match the 
        rununit command in IBEX. 
  SUR[CHARGE] 
        Specifies proprietary accounting should be done for the run unit.  If 
        a program resides in :SYS and surcharge is specified, a step 
        accounting record will be written regardless of whether !REPORT has 
        been specified. 
  SY[STEM] 
        Suppresses the inclusion of most system information in the run unit, 
        including the TCB, tree tables, DCBs, and association of public 
        libraries.  SYSTEM is used when linking special program images, like 
        the monitor.  If SYSTEM is specified, output from the LINK Processor 
        has the same general format as a run unit file, but the created entity 
        is not executable as a user program. 
  TC[B]=value 
        Is a decimal value that specifies in frames the maximum number of 
        environments to be stacked in the task environment stack.  The task 
        environment stack saves the program's environments during processing 
        of asynchronous events such as program traps and breaks.  The default 
        is 3. 
  UN[SAT]={libfid|(libfid,libfid[,libfid...])} 
        Specifies the order in which library files are to be searched to 
        resolve unsatisfied primary entry references.  These library files are 
        searched after each node of an overlaid program is linked, if there 
        are any outstanding primary entry references introduced by the node. 
        Only primary entry references cause inclusion of object units from 
        library files.  If the UNSAT option is not specified, only the system 
        library file(s) are automatically searched (see NOSYSLIB).  If private 
        libraries are specified, they are searched before the system library 
        file(s). 
  V[ECTOR](option[,option]...) 
        Specifies that a transfer vector be generated for a shared library. 
        The options are: 
        RF=file   -   specifies that the transfer vector in the specified run 
        unit file should be used. 
        DATA=value   -   used to reserve a specific amount of library data 
        when initially forming a library to allow room for expansion without 
        obsoleting programs linked with the library.  When subsequently 
        forming new versions of the library, this option is used to warn the 
        maker of the library if the data size is being exceeded.  Value is a 
        decimal value from 0 to 256K, indicating 0-256k words. 
        E[NTRIES](entry,[,entry]...)   -   specifies entries in the transfer 
        vector.  Where entry is an ENTDEF name, a range of ENTDEF names 
        (e.g.,A - Z), or EMPTY=decimal, where decimal is the number of empty 
        slots to reserve in the transfer vector.  Note that a hyphen must be 
        enclosed in blanks. 
        REMOVE_E[NTDEF]   -   specifies that the linker should remove all 
        ENTDEF's from the run unit that are not included in the transfer 
        vector. 
        REMOVE_S[YMDEF]   -   specifies that the linker should remove all 
        SYMDEF's from the run unit. 
        The VECTOR option causes the values of entry definitions to be 
        changed.  A map produced at link time will reflect the values before 
        change.  A map produced subsequently will reflect the values after 
        change. 
  VER[SION]={version|(version)} 
        Version may be 1 to 6 characters.  Specifies the version identifier 
        that is put in the run unit that is pointed to by B$VERSION$ symdef 
        (built by LINK).  The run unit can use the $BVERSION$ to find and 
        display its current version. 
  WA[RN] 
        Specifies the inclusion of all warning messages supplied by the 
        Linker.  This is the default. 
  WLOCK(lock[,lock]...) 
        Sets a weak series of "locks" or access controls to the run-unit.  A 
        lock is a decimal integer from 1 to 72.  Each user has a set of keys 
        as established by the system manager.  WLOCK specifies that the user 
        must have any one of the keys to access the run-unit.  See SLOCK.  A 
        non-zero value enables use of @ modification in RUM. 
  XT[NSIZE]=value 
        Specifies the additional extent of the run unit file. 
        value    is a decimal number from 1 to 2**17.  The default is 10. 
00001
00002
00003
00004
00005
00006
00007
00008
00009
00005
00010
00011
00012
00013
00014
00017
00015
00009
00016
00018
00019
00026
00020
00021
00022
00023
00029
00023
00024
00025
00026
00027
00028
00029
00022
00030
00043
00020
00021
00031
00032
00008
00033
00035
00034
00035
00036
00037
00038
00039
00041
00040
00041
00042
00043
00044
00006
00045
00046
00047
00048
00049
00050
00051
00052
00007
00053
00054
00055
00056
00057
00058
The following figure depicts the main memory layout of an overlay program: 
                              +-----------+ 
                              |     D     | 
                              +-----------+ 
                              |     ^ 
                 +------------+     | 
                 |     B      |  OVERLAYS 
                 +------------+     | 
                 |    ^       |     v 
                 |    |       +---------+ 
                 |    |       |    E    | 
   ROOT  +-------+    |       +---------+ 
   NODE  |   A   | OVERLAYS 
         +-------+    | 
                 |    |    +---------+ 
                 |    |    |    F    | 
                 |    |    +---------+ 
                 |    v    |     ^ 
                 +---------+     | 
                 |    C    |     | 
                 +---------+  OVERLAYS 
                           |     | 
                           |     v 
                           +-----------+ 
                           |     G     | 
                           +-----------+ 
Each box represents a portion or node of the program.  Each node is stored as 
a separate entity within the run unit file.  Memory allocation extends 
horizontally, that is, the horizontal coordinate denotes increasing address 
allocation from left to right.  Nodes of the program that overlay each other 
are depicted one over the other in the vertical direction and are connected 
with a line.  Thus, in the sample overlay program, B and C overlay each other, 
D and E overlay each other, and F and G overlay each other. 
Nodes that overlay each other start at the same address, and, depending on 
their size, occupy part or all of the same memory area.  Therefore only one of 
them can reside in main memory at a time. 
In the sample overlay program, seven distinct node combinations can be 
resident in main memory: 
A 
A and B 
A and C 
A, B, and D 
A, B, and E 
A, C, and F 
A, C, and G 
Note that the leftmost node, labeled A, is always in memory.  Node A is the 
root node; it is that portion of the program that resides in memory throughout 
program execution.  There is only one root node in a program and it is never 
overlaid. 
The LINK Processor constructs two different overlay structures, one for data 
(with read/write/execute access), and one for procedure (with read/execute 
access). 
The data structure is allocated first; the procedure structure is allocated 
starting at the page boundary following the maximum path of the data structure 
(unless modified by the PBIAS option). 
Each of the seven combinations listed above falls along a program path.  The 
paths are defined by the linkage from the root node to each of the farthest 
nodes.  Only portions of a program that extend from the root node along one 
path may occupy memory at a time.  The four complete paths in the sample 
overlay program are: 
A, C, and G 
A, C, and F 
A, B, and E 
A, B, and D 
The path formed by A, B and D occupies the most memory and is called the 
maximum path. 
Note that A and the combinations A and B, and A and C form part of a path and 
can be loaded.  The portion of a path that extends from a node back to the 
root is called the backward path of the node.  Any part of a path can be 
loaded. 
See PROGRAM_TREES and USING_OVERLAYS for additional information. 
00001
In overlay structures, a reference to a name (REF) can be satisfied if the 
name is defined (DEF) in the node itself, in one of the descendants of the 
node or in one of the ancestors of the node.  Nodes may communicate with each 
other via REFs and DEFs only if they lie in the same path.  In the sample 
overlay program (see OVERLAYS) if node B references the name SLOTH, SLOTH may 
be defined in B itself, D or E (descendants), or in A (the ancestor). 
However, if the only definition of SLOTH is in any of the nodes C, F, or G, 
the reference from B is unresolved.  Similarly, if a reference to SLOTH 
originates from C, SLOTH may be defined in C, F, G or A, but cannot be 
resolved if the definition is in B, D or E. 
A node is named from the first object file in its defining list.  Each node 
must have a unique name.  Therefore, the programmer needs to ensure that the 
first file specified in each node definition list has a unique name.  For 
example, the following specification is not permitted: 
A(B,C)(B,E) 
But, the following alternatives are permitted: 
A(B,C) (E,B) 
A(C,B) (E,B) 
A(C,B) (B,E) 
Ambiguous References If a reference can be resolved in more than one way, 
resolution is ambiguous.  Overlay structures introduce the possibility that 
the programmer can create ambiguous references.  The following rules govern 
ambiguous references: 
1.  There is no possibility of ambiguity if there are multiple references 
    along the path of a single definition.  For example, none of the following 
    situations are ambiguous: 
        (Ref)          (Def)              (   ) 
         /             /   \              /   \ 
        /             /     \            /     \ 
       /             /       \          /       \ 
    (Ref)          (Ref)   (Ref)     (   )    (   ) 
     /                               /   \ 
    /                               /      \ 
  (Ref)                           (Ref)   (Ref) 
                                /         /   \ 
                               /         /     \ 
                            (Ref)     (   )   (   ) 
2.  If multiple definitions exist, but a single definition occurs on each path 
    in which a reference occurs, resolution is nonambiguous.  For example, the 
    following situation is not ambiguous: 
                          (   ) 
                          /   \ 
                         /     \ 
                      (Def)   (Def) 
                       /         \ 
                      /           \ 
                   (Ref)         (Def) 
3.  Ambiguous resolution occurs if there are multiple definitions along the 
    path of a reference.  All of the following examples introduce ambiguous 
    resolutions: 
       (Ref)          (Ref)                (Ref) 
        /              / \                 / | \ 
       /              /   \               /  |  \ 
      /              /     \             /   |   \ 
    (Def)         (Def)   (Def)      (   ) (   ) (   ) 
    /                                 / \         / \ 
   /                                 /   \       /   \ 
  /                                 /     \     /     \ 
(Def)                            (   )  (   ) (Def)  (   ) 
                                  /      / \ 
                                 /      /   \ 
                                /      /     \ 
                             (Def)  (   )   (   ) 
If there are ambiguous references in an overlay, the LINK Processor selects a 
definition to resolve the reference.  The LINK Processor will select, first, a 
definition from any ancestor, starting with the root node.  If no ancestor 
contains a definition, the LINK Processor will attempt to resolve the 
reference in the current node.  If the current node does not contain a 
definition, the LINK Processor will attempt to resolve the reference from a 
descendant node, selecting in the left-to-right order in which the descendants 
have been defined (see the next subsection). 
Note that if a node at a lower level references a DEF name that is both in a 
higher level node and a library, the library DEF is used. 
The LINK Processor collects ambiguous references, and, at the end of the 
linking process, lists them. 
00001
To simplify the relationships of nodes and to make the paths easily 
identifiable, program overlay structures are often depicted as a tree.  The 
following figure depicts the sample overlay program as a tree structure. 
     Level 0             (A) 
                        /   \ 
                       /     \ 
                      /       \ 
     Level 1        (B)       (C) 
                   /   \     /   \ 
                  /     \   /     \ 
     Level 2    (D)    (E) (F)    (G) 
The linkage forms the paths of the tree and determines the resolution of 
references:  in an overlay program, references are made up and down the paths 
of the program.  The four paths in the sample program are the four unbroken 
lines which proceed from the root node (A), to the four farthest nodes (D, E, 
F, and G). 
Node relationships are defined in terms of levels, meaning their distance from 
the root node, and in terms of parentage, meaning their ancestor/descendant 
associations. 
The root node is at level 0.  Nodes connected to the root node are at level 1, 
and so on through the last level of the tree.  In the sample tree structure, 
there are three levels. 
All nodes except the root node have a parent node, a node at the previous 
level to which the node is directly connected.  For example, all nodes at 
level 1 of a tree structure are directly connected to the root node:  the root 
node is the parent of all level 1 nodes.  The level 1 nodes are referred to as 
the direct descendants of the root node (in the sample tree structure, B and C 
are at level 1 and are the direct descendants of the root node).  Level 1 
nodes, in turn, are the parents of the level 2 nodes connected to them (in the 
sample tree structure, B is the parent of D and E; F and G are the direct 
descendants of C). 
The descendants of a node are all nodes to the nth level of the tree that 
descends in an unbroken line from the node (In the sample tree structure, the 
descendants of B are D and E, and the descendants of A are all the remaining 
nodes in the structure).  A node that has no descendants is referred to as a 
leaf node). 
The ancestors of a node are all parent nodes in a backward path to the root 
node.  (In the sample tree structure, A and B are the ancestors of D). 
Loading Nodes 
The paths of the tree include all possible pieces of the run unit that may be 
memory resident.  One of these paths, the resident path, describes the 
resident nodes at any instant.  When a run is initiated, the resident path 
consists of the root node only.  As execution proceeds, references from a node 
are made to items defined in its ancestors, itself, and its descendants.  If 
the reference is defined in either its ancestors or itself, no additional 
portions of the run unit are brought into memory, since the referencing node 
and all its ancestors are resident.  If the reference is to a descendant, the 
definition may not be in the resident path. 
If the definition is in the resident path, the descendant and all necessary 
ancestors to form a continuous backward path are brought into memory.  If the 
reference is not along the resident path, the operating system examines the 
paths, establishes a new resident path that contains the definition, and 
brings into memory the portions of the run unit that are not present.  For 
example, if the current path is A, B, and D and during execution B references 
a name defined in E, the new resident path is A, B and E.  The portion of the 
run unit corresponding to node E is brought into memory over the address space 
previously occupied by D.  See OVERLAY_REFERENCES for additional information. 
00001
RUN
OVERLAY_REFERENCES
Syntax: 
RUN fid[,fid]...[,][tree][{ON|OVER} rununit,listfid[(option[,option]...)] 
Parameters: 
fid   -   specifies an object file or a run unit file.  If an object file is 
specified, all of the object units in the file are included.  If a run unit is 
specified, only information concerning defined symbols in the file is used; no 
procedure or data is extracted from the run unit file.  Using run unit files, 
the LINK Processor can satisfy references to symbols that are offsets from 
defined memory images. 
tree   -   optionally specifies a tree structure. 
ON   -   specifies that if the value for rununit identifies a file that 
already exists, the existing file is not to be overwritten. 
OVER   -   specifies that if the value for rununit identifies a file that 
already exists, the existing file is to be overwritten.  If neither ON nor 
OVER is specified the default is OVER. 
rununit   -   identifies the file to contain the run unit. 
listfid   -   identifies file for listing output. 
options   -   options are enclosed in a set of parentheses.  If more than one 
option is specified, options are separated by commas: 
ALT[SHARELIB]=libfid 
AS[LIB] 
B[REF]=value 
DB[IAS]=address 
DC[BSLOTS]=value 
{DCB1|SI[DCB]}=dcbname 
{DCB2|UI[DCB]}=dcbname 
{DCB3|OU[DCB]}=dcbname 
{DCB4|LO[DCB]}=dcbname 
DP[ATCH]=value 
DU[PLICATE] 
I[NCLUDE] ( (nodename,libfid,pen) [,(nodename,libfid,pen)...] ) 
IP[ATCH]=value 
IXT[NSIZE]=value 
LIBSR[CH](ac1[,ac2]...) 
LL[MU] 
LS[AU] 
M[AP]([{N[AME]|V[ALUE]|L[DEF]|U[DEF]} [,{N[AME]|V[ALUE]|L[DEF]|U[DEF]}]...]) 
NB[REF] 
{NDCB1|NSI[DCB]} 
{NDCB2|NUI[DCB]} 
{NDCB3|NOU[DCB]} 
{NDCB4|NLO[DCB]} 
NOALT[SHARELIB] 
NOC[HGPMEM] 
{NOD[EBUG]|ND} 
NOE[DITING] 
NOSH[ARELIB] 
{NOSY[SLIB]|NL} 
NPL[0VER] 
NWA[RN] 
OS[P] 
PB[IAS]=address 
PRI[VILEGES]{=priv|[=](priv[,priv]...)} 
PR[OCACC] 
PROMOTE 
PROMOTE_B[LANK] 
PROMOTE_L[ABEL] 
PSEUDO=(resnm[,decimal_number]) 
RE[PORT]=value 
SE[VERITY]=value 
{SHAREA[BLE]|NSHAREA[BLE]} 
SHAREL[IB]=libfid 
SL[IB] 
SLOCK(lock[,lock]...) 
SR[CH](ac1 [,ac2]...) 
ST[ART]=address 
STD[INVOC] 
SUR[CHARGE] 
SY[STEM] 
TC[B]=value 
UN[SAT]={libfid|(libfid,libfid[,libfid...])} 
V[ECTOR](option[,option]...) 
VER[SION]={version|(version)} 
WA[RN] 
WLOCK(lock[,lock]...) 
XT[NSIZE]=value 
Description: 
The RUN command creates an executable program (run unit), optionally creates 
overlays, and submits the run unit for immediate execution. 
Related Commands: 
LINK, MAP 
00002
00001
00003
NOTATION
The programmer uses the complex form of the LINK, LOAD, LYNX or RUN commands 
to define and describe a program overlay structure.  In fact, the only 
difference between the complex and simple forms of these commands is the 
additional syntax included in the complex form through which the programmer 
defines nodes and describes relationships in an overlay program.  The 
programmer defines member nodes by specifying their names, and describes their 
relationships by identifying their levels through balanced or nested 
parentheses.  The tree specification in the LINK command has the following 
format: 
(fid[,fid]...[tree])[tree] 
The syntax conveys the recursive nature and the two dimensional aspects of an 
overlay structure.  At level 0 there is only one dimension (vertical), but at 
level 1 there are two dimensions (vertical and horizontal).  Consider the 
following tree structure: 
                          (A) 
                         /   \ 
                        /     \ 
                      (B)     (C) 
This overlay structure is defined as follows: 
A(B)(C) 
Note that the root node (A) is not enclosed in parentheses, that each of its 
level 1 descendants is defined as a tree, and that that definition is 
communicated by enclosing each level 1 node in a separate set of parentheses. 
Note also that both the member nodes and the tree order is established through 
the command:  B is now defined as the leftmost path.  This order is important 
in that it establishes the order in which the LINK Processor searches 
descendant nodes to resolve ambiguities. 
Now, consider again the tree structure: 
                         (A) 
                        /   \ 
                       /     \ 
                      /       \ 
                    (B)       (C) 
                   /   \     /   \ 
                  /     \   /     \ 
                (D)    (E) (F)    (G) 
This overlay structure is defined as follows: 
!LINK A(B(D)(E))(C(F)(G)) ON... 
Usage Note: 
The BREF LINK option must be specified for overlays unless the program loads 
its own overlays via M$OLAY monitor service.  The value usually specified for 
BREF equals the number of nodes minus one.  See HELP (LINK) OPTIONS BREF 
When overlay structures become more complex, they may contain ambiguous 
references.  See OVERLAY_REFERENCES. 
00001
