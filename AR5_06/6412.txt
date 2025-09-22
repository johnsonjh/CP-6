    The IMP processor is invoked by the following command: 
    !IMP [fid1] [{ON|OVER} fid2] [(command)][,listing-fid] 
Parameters: 
fid1   -   is a file of IMP commands, or the fid2 (object file) of a 
previously issued IMP command.  In either case the IMP functions defined are 
immediately applied to the terminal session unless fid2 specifies a file.  The 
default is ME. 
fid2   -   is an output file for IMP functions or the name of a stream in a 
window to which the IMP functions defined are to be immediately applied.  This 
parameter is ignored if it specifies a file and fid1 specifies an IMP object 
file. 
command   -   is a single IMP command that replaces the commands in fid1. 
This parameter is ignored if fid1 specifies a file. 
listing-fid   -   is an optional file for IMP output. If specified, 
listing-fid will receive all output except M$DO, which always goes to the 
user's terminal unless !SET M$DO ??? is specified. 
Examples: 
!IMP 
IMP C01 HERE 
->D ALL 
->END 
! 
The -> is a prompt indicating that IMP is prepared to receive commands.  In 
answer to the prompt, the user enters D ALL to delete all previous IMP 
commands.  This takes effect immediately following the END command, which 
returns the user to IBEX. 
!IMP IMP_COMMANDS 
! 
This command invokes IMP to read a file of commands from the file 
IMP_COMMANDS.  These commands take effect immediately after the end of file is 
read.  The user is returned to IBEX. 
!IMP IMP_COMMANDS OVER IMP_OU 
! 
In the above case, commands are read from the file IMP_COMMAND, and IMP output 
is written to IMP_OU.  The input functions take effect when the following is 
specified: 
!IMP IMP_OU 
!IMP ON UC05 (ADD SPECIAL '#' T='A.X' READ TY ECHO) 
! 
This is a one time invocation of IMP, with this input function taking effect 
immediately in the window containing UC05. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
ADD
If specified, the CP-6 system will acknowledge the input function with an 
'<identifier>'.  The '<F>' obtained when <ESC> <F> is typed is an example of 
this.  This component is optional.  When a system input function is used as 
part of an IMP defined input function, the system input function will not 
acknowledge independently of the setting of this component. 
Syntax: 
A[DD] [function-type [I[NTRODUCER]=introducer]] identifier input-operator-1 
[...input-operator-n] 
Parameters: 
function-type   -   is one of the following: 
    P[RIMARY_ESCAPE] 
    SE[CONDARY_ESCAPE] 
    SP[ECIAL_CHARACTER] 
introducer   -   is used only when function type is PRIMARY ESCAPE or 
SECONDARY ESCAPE.  It may be one or two characters specified in either of the 
following two ways: 
1.  token[,token] 
    where token may be any of the following: 
    any alphanumeric ASCII character enclosed in single quotes or slashes 
    any valid ASCII mnemonic taken from the following set:  NUL, SOH, STX, 
    ETX, EOT, ENQ, ACK, BEL, BS, HT, LF, VT, FF, CR, SO, SI, DLE, DC1, DC2, 
    DC3, DC4, NAK, SYN, ETB, CAN, EM, SUB, ESC, FS, GS, RS, US, SP, DEL 
    X'nn' - where nn is two hexadecimal digits 
    O'nnn' - where nnn is three octal digits 
    for the first token only - any function-key-name or control-string-name 
2.  'charactercharacter' or /charactercharacter/ 
    where character may be any alphanumeric ASCII character.  Note that there 
    is no space separating the two characters inside the slashes or single 
    quotes.  However, the ASCII blank can be one or both of the characters. 
identifier    -   is a function-key-name, a control-string-name, or a single 
character specified in one of the following two ways: 
1.  /character/ or 'character' 
    where character may be any ASCII alphanumeric character, 
2.  character 
    where character may be: 
    any valid ASCII mnemonic taken from the following set:  NUL, SOH, STX, 
    ETX, EOT, ENQ, ACK, BEL, BS, HT, LF, VT, FF, CR, SO, SI, DLE, DC1, DC2, 
    DC3, DC4, NAK, SYN, ETB, CAN, EM, SUB, ESC, FS, GS, RS, US, SP, DEL, 
    X'nn' - where nn is two hexadecimal digits, 
    O'nnn' - where nnn is three octal digits. 
input-operator(s)   -   take the following form: 
    T[EXT]= text-string [A[CKNOWLEDGE]][E[CHO]] phase operation 
    text-strings may be any combination of the following separated by commas: 
        Quoted string - e.g., 'ABC' 
        Slash string - e.g., /ABC/ 
        A standard ASCII control code mnemonic chosen from the same set as the 
        INTRODUCER and IDENTIFIER mnemonics. 
        A hexadecimal string of one or more characters - e.g., X'414243' 
        An octal string of one or more characters - e.g., O'101102103' 
    phase may be either or both of the following: 
        R[EAD] 
        I[MMEDIATE] 
    operation may be any one of the following: 
        IN[PUT_FUNCTION] 
        TY[PEAHEAD_BUFFER] 
        B[UFFER] 
        W[RITE] 
        {WRITE_T[RANSPARENT]}|{WT} 
        {WRITE_V[IRTUAL]}|{WV} 
Description: 
The ADD command adds a user-defined input function. 
The first ADD command for a given escape function type must specify an 
INTRODUCER.  All subsequent commands for the same function type will 
automatically have the same INTRODUCER.  This applies only to primary and 
secondary escapes, not special characters, function keys, or control strings. 
An ADD operation performed with an input function already in place, identified 
with the same identifier, causes an implied delete (see DELETE command) of the 
old input function. 
An ADD primary or secondary escape operation performed with some input 
functions of the same type already in place but with a different introducer 
specification will cause an error to be reported when the operation is 
actually applied to the terminal session.  This usually occurs when IMP 
returns to IBEX.  In the case of a newly created window in which the functions 
were "inherited" from a previously existing window, this conflict is resolved 
by first performing a DELETE PRIMARY ALL or DELETE SECONDARY ALL operation. 
Examples: 
-> ADD PRIMARY I=ESC '1' T='WRITE THIS TEXT' I ACK WRITE 
This command adds a primary escape sequence whose introducer is the ASCII ESC 
and whose identifier is '1'.  The escape sequence will have the effect of 
writing the indicated text to the user's console, preceded by '<1>', the 
acknowledgment.  No text will be buffered.  The operation will be performed at 
keystroke time. 
-> ADD SPECIAL '#' T='A.X',CR R ECHO INPUT 
This command adds a special character '#'.  When a # is typed in, the 
indicated text string will be placed in the user's read buffer and the 
carriage return will cause activation to occur.  The processor A.X may then be 
invoked.  The text string will be echoed to the user's terminal if echoplex is 
turned on.  This input function occurs only if a read is pending.  If no read 
is pending, it will be buffered until the next logical read to the terminal, 
for this data.  Since carriage return (CR) is specified here, and no text 
follows it, the INPUT_FUNCTION operation may be used.  Carriage return and 
line feed (LF) should be processed in this manner.  TYPEAHEAD_BUFFER could 
also have been used, but need only be used when text follows an activation 
character. 
-> ADD SECONDARY INTRO=F1 '1' T='F$DCB.ARS#' READ TYP 
This command adds a secondary escape sequence introduced by the F1 function 
key and identified by '1'.  When the next logical read comes to the user's 
terminal, the text will be placed in his typeahead buffers.  This type of 
sequence might be used by a programmer keying in a source program with many 
occurrences of the string 'F$DCB.ARS#'. 
-> ADD SPECIAL '$' TEXT=ESC IMMEDIATE READ INPUT_FUNCTION 
This command adds a special character '$' which maps to the system escape 
introducer.  A command like this might be executed if the ESC key on a given 
keyboard is in an inconvenient place.  Note that both READ and IMMEDIATE are 
used here, since the phase of the system function being introduced is unknown. 
-> ADD LTARROW T=BS READ INPUT_FUNCTION 
-> ADD RTARROW T=DC2 READ INPUT_FUNCTION 
On a Honeywell VIP7801, there are two keys with arrows facing in the left and 
right direction, respectively.  The key with the right pointing arrow 
generates an <ESC> <C> sequence, the key with the left pointing arrow an <ESC> 
<D> sequence.  The two commands above allow these two keys to move the cursor 
in the left and right directions.  A BS will move the cursor left and a DC2 
moves the cursor to the right.  Both are defined to occur during the read 
phase, since editing is meaningful only in this phase. 
-> ADD SECONDARY I=ESC,'[' 'I' T=ESC,'J' TYPEAHEAD READ 
The above example shows how a two-character introducer can be used.  On a 
Honeywell VIP7801, the DEL CHAR INS key generates ESC '[ I', a three-character 
sequence.  By means of the above IMP command, this three-character sequence is 
defined as <ESC> <J>, which triggers the insert mode.  Once this 
three-character sequence has been implemented as shown above, the 'DEL CHAR 
INS' key is redefined as <ESC> <J>. 
It could also be defined as follows: 
-> ADD INSERT_CHAR T=ESC 'J' TYPEAHEAD READ 
provided the terminal profile has the INSERT_CHAR key defined. 
The following example shows how imbedded activation characters are used to 
provide combinations of often-typed keystroke sequences. 
-> ADD SPECIAL '&' T='EDIT SOURCE_FILE',CR,'TY 0-100',CR; 
-> TYPEAHEAD READ 
If a user had an often-used source file and usually looked at the first few 
lines in the file, he could define a special character that gave him all his 
keystrokes at once.  This input function will only occur during the read 
phase, and the text will be echoed to the user's terminal if echoplex is 
turned on.  (Note the semicolon used for continuation and that TYPEAHEAD was 
specified, since an imbedded activation character was present.) 
00002
00003
00001
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
Although it is possible to redefine any single character that the terminal can 
send, most SPECIAL CHARACTER definitions will refer to the control codes.  An 
example is the system input function <CNTL-Y>.  However, redefinition of 
normal printing characters may sometimes be desirable when using a terminal 
whose keyboard layout is unfamiliar. 
Since the SPECIAL characters are checked last, they may never be the same as 
introducers.  When the CP-6 system sees an introducer not followed by an 
identifier it recognizes, the translation logic terminates, and the SPECIAL 
character never gets translated. 
A SPECIAL character may be set up to generate an introducer.  When this is 
done, the character keyed in after the SPECIAL character is treated as the 
identifier.  In addition, when the CP-6 system sees an identifier it does not 
recognize following an introducer it does recognize, the pair will be treated 
as if the introducer was never keyed in;  only the identifier will appear. 
IMP recognizes four commands: 
ADD 
DELETE 
SPELL 
END 
See also INVOKING_IMP 
Input functions are made up of one or more input operators.  Input operators 
define what is to be done by the input function.  An input operator specifies 
strings of characters, what is to be done with those characters, and when it 
is to be done.  Input operators have three required components and two 
optional components: 
1.  TEXT 
2.  PHASE 
3.  OPERATION 
4.  ACKNOWLEDGE (optional) 
5.  ECHO (optional) 
The following concepts are needed to understand the IMP Processor: 
INPUT FUNCTIONS 
INPUT FUNCTION TYPES 
FUNCTION KEYS 
SPECIAL CHARACTERS 
CONTROL STRINGS 
CONTROL CODE MAPPING 
DATA CONTROL BLOCKS 
CONTROL STRINGS are internally generated by the CP-6 terminal handler in 
response to certain line conditions.  The four conditions so recognized by the 
asynchronous terminal handler are BREAK, PARITY ERROR, DATA OVERRUN, and LINE 
DISCONNECT.  It is possible to redefine the meaning of the first three with 
the IMP processor, using the special names BREAK, PARITY, and OVRRUN.  It is 
not possible for a control string to be recognized as any other type of input 
because it does not actually consist of characters received from the device. 
The position of CONTROL STRINGS in the order of recognition is therefore 
irrelevant. 
DELETE
IMP reads through M$SI and writes through M$ME.  Diagnostic output is written 
through M$DO.  Object unit output is written through F$IMP.  File names may be 
specified on the processor invocation line for both source input (M$SI) and 
object unit output (F$IMP). 
If an object unit is created, input functions do not take effect until that 
object unit is read back via IMP.  This can be achieved by specifying the IMP 
created object unit name as the SI file name on subsequent IMP invocations. 
IMP will examine the SI file type, realize it had previously created it, and 
take the appropriate action. 
Syntax: 
D[ELETE] A[LL] 
D[ELETE] function-type A[LL] 
D[ELETE] function-type identifier 
D[ELETE] function-key-name 
D[ELETE] control-string-name 
Parameters: 
Both the function-type and identifier fields are composed the same way as 
those discussed under the ADD command. 
If ALL is specified without function-type, the normal system input function 
table is restored as the user's only input function table.  All user defined 
input functions disappear.  No other options may be specified with ALL. 
If ALL is specified instead of an identifier, all input functions of the 
specified function-type are deleted.  For the DELETE command, the function 
types FUN[CTION_KEY] and CTRSTR are also permitted when used with ALL. 
If an identifier is specified, just the input function associated with that 
identifier is deleted. 
Note:  An ADD operation performed with an input function already in place, 
identified with the same identifier, causes an implied delete of the old input 
function. 
Description: 
Deletes input functions. 
Examples: 
-> DELETE ALL 
This operation is used to delete all user defined input functions and return 
to those supplied by the CP-6 system. 
-> DELETE PRIMARY_ESCAPE ALL 
This command is used to delete all user defined primary escapes. 
-> DEL P 'I' 
This command is used to delete the primary input function with the identifier 
'I'. 
-> DEL SPECIAL X'2A' 
This command is used to delete the special character input function identified 
by an asterisk (*).  The only way to delete special characters in interactive 
mode is to specify them as mnemonics or as hexadecimal or octal strings, since 
any time the special character is typed it is replaced by the text specified 
in its input function. 
Related Commands: 
ADD 
00002
00003
00001
00004
END
If specified, the text associated with this input operator will be echoed to 
the user's terminal.  Note that if echoplex has been turned off, no echoing 
will occur, no matter what is specified here.  ECHO has an effect on BUFFER 
and INPUT_FUNCTION operations and has no effect on WRITE and TYPEAHEAD_BUFFER 
operations.  The ECHO component is optional. 
Syntax: 
{E[ND]|Q[UIT]} 
Parameters: 
None 
Description: 
Exits the IMP processor. 
Note:  IMP may also be exited by an end of file. 
Examples: 
-> END 
This command exits IMP. 
Related Commands: 
None 
00002
00003
00001
00004
Input functions define character strings and the procedures for manipulating 
those strings. 
Escape sequences, which are one type of input function, are identified by two 
parts: the INTRODUCER and the IDENTIFIER. 
o   the INTRODUCER is the character or sequence of two characters which tell 
    the CP-6 system that this keystroke sequence may be an input function. 
    For system input functions, this is the ASCII character ESC. 
o   the IDENTIFIER is the character which indicates which input function to 
    invoke.  For example, in the system <ESC><F> input function, F is the 
    identifier. 
See the ADD command for details of how INTRODUCERS and IDENTIFIERS are 
specified. 
In certain cases, only one keystroke is necessary to invoke an input function. 
This is the case of the SPECIAL CHARACTER and the FUNCTION KEY described 
below.  The system input function <CNTL-X> is an example of a special 
character input function. 
If the terminal profile has been properly created, those terminal keys that 
cause multi-character sequences to be sent will have been assigned 
function-key-names.  Those names can be used in IMP to redefine the character 
sequences sent by the keys.  The SPELL command is used to determine the 
name(s) associated with any particular key. 
Note that IMPing via key-name doesn't conflict with, or use, either the 
primary or secondary escapes also available.  In fact, the first key of a one 
or two key introducer for the escapes can be defined as a keyname. 
Note also that the characters comprising a function-key must be received 
quickly to be so interpreted.  This makes it possible to have two different 
meanings for the same sequence, depending on how quickly it is typed.  This 
timing information is lost when such a sequence must be saved as type-ahead, 
so if the slow meaning is to be used in READ phase, it must not be typed 
ahead. 
A 
  ACKNOWLEDGE Component (IMP) - 
      HELP ACKNOWLEDGE 
  ADD Command - 
      HELP ADD 
C 
  Control Code Mapping - 
      HELP MAPPING 
  Control Strings - 
      HELP CONTROL_STRINGS 
D 
  Data Control Blocks - 
      HELP DCBS 
  Data Control Blocks (DCBs) -   
    IMP - 
      HELP DCBS 
  DCBs -   
    IMP - 
      HELP DCBS 
  DELETE Command -   
    IMP - 
      HELP DELETE SYNTAX: 
  DELETE Command - 
      HELP DELETE 
E 
  ECHO Component - 
      HELP ECHO 
  END Command -   
    IMP - 
      HELP END SYNTAX: 
  END Command - 
      HELP END 
F 
  Function Keys - 
      HELP FUNCTION_KEYS 
I 
  identifier (IMP) - 
      HELP FUNCTIONS 
  IMP -   
    control code mapping - 
      HELP MAPPING 
    identifier - 
      HELP FUNCTIONS 
    introducer - 
      HELP FUNCTIONS 
    two-character introducer - 
      HELP FUNCTIONS 
    two-character introducer example - 
      HELP ADD EXAMPLES: 
  IMP ACKNOWLEDGE Component - 
      HELP ACKNOWLEDGE 
  IMP command - 
      HELP INVOKING_IMP 
  IMP Commands - 
      HELP COMMANDS 
  IMP Components - 
      HELP COMPONENTS 
  IMP Concepts - 
      HELP CONCEPTS 
  IMP OPERATION Component - 
      HELP OPERATION 
  IMP PHASE Component - 
      HELP PHASE 
  IMP TEXT Component - 
      HELP TEXT 
  Input Function Types - 
      HELP TYPES 
  Input Functions - 
      HELP FUNCTIONS 
  introducer (IMP) - 
      HELP FUNCTIONS 
  Invoking IMP - 
      HELP INVOKING_IMP 
O 
  OPERATION Component (IMP) - 
      HELP OPERATION 
P 
  PHASE Component (IMP) - 
      HELP PHASE 
S 
  Special Characters - 
      HELP CHARACTERS 
  SPELL Command -   
    IMP - 
      HELP SPELL_COMMAND SYNTAX: 
  SPELL Command - 
      HELP SPELL_COMMAND 
T 
  TEXT Component (IMP) - 
      HELP TEXT 
  two-character introducer -   
    example - 
      HELP ADD EXAMPLES: 
    IMP - 
      HELP FUNCTIONS 
00001
00002
00003
00004
00005
00006
00007
00008
00009
HELP_INDEX

The following table provides a commonly used mapping of control codes to 
hexadecimal values. 
  CNTL-CHAR        CODE        MNEMONIC 
<CNTL-A>         X'01'       SOH 
<CNTL-B>         X'02'       STX 
<CNTL-C>         X'03'       ETX 
<CNTL-D>         X'04'       EOT 
<CNTL-E>         X'05'       ENQ 
<CNTL-F>         X'06'       ACK 
<CNTL-G>         X'07'       BEL 
<CNTL-H>         X'08'       BS 
<CNTL-I>         X'09'       HT 
<CNTL-J>         X'0A'       LF 
<CNTL-K>         X'0B'       VT 
<CNTL-L>         X'0C'       FF 
<CNTL-M>         X'0D'       CR 
<CNTL-N>         X'0E'       SO 
<CNTL-O>         X'0F'       SI 
<CNTL-P>         X'10'       DLE 
<CNTL-Q>         X'11'       DC1 
<CNTL-R>         X'12'       DC2 
<CNTL-S>         X'13'       DC3 
<CNTL-T>         X'14'       DC4 
<CNTL-U>         X'15'       NAK 
<CNTL-V>         X'16'       SYN 
<CNTL-W>         X'17'       ETB 
<CNTL-X>         X'18'       CAN 
<CNTL-Y>         X'19'       EM 
<CNTL-Z>         X'1A'       SUB 
The following table specifies some characters requiring extra user care when 
redefining: 
  CHAR        Reason for Caution 
<DC1>       Certain terminals use these characters for flow control 
<DC3>       purposes.  The terminal itself may send them to tell 
<ACK>       the CP-6 system what the current state of its buffer is. 
            For terminals with no flow control, this is not a problem. 
<CNTL-J>    This is the line feed function. 
<CNTL-M>    This is the carriage return function. 
<CNTL-H>    This is the backspace function. 
<CNTL-I>    This is the horizontal tab function. 
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
The operation component tells the CP-6 system what is to be done with the text 
specified in the input operator.  There are six possibilities: 
TYPEAHEAD_BUFFER, INPUT_FUNCTION, WRITE, WRITE_TRANSPARENT, WRITE_VIRTUAL, and 
BUFFER. 
TYPEAHEAD_BUFFER 
This means place this text into the user's typeahead buffers.  This is almost 
identical to the user keying in the text at his terminal, except that certain 
translation which is normally performed on keyboard generated text will not be 
done.  This includes translation from the code set generated by the keyboard 
to the code set understood by the CP-6 system.  This, in general, should not 
be a problem, since normal ASCII text is used by the TEXT operator.  When 
generating text that is to be buffered, this operation must be used if the 
text contains an activation character, followed by additional text.  This is 
because the INPUT_FUNCTION and BUFFER operators below will stop processing on 
activation and all text after the activation character will be lost. 
INPUT_FUNCTION 
This means pass this text through the system input function table for possible 
input function recognition and read buffering.  This gives the user the 
capability to use system input functions in concert with his own, or to invent 
new combinations of system input functions.  To have the desired effect, the 
PHASE of the user's input function and that of the system input function he is 
using must be identical.  Remember, if activation will occur within the text 
string, TYPEAHEAD_BUFFER must be used. 
WRITE 
This means pass the specified text directly to the user's terminal.  Do not 
pass it to the reading program. 
WRITE_TRANSPARENT 
This means pass the specified text directly to the user's terminal with a 
transparent write.  Do not pass it to the reading program. 
WRITE_VIRTUAL 
This means pass the specified text directly to the user's terminal as if it 
has been written from a host program. 
BUFFER 
This means place this text into the user's read buffers.  The data in this 
buffer will eventually be placed in the reading program's buffer.  No more 
translation or checking for system input functions will be done.  If 
activation occurs, all unprocessed text is lost.  The BUFFER component cannot 
be used with IMMEDIATE PHASE component. 
00006
00002
00001
00003
00004
00005
The phase of an input operator specifies when the activity associated with 
this operator is to occur.  Following are the two possibilities: 
o   READ - Specifying READ indicates that this input operator is only to be 
    processed if a read is pending at the user's console.  If no read is 
    pending, the character(s) INVOKING this input operator will be buffered 
    until the next read that would logically read the data.  At that time any 
    operators specifying READ will be processed. 
o   IMMEDIATE - Specifying IMMEDIATE indicates that this operator will be 
    processed at keystroke time, independent of whether or not a read is 
    pending.  IMMEDIATE is permissible for any OPERATION component except 
    BUFFER. 
The table below gives the phase of some commonly used system input functions. 
Note that the <ESC> <V> requires both read and immediate processing.  This is 
to accommodate a sequence like <ESC><V> <CNTL-Y>.  This sequence should have 
no effect until a read is pending.  Without IMMEDIATE being specified, this 
would not be true, since <CNTL-Y> would have its usual effect (return control 
to the command processor) if the <ESC><V> were not honored. 
  SYSTEM INPUT FUNCTION          PHASE 
Backspace                      READ 
Carriage Return                READ 
<ESC> <A>                      IMMEDIATE 
<ESC> <D>                      READ 
<ESC> <E>                      READ 
<ESC> <F>                      READ 
<ESC> <G>                      IMMEDIATE 
<ESC> <H>                      IMMEDIATE 
<ESC> <K>                      READ 
<ESC> <M>                      READ 
<ESC> <N>                      READ 
<ESC> <O>                      READ 
<ESC> <R>                      READ 
<ESC> <V>                      READ,IMMEDIATE 
<ESC> <W>                      IMMEDIATE 
<CNTL-R>                       READ 
<CNTL-H>                       READ 
Note:  Since an input function can have multiple input operators, those 
defined as IMMEDIATE will be processed at keystroke time, and those defined as 
READ will be processed by the CP-6 system at the logical time.  Those defined 
as both will be processed twice if the two times are not the same. 
CP-6 IMP (Input Manipulation Processor) defines new escape sequences, function 
keys, and special characters.  IMP commands specify text strings that are to 
be generated as a result of a specified keystroke at the terminal (such as an 
escape sequence or special character).  Using IMP, user-defined escape 
sequences or special characters may invoke unique combinations of system 
escape sequences and special characters, or new special purpose functions 
suited to the individual user. 
Applications of IMP vary widely.  IMP has been used to: 
o   redefine the keys on the keyboard of one terminal so that it looks like 
    the keyboard of another terminal 
o   define function keys to perform commonly used functions such as checking 
    on jobs 
o   define keys to generate often used strings such as lengthy variable names 
    in a program. 
END
Syntax: 
[SP[ELL]] key 
Parameters: 
key   -   any terminal key. 
Description: 
The SPELL command is provided to assist in determining the characteristics of 
the function key definitions provided in the terminal profile.  It is only 
operable in interactive mode and with no currently defined function-key input 
functions.  The DELETE FUNCTIONKEY ALL command may be used to accomplish the 
latter, but must be followed by END and re-invoking IMP to take effect.  If a 
particular function key is defined in the profile, it will activate the read 
and IMP will display its name with a slash preceding any optional portion of 
the spelling.  If the key activates the read, the SPELL keyword is optional. 
Examples: 
->SPELL <left-arrow-key> 
=Funkey LTA/RROW 
->SPELL <CNTL-G><CR> 
=Spcchr BEL 
->SPELL <Q><CR> 
=Spcchr 'Q' 
->END 
! 
00002
00003
00001
CONTROL_STRINGS
NOTATION
This component specifies a string of characters to be operated on. 
There are five types of input functions:  PRIMARY ESCAPES, SECONDARY ESCAPES, 
SPECIAL CHARACTERS, FUNCTION KEYS, and CONTROL STRINGS.  The first two are 
composed of an introducer followed by an identifier.  The third is just a 
single character.  The five classes are distinguished only by the order in 
which the CP-6 system checks an incoming character sequence to see to which of 
the classes it belongs.  In all other ways, the five classes are identical. 
When a character is received from the terminal, the CP-6 system first checks 
whether it is defined by the terminal profile to start a function key 
sequence.  If not, the system checks to see if it was declared by the user to 
be a PRIMARY introducer, SECONDARY introducer or SPECIAL character, in that 
order.  If all these checks fail, the CP-6 system then checks the system 
tables to see if a match is found in its PRIMARY, SECONDARY or SPECIAL tables, 
also in that order.  The user's tables are always checked before the system's. 
This allows the user to redefine any system defined input function. 
If a character or sequence matches a function key in the profile, but no user 
definition for that key exists, the sequence is interpreted as though the 
profile definition did not exist. 
If a match is found when searching for an introducer, the CP-6 system will 
remember that an escape sequence is pending for any level which had an 
introducer which matched the one that was keyed in.  When the rest of the 
sequence is received, all pending levels will be checked, in the same order, 
to see if an identifier match can be found. 
Note that this means it is difficult to define a special character that is the 
same as a function key introducer or a user escape introducer.  The character 
most often so affected is the <ESC> key.  The CP-6 system recognizes such a 
definition only if the character is not used as an introducer by the user for 
a primary or secondary escape.  If such a definition is used, the function key 
definitions in the profile that uses the introducer are disabled. 
To summarize, the input function recognition order is the following: 
1.  FUNCTION KEY or CONTROL STRING 
2.  USER PRIMARY ESCAPE 
3.  USER SECONDARY ESCAPE 
4.  USER SPECIAL CHARACTER 
5.  SYSTEM PRIMARY ESCAPE 
6.  SYSTEM SECONDARY ESCAPE 
7.  SYSTEM SPECIAL CHARACTER 
Having multiple sets of input functions gives the user the capability to 
define a large number of his own functions.  The PRIMARY set could be set up 
to have one introducer; the SECONDARY set, another.  Thus, one identifier 
could have two different functions depending on the introducer preceding it. 
There is also no reason why the PRIMARY and SECONDARY introducers can not be 
identical, providing that the identifiers are different.  If the identifiers 
are the same, the PRIMARY function will be recognized. 
