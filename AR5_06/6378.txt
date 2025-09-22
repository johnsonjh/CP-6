Syntax: 
ADAPT [ source-file ] [ , update-file ] 
    [ { ON   }                                    ] 
    [ { OVER } [ script-file ] [ , listing-file ] ] [ ( options ) ] 
    [ { INTO }                                    ] 
    [ { TO   }                                    ] 
Parameters: 
source-file    specifies the file identifier of a dialog definition file. 
update-file    specifies the file identifier of a file containing source file 
updates. 
script-file    specifies the file identifier of the script file to be 
generated. 
listing-file    specifies the file identifier of the destination for the 
compilation listing. 
options    enter: HELP (ADAPT) COMPILER_OPTIONS. 
Description: 
The ADAPT compiler is a CP-6 program which accepts a file containing 
statements in the ADAPT language and produces a script file. 
Rules: 
1.  ON, OVER, INTO, or TO must be used, if either of the output files are 
    specified, to determine how to handle these files if they already exist. 
    In any case, an output file is created if it does not exist. 
2.  ON and TO specify that if the script-file or listing-file already exists, 
    an error is reported and compilation is aborted. 
3.  OVER specifies that if the script-file or listing-file already exists, the 
    existing file is to be overwritten. 
4.  INTO specifies that if the script-file or listing-file already exists, new 
    output is to be added to the existing file. 
    See HELP (ADAPT) COMPILER_OPTIONS for a list of compiler options. 
    See: HELP (ADAPT) COMPILER_OPTIONS option for a specific option. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
Syntax: 
A[BORT] 
Description: 
The ABORT statement triggers the current abort action. 
Rules: 
1.  The ABORT statement transfers control to the abort action, as defined by 
    the ON ABORT statement.  If the current frame has no abort action, it is 
    terminated immediately and the abort action for the prior frame is 
    entered.  If that frame also has no abort action, it is also terminated, 
    an so on.  If the top frame for the calling program is reached without 
    finding an abort action, the top frame is repeated if it is defined as a 
    repeating frame; otherwise, it is exited. 
2.  An ABORT statement in an ON ABORT action is treated as if the frame has no 
    abort action.  In other words, it triggers the abort action of the next 
    higher level frame that has one. 
00001
The abort action assumes control when the frame is aborted.  A request to 
repeat the frame transfers control to the start action.  A request to exit the 
frame transfers control to the exit action.  Normal completion is treated as a 
request to repeat if the frame is defined as a repeating frame; otherwise, it 
is treated as a request to exit. 
If a frame that has no abort action is aborted, the frame is terminated 
immediately, as are all prior frames that have no abort action, until the top 
frame for the calling program is reached.  If no frame for the program has an 
abort action, the top frame is reentered at the start action if it is defined 
as a repeating frame; otherwise, it is terminated. 
    The dialog designer can define sequences of statements for the dialog 
    manager to execute at particular points during execution of a frame. 
    These statement sequences are referred to as actions. 
    A frame can define an action to be executed just after the frame is 
    entered.  It can also define an action to be executed just before the 
    frame exits.  A repeating frame can define actions to be executed at the 
    start and end of each repetition.  The general flow of control through a 
    frame therefore consists of the following steps: 
1.  If the frame specifies a program invocation command, the specified program 
    is started. 
2.  The frame entry action is executed. 
3.  The repetition start action is executed. 
4.  For a menu frame, the menu is displayed and the user is prompted to select 
    a choice.  Then the choice start action is executed, followed by the 
    action for the selected choice. 
5.  The repetition end action is executed.  For a repeating frame, control is 
    then passed back to step 3.  Otherwise, control passes to step 6. 
6.  The frame exit action is executed and the frame terminates. 
There can also be special actions to be executed when the <BREAK> key is 
pressed and when a frame is aborted.  The following subsections describe each 
type of action in more detail.  If an action is not present for a frame, 
processing proceeds as if an action completed normally. 

Syntax: 
{ { EM[PHASIS]          }              } 
{ { ER[ROR]             }              } 
{ { H[IDDEN] A[BSTRACT] }              } 
{ { INP[UT]             }              } 
{ { NO[NE]              }              } 
{ { NU[LL]              }              } 
{ { O[UTPUT]            }              } 
{ { W[ARNING]           }              } 
{                                      } 
{ INI[TIAL]                            } 
{                                      } 
{ { D[ECREATED] [ INT[ENSITY] ]  }     } 
{ { B[LINK]                      }     } 
{ { F[AST] [ B[LINK] ]           }     } 
{ { H[IDDEN]                     }     } 
{ { INC[REASED] [ INT[ENSITY] ]  } ... } 
{ { INT[ENSITY]                  }     } 
{ { R[EVERSE] [ V[IDEO] ]        }     } 
{ { S[LOW] [ B[LINK] ]           }     } 
{ { U[NDERSCORE]                 }     } 
Description: 
Attributes specify special display attributes for fields in forms.  Initial 
attributes are specified on the statements that declare the fields. 
Attributes can be changed by the SET ATTRIBUTES statement. 
Rules: 
1.  Attributes can be specified either abstractly or explicitly.  Abstract 
    attributes specify generic attribute types that are interpreted in a 
    manner appropriate to the user's terminal.  Explicit attributes specify 
    exactly which display attributes are to be applied. 
2.  Only one abstract attribute can be specified.  Possible attributes are 
    EMPHASIS, HIDDEN ABSTRACT, INPUT, NONE, NULL, OUTPUT, and WARNING.  Note 
    that INPUT and OUTPUT do not change a field's type; they allow all fields 
    of a type to be displayed the same way. 
3.  Any combination of explicit attributes can be specified.  Possible 
    attributes are: DECREASED INTENSITY, FAST BLINK, HIDDEN, INCREASED 
    INTENSITY, REVERSE VIDEO, SLOW BLINK, and UNDERSCORE.  In addition, BLINK 
    can be specified to mean whichever blink speed (FAST or SLOW) the terminal 
    supports.  Similarly, INTENSITY can be used to specify whichever alternate 
    intensity (INCREASED or DECREASED) the terminal supports.  Use of explicit 
    attributes not supported by the user's terminal is ignored.  The 
    combination of attributes specified on a SET ATTRIBUTES statement replaces 
    whatever prior attributes were applied to the field or fields. 
4.  An attribute of INITIAL is accepted only on a SET ATTRIBUTE statement.  It 
    resets fields' attributes to those specified on the corresponding field 
    definition statements.  Like abstract attributes, it must be specified 
    alone. 
00001
00002
BREAK
Syntax: 
BE[GIN] 
Description: 
The BEGIN statement begins a statement block.  This is a group of statements 
that are executed as a unit. 
Rules: 
1.  The statements following the BEGIN statement contstitute a statement 
    block.  This block must be terminated by an END statement. 
2.  Statement blocks are most useful in compound statements (IF/THEN/ELSE, 
    WHILE, and UNTIL), but can be used anywhere a single statement appears. 
3.  Statement blocks can be contained in other statement blocks.  Blocks can 
    be nested to any depth. 
4.  Statement blocks cannot span actions.  In other words, a statement that 
    begins a new action (CHOICE, FIELD, etc.) cannot appear within a statement 
    block. 
00001
00002
Syntax: 
BR[EAK] 
Description: 
The BREAK statement simulates the user pressing the <BREAK> key. 
Rules: 
1.  If a BREAK statement is executed, or if the user presses the <BREAK> key, 
    the current break action is entered. 
2.  The break action is established by an ON BREAK statement.  If the current 
    frame has no break action, it is terminated immediately and the break 
    action for the prior frame is entered.  If that frame also has no break 
    action, it is also terminated, and so on.  If the top frame for the 
    calling program is reached without finding a break action, the top frame 
    is repeated if it is defined as a repeating frame; otherwise, it is 
    exited. 
3.  A BREAK statement on a break action is treated as if the frame has no 
    break action.  In other words, it triggers the break action of the next 
    higher level frame that has one. 
4.  The contents of the input buffer are cleared by a BREAK statement or the 
    user pressing <BREAK>. 
00001
The break action assumes control when the user presses the <BREAK> key while 
the dialog manager is running.  A request to repeat the frame transfers 
control to the start action.  A request to exit the frame transfers control to 
the exit action.  A normal completion is treated as a request to repeat if the 
frame is defined as a repeating frame, otherwise it is treated as a request to 
exit. 
If <BREAK> is pressed when a frame that has no break action is active, the 
frame is terminated immediately, as are all prior frames that have no break 
action.  If no frame for the calling program has a break action, the top frame 
for the program is reentered at the start action if it is defined as a 
repeating frame; otherwise, it is exited. 
If <BREAK> is pressed when the dialog manager is not in control (i.e., when 
the program running under the dialog is executing), the normal break handling 
for the running program is invoked.  In general, the only time <BREAK> can be 
reliably expected to trigger the dialog break action is when the terminal is 
hanging on a dialog prompt. 
FUNCTIONS
CHOICE
o   The syntax for the ENTER Program has been revised. 
o   Rule number 3 of the ENTER Program has been modified to discuss use of 
    'initial-input' in the ENTER Program syntax. 
o   Under Rule 5 of the FORM Statement and Rule 6 of the MENU Statement, 
    instructions are given on how to ensure you are notified of an overwitten 
    MAIN frame (when compiling) using the WARN option. 
o   A sentence has been added to Rule 4 of 'Expressions' to give the allowable 
    range for numeric results. 
o   Under 'Constants', the range for numbers has been added. 
Syntax: 
         { C[OLUMN] [ IS | = ] position-option                 } 
         { EL[SE]                                              } 
         { EN[D]                                               } 
         { ENT[ER] { [script-fid,] frame-name }                } 
         {         { script-fid               }                } 
CH[OICE] { NA[ME] [ IS | = ] choice-name ...                   } ... 
         { NUL[L]                                              } 
         { NUM[BER] [ IS | = ] number                          } 
         { P[ROMPT] [ IS | = ] { choice-description | N[ONE] } } 
         { R[OW] [ IS | = ] position-option                    } 
Parameters: 
position-option    enter: HELP (ADAPT) POSITION_OPTIONS 
script-fid    specifies the file identifier for a dialog script file. 
frame-name    specifies the name of a frame. 
choice-name    specifies an alphanumeric string or a quoted string of up to 30 
characters. 
number    specifies a number between 1 and 99. 
choice-description    specifies a quoted string. 
Description: 
The CHOICE statement defines one of the choices that can be selected within a 
menu frame. 
Rules: 
1.  The CHOICE statement is allowed only within a menu frame. 
2.  Choices in a menu are numbered automatically in sequence according to 
    their position in the template, unless numbering is suppressed by the MENU 
    statement.  The choice number can be entered by the user to make a 
    selection.  A period and a blank (. ) are inserted automatically after the 
    number in the prompt that appears in the menu template. 
3.  The COLUMN and ROW clauses specify placement of the choice within the 
    frame.  If either is omitted, the default is taken from the MENU 
    statement.  The options allowed are described under HELP (ADAPT) 
    POSITION_OPTIONS.  Choices do not have to be specified in order according 
    to their position, but they cannot overlap. 
4.  ELSE defines an action that is executed when an undefined choice is 
    selected.  If there is no ELSE choice for a menu, a diagnostic is issued 
    and the menu prompt is repeated if the user's selection does not match one 
    of the choices. 
5.  END can be specified to indicate that the choice is to be selected if 
    E[ND] or any of the standard CP-6 synonyms (Q[UIT], EX[IT], X[IT]) is 
    entered. 
6.  The ENTER clause specifies the name of a frame to be entered to process 
    the choice.  The frame can be specified by giving the script-file fid or 
    the frame-name or both, according to the rules for the ENTER statement. 
    If the CHOICE statement is followed by executable statements, they are 
    executed on return from the entered frame. 
7.  The NAME clause specifies a name that can be used to select this choice. 
    If choice numbering is suppressed by the MENU statement, NAME is required 
    on all choices, with the exception of NULL and ELSE choices.  All choice 
    names in a menu must be unique.  A list of names can be specified to 
    define synonymous choice names.  If multiple names are defined, the list 
    must be enclosed in parentheses.  Only the first name from the list 
    appears in the menu. 
    Choice names can contain a slash (/) to indicate the shortest possible 
    abbreviation.  The shortest abbreviations of each name within a menu must 
    be unique.  The slash is removed from the name when it is displayed in the 
    menu.  If the MENU statement specifies automatic abbreviation, a slash in 
    the choice-name can be used to specify an abbreviation other than the 
    minimal one.  A slash at the end of the choice-name specifies that no 
    abbreviation is allowed. 
8.  NULL defines an action that is executed when a null (all blank) response 
    it entered.  If there is no NULL choice for a menu, a null response is 
    processed according to the rule for the ELSE choice. 
9.  The NUMBER clause can be used to force gaps in menu numbers.  If present, 
    the choice is given the specified number.  Subsequent choices are numbered 
    sequentially from that number.  The number must exceed the number of all 
    prior choices.  This clause does not apply to menus that suppress 
    numbering. 
10. The PROMPT clause specifies a choice description that is displayed 
    following the number and name.  PROMPT NONE specifies that the choice is 
    not to appear in the menu.  A choice name (or END or NULL) must be 
    specified with PROMPT NONE so that the choice can be selected.  The PROMPT 
    clause is required. 
11. The text that appears in the menu to describe the choice consists of the 
    choice number, followed by the name, followed by the choice description 
    supplied by the PROMPT clause.  Appropriate punctuation is inserted 
    depending on the combination of options provided to define the choice. 
    The permissible combinations of options are: 
        nn. name - description 
        nn. name 
        nn. description 
        name - description 
    Choice numbers are assigned in sequence by position in the menu, not in 
    the order the choices are defined in the source file. 
12. Executable statements following the CHOICE statement constitute the action 
    that is taken when the choice is selected.  The choice action ends with 
    the first following nonexecutable statement. 
Examples: 
CHOICE NAME IS REN/AME, PROMPT IS 'Change a name' 
defines a choice that can be selected by entering the keyword RENAME, which 
can be abbreviated to RENAM, RENA, or REN.  The choice is shown in the menu as 
follows (assuming choice numbering is disabled): 
    RENAME - Change a name 
CHOICE END NULL PROMPT(NONE) 
defines a choice that can be selected by entering the keyword END or any of 
the standard synonyms and abbreviations, or by just pressing <CR>.  Nothing 
appears in the menu to indicate that this choice is available. 
00002
00001
A menu frame has a choice action for each choice defined by the menu.  The 
action for the selected choice is entered after the choice start action.  A 
request to repeat the frame transfers control back to the start action.  A 
request to exit the frame transfers control directly to the exit action. 
Normal completion transfers control to the end action. 
The choice start action applies only to menu frames.  It is executed after the 
user has selected a valid choice, but before the action for the selected 
choice begins.  A request to repeat the frame transfers control back to the 
start action.  A request to exit the frame transfer control directly to the 
exit action.  Normal completion transfers control to the action for the 
selected choice. 
Syntax: 
        { IN[PUT]   } 
        { O[UTPUT   } 
CLE[AR] { IW[INDOW] } 
        { W[INDOW]  } 
        { UCxx      } 
Description: 
The CLEAR statement clears the contents of screen windows and internal 
buffers. 
Rules: 
1.  CLEAR INPUT discards any characters in the dialog input buffer. 
2.  CLEAR OUTPUT discards any partial command line that has been built in the 
    command buffer. 
3.  CLEAR IWINDOW clears the user interaction screen window for the current 
    frame. 
4.  CLEAR WINDOW clears the frame window (menu or form) for the current frame. 
    If the current frame is a procedure frame, which has no frame window, the 
    one for the invoking frame is cleared. 
5.  CLEAR UCxx clears the window for the specified logical device stream. 
    UCxx can be either an explicit stream number (e.g., UC02) or a symbolic 
    stream name (e.g., UCAA).  In either case, the stream must be one that is 
    known to the dialog.  See HELP (ADAPT) WINDOW_OPTIONS for more information 
    about stream names and numbers. 
00001
Syntax: 
CLO[SE]  [ #file-number ] 
Parameters: 
file-number    specifies an internal file number from 1 to 9. 
Description: 
The CLOSE statement closes a disk file. 
Rules: 
1.  The file-number should be the same as the number specified when the file 
    was opened.  If specified, the file-number must be prefixed with a pound 
    sign (#).  If omitted, #1 is assumed. 
2.  All files are initially closed.  Any files left open when the dialog 
    terminates are closed automatically. 
3.  If the close is unsuccessful for any reason, the appropriate CP-6 error 
    code is saved where it can be accessed by the $ERROR function.  If the 
    close is successful, $ERROR is set to zero. 
00001
The command buffer is used to hold commands being built to send to the calling 
program.  It can also be used for commands to be sent to the system command 
processor (IBEX).  A command can be built and sent for execution in a single 
statement.  It is also possible to build a single command piece by piece, and 
send it for execution after it is completely assembled.  The command buffer is 
cleared after each command is sent. 
    A number of standard CP-6 compiler options can be specified to affect the 
    operation of the ADAPT compiler.  The options supported by ADAPT are 
    listed below. 
    The options are:  BC, LPS, NLPS, LS, NLS, LU, NLU, OPTUI, OU, NOU, SO, 
    NSO, SRCH, UI, NUI, WARN, NWARN. 
    To see all the options, enter: ??  To see one option at a time, enter: ? 
    To see a specific option, enter: HELP (ADAPT) COMPILER_OPTIONS option 
    Note:  In HELP the option name can be abbreviated to the minimum number of 
    characters needed to identify the option uniquely. 
  Option     Description 
  BC ( list ) 
             BC allows selective compilation of frames in source files that 
             contain multiple frames.  The list consists of either the word 
             ALL or one to ten frame numbers separated by commas.  ALL 
             specifies that all frames in the source file are to be compiled. 
             A list of numbers specifies that only the frames included in the 
             list are to be compiled.  The default is ALL. 
  { LPS | NLPS } 
             LPS specifies that the output of the preprocessor is to be 
             listed.  NLPS suppresses the preprocessor output listing.  The 
             default is NLPS. 
  { LS | NLS } 
             LS specifies that compilation listing is to be written through 
             M$LO.  NLS suppresses the compilation listing.  The default is 
             LS. 
  { LU | NLU } 
             LU causes the contents of the update-file to be written through 
             M$LO before any listing generated for the LS option.  NLU 
             suppresses the update-file listing.  The default is NLU. 
  OPTUI 
             OPTUI specifies that the UI and LU options are to be applied only 
             if the update-file actually exists.  If OPTUI is not specified, 
             an error is reported and compilation is aborted if the 
             update-file is specified and the file does not exist. 
  { OU | NOU } 
             OU specifies that the script-file is to be written through M$OU. 
             NOU specifies that no script file is to be written.  The default 
             is OU. 
  { SO | NSO } 
             SO specifies that a new dialog definition file with merged 
             updates is to be written through M$SO.  NSO suppresses creation 
             of a new dialog definition file.  NSO is the default. 
  SRCH ( list ) 
             SRCH specifies accounts and packsets to be searched when an 
             INCLUDE statement specifies a file by the file name only.  The 
             accounts and packsets in the list are searched in the order 
             specified.  List entries must be separated by commas.  Account 
             names in the list must have a leading period (.). 
  { UI | NUI } 
             UI specifies that source file updates are to be read through 
             M$UI.  NUI specifies that no source file updates are to be read. 
             The default is UI if the update-file is specified, and NUI if the 
             update-file is omitted. 
  { WA[RN] | NWA[RN] } 
             WARN specifies that warning messages are to be generated.  NWARN 
             suppresses warning message generation.  The default is NWARN. 
00001
00002
00003
00004
00002
00003
00004
00006
00007
00009
00010
00005
00006
00007
00008
00009
00010
COMPILER_OPTIONS
Syntax: 
CO[NSTANT] [ field-name = ] string 
    [ { A[TTRIBUTES | ATTRS } [ IS | ARE | = ] attributes  ] 
    [ C[OLUMN] [ IS | = ] position-option                  ] 
    [ I[NITIALIZE] [ WITH | IS | = ] string                ] ... 
    [ J[USTIFY] [ IS | = ] { L[EFT] | C[ENTER] | R[IGHT] } ] 
    [ L[ENGTH] [ IS | = ] length                           ] 
    [ R[OW] [ IS | = ] position-option                     ] 
Parameters: 
field-name    specifies the name of the text field. 
string    is a quoted string. 
attribute    enter: HELP (ADAPT) ATTRIBUTE 
position-option    enter: HELP (ADAPT) POSITION_OPTIONS 
length    specifies an unsigned integer. 
Description: 
The CONSTANT statement defines constant text to appear in a form or menu. 
Rules: 
1.  The CONSTANT statement is allowed only in menu and form frames. 
2.  The field-name is optional.  It specifies the name that can be used to 
    refer to the text field.  All field-names in a frame must be unique.  A 
    constant field name can only be referenced on a SET ATTRIBUTES statement. 
3.  The value of the constant must be specified by a quoted string.  The 
    string can either be specified just after the field name, if any, or by 
    the INITIALIZE clause. 
4.  The ATTRIBUTES option is meaningful only in form frames.  It defines the 
    default display attributes to be applied to the constant field.  If the 
    field's attributes are altered by a SET ATTRIBUTES statement, they are 
    reset to the default whenever the frame's start action is executed. 
5.  The COLUMN and ROW clauses specify placement of the text field within the 
    frame.  The options allowed are described under HELP (ADAPT) 
    POSITION_OPTIONS. 
6.  The JUSTIFY clause specifies how to truncate or pad field values.  LEFT 
    specifies truncation and padding at the right end of the field.  RIGHT 
    specifies truncation and padding at the left end of the field.  CENTER 
    specifies truncation at the right and padding on both sides of the field. 
    The default is LEFT. 
7.  The LENGTH clause specifies the maximum number of characters in the text. 
    If the constant contains fewer characters than specified by the length, it 
    is padded with blanks.  If it contains more characters than are allowed, 
    it is truncated.  LENGTH is most useful in conjunction with JUSTIFY to 
    center or right justify a constant without having to count spaces. 
8.  The CONSTANT statement does not have an associated action.  It must be 
    followed by another nonexecutable statement. 
00002
00001
00003
    A constant is a value that never changes.  ADAPT supports four types of 
    constants: character strings, octal strings, numbers, and control 
    character mnemonics. 
    A character string is a sequence of up to 127 characters enclosed in 
    single quote marks (').  A pair of single quotes ('') must be used to 
    represent a single quote within the string. 
    An octal string is a sequence of octal digits enclosed in single quotes 
    and preceded with the letter "O".  It must contain a multiple of three 
    digits, where each triad represents the corresponding 9-bit character 
    code. 
    A number is a sequence of decimal digits.  It can be prefixed with a plus 
    sign (+) or minus sign (-).  If no sign appears, plus is assumed.  Numbers 
    must be in the range -131072 to 131071. 
    A control character mnemonic is the name of an ASCII control character 
    enclosed in <angle brackets>.  The permissible control character mnemonics 
    and their decimal values are: 
        NULL  0     SOH   1     STX   2     ETX   3 
        EOT   4     ENQ   5     ACK   6     BEL   7 
        BS    8     HT    9     LF   10     VT   11 
        FF   12     CR   13     SO   14     SI   15 
        DLE  16     DC1  17     DC2  18     DC3  19 
        DC4  20     NAK  21     SYN  22     ETB  23 
        CAN  24     EM   25     SUB  26     ESC  27 
        FS   28     GS   29     RS   30     US   31 
        DEL  127 
    A special form of control code mnemonic converts a printable ASCII 
    character to the corresponding control character: 
        <CNTL-x>        where x is an alphabetic character 
    The specified character is converted to a control character by taking its 
    value modulus 32. 
DATE_TIME_FORMATS
ADAPT supports several different formats for dates and time of day.  Each 
format is referred to by mnemonic name. Format names are used in functions 
that return the current date and time.  They are also used as validation 
options to ensure that a date or time is properly formatted.  The following 
table shows the different formats and the context in which they apply. 
 +--------------------------------------------------------------------+ 
 |         |            | Validate | Validate |        |      |       | 
 |  Name   |   Format   |   Date   |   Time   | $Date  | $Day | $Time | 
 |====================================================================| 
 | ANS     | YYMMDD     |    X     |          |   X    |      |       | 
 |         |------------+----------+----------+--------+------+-------| 
 |         | HHMMSSTT   |          |    X     |        |      |   X   | 
 |         | HHMMSS     |          |    X     |        |      |       | 
 |         | HHMM       |          |    X     |        |      |       | 
 |---------+------------+----------+----------+--------+------+-------| 
 | DAY     | DAY        |          |          |        |  X   |       | 
 |---------+------------+----------+----------+--------+------+-------| 
 | EXT     | MON DD 'YY |          |          |   X    |      |       | 
 |---------+------------+----------+----------+--------+------+-------| 
 | JULIAN  | YYDDD      |          |          |   X    |      |       | 
 |---------+------------+----------+----------+--------+------+-------| 
 | LOCAL   | MM/DD/YY   |    X     |          |   X    |      |       | 
 |         |------------+----------+----------+--------+------+-------| 
 |         | HH:MM:SS:TT|          |    X     |        |      |   X   | 
 |         | HH:MM:SS   |          |    X     |        |      |       | 
 |         | HH:MM      |          |    X     |        |      |       | 
 +--------------------------------------------------------------------+ 
Syntax: 
DE[LETE] 
    { [ #file-number ] K[EY] [ IS | = ] expression [[ , ] expression ] } 
    { F[ILE] [ IS | = ] expression                                     } 
Parameters: 
file-number    specifies an internal file number from 1 to 9. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The DELETE statement deletes a record or group of records from a disk file. 
It can also delete entire files. 
Rules: 
1.  The file-number should be the same as the number specified when the file 
    was opened.  An error occurs if the file is not open.  If specified, the 
    file-number must be prefixed with a pound sign (#).  If omitted, #1 is 
    assumed. 
2.  The KEY clause specifies the record or records to delete.  If a single 
    expression is specified, only one record is deleted.  If the expression 
    evaluates to a string, the result is the key of the record to delete.  If 
    the expression evaluates to a number, it specifies the record number 
    within the file of the record to delete.  If a pair of expressions are 
    specified, a range of records is deleted.  The string result of the first 
    expression supplies the starting key of the range; the string result of 
    the second expression supplies the key of the last record in the range. 
    Deletion by range of record numbers is not supported. 
    Deletion by key applies only to KEYED files.  Deletion by record number is 
    allowed on both KEYED and CONSEC files. 
3.  The FILE option specifies that the entire file is to be deleted.  The 
    string value of the expression provides the fid of the file to delete. 
    The file must not be open. 
4.  If the operation is unsuccessful for any reason, the appropriate CP-6 
    error code is saved where it can be accessed by the $ERROR function.  If 
    the operation is successful, $ERROR is set to zero. 
Examples: 
DELETE FILE '*TEMP' 
deletes a file with a fid of *TEMP. 
DELETE#3 KEY = 'ABC' 
deletes the record from file number 3 that has a key of ABC. 
DELETE KEY('ABC'||<NULL>, 'ABC'||<DEL>) 
deletes all records from file number 1 (the default) with an ASCII key 
beginning with ABC. 
00002
00001
DISPLAY
The dialog manager executes compiled dialog scripts.  A dialog can be put into 
execution in one of three ways: 
o   The ENTER program can be invoked from IBEX. 
o   The ENTER command can be issued from within a program that can run under a 
    dialog. 
o   An application program can call the dialog manager library services. 
For details, enter: HELP (ADAPT) ENTER_PROGRAM 
                    HELP (ADAPT) ENTER_COMMAND 
Syntax: 
DI[SPLAY] expression [ [WITH] VFC ] 
Parameters: 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The DISPLAY statement writes text to the user's terminal.  It is used 
typically to issue error diagnostics and other messages. 
Rules: 
1.  The string result of the expression is written to the interaction window. 
2.  Each DISPLAY statement writes one line of text.  However, if the size of 
    the line exceeds the window width, the line is wrapped. 
3.  If WITH VFC (vertical format control) is specified, the first character of 
    the line is used as the VFC when the line is written.  Otherwise, the line 
    is written using the default VFC (Transition-1). 
4.  The DISPLAY $ERROR statement is a special case.  Instead of the current 
    error code, which is what the $ERROR function normally returns, the 
    corresponding error message is displayed.  If $ERROR is zero, nothing is 
    output. 
00001
Syntax: 
DO { expression | / | \ } ,... 
Parameters: 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The DO statement builds program invocation command lines and submits them to 
the system command processor (IBEX). 
Rules: 
1.  The expressions are evaluated in the order specified.  If more than one 
    expression appears, a comma is required between each pair of expressions. 
    The string result of each expression is appended to the current command 
    buffer. 
2.  A slash (/) can be used within the list to submit the current contents of 
    the command buffer to IBEX before processing the remaining expressions. 
    This makes it possible to submit several commands with a single DO 
    statement. 
3.  The command buffer is normally submitted to the system command processor 
    (IBEX) after all expressions have been evaluated.  A backslash (\) can be 
    used as the last item in the expression list to inhibit this action.  This 
    makes it possible to construct a single command with several DO 
    statements. 
4.  When a command is submitted to IBEX, script execution does not continue 
    until the command or invoked program terminates.  The command buffer is 
    cleared before continuing. 
5.  If the invoked program or IBEX command does not complete normally, the 
    error code returned can be examined via the $ERROR function.  $ERROR is 
    set to zero on normal completion. 
Examples: 
DO 'SET M$DO *DO' 
issues an IBEX command to direct subsequent output through M$DO to the *DO 
temporary file. 
DO 'RESET F$105', /, 'RESET F$106' 
issues two IBEX commands.  The first resets the assignment for the F$105 DCB; 
the second resets F$106. 
DO 'C '||FILENAME||' TO LP' 
issues a command to copy the file whose fid is contained in the FILENAME 
variable to the lineprinter. 
DO 'L', \ IF WITH_ATTRIBUTES THEN DO '(A)', \ DO ' XYZ?' 
issues the command L(A) XYZ? if the variable WITH_ATTRIBUTES is true; 
otherwise, issues the command L XYZ?.  Note the use of backslashes (\) to hold 
the partially built command in the command buffer. 
00002
00001
ENTER
Syntax: 
END 
Description: 
The END statement terminates a statement block that was started by a BEGIN 
statement. 
Rules: 
1.  Every BEGIN statement must have a corresponding END statement. 
2.  An END statement is matched with the most recent BEGIN statement for which 
    a corresponding END statement has not already been encountered. 
3.  A label on an END statement is treated as being within the block, after 
    the last statement in the block.  Thus, a GOTO statement that references 
    such a label on a block for a WHILE or UNTIL statement transfers control 
    to the point where the looping condition is about to be tested.  Going to 
    an END label on an IF or ELSE block is equivalent to a transfer to the 
    statement after the IF/THEN/ELSE structure. 
00001
00002
In a menu frame, the end action is executed after a choice action.  In a 
procedure frame, it is executed following the start action.  If the frame is 
to be repeated, control transfers back to the start action on completion. 
Otherwise, control transfers to the exit action. 
Syntax: 
ENT[ER] { [ script-file, ] frame-name } [ expression ] 
        { script-file                 } 
Parameters: 
script-file    specifies the file identifier for a dialog script file. 
frame-name    specifies the name of a frame. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The ENTER statement starts the next frame.  Control normally returns to the 
statement following ENTER when the invoked frame terminates. 
Rules: 
1.  If the script-file is specified, the frame must be in that file.  If the 
    script-file is omitted, the frame must be in the current script file.  The 
    script-file may be either a fid or an expression.  If a fid is specified, 
    it must contain the account name; a trailing period (.) is required if the 
    fid is to be obtained from the current account.  If an expression is 
    specified, it must be enclosed in parentheses. 
2.  The frame-name defines the frame to be entered.  It must be specified if 
    the script-file is omitted.  If the script-file is specified with no 
    frame-name, the MAIN frame in the script-file is started. 
3.  If an expression is specified, the string result is inserted at the 
    beginning of the input buffer before the new frame is started.  Once it is 
    in the input buffer, this text is processed just as if it has been entered 
    by the user, as described under HELP (ADAPT) PROMPTS.  It can supply 
    responses to any number of prompts.  If any of this text remains when the 
    new frame exits, it is deleted automatically. 
Examples: 
ENTER SUBFRAME 
invokes the frame named SUBFRAME in the current script file. 
ENTER MAIL_SCRIPT.COMMON 
invokes the main frame of the script file named MAIL_SCRIPT in the COMMON 
account. 
ENTER GET_NAME_DESC CUR_NAME || ';' CUR_DESC 
invokes the frame named GET_NAME_DESC in the current script file and passes 
two input values to that frame via the input buffer.  The first $INPUT request 
in GET_NAME_DESC returns the value of the CUR_NAME variable, the second 
request returns the value of CUR_DESC.  If GET_NAME_DESC is invoked elsewhere 
with the statement: 
ENTER GET_NAME_DESC 
without passing any input values, the $INPUT requests result in prompts to the 
user to enter these values. 
ENTER ('SUB_SCRIPT,'||$FID_ACCT($SCRIPT)),SUB_FRAME 
invokes the frame named SUB_FRAME in the script file named SUB_SCRIPT that is 
in the same account as the current script file.  This is a convenient 
technique for keeping test and production versions of the same scripts in 
separate accounts. 
00002
00001
Syntax: 
ENTER [ script-fid ] [ , frame-name ] [ initial-input ] 
Parameters: 
script-fid    is the file identifier for the script to execute. 
frame-name    is the first frame of the script to execute. 
initial-input    supplies responses to the initial prompts for the dialog. 
Description: 
The ENTER command starts execution of a dialog for the current processor.  It 
can only be issued from within a processor that is capable of running under a 
dialog, and that accepts the ENTER command.  Most programs that get commands 
via XUG/XUR$GETCMD host library services do this.  The most notable exceptions 
are special shared processors (IBEX, DELTA, etc.). 
Rules: 
1.  The script-fid parameter specifies the file containing the compiled script 
    for the dialog to be executed.  The default is the current setting of the 
    ADAPT$SCRIPT DCB. 
2.  The frame-name parameter specifies the first frame of the script-fid to be 
    executed.  The default is the MAIN frame for the script. 
3.  The initial-input parameter can be used to presupply responses to the 
    initial prompts for the dialog.  The text supplied is put into the dialog 
    input buffer before the first frame is started.  The default is no initial 
    input text, which means that the user is prompted for all dialog inputs. 
    Either the script-fid or frame-name must be specified if initial-input is 
    provided. 
4.  The dialog is put into execution under the currently running program.  It 
    can issue IBEX commands and start programs by using the DO statement to 
    pass command lines to IBEX.  It can also execute ISSUE statements to pass 
    commands to be executed by the running program. 
5.  Terminal input is read through the DCB used by the running program for 
    command input.  Output to the interaction window is written through the 
    DCB used by the program for command output.  Any output written by the 
    program through this DCB appears in the current interaction window. 
00001
Syntax: 
!ENTER [ script-fid ] [ , frame-name ] [['('] initial-input [')']] 
Parameters: 
script-fid    is the file identifier for the script to execute. 
frame-name    is the first frame of the script to execute. 
initial-input    supplies responses to the initial prompts for the dialog. 
Description: 
The ENTER program starts execution of a dialog at the IBEX level.  It can be 
used to run dialogs that only issue IBEX commands, or to start a dialog that 
invokes and runs under another program.  It can also be used to test dialogs 
to be started by another program. 
Rules: 
1.  The script-fid parameter specifies the file containing the compiled script 
    for the dialog to be executed.  The default is the current setting of the 
    ADAPT$SCRIPT DCB.  If the script-fid does not specify an account, the file 
    of the specified name in :SYS is used if it exists; otherwise, the current 
    directory account is the default.  To ensure that the file in the current 
    account is used, a period (.) must follow the file name. 
2.  The frame-name parameter specifies the first frame of the script-fid to be 
    executed.  The default is the MAIN frame for the script. 
3.  The initial-input parameter can be used to presupply responses to the 
    initial prompts for the dialog.  The text supplied is put into the dialog 
    input buffer before the first frame is started.  The default is no initial 
    input text, which means that the user is prompted for all dialog inputs. 
    The initial-input can be optionally enclosed in parentheses.  Either the 
    script-fid or frame-name must be specified if initial-input is provided 
    and is not enclosed in parentheses. 
4.  The dialog is put into execution at the IBEX level.  It can issue IBEX 
    commands and start programs by using the DO statement to pass command 
    lines to IBEX.  If the dialog executes any ISSUE statements to pass 
    commands to the running program, the commands are echoed through M$LO. 
5.  If any frame of the script, including the top frame, is defined to be run 
    under another program (via the DO clause on the frame definition 
    statement), that frame and all frames it enters run under the specified 
    program, not at the IBEX level.  Dialogs running under another program 
    function as described under HELP (ADAPT) ENTER_COMMAND. 
6.  Terminal input for a dialog running at the IBEX level is read through 
    M$SI.  Output to the interaction window is written through M$LO. 
00001
The entry action is the first action executed when the frame is entered.  A 
request to repeat the frame reenters the entry action.  A request to exit the 
frame within an entry action does so without invoking any other actions. 
Normal completion of the entry action transfers control to the start action. 
Syntax: 
EX[IT] 
Description: 
The EXIT statement returns control to the frame that entered the current 
frame. 
Rules: 
1.  Reaching the end of a frame is treated as an implied EXIT statement if the 
    frame does not specify REPEAT. 
2.  Exiting the top frame of a dialog returns the terminal to normal 
    timesharing mode.  If dialog mode was entered within a program, the user 
    is left within that program.  If the dialog was started from IBEX, control 
    is returned to IBEX. 
3.  Exiting the top frame of a program that was started by the dialog manager 
    returns control to the dialog manager in the invoking program at the point 
    just after the ENTER statement that started the new program. 
4.  If the frame has an ON EXIT action, it is normally executed before the 
    frame terminates.  However, an EXIT statement in an ON ENTRY action 
    bypasses any ON EXIT action. 
5.  An EXIT statement in an ON EXIT action is treated as a GO statement. 
00001
The exit action assumes control when the frame is exited from a start, choice 
start, choice, or end action.  A request to repeat the frame from within the 
exit action transfers control back to the start action.  Otherwise, the frame 
is terminated when the exit action completes. 
Syntax: 
          { constant       } 
[ unary ] { symbol-name    } [ operator expression ] 
          { function       } 
          { ( expression ) } 
Parameters: 
unary    specifies an arithmetic or logical unary operator. 
        The arithmetic unary operators are: 
            +               identity 
            -               negation 
        The logical unary operator is: 
            ~ or NOT        logical reversal 
constant    enter: HELP (ADAPT) CONSTANTS 
symbol-name    enter: HELP (ADAPT) SYMBOL_NAMES 
function    enter: HELP (ADAPT) FUNCTIONS 
expression    specifies another expression.  Expressions can be nested to any 
    depth. 
operator    specifies an arithmetic, string, comparison, or logical operator. 
        The arithmetic operators are: 
            +               addition 
            -               subtraction 
            *               multiplication 
            /               division 
        The string operator is: 
            || or !!        concatenation 
        The comparison operators are: 
            EQ or =         equal 
            NE or ~= or <>  not equal 
            GT or >         greater than 
            LT or <         less than 
            GE or >=        greater than or equal 
            LE or <=        less than or equal 
        The logical operators are: 
            AND or &        logical and 
            OR  or | or !   logical or 
Description: 
Expressions specify computations to be performed. 
Rules: 
1.  Depending on the context, the result of an expression is treated as a 
    string, a number, or a truth value. 
2.  Arithmetic operators produce a numeric result.  The string operator 
    produces a string result.  Comparison and logical operators produce a 
    truth value.  If the result of the expression requires a different type 
    than the result of the last operation, it is converted to the proper type. 
3.  A string result is a string of between 0 and 511 ASCII characters. 
4.  A numeric result is a signed integer.  If a numeric result is used in a 
    string expression, the result is a decimal integer; leading zeros are 
    removed, and a leading minus sign (-) appears on negative values.  An 
    attempt to use a non-numeric value in a numeric expression results in an 
    error.  Numeric results can range from -34,359,738,368 to 34,359,738,367. 
5.  A truth value result is either true or false.  If a non-truth expression 
    is used where a truth value is required, the numeric result of the 
    expression is used to determine whether it is true or false.  A result not 
    equal to zero is true; otherwise, it is false. 
6.  A reference to an operand that has no value results in an empty string. 
    An empty string is a string of no characters, the number zero, or false, 
    depending on the type of value required. 
7.  Operators are applied in order of precedence.  Operations of the highest 
    precedence are done first.  Within a precedence level, operations are done 
    from left to right.  Parentheses can be used to force the enclosed 
    subexpression to be evaluated first. 
        Operator    Precedence      Operation 
        --------    ----------      --------------------- 
        unary +         8           identity 
        unary -         8           inversion 
            *           7           multiplication 
            /           7           division 
            +           6           addition 
            -           6           subtraction 
        || or !!        5           concatenation 
        =  or EQ        4           equal 
        ~= or NE        4           not equal 
        >  or GT        4           greater than 
        >= or GE        4           greater than or equal 
        <  or LT        4           less than 
        <= or LE        4           less than or equal 
        ~ or NOT        3           logical reversal 
        & or AND        2           logical and 
        | or OR or !    1           logical or 
00001
Syntax: 
FI[ELD] field-name [ ( length ) ] [ = expression ] 
    [ { A[TTRIBUTES | ATTRS } [ IS | ARE | = ] attributes  ] 
    [ C[OLUMN] [ IS | = ] position-option                  ] 
    [ ENT[ER] { [ script-file , ] frame-name }             ] 
    [         { script-file                  }             ] 
    [ I[NITIALIZE] [ WITH | IS | = ] expression            ] ... 
    [ J[USTIFY] [ IS | = ] { L[EFT] | C[ENTER] | R[IGHT] } ] 
    [ L[ENGTH] [ IS | = ] length                           ] 
    [ P[ROMPT] [ IS | = ] { field-prompt | N[ONE] }        ] 
    [ R[OW] [ IS | = ] position-option                     ] 
    [ V[ALIDATION] [ IS | = ] validation-option            ] 
Parameters: 
field-name    specifies the name of the text field. 
length    specifies an unsigned integer. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
attribute    enter: HELP (ADAPT) ATTRIBUTE 
script-file    specifies the file identifier for a dialog script file. 
frame-name    specifies the name of a frame. 
field-prompt    is a quoted string. 
position-option    enter: HELP (ADAPT) POSITION_OPTIONS 
validation-option    enter: HELP (ADAPT) VALIDATION_OPTIONS 
Description: 
The FIELD statement defines an I/O field to appear in a form.  It can also 
supply a constant to serve as the prompt for the field. 
Rules: 
1.  The TEXT statement is allowed only in form frames. 
2.  After a form has been input, all fields are processed in the order they 
    appear on the screen, from left to right, top to bottom.  Only fields 
    touched by the cursor during form input are processed, but those fields 
    are reprocessed even if their value was unchanged.  If the form is 
    reopened for input due to an error before all fields have been processed, 
    unprocessed fields are remembered for later processing even if the cursor 
    does not touch them again.  Processing a field involves checking any 
    validation criteria, entering any associated frame, and executing any 
    action that follows the FIELD statement. 
3.  The field-name is required.  It specifies the name that is used to refer 
    to the field.  All field-names in a frame must be unique. 
4.  If an expression is specified, the string result of the expression is used 
    to initialize the field.  Field values are reset just before start action 
    is executed.  Existing field values are retained when the form is repeated 
    with a REPEAT FORM statement.  If no initialization expression is 
    specified, the field is initialized to a null string.  The expression can 
    be specified in several ways, as shown in the syntax, but only one 
    expression is allowed. 
5.  The ATTRIBUTES option defines the default display attributes to be applied 
    to the field.  If the statement also defines the prompt for the field, the 
    specified attributes also are also applied to the prompt.  If the field's 
    attributes are altered by a SET ATTRIBUTES statement, they are reset to 
    the default whenever the frame's start action is executed. 
6.  The COLUMN and ROW clauses specify placement of the text field within the 
    frame.  If either is omitted, the default is taken from the MENU 
    statement.  The options allowed are described under HELP (ADAPT) 
    POSITION_OPTIONS.  Fields do not have to be specified in order according 
    to their position, but they cannot overlap. 
7.  The ENTER clause specifies a frame to be entered after the field's value 
    has passed the validation criteria, if any.  The new value is pushed into 
    the input buffer, and can be obtained within the entered frame via the 
    $INPUT function.  Thus, this clause can be used to specify a common 
    procedure that performs additional field validation. 
8.  The JUSTIFY clause specifies how to truncate or pad displayed values. 
    LEFT specifies truncation and padding at the right end of the field. 
    RIGHT specifies truncation and padding at the left end of the field. 
    CENTER specifies truncation at the right and padding on both sides of the 
    field.  The default is LEFT.  JUSTIFY also determines how to strip leading 
    and trailing blanks from input values.  BLANKS are removed from input 
    values where they could have been added on output. 
9.  The length is required to specify the maximum number of characters in the 
    field.  The length can be enclosed in parentheses before the expression. 
    It can also be specified by the LENGTH clause. 
10. The PROMPT clause specifies the text to be used as a prompt for the field. 
    If present, the prompt precedes the field itself, with a blank between 
    them.  If no prompt is provided for a field in a form that specifies 
    PROMPTS=YES, the field name is used as the prompt by default.  PROMPT=NONE 
    can be specified to override this default. 
11. Executable statements following the FIELD statement constitute the action 
    that is taken when the field is processed.  The field action ends with the 
    first following nonexecutable statement. 
12. The VALIDATION clause specifies the validation criteria for the field.  If 
    a new field value does not meet the criteria specified, the appropriate 
    diagnostic is displayed in the interaction window and the form is repeated 
    with the cursor positioned to the failing field. 
00002
00001
00003
Each field in a form frame can have an associated action.  Field actions for 
all fields that were input are executed after form input is completed.  The 
actions are executed in the same order as the fields appear on the screen. 
Within a field action, statements that refer to form fields refer by default 
to the current field. 
A request to repeat the frame transfers control back to the start action.  A 
request to exit the frame transfers control directly to the exit action. 
Normal completion transfers control to the field action for the next input 
field.  After the action for the last field completes normally, control 
transfers to the end action. 
Syntax: 
FO[RM] [ IS | = ] form-name 
    [ C[OLUMN] [ IS | = ] position-option           ] 
    [ DO [ IS | = ] expression                      ] 
    [ ISS[UE] [ IS | = ] expression                 ] 
    [ IW[INDOW] [ IS | = ] window-options           ] 
    [ M[AIN]                                        ] 
    [ P[ROMPTS] [ [ IS | = ] { Y[ES] | N[O] } ]     ] ... 
    [ RE[PEAT] [ [ IS | = ] { Y[ES] | N[O] } ]      ] 
    [ R[OW] [ IS | = ] position-option              ] 
    [ T[ABS] [ IS | ARE | = ] { [ E[VERY] ] n } ... ] 
    [ UP[DATE] [ [ IS | = ] { Y[ES] | N[O] } ]      ] 
    [ W[INDOW] [ IS | = ] window-options            ] 
Parameters: 
form-name    specifies the name of the form. 
position-option    enter: HELP (ADAPT) POSITION_OPTIONS 
expression    enter: HELP (ADAPT) EXPRESSIONS 
window-options    enter: HELP (ADAPT) WINDOW_OPTIONS 
n    specifies an unsigned integer. 
Description: 
The FORM statement begins the definition of a form frame.  A form displays a 
formatted screen containing fields that the user can input or update. 
Rules: 
1.  The frame-name is required.  It specifies the name that is used to invoke 
    the menu.  All frames in a script file must have unique names. 
2.  The COLUMN and ROW clauses supply default positioning options for 
    CONSTANT, FIELD, and TEXT statements that omit these clauses.  Only 
    relative and tabular positions can be specified as defaults; absolute 
    positions are not allowed.  Enter: HELP (ADAPT) POSITION_OPTIONS for more 
    information. 
3.  Normally, the new frame runs under the same program as the invoking frame. 
    If the frame is to run under a different program, the DO or ISSUE clause 
    must be provided.  The DO clause specifies that the program is to be 
    invoked by the dialog manager.  The ISSUE clause should be used if the new 
    program is to be invoked by a command issued to the calling program.  The 
    string result of the expression is passed to IBEX or the calling program 
    in the same manner as for the DO and ISSUE statements. 
    The frame becomes the top level frame for the portion of the dialog that 
    is run under the new program.  Exiting the frame terminates the program. 
    Terminating the program runs the dialog down to the point where the frame 
    was entered. 
4.  The IWINDOW clause defines the interaction window for this frame.  If 
    omitted, the interaction window for the invoking frame is used. 
5.  The MAIN clause specifies that, if the script file is invoked without 
    specifying a frame name, this frame is to be used.  There can be only one 
    MAIN frame per script file.  Each MAIN frame definition overrides the 
    previous one.  To be notified of an overwritten MAIN frame, use the WARN 
    option when compiling. 
6.  The PROMPTS clause specifies whether or not form field names are to be 
    used as field prompts by default.  YES specifies that they are; NO 
    indicates they are not.  If prompts are requested, each field is preceded 
    by a constant consisting of the field name.  A single space separates the 
    prompt from the field.  If no prompt is requested, fields must be 
    preceding CONSTANT statements if they are to be identified by a prompt. 
7.  The REPEAT clause specifies whether or not the frame is to be executed 
    repetitively.  YES specifies that the frame is to be reexecuted until a 
    EXIT statement is encountered.  NO means that the frame is to be 
    terminated after it has been executed once.  The default is NO. 
8.  The TABS clause defines the position of tab stops.  These positions are 
    used by tabular positioning options for CONSTANT, FIELD, and TEXT 
    statements.  Specifying a list of numbers establishes tab stops at those 
    positions. 
    The EVERY option establishes tab stops at fixed intervals across the 
    window.  If the last or only TAB option is an EVERY option, tabs are set 
    the specified number of columns apart up to the width of the window.  If 
    an EVERY option is not the last in the list, it must be followed by a 
    number, not another EVERY option.  The number limits the range of columns 
    filled with tabs by the EVERY option; it also sets a tab at that position. 
9.  The UPDATE option specifies whether this form is can be updated or is for 
    display only.  The default is YES, which means that fields are to be open 
    for user input when the form is executed.  If NO is specified, the form is 
    displayed without being opened for input.  The SET UPDATE statement can 
    also be used within the frame to alter the update setting.  Note that if 
    update is turned off, it is the dialog designer's responsibility to issue 
    a prompt or force pagehalt or take some other action to stop processing so 
    that the user can view the displayed form.  Otherwise, the form will flash 
    up and be erased when the frame exits. 
10. The WINDOW clause defines the window to be used to display the menu for 
    the frame.  If omitted, the frame window for the invoking frame is used. 
    If that frame is a procedure, the most recent frame window in the 
    invocation path is used.  If there is no frame window defined for any 
    frame in the invocation path, the menu appears in the interaction window. 
    In that case, the interaction window is inaccessible within the frame. 
11. Executable statements following the FORM statement constitute the frame 
    start action.  This action ends with the first following nonexecutable 
    statement.  If no executable statements immediately follow the FORM 
    statement, a start action can appear later in the frame, following an ON 
    START statement. 
00002
00001
00003
    A form is a formatted display of information on the user's terminal.  It 
    contains both variable fields and constants.  Fields contain values 
    obtained or to be read by the dialog.  Constants supply titles, field 
    names, and other fixed information.  When a form is executed, the form is 
    displayed on the terminal, and the user is allowed to enter or change the 
    form's fields.  When user input is complete, new field values are read and 
    validated.  If a field is in error, a diagnostic is issued and the form is 
    reopened for input.  Each field can have an associated action that 
    performs special processing when that field is input. 
    Forms for dialogs can be defined by the FORGE processor.  FORGE is an 
    interactive, full screen facility to build and maintain form definitions. 
    It can generate files of ADAPT form definition statements that can be 
    included by the dialog source file.  See the FORGE Reference Manual 
    (HA13-01) for more information.  FORGE is not required to use forms in 
    dialogs, though.  Form definitions can also be coded directly into the 
    dialog source file. 
    The basic unit of an ADAPT script is a frame.  When the dialog manager 
    executes a compiled script, it does so frame by frame.  One frame, known 
    as the top level frame, is started when the dialog manager is first 
    entered.  The top level frame can enter other frames, each of which can 
    enter still other frames, and so on.  Frames can be nested as deeply as 
    necessary. 
    There are two types of frames: menu, and procedure.  A menu frame displays 
    a number of possible choices and asks the user to pick one of them.  A 
    procedure frame defines an action to be executed without any user 
    interaction. 
    A frame can be defined as a repeating frame.  When a frame that does not 
    repeat is entered, it is executed once and then exits.  When a repeating 
    frame is entered, it is executed over and over until it is specifically 
    told to exit. 
    The following subsections describe special handling for each type of 
    frame. 
    A number of built-in functions are available for use in expressions.  Some 
    functions provide specialized operations that augment the normal 
    operators.  Other functions return values that are maintained by the 
    system.  The functions available with ADAPT are listed below.  The 
    functions are:  $ABS, $ACCT, $CHOICE, $CMDVAR, $DATE, $DAY, $DIRECTORY, 
    $ERROR, $FID_ACCT, $FID_ASN, $FID_EXIST, $FID_NAME, $FID_NRECS, $FID_ORG, 
    $FID_PASS, $FID_PSN, $FID_RES, $FID_TYPE, $FID_WSN, $HSET, $IBUF, $IF, 
    $INDEX, $INPUT, $LENGTH, $LOWER, $MAXIMUM, $MINIMUM, $NULL, $QUOTE, $RU, 
    $SEARCH, $STEPCC, $SUBSTR, $SWITCH, $TIME, $UNAME, $UPPER, $VALIDATE, 
    $VERIFY.  To see all of the functions, enter: ??  To see one function at a 
    time, enter: ?  To see a specific function, enter: HELP (ADAPT) FUNCTIONS 
    function Note: The function name can be the entire name or an abbreviation 
    of the minimum number of characters needed to identify the name uniquely. 
  Option     Description 
  $AB[S] ( number ) 
             Returns the absolute value of the argument.  If the value is less 
             than zero, its complement is returned.  Otherwise, the value is 
             returned intact. 
  $AC[CT] 
             Returns the account portion of the current logon. 
  $CH[OICE] 
             Returns the response to the last prompt for a menu choice. 
  $CM[DVAR] ( name ) 
             Returns the value of the IBEX command variable of the name 
             specified.  If there is no such command variable, an empty string 
             is returned. 
  $DAT[E] [ ( { A[NS] | E[XT] | J[ULIAN] | L[OCAL] } ) ] 
             Returns the current date in the specified format.  Enter: HELP 
             (ADAPT) DATE_TIME_FORMATS for a description of the possible 
             formats.  The default format is ANS. 
  $DAY 
             Returns the current day of the week: SUN - SAT. 
  $DIR[ECTORY] 
             Returns the current file management directory account. 
  $E[RROR] 
             Returns the error code for the last statement or function 
             executed that can result in an error.  If the statement or 
             function executed without error, zero is returned.  Note that 
             only the code portion of the standard CP-6 error code word is 
             returned.  The FCG, severity, and monitor bit are inaccessible. 
  $FID_AC[CT] ( fid ) 
             Returns the account portion of the specified fid.  If the fid 
             does not specify an account, an empty string is returned. 
  $FID_AS[N] ( fid ) 
             Returns the assignment type of the specified fid.  The result is 
             a string containing one of the keywords that can be specified for 
             ASN on an M$OPEN pmme (DEVICE, FILE, TAPE, etc.). 
  $FID_E[XIST] ( fid ) 
             Returns a truth value indicating whether or not the specified fid 
             exists. 
  $FID_NA[ME] ( fid ) 
             Returns the name portion of the specified fid.  If the fid does 
             not specify a name, an empty string is returned. 
  $FID_NR[ECS] ( fid ) 
             Returns the number of records in the file for the specified fid. 
             If the fid does not specify a disk file or the file does not 
             exist, zero is returned. 
  $FID_O[RG] ( fid ) 
             Returns the organization of the specified fid.  The result is a 
             string containing one of the keywords that can be specified for 
             ORG on an M$OPEN pmme (KEYED, CONSEC, INDEXED, etc.).  If the fid 
             specifies a file that does not exist, an empty string is 
             returned. 
  $FID_PA[SS] ( fid ) 
             Returns the password portion of the specified fid.  If the fid 
             does not contain a password, an empty string is returned. 
  $FID_PS[N] ( fid ) 
             Returns the packset name portion of a disk fid, or the serial 
             number portion of a tape fid.  If the fid does not contain a 
             packset name or serial number, an empty string is returned. 
  $FID_R[ES] ( fid ) 
             Returns the resource name portion of a fid.  If the fid does not 
             contain a resource name, an empty string is returned. 
  $FID_T[YPE] ( fid ) 
             Returns the file type code of the file with the specified fid. 
             An empty string is returned if the fid does not specify a disk 
             file or if the file does not exist. 
  $FID_W[SN] ( fid ) 
             Returns the workstation portion of the specified fid.  If the fid 
             does not contain a workstation, an empty string is returned. 
  $HS[ET] 
             Returns the name of the home packset for the current user. 
  $IB[UF] 
             Returns the current contents of the dialog input buffer.  The 
             input buffer itself is not changed. 
  $IF ( condition , [ then ] [ , else ] ) 
             Returns either the result of the second or third argument, 
             depending on the value of the first argument.  The truth value of 
             the condition argument is derived.  If true, the then argument is 
             evaluated; otherwise, the else argument is evaluated.  If the 
             argument to be evaluated is omitted, the result is an empty 
             string. 
  $IND[EX] ( string , pattern [ , [ start ] [ , end ] ] ) 
             Returns the offset into the string argument of the first 
             character of the pattern argument.  If the pattern is not found 
             in the string, the result is the length of the string.  The first 
             character of the string has an offset of zero.  The start and end 
             arguments can be specified to limit the search to a portion of 
             the string. 
  $INP[UT] ( prompt [, [validation-options|TR] [, message-code ] ] ) 
             The $INPUT function requests data from the user.  The prompt 
             argument is used to prompt the user for the input.  If no prompt 
             is specified, a question mark (?) is used.  If the validation 
             options see HELP (ADAPT) VALIDATION_OPTIONS) specified are not 
             satisfied, the user is informed and the function is retried.  If 
             the user enters a question mark (?), the message with the 
             specified message-code is displayed from the message file 
             specified by the SET MSGFILE statement, and the function is 
             retried.  Note that the keyword TR[ANSPARENT] is allowed as an 
             alternative to validation-options as the second argument.  If 
             specified, the user's input is accepted as is, with no validation 
             or editing. 
  $LE[NGTH] ( string ) 
             Returns the number of characters in the string value of its 
             argument. 
  $LO[WER] ( string ) 
             Returns the string value of the argument with all upper-case 
             letters converted to lower-case. 
  $MA[XIMUM] ( value ... ) 
             Returns the largest of the arguments.  Any number of arguments 
             can be specified.  The first argument determines the type of 
             comparison (string or numeric) that is done. 
  $MI[NIMUM] ( value ... ) 
             Returns the smallest of the arguments.  Any number of arguments 
             can be specified.  The first argument determines the type of 
             comparison (string or numeric) that is done. 
  $N[ULL] 
             Returns an empty string. 
  $Q[UOTE] ( string [ , delimiter ] ) 
             Returns the string value of the first argument enclosed by 
             delimiters, with any delimiters within the string doubled.  If no 
             delimiter is specified, the default is a single quote mark ('). 
             The delimiter must be a single character. 
  $RU 
             Returns the fid of the currently executing run unit. 
  $SE[ARCH] ( string , pattern [ , [ start ] [ , end ] ] ) 
             Returns the offset into the string argument of the first 
             character that is present in the pattern argument.  If none of 
             the characters in the string are present in the pattern, the 
             result is the length of the string.  The first character in the 
             string has an offset of zero.  The start and end arguments can be 
             specified to limit the search to a portion of the string. 
  $ST[EPCC] 
             Returns the step condition code set by the last program executed. 
  $SU[BSTR] ( string [ , [ start ] [ , length ] ] ) 
             Returns a portion of the string argument.  The start argument 
             specifies the offset into the string of the first character to 
             return.  The length argument specifies the number of characters 
             to return.  If the start is omitted, zero is assumed.  If the 
             length is omitted, the length of the string minus the starting 
             offset is assumed. 
  $SW[ITCH] ( number ) 
             Returns the value of the specified switch.  The argument 
             specifies which switch to return; it must be between 0 and 35. 
             Switches can be turned on and off with the IBEX SWITCH command. 
  $TI[ME] [ ( { A[NS] | L[OCAL] } ) ] 
             Returns the current time of day in the specified format.  Enter: 
             HELP (ADAPT) DATE_TIME_FORMATS for a description of the possible 
             formats.  The default format is ANS. 
  $UN[AME] 
             Returns the user name portion of the current logon. 
  $UP[PER] ( string ) 
             Returns the string value of the argument with all lower-case 
             characters converted to upper-case. 
  $VA[LIDATE] ( expression , validation-options ) 
             Returns a truth value that indicates whether or not the first 
             argument passes the validation criteria specified by the second 
             argument.  If the validation fails, $ERROR is set to an 
             appropriate error code.  Enter: HELP (ADAPT) VALIDATION_OPTIONS 
             for more information. 
  $VE[RIFY] ( string , pattern [ , [ start ] [ , end ] ] ) 
             Returns the offset into the string argument of the first 
             character that is not present in the pattern argument.  If all of 
             the characters in the string are present in the pattern, the 
             result is the length of the string.  The first character in the 
             string has an offset of zero.  The start and end arguments can be 
             specified to limit the search to a portion of the string. 
00001
00002
00003
00004
00004
00005
00006
00007
00008
00009
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
00029
00030
00031
00032
00033
00034
00035
00036
00037
00038
00039
00040
Syntax: 
GL[OBAL] variable-name ... 
Parameters: 
variable-name    specifies the name of a variable. 
Description: 
The GLOBAL statement declares variables that have global scope.  Such 
variables can be used to pass parameters to other frames and to return values 
to an invoking frame. 
Rules: 
1.  A global variable is common to all frames that declare it as global for a 
    given invocation of the dialog manager.  The value of a global set in one 
    frame is available to any other frame that also declares it global. 
    Variables not declared as global are known only to the frame that uses 
    them, and are lost when the frame exits. 
2.  A frame can contain any number of GLOBAL statements.  Each statement 
    defines one or more global variables.  A variable should not be declared 
    as global more than once in a frame.  The declaration applies to only the 
    frame containing the GLOBAL statement.  It is recommended, but not 
    required, that the declaration appear before the first reference to the 
    named variable. 
3.  Unlike other nonexecutable statements, GLOBAL does not indicate the start 
    or end of an action.  It can appear anywhere, even in the middle of an 
    action. 
00001
Syntax: 
GO 
Description: 
The GO statement terminates the current action.  The dialog manager continues 
with frame execution, just as if the end of the action has been reached.  GO 
is implied after the last statement of an action. 
Syntax: 
GOT[O] label 
Parameter: 
label    specifies the label of a statement. 
Description: 
The GOTO statement transfers control to a statement with a given label. 
Rules: 
1.  Normally, statements of an action are executed in the order they appear in 
    the dialog definition file.  GOTO can be used to alter this order by 
    jumping to another point in the frame. 
2.  The specified label should be defined elsewhere within the same action or 
    in another action of the same type.  If the label is in another action, it 
    must be in the same frame.  Going to a label in a different type of action 
    is permitted, but the statements after the label are executed as if they 
    were part of the action that executed the GO TO.  Branching to a start 
    action from an end action, for example, does not implicitly repeat a 
    frame; it only executes statements coded in the start action as part of 
    the end action. 
00001
00002
A 
  ABBREVIATIONS Clause - 
      HELP MENU RULES: 
  Abort Action - 
      HELP ABORT_ACTION 
  ABORT Statement - 
      HELP ABORT 
  $ABS - 
      HELP FUNCTIONS $ABS 
  $ACCT - 
      HELP FUNCTIONS $ACCT 
  Actions - 
      HELP ACTIONS 
  ADAPT Compiler - 
      HELP ADAPT_COMPILER 
  Argument Handling Conventions - 
      HELP XT_ARGUMENTS 
  Attributes - 
      HELP ATTRIBUTES 
B 
  BC - 
      HELP COMPILER_OPTIONS BC 
  BEGIN Statement - 
      HELP BEGIN 
  Break Action - 
      HELP BREAK_ACTION 
  BREAK Statement - 
      HELP BREAK 
  BTMBRDR Option - 
      HELP WINDOW_OPTIONS RULES: 
C 
  $CHOICE - 
      HELP MENU RULES: 
      HELP FUNCTIONS $CHOICE 
  Choice Action - 
      HELP CHOICE_ACTION 
  Choice Start Action - 
      HELP CHOICE_START_ACTION 
  CHOICE Statement - 
      HELP CHOICE 
  CLEAR Statement - 
      HELP CLEAR 
  CLOSE Statement - 
      HELP CLOSE 
  $CMDVAR - 
      HELP FUNCTIONS $CNDVAR 
  COLUMN Clause - 
      HELP CHOICE RULES: 
      HELP CONSTANT RULES: 
      HELP FIELD RULES: 
      HELP FORM RULES: 
      HELP MENU RULES: 
      HELP TEXT RULES: 
  Command Buffer - 
      HELP COMMAND_BUFFER 
      HELP DO RULES: 
      HELP ISSUE DESCRIPTION: 
  Compiler Options - 
      HELP COMPILER_OPTIONS 
  CONSEC Option - 
      HELP OPEN RULES: 
  CONSTANT Statement - 
      HELP CONSTANT 
  Constants - 
      HELP CONSTANTS 
  CREATE Option - 
      HELP OPEN RULES: 
D 
  $DATE - 
      HELP FUNCTIONS $DATE 
  Date/Time Formats - 
      HELP DATE_TIME_FORMATS 
  $DAY - 
      HELP FUNCTIONS $DAY 
  DELETE Statement - 
      HELP DELETE 
  Dialog Manager - 
      HELP DIALOG_MANAGER 
  $DIRECTORY - 
      HELP FUNCTIONS $DIRECTORY 
  DISPLAY Statement - 
      HELP DISPLAY 
  DO Clause - 
      HELP FORM RULES: 
      HELP MENU RULES: 
  DO Statement - 
      HELP DO 
E 
  ECHO Option - 
      HELP SET RULES: 
  ELSE Clause - 
      HELP CHOICE RULES: 
  End Action - 
      HELP END_ACTION 
  END Clause - 
      HELP CHOICE RULES: 
  END Statement - 
      HELP END 
  ENTER Clause - 
      HELP CHOICE RULES: 
  ENTER Command - 
      HELP ENTER_COMMAND 
      HELP ENTER_COMMAND SYNTAX: 
  ENTER Program - 
      HELP ENTER_PROGRAM 
  ENTER Statement - 
      HELP ENTER 
  Entry Action - 
      HELP ENTRY_ACTION 
  $ERROR - 
      HELP CLOSE RULES: 
      HELP DELETE RULES: 
      HELP DISPLAY RULES: 
      HELP ISSUE RULES: 
      HELP OPEN RULES: 
      HELP READ RULES: 
      HELP WRITE RULES: 
      HELP FUNCTIONS $ERROR 
  Exit Action - 
      HELP EXIT_ACTION 
  EXIT Statement - 
      HELP EXIT 
  Expressions - 
      HELP EXPRESSIONS 
F 
  $FID_ACCT - 
      HELP FUNCTIONS $FID_ADDT 
  $FID_ASN - 
      HELP FUNCTIONS $FID_ASN 
  $FID_EXIST - 
      HELP FUNCTIONS $FID_EXIST 
  $FID_NAME - 
      HELP FUNCTIONS $FID_NAME 
  $FID_NRECS - 
      HELP FUNCTIONS $FID_NRECS 
  $FID_ORG - 
      HELP FUNCTIONS $FID_ORG 
  $FID_PASS - 
      HELP FUNCTIONS $FID_PASS 
  $FID_PSN - 
      HELP FUNCTIONS $FID_PSN 
  $FID_RES - 
      HELP FUNCTIONS $FID_RES 
  $FID_TYPE - 
      HELP FUNCTIONS $FID_TYPE 
  $FID_WSN - 
      HELP FUNCTIONS $FID_WSN 
  Field Action - 
      HELP FIELD_ACTION 
  FIELD Statement - 
      HELP FIELD 
  FILE Option - 
      HELP DELETE RULES: 
  Form Frames - 
      HELP FORM_FRAMES 
  FORM Statement - 
      HELP FORM 
  Frames - 
      HELP FRAMES 
  FROM WINDOW Option - 
      HELP WINDOW_OPTIONS RULES: 
  Functions - 
      HELP FUNCTIONS 
G 
  GLOBAL Statement - 
      HELP GLOBAL 
  GO Statement - 
      HELP GO 
  GOTO Statement - 
      HELP GOTO 
H 
  HBRDRCHR Option - 
      HELP WINDOW_OPTIONS RULES: 
  HBRDRSIZ Option - 
      HELP WINDOW_OPTIONS RULES: 
  $HSET - 
      HELP FUNCTIONS $HSET 
I 
  $IBUF - 
      HELP FUNCTIONS $IBUF 
  $IF - 
      HELP FUNCTIONS $IF 
  IF Statement - 
      HELP IF 
  $INDEX - 
      HELP FUNCTIONS $INDEX 
  $INPUT - 
      HELP FUNCTIONS $INPUT 
  Input Buffer - 
      HELP INPUT_BUFFER 
  INPUT Option - 
      HELP CLEAR RULES: 
      HELP OPEN RULES: 
  $INPUT Option - 
      HELP SET RULES: 
  Interprogram Linkage - 
      HELP INTERPROGRAM_LINKAGE 
  Introduction - 
      HELP PROCESSOR 
  ISSUE Clause - 
      HELP FORM RULES: 
      HELP MENU RULES: 
  ISSUE Statement - 
      HELP ISSUE 
  IWINDOW Clause - 
      HELP FORM RULES: 
      HELP MENU RULES: 
      HELP PROCEDURE RULES: 
  IWINDOW Option - 
      HELP CLEAR RULES: 
      HELP REMOVE RULES: 
J 
  JUSTIFY Clause - 
      HELP CONSTANT RULES: 
      HELP FIELD RULES: 
      HELP TEXT RULES: 
K 
  KEY Clause - 
      HELP DELETE RULES: 
      HELP READ RULES: 
      HELP WRITE RULES: 
  KEYED Option - 
      HELP OPEN RULES: 
L 
  $LENGTH - 
      HELP FUNCTIONS $LENGTH 
  LENGTH Clause - 
      HELP CONSTANT RULES: 
      HELP FIELD RULES: 
      HELP TEXT RULES: 
  LENGTH Option - 
      HELP WINDOW_OPTIONS RULES: 
  LET Statement - 
      HELP LET 
  LFTBRDR Option - 
      HELP WINDOW_OPTIONS RULES: 
  $LOWER - 
      HELP FUNCTIONS $LOWER 
  LPS - 
      HELP COMPILER_OPTIONS LPS 
  LS - 
      HELP COMPILER_OPTIONS LS 
  LU - 
      HELP COMPILER_OPTIONS LU 
M 
  MAIN Clause - 
      HELP FORM RULES: 
      HELP MENU RULES: 
      HELP PROCEDURE RULES: 
  $MAXIMUM - 
      HELP FUNCTIONS $MAXIMUM 
  Menu Frames - 
      HELP MENU_FRAMES 
  MENU Statement - 
      HELP MENU 
  MESSAGE Clause - 
      HELP MENU RULES: 
  $MINIMUM - 
      HELP FUNCTIONS $MINIMUM 
  MINLENGTH Option - 
      HELP WINDOW_OPTIONS RULES: 
  MINWIDTH Option - 
      HELP WINDOW_OPTIONS RULES: 
  MSGFILE Option - 
      HELP SET RULES: 
N 
  NAME Clause - 
      HELP CHOICE RULES: 
  NAME Option - 
      HELP WINDOW_OPTIONS RULES: 
  NLPS - 
      HELP COMPILER_OPTIONS LPS 
  NLS - 
      HELP COMPILER_OPTIONS LS 
  NLU - 
      HELP COMPILER_OPTIONS LU 
  NOU - 
      HELP COMPILER_OPTIONS OU 
  NSO - 
      HELP COMPILER_OPTIONS SO 
  NUI - 
      HELP COMPILER_OPTIONS UI 
  $NULL - 
      HELP FUNCTIONS $NULL 
  NULL Clause - 
      HELP CHOICE RULES: 
  NUMBER Clause - 
      HELP CHOICE RULES: 
  NUMBERS Clause - 
      HELP MENU RULES: 
  NWARN - 
      HELP COMPILER_OPTIONS WARN 
O 
  ON Statement - 
      HELP ON 
  OPEN Statement - 
      HELP OPEN 
  OPTIONAL Option - 
      HELP WINDOW_OPTIONS RULES: 
  OPTUI - 
      HELP COMPILER_OPTIONS OPTUI 
  OU - 
      HELP COMPILER_OPTIONS OU 
  OUTPUT Option - 
      HELP CLEAR RULES: 
P 
  PAGEHALT Option - 
      HELP WINDOW_OPTIONS RULES: 
  POSITION Option - 
      HELP WINDOW_OPTIONS RULES: 
  Position Options - 
      HELP POSITION_OPTIONS 
  Procedure Frames - 
      HELP PROCEDURE_FRAMES 
  PROCEDURE Statement - 
      HELP PROCEDURE 
  PROMPT Clause - 
      HELP CHOICE RULES: 
      HELP MENU RULES: 
  Prompts - 
      HELP PROMPTS 
  PROMPTS Clause - 
      HELP FORM RULES: 
Q 
  $QUOTE - 
      HELP FUNCTIONS $QUOTE 
R 
  READ Statement - 
      HELP READ 
  REMOVE Statement - 
      HELP REMOVE 
  REPEAT Clause - 
      HELP FORM RULES: 
      HELP MENU RULES: 
      HELP PROCEDURE RULES: 
  REPEAT Statement - 
      HELP REPEAT 
  RHTBRDR Option - 
      HELP WINDOW_OPTIONS RULES: 
  ROW Clause - 
      HELP CHOICE RULES: 
      HELP CONSTANT RULES: 
      HELP FIELD RULES: 
      HELP FORM RULES: 
      HELP MENU RULES: 
      HELP TEXT RULES: 
  $RU - 
      HELP FUNCTIONS $RU 
S 
  SCROLL Option - 
      HELP WINDOW_OPTIONS RULES: 
  $SEARCH - 
      HELP FUNCTIONS $SEARCH 
  SELECT Statement - 
      HELP SELECT 
  SET Statement - 
      HELP SET 
  SO - 
      HELP COMPILER_OPTIONS SO 
  SRCH - 
      HELP COMPILER_OPTIONS SRCH 
  Start Action - 
      HELP START_ACTION 
  $STEPCC - 
      HELP FUNCTIONS $STEPCC 
  $SUBSTR - 
      HELP FUNCTIONS $SUBSTR 
  $SWITCH - 
      HELP FUNCTIONS $SWITCH 
  Symbol Names - 
      HELP SYMBOL_NAMES 
T 
  TABS Clause - 
      HELP FORM RULES: 
      HELP MENU RULES: 
  TEXT Statement - 
      HELP TEXT 
  $TIME - 
      HELP FUNCTIONS $TIME 
  TOPBRDR Option - 
      HELP WINDOW_OPTIONS RULES: 
U 
  UCxx Option - 
      HELP CLEAR RULES: 
      HELP REMOVE RULES: 
  UI - 
      HELP COMPILER_OPTIONS UI 
  $UNAME - 
      HELP FUNCTIONS $UNAME 
  UNTIL Statement - 
      HELP UNTIL 
  UPDATE Option - 
      HELP OPEN RULES: 
  $UPPER - 
      HELP FUNCTIONS $UPPER 
V 
  $VALIDATE - 
      HELP FUNCTIONS $VALIDATE 
  Validation Options - 
      HELP VALIDATION_OPTIONS 
  VBRDRCHR Option - 
      HELP WINDOW_OPTIONS RULES: 
  VBRDRSIZ Option - 
      HELP WINDOW_OPTIONS RULES: 
  $VERIFY - 
      HELP FUNCTIONS $VERIFY 
W 
  WARN - 
      HELP COMPILER_OPTIONS WARN 
  WHILE Statement - 
      HELP WHILE 
  WIDTH Option - 
      HELP WINDOW_OPTIONS RULES: 
  WINDOW Clause - 
      HELP FORM RULES: 
      HELP MENU RULES: 
  WINDOW Option - 
      HELP CLEAR RULES: 
      HELP REMOVE RULES: 
      HELP WINDOW_OPTIONS RULES: 
  Window Options - 
      HELP WINDOW_OPTIONS 
  Windows - 
      HELP WINDOWS 
  WRAPPAGE Option - 
      HELP WINDOW_OPTIONS RULES: 
  WRITE Statement - 
      HELP WRITE 
X 
  XT Services - 
      HELP XT_SERVICES 
  XT_ADAPT_C - 
      HELP XT_INCLUDE_FILES 
  XT_ADAPT_COBOL - 
      HELP XT_INCLUDE_FILES 
  XT_ADAPT_FORTRAN - 
      HELP XT_INCLUDE_FILES 
  XT_ADAPT_PASCAL - 
      HELP XT_INCLUDE_FILES 
  XT_ENTER - 
      HELP XT_SERVICES XT_ENTER 
  XT_ENTER Service - 
      HELP XT_ENTER 
  XT_INIT - 
      HELP XT_SERVICES XT_INIT 
  XT_INIT Service - 
      HELP XT_INIT 
  XT_MACRO_M - 
      HELP XT_INCLUDE_FILES 
  XT_PARAM - 
      HELP XT_PARAM_STRUCTURE 
  XT_PERR_E - 
      HELP XT_INCLUDE_FILES 
  XT_READ - 
      HELP XT_SERVICES XT_READ 
  XT_READ Service - 
      HELP XT_READ 
  XT_RESTART - 
      HELP XT_SERVICES XT_RESTART 
  XT_RESTART Service - 
      HELP XT_RESTART 
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
HELP_INDEX
Syntax: 
IF expression [ THEN ] statement-1 
[ EL[SE] statement-2 ] 
Parameters: 
expression    Enter: HELP (ADAPT) EXPRESSIONS 
statement-1, statement-2    are any executable ADAPT statements. 
Description: 
The IF statement executes another statement if a specified condition is true. 
It can also provide a statement to execute if the condition is false. 
Rules: 
1.  The truth value of the expression determines whether statement-1 or 
    statement-2 is executed.  If the expression is true, statement-1 is 
    executed and statement-2, if present, is bypassed.  If the expression is 
    false, statement-1 is bypassed and statement-2, if present, is executed. 
2.  Both statement-1 and statement-2 can be single statements or a BEGIN 
    statement.  A BEGIN statement begins a block of statements that are 
    executed as a group.  An END statement must terminate each BEGIN block. 
3.  The ELSE clause is treated syntactically as if it were a separate 
    statement that is only permissible following an IF statement.  It must 
    begin on a separate line and must not be connected to the IF statement 
    with a continuation mark (;) on the preceding line.  However, statement-1 
    and statement-2 are parts of a compound statement.  If they are coded on a 
    line separate from the IF or ELSE, they must be connected to it with a 
    continuation mark (;).  See Examples for illustrations of proper 
    punctuation. 
4.  IF statements can be nested to any depth.  Each ELSE is paired with the 
    most recent IF that has not already been matched with an ELSE.  Any 
    statement other than an ELSE at the point where an ELSE could appear 
    implicitly terminates the entire nested IF structure. 
5.  Null ELSE statements are not allowed.  An emtpy BEGIN/END block must be 
    used if there is nothing for an ELSE condition to do within a nested IF. 
    (This feature enables diagnosis of missing continuation marks when the 
    ELSE and its target statement are on separate lines.) 
Examples: 
IF SHUT_UP THEN ; 
    SET QUIET ON 
If the variable SHUT_UP is nonzero, the SET statement is executed to establish 
quiet mode.  Note that a continuation mark (;) is needed at the end of the 
first line to indicate that the compound IF statement continues on the next 
line. 
IF A > B ; 
THEN ; 
    IF A > C ; 
        THEN ; 
            DISPLAY 'A is largest.' 
        ELSE ; 
            DISPLAY 'C is largest.' 
    ELSE ; 
        IF B > C ; 
        THEN ; 
            DISPLAY 'B is largest.' 
        ELSE ; 
            DISPLAY 'C is largest.' 
This illustrates the proper use of continuation marks for nested IF 
statements.  Note that all lines up to each target statement need final 
semicolons to indicate continuation, but that there are no continuation marks 
on the target statements themselves. 
IF A > B THEN BEGIN 
    DISPLAY 'A is larger.' 
    LET BIG = A 
    END 
ELSE IF B > A THEN BEGIN 
    DISPLAY 'B is larger.' 
    LET BIG = B 
    END 
ELSE BEGIN 
    DISPLAY 'A and B are equal.' 
    LET BIG = A 
    END 
This illustrates the use of statement blocks.  Note that there are no 
continuation marks to connect the BEGIN and END statements to the ones 
following them. 
00002
00004
00001
00003
The input buffer is used to hold the user's responses to prompts issued by the 
dialog manager.  Forms field inputs are handled differently.  They go directly 
into the corresponding fields, without affecting the input buffer. 
The user can follow the response to any prompt with values that are needed for 
following prompts.  This enables users who are familiar with a script to skip 
one or more steps by presupplying the necessary responses before the prompts 
are issued.  If responses are presupplied in this manner, the usual prompts 
and/or menus are not displayed. 
ADAPT's ability to presupply inputs should not be confused with normal CP-6 
type ahead.  Pressing <CR> after an input and entering expected subsequent 
responses before the responses appear is handled by the normal type ahead 
facilities, which do not inhibit the prompts and menus for typed ahead inputs. 
If text obtained from the input buffer is not a valid response for the current 
prompt, the input buffer is cleared and the error is handled as if it had 
resulted from a direct user input. 
Each frame of a dialog is associated with a program.  Other frames that are 
invoked are normally associated with the same program.  Dialog execution is 
suspended while the program executes a command, and resumed when the program 
is ready to read the next command.  The information needed for the dialog to 
resume where it was interrupted is called the dialog context.  The dialog 
context is kept in memory that is associated with the program running under 
the dialog. 
A frame can issue IBEX commands without affecting the dialog context or the 
associated program.  Dialog execution is suspended while IBEX executes the 
command, and resumes where it was interrupted when IBEX is done.  The dialog 
context is not affected, and the associated program is not aware that it has 
been interrupted. 
Invoking a noninteractive program is similar to issuing an IBEX command.  The 
program associated with the frame is suspended while the invoked program is 
running and is restarted when that program terminates.  Internally, this is 
more complicated than executing an IBEX command, but it is not much different 
from the perspective of the dialog designer or user. 
A frame can also invoke interactive programs in the same way as noninteractive 
programs.  However, when the invoked program is interactive, it issues its 
normal prompts and interacts with the user as if it were invoked outside of 
the dialog.  When the program terminates, dialog execution resumes at the 
point where it was interrupted, with no knowledge that any additional user 
interaction has taken place. 
For a dialog to invoke another interactive program to run under the dialog, a 
new frame must be entered that is associated with the new program.  This is 
done by specifying the new program name on the statement that defines the new 
frame.  Programs that are started explicitly under dialog control are 
specified with a DO clause; those that are started implicitly by returning a 
command to the running program (e.g., for the FORWARD and ANSWER commands in 
MAIL) are specified with an ISSUE clause.  This is the only way that links 
between interactive programs can be made transparent to the end user.  Only 
programs that are capable of running under a dialog can be invoked in this 
way.  When the invoked program terminates normally or abnormally, no matter 
what dialog frame is active, dialog execution resumes with the invoking 
program at the point where the frame that started the new program was entered. 
If the frame that started the new program exits, the program is terminated, so 
that when the prior frame resumes control, it will be communicating with the 
same program as before. 
Syntax: 
IS[SUE] { expression | / | \ } ,... 
Parameters: 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The ISSUE statement is used to issue commands to the calling program.  It puts 
text into the command buffer and/or returns the contents of the command buffer 
to the calling program. 
Rules: 
1.  The expressions are evaluated in the order specified.  If more than one 
    expression appears, a comma is required between each pair of expressions. 
    The string result of each expression is appended to the current command 
    buffer. 
2.  A slash (/) can be used within the list to send the current contents of 
    the command buffer to the calling program before processing the remaining 
    expressions.  This makes it possible to send several commands with a 
    single ISSUE statement. 
3.  The command buffer is normally sent to the calling program after all 
    expressions have been evaluated.  A backslash (\) can be used as the last 
    item in the expression list to inhibit this action.  This makes it 
    possible to construct a single command with several ISSUE statements. 
4.  When a command is passed to the calling program, script execution does not 
    continue until the program finishes processing the command.  The command 
    buffer is cleared before continuing, and the $ERROR function is set to 
    return any error code passed back from the program. 
Examples: 
ISSUE 'LIST ALL' 
issues the LIST ALL command to the program (presumably MAIL) that is running 
under the dialog. 
ISSUE 'SELECT * FROM A_TABLE WHERE NAME=''' || NAME || '''' 
issues the ARES command: 
    SELECT * FROM A_TABLE WHERE NAME='xxxx' 
where xxxx is the value of the variable NAME.  Note the use of pairs of quotes 
to represent a single quote with a string constant.  The three quotes after 
the equals sign constitute a single quote within the constant, followed by a 
quote to end the constant.  The four quotes at the end of the statement 
specify a constant consisting of a single quote.  The first and last quote 
delimit the constant, and the middle two generate a single quote within the 
constant. 
00002
00001
Syntax: 
L[ET] { variable-name } = expression 
      { field-name    } 
Parameters: 
variable-name    specifies the name of a local or global variable. 
field-name   specifies the name of a field in the current menu. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The LET statement assigns a value to a variable or field. 
Rules: 
1.  The specified expression is evaluated and the result replaces the current 
    value of the named variable or field. 
2.  If the name specified appears on a GLOBAL statement in the current frame, 
    the variable has global scope.  Once it has been given a value, a global 
    variable can be used outside of the frame. 
3.  If the name specified is not defined as a global variable and is not the 
    name of a field, it is assumed to refer to a local variable.  Local 
    variables pertain to only the frame in which they are defined.  They are 
    defined implicitly by assigning them a value with a LET statement. 
4.  A reference to a variable before it has been assigned a value results in 
    an empty string. 
00001
Syntax: 
M[ENU] frame-name 
    [ AB[BREVIATIONS] [ [ IS | = ] Y[ES] | N[O] | IN CAPS ] ] 
    [ C[OLUMN] [ IS | = ] position-option                   ] 
    [ DO [ IS | = ] expression                              ] 
    [ ISS[UE] [ IS | = ] expression                         ] 
    [ IW[INDOW] [ IS | = ] window-options                   ] 
    [ M[AIN] [ [ IS | = ] Y[ES] | N[O] ]                    ] ... 
    [ ME[SSAGE] [ IS | = ] expression                       ] 
    [ NU[MBERS] [ [ IS | = ] Y[ES] | N[O] ]                 ] 
    [ P[ROMPT] [ IS | = ] prompt-string                     ] 
    [ RE[PEAT] [ [ IS | = ] Y[ES] | N[O] ]                  ] 
    [ R[OW] [ IS | = ] position-option                      ] 
    [ T[ABS] [ IS | ARE | = ] { [ E[VERY] ] n } ...         ] 
    [ W[INDOW] [ IS | = ] window-options                    ] 
Parameters: 
frame-name    specifies the name of the frame. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
position-option    enter: HELP (ADAPT) POSITION_OPTIONS 
window-options    enter: HELP (ADAPT) WINDOW_OPTIONS 
prompt-string    specifies a quoted string. 
n    specifies an unsigned integer. 
Description: 
The MENU statement begins the definition of a menu frame.  A menu frame 
displays a list of choices and asks the user to pick one. 
Rules: 
1.  The frame-name is required.  It specifies the name that is used to invoke 
    the menu.  All frames in a script file must have unique names. 
2.  The ABBREVIATIONS clause determines whether or not minimum abbreviations 
    are to be constructed automatically for all choice names.  YES specifies 
    that this is to be done.  IN CAPS implies YES, and specifies that the 
    least number of characters needed to select a choice be shown in the menu 
    in upper case, with the remaining characters in lower case.  The default 
    is NO.  Automatic abbreviations can be overridden by specifying a 
    different abbreviation on a CHOICE statement. 
3.  The COLUMN and ROW clauses supply default positioning options for CHOICE, 
    CONSTANT, and TEXT statements that omit these clauses.  Only relative and 
    tabular positions can be specified as defaults; absolute positions are not 
    allowed.  Enter: HELP (ADAPT) POSITION_OPTIONS for more information. 
4.  Normally, the new frame runs under the same program as the invoking frame. 
    If the frame is to run under a different program, the DO or ISSUE clause 
    must be provided.  The DO clause specifies that the program is to be 
    invoked by the dialog manager.  The ISSUE clause should be used if the new 
    program is to be invoked by a command issued to the calling program.  The 
    string result of the expression is passed to IBEX or the calling program 
    in the same manner as for the DO and ISSUE statements. 
    The frame becomes the top level frame for the portion of the dialog that 
    is run under the new program.  Exiting the frame terminates the program. 
    Terminating the program runs the dialog down to the point where the frame 
    was entered. 
5.  The IWINDOW clause defines the interaction window for this frame.  If 
    omitted, the interaction window for the invoking frame is used. 
6.  The MAIN clause specifies that, if the script file is invoked without 
    specifying a frame name, this frame is to be used.  There can be only one 
    MAIN frame per script file.  Each MAIN frame definition overrides the 
    previous one.  To be notified of an overwritten MAIN frame, use the WARN 
    option when compiling. 
7.  The MESSAGE clause provides the message number of a diagnostic to be 
    issued when the user responds to the menu prompt with a question mark (?). 
8.  The NUMBERS clause specifies whether or not menu choices are to be 
    numbered.  YES specifies that a number is to be assigned to each choice. 
    NO indicates that choices are not to be numbered.  If numbers are 
    assigned, the number of a choice can be entered at the menu prompt to 
    select it.  If numbering is suppressed, choice names must be used to make 
    menu selections. 
9.  The PROMPT clause specifies the string to be used to prompt the user to 
    select a choice.  If omitted, a question mark (?) is used. 
10. The REPEAT clause specifies whether or not the frame is to be executed 
    repetitively.  YES specifies that the frame is to be reexecuted until a 
    EXIT statement is encountered.  NO means that the frame is to be 
    terminated after it has been executed once.  The default is NO. 
11. The TABS clause defines the position of tab stops.  These positions are 
    used by tabular positioning options for CHOICE and TEXT statements. 
    Specifying a list of numbers establishes tab stops at those positions. 
    The EVERY option establishes tab stops at fixed intervals across the 
    window.  If the last or only TAB option is an EVERY option, tabs are set 
    the specified number of columns apart up to the width of the window.  If 
    an EVERY option is not the last in the list, it must be followed by a 
    number, not another EVERY option.  The number limits the range of columns 
    filled with tabs by the EVERY option; it also sets a tab at that position. 
12. The WINDOW clause defines the window to be used to display the menu for 
    the frame.  If omitted, the frame window for the invoking frame is used. 
    If that frame is a procedure, the most recent frame window in the 
    invocation path is used.  If there is no frame window defined for any 
    frame in the invocation path, the menu appears in the interaction window. 
    The menu is displayed only if the prompt for a selection is issued on the 
    user's terminal.  If a valid menu selection is obtained from the input 
    buffer, the prompt is not issued and the contents of the frame window are 
    not changed.  The menu is also not displayed if it is already in the 
    specified window. 
13. Executable statements following the MENU statement constitute the frame 
    start action.  This action ends with the first following nonexecutable 
    statement.  If no executable statements immediately follow the MENU 
    statement, a start action can appear later in the frame, following an ON 
    START statement. 
14. The user makes a selection by responding to a prompt in the interaction 
    window, as described under HELP (ADAPT) PROMPTS.  The response is compared 
    to the possible choice names and/or numbers to determine which choice is 
    selected.  Comparisons are case insensitive.  The $CHOICE function can be 
    used to obtain the text of the menu choice for use in the dialog. 
00001
    A menu is a list of choices.  Each choice has a name, a number, or both. 
    When a menu is executed, the list of choices is displayed on the user's 
    terminal and a prompt is issued.  The user must respond to the prompt by 
    entering the name or number of the desired choice.  Each choice has an 
    associated action.  This action is executed when the user selects the 
    choice. 
    The user is normally forced to enter a valid response to the menu prompt; 
    if the response does not match the name or number of any of the choices, 
    the user is informed and the prompt is repeated.  It is possible to 
    override this behavior by defining an action to be taken for an 
    unrecognized response.  A default choice, to be used when the user enters 
    a null response, can also be defined. 
The following table shows the notation conventions used in this manual to 
describe statements, and other language elements.       
  Notation     Description 
  Lowercase Letters 
               Lowercase letters indicate that the element is a variable, to 
               be replaced with the desired value. 
  Capital Letters 
               Capital letters indicate a literal, to be entered as shown. 
  Special Characters 
               Special characters are literals, to be entered as shown. 
  Numerals 
               Numerals standing alone are literals, to be entered as shown. 
               Numerals embedded in or affixed to a string of capital letters 
               are also literals, to be entered as shown.  Numerals embedded 
               in or affixed to a string of lowercase letters are part of the 
               variable name to be replaced with a desired value, for example 
               fid1. 
  Brackets 
               An element inside brackets is optional.  If elements are 
               stacked vertically within brackets, the elements may be omitted 
               or one of them may be entered.  The brackets may be elongated 
               to contain the stack of elements, or may be represented by 
               vertically stacked, printed brackets. 
               For example, the notation 
                   [ COLUMN ]            or         [ COLUMN | ROW ] 
                   [ ROW    ] 
               means that the user may omit this entry, or may enter COLUMN, 
               or may enter ROW.  When used to enclose portions of keywords, 
               brackets signify that the bracketed portion may be omitted, or 
               truncated at any point.  For example, the notation K[EY] means 
               that the user may enter K, KE, or KEY. 
  Braces 
               Elements stacked inside a pair of braces identify a required 
               choice.  The braces may be elongated to contain the possible 
               choices, or may be represented by vertically-stacked printed 
               braces. 
                   {id }    means that either a value for id or the word 
                   {ALL}    ALL must be entered. 
               Alternatively, the vertical OR bar is used to separate the 
               choices, thus:  {id|ALL}. 
  OR Bar 
               The OR bar separates elements in a list from which one element 
               may be, or must be, chosen. 
                   {A|id}    means that either the letter A or the value 
                             of id must be entered. 
  Horizontal Ellipsis 
               The horizontal ellipsis indicates that a previous bracketed 
               element may be repeated. 
                   name ...    means that one or more name values may 
                     or        be entered.  A comma is always allowed 
                   name, ...   between list elements, but a blank is 
                               usually sufficient.  In a few cases, a 
                               comma is required.  These cases are 
                               indicated by the presence of a comma 
                               before the ellipsis (, ...). 
Syntax: 
   { A[BORT]  } 
   { C[HOICE] } 
   { B[REAK]  } 
ON { END      } 
   { ENT[RY]  } 
   { EX[IT]   } 
   { S[TART]  } 
Description: 
The ON statement is used to define an action to be executed at a given point 
during execution of a frame. 
Rules: 
1.  Executable statements following the ON statement constitute the action for 
    the specified condition.  This action is terminated by the first following 
    nonexecutable statement. 
2.  ON ABORT identifies an action to be taken when an ABORT statement is 
    executed.  An ON ABORT action differs from most other actions because it 
    is inherited by frames entered from the one defining the action while 
    those frames do not define their own abort actions.  When an ABORT 
    statement is encountered in a frame that does not define an abort action, 
    all frames in the path between the one that contains the action and the 
    one that issues the abort are terminated before executing the action. 
3.  ON BREAK identifies an action to be taken when the <BREAK> key is pressed. 
    An ON BREAK action differs from most other actions because it is inherited 
    by frames entered from the one defining the action while those frames do 
    not define their own break actions.  If <BREAK> is pressed while executing 
    a frame that does not define a break action, all frames in the path 
    between the one that contains the action and the current one are 
    terminated before executing the action. 
4.  ON CHOICE identifies an action to be taken after a valid choice is 
    selected, but before the action for the selected choice is performed.  ON 
    CHOICE is allowed only on menu frames. 
5.  ON END identifies an action to be taken at the end of a frame.  If the 
    frame is to be repeated, this action is followed by the frame start 
    action.  Otherwise, it is followed by the frame exit action. 
6.  ON ENTRY identifies an action to be taken once when the frame is entered 
    initially. 
7.  ON EXIT identifies an action to be taken once just before control returns 
    to the invoking frame. 
8.  ON START identifies an action to be taken just after the entry action.  If 
    the frame repeats, the start action (but not the entry action) is 
    reexecuted at the start of each repetition.  The start action is the 
    default action for a frame.  Executable statements immediately following a 
    MENU or PROCEDURE statement are assumed to constitute the start action. 
9.  A given frame can have only one ON statement for a given condition. 
00001
Syntax: 
OP[EN]  [# file-number ] expression 
    [ { CR[EATE] | IN[PUT] | U[PDATE] } ] ... 
    [ { CO[NSEC] | K[EYED] }            ] 
Parameters: 
file-number    specifies an internal file number from 1 to 9. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The OPEN statement opens a disk file for use by the dialog.  If a file is 
opened for INPUT, the dialog is initially positioned at the beginning of the 
file.  If it is opened for UPDATE, the initial position of the dialog is at 
the end of the file. 
Rules: 
1.  The file-number is used to identify the file on READ, WRITE, and CLOSE 
    statements.  If present, it must be prefixed with a pound sign (#).  If 
    omitted, #1 is assumed.  If a file is already open for the specified 
    number, that file is automatically closed. 
2.  The string value of the expression specifies the fid of the file to be 
    opened.  An error occurs if the file does not exist or cannot be accessed. 
3.  The CREATE, INPUT, or UPDATE keywords can be specified to determine the 
    file access mode, as follows: 
    a.  CREATE specifies that the file is to be created if it does not exist 
        or overwritten if it does exist. 
    b.  INPUT specifies that the file is to be opened for input only.  This is 
        the default.  An error occurs if the file does not exist. 
    c.  UPDATE specifies that the existing file is to be used if it already 
        exists or created if it does not exist. 
4.  The CONSEC or KEYED keyword can be specified to determine the organization 
    of the file that is to be created.  Only keyed and consecutive 
    organizations are allowed.  This option is ignored if an existing file is 
    accessed. 
5.  If the open is unsuccessful for any reason, the appropriate CP-6 error 
    code is saved where it can be accessed by the $ERROR function.  If the 
    open is successful, $ERROR is set to zero. 
Examples: 
OPEN '*TEMP' 
opens file number 1 (the default) to read from the *TEMP file. 
OPEN#3 NEW_FID, CREATE, KEYED 
opens file number 3 to the fid specified by the contents of the NEW_FID 
variable.  The file is created as a keyed file, replacing any existing file of 
the same name. 
00002
00001
COMPILER_OPTIONS
PROCEDURE
Syntax: 
C[OLUMN] [ IS | = ] { n | +n | { T[AB] | # } [ n ] } 
R[OW] [ IS | = ] { n | +n | { T[AB] | # } [ n ] } 
Parameters: 
n    specifies an unsigned integer. 
Description: 
Position options specify where items are placed in menus and forms.  Positions 
may be defined in one of three ways: absolute, relative, and tabular.  An 
absolute position is a fixed point within the frame window.  A relative 
position is based on the position of the previously defined item.  Tabular 
positioning places an item according to the tab stops defined for the frame. 
Rules: 
1.  The window in which a menu or form appears is treated as a grid of rows 
    and columns, where the upper left hand corner is row 1, column 1.  All 
    positions are established relative to that corner.  The actual row and 
    column where an item appears on the screen depends on the position of the 
    window placed on the screen. 
2.  The ROW clause defines the window row where the item is placed.  The 
    COLUMN clause defines the starting column within the row.  Unless an item 
    has an absolute position, its placement depends on the position of the 
    item defined just before it.  The initial position is before the first row 
    and before the first column.  If an item is on the same row as the prior 
    one, the previous position is the column after the end of the prior item. 
    Otherwise, the previous position is before the first column on the new 
    row. 
3.  A ROW or COLUMN clause that specifies only number is an absolute position. 
    The item is positioned starting at the specified row or column number. 
    Since rows and columns are numbered from 1, an absolute position of zero 
    is not allowed. 
4.  A number preceded by a plus sign (+) specifies a relative position. 
    Relative positioning places the item the specified number of rows or 
    columns beyond the previous position.  An item placed relative to an 
    absolute row is treated as if it also had an absolute row.  An item that 
    is relative to a tabular row is treated as part of that tabular row block. 
    ROW +0 places the item on the same row as the prior item, or on row 1 if 
    this is the first item defined.  COLUMN +0 concatenates the item to the 
    prior one if they are both on the same row, or places it in column 1 if 
    this item is on a different line or is the first one defined.  A position 
    of ROW +0, COLUMN +0 is the only way to concatente items.  Otherwise, an 
    error is reported unless at least one column separates each item. 
    ROW +1 places the item one row below the prior item, or on row 1 if it is 
    the first item defined.  COLUMN +1 starts the item one space beyond the 
    end of the prior item if they are on the same line, or in column 1 if the 
    item is on another row. 
    ROW +2 places the item two rows below the prior item or on row 2, 
    COLUMN +2 places it two spaces past the prior item on the line or in 
    column 2, and so on for higher numbers. 
5.  A position specification that contains pound sign (#) or the word TAB is a 
    tabular position.  Tabular positioning places items according to tab stops 
    defined by the TABS clause on the MENU or FORM statement.  If no TABS 
    clause was specified, tabular positions are not allowed.  Tabular 
    positions can be relative and absolute.  If TAB is used alone, it is a 
    relative tabular position.  If followed by a number, it is an absolute 
    tabular position. 
    a.  Relative tabular positions are allowed for both ROW and COLUMN. 
        For COLUMN, the item is placed at the first tab stop following the end 
        of the prior item, such that at least one column separates them.  If 
        there are no more tab stops in the row, of if the item would extend 
        past the last column of the window, the item is placed at the first 
        tab stop in the next row. 
        For ROW, a group of consecutive items specifying tabular row positions 
        is placed in row-major order across all tab stops in a block of rows. 
        The block starts on the row just below the previous item, or on row 1 
        if there is no prior items.  It extends down as many rows as it takes 
        to hold the entire group.  If the number of items is not evenly 
        divisible by the number of tab stops, the spare space is distributed 
        across the right-hand portion of the last line of the block.  An item 
        that specifies a row relative to one in a tabular row group is placed 
        that many tabular rows beyond the prior item.  Therefore, once a 
        tabular row group has been started, all subsequent items are part of 
        it, until one that specifies an absolute row.  Within the group, only 
        relative COLUMN positions may be specified. 
    b.  Absolute tabular positions are allowed only for COLUMN.  The item is 
        places starting at the specified tab stop on the row.  For example, 
        COLUMN #2 specifies the second tab stop defined for the frame.  If the 
        prior item started at or after that position on the same row, the item 
        is moved to the specified tab stop on the next row. 
6.  ROW and COLUMN clauses on the MENU or FORM statement are used by default 
    for all items that do not specify their own positioning.  If an item 
    specifies COLUMN but not ROW, ROW +0 is assumed.  If an item specifies ROW 
    but not COLUMN, COLUMN TAB is assumed if the frame defines tab stops, 
    otherwise the default is COLUMN +1.  If both ROW and COLUMN are omitted 
    for both the frame and the item, the defaults are ROW +1, and COLUMN TAB 
    if the frame defines tabs, or COLUMN +1 otherwise. 
Examples: 
On a MENU statement that uses an 80-column window and defines eight choices, 
the clauses: 
    ROW(TAB) TABS(1 21 41 61) 
cause the choices to be laid out at tab stops in row-major order, as follows: 
    choice1         choice3         choice5         choice7 
    choice2         choice4         choice6         choice8 
Given the same assumptions, the clauses: 
    COL(TAB) TABS(1 41) 
cause the choices to be positioned in column-major order, giving the following 
menu layout: 
    choice1                         choice2 
    choice3                         choice4 
    choice5                         choice6 
    choice7                         choice8 
The above assumes that neither ROW nor COLUMN is specified for any of the 
choices.  Specifying these options on menu items alters the default 
positioning.  Given the MENU options: 
    ROW IS TAB, TABS EVERY 33 
if the third choice specifies ROW +2, the menu layout is: 
    choice1         choice3             choice6 
    choice2         choice4             choice7 
                    choice5             choice8 
To define a menu that uses tabular row positioning for choices and has a menu 
title on the top line, use: 
    MENU...ROW=TAB, TABS=(1,41) 
    CONSTANT 'Menu Title' ROW=1 
    CONSTANT ' ' ROW=2 
    CHOICE PROMPT('First choice') 
        . 
        . 
        . 
    CHOICE PROMPT('Last choice') 
Note the use of a constant on row 2.  This forces the tabular row block to 
begin on the next line.  Specifying ROW=3 on the first choice would not have 
the same effect.  That would give an absolute position to that choice, so it 
would not be part of the tabular row block. 
00002
00001
Syntax: 
P[ROCEDURE] frame-name 
    [ DO [ IS | = ] expression             ] 
    [ ISS[UE] [ IS | = ] expression        ] 
    [ IW[INDOW] [ IS | = ] window-options  ] ... 
    [ M[AIN] [ [ IS | = ] Y[ES] | N[O] ]   ] 
    [ RE[PEAT] [ [ IS | = ] Y[ES] | N[O] ] ] 
Parameters: 
frame-name    specifies the name of the frame. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
window-options    enter: HELP (ADAPT) WINDOW_OPTIONS 
Description: 
The PROCEDURE statement begins the definition of a procedure frame.  A 
procedure is a frame that is executed without any implicit user interaction. 
Rules: 
1.  The frame-name is required.  It specifies the name that is used to invoke 
    the procedure.  All frames in a script file must have unique names. 
2.  If the procedure frame does not include any DISPLAY statements or $INPUT 
    functions, the frame is executed without user interaction.  If DISPLAY 
    statements or $INPUT functions are used, the appropriate messages and 
    prompts are issued in the interaction window. 
3.  Normally, the new frame runs under the same program as the invoking frame. 
    If the frame is to run under a different program, the DO or ISSUE clause 
    must be provided.  The DO clause should be used when the program is to be 
    invoked by the dialog manager.  The ISSUE clause should be used if the 
    program is to be invoked by a command issued to the calling program.  The 
    string result of the expression is passed to IBEX or the calling program 
    in the same manner as for the DO and ISSUE statements. 
    The frame becomes the top level frame for the portion of the dialog that 
    is run under the new program.  Exiting the frame terminates the program. 
    Terminating the program runs the dialog down to the point where the frame 
    was entered. 
4.  The IWINDOW clause defines the interaction window for this frame.  If 
    IWINDOW is omitted, the interaction window for the invoking frame is used. 
5.  The MAIN clause specifies that, if the script file is invoked without 
    specifying a frame name, this frame is to be used.  There can be only one 
    MAIN frame per script file.  Each MAIN frame definition overrides the 
    previous one. 
6.  The REPEAT clause specifies whether or not the frame is to be executed 
    repetitively.  YES specifies that the frame is to be reexecuted until an 
    EXIT statement is encountered.  NO means that the frame is to be 
    terminated after it has been executed once.  The default is NO. 
7.  Executable statements following the PROCEDURE statement constitute the 
    frame start action.  This action ends with the first following 
    nonexecutable statement.  If no executable statements immediately follow 
    the MENU statement, a start action can appear later in the frame, 
    following an ON START statement. 
00001
    A procedure frame consists of an action to be executed.  There is no 
    implicit user interaction involved as there is with a menu.  However, a 
    procedure can include statements that explicitly display messages and 
    prompt the user for inputs. 
The CP-6 ADAPT (A Dialog And Presentation Translator, hereinafter referred to 
as ADAPT) system is a tool for building menu-driven dialogs to support end 
users.  ADAPT allows a knowledgeable user to tailor a CP-6 product or set of 
products to fit the end user's understanding of the task to be performed. 
Based on rules defined by the knowledgeable user, ADAPT transforms end user 
inputs into the program invocations and commands needed to actually accomplish 
the task.  This makes it possible for end users to take advantage of a wide 
range of CP-6 capabilities, regardless of their background, computer 
experience, or native language. 
For a complete list of ADAPT HELP topics, enter: HELP (ADAPT) TOPICS. 
The dialog manager issues requests for user input by means of prompts in the 
interaction window.  There are two types of prompts:  those for menu 
selections and those for other inputs.  The two types of prompt are similar in 
many ways.  In both cases, a prompt string is displayed at the start of the 
next line of the interaction window.  The user can the enter the response on 
the same line, just after the prompt.  The user's input for any prompt can 
contain responses to satisfy anticipated subsequent prompts of either type. 
However, the rules for dividing the input into responses for multiple prompts 
differ slightly depending on the type of prompt. 
For a menu prompt, the portion of the user's input up to the first blank or 
semicolon (;) is treated as the menu selection.  For other prompts, embedded 
blanks are allowed; a semicolon is required to mark the end of the response. 
Anything after a semicolon (or a blank, for menu prompts) is placed in the 
input buffer.  If the input buffer is not empty when the dialog manager is 
ready to issue a prompt, its contents are used as if they had been entered by 
the user for that prompt.  The response to the prompt is determined as 
specified, depending on the type of prompt, and anythingTN15 left over is put 
back in the input buffer. 
To enter a response that contains a semicolon, the user must enclose the 
response in single quotes (').  Within a quoted input, a pair of quotes ('') 
must be used to represent a single quote.  However, single quotes embedded in 
an input that is not enclosed in quotes require no special treatment.  Leading 
and trailing blanks are automatically stripped from the response for each 
prompt.  Note that dialogs can also request transparent input for a prompt. 
In this case, the user's entire input is taken exactly as entered.  Leading 
and trailing blanks are retained, and semicolons and quotes have no special 
significance.  Transparent input is most useful for entering lines of text, 
such as the body of a mailgram. 
Syntax: 
REA[D] [ #file-number ] variable-name [ K[EY] [ IS | = ] expression ] 
Parameters: 
file-number    specifies an internal file number from 1 to 9. 
variable-name    specifies the name of a local or global variable. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The READ statement reads a record from a disk file. 
Rules: 
1.  The file-number should be the same as the number specified when the file 
    was opened.  An error occurs if the file is not open.  If specified, the 
    file-number must be prefixed with a pound sign (#).  If omitted, #1 is 
    assumed. 
2.  The variable-name specifies where the contents of the record are to be 
    stored.  If an error occurs, the specified variable is set to an empty 
    string. 
3.  The file can be of KEYED, CONSEC, INDEXED, or UR organization.  If it 
    contains VFC characters, they are ignored. 
4.  If the KEY clause is omitted, the file is read consecutively.  The record 
    returned is the one after the last one accessed.  If the file was just 
    opened, the first record is returned. 
5.  If the KEY clause is supplied, it specifies the key of the record to be 
    read.  If the expression evaluates to a string result, the result is used 
    as the key.  String keys can be used only with KEYED files.  If the 
    expression evaluates to a number, it is used as the record number within 
    the file. 
6.  If the read is unsuccessful for any reason, the appropriate CP-6 error 
    code is saved where it can be accessed by the $ERROR function.  If the 
    read is successful, $ERROR is set to zero. 
Examples: 
READ REC 
reads the next record of file number 1 (the default) and puts its contents 
into the REC variable. 
READ #4 REC2 K(2) 
reads the second record of file number 4 and places its contents in the REC2 
variable. 
00002
00001
Syntax: 
         { IW[INDOW] } 
REM[OVE] { W[INDOW]  } 
         { UCxx      } 
Description: 
The REMOVE statement removes windows from the terminal screen. 
Rules: 
1.  REMOVE IWINDOW removes the current interaction window. 
2.  REMOVE WINDOW removes the current frame (form or menu) window.  In a 
    procedure frame, this removes the window for the menu or form frame that 
    invoked the procedure, either directly or indirectly. 
3.  REMOVE UCxx removes the window for the specified logical device stream. 
    This can be either an explicit stream number (e.g., UC02) or a symbolic 
    stream name (e.g., UCAA).  In either case, the stream must be one that is 
    known to the dialog.  See HELP (ADAPT) WINDOW_OPTIONS for more information 
    on stream names and numbers. 
4.  An attempt to remove the original window for the dialog is ignored.  To 
    erase the contents of this window, the CLEAR statement should be used 
    instead. 
5.  A removed window is recreated automatically the next time the dialog 
    attempts to read from or write to it. 
00001
Syntax: 
REP[EAT] [[ frame-name ] FR[AME] ] 
         [ FORM                  ] 
Parameters: 
frame-name    specifies the name of a frame. 
Description: 
The REPEAT statement forces reexecution of the current frame. 
Rules: 
1.  If no frame-name is specified, the current frame is repeated.  If the 
    frame definition statement specifies REPEAT, reaching the end of the frame 
    is treated as an implied REPEAT statement. 
2.  If a frame-name is specified, the named frame is repeated.  Specifying the 
    current frame is equivalent to omitting the frame-name.  If the frame 
    named is not the current one, it must be in the path of frames entered to 
    get to the current one.  All frames in the path from the named frame to 
    the current one are immediately terminated; any exit or abort actions for 
    these frames are bypassed. 
3.  The repeated frame normally resumes execution with its start action. 
    However, a REPEAT statement on an entry action repeats the entry action. 
4.  REPEAT FORM repeats the current form.  If the current frame is not a form, 
    all frames in the path from the current frame to the most recent form are 
    immediately terminated.  This statement simulates the response to a 
    validation error on a form field.  Unlike REPEAT FRAME, it resumes 
    execution with the repainting of the form at the end of the start action. 
00001
SET
Syntax: 
SEL[ECT] [ field-name ... ] 
Parameters: 
field-name    specifies the name of a field in the current form. 
Description: 
The SELECT statement selects the fields to be open for input the next time the 
current form is read. 
Rules: 
1.  Field selections are cumulative.  That is, each SELECT statement adds to 
    the list of fields already selected.  All fields selected before the form 
    is first read are open for user input the first time through the form 
    frame.  All fields selected between form inputs are open on subsequent 
    repetitions. 
2.  If no SELECT statement is encountered before or beteween form reads, the 
    default is to select all fields defined by a FIELD statement. 
3.  A field-name list is only allowed within the form frame itself.  All names 
    in the list must be declared on FIELD statements elsewhere in the frame. 
    CONSTANT and TEXT fields cannot be selected. 
4.  A SELECT statement with no field-name list is allowed in any frame, but 
    has no effect unless there is a form active.  If multiple forms are 
    active, the statement applies to the one most recently entered.  If 
    executed within a field action, the current field is selected; otherwise, 
    all input fields in the form are selected. 
00002
00001
00003
Syntax: 
      { ATTR | A[TTRIBUTES] } [ FOR field-name ... ] [ TO | = ] attribute...} 
      {                                                                     } 
      { C[URSOR] [ TO | = ] field-name                                      } 
      {                                                                     } 
      { E[CHO] [ [ IS | = ] { ON | OF[F]   } ]                              } 
      {        [            { Y[ES] | N[O] } ]                              } 
      {                                                                     } 
SE[T] { $ERROR [ IS | = ] expression                                        } 
      {                                                                     } 
      { $INP[UT] [ IS | = ] expression                                      } 
      {                                                                     } 
      { { MSG | M[ESSAGE] } F[ILE] [ IS | = ] expression                    } 
      {                                                                     } 
      { Q[UIET] [ [ IS | = ] { ON | OF[F]   } ]                             } 
      {         [            { Y[ES] | N[O] } ]                             } 
      {                                                                     } 
      { U[PDATE] [ [ IS | = ] { ON | OF[F]   } ]                            } 
      {          [            { Y[ES] | N[O] } ]                            } 
Parameters: 
field-name    is the name of a field in the current form. 
attribute    enter: HELP (ADAPT) ATTRIBUTE 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The SET statement sets the value of various options. 
Rules: 
1.  SET ATTRIBUTES changes the display attributes of fields in a form.  A 
    field-name list is only allowed within a form frame.  The names in the 
    list must be declared on a CONSTANT, FIELD, or TEXT statement elsewhere in 
    the frame.  SET ATTRIBUTE statements with no field-name list are allowed 
    in any frame, but are only meaningful if there is a form active.  If the 
    current action for the active form is a field action, that field's 
    attributes are changed; otherwise, attributes for all fields in the form 
    are changed. 
2.  SET CURSOR establishes the field where the cursor is to initially appear 
    when the form is next read.  There can only be one initial cursor setting; 
    each SET CURSOR statement overrides any previous one.  The setting applies 
    only to the next read; cursor settings are not saved across form reads. 
    If no initial cursor setting is established, the default is to put the 
    cursor in the first input field on the form.  A field-name is only allowed 
    within a form frame.  The name must be declared on a FIELD statement 
    elsewhere in the frame.  SET CURSOR statements with no field-name are 
    allowed in any frame, but are only meaningful if there is a form active. 
    If the current action for the current form is a field action, the cursor 
    is set to appear in that field; otherwise, it is set to the first input 
    field in the form. 
3.  SET ECHO turns command echoing on or off.  When command echoing is on, all 
    commands issued with the ISSUE or DO statements are copied to the 
    interaction window before being passed on for execution.  YES and NO can 
    be used in place of ON and OFF, respectively.  If SET ECHO is specified 
    with no option, ON is assumed. 
4.  SET $ERROR sets the error code to be used by a subsequent DISPLAY $ERROR 
    command or by a user input of a question mark (?).  The numeric result of 
    the expression is used as the error number.  The other components of the 
    error code are set to zero. 
5.  SET $INPUT primes the reread buffer for the next user input to the string 
    result of the specified expression.  When the next prompt is issued, for 
    either a menu input or a $INPUT function, the specified text is displayed 
    after the prompt, and is taken as the response to the prompt if the user 
    presses <CR>.  This value is cleared automatically after the next prompt 
    has been satisfied.  If the prompt is not issued because it can be 
    satisfied by text in the input buffer, the reread buffer is not altered; 
    <ESC-D> still recalls the last line typed by the user. 
6.  SET MSGFILE establishes the message file that contains the messages to be 
    issued when the user types a question mark (?) in response to a prompt. 
    The string result of the expression supplies the fid of this file. 
7.  SET QUIET can be used to suppress unwanted output.  When quiet mode is 
    set, all output to the terminal from programs running under the dialog is 
    discarded.  Quiet mode is reset automatically before any terminal I/O that 
    is issued by the dialog.  ON or YES sets quiet mode.  OFF or NO resets it. 
    If SET QUIET is specified with no option, ON is assumed. 
8.  SET UPDATE can be used to change the ability to update the current form. 
    See the UPDATE option rule (9) of the FORM statement for more information. 
00001
The start action is executed after the entry action.  Once the action is 
started, any request to repeat the frame reenters the action.  A request to 
exit the frame within a start action transfers control to the exit action.  In 
a menu frame, normal completion of the start action brings up the menu.  In a 
procedure frame, control transfers directly to the end action.  In a form 
frame, field values and attributes are reset before the action is executed, 
and the form is displayed and read on normal completion. 
    ADAPT statements are:  ABORT, BEGIN, BREAK, CHOICE, CLEAR, CLOSE, 
    CONSTANT, DELETE, DISPLAY, DO, END, ENTER, EXIT, FIELD, FORM, GO, GOTO, 
    IF, ISSUE, LET, MENU, ON, OPEN, READ, REMOVE, REPEAT, SELECT, SET, TEXT, 
    UNTIL, WHILE, and WRITE. 
    To see a specific statement, enter:  HELP (ADAPT) statement.  Note:  Each 
    statement can be abbreviated to the minimum number of characters needed to 
    identify the statement uniquely. 
    A symbolic name used in an expression refers to a global variable, a local 
    variable, or a field. 
    If the name is declared on a GLOBAL statement in the same frame as the 
    reference, the name refers to a global variable.  If the name is declared 
    on a TEXT statement, it refers to a field.  A local variable is declared 
    implicitly by assigning it a value with a LET statement. 
    A reference to a name that is not defined in one of these ways results in 
    a compile error.  The definition need not precede the reference, but it 
    must appear in the same frame. 
    A reference to a name that is defined but has not yet been assigned a 
    value results in an empty string. 
Syntax: 
T[EXT] { field-name [ ( length ) ] [ = expression ] } 
       { expression                                 } 
    [ { A[TTRIBUTES] | ATTRS } [ IS | ARE | = ] attributes ] 
    [ C[OLUMN] [ IS | = ] position-option                  ] 
    [ I[NITIALIZE] [ WITH | = ] expression                 ] 
    [ J[USTIFY] [ IS | = ] { L[EFT] | C[ENTER] | R[IGHT] } ] ... 
    [ L[ENGTH] [ IS | = ] length                           ] 
    [ P[ROMPT] [ IS | = ] { field-prompt | N[ONE] }        ] 
    [ R[OW] [ IS | = ] position-option                     ] 
Parameters: 
attribute    enter: HELP (ADAPT) ATTRIBUTE 
field-name    specifies the name of the text field. 
length    specifies an unsigned integer. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
field-prompt    is a quoted string. 
position-option    enter: HELP (ADAPT) POSITION_OPTIONS 
Description: 
The TEXT statement defines text to appear in a menu or form.  The text can be 
changed by the dialog, but not by the user. 
Rules: 
1.  The TEXT statement is allowed only in menu and form frames. 
2.  The field-name is optional.  It specifies the name that can be used to 
    refer to the text field.  All field-names in a frame must be unique. 
3.  If an expression is specified, the string result of the expression is 
    displayed.  For menus, the expression is evaluated before the start action 
    is executed.  If a field-name is also specified, the value of the field is 
    changed when the expression is evaluated.  An expression can be specified 
    in several ways, as shown in the syntax, but only one expression is 
    allowed. 
4.  The ATTRIBUTES option is meaningful only in form frames.  It defines the 
    default display attributes to be applied to the field.  If the statement 
    also defines the prompt for the field, the specified attributes also are 
    also applied to the prompt.  If the field's attributes are altered by a 
    SET ATTRIBUTES statement, they are reset to the default whenever the 
    frame's start action is executed. 
5.  The COLUMN and ROW clauses specify placement of the text field within the 
    frame.  The options allowed are described under HELP (ADAPT) 
    POSITION_OPTIONS. 
6.  The JUSTIFY clause specifies how to truncate or pad field values.  LEFT 
    specifies truncation and padding at the right end of the field.  RIGHT 
    specifies truncation and padding at the left end of the field.  CENTER 
    specifies truncation at the right and padding on both sides of the field. 
    The default is LEFT. 
7.  The length specifies the maximum number of characters in the text.  It can 
    be omitted if the value is specified to be a constant.  The length can be 
    enclosed in parentheses before the expression.  It can also be specified 
    by the LENGTH clause.  If a value contains fewer characters than specified 
    by the length, it is padded with blanks.  If a value contains more 
    characters than are allowed, it is truncated. 
8.  The PROMPT clause specifies the text to be used as a prompt describing the 
    text field.  If present, the prompt precedes the field itself, with a 
    blank between them.  If no prompt is provided for a field in a form that 
    specifies PROMPTS=YES, the field name is used as the prompt by default. 
    PROMPT=NONE can be specified to override this default. 
9.  The TEXT statement does not have an associated action.  It must be 
    followed by another nonexecutable statement. 
Examples: 
TEXT 'Enter HELP for more information' C(40) R(1) 
defines a field of constant text to appear on the first line of the menu, 
starting at position 40. 
TEXT 'The current value is '||CURVAL, LENGTH IS 20 
defines a text field containing: 
    The current value is #################### 
where the string of #'s is replaced by the value of the variable CURVAL.  Note 
that the LENGTH option is required to specify the maximum size of the field. 
This is because the field contains a variable, which has no set length. 
TEXT '---- MAIN MENU ----' ROW 1, COL 1, LEN 80, JUSTIFY CENTER 
defines a field consisting of the entire top line of the menu, with a constant 
title in the center of the line.  Note that although the length is not 
required when constant text is used, it can still be provided.  This technique 
makes it possible to build menus with centered titles without having to count 
columns. 
00002
00001
DATE_TIME_FORMATS
Syntax: 
U[NTIL] expression statement 
Parameters: 
expression    enter: HELP (ADAPT) EXPRESSIONS 
statement    is any executable ADAPT statement. 
Description: 
The UNTIL statement executes another statement or statement block until a 
specified condition is true. 
Rules: 
1.  The statement to be executed can be a single statement or a BEGIN 
    statement.  A BEGIN statement begins a block of statements that are to be 
    executed.  An END statement must terminate the block. 
2.  The specified expression is evaluated after the statement or block has 
    been executed.  If the expression is true, the statement or block is 
    executed again.  If it is false, control passes to the next statement.  If 
    a statement block is specified, the statement following the END statement 
    terminates the block. 
3.  The UNTIL statement is a compound statement; the statement it contains is 
    part of the UNTIL.  If this statement appears on a separtate line, it must 
    be connected to the first line with a continuation mark (;) at the end of 
    the first line. 
Example: 
    IF $FID_NRECS( 'MYFILE' ) > 0 ; 
    THEN BEGIN 
        OPEN 'MYFILE' 
        UNTIL $ERROR BEGIN 
            READ A_LINE 
            DISPLAY A_LINE 
            END 
        CLOSE 
        END 
This loop copies the contents of the file named MYFILE to the user's terminal. 
The loop stops when an error (presumably end-of-file) occurs while reading the 
file.  Note that since the condition is checked at the end of the loop, at 
least one record is read and displayed if the loop is entered.  Therefore a 
special check is needed to catch the case of an empty file and avoid entering 
the loop if there is not at least one record to be displayed. 
00002
00004
00001
00003
Syntax: 
{ { { A  }                                     }     } 
{ { { AN }                                     }     } 
{ { { N  } [ length ] [ { + | - } exceptions ] } ... } 
{ { { O  }                                     }     } 
{ { { X  }                                     }     } 
{                                                    } 
{ [ { NOT | ~ } ] IN                                 } [ R[EQUIRED] ] 
{     ( { constant [ { TO | - } constant ] } ... )   } 
{                                                    } 
{ D[ATE] [ ( { A[NS] | L[OCAL] } ) ]                 } 
{                                                    } 
{ [FID]                                              } 
{                                                    } 
{ T[IME] [ ( { A[NS] | L[OCAL] } ) ]                 } 
Parameters: 
length    specifies a positive integer between 1 and 31. 
exceptions    specifies a quoted string. 
constant    enter: HELP (ADAPT) CONSTANTS 
Description: 
Validation options define the validation criteria for responses to $INPUT 
functions.  They are also used to verify the contents of variables with the 
$VALIDATE function. 
Rules: 
1.  Validation can be specified in one of three ways: by character set, by 
    value, or by format.  Multiple options can be specified for some 
    validation types, but multiple validation types cannot be used for a 
    single input. 
2.  A, AN, N, O, and X specify character set validation.  A list of these 
    options can be specified to validate an item that consists of parts with 
    different character sets.  These options are defined as follows: 
    a.  A - requires an upper- or lower-case alphabetic character. 
    b.  AN - requires an upper- or lower-case alphabetic character or a 
        decimal digit. 
    c.  N - requires a decimal digit. 
    d.  O - specifies that only characters in the exceptions string are 
        allowed.  The exceptions string is required. 
    e.  X - allows any ASCII character. 
3.  Any character set validation keyword can be followed by a number that 
    indicates the number of characters allowed.  A number on the last or only 
    option indicates the maximum number of characters.  A number on any option 
    except the last one indicates that exactly that many characters must be 
    entered. 
4.  An exceptions string can be used with any character set validation option 
    to specify additions or deletions from the list of permissible characters. 
    If the exception string is preceded with a plus sign (+), all characters 
    in the string are added to the list of permissible characters.  If the 
    exception string is preceded with a minus sign (-), characters in the 
    exception string are removed from the list.  Additions are not allowed for 
    X; deletions are not allowed for O. 
5.  IN specifies validation by value.  The IN keyword must be followed by a 
    list of individual values and ranges of values in any order and 
    combination.  The list must be enclosed in parentheses.  Normally, inputs 
    that match an individual value or fall within one of the ranges are 
    accepted.  If the NOT keyword is used, the only values accepted are those 
    that would otherwise be rejected.  Comparisons are case insensitive. 
    All constants in the list must be either string or numeric.  Mixed data 
    types are not allowed. 
    String constants can contain a slash (/) to indicate the minimum number of 
    characters that must be entered.  Abbreviations are allowed only for 
    individual values; they are not allowed on limiting values for a range. 
6.  DATE and TIME validation check to ensure that the value is in the 
    specified format, and that all subfields are within the allowable range. 
    The possible formats, ANS and LOCAL, are described under HELP (ADAPT) 
    DATE_TIME_FORMATS.  If no format is specified, ANS is assumed. 
7.  If FID is specified, only values that conform to the rules for a fid are 
    accepted.  This verifies the format but does not ensure that the fid can 
    actually be opened.  It does verify that the name and account do not use 
    any impermissible characters.  Note that a question mark (?) is considered 
    a permissible character. 
8.  If the REQUIRED option is specified, a null value is not accepted. 
    Otherwise, a null value is always accepted, regardless of the validation 
    options specified.  If REQUIRED is specified, the entire validation 
    criteria must be enclosed in parentheses. 
9.  If the validation criteria are not met, an appropriate error code is 
    created for subsequent access via the $ERROR function. 
Examples: 
LET NAME = $INPUT('What name?', X20) 
prompts the user for a name containing a maximum of 20 characters.  If too 
many characters are entered, a diagnostic is issued and the prompt is 
repeated. 
LET NAME = $INPUT('What name?', (X20,REQ)) 
This is the same as the previous example, except that a null input is not 
allowed.  Note the use of parentheses around the validation options.  They are 
required since there is more than one clause in the validation criteria. 
LET VALID_SSN=(SSN||' ',(N3,O1+'-',N2,O1+'-',N4,O+' ')) 
sets the variable VALID_SSN to true if the value of SSN is of the form: 
    nnn-nn-nnnn 
SSN is concatenated with a blank and a blank is required at the end to ensure 
that all four digits of the last component are present.  If this was not done, 
the validation would succeed if the last component only contained one, two, or 
three digits. 
LET NUM=$INPUT('Enter a number between 1 and 10.',IN(1-10)) 
prompts the user for a number and issues a diagnostic if the number entered is 
not between 1 and 10.  The number entered is stored in the variable named NUM. 
LET MODE=$INPUT('Batch or Xeq?',(IN('B/ATCH','X/EQ'),REQUIRED)) 
prompts the user to enter either BATCH or XEQ, both of which can be 
abbreviated to their first letter.  A null input is rejected.  Note that the 
extra pair of parentheses is required around the entire validation criteria, 
and the REQUIRED option must not be inside the parentheses that surround the 
list of permissible values. 
00002
00001
WRITE
Syntax: 
WH[ILE] expression statement 
Parameters: 
expression    enter: HELP (ADAPT) EXPRESSIONS 
statement    is any executable ADAPT statement. 
Description: 
The WHILE statement executes another statement or statement block as long as a 
specified condition is true. 
Rules: 
1.  The statement to be executed can be a single statement or a BEGIN 
    statement.  A BEGIN statement begins a block of statements that are to be 
    executed.  An END statement must terminate the block. 
2.  The truth value of the expression determines whether the specified 
    statement or block is to be executed.  If the expression is true, the 
    statement or block is executed, and control loops back to reevaluate the 
    expression.  If the expression is false, control transfers to the next 
    statement.  If a statement block is specified, the statement following the 
    END statement terminates the block. 
3.  The WHILE statement is a compound statement; the statement it contains is 
    part of the WHILE.  If this statement appears on a separate line, it must 
    be connected to the first line with a continuation mark (;) at the end of 
    the first line. 
Example: 
    OPEN 'MYFILE' 
    READ A_LINE 
    WHILE NOT $ERROR BEGIN 
        DISPLAY A_LINE 
        READ A_LINE 
        END 
    CLOSE 
This loop copies the contents of the file named MYFILE to the user's terminal. 
The loop stops when an error (presumably end-of-file) occurs while reading the 
file.  Note that since the condition is checked at the start of each 
repetition of the loop, the first record must be read before entering the 
loop, and the next record read at the end of the loop, to avoid trying to 
display a record after end-of-file is reached. 
00002
00004
00001
00003
All communication between the dialog manager and the user takes place in one 
of two windows: the frame window or the interaction window.  The frame window 
contains the menu for menu frames; it does not exist for procedure frames. 
The interaction window is used for messages and prompts; this window is 
available in all frames. 
The initial window for a dialog is the one for the command output data control 
block (DCB) of the calling program.  Until otherwise specified, this window is 
both the frame and interaction window.  Menu frame and interaction windows can 
coexist.  Forms reqiure a separate frame window.  All windows used by the 
dialog are derived from the initial window.  If the command output DCB is 
assigned to a file, all dialog output is written to that file.  Dialogs using 
forms cannot use a file for output. 
Each frame can define a new logical device stream to be used for either 
window.  If either window is not defined, the corresponding stream for the 
invoking frame is used. 
The dialog manager does not open a window until it needs to read or write in 
it.  Therefore, if a frame issues no messages or prompts, the interaction 
window is never opened.  The frame window for a menu is opened at the time the 
menu is to be displayed, just before the prompt for the menu choice.  If a 
choice is supplied in the input buffer, the menu is not displayed and the 
window is not opened. 
The window used for output written to the terminal by the program running 
under the dialog depends on the DCB the program uses to write it.  Output 
through the program's command output DCB appears in the current dialog 
interaction window.  Output through other DCBs appears in the same window that 
it would if the dialog manager were not active (typically UC01 for normal 
processors, and UC98 for IBEX).  If the dialog uses an interaction window 
other than the default one, the dialog designer must take care to leave a 
default window of sufficient size to hold any output that the program might 
direct to it. 
Syntax: 
{ B[TMBRDR] [ [ IS | = ] Y[ES] | N[O] ]                         } 
{ F[ROM] [W[INDOW]] [ IS | = ] stream-name                      } 
{ HBDRC[HR] [ IS | = ] char                                     } 
{ HBDRS[IZ] [ IS | = ] size                                     } 
{ { L[ENGTH] | WL[ENGTH] } [ IS | = ] value                     } 
{ LF[TBRDR] [ [ IS | = ] Y[ES] | N[O] ]                         } 
{ MIN[LENGTH] [ IS | = ] length                                 } 
{ MINW[IDTH] [ IS | = ] width                                   } 
{ NA[ME] [ IS | = ] stream-name                                 } 
{ O[PTIONAL] [ [ IS | = ] Y[ES] | N[O] ]                        } ... 
{ PA[GEHALT] [ [ IS | = ] Y[ES] | N[O]                          } 
{ PO[SITION] [ IS | = ] { T[OP] | B[OTTOM] | L[EFT] | R[IGHT] } } 
{ R[HTBRDR] [ [ IS | = ] Y[ES] | N[O] ]                         } 
{ SC[ROLL] [ [ IS | = ] Y[ES] | N[O]                            } 
{ T[OPBRDR] [ [ IS | = ] Y[ES] | N[O] ]                         } 
{ VBDRC[HR] [ IS | = ] char                                     } 
{ VBDRS[IZ] [ IS | = ] size                                     } 
{ { W[IDTH] | WW[IDTH] } [ IS | = ] value                       } 
{ WR[APPAGE] [ [ IS | = ] Y[ES] | N[O]                          } 
Parameters: 
stream-name    specifies a terminal resource name: UCxx. 
char    specifies a single quoted character. 
size    specifies an integer between 0 and 15. 
length    specifies an integer between 0 and 254. 
width    specifies an integer between 0 and 254. 
Description: 
Window options specify the characteristics of the frame and interaction 
windows used by an ADAPT frame.  Unless otherwise specified, all options have 
the same function as the corresponding LDEV or TERMINAL options.  See: HELP 
(IBEX) WINDOW_OPS. 
Rules: 
1.  If no window options are specified for a window, the same window as was 
    used by the invoking frame is used.  If no window options are specified 
    for the top level frame, the window for the calling program is used.  If 
    the program's output DCB is not assigned to a terminal, or is assigned to 
    a terminal incapable of vertical cursor movement, all window handling 
    specifications are ignored. 
2.  In a menu frame, both the frame and interaction window can use the same 
    stream.  In a form frame, both windows must be different. 
3.  BTMBRDR specifies whether or not space is to be reserved at the bottom to 
    separate this window from the one below it.  The default for a new window 
    is the setting of this option for the FROM WINDOW.  The default for an 
    existing window is to ignore this option. 
4.  FROM WINDOW specifies the stream from which the new stream is to be 
    created.  This is ignored for existing windows.  The default is the 
    current stream for the window (frame or interaction) being defined. 
5.  HBRDRCHR specifies an ASCII character to be used to mark the edge of the 
    horizontal border space(s).  The default for a new window is the setting 
    of this option for the FROM WINDOW.  The default for an existing window is 
    to ignore this option. 
6.  HBRDRSIZ specifies the size in lines of the horizontal border space(s) 
    (TOPBRDR and BTMBRDR).  The default for a new window is the setting of 
    this option for the FROM WINDOW.  The default for an existing window is to 
    ignore this option.  If set to a value greater than 1, all border lines 
    except the one closest to the edge are filled with blanks. 
7.  LENGTH specifies window length, including any borders, as an absolute 
    number of lines.  LENGTH is ignored for new windows with a POSITION of 
    LEFT or RIGHT.  The default is zero, which results in no change to an 
    existing window, but is interpreted to mean all but one line of the FROM 
    WINDOW for a new window. 
8.  LFTBRDR specifies whether or not to reserve space at the left to separate 
    this window from the one to the left.  The default for a new window is the 
    setting of this option for the FROM WINDOW.  The default for an existing 
    window is to ignore this option. 
9.  MINLENGTH specifies the minimum length for this window in lines.  MINWIDTH 
    specifies the minimum width for this window in columns. 
10. NAME specifies the logical device name for the stream being defined.  This 
    can be an explicit stream number (e.g., UC02) or a symbolic stream name 
    (e.g., UCAA).  For the latter, an unused stream number is assigned.  The 
    same stream name can be used in subsequent frames to refer to this window 
    without having to assign a specific number.  If the specified stream is 
    already defined, the existing window is used; otherwise, a new window is 
    created for the new stream.  If NAME is omitted, a new window is created 
    using the next available UC stream number. 
11. OPTIONAL specifies whether or not the window size is permitted to drop 
    below MINWIDTH or MINLENGTH.  If so, the window is removed from the screen 
    when too small, but its context is maintained. 
12. PAGEHALT specifies whether or not output is to be suspended when the 
    window has been filled by lines of continuous output.  YES specifies that 
    output is to be halted until the user presses <CR>.  NO specifies that 
    output is to continue uninterrupted.  The default is NO for a menu window. 
    For an interaction window, the default is the setting in effect when the 
    dialog was started. 
13. POSITION specifies the portion of FROM WINDOW that the new window is to 
    occupy. This is ignored for existing windows. The options are TOP, BOTTOM, 
    LEFT, and RIGHT.  The default is TOP. 
14. RHTBRDR specifies whether or not to reserve space at the right to separate 
    this window from the one to the right.  The default for a new window is 
    the setting of this option for the FROM WINDOW.  The default for an 
    existing window is to ignore this option. 
15. SCROLL specifies whether or not the window is to be treated as a 
    continuous scrolling device.  YES specifies that when the cursor reaches 
    the bottom line it stays there, and each new line causes prior lines to 
    scroll up.  NO specifies that after the cursor reaches the bottom line, it 
    wraps back to the top line and travels down the screen again.  The default 
    is NO for a menu window.  For an interaction window, the default is the 
    setting in effect when the dialog was started. 
    When a window is cleared, the cursor is placed on the bottom line if 
    scrolling is enabled, and on the top line if scrolling is disabled.  Note 
    that some terminals do not support scrolling, and others allow it only 
    when the screen is not split into multiple windows. 
16. TOPBRDR specifies whether or not to reserve space at the top to separate 
    this window from the one above it.  The default for a new window is the 
    setting of this option for the FROM WINDOW.  The default for an existing 
    window is to ignore this option. 
17. VBRDRCHR specifies the single ASCII character to be used to mark the 
    vertical border space(s).  The default for a new window is the setting of 
    this option for the FROM WINDOW.  The default for an existing window is to 
    ignore this option. 
18. VBRDRSIZ specifies the size in columns of the vertical border space(s) 
    (LFTBRDR and RHTBRDR).  The default for a new window is the setting of 
    this option for the FROM WINDOW.  The default for an existing window is to 
    ignore this option.  If set to a value greater than 1, all border columns 
    except the one closest to the edge are filled with blanks. 
19. WIDTH specifies window width, including any borders, as an absolute number 
    of columns.  WIDTH is ignored for new windows with a POSITION of TOP or 
    BOTTOM.  The default is zero, which results in no change to an existing 
    window, but is interpreted to mean all but one column of the FROM WINDOW 
    for a new window. 
20. WRAPPAGE specifies how the screen is to be cleared when the cursor wraps 
    from the bottom to the top line of the window.  This option only applies 
    to streams that specify SCROLL=NO.  YES specifies that the window is to be 
    erased one line at a time, such that the line below the cursor is always 
    blank.  NO specifies that the entire window is to be erased after using 
    the bottom line.  The default is the setting in effect when the dialog was 
    started. 
21. Each window defined creates a new logical stream.  Since there is a limit 
    of 15 logical streams of all types that can be defined at any one time, 
    care must be exercised in deciding when to define a new window.  It is 
    usually not a good idea to redefine the windows for each frame, 
    particularly if frames can be nested more than a few levels.  Whenever 
    possible, frames should be designed to use the same windows as the 
    invoking frame. 
22. If more than one option is specified, the option list must be enclosed in 
    parentheses. 
00001
Syntax: 
W[RITE] [ #file-number ] expression [ K[EY] [ IS | = ] expression ] 
Parameters: 
file-number    specifies an internal file number from 1 to 9. 
expression    enter: HELP (ADAPT) EXPRESSIONS 
Description: 
The WRITE statement writes a record to a disk file. 
Rules: 
1.  The file-number should be the same as the number specified when the file 
    was opened.  An error occurs if the file is not open.  If specified, the 
    file-number must be prefixed with a pound sign (#).  If omitted, #1 is 
    assumed. 
2.  The string value of the first or only expression supplies the contents of 
    the record that is written.  The record is written with no VFC. 
3.  For files with CONSECUTIVE organization, the KEY clause is normally 
    omitted.  In this case, the record is written at the current position in 
    the file.  The initial position in a file opened to allow writing is at 
    the end.  Thereafter, the current position is just after the last record 
    accessed.  If a key clause is provided, it must be the number of the 
    record in the file to be written.  Writing to anywhere except the end of 
    the file implicitly deletes the prior contents of the file from that point 
    on. 
4.  For files with KEYED organization, the KEY clause is normally supplied to 
    specify the key of the record to be written.  If a string key is given, it 
    specifies the value of the key for the new record.  If a record already 
    exists with that key, it is replaced; otherwise, a new record is added to 
    the file.  If a numeric key is given, it must be a positive number not 
    exceeding the number of records in the file.  The record at that position 
    in the file is replaced.  If the KEY clause is omitted and the last 
    operation performed on the file was a READ, the record that was read is 
    replaced. 
5.  If the operation is unsuccessful for any reason, the appropriate CP-6 
    error code is saved where it can be accessed by the $ERROR function.  If 
    the operation is successful, $ERROR is set to zero. 
Examples: 
WRITE REC 
writes the contents of the REC variable to file number 1 (the default). 
Assuming the file was created as a CONSEC file and no statement has reset the 
file position, the record is appended to the file. 
WRITE #2 NEWID, KEY IS 'ID' 
writes a record consisting of the value of the NEWID variable to file number 2 
with a key of ID. 
00002
00001
XT_SERVICES
The first argument on all dialog manager service calls is the dialog manager's 
parameter block (XT_PARAM).  All other arguments are optional character 
strings.  If specified, they can be provided either as arguments on the 
service calls or via fields in the parameter block.  There is an address and a 
length field in XT_PARAM for each optional argument.  If an argument is 
present on a service call, its address is copied to the corresponding XT_PARAM 
field.  Argument addresses can also be presupplied in XT_PARAM.  In either 
case, a length must be provided for each argument specified. 
Argument lengths can either be preset in XT_PARAM or obtained from the calling 
sequence.  If an argument address is specified and the corresponding length 
field in XT_PARAM is zero, the way the length is obtained depends on the 
language used to make the call.  For calls from languages that generate 
argument descriptor lists (COBOL85, FORTRAN, and Pascal), the length is taken 
from the argument descriptor.  Languages that do not generate descriptor lists 
on calls (C and PL-6) must pass arguments as TEXTC strings if their lengths 
are not presupplied in XT_PARAM.  (A TEXTC string is one whose first byte 
contains the number of characters in the string that follows.) 
Although these rules sound complex, they should serve to simplify calls to the 
dialog manager from any language by making the best use of the capabilities of 
each language.  See sections on individual language interfaces later in this 
appendix for additional information. 
Syntax: 
CALL XT_ENTER(XT_PARAM [, [script] [, [frame] [,ibuf]]] );      [PL-6] 
CALL XT_ENTER(XT_PARAM [, [script] [, [frame] [,ibuf]]] )       [FORTRAN] 
XT_ENTER(XT_PARAM [, [script] [, [frame] [,ibuf]]] );           [C] 
CALL "XT_ENTER" USING XT-PARAM [, [script] [, [frame] [,ibuf]]] [COBOL] 
Parameters: 
XT_PARAM     is the dialog manager's parameter block. 
script     is the fid for the script file containing the initial frame.  If 
omitted, the current setting of the ADAPT$SCRIPT DCB is used. 
frame     is the name of the initial frame for the dialog.  If omitted, the 
MAIN frame in the designated script file is used. 
ibuf     is the initial contents of the dialog input buffer.  If omitted, the 
input buffer is initially empty. 
Description: 
XT_ENTER starts dialog execution.  It allocates the dialog workspace, reads 
the initial script frame, and does other necessary setup.  XT_ENTER merely 
initiates dialog mode.  Subsequent calls to XT_READ are needed to actually 
return commands.  Once dialog mode is initiated, the program continues to run 
in dialog mode until the initial frame terminates. 
Syntax: 
CALL XT_INIT(XT_PARAM);                                         [PL-6] 
CALL XT_INIT(XT_PARAM)                                          [FORTRAN] 
XT_INIT(XT_PARAM);                                              [C] 
CALL "XT_INIT" USING XT-PARAM                                   [COBOL] 
Parameters: 
XT_PARAM     is the dialog manager's parameter block. 
Description: 
XT_INIT sets all fields in the XT_PARAM block to their default values.  It is 
most useful for Pascal programs, since Pascal does not support data 
initialization. 
Syntax: 
CALL XT_READ(XT_PARAM [, [buffer] [, prompt ]] );               [PL-6] 
CALL XT_READ(XT_PARAM [, [buffer] [, prompt ]] )                [FORTRAN] 
XT_READ(XT_PARAM [, [buffer] [, prompt ]] );                    [C] 
CALL "XT_READ" USING XT-PARAM [, buffer [, prompt ]]            [COBOL] 
Parameters: 
XT_PARAM     is the dialog manager's parameter block. 
buffer     is a buffer in which the command is returned.  If omitted on the 
call, a command buffer must be specified by the corresponding XT_PARAM fields. 
prompt     is the terminal input prompt that would be issued if a dialog were 
not in progress.  If omitted, the default prompt of an asterisk (*) is 
assumed. 
Description: 
XT_READ returns a command line to the program.  If dialog execution is in 
progress, the command is built by executing the dialog.  Otherwise, a normal 
sequential read is done through the DCB specified by XT_PARAM.INDCB. 
If a call to XT_READ results in normal termination of dialog mode (i.e., if 
the initial frame exits), the routine returns with the XT_PARAM.EOD flag set 
and an error code of %E$XT#EOD (End Of Dialog).  The calling program should 
expect this to happen and take appropriate action when it does.  Any other 
error code indicates an unexpected fatal error.  Dialog mode is always 
terminated before returning a fatal error. 
The prompt supplied on the XT_READ call is restored when dialog mode is 
terminated.  It is also displayed on issued commands echoed by the dialog. 
	hese are the only uses made of this parameter.  When XT_READ is called in 
non-dialog mode, the proper prompt is assumed to have already been 
established.  If the XT_PARAM.PROMPT_VFC flag is set, the first character of 
the prompt is treated as a VFC character. 
The command buffer supplied by XT_READ is also used for IBEX commands issued 
by the dialog.  Although dialogs can issue continued commands to programs that 
support them, IBEX commands are limited to the length of the command buffer 
supplied by the caller. 
Syntax: 
CALL XT_RESTART(XT_PARAM);                                      [PL-6] 
CALL XT_RSTART(XT_PARAM)                                        [FORTRAN] 
XT_RESTART(XT_PARAM);                                           [C] 
CALL "XT_RESTART" USING XT-PARAM                                [COBOL] 
Parameters: 
XT_PARAM     is the dialog manager's parameter block. 
Description: 
XT_RESTART resumes dialog execution if the program was invoked to run under 
the control of a dialog.  It does nothing and returns normally if the program 
was not invoked to run under a dialog.  For a programs to be able to come up 
running in dialog mode, it must call XT_RESTART before the first call to 
XT_READ.  An error return from XT_RESTART indicates a fatal error in 
attempting to restart dialog execution. 
    The XT library services constitute the ADAPT dialog manager.  A program 
    using these services can get its command input from a dialog as well as 
    from command lines typed directly by the user.  A simplified interface to 
    these services is available to programs that get their command input via 
    standard CP-6 GETCMD library services. 
    For a list of XT services, enter: ??.  For detail information on each 
    service, enter: HELP (ADAPT) service. 
  Service        Description 
  XT_ENTER 
                 Enters dialog mode by initializing the dialog workspace. 
  XT_INIT 
                 Initializes dialog manager parameter block to all default 
                 values. 
  XT_READ 
                 Returns a command line.  If dialog mode has been entered, the 
                 command is obtained from the dialog; otherwise, it is read 
                 directly from the input stream. 
  XT_RESTART 
                 Restarts dialog mode if the program was invoked to run under 
                 a dialog. 
00001
00002
00003
00004
