Syntax 1: 
BASIC [fid1] [{ON|OVER}[fid2][,fid3]] 
Parameters 1: 
fid1    is a file of BASIC source statements and/or commands, which is loaded 
into the workspace as if a LOAD command were issued immediately after entering 
BASIC.  If unspecified, no program is loaded and the workspace is empty. 
fid2    is the default continuation workspace. 
fid3    is the destination for listing output. 
Description 1: 
The BASIC processor is entered from IBEX. 
Syntax 2: 
BASIC {ON|OVER} fid 
Parameters 2: 
ON    specifies that fid is a newly-named file.  If fid already exists, the 
command aborts. 
OVER    specifies that any existing file identified by fid is to be replaced. 
fid    is a BASIC workspace file that is created if an abnormal exit is taken 
from BASIC. 
If ON or OVER is not specified, BASIC creates a default name consisting of 
"BASIC:" followed by the users logon account name. 
Description 2: 
A variation of the BASIC command preserves the workspace in the event of an 
abnormal exit from the BASIC processor. 
Abnormal exits include line disconnections, operator aborts, monitor aborts, 
exceeded limits, etc.  If an abnormal exit occurs, BASIC can be reentered and 
the saved workspace reloaded via WLOAD. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1994 
  ************************************************************** 
These functions are: ABS, DET, EXP, INT, LGT or LOG10, LOG, LTW or LOG2, MAX, 
MIN, MOD, RND, SGN, and SQR. 
  Function     Meaning            Arg. Domain      Range Result   Inaccuracies 
ABS(expr)    The absolute       Any practical    0 to 10E+152   None. 
             value of expr.     representable 
                                numeric values. 
DET(aname)   Returns the        Any matrix.      Limited by     None. 
             determinant of a                    memory 
             matrix.                             allocation. 
EXP(expr)    Exponential of     Minus machine    0 to about     Accuracy 
             expr (e**expr),    infinity to      1.68900E+152   decreases as 
             where e is the     +88.0229.                       exponent 
             base of natural                                    increases. 
             logarithms. 
INT(expr)    Integer function   any practical    10E-156 to     None. 
             of expr (largest   positive value   10E+152 
             integer not 
             greater than 
             expr).  Note 
             that INT(-A) = 
             -INT(A)-1. 
LGT(expr)    The mathematical   Any practical    -156 to +152   Neighborhood 
   or        common log (base   positive value                  of 1. 
LOG10(expr)  10) function. 
LOG(expr)    The mathematical   Any practical    -89 to 89      Neighborhood 
             natural            positive value                  of 1. 
             (Napierian) 
             logarithm 
             function with 
             argument expr. 
LTW(expr)    The mathematical   Any practical    -123 to 130.   Neighborhood 
   or        log to the base    positive value                  of 1. 
LOG2(expr)   two of argument 
             expr. 
MAX(expr,    Returns the        -10E+152         -10E+152       None. 
expr,...)    largest value      to 10E+152       to 10E+152 
             among the 
             expressions. 
MIN(expr,    Returns the        -10E+152         -10E+152       None. 
expr,...)    smallest value     to 10E+152       to 10E+152 
             among the 
             expressions. 
MOD(expr1,   The mathematical   The difference   -10E+152       Accuracy 
expr2)       function           between expr1    to 10E+152     diminished for 
             representing       and expr2                       large ratio of 
             modulo             should yield                    expr1 to expr2.
             arithmetic.        at least 6 
             Result =           significant 
             remainder of       digits after 
             expr1/expr2.       evaluation of 
                                the function. 
RND          Pseudo-random      No argument.     0 <= result    None. 
             number function.                    < 1 
             See the 
             RANDOMIZE 
             statement for 
             control over 
             random 
             sequences. 
SGN(expr)    Signum (sign) of   Any numeric      -1 for expr    None. 
             expr.              value            < 0.  0 for 
                                                 expr = 0. 
                                                 +1 for expr 
                                                 > 0. 
SQR(expr)    Non-negative       Non-negative     0 to 10E+76    None. 
             square root of     value 
             expr. 
There are five types of alphanumeric replacement fields:  simple, extended, 
left-justified, right-justified, and centered.  All five are used to format 
character strings; if a numeric variable is assigned to an alphanumeric 
replacement field, an error results.  Alphanumeric replacement fields consider 
all characters as filling one print column.  Thus, if a string contains 
backspaces, tabs, linefeeds, etc., the positioning of the string may be 
destroyed. 
See also:  SIMPLE, EXTENDED, LEFT_JUSTIFIED, RIGHT_JUSTIFIED, and CENTERED. 
    The meaning of an array reference is dependent upon the type of statement 
    in which the reference occurs.  In DIM statements, references are always 
    subscripted and the subscript values set the dimensions of the arrays.  In 
    MAT statements, references either access all the values of an array, or 
    assign values to all elements of an array.  In MAT statements that assign 
    values, subscripts are used to set current dimensions for the target 
    array.  CHANGE statements can reference values from a numeric vector with 
    an optional subscript which indicates a subset of the values to be 
    converted.  A CHANGE statement can also assign values and set the current 
    dimensions of a vector.  However, a vector cannot be changed to a matrix 
    or vice versa.  (See the DIM, MAT, and CHANGE statements for a detailed 
    explanation of these features.) 
    In all other statements, array references are always subscripted, and the 
    subscripts select a single element of the array.  If a reference assigns a 
    value to an element of an array that has a current value, the assignment 
    replaces the existing value and leaves other elements undisturbed.  A 
    single element assignment must fall within the current dimensions of the 
    array. 
    Array values are available to direct statements, and can be shared between 
    programs, but they are subject to the constraints imposed by explicit and 
    implicit changes in the use of dimension and array names.  Rules for 
    retaining array data are described in the DIM statement.  In general, if 
    two programs use the same array name in the same session, but the second 
    program neither initializes or clears arrays nor sets dimensions, then the 
    data values can be shared. 
Syntax: 
AUT[O]  [n][,m] 
Parameters: 
n    is the starting line number.  The default is 10. 
m    is the increment.  The default is 10. 
Description: 
The AUTO command causes automatic line numbering.  If an error is made in 
typing a statement, the line number is repeated.  Typing an unaccompanied 
carriage return terminates the operation. 
00002
00001

Syntax: 
BAT[CH] fid [, ["options"],["resource"],["cmnds"]] 
Parameters: 
options    are the !JOB card options to use, such as priority.  The defaults 
are the system defaults. 
resource    is an optional resource card.  The defaults are the system 
defaults. 
cmnds    are the commands to execute after the fid is loaded into BASIC.  The 
default is "RUNH". 
Each quoted item may be a list.  Note that the quotes are required. 
Description: 
The BATCH command enters BASIC jobs into the batch stream.  If no command is 
specified, a RUNH command is inserted, following the command to load the 
specified file. 
Example: 
    BATCH SORT,"PRIO=7,WSN=LOCAL","MEM=100,TIME=1","LIST,FAST" 
00002
00003
00001
Syntax: 
[line] BREAK {ON|OFF}[line[,line]...] 
Parameters: 
ON    sets breakpoints at the specified line numbers, halting program 
execution at each indicated line before that line is executed.  At each 
breakpoint the following message is printed: 
    BREAK AT xxxxx 
The xxxxx value is the flagged line number.  The user may then issue a PROCEED 
or a direct GOTO statement to resume execution.  A programmed breakpoint 
remains set until the indicated statement is removed or altered.  BREAK ON 
with no line list sets breakpoints at all program lines. 
OFF    resets break control.  BREAK OFF with no line list removes all break 
control assignments.  If a line list is included, only the indicated 
breakpoints are removed. 
Description: 
The BREAK statement halts program execution at specified line numbers. 
Usage Notes: 
Various direct statements and BASIC commands can be executed while a program 
is suspended between a BREAK and a PROCEED.  However, any program modification 
occurring while the program is in suspended execution causes an implicit 
recompile. 
Examples: 
    100 BREAK ON 300,400,550 
         . 
         . 
         . 
    355 BREAK OFF 400 
         . 
         . 
         . 
    5000 BREAK OFF 
Line 100 sets breakpoints at the indicated lines.  Line 355 removes the 
breakpoint set at line 400, while line 5000 removes all break control 
assignments.  A BREAK keyin from the user's console will still suspend program 
execution. 
00002
00004
00001
00003
Syntax: 
BUI[LD] [n][,m] 
Parameters: 
n    is the starting line number.  If n exists in the command file, it is 
replaced.  The default is 10. 
m    specifies the increment for the pseudo-line numbers.  The default is 10. 
Description: 
The BUILD command creates a file of embedded commands and direct statements. 
The prompt for BUILD operations is a line number followed by a colon.  BUILD 
is terminated when an unaccompanied carriage return is issued. 
00002
00001
Syntax: 
BYE 
Description: 
The BYE command closes all open files, releases queue entries, and then ends 
the batch operation or terminal session.  The BYE command is a synonym for the 
OFF command. 
00001
Syntax: 
CAL[C] 
Description: 
The CALC command allows user to enter calculator mode where expressions are 
taken as implying direct print. 
The only way to exit CALC mode is to type:  END.  This is the only use for the 
END command. 
00001
Syntax: 
CAT[ALOG] [[ACCT = account|[,ALL]]|[ALL]] 
Parameters: 
account    specifies the account to be listed.  The default is the user's 
directory account. 
ALL    specifies that all file types are to be listed. 
Description: 
The CATALOG command lists either the BASIC created files or all the files, 
regardless of type.  The default account is the current account. 
Examples: 
When the CATALOG command is entered by the owner of a file, 
the following is displayed: 
WED FEB 10  '84  10:20:37.68     LISTING OF ACCOUNT: XYZ 
ORG    TYPE  GRAN    REC     LAST MODIFIED               NAME 
___    ____  ____    ___     _____________               ____ 
CON    SB       1      2     FEB 14 '84 06:18:03.20    S FILENAME 
The letter "S" between the LAST MODIFIED and NAME columns indicates a sealed 
workspace.  If someone other than the owner of the sealed file enters the 
CATALOG command, the following is displayed: 
WED FEB 10  '84  10:20:37.68     LISTING OF ACCOUNT: XYZ 
ORG    TYPE  GRAN    REC     LAST MODIFIED               NAME 
___    ____  ____    ___     _____________               ____ 
CON    SB  *** EXECUTABLE ONLY ***                     S FILENAME 
The letter "S" is also displayed to indicate a sealed workspace, but other 
information is not listed.  The following examples demonstrate different ways 
to list information using the CATALOG command: 
    CAT                   lists all the BASIC created files (SB, 
                          WB types) in the current account. 
    CAT ACCT=NGBASIC      lists the BASIC created files (SB,WB 
                          types) in account NGBASIC. 
    CAT ALL               lists all files in the current account. 
    CAT ACCT=NGBASIC,ALL  lists all files in account NGBASIC. 
00002
00003
00001
Syntax: 
'C[C...] 
Description: 
These fields are represented by an apostrophe followed by one or more C 
characters. 
The apostrophe and the C's are replaced by characters from the string 
variable.  If the variable is shorter than the field, blanks are appended 
alternately to the left and right to provide a centered representation.  If 
the variable is longer than the field, characters to the right of the field 
are truncated. 
Examples: 
    100 LET E$="IRV" 
    200 LET F$="RICHARD" 
    300 PRINT USING 400, E$, F$ 
    400 : 'CCCC 
Line 300 prints the message: 
     IRV 
    RICHA 
Note that E$ is centered in the field, but that F$ has been truncated on the 
right. 
00001
00002
Syntax: 
CFE[TCH]  fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The CFETCH command performs a clear and fetch of a non-line-numbered file. 
00002
00001
Syntax: 
[line] CHAIN str-expr [,line] 
Parameters: 
str-expr    must specify a file identifier which is only a BASIC source 
program and the user must have execute or read access to that file. 
line    specifies an optional line number at which execution is to start. 
Description: 
The CHAIN statement allows a task too large for processing by a single BASIC 
program to be accomplished by a sequence of two or more programs. 
Usage Notes: 
When a CHAIN statement is executed, the executing program is terminated and 
the new program is compiled.  Existing open data files remain open and are 
unchanged by CHAIN.  If chained programs are not to share data files, the 
program containing the CHAIN statement should close its files prior to 
executing CHAIN. Existing data is available, subject to restrictions on 
changed designation and dimensions on array data.  If data is not to be 
shared, either the terminating or the new program should include statements to 
clear old data or initialize new.  (See the DIM and CLEAR statements.) 
Examples: 
    1 REM    PROGRAM NAME=MYFILE 
    90000 LET B$="YOURFILE.YOURACCT.SECRET" 
    90010 CHAIN B$,100 
                . 
                . 
                . 
     100 REM    THIS IS THE CHAINED PROGRAM 
     15000 CHAIN "MYFILE" 
Line 90010 terminates the executing program, loads and compiles the BASIC 
source program YOURFILE, existing in the account YOURACCT, with the password 
SECRET, and starts execution of YOURFILE at line 100.  Line 15000 of the new 
program returns control to MYFILE. 
00002
00004
00001
00003
Syntax 1: 
[line] CHANGE aname[(num-expr1)] TO str-var [BIT num-expr2] 
Parameters: 
aname    represents a numeric vector.  If the vector name is not qualified by 
an index expression, the current dimension of the vector is used. 
num-expr1    is a value between 0 and the number of elements currently present 
in the vector (rounded to an integer).  This value establishes the number of 
elements to be converted.  Each numeric value of the vector is converted to 
string form by rounding to an integer, using the right-most number of bits 
specified by num-expr2. 
num-expr2    specifies a value from 1 to 9 that is used to internally format 
elements of the string array.  The default is 9.  The BIT option allows the 
user to pack small integer numeric values.  Normally num-expr2 is 9, and the 
character string created by a CHANGE statement is a conventional character 
string using the standard internal representation of 9 binary bits per ASCII 
character.  If num-expr2 is specified via the BIT option, the result is a 
pseudo-character string, without the padding of leading zeros usually found in 
internally formatted ASCII characters.  Since such strings have no padding, 
they are unreadable unless unpacked using the reverse process.  Care must be 
taken if the BIT option is used.  Strings created via the BIT option take up 
significantly less data space than those stored by conventional methods. 
A run-time error is printed if the data value from the numeric vector will not 
fit within the specified number of bits. 
Syntax 2: 
[line] CHANGE str-expr TO aname [BIT num-expr] 
Parameters: 
str-expr    is any string expression. 
aname    is the name of an array. 
num-expr    is a numeric expression. 
The characters or pseudo-characters in the string expression are converted to 
integer values corresponding to their position (if true characters) in the 
ASCII collating sequence.  The values must be assigned to a numeric vector; 
the current dimension of the vector is set by the number of items in the 
string.  If BIT is specified and its value is other than 9, the string is 
accessed as pseudo-characters.  The BIT option is used to decode vectors 
packed via the BIT option in a numeric to string conversion CHANGE statement. 
Description: 
The CHANGE statement provides a means of conversion between character strings 
and numeric vectors composed of their numeric values in the ASCII character 
set.  An option within CHANGE provides a means of packing small integer 
numeric values into pseudo-character strings and retrieving those values.  The 
CHANGE statement, like the various MAT statements, processes the entire vector 
rather than each specific element.  The CHANGE statement has two basic 
formats, numeric to string, and string to numeric. 
CHANGE can be used to create a superset of the ASCII character set and the 
full range of special characters.  However, the processing of such special 
characters on device I/O is subject to the characteristics of the operating 
system. 
Examples: 
    100 CHANGE "0123456789" TO BANDERSNATCH 
    200 CHANGE BANDERSNATCH TO BANDERSNATCH$ 
    300 CHANGE BANDERSNATCH(6) TO JABBERWOCK$ BIT 6 
    400 CHANGE BANDERSNATCH$ & SWORD$ TO FRUMIOUS 
Assuming BASE=1,: line 100 creates a vector A with 
    BANDERSNATCH(1) = 48 
    BANDERSNATCH(2) = 49 
            . 
            . 
            . 
    BANDERSNATCH(10) = 57 
The vector BANDERSNATCH is dimensioned to length 10.  Line 200 creates 
BANDERSNATCH$ containing the string 0123456789.  Line 300 creates a 
pseudo-character string in JABBERWOCK$ containing six 6-bit pseudo-characters. 
Only the user's application is cognizant of the special nature of JABBERWOCK$. 
Line 400 changes the string formed by a concatenation of BANDERSNATCH$ and 
SWORD$ to the numeric vector FRUMIOUS. 
00003
00004
00001
00002
CLEAR_COMMAND
Syntax: 
[line] CLEAR NUMERIC ARRAYS [aname[,aname]...] 
[line] CLEAR NUMERIC SCALARS [var[,var]...] 
[line] CLEAR STRING ARRAYS [aname$[,aname$]...] 
[line] CLEAR STRING SCALARS [var$[,var$]...] 
[line] CLEAR DATA 
Parameters: 
aname    is the name of an array. 
var    is a simple variable. 
The variable names used in CLEAR STRING statements must be string variables, 
and the variable names used in CLEAR NUMERIC statements must be numeric 
variables. 
If no variable names are included, the statement clears the entire class of 
data.  If one or more variable names are included, the statement clears only 
the specified items of data.  When references to simple variable names are 
cleared, the names have zero (numeric) or null (string) value.  When array 
references are cleared, the arrays are set to size zero with no values. 
Description: 
The CLEAR statement erases data selectively from the working storage area 
prior to execution or other actions. 
The CLEAR DATA statement clears all string and numeric arrays and variables in 
the current BASIC workspace.  No workspace parameters (e.g., precision, array 
base, etc.) nor program source lines are affected.  The CLEAR DATA statement 
is a shorthand specification for the following four commands:  CLEAR NUMERIC 
ARRAYS, CLEAR STRING ARRAYS, CLEAR NUMERIC SCALARS, CLEAR STRING SCALARS. 
Usage Notes: 
CLEAR statements are not executable.  Like the DIM statement, CLEAR statements 
take effect as they are reached during program compilation.  Thus, a CLEAR 
statement that references an array must be assigned a lower line number than 
the corresponding DIM statement that dimensions the array.  This allows BASIC 
to release space before the DIM statement seeks additional data space. 
Examples: 
    100 CLEAR NUMERIC ARRAYS 
    110 CLEAR STRING ARRAYS A$,B$,W$,X$,Z$ 
    120 CLEAR STRING SCALARS A1$,A2$,A3$ 
Line 100 clears all the current numeric arrays.  Lines 110 and 120 selectively 
clear the indicated string arrays and string scalars. 
00002
00004
00001
00003
Syntax: 
CLE[AR] 
Description: 
The CLEAR command clears all user context, erasing everything in the working 
storage area, including variable values, the object program, and the source 
program.  All open data files are closed and all queued items are dequeued. 
00001
Syntax: 
CLO[AD] fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The CLOAD command combines the functions of the CLEAR and LOAD commands.  The 
CLOAD command clears the working storage environment and copies the specified 
source program file into working storage. 
00002
00001
Syntax: 
[line] CLOSE {stream|ALL} 
Parameters: 
stream    is an expression (rounded to an integer) that represents a valid 
stream number. 
ALL    specifies that all currently open I/O streams are to be closed. 
If stream is specified, the indicated I/O stream is closed.  If the stream is 
open to a file, it is dequeued and saved.  If the stream is not open, no 
action is taken.  The ALL form is convenient if the program does not need to 
access any streams which may be open. 
Description: 
The CLOSE statement is used to close and save currently opened data files 
assigned to I/O streams. 
Examples: 
    100 CLOSE 2 
    500 CLOSE ALL 
Line 100 closes and saves the file associated with stream 2.  Line 500 closes 
and saves all currently open files. 
00002
00003
00001
Syntax: 
COD[ESAVE] {ON|OFF} 
Parameters: 
ON    specifies that the results of the syntax pass are saved.  The default is 
ON. 
OFF    specifies that nothing is to be saved.  Less memory is used with OFF 
but program compilation is slower. 
Description: 
The CODESAVE command allows the user the option of whether or not to save the 
code generated during the syntax pass over the source. 
00002
00001
  Command        Description 
AUTO           Automatic line numbering. 
BASIC          Invokes the BASIC processor. 
BATCH          Submits a batch job. 
BUILD          Builds command file. 
BYE            Logs off system. 
CALC           Enters calculator mode. 
CATALOG        Lists files. 
CFETCH         Clears and loads command file. 
CLEAR          Clears user context. 
CLOAD          Clears and retrieves source program. 
CODESAVE       Allows user to save or not save code. 
DELETE         Deletes source program statement. 
DFILE          Deletes source program file. 
END            Returns control from CALC mode to BASIC. 
FAST           Compiles and executes. 
FASTER         Compiles and executes, code efficient. 
FASTEST        Compiles and executes, code optimized. 
FETCH          Loads command file. 
GO             Resumes execution. 
GOODBYE        Logs off system. 
HELP           Obtains information on BASIC. 
LAST           Lists highest source program statement. 
LIST           Lists source program statement. 
LOAD           Retrieves source program. 
NEW            Creates new environment. 
NRESAVE        Resaves command file. 
NSAVE          Stores command file. 
NSEAL          Stores and seals command file. 
OFF            Logs off system. 
Q              Returns to command processor. 
REENTER        Executes compiled program. 
RENAME         Renames environment. 
RENUMBER       Renumbers source program. 
RESAVE         Stores and replaces source program. 
RR             Reread. 
RUN            Compiles and executes, with checking. 
SAVE           Stores source program. 
SAVE ON        Stores source program. 
SAVE OVER      Stores and replaces source program. 
SEAL           Stores and seals source program. 
SEQUENCE       Assigns pseudo-line numbers. 
SHOW           Displays information. 
START          Executes compiled program. 
STEP           Permits execution of one or move lines in a BASIC program. 
SYS            Returns to command processor. 
UNSAVE         Deletes source program file. 
WEAVE          Weaves source programs. 
WFSAVE         Saves the workspace file. 
WRESAVE        Stores and replaces environment. 
WSAVE          Stores environment. 
WSEAL          Stores and seals environment. 
WLOAD          Loads environment. 
X              Returns to command processor. 
XREF           Produces cross reference listing. 
The evaluation of complex expressions can be illustrated by assuming the 
equation: 
    -A(I,J(K+2))**B-C/D*SIN(X-5) 
1.  Evaluate the simple expression K+2, and locate the element of vector J. 
    (For purposes of illustration, call this element V1.) 
2.  Using the values of I and V1, locate the element of matrix A and 
    exponentiate using the value B.  (Call the result V2.) 
3.  Evaluate the simple expression C/D.  (Call the result V3.) 
4.  Evaluate SIN(X-5).  (Call it V4.) 
5.  Evaluate the sequence V3*V4.  (Call it V5.) 
6.  Evaluate -V2-V5. 
NOTE:  An expression is reduced and evaluated from left to right at compile 
time, but the order of evaluation can make a difference in the numerical 
result.  For example, A + (B+C) is not necessarily the same as (A+B) + C due 
to the computer's limited precision. 
The following example illustrates how an expression can be evaluated 
differently depending on placement of parentheses: 
    10 REM WHAT DOES THIS DO? 
    20 LET I=2 
    30 FOR J=1 TO 5 
    40     LET I=I + (-1 ** J) 
    50     PRINT I; 
    60 NEXT J 
    65 PRINT 
    70 END 
The standards document, ANS X3.60 requires that -2**B be interpreted as 
-(2**B), therefore the expected result might be: 
    1 2 1 2 1 
The actual result is: 
    1 0 -1 -2 -3 
BASIC interprets line 40 as: 
    40     LET I=I + (0 - 1 ** J) 
The solution is to place parentheses around -1: 
    40     LET I=I + ((-1) ** J) 
Syntax: 
line DEF FNvariablename[(parameter[,parameter]...)] 
line[s] definition-block 
[line FNvariablename=expr] 
[line [s] definition block continued] 
line FNEND 
Parameters: 
variablename    identifies the function.  If a "$" is included, the function 
is a string function and returns a string result; otherwise, the function is 
numeric. 
parameter    is any simple variable name, such as B1, C, X, etc. 
definition-block    is a set of BASIC statements with line numbers between the 
DEF statement which begins the function definition, and the FNEND statement 
that ends it. 
FNvariablename=expr    is a dummy result name that defines that value that 
will be returned when the function is accessed elsewhere in the program. 
FNEND    is a statement that ends the multiple statement function definition. 
Description: 
Defines a function that is too long to fit on a single line. 
00002
00001
These functions are: ASC, SCR$, NUM$, STR$, and VAL. 
  Function      Meaning 
  ASC($expr) 
                Provides the ASCII numeric value of $expr where $expr is a 
                quoted ASCII character or a 2 to 3 letter abbreviation. 
  CHR$(expr) 
                Converts expr to its ASCII equivalent, where expr is a decimal 
                numeric value (rounded to an integer) greater than or equal to 
                0 and less than or equal to 511.  Note that expr is a decimal 
                value and not the octal representation of the character. 
  NUM$(expr) 
                Converts expr to string format, where expr is a numeric 
                argument.  For example: 
                   10 PRINT NUM$(1234) 
                produces a result of 1234. 
  STR$(expr[,field]) 
                Converts expr to string format, where expr is a numeric 
                argument, and field is an optional numeric replacement field. 
                If field is omitted, the resultant string is formatted and 
                rounded as if produced in a PRINT statement.  If field is 
                included, it must conform to the rules for numeric replacement 
                in the PRINT USING statement.  For example, the statements 
                    100 A = 12.5 
                    200 B$ = STR$(A,"$$#.##") 
                    300 PRINT B$ 
                produce a result of $12.50. 
                NOTE:  a trailing blank is not included in the resultant 
                string. 
  VAL($expr) 
                Returns the numeric value of $expr where $expr is a string 
                expression that represents a valid numeric. 
00001
00002
00003
00004
00005
Syntax: 
line DATA datum[,datum]... 
Parameter: 
datum    is either a quoted string constant or an unquoted text string.  An 
unquoted text string may represent a numeric constant or may be accessed as a 
text string. 
Description: 
The DATA statement defines the data accessed by the READ statement. 
Usage Notes: 
The following rules apply for DATA statements: 
1.  Each DATA statement must include at least one datum. 
2.  Empty unquoted text strings (a comma immediately following a comma) are 
    invalid. 
3.  An unquoted text string may not include internal quotation marks. 
4.  A text string datum containing a comma must be enclosed within quotation 
    marks. 
5.  An unquoted text string may include internal blanks.  Leading and trailing 
    blanks are ignored. 
6.  DELIMIT has no effect on DATA or record behavior. 
Data from all of the DATA statements in a program are collected into a 
single-data sequence, which is read from left to right within a DATA 
statement.  DATA statements may appear anywhere in a program.  During program 
execution, a pointer is maintained for READ statements to keep track of the 
last read datum.  Initially this pointer is set to the first element in the 
first DATA statement.  It is advanced by each READ access.  The data pointer 
can be manipulated via the RESTORE statement. 
If DATA statements are reached during program execution, they are skipped with 
no effect.  Note that direct (no line number) DATA statements are invalid. 
The determination of whether an unquoted text string represents a numeric 
value is made at execution time by the READ statement.  All DATA elements are 
stored as text strings at compilation time. 
Examples: 
    100 DATA 2.3,"2.3" 
    200 DATA 5 SEPT.,1977 
    300 DATA "TEXT","","MORE" 
Line 100 contains two elements.  The first may be read into either a string or 
a numeric variable.  The second must be read into a string variable.  Line 200 
contains two elements.  The first is the unquoted string starting with the 
character 5 and ending with the period.  The second is an unquoted text string 
which represents a single numeric value, and thus can be read into either a 
numeric or string variable.  Line 300 contains 3 text strings, the second of 
which is the valid form for an empty string. 
00002
00004
00001
00003
Syntax: 
DBEMPTY(str-expr) 
DBOWNER(str-expr) 
DBMEMBER(str-expr) 
DBTENANT(str-expr) 
Parameters: 
str-expr    must represent a set name. 
Description: 
These functions return a 0 or 1, depending on the status of the current 
record. 
Example: 
If the current record is a member of setname, then DBMEMBER returns a 1. 
00002
00003
00001
Syntax: 
[line] MAT aname = DBMEMBERINFO$(str-expr) 
Parameters: 
str-expr    is either the name of a set or a record. 
aname    is dynamically dimensioned to N by 3. 
Description: 
The first column indicates the sets or records that the supplied record or set 
may be a member of.  The second column contains "MANUAL" or "AUTOMATIC" to 
tell what the membership is.  The third column contains "OPTIONAL" or 
"MANDATORY" to tell another attribute of membership. 
00002
00001
Syntax: 
DBOWNERINFO$(str-expr1) 
   or 
[line] MAT aname = DBOWNERINFO$(str-expr2) 
Parameters: 
str-expr1    must be a set name.  The result returned is a string which is the 
name of the record which owns this set. 
str-expr2    must be a record name.  The result of that function are strings 
which are the names of the sets that this record may own. 
aname    is dynamically dimensioned. 
Description: 
This function returns the name of the record owning the set or the names of 
the sets that this record may own. 
00002
00001
Syntax: 
[line] DB FROM dbvar, basicvar 
Description: 
This function moves the specified data base item to a BASIC variable. 
00001
Syntax: 
[line] DB SUB sub-schema-name [,privacy-lock] 
Description: 
This must be the first I-D-S/II statement encountered in a BASIC session.  The 
statement takes effect immediately upon compilation.  If the user needs to do 
any SETs in order to access the data base, then this may be done in BASIC 
through the IBEX command. 
Examples: 
    IBEX "SET SSCHFILE SCHEMA_FILE.ACCOUNT" 
00001
00002
Syntax: 
[line] DB TO expr, dbvar 
Description: 
This function moves the result of the evaluated expression to the specified 
data base item. 
00001
Syntax: 
[line] DDIGITS num-expr 
Parameter: 
num-expr    is an integer number between 6 and 61.  The default is 14. 
Description: 
The DDIGITS statement specifies the decimal precision for decimal arithmetic 
operations utilizing decimal arithmetic functions. 
Example: 
    100 DDIGITS 61 
Means use 61 places of accuracy when utilizing decimal arithmetic functions. 
00002
00003
00001
DECIMAL_NUMERIC
These functions are: SUM$, DIF$, PROD$, QUO$, PLACE$, and COMP. 
  Function      Description 
  COMP (str-expr1,str-expr2) 
                Compares two decimal values represented in string form.  The 
                COMP function compares the two string expressions as though 
                they were decimal values, and returns -1 if str-expr1 is less 
                than str-expr2, 0 if strexp1 = str-expr2, and 1 if str-expr1 
                is greater than strexp2. 
  DIF$(str-expr1,str-expr2) 
                Produces the decimal difference of two string arguments.  The 
                DIF$ function works the same as the SUM$ function, except that 
                the result represents the difference of str-expr1 less 
                str-expr2. 
  PLACE$ (str-expr,num-expr) 
                Provides rounding for decimal values.  The PLACE$ function 
                rounds the decimal value represented by the string expression 
                to the number of digits specified by the numeric expression. 
                If the size of str-expr is already less than num-expr, 
                str-expr will not be modified.  If num-expr is 0, the string 
                is rounded to the nearest integer value.  If num-expr is 
                negative, the string is effectively multiplied by 10**num-expr 
                and a PLACE$ is done of the resultant string and zero. 
  PROD$(str-expr1,str-expr2[,num-expr]) 
                Produces the decimal product of two strings.  The PROD$ 
                function produces the decimal product of str-expr1 and 
                str-expr2.  The num-expr is an optional specification of the 
                number of digits to return in the result.  The default is the 
                value specified in the DDIGITS statement. 
  QUO$(str-expr1,str-expr2[,num-expr]) 
                Produces the decimal quotient of two string arguments.  The 
                QUO$ function produces the decimal quotient of the two string 
                expressions (str-expr1 divided by str-expr2) assuming both 
                string expressions represent valid numerics.  The num-expr is 
                an optional precision for the result that overrides the 
                DDIGITS value.  If the user divides by zero, a warning message 
                is issued. 
  SUM$(str-expr1,str-expr2) 
                Produces the decimal sum of two string arguments.  The two 
                string expressions must represent valid numeric forms that 
                BASIC normally accepts.  The function returns a string which 
                represents the decimal sum of the two strings. 
00001
00002
00003
00004
00005
00006
Syntax: 
#[#...]decimal-point[#...] 
Description: 
These fields are represented by pound signs with a decimal point included. 
A decimal field is a string of pound signs with a decimal point placed 
anywhere within the field.  The fractional values to the right of the decimal 
point are rounded and truncated to conform to the field.  If the field has n 
decimal places to the right of the decimal point, and the number assigned to 
the field has more than n significant digits, a rounding operation takes place 
at the n+1 digit.  Integer values are placed to the left of the decimal point, 
just as in an integer numeric field.  If the integer portion of the value is 
too large for the field including a minus sign for negative values, the field 
is filled with asterisks.  If the number contains less digits of significance 
than #'s to the right of the decimal, then zeros are appended. 
Examples: 
    100 LET X=4.56 
    200 LET Y=-45.6 
    300 LET Z=456 
    400 PRINT USING "###.#",X,Y,Z 
Line 400 generates: 
      4.6 
    -45.6 
    456.0 
Note that the fractional portion of X is rounded and truncated.  The following 
table illustrates various types of decimal numeric fields, combined with 
control characters (described below). 
The sequence of values -.1, 1.2, -12.34, 123.456, -1234.5678 is inserted into 
each field until the size of the number exceeds the size of the field, at 
which point a line of asterisks is printed. 
   ####.    $##.##    -#.###    +.##    ####.## 
      0.    $ -.10    - .100    -.10       -.10 
      1.    $ 1.20     1.200    1.20       1.20 
    -12.    ******    ******    ****     -12.34 
    123.                                 123.46 
   *****                                ******* 
00001
00002
Syntax: 
DEL[ETE] line-list 
Parameters: 
line-list    is defined as a list of line numbers and/or line ranges, 
separated by commas.  The three types of line ranges are the same as for the 
LIST command. 
Description: 
The DELETE command deletes specified lines or ranges of lines from the source 
program in working storage. 
Examples: 
    DELETE 150,800,1000- 
    DELETE -100 
The first command deletes line 150, 800, and all lines beginning with 1000 to 
the end of the program.  The second command deletes all lines from the 
beginning of the program to line 100. 
Usage Notes: 
Because a line deletion modifies the current source program, a compiled 
program in suspended execution is recompiled to reflect changes made by the 
DELETE command. 
00002
00003
00001
00004
Syntax: 
[line] DELIMIT[# stream,]str-expr 
Parameters: 
stream    is a numeric expression between 0 and 12 inclusive (rounded to an 
integer). 
str-expr    specifies from one to four of the following characters to be used 
as delimiters: 
    b      blank 
    "      quotation mark 
    $      currency symbol 
    &      ampersand 
    '      apostrophe 
    (      opening parenthesis 
    )      closing parenthesis 
    *      asterisk 
     +      plus sign 
    ,      comma 
    -      minus sign (hyphen) 
    .      period 
    /      slash 
    :      colon 
    ;      semicolon 
    <      less than sign 
    >      greater than sign 
    =      equal sign 
If the stream value is either zero or omitted, the DELIMIT statement pertains 
to terminal or specified input stream.  input via the INPUT statement.  If the 
stream value (after rounding) is from 1 to 12, the statement applies to the 
indicated I/O stream for file INPUT# statements. 
If the blank character is designated as a delimiter, any number of consecutive 
blanks are treated as a single delimiter. 
Description: 
The DELIMIT statement assigns a character or characters as delimiters (in 
place of the default comma) which separates data elements in lines or records 
of input data. 
Example: 
    100 DELIMIT ", ;:" 
    500 INPUT A,B,C,D 
Line 100 sets terminal input delimiters to include the comma, blank, 
semicolon, and colon.  The statements make the following input reply valid: 
    ?100:200;300    600 
This reply assigns the value 100 to A, 200 to B, 300 to C, and 600 to D. 
00002
00003
00001
Syntax: 
[line] DELIMIT# stream,str-expr 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
str-expr    is a string of one to four characters that are to be recognized as 
delimiters. 
Description: 
The DELIMIT# statement allows the user to specify a delimiter character or 
characters in place of the default comma to determine the separation of data 
elements in lines or records of input data.  A list of valid delimiters is 
given under the DELIMIT statement. 
Examples: 
    350 DELIMIT# 1," ,;:" 
Line 350 sets stream 1 delimiters to include the blank, comma, semicolon, and 
colon.  Any INPUT# on stream 1 will recognize these four characters as 
delimiters separating individual data.  The DELIMIT# statement applies only to 
ASCII data files. 
00002
00003
00001
Syntax: 
[line] DELREC{#|:} stream[,key] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number.  The indicated stream must be open for output or update. 
key    is a numeric or string expression that represents the value of the key 
which points to the record to be deleted. 
Description: 
The DELREC statement deletes an indicated record from a data file. 
Usage Notes: 
If the stream is open to an ASCII data file, a pound sign (#) follows the 
DELREC.  If the stream is open to a binary data file, a colon (:) follows the 
DELREC.  If no key is specified, the current key value is used. 
00002
00001
00003
DELREC
DELREC
Syntax: 
[line] DEQ {stream|ALL} [;resource] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number.  ALL represents streams 1 through 12 inclusive. 
resource    is a request for resources.  The default is all resources 
associated with the stream. 
Description: 
The DEQ statement removes an access request from the operating system queue. 
A file that is enqueued by either ENQS or ENQE must be dequeued before it can 
be enqueued again.  A direct upgrade from ENQS to ENQE is not permitted. 
00002
00001
Syntax: 
DFI[LE] fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The DFILE command deletes a specified file, unless the user is not permitted 
to do so.  The DFILE command functions the same way for working storage files. 
00002
00001
Syntax: 
[line] DIGITS num-expr 
Parameter: 
num-expr    specifies the number of significant digits for PRINT statments, 
which cannot be less than 1 nor greater than the maximum value for the current 
PRECISION setting.  The maximum value for single precision is 9; the maximum 
for double precision is 20. 
Description: 
The DIGITS statement controls the number of significant digits used in output 
generated by PRINT and PRINT# statements. 
Usage Notes: 
The rounding of values output via PRINT and PRINT# statements is adjusted 
according to the DIGITS setting.  The default digits setting for BASIC is 6. 
The DIGITS statement does not control output formatting of numeric data for 
PRINT USING, and has nothing to do with internal representations or 
computational precision. 
See the PRINT statement for a detailed description of the way in which DIGITS 
interacts with the PRINT statement. 
00002
00001
00003
Syntax: 
[line] DIM variable[$](int[,int])[=const] 
[,variable][$](int[,int])[=const]]... 
Parameters: 
int    is a non-negative integer. 
variable    is a name beginning with an alphabetic character and having a 
maximum of 31 alphanumeric characters. 
const    is a numeric constant if the preceding array is a numeric array and a 
string constant if the preceding array is a string array. 
Description: 
The DIM statement identifies and initializes one or more arrays as vectors or 
matrixes and reserves data space for values to be inserted into the respective 
array(s). 
Usage Notes: 
DIM statements are not executable, and a transfer to a DIM statement passes 
control to the next executable statement.  Numbered DIM statements are 
processed during the compilation of a program.  Direct DIM statements are 
processed as they are entered.  The behavior of a DIM statement depends upon 
three factors: 
1.  The existence or absence of a prior array with the same name. 
2.  The use of zero and/or non-zero dimension values. 
3.  The use of an optional initializing constant. 
Thus the following rules apply: 
1.  For a DIM statement that has zero dimension values and no initializing 
    constant: 
        If an old array exists and the DIM statement has the same number of 
        dimensions (i.e. vector vs. matrix), the old dimensions and data 
        values are used.  If the DIM statement does not have the same number 
        of dimensions, the new array is initialized with default dimensions 
        and zero or null values. 
2.  For a DIM statement that has zero dimension values and an initializing 
    constant: 
        All values are initialized to the specified constant.  If an old array 
        exists and the DIM statement has the same number of dimensions, the 
        new array has the current dimensions of the old array; otherwise, the 
        new array has default dimensions. 
3.  For a DIM statement that has non-zero dimension values and no initializing 
    constant: 
        If an old array exists with the same name and dimensions, the new 
        array is identical to the old.  Otherwise, the new array is 
        dimensioned as specified but the values are set to zero or the null 
        string. 
4.  For a DIM statement that has non-zero dimension values and an initializing 
    constant: 
        A new array with the specified dimensions and initial values is always 
        created. 
The dimension values set within DIM statements indicate the upper index limit 
for the elements.  When BASE=1: 
o   The lower limit is 1. 
o   The maximum dimension is 131068. 
o   DIM K(14) defines 14 elements (1-14). 
When BASE=0: 
o   The lower limit is 0. 
o   The maximum dimension is 131067, since counting starts with 0. 
o   DIM(14) defines 15 elements (0-14). 
In case of a two-dimensional array, the total number of elements must not 
exceed 131068 when BASE=1 and 131067 when BASE=0.  (See the OPTION statement.) 
The same array name may not be used for both a vector and a matrix.  If BASIC 
encounters this conflict, it produces an error message.  Error messages are 
also produced if: 
o   The user's data space (the auto allocation set by BASIC) is exceeded by 
    the actual data value allocations while arrays are being dimensioned with 
    existing data. 
o   The array's space reservation will exceed the user data space available if 
    all the arrays are used as dimensioned. 
Examples: 
    200 DIM K_DUCK(5)=0,B$(25),C(0,0),D$(0) 
    300 DIM B_FUDDLE(0,0)=1,F(0),G(10) 
If at the time these statements are compiled, the user already has existing 
data in arrays K_DUCK, C, D$, B_FUDDLE, and G, then the following will be true 
of the specified arrays after compilation has terminated: 
    Array     Condition 
    -----     --------- 
    K_DUCK    Has 5 new values, set to 0. 
    B$        Is created with 25 null strings. 
    C         Is used in the form that it existed previously, unless the old 
              array was a vector.  In this case C is now a 10 by 10 matrix 
              with zero values. 
    D$        Is used in the form it existed previously, unless the old array 
              was a matrix.  In this case D$ is now a 10 element vector with 
              null string values. 
    B_FUDDLE  Has every element set to 1 and has the form in which it existed 
              previously, unless the old B_FUDDLE was a vector.  In this case, 
              B_FUDDLE is dimensioned 10 by 10. 
    F         Is created as a 10 element vector with zero values. 
    G         Is a 10 element vector.  If the old G was a 10 element vector, 
              the new array is identical.  If not, all values are zero. 
00002
00004
00001
00003
Syntax: 
line DO UNTIL truth-expression 
line statement 
[line statements] 
   . 
   . 
   . 
line END DO 
Parameters: 
truth-expression    specifies a logical or relational expression. 
Description: 
The DO UNTIL and END DO statements define a loop that executes until a truth 
expression proves true.  The test for truth is made at the end of the loop. 
Once the truth expression is satisfied, execution resumes at the statement 
following the END DO statement. 
00002
00001
Syntax: 
line DO WHILE truth-expression 
line statement 
[line statements] 
   . 
   . 
   . 
line END DO 
Parameters: 
truth-expression    specifies a logical or relational expression. 
Description: 
The DO WHILE and END DO statements define a loop that executes while a truth 
expression proves true.  The test for truth is made at the beginning of the 
loop (compare with the DO_UNTIL statement). 
Once the truth expression is no longer satisfied, execution resumes at the 
statement following the END DO statement. 
00002
00001
IF_THEN_ELSE
Syntax: 
line END 
Description: 
The END statement signifies the physical end of the program and must be 
present before a program can be executed. 
00001
IF_THEN_ENDIF
Syntax: 
END 
Description: 
The END command is used only to exit CALC mode.  Its previous use as a way to 
exit BASIC has been eliminated in Release E00.  An attempt to exit BASIC by 
typing END now results in a warning message to use Q instead. 
00001
DO_UNTIL
Syntax: 
[line] ENQE stream[;resource][,wait time] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number from 1 to 12. 
resource    is a request for resources.  The default is BASICFILE. 
wait time    is an approximate number of seconds (rounded to an integer) that 
the request will wait before being timed out. 
Description: 
The ENQE statement enqueues the user for exclusive access to a file.  Attempts 
to write or delete records of a BASIC file opened in shared mode are not 
permitted unless ENQE is in effect.  When ENQE is issued, if no other users 
have active or pending enqueued access, the request is honored and the 
operating system records that the file is in exclusive use.  If other users 
are active or enqueued and no wait time was specified, a diagnostic message is 
printed; if a wait time was specified, the request is queued and the user is 
suspended until access is granted or a time-out occurs. 
00002
00001
Syntax: 
[line] ENQS stream[;resource][,wait time] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number from 1 to 12. 
resource    is a request for resources.  The default is BASICFILE. 
wait time    is an approximate number of seconds (rounded to an integer) that 
the request will wait before being timed out. 
Description: 
The ENQS statement enqueues the user for shared access.  If one or more 
user(s) issues an ENQS statement for a particular file, updates are denied. 
When ENQS is issued, if the file is not currently subject to an ENQE statement 
in another user's program, and if the operating system queue stack is not 
full, the ENQS request is honored and the operating system records that the 
file is in shared use by the indicated user.  If the file is subject to a 
prior ENQE by another user, and no wait time is specified in the ENQS 
statement, a diagnostic message is returned.  If a wait time is specified, the 
ENQS request is queued and the user is suspended until access is granted or 
time-out occurs. 
00002
00001
Mantissa Syntax: 
[{+|-}]{#[#...][decimal-point[#...]]|decimal-point#[#...]} & {^^^|^^^^|^^^^^} 
~^B^ DESCRIPTION: 
Description: 
These fields are represented by fields of pound signs with a decimal point 
included, followed by three, four, or five circumflex (up arrow) characters. 
The area to the left of the circumflex (up arrow) characters can be considered 
a decimal numeric field in which a scaled representation of the value of the 
variable is inserted.  The value is scaled so that the maximum number of 
characters (including a leading blank or minus sign) will conform to the area 
to the left of the decimal point.  The circumflex characters are replaced by 
the standard BASIC exponential notation.  (See the PRINT statement.) 
Fractional values in the scaled value are rounded and truncated if they are 
too long for the field to the right of the decimal point.  If they are, the 
fractional values are padded with zeros. 
The following table illustrates various types of exponential numeric fields. 
The sequence of values -.1, 1.2, -12.34, 123.456, -1234.5678 are inserted into 
each field. 
         #.##^^^^          ###.##^^^^          ###.^^^^ 
         -.10E+00          -10.00E-02          -10.E-02 
         1.20E+00          120.00E-02          120.E-02 
         -.12E+02          -12.34E+00          -12.E+00 
         1.23E+02          123.46E+00          123.E+00 
         -.12E+04          -12.35E+02          -12.E+02 
The format of a simple expression follows. 
Format: 
[sign]value[operator value]... 
Parameter: 
value    is either a numeric constant or variable. 
The order of precedence with arithmetic operators determines the order of 
evaluation as follows: 
    Level       Operator 
    -----       -------- 
      1         Exponentiation. 
      2         Multiplication and division. 
      3         Addition and subtraction. 
Exponentiations are evaluated first; the expression is thus reduced by one 
operator and one argument for each exponentiation.  Multiplications and 
divisions are evaluated at the same level.  A sequence of multiplications and 
divisions without intervening additions or subtractions is evaluated in left 
to right order.  For example, A/B/C is evaluated the same as (A/B)/C. 
Additions and subtractions are performed last, in left to right order.  For 
example, A-B-C is equivalent to (A-B)-C. 
00001
00002
Syntax: 
'E[E...] 
Description: 
These fields are represented by an apostrophe followed by one or more E 
characters. 
The apostrophe and the E's are replaced by characters from the string 
variable.  If the string is shorter than the field, the area following the 
filled portion is padded with blanks.  If the string is longer than the field, 
the field is extended to the right.  Note that if an extended field is 
specified in a format-string, the total length of the converted output string 
is variable. 
Examples: 
    100 LET G$="GEOFF" 
    200 D$="THE LETTERS IN G$ ARE 'EEEEEEE." 
    300 PRINT USING D$, G$ 
    400 PRINT A 
    500 END 
Line 300 prints the message: 
    THE LETTERS IN G$ ARE GEOFF. 
Note that line 200, even though it is not an image statement, defines the 
format-string used by the PRINT USING statement in line 300. 
00001
00002
Syntax: 
FAS[T[H]] [time] 
Parameters: 
time    is an integer that specifies the number of seconds of compute time the 
program may execute. 
The form FASTH generates a "header" line that displays the time, date, and 
program name.  Note that FAS, FAST and FASTH are valid forms of this command, 
while FASH is illegal. 
Description: 
The FAST command initiates execution of the source program in the working 
storage area, and increases execution speed by eliminating index checking on 
array element references. 
A program executed via RUN always indicates an error if an array access 
involves an index value out-of-range.  A program executed via FAST may, 
depending on the value of the out-of-range indexes, run to completion using 
invalid data, or it may trap or abort.  The initialization of a FAST command 
is similar to RUN. 
00002
00001
Syntax: 
FASTER[H] 
Description: 
The FASTER command decreases compile speed but generates more efficient code. 
Thus, depending on the program, FASTER gives a performance improvement over 
FAST or RUN. 
00001
FASTER
Syntax: 
FASTEST[H] 
Description: 
The FASTEST command is specifically designed to make programs with explicit 
array references run as quickly as possible.  In order to accomplish this, 
BASIC does not allow the user to do any redimensioning of matrices during 
execution.  Statements such as "MAT INPUT B(I,I)" will be flagged as illegal 
if used in a program when running with FASTEST. 
00001
FASTEST
FAST
Syntax: 
FET[CH] fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The FETCH command loads, but does not execute a file that does not have line 
numbers.  The fetched file must have been built by EDIT or BASIC (via BUILD). 
The line numbers generated correspond to the key of the record read, only if 
that key is an integer.  If an EDIT file is FETCHed into BASIC with both 
integer and non-integer keys, some of the records may not be loaded into the 
BASIC workspace.  EDIT files that contain non-integer keys should be 
re-numbered to integer keys before they are FETCHed into BASIC. 
Usage Note: 
A file that was loaded with the FETCH command is non-executable.  The FETCH 
command is to be used only for editing purposes.  To execute a FETCHed file, 
first issue an NSAVE fid followed by a LOAD fid. 
00002
00001
00003
Format: 
name[.[account][.password]] 
Parameters: 
name    specifies 1 to 31 characters that assigns an identifying name to a 
file.  The valid characters for this parameter are upper and lowercase A 
through Z, the digits 0 through 9, the dollar sign ($), the underscore (_), 
the colon (:), and the hyphen (-).  The * character is used as a first 
character to identify star files, which are temporary files that are deleted 
when the user exits the system. 
account    specifies 1 to 8 characters that assigns a file to a particular 
group of files.  Accounts are created by the system manager and are used to 
control access to the system and to user files.  If unspecified, the user's 
file management account is assumed.  The valid characters for the account 
parameter are the same as those for the name parameter. 
password    specifies 1 to 8 characters that provides a security check for 
file access.  Only users who know the password can access the file.  If 
unspecified, no password is included in the fid. 
00001
The following general rules apply to file I/O: 
1.  If the user specifies a key on input that does not exist, a monitor error 
    occurs.  If the user takes control over the monitor error and does a 
    regular INPUT, the next sequential record is read. 
2.  If no key is specified, records are accessed sequentially. 
3.  A semicolon after the stream number must be followed by a key. 
4.  If files are open for input or update, and the end of the file (EOF) is 
    reached, control is returned to the program if a WHEN EOF statement is set 
    for that stream; otherwise, a run-time error occurs. 
5.  A key numbered 1 in BASIC refers to 1.000 in EDIT. 
6.  When accessing binary files, the current MARGIN setting refers to the 
    number of 36-bit words rather than the number of characters. 
7.  Stream numbers are rounded according to the formula INT(value +.5). 
Syntax: 
[line] statement1 FOR control variable=initial value TO limit & 
STEP increment 
or 
[line] statement1 FOR control variable=initial value STEP increment & 
{WHILE|UNTIL} truth-expression 
Parameters: 
statement1    is any allowable BASIC statement. 
control variable    is a simple numeric variable. 
initial value    is a numeric expression representing the value that will be 
assigned to the control variable at the beginning of the loop. 
increment    is an optional numeric expression representing the value that 
will be added to the control variable.  If this option is used with the first 
format, the value is increased until the limit of the loop is reached.  If 
this option is used with the second format (WHILE|UNTIL), the value is 
increased as long as the WHILE condition is true or the UNTIL condition is 
false.  If the STEP option is not specified, this value is assumed to be 1. 
truth-expression    specifies a logical or relational expression. 
Description: 
The FOR modifier creates an implied loop on a single statement.  The FOR 
modifier eliminates the need of the FOR-NEXT statements when using simple 
loops.  If the STEP option is used, the loop continues until the limit is 
reached.  If the WHILE|UNITL options are used, the loop continues as long as 
the WHILE condition is true, or the UNTIL condition is false. 
Examples: 
In the following example, the FOR modifier is used to create a simple loop on 
a single line: 
    10 PRINT A(J) FOR J=1 TO 5 \ REM to skip 5 lines 
00002
00003
00001
Syntax: 
line FOR control variable = initial value TO limit [STEP increment] 
[line[s] statements] 
line NEXT control variable 
or 
line FOR control variable = initial value [STEP increment] {WHILE|UNTIL} & 
truth-expression 
[line[s] statements] 
line NEXT control variable 
Parameters: 
control variable    is a simple numeric variable. 
initial value    is a numeric expression representing the value that will be 
assigned to the control variable at the beginning of the loop. 
limit    is a numeric expression representing a value that, when reached by 
the control variable, will end the loop. 
increment    is an optional numeric expression representing the value that 
will be added to the control variable every time the corresponding NEXT 
statement is encountered.  If the STEP option is not specified, this value is 
assumed to be 1. 
truth-expression    specifies a logical or relational expression.  When the 
conditional FOR-NEXT statement format is used: 
o   Each time the loop is about to begin, BASIC evaluates the truth 
    expression.  The loop terminates if the truth-expression is true and UNTIL 
    is used, or if the truth-expression is false and WHILE is used. 
o   The loop is incremented and BASIC checks if the limit has been exceeded. 
    If it has not been exceeded, BASIC checks the truth-expression. 
Description: 
The FOR statement and the NEXT statement create repetitive redirections of 
program flow referred to as loops.  Instructions generated for computational 
loops (as opposed to loops with input/output operation) are given special 
attention when FASTER and FASTEST modes of operation are used. 
Usage Notes: 
The entire span of statements between and including a FOR statement and the 
first subsequent NEXT statement with the same control variable is defined as a 
FOR-NEXT block.  When BASIC encounters a FOR-NEXT block, it sets the control 
variable to the initial value.  The statements following the FOR statement are 
executed until the corresponding NEXT statement is reached, which adds the 
increment to the control variable, and passes execution to the statement 
following the FOR statement.  This process continues until the value of the 
control variable goes outside the range between the initial value and the 
limit.  At that point, the first executable statement following the NEXT 
statement is executed. 
The control variable can be accessed and changed by the program within the 
block.  The values of the limit and increment expressions cannot be changed 
within the block. 
The values of the initial value, limit expression and increment expression are 
computed only on normal entry to a FOR-NEXT block (i.e., when program flow is 
directed to the FOR statement). 
A FOR-NEXT block becomes active when entered via a FOR statement.  The 
FOR-NEXT block remains active until the NEXT statement results in an exit.  A 
NEXT exit occurs when the value of the simple variable exceeds the range 
between the initial value and the limit at the time a NEXT statement is 
encountered. 
The use of fractional values for increments is subject to cumulative 
round-off, and thus may not always yield the expected loop count. 
When control is transferred out of a FOR-NEXT block via the NEXT statement, 
the control variable contains the first value that violates the conditions set 
up in the FOR statement. 
Special Considerations: 
If a FOR-NEXT block is entered at some point other than the FOR statement, an 
error will be reported during program compilation. 
If the increment expression has a value of zero, an error is reported when the 
NEXT is reached.  Compile-time errors are reported if a FOR statement occurs 
without a corresponding NEXT, or a NEXT statement occurs without a 
corresponding FOR. 
A FOR-NEXT block can contain nested FOR-NEXT blocks within it, but FOR-NEXT 
blocks may not be interleaved.  A FOR-NEXT block may contain only complete 
FOR-NEXT blocks; a FOR-NEXT block that begins within another FOR-NEXT block 
may not have a NEXT statement that follows the NEXT statement of the 
containing block.  The control variable of a nested block must be different 
than that of any containing block.  However, FOR-NEXT blocks that are 
completely separate may have the same control variable. 
Examples: 
    5   DIM X(3,3) 
    7   DEF FNX(X)=(X| (1/2))*2 
    10  FOR I=1 TO 10 
    20  A(I)=I 
    30  NEXT I 
    40  FOR J=8 TO -8 STEP -1 
    50  PRINT FNX(J) 
    60  NEXT J 
    100 FOR I=1 TO 3 
    110 FOR J=1 TO 3 
    120 LET Q=I+J 
    130 LET X(I,J)=Q 
    140 NEXT J 
    150 NEXT I 
    160 MAT PRINT X; 
Lines 10 to 30 set up a loop that creates a vector A with the elements 1 
through 10.  Lines 40 to 60 set up a loop whose values are dependent upon 
subsequent lines in the program.  The user-defined function FNX is called, 
using the successive values of J as parameters.  Lines 100 to 160 construct 
and print a matrix X that has the form: 
    2     3     4 
    3     4     5 
    4     5     6 
Notice that both I and J are used twice as control variables, and that lines 
110 to 140 contain a FOR-NEXT block that is nested inside the FOR-NEXT block 
that spans lines 100 to 150. 
00002
00005
00001
00004
00003
Syntax: 
line    DEF FNvariablename[(parameter1[,parameter2]...)]=expr 
Parameters: 
variablename    identifies the function.  If a "$" is included, the function 
is a string function and returns a string result; otherwise, the function is 
numeric. 
parameter    is any simple variable name, such as B1, C, X, etc. 
expr    is a valid numeric or string BASIC expression, depending on whether 
the FN name is numeric or string. 
Once defined, the user calls a function as follows: 
    FNvariablename[(expr1[,expr2]...)] 
Description: 
The DEF statement allows the user to create and define functions. 
Usage Notes: 
The expressions must be the same in number and type as the parameters defined 
in the DEF statement.  When the function is called, the expressions, which are 
called an argument list, are evaluated and then assigned to the parameters in 
the function definition.  The expression in the function definition is 
evaluated using the values in the argument list, returning a new value based 
upon the operations defined for the function.  The parameters within a 
function definition are not the same as variables within the main program that 
may have the same letter.  The difference between local and global variables 
is described later in this section. 
Examples: 
    100 DEF FNFROG(A,B)=A+B 
    200 DEF FNPETK(A,B)=B-A 
    1000 LET X=FNFROG(5,7)*FNPETK(10,Z) 
Line 100 defines a function that adds together the two parameters.  The 
parameter names are local to the function definition, and are not the same as 
any other variables called A or B that may appear in the main program or in 
another function definition.  Line 200 defines another function that subtracts 
one parameter from another.  Line 1000 calls both FNFROG and FNPETK.  When 
FNFROG is called, the values 5 and 7 are assigned to the local variables A and 
B respectively, and the function is evaluated.  When FNPETK is called, the 
values 10 and Z are assigned to the local variables A and B, and the function 
is evaluated.  In other words, line 1000 is equivalent to the following 
statement: 
    1000 LET X=(5+7)*(Z-10) 
00002
00004
00001
00003
Syntax: 
[line] GET: stream[;key][,CRPT=str-expr],num-var[,num-var]... 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of the key 
which points to the first record to be read. 
CRPT=str-expr    specifies the encryption seed for binary data files.  The 
seed can be entered as a string of characters of length less than or equal to 
4.  If a seed has a length of 1 to 3, it will be right justified and ".000" is 
placed in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write. 
num-var    is a numeric variable that is to be read from the binary file. 
Description: 
The GET: statement reads data from binary files for assignment to scalar 
variable and individual array elements. 
Usage Notes: 
If no key is included and unused data values are currently buffered for the 
indicated stream, the unused values are accessed.  If there are no unused 
values pending, the next record is read.  Values are assigned to numeric 
variables in left to right order.  The GET: statement functions asynchronously 
unless statements include specific keys, in which case input starts at the 
beginning of the record.  GET: does not recognize the precision of the file 
data; that is contained in the OPEN statement. 
Examples: 
    350 GET: I;K1,A,B,C(3) 
    400 GET: I,C(J) 
Statement 350 accesses the record with a key value of K1 on stream I, which 
must be open for GET: access.  Three values are accessed and assigned. 
Remaining values are retained in the stream I buffer.  Statement 400 accesses 
the next value from the stream I input buffer.  If the buffer is empty, 
another record will be read. 
00002
00004
00001
00003
Syntax: 
GO 
Description: 
The GO command resumes execution of BASIC after a break condition only for 
compiled programs.  It does not handle directly executed statements.  See the 
PROCEED_STATEMENT. 
00001
Syntax: 
[GOOD]BYE 
Description: 
The GOODBYE command closes all open files, releases queue entries, and then 
ends the batch operation or terminal session.  The GOODBYE command is a 
synonym for the BYE and OFF commands. 
00001
Syntax 1: 
[line] {GOSUB|GO SUB} line 
    . 
    . 
    . 
[line] RETURN 
Parameters: 
line    specifies the line to which control is to be transferred in the 
subroutine. 
GOSUB and GO SUB are synonyms. 
Description: 
The GOSUB statement unconditionally transfers program flow to a subroutine 
within the program. A RETURN statement transfers control to the line following 
the most recently executed GOSUB statement.  Note that RETURN need not have a 
larger line number than the GOSUB. 
Usage Notes: 
When a GOSUB statement is encountered in a BASIC program, control is 
transferred to the specified line.  Simultaneously, the line number of the 
line following the GOSUB is placed in a portion of memory referred to as the 
GOSUB-RETURN stack.  If another GOSUB is encountered prior to the reaching of 
a RETURN statement, the line number of the line following the second GOSUB is 
stored in the GOSUB-RETURN stack, and so forth, until a RETURN is encountered. 
At that point, control is transferred to the line number last stored in the 
GOSUB-RETURN stack (the line following the most recent GOSUB).  Thus the 
GOSUB-RETURN stack operates on the last-in/first-out principle. 
GOSUB statements can be nested; entries accumulate in the stack, and are then 
accessed by RETURN statements in the reverse order in which they were entered. 
The GOSUB-RETURN stack holds up to 76 entries; up to 76 GOSUBs may be issued 
before a RETURN.  The GOSUB-RETURN stack is cleared when an END or a STOP 
statement is encountered, but not by a user break or error halt.  The stack is 
cleared when a program is started into execution, but not when interrupted 
execution is resumed. 
A GOSUB statement must branch to a line number that exists in the program.  If 
a RETURN statement is encountered before a GOSUB is active, a run-time error 
occurs. 
If execution of a subroutine is interrupted, a direct RETURN statement can be 
issued to resume program operation at the line number following the latest 
GOSUB. 
Examples: 
    400 GOSUB 800 
    410 PRINT A 
    420 GOSUB 900 
    430 PRINT "B=";B 
    440 STOP 
    800 IF A=0 THEN 820 
    810 LET A=1 
    820 RETURN 
    900 IF B<0 THEN 920 
    910 RETURN 
    920 LET B=0 
    930 RETURN 
Line 800 is the start of a subroutine with a single RETURN at 820.  Control 
goes from line 400 to 800 and from 820 to 410.  Line 900 is the start of a 
subroutine with two RETURN statements, both of which return control to line 
430.  Line 440 prevents accidental in-line entry into the subroutine that 
begins at line 800.  The RETURN statement at 820 prevents accidental in-line 
entry at 900. 
Special Considerations: 
If a GOSUB statement is a direct statement or a statement not within a 
multi-line, user-defined function, the transfer line number must not be within 
a user function definition block. 
There is no special treatment of GOSUBs in user defined functions.  If there 
is still a pending RETURN when the function is exited, and a RETURN is later 
executed outside of the function, then an error is issued. 
Subroutines accessed via GOSUB differ from user-defined functions in that they 
are open rather than closed.  A user-defined function can only be accessed at 
its entry point, via a function call, and exited via a single FNEND statement. 
Subroutines accessed via GOSUB can be entered at different points and exited 
from any RETURN statement reached. 
00002
00004
00001
00005
00003
Syntax: 
[line] {GOTO|GO TO} {line|ERL|DBERR} 
Parameters: 
line    specifies the line number to which control is to be transferred.  This 
line number must exist within the program. 
ERL    is the error line. 
DBERR     is the line after the data base error occurred. 
Description: 
The GOTO statement unconditionally transfers control to a specified line 
number.  GOTO and GO TO are synonyms.  If the statement to which control is 
transferred is non-executable, transfer is made to the next executable 
statement following the target statement. 
Examples: 
    100 GOTO 900 
    . 
    . 
    . 
    250 GOTO 500 
Line 100 transfers control to line 900, while line 200 transfers control to 
line 500. 
00002
00003
00001
Syntax: 
{H|HELP} [(processor)][ TOPICS ][ keyword1 ][ - ][ keyword2] 
Parameters: 
processor    specifies a program or processor that has an associated helpfile 
in the form HELP:processor:[.[account][.password].  The default is the 
processor currently under control. 
TOPICS    specifies that only a list of available topics (message names) is 
required.  The range of topics is determined by keyword1 or keyword2. 
keyword1    specifies the name of the message to be printed. 
keyword2    if a range is specified (by including a dash "-"), keyword2 is the 
upper limit of the range.  If a range is not specified, keyword2 is a 
submessage, or category within a message. 
Description: 
HELP prints information. 
HELP messages have levels.  Once the initial level has been printed, typing a 
question mark prints the next level, usually containing greater detail. 
Typing two question marks prints the entire message. 
Any standard HELP file (even those for other processors) can be read with the 
HELP command. 
Examples: 
HELP TOPICS 
means print a list of names of available messages. 
HELP TOPICS A - C 
means print a list of message names from A to C inclusive. 
HELP SHOW 
means print information about the SHOW command. 
HELP PRINT 
means print information about the PRINT statement. 
00002
00003
00001
A 
  abbreviations of parameters - 
      HELP PARAMS 
  abnormal exits -   
    exceeded limits - 
      HELP BASIC_COMMAND DESCRIPTION_2: 
    line disconnections - 
      HELP BASIC_COMMAND DESCRIPTION_2: 
    monitor aborts - 
      HELP BASIC_COMMAND DESCRIPTION_2: 
    operator aborts - 
      HELP BASIC_COMMAND DESCRIPTION_2: 
  aborts - 
      HELP BASIC_COMMAND DESCRIPTION_2: 
  ABS Function - 
      HELP ALGEBRA_FUNCTIONS 
  accessing data from binary files - 
      HELP MAT_GET: DESCRIPTION: 
  accessing data representations - 
      HELP READ DESCRIPTION: 
  account - 
      HELP CATALOG PARAMETERS: 
  account parameter - 
      HELP FID PARAMETERS: 
  ACOS Function - 
      HELP TRIG_FUNCTIONS 
  ACS Function - 
      HELP TRIG_FUNCTIONS 
  adding program documentation - 
      HELP REM DESCRIPTION: 
  addition operator - 
      HELP OPERATORS 
  adescr parameter - 
      HELP PARAMS 
  advancing to the next page - 
      HELP PAGE USAGE_NOTES: 
  Algebraic Functions -   
    ABS - 
      HELP ALGEBRA_FUNCTIONS 
    DET - 
      HELP ALGEBRA_FUNCTIONS 
    EXP - 
      HELP ALGEBRA_FUNCTIONS 
    INT - 
      HELP ALGEBRA_FUNCTIONS 
    LGT - 
      HELP ALGEBRA_FUNCTIONS 
    LOG - 
      HELP ALGEBRA_FUNCTIONS 
    LOG10 - 
      HELP ALGEBRA_FUNCTIONS 
    LOG2 - 
      HELP ALGEBRA_FUNCTIONS 
    LTW - 
      HELP ALGEBRA_FUNCTIONS 
  ALL - 
      HELP CATALOG PARAMETERS: 
      HELP CLOSE PARAMETERS: 
  ALL (SHOW option) - 
      HELP SHOW PARAMETERS: 
  Alphanumeric replacement fields -   
    centered - 
      HELP ALPHANUMERIC_REPLACEMENT_FILEDS 
      HELP CENTERED_ALPHANUMERIC 
    extended - 
      HELP ALPHANUMERIC_REPLACEMENT_FILEDS 
      HELP EXTENDED_ALPHANUMERIC 
    left-justified - 
      HELP ALPHANUMERIC_REPLACEMENT_FILEDS 
      HELP LEFT_JUSTIFIED_ALPHANUMERIC 
    right-justified - 
      HELP ALPHANUMERIC_REPLACEMENT_FILEDS 
      HELP RIGHT_JUSTIFIED_ALPHANUMERIC 
    simple - 
      HELP ALPHANUMERIC_REPLACEMENT_FILEDS 
  Alphanumeric Replacement Fields - 
      HELP ALPHANUMERIC_REPLACEMENT_FILEDS 
  aname parameter - 
      HELP PARAMS 
  AND expression - 
      HELP IF_THEN USAGE_NOTES: 
  apostrophe - 
      HELP SIMPLE_ALPHANUMERIC DESCRIPTION: 
  argument matrix - 
      HELP MAT_SIM USAGE_NOTES: 
  Arithmetic Operators - 
      HELP OPERATORS 
      HELP IF_THEN USAGE_NOTES: 
  array descriptor - 
      HELP MAT_GET: USAGE_NOTES: 
  array names - 
      HELP VARIABLES SYNTAX: 
  array usage - 
      HELP SUBSCRIPT_EXPRESSIONS 
  Array Variable Reference - 
      HELP ARRAYS 
  ASC Function - 
      HELP CONVERSION_FUNCTIONS ASC 
  ASCII character set - 
      HELP EXAMPLES_OF_CP_6_BASIC_I_D_S/II 
  ASCII file output - 
      HELP MAT_PRINT# DESCRIPTION: 
  ASCII file records - 
      HELP MAT_PRINT#_USING DESCRIPTION: 
  ASIN Function - 
      HELP TRIG_FUNCTIONS 
  ASN Function - 
      HELP TRIG_FUNCTIONS 
  assigning value to a variable - 
      HELP LET DESCRIPTION: 
  assignment statements - 
      HELP DDIGITS EXAMPLE: 
  assignment symbol - 
      HELP MAT_ASSIGNMENT USAGE_NOTES: 
  asynchronous input - 
      HELP INPUT# USAGE_NOTES: 
  ATN Function - 
      HELP TRIG_FUNCTIONS 
  AUTO Command - 
      HELP AUTO 
  AUTOMATIC - 
      HELP DBMEMBERINFO$ DESCRIPTION: 
  automatic line numbering - 
      HELP AUTO DESCRIPTION: 
B 
  BASE - 
      HELP OPTION USAGE_NOTES: 
  BASIC -   
    I-D-S/II Interface - 
      HELP CALLING_A_USER_DEFINED_FUNCTION 
    Reserved words - 
      HELP RESERVED_WORDS 
    standard functions - 
      HELP GOTO_DBERR_STATEMENT 
  BASIC Command - 
      HELP BASIC_COMMAND 
  BATCH -   
    JOB card - 
      HELP BATCH PARAMETERS: 
    RUNH - 
      HELP BATCH PARAMETERS: 
  BATCH Command - 
      HELP BATCH 
  BCL Function - 
      HELP STATUS_FUNCTIONS BCL 
  binary data files - 
      HELP MAT_SIM EXAMPLES: 
  BIT option - 
      HELP CHANGE PARAMETERS: 
  block structured programming - 
      HELP IF_THEN_ENDIF DESCRIPTION: 
  BREAK key - 
      HELP LIST DESCRIPTION: 
  BREAK response - 
      HELP WHEN PARAMETERS: 
  BREAK Statement - 
      HELP BREAK 
  breaking a display - 
      HELP LIST DESCRIPTION: 
  buffer - 
      HELP MAP PARAMETERS: 
  buffer size - 
      HELP MAP USAGE_NOTES: 
  BUILD Command - 
      HELP BUILD 
  building a file - 
      HELP BUILD DESCRIPTION: 
  BYE Command - 
      HELP BYE 
C 
  CALC Command - 
      HELP CALC 
  calculator mode - 
      HELP END_COMMAND DESCRIPTION: 
  CATALOG Command - 
      HELP CATALOG 
  Centered Alphanumeric Fields - 
      HELP CENTERED_ALPHANUMERIC 
  CFETCH Command - 
      HELP CFETCH 
  CHAIN Statement - 
      HELP CHAIN 
  CHANGE Statement - 
      HELP CHANGE 
  changing existing line numbers - 
      HELP RENUMBER DESCRIPTION: 
  changing the current workspace name - 
      HELP RENAME DESCRIPTION: 
  character records - 
      HELP PRINT#_USING DESCRIPTION: 
  CHR$ Function - 
      HELP CONVERSION_FUNCTIONS CHR$ 
  circumflex - 
      HELP EXPONENTIAL_NUMERIC DESCRIPTION: 
  CLEAR Command - 
      HELP CLEAR_COMMAND 
  CLEAR DATA Statement - 
      HELP CLEAR DESCRIPTION: 
  CLEAR Statement -   
    CLEAR NUMERIC - 
      HELP CLEAR PARAMETERS: 
    CLEAR STRING - 
      HELP CLEAR PARAMETERS: 
    DATA - 
      HELP CLEAR SYNTAX: 
    NUMERIC ARRAYS - 
      HELP CLEAR SYNTAX: 
    NUMERIC SCALARS - 
      HELP CLEAR SYNTAX: 
    STRING ARRAYS - 
      HELP CLEAR SYNTAX: 
    STRING SCALARS - 
      HELP CLEAR SYNTAX: 
  CLEAR Statement - 
      HELP CLEAR 
  clearing and fetching a file - 
      HELP CFETCH DESCRIPTION: 
  clearing working storage environment - 
      HELP DFILE DESCRIPTION: 
  CLK$ Function - 
      HELP STATUS_FUNCTIONS CLK$ 
  CLOAD Command - 
      HELP CLOAD 
  CLOSE - 
      HELP MARGIN USAGE_NOTES: 
  CLOSE Statement - 
      HELP CLOSE 
  CMP Function - 
      HELP STRING_FUNCTIONS CMP 
  code saving - 
      HELP CODESAVE DESCRIPTION: 
  CODESAVE Command - 
      HELP CODESAVE 
  coefficient matrix - 
      HELP MAT_SIM USAGE_NOTES: 
  colon (:) - 
      HELP LET DESCRIPTION: 
  comma - 
      HELP INPUT# USAGE_NOTES: 
  common parameter abbreviations - 
      HELP PARAMS 
  COMP Function - 
      HELP DECIMAL_FUNCTIONS COMP_ 
  comparisons - 
      HELP IF_THEN USAGE_NOTES: 
  Complex Expressions - 
      HELP COMPLEX_EXPRESSIONS 
  concatenation - 
      HELP OPEN USAGE_NOTES: 
  concatenation operator - 
      HELP STRING_EXPRESSIONS 
  CONSEC (consecutive) - 
      HELP OPEN PARAMETERS: 
  const parameter - 
      HELP PARAMS 
  constant - 
      HELP LET DESCRIPTION: 
  control variable - 
      HELP FOR_NEXT SYNTAX: 
      HELP FOR_NEXT USAGE_NOTES: 
  copying a source program - 
      HELP RESAVE DESCRIPTION: 
  COS Function - 
      HELP TRIG_FUNCTIONS 
  COSH Function - 
      HELP TRIG_FUNCTIONS 
  COT Function - 
      HELP TRIG_FUNCTIONS 
  CPU Function - 
      HELP STATUS_FUNCTIONS CPU 
  creating a file - 
      HELP BUILD DESCRIPTION: 
  creating a new workspace name - 
      HELP NEW DESCRIPTION: 
  creating and defining functions - 
      HELP FUNCTION_DEFINITION DESCRIPTION: 
  cross-reference of source program - 
      HELP XREF DESCRIPTION: 
  CRPT option - 
      HELP INPUT# PARAMETERS: 
      HELP LINPUT# PARAMETERS: 
      HELP MAT_INPUT# PARAMETERS: 
      HELP PRINT# PARAMETERS: 
      HELP PRINT#_USING PARAMETERS: 
      HELP MAT_PRINT# PARAMETERS: 
      HELP MAT_PRINT#_USING PARAMETERS: 
      HELP GET: PARAMETERS: 
      HELP MAT_GET: PARAMETERS: 
      HELP PUT: PARAMETERS: 
      HELP MAT_PUT: PARAMETERS: 
  CSC Function - 
      HELP TRIG_FUNCTIONS 
D 
  DAT$ Function - 
      HELP STATUS_FUNCTIONS DAT$ 
  data base error - 
      HELP GOTO_DBERR_STATEMENT 
  data file processing - 
      HELP MAT_SIM EXAMPLES: 
  data pointer - 
      HELP DATA USAGE_NOTES: 
  DATA Statement - 
      HELP DATA 
  DATE$ Function - 
      HELP STATUS_FUNCTIONS DATE$ 
  datum - 
      HELP INPUT USAGE_NOTES: 
      HELP DATA PARAMETER: 
  DB FROM - 
      HELP DB_FROM 
  DB SUB Statement - 
      HELP DB_SUB 
  DB TO - 
      HELP DB_TO 
  DBERR - 
      HELP GOTO PARAMETERS: 
      HELP WHEN DESCRIPTION: 
  DBMEMBERINFO$ - 
      HELP DBMEMBERINFO$ 
  DBNAMES$ - 
      HELP MAT_DBTYPES 
  DBOWNERINFO$ - 
      HELP DBOWNERINFO$ 
  DCBs - 
      HELP MAT_SIM EXAMPLES: 
  DDIGITS Statement - 
      HELP DDIGITS 
  debugging - 
      HELP RESTORE# USAGE_NOTES: 
  Debugging statements - 
      HELP RESTORE# USAGE_NOTES: 
  Decimal Numeric Fields - 
      HELP DECIMAL_NUMERIC 
  decimal precision - 
      HELP DDIGITS DESCRIPTION: 
  decimal scaling indicator - 
      HELP NUMERIC_CONSTANTS 
  decreasing compile time - 
      HELP FASTER DESCRIPTION: 
  DEF FN - 
      HELP FUNCTION_DEFINITION SYNTAX: 
  DEF statement - 
      HELP FUNCTION_DEFINITION DESCRIPTION: 
  default execution mode - 
      HELP REENTER DESCRIPTION: 
  defining functions - 
      HELP FUNCTION_DEFINITION DESCRIPTION: 
  definition-block - 
      HELP COMPLEX_FUNCTION_DEFINITION PARAMETERS: 
  DEG Function - 
      HELP TRIG_FUNCTIONS 
  DELETE Command - 
      HELP DELETE 
  deleting a file - 
      HELP DFILE DESCRIPTION: 
  deleting a file  - 
      HELP UNSAVE DESCRIPTION: 
  deleting a range of lines - 
      HELP DELETE DESCRIPTION: 
  deleting specific lines - 
      HELP DELETE DESCRIPTION: 
  DELIMIT# Statement - 
      HELP DELIMIT# 
  DELIMIT Statement - 
      HELP DELIMIT 
      HELP DATA USAGE_NOTES: 
  DELREC Statement - 
      HELP DELREC 
  DEQ Statement - 
      HELP DEQ 
  DET Function - 
      HELP ALGEBRA_FUNCTIONS 
  DFILE Command - 
      HELP DFILE 
  DIF$ Function - 
      HELP DECIMAL_FUNCTIONS DIF$ 
  DIG Function - 
      HELP STATUS_FUNCTIONS DIG 
  DIGITS setting - 
      HELP PRINT USAGE_NOTES: 
  DIGITS Statement - 
      HELP DIGITS 
  DIM Statement - 
      HELP DIM 
  dimension values - 
      HELP DIM USAGE_NOTES: 
  dimensional range - 
      HELP READ USAGE_NOTES: 
  dimensions - 
      HELP SUBSCRIPT_EXPRESSIONS 
      HELP MAT_INPUT USAGE_NOTES: 
      HELP MAT_READ USAGE_NOTES: 
  direct DATA statements - 
      HELP DATA USAGE_NOTES: 
  displaying HELP information - 
      HELP HELP DESCRIPTION: 
  division operator - 
      HELP OPERATORS 
  DO UNTIL-END DO Statement - 
      HELP DO_UNTIL 
  DO WHILE-END DO Statement - 
      HELP DO_WHILE 
  documentation of programs - 
      HELP RESTORE# USAGE_NOTES: 
  Documentation statements - 
      HELP RESTORE# USAGE_NOTES: 
  dollar sign - 
      HELP VARIABLES SYNTAX: 
  DOUBLE - 
      HELP OPTION SYNTAX: 
  DOUBLE mode - 
      HELP OPEN USAGE_NOTES: 
  DUP$ Function - 
      HELP STRING_FUNCTIONS DUP$ 
E 
  EDIT$ Function - 
      HELP STRING_FUNCTIONS EDIT$ 
  ejecting paper - 
      HELP PAGE USAGE_NOTES: 
  element in an array - 
      HELP SUBSCRIPT_EXPRESSIONS 
  ELSE - 
      HELP IF_THEN_ELSE SYNTAX: 
  Encryption -   
    CRPT option - 
      HELP INPUT# PARAMETERS: 
      HELP LINPUT# PARAMETERS: 
      HELP MAT_INPUT# PARAMETERS: 
      HELP PRINT# PARAMETERS: 
      HELP PRINT#_USING PARAMETERS: 
      HELP MAT_PRINT# PARAMETERS: 
      HELP MAT_PRINT#_USING PARAMETERS: 
    CRPT option  - 
      HELP GET: PARAMETERS: 
    CRPT option - 
      HELP MAT_GET: PARAMETERS: 
      HELP PUT: PARAMETERS: 
      HELP MAT_PUT: PARAMETERS: 
  END Command - 
      HELP END_COMMAND 
  END DO Statement - 
      HELP DO_UNTIL DESCRIPTION: 
  END Statement - 
      HELP END 
  ENDIF Statement - 
      HELP IF_THEN_ENDIF DESCRIPTION: 
  ENQE Statement - 
      HELP ENQE 
  ENQS Statement - 
      HELP ENQS 
  entering calculator mode - 
      HELP END_COMMAND DESCRIPTION: 
  EOF - 
      HELP WHEN PARAMETERS: 
      HELP FILE_RULES 
  ERL - 
      HELP GOTO PARAMETERS: 
  ERL Function - 
      HELP STATUS_FUNCTIONS ERL 
  ERM Function - 
      HELP STATUS_FUNCTIONS ERM 
  ERN Function - 
      HELP STATUS_FUNCTIONS ERN 
  ERROR - 
      HELP OPTION PARAMETERS: 
      HELP WHEN PARAMETERS: 
  error code - 
      HELP EXAMPLES_OF_CP_6_BASIC_I_D_S/II 
  error conditions - 
      HELP INPUT USAGE_NOTES: 
      HELP MAT_INPUT USAGE_NOTES: 
  error control - 
      HELP READ USAGE_NOTES: 
  error messages - 
      HELP EXAMPLES_OF_CP_6_BASIC_I_D_S/II 
  error point - 
      HELP MAT_READ USAGE_NOTES: 
  ERT Function - 
      HELP STATUS_FUNCTIONS ERT 
  evaluation of complex expressions - 
      HELP COMPLEX_EXPRESSIONS 
  exceeded limits - 
      HELP BASIC_COMMAND DESCRIPTION_2: 
  executing a compiled program - 
      HELP REENTER DESCRIPTION: 
  executing one or more lines in a program - 
      HELP STEP DESCRIPTION: 
  execution - 
      HELP IBEX DESCRIPTION: 
  exiting calculator mode - 
      HELP END_COMMAND DESCRIPTION: 
  EXP Function - 
      HELP ALGEBRA_FUNCTIONS 
  Exponential Numeric Fields - 
      HELP EXPONENTIAL_NUMERIC 
  exponentiation operator - 
      HELP OPERATORS 
  expression - 
      HELP LET DESCRIPTION: 
  Expressions -   
    complex - 
      HELP COMPLEX_EXPRESSIONS 
    simple - 
      HELP EXPRESSIONS 
    string - 
      HELP STRING_EXPRESSIONS 
  Extended Alphanumeric Fields - 
      HELP EXTENDED_ALPHANUMERIC 
F 
  false - 
      HELP IF_THEN USAGE_NOTES: 
  FAST Command - 
      HELP FAST 
  FASTER Command - 
      HELP FASTER 
  FASTEST Command - 
      HELP FASTEST 
  FETCH Command - 
      HELP FETCH 
  fid -   
    account - 
      HELP FID PARAMETERS: 
    name - 
      HELP FID PARAMETERS: 
    password - 
      HELP FID PARAMETERS: 
  File I/O Considerations - 
      HELP FILE_RULES 
  File I/O rules - 
      HELP FILE_RULES 
  file pointer - 
      HELP RESTORE# DESCRIPTION: 
  file records - 
      HELP MAT_PRINT#_USING DESCRIPTION: 
  FILES (SHOW option) - 
      HELP SHOW PARAMETERS: 
  FNS (SHOW option) - 
      HELP SHOW PARAMETERS: 
  FOR Modifier - 
      HELP FOR 
  FOR Statement - 
      HELP FOR_NEXT DESCRIPTION: 
  FOR-NEXT Statements - 
      HELP FOR_NEXT 
  format-string - 
      HELP PRINT_USING USAGE_NOTES: 
  formatted ASCII file records - 
      HELP MAT_PRINT#_USING DESCRIPTION: 
  formatted character records - 
      HELP PRINT#_USING DESCRIPTION: 
  fraction - 
      HELP NUMERIC_CONSTANTS 
  Function -   
    ABS - 
      HELP ALGEBRA_FUNCTIONS 
    ACOS - 
      HELP TRIG_FUNCTIONS 
    ACS - 
      HELP TRIG_FUNCTIONS 
    ASC - 
      HELP CONVERSION_FUNCTIONS ASC 
    ASIN - 
      HELP TRIG_FUNCTIONS 
    ASN - 
      HELP TRIG_FUNCTIONS 
    ATN - 
      HELP TRIG_FUNCTIONS 
    BCL - 
      HELP STATUS_FUNCTIONS BCL 
    CHR$ - 
      HELP CONVERSION_FUNCTIONS CHR$ 
    CLK$ - 
      HELP STATUS_FUNCTIONS CLK$ 
    CMP - 
      HELP STRING_FUNCTIONS CMP 
    COMP - 
      HELP DECIMAL_FUNCTIONS COMP_ 
    COS - 
      HELP TRIG_FUNCTIONS 
    COSH - 
      HELP TRIG_FUNCTIONS 
    COT - 
      HELP TRIG_FUNCTIONS 
    CPU - 
      HELP STATUS_FUNCTIONS CPU 
    CSC - 
      HELP TRIG_FUNCTIONS 
    DAT$ - 
      HELP STATUS_FUNCTIONS DAT$ 
    DATE$ - 
      HELP STATUS_FUNCTIONS DATE$ 
    DEG - 
      HELP TRIG_FUNCTIONS 
    DET - 
      HELP ALGEBRA_FUNCTIONS 
    DIF$ - 
      HELP DECIMAL_FUNCTIONS DIF$ 
    DIG - 
      HELP STATUS_FUNCTIONS DIG 
    DUP$ - 
      HELP STRING_FUNCTIONS DUP$ 
    EDIT$ - 
      HELP STRING_FUNCTIONS EDIT$ 
    ERL - 
      HELP STATUS_FUNCTIONS ERL 
    ERM - 
      HELP STATUS_FUNCTIONS ERM 
    ERN - 
      HELP STATUS_FUNCTIONS ERN 
    ERT - 
      HELP STATUS_FUNCTIONS ERT 
    EXP - 
      HELP ALGEBRA_FUNCTIONS 
    HCS - 
      HELP TRIG_FUNCTIONS 
    HPOS - 
      HELP STATUS_FUNCTIONS HPOS 
    HSN - 
      HELP TRIG_FUNCTIONS 
    HTN - 
      HELP TRIG_FUNCTIONS 
    IDA - 
      HELP STATUS_FUNCTIONS IDA 
    INSTR - 
      HELP STRING_FUNCTIONS INSTR_ 
    INT - 
      HELP ALGEBRA_FUNCTIONS 
    KEY - 
      HELP STATUS_FUNCTIONS KEY_ 
    KEY$ - 
      HELP STATUS_FUNCTIONS KEY$_ 
    KYEN - 
      HELP STATUS_FUNCTIONS KYEN_ 
    KYES - 
      HELP STATUS_FUNCTIONS KYES_ 
    KYF - 
      HELP STATUS_FUNCTIONS KYF_ 
    KYF$ - 
      HELP STATUS_FUNCTIONS KYF$_ 
    KYL - 
      HELP STATUS_FUNCTIONS KYL_ 
    KYL$ - 
      HELP STATUS_FUNCTIONS KYL$_ 
    LBE - 
      HELP STATUS_FUNCTIONS LBE 
    LEFT$ - 
      HELP STRING_FUNCTIONS LEFT$ 
    LEN - 
      HELP STRING_FUNCTIONS LEN 
    LGT - 
      HELP ALGEBRA_FUNCTIONS 
    LIN - 
      HELP PRINT_FUNCTIONS LIN_ 
    LOC$ - 
      HELP STRING_FUNCTIONS LOC$ 
    LOG - 
      HELP ALGEBRA_FUNCTIONS 
    LOG10 - 
      HELP ALGEBRA_FUNCTIONS 
    LOG2 - 
      HELP ALGEBRA_FUNCTIONS 
    LTW - 
      HELP ALGEBRA_FUNCTIONS 
    LWRC$ - 
      HELP STRING_FUNCTIONS LOC$ 
    MAR - 
      HELP STATUS_FUNCTIONS MAR_ 
    MAX - 
      HELP ALGEBRA_FUNCTIONS 
    MID$ - 
      HELP STRING_FUNCTIONS MID$ 
    MIN - 
      HELP ALGEBRA_FUNCTIONS 
    MNE - 
      HELP STATUS_FUNCTIONS MNE 
    MOD - 
      HELP ALGEBRA_FUNCTIONS 
    NUM - 
      HELP STATUS_FUNCTIONS NUM_ 
    NUM$ - 
      HELP CONVERSION_FUNCTIONS NUM$ 
    PLACE$ - 
      HELP DECIMAL_FUNCTIONS PLACE$_ 
    POS - 
      HELP STRING_FUNCTIONS POS_ 
    PPOS - 
      HELP STRING_FUNCTIONS PPOS 
    PPS - 
      HELP STATUS_FUNCTIONS PPS 
    PROD$ - 
      HELP DECIMAL_FUNCTIONS PROD$ 
    QUO$ - 
      HELP DECIMAL_FUNCTIONS QUO$ 
    RAD - 
      HELP TRIG_FUNCTIONS 
    REP$ - 
      HELP STRING_FUNCTIONS REP$ 
    RIGHT$ - 
      HELP STRING_FUNCTIONS RIGHT$ 
    RND - 
      HELP ALGEBRA_FUNCTIONS 
    RNS - 
      HELP STATUS_FUNCTIONS RNS 
    SCN - 
      HELP STRING_FUNCTIONS SCN 
    SEC - 
      HELP TRIG_FUNCTIONS 
    SEG$ - 
      HELP STRING_FUNCTIONS SEG$ 
    SEND$ - 
      HELP STATUS_FUNCTIONS SEND$_ 
    SIN - 
      HELP TRIG_FUNCTIONS 
    SINH - 
      HELP TRIG_FUNCTIONS 
    SPC - 
      HELP PRINT_FUNCTIONS SPC 
    SQR - 
      HELP ALGEBRA_FUNCTIONS 
    SST$ - 
      HELP STRING_FUNCTIONS SST$ 
    STR$ - 
      HELP CONVERSION_FUNCTIONS STR$ 
    SUM$ - 
      HELP DECIMAL_FUNCTIONS SUM$ 
    TAB - 
      HELP PRINT_FUNCTIONS TAB 
    TAN - 
      HELP TRIG_FUNCTIONS 
    TANH - 
      HELP TRIG_FUNCTIONS 
    TIM - 
      HELP STATUS_FUNCTIONS TIM 
    TIME$ - 
      HELP STATUS_FUNCTIONS TIME$ 
    UPC$ - 
      HELP STRING_FUNCTIONS UPC$ 
    USR$ - 
      HELP STATUS_FUNCTIONS USR$ 
    VAL - 
      HELP CONVERSION_FUNCTIONS VAL 
    VPS - 
      HELP STATUS_FUNCTIONS VPS 
  function call - 
      HELP LET DESCRIPTION: 
  Functions -   
    Intrinsic - 
      HELP GOTO_DBERR_STATEMENT 
    Print Control - 
      HELP PRINT_FUNCTIONS 
    Status Information - 
      HELP STATUS_FUNCTIONS 
    String Manipulation - 
      HELP STRING_FUNCTIONS 
    String-Numeric - 
      HELP CONVERSION_FUNCTIONS 
    Trigonometric - 
      HELP TRIG_FUNCTIONS 
  Functions - 
      HELP GOTO_DBERR_STATEMENT 
  FUNCTIONS (SHOW option) - 
      HELP SHOW PARAMETERS: 
G 
  General Rules for Matrix Arithmetic - 
      HELP MATRIX_RULES 
  generating ASCII file output - 
      HELP MAT_PRINT# DESCRIPTION: 
  generating formatted ASCII file records - 
      HELP MAT_PRINT#_USING DESCRIPTION: 
  generating formatted character records - 
      HELP PRINT#_USING DESCRIPTION: 
  generating labeled output - 
      HELP PRINT DESCRIPTION: 
  generating unlabeled output - 
      HELP PRINT DESCRIPTION: 
  GET mode - 
      HELP MAT_SIM EXAMPLES: 
      HELP OPEN USAGE_NOTES: 
  GET: Statement - 
      HELP GET: 
  getting data from binary files - 
      HELP MAT_GET: DESCRIPTION: 
  GO Command - 
      HELP GO 
  GO SUB Statement - 
      HELP GOSUB_RETURN PARAMETERS: 
  GOODBYE Command - 
      HELP GOODBYE 
  GOSUB Statement - 
      HELP GOSUB_RETURN PARAMETERS: 
  GOSUB-RETURN Statement - 
      HELP GOSUB_RETURN 
  GOSUBS (SHOW option) - 
      HELP SHOW PARAMETERS: 
  GOTO Statement - 
      HELP GOTO 
H 
  Halting Program Execution - 
      HELP BREAK DESCRIPTION: 
  HCS Function - 
      HELP TRIG_FUNCTIONS 
  HELP Command - 
      HELP HELP 
  HPOS Function - 
      HELP STATUS_FUNCTIONS HPOS 
  HSN Function - 
      HELP TRIG_FUNCTIONS 
  HTN Function - 
      HELP TRIG_FUNCTIONS 
I 
  I-D-S/II Interface - 
      HELP CALLING_A_USER_DEFINED_FUNCTION 
  I/O (input/output) stream - 
      HELP MAT_SIM EXAMPLES: 
  IBEX Statement - 
      HELP IBEX 
  IDA Function - 
      HELP STATUS_FUNCTIONS IDA 
  IF Modifier - 
      HELP IF 
  IF-THEN Statement - 
      HELP IF_THEN 
  IF-THEN-ELSE Statement - 
      HELP IF_THEN_ELSE 
  IF-THEN-ENDIF Statement - 
      HELP IF_THEN_ENDIF 
  IMAGE Statement (:) - 
      HELP PRINT_USING PARAMETERS: 
  increment - 
      HELP FOR_NEXT PARAMETERS: 
  increment expression - 
      HELP FOR_NEXT USAGE_NOTES: 
  index limit - 
      HELP DIM USAGE_NOTES: 
  INDEXED (indexed) - 
      HELP OPEN PARAMETERS: 
  indexed files - 
      HELP MAP EXAMPLES: 
  initial value - 
      HELP FOR_NEXT PARAMETERS: 
  initializing arrays as matrixes - 
      HELP DIM DESCRIPTION: 
  initializing arrays as vectors - 
      HELP DIM DESCRIPTION: 
  initiating execution of source program - 
      HELP FAST DESCRIPTION: 
  inner product - 
      HELP MAT_INNER_PRODUCT DESCRIPTION: 
  INPUT# Statement - 
      HELP INPUT# 
  input lines - 
      HELP MAT_INPUT USAGE_NOTES: 
  INPUT mode - 
      HELP OPEN USAGE_NOTES: 
  input reply - 
      HELP INPUT USAGE_NOTES: 
  INPUT Statement - 
      HELP INPUT 
  inputting elements of an array - 
      HELP MAT_INPUT DESCRIPTION: 
  inserting program documentation - 
      HELP REM DESCRIPTION: 
  INSTR Function - 
      HELP STRING_FUNCTIONS INSTR_ 
  INT Function - 
      HELP ALGEBRA_FUNCTIONS 
  int parameter - 
      HELP PARAMS 
  Integer Numeric Fields - 
      HELP INTEGER_NUMERIC 
  intrinsic functions - 
      HELP GOTO_DBERR_STATEMENT 
  inversion - 
      HELP MAT_INV USAGE_NOTES: 
J 
  JOB card - 
      HELP BATCH PARAMETERS: 
K 
  key - 
      HELP FILE_RULES 
  KEY Function - 
      HELP STATUS_FUNCTIONS KEY_ 
  key parameter - 
      HELP PARAMS 
  Key type -   
    CONSEC - 
      HELP OPEN PARAMETERS: 
    INDEXED - 
      HELP OPEN PARAMETERS: 
    NKEY - 
      HELP OPEN PARAMETERS: 
    SKEY - 
      HELP OPEN PARAMETERS: 
  KEY$ Function - 
      HELP STATUS_FUNCTIONS KEY$_ 
  KYEN Function - 
      HELP STATUS_FUNCTIONS KYEN_ 
  KYES Function - 
      HELP STATUS_FUNCTIONS KYES_ 
  KYF Function - 
      HELP STATUS_FUNCTIONS KYF_ 
  KYF$ Function - 
      HELP STATUS_FUNCTIONS KYF$_ 
  KYL Function - 
      HELP STATUS_FUNCTIONS KYL_ 
  KYL$ Function - 
      HELP STATUS_FUNCTIONS KYL$_ 
L 
  LAST Command - 
      HELP LAST 
  LBE Function - 
      HELP STATUS_FUNCTIONS LBE 
  LEFT$ Function - 
      HELP STRING_FUNCTIONS LEFT$ 
  Left-justified Alphanumeric Fields - 
      HELP LEFT_JUSTIFIED_ALPHANUMERIC 
  LEN Function - 
      HELP STRING_FUNCTIONS LEN 
  LET Statement - 
      HELP LET 
  LGT Function - 
      HELP ALGEBRA_FUNCTIONS 
  LIBERR - 
      HELP WHEN PARAMETERS: 
  limit - 
      HELP FOR_NEXT PARAMETERS: 
  limit expression - 
      HELP FOR_NEXT USAGE_NOTES: 
  LIN Function - 
      HELP PRINT_FUNCTIONS LIN_ 
  line - 
      HELP GOSUB_RETURN PARAMETERS: 
  line disconnections - 
      HELP BASIC_COMMAND DESCRIPTION_2: 
  line list - 
      HELP LIST PARAMETERS: 
  linear equations - 
      HELP MAT_SIM USAGE_NOTES: 
  LINK Statement - 
      HELP LINK 
  LINPUT# Statement - 
      HELP LINPUT# 
  LINPUT Statement - 
      HELP LINPUT 
  LIST Command - 
      HELP LIST 
  listing all files - 
      HELP CATALOG DESCRIPTION: 
  listing BASIC created files - 
      HELP CATALOG DESCRIPTION: 
  listing HELP information - 
      HELP HELP DESCRIPTION: 
  listing highest numbered line - 
      HELP LAST DESCRIPTION: 
  LOAD Command - 
      HELP LOAD 
  loading a source program - 
      HELP LOAD DESCRIPTION: 
  LOC$ Function - 
      HELP STRING_FUNCTIONS LOC$ 
  LOG Function - 
      HELP ALGEBRA_FUNCTIONS 
  LOG10 Function - 
      HELP ALGEBRA_FUNCTIONS 
  LOG2 Function - 
      HELP ALGEBRA_FUNCTIONS 
  loops - 
      HELP FOR_NEXT DESCRIPTION: 
  LTW Function - 
      HELP ALGEBRA_FUNCTIONS 
  LWRC$ Function - 
      HELP STRING_FUNCTIONS LOC$ 
M 
  MANDATORY - 
      HELP DBMEMBERINFO$ DESCRIPTION: 
  MANUAL - 
      HELP DBMEMBERINFO$ DESCRIPTION: 
  MAP statement -   
    arrays - 
      HELP MAP USAGE_NOTES: 
  MAP Statement - 
      HELP MAP 
  Mapping -   
    arrays - 
      HELP MAP USAGE_NOTES: 
  MAR Function - 
      HELP STATUS_FUNCTIONS MAR_ 
  MARGIN Statement - 
      HELP MARGIN 
  MAT ADDITION and SUBTRACTION Statement - 
      HELP MAT_ADDITION 
  MAT ADDITION Statement - 
      HELP MAT_ADDITION 
  MAT Arithmetic Statements - 
      HELP MATRIX_RULES 
  MAT ASSIGNMENT Statement - 
      HELP MAT_ASSIGNMENT 
  MAT CON Statement - 
      HELP MAT_CON 
  MAT DBNAMES$ Statement - 
      HELP MAT_DBNAMES$ 
  MAT DBTYPES Statement - 
      HELP MAT_DBTYPES 
  MAT GET: Statement - 
      HELP MAT_GET: 
  MAT IDN Statement - 
      HELP MAT_IDN 
  MAT INNER PRODUCT Statement - 
      HELP MAT_INNER_PRODUCT 
  MAT INPUT# Statement - 
      HELP MAT_INPUT# 
  MAT INPUT Statement - 
      HELP MAT_INPUT 
  MAT INV Statement - 
      HELP MAT_INV 
  MAT MULTIPLICATION BY SCALAR Statement - 
      HELP MAT_MULTIPLICATION 
  MAT NUL Statement - 
      HELP MAT_NUL 
  MAT PRINT# Statement - 
      HELP MAT_PRINT# 
  MAT PRINT# USING Statement - 
      HELP MAT_PRINT#_USING 
  MAT PRINT Statement - 
      HELP MAT_PRINT 
  MAT PRINT USING Statement - 
      HELP MAT_PRINT_USING 
  MAT PUT: Statement - 
      HELP MAT_PUT: 
  MAT READ Statement - 
      HELP MAT_READ 
  MAT SIM Statement - 
      HELP MAT_SIM 
  MAT statements -   
    MAT ADDITION - 
      HELP MAT_ADDITION 
    MAT ASSIGNMENT - 
      HELP MAT_ASSIGNMENT 
    MAT CON - 
      HELP MAT_CON 
    MAT IDN - 
      HELP MAT_IDN 
    MAT INNER PRODUCT - 
      HELP MAT_INNER_PRODUCT 
    MAT INV - 
      HELP MAT_INV 
    MAT MULTIPLICATION BY SCALAR - 
      HELP MAT_MULTIPLICATION 
    MAT NUL - 
      HELP MAT_NUL 
    MAT SIM - 
      HELP MAT_SIM SYNTAX: 
    MAT SUBTRACTION - 
      HELP MAT_ADDITION 
    MAT TRANSPOSE - 
      HELP MAT_TRANSPOSE 
    MAT ZER - 
      HELP MAT_ZER 
  MAT SUBTRACTION Statement - 
      HELP MAT_ADDITION 
  MAT TRANSPOSE Statement - 
      HELP MAT_TRANSPOSE 
  MAT ZER Statement - 
      HELP MAT_ZER 
  mathematical inverse - 
      HELP MAT_INV DESCRIPTION: 
  matrix arithmetic, general rules for - 
      HELP MATRIX_RULES 
  Matrixes -   
    adding - 
      HELP MAT_ADDITION DESCRIPTION: 
    array of various solutions - 
      HELP MAT_SIM DESCRIPTION: 
    assigning elements - 
      HELP MAT_ASSIGNMENT DESCRIPTION: 
    identity matrix - 
      HELP MAT_IDN DESCRIPTION: 
    inner product - 
      HELP MAT_INNER_PRODUCT DESCRIPTION: 
    mathematical inverse - 
      HELP MAT_INV DESCRIPTION: 
    multiplying by scalar - 
      HELP MAT_MULTIPLICATION DESCRIPTION: 
    null strings - 
      HELP MAT_NUL DESCRIPTION: 
    setting a specific value - 
      HELP MAT_CON DESCRIPTION: 
    setting values to zero - 
      HELP MAT_ZER DESCRIPTION: 
    subtracting - 
      HELP MAT_ADDITION DESCRIPTION: 
    transposing - 
      HELP MAT_TRANSPOSE DESCRIPTION: 
  matrixes - 
      HELP DIM DESCRIPTION: 
      HELP MAT_INPUT USAGE_NOTES: 
      HELP LET DESCRIPTION: 
      HELP MAT_READ USAGE_NOTES: 
  MAX Function - 
      HELP ALGEBRA_FUNCTIONS 
  MID$ Function - 
      HELP STRING_FUNCTIONS MID$ 
  MIN Function - 
      HELP ALGEBRA_FUNCTIONS 
  MNE Function - 
      HELP STATUS_FUNCTIONS MNE 
  MOD - 
      HELP MAT_DBTYPES 
  MOD Function - 
      HELP ALGEBRA_FUNCTIONS 
  mode - 
      HELP OPEN PARAMETERS: 
  MODE (SHOW option) - 
      HELP SHOW PARAMETERS: 
  MONERR - 
      HELP WHEN PARAMETERS: 
  monitor aborts - 
      HELP BASIC_COMMAND DESCRIPTION_2: 
  Multiple Statement Function Definition - 
      HELP COMPLEX_FUNCTION_DEFINITION 
  multiplication operator - 
      HELP OPERATORS 
N 
  name parameter - 
      HELP FID PARAMETERS: 
  NEW Command - 
      HELP NEW 
  NEXT Statement - 
      HELP FOR_NEXT DESCRIPTION: 
  NEXTS (SHOW option) - 
      HELP SHOW PARAMETERS: 
  NKEY (numeric key) - 
      HELP OPEN PARAMETERS: 
  NOWARN - 
      HELP OPTION SYNTAX: 
  NRESAVE Command - 
      HELP NRESAVE 
  NSAVE Command - 
      HELP NSAVE 
  NSEAL Command - 
      HELP NSEAL 
  NULL Statement - 
      HELP NULL 
  NUM Function - 
      HELP STATUS_FUNCTIONS NUM_ 
  NUM$ Function - 
      HELP CONVERSION_FUNCTIONS NUM$ 
  num-expr parameter - 
      HELP PARAMS 
  num-var parameter - 
      HELP PARAMS 
  Numeric Constants -   
    scaled integer - 
      HELP NUMERIC_CONSTANTS 
    scaled real - 
      HELP NUMERIC_CONSTANTS 
    unscaled integer - 
      HELP NUMERIC_CONSTANTS 
    unscaled real - 
      HELP NUMERIC_CONSTANTS 
  numeric matrixes - 
      HELP MAT_SIM USAGE_NOTES: 
  Numeric replacement fields -   
    circumflex - 
      HELP EXPONENTIAL_NUMERIC DESCRIPTION: 
    decimal - 
      HELP NUMERIC_REPLACEMENT_FIELDS 
      HELP DECIMAL_NUMERIC 
    exponential - 
      HELP NUMERIC_REPLACEMENT_FIELDS 
      HELP EXPONENTIAL_NUMERIC 
    integer - 
      HELP NUMERIC_REPLACEMENT_FIELDS 
      HELP INTEGER_NUMERIC 
    pound signs - 
      HELP EXPONENTIAL_NUMERIC DESCRIPTION: 
    rules - 
      HELP NUMERIC_REPLACEMENT_FIELDS 
    up arrow - 
      HELP EXPONENTIAL_NUMERIC DESCRIPTION: 
  Numeric Replacement Fields - 
      HELP NUMERIC_REPLACEMENT_FIELDS 
  numeric underflow - 
      HELP INPUT USAGE_NOTES: 
O 
  OFF Command - 
      HELP OFF 
  ON Statement - 
      HELP ON 
  OPEN statement -   
    key type - 
      HELP OPEN PARAMETERS: 
    mode - 
      HELP OPEN PARAMETERS: 
    precision - 
      HELP OPEN PARAMETERS: 
  OPEN Statement - 
      HELP OPEN 
  operator aborts - 
      HELP BASIC_COMMAND DESCRIPTION_2: 
  Operators -   
    addition - 
      HELP OPERATORS 
    arithmetic - 
      HELP OPERATORS 
    concatenation - 
      HELP STRING_EXPRESSIONS 
    division - 
      HELP OPERATORS 
    exponentiation - 
      HELP OPERATORS 
    multiplication - 
      HELP OPERATORS 
    subtraction - 
      HELP OPERATORS 
  OPTION PRECISION - 
      HELP OPTION USAGE_NOTES: 
  OPTION Statement -   
    BASE - 
      HELP OPTION SYNTAX: 
    DOUBLE - 
      HELP OPTION SYNTAX: 
    NOWARN - 
      HELP OPTION SYNTAX: 
    SINGLE - 
      HELP OPTION SYNTAX: 
    UNDERFLOW - 
      HELP OPTION SYNTAX: 
    WARN - 
      HELP OPTION SYNTAX: 
  OPTION Statement - 
      HELP OPTION 
  OPTIONAL - 
      HELP DBMEMBERINFO$ DESCRIPTION: 
  optional modes - 
      HELP OPTION DESCRIPTION: 
  OR expression - 
      HELP IF_THEN USAGE_NOTES: 
  order of precedence - 
      HELP EXPRESSIONS PARAMETER: 
  output - 
      HELP PRINT DESCRIPTION: 
  output in tabular form - 
      HELP PRINT DESCRIPTION: 
  OVER - 
      HELP RESAVE PARAMETER: 
  OVERFLOW - 
      HELP OPTION PARAMETERS: 
P 
  PAGE Statement - 
      HELP PAGE 
  Parameter abbreviations -   
    adescr - 
      HELP PARAMS 
    aname - 
      HELP PARAMS 
    const - 
      HELP PARAMS 
    int - 
      HELP PARAMS 
    key - 
      HELP PARAMS 
    num-expr - 
      HELP PARAMS 
    num-var - 
      HELP PARAMS 
    repl-field - 
      HELP PARAMS 
    simp-var - 
      HELP PARAMS 
    str-expr - 
      HELP PARAMS 
    str-var - 
      HELP PARAMS 
    stream - 
      HELP PARAMS 
    var - 
      HELP PARAMS 
    variablename - 
      HELP PARAMS 
  password parameter - 
      HELP FID PARAMETERS: 
  PLACE$ Function - 
      HELP DECIMAL_FUNCTIONS PLACE$_ 
  PLATEN command - 
      HELP PAGE USAGE_NOTES: 
  POS Function - 
      HELP STRING_FUNCTIONS POS_ 
  pound signs - 
      HELP INTEGER_NUMERIC DESCRIPTION: 
      HELP EXPONENTIAL_NUMERIC DESCRIPTION: 
  PPOS Function - 
      HELP STRING_FUNCTIONS PPOS 
  PPS Function - 
      HELP STATUS_FUNCTIONS PPS 
  precedence, order of - 
      HELP EXPRESSIONS PARAMETER: 
  PRECISION - 
      HELP OPTION USAGE_NOTES: 
  PRECISION (SHOW option) - 
      HELP SHOW PARAMETERS: 
  precision parameter - 
      HELP OPEN PARAMETERS: 
  Precision setting -   
    DOUBLE - 
      HELP OPEN PARAMETERS: 
    SINGLE - 
      HELP OPEN PARAMETERS: 
  Precision setting - 
      HELP DIGITS PARAMETER: 
  PRINT# Statement - 
      HELP PRINT# 
  PRINT# USING Statement - 
      HELP PRINT#_USING 
  print list - 
      HELP PRINT USAGE_NOTES: 
  PRINT mode - 
      HELP OPEN USAGE_NOTES: 
  PRINT Statement - 
      HELP PRINT 
  PRINT USING Statement - 
      HELP PRINT_USING 
  printing HELP information - 
      HELP HELP DESCRIPTION: 
  printing source program - 
      HELP LIST DESCRIPTION: 
  PROCEED Command - 
      HELP PROCEED 
  PROCEED Statement - 
      HELP PROCEED_STATEMENT 
  PROD$ Function - 
      HELP DECIMAL_FUNCTIONS PROD$ 
  producing ASCII file output - 
      HELP MAT_PRINT# DESCRIPTION: 
  producing file records - 
      HELP MAT_PRINT#_USING DESCRIPTION: 
  Program Execution Control Statements - 
      HELP CHANGE EXAMPLES: 
  PROMPT Statement - 
      HELP PROMPT 
  prompting string - 
      HELP INPUT PARAMETERS: 
      HELP LINPUT PARAMETERS: 
  PUT mode - 
      HELP MAT_SIM EXAMPLES: 
      HELP OPEN USAGE_NOTES: 
  PUT: Statement - 
      HELP PUT: 
Q 
  Q Command - 
      HELP Q 
  QUO$ Function - 
      HELP DECIMAL_FUNCTIONS QUO$ 
  quoted string - 
      HELP OPEN USAGE_NOTES: 
R 
  RAD Function - 
      HELP TRIG_FUNCTIONS 
  RANDOMIZE Statement - 
      HELP RANDOMIZE 
  READ access - 
      HELP DATA USAGE_NOTES: 
  READ Statement - 
      HELP READ 
  reading data from binary files - 
      HELP GET: DESCRIPTION: 
  READPT (SHOW option) - 
      HELP SHOW PARAMETERS: 
  Record mapping -   
    arrays - 
      HELP MAP USAGE_NOTES: 
  REENTER Command - 
      HELP REENTER 
  relational-expression - 
      HELP IF_THEN PARAMETERS: 
      HELP IF_THEN_ENDIF PARAMETERS: 
  relational-operator - 
      HELP IF_THEN PARAMETERS: 
      HELP IF_THEN_ENDIF PARAMETERS: 
  REM Statement - 
      HELP REM 
  RENAME Command - 
      HELP RENAME 
  renaming the current workspace - 
      HELP RENAME DESCRIPTION: 
  RENUMBER Command - 
      HELP RENUMBER 
  renumbering unnumbered file - 
      HELP SEQUENCE DESCRIPTION: 
  REP$ Function - 
      HELP STRING_FUNCTIONS REP$ 
  repl-field parameter - 
      HELP PARAMS 
  replacement fields - 
      HELP PRINT_USING USAGE_NOTES: 
  replacing an existing file - 
      HELP WRESAVE DESCRIPTION: 
  replacing working storage - 
      HELP WLOAD DESCRIPTION: 
  requesting data - 
      HELP INPUT DESCRIPTION: 
  rereading an existing line - 
      HELP RR DESCRIPTION: 
  RESAVE command - 
      HELP SAVE DESCRIPTION: 
  RESAVE or SAVE OVER Command - 
      HELP RESAVE 
  Reserved Words - 
      HELP RESERVED_WORDS 
  resource - 
      HELP ENQE PARAMETERS: 
      HELP ENQS PARAMETERS: 
  RESTORE Statement - 
      HELP RESTORE 
      HELP RESTORE# 
  resuming execution after break - 
      HELP GO DESCRIPTION: 
  resuming program execution - 
      HELP PROCEED_STATEMENT DESCRIPTION: 
  RETRY process - 
      HELP MAT_INPUT USAGE_NOTES: 
  RETRY request - 
      HELP INPUT USAGE_NOTES: 
  RETURN statement - 
      HELP GOSUB_RETURN DESCRIPTION: 
  returning to run-time error line - 
      HELP GOTO_ERL_STATEMENT 
  RIGHT$ Function - 
      HELP STRING_FUNCTIONS RIGHT$ 
  Right-justified Alphanumeric Fields - 
      HELP RIGHT_JUSTIFIED_ALPHANUMERIC 
  RND function - 
      HELP RANDOMIZE DESCRIPTION: 
      HELP ALGEBRA_FUNCTIONS 
  RNS function - 
      HELP RANDOMIZE DESCRIPTION: 
      HELP STATUS_FUNCTIONS RNS 
  RR Command - 
      HELP RR 
  Rules -   
    file I/O - 
      HELP FILE_RULES 
  RUN Command - 
      HELP RUN 
  run-time error - 
      HELP LET DESCRIPTION: 
  run-time prompt character - 
      HELP PROMPT DESCRIPTION: 
  RUNH - 
      HELP BATCH PARAMETERS: 
      HELP RUN PARAMETER: 
S 
  SAVE or SAVE ON Command - 
      HELP SAVE 
  SAVE OVER command - 
      HELP SAVE DESCRIPTION: 
  saving a file without line numbers - 
      HELP NRESAVE DESCRIPTION: 
  saving a source program - 
      HELP SAVE DESCRIPTION: 
  saving generated code - 
      HELP CODESAVE DESCRIPTION: 
  saving working storage environment - 
      HELP WSAVE DESCRIPTION: 
  scalar - 
      HELP MAT_MULTIPLICATION DESCRIPTION: 
  scaled integer - 
      HELP NUMERIC_CONSTANTS 
  scaled real - 
      HELP NUMERIC_CONSTANTS 
  SCN Function - 
      HELP STRING_FUNCTIONS SCN 
  SEAL Command - 
      HELP SEAL 
  sealing and saving unnumbered file - 
      HELP NSEAL DESCRIPTION: 
  SEC Function - 
      HELP TRIG_FUNCTIONS 
  SEG$ Function - 
      HELP STRING_FUNCTIONS SEG$ 
  SEND$ Function - 
      HELP STATUS_FUNCTIONS SEND$_ 
  SEQUENCE Command - 
      HELP SEQUENCE 
  setting optional modes - 
      HELP OPTION DESCRIPTION: 
  setting run-time prompt - 
      HELP PROMPT DESCRIPTION: 
  SGN Function - 
      HELP ALGEBRA_FUNCTIONS 
  shared file access, effective use of - 
      HELP DEQ DESCRIPTION: 
  SHARED mode - 
      HELP OPEN USAGE_NOTES: 
  SHOW Command - 
      HELP SHOW 
  SHOW Options -   
    ALL - 
      HELP SHOW PARAMETERS: 
    BASE - 
      HELP SHOW PARAMETERS: 
    BREAKS - 
      HELP SHOW PARAMETERS: 
    DELIMS - 
      HELP SHOW PARAMETERS: 
    DIM - 
      HELP SHOW PARAMETERS: 
    FILES - 
      HELP SHOW PARAMETERS: 
    FNS - 
      HELP SHOW PARAMETERS: 
    FUNCTIONS - 
      HELP SHOW PARAMETERS: 
    GOSUBS - 
      HELP SHOW PARAMETERS: 
    MODE - 
      HELP SHOW PARAMETERS: 
    NEXTS - 
      HELP SHOW PARAMETERS: 
    PRECISION - 
      HELP SHOW PARAMETERS: 
    READPT - 
      HELP SHOW PARAMETERS: 
    TRACES - 
      HELP SHOW PARAMETERS: 
    VARS - 
      HELP SHOW PARAMETERS: 
  SHOW Options - 
      HELP SHOW PARAMETERS: 
  sign - 
      HELP NUMERIC_CONSTANTS 
  simp-var parameter - 
      HELP PARAMS 
  Simple Alphanumeric Fields - 
      HELP SIMPLE_ALPHANUMERIC 
  Simple Expressions - 
      HELP EXPRESSIONS 
  simple variable names - 
      HELP VARIABLES SYNTAX: 
  SIN Function - 
      HELP TRIG_FUNCTIONS 
  SINGLE - 
      HELP OPTION SYNTAX: 
  SINGLE mode - 
      HELP OPEN USAGE_NOTES: 
  Single Statement Function Definition - 
      HELP FUNCTION_DEFINITION 
  SINH Function - 
      HELP TRIG_FUNCTIONS 
  size of a buffer - 
      HELP MAP USAGE_NOTES: 
  SKEY (string key) - 
      HELP OPEN PARAMETERS: 
  SPC function - 
      HELP PRINT USAGE_NOTES: 
      HELP PRINT_FUNCTIONS SPC 
  SQR Function - 
      HELP ALGEBRA_FUNCTIONS 
  SST$ Function - 
      HELP STRING_FUNCTIONS SST$ 
  standard functions - 
      HELP GOTO_DBERR_STATEMENT 
  Standard I-D-S/II Functions - 
      HELP IDS_STATEMENTS 
  START Command - 
      HELP START 
  statement summary - 
      HELP EXAMPLES_OF_CP_6_BASIC_I_D_S/II 
  STEP Command - 
      HELP STEP 
  STEP option - 
      HELP FOR_NEXT PARAMETERS: 
  STOP Statement - 
      HELP STOP 
  stopping a display - 
      HELP LIST DESCRIPTION: 
  stopping program execution - 
      HELP BREAK DESCRIPTION: 
  storing a source program - 
      HELP SAVE DESCRIPTION: 
  STR$ Function - 
      HELP CONVERSION_FUNCTIONS STR$ 
  str-expr - 
      HELP PROMPT PARAMETERS: 
      HELP DELIMIT PARAMETERS: 
  str-expr parameter - 
      HELP PARAMS 
  str-var - 
      HELP LET PARAMETERS: 
  str-var parameter - 
      HELP PARAMS 
  stream - 
      HELP DELIMIT PARAMETERS: 
      HELP ENQE PARAMETERS: 
  Stream assignments -   
    OPEN statement - 
      HELP OPEN 
  stream parameter - 
      HELP PARAMS 
  string array - 
      HELP VARIABLES SYNTAX: 
  string array element substring assignment - 
      HELP LET SYNTAX: 
  String expressions -   
    concatenation operator - 
      HELP STRING_EXPRESSIONS 
  String Expressions - 
      HELP STRING_EXPRESSIONS 
  string variable - 
      HELP OPEN USAGE_NOTES: 
  subscript calculations - 
      HELP LET DESCRIPTION: 
  subscript expression - 
      HELP READ USAGE_NOTES: 
  Subscript Expressions - 
      HELP SUBSCRIPT_EXPRESSIONS 
  substring assignment - 
      HELP LET SYNTAX: 
  subtraction operator - 
      HELP OPERATORS 
  SUM$ Function - 
      HELP DECIMAL_FUNCTIONS SUM$ 
  supplying elements of an array - 
      HELP MAT_INPUT DESCRIPTION: 
  synchronization - 
      HELP PUT: USAGE_NOTES: 
  Syntactical Abbreviations - 
      HELP PARAMS 
  SYS Command - 
      HELP SYS 
T 
  TAB function - 
      HELP PRINT USAGE_NOTES: 
      HELP PRINT_FUNCTIONS TAB 
  TAN Function - 
      HELP TRIG_FUNCTIONS 
  TANH Function - 
      HELP TRIG_FUNCTIONS 
  target array - 
      HELP MAT_INPUT USAGE_NOTES: 
  text string - 
      HELP VARIABLES 
  THEN statement - 
      HELP IF_THEN USAGE_NOTES: 
  TIM Function - 
      HELP STATUS_FUNCTIONS TIM 
  TIME$ Function - 
      HELP STATUS_FUNCTIONS TIME$ 
  time-out - 
      HELP INPUT PARAMETERS: 
  TRACE Statement - 
      HELP TRACE 
  TRACES (SHOW option) - 
      HELP SHOW PARAMETERS: 
  tracking program flow - 
      HELP TRACE DESCRIPTION: 
  true - 
      HELP IF_THEN USAGE_NOTES: 
  truth-expression - 
      HELP IF_THEN PARAMETERS: 
      HELP IF_THEN_ENDIF PARAMETERS: 
U 
  UNDERFLOW - 
      HELP OPTION SYNTAX: 
  UNLESS Modifier - 
      HELP UNLESS 
  unquoted text string - 
      HELP INPUT USAGE_NOTES: 
  UNSAVE Command - 
      HELP UNSAVE 
  unscaled integer - 
      HELP NUMERIC_CONSTANTS 
  unscaled real - 
      HELP NUMERIC_CONSTANTS 
  UNTIL Modifier - 
      HELP UNTIL 
  up arrow - 
      HELP EXPONENTIAL_NUMERIC DESCRIPTION: 
  UPC$ Function - 
      HELP STRING_FUNCTIONS UPC$ 
  UPDATE mode - 
      HELP OPEN USAGE_NOTES: 
      HELP PUT: USAGE_NOTES: 
  user-defined function - 
      HELP VARIABLES SYNTAX: 
  user-defined functions - 
      HELP DECIMAL_FUNCTIONS SUM$ 
  using calculator mode - 
      HELP END_COMMAND DESCRIPTION: 
  USR$ Function - 
      HELP STATUS_FUNCTIONS USR$ 
V 
  VAL Function - 
      HELP CONVERSION_FUNCTIONS VAL 
  var - 
      HELP INPUT PARAMETERS: 
  var parameter - 
      HELP PARAMS 
  variable - 
      HELP READ PARAMETERS: 
  variablename parameter - 
      HELP PARAMS 
  Variables -   
    array names - 
      HELP VARIABLES 
    simple variable names - 
      HELP VARIABLES 
  Variables - 
      HELP VARIABLES 
  VARS (SHOW option) - 
      HELP SHOW PARAMETERS: 
  vectors - 
      HELP DIM DESCRIPTION: 
      HELP MAT_INPUT USAGE_NOTES: 
      HELP LET DESCRIPTION: 
      HELP MAT_READ USAGE_NOTES: 
  VPS Function - 
      HELP STATUS_FUNCTIONS VPS 
W 
  wait time - 
      HELP ENQE PARAMETERS: 
  WARN - 
      HELP OPTION SYNTAX: 
  WEAVE Command - 
      HELP WEAVE 
  WFSAVE Command - 
      HELP WFSAVE 
  WHEN BREAK - 
      HELP WHEN PARAMETERS: 
  WHEN DBERR - 
      HELP WHEN PARAMETERS: 
  WHEN EOF - 
      HELP WHEN PARAMETERS: 
      HELP FILE_RULES 
  WHEN ERROR - 
      HELP WHEN PARAMETERS: 
  WHEN LIBERR - 
      HELP WHEN PARAMETERS: 
  WHEN MONERR - 
      HELP WHEN PARAMETERS: 
  WHEN Statement - 
      HELP WHEN 
  WHILE Modifier - 
      HELP WHILE 
  WLOAD Command - 
      HELP WLOAD 
  WRESAVE Command - 
      HELP WRESAVE 
  writing numeric data to binary file - 
      HELP PUT: DESCRIPTION: 
  writing records to a file - 
      HELP PRINT# DESCRIPTION: 
  writing values to a binary file - 
      HELP MAT_PUT: DESCRIPTION: 
  WSAVE Command - 
      HELP WSAVE 
  WSEAL Command - 
      HELP WSEAL 
X 
  X Command - 
      HELP X_COMMAND 
  XREF Command - 
      HELP XREF 
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
[line] IBEX str-expr 
Parameters: 
str-expr    is a valid IBEX command. 
Description: 
The IBEX statement passes a string to the CP-6 executive processor (IBEX) for 
execution as an IBEX command.  An error results if the str-expr is not a valid 
IBEX command.  At completion, execution resumes with the statement following 
the IBEX statement. 
Example: 
    IBEX "STATUS" 
Means print the status of the system. 
00002
00003
00001
The following is a brief description of the standard I-D-S/II functions (i.e., 
the BASIC statements that do data base manipulation). 
[line] DB ACCEPT num-var [FROM] [recordname] CURRENCY 
                                        [realmname ] 
                                       [setname   ] 
[line] DB ACCEPT str-var [FROM] [recordname] REALMNAME 
                                       [dbkey     ] 
                                                {NEXT    } 
[line] DB ACCEPT num-var [FROM] setname {PRIOR   } 
                                                {CURRENCY} 
                                                {OWNER   } 
[line] DB BUFFERS exp,num-var 
[line] DB CALC num-var recordname 
[line] DB CHECK integer 
[line] DB CONNECT [recordname] [TO] setname 
[line] DB CRPT integerexp 
[line] DB DISCONNECT [recordname] [FROM] setname 
[line] DB ERASE [recordname] [ALL MEMBERS] 
                                       {dbkey          } 
[line] DB FIND [recordname] DBKEY [IS] {num-var} 
[line] DB FIND ANY recordname 
[line] DB FIND DUPLICATE recordname 
[line] DB FIND DUPLICATE [WITHIN] setname [USING] itemlist 
               {FIRST                      } 
               {NEXT                       } 
[line] DB FIND {PRIOR [recordname] [WITHIN]} {setname  } 
               {LAST                       } {realmname} 
               {integer or num-var } 
                                             {setname  } 
[line] DB FIND CURRENT [recordname] [WITHIN] {realmname} 
                                             {keyname  } 
[line] DB FIND OWNER [WITHIN] setname 
[line] DB FIND recordname WITHIN setname CURRENT [[USING] itemlist] 
               {FIRST [recordname]} 
[line] DB FIND {NEXT  [recordname]} USING keyname 
               {recordname        } 
[line] DB FINISH [realmnamelist] 
[line no[ DB GET [recordname] 
[line] DB GET identifierlist 
[line] DB KEEP 
                              [ONLY      {ALL        }             ] 
[line] DB MODIFY [recordname] [INCLUDING {setnamelist} [MEMBERSHIP]] 
                                     {ALL        } 
[line] DB MODIFY itemlist [INCLUDING {setnamelist} [MEMBERSHIP]] 
                       {GET   } 
[line] DB PRIVACY ITEM {MODIFY} privacykey itemlist 
                      {CONNECT   } 
[line] DB PRIVACY SET {DISCONNECT} privacykey [setnamelist] 
                      {FIND      } 
                          {CONNECT                       } 
                          {DISCONNECT                    } 
 [line] DB PRIVACY RECORD {ERASE privacykey [record list]} 
                          {GET                           } 
                          {MODIFY                        } 
                          {STORE                         } 
                            {UPDATE    [SHARE]   } 
                            {RETRIEVAL [SHAREIN] } 
[line] DB READY [realmlist] {LCAD      [NOSHARE] } 
                            {          [SHAREANY]} 
                            {          [SHARECUR]} 
[line] DB REDUCEQ 
                 {REALM      } 
                 {RECORD     } 
[line] DB RETAIN {SETS       } 
                 {setnamelist} 
[line] DB ROLL 
[line] DB RPTSTATS 
[line] DB STATSOFF 
[line] DB STATSON 
[line] DB STORE recordname 
[line] DB TRACEOFF [integer] 
[line] DB TRACEON [integer] 
NOTE:  On RETAIN and PRIVACY the user may specify more than one keyword 
       from the lists. 
Syntax: 
[line] statement1 IF truth-expression 
Parameters: 
statement1    specifies any allowable BASIC statement. 
truth-expression    is any numeric expression. 
Description: 
The IF modifier defines a condition which controls execution of a statement. 
The statement is executed only when the expression is true. 
Examples: 
At the IF modifier, BASIC checks to see whether the IF statement is true or 
false.  If the statement is true (i.e., if A=2), then the statement is 
executed. 
    20 A = 10 
    30 B = 20 IF A = 2 
    40 PRINT B 
    50 END 
00002
00003
00001
Syntax: 
[line] IF truth-expression {THEN statement|{THEN|GOTO}line} 
Parameters: 
truth-expression    is defined as: 
    [relational-expression [{AND|OR} relational-expression]... 
relational-expression    is defined as: 
    expression relational-operator expression 
    where 
    expression    is either an arithmetic expression or a string expression. 
    relational-operator    is one of the following: 
        Symbol        Meaning 
        ------        ------- 
        <             Less than 
        <= or =<      Less than  or equal to 
        <> or ><      Not equal to 
        >             Greater than 
        >= or =>      Greater than or equal to 
        =             Equal to 
statement    is a single executable BASIC statement (excluding DEF, FNEND or 
another IF statement). 
line    is a line number. 
Description: 
The IF-THEN statement transfers control to a specified line number.  The 
transfer is conditionally based upon the truth of a relational expression or a 
combination of relational expressions.  If the relational expression on an 
IF-THEN statement is true, all the statements in a multi-statement construct 
behave as with the IF-THEN-ENDIF construct.  If the condition is not true, all 
of the statements in a multi-statement construct which follow the THEN in an 
IF-THEN statement are bypassed during execution. 
Usage Notes: 
A relational expression yields either a true or false value.  An AND 
expression yields a true value if and only if the relational expressions to 
the right and left of it are true.  An OR expression yields a true value if 
either or both relational expressions to the right and left of it are true. 
The following examples illustrate the procedure to test for truth conditions 
in truth expressions: 
    IF A=B AND C=D+1 THEN 100 
    IF A$+B$="FISH" OR A$+D$="BIRD" THEN 100 
In the first line the arithmetic expression D+1 is resolved.  Then A is tested 
against B and C is tested against the value received after D+1 is resolved. 
If A is equal to B and C is equal to D+1, control is transferred to line 100. 
In the second example, A$ is concatenated to B$, then A$ is concatenated to 
D$.  The result of the first is compared to the string "FISH", and the result 
of the second concatenation is compared to the string "BIRD".  If either or 
both of these comparisons proves to be true, then control is transferred to 
line 100. 
Note that the operator order of precedence is: 
1.  Arithmetic operators, which can have several levels (such as A-(B*C)). 
2.  Relational operators, which can have one level only. 
3.  AND expressions. 
4.  OR expressions. 
Relations between arithmetic expressions consist of simple numeric comparisons 
of the values.  In cases where approximate relational tests are needed, the 
user must supply his own epsilon (or fuzz) value.  For example, E>ABS(A-B) can 
be used to test for the approximate equality of A versus B, where E functions 
as the user's epsilon. 
Characters in strings are compared in left-to-right order.  Comparison stops 
when corresponding characters from the two strings are not identical, or when 
the end of one or both strings is reached.  Character strings are equal only 
if they contain identical characters and are of the same length.  Any 
relational operator may be used to compare character strings. 
A compile-time error is reported if the expression between IF and THEN is not 
a truth expression as described above, or if the line number to which program 
flow is directed does not exist in the program. 
The conditional statement form of the IF statement operates the same as the 
conditional transfer form, except that program flow is not redirected.  The 
statement after the THEN statement is executed, and control is passed to the 
next executable line following the IF statement. 
Examples: 
    100 IF A$="DRAGON" THEN 800 
    200 IF (A$="DRAGON" OR A$="SERPENT") AND B1<SQR(10) THEN 900 
    220 IF A$="DRAGON" OR A$="SERPENT" AND B1<=SQR(10) GOTO 900 
    240 IF A$="DRAGON" OR (A$="SERPENT" AND B1<=SQR(10)) THEN 900 
    300 IF C>=10 AND C=<20 THEN 1000 
    500 IF A>=0 THEN LET B=SQR(A) 
    600 IF A<0 THEN PRINT "A NEGATIVE, NO SQUARE ROOT!" 
Line 100 transfers control to 800 only if A$ contains the six character string 
"DRAGON".  Line 200 transfers to 900 if B1 is less than the square root of 10 
and if A$ is either "DRAGON" or "SERPENT".  The lack of parentheses in line 
220 causes it to be analyzed differently than line 200.  Line 220 transfers to 
900 if either A$ is "SERPENT" and B1 is no greater than the square root of 10 
or A$ is "DRAGON".  Line 240 functions identically to line 220 but shows the 
order of operator precedence.  Line 300 illustrates how to test if a variable 
(C) lies within a closed range (10 to 20).  Note that when using the IF 
statement for conditional transfer, either THEN or GOTO may follow the truth 
expression. 
The evaluation of truth expressions may not require the evaluation of all the 
relational expressions contained to establish the overall true/false status. 
Thus the order of evaluation at the AND-OR level may be optimized.  It is 
safest to assume that any given relational expression will be evaluated. 
Calls to multiple line user-defined functions that may modify global variables 
should be avoided. 
Line 500 checks to see if A is positive, and if so, sets the variable B to the 
square root of A.  Line 600 tests if A is negative, and if so, prints a 
message to the user. 
00002
00004
00001
00003
Syntax: 
line IF truth-expression THEN 
line statement 
[line statements] 
   . 
   . 
   . 
line ELSE 
line statement 
[line statements] 
   . 
   . 
   . 
line ENDIF 
Parameters: 
truth-expression    is defined as: 
    [relational-expression [{AND|OR} relational-expression]... 
relational-expression    is defined as: 
    expression relational-operator expression 
    where 
    expression    is either an arithmetic expression or a string expression. 
    relational-operator    is one of the following: 
        Symbol        Meaning 
        ------        ------- 
        <             Less than 
        <= or =<      Less than  or equal to 
        <> or ><      Not equal to 
        >             Greater than 
        >= or =>      Greater than or equal to 
        =             Equal to 
statement    is a single executable BASIC statement (excluding DEF, FNEND or 
another IF statement). 
line    is a line number. 
Description: 
The IF-THEN-ELSE statement is a further expansion of BASIC's block-structured 
programming capability.  Two sets of statements are defined; the first set 
executes if the truth expression proves true, and the second set executes if 
the truth expression proves false.  The first set of statements follows the IF 
statement and is terminated by the ELSE statements; the second set of 
statements follows the ELSE statement and is terminated by an ENDIF statement; 
the second set of statements follows the ELSE statement and is terminated by 
an ENDIF statement, which also terminates the "block".  When either of the two 
sets is executed, execution resumes with the statement that immediately 
follows the ENDIF statement. 
00002
00001
Syntax: 
line IF truth-expression THEN 
line statement 
[line statements] 
   . 
   . 
   . 
line ENDIF 
Parameters: 
truth-expression    is defined as: 
    [relational-expression [{AND|OR} relational-expression]... 
relational-expression    is defined as: 
    expression relational-operator expression 
    where 
    expression    is either an arithmetic expression or a string expression. 
    relational-operator    is one of the following: 
        Symbol        Meaning 
        ------        ------- 
        <             Less than 
        <= or =<      Less than  or equal to 
        <> or ><      Not equal to 
        >             Greater than 
        >= or =>      Greater than or equal to 
        =             Equal to 
statement    is a single executable BASIC statement (excluding DEF, FNEND or 
another IF statement). 
line    is a line number. 
Description: 
The IF-THEN-ENDIF statement can also be used to perform block structured 
programming.  This is similar to the conditional statement form of IF-THEN, 
except that multiple statements are executed if the truth expression proves 
true.  The statements to be executed terminate with an ENDIF statement.  If 
the truth expression proves false, execution resumes at the statement 
immediately following the ENDIF statement.  IF blocks may be nested. 
00002
00001
Syntax: 
[line] INPUT[[:prompt$][;time-out],]var[,var]... 
Parameters: 
:prompt$    is the prompting string.  This is either a variable string of 511 
characters or a quoted string of up to 255 characters.  The (:) is used as a 
delimiter to distinguish the prompting string from a variable string.  If the 
time-out parameter is omitted, a comma must be used to separate the prompt 
from the variable. 
time-out    designates a time-out value (in seconds). 
var    refers to a single numeric value or text string, either a scalar 
(unsubscripted variable) or an element of an array.  Subscript expressions are 
permitted. 
If the user fails to respond to the input prompt within the specified number 
of seconds, an error is reported by BASIC.  (Error control can be utilized to 
transfer program-flow control to another location upon time-out.  See the WHEN 
statement.)  A time-out request in a batch job is ignored. 
Description: 
The INPUT statement requests data.  If the program is being run on-line, the 
source for this data is the user's terminal.  If the program is being run as a 
batch job, the source is the specified input stream. 
Usage Notes: 
When an INPUT statement is encountered during an on-line BASIC session, a 
question mark is printed to prompt the user that a value is being requested. 
If a prompt is already set by the PROMPT statement, it is turned off when a 
prompting string is specified in an INPUT statement.  It is the programmer's 
responsibility to indicate to the user what values are required.  This is can 
be done through the use of a preceding PRINT statement or a :prompt$ prompting 
string in the INPUT statement.  The prompt should describe the variables and 
the requirements and/or limitations involved in a proper reply to the input 
request. 
When an INPUT statement is encountered during a batch BASIC job, the input 
device is activated; if the proper values are not received, the program aborts 
(unless the program includes an error control that transfers program-flow to 
another area in the program). 
The syntax of an input reply has the form: 
    datum[,datum]...[,] 
datum    represents either a valid BASIC string, enclosed in quotation marks, 
or an unquoted text string. 
The following rules apply for input replies: 
1.  An unquoted text string may represent either a numeric constant or may be 
    accessed as a text string.  Unquoted text strings that are proper 
    representations of numeric constants may be treated as text strings or 
    numeric values, depending on the variable to which they are assigned. 
2.  Empty unquoted text strings are invalid. 
3.  A text-string datum that includes a comma (or any other delimiter 
    designated by a prior DELIMIT statement) must be enclosed within quotes. 
4.  An unquoted text string may include blanks, but leading and trailing 
    blanks are not considered significant.  Because internal blanks are 
    significant, blanks are not normally used as delimiters (see the DELIMIT 
    statement). 
5.  An unquoted text string may not include internal quotation marks. 
When an INPUT statement is encountered, program execution is suspended until 
one of the following three events take place: 
1.  A complete input reply is received. 
2.  Time-out occurs. 
3.  An input reply supplies more data than is requested. 
If an input reply ends with a comma, BASIC responds by issuing a prompt for 
additional input, and a new input call is issued, unless the current data list 
already contains as many or more values than those required.  The trailing 
comma permits the use of several input lines (or cards) to provide a single 
input reply. 
Input replies are scanned for validity before any value is assigned to a 
variable.  The number of elements in the reply must correspond to the number 
of variables in the INPUT statement, and each datum must be appropriate for 
assignment to the corresponding variable in the INPUT statement.  For numeric 
variables, the datum is always an unquoted text string that is a correct 
representation of a single numeric value and cannot exceed the numeric 
overflow limits in BASIC.  A numeric value that is less than the numeric 
underflow limitations is replaced by zero. 
If the scan of the input reply has not resulted in a syntax error, the data 
values are assigned to the variables in the INPUT statement in left to right 
order.  The evaluation of a subscript expression for a variable is made 
immediately before any assignment of a datum value to that variable.  For 
example, the statement INPUT I,A(I) has a different meaning and effect than 
the statement INPUT A(I),I. 
If an error condition is recognized while matching the input data list to the 
INPUT statement variable list (see the READ statement), no assignments are 
made and an error message is printed.  If the user is on-line, the error 
message is followed by a request for reentry of the entire input.  For batch 
jobs, the message is followed by the line number of the INPUT statement and by 
a printout of the input reply; the program is then aborted.  If an input reply 
contains no data, the error message is not followed by a RETRY request.  If a 
subscript expression evaluates to a number that exceeds the dimensional range 
of the array, an error occurs and no RETRY request is made. 
Examples: 
    200 INPUT A 
    300 INPUT A,A$,B(A),B$(A+1) 
    400 INPUT;15,X 
    500 INPUT: "HELLO",NAME$ 
Line 200 requests a single numeric value.  Line 300 requests four values.  The 
first and third values must be numeric.  The value input for A determines the 
subscript values for the third and fourth entries.  Line 400 contains an INPUT 
statement with a time-out option.  If the user fails to supply a value for X 
within 15 seconds, an error is reported.  If the program has included error 
control, the error message is suppressed, and program execution proceeds at 
the line number specified by the WHEN statement.  Line 500 contains an INPUT 
statement with a prompting string called "HELLO" and a character string 
variable called NAME$. 
In line 300, if the input reply for the first value is not numeric, no 
assignments to values are made, and a RETRY is requested.  If the value 15 is 
assigned to A, and vector B is currently dimensioned to 20 elements, but 
string vector B$ is dimensioned to only 10 elements, assignments will be made 
to A, A$, and B(15) before the error is detected.  Once the error is detected, 
program execution stops and an error message is printed that specifies the 
line number of the INPUT statement and the number of the offending item. 
00002
00004
00001
00003
Syntax: 
[line] INPUT# stream[;key][,CRPT=str-expr][,var]...[,] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of the key 
which points to the record at which the read is to begin.  If indexed files 
are used, the key format is: 
    [;KEY num-expr[EQ str-expr]] 
    where 
    num-expr    is an integer representing the primary key if the value is 
    zero or the "nth" specified alternate key if it is greater than zero.  If 
    num-expr is not specified, the next sequential record for the most 
    recently processed key (or primary key if there is none) is read.  If 
    num-expr is specified alone, the next sequential record for that key is 
    read. 
    str-expr    is a string representing the value of the KEY. 
    For example: 
    300 INPUT#1;KEY N1 EQ KEY1$ 
    Line 300 reads from stream number 1, for the (first) record whose N1st key 
    is equal to the value contained in KEY1$. 
CRPT=str-expr    specifies the encryption seed for data files.  The seed can 
be entered as a string of characters of length less than or equal to 4.  If a 
seed has a length of 1 to 3, it will be right justified and ".000" is placed 
in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write.  The 
CRPT parameter is not specified when using indexed files. 
var    is a valid BASIC variable that is to be assigned a value from the data 
file.  The var parameter is not specified when using indexed files. 
Description: 
The INPUT# statement reads a record from an ASCII file. 
Usage Notes: 
When BASIC encounters an INPUT# statement, the stream number is rounded to an 
integer (if it is not already one) and then evaluated.  For an INPUT# 
statement to be valid, the stream must be currently open for input via an OPEN 
statement in the INPUT or UPDATE mode. 
If a key is included, the file is positioned to the record indicated by the 
key.  If a key is not specified and the input buffer does not include unused 
values from a prior INPUT# on the same stream, the next record in the sequence 
is accessed. 
Data access and assignment of values to variables in the list is carried out 
in much the same way terminal input is effected, except that if a record does 
not contain enough data values, the next record is accessed.  If a record 
supplies more values than required, an error is not reported. 
If an INPUT# statement does not end with a comma, the unused values are 
discarded and a subsequent INPUT# statement on the same stream will access the 
next record of the data file.  If the INPUT# statement ends with a comma, 
unused values in the data file are retained in an input buffer and are used to 
satisfy the next INPUT# request followed by items from the next sequential 
record.  The use of a trailing comma thus provides for asynchronous input. 
(See the discussion of the INPUT statement for data type requirements.) 
If an INPUT# with a trailing comma is followed by an INPUT# with a key, the 
record specified by that key will not be read, if the input request is 
satisfied by items left in the input buffer.  See the WHEN statement. 
If a prompting string is specified with the INPUT# statement, it is ignored by 
BASIC.  See the INPUT statement for information on prompting strings. 
Examples: 
    200 INPUT# M;K-1,A 
    300 INPUT# 3,B$,C, 
Line 200 accesses the stream indicated by M, sets the key value to K-1, and 
accesses a single numeric value, which is assigned to the scalar variable A. 
Any unused values are discarded.  Line 300 reads the next available data from 
stream number 3, which may include unused values from a prior INPUT# from 
stream 3.  A textual value is accessed and assigned to B$, and a numeric value 
is accessed and assigned to the scalar variable C.  The trailing comma retains 
any remaining values in the current record for later use. 
00002
00004
00001
00003
Syntax: 
#[#...] 
Description: 
These fields are represented by one or more pound signs. 
The pound signs are replaced by the integer value of the numeric variable. 
Fractional portions are truncated, the number is right-justified, and the 
unused field positions are filled with blanks.  The sign of the value is 
included in the field width and is printed as a blank for positive values or a 
minus sign for negative values.  If the number of characters in the integer 
value including the minus sign for the negative values is greater than the 
number of characters in the field, the field is filled with asterisks. 
Usage Notes: 
The total number of pound signs to a numeric replacement field cannot be 
greater than 62. 
Examples: 
    100 LET X=1.23 
    200 LET Y=-12.3 
    300 LET Z=123 
    400 LET Z1=-123 
    500 LET Z2=1234 
    600 LET Z3=-1234 
    700 PRINT USING "###", X,Y,Z,Z1,Z2,Z3 
Line 700 prints the message: 
      1 
    -12 
    123 
    *** 
    *** 
    *** 
NOTE:  Because Z1 requires four characters (one for the minus sign and three 
digits), it is too large for the replacement field specified in line 700.  It 
is not printed, instead the field is filled with asterisks.  This is also true 
for Z2 and Z3.  The following table illustrates several types of integer 
numeric fields; combined with control characters (described in full below). 
The sequence of values 1, -12, 123, -1234, etc., is inserted into each field 
until the size of the number exceeds the size of the field, at which point a 
line of asterisks is printed. 
#####  $####  $$$##  +####  ++++#  -####  --###  $,$$$,$$# 
    1  $   1    $ 1  +   1     +1      1      1         $1 
  -12  $ -12   $-12  -  12    -12  -  12   - 12       $-12 
  123 $ 123 $123 + 123 +123 123 123 $123 -1234 ***** ***** -1234 -1234 -1234 
-1234 $-1,234 *****                *****  *****  *****  *****    $12,345 
                                                 ********* 
00001
00003
00002
Syntax: 
LAS[T] 
Description: 
The LAST command lists the highest numbered line of the source program in 
working storage. 
00001
Syntax: 
'L[L...] 
Description: 
These fields are represented by an apostrophe followed by one or more L 
characters. 
The apostrophe and the L are replaced by characters from the string variable. 
If the string is shorter than the field, the area to the right of the filled 
portion of the field is padded with blanks.  If the string is longer than the 
field, all characters to the right of the field are truncated. 
Examples: 
    100 LET C$="MAGICK" 
    200 LET D$="GRIMOIRE" 
    300 PRINT USING "'LLLLLL", C$, D$ 
Line 300 prints the message: 
    MAGICK 
    GRIMOIR 
The format-string contained within the PRINT USING statement is used twice. 
C$ is padded with one blank to fill the replacement field, and D$ is truncated 
on the right so that it fits within the field. 
00001
00002
Syntax: 
[line] [LET] num-var[=num-var]...=num-expr (for numeric assignment) 
    or 
[line] [LET] str-var[=str-var]...=str-expr (for string assignment) 
    or 
[line] [LET] str-var(:num-expr1, num-expr2)=str-expr  (substring assignment) 
    or 
[line] [LET] str-var(:num-expr1, num-expr2)(num-expr3, num-expr4)=str-expr 
(string array element substring assignment) 
Parameters: 
str-var    is a valid string variable. 
num-var    is a valid numeric variable. 
num-expr    is any valid numeric expression. 
str-expr    is any valid string expression. 
num-expr1    is the position of the first character of the substring.  The 
colon (:) is used to introduce the starting position of a substring. 
num-expr2    is the length of a substring. 
num-expr3    is the left element of the array variable. 
num-expr4    is the right element of the array variable. 
Description: 
The LET statement assigns the value of an expression to one or more variables. 
Note that the LET is optional. 
When a LET statement is encountered by BASIC, the value of the expression is 
computed and assigned to all variables in the LET list.  All subscript 
calculations, both in the variables and in the expression, are made prior to 
any assignment of values.  This makes the specific order of the variables in 
the statement unimportant. 
A constant, expression, or function call cannot be used as a target for 
assignment via the LET statement.  A single LET statement cannot include both 
string and numeric expressions or variables.  Any attempt to access or assign 
values outside the current dimensions of vectors or matrixes results in a 
run-time error.  Note that the colon (:) is used to introduce the starting 
position of a substring. 
Examples: 
    100 LET A1=SQR(2) 
    200 X=1 
    300 LET A(X)=X=X+1 
    400 LET X=1 
    500 X=A(X)=X+1 
    600 LET A$=B$="IRA" 
Line 100 assigns the value of the square root of 2 to the variable A1.  Line 
200 assigns the value of 1 to the variable X.  Line 300 yields the result 
A(1)=2, and X=2.  Line 400 resets the value of X to 1.  Line 500 also yields 
the result A(1)=2 and X=2.  Note that subscripts are calculated before 
assignments are made.  Line 600 assigns the string expression "IRA" to the 
string variables A$ and B$.  The following is an example of substring 
assignment: 
    10 DIM A$(3,4) 
    20 A$(:3,2)(2,3)="ABCDEF" 
    30 B$(:2,1)=SST$(A$(2,3),3,1) 
    40 PRINT A$(2,3);B$ 
    50 END 
The result is:  bbABbA (See SST$ under the topic STRING_FUNCTIONS). 
00002
00003
00001
Syntax: 
[line] LINK str-expr1[,str-expr2] 
Parameters: 
str-expr1    specifies the run unit to which control is to be transferred. If 
no account is specified, the user's directory account is assumed.  (Thus :SYS 
must be specified when calling other CP-6 processors.) 
str-expr2    specifies a "command" that is to be read and interpreted by the 
first input request of the run unit for which control has transferred. 
Description: 
The LINK statement transfers control to any run unit in the system.  At 
completion, control remains with the run unit.  When this run unit is exited, 
BASIC is re-entered, and control returns to the statement that follows the 
LINK statement. 
Examples: 
LINK "PCL.:SYS", "COPY MYFILE TO LP(VFC)" 
00002
00003
00001
Syntax: 
[line] LINPUT[:prompt$][;time-out,]str-var[,str-var]... 
Parameters: 
:prompt$    is the prompting string.  This is either a variable string of 511 
characters or a quoted string of up to 255 characters.  The (:) is used as a 
delimiter to distinguish the prompting string from a variable string.  If the 
time-out parameter is omitted, a comma must be used to separate the prompt 
from the variable. 
time-out    designates a time-out value (in seconds). 
str-var    is a valid string variable. 
Description: 
The LINPUT statement requests that each line of input be considered a single 
text string to be assigned to a string variable.  If a prompting string is 
specified, it is repeated for each line of input.  If a prompt is already set 
by a PROMPT statement, it is suspended while the prompting string is specified 
in an LINPUT statement. 
Usage Note: 
The operation of the LINPUT statement is the same as that for the INPUT 
statement, except that a single LINPUT statement may require several lines of 
input with intervening prompts.  Each line of input reply is treated as a 
single string datum.  No characters are considered to be delimiters, and there 
are no invalid replies.  (The MARGIN statement limits both input and output.) 
Examples: 
    320 LINPUT A$,B$(5) 
    500 LINPUT;10, C$ 
    600 LINPUT "PROMPTSTRING", A$ 
Line 320 requests two lines of input.  The first line is assigned to A$, and 
the second to the fifth element of the string vector B$.  Line 500 specifies 
that input for C$ must be provided within 10 seconds.  Line 600 specifies 
"PROMPTSTRING" as a prompting string before input to A$. 
00002
00004
00001
00003
Syntax: 
[line] LINPUT# stream[;key][,CRPT=str-expr],str-var[,str-var]... 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of the key 
at which the read is to begin. 
CRPT=str-expr    specifies the encryption seed for data files.  The seed can 
be entered as a string of characters of length less than or equal to 4.  If a 
seed has a length of 1 to 3, it will be right justified and ".000" is placed 
in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write. 
str-var    is a valid string variable. 
Descriptions: 
The LINPUT# statement is a variation of the INPUT# statement in which each 
record of input is considered to be a single text string, for assignment to a 
string variable.  LINPUT# operates the same as INPUT#, except that input is 
defined as one string datum per record.  The LINPUT# statement may not be used 
for indexed file operations. 
Usage Note: 
A trailing comma is invalid in a LINPUT# statement. 
If a prompting string is specified with the LINPUT# statement, it is ignored 
by BASIC.  See the LINPUT statement for information on prompting strings. 
Examples: 
    320 LINPUT# 2;K1,A$,B$(5) 
    340 LINPUT# 1,C$ 
Line 320 reads from stream number 2, starting with the record with key value 
K1; this record is assigned to A$, and the next record is assigned to B$(5). 
Line 340 reads the next record from stream number 1 and assigns the text 
string to C$.  LINPUT# always accesses a data record. 
00002
00004
00001
00003
Syntax: 
LIS[T] [line-list] 
Parameters: 
line-list    is a list of line numbers and/or line ranges, separated by 
commas.  There are three types of line ranges.  Given the line numbers n and 
m, where n is smaller than m, the following ranges may be constructed: 
    Range        Meaning 
    -----        ------- 
    n-m          From line n to m. 
    -n           From the beginning of the program to line n. 
    m-           From line m to the end of the program. 
Description: 
The LIST command prints all or selected parts of the source program in working 
storage on the output medium. 
A display by LIST may be stopped by pressing the BREAK key at the terminal. 
Lines longer than the platen width currently in affect are listed on two or 
more lines. 
Examples: 
    LIST 
    LIST 200,100 
    LIST -500,1000- 
    LIST 200-400 
The first command lists the entire program in working storage.  The second 
command lists line 200 and then line 100.  The third command lists all lines 
up to and including line 500, followed by all the lines from 1000 to the end 
of the program.  The fourth command lists lines 200 to 400 inclusive. 
00002
00003
00001
Syntax: 
LOA[D] fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The LOAD command loads a saved BASIC source program into working storage, 
replacing whatever program may currently be there.  File records are read 
sequentially, and each record is validated as it is read.  Syntax errors are 
noted, and error lines are excluded from the program being formed.  The 
validation check of the input source lines is the same as for direct entry at 
the terminal. 
The line numbers need not be in order; BASIC rearranges them into ascending 
sequence.  Program input continues until the end of the file is reached.  LOAD 
does not affect existing named data values or the status of currently open 
data files; hence, a program that has been copied into working storage via the 
LOAD command may access existing data and opened data files. 
00002
00001
Syntax: 
line MAP [(]buffer[)] [ALIGNED|UNALIGNED] element[,element]... 
Parameters: 
buffer    is a valid numeric or string variable name.  The parentheses are 
optional. 
ALIGNED|UNALIGNED    is ignored, if present. 
element    is one or more of the following items, separated by commas, which 
are used to define a given field within a record: 
1.  A string variable or array name with dimension specifications, optionally 
    followed by "=m", where m is the fixed string length. 
2.  FILL$[=m] which reserves m character positions in a record. 
3.  FILL$(n)[=m] which reserves n*m characters in a record. 
Description: 
The MAP statement defines the format of a record by matching individual fields 
in a record with specific elements in the MAP statement.  The MAP statement is 
only used for indexed file operations.  Indexed files are processed by 
defining a buffer with the MAP statement. 
Usage Notes: 
The MAP statement must preceed an OPEN statement which references it, as well 
as any executable statements referencing elements included in it.  It may not 
be a direct statement.  Multiple MAP statements with the same name are 
permissible.  The statement representing the longest buffer must be specified 
first.  If the same element appears in more than one MAP statement of the same 
name, it must be in the same position in all instances. 
Arrays are specified by following the name with dimension(s) enclosed in 
parentheses.  Array dimensions precede the "=n" for string arrays.  Arrays may 
not be specified in a DIM statement or redimensioned once specified in a MAP 
statement.  The default length assigned to a string is 16. 
String data whose length is greater than the field defined in a MAP statement 
is truncated on the right for insertion in the buffer.  Data which is less 
than the field is left-justified and padded with blanks to the right. 
Normally, a FILL field contains the value from the previous input operation. 
However, if the last operation was not input, the value of the FILL field is 
unknown.  The contents of the buffer are also unknown following each 
recompilation of a program. 
If strings are converted to numerics using the VAL function and converted back 
to strings using the STR$ function prior to output, the optional imaging 
operand may be required for the STR$ function, to assure alignment of values 
and decimal points. 
The size of a buffer is set according to the way it is defined in a MAP 
statement.  The buffer is initially filled with blanks.  The contents of the 
buffer are modified only when: 
o   An INPUT# statement is executed which references the MAP statement in 
    question. 
o   The value of a string or element of a string array used in defining a MAP 
    statement has changed. 
Any PRINT# statement executed for indexed file processing uses the buffer 
content at the time of output for the content of the record which it outputs. 
Note that lists cannot be specified with the INPUT#, PRINT#, or PRINT# USING 
statements. 
Examples: 
10 MAP MAP1 A$=6,B$(2,3)=4,FILL$=96 
Line 10 defines the buffer named MAP1 by listing the elements in it. 
00002
00004
00001
00003
Syntax: 
[line] MARGIN[# num-expr1,] num-expr2 
Parameters: 
num-expr1    represents the stream number.  Zero indicates the user's terminal 
(or line printer for batch operation).  One through twelve represents the 
corresponding file output stream. 
num-expr2    sets the maximum number of characters per output line, and can be 
any number greater than 39.  For stream 0 (user's console), the maximum margin 
is 254 (see Usage Notes for greater margin for user's console). 
Description: 
The MARGIN statement provides for control of the line or record width for 
terminal and file PRINT and INPUT statements. 
Usage Notes: 
If MARGIN is set higher than the number of columns on a physical device, the 
last character may overprint or the output may continue on another line 
depending on device characteristics.  The numeric expressions are rounded to 
integer values if required. 
The MARGIN setting may be made whether a stream is currently open for file 
output or not, and resets to default on a CLOSE.  The default margin setting 
when BASIC is called is 72. 
MARGIN tracks a simple character count in the output and input line.  If the 
user includes backspaces, tab characters, line-feeds, etc., within the line, 
the physical carriage position will not correspond to the character count. 
Also, when accessing binary files through stream I/O, the MARGIN value is 
interpreted as number of words (36 bits) rather than number of characters.  If 
the user wants a greater margin for the user's console, the IBEX SET command 
is issued. 
00002
00001
00003
    The following operational rules apply to all MAT arithmetic statements: 
1.  A MAT statement may not be used to change a vector to a matrix or a matrix 
    to a vector. 
2.  If an error occurs during the processing of a MAT statement, the target 
    array is left undefined. 
3.  MAT arithmetic statements use current dimensions for arrays being accessed 
    and create dimensions for the target array. 
4.  If BASE=0, the zero row and column are included in the elements processed 
    by MAT statements. 
5.  Any MAT arithmetic statement results in an error if the assignment of 
    values to the target array exceeds the user's data space. 
6.  The determinant of a matrix is obtained by using the DET function. 
Syntax: 
[line] MAT aname1=aname2{+|-}aname3 
Parameters: 
aname1, aname2 and aname3    are the names of arrays. 
Description: 
The MAT ADDITION and SUBTRACTION statement creates a target array whose 
elements are the result of adding or subtracting elements with the same 
indexes within the argument arrays.  The arrays must be numeric, and the 
argument arrays must have the same current dimensions.  Vectors and matrixes 
may not be mixed in a MAT add or subtract. 
Examples: 
    300 MAT A=B+C 
    400 MAT V=W-X 
If B and C are 4 by 6 matrixes, then line 300 sets the current dimensions of 
array A to 4 by 6, and sets the values of the elements according to the 
formula A(i,j)=B(i,j)+C(i,j) for all values of i and j from BASE (0 or 1) for 
i=BASE to 4 and j=BASE to 6.  If W and X, for example, are vectors with 
current dimensions of 12, line 400 sets the current dimension of V to 12 and 
assigns V(i)=W(i)-X(i) for i=BASE to 12. 
00002
00003
00001
Syntax: 
[line] MAT aname1=aname2 
Parameters: 
aname1    identifies the target array. 
aname2    specifies an existing array whose elements are to be assigned to 
aname1. 
Description: 
The MAT ASSIGNMENT statement assigns the elements of an existing array to a 
target array. 
Usage Notes: 
The elements of the array to the right of the assignment symbol (=) are 
assigned to the array to the left of the assignment symbol.  The arrays may be 
string or numeric, but not a mixture.  Matrixes and vectors cannot be mixed. 
Examples: 
    100 MAT A=B 
    200 MAT C$=X$ 
Line 100 assigns the elements of array B to array A.  Line 200 assigns the 
elements of string array X$ to string array C$. 
00002
00004
00001
00003
Syntax: 
[line] MAT aname=[(expr1)*]CON[(num-expr1[,num-expr2])] 
Parameters: 
aname    is the target array name. 
expr1    is assigned to the elements specified by the numeric expressions 
following the keyword CON.  If this expression is omitted, the value of 1 is 
used as a default.  Note that this expression must be enclosed in parentheses. 
A string expression is permitted if the target is a string array.  The default 
for strings is the string of zero length.  This operation results in the 
setting of all items of aname to the value of expr1. 
num-expr1    are optional values (rounded to integral values as required). 
num-expr2    results in redefining the size of the aname array. 
Description: 
The MAT CON statement sets all elements of the target array to a specified 
value. 
Usage Notes: 
Error conditions are caused if aname and expr1 are not either both numeric or 
both strings, or if neither num-expr1 or num-expr2 are not strictly positive 
in value. 
If the expressions following the keyword CON are omitted, the current 
dimensions for the array are retained. 
Examples: 
    120 MAT B=CON(5,5) 
    130 MAT C=(-1)*CON(25) 
Line 120 assigns the value of 1 to the elements in array B; new dimensions, 
5,5 are assigned.  Line 130 assigns the value of -1 to the elements in array 
C; C is set to new dimensions and is now a vector length of 25. 
00002
00004
00001
00003
Syntax: 
[line] MAT aname = DBNAMES$ 
Description: 
This is a statement with no arguments that returns the names of all realms, 
sets, records, items and I-D-S/II keywords available through the current 
subschema.  The result is a string vector.  The size of aname is dynamically 
determined by the number of names returned. 
00001
Syntax: 
[line] MAT aname = DBTYPES 
Description: 
The result of this function is an N by 6 array.  The size of aname is 
dynamically modified if necessary.  The first element of each row indicates 
the type of object represented by that name as follows: 
    0 - REALM 
    1 - SET 
    2 - RECORD 
    3 - FIELD 
    4 - unused 
    5 - PARAMETER 
    6 - LOCK 
    7 - IDS KEYWORD 
    8 - KEY 
Record Type Information: 
For records the second column contains the location mode for the record: 
    0 - DIRECT 
    1 - CALC 
    2 - VIA SET 
    3 - SEQUENTIAL 
    4 - INDEXED 
The third column contains a set of flags for record or field types.  The bits 
are packed into a floating point number.  In order to access the first bit, 
the user types: 
    MOD(A(2,3),2) 
In order to access the second bit, the user types: 
    MOD(A(2,3)/2,2) 
and so on. 
The meaning of these flags is as follows: 
    First    - Name is in subschema 
    Second   - Name understood by I-D-S/II 
    Third    - STORE is allowed 
    Fourth   - MODIFY is allowed 
    Fifth    - DELETE is allowed 
    Sixth    - ERASE is allowed 
    Seventh  - Variable length 
    Eighth   - In multiple realms 
    Ninth    - Has alternate keys 
    Tenth    - An elementary item 
    Eleventh - Item is signed 
    Twelfth  - Item is scaled 
Field Type Information 
The second column for fields contains usage information.  The range of 
possible values are: 
    0 - DATA ITEM 
    1 - DATA BASE PARAMETER 
    2 - LOCATION MODE DIRECT FIELD 
    3 - REALM-ID FIELD 
    4 - CALC KEY SYNONYM FIELD 
    5 - SCAN KEY SYNONYM FIELD 
The third column for fields contains the same flag settings as for the record 
flags. 
The fourth column for fields contains the record number in DBNAMES$ that this 
field belongs to. 
The fifth column for fields contains the data type of this field.  The values 
are: 
    0  - TEXT 
    13 - SINGLE PRECISION FLOATING POINT 
    14 - DOUBLE PRECISION FLOATING POINT 
The sixth column for fields is used to indicate the length of text data items. 
Set Type Information 
The second column for sets indicates the mode of this set.  Valid mode values 
are: 
    0 - CHAIN 
    1 - RECORD ARRAY 
    2 - POINTER ARRAY 
The fourth column for sets indicates the index in DBNAMES$ of the record that 
owns the set. 
The fifth column for sets indicates the type of set that this is.  Set type 
values are: 
    0 - USER SET 
    1 - CALC SET 
    2 - PRIMARY KEY 
    3 - SECONDARY KEY 
The sixth column for sets indicates how this set is ordered.  The values are: 
    0 - FIRST 
    1 - LAST 
    2 - NEXT 
    3 - PRIOR 
    4 - SORTED BY KEY 
00001
Syntax: 
[line] MAT GET: stream[;key][,CRPT=str-expr],adescr[,adescr]... 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of a key 
which points to the record at which the read is to begin. 
CRPT=str-expr    specifies the encryption seed for binary data files.  The 
seed can be entered as a string of characters of length less than or equal to 
4.  If a seed has a length of 1 to 3, it will be right justified and ".000" is 
placed in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write. 
adescr    is an array descriptor of the form: 
    aname[(num-expr[,num-expr])] 
    where 
    aname    is a numeric array name that is to be read from the binary file. 
    num-expr    is a numeric expression representing the dimensions of aname. 
Description: 
The MAT GET: statement accesses data from binary files for assignment to array 
variables. 
Usage Notes: 
If an array descriptor does not specify dimensions, the current dimensions for 
the named array are used.  If dimensions are specified, their number must 
match those of the DIM statement for that array.  Matrixes may not be 
redimensioned to vectors or vice versa.  The array list is processed from left 
to right.  Individual arrays are filled according to row order. 
Examples: 
    400 MAT GET: 1;K3,A,B(5,5) 
    500 MAT GET: J,E(4) 
Line 400 accesses data from stream 1, starting at the record with key value 
K3. Array A is filled first, using its current dimensions.  Array B is 
dimensioned 5 by 5 and then filled.  Line 500 accesses data from the stream 
represented by the variable J, using the current file position (as no key is 
specified).  E is dimensioned to length 4, and then filled. 
00002
00004
00001
00003
Syntax: 
[line] MAT aname=IDN[(num-expr,num-expr)] 
Parameter: 
aname    is the target array name (must be numeric). 
num-expr    represents an optional value rounded to an integer.  If num-expr 
is not specified, the current dimensions are used.  In either case, the 
dimensions must be equal to define a square matrix. 
Description: 
The MAT IDN statement creates an identity matrix in which all diagonal 
elements (that is, elements with equal row and column indexes) are set to 1 
and all other elements are set to zero. 
Examples: 
    780 MAT K=IDN 
    790 MAT L=IDN(C5,C5) 
Line 780 creates an identity matrix K set to the current dimensions of K. 
Line 790 creates an identity matrix L, with the dimensions of the value 
represented by the variable C5.  Note that the value must be entered twice, 
specifying an identical value for column and row size. 
00002
00003
00001
Syntax: 
[line] MAT aname1=aname2*aname3 
Parameters: 
aname1    is the target array name. 
aname2    is an array to be multiplied by aname3. 
aname3    is an array to be multiplied by aname2. 
Description: 
The MAT INNER PRODUCT statement assigns a set of values to the target array 
that comprises the mathematical inner product of the argument arrays.  The 
second dimension of the first argument must be equal to the first dimension of 
the second argument.  All arrays must be numeric. 
Examples: 
    100 MAT A=B*C 
If the current dimensions of B are m,n then the current dimensions of C must 
be n,p and the dimensions of A will be m,p according to the formula given 
below: 
            k=n 
            ____ 
    A(i,j)= \    B(i,k)*C(k,j) 
            /___ 
            k=BASE 
The following special cases can occur: 
1.  If B is a matrix, and C is a vector of length n, C is handled as if it is 
    a one column matrix with dimensions n,1.  The dimensions of the resulting 
    array will be m,1. 
2.  If B is a vector of length n, and C is a matrix, B is handled as if it is 
    a one row matrix with dimensions 1,n.  The dimensions of the resultant 
    array will be 1,p. 
3.  If B and C are vectors of identical length, they are handled as one row 
    and one column matrixes, and the resultant array will be a one row, one 
    column matrix. 
00002
00003
00001
Syntax: 
[line] MAT INPUT aname[(num-expr[,num-expr])] 
Parameters: 
aname    is the name of an array. 
num-expr    is a numeric expression. 
Description: 
The MAT INPUT statement allows the user to supply the elements of an array. 
Note that arrays in BASIC are filled in row order. 
Usage Notes: 
If the target array is explicitly dimensioned in the MAT INPUT statement, the 
new dimensions override those of the corresponding DIM statement.  If the 
target array is not redimensioned explicitly, the processing is handled 
differently for vectors and matrixes.  For vectors, the array is implicitly 
redimensioned by the number of elements provided by the user.  For matrixes, 
the dimensions set by DIM or by prior redimensioning are used. 
The error conditions for MAT INPUT are the same as those for INPUT except that 
there is no check between the lengths of data lists and the lengths of 
variable lists.  Matrixes and vectors are handled differently.  If the number 
of input replies is insufficient to fill the current dimensions of a matrix, 
the unassigned portions are filled with zeros (numeric matrixes) or null 
strings (string matrixes).  If the number of input replies exceeds the current 
dimensions of a matrix, the excess values are ignored.  No diagnostic messages 
are issued in either case. 
Vectors are always redimensioned by MAT INPUT statements.  If the dimension is 
not specified in the MAT INPUT statement, the number of input replies becomes 
the dimension of the vector.  If the dimension is specified in the MAT INPUT 
statement, and the number of input replies is less than the dimension 
specified, then unassigned portions are filled with zeros (numeric vectors) or 
null strings (string vectors). 
The RETRY process for MAT INPUT (see the INPUT statement) refers only to the 
input line just entered, which may have been preceded by several input lines 
with trailing commas.  To abort the entire response, the user types an input 
line with no values.  A diagnostic message identifies the line at which 
execution stopped.  If the program includes error control or does not attempt 
RETRY if an array is only partially filled, the unfilled values are set to 
zero or null strings. 
Examples: 
    200 MAT INPUT JABBERWOCK(5) 
    300 MAT INPUT JABBERWOCK 
    500 MAT INPUT JUBJUB_BIRD$(4,5) 
    600 MAT INPUT JUBJUB_BIRD$ 
Line 200 requires five numeric values in the input reply, resulting in a 
vector with 5 elements (assuming BASE = 1).  Line 300 allows a variable number 
of numeric values in the input reply, and sets the current dimension of 
JABBERWOCK accordingly.  Line 500 dimensions JUBJUB_BIRD$, and requires 20 
string entries in the input reply.  Line 600 uses the current dimensions of 
JUBJUB_BIRD$ and requires the correct number of values in the input reply. 
Note that a statement like line 600 should be used only if the user is aware 
of the current dimensions, which will usually be those set by a DIM statement. 
00002
00004
00001
00003
Syntax: 
[line] MAT INPUT# stream[;key][,CRPT=str-expr],adescr[,adescr]...[,] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of the key 
which points to the record at which the read is to begin. 
CRPT=str-expr    specifies the encryption seed for data files.  The seed can 
be entered as a string of characters of length less than or equal to 4.  If a 
seed has a length of 1 to 3, it will be right justified and ".000" is placed 
in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write. 
adescr    is a valid array descriptor of the form: 
    aname[(num-expr[,num-expr])] 
    where 
    aname    is a numeric array name. 
    num-expr    is a numeric value representing the dimensions of aname. 
Description: 
The MAT INPUT# statement accesses ASCII file data for assignment to array 
variables.  The MAT INPUT# statement may not be used for indexed file 
operations. 
Usage Notes: 
MAT INPUT# is similar to MAT INPUT from the terminal, with the following 
exceptions: 
1.  As many records are read as are required to fill the arrays. 
2.  Several target arrays may be specified.  When one is filled, the next 
    datum is used to start filling the next array.  Therefore, successive 
    arrays in the same MAT INPUT# may be filled asynchronously with respect to 
    input record lengths. 
3.  If a target array is a vector without explicit dimensions, its current 
    dimension is used to determine the number of file elements that are to be 
    accessed.  This differs from terminal input, which allows the user to 
    assign a variable number of elements. 
Examples: 
    200 MAT INPUT# J;R1,B(5),A 
    300 MAT INPUT# J,C$, 
Line 200 accesses the stream indicated by the variable J at the record 
indicated by the variable R1.  The first five values are read into vector B. 
Values are then read into array A as determined by its current dimension 
setting.  Any unused values in the last record read are discarded.  Line 300 
reads string values from stream J into the array C$, using its current 
dimensions.  The trailing comma indicates that all unused values are held in 
the input buffer at the end of input. 
00002
00004
00001
00003
Syntax: 
[line] MAT aname1=INV(aname2) 
Parameters: 
aname1    is a square numeric array name. 
aname2    is a square numeric array name that is to be inverted. 
Description: 
The MAT INV statement results in the mathematical inverse of a square numeric 
matrix. 
Usage Notes: 
Both specified arrays must be square numeric matrixes.  An execution error 
will result if, within the precision of the computations used in inversion, no 
result can be developed satisfying the condition that the inner product of an 
array and its inverse is a reasonable approximation of an identity matrix. 
Many arrays are truly singular in the mathematical sense, and others may be 
reported as singular because they so closely approximate singularity that an 
inverse cannot be computed with reasonable accuracy. 
Examples: 
    100 MAT B=INV(A) 
    200 MAT C=B*A 
    300 MAT D=INV(B) 
Line 100 sets the value of the elements of B to the inverse of array A.  Line 
200 creates array C, which will closely approximate an identity matrix (within 
the precision limitations of the computational processes involved).  Line 300 
creates array D, which will closely approximate array A, by taking the inverse 
of the inverse of A. 
00002
00004
00001
00003
Syntax: 
[line] MAT aname1=(num-expr)*aname2 
Parameter: 
aname1    is the target array name. 
num-expr    represents the scalar value. 
aname2    is an array to be multiplied by the scalar value. 
Description: 
The MAT MULTIPLICATION BY SCALAR statement forms each element of the result by 
multiplying the corresponding element of the argument array by the value of 
the numeric expression. 
Usage Notes: 
All arrays must be numeric.  The numeric expression is evaluated once prior to 
assigning elements to the result.  Note that the numeric expression must 
always be enclosed in parentheses.  A compile-time error is reported if one 
array is a vector and the other a matrix. 
Examples: 
    250 MAT A=(SQR(2))*A 
    300 MAT C=(5)*B 
Line 250 multiples all elements of array A by the square root of two.  Line 
300 multiplies all elements of array B by 5. 
00002
00004
00001
00003
Syntax: 
[line] MAT aname=NUL[(num-expr[,num-expr])] 
Parameters: 
aname    is a string array name that is to be set to null. 
num-expr    represents an optional value (rounded to an integer) to set the 
current dimensions of the target array.  If none is specified, the existing 
current dimensions are retained. 
Description: 
The MAT NUL statement is similar to the MAT ZER statement described 
immediately above, but string arrays are involved, and the result consists of 
string elements of length zero (null strings). 
The specified array must be a string array. 
00002
00001
Syntax: 
[line] MAT PRINT aname ]{,|;}aname[...[{,|;}] 
Parameters: 
aname    is a numeric or string array name. 
Description: 
The MAT PRINT statement causes an entire array or set of arrays to be printed 
row by row. 
The MAT PRINT operation functions the same as a set of successive PRINT 
statements.  For each array, a PRINT statement would reference the elements of 
each row, with the indicated punctuation between elements.  This implies that 
each row of a matrix starts a new print line.  A row may, however, cause more 
than one physical line to be printed, depending upon the punctuation following 
the array name, the margin setting, the number of elements in each row, and 
the physical size of the output device.  (See the PRINT_STATEMENT for a 
description of the print zones used with a comma punctuator.) 
For string arrays, the semicolon causes the strings composing a row to run 
together with no intervening spaces. 
A trailing punctuation mark on a MAT PRINT statement does not indicate (as it 
does on a PRINT statement) that the line is not to be written out immediately; 
it is the punctuation control for the preceding array name.  If there is no 
trailing punctuation, a comma is assumed. 
Examples: 
    400 MAT PRINT A,A; 
    500 MAT PRINT B$,B$; 
In line 400, if A is a 2 by 10 matrix, and BASE=1, the MAT PRINT statement is 
equivalent to: 
    PRINT 
    PRINT A(1,1),A(1,2),...A(1,10) 
    PRINT A(2,1),A(2,2),...A(2,10) 
    PRINT 
    PRINT A(1,1);A(1,2);...A(1,10) 
    PRINT A(2,1);A(2,2);...A(2,10) 
In line 500, if B$ is a 4 element vector, and BASE=1, the MAT PRINT statement 
is equivalent to: 
    PRINT B$(1),B$(2),B$(3),B$(4) 
    PRINT B$(1);B$(2);B$(3);B$(4) 
00002
00003
00001
Syntax: 
[line] MAT PRINT# stream[;key][,CRPT=str-expr],aname & 
{,|;},aname]...[{,|;}] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of the key 
which points to the record at which the write is to begin. 
CRPT=str-expr    specifies the encryption seed for data files.  The seed can 
be entered as a string of characters of length less than or equal to 4.  If a 
seed has a length of 1 to 3, it will be right justified and ".000" is placed 
in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write. 
aname    is an array name that is to be printed out. 
Description: 
The MAT PRINT# statement generates ASCII file output from the data values in 
listed arrays.  The operation bears the same relationship to the MAT PRINT 
statement that PRINT# bears to the PRINT statement.  The examples given for 
the MAT PRINT statement show how arrays are formatted for printed output; 
similar MAT PRINT# statements generate ASCII records with characters. 
00002
00001
Syntax: 
[line] MAT PRINT# stream[;key][,CRPT=str-expr] & 
,USING{line|str-expr},aname[,aname]... 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of the key 
which points to the record at which the write is to begin. 
CRPT=str-expr    specifies the encryption seed for data files.  The seed can 
be entered as a string of characters of length less than or equal to 4.  If a 
seed has a length of 1 to 3, it will be right justified and ".000" is placed 
in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write. 
str-expr    is a string expression representing the format of the MAT PRINT# 
USING statement. 
aname    is an array name that is to be printed out. 
Description: 
The MAT PRINT# USING statement generates formatted ASCII file records with 
data drawn from arrays.  The operation of MAT PRINT# USING bears the same 
relationship to the MAT PRINT USING statement that PRINT# bears to the PRINT 
statement.  The MAT PRINT# USING statement may not be used for indexed file 
operations. 
00002
00001
Syntax: 
[line] MAT PRINT USING [line|str-expr],aname[,aname]... 
Parameters: 
str-expr    is a string expression representing the format of the PRINT 
statement. 
aname    is a numeric or string array name. 
Description: 
The MAT PRINT USING statement allows the image formatting of array elements in 
output lines. 
The MAT PRINT USING statement functions similarly to the PRINT USING 
statement.  The fields in the image statement or string are replaced by the 
elements of the listed arrays.  See the PRINT USING statement for further 
information. 
Example: 
    100 A$ = "###     ###    $#,###.##" 
    200 DIM C(5,3),B(6) 
    300 MAT PRINT USING A$,C,B 
The execution of line 300 will print 7 lines, each in the format described by 
A$.  Array C will generate 5 lines, one for each row.  The vector B will 
generate two lines, each of which uses 3 of the 6 elements (BASE=1). 
00002
00003
00001
Syntax: 
[line] MAT PUT: stream[;key][,CRPT=str-expr],aname[,aname]... 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of a key 
which points to the record at which the write is to begin. 
CRPT=str-expr    specifies the encryption seed for binary data files.  The 
seed can be entered as a string of characters of length less than or equal to 
4.  If a seed has a length of 1 to 3, it will be right justified and ".000" is 
placed in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write. 
aname    is an array name that is to be put into the file. 
Description: 
The MAT PUT: statement writes the values of numeric arrays to a binary file. 
Usage Notes: 
The operation of the MAT PUT: statement functions as though the contents of 
the indicated arrays are listed in row order as expressions in a PUT: 
statement. 
Examples: 
    200 MAT PUT:3;K2,C,D 
A record is started with the key indicated by K2, on stream number 3.  The 
values of arrays C and D are written into one or more records.  When more than 
one record is written, the keys of the subsequent records are incremented by 
1. 
00002
00004
00001
00003
Syntax: 
[line] MAT READ adescr[,adescr]... 
Parameter: 
adescr    is the name of a numeric or string array followed optionally by a 
dimensioning expression or expressions.  The syntax of adescr is: 
    aname[(num-expr[,num-expr])] 
where 
    num-expr    is a numeric expression representing the dimensions of the 
    array. 
Description: 
The MAT READ statement accesses data from the sequence of data representations 
contained in DATA statements, filling the elements of numeric or string arrays 
with this data. 
Usage Notes: 
MAT READ operates similarly to the READ statement, but possesses the following 
special characteristics: 
1.  If an adescr does not specify dimensions, current dimensions for the named 
    array are used.  If dimensions are specified, the number of the dimensions 
    must be identical to the number of dimensions defined by the corresponding 
    DIM statement.  In other words, vectors cannot be redimensioned into 
    matrixes and vice versa. 
2.  Arrays in the list of a MAT READ statement are processed from left to 
    right.  Each array is filled in row order. 
3.  If an error occurs during the assignment of elements to an array, arrays 
    to the left of the array in which the error occurred will have their new 
    values, while arrays to the right will retain their old values.  The array 
    in which the error actually occurs will contain new values starting in the 
    first row, up to the error point.  Values from the error point to the end 
    of the array will be zero or, in the case of a string array, will consist 
    of null strings. 
Examples: 
    400 MAT READ A,B(5,5),C$(20) 
    500 MAT READ D$,E(4) 
Arrays A and D$ will be dimensioned as specified by corresponding DIM 
statements.  Arrays B, C$, and E are dimensioned as specified.  If BASE = 0, 
the zero row and column are included in a MAT READ operation. 
00002
00004
00001
00003
Syntax: 
[line] MAT aname1=SIM(aname2,aname3) 
Parameters: 
aname1    is a numeric array representing the systems of linear equations 
described by aname1 and aname2. 
aname2    is a numeric array representing the argument matrix. 
aname3    is a numeric array name representing the coefficient matrix. 
Description: 
The MAT SIM statement creates an array composed of the various solutions to 
one or more systems of linear equations described by additional arrays. 
Usage Notes: 
The sample array names R, C, and E are used to help define the workings of the 
MAT SIM statement.  Given the statement: 
    MAT R=SIM(E,C) 
The arrays E and C describe one or more systems of linear equations, and R 
will be composed (after execution) of the solution or solutions to these 
equations.  Taken individually, these arrays have the following attributes: 
    C    is the coefficient matrix.  It must be a square matrix.  The 
         dimensions of C are n,n. 
    E    is the argument matrix.  Each column represents one set of arguments 
         for application to C.  E must contain the same number of rows as C. 
         The dimensions of E are n,k.  (See the formula given below.)  If E is 
         a vector of length n, it will be treated as a matrix of dimensions 
         n,1. 
    R    is the matrix containing one or more solutions to the systems of 
         linear equations described by E and C.  The dimensions of R are n,k. 
All arrays must be numeric matrixes.  E and C must satisfy the conformity 
rules for dimensions as described above or a run-time error will be reported. 
An error is also reported if C is singular as described in the MAT INV 
statement. 
Examples: 
    200 MAT W=SIM(E,C) 
    300 MAT Q=SIM(Y,D) 
In line 200, if C is a 3 by 3 matrix with the values 
    3     1     4 
    1     5     9 
    2     6     5 
And E is a 3 by 1 matrix with values 
    7 
    -4 
    -9 
Then E and C represent a single system of simultaneous equations of the form: 
    7=3X+1Y+4Z 
    -4=1X+5Y+9Z 
    -9=2X+6Y+5Z 
Thus line 200 provides a matrix result W with dimensions 3 by 1 and the values 
2, -3, and 1.  The statement: 
    MAT X=C*W 
will provide a result X with dimensions 3 by 1 and the values 7, -4, and -9, 
illustrating that W is indeed a solution to the system defined by E and C. 
00002
00004
00001
00003
MAT_ADDITION
Syntax: 
[line] MAT aname1=TRN(aname2) 
Parameters: 
aname1    is the target array name. 
aname2    is the argument array to be transposed. 
Description: 
The MAT TRANSPOSE statement interchanges the rows and columns of the argument 
matrix to the target matrix.  Both string arrays and numeric arrays may be 
transposed, but a string array may not be transposed to a numeric array or 
vice versa. 
Examples: 
    240 MAT A=TRN(B) 
    250 MAT A$=TRN(B$) 
In line 240, if the current dimensions of B are m,n then the current 
dimensions of A are set to n,m and A(i,j)=B(j,i).  In line 250 the 
transposition is effected with string matrixes. 
00002
00003
00001
Syntax: 
[line] MAT aname=ZER[(num-expr[,num-expr])] 
Parameter: 
aname    is a numeric array name that is to be set to zero. 
num-expr    represents an optional value (rounded to an integer) to set the 
current dimensions of the target array.  If none is specified, the existing 
current dimensions are retained. 
Description: 
The MAT ZER statement sets values to zero within a numeric array. 
Usage Notes: 
The rounded value of a dimension expression must not be less than the BASE 
value (0 or 1).  A compile-time error occurs if the specified dimension 
expressions will switch a vector to a matrix or a matrix to a vector. 
Examples: 
    710 MAT C=ZER 
    720 MAT D=ZER(I,J+1) 
Line 710 assigns the value of zero to all elements in array C.  Line 720 sets 
the dimensions of array D to the value represented by the variables I and J+1. 
00002
00004
00001
00003
Syntax: 
NEW [fid] 
Parameters: 
fid    is a valid CP-6 file identifier. 
Description: 
The NEW command effects a CLEAR and creates a new workspace name for the 
specified fid.  If no fid is specified, BASIC asks for a name by printing "New 
Program Name".  If no new name is desired, carriage return is pressed.  In 
this case, the default fid NONAME is issued. 
00002
00001
FOR_NEXT
Syntax: 
NRE[SAVE]  fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The NRESAVE command saves a file without line numbers, replacing any existing 
file of the same name. 
00002
00001
Syntax: 
NSA[VE]  fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The NSAVE command saves a command file; no line numbers are included with the 
stored file. 
00002
00001
Syntax: 
NSE[AL]  fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The NSEAL command seals and saves a non-line-numbered file. 
00002
00001
Description: 
NULL statements consisting of line numbers and followed by one or more blanks 
can be included in a program.  Such NULL statements are not executable.  If 
control is transferred to a NULL statement, operation continues at the next 
executable statement.  NULL statements can be used to visually separate 
logical sections of a source program, thereby making a program listing easier 
to read. 
Usage Notes: 
One or more blanks must be typed after the line number in a NULL statement. 
If these blanks are omitted, the only effect is the deletion of an existing 
statement with the same number. 
00001
  Type                  Format                              Example 
Unscaled integer      [s]digits[.]                        +5 
                                                          10. 
                                                          -12 
                                                          123456 
Scaled integer        [s]digits[.]E[s]digits              1E+12 
                                                          -2.E-5 
                                                          -1E-20 
                                                          634.E+132 
Unscaled real         [s][digits].fraction                +.000375 
                                                          9.98700001 
                                                          -.237512 
                                                          -.00000001 
Scaled real           [s] [digits].fractionE[s]digits     137.5E-3 
                                                          .8701E-1 
                                                          -2.375E+3 
                                                          312.6E-145 
  digits     specifies one or more digits with no embedded blanks. 
  s          specifies a negative or positive sign (- or +).  A negative sign 
  is always present for negative values or negative exponents.  The positive 
  sign for a value is optional and can be replaced by a leading blank or 
  omitted entirely.  The positive sign for positive exponents is optional and 
  may be omitted; it cannot be replaced by a leading blank. 
  fraction   specifies the digits following a decimal point that represent a 
  fractional value. 
  E          is a decimal scaling indicator. 
There are three forms of numeric replacement fields:  integer, decimal, and 
exponential.  In addition, numeric replacement fields can contain special 
control characters that alter the final formatting of the numeric value. 
Numeric replacement fields can only format numeric values; an error results if 
a string variable is assigned to a numeric field. 
When entering multiple numeric replacement fields on one line, each field must 
be separated by a blank as follows: 
    ##,### ##,###,### 
The following rules apply to the leading sign associated with a value for any 
of the three types of numeric replacement fields: 
1.  If the value is negative, then regardless of any sign in the field, a 
    minus sign is generated. 
2.  If the value is positive and the field contains a plus sign, then a plus 
    sign is generated. 
3.  If the value is positive and the field contains a minus sign, then a blank 
    space is generated. 
4.  If the value is positive and the field does not contain a sign, then no 
    leading blank space or sign is generated. 
The following examples illustrate how these rules are applied: 
    10 :##.##+##.##-##.## ##.## 
    20 PRINT USING 10,12.34,-12.34,+12.34,-12.34 
    30 PRINT USING 10,12.34,+12.34,-12.34,-1.234 
The result of line 20 is: 
    12.34-12.34 12.34 ***** 
The result of line 30 is: 
    12.34+12.34-12.34 -1.23 
See also:  INTEGER, DECIMAL, and EXPONENTIAL. 
Syntax: 
OFF 
Description: 
The OFF command closes all open files, releases queue entries, and then ends 
the batch operation or terminal session.  The OFF command is a synonym for the 
BYE command. 
00001
Syntax: 
[line] ON num-expr [GOTO|THEN|GOSUB] line[,line]... 
Parameters: 
num-expr    represents the value of the numeric expression rounded to the 
nearest integer.  The integer is used as an index position, counting from 1, 
to select a number from the list of line numbers.  If the position is within 
the range of the count of line numbers, control is transferred to the indexed 
line number.  If the index position is not in the specified range, an error is 
reported. 
Description: 
The ON statement transfers control to any of several program points or 
subroutines based on the value of a numeric expression. 
Usage Notes: 
The forms GO TO and GO SUB are also permitted.  The forms GOTO and THEN 
function identically.  See the GOTO and GOSUB statements. 
Examples: 
    100 ON A(1) GOSUB 400,500,400,500,600 
    200 ON C-5 GOTO 300,320,250 
When line 100 is executed, if A(1) has a value from 1 to 5, control transfers 
to the indicated line.  For example, if A(1)=5, control will transfer to line 
600.  Note that line numbers may be repeated.  Since the branch is a GOSUB, 
control returns to the line following 100 when RETURN is executed.  When line 
200 is executed, if C has a value from 6 to 8, control transfers to line 300, 
320, or 250. 
Since an error results if the numeric expression is not within the specified 
range, the user may want to utilize error control via the WHEN statement. 
00002
00004
00001
00003
Syntax: 
[line-no] OPEN str-expr TO expression, mode 
Parameters: 
str-expr    is a valid CP-6 fid.  Devices may not be specified for fid. 
mode    is defined as one of the following: 
    INPUT[,UPDATE][,SHARED] [,key type] 
    GET[,UPDATE][,SHARED][,precision][,key type] 
    PRINT[,OVER][,key type] 
    PUT[,OVER][,precision][,key type] 
precision    is SINGLE or DOUBLE. 
key type    is NKEY (numeric key), SKEY (string key), CONSEC (consecutive), or 
INDEXED (indexed).  NKEY is the default if not specified.  If INDEXED is 
specified, the key type format is: 
    INDEXED (buffer),primary-key [,secondary-key [[NO]DUPLICATES]]... 
    where 
    buffer    is a valid numeric or string variable name. 
    primary key    specifies a scalar element of the corresponding MAP 
    statement.  Elements of arrays may not be used. 
    secondary key    specifies a different scalar element of the corresponding 
    MAP statement.  Elements of arrays may not be used. 
    NODUPLICATES    specifies that two records with the same secondary key 
    values cannot be written to a file.  This is the default. 
    DUPLICATES    specifies that two records with the same secondary key 
    values can be written to a file. 
Description: 
The OPEN statement is used to associate an external file with an I/O stream 
and specifies the mode of I/O that is going to take place. 
Usage Notes: 
The string expression must represent a valid form for file identification on 
the CP-6 system.  It may be a quoted string, string variable, or concatenation 
of either or both. 
The numeric expression after TO, rounded if required, must represent an 
integer in the range 1 to 12.  The value is the I/O stream number to be 
associated with the named file. 
The modes have the following meaning: 
    INPUT - Open an existing file, which is to be read as an ASCII data file. 
    The user must have read access to the file. 
    GET - Open an existing file which is to be read as a binary file.  The 
    file will normally be numerically keyed.  User must have read access to 
    the file. 
    SHARED - Allows user to control file access. 
    UPDATE - Applied to INPUT or GET.  Open an existing file in the indicated 
    mode but allow update operations; PRINT for INPUT files, PUT for GET 
    files.  The existing file must be keyed or consecutive and the user must 
    have both read and write access. 
    PRINT - Open a file for ASCII output.  No old file of the same name must 
    exist unless the OVER option is included.  PRINT, OVER will delete any old 
    file of the same name prior to opening a new one.  The file will be keyed 
    or consecutive. 
    PUT - Open a file for binary output.  No old file of the same name must 
    exist unless the OVER option is included.  The file will be keyed or 
    consecutive. 
    SINGLE or DOUBLE - Sets precision for binary file access.  Used when file 
    has different data precision than running program. 
    NKEY, SKEY, CONSEC, or INDEXED - Opens the file as having numeric keys, 
    string keys, consecutive, or indexed organization. 
Execution of the OPEN statement associates the indicated I/O stream with a 
named file, establishes which I/O operations are valid for the stream, and 
sets access at the beginning of the file.  If the mode is PRINT or PUT, a new 
file is created with no current records. 
Once an I/O stream is opened to a particular file, the open status persists 
until a CLOSE or CLEAR statement is executed for that stream or until the user 
leaves BASIC.  File access thus persists through LOAD and CHAIN operations. 
The execution of a CHAIN, END, or STOP statement or issuance of the RUN, FAST, 
FASTER, or FASTEST compile and execute commands will not have any effect on 
the open status of any stream. 
When an OPEN statement is executed to a stream which is already open: 
o   If the fid and function are identical in both the OPEN statement and the 
    DCB currently associated with the stream, a warning message is issued, the 
    DCB is closed, and the OPEN statement is executed. 
o   Otherwise, an error message is issued, and an error condition is raised. 
Examples: 
    250 OPEN "MYASCII" TO 1,PRINT,OVER 
    300 OPEN "SAVEBINARY" TO 2,PUT,OVER, NKEY 
    400 OPEN C$ TO 3,PRINT, CONSEC 
    500 OPEN D$ TO 5,INPUT,UPDATE,SHARED, SKEY 
    600 OPEN E$ TO 11,INPUT 
    700 OPEN E$ TO 7,INPUT, NKEY 
    800 OPEN "STATDATA.STATLIB" TO 8,GET, SHARED 
Files "MYASCII" and "SAVEBINARY" are opened as newly created output files in 
the user's account.  The file named by string C$ is opened as a newly created 
file unless an old file exists with the same name.  The files referenced above 
are all opened in exclusive mode.  While a user has write access to a file, 
his access is exclusive unless it is shared update mode.  The file named by D$ 
is opened for shared update.  This file may not be open in unshared mode 
concurrently.  The file named by E$ is opened for input on both streams 11 and 
7.  A file may be concurrently open to several users or streams for input as 
long as it is not open for update.  STATDATA in account STATLIB is open for 
binary input, shared.  It may be opened even if it is concurrently open for 
update.  Binary file operations may not be used for indexed file operations. 
00002
00004
00001
00003
The five arithmetic operators used in expressions are: 
                                                           Precedence 
    Operator           Symbol                                Level 
    --------           ------                              ---------- 
    Exponentiation     ^ or **       (up arrow or double       1 
                                     asterisk) 
    Multiplication     *             (asterisk)                2 
    Division           /             (slash)                   2 
    Addition           +             (plus)                    3 
    Subtraction        -             (minus)                   3 
The exponentiation, multiplication, and division operators require both left 
and right arguments.  The plus and minus operators can occur at the left of an 
expression, but successions of plus and minus signs are not permitted.  Note 
that forms such as A*-B do not violate these rules.  In this case, the right 
argument of the multiplication operator is -B.  However, forms such as A+-B or 
A--B are invalid. 
Syntax: 
[line] OPTION [BASE] 1 
[line] OPTION [BASE] 0 
[line] OPTION [PRECISION] DOUBLE 
[line] OPTION [PRECISION] SINGLE 
[line] OPTION WARN 
[line] OPTION NOWARN 
[line] OPTION [UNDERFLOW] {ERROR|ZERO} 
[line] OPTION OVERFLOW {ERROR|MAX} 
Parameters: 
BASE    only affects array data.  If BASE is changed, all current arrays are 
vacated.  The default is 1. 
PRECISION    affects BASIC binary file input/output.  Binary files created or 
updated by BASIC carry information concerning precision with each physical 
record.  Input from binary files created by BASIC is modified if the filed 
data is not at the same precision, and program operation is double; fractional 
values are extended by zeros.  If filed data is double precision and program 
operation is single, values are truncated with rounding to single precision. 
The default is SINGLE. 
WARN    allows warnings to be printed.  This is the default. 
NOWARN    suppresses the printing of warning error messages. 
UNDERFLOW    allows the user a choice of what to do in case of underflow.  If 
the user specifies ERROR, then an error message will be reported in case of 
underflow.  If the user specifies ZERO, then in case of underflow, the result 
will be zero.  This applies to both numeric arithmatic, and decimal arithmatic 
packages. 
OVERFLOW    allows the user a choice of what to do in case of overflow.  If 
the user specifies ERROR, then an error message will be reported in case of 
overflow.  If the user specifies MAX, then in case of overflow, the result 
will be the maximum value.  This applies to both numeric arithmatic, and 
decimal arithmatic packages. 
Description: 
The OPTION statement is used to establish any of several optional modes which 
effect the compilation and execution of BASIC programs.  OPTION statements 
have a profound effect on the total working storage environment and behavior 
of programs, and must be used with great caution. 
Usage Notes: 
OPTION statements, if present, must precede all other statements in a BASIC 
program.  If no OPTION statements are included in a program, the default 
values are used. 
During program compilation, if OPTION PRECISION changes from its prior 
setting, all current data values are modified.  A change from SINGLE to DOUBLE 
reallocates storage and extends the fraction in the internal data form with 
zeros.  An OUT OF SPACE error may occur.  A change from DOUBLE to SINGLE 
reallocates storage and truncates double precision values to single precision 
with rounding.  If PRECISION changes because of a direct OPTION statement, any 
current object program is voided and subsequent option requires recompilation. 
00002
00001
00003
Syntax: 
[line] PAGE [#num-expr] 
Parameters: 
num-expr    represents the stream number. 
Description: 
The PAGE statement causes the paper to be advanced to the next page for 
printed output. 
Usage Notes: 
When a PAGE statement is encountered, BASIC generates a system call to eject 
the current page on the output device and advance to the next page. 
The number of lines per page (page depth) cannot be altered by BASIC, but can 
be changed through the PLATEN command at the execution (!) level. 
00002
00001
00003
The following table lists abbreviations of parameters that appear frequently 
in the syntax of BASIC statements.  are also listed in the Glossary. 
  Abbreviation        Description 
aname               Name of an array. 
adescr              Array descriptor of the form: 
                    aname[(num-expr[,num-expr])] 
const               Numeric floating point constant. 
int                 Integer value. 
key                 Line number of a file record. 
num-expr            Numeric expression. 
num-var             Numeric variable. 
repl-field          Numeric or alphanumeric replacement field. 
simp-var            A simple variable, either a string or numeric scalar. 
str-expr            String expression. 
str-var             String variable. 
stream              A numeric expression between 0 and 12 inclusive that 
                    is rounded to an integer. 
var or              Simple or subscripted variable. 
variablename 
Syntax: 
[line] PRINT 
       or 
[line] PRINT [{,|;}...{,|;}]item [{,|;}...{,|;} item]...[{,|;}...{,|;}] 
Parameter: 
item    is any numeric or string expression, or a TAB or SPC function call. 
Description: 
The PRINT statement generates labeled output, unlabeled output, and output in 
tabular form. 
Usage Notes: 
The series of items and punctuation marks following the PRINT are called a 
print list.  If a print list is absent, a blank line is generated, unless a 
prior PRINT statement has output pending (end in a ";" or a ","), in which 
case a blank PRINT statement causes the current line to be output. 
Each print line is divided into print zones whose length is the current DIGITS 
setting plus 8 spaces.  The final print does not require trailing blanks.  The 
DIGITS value determines the precision and spacing of the printed numeric 
values. 
The presence of a semicolon separator generates no output characters.  The 
presence of a comma separator generates enough spaces to fill out the current 
print zone, unless the current zone is the last zone on the output line, in 
which case the line is output and a new print line is initiated.  If either a 
semicolon or a comma appears at the end of the print list, it is a signal that 
the line is not to be output immediately, but is to be held for pending PRINT 
statements.  If the print list does not end in a semicolon or comma, the 
current line is output immediately. 
The execution of a PRINT statement generates a string of characters for 
transmission to the output device.  The string of characters is determined by 
the successive evaluation of each item and punctuation mark in the print list, 
the print position of the carriage, the margin setting, and the current digits 
value. 
Whenever the generation of characters for an item in the print list will 
exceed the margin width for the current line, the current line is completed 
and a new print line initiated. 
Numeric expressions generate output strings according to the following rules 
(d = the current DIGITS setting): 
1.  A leading blank is the first character to be printed, except if the number 
    is negative, in which case the first character is a minus sign. 
2.  If the value is an integer with d or fewer significant digits, the output 
    string is an integer with no decimal point. 
3.  Non-integers within the range from .1-.5*10**(-d-1) to 10**d-.5 are 
    represented in integer decimal point form, with d significant digits 
    (although trailing zeros in the fraction are omitted).  The integer zero 
    before the decimal point is omitted for numbers in this range that are 
    less than 1. 
4.  Numbers lower in magnitude than the range specified above, but which can 
    be exactly represented with no more than d digits following a period, are 
    also represented in the integer decimal point fraction form. 
5.  All other numbers are represented as scaled values with associated decimal 
    exponents of the form: 
        digit.fractionE[-|+]exponent 
    The fraction is composed of d-1 digits, and trailing zeros are included. 
    The letter E signifies exponent scaling, where the exponent (whether 
    negative or positive) is the power of ten that must be applied to the 
    representation to obtain the numeric value. 
6.  E is omitted from the printed field for exponents greater than 99 or less 
    than -99. 
7.  A trailing blank is generated for all numeric representations. 
String expressions are evaluated to generate a string of characters. 
The TAB function is evaluated and the argument is rounded to an integer.  The 
argument cannot be less than 1.  If it is greater than the margin setting, the 
rounded argument is reduced by an integer multiple of the margin width so that 
the result is within the range of the print line column numbers.  If the 
column specified by the rounded argument is to the right of the current line 
position, enough blanks are generated to set the line position to the 
specified value.  If the rounded argument specifies a value to the left of the 
current line position, the current line is output, and a new line is 
initiated.  Blanks are generated to set the line position to the specified 
value. 
The SPC function call generates the number of spaces specified by the argument 
(rounded to an integer) of the function. 
Examples: 
    100 PRINT X 
    150 PRINT I,J,K 
    200 PRINT TAB(30);I;J;K 
    250 PRINT "NAME",TAB(40);"SALARY";TAB(60);"HIRE DATE" 
    300 PRINT A$;B$; 
    350 PRINT I;TAB(Y); 
Line 100 prints the value of X.  Line 150 prints the values of I, J, and K in 
successive print zones.  Line 200 prints I, J, and K in a closely-packed form 
starting at column 30.  Since numeric representations have trailing blanks, 
the values will be separated by one or two blanks.  Line 250 uses TAB to space 
items on a title line for a report.  Line 300 results in a line with the 
characters of strings A$ and B$.  This series of characters (due to the 
trailing semicolon) is not written out unless the combination of the two 
strings exceeds the margin width.  Margin overflow causes part or all of the 
contents of the current print line to be printed.  Line 350 implants the value 
of I into the current line pending.  If the tab setting is to the left of the 
current position, the line is written out and a new line is started. 
00002
00001
00003
Syntax: 
[line] PRINT# stream[;key][,CRPT=str-expr][,[{,|;}...[item]]...] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of the key 
which points to the record at which the write is to begin.  When using indexed 
files, the key format is: 
    [;MAP num-expr] 
    where 
    num-expr    is an integer value which specifies a MAP statement as it is 
    encountered by increasing line number.  For instance, the value 1 
    represents the default or first MAP statement for the specified name, 2 
    represents the following MAP statement of the same name, and so on. 
    For example: 
    400 PRINT# 3;MAP 3 
    Line 400 generates a record on stream number 3 with a size as specified by 
    the third encountered MAP statement of the specified name. 
CRPT=str-expr    specifies the encryption seed for data files.  The seed can 
be entered as a string of characters of length less than or equal to 4.  If a 
seed has a length of 1 to 3, it will be right justified and ".000" is placed 
in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write.  The 
CRPT parameter is not specified when using indexed files. 
item    is any numeric or string expression, or a TAB or SPC function call. 
The item parameter is not specified when using indexed files. 
Description: 
The PRINT# statement writes records in ASCII to a file in the same format that 
a PRINT statement writes to a terminal. 
Usage Notes: 
The punctuation separating the individual items in the print list may be 
either a comma or a semicolon depending on the desired format.  (See the 
PRINT_STATEMENT for formatting effects of the comma and semicolon.) 
The execution of a PRINT# statement generates a string of characters for 
transmission to an external file in the same way that the PRINT statement 
generates output lines to a printing device.  A single PRINT# statement will 
frequently create more than one record, just as a PRINT statement may create 
more than a single line.  Key values are incremented by 1 for each successive 
record created by a single PRINT# statement.  If a file has string keys, 
however, each record must have a unique key. 
A trailing punctuation mark on the PRINT# statement leaves characters buffered 
for output, allowing a later PRINT# to add characters to the current record on 
the indicated stream.  As a result, the records generated by a PRINT# command 
with a trailing comma or semicolon will not actually be written into the file 
until one of four things takes place: 
1.  A PRINT# statement using the same stream is encountered which has no 
    trailing comma, which causes the output from both PRINT# statements to be 
    written to the file. 
2.  The stream is closed via the CLOSE command. 
3.  The user exits BASIC, thereby causing a close of all streams. 
4.  The length of the print buffer exceeds the MARGIN setting. 
The current DIGITS setting controls the conversion of numeric values to text 
representations.  The MARGIN control may be set separately for individual 
output streams.  The TAB and SPC functions perform the same as for the PRINT 
statement. 
If the stream number evaluates to zero, the statement is handled as a 
conventional print statement, in which case a key expression, if present, is 
ignored. 
Examples: 
    100 PRINT# 1;Q1,X 
    150 PRINT# M,I,J,K 
    200 PRINT# Q,TAB(30);I;J;K 
    300 PRINT# 2,A$;B$; 
    350 PRINT# 2,C$ 
Line 100 generates a record on stream 1 with a key value represented by the 
variable Q1, and the text representation of the numeric value X.  Line 150 
generates a record on the stream represented by the variable M, increments the 
current key value by 1.  The values of I,J, and K are written into successive 
print zones.  Line 200 generates a record on stream Q with the values of I,J, 
and K closely packed, following 30 blank characters (inserted with the TAB 
option).  Line 300 buffers the contents of A$ and B$ for output on stream 2, 
but will not write out a record to the actual file (designated by the OPEN 
statement described above) until statement 350 is encountered.  (Exception: 
if the combined width of A$ and B$ exceeds the margin width of stream 2, line 
300 will write out a record.)  Line 350 appends the value of C$ to the record 
accessed in line 300; the lack of a trailing punctuation mark causes the 
buffer to be written to the file. 
PRINT# and its related statements (MAT PRINT#, PRINT# USING, etc.) may be used 
to update existing files, replacing existing records or inserting new records. 
However, this feature must be handled with caution, because a single PRINT# 
statement can generate more than one record.  If this procedure is used, the 
user is advised to create the original file with a large PRINT# key increment 
such as 100 to prevent inadvertently replacing records during subsequent 
record insertion. 
00002
00004
00001
00003
Syntax: 
[line] PRINT# stream[;key][,CRPT=str-expr],USING & 
{line|str-expr},var[,var]...[;] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of the key 
which points to the record at which the write is to begin. 
CRPT=str-expr    specifies the encryption seed for data files.  The seed can 
be entered as a string of characters of length less than or equal to 4.  If a 
seed has a length of 1 to 3, it will be right justified and ".000" is placed 
in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write. 
str-expr    is a string expression representing the format of the PRINT# USING 
statement. 
var    is a variable name that is to be printed out. 
Description: 
The PRINT# USING statement generates formatted character records in ASCII 
files.  PRINT# USING bears the same relationship to the PRINT USING statement 
that PRINT# does to the PRINT statement.  The PRINT# USING statement may not 
be used for indexed file operations. 
00002
00001
These functions are:  LIN, SPC and TAB. 
  Function      Meaning 
  LIN (expr) 
                The LIN function is used in a PRINT statement to advance the 
                output device by the number of lines designated by expr, which 
                in turn causes the generation of blank lines.  The LIN 
                function can be specified more than once in a single PRINT 
                statement. 
  SPC(expr) 
                The SPC function is used in a PRINT statement to advance the 
                output device by the number of spaces specified by expr 
                (rounded to an integer) from the current print column.  If the 
                function specifies a print line longer than the current MARGIN 
                setting, the current line is filled with blanks, and remaining 
                blanks are inserted on the following line before the remaining 
                items of the line are printed. 
  TAB(expr) 
                The TAB function is used in a PRINT statement to advance the 
                print device to the column designated by expr (rounded to an 
                integer).  The TAB function is discussed in detail within the 
                description of the PRINT statement. 
00001
00002
00003
Syntax: 
[line] PRINT USING line[,var]...[;] 
[line] PRINT USING str-expr[,var]...[;] 
Parameters: 
line    specifies the number of a line in the program that contains an IMAGE 
statement of the form: 
    line :    format-string 
str-expr    must be a valid format-string. 
Description: 
The PRINT USING statement creates formatted output controlled by images or 
templates. 
Usage Notes: 
A format-string is a string of characters that contains one or more 
replacement fields, that is, areas within the string that serve as a template 
for the formatting of output. 
There are two types of replacement fields:  alphanumeric and numeric. 
Alphanumeric replacement fields always start with an apostrophe and are used 
to format the values of string variables.  Numeric replacement fields always 
contain one or more pound signs (#), and are used to format the values of 
numeric variables. 
When a PRINT USING statement is encountered, the format-string (either within 
an image statement or in a str-expr) is scanned.  Characters from the 
format-string are moved into the current print line until a replacement field 
is reached.  The first element of the variable list is inserted into the 
replacement field, which may alter its form through rounding and/or 
truncation.  This process continues until all the elements in the variable 
list have been placed into the current print line.  When the scanning process 
reaches the end of the format-string, the current print line is written out. 
If the variable list contains more elements than the number of replacement 
fields, the format-string is reused until all elements are assigned.  In this 
case, each time the end of the format-string is reached, the line is written 
out. 
If the PRINT USING statement ends with a semicolon, the last current print 
line generated by the PRINT USING statement will be held for output. 
The PRINT USING statement does not override the margin setting.  If a current 
print line reaches the margin value in the middle of output formatting, the 
line is printed and a new line is begun.  If a current print line exists when 
a PRINT USING is reached, the output for the PRINT USING is appended to the 
partially completed line. 
00002
00001
00003
Syntax: 
PRO[CEED] 
Description: 
The PROCEED command resumes execution of BASIC after a break condition only 
for compiled programs.  It does not handle directly executed statements.  See 
the PROCEED_STATEMENT. 
00001
Syntax: 
[line] PROCEED 
Description: 
The PROCEED statement is used to resume operation after a program has been 
suspended by a break or error condition, or diverted by error control.  (See 
the GO command.) 
Usage Notes: 
If used as a direct statement issued after a BREAK, PROCEED transfers to the 
next executable program statement following the interrupt.  As a direct 
statement issued after an error during run-time, PROCEED normally transfers to 
the first executable statement following that in which the error occurred.  In 
some instances (such as a RETURN statement with no return point in the 
GOSUB-RETURN stack) execution of the next statement is illogical, in which 
case an error message is produced.  In general, a PROCEED should not be issued 
after an error halt unless the user has insured that continued program 
execution makes sense under the circumstances. 
A PROCEED issued after a program has been edited while suspended results in an 
error message. 
As a program statement, PROCEED may only be used to resume operation after a 
WHEN BREAK statement has controlled a BREAK keyin from the user's console.  In 
this case, PROCEED behaves as if the program has been suspended at the point 
of the most recent break. 
00001
00002
Syntax: 
[line] PROMPT  str-expr 
Parameters: 
str-expr    is any string less than 32 characters long. 
Description: 
The PROMPT statement sets the run-time prompt character during execution of 
the program.  The characters must be surrounded by a pair of quotation marks 
("). 
Examples: 
    100 PROMPT "?!?!?" 
Line 100 sets the prompt to "?!?!?". 
00002
00003
00001
Syntax: 
[line] PUT: stream[;key][,CRPT=str-expr],num-var[,num-var]... 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of a key 
which points to the record to which it is to be initially written. 
CRPT=str-expr    specifies the encryption seed for binary data files.  The 
seed can be entered as a string of characters of length less than or equal to 
4.  If a seed has a length of 1 to 3, it will be right justified and ".000" is 
placed in front of it.  The default is zero or no seed.  If the seed length is 
greater than 4, a run time error is issued.  Note that the seed in every 
command is temporary; it is valid only for that particular read or write. 
num-var    is a variable representing the value that is to be written into the 
file. 
Description: 
The PUT: statement writes numeric data to a binary file. 
Usage Notes: 
If a key expression is included any values currently buffered for output on 
the indicated stream become output, possibly creating a short record; a new 
record is started with the specified key.  If no key expression is indicated 
and a partially filled output record is pending, values are added to that 
record.  As records are filled, they are written out, and new records are 
written with incremented key values.  Output records are formed by evaluating 
the expressions in the PUT: statement, all of which must be numeric. 
Synchronization between individual PUT: statements and data records does not 
occur unless the statement includes a key expression or contains exactly the 
number of values contained in a full record. 
If an unkeyed PUT: is the first output statement on a new file, the key is set 
to 1, however, files with string keys must specify a key for each PUT:.  If an 
unkeyed PUT: is the first I/O statement on an old file opened in UPDATE mode, 
the key is that of the first record in the file, which will be replaced. 
Since successive PUT: records have key values incremented by 1, unless keys 
are explicitly specified, the use of unkeyed PUT: statements in UPDATE mode 
requires knowledge of the prior file structure. 
Examples: 
    200 PUT: 1;R3,SIN(X),COS(X),X 
    300 PUT: J,Y1,FNY(Y1),5+Y2 
Line 200 starts a new record on stream 1 with the key indicated by R3.  Any 
partially filled record for stream 1 is written out first.  The values of 
SIN(X), COS(X) and X are buffered for output.  Line 300 continues on the 
stream indicated by J.  The values of the three expressions are buffered for 
output.  A record is written out if any of these values fills the current 
output buffer for the stream. 
00002
00004
00001
00003
Syntax: 
Q 
Description: 
The Q command allows the user to exit BASIC.  Control is transferred to the 
operating system. 
00001
Syntax: 
[line] RANDOMIZE [num-expr] 
Parameters: 
num-expr    is a numeric word value which is used in the random number 
generator algorithm to set a point in the pseudo-random number sequence.  If 
num-expr is not specified, RANDOMIZE sets a point in the pseudo-random number 
sequence that is determined by the time and date of execution, thereby making 
successive runs non-repetitive. 
Description: 
The RANDOMIZE statement changes the random seed value utilized by the RND 
function to generate pseudo-random numbers.  The RANDOMIZE statement must 
appear before the RND and RNS functions. 
If RANDOMIZE is to be effective within a program, it must be executed after 
the program is initialized; in other words, it must be a numbered, executed 
statement within the program, or be issued as a direct statement after a BREAK 
that is followed by a PROCEED or a direct GOTO. 
00002
00001
Syntax: 
[line] READ var[,var]... 
Parameters: 
var    specifies a single numeric value or text string.  The variable may be a 
scalar (unsubscripted variable) or an element of an array.  Subscripted 
variables are permitted. 
Description: 
The READ statement accesses the sequence of data representations associated 
with DATA statements. 
Usage Notes: 
When a READ statement is reached during program execution, the set of data 
representations in the program's DATA statement is accessed.  The number of 
data elements is checked by BASIC to determine if enough are available to 
satisfy the variable list.  The elements are also scanned to determine if they 
are appropriate representations for assignment to the corresponding variables 
of the READ statement.  If an error condition is recognized in matching data 
values to READ variables, no assignments are made, an error message is issued, 
and program execution stops.  The pointer for accessing data is set as though 
no READ has been attempted.  If no errors are indicated, the data values are 
assigned to the variables in left to right order.  The pointer for accessing 
data is advanced appropriately. 
The evaluation of a subscript expression for a variable takes place 
immediately before the assignment of a datum to that variable.  Thus the 
statement READ I,A(I) has a different meaning and effect than the statement 
READ A(I),I. 
If a subscripted expression evaluates to a number outside the dimensional 
range for an array, an error occurs, and assignment to variables to the left 
of the offending variable will be made.  In this case, the data pointer is set 
to the offending element. 
If the program user includes error control, error messages are suppressed and 
program execution proceeds at the line number specified by the WHEN statement. 
Note that READ, unlike INPUT, does not require an exact association between 
the lengths of the data lists and the lengths of the variable lists. 
Examples: 
    READ A$,B(1,1) 
    120 READ W,C(W-J),D$(3) 
The first example illustrates READ as a direct statement; for this statement 
to be effective, a program must be present in working storage, and must be in 
suspended operation as the result of a real or simulated break condition.  The 
READ will access data using the current position of the data pointer.  Line 
120 accesses three data representations.  If there are not three values left 
in the data sequence, or the types are not correct, an error is noted and no 
variables are assigned.  If the datum for W is such that the subscript for C 
is out of range, W is assigned, but no assignment is made to C or D$ and an 
error is reported. 
00002
00004
00001
00003
Syntax: 
REE[NTER] 
Description: 
The REENTER command executes a compiled program using the previous execution 
mode.  The default execution mode is RUN.  If the program has been edited 
since the last execution, or has not been compiled or executed, BASIC prints 
an error message stating that the RUN command must be used. 
00001
Syntax: 
[line] {REM|!} [commentary] 
Parameters: 
commentary    consists of any characters to the end of the line. 
Description: 
The REM statement is used to insert program documentation. 
Usage Notes: 
REM is not an executable statement.  If control is transferred to a REM 
statement, operation continues at the next executable statement.  The 
exclamation point may also be used to insert commentary at the end of a 
statement.  The exclamation point cannot be used in batch without a line 
number. 
Examples: 
    100 REM    THIS IS THE BEGINNING OF THE PROGRAM 
    200 REM    THIS IS THE MIDDLE OF THE PROGRAM. 
    300 GOTO   5000 ! THIS TRANSFERS CONTROL. 
    400 REM    THIS IS THE END 
    401 END 
00002
00004
00001
00003
RENUMBER
Syntax: 
RENA[ME] [fid] 
Parameters: 
fid    is a valid CP-6 file identifier. 
Description: 
The RENAME command changes the name of the current workspace to a valid file 
name.  If fid is not specified, the default name assigned is NONAME.  If fid 
is specified, it becomes the default for the RESAVE command. 
00002
00001
Syntax: 
REN[UMBER] [n][,m][,r-[s]] 
Parameters: 
n    is the starting line number of the renumbered program.  The default is 
10. 
m    is the increment of each successive line number.  The default is 10. 
 r-s    specifies the range to be renumbered; specifying r without s (or r-) 
means renumber from r to the end of the program; specifying r instead of s (or 
r-r) means renumber only line r.  The default is renumber the entire program. 
Description: 
The RENUMBER command changes existing line numbers (including line number 
references inside control statements), creating a program with a specified 
first line number and a specified fixed increment between line numbers. 
Examples: 
    REN 
    RENUMBER 1000,5 
    RENUMBER 100,10 
    RENUMBER 5000,10,500-600 
The first command is all defaults 10 by 10 for all lines.  The second command 
renumbers the lines so that the first line is numbered 1000, and each 
successive line is increased by increments of 5 (e.g., 1000, 1005, 1010, 1020, 
etc.).  The third command renumbers the lines so that the first line is 
numbered 100, increased by increments of 10.  The fourth command renumbers the 
lines 500 through 600, starting at 5000 and increasing by increments of 10. 
00002
00003
00001
Syntax: 
RES[AVE] [fid] 
SAV[E] OVER [fid] 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The RESAVE or SAVE OVER command copies a BASIC source program to file storage 
either as a newly-named file (like the SAVE command) or as a replacement to a 
previous version.  If the workspace is not empty and no file name has been 
specified, the RESAVE or SAVE command uses NONAME as the default fid. 
00002
00001
A BASIC reserved word is an identifier with a specific meaning which is part 
of the definition of BASIC.  Reserved words are used within the language to 
identify statements, components of statements, and function names.  Therefore, 
these names may not be used as variable names by the programmer.  A complete 
list of all BASIC reserved words is given in the following table. 
 ABS                       DUPLICATES                OPTION 
 ACCEPT                    ELSE                      OR 
 ACOS                      ENDDO                     OTHER 
 ACS                       ENDIF                     OVER 
 ALIGNED                   ENQE                      OVERFLOW 
 ALL                       ENQS                      PAGE 
 AND                       EOF                       PLACE$ 
 ANS                       EQ                        POS 
 ARRAYS                    ERASE                     PPOS 
 ASC                       ERL                       PRECISION 
 ASIN                      ERN                       PRINT 
 ASN                       ERROR                     PRIVACY 
 ATN                       EXP                       PROCEED 
 B                         FIND                      PROD$ 
 BASE                      FNEND                     PROMPT 
 BCL                       FOR                       PUT 
 BIT                       FROM                      QUO$ 
 BREAK                     GET                       RANDOMIZE 
 BUFFERS                   GOSUB                     READ 
 CALC                      GOTO                      READY 
 CHAIN                     HPOS                      REDUCEQ 
 CHANGE                    HSN                       REM 
 CHECK                     HTN                       REP$ 
 CHR$                      IBLET$                    RESTORE 
 CLEAR                     IDA                       RETAIN 
 CLK$                      IDN                       RETURN 
 CLOSE                     IF                        RIGHT$ 
 CMP                       INPUT                     RND 
 CMPB                      INSTR                     RNS 
 COMP                      INT                       ROLL 
 CON                       INV                       RPTSTATS 
 CONNECT                   KEY                       SCALARS 
 CONSEC                    KEY$                      SCN 
 COS                       KYEN                      SEC 
 COSH                      KYES                      SEG$ 
 COT                       KYF                       SEND$ 
 CPU                       KYF$                      SGN 
 CRPT                      KYL                       SHARED 
 CSC                       LEFT$                     SIM 
 DAT$                      LEN                       SINGLE 
 DATA                      LET                       SKEY 
 DATE$                     LGT                       SPC 
 DB                        LIBERR                    SST$ 
 DBDATANAME$               LIN                       STATSOFF 
 DBEMPTY                   LINK                      STATSON 
 DBERR                     LINPUT                    STOP 
 DBKEYNAME$                LOC$                      STORE 
 DBMEMBER                  LOG                       STR$ 
 DBMEMBERINFO$             LOG2                      SUB 
 DBNAMES$                  LTW                       SUM$ 
 DBOWNER                   MAR                       TAN 
 DBOWNERINFO$              MARGIN                    TANH 
 DBPRIVACY$                MAT                       THEN 
 DBRECORD$                 MAX                       TIM 
 DBSET$                    MID$                      TIME$ 
 DBSTATUS                  MIN                       TO 
 DBTENANT                  MNE                       TRACE 
 DDIGITS                   MOD                       TRACEOFF 
 DEF                       MODIFY                    TRACEON 
 DEG                       MONERR                    TRN 
 DELIMIT                   NEXT                      UNALIGNED 
 DEQ                       NKEY                      UNDERFLOW 
 DET                       NODUPLICATES              UNLESS 
 DIF$                      NOTRACE                   UNTIL 
 DIG                       NOWARN                    UPC$ 
 DIGITS                    NUL                       UPDATE 
 DIM                       NUM                       UPRC$ 
 DIRECTREFERENCE           NUM$                      USING 
 DISCONNECT                NUMERIC                   VPS 
 DO                        OFF                       WHEN 
 DOUBLE                    ON                        WHILE 
 DUP$                      OPEN                      ZERO 
Syntax: 
[line] RESTORE [line] 
Description: 
The RESTORE statement modifies the pointer that determines which DATA 
statement will be accessed by the next READ in the program. 
Usage Notes: 
When a RESTORE statement is reached in program execution, the data pointer for 
READ is set to the first data representation of the indicated DATA statement. 
An error results at compile time if the designated line number is not a DATA 
statement. 
If the RESTORE statement does not include a target line number, the next DATA 
statement accessed will be the one with the lowest number in the program. 
Examples: 
    RESTORE 200 
    170 RESTORE 
    180 RESTORE 500 
The first example illustrates RESTORE as a direct statement; for this 
statement to be effective, a program must be present in working storage and in 
suspended operation.  Any subsequent READ will start from line 200.  Line 170 
restores the pointer to the first DATA statement in the program.  Line 180 
sets the pointer to the first datum in line 500. 
00001
00003
00002
Syntax: 
[line] RESTORE{#|:} stream[,key|,EOF] 
Parameters: 
stream    is a numeric expression (rounded to an integer) that represents a 
valid stream number. 
key    is a numeric or string expression that represents the value of the key 
which points to the record to which the pointer is to be redirected.  If 
omitted, the key of the first record in the file is assumed. 
EOF    to position the file to the end of the file (past the last record). 
Description: 
The RESTORE statement resets the file pointer for an indicated I/O stream to a 
designated record. 
Usage Notes: 
If the stream is open to an ASCII data file, a pound sign (#) follows the 
RESTORE.  If the stream is open to a binary data file, a colon (:) follows the 
RESTORE. 
00002
00001
00003
RESTORE#
GOSUB_RETURN
Syntax: 
'R[R...] 
Description: 
These fields are represented by an apostrophe followed by one or more R 
characters. 
The apostrophe and the R's are replaced by characters from the string 
variable.  If the string is shorter than the field, it is padded with blanks 
on the left.  If the variable is longer than the field, characters to the 
right are truncated. 
Examples: 
    100 LET C$="WALRUS" 
    200 LET D$="CARPENTER" 
    300 PRINT USING "'RRRRRR", C$, D$ 
Line 300 prints the message: 
     WALRUS 
    CARPENT 
00001
00002
Syntax: 
RR    n[,m] 
Parameters: 
n    is an existing line in a BASIC program. 
m    is the column number to position to. 
Description: 
The RR command rereads an existing line or consecutive lines in a BASIC 
program.  The line will be displayed with the cursor positioned at the end of 
the line or to a special column within the line.  The user may then edit the 
line. 
Press <CR> to edit the next line in the program.  If the line just edited is 
the final source line, an error is caused by pressing <CR>. 
00002
00001
Syntax: 
RUN[H] [time] 
Parameter: 
time    is an integer that specifies the maximum number of seconds of compute 
time (not elapsed time) that the program may execute. 
If the form RUNH is used, a "header" line is generated that displays the time, 
date, and program name. 
Description: 
The RUN command initiates execution of the source program in the working 
storage area. 
Execution is preceded by program initialization.  Initialization clears any 
values indicated by CLEAR statements, sets the array dimensions, clears the 
list of active GOSUB statements, and resets the DATA pointer to the first DATA 
statement. 
00002
00001
RUN
Syntax: 
SAV[E]   fid 
SAV[E] ON fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The SAVE or SAVE ON command stores a BASIC source program as a newly-named 
file.  Files stored via the SAVE and RESAVE commands are EDIT-compatible, 
keyed ASCII files in which the EDIT key corresponds to the line number of the 
BASIC statement.  If a file of the fid already exists, it causes an error 
condition.  If the workspace is not empty and no file name has been specified, 
the SAVE command uses NONAME as the default fid. 
00002
00001
Syntax: 
SEA[L] fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The SEAL command is similar to SAVE except that the saved program may be 
executed only, and only in BASIC.  Likewise, other users with access to the 
sealed file may execute but not examine or save the program. 
00002
00001
Syntax: 
SEQ[UENCE] [n][,m][,r[-[s]]] 
Parameters: 
n    is the starting line number. 
m    is the increment 
r-s    specifies the range to be renumbered; specifying r without s means 
renumber only line r. 
r-    means renumber from r to the end of the program. 
Description: 
The SEQUENCE command renumbers (with pseudo-line numbers) a non-line-numbered 
file (see BUILD).  Although these files do not have line numbers in their 
'saved' format, pseudo-line numbers are appended when the program is 
'fetched'. 
00002
00001
Syntax: 
SHOW option 
Parameters: 
option    is defined as one of the following: 
    ALL               Displays all SHOW options and related information. 
    BASE              The index origin of the arrays (prints 0 or 1). 
    BREAKS            The line numbers of all current breakpoint settings. 
                      Prints NONE if there are no breakpoints, or ALL if every 
                      line is a breakpoint. 
    DELIMS            The delimiter characters for terminal and file INPUT 
                      statements.  If the blank character is a delimiter, the 
                      word BLANK is included in the display. 
    DIM [var[$]]...   The current dimensions of the array identified by var. 
                      If the array is not dimensioned, prints NOT DIMENSIONED. 
                      Specifying no var lists all currently dimensional 
                      arrays. 
    FILES             The stream number, file-id, file type, I/O modes, and 
                      queue status for each file I/O stream that is currently 
                      open. 
    FNS               Lists all multi-lined, user-defined functions which are 
                      currently in execution.  This will normally occur only 
                      during a BREAK or error halt condition.  Prints NONE if 
                      no such functions are active. 
    FUNCTIONS         Prints all currently defined function names.  Prints 
                      NOTHING TO SHOW if there are no active functions. 
    GOSUBS            Line numbers of active GOSUB statements. 
    MODE              Displays the last mode of program execution.  The 
                      possible modes of execution include FAST, FASTER, 
                      FASTEST, RUN, or the message "Program was not executed 
                      yet". 
    NEXTS             Line numbers of NEXT statements of active FOR-NEXT 
                      loops. 
    PRECISION         Current precision (prints SINGLE or DOUBLE). 
    READPT            Location in DATA statements from which the next datum 
                      will be accessed for a READ.  This consists of the 
                      program line number followed by a datum number (not the 
                      actual value of the datum) within the line.  Prints NONE 
                      if the program includes no DATA statements.  Prints DATA 
                      LIST EXHAUSTED if end of data condition exists. 
    TRACES            Line numbers of current TRACE settings.  Prints NONE if 
                      there are no TRACE settings, or ALL if all lines are to 
                      be traced. 
    VARS              Prints a list of all currently defined simple string and 
                      numeric variables.  Prints NOTHING TO SHOW if there are 
                      no active variables. 
Description: 
The SHOW command displays specified information on the user's output device. 
00002
00001
Syntax: 
' 
Description: 
These fields are represented by an apostrophe (not followed by E, L, R, or C) 
in a format-string.  This apostrophe is replaced by the first character of the 
string assigned to it.  All other characters in the string are ignored. 
Examples: 
    100 LET A$="ABCDE" 
    200 PRINT USING 300, A$ 
    300 : THE FIRST CHARACTER OF A$ IS '. 
Line 200 prints the message: 
    THE FIRST CHARACTER OF A$ IS A. 
Note that the apostrophe in line 300 (the image statement) has been replaced 
by the first character of A$.  All other characters in the string are ignored. 
00001
00002
Syntax: 
STA[RT] 
Description: 
The START command executes a compiled program using the previous execution 
mode.  The default execution mode is RUN.  If the program has been edited 
since the last execution, or has not been compiled or executed, BASIC prints 
an error message stating that the RUN command must be used. 
00001
Data Initialization Statements: 
CLEAR, DIM, OPTION, PROMPT 
Random Number Seed Generation Statements: 
RANDOMIZE, DDIGITS 
Assignment Statements: 
CHANGE, DATA, DELIMIT, INPUT, LET, 
LINPUT, MAT INPUT, MAT READ, READ, RESTORE 
Program Execution Control Statements: 
CHAIN, DOUNTIL-END DO, DO WHILE-END DO, END, 
FOR-NEXT, GOSUB-RETURN, GOTO, IBEX, IF-THEN, 
IF-THEN-ELSE, IF-THEN-ENDIF, LINK, ON, STOP, WHEN 
Output Control Statements: 
DIGITS, MARGIN, MAT PRINT, MAT PRINT USING, PAGE, PRINT 
PRINT USING 
Matrix Arithmetic Statements: 
MAT_ADDITION, MAT_ASSIGNMENT, MAT_CON, MAT_IDN, 
MAT_INNER_PRODUCT, MAT_INV, MAT_MULTIPLICATION, MAT_NUL, 
MAT_SIM, MAT_TRANSPOSE, MAT_ZER. 
These functions are: BCL, CLK$, CPU, DAT$, DATE$, DIG, ERL, ERM, ERN, ERT, 
HPOS, IDA, KEY, KYEN, KYES, KYF, KYL, KEY$, KYF$, KYL$, LBE, MAR, MNE, NUM, 
PPS, RNS, SEND$, TIM, TIME$, USR$, and VPS. 
  Function      Meaning 
  BCL 
                Returns the time of day as a numeric value in the form of 
                hours and decimal fraction of hours based upon a 24 hour 
                clock.  For example, at 3:42 P.M., BCL provides the result 
                15.7.  The BCL function has no argument. (See CLK$ for the 
                time of day as a character string.) 
  CLK$ 
                Returns the time of day as an eight character string in the 
                form hh:mm:ss.  For example, at 3:42 P.M. plus 12 seconds, 
                CLK$ provides the string result 15:42:12. 
  CPU 
                Returns the accumulated CPU time as a numeric value.  CPU time 
                is reported in seconds and fractions of seconds, and is 
                measured from the time BASIC is called.  Note that CPU time is 
                distinct from elapsed time. (See the TIM function.)  The CPU 
                function has no argument. 
  DAT$ 
                Returns the date as an eight character string in the form 
                mm/dd/yy.  For example, on December 1, 1984, DAT$ will provide 
                the string 12/01/84.  (See the IDA function for the date as a 
                numeric string.) 
  DATE$(expr) 
                Returns the nth day specified by expr (rounded to an integer) 
                starting in 1970.  The result is an eight character string in 
                the form mm/dd/yy.  If the value of expr is 0, the current 
                date is returned (the equivalent of the DAT$ function).  For 
                example, DATE$(5) returns 01/05/70, the fifth day from 
                01/01/70. 
  DIG 
                Returns the current DIGITS setting as a numeric value.  If a 
                DIGITS statement has not been executed during this BASIC 
                session, the default value of 6 is returned.  The DIG function 
                has no argument. 
  ERL 
                Returns the line number at which the latest error occurred. 
                If no run-time error has occurred since the program started, a 
                zero value is returned. 
  ERM 
                Displays the last run-time error message reported by the BASIC 
                processor.  If the buffer does not contain a run-time error, 
                BASIC displays a warning message.  Note, however, that the ERN 
                function contains the number of the actual error message. 
                     PRINT ERM 
                     A$=ERM 
  ERN 
                Returns the code number for the latest error.  If no error has 
                occurred since the program started, a zero value is returned. 
  ERT 
                Returns the type of error last-issued.  Returns 1 for monitor 
                errors, 2 for library errors, and 3 for BASIC run-time errors. 
                Return a zero if no error has occurred. 
  HPOS(expr) 
                Returns the current horizontal print position of the stream 
                specified by expr.  The selected streams must be opened to 
                unit record (UR) files.  The SET command must be used for this 
                procedure. 
  IDA 
                Returns the date as a numeric value in the form yymmdd.  For 
                example, on December 1, 1984, IDA would provide the integer 
                value 841201.  The IDA function has no argument. 
  KEY (expr) 
                Function to return the numeric KEY value of the most recently 
                attempted access to a file (whether successful or not) on the 
                input/output stream indicated by expr.  Expr is rounded to an 
                integer if required and must be in the range of 1 to 12.  For 
                consecutive files, the value returned will be a record number. 
  KYEN (stream, num-expr) 
                Returns a numeric value indicating whether or not a key value 
                exists.  Returns 0 if a key value does not exist, and 1 if a 
                key value does exist.  Key is equal to the value of the 
                num-expr.  Stream is rounded to an integer if required and 
                must be in the range of 1 to 12.  This function operates only 
                with numeric keys. 
  KYES (stream, str-expr) 
                Returns a numeric value indicating whether or not a key value 
                exists.  Returns 0 if a key value does not exist, and 1 if a 
                key value does exist.  Key is equal to the value of the 
                str-expr.  Stream is rounded to an integer if required and 
                must be in the range of 1 to 12.  This function operates only 
                with string keys.  This function can be used with indexed 
                files.  In this case, processing is performed with respect to 
                the primary key. 
  KYF (expr) 
                Similar to KEY, except returns value of key of first record in 
                the file.  Expr is rounded to an integer if record in the 
                range of 1 to 12.  For consecutive files, the value returned 
                will be one. 
  KYL (expr) 
                Similar to KEY, except returns value of key of last record in 
                file.  Expr is rounded to an integer if required and must be 
                in the range of 1 to 12.  For consecutive files, the value 
                returned will be a record number. 
  KEY$ (expr) 
                Function to return the string KEY value of the most recently 
                attempted access to a file (whether successful or not) on the 
                input/output stream.  Expr is rounded to an integer if 
                required and must be in the range of 1 to 12.  This function 
                can be used with indexed files.  In this case, processing is 
                performed with respect to the primary key. 
  KYF$ (expr) 
                Similar to KEY$, except returns the value of the first record 
                in the file.  This function can be used with indexed files. 
                In this case, processing is performed with respect to the 
                primary key. 
  KYL$ (expr) 
                Similar to KEY$, except returns the value of the last record 
                in the file.  This function can be used with indexed files. 
                In this case, processing is performed with respect to the 
                primary key. 
  LBE 
                Returns the integer portion of the last library error.  For 
                example, if a program attempted to get the square root of a 
                negative number, the library would return an XPE-00003 error, 
                and LBE would be set to three.  If no error has occurred since 
                the program started, a zero value is returned. 
  MAR (expr) 
                Function provides the present margin setting for the stream 
                number indicated by expr rounded to an integer.  Stream number 
                zero represents output for PRINT statements, and streams 1 to 
                12 are used for file output.  The result will be an integer 
                value greater than 39.  If the stream is not open, a zero is 
                returned. 
  MNE 
                Returns the integer portion of the last monitor error.  For 
                example, if a program attempted to open a file which did not 
                exist, the monitor would return an FMN-N00113 error, and MNE 
                would be set to 113.  If no error has occurred since the 
                program started, a zero is returned. 
  NUM (array-name) 
                Provides the number of elements currently present in the 
                indicated array.  If the array has no defined values, a zero 
                is returned.  If BASE=0, the elements of row and column zero 
                are included in NUM. 
  PPS(expr) 
                Returns the total page count for the specified stream.  The 
                selected streams must be opened to unit record (UR) files. 
                The SET command must be used for this procedure. 
  RNS 
                Returns the 36-bit value used internally by the RND function 
                to generate the next pseudo-random number.  If the bit pattern 
                of RNS is saved at the end of a run and used as the argument 
                of the RANDOMIZE statement in a subsequent run of a program, 
                the second run continues the sequence of pseudo-random 
                numbers. 
  SEND$ (str-expr) 
                Sends the str-expr to the OC and then waits for a response. 
                The function results in the operator's response.  A warning 
                will be printed if the response is greater than 255 
                characters.  If the user wants to send a message without 
                getting a response, that capability already exists in BASIC. 
                An IBEX command is provided which will pass commands to IBEX. 
                If the user wanted to send a message to the OC the user could 
                type: 
                    IBEX "M PLEASE MOUNT TAPE# 1234" 
  TIM 
                Returns the elapsed running time as a numeric value.  The 
                result of TIM is reported in seconds and fractions of seconds, 
                and is measured from the time BASIC is called.  Note that 
                elapsed time is not the same as CPU time charged to the 
                individual user. (See the CPU function.)  The TIM function has 
                no argument. 
  TIME$(expr) 
                Returns the time at midnight (24 hour clock) minus the number 
                of minutes specified by expr rounded to an integer.  The 
                result is a five character string in the form hh:mm.  If the 
                value for expr is 0, the current time is returned (the 
                equivalent of the CLK$ function).  For example, TIME$(10) 
                returns the time 23:50. 
  USR$ 
                Returns the user's account identification as a character 
                string of up to eight characters.  The USR$ function has no 
                argument. 
  VPS(expr) 
                Returns the current vertical print position of the specified 
                stream.  The selected streams must be opened to unit record 
                (UR) files.  The SET command must be used for this procedure. 
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
00018
00013
00014
00015
00019
00016
00020
00017
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
Syntax: 
STE[P] [n] 
Parameter: 
n    causes the execution of the next n lines in the program if a BASIC 
workspace is in the state of suspended execution.  An error condition is 
caused if the current state is not in suspended execution (i.e. after 
execution is interrupted via a BREAK keyin). 
Description: 
The STEP command permits the execution of one or more lines in a BASIC 
program. 
00002
00001
Syntax: 
line STOP 
Description: 
The STOP statement may occur anywhere in a program.  If a STOP is reached, the 
program halts, the GOSUB-RETURN stack is cleared.  The current program is 
available for resumed operation by a direct GOTO statement.  At this point, 
the values of variables used in the program are still intact. 
00001
String expressions are composed of sequences of string value representations 
(string constants, string variable references, or string function calls) 
connected by the concatenation operator.  String expressions can include 
numeric expressions for such purposes as subscript evaluation for string array 
references.  String expressions can also include substrings which contain 
numeric expressions. 
Either a plus sign (+) or an ampersand (&) is permitted as the concatenation 
operator.  The following example illustrates the use of the concatenation 
operator: 
    PRINT A$+"--"&B$ 
This statement prints the strings contained in A$ and B$, separated by two 
dashes. 
These functions are: CMP, DUP$, EDIT$, INSTR, LEFT$, LEN, LOC$ or LWRC$, MID$, 
POS, PPOS, REP$, RIGHT$, SCN, SEG$, SST$, and UPC$ or UPRC$. 
  Function      Meaning 
  CMP($expr1,$expr2) 
                The CMP function compares $expr1 to $expr2 as though they were 
                converted to the same case.  That is, a case blind comparison 
                of strings.  The resulting value of the CMP function is: 
                    -1 is $expr1 is less than $expr2. 
                    0 if $expr1 is equal to $expr2. 
                     +1 if $expr1 is greater than $expr2. 
                (See the description of the IF statement for the meaning of 
                less than, equal to, and greater than in string comparisons.) 
  DUP$(str-expr,num-expr) 
                Creates strings composed of repetitions of a string.  The 
                result consists of the concatenation of the specified (by the 
                numeric expression) number of instances of the string 
                expression.  If string expression has zero length, or if the 
                value of the numeric expression is zero, the string result is 
                of zero length.  The value of the numeric expression is 
                rounded to the nearest integral value, if required.  An error 
                condition is caused if the resultant string length would be 
                greater than 255, or if the value of the numeric expression is 
                negative. 
  EDIT$($expr1,expr2) 
                The EDIT$ function formats and edits a string according to the 
                specifications assigned to an integer specified by expr2. 
                $expr1 is a valid string expression. 
                expr2 is a value (rounded to an integer) equal to one integer 
                or to the sum of several of the following integers: 
                    2     delete all spaces and tabs 
                    4     delete CR, LF, FF, RUBOUT, NULL 
                    8     delete leading spaces and tabs 
                    16    reduce spaces and tabs to a single space 
                    32    convert lowercase to uppercase 
                    64    convert "[" to "(" and "]" to ")" 
                    128   delete trailing spaces and tabs 
                    256   do not alter characters inside quotes 
                For example: 
                    >10 PRINT EDIT$("THIS IS AN EXAMPLE",2) 
                    >20 PRINT EDIT$("this is an example",32) 
                    >30 PRINT EDIT$("THIS IS AN [ EXAMPLE ]",64) 
                    >40 PRINT EDIT$("THIS IS AN "" [ EXAMPLE "" ]",256+2+64) 
                    >50 END 
                This set of EDIT$ functions produces the following results: 
                    THISISANEXAMPLE               result of line 10 
                    THIS IS AN EXAMPLE            result of line 20 
                    THIS IS AN ( EXAMPLE )        result of line 30 
                    THISISAN" [ EXAMPLE ")        result of line 40 
                In the first line, all spaces are removed between words 
                because the value 2 is specified.  The second line is 
                converted to uppercase letters since the value 32 is 
                specified.  In the third line, both brackets are converted to 
                parentheses, since the value 64 is specified. 
                Line four is modified in several ways.  The value 256 
                specifies not to change anything within quotes.  Note that 
                BASIC uses double quotes to signify quotes ("" [ EXAMPLE "" 
                ]).  The value 2 removes blanks between the first three words 
                (THISISAN").  The value 64 converts only the second bracket to 
                a parenthesis, since the first one is within the double 
                quotes. 
  INSTR (expr1,$expr2,$expr3) 
                The INSTR function searches for the first occurrence of a 
                specified segment within a string. 
                expr1 is the number (rounded to an integer) of the character 
                position in $expr2 at which the search is to begin. 
                $expr2 is the string that is to be scanned for a segment 
                matching $expr3. 
                $expr3 is the segment string that is to be found. 
                The result of the INSTR function is the character position of 
                $expr3 in $expr2.  If the specified segment is not found, a 
                value of 0 is returned. 
  LEN($expr) 
                Returns the number of characters contained in $expr.  The 
                range of the result is 0 (null string) to the maximum string 
                length. 
  LEFT$($expr1,expr2) 
                The LEFT$ function returns the segment in a string which is to 
                the left of the specified character position. 
                $expr1 is the string that is to be scanned for a segment. 
                expr2 is the number (rounded to an integer) of the character 
                position in $expr1 that indicates the end of the segment to be 
                returned.  Everything to the left of expr2 in the string 
                $expr1 is returned. 
  LOC$($expr)    or    LWRC$ ($expr) 
                The LOC$ function converts all alphabetic characters within 
                $expr to lowercase.  Non-alphabetic characters contained in 
                $expr are not altered. 
  MID$($expr1,expr2,expr3) 
                The MID$ function returns a segment within a string. 
                $expr1 is the string to be scanned for a segment. 
                expr2 is the beginning character position of the segment to be 
                found. 
                expr3 is the length of the segment to be found starting at 
                expr2. 
                The result of the MID$ function is to return a segment whose 
                first character position is expr2 and length is expr3 from 
                $expr1. 
  POS ($expr1,$expr2,expr3) 
                The POS function searches for the first occurrence of a 
                specified segment within a string. 
                $expr1 is the string that is to be scanned for a segment 
                matching $expr2. 
                $expr2 is the segment string that is to be found. 
                expr3 is the number (rounded to an integer) of the character 
                position in $expr1 at which the search is to begin. 
                The result of the POS function is the character position of 
                $expr2 in $expr1.  If the specified segment is not found, a 
                value of 0 is returned. 
  PPOS(str-expr1,str-expr2,str-expr3,num-expr4,num-expr5) 
                The PPOS function searches for a specified segment within a 
                string, using a relational operator. 
                str-expr1 is the string to be scanned for a segment matching 
                str-expr3. 
                str-expr2 is the relational operator to be specified for the 
                scan.  Valid values for str-expr2 are: 
                    =   >=    =< 
                    >   =>    <> 
                    <   <=    >< 
                with no leading or trailing blanks. 
                str-expr3 is the string to be compared against str-expr1 based 
                on the relational operator in str-expr2. 
                num-expr4 is the number (rounded to an integer) of the 
                occurrence of str-expr3 that is to be found. 
                num-expr5 is the number (rounded to an integer) of the 
                character position in str-expr1 at which the search is to 
                begin.  If num-expr5 is positive, the search starts from left 
                to right at the character position (counting from the left) 
                equal to num-expr5. 
                If num-expr5 is negative, the search starts from right to left 
                at the character position (counting from the right) equal to 
                the absolute value of num-expr5. 
                The result of the PPOS function is the first character 
                position of the specified occurrence (by num-expr4) of 
                str-expr3 in str-expr1.  If the specified occurrence of 
                str-expr3 does not exist in str-expr1, the result of the PPOS 
                is zero.  Neither str-expr1 nor str-expr3 may be null strings. 
                For example: 
                    100 PRINT PPOS ("AJDHFHHHAN","<","AN",3,2) 
                    Result:  0 
                    200 PRINT PPOS ("AJDHFHHHAN",">=","A",1,2) 
                    Result:  2 
                The letter "J" in position 2 is greater than "A". 
  REP$($expr1,$expr2,$expr3,expr4,expr5) 
                The REP$ function performs substring replacement.  $expr1 is 
                the string that contains the substring that is to be replaced. 
                If $expr1 is a null string, the result of the function is a 
                null string. 
                $expr2 is the segment within $expr1 that is to be replaced. 
                $expr2 may not be a null string. 
                $expr3 is the segment that is to replace $expr2.  If $expr3 is 
                a null string, the specified occurrences of $expr2 are 
                deleted. 
                expr4 is an expression (rounded to an integer) that specifies 
                the number of occurrences of $expr2 that are to be replaced. 
                If expr4 is less than zero, then all occurrences of $expr2 
                from the position indicated by expr5 to the end of $expr1 are 
                replaced.  If expr4 equals one, then the first occurrence of 
                expr2 where expr5 is an expression (rounded to an integer) 
                that specifies the character position to $expr1 in which 
                search and replacement are to begin, and so on for other 
                values of expr4.  The string resulting from a REP$ replacement 
                can be no greater than the maximum string length.  The 
                following example illustrates the use of the REP$ function: 
                    100 A$ = "THE MOOSE IS BROWN AND 
                              THE GOOSE IS BROWN." 
                    200 B$ = "BROWN" 
                    300 C$ = "CHARTREUSE" 
                    400 D$ = REP$(A$,B$,C$,1,19) 
                    500 E$ = REP$(A$,B$,C$,-1,1) 
                    600 PRINT D$ 
                    700 PRINT E$ 
                Line 100 defines the string that is to be searched, and line 
                200 defines the substring that is to be searched for.  Line 
                300 defines the replacement substring.  Line 400 begins a 
                search at column 19, locating the second occurrence of BROWN 
                and performing the replacement.  Line 500 begins the search at 
                column 1 and replaces all occurrences of BROWN. 
                Execution of (lines 600 and 700 produce the following 
                messages: 
                    THE MOOSE IS BROWN AND THE GOOSE 
                    IS CHARTREUSE. 
                    THE MOOSE IS CHARTREUSE AND THE 
                    GOOSE IS CHARTREUSE. 
  RIGHT$($expr1,expr2) 
                The RIGHT$ function returns the segment in a string which is 
                to the right of the specified character position. 
                $expr1 is the string that is to be scanned for a segment. 
                expr2 is the number (rounded to an integer) of the character 
                position in $expr1 that indicates the beginning of the segment 
                to be returned.  Everything to the right of expr2 in $expr1 is 
                returned. 
  SCN($expr1,$expr2,expr3,expr4) 
                The SCN function searches for a specified segment within a 
                string. 
                $expr1 is the string that is to be scanned for a segment 
                matching $expr2. 
                $expr2 is the segment string that is to be found. 
                expr3 is the number (rounded to an integer) of the occurrence 
                of $expr2 that is to be found. 
                expr4 is the number (rounded to an integer) of the character 
                position in $expr1 at which the search is to begin. 
                The result of the SCN function is the first character position 
                of the specified occurrence (by expr3) of $expr2 in $expr1. 
                If the specified occurrence of $expr2 does not exist in 
                $expr1, the result of the SCN is zero.  Neither $expr1 nor 
                $expr2 may be null strings. 
                For example: 
                    100 A$ = "THE FROG IS GREEN." 
                    200 B = SCN(A$,"FROGS",1,3) 
                    300 C = SCN(A$,"G",2,4) 
                    400 PRINT "B=";B,"C=";C 
                Line 100 defines the string that is to be searched.  Line 200 
                scans for the first occurrence of the segment FROGS, beginning 
                at column 3.  Note that $expr2 is defined within quotes rather 
                than identified by a string variable:  either form is 
                permissible.  Line 300 searches for the second occurrence of 
                segment G, beginning at column 4.  Line 400 prints the 
                following message: 
                    B = 0        C = 13 
  SEG$($expr1,expr2,expr3) 
                The SEG$ function returns a segment within a string. 
                $expr1 is the string that is to be scanned for a segment whose 
                boundaries are the character positions specified by expr2 and 
                expr3. 
                expr2 is the beginning character position of the segment to be 
                returned. 
                expr3 is the ending character position of the segment to be 
                returned. 
                The numbers specified by expr2 and expr3 designate the 
                beginning and ending character positions of the segment to be 
                returned. 
  SST$($expr1,expr2,expr3) 
                The SST$ function performs substring generation. 
                $expr1 is the string from which the substring is to be 
                extracted.  This string may not be a null string unless expr3 
                is zero, in which case SST$ returns a zero-length string. 
                expr2 is the column in which the substring begins.  expr2 
                cannot be less than or equal to zero, nor can it specify a 
                starting position larger than the length of the $expr1. 
                expr3 is the number of characters in the substring. 
                The sum of expr3 and expr2 must be smaller than the length of 
                $expr1 plus 1.  The following example illustrates the SST$ 
                function: 
                    100 A$ = "THE GRYPHON IS GREAT." 
                    200 B$ = SST$(A$,5,7) 
                    300 PRINT B$ 
                Line 100 defines the string from which the substring is to be 
                subtracted.  Line 200 uses the SST$ function to locate a seven 
                character substring beginning in column five.  Line 300 prints 
                the designated substring, which appears as: 
                    GRYPHON 
  UPC$($expr)    or    UPRC$($expr) 
                The UPC$ function converts all alphabetic characters contained 
                in $expr to uppercase.  Non-alphabetic characters are not 
                affected. 
00001
00002
00003
00004
00006
00005
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
Subscript expressions always identify the use of a name as an array usage, and 
the number of dimensions.  The values of subscript expressions are, if 
necessary, rounded to integer numbers.  In DIM and MAT statements, the values 
of subscript expressions are used to indicate the upper bounds of the 
dimensions of arrays.  Lower bounds are always 1 or 0, depending on the BASE 
value, which may be set by an OPTION statement.  In other BASIC statements, 
subscript expressions are used to indicate a single element in an array. 
For example, if an array represented by the array name H has the form: 
    1 2 3 
    4 5 6 
    7 8 9 
the following holds true: 
    H(1,1) = 1 
    H(1,2) = 2 
    H(1,3) = 3 
    H(2,1) = 4 
    H(2,2) = 5 
    H(2,3) = 6 
    H(3,1) = 7 
    H(3,2) = 8 
    H(3,3) = 9 
Syntax: 
SYS 
Description: 
The SYS command closes all open files and returns control to the command 
processor level.  If BASIC has been invoked from a processor other than the 
command processor, SYS returns control to that processor. 
00001
Syntax: 
[line] TRACE {ON|OFF}[line[,line]...] 
Parameters: 
ON    specifies that when the TRACE point is encountered in the program or is 
issued as a direct statement during suspended execution, the message AT xxxxx 
is printed (where xxxxx represents a line number).  By including line numbers 
in the TRACE statement, the user can specify which lines are to be flagged. 
OFF    specifies that when TRACE OFF is specified with line numbers, the 
indicated tracepoints are removed.  When line numbers are omitted, TRACE OFF 
removes all tracepoints. 
Description: 
The TRACE statement tracks program flow and is a valuable aid in debugging as 
it can reveal invalid branches in the program logic.  TRACE is similar to 
BREAK with an automatic PROCEED issued at every flagged line. 
Usage Note: 
If BREAK and TRACE are assigned to the same line, only BREAK applies. 
However, if a breakpoint is removed from a line that has a tracepoint assigned 
to it, the tracepoint remains active.  TRACE and BREAK may both be set to "ON" 
to non-executable statements, (e.g., REM) but when printout message "AT XXXX" 
occurs, XXXX will be first executable statement following REM. 
00002
00001
00003
These functions are: ACS or ACOS, ASN or ASIN, ATN, COS, COT, CSC, DEG, HCS or 
COSH, HSN or SINH, HTN or TANH, RAD, SEC, SIN, and TAN. 
  Function     Meaning            Arg. Domain      Range Result   Inaccuracies 
ACS(expr)    The mathematical   -1 <= expr <= 1. 0 to PI        Accuracy 
    or       arccosine                                          deteriorates 
ACOS(expr)   function.                                          for expr 
                                                                between .9 
                                                                and 1. 
ASN(expr)    The mathematical   -1 <= expr <= 1. -PI/2 to PI/2  Accuracy 
    or       arcsine function                                   deteriorates 
ASIN(expr)                                                      for expr 
                                                                between .9 
                                                                and 1. 
ATN(expr)    The mathematical   Any numeric      -PI/2 to PI/2  None. 
             arctangent         value 
             function. 
COS(expr)    The mathematical   Single and       -1 to 1        For arguments 
             cosine function    double                          greater than 
             with expr in       precision: 0                    PI/2, about 
             radians.           4095 radians.                   one decimal 
                                Range                           place of 
                                restrictions                    accuracy is 
                                provide minimum                 lost for each 
                                of 6-place                      additional 
                                accuracy near                   power of ten 
                                extremes.                       multiple of 
                                                                PI/2. 
COT(expr)    The mathematical   Single           0 to 10E+16    Argument near 
             cotangent          precision:                      integral 
             function, with     0 to 10E+3                      multiples of 
             expr in radians.   radians.                        PI result in 
                                Double                          an error. 
                                precision: 0 to                 For arguments 
                                10E+13 radians.                 greater than 
                                Range                           PI/2, about 
                                restrictions                    one decimal 
                                provide a                       place of 
                                minimum of                      accuracy is 
                                6-place                         lost for each 
                                accuracy                        additional 
                                near extremes.                  power of 
                                                                ten multiple 
                                                                of PI/2. 
CSC(expr)    The mathematical   Single and       10E-156 to     Arguments 
             cosecant           double           10E+151        near integral 
             function.          precision: 0 to                 multiples of 
                                4095 radians.                   PI result in 
                                Range                           an error. For 
                                restrictions                    arguments 
                                provide a                       greater than 
                                minimum of                      PI/2, about 
                                provide a                       one decimal 
                                minimum of                      place of 
                                6-place                         accuracy is 
                                accuracy near                   lost for each 
                                extremes.                       additional 
                                                                power of ten 
                                                                multiple of 
                                                                PI/2. 
DEG(expr)    Converts radians   expr <= 10E+151  -10E+151 to    None. 
             to degrees.                         10E+151 
HCS(expr)    The mathematical   -352<=expr<=352  0 to 10E+151   None. 
   or        hyperbolic 
COSH(expr)   cosine function. 
HSN(expr)    The mathematical   -352<=expr<=352  -10E152 to     None. 
    or       hyperbolic sine                     10E+151 
SINH(expr)   function. 
HTN(expr)    The mathematical   expr <= 10E+152  -1 to 1.       None. 
   or        hyperbolic 
TANH(expr)   tangent 
             function. 
RAD(expr)    Converts degrees   expr <= 10E+152  -10E151 to     None. 
             to radians.                         10E+151 
SEC(expr)    The mathematical   Single and       10E-156 to     Arguments 
             secant function,   double           10E+151        should not be 
             with argument in   precision: 0 to                 near odd 
             radians.           4095 radians.                   integral 
                                                                multiples of 
                                                                PI/2.  If 
                                                                expr > PI/2, 
                                                                about one 
                                                                decimal 
                                                                place of 
                                                                accuracy is 
                                                                lost for 
                                                                each power of 
                                                                ten multiple 
                                                                of PI/2. 
SIN(expr)    The mathematical   Single and       -1 to 1        If expr > 
             sine function,     double                          PI/2, about 
             with argument in   precision: 0 to                 one decimal 
             radians.           4095 radians.                   place of 
                                                                accuracy is 
                                                                lost for 
                                                                each power of 
                                                                ten multiple 
                                                                of PI/2. 
TAN(expr)    The mathematical   Single and       0 to 10E+16    Arguments 
             tangent            double                          should not be 
             function.          precision: 0 to                 odd integral 
                                4095 radians.                   multiples of 
                                                                PI/2. 
                                                                If expr > 
                                                                PI/2, about 
                                                                one decimal 
                                                                place of 
                                                                accuracy is 
                                                                lost for 
                                                                each 
                                                                additional 
                                                                power of 
                                                                PI/2. 
Syntax: 
[line] statement1 UNLESS truth-expression 
Parameters: 
statement1    specifies any allowable BASIC statement. 
truth-expression    is any numeric expression. 
Description: 
The UNLESS modifier defines a condition which controls the execution of a 
statement.  The statements executes only if the expression is false. 
Examples: 
Using the UNLESS modifier, BASIC checks to see if the condition set is true or 
false.  The value for B is only printed if A is not equal to 0 (i.e. the 
expression is false). 
    20 A = 0 
    30 B = 20 IF A = 2 
    40 PRINT B UNLESS A = 0 
00002
00003
00001
Syntax: 
UNS[AVE] [fid] 
Parameters: 
fid    is a valid CP-6 file identifier. 
Description: 
The UNSAVE command deletes the specified file from the workspace.  If fid is 
not specified, the file corresponding to the current workspace name is 
deleted. 
00002
00001
Syntax: 
[line] statement1 UNTIL truth-expression 
Parameters: 
statement1    is any allowable BASIC statement. 
truth-expression    is any numeric expression. 
Description: 
The UNTIL modifier defines a loop that executes until a truth expression 
proves true.  At least one execution is performed. 
Examples: 
The UNTIL modifier is used to repeat a loop until the condition becomes true. 
The values for J continue to print until J is equal to 41. 
    10 J = 35 
    20 J = J + 1 UNTIL J > 40 
    30 PRINT J 
00002
00003
00001
  A variable name may be associated with a scalar numeric value, a text string 
  or a one or two dimensional array of numeric values or strings.  A variable 
  name may consist of from one to thirty-one total characters.  Use of 
  variable names greater than one letter may cause incompatibilities with 
  other BASICs. 
Syntax: 
Simple Variable Names 
letter [digit|letter|underscore][digit|letter|underscore]...] [$] 
The presence of a $ indicates a string variable.  A simple variable name is 
never immediately followed by a subscript expression. 
Array Names 
letter [digit|letter|underscore][digit|letter|underscore]...] 
       [$] [(num-expr[,num-expr])] 
The presence of a $ indicates a string array.  If an array name does not 
include subscript(s), it must be in a MAT or CHANGE statement. 
The only exception is that any name beginning with FN is a reference to a 
user-defined function (see the DEF statement). 
00001
Syntax: 
WEA[VE] fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The WEAVE command adds a saved BASIC program to the program currently in the 
user's working storage.  WEAVE behaves as if the lines in the file were being 
entered via the terminal.  For example, if a line in the file being accessed 
has the same number as a line of the current program, the line from the new 
file replaces the existing line. 
00002
00001
Syntax: 
WFS[AVE] [{ON|OFF}] 
Parameters: 
ON    specifies that the workspace file is to be saved. 
OFF    specifies that no workspace is to be saved. 
Description: 
The WFSAVE command allows the user the option of whether or not to save the 
workspace file when abnormally exiting Basic due to an error condition.  If no 
option is specified, the default is ON. 
00002
00001
Syntax: 
[line] WHEN BREAK GOTO {line|ERROR} 
[line] WHEN ERROR [int[,int]...] GOTO {line|ERROR} 
[line] WHEN EOF[#][stream] GOTO {line|ERROR} 
[line] WHEN MONERR GOTO {line|ERROR} 
[line] WHEN LIBERR GOTO {line|ERROR} 
[line] WHEN DBERR {[int[,int]...]|OTHER} GOTO line 
Parameters: 
WHEN BREAK    modifies the action BASIC takes when the user enters a BREAK to 
interrupt program operation.  If BREAK response is set to a line number, the 
program retains control.  This feature must be used with caution, since it can 
create a situation in which the user must leave BASIC to regain control.  The 
form WHEN BREAK GOTO ERROR restores the normal BREAK response. 
WHEN ERROR    modifies the action BASIC takes in the event of specified 
run-time errors.  One or more integer error numbers may be specified in a WHEN 
ERROR statement.  If no error number is specified, the WHEN ERROR statement 
sets all error control to the indicated line number.  If the word ERROR is 
specified after the GOTO, all error responses are reset to the conventional 
error messages and program suspension. 
int    specifies the DB error number. 
WHEN EOF    sets control for an end-of-file condition on the stream number 
specified by integer. 
stream    is an integer between 1 and 12, inclusive.  If no stream number is 
indicated, the WHEN EOF control applies to all streams.  A designated 
input/output stream need not be currently open for input at the time a WHEN 
EOF is executed.  However, a compile-time error is reported if the number of 
the file stream is out of range. 
WHEN MONERR    sets control when a CP-6 monitor error is issued. 
WHEN LIBERR    sets control when a CP-6 library error is issued. 
WHEN DBERR     transfers control to the given line number if the specified 
error occurs as a result of a DB type statement. 
OTHER    implies a catch-all for data base errors which have not been 
previously mentioned in WHEN DBERR statements. 
Description: 
The WHEN statement is used to establish user control over conditions that may 
occur during the execution of a program. 
Usage Notes: 
All WHEN statements that set control to a specific line number are reset to 
normal control by any action that modifies the current program.  Also, the 
line number following the GOTO must not violate the rules for GOTO statements. 
See the ERL, ERN, ERT, LBE, and MNE functions. 
00002
00001
00003
Syntax: 
[line] statement1 WHILE truth-expression 
Parameters: 
statement1    is any allowable BASIC statement. 
truth-expression    is any numeric expression. 
Description: 
The WHILE modifier defines a loop that executes while a truth expression 
proves true. 
Examples: 
The WHILE modifier repeats the following loop as long as the condition is 
true.  Therefore, in the following example, C is read until C=8. 
    10 C = 2 
    20 C = C + 2 
    30 READ C WHILE C < 8 
00002
00003
00001
Syntax: 
WLO[AD] fid 
Parameter: 
fid    is a valid CP-6 file identifier. 
Description: 
The WLOAD command replaces the user's current working storage with the 
contents of a WSAVE file.  If the indicated working storage file exists and 
can be loaded for execution under BASIC, the following sequence occurs: 
1.  The user's current working storage is cleared. 
2.  The remaining part of the saved working storage provides values for named 
    scalar and array variables, MARGIN settings, etc.  Data file status is not 
    changed; however, if the environment attempts to reopen files that no 
    longer exist or attempts to access keys that have been deleted, an error 
    diagnostic message is printed. 
3.  The source program, which constitutes the first part of a WSAVE file, is 
    read and loaded as described under the LOAD command. 
00002
00001
Syntax: 
WRE[SAVE] [fid] 
Parameter: 
fid    is a valid CP-6 file identifier.  If fid is not specified, the default 
name assigned is NONAME. 
Description: 
The WRESAVE command performs the same function as the WSAVE command but allows 
replacement of an already existing file. 
00002
00001
Syntax: 
WSA[VE] [fid] 
Parameter: 
fid    is a valid CP-6 file identifier.  If fid is not specified, the default 
name assigned is NONAME. 
Description: 
The WSAVE command saves the current user's working storage environment as a 
newly-named file.  The information saved is sufficient enough to permit the 
user to continue execution from the point of interruption.  If a fid already 
exists, it causes an error condition. 
00002
00001
Syntax: 
WSE[AL] [COMPILE [FAST|FASTER|FASTEST]] fid 
Parameters: 
COMPILE    compiles the Basic program before  saving the workspace. 
FAST|FASTER|FASTEST    are the levels of optimization of that compilation. 
The default is the normal compile mode. 
fid    is a valid CP-6 file identifier. 
Description: 
The WSEAL command functions similarly to the SEAL command, except that it 
operates upon the entire working storage environment.  A sealed working 
storage environment cannot be modified or examined by a user except the 
creator. 
00002
00001
Syntax: 
XRE[F] [option] 
Parameters: 
Option is as follows: 
    Any simple numeric variable. 
    Any simple string variable. 
    Any line number. 
    The keyword MAT followed by a legal variable name. 
    Any of the following phrases may be used: 
        LINE NUMBERS 
        NUMERIC VARIABLES 
        NUMERIC ARRAYS 
        STRING VARIABLES 
        STRING ARRAYS 
        STRING FUNCTIONS 
Description: 
The XREF command produces an alphabetical cross reference list of the source 
program in working storage, including:  all simple numeric variables, simple 
string variables, numeric arrays, string arrays, numeric functions, string 
functions, and line number references in that order.  Each category will 
appear under a separate heading.  A category heading will be printed only if 
there are items for that category.  If no option is specified, all cross 
references are listed. 
Examples: 
XREF A$ 
cross references just the variable A$. 
XREF 110 
cross references the line number 110. 
XREF MAT A 
cross references the matrix A. 
XREF STRING FUNCTIONS 
cross references all string functions. 
XREF 
cross references all line numbers, variables, arrays, and functions. 
00002
00003
00001
Syntax: 
X 
Description: 
The X command allows the user to exit BASIC.  Control is transferred to the 
operating system. 
MAT ADDITION, MAT ASSIGNMENT, MAT CON, MAT IDN, MAT INNER PRODUCT, MAT INV, 
MAT MULTIPLICATION BY A SCALAR, MAT NUM, MAT SIM, MAT TRANSPOSE, MAT ZER 
File Access Statements: 
CLOSE, DELIMIT#, DELREC, DEQ, ENQE, ENQS, GET:, INPUT#, LINPUT#, MAT GET, MAT 
INPUT#, MAP, MAT PRINT#, MAT PUT:, OPEN, PRINT#, PRINT# USING, PUT:, RESTORE 
Documentation and Debugging Statements: 
BREAK, NULL, PROCEED, REM, TRACE 
I-D-S/II Interface Statements: 
DB FROM, DBMEMBERINFO$, MAT DBNAMES$, MAT DBTYPES, DBOWNERINFO$, DB SUB, DB TO 
00001
