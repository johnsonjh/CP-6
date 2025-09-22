For host library service topics, enter: 
!HELP (HOSTLIB) TOPICS 
Topics include the following: 
    Service names (e.g., XUR$GETCMD) for call format, parameters, description, 
    etc.  To view the complete information on a service, type ? or ??.  Parts 
    of the complete message can be viewed by specifying a subtopic, e.g., 
    !HELP (HOSTLIB) XUU$READ PARAMETERS.  Subtopics are as follows (unless 
    otherwise indicated):  PARAMETERS, DESCRIPTION, and if appropriate, ERROR 
    and EXAMPLE. 
    Structure names (e.g., XUR_INIT) for a description of the keywords or 
    field names within the structure. 
    Functional Code Group for summary information including any of the 
    following: 
    XSA    Fast Sequential File Access Services 
    XSF    FIT Access Services 
    XUD    Date and Time Services 
    XUE    Preprocess and Evaluation Services 
    XUF    Formatted Write Service 
    XUG    Command Reading and Error Reporting Services 
    XUH    HELP Service 
    XUM    Least Recently Used Algorithm Services 
    XUO    Object Unit Generation Services 
    XUP    Parsing Services 
    XUR    Command Reading and Error Reporting Services 
    XUS    Correct Spelling Service 
    XUU    Source Update Services 
    XUW    Wildcard Services 
    XUX    Processor Invocation Services 
Most topics in this help facility begin with the Functional Code Group prefix, 
e.g., XUG.  Topics not conforming to this convention are correlated to their 
Functional Code Group in the following list.    XUD -  DATA_TYPES, 
DATE_TIME_PICTURE, DATE_TIME_EXAMPLES, TIMESPAN_PICTURE, TIMESPAN_EXAMPLES 
XUE -  EXPRESSION_EVALUATION, PREPROCESSOR_EXPRESSIONS, X$DEC_CONVERT, X$EVAL, 
X$GET_VAR, X$PRE_PROCESS, X$PUT_VAR, X$STRIP_BLANKS 
XUF -  COUNT_EXPRESSIONS, FMT, FORMATTING_CODES, FMT_FLAGS, MISC_INSERT_CODE, 
NUM_INSERT_CODE, CHAR_INSERT_CODE, X$FORMAT, X$WRITE, F_FDS 
XUH -  X$HELP 
XUP -  PARSING_TOOLS, X$PARSE, OUT$BLK, PARSE$OUT, OUT$SYM, PARSE$SYM, P_PCB, 
PCB, P$KEYWORDS, PARAM, PARSE$PARAM PARTRGE_STRUCTURES, P$NODE, P$LIT, P$SYM, 
P$DSTR 
XUU -  UPDATE_FILE_FORMAT 
XUW -  X$WILDCMP, X$WILDFMT, XUW_WILDCARD 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
The E03 Host release changed the definition of a UTS.  This invalidates using 
a UTS to store a timespan that exceeds an interval of about fifteen years. 
Since the UTS tick rate is no longer a single constant value, all XUD services 
that use clock ticks have been redefined to use a number of centiseconds (i.e. 
hundredths of seconds).  This is to ensure compatibility with previous 
releases. 
Five new services have been added to replace the lost ability to perform math 
directly on UTS values.  These are:  XUD$UTS_ADJUST, XUD$UTS_ADJ_25TH, 
XUD$UTS_DIFF, XUD$UTS_DIFF_25TH, and XUD$UTS_DIFF_SEC. 
The new field INPUT_DCB was added to the XUE_ECB structure. 
A description for the return values of valueless functions was added to XUE. 
For XUF, changes were made to insertion code J to allow the CNT(2) field for 
DCB#. 
For XUG, PROMPT/RPROMPT was revised to disallow the use of TEXTC structures. 
For XUR, an error_code field was added to XUR$OPENOUT. 
For a description of the character insertion codes, type: 
HELP (HOSTLIB) CHAR_INSERT_CODE code 
where code is A or T. 
  Code           Meaning 
  A 
                 Move a TEXT string CNT(1) characters long into a field CNT(0) 
                 characters wide.  The default for CNT(1) is the value of 
                 CNT(0).  If CNT(1)=0 or exceeds the length of the current 
                 data vector, then the remainder of the current data vector is 
                 used. 
                 If CNT(2) is 1 or 2, the text presented by the A-function is 
                 translated using the B$XL_ASC_DUMP or B$XL_EBC_DUMP table, 
                 respectively.  See the CP-6 Host Monitor Services Reference, 
                 Appendix G for more information on these translation tables. 
                 Note that if CNT(2) is specified, CNT(1) is also specified, 
                 so its default value (CNT(0)) must be specified explicitly. 
                 For example, %2..1A displays the last two characters of the 
                 current data vector, while %2A displays the next two 
                 characters. 
  T 
                 Move a TEXTC string.  The current data pointer is assumed to 
                 point to a TEXTC string which is to be moved into a field 
                 CNT(0) characters wide according to the setting of the L and 
                 M flags.  CNT(0)=0 means move the entire string. 
00001
00002
For a description of each count expression, type: 
HELP (HOSTLIB) COUNT_EXP exp 
where exp is one of the following:  N, #, or :  . 
  Expression   Meaning 
  N 
               Supply data for a CNT field.  If the current value for CNT is 
               greater than 0 and less than 36, then that many bits of data 
               are obtained for the current CNT.  Otherwise one word of data 
               is obtained.  For example, %ND obtains a 36-bit word for CNT(0) 
               and displays the next word as a decimal number in a field 
               CNT(0) characters wide; %9NA is equivalent to %T. 
  # 
               Variable reference.  Replaces the current CNT value with the 
               variable numbered by the value being replaced.  For example, 
               %1#.0= assigns the value of variable-1 to variable-0.  The 
               example could be abbreviated %1#=.  If the reference number 
               exceeds 99, the words of the F_FDS are referenced instead (up 
               to 100+sizew(F_FDS)).  Note that only reference to F_FDS is 
               permitted.  Some useful items that might be referenced from 
               F_FDS include BUFSIZE, BUFX, MEMSZ, and USERDATn. 
  : 
               CNT expression.  The current CNT value is saved and 
               reinitialized to zero.  When a CNT expression operator is 
               encountered, the current CNT value is replaced by 
               saved_value-operator-current_value.  For example, :4- could be 
               used to subtract four from the CNT value.  The operators and 
               their meanings for the expression a:b(op) are: 
               a:b+  =a+b          a:b-  =a-b          a:b*  =a*b 
               a:b&  =a&b          a:b|  =a|b          a:b\  =a\b 
               a:b/  =a/b          a:b>  =max(a,b)     a:b<  =min(a,b) 
               a:b=  assigns a to variable-b, CNT remains as a. 
               a:b?  =sign(a-b) 
00002
00003
00001
The XUD services support two representations of date and time:  UTS and DATE. 
A UTS, the standard CP-6 Universal Time Stamp, is a 36-bit binary value.  A 
DATE is a packed signed decimal doubleword containing the time elapsed since 
midnight on Jan. 1, 1 A.D.  A UTS can represent dates from Jan. 1, 1978 
through Feb. 6, 2020.  The range for a DATE is in excess of 300,000 years B.C 
and A.D. 
A DATE value may be treated as either a date and time, or as a timespan.  A 
UTS value should be treated only as a date and time, not as a timespan.  Using 
a UTS as a timespan may have unpredictable results.  In such cases, use of the 
XUD$UTS_ADJUST and XUD$UTS_DIFF services is recommended.  This 
unpredictability is due to the internal structure of a UTS.  A UTS as an 
interval becomes invalid at a span of around 15 years.  A timespan is similar 
to a date and time, except that it represents an interval of time rather than 
a fixed date and time.  The internal representation is the same in either 
case, but the formatting rules are different. 
UTS fields can be character aligned.  DATE fields can be nibble aligned.  It 
is generally most convenient to define a UTS as a 4-character field, and a 
DATE as an 8-character field.  It is sometimes possible for programs to 
operate directly on dates by treating them as a count of hundredths of 
seconds.  In PL-6 programs, a UTS can be defined as a UBIN WORD.  In COBOL 
programs, a DATE can be defined as COMP-4 SIGN LEADING PIC 9(15).  A UTS can 
be defined as COMP-6 in COBOL, or INTEGER in FORTRAN, so long as its value 
does not exceed Nov. 20, 1988. 
Dates can be represented as fixed and variable length (TEXTC) character 
strings as well as the DATE and UTS internal forms.  When dates are 
represented as character strings, the user may provide a picture that 
describes the format of the string.  A default picture is used if none is 
provided.  Date pictures and defaults are described below. 
Although nominally accurate to the hundredth of a second, all dates are 
calculated according to the Gregorian calendar, which was devised by the 
Council of Trent in 1582, and was not in general use until about 150 years 
later.  Dates earlier than 1582 should be regarded as approximate; they will 
almost certainly not correspond to dates according to the calendar in use at 
the time. 
NOTE:  Although time/date values are precise to the hundredth of a second, the 
accuracy depends entirely upon the operator's entry of the accurate time. 
NOTE:  centisecond timespans as used by XUD$UTS_ADJUST and XUD$UTS_DIFF are 
signed values only capable of spanning approximately 11 years in either 
direction. 
The following examples illustrate how the first and last days of the year 1985 
appear using various date formats: 
Picture                 Formatted Result 
-------                 ---------------- 
MM/DD/YY                01/01/85       12/31/85 
MMM.D,'YY               JAN.1,'85      DEC.31,'85 
Q"Q"YY                  1Q85           4Q85 
w Mmm d,yyyy            Tu Jan 1,1985  Tu Dec 31,1985 
Www m/dd/yy             Tue 1/01/85    Tue 12/31/85 
The following examples show the effect of various pictures in formatting a 
given time: 
Picture                 Formatted Result 
-------                 ---------------- 
HH:MM:SS.TT             13:30:10.50 
H "O'CLOCK"             13 O'CLOCK 
H "O'CLOCK" AM          1 O'CLOCK PM 
HH:MM AM                01:30 PM 
H:MM:SS.T AM            1:30:10.5 PM 
The following examples show how both date and time can be formatted as a 
single value: 
Picture                 Formatted Result 
-------                 ---------------- 
MM/DD/YY! HH:MM:SS      05/06/85 13:30:10 
Mmm d 'YY, !HH:MMAM     May 6 85, 01:30PM 
The format of dates is defined by a picture that contains identifiers for the 
date and time subfields along with any desired punctuation characters. 
The following subfield identifiers are for the date: 
    M       the month, with zero suppression (1 to 12). 
    MM      the month, without zero suppression (01 to 12). 
    D       the day of the month, with zero suppression (1 to 31). 
    DD      the day of the month, without zero suppression (01 to 31). 
    Y       the last digit of the year (0 to 9). 
    YY      the last two digits of the year, without zero suppression 
            (00 to 99). 
    YYY     the last four digits of the year, with zero suppression 
            (0 to 9999). 
    YYYY    same as YYY. 
    YYYYY   the year, with zero suppression (1 to 316888). 
    YYYYYY  same as YYYYY. 
    J       the day of the year, with zero suppression (1 to 366). 
    JJ      same as J. 
    JJJ     the day of the year, without zero suppression (001 to 366). 
    Q       the quarter of the year (1 to 4). 
        All of the above are case insensitive. 
    MMM     the abbreviated month name (JAN to DEC). 
    MMMM    the unabbreviated month name (JANUARY to DECEMBER). 
    W       the minimal abbreviation of the day of the week 
            (SU, M, TU, W, TH, F, SA). 
    WW      the day of the week abbreviated to two characters 
            (SU to SA). 
    WWW     the day of the week abbreviated to three characters 
            (SUN to SAT). 
    WWWW    the unabbreviated day of the week (SUNDAY to SATURDAY). 
        The above appear in the same case as the identifier: 
        uppercase, initial capital, or lowercase.  A single 
        lowercase w gives a value with an initial capital. 
        Five or more Ms or Ws are equivalent to four Ms or Ws. 
    AD      results in "AD" for years Anno Domini, 
            and "BC" for years Before Christ. 
    A.D.    results in "A.D." for years Anno Domini, 
            and "B.C." for years Before Christ. 
    BC      results in nothing for years Anno Domini, 
            and "BC" for years Before Christ. 
    B.C.    results in nothing for years Anno Domini, 
            and "B.C." for years Before Christ. 
    BCE     results in nothing for years within the Common Era, 
            and "BCE" for years Before Common Era. 
    B.C.E.  results in nothing for years within the Common Era, 
            and "B.C.E." for years Before Common Era. 
    CE      results in "CE" for years within the Common Era, 
            and "BCE" for years Before Common Era. 
    C.E.    results in "C.E." for years within the Common Era, 
            and "B.C.E." for years Before Common Era. 
The following subfield identifiers are for the time: 
    H       the hour, with leading zero suppression (0 to 23). 
    HH      the hour, without zero suppression (00 to 23). 
    M       the minute, with leading zero suppression (0 to 59). 
    MM      the minute, without zero suppression (00 to 59). 
    S       the second, with leading zero suppression (0 to 59). 
    SS      the second, without zero suppression (00 to 59). 
    T       hundredths of a second, with trailing zero suppression 
            (0 to 99). 
    TT      hundredths of a second, without zero suppression (00 to 99). 
        All of the above are case insensitive. 
    AM      results in "AM" for times before noon, and "PM" for times 
            after noon, and specifies that hours are presented modulus 
            12.  Noon is 12 PM.  Midnight is 12 AM. 
    PM      same as AM. 
    A.M.    results in "A.M." for times before noon, and "P.M." for 
            times after noon, and specifies that hours are presented 
            modulus 12.  Noon is 12 PM.  Midnight is 12 AM. 
    P.M.    same as A.M. 
When the picture specifies both date and time, an (!) exclamation mark must 
separate them.  If a blank or other punctuation is required between the date 
and time, it should be placed in the picture just before or after the (!) 
exclamation mark. 
Only one occurrence of each subfield (day, month, year, weekday, and era for 
dates; hour, minute, second, hundredths of seconds, and meridiem for time) is 
allowed in a given picture.  The Julian day and quarter of the year specify 
both the month and the day for purposes of detecting duplicate subfields. 
Time subfields must be specified in order: hours, minutes, seconds, and 
hundredths.  If any subfield is omitted, the following subfields must also be 
omitted.  The meridiem, if specified, must follow all other time subfields. 
Date subfields can appear in any order and in any meaningful combination, but 
ambiguous combinations of subfields are disallowed.  An ambiguous combination 
is one that does not designate a specific date and time.  For example, "March, 
2PM" and "Wednesday, 1985" are ambiguous in this sense. 
Any blanks, digits, and punctuation characters in a picture appear in the same 
position in each formatted value as in the picture.  Punctuation characters 
must not have a decimal value greater than 255. 
Alphabetic characters (and anything else) enclosed in (") double quote marks 
are treated as punctuation.  All alphabetic characters not enclosed in (") 
double quotes must be subfield identifiers.  Double ("") double quotes within 
a double quoted string appear as a single (") double quote in formatted 
values. 
A punctuation character is required between two alphabetic subfields. 
Adjacent numeric subfields are allowed, but a zero suppressed subfield cannot 
be immediately followed by another numeric subfield.  These restrictions are 
required to insure that any value output through a picture can be read back 
without ambiguity. 
The X$EVAL service performs evaluation of expressions that 
o   Conform to the IBEX conventions described in the HELP (IBEX) EXPRESSION 
    topic.  Expressions can include decimal strings, command variables, 
    built-in functions, etc.  For example, decimal strings and command 
    variables appear in the following: 
    !LET A='123' 
    !LET B=100 
    !LET C=A+B 
    which results in '223' as the value of C. 
o   May include user-defined functions that are similar to built-in functions. 
    A user-supplied routine to process these functions is invoked by X$EVAL. 
    This routine is called the User-Defined Functions Routine. 
o   May include private command variables or user-managed command variables. 
    When private command variables are required, the X$EVAL service performs a 
    call to M$CMDVAR to get or store variables.  If the program -- instead of 
    using standard command variables or private command variables -- prefers 
    to manage its own variables, X$EVAL invokes a routine supplied by the user 
    for this purpose; this routine is called the User-Managed Variables 
    Routine. 
Formatting codes, delimited on the left by the % symbol, appear in the 
following format: 
    %si 
For more information, type ? 
s    specifies one or a combination of count expressions and flags, if 
applicable to the format function identified by the insertion (i) code.  When 
applicable, flags may be coded in any sequence. 
    count expression    may include four counts.  In subsequent explanations, 
    the counts are referred to as CNT(0), CNT(1), CNT(2), CNT(3).  In 
    specifying counts as part of the FMT string, the following format is used: 
    c0.c1.c2.c3 where cn is the expression for the corresponding count.  In 
    scanning the FMT string the Formatter determines by counting the points 
    (.) which count is being specified.  For example, when the FMT string 
    contains 3...7, then CNT(0)=3 and CNT(3)=7. 
    A count may be expressed as an integer or may include the following codes: 
        #    Variable reference. 
        :    CNT expression. 
        N    Supplies data for CNT field. 
    For more information, type HELP (HOSTLIB) COUNT_EXPRESSIONS. 
    Note:  Often a count value specifies the number of times to perform a 
    function such as the number of times to insert a space; in such cases 
    CNT(n)=0 is the same as CNT(n)=1.  Count values can also specify format 
    characteristics such as the width of a field; in such cases CNT(n)=0 may 
    have a special meaning. 
    Flags    are specified by single characters -- either alphabetic or 
    special symbol characters.  The following list summarizes the flags 
    available: 
        &    Check field width. 
        *    Insert stars on overflow. 
        +    Produce signed number. 
        <    Delete leading blanks. 
        >    Delete trailing blanks. 
        @    Access data in FEP mode. 
        K    Use CNT(1) as data. 
        L    Left justify in field. 
        M    Keep most significant digits (characters). 
        Z    Produce leading zeros. 
        |    Toggle FDS.DEBUG. 
    For more information on flags, type HELP (HOSTLIB) FMT_FLAGS.  If 
    appropriate, several flags may precede the insertion code.  For instance, 
    to request insertion of leading zeros for numeric data the flag Z can be 
    used and, to include a sign character, the flag + can be used.  In 
    combination with the insertion character D, these flags could be specified 
    as %+ZD or as %Z+D with identical results. 
i    specifies an insertion code that identifies the format function to 
perform.  Insertion codes include these types:  numeric, character, and 
miscellaneous.  The following table summarizes these formatting functions. 
Miscellaneous Functions 
  Sequence-of-Operation Functions 
    (   Begin repeat group. 
    )   End repeat group (with DO UNTIL option). 
    [   Begin If-Elseif-Endif group. 
    ?   Elseif group. 
    ]   Endif group. 
    C   Subroutine. 
    =   Assign value to variable. 
    E   Call edit routine. 
    Q   Quit processing format. 
  Input Positioning Functions 
    P   Position Data Pointer. 
    S   Skip n bytes plus m bits of data. 
    ^   Set rescan point. 
  Output Positioning Functions 
    !   Skip to top of form. 
    -   Tab to column n. 
    /   Print n lines. 
    R   Set wrap point. 
    V   Set VFC character. 
    X   Insert space n times, or backspace. 
    \   Continuation function. 
  Special Output Functions 
    F   Use special format: descriptor, pointer, DCB information. 
    J   Convert standard error code. 
    U   Convert UTS to time and date. 
    %   Put % in buffer. 
Numeric Functions 
    B   Convert to binary. 
    D   Convert to decimal. 
    H   Convert to hexadecimal. 
    O   Convert to octal. 
    Y   Convert to hexadecimal in 8 of 9 format. 
Character Functions 
    A   Move a TEXT string. 
    T   Move a TEXTC string. 
For further description of insertion codes, type one of the following: 
HELP (HOSTLIB) MISC_INSERT_CODE 
HELP (HOSTLIB) CHAR_INSERT_CODE 
HELP (HOSTLIB) NUM_INSERT_CODE 
The numeric insertion codes cause data to be obtained, converted to a text 
string and placed in the output buffer.  CNT(0) specifies the width of the 
field in the output buffer.  CNT(0)=0 means a variable width field (i.e. the 
field will be wide enough to contain the text string).  CNT(1) specifies the 
number of bits of data to be obtained.  If CNT(1) is larger than 36, then 36 
bits of data are obtained.  If CNT(1) is zero, then 36 bits or the remainder 
of the current data vector, whichever is smaller, are obtained. 
Examples: 
DATA         FORMAT          RESULTS 
100          %D              100 
100          %5D             bb100 
100          %5ZD            00100 
100          %5LD            100bb 
'777'O       %H              1FF 
'777'O       %Y              FF 
'777063'O    %Y              FF33 
-100         %D              68719476636 
-100         %+D             -100 
-100         %5+D            b-100 
-100         %5+LD           -100b 
-100         %5+ZD           -0100 
In formatting numeric data, bits are obtained beginning at the current data 
pointer.  For character data, the data pointer is first aligned to the next 
character boundary. 
00002
For a description of each flag, type: 
HELP (HOSTLIB) FMT_FLAGS flag 
where flag is one of the following:  AND or CHECK_FIELD_WIDTH (for &), * (for 
Stars on Overflow), PLUS or SIGNED (for +), DELETE_LEAD_BLANKS or LESS_THAN 
(for <), DELETE_TRAIL_BLANKS or GREATER_THAN (for >), @ (for FEP Mode), K (for 
CNT(1) as data), L (for Left Justify), M (form Most Significant Digits), Z 
(for Leading Zeroes), DEBUG_TOGGLE or OR_BAR (for |). 
  Flag         Meaning 
  & 
               Check field width.  If the field to be inserted will not fit on 
               the current line, then print the current line and start a new 
               one.  Otherwise, the line will be wrapped in the middle of the 
               field. 
  * 
               Insert stars on overflow.  If a numeric value exceeds the 
               specified field width, then insert stars instead of the 
               truncated value. 
  + 
               Produce signed number.  This flag is significant only for 
               numeric insertion codes.  If this flag is set, then the data 
               obtained is interpreted as a signed number.  If it is negative, 
               it will be preceded by a '-' in the field.  If this flag is not 
               set, then the data obtained is interpreted as positive. 
  < 
               Delete leading blanks.  If this flag is set, then leading 
               blanks are deleted from the string before it is put in the 
               output buffer. 
  > 
               Delete trailing blanks.  If this flag is set, then trailing 
               blanks are deleted from the string before it is put in the 
               output buffer.  For the '-' format, this flag means never tab 
               backwards. 
  @ 
               Format in FEP mode.  The data accessed through the data vector 
               is assumed to be sparse FEP data with a slack bit at the top of 
               each byte.  For the S and P insertion codes this will cause the 
               specified bit values to be multiplied by 9/8.  For numeric 
               insertion codes or the N code, the slack bits will be 
               compressed out.  The number of bits specified should not 
               include slack bits.  Affects the operation of the N code if it 
               precedes the N. 
               Note that the position of the slack bits depends on their 
               offset from the beginning of the data vector, not from the 
               current position in the data vector. 
  K 
               Use CNT(1) as data flag.  For functions where the size of data 
               to be displayed is normally obtained from CNT(1), the actual 
               data to be displayed is obtained from CNT(1) instead.  This 
               includes all the numeric codes, the J-code, the U-code, and the 
               A-code, but not the T-code. 
  L 
               Left justify in field.  If this flag is set and the string is 
               smaller than the fixed width field, then the field will be 
               filled on the right with blanks.  If this flag is not set, then 
               the field will be filled on the left with blanks. 
  M 
               Keep most significant digits (characters).  If this flag is set 
               and the string size exceeds the size of a fixed width field, 
               then the leftmost characters of the string are put into the 
               field.  If this flag is not set, the rightmost characters are 
               put in the field. 
  Z 
               Produce leading zeroes.  This flag is significant only for 
               numeric insertion codes.  If this flag is set and a number is 
               put in a fixed width field, then leading zeroes will be put in 
               the buffer instead of leading blanks. 
  | 
               Toggle F_FDS.DEBUG.  When F_FDS.DEBUG is set, the Formatter 
               traces a number of useful events while processing the format. 
               Entries and returns from different auto levels (e.g. (, [, ?, 
               and C functions) are displayed.  The value of CNT(1) for 
               [-functions is displayed.  Variable assignments and functions 
               which produce output are displayed.  Each access through the 
               data vector is displayed. 
00002
00006
00001
00001
00001
00011
00004
00005
00006
00005
00007
00008
00010
00008
00004
00009
00011
00003
00003
00011
00010
FMT
For a description of each parameter, type: 
HELP (HOSTLIB) F_FDS param 
where param is one of the following:  BUF, BUFSIZE, BUFX, CUR$, DCB, DVFC, 
EDIT, FIELDX, FMT, FMTSIZE, FMTX, FWID, MEMSZ, NVECS, OUTPUT, TABDFLT, TRUNC, 
VECTR, WRAP, or WRAPTAB. 
    BUF = VARIABLE    locates the area to be used as the output buffer.  The 
    default is NIL and may not be used.  Upon return the buffer will contain 
    the last line formatted.  The size of the BUF variable determines the 
    point at which lines are wrapped.  The first character is used for a VFC 
    character. 
    BUFSIZE - VALUE-DEC (0-?)    is used by the formatter to contain the size 
    of the output buffer in characters (SIZEC(BUF)). 
    BUFX - VALUE-SBIN    on return, contains the current index into the output 
    buffer (size of the last line formatted). 
    CUR$ - PTR    on return, locates the next data item that will be accessed. 
    DCB = DCBNAME    specifies the DCB through which output is written.  The 
    default is NIL.  If DCB is NIL then the formatted lines are not written. 
    DEBUG = VALUE-BIT(1)    set for debug mode.  See the | insertion code 
    which toggles this flag. 
DVFC = VALUE-CHAR(1)    specifies the VFC character to be used for all lines 
    that do not have a %V insertion code.  Specifying DVFC=* means to write 
    with no VFC.  The default is BITASC('101'O) meaning 'space 1 after print'. 
    EDIT = {ENTRY|NIL}    specifies the routine to call when a %E insertion 
    code is found.  For more information see the description of the %E 
    insertion code. 
    FIELDX - VALUE-SBIN    on return, contains the index of the last field in 
    the output buffer. 
    FMT = VARIABLE    locates the area containing the format string associated 
    with the FDS.  FMT_ contains two fields:  BOUND and FMT$.  BOUND specifies 
    the size of the string.  FMT$ is a pointer to the start of the string. 
    The parameter FMT must be specified.  For more information, type: 
    HELP (HOSTLIB) FMT 
    FMTSIZE - VALUE-SBIN    on return, contains the number in characters in 
    the FMT string. 
    FMTX - VALUE-SBIN    on return, contains an index to the next character of 
    the FMT string. 
    FWID - VALUE-SBIN    on return, contains the width of the last field in 
    the output buffer. 
    MEMSZ - VALUE-SBIN    on return, contains the number of bits remaining in 
    the current data vector. 
    NVECS = VALUE-DEC(0-?)    number of data vectors.  Default is 0. 
    OUTPUT = {ENTRY|NIL}    specifies the routine to call when records are 
    output.  This routine is called before the record is written through DCB 
    with FPT_WRITE.BUF_ and F_FDS as arguments.  Default is NIL. 
TABDFLT = VALUE-DEC(0-?)    when a '-' insertion code is encountered with 
    CNT(0)=0, the buffer pointer will be incremented to the next multiple of 
    TABDFLT plus one.  The default value for TABDFLT is 10 (i.e., tabs at 11, 
    21, 31,...). 
    TRUNC = {YES|NO}    specifies, if YES, that output is truncated at the 
    buffer size.  If NO then when the end of the output buffer is encountered, 
    the output is wrapped.  The default is YES. 
    USERDATn = VALUE-SBIN    where n= 1, 2, or 3 for each of three parameters, 
    supplies context information for the FMT string via the # function in a 
    CNT expression.  USERDAT1# can be referenced as 127#, USERDAT2# as 128#, 
    and USERDAT3# as 129#, since they are located starting at word 27 of the 
    F_FDS structure. 
    VECTR = VARIABLE    locates the array (NVECS long) of data vectors. 
    Default is NIL. 
    WRAP - VALUE-BIT(1)    on return, is set if the formatting operation 
    resulted in one or more lines being wrapped. 
    WRAPTAB = VALUE-DEC(0-?)    specifies column to tab to when wrapping a 
    line.  The default is column 1. 
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
A 
  ABORT -   
    XUG_INIT - 
      HELP XUG_INIT ABORT 
  ABORT|BRKMSG|CONTINUE -   
    XUR_INIT - 
      HELP XUR_INIT ABORT 
  ABREV -   
    P$LIT - 
      HELP P$LIT ABREV 
  ACCEPT -   
    PARSE$PARAM - 
      HELP PARAM ACCEPT 
  ACCT -   
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST ACCT 
  ACCT_LIST -   
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST ACCT_LIST 
  accuracy, time for XUD services - 
      HELP DATA_TYPES 
  ADAPT -   
    XUG_INIT - 
      HELP XUG_INIT ADAPT 
    XUR_INIT - 
      HELP XUR_INIT ADAPT 
  ADDL_NRECS -   
    XUG_INIT - 
      HELP XUG_INIT ADDL_NRECS 
  ALL -   
    XUH_PARAM - 
      HELP XUH_PARAM ALL 
  ALLOCATE$$ -   
    XUU_PARAM - 
      HELP XUU_PARAM ALLOCATE$$ 
  allocation table - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  alphanumeric stream - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  ALWAYS_SET_PROMPT -   
    XUG_GETCMD - 
      HELP XUG_GETCMD ALWAYS_SET_PROMPT 
    XUG_INIT - 
      HELP XUG_INIT ALWAYS_SET_PROMPT 
  ARS -   
    XUU_PARAM - 
      HELP XUU_PARAM ARS 
  ASCII_KEY -   
    XUU_PARAM - 
      HELP XUU_PARAM ASCII_KEY 
  ASN -   
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST ASN 
B 
  BBUF -   
    XSA_PARAM - 
      HELP XSA_PARAM BBUF 
  BC -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS BC 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS BC 
  BC_UNIT -   
    XUX$PARAM - 
      HELP XUX$PARAM BC_UNIT 
  BLANKONLY -   
    P_PCB - 
      HELP P_PCB BLANKONLY 
  BRKMSG -   
    XUG_INIT - 
      HELP XUG_INIT BRKMSG 
  BUF -   
    F_FDS - 
      HELP F_FDS BUF 
  BUF$ -   
    XUG_GETCMD - 
      HELP XUG_GETCMD BUF$ 
  BUFFER -   
    XUX$PARAM_NO_PARSE - 
      HELP XUX$PARAM_NO_PARSE BUFFER 
  BUFSIZE -   
    F_FDS - 
      HELP F_FDS BUFSIZE 
  BUFX -   
    F_FDS - 
      HELP F_FDS BUFX 
  buf_vec - 
      HELP XUU$READ PARAMETERS: 
  B_ERRORS_C - 
      HELP XUG_INCLUDE_FILES 
      HELP XUR_INCLUDE_FILES 
C 
  C -   
    P_PCB - 
      HELP P_PCB C 
  C.INCL_ERRCODE -   
    XUU_PARAM - 
      HELP XUU_PARAM C.INCL_ERRCODE 
  C.SO_ERRCODE -   
    XUU_PARAM - 
      HELP XUU_PARAM C.SO_ERRCODE 
  CHARPOS -   
    PARSE$PARAM - 
      HELP PARAM CHARPOS 
    XUH_PARAM - 
      HELP XUH_PARAM CHARPOS 
  CMDSZ -   
    XUG_INIT - 
      HELP XUG_INIT CMDSZ 
  CMDVAR -   
    XUE_ECB - 
      HELP XUE_ECB 
  CMD_COMPLETE -   
    XUX$PARAM_NO_PARSE - 
      HELP XUX$PARAM_NO_PARSE CMD_COMPLETE 
  CMD_LEN -   
    XUX$PARAM_NO_PARSE - 
      HELP XUX$PARAM_NO_PARSE CMD_LEN 
  CNTU -   
    P_PCB - 
      HELP P_PCB CNTU 
  CODE -   
    P$NODE - 
      HELP P$NODE CODE 
    PARSE$OUT - 
      HELP OUT$BLK CODE 
    PARSE$PARAM - 
      HELP PARAM CODE 
    PARSE$SYM - 
      HELP OUT$SYM CODE 
    XUE_FUNPARAM - 
      HELP XUE_FUNPARAM 
    XUE_OPTION - 
      HELP XUE_OPTION 
    XUE_VARPARAM - 
      HELP XUE_VARPARAM 
  CODE01 - 
      HELP XSF_INCLUDE_FILES 
  CODE02 - 
      HELP XSF_INCLUDE_FILES 
  CODE03 - 
      HELP XSF_INCLUDE_FILES 
  CODE04 - 
      HELP XSF_INCLUDE_FILES 
  CODE05 - 
      HELP XSF_INCLUDE_FILES 
  CODE06 - 
      HELP XSF_INCLUDE_FILES 
  CODE07 - 
      HELP XSF_INCLUDE_FILES 
  CODE08 - 
      HELP XSF_INCLUDE_FILES 
  CODE09 - 
      HELP XSF_INCLUDE_FILES 
  CODE11 - 
      HELP XSF_INCLUDE_FILES 
  CODE12 - 
      HELP XSF_INCLUDE_FILES 
  CODE13 - 
      HELP XSF_INCLUDE_FILES 
  CODE14 - 
      HELP XSF_INCLUDE_FILES 
  CODE15 - 
      HELP XSF_INCLUDE_FILES 
  CODE16 - 
      HELP XSF_INCLUDE_FILES 
  CODE17 - 
      HELP XSF_INCLUDE_FILES 
  CODE18 - 
      HELP XSF_INCLUDE_FILES 
  CODE19 - 
      HELP XSF_INCLUDE_FILES 
  CODE20 - 
      HELP XSF_INCLUDE_FILES 
  command line options, non-standard - 
      HELP XUX 
      HELP XUX$LEGAL_OPTIONS 
  command line options, standard - 
      HELP XUX 
      HELP XUX$LEGAL_OPTIONS 
      HELP XUX$STD_OPTIONS 
  command variables - 
      HELP X$EVAL DESCRIPTION: 
  command, multi-line (processor invocation) - 
      HELP XUX$GETLINE DESCRIPTION: 
  command, processor invocation - 
      HELP XUX 
  COMMANDS -   
    XUG_INIT - 
      HELP XUG_INIT COMMANDS 
    XUR_INIT - 
      HELP XUR_INIT COMMANDS 
  COMMENT -   
    P_PCB - 
      HELP P_PCB COMMENT 
  +* comment - 
      HELP UPDATE_FILE_FORMAT COMMENT 
  *CONTINUATION_COMMANDS file - 
      HELP XUX$GETLINE DESCRIPTION: 
  CONTINUE -   
    XUG_INIT - 
      HELP XUG_INIT CONTINUE 
  CONTINUED# -   
    XUG_GETCMD - 
      HELP XUG_GETCMD CONTINUED# 
  CONTINUE_OK -   
    XUG_GETCMD - 
      HELP XUG_GETCMD CONTINUE_OK 
  COUNT -   
    P$LIT - 
      HELP P$LIT COUNT 
    P$SYM - 
      HELP P$SYM COUNT 
    PARSE$SYM - 
      HELP OUT$SYM COUNT 
    XUE_OPTION - 
      HELP XUE_OPTION COUNT 
    XUE_VARPARAM - 
      HELP XUE_VARPARAM COUNT 
  CPOS -   
    PARSE$OUT - 
      HELP OUT$BLK CPOS 
    PARSE$SYM - 
      HELP OUT$SYM CPOS 
    XUE_FUNPARAM - 
      HELP XUE_FUNPARAM CPOS 
    XUE_OPTION - 
      HELP XUE_OPTION CPOS 
    XUE_VARPARAM - 
      HELP XUE_VARPARAM CPOS 
  CUR$ -   
    F_FDS - 
      HELP F_FDS CUR$ 
  C_LD -   
    P_PCB - 
      HELP P_PCB C_LD 
  C_TL -   
    P_PCB - 
      HELP P_PCB C_TL 
D 
  Data Types - 
      HELP DATA_TYPES 
  DATA_SIZE -   
    XUD_PARAM - 
      HELP XUD_PARAM DATA_SIZE 
  DATE - 
      HELP DATA_TYPES 
  Date and Time Examples: - 
      HELP DATE_TIME_EXAMPLES 
  Date and Time Pictures - 
      HELP DATE_TIME_PICTURE 
  DCB -   
    F_FDS - 
      HELP F_FDS DCB 
  DCB# -   
    XUU_PARAM - 
      HELP XUU_PARAM DCB# 
  DCB1 -   
    XUX$PARAM - 
      HELP XUX$PARAM DCB1 
  DCB2 -   
    XUX$PARAM - 
      HELP XUX$PARAM DCB2 
  DCB2_PARAM -   
    XUG_GETCMD - 
      HELP XUG_GETCMD DCB2_PARAM 
  DCB_LS -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS DCB_LS 
  DCB_OU -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS DCB_OU 
  DCB_PARAM -   
    XUG_GETCMD - 
      HELP XUG_GETCMD DCB_PARAM 
  DCB_UI -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS DCB_UI 
  DEBUG -   
    F_FDS - 
      HELP F_FDS DEBUG 
  Debug names, Object file - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  debug record types 22 to 15 - 
      HELP XUO$OUINIT INPUT: 
  DISP -   
    XUG_GETCMD - 
      HELP XUG_GETCMD DISP 
  DISP_ONLY -   
    XUX$PARAM_NO_PARSE - 
      HELP XUX$PARAM_NO_PARSE DISP_ONLY 
  DLIM -   
    P$DSTR - 
      HELP P$DSTR DLIM 
  DMAP -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS DMAP 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS DMAP 
  DONT_REREAD_CCBUF -   
    XUG_INIT - 
      HELP XUG_INIT DONT_REREAD_CCBUF 
  DONT_REREAD_CCBUFF -   
    XUR_INIT - 
      HELP XUR_INIT DONT_REREAD_CCBUF 
  DONT_STRIP_PROMPT -   
    XUG_INIT - 
      HELP XUG_INIT DONT_STRIP_PROMPT 
    XUR_INIT - 
      HELP XUR_INIT DONT_STRIP_PROMPT 
  Drawing Conventions - 
      HELP NOTATION VERTICAL_ELLIPSIS 
  DVFC -   
    F_FDS - 
      HELP F_FDS DVFC 
  DYNAMIC -   
    P_PCB - 
      HELP P_PCB DYNAMIC 
E 
  ECHO -   
    XUG_GETCMD - 
      HELP XUG_GETCMD ECHO 
    XUG_INIT - 
      HELP XUG_INIT ECHO 
    XUR_INIT - 
      HELP XUR_INIT ECHO 
  EDIT -   
    F_FDS - 
      HELP F_FDS EDIT 
  +END - 
      HELP UPDATE_FILE_FORMAT END_OF_UPDATES 
  ENTDEF - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  ENTREF - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  EOMCHAR# -   
    XUG_GETCMD - 
      HELP XUG_GETCMD EOMCHAR# 
  EPOS -   
    XUG_GETCMD - 
      HELP XUG_GETCMD EPOS 
  ERR -   
    XUD_PARAM - 
      HELP XUD_PARAM ERR 
    XUE_ECB - 
      HELP XUE_ECB ERR 
    XUE_FUNPARAM - 
      HELP XUE_FUNPARAM ERR 
    XUE_VARPARAM - 
      HELP XUE_VARPARAM ERR 
    XUH_PARAM - 
      HELP XUH_PARAM 
  ERR# -   
    XUG_GETCMD - 
      HELP XUG_GETCMD ERR# 
  ERRCODE -   
    XUU_PARAM - 
      HELP XUU_PARAM ERRCODE 
  ERRDCB -   
    XUG_GETCMD - 
      HELP XUG_GETCMD ERRDCB 
    XUH_PARAM - 
      HELP XUH_PARAM ERRDCB 
  ERRMFID -   
    XUG_GETCMD - 
      HELP XUG_GETCMD ERRMFID 
  ERRMSG_VFC -   
    XUG_GETCMD - 
      HELP XUG_GETCMD ERRMSG_VFC 
  ERROR -   
    P_PCB - 
      HELP P_PCB ERROR 
  ERROR# -   
    XUX$PARAM - 
      HELP XUX$PARAM ERROR# 
  ERROR_CODE -   
    XUX$PARAM - 
      HELP XUX$PARAM ERROR_CODE 
    XUX$PARAM_NO_PARSE - 
      HELP XUX$PARAM_NO_PARSE ERROR_CODE 
  ERROR_PROC$$ -   
    XUU_PARAM - 
      HELP XUU_PARAM ERROR_PROC$$ 
  ERROR_PROC$$ - 
      HELP XUU$READ ERROR_CONDITIONS: 
  ERR_CODE -   
    XUG_GETCMD - 
      HELP XUG_GETCMD ERR_CODE 
  ERR_DCB -   
    XUE_ECB - 
      HELP XUE_ECB ERR_DCB 
    XUE_FUNPARAM - 
      HELP XUE_FUNPARAM ERR_DCB 
    XUE_VARPARAM - 
      HELP XUE_VARPARAM ERR_DCB 
  ERR_POS -   
    XUE_ECB - 
      HELP XUE_ECB ERR_POS 
    XUE_FUNPARAM - 
      HELP XUE_FUNPARAM ERR_POS 
    XUE_VARPARAM - 
      HELP XUE_VARPARAM ERR_POS 
  Executable Statement Debug Record (Record Type TYPEXST) - 
      HELP XUO$EXST DESCRIPTION: 
      HELP XUO$EXSTNUM DESCRIPTION: 
  Expression Evaluation - 
      HELP EXPRESSION_EVALUATION 
  External Data Definition Record (Record Type TYPSDEF) - 
      HELP XUO$SDEF DESCRIPTION: 
      HELP XUO$SDEF_CONST DESCRIPTION: 
  External Data Reference Record (Record Type TYPSREF) - 
      HELP XUO$SREF DESCRIPTION: 
  External Procedure Definition (Record Type TYPEDEF) - 
      HELP XUO$EDEF DESCRIPTION: 
  External Procedure Reference (Record Type TYPEREF) - 
      HELP XUO$EREF DESCRIPTION: 
  External Segment Definition (Record Type TYPSEGDEF) - 
      HELP XUO$SEGDEF DESCRIPTION: 
  External Segment Definition Record (Record Type TYPSEGDEF) - 
      HELP XUO$SEGDEF_CONST DESCRIPTION: 
  External Segment Reference Record (Record Type TYPSEGREF) - 
      HELP XUO$SEGREF DESCRIPTION: 
  Externally defined names - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  Externally Defined Names (Record Type TYPDNAM) - 
      HELP XUO$DNAME DESCRIPTION: 
  Externally referenced names - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  Externally Referenced Names Record (Record Type TYPRNAM) - 
      HELP XUO$RNAME DESCRIPTION: 
F 
  F1 -   
    XUG_GETCMD - 
      HELP XUG_GETCMD F1 
  F2 -   
    XUG_GETCMD - 
      HELP XUG_GETCMD F2 
  F3 -   
    XUG_GETCMD - 
      HELP XUG_GETCMD F3 
  Fast Sequential File Access Services (XSA) - 
      HELP CHANGES 
  FID_ONLY -   
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST FID_ONLY 
  FIELDX -   
    F_FDS - 
      HELP F_FDS FIELDX 
  FITALTKEYS - 
      HELP XSF_INCLUDE_FILES 
  FLAGS.BAD_UPDATE# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.BAD_UPDATE# 
  FLAGS.BASE# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.BASE# 
  FLAGS.BLANK_FILL -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.BLANK_FILL 
  FLAGS.CLOSE_ALL# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.CLOSE_ALL# 
  FLAGS.FAST_BASE# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.FAST_BASE# 
  FLAGS.FAST_INCLUDE# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.FAST_INCLUDE# 
  FLAGS.FAST_UPDATE# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.FAST_UPDATE# 
  FLAGS.INCLUDE# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.INCLUDE# 
  FLAGS.KEY_REC# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.KEY_REC# 
  FLAGS.LU_FIRST# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.LU_FIRST# 
  FLAGS.LU_WHILE# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.LU_WHILE# 
  FLAGS.OPT_UI# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.OPT_UI# 
  FLAGS.SOURCE_OUT# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.SOURCE_OUT# 
  FLAGS.SO_ERR# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.SO_ERR# 
  FLAGS.UP_DATE# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.UP_DATE# 
  FLAGS.XUU_ERR# -   
    XUU_PARAM - 
      HELP XUU_PARAM FLAGS.XUU_ERR# 
  FLGLEV -   
    XUG_GETCMD - 
      HELP XUG_GETCMD FLGLEV 
  FM$FIT - 
      HELP XSF_INCLUDE_FILES 
  FMT -   
    F_FDS - 
      HELP F_FDS FMT 
  FMTSIZE -   
    F_FDS - 
      HELP F_FDS FMTSIZE 
  FMTX -   
    F_FDS - 
      HELP F_FDS FMTX 
  FM_FITCODE - 
      HELP XSF_INCLUDE_FILES 
  Format of the Update File - 
      HELP UPDATE_FILE_FORMAT 
  Formatter -   
    % character in buffer - 
      HELP MISC_INSERT_CODE PERCENT 
    Assign value to variable - = function - 
      HELP MISC_INSERT_CODE EQUALS 
    Backspace - X function - 
      HELP MISC_INSERT_CODE X 
    Binary, convert to - B function - 
      HELP NUM_INSERT_CODE B 
    Check field width - & flag - 
      HELP FMT_FLAGS CHECK_FLD_WIDTH 
    Continuation - / function - 
      HELP MISC_INSERT_CODE CONTINUATION 
    Convert standard error code - J function - 
      HELP MISC_INSERT_CODE J 
    DCB number format - see F function - 
      HELP MISC_INSERT_CODE F 
    Decimal, convert to - D function - 
      HELP NUM_INSERT_CODE D 
    Delete leading blanks - < flag - 
      HELP FMT_FLAGS DELETE_LEAD_BLANKS 
    Delete trailing blanks - > flag - 
      HELP FMT_FLAGS DELETE_TRAIL_BLANKS 
    Descriptor format - see F function - 
      HELP MISC_INSERT_CODE F 
    DO UNTIL - ) function with CNT(0) - 
      HELP MISC_INSERT_CODE REPEAT_GROUP_END 
    Edit routine, call - E function - 
      HELP MISC_INSERT_CODE E 
    Elseif - [?] functions - 
      HELP MISC_INSERT_CODE ELSEIF 
    Endif group - ] function - 
      HELP MISC_INSERT_CODE ENDIF 
    Error code convert - J function - 
      HELP MISC_INSERT_CODE J 
    FEP mode flag - @ flag - 
      HELP FMT_FLAGS @ 
    Hexadecimal in 8 of 9 format, convert to - Y function - 
      HELP NUM_INSERT_CODE Y 
    Hexadecimal, convert to - H function - 
      HELP NUM_INSERT_CODE H 
    If-Elseif-Endif group (begin) - [ function - 
      HELP MISC_INSERT_CODE IF 
    Insert space n times - X function - 
      HELP MISC_INSERT_CODE X 
    Insert stars on overflow - * flag - 
      HELP FMT_FLAGS * 
    Leading zeros - Z flag - 
      HELP FMT_FLAGS Z 
    Left justify in field - L flag - 
      HELP FMT_FLAGS L 
    Line wrap - R function - 
      HELP MISC_INSERT_CODE R 
    Most significant digits - M flag - 
      HELP FMT_FLAGS M 
    Move a TEXT string - A function - 
      HELP CHAR_INSERT_CODE A 
    Octal, convert to - O function - 
      HELP NUM_INSERT_CODE O 
    operators in CNT expressions - 
      HELP COUNT_EXPRESSIONS : 
    Pointer format - see F function - 
      HELP MISC_INSERT_CODE F 
    Position data pointer - P function - 
      HELP MISC_INSERT_CODE P 
    Print n lines - \ code - 
      HELP MISC_INSERT_CODE PRINT_N_LINES 
    Quit processing format - Q function - 
      HELP MISC_INSERT_CODE Q 
    Repeat group (begin) - ( function - 
      HELP MISC_INSERT_CODE REPEAT_GROUP_BEGIN 
    Repeat group (end) - ) function - 
      HELP MISC_INSERT_CODE REPEAT_GROUP_END 
    Set rescan point - N function - 
      HELP MISC_INSERT_CODE CARET 
    Set VFC character - V function - 
      HELP MISC_INSERT_CODE V 
    Set wrap point - R function - 
      HELP MISC_INSERT_CODE R 
    Signed number - + flag - 
      HELP FMT_FLAGS PLUS 
    Skip n bytes of data plus m bits of data - S function - 
      HELP MISC_INSERT_CODE S 
    Special formats - F function - 
      HELP MISC_INSERT_CODE F 
    Subroutine - C function - 
      HELP MISC_INSERT_CODE C 
    Supply data for CNT - N count expression - 
      HELP COUNT_EXPRESSIONS O 
    Tab to column n - dash code - 
      HELP MISC_INSERT_CODE TAB 
    TEXTC string, move - T function - 
      HELP CHAR_INSERT_CODE T 
    Time and date, convert from UTS - U function - 
      HELP MISC_INSERT_CODE U 
    Toggle F_FDS.DEBUG - | flag - 
      HELP FMT_FLAGS DEBUG_TOGGLE 
    Top of form - ! function - 
      HELP MISC_INSERT_CODE TOF 
    Use CNT(1) as data - K flag - 
      HELP FMT_FLAGS K 
    UTS to time and date - U function - 
      HELP MISC_INSERT_CODE U 
    Variable reference - # count expression - 
      HELP COUNT_EXPRESSIONS # 
    VFC character - V function - 
      HELP MISC_INSERT_CODE V 
  Formatter count expression -   
    # - Variable reference - 
      HELP COUNT_EXPRESSIONS # 
    : - operators in CNT expressions - 
      HELP COUNT_EXPRESSIONS : 
    N - Supply data for CNT - 
      HELP COUNT_EXPRESSIONS O 
  Formatter flag -   
    & - Check field width - 
      HELP FMT_FLAGS CHECK_FLD_WIDTH 
    * - Insert stars on overflow - 
      HELP FMT_FLAGS * 
    + - Signed number - 
      HELP FMT_FLAGS PLUS 
    < - Delete leading blanks - 
      HELP FMT_FLAGS DELETE_LEAD_BLANKS 
    > - Delete trailing blanks - 
      HELP FMT_FLAGS DELETE_TRAIL_BLANKS 
    @ - FEP mode flag - 
      HELP FMT_FLAGS @ 
    K - Use CNT(1) as data - 
      HELP FMT_FLAGS K 
    L - Left justify in field - 
      HELP FMT_FLAGS L 
    M - Most significant digits - 
      HELP FMT_FLAGS M 
    Z - Leading zeros - 
      HELP FMT_FLAGS Z 
    | - Toggle F_FDS.DEBUG - 
      HELP FMT_FLAGS DEBUG_TOGGLE 
  Formatter function -   
    \ - Print n lines - 
      HELP MISC_INSERT_CODE PRINT_N_LINES 
    ! - Top of Form - 
      HELP MISC_INSERT_CODE TOF 
    % character in buffer - 
      HELP MISC_INSERT_CODE PERCENT 
    ( - Repeat group (begin) - 
      HELP MISC_INSERT_CODE REPEAT_GROUP_BEGIN 
    ) - Repeat group (end) with DO UNTIL option - 
      HELP MISC_INSERT_CODE REPEAT_GROUP_END 
    - (dash) - Tab to column n - 
      HELP MISC_INSERT_CODE TAB 
    / - Continuation - 
      HELP MISC_INSERT_CODE CONTINUATION 
    = - Assign value to variable - 
      HELP MISC_INSERT_CODE EQUALS 
    ? - Elseif function - 
      HELP MISC_INSERT_CODE ELSEIF 
    A - Move a TEXT string - 
      HELP CHAR_INSERT_CODE A 
    B - Binary, convert to - 
      HELP NUM_INSERT_CODE B 
    C - Subroutine function - 
      HELP MISC_INSERT_CODE C 
    D - Decimal, convert to - 
      HELP NUM_INSERT_CODE D 
    E - Edit routine, call - 
      HELP MISC_INSERT_CODE E 
    F - Special formats (Descriptor, Pointer, DCB number) - 
      HELP MISC_INSERT_CODE F 
    H - Hexadecimal, convert to - 
      HELP NUM_INSERT_CODE H 
    J - Error code convert - 
      HELP MISC_INSERT_CODE J 
    N - Set rescan point - 
      HELP MISC_INSERT_CODE CARET 
    O - Octal, convert to - 
      HELP NUM_INSERT_CODE O 
    P - Position data pointer - 
      HELP MISC_INSERT_CODE P 
    Q - Quit processing format - 
      HELP MISC_INSERT_CODE Q 
    R - Set wrap point - 
      HELP MISC_INSERT_CODE R 
    S - Skip n bytes of data plus m bits of data - 
      HELP MISC_INSERT_CODE S 
    T - TEXTC string, move - 
      HELP CHAR_INSERT_CODE T 
    U - UTS to time and date convert - 
      HELP MISC_INSERT_CODE U 
    V - Set VFC character - 
      HELP MISC_INSERT_CODE V 
    X - Insert space n times or Backspace - 
      HELP MISC_INSERT_CODE X 
    Y - Hexadecimal in 8 of 9 format, convert to - 
      HELP NUM_INSERT_CODE Y 
    [ - If-Elseif-Endif group (begin) function - 
      HELP MISC_INSERT_CODE IF 
    ] - Endif function - 
      HELP MISC_INSERT_CODE ENDIF 
  Formatting Codes - 
      HELP FMT 
  Forward References, XUO - 
      HELP XUO$FRWD_REF DESCRIPTION: 
  FPL status variable - 
      HELP XUO$VREBL_CONT_SET DESCRIPTION: 
  FPT$ -   
    XUG_GETCMD - 
      HELP XUG_GETCMD FPT$ 
  fpt_close - 
      HELP XSA$CLOSE PARAMETERS: 
  fpt_open - 
      HELP XSA$OPEN PARAMETERS: 
  fpt_pfil - 
      HELP XSA$PFIL PARAMETERS: 
  fpt_precord - 
      HELP XSA$PRECORD PARAMETERS: 
  fpt_read - 
      HELP XSA$READ PARAMETERS: 
  fpt_write - 
      HELP XSA$WRITE PARAMETERS: 
  FUN -   
    XUE_ECB - 
      HELP XUE_ECB FUN 
  FWID -   
    F_FDS - 
      HELP F_FDS FWID 
  F_F -   
    P$NODE - 
      HELP P$NODE F_F 
  F_FDS - 
      HELP F_FDS WRAPTAB 
  F_FDS Structure - 
      HELP F_FDS 
G 
  GLOBAL$ -   
    PARSE$PARAM - 
      HELP PARAM GLOBAL$ 
  GOODCMD -   
    XUG_INIT - 
      HELP XUG_INIT GOODCMD 
    XUR_INIT - 
      HELP XUR_INIT GOODCMD 
H 
  Head Key - 
      HELP XUO$OUINIT DESCRIPTION: 
  Head Record - 
      HELP XUO$HEADSTART DESCRIPTION: 
      HELP XUO$HEAD_SEVERITY DESCRIPTION: 
  Head Record Key - 
      HELP XUO$HEADNAME DESCRIPTION: 
  HEAD record, Object file - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  HELP -   
    XUH_PARAM - 
      HELP XUH_PARAM HELP 
  HELP service for XUH - 
      HELP XUH 
  HINODE$ -   
    P_PCB - 
      HELP P_PCB HINODE$ 
  HI_CHAR -   
    P_PCB - 
      HELP P_PCB HI_CHAR 
I 
  ICHARS -   
    XUE_PPCB - 
      HELP XUE_PPCB 
  INBUF -   
    XUE_PPCB - 
      HELP XUE_PPCB INBUF 
  INDCB -   
    XUG_GETCMD - 
      HELP XUG_GETCMD INDCB 
  INFOMSG -   
    XUG_GETCMD - 
      HELP XUG_GETCMD INFOMSG 
  INHIBIT_DATE -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_DATE 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_DATE 
  INHIBIT_DIRECTORY -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_DIRECTORY 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_DIRECTORY 
  INHIBIT_DO -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_DO 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_DO 
  INHIBIT_END -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_END 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_END 
  INHIBIT_ENTER -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_ENTER 
  INHIBIT_ERASE -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_ERASE 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_ERASE 
  INHIBIT_HELP -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_HELP 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_HELP 
  INHIBIT_NULL -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_NULL 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_NULL 
  INHIBIT_OUTPUT -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_OUTPUT 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_OUTPUT 
  INHIBIT_PRINT -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_PRINT 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_PRINT 
  INHIBIT_QMARK -   
    XUG_INIT - 
      HELP XUG_INIT INHIBIT_QMARK 
    XUR_INIT - 
      HELP XUR_INIT INHIBIT_QMARK 
  INIT_NRECS -   
    XUG_INIT - 
      HELP XUG_INIT INIT_NRECS 
  INIT_PIC -   
    XUD_PARAM - 
      HELP XUD_PARAM INIT_PIC 
  INPUT_DCB -   
    XUE_ECB - 
      HELP XUE_ECB INPUT_DCB 
  Internal entries, Object file - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  Internal Entry Debug Record (Record Type TYPINTNTRY) - 
      HELP XUO$INTNTRY DESCRIPTION: 
  INTO - 
      HELP XUG$OPENOUT USAGE_NOTES: 
J 
  +j,k comment - 
      HELP UPDATE_FILE_FORMAT DELETE_AND_REPLACE 
K 
  KBUF -   
    XSA_PARAM - 
      HELP XSA_PARAM KBUF 
  KEYSCAN -   
    P_PCB - 
      HELP P_PCB KEYSCAN 
  KEYWORD -   
    XUH_PARAM - 
      HELP XUH_PARAM KEYWORD 
  KEYWORDS$ -   
    P$KEYWORDS - 
      HELP P$KEYWORDS KEYWORDS$ 
  KEYWORD_COUNT -   
    P$KEYWORDS - 
      HELP P$KEYWORDS KEYWORD_COUNT 
L 
  LEAD -   
    XUE_ECB - 
      HELP XUE_ECB LEAD 
  LEGAL$ -   
    P$KEYWORDS - 
      HELP P$KEYWORDS LEGAL$ 
  LEGAL_OPTIONS -   
    XUX$PARAM - 
      HELP XUX$PARAM LEGAL_OPTIONS 
  LEVEL -   
    XUU_PARAM - 
      HELP XUU_PARAM LEVEL 
  LEXTYPE -   
    P$DSTR - 
      HELP P$DSTR LEXTYPE 
    P$SYM - 
      HELP P$SYM LEXTYPE 
  LO -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS LO 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS LO 
  Logical Block Debug Record (Record Type TYPLOGBLK) - 
      HELP XUO$LOGBLKALLOC DESCRIPTION: 
      HELP XUO$LOGBLKEXSTINIT DESCRIPTION: 
      HELP XUO$LOGBLKEXSTTERM DESCRIPTION: 
      HELP XUO$LOGBLKNOAUTO DESCRIPTION: 
      HELP XUO$LOGBLKTERM DESCRIPTION: 
      HELP XUO$LOGBLKVREBLINIT DESCRIPTION: 
      HELP XUO$LOGBLKVREBLTERM DESCRIPTION: 
  Logical block, Object file - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  Lookup Routine - 
      HELP XUO$FRWD_REF DESCRIPTION: 
  LS -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS LS 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS LS 
M 
  main program - 
      HELP XUO$HEADSTART DESCRIPTION: 
  MAKEUC -   
    P$SYM - 
      HELP P$SYM MAKEUC 
  MAXL -   
    P$SYM - 
      HELP P$SYM MAXL 
  MAX_SIZE -   
    XUD_PARAM - 
      HELP XUD_PARAM MAX_SIZE 
  MDMAP -   
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS MDMAP 
  MEMSZ -   
    F_FDS - 
      HELP F_FDS MEMSZ 
  MORE -   
    XUH_PARAM - 
      HELP XUH_PARAM MORE 
  MOREMEM -   
    XUG_INIT - 
      HELP XUG_INIT MOREMEM 
  multi-line command (processor invocation) - 
      HELP XUX$GETLINE DESCRIPTION: 
N 
  N# -   
    P_PCB - 
      HELP P_PCB N# 
  NAME -   
    XUH_PARAM - 
      HELP XUH_PARAM NAME 
  NBL -   
    P_PCB - 
      HELP P_PCB NBL 
  NDTYPE -   
    PARSE$OUT - 
      HELP OUT$BLK NDTYPE 
    PARSE$SYM - 
      HELP OUT$SYM NDTYPE 
  NLINES -   
    XUG_GETCMD - 
      HELP XUG_GETCMD NLINES 
  NODE$ -   
    PARSE$PARAM - 
      HELP PARAM NODE$ 
  NODES -   
    XUG_GETCMD - 
      HELP XUG_GETCMD NODES 
  non-constant entry - 
      HELP XUO$SDEF DESCRIPTION: 
      HELP XUO$SEGDEF DESCRIPTION: 
  NOPTS -   
    XUE_FUNPARAM - 
      HELP XUE_FUNPARAM NOPTS 
  NO_DOWNGRADE -   
    XUG_INIT - 
      HELP XUG_INIT NO_DOWNGRADE 
  NSTD -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS NSTD 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS NSTD 
  NSUBLKS -   
    PARSE$OUT - 
      HELP OUT$BLK NSUBLKS 
    PARSE$SYM - 
      HELP OUT$SYM NSUBLKS 
  NSUBNDS -   
    P$NODE - 
      HELP P$NODE NSUBNDS 
  NUM -   
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST NUM 
  NVECS -   
    F_FDS - 
      HELP F_FDS NVECS 
  NX -   
    P_PCB - 
      HELP P_PCB NX 
O 
  O.FPT_PTR$ -   
    XUU_PARAM - 
      HELP XUU_PARAM O.FPT_PTR$ 
  O.INCL_ERRCODE -   
    XUU_PARAM - 
      HELP XUU_PARAM O.INCL_ERRCODE 
  Object Unit Initialization - 
      HELP XUO$OUINIT DESCRIPTION: 
  object unit record type TYPDBGNAM - 
      HELP XUO$DBGNAME DESCRIPTION: 
  object unit record type TYPDNAM - 
      HELP XUO$DNAME DESCRIPTION: 
  object unit record type TYPEDEF - 
      HELP XUO$EDEF DESCRIPTION: 
  object unit record type TYPEREF - 
      HELP XUO$EREF DESCRIPTION: 
  object unit record type TYPEXST - 
      HELP XUO$EXST DESCRIPTION: 
      HELP XUO$EXSTNUM DESCRIPTION: 
  object unit record type TYPINTNTRY - 
      HELP XUO$INTNTRY DESCRIPTION: 
  object unit record type TYPLOGBLK - 
      HELP XUO$LOGBLKALLOC DESCRIPTION: 
      HELP XUO$LOGBLKEXSTINIT DESCRIPTION: 
      HELP XUO$LOGBLKEXSTTERM DESCRIPTION: 
      HELP XUO$LOGBLKNOAUTO DESCRIPTION: 
      HELP XUO$LOGBLKTERM DESCRIPTION: 
      HELP XUO$LOGBLKVREBLINIT DESCRIPTION: 
      HELP XUO$LOGBLKVREBLTERM DESCRIPTION: 
  object unit record type TYPPROG, subtype SUBTYPPROG - 
      HELP XUO$PRGM DESCRIPTION: 
      HELP XUO$PRGM_TEXT DESCRIPTION: 
  object unit record type TYPPROG, subtype SUBTYPREL - 
      HELP XUO$RELOC DESCRIPTION: 
  object unit record type TYPRNAM - 
      HELP XUO$RNAME DESCRIPTION: 
  object unit record type TYPSDEF - 
      HELP XUO$SDEF DESCRIPTION: 
      HELP XUO$SDEF_CONST DESCRIPTION: 
  object unit record type TYPSECT - 
      HELP XUO$SECTBUILD DESCRIPTION: 
      HELP XUO$SECTNAME DESCRIPTION: 
      HELP XUO$SECTSIZE DESCRIPTION: 
  object unit record type TYPSEGDEF - 
      HELP XUO$SEGDEF DESCRIPTION: 
      HELP XUO$SEGDEF_CONST DESCRIPTION: 
  object unit record type TYPSEGREF - 
      HELP XUO$SEGREF DESCRIPTION: 
  object unit record type TYPSREF - 
      HELP XUO$SREF DESCRIPTION: 
  object unit record type TYPVREBL - 
      HELP XUO$VREBL DESCRIPTION: 
      HELP XUO$VREBLNUM DESCRIPTION: 
      HELP XUO$VREBL_CONT DESCRIPTION: 
      HELP XUO$VREBL_CONT_ADJ DESCRIPTION: 
      HELP XUO$VREBL_CONT_ET DESCRIPTION: 
      HELP XUO$VREBL_CONT_SET DESCRIPTION: 
  OCHARS -   
    XUE_PPCB - 
      HELP XUE_PPCB OCHARS 
  ON|TO - 
      HELP XUG$OPENOUT USAGE_NOTES: 
  OPT -   
    P$NODE - 
      HELP P$NODE OPT 
  OPTION -   
    XUE_FUNPARAM - 
      HELP XUE_FUNPARAM OPTION 
  options, processor invocation - 
      HELP XUX 
  OPTUI -   
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS OPTUI 
  OU -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS OU 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS OU 
  OU Key - 
      HELP XUO$OUINIT DESCRIPTION: 
  OUT -   
    XUE_ECB - 
      HELP XUE_ECB OUT 
    XUE_FUNPARAM - 
      HELP XUE_FUNPARAM OUT 
  OUT$ -   
    PARSE$PARAM - 
      HELP PARAM OUT$ 
    P_PCB - 
      HELP P_PCB OUT$ 
    XUG_GETCMD - 
      HELP XUG_GETCMD OUT$ 
  OUT$BLK Structure/PARSE$OUT Macro - 
      HELP OUT$BLK 
  OUT$SYM Structure/PARSE$SYM Macro - 
      HELP OUT$SYM 
  OUTBUF -   
    XUE_PPCB - 
      HELP XUE_PPCB OUTBUF 
  OUTDCB -   
    P_PCB - 
      HELP P_PCB OUTDCB 
    XUG_GETCMD - 
      HELP XUG_GETCMD OUTDCB 
  OUTDCB1 -   
    XUH_PARAM - 
      HELP XUH_PARAM OUTDCB1 
  OUTDCB2 -   
    XUH_PARAM - 
      HELP XUH_PARAM OUTDCB2 
  OUTENT$ -   
    P_PCB - 
      HELP P_PCB OUTENT 
  OUTPUT -   
    F_FDS - 
      HELP F_FDS OUTPUT 
  OVER - 
      HELP XUG$OPENOUT USAGE_NOTES: 
  O_F -   
    P$NODE - 
      HELP P$NODE O_F 
P 
  P$DSTR - 
      HELP P$DSTR TYPE 
  P$DSTR Structure - 
      HELP P$DSTR 
  P$KEYWORDS - 
      HELP P$KEYWORDS LEGAL$ 
  P$KEYWORDS Structure - 
      HELP P$KEYWORDS 
  P$LIT - 
      HELP P$LIT UPRLOWR 
  P$LIT Structure - 
      HELP P$LIT 
  P$NODE - 
      HELP P$NODE TYPE 
  P$NODE Structure - 
      HELP P$NODE 
  P$SYM - 
      HELP P$SYM XTRA 
  P$SYM Structure - 
      HELP P$SYM 
  PARAM Structure/PARSE$PARAM Macro - 
      HELP PARAM 
  PARAMS$ -   
    XUG_INIT - 
      HELP XUG_INIT PARAMS$ 
  PARSE$OUT - 
      HELP OUT$BLK SUBLK$ 
  PARSE$OUT macro for OUT$BLK - 
      HELP OUT$BLK 
  PARSE$PARAM - 
      HELP PARAM WKSZ 
  PARSE$PARAM macro for PARAM - 
      HELP PARAM 
  PARSE$SYM - 
      HELP OUT$SYM TEXTC$ 
  PARSE$SYM macro for OUT$SYM - 
      HELP OUT$SYM 
  Parsing Tools - 
      HELP PARSING_TOOLS 
  parsing, processor invocation command - 
      HELP XUX 
  PARTRGE Structures - 
      HELP PARTRGE_STRUCTURES 
  PASS -   
    XUG_GETCMD - 
      HELP XUG_GETCMD PASS 
    XUG_INIT - 
      HELP XUG_INIT PASS 
    XUR_INIT - 
      HELP XUR_INIT PASS 
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST PASS 
  PCB -   
    XUG_INIT - 
      HELP XUG_INIT PCB 
    XUR_INIT - 
      HELP XUR_INIT PCB 
  PCB$ -   
    PARSE$PARAM - 
      HELP PARAM PCB$ 
    XUG_GETCMD - 
      HELP XUG_GETCMD PCB$ 
  PIC$ -   
    XUD_PARAM - 
      HELP XUD_PARAM PIC$ 
  PIC_SIZE -   
    XUD_PARAM - 
      HELP XUD_PARAM PIC_SIZE 
  PIC_TEXTC -   
    XUD_PARAM - 
      HELP XUD_PARAM PIC_TEXTC 
  PMAP -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS PMAP 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS PMAP 
  POST_EXEC -   
    XUG_INIT - 
      HELP XUG_INIT POST_EXEC 
    XUR_INIT - 
      HELP XUR_INIT POST_EXEC 
  PPCB -   
    XUG_INIT - 
      HELP XUG_INIT PPCB 
    XUR_INIT - 
      HELP XUR_INIT PPCB 
  PP_DCB -   
    XUG_INIT - 
      HELP XUG_INIT PP_DCB 
    XUR_INIT - 
      HELP XUR_INIT PP_DCB 
  PP_FUN -   
    XUG_GETCMD - 
      HELP XUG_GETCMD PP_FUN 
  PP_PROCNAME -   
    XUG_INIT - 
      HELP XUG_INIT PP_PROCNAME 
  PP_ROOT -   
    XUG_INIT - 
      HELP XUG_INIT PP_ROOT 
  PP_ROOT$ -   
    XUG_GETCMD - 
      HELP XUG_GETCMD PP_ROOT$ 
  precision, time for XUD services - 
      HELP DATA_TYPES 
  PREPROCESS -   
    XUG_INIT - 
      HELP XUG_INIT PREPROCESS 
    XUR_INIT - 
      HELP XUR_INIT PREPROCESS 
  PREPROCESSOR -   
    XUG_INIT - 
      HELP XUG_INIT PREPROCESSOR 
    XUR_INIT - 
      HELP XUR_INIT PREPROCESSOR 
  Preprocessor Expressions - 
      HELP PREPROCESSOR_EXPRESSIONS 
  PRE_EXEC -   
    XUG_INIT - 
      HELP XUG_INIT PRE_EXEC 
    XUR_INIT - 
      HELP XUR_INIT PRE_EXEC 
  PRIVATE -   
    XUE_ECB - 
      HELP XUE_ECB PRIVATE 
  PROCACCT -   
    XUE_ECB - 
      HELP XUE_ECB PROCACCT 
    XUH_PARAM - 
      HELP XUH_PARAM PROCACCT 
  PROCACCT_ -   
    XUG_INIT - 
      HELP XUG_INIT PROCACCT_ 
  Procedure Names Debug Record (Record Type TYPDBGNAM) - 
      HELP XUO$DBGNAME DESCRIPTION: 
  processor invocation - 
      HELP XUX 
  PROCNAME -   
    XUE_ECB - 
      HELP XUE_ECB PROCNAME 
    XUH_PARAM - 
      HELP XUH_PARAM PROCNAME 
    XUR_INIT - 
      HELP XUR_INIT PROCNAME 
  PROCNAME_ -   
    XUG_INIT - 
      HELP XUG_INIT PROCNAME_ 
  PROCPASS -   
    XUH_PARAM - 
      HELP XUH_PARAM PROCPASS 
  PROCPSN -   
    XUH_PARAM - 
      HELP XUH_PARAM PROCPSN 
  Program Key - 
      HELP XUO$OUINIT DESCRIPTION: 
  Program Record (Record Type TYPPROG, Subtype SUBTYPPROG) - 
      HELP XUO$PRGM DESCRIPTION: 
      HELP XUO$PRGM_TEXT DESCRIPTION: 
  Program record, Object file - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  PROMPT -   
    XUE_ECB - 
      HELP XUE_ECB PROMPT 
    XUG_GETCMD - 
      HELP XUG_GETCMD PROMPT 
  PROMPT_VFC -   
    XUG_GETCMD - 
      HELP XUG_GETCMD PROMPT_VFC 
  P_F -   
    P$NODE - 
      HELP P$NODE P_F 
  P_PCB - 
      HELP P_PCB WSZ 
  P_PCB Structure - 
      HELP P_PCB 
R 
  R -   
    P_PCB - 
      HELP P_PCB OUTENT 
  RCHARS -   
    XUE_PPCB - 
      HELP XUE_PPCB RCHARS 
  RCVD -   
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST RCVD 
  RCVD_PROMPT# -   
    XUG_GETCMD - 
      HELP XUG_GETCMD RCVD_PROMPT# 
  READR -   
    XUG_GETCMD - 
      HELP XUG_GETCMD READR 
  REJECT -   
    PARSE$PARAM - 
      HELP PARAM REJECT 
  RELEASE$$ -   
    XUU_PARAM - 
      HELP XUU_PARAM RELEASE$$ 
  Relocation Directives Record (Record Type TYPPROG, Subtype SUBTYPREL) - 
      HELP XUO$RELOC DESCRIPTION: 
  Relocation Key - 
      HELP XUO$OUINIT DESCRIPTION: 
  relocation record - 
      HELP XUO$FRWD_REF DESCRIPTION: 
  Relocation record, Object file - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  REQ_PROMPT -   
    XUG_INIT - 
      HELP XUG_INIT REQ_PROMPT 
  RES -   
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST RES 
  RETRY -   
    PARSE$PARAM - 
      HELP PARAM RETRY 
  RE_ASCII_KEY -   
    XUU_PARAM - 
      HELP XUU_PARAM RE_ASCII_KEY 
  RLT$ -   
    XUG_GETCMD - 
      HELP XUG_GETCMD RLT$ 
  ROOT -   
    XUE_PPCB - 
      HELP XUE_PPCB ROOT 
  RPEAT -   
    P$NODE - 
      HELP P$NODE RPEAT 
  RPROMPT -   
    XUG_GETCMD - 
      HELP XUG_GETCMD RPROMPT 
  RTEXT -   
    P$NODE - 
      HELP P$NODE RTEXT 
S 
  SCHEMA -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS SCHEMA 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS SCHEMA 
  schema option - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  SCRITCH -   
    PARSE$OUT - 
      HELP OUT$BLK SCRITCH 
    PARSE$SYM - 
      HELP OUT$SYM SCRITCH 
  section number - 
      HELP XUO$PRGM DESCRIPTION: 
  Section Record (Record Type TYPSECT) - 
      HELP XUO$SECTBUILD DESCRIPTION: 
      HELP XUO$SECTNAME DESCRIPTION: 
      HELP XUO$SECTSIZE DESCRIPTION: 
  Section, Object file - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  SEGDEF - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  segment name - 
      HELP XUO$SEGREF DESCRIPTION: 
  SEGREF - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  SEQ_REC#.BASE# -   
    XUU_PARAM - 
      HELP XUU_PARAM SEQ_REC#.BASE# 
  SEQ_REC#.UP_INCL# -   
    XUU_PARAM - 
      HELP XUU_PARAM SEQ_REC#.UP_INCL# 
  SFROUTINE -   
    XUG_GETCMD - 
      HELP XUG_GETCMD SFROUTINE 
  SIZE -   
    XUD_PARAM - 
      HELP XUD_PARAM SIZE 
  SI_ERRCODE -   
    XUU_PARAM - 
      HELP XUU_PARAM SI_ERRCODE 
  SKBL -   
    P$NODE - 
      HELP P$NODE SKBL 
  SKIP_PREPROCESS -   
    XUG_GETCMD - 
      HELP XUG_GETCMD SKIP_PREPROCESS 
  SN -   
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST SN 
  SO -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS SO 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS SO 
  SPELLING -   
    XUG_INIT - 
      HELP XUG_INIT SPELLING 
    XUR_INIT - 
      HELP XUR_INIT SPELLING 
  SPHANDLE -   
    XUG_INIT - 
      HELP XUG_INIT SPHANDLE 
  SRCH -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS SRCH 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS SRCH 
  SRCH_LIST -   
    XUX$PARAM - 
      HELP XUX$PARAM SRCH_LIST 
  Statement table, Object file - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  STD_OPTIONS -   
    XUX$PARAM - 
      HELP XUX$PARAM STD_OPTIONS 
  SUBLK$ -   
    PARSE$OUT - 
      HELP OUT$BLK SUBLK$ 
  SUBNDS$ -   
    P$NODE - 
      HELP P$NODE SUBNDS$ 
  SYMDEF - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  SYMREF - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  SYNERR_NODES$ -   
    XUG_GETCMD - 
      HELP XUG_GETCMD SYNERR_NODES$ 
  SYNTAX -   
    XUG_INIT - 
      HELP XUG_INIT SYNTAX 
    XUR_INIT - 
      HELP XUR_INIT SYNTAX 
  S_F -   
    P$NODE - 
      HELP P$NODE S_F 
T 
  T -   
    P_PCB - 
      HELP P_PCB T 
  TABDFLT -   
    F_FDS - 
      HELP F_FDS TABDFLT 
  terminate object unit building - 
      HELP XUO$OUTERM DESCRIPTION: 
  TEXT -   
    P$LIT - 
      HELP P$LIT TEXT 
    P$SYM - 
      HELP P$SYM TEXT 
    PARSE$SYM - 
      HELP OUT$SYM TEXT 
    XUE_OPTION - 
      HELP XUE_OPTION TEXT 
    XUE_VARPARAM - 
      HELP XUE_VARPARAM TEXT 
    XUG_GETCMD - 
      HELP XUG_GETCMD TEXT 
  TEXTC -   
    XUD_PARAM - 
      HELP XUD_PARAM TEXTC 
  TEXTC$ -   
    PARSE$SYM - 
      HELP OUT$SYM TEXTC$ 
  three level-0 ENTRY statement - 
      HELP XUO$EDEF DESCRIPTION: 
  TIMESPAN -   
    XUD_PARAM - 
      HELP XUD_PARAM TIMESPAN 
  Timespan Examples: - 
      HELP TIMESPAN_EXAMPLES 
  Timespan Pictures - 
      HELP TIMESPAN_PICTURE 
  TOPICS -   
    XUH_PARAM - 
      HELP XUH_PARAM TOPICS_PARAM 
  TRAIL -   
    XUE_ECB - 
      HELP XUE_ECB TRAIL 
  TREAD -   
    XUG_GETCMD - 
      HELP XUG_GETCMD TREAD 
  TREE -   
    XUE_ECB - 
      HELP XUE_ECB TREE 
  TRUNC -   
    F_FDS - 
      HELP F_FDS TRUNC 
  TYPE -   
    P$DSTR - 
      HELP P$DSTR TYPE 
    P$LIT - 
      HELP P$LIT TYPE 
    P$NODE - 
      HELP P$NODE TYPE 
    P$SYM - 
      HELP P$SYM TYPE 
    PARSE$PARAM - 
      HELP PARAM TYPE 
U 
  U$ -   
    P_PCB - 
      HELP P_PCB U$ 
  UI -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS UI 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS UI 
  UI_ERRCODE -   
    XUU_PARAM - 
      HELP XUU_PARAM UI_ERRCODE 
  UNFAST -   
    XSA_PARAM - 
      HELP XSA_PARAM UNFAST 
  Universal Time Stamp (UTS) - 
      HELP DATA_TYPES 
      HELP XUO$OUINIT INPUT: 
  UPRLOWR -   
    P$LIT - 
      HELP P$LIT UPRLOWR 
  UREF -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS UREF 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS UREF 
  USER -   
    XUE_ECB - 
      HELP XUE_ECB USER 
    XUE_FUNPARAM - 
      HELP XUE_FUNPARAM USER 
    XUE_VARPARAM - 
      HELP XUE_VARPARAM USER 
  USER$ -   
    PARSE$PARAM - 
      HELP PARAM USER$ 
  user-defined functions - 
      HELP X$EVAL DESCRIPTION: 
  USERDATn -   
    F_FDS - 
      HELP F_FDS USERDATn 
  USERPTR -   
    P_PCB - 
      HELP P_PCB USERPTR 
  USER_NODES$ -   
    XUX$PARAM - 
      HELP XUX$PARAM USER_NODES$ 
  USER_ROUTINE -   
    XUX$PARAM - 
      HELP XUX$PARAM USER_ROUTINE 
  USE_EPOS -   
    XUG_GETCMD - 
      HELP XUG_GETCMD USE_EPOS 
  UTIL -   
    XUG_GETCMD - 
      HELP XUG_GETCMD UTIL 
  UTS - 
      HELP DATA_TYPES 
  UTS, Formatter U function to convert to time and date - 
      HELP MISC_INSERT_CODE U 
V 
  VALUE -   
    XUE_VARPARAM - 
      HELP XUE_VARPARAM VALUE 
  VAR -   
    XUE_ECB - 
      HELP XUE_ECB VAR 
  Variable Debug Record (Record Type TYPVREBL) - 
      HELP XUO$VREBL DESCRIPTION: 
  Variable Debug Record Continuation (Record Type TYPVREBL) - 
      HELP XUO$VREBL_CONT DESCRIPTION: 
      HELP XUO$VREBL_CONT_ADJ DESCRIPTION: 
      HELP XUO$VREBL_CONT_ET DESCRIPTION: 
      HELP XUO$VREBL_CONT_SET DESCRIPTION: 
  Variable Debug Records (Record Type TYPVREBL) - 
      HELP XUO$VREBLNUM DESCRIPTION: 
  Variable table, Object file - 
      HELP OBJECT_UNIT_SPECIFICATIONS 
  VECTR -   
    F_FDS - 
      HELP F_FDS VECTR 
  VERSION_CODE -   
    P_PCB - 
      HELP P_PCB VERSION_CODE 
  VFC -   
    XUH_PARAM - 
      HELP XUH_PARAM VFC 
W 
  W -   
    P_PCB - 
      HELP P_PCB W 
  WARN -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS WARN 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS WARN 
  WKSZ -   
    PARSE$PARAM - 
      HELP PARAM WKSZ 
    XUE_ECB - 
      HELP XUE_ECB WKSZ 
  WK_USED -   
    P_PCB - 
      HELP P_PCB WK_USED 
  WORK -   
    XUE_ECB - 
      HELP XUE_ECB WORK 
    XUG_INIT - 
      HELP XUG_INIT WORK 
    XUR_INIT - 
      HELP XUR_INIT WORK 
  WORK_DCB -   
    XUE_ECB - 
      HELP XUE_ECB WORK_DCB 
  WRAP -   
    F_FDS - 
      HELP F_FDS WRAP 
  WRAPTAB -   
    F_FDS - 
      HELP F_FDS WRAPTAB 
  WSEG -   
    XUG_INIT - 
      HELP XUG_INIT WSEG 
  WSN -   
    XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST WSN 
  WSZ -   
    P_PCB - 
      HELP P_PCB WSZ 
X 
  X$DEC_CONVERT - 
      HELP XUE X$DEC_CONVERT 
  X$DEC_CONVERT Service - 
      HELP X$DEC_CONVERT 
  X$EVAL - 
      HELP XUE X$EVAL 
  X$EVAL Service - 
      HELP X$EVAL 
  X$FORMAT Service - 
      HELP X$FORMAT 
  X$GET_VAR - 
      HELP XUE X$GET_VAR 
  X$GET_VAR Service - 
      HELP X$GET_VAR 
  X$HELP Service - 
      HELP X$HELP 
  X$PARSE Service - 
      HELP X$PARSE 
  X$PRE_PROCESS - 
      HELP XUE X$PRE_PROCESS 
  X$PRE_PROCESS Service - 
      HELP X$PRE_PROCESS 
  X$PUT_VAR - 
      HELP XUE X$PUT_VAR 
  X$PUT_VAR Service - 
      HELP X$PUT_VAR 
  X$STRIP_BLANKS - 
      HELP XUE X$STRIP_BLANKS 
  X$STRIP_BLANKS Service - 
      HELP X$STRIP_BLANKS 
  X$WILDCMP Service - 
      HELP X$WILDCMP 
  X$WILDFMT Service - 
      HELP X$WILDFMT 
  X$WRITE Service - 
      HELP X$WRITE 
  XREF -   
    XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS XREF 
    XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS XREF 
  XSA Services - 
      HELP XSA 
  XSA$CLOSE Service - 
      HELP XSA$CLOSE 
  XSA$OPEN Service - 
      HELP XSA$OPEN 
  XSA$PFIL Service - 
      HELP XSA$PFIL 
  XSA$PRECORD Service - 
      HELP XSA$PRECORD 
  XSA$READ Service - 
      HELP XSA$READ 
  XSA$WRITE Service - 
      HELP XSA$WRITE 
  XSA_ENTRIES - 
      HELP XSA_INCLUDE_FILES 
  XSA_PARAM - 
      HELP XSA_PARAM UNFAST 
  XSA_PARAM Structure - 
      HELP XSA_PARAM 
  XSA_PARAM.ARS - 
      HELP XSA$PRECORD DESCRIPTION: 
  XSA_PARAM.ARS# - 
      HELP XSA$READ DESCRIPTION: 
  XSA_PARAM.BBUF - 
      HELP XSA$PFIL DESCRIPTION: 
  XSA_PARAM.DVBYTE - 
      HELP XSA$READ DESCRIPTION: 
  XSA_PARAM.ORG - 
      HELP XSA$OPEN DESCRIPTION: 
  XSF Services - 
      HELP XSF 
  XSF$LOCCODE Service - 
      HELP XSF$LOCCODE 
  XSF$LOCCODP Service - 
      HELP XSF$LOCCODP 
  XSF$LOCCODT Service - 
      HELP XSF$LOCCODT 
  XSF$LOCCODX Service - 
      HELP XSF$LOCCODX 
  XS_MACRO_C - 
      HELP XSA_INCLUDE_FILES 
  XTRA -   
    P$SYM - 
      HELP P$SYM XTRA 
  XT_PARAM$ -   
    XUG_GETCMD - 
      HELP XUG_GETCMD XT_PARAM$ 
  XUD Services - 
      HELP XUD 
  XUD$ADD_DATE_DATE Service - 
      HELP XUD$ADD_DATE_DATE 
  XUD$ADD_DATE_TICS Service - 
      HELP XUD$ADD_DATE_TICS 
  XUD$CHAR_DATE Service - 
      HELP XUD$CHAR_DATE 
  XUD$CHAR_UTS Service - 
      HELP XUD$CHAR_UTS 
  XUD$CLOCK_CHAR Service - 
      HELP XUD$CLOCK_CHAR 
  XUD$CLOCK_DATE Service - 
      HELP XUD$CLOCK_DATE 
  XUD$CLOCK_UTS Service - 
      HELP XUD$CLOCK_UTS 
  XUD$CMPR_DATES Service - 
      HELP XUD$CMPR_DATES 
  XUD$DATE_CHAR Service - 
      HELP XUD$DATE_CHAR 
  XUD$DATE_UTS Service - 
      HELP XUD$DATE_UTS 
  XUD$FROM_DATE Service - 
      HELP XUD$FROM_DATE 
  XUD$INIT_PIC Service - 
      HELP XUD$INIT_PIC 
  XUD$SUB_DATE_DATE Service - 
      HELP XUD$SUB_DATE_DATE 
  XUD$SUB_DATE_TICS Service - 
      HELP XUD$SUB_DATE_TICS 
  XUD$TO_DATE Service - 
      HELP XUD$TO_DATE 
  XUD$UTS_ADJUST Service - 
      HELP XUD$UTS_ADJUST 
  XUD$UTS_ADJ_25TH Service - 
      HELP XUD$UTS_ADJ_25TH 
  XUD$UTS_CHAR Service - 
      HELP XUD$UTS_CHAR 
  XUD$UTS_DATE Service - 
      HELP XUD$UTS_DATE 
  XUD$UTS_DIFF Service - 
      HELP XUD$UTS_DIFF 
  XUD$UTS_DIFF_25TH Service - 
      HELP XUD$UTS_DIFF_25TH 
  XUD$UTS_DIFF_SEC Service - 
      HELP XUD$UTS_DIFF_SEC 
  XUD_PARAM - 
      HELP XUD_PARAM TIMESPAN 
  XUD_PARAM Structure - 
      HELP XUD_PARAM 
  XUE Services - 
      HELP XUE 
  XUE$PP_SUCCESS - 
      HELP XUE XUE$PP_SUCCESS 
  XUE$PP_SUCCESS Service - 
      HELP XUE$PP_SUCCESS 
  XUE_ECB - 
      HELP XUE_ECB WORK_DCB 
  XUE_ECB Structure - 
      HELP XUE_ECB 
  XUE_FUNPARAM - 
      HELP XUE_FUNPARAM USER 
  XUE_FUNPARAM Structure - 
      HELP XUE_FUNPARAM 
  XUE_OPTION - 
      HELP XUE_OPTION TEXT 
  XUE_OPTION Structure - 
      HELP XUE_OPTION 
  XUE_PPCB - 
      HELP XUE_PPCB ROOT 
  XUE_PPCB Structure - 
      HELP XUE_PPCB 
  XUE_VARPARAM - 
      HELP XUE_VARPARAM VALUE 
  XUE_VARPARAM Structure - 
      HELP XUE_VARPARAM 
  XUF Services - 
      HELP XUF 
  XUG Services - 
      HELP XUG 
  XUG$ALLMSG Service - 
      HELP XUG$ALLMSG 
  XUG$BLANK_PASSWORD Service - 
      HELP XUG$BLANK_PASSWORD 
  XUG$BREAK Service - 
      HELP XUG$BREAK 
  XUG$CLOSE_DCBS Service - 
      HELP XUG$CLOSE_DCBS 
  XUG$CLRENABLE Service - 
      HELP XUG$CLRENABLE 
  XUG$CORRES Service - 
      HELP XUG$CORRES 
  XUG$DISABLE Service - 
      HELP XUG$DISABLE 
  XUG$ECHO Service - 
      HELP XUG$ECHO 
  XUG$ECHOIF Service - 
      HELP XUG$ECHOIF 
  XUG$ECHOLAST Service - 
      HELP XUG$ECHOLAST 
  XUG$ENABLE Service - 
      HELP XUG$ENABLE 
  XUG$ERRCNVRT Service - 
      HELP XUG$ERRCNVRT 
  XUG$ERRMSG Service - 
      HELP XUG$ERRMSG 
  XUG$ERRPTR Service - 
      HELP XUG$ERRPTR 
  XUG$ERRTOLCP6 Service - 
      HELP XUG$ERRTOLCP6 
  XUG$FINDDCB Service - 
      HELP XUG$FINDDCB 
  XUG$GETCMD Service - 
      HELP XUG$GETCMD 
  XUG$GETDCB Service - 
      HELP XUG$GETDCB 
  XUG$HELP Service - 
      HELP XUG$HELP 
  XUG$INIT Service - 
      HELP XUG$INIT 
  XUG$MOREMSG Service - 
      HELP XUG$MOREMSG 
  XUG$OPENOUT Service - 
      HELP XUG$OPENOUT 
  XUG$SETERRMSG Service - 
      HELP XUG$SETERRMSG 
  XUG$SIMULATE_BREAK Service - 
      HELP XUG$SIMULATE_BREAK 
  XUG_ENTRY - 
      HELP XUG_INCLUDE_FILES 
  XUG_GETCMD - 
      HELP XUG_GETCMD XUH 
  XUG_GETCMD Structure - 
      HELP XUG_GETCMD 
  XUG_INIT - 
      HELP XUG_INIT WSEG 
  XUG_INIT Structure - 
      HELP XUG_INIT 
  XUH -   
    XUG_GETCMD - 
      HELP XUG_GETCMD XUH 
  XUH_PARAM - 
      HELP XUH_PARAM VFC 
  XUH_PARAM DRAW - 
      HELP XUH_PARAM VFC 
  XUH_PARAM Structure - 
      HELP XUH_PARAM 
  XUM Services - 
      HELP XUM 
  XUM$CREATE_NEW_ITEM Service - 
      HELP XUM$CREATE_NEW_ITEM 
  XUM$DELETE_ITEM Service - 
      HELP XUM$DELETE_ITEM 
  XUM$GET_LRU_ITEM Service - 
      HELP XUM$GET_LRU_ITEM 
  XUM$GET_MRU_ITEM Service - 
      HELP XUM$GET_MRU_ITEM 
  XUM$INIT_WORKSPACE Service - 
      HELP XUM$INIT_WORKSPACE 
  XUM$MAKE_ITEM_LRU Service - 
      HELP XUM$MAKE_ITEM_LRU 
  XUM$MAKE_ITEM_MRU Service - 
      HELP XUM$MAKE_ITEM_MRU 
  XUO Default Buffer Sizes - 
      HELP XUO$BUFINIT DESCRIPTION: 
  XUO Services - 
      HELP XUO 
  XUO$BUFINIT Service - 
      HELP XUO$BUFINIT 
  XUO$DBGNAME Service - 
      HELP XUO$DBGNAME 
  XUO$DNAME Service - 
      HELP XUO$DNAME 
  XUO$EDEF Service - 
      HELP XUO$EDEF 
  XUO$EREF Service - 
      HELP XUO$EREF 
  XUO$EXST Service - 
      HELP XUO$EXST 
  XUO$EXSTNUM Service - 
      HELP XUO$EXSTNUM 
  XUO$FRWD_REF Service - 
      HELP XUO$FRWD_REF 
  XUO$HEADNAME Service - 
      HELP XUO$HEADNAME 
  XUO$HEADSTART Service - 
      HELP XUO$HEADSTART 
  XUO$HEAD_SEVERITY Service - 
      HELP XUO$HEAD_SEVERITY 
  XUO$INTNTRY Service - 
      HELP XUO$INTNTRY 
  XUO$LOGBLKALLOC Service - 
      HELP XUO$LOGBLKALLOC 
  XUO$LOGBLKEXSTINIT Service - 
      HELP XUO$LOGBLKEXSTINIT 
  XUO$LOGBLKEXSTTERM Service - 
      HELP XUO$LOGBLKEXSTTERM 
  XUO$LOGBLKNOAUTO Service - 
      HELP XUO$LOGBLKNOAUTO 
  XUO$LOGBLKTERM Service - 
      HELP XUO$LOGBLKTERM 
  XUO$LOGBLKVREBLINIT Service - 
      HELP XUO$LOGBLKVREBLINIT 
  XUO$LOGBLKVREBLTERM Service - 
      HELP XUO$LOGBLKVREBLTERM 
  XUO$OUINIT Service - 
      HELP XUO$OUINIT 
  XUO$OUTERM Service - 
      HELP XUO$OUTERM 
  XUO$PRGM Service - 
      HELP XUO$PRGM 
  XUO$PRGM_TEXT Service - 
      HELP XUO$PRGM_TEXT 
  XUO$RELOC Service - 
      HELP XUO$RELOC 
  XUO$RNAME Service - 
      HELP XUO$RNAME 
  XUO$SDEF Service - 
      HELP XUO$SDEF 
  XUO$SDEF_CONST Service - 
      HELP XUO$SDEF_CONST 
  XUO$SECTBUILD Service - 
      HELP XUO$SECTBUILD 
  XUO$SECTNAME Service - 
      HELP XUO$SECTNAME 
  XUO$SECTSIZE Service - 
      HELP XUO$SECTSIZE 
  XUO$SEGDEF Service - 
      HELP XUO$SEGDEF 
  XUO$SEGDEF_CONST Service - 
      HELP XUO$SEGDEF_CONST 
  XUO$SEGREF Service - 
      HELP XUO$SEGREF 
  XUO$SREF Service - 
      HELP XUO$SREF 
  XUO$VREBL Service - 
      HELP XUO$VREBL 
  XUO$VREBLNUM Service - 
      HELP XUO$VREBLNUM 
  XUO$VREBL_CONT Service - 
      HELP XUO$VREBL_CONT 
  XUO$VREBL_CONT_ADJ Service - 
      HELP XUO$VREBL_CONT_ADJ 
  XUO$VREBL_CONT_ET Service - 
      HELP XUO$VREBL_CONT_ET 
  XUO$VREBL_CONT_SET Service - 
      HELP XUO$VREBL_CONT_SET 
  XUP Service (X$PARSE) - 
      HELP X$PARSE 
  XUR Services - 
      HELP XUR 
  XUR$ALLMSG Service - 
      HELP XUR$ALLMSG 
  XUR$BREAK Service - 
      HELP XUR$BREAK 
  XUR$CLOSE_DCBS Service - 
      HELP XUR$CLOSE_DCBS 
  XUR$CLRENABLE Service - 
      HELP XUR$CLRENABLE 
  XUR$CORRES Service - 
      HELP XUR$CORRES 
  XUR$DISABLE Service - 
      HELP XUR$DISABLE 
  XUR$ECHO Service - 
      HELP XUR$ECHO 
  XUR$ECHOIF Service - 
      HELP XUR$ECHOIF 
  XUR$ECHOLAST Service - 
      HELP XUR$ECHOLAST 
  XUR$ENABLE Service - 
      HELP XUR$ENABLE 
  XUR$ERRCNVRT Service - 
      HELP XUR$ERRCNVRT 
  XUR$ERRMSG Service - 
      HELP XUR$ERRMSG 
  XUR$ERRPTR Service - 
      HELP XUR$ERRPTR 
  XUR$ERRTOLCP6 Service - 
      HELP XUR$ERRTOLCP6 
  XUR$FINDDCB Service - 
      HELP XUR$FINDDCB 
  XUR$GETCMD Service - 
      HELP XUR$GETCMD 
  XUR$GETDCB Service - 
      HELP XUR$GETDCB 
  XUR$HELP Service - 
      HELP XUR$HELP 
  XUR$INFOMSG Service - 
      HELP XUR$INFOMSG 
  XUR$INIT Service - 
      HELP XUR$INIT 
  XUR$MOREMSG Service - 
      HELP XUR$MOREMSG 
  XUR$OPENOUT Service - 
      HELP XUR$OPENOUT 
  XUR$SETDCBS Service - 
      HELP XUR$SETDCBS 
  XUR$SETERRMSG Service - 
      HELP XUR$SETERRMSG 
  XUR$SIMULATE_BREAK Service - 
      HELP XUR$SIMULATE_BREAK 
  XUR_ENTRY - 
      HELP XUR_INCLUDE_FILES 
  XUR_INIT - 
      HELP XUR_INIT WORK 
  XUR_INIT Structure - 
      HELP XUR_INIT 
  XUS$CORRECT_SPELLING Service - 
      HELP XUS$CORRECT_SPELLING 
  XUU Services - 
      HELP XUU 
  XUU$ALLOC_TYPES - 
      HELP XUU_INCLUDE_FILES 
  XUU$CLOSE Service - 
      HELP XUU$CLOSE 
  XUU$ENTRY - 
      HELP XUU_INCLUDE_FILES 
  XUU$OPEN Service - 
      HELP XUU$OPEN 
  XUU$READ Service - 
      HELP XUU$READ 
  XUU_PARAM - 
      HELP XUU_PARAM UI_ERRCODE 
  XUU_PARAM Structure - 
      HELP XUU_PARAM 
  XUW Services - 
      HELP XUW 
  XUW$ENTRIES macro - 
      HELP XUW_INCLUDE_FILES 
  XUW_WILDCARD - 
      HELP XUW_WILDCARD 
  XUW_WILDCARD DRAW - 
      HELP XUW_WILDCARD 
  XUW_WILDCARD macro - 
      HELP XUW_INCLUDE_FILES 
  XUW_WILDCARD Structure - 
      HELP XUW_WILDCARD 
  XUX Services - 
      HELP XUX 
  XUX$BC_UNIT - 
      HELP XUX$BC_UNIT 
  XUX$BC_UNIT Structure - 
      HELP XUX$BC_UNIT 
  XUX$CLEANUP Service - 
      HELP XUX$CLEANUP 
  XUX$COMMON_OPTIONS Service - 
      HELP XUX$COMMON_OPTIONS 
  XUX$GETLINE Service - 
      HELP XUX$GETLINE 
  XUX$LEGAL_OPTIONS - 
      HELP XUX$LEGAL_OPTIONS XREF 
  XUX$LEGAL_OPTIONS Structure - 
      HELP XUX$LEGAL_OPTIONS 
  XUX$PARAM - 
      HELP XUX$PARAM USER_ROUTINE 
  XUX$PARAM Structure - 
      HELP XUX$PARAM 
  XUX$PARAM_NO_PARSE - 
      HELP XUX$PARAM_NO_PARSE ERROR_CODE 
  XUX$PARAM_NO_PARSE Structure - 
      HELP XUX$PARAM_NO_PARSE 
  XUX$SRCH_LIST - 
      HELP XUX$SRCH_LIST WSN 
  XUX$SRCH_LIST Structure - 
      HELP XUX$SRCH_LIST 
  XUX$STD_OPTIONS - 
      HELP XUX$STD_OPTIONS XREF 
  XUX$STD_OPTIONS Structure - 
      HELP XUX$STD_OPTIONS 
  XU_MACRO_C - 
      HELP XUG_INCLUDE_FILES 
      HELP XUR_INCLUDE_FILES 
      HELP XUU_INCLUDE_FILES 
  XU_PERR_C - 
      HELP XUG_INCLUDE_FILES 
      HELP XUR_INCLUDE_FILES 
      HELP XUU_INCLUDE_FILES 
  XU_PERR_C macro - 
      HELP XUW_INCLUDE_FILES 
  XU_SUBS_C - 
      HELP XUG_INCLUDE_FILES 
      HELP XUR_INCLUDE_FILES 
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
For a description of each miscellaneous insertion code, type: 
HELP (HOSTLIB) MISC_INSERT_CODE code 
where code is one of the following:  REPEAT_GROUP_BEGIN (for ) ), 
REPEAT_GROUP_END (for ) ), IF (for [ ), ELSEIF (for ?), ENDIF (for ] ), C (for 
Subroutine), EQUALS (for =), Q (for Quit processing format), P (for Position 
data pointer), S (for Skip), CARET (for Rescan Point), TOF (for !), TAB (for - 
), SLASH (for Print n lines), R (for Wrap point), V (for Set VFC), X (for 
Insert n spaces or Backspace), CONTINUATION (for \), F (for Special formats), 
J (for error code convert), U (for UTS to time and date conversion), PERCENT 
(for %). 
  Code           Meaning 
  ( 
                 Begin repeat group.  Repeat this section of the format CNT(0) 
                 times. 
  ) 
                 End repeat group.  If CNT(0) is present, it replaces the 
                 loop-variable for the repeat group.  The group repeats until 
                 the variable is <= zero, thus providing a DO UNTIL function. 
  [ 
                 Begin If-Elseif-Endif group.  Format this section if 
                 CNT(0)=CNT(1), until terminated by Elseif (?) or Endif(]) 
                 code.  For example, the following format text would display 
                 the familiar 2-bit yes/no/dc option in an FPT_OPEN or 
                 VLP_TRMCTL: 
                   Option =%2.2N[ yes%0? no%? DC %] 
                 If-Elseif-Endif groups may be nested until auto space runs 
                 out. 
  ? 
                 Elseif function.  Format this section if CNT(0) matches the 
                 CNT(1) value from the corresponding [-function.  The 
                 expression for CNT(0) must be a constant (the N, #, and : 
                 codes are not permitted in the count expression).  If CNT(0) 
                 is not specified, the section is formatted if no match has 
                 yet been found (Else function).  %? (as opposed to %0?) 
                 serves as an Else function, or wildcard match.  It should be 
                 used last. 
  ] 
                 Endif function.  Terminates an If-Elseif-Endif group. 
  C 
                 Subroutine.  If CNT(0) is greater than zero, executes the 
                 subroutine numbered thereby.  Otherwise, if CNT(1) is greater 
                 than zero, marks the start of the subroutine numbered 
                 thereby.  Subroutine numbers must be between 1 and 99 
                 inclusive, and share the same space as the variables.  As a 
                 result, variable number n conflicts with subroutine number 
                 100-n.  A subroutine definition is terminated by a C-function 
                 with no CNT(0) and no CNT(1) (e.g., %C).  A subroutine may be 
                 called, but not defined, within another subroutine. 
                 Subroutine calls may be nested until auto space runs out. 
  = 
                 Assign value to variable.  Assigns the value in CNT(0) to the 
                 variable numbered by CNT(1).  CNT(1) must be between 0 and 
                 99, inclusive. 
  E 
                 Call edit routine.  If FDS.EDIT# is not ENTADDR(NIL) then 
                 CALL FDS.EDIT#(FDS,CNT).  Where FDS is the current FDS and 
                 CNT is the array of counts described earlier.  If the edit 
                 routine ALTRETs the formatter will remain in the insertion 
                 mode.  A normal return will cause the formatter to return to 
                 transfer mode.  For a discussion of insertion mode and 
                 transfer mode, see the description of the X$FORMAT service. 
  Q 
                 Quit processing format if no data remains.  If CNT(0) is 
                 greater than zero, processing is terminated unconditionally. 
  P 
                 Position data pointer to word CNT(1), character CNT(2), bit 
                 CNT(3) of data vector CNT(0).  If CNT(0)=0, then positioning 
                 is from the beginning of the current data vector.  Data 
                 vectors are numbered 1 through NVECS. 
  S 
                 Skip CNT(0) bytes of data plus CNT(1) bits of data.  If both 
                 CNT(0) and CNT(1) are zero, and if the data pointer is not 
                 positioned at the beginning of data vector, skip to the next 
                 data vector.  If the CNT fields exceed the size of the 
                 current data vector, the results will be unpredictable. 
  ^ (caret) 
                 Set rescan point.  If the end of format is hit and there is 
                 still data remaining, then the buffer is output and the 
                 format pointer is set to the rescan point.  The 
                 default is the beginning of the format.  CAUTION:  If the 
                 rescan point is set to be within a repeat group then results 
                 are unpredictable. 
  ! 
                 Skip to top of form.  The current buffer is output and an 
                 M$DEVICE(PAGE=YES) is issued on DCB. 
  - (dash) 
                 Tab to column CNT(0).  If CNT(0) is 0, then tab to the next 
                 multiple of FDS.TABDFLT# plus 1.  If CNT(0) is non-zero and 
                 less than the current buffer position and the > flag is set, 
                 then a single space will be inserted. 
                 If CNT(1) is greater than zero, it sets the value for 
                 F_FDS.TABDFLT#. 
                 If CNT(2) is greater than zero, it sets the value for 
                 FDS.WRAPTAB#. 
  / 
                 Print CNT(0) lines.  The first line is the current buffer. 
                 Subsequent lines are blank. 
  R 
                 Set wrap point.  R wraps the output line if the output buffer 
                 does not have room for at least CNT(0) bytes. 
                 If CNT(0) is zero, the line is wrapped at the current 
                 position if it would otherwise overflow before the next 
                 R-function or /-function. 
                 If the output buffer is empty, the R code has no effect. 
  V 
                 Set VFC character.  The character following %V in the FMT 
                 string is put in character 0 of the buffer unless it is a % 
                 character, in which case one byte of data is obtained for the 
                 VFC character.  If the character following %V is *, that 
                 character is stored in the buffer in character 0 to indicate 
                 the write should occur with no VFC. 
  X 
                 Insert a space CNT(0) times.  CNT(0) may be negative (e.g., 
                 %:4-X), which has the effect of backspacing CNT(0) positions. 
  \ 
                 Continuation function.  Disables the automatic dumping of any 
                 partially filled output buffer when X$FORMAT returns to the 
                 caller.  Then, if the next call to X$FORMAT uses the same 
                 F_FDS and the first two characters of the format string are 
                 %\, that partially filled buffer will be extended.  Note that 
                 the last line of output for a display that uses the 
                 \-function MUST be explicitly displayed via the /-function. 
                 Note:  If the %\ code occurs at the beginning of the first 
                 format buffer, the user must set F_FDS.BUFX# to zero at the 
                 first call to the Formatter.  (Setting BUFX# to 0 can be 
                 accomplished by invoking the %F_FDS macro; or if STCLASS is 
                 STATIC or CONSTANT by moving the the entire structure to an 
                 AUTO copy before setting BUFX# to zero.)  Thereafter, BUFX# 
                 should be left unchanged between calls to the Formatter. 
  F 
                 Use special formats.  Format is determined by the value of 
                 CNT(1).  Currently defined values are: 
                     1  Acquire two words of data and format as a 
                        descriptor.  CNT(0) is field width. 
                     2  Acquire one word of data and format as a 
                        pointer.  CNT(0) is field width. 
                     3  Acquire one word of data and use it as a DCB 
                        number in a call to M$UNFID.  The resultant fid is 
                        placed in the output buffer.  CNT(0) is field 
                        width. 
                     4  Acquire one word of data and use it as a dcb 
                        number.  The associated DCB name is placed in the 
                        output buffer.  CNT(0) is field width. 
  J 
                 Convert standard error code.  CNT(0) is the field width. 
                 CNT(1) is the number of bits of data to acquire for the error 
                 code.  If CNT(2) is present, its value is used as the DCB 
                 number from which to make Fid substitutions in the error 
                 message.  The error code is displayed in message form using 
                 M$ERRMSG. 
  U 
                 Convert UTS to time and date. 
                 CNT(0) is the field width. 
                 CNT(1) is number of bits of data to acquire for UTS, default 
                 is 36. 
                 CNT(2) is output format and has the following values: 
                     0 - HH:MM             (Time only) 
                     1 - MM/DD/YY          (Date only) 
                     2 - HH:MM MM/DD/YY    (Time and date) 
                     3 - MM/DD/YY HH:MM    (Date and time) 
                 The values 4 - 7 correspond with 0 - 3 except the system 
                 clock is used as the source of the UTS instead of acquiring 
                 data. 
                 The values 8 - 11 correspond with 0 - 3 except that the 
                 acquired data is presumed to be an FEP UTS. 
                 CNT(3) is the M$TIME format and has the following values: 
                     0 - M$TIME LOCAL format. 
                     1 - M$TIME EXT format. 
                     2 - M$TIME ANS format. 
                     3 - Unused. 
                 Values 4 - 7 correspond with 0 - 3 except HH:MM becomes 
                 HH:MM:SS. 
                 Values 8 - 11 correspond with 0 - 3 except HH:MM becomes 
                 HH:MM:SS.SS (i.e., a FEP UTS). 
  % 
                 Put one % character in the buffer. 
00019
00018
00013
00006
00008
00012
00019
00014
00008
00004
00005
00007
00021
00020
00003
00018
00021
00003
00001
00010
00023
00010
00015
00009
00004
00009
00016
00001
00002
00012
00005
00002
00011
00015
00020
00006
00014
00013
00022
00017
00016
00018
CHANGES
To list all conventions, type ??.  To list a specific convention, type: 
HELP (processor) NOTATION name 
Valid names are LOWERCASE, UPPERCASE, SPECIAL_CHARACTERS, NUMERALS, BRACKETS, 
BRACES, OR_BAR, HORIZONTAL_ELLIPSIS, VERTICAL_ELLIPSIS. 
  Notation    Description 
  lower-case 
              Lower-case letters indicate that the element is a variable, to 
              be replaced with the desired value. 
  UPPER-CASE 
              Upper-case letters indicate a literal, to be entered as shown. 
  special characters 
              Special characters are literals, to be entered as shown. 
  numerals 
              Numerals standing alone are literals, to be entered as shown. 
              Numerals embedded in or affixed to a string of capital letters 
              are also literals, to be entered as shown, for example, GHOST1. 
              Numerals embedded in or affixed to a string of lower-case 
              letters are part of the variable name to be replaced with a 
              desired value, for example, attribute1. 
  brackets 
              An element inside brackets ([]) is optional.  If elements are 
              stacked vertically within brackets, the elements may be omitted 
              or one of them may be entered.  For example, the notation 
                  [DISK] 
                  [TAPE]    means that the user may omit this entry, or 
                            may enter DISK, or may enter TAPE. 
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
                  {ALL}    means that either a value for id or the word 
                           ALL must be entered. 
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
                  name1[,name2] ... means that one or more name values 
                                    may be entered, with commas inserted 
                                    between the name values. 
  vertical ellipsis 
              The vertical ellipsis indicates that commands have been omitted. 
                  OPT*PRO=TTY4    means that there are one or more 
                  .               statements omitted between the two OPT 
                  .               commands. 
                  . 
                  OPT*END 
Each of the structure drawings in this manual represents one %MACRO entry 
which defines a structure.  Comments and most preprocessor constructs have 
been removed from the descriptions to make them easier to read.  There are one 
or two sections in each drawing, depending on the data contained in the text 
of the structure and whether the structure is a %MACRO or DCL. 
The first section of each drawing contains an alphabetized list of all the 
parameters specified in the %MACRO header and their default values.  If 
substitution keywords are also present, they are listed alphabetically under 
the parameter to which they apply, along with their values.  Most parameters 
are used in the INIT clause of the DCL; in this case the (first) location in 
the structure in which the parameter value will be found is printed opposite 
the parameter name.  The format used is ".octal word-byte-bit".  If the 
parameter is not referenced in an INIT clause, the location is replaced by 
".....".  Only one value per INIT clause may be cross-referenced in this 
manner; if multiple values are present in the INIT clause, the second and 
succeeding ones will be flagged as "not found" (".....") in the parameter 
listing. 
The second section is the actual text of the DCL and a drawing of the 
structure it generates.  The right half of the page contains the structure as 
it appears in the source file, except that comments and preprocessor 
expressions have been removed.  The left half of each line shows the memory 
layout generated by the code to its right on the same line.  The drawing is 
one word (36 bits) wide and continues for as many words as necessary to 
describe the entire structure.  The words are divided into four bytes of three 
nibbles each to make them easier to read.  Lower case letters are used to 
represent the bits occupied by the item being described: 
    bbb - indicates a BIT item. 
    ccc - indicates a CHAR item. 
    eee - indicates an EPTR item. 
    ppp - indicates a PTR item. 
    rrr - indicates a REMEMBER item. 
    sss - indicates an SBIN item. 
    uuu - indicates a UBIN item. 
    vvv - indicates a VECTOR item. 
If the data item either begins or ends on a non-byte boundary, its 
representation in the drawing is changed to a string of octal digits, 
indicating the bits occupied within the octal nibble of the byte.  This 
assists in decoding fields which are non-byte aligned when only an octal 
representation is available. 
Filler or supplementary storage which will be present in the structure is 
indicated by a sequence of one or more periods ("."). 
If a data item generates six or more words of storage, the "middle" words will 
not be printed to conserve space.  This omission is indicated by a line of "Z" 
characters replacing the vertical bars ("|") normally used to separate bytes. 
Only one occurrence of an array element is shown, to illustrate its shape. 
Blank spaces and/or "Z" lines represent the remaining space occupied by the 
array. 
Items which are variable-length are shown as one bit (or byte) wide; the user 
must use the actual values used in the structure to determine the true length 
of the item at execution time.  Similarly, arrays with variable upper bounds 
are shown with only one element. 
Each word in the drawing is preceded by its octal offset from the beginning of 
the structure.  The total length of the structure is indicated below the last 
line of the DCL in the form ".octal words-bytes-bits".  If the structure 
contains variable-length strings or variable-dimension arrays, it is flagged 
as "variable". 
The following sample structure illustrates many of these points.  Numbers in 
brackets refer to the items indicated by the bracketed numbers on the example. 
[1] The %MACRO or DCL name is printed at the center at the beginning of the 
structure drawing and on each continuation page. 
[2] This is a listing of the parameters in alphabetic order. 
[3] Indicates that the storage for "TYPE" begins at word 3 (octal), byte 0, 
bit 0. 
[4] This is the parameter ("TYPE") and its default value ("0"). 
[5] These are the keywords which may be specified to change the value of the 
parameter (e.g., "TYPE=TERMINAL" places "3" in the TYPE field of the 
structure) and the values they represent. 
[6] The periods (".") indicate that this parameter was not found in an INIT 
clause or is part of a list of initial values.  In this case, the latter is 
true. 
[7] The remainder of the entry is the drawing section. 
[8] The right half of this section contains the DCL text. 
[9] The left half of this section contains the drawing of the storage 
generated by the DCL text. 
[10] The location for this line is indicated in octal.  Since there is nothing 
else in the drawing, this line of the DCL generates no storage. 
[11] This line of the DCL has generated a 72-bit (two word) bit item, 
represented by the b's.  Other items generate e's, u's, and so forth, 
depending on their type. 
[12] This is an array element.  Note that the two bytes following it in word 
.4 are blank, indicating that the array occupies this space. 
[13] Although DIRECTION# is a UBIN value, its storage is represented by the 
two bits "6" since it does not end on a byte boundary.  The "6" indicates that 
DIRECTION# occupies the leftmost two bits of the first octal nibble of this 
byte. 
[14] Since HEADER# generates 20 words of storage, it is shortened to its first 
two words and last two words.  The "Z" line indicates that one or more words 
have been omitted to conserve space. 
[15] Since C# is a variable-length string, only one byte is indicated as its 
length in the drawing.  The user would consult the L# byte to determine the 
true length of C# at run time. 
[16] Periods indicate supplementary or filler storage.  Three bytes of 
supplementary storage are added to L# since it is (by default) ALIGNED.  Up to 
seven bytes of filler storage are added to the structure after the last 
character of C# since it is DALIGNED. 
[17] The total length of the structure is octal .34 words, 0 bytes, and 0 
bits; however, since this structure contains a variable-length item, the user 
must adjust the total length appropriately at run time. 
                                     SAMPLE  <--[1] 
        .4-3-2 ABC='0'B                          ) 
                NO='0'B                          ) 
                YES='1'                          )<--[2] 
        ..... ALGN=WALIGNED                      ) 
      .32-0-0 C=' '                              ) 
        ..... DCB=NIL                            ) 
       .4-3-0 DIRECTION=1                        ) 
                INPUT=1                          ) 
                OUTPUT=2                         ) 
        ..... FPTN=SAMPLE                        ) 
       .4-0-0 INDENT1=5                          ) 
        ..... INDENT2=10                         ) 
 [6]--> ..... INDENT3=15                         ) 
      .31-0-0 L=0                                ) 
        ..... PFMT="BIT(72)"                     ) 
        ..... STCLASS=BASED                      ) 
 [3]-->.3-0-0 TYPE=0   <--[4]                    ) 
                FILE=1                           ) 
 [5]-->         TERMINAL=3                       ) 
       .0-0-0 USER=NIL                           ) 
       .2-0-0 ZZZ=NIL                            ) 
     /------------------[7]------------------\ 
      /-------[9]------\/--------[8]---------\ 
       0   1   2   3 
     +---+---+---+---+ DCL 
  .0 |<--[10]|   |   | 1 FPTN STCLASS DALIGNED, 
  .0 |bbb|bbb|bbb|bbb|   2 USER_          PFMT INIT(VECTOR(USER)), 
  .1 |bbb|bbb|bbb|bbb| <--[11] 
  .2 |   |   |   |   |   2 V, 
  .2 |eee|eee|eee|eee|     3 ZZZ#         EPTR INIT(ENTADDR(ZZZ)), 
  .3 |uuu|   |   |   |     3 TYPE#        UBIN BYTE UNAL INIT(TYPE), 
  .3 |   |bbb|   |   |     3 *            BIT(9) INIT('0'B), 
  .3 |   |   |   |   |     3 DCB#         UBIN HALF UNAL 
  .3 |   |   |uuu|uuu|                    INIT(DCBNUM(DCB)), 
  .4 |   |   |   |   |     3 IDENT#(0:2)  SBIN BYTE UNAL INIT(INDENT1, 
  .4 |sss|<--[12]|   |                    INDENT2,INDENT3), 
  .4 |   [13]--> |6  |     3 DIRECTION#   UBIN(2) UNAL INIT(DIRECTION), 
  .4 |   |   |   |1  |     3 ABC#         BIT(1) INIT(ABC), 
  .4 |   |   |   | 77|     3 *            BIT(6) UNAL INIT('0'B), 
  .5 |ccc|ccc|ccc|ccc|     3 HEADER#      CHAR(80) INIT(' '), 
  .6 |ccc|ccc|ccc|ccc| 
     Z   Z   Z   Z   Z <--[14] 
 .27 |ccc|ccc|ccc|ccc| 
 .30 |ccc|ccc|ccc|ccc| 
 .31 |   |   |   |   |     3 FNAME, 
 .31 |uuu|.<--[16]...|       4 L#         UBIN BYTE INIT(L), 
 .32 |   |   |   |   |       4 C#         CHAR(FPTN.V.FNAME.L#) 
 .32 |ccc|.<--[15]...|                    INIT(C); 
 .33 |...|...|...|...| 
     +---+---+---+---+ 
       0   1   2   3    .34-0-0 total length (variable) <--[17] 
00006
00005
00008
00001
00004
00007
00003
00002
00009
For a description of each numeric insertion code, type: 
HELP (HOSTLIB) NUM_INSERT_CODE code 
where code is one of the following:  D, O, B, H, or Y. 
  Code           Meaning 
  B 
                 Convert to binary number. 
  D 
                 Convert to decimal number. 
  H 
                 Convert to hexadecimal number. 
  O 
                 Convert to octal number. 
  Y 
                 Convert to hexadecimal number in 8 of 9 format.  When used 
                 with the @ flag, the results, though predictable, are most 
                 likely wrong.  Y and @X produce identical results only when 
                 the data being converted ends at a byte boundary. 
00001
00002
00003
00004
00005
    The contents in the OUT$BLK structure, generated via the PARSE$OUT macro, 
    can be viewed individually by typing: 
    !HELP (HOSTLIB) OUT$BLK field 
    Or type ?? to see all field descriptions. 
    CODE - VALUE-DEC(0-65535)    contains the numeric "node code" specified by 
    the user when the corresponding parse node was defined. 
    CPOS - VALUE-DEC (0-(2**20-1))    is the "character position" of this 
    block.  This field will contain a character index (starting at 0) into the 
    original parse string; the index identifies the first character of the 
    string which was accepted by this node (or by any of its sub-nodes). 
    NDTYPE = OPTION    specifies the type of parse node to which this 
    PARSE$OUT block corresponds.  EQUs defined in the file XU_SUBS_C can be 
    used when examining this field: 
            Expression          Meaning 
            ACCOUNT#            .ACCOUNT 
            ANUM#               .ANUM 
            ALPHA#              .ALPHA 
            ALTERN#             Alternative 
            ASYM#               .ASYM 
            BLANK#              .BLANK 
            DEC#                .DECIMAL 
            DSTRING#            .QUOTE, .SLASH, .DSTR 
            EOL#                .END 
            FID#                .FID 
            HEX#                .HEX 
            JOBNAME#            .JOBNAME 
            KONCAT#             Concatenation 
            LIST#               List 
            LITERAL#            Literal 
            NULL#               .NULL 
            OCT#                .OCTAL 
            PL6SYM#             .PL6SYM 
            RALTERN#            Reducing alternative 
            RTEXT#              Text with no editing or case conversion 
            SYM#                .SYMBOL 
    NSUBLKS = VALUE-DEC(0-(2**18-1))    is a number of sub-blocks.  This field 
    contains the count of pointers actually available in the SUBLK$ array.  If 
    this block represents a literal, NSUBLKS = 0. 
    SCRITCH = VALUE-BIT(18)    is a scritch field reserved for the user. 
    X$PARSE initializes this field to zero when the PARSE$OUT structure is 
    allocated, and never sets or examines it thereafter.  The name of this 
    field may be changed when the PARSE$OUT macro is invoked by the user 
    (e.g., "SCRITCH=yourname"); its data type may also be changed (e.g., 
    "SCRMODE=pl6_datatype"), as may its alignment (e.g., 
    SCRALGN="pl6_alignment"). 
    NOTE:  This field must be 18-bits long, and must be UNAL, CALIGNED, or 
    HALIGNED. 
    SUBLK$ = ARRAY    is an array of PL-6 PTRs.  The number of elements in 
    this array is found in OUT$BLK.NSUBLKS; each PTR will point to another 
    OUT$BLK structure, or to an OUT$SYM structure.  SUBLK$ is omitted if this 
    block represents a literal. 
00001
00002
00003
00004
00005
00006
The fields in the OUT$SYM structure, generated via the PARSE$SYM macro, can be 
viewed individually by typing: 
!HELP (HOSTLIB) OUT$SYM field 
Or type ?? to see all field descriptions. 
    CODE - VALUE-DEC(0-65535)    See CODE in the OUT$BLK structure. 
    COUNT - VALUE-DEC(0-?)    contains the number of characters in TEXT in the 
    OUT$SYM structure. 
    CPOS - VALUE-DEC(0-(2**18-1))    See CPOS in the OUT$BLK structure. 
    NDTYPE = OPTION    See NDTYPE in the OUT$BLK structure. 
    NSUBLKS = VALUE-DEC(0-(2**18-1))    See NSUBLKS in the OUT$BLK structure. 
    (Always 1 for OUT$SYM.) 
    SCRITCH = VALUE-BIT(18)    See SCRITCH in the OUT$BLK structure. 
    TEXT - VALUE-CHAR(n)    contains the text of a string, decimal number, 
    PL-6 identifier, or some other parser "symbol". 
    TEXTC$ - PTR    a pointer to a TEXTC-type string (a 1-byte count field 
    followed by a variable number of characters).  Always points to 
    OUT$SYM.COUNT in the current OUT$SYM block. 
00001
00002
00003
00004
00005
00006
00007
00008
P$DSTR is a structure used to describe a "delimited string" node.  Many of 
P$DSTR's sub-fields are identical to those of P$NODE or P$SYM, and are 
documented within those structures.  The contents of the P$DSTR structure can 
be viewed individually by typing: 
!HELP (HOSTLIB) P$DSTR field 
Or type ?? to see all field descriptions. 
    DLIM - specifies the character which delimits this string.  If P$DSTR.DLIM 
    = BINASC(0), a generic delimited string is being requested; such a string 
    may be delimited by any printable character which does not belong to the 
    alphanumeric class (A-Z, a-z, 0-9). 
    LEXTYPE - identifies this lexical block as a delimited string.  This field 
    always contains the value %LEX_DSTRING#. 
    TYPE - identifies this node as a P$DSTR.  This field always contains the 
    value %TYPE_LEXEME#. 
00001
00002
00003
The fields in the P$KEYWORDS structure can be viewed individually by typing: 
!HELP (HOSTLIB) P$KEYWORDS field 
Or type ?? to see all field descriptions. 
    KEYWORD_COUNT - VALUE-DEC(0-?) contains the number (SBIN WORD) of keywords 
    which would be legal at the parse-error point. 
    KEYWORDS$ - ARRAY    is an array of effective dimension 
    (0:KEYWORD_COUNT-1).  Each element in this array is a pointer to a TEXTC 
    string which contains a keyword which would be legal at the parse-error 
    point. 
    LEGAL$ - PTR    points to a word-aligned scratch area at least 
    KEYWORD_COUNT bits long. 
00002
00001
00003
P$LIT is a structure used to describe "literal" parse nodes, as built by 
PARTRGE and interrogated by X$PARSE.  The P$LIT structure is a sort of 
"overlay" of P$NODE; these structures have many sub-fields in common (TYPE, 
P_F, S_F, O_F, OPT, RPEAT, SKBL, and RTEXT).  Documentation for these common 
sub-fields may be found under the P$NODE structure.  The contents of the P$LIT 
structure can be viewed individually by typing: 
!HELP (HOSTLIB) P$LIT field 
Or type ?? to see all field descriptions. 
    ABREV - an integer field which contains either 0, or the minimum length of 
    an acceptable abbreviation of this literal.  For example:  the PARTRGE 
    literal 'ABCDEF' has an ABREV of 0; the literal 'ABC/DEF' has an ABREV of 
    3. 
    COUNT - the number of characters in this literal. 
    TEXT - a CHAR variable which contains the text of this literal. 
    TYPE - identifies the type of this P$LIT node.  This field always contains 
    the value %TYPE_LITERAL# as found in XU_SUBS_C.:LIBRARY. 
    UPRLOWR - specifies that this node is to be compared to the input string 
    in a case-insensitive fashion; upper- and lower-case characters are 
    considered equivalent.  This option is normally set for all 'literal' 
    nodes; it is reset if the first character of a literal node is an '=' 
    character, which indicates that the literal text must be matched exactly. 
00001
00002
00003
00004
00005
P$NODE is a structure used to describe syntax nodes, as built by PARTRGE and 
interrogated by X$PARSE.  This structure may be used to examine all of the 
attributes of nodes of several types:  concatenation, list, alternative, and 
reducing alternative.  It may also be used to examine a few of the attributes 
of symbol and delimited-string nodes, as indicated.  The contents of the 
P$NODE structure can be viewed individually by typing: 
!HELP (HOSTLIB) P$NODE field 
Or type ?? to see all field descriptions. 
    CODE - specifies the code number for this parse node.  This value will be 
    returned in OUT$BLK.CODE (or OUT$SYM.CODE) in any parse block built by 
    X$PARSE which corresponds to this node. 
    F_F - specifies that the user wants to be notified of any failed attempts 
    to match this node; set if the user specified the (FAIL) option in the 
    PARTRGE definition of this node. 
    NSUBNDS - specifies the number of sub-nodes within this parse block. 
    OPT - set if this node is "optional".  This flag is set if the PARTRGE 
    definition of this node was enclosed in a set of square-brackets. 
    O_F - specifies that this node is to result in the creation of a block in 
    the X$PARSE output tree.  The setting of this flag is controlled by 
    several PARTRGE attributes:  the OUT option, the NOUT option, the "code" 
    option, and the node's basic type.  If the user specifies OUT, this flag 
    will be set; if the user specifies NOUT, this flag will not be set; if the 
    user specifies neither OUT nor NOUT, this flag will be set if the "code" 
    option was specified or if the node is of the "delimited string" or 
    "symbol" varieties. 
    P_F - specifies that the user wants to be able to pre-approve any attempt 
    to match this node.  This flag is set if the user supplied the (PRE) 
    option in the PARTRGE definition of this node. 
    RPEAT - specifies that this node can be repeated (may occur more than 
    once).  This flag is set of the PARTRGE definition of this node was 
    enclosed in a set of asterisks. 
    RTEXT - specifies that this node should produce an OUT$SYM block 
    incorporating all of the text (and blanks and/or comments) accepted by 
    this node, with no editing or case conversion.  This flag is set if the 
    PARTRGE definition of this node included the (RTEXT) option. 
    SKBL - specifies that blanks (and/or comments) may legally appear after 
    this node.  This flag is set unless the PARTRGE definition of this node 
    included a trailing hyphen. 
    SUBNDS$ - an array of PTRs, which point to the NSUBNDS sub-nodes of this 
    parse node. 
    S_F - specifies that the user wants to be able to post-approve any 
    successful attempts to match this node; set if the user supplied the 
    (SUCC) option in the PARTRGE definition of this node. 
    TYPE - specifies the "major type" of this node.  See the 
    XU_SUBS_C.:LIBRARY file for the permissible values in this field 
    (%TYPE_xxx#). 
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
P$SYM is a structure used to describe an X$PARSE symbol of one sort or 
another.  Symbols include such specific things as: 
decimal integers, PL-6 identifiers, hexadecimal numbers, account identifiers, 
job names, etc.  The P$SYM structure has many sub-fields in common with 
P$NODE; these are documented in the P$NODE structure itself.  The contents of 
the P$SYM structure can be viewed individually by typing: 
!HELP (HOSTLIB) P$SYM field 
Or type ?? to see all field descriptions. 
    COUNT - contains the number of additional characters which are stored in 
    the P$SYM.TEXT field. 
    LEXTYPE - specifies the type of this P$SYM block; that is, the actual type 
    of symbol or lexeme that this block must match.  Values which may appear 
    in this field are defined as %LEX_xxx# in the XU_SUBS_C.:LIBRARY file; 
    examples include %LEX_DECIMAL#, %LEX_OCTAL#, %LEX_JOBNAME#, etc. 
    MAKEUC - contains '1'B to indicate "force this symbol to upper-case when 
    building an output block".  This option is controlled by the MAKEUC option 
    on this node, within the PARTRGE definition. 
    MAXL - specifies the maximum length of the symbol that may be accepted by 
    this node.  If this field contains 0, or is not present (P$SYM.XTRA='0'B), 
    a symbol of up to 511 characters may be accepted. 
    TEXT - contains 0 or more additional characters, which may appear within a 
    string accepted by this P$SYM block.  For example, the PARTRGE definition 
    "TOUCHTONE=.decimal+'#*'" would have the following values:  XTRA='1'B, 
    MAXL=0, COUNT=2, TEXT='#*'; X$PARSE would accept any string composed of 
    the digits 0 through 9 and/or the characters '#' and/or '*' as being a 
    legal "TOUCHTONE" entry. 
    TYPE - identifies this node as a P$SYM.  This field always contains the 
    value %TYPE_LEXEME# as found in XU_SUBS_C.:LIBRARY. 
    XTRA - indicates that this P$SYM structure contains extra information 
    (i.e., a maximum length count MAXL, and/or a set of additional legal 
    characters "TEXT").  If this flag is not set, the MAXL, COUNT, and TEXT 
    sub-fields do not exist within this P$SYM structure, and should not be 
    examined. 
00001
00002
00003
00004
00005
00006
00007
The contents of the PARAM structure, generated via the PARSE$PARAM macro, can 
be viewed individually by typing: 
!HELP (HOSTLIB) PARAM field 
Or type ?? to see all field descriptions. 
    ACCEPT    can be set by the U$ routine to indicate that X$PARSE is to 
    resume parsing at the position indicated by PARSE_PARAM.CHARPOS.  If 
    ACCEPT is set, both REJECT and RETRY must be reset. 
    NOTE:  If this node is a failure, no output blocks will have been 
    generated if it is a symbol, literal, or delimited string. 
    CHARPOS    contains an index into the T buffer.  If TYPE=FAIL#, CHARPOS 
    indicates the text in the buffer for which X$PARSE could find no match to 
    a syntax definition.  If TYPE=PRE# or SUCC#, CHARPOS indicates the 
    character which X$PARSE will examine next.  If TYPE=INPUT#, CHARPOS 
    indicates the position of the continuation indicator (semi-colon which is 
    replaced with a blank). 
    If the user's routine changes CHARPOS, the new value of CHARPOS will 
    effect further parsing for the current node and all nodes referenced by 
    the current node.  It will have no effect on nodes at a higher level if 
    the current node should fail to parse successfully. 
    CODE    if PARSE_PARAM.TYPE = %PRE#, %SUCC#, or %FAIL#, this field will 
    contain the "node code" value of the syntax node being parsed. 
    GLOBAL$    is an internal pointer used by X$PARSE. 
    NODE$    is a pointer to the current parse node. 
    OUT$    is a pointer to the output block (OUT$BLOCK or OUT$SYM) just 
    created by X$PARSE.  If there is no block, OUT$=ADDR(NIL). 
    PCB$    points to the P_PCB structure which controls this parsing 
    operation. 
    REJECT    can be set by the U$ routine to indicate that X$PARSE is to 
    resume parsing at the position indicated by PARSE_PARAM.CHARPOS, as though 
    the current node failed.  The output block associated with the node is 
    deleted. 
    NOTE:  If the user's routine was called with PARSE_PARAM.TYPE=%SUCC# and 
    the user wishes to reject the successful match (and force X$PARSE to try 
    other alternatives), the user must set PARSE_PARAM.CHARPOS equal to 
    PARSE_PARAM.OUT$->OUT$BLK.CPOS before returning to X$PARSE.  If this is 
    not done, X$PARSE will discard the characters which had been successfully 
    matched. 
    RETRY    can be set by the U$ routine to indicate that X$PARSE should 
    retry parsing of the node at the position indicated by 
    PARSE_PARAM.CHARPOS. 
    TYPE    is set to indicate the condition which caused the call to the U$ 
    routine.  The EQUs defined to represent these conditions are available in 
    the XU_SUBS_C file:  PRE#, SUCC#, FAIL#, INPUT#, and SPACE#. 
    USER$    points to an (optional) user-owned block of data, as originally 
    identified by P_PCB.USER$.  Management of this block of data is entirely 
    up to the user's routine(s). 
    WKSZ    on entry to the user's routine, this field contains the current 
    size (in words) of the parse work area.  If the user's routine has been 
    called with PARSE_PARAM.TYPE=%SPACE#, the user's routine may extend the 
    work area, and set the WKSZ field equal to the new (larger) size. 
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
OUT$BLK
PARAM
OUT$SYM
XUP
PARAM
The parsing tools consist of the following: 
1.  The X$PARSE library service and related macros. 
2.  The PARse TRee GEnerator, PARTRGE.:SYS, which produces an object unit 
    consisting of parse nodes (i.e., a syntax definition tree).  This object 
    unit can be linked with the object unit that calls X$PARSE.  For 
    information on the PARTRGE metalanguage and use of the PARTRGE processor, 
    type !HELP (PARTRGE). 
3.  PARSE.X which displays output blocks created by input to X$PARSE for 
    testing purposes.  Type !HELP (PARSE.X) for details. 
The structures P$NODE, P$LIT, P$SYM, and P$DSTR are generated by PARTRGE. 
These structures are of interest for debugging purposes. 
P_PCB
    The X$PRE_PROCESS service performs substitutions for preprocessor 
    expressions.  For example, 
    !LET LINK = 'LINK A,B,C,D OVER FRED' 
    !%LINK 
provides substitution of the string for %LINK, thus allowing abbreviation of 
frequently used long commands.  Preprocessing also permits more complex 
substitutions such as 
    !FORTRAN %$INPUT('What fid?') OVER OUT (NLS) 
In this example the user is prompted with 'What fid?' by the built-in function 
$INPUT.  The user's input is substituted into the command.  If the user had 
entered 'TEST', then the command would be: 
    !FORTRAN TEST OVER OU (NLS) 
In this case, X$PRE_PROCESS calls X$EVAL to process the built-in function 
$INPUT. 
The parameters of the P_PCB structure can be viewed individually by typing: 
!HELP (HOSTLIB) P_PCB parameter 
Or type ?? to see all parameter descriptions. 
    BLANKONLY - VALUE-DEC(1) is a flag that is meaningful only upon return 
    from a call to X$PARSE in which the "next alternatives, please" flag 
    (P_PCB.NXT) was set.  P_PCB.BLANKONLY will be set if the only legal 
    alternative that the parser located was a "required blank", and will be 
    reset if anything other than a "required blank" would be legal at the 
    point of error. 
    C = {YES|NO}    is a flag for compression of output blocks.  Setting this 
    flag produces the most compact output from X$PARSE.  If it is essential to 
    produce output that exactly matches the syntax definition tree, this flag 
    can be reset.  C initializes P_PCB.CMPRS.  Default = YES (compress the 
    tree). 
    CNTU = {YES|NO}    is a flag which indicates that X$PARSE is to regard the 
    semi-colon as the continuation indicator.  When this flag is set and 
    continuation is detected, X$PARSE gives control to the user routine named 
    by U$.  This parameter is used to initialize P_PCB.CONTINUE.  Default = 
    YES. 
    COMMENT - Specifies the character(s) which introduce and terminate 
    comments within a command. 
    C_LD = VALUE-CHAR(2)    is the 2-character value of the leading delimiter 
    of comments included in command input.  A single character delimiter must 
    include a leading blank.  If this field is completely blank, X$PARSE 
    assumes that the command may not contain comments of any sort.  Default = 
    ' "'. 
    C_TL = VALUE-CHAR(2)    is the 2-character value of the trailing delimiter 
    of comments included in command input.  A single character delimiter must 
    include a leading blank.  If this field is blank, X$PARSE assumes that 
    comments are terminated only by the end of the command (and thus cannot 
    appear in the middle of a command).  Default = ' "'. 
    DYNAMIC = {YES|NO}    specifies whether (YES) or not (NO) the user's U$$ 
    routine is capable of expanding the PARSE work area dynamically if X$PARSE 
    runs out of space.  This parameter initializes P_PCB.DYNMEM.  Default = 
    NO. 
    ERROR - VALUE-BIT(36)    contains an error code in standard error code 
    format.  If X$PARSE is unable to successfully parse its input string, it 
    stores an error code in P_PCB.ERROR and performs an ALTRETURN.  The 
    possible error codes and descriptions of the conditions producing the 
    error codes are included later in this section. 
    HINODE$ - PTR    points to a structure (P$NODE, P$LIT, P$SYM, or P$DSTR 
    available in XU_MACRO_C.:LIBRARY) which corresponds to the last node 
    successfully parsed, except in the case of P_PCB.ERROR.CODE = %E$BADNODE. 
    In that case HINODE$ points to a node which X$PARSE has decided is illegal 
    (is malformed, performs an immediate left recursion, or is located at 
    ADDR(NIL) or at location 0 within the user's instruction segment). 
    HI_CHAR - VALUE-DEC(0-(2**18-1))    upon return from X$PARSE, 
    P_PCB.HI_CHAR contains the index into the text string (pointed to by 
    P_PCB.TEXT$) of the last character successfully parsed.  If X$PARSE 
    ALTRETURNs, the character(s) immediately following the HI_CHAR position 
    are the ones which X$PARSE was unable to parse successfully. 
    KEYSCAN = {YES|NO}    if set YES, requests that X$PARSE make available a 
    list of literals (keywords) which are legal at the point at which a 
    previous parse failed. 
    The KEYWORDS flag (set by KEYSCAN=YES) is meaningful only if P_PCB.NXT is 
    set (that is, X$PARSE is being asked to determine the literals and lexemes 
    which would be legal at the point at which a previous parsing operation 
    failed due to a syntax error).  If NXT='1'B and KEYWORDS='1'B, X$PARSE 
    will not display the list of literals and lexemes; instead, it will 
    construct a table of literal information and pointers (formatted per 
    P$KEYWORDS), and will set P_PCB.OUT$ equal to the ADDR of this P$KEYWORDS 
    table. 
    N# = VALUE-DEC(1-(2**20-1))    is the number of characters in the text 
    string to be parsed.  N# is used to initialize the P_PCB.NCHARS field. 
    Default = 0. 
    NBL = {YES|NO}    is a flag which indicates that X$PARSE is to disallow 
    blanks, comments, or continuation before the first syntactical element is 
    encountered.  This parameter initializes P_PCB.NOLEADBLANKS.  Default = 
    NO. 
    NX = {YES|NO}    is a flag which indicates that the parser is to display 
    the legal alternatives, after a parse failure occurs.  This parameter 
    initializes P_PCB.NXT.  Default = NO. 
    NOTE:  When X$PARSE is called with NXT set to '1'B, this option will 
    function correctly if the following conditions hold true: 
    o   P_PCB.WKSZ, P_PCB.WK_USED, and P_PCB.HI_CHAR must contain the same 
    values that they held at the time X$PARSE ALTRETURNed with a "Syntax 
    error" code in P_PCB.ERROR; 
    o   P_PCB.ROOT$ must point to the same node as it did during the 
    unsuccessful parsing operation; 
    o   The behavior of the user's U$$ routine (which services pre-parsing, 
    success- and failed-node intervention, and other useful functions) must be 
    identical to its behavior during the original (unsuccessful) parsing 
    operation. 
    OUT$ - PTR    upon a successful return from X$PARSE, OUT$ points to the 
    root of a tree of blocks built by the parser, which contain the result of 
    the parsing operation. 
    OUTDCB = DCBNAME    specifies the DCB to be used to produce the list of 
    alternatives constructed as a result of setting the NX flag.  This 
    parameter initializes P_PCB.OUTDCB#.  Default = NIL. 
    If OUTDCB and OUTENT$ are both NIL, the list of alternatives is written 
    through M$DO. 
    OUTENT = ENTRY    contains the address of an (optional) user-supplied 
    output routine.  If present, this routine will be called by X$PARSE to 
    display legal syntax alternatives when P_PCB.NXT is set to '1'B.  This 
    routine will be entered with one parameter consisting of a single string 
    of 80 characters which will contain a set of possible keywords or a line 
    of text describing a lexeme. 
    If OUTDCB is not NIL, the list of alternatives is written through the 
    specified DCB (OUTENT$ is ignored).  If OUTENT$ and OUTDCB are both NIL, 
    the list of alternatives is written through M$DO. 
R = VARIABLE    specifies the root node of the syntax definition tree. 
    ADDR(R) is used to initialize the P_PCB.ROOT$ pointer.  Default = NIL. 
    T = VARIABLE    specifies the buffer containing the text string to be 
    parsed.  ADDR(T) is used to initialize the P_PCB.TEXT$ field.  Default = 
    NIL. 
    U$ = ENTRY    specifies the user routine to receive control at these 
    times: 
       1.  Prior to the initiation of the parse of any specified node. 
       2.  Upon successful termination of the parse of any specified node. 
       3.  Upon failure to parse the node. 
       4.  Upon detection of the continued-record condition (see the CNTU 
           parameter). 
       5.  When space is to be added to the work area. 
    The calling sequence for the U$ routine is 
    CALL p_pcb.U$$ ( parse_param ); 
    where: 
    parse_param    is a PARSE$PARAM parameter block. 
    ENTADDR(U$) is used to initialize P_PCB.U$$.  Default = NIL. 
    USERPTR = VARIABLE    points to an optional user-owned block of memory. 
    If this pointer is non-NIL when X$PARSE is called, the indicated block of 
    memory will be passed (as a parameter) to the user's parse-intervention 
    routine (identified by P_PCB.U$$).  ADDR(USERPTR) is used to initialize 
    P_PCB.USER$.  Default = NIL. 
    VERSION_CODE - VALUE-BIT(1)    specifies which version of the P_PCB 
    structure this is.  The C00 and later versions of X$PARSE use a 
    VERSION_CODE of 1.  The user should not alter this field. 
    W = VARIABLE    specifies an area in the user's work space for use as a 
    scratch space by X$PARSE and for the output blocks generated for the 
    command text.  The work space should be equal to the minimum number of 
    characters expected plus 10 words.  ADDR(W) is used to initialize the 
    P_PCB.WORK$ pointer. Default = NIL. 
    WK_USED - VALUE-DEC(0-(2**18-1))    upon a successful return from X$PARSE, 
    this field contains the number of words from the beginning of the W 
    buffer, which are in use by the output blocks generated by X$PARSE. 
    NOTE:  This information is accurate only on normal return from X$PARSE. 
    WSZ = VALUE-DEC(0-(2**18-1))    specifies the size, in words, of the work 
    area defined by W.  WSZ is used to initialize P_PCB.WKSZ.  Default = 0. 
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
NOTATION
The following examples show how a given timespan appears when formatted with 
different pictures: 
Picture                 Formatted Result 
-------                 ---------------- 
DDDD.HH:MM:SS.TT        18:15:30.50 
HHHH "Hours"            18 Hours 
MMMM "min," S "sec"     2175 min, 30 sec 
TTTTTTTTTT              13053050 
Timespan pictures are similar to time pictures.  The following subfield 
identifier characters are recognized: 
    D   the number of days 
    H   the number of hours 
    M   the number of minutes 
    S   the number of seconds 
    T   the number of hundredths of seconds 
The subfields must appear in the order shown.  One or more subfields may be 
omitted from either or both ends of the list.  The first subfield character 
used may be repeated up to ten times to indicate the number of digits to 
reserve for the subfield.  Subsequent subfields may be indicated by one or two 
characters each, and have the same meaning as they would in a time picture. 
Rules for punctuation are the same as for dates and times. 
If the value is negative, the first digit of the first subfield is replaced by 
a (-) minus sign.  A plus (+) sign is also recognized, but is never generated. 
    The update file consists of records in sequential order.  The source 
    update routines perform no sorting. 
    The update file consists of two types of records, (1) "plus" records which 
    designate where source updates are to be made, and (2) text records which 
    supply new source lines.  For a description of 'plus' record forms, type: 
    HELP (HOSTLIB) UPDATE_FILE_FORMAT form 
    where form is one of the following:  INSERT, DELETE_AND_REPLACE, 
    END_OF_UPDATES, START_OF_UPDATES, or COMMENT. 
  Plus Record Format                Explanation 
  +i  comment 
                                    Inserts the text records following it 
                                    after line i of the base source file. 
                                    Example:  161.000 +161 JFR 8/14/79 
                                              161.010 text 
                                    The text record (161.01) in the update 
                                    file is added following the 161st record 
                                    in the base source file. 
  +j,k  comment 
                                    Deletes lines j through k and inserts the 
                                    text records following it (if any) in 
                                    place of the lines j through k in the base 
                                    source file. 
                                    NOTE:  k must be equal to or greater 
                                           than j. 
                                    Example:  400.00 +400,401  JFR 8/14/79 
                                              400.010 text 
                                              400.020 text 
                                    Deletes lines 400 to 401 in the base 
                                    source file and replaces them with 400.01 
                                    and 400.02 from the update file. 
                                    Example:  480.000 +480,480 
                                              520.000 +502,502 
                                              502.010 text 
                                    Deletes line 480 in the base source file. 
                                    Since the update file contains no text 
                                    records between 480 and 502, no record 
                                    replaces the deleted record in the base 
                                    source file.  Deletes line 502 in the base 
                                    source file and inserts line 502.01 from 
                                    the update file. 
  +END 
                                    End of updates.  +END is assumed on 
                                    end-of-file for the update file. 
  +0 
                                    Is assumed if the update file does not 
                                    start with a "plus" record. 
  +*  comment 
                                    Comment record.  A comment record may 
                                    appear anywhere within the update file and 
                                    is ignored by source update services. 
The following relationships are permissible in the update file. 
 +i 
     . 
     . 
 +j,k 
     . 
     . 
 where i < j < k 
 +i,j 
    . 
    . 
 +k 
    . 
    . 
    . 
where i < J < k 
 +i 
    . 
    . 
 +j 
    . 
    . 
    . 
where i < j 
 +i,j 
    . 
    . 
 +k,l 
    . 
    . 
    . 
where i < j < k < l 
 +i,j 
 . 
 . 
 . 
 +j 
 . 
 . 
 . 
where the base file contains exactly j records. 
 +0 
    . 
    . 
where the +0 record, if used, must be the first 
record in the update file. 
The following constructs are illegal in an update file: 
 +i 
 . 
 . 
 . 
 +i 
 . 
 . 
 . 
(that is, duplicate +i records are not permitted). 
 +0,j 
 . 
 . 
 . 
(that is, +0,j is illegal). 
 +j 
 . 
 . 
 . 
(or) 
 +i,j 
 . 
 . 
 . 
(where j is beyond the end of the base file is illegal). 
00005
00002
00003
00001
00004
Format: 
CALL X$DEC_CONVERT (textc$,value) ALTRET (label); 
Parameters: 
textc$    points to the TEXTC string that is to be converted. 
value    returns an SBIN WORD value. 
Description: 
The X$DEC_CONVERT service converts a text string to a decimal value.  The 
decimal value must be no greater than 34359738367, which can be accommodated 
in one word. 
Error Conditions: 
If X$DEC_CONVERT discovers that the value to be converted cannot be 
accommodated in one word or contains an illegal character, it takes the 
alternate return. 
00002
00003
00001
Format: 
CALL X$EVAL (xue_ecb) ALTRET (label); 
Parameters: 
xue_ecb    specifies a structure generated by the XUE_ECB macro.  Significant 
parameters in that structure are:  TREE, WORK, WKSZ, and WORK_DCB; FUN (if a 
User-Defined Functions Routine is used), VAR (if a User-Managed Command 
Variables Routine is used), USER (to provide user data to user-defined 
functions or user-managed command variables routine), PROCNAME and PROCACCT 
(if private command variables are used), CMDVAR, PRIVATE. 
Description: 
The X$EVAL service evaluates an expression contained in the parse tree created 
by X$PARSE and returns a standard TEXTC string stored in a work area that the 
user supplies.  On return from X$EVAL, the significant fields in XUE_ECB are 
XUE_ECB.OUT$ and XUE_ECB.RESULTS.PROMPT#. 
The X$EVAL service provides options to permit processing of user-defined 
functions and command variables.  Those options are explained further below. 
o   User-Defined Function processing. 
    If the user provides for user-defined functions, X$EVAL gives control to 
    the User-Defined Functions Routine when such a function is encountered in 
    command text.  This routine executes the appropriate function and returns 
    information to X$EVAL. 
    When the User-Defined Functions Routine is invoked, the structure 
    XUE_FUNPARAM identifies which specific user-defined function is to be 
    performed, and XUE_FUNPARAM and XUE_OPTION provide access to any 
    expressions entered with the user-defined function. 
    The significant fields passed to the User-Defined Functions Routine are as 
    follows:  XUE_FUNPARAM.CODE# (identifies which user-defined function to 
    perform), XUE_FUNPARAM.NOPTS# and XUE_FUNPARAM.OPTION$ (to provide access 
    to any XUE_VALUEs entered along with the user-defined function in the 
    command text), XUE_FUNPARAM.CPOS#, XUE_OPTION.CODE# (identifies the option 
    associated with the XUE_VALUE). 
    At successful completion, a user-defined function should ensure that 
    XUE_FUNPARAM.OUT$ points to the TEXTC results of the user-defined 
    function; the User-Defined Functions Routine then returns control to 
    X$EVAL. 
o   Command Variable processing. 
    A program using command variables has three options:  standard command 
    variables, private command variables, or user-managed command variables. 
    The X$EVAL service assumes standard command variables are used unless: 
    o   XUE_ECB.FLAGS.PRIVATE# is set, meaning private command variables are 
        to be used.  In this case, the fields XUE_ECB.PROCNAME_ and 
        XUE_ECB.PROCACCT_ identify the processor. 
    o   XUE_ECB.FLAGS.CMDVAR# is reset, meaning that user-managed command 
        variables are used.  In this case, XUE_ECB.VAR$$ contains the address 
        of the User-Managed Command Variables Routine. 
    In the case of standard command variables or private command variables, 
    the X$EVAL service calls the M$CMDVAR monitor service to fetch or store 
    variables. 
    When the User-Managed Command Variables Routine is invoked by X$EVAL, the 
    structure XUE_VARPARAM contains a TEXTC representation of the variable 
    name to be manipulated.  The fetch or store code in XUE_VARPARAM.CODE# 
    indicates which function is to be performed.  The field 
    XUE_VARPARAM.VALUE$ points to a TEXTC field that holds the value fetched 
    or stored. 
    At successful completion of the fetch or store, the routine performs a 
    return to X$EVAL. 
Error Conditions: 
If an error is detected, X$EVAL takes the alternate return; in that case, the 
significant fields in XUE_ECB are:  XUE_ECB.ERR_POS#, XUE_ECB.ERR_DCB#, 
XUE_ECB.ERR. 
If an error is detected by the user-defined function, it should perform an 
alternate return to X$EVAL with these fields set:  XUE_FUNPARAM.ERR_POS#, 
XUE_FUNPARAM.ERR_DCB#, XUE_FUNPARAM.ERR.  The error information from 
XUE_FUNPARAM is transferred into XUE_ECB; then X$EVAL performs an alternate 
return to the caller of X$EVAL. 
If an error is detected by the User-managed Command Variables Routine, it 
performs an alternate return to X$EVAL with these fields set: 
XUE_VARPARAM.ERR_POS#, XUE_VARPARAM.ERR_DCB#, XUE_VARPARAM.ERR.  The error 
information from XUE_VARPARAM is transferred into XUE_ECB; then X$EVAL 
performs an alternate return to the caller of X$EVAL. 
Usage Notes: 
1.  The X$EVAL service requires a work area to perform the evaluation 
    function.  The work area is referenced by XUE_ECB.WORK$ and XUE_ECB.WKSZ#. 
    It is recommended that this area be in a dynamic data segment to allow 
    expansion, if required. 
    The amount of work area required varies depending on the functions to be 
    performed by X$EVAL.  These guidelines apply: 
    o   For evaluations not involving user-managed command variables or 
        user-defined functions, approximately 150 words are required. 
    o   For evaluations involving user-defined functions, approximately 100 
        additional words are needed. 
    o   For evaluations involving expressions associated with user-defined 
        functions, an additional 10 words per parameter are required. 
        For example, if a user defined function has eight possible parameters, 
        150 words are needed for the general work area, plus 100 words for the 
        user-defined function, plus 80 words for the parameters; in other 
        words a total of approximately 330 words would be necessary. 
    If a call to X$EVAL results in error because the work area is too small, 
    the work area can be enlarged and the call to X$EVAL can be repeated. 
2.  The system-supplied parse nodes used by X$EVAL have node codes in the 
    range of 1 to 125.  Users of X$EVAL should avoid using codes in this range 
    for their own nodes to avoid potential conflicts. 
00002
00003
00001
00004
Format: 
CALL X$FORMAT (fdsname); 
Parameters: 
fdsname    specifies a structure generated via the F_FDS macro.  This 
structure must contain the following parameters at the time of the call:  FMT, 
BUF, NVECS, VECTR.  Additional optional parameters may also be specified in 
the F_FDS structure. 
Description: 
X$FORMAT scans the FMT string from left to right.  Depending on the contents 
of the string, it operates in one of two modes:  transfer or insertion mode. 
On encountering the % delimiter in the FMT string, it enters insertion mode. 
In that mode it examines the subsequent count(s), flag(s), and insertion code; 
based on those codes it formats the data referenced and moves it to the output 
buffer.  The formatter maintains a pointer to the current data which it 
updates after each format function; the amount of data processed is determined 
by the insertion code.  For instance for numeric insertion codes, the 
preceding CNT(1) value specifies the amount of data to be formatted and moved. 
After processing a format function, X$FORMAT normally scans for the next % 
code.  In this mode, called transfer mode, it simply moves to the output 
buffer any ASCII text characters it encounters.  The ASCII text could include 
spaces, dashes, alphanumeric titles, etc. which are added for readability or 
labeling purposes. 
The formatter scans the FMT string and processes data until the data is 
exhausted.  If the end of the FMT string is reached and data remains, the 
current buffer will be output (via the specified DCB) and the FMT string will 
be scanned again beginning at the rescan point.  If an insertion code 
requiring data is encountered and the data has been exhausted, then the buffer 
will be output and the call to X$FORMAT will be terminated. 
To provide flexibility, several features are available to alter the normal 
sequence of operation: 
o   A repeat feature is provided. 
o   An If-Elseif-Endif feature is provided. 
o   A subroutine feature is provided. 
o   Local variables are available. 
o   A feature to suspend writing of text so that more text can be added during 
    subsequent calls.  \ insertion code.\ 
o   Transfer of control to a user-supplied edit subroutine. 
o   Transfer of control to a user-supplied output subroutine. 
Error Conditions: 
X$FORMAT detects these error conditions: 
UNKNOWN INSERTION CODE - reports an invalid insertion code.  A portion of the 
format text is displayed with a caret beneath the offending character. 
UNBALANCED GROUP CODES - CC, (), OR [?] - reports mismatched group delimiters. 
BAD NUMBER FOR VALUE OR SUBROUTINE - reports a number exceeding 100 or less 
than zero. 
RAN OUT OF DATA VECTORS - reports a format that continued to attempt to access 
data beyond the end of all the data vectors. 
In each error condition, the formatting operation is aborted and a normal 
return is made from X$FORMAT. 
X$FORMAT makes no attempt to validate access to the data supplied via the data 
vectors.  Memory faults may occur if there is an error in the data list. 
00002
00003
00001
Format: 
CALL X$GET_VAR (var_name$, var_value$, xue_ecb[,charpos]) ALTRET (label); 
Parameters: 
var_name$    points to the TEXTC variable name. 
var_value$    points to the 512 byte TEXTC result area. 
xue_ecb    specifies an XUE_ECB structure in which these parameters are 
significant:  CMDVAR, PRIVATE, PROCNAME, PROCACCT, VAR, and USER. 
charpos    is an optional parameter that indicates the location in the source 
string where the variable name (referenced by var_name$) was encountered (SBIN 
WORD). 
Description: 
The X$GET_VAR service gets the value of a specified command variable. 
X$GET_VAR calls M$CMDVAR for standard or private command variables, or the 
user User-Managed Command Variables Routine, as needed. 
Error Condition: 
If the X$GET_VAR service detects an error, it takes the alternate return; in 
that case, these fields are significant:  XUE_ECB.ERR, XUE_ECB.ERR_POS#, 
XUE_ECB.ERR_DCB#. 
00002
00003
00001
Format: 
CALL X$HELP (xuh_param) [ALTRET (label)]; 
Parameters: 
xuh_param    an XUH_PARAM structure. 
Description: 
The X$HELP service displays one or more messages from a HELP database, or 
retrieves information about the database itself.  X$HELP proceeds as follows: 
1.  If MORE and ALL are both set, ALL is used and no other parameters are 
    meaningful. 
2.  If MORE is set, then it is used and no other parameters are meaningful. 
3.  If TOPICS is set, then it is used and no other parameters are meaningful. 
4.  If the HELP parameter is given, the text of the HELP command is used; 
    other parameters in the XUH_PARAM block are meaningful with the exception 
    of MORE, ALL, TOPICS, and KEYWORD. 
5.  If no HELP pointer is given, the KEYWORD parameter is used to determine 
    what is to be accessed from the data base. 
Usage Note: 
The HELP database allows an unlimited number of topic names.  However, there 
is a limit of 512 subtopics and each of these subtopics is limited to 512 
lines of text. 
00002
00001
00003
Format: 
CALL X$PARSE (pcbname) ALTRET (label); 
Parameters: 
pcbname    specifies the Parse Control Block generated via the P_PCB macro. 
Use the topic P_PCB for details.  For information on creating the syntax 
definition tree (user parse nodes) which is specified via the Parse Control 
Block, see !HELP (PARTRGE). 
Description: 
The X$PARSE service performs these functions: 
1.  Creates an output tree which more or less parallels the user's parse nodes 
    (i.e., syntax definition tree).  The output tree is available via a 
    pointer (OUT$) in the Parse Control Block which locates the first block. 
2.  Detects and ignores comments in the input string. 
3.  Detects continuation indicator (the semi-colon character), if the Parse 
    Control Block specifies CNTU=YES.  At a semi-colon, X$PARSE passes control 
    to the user (at the location identified by U$ in the Parse Control Block) 
    for further input.  Parsing resumes after the caller supplies additional 
    text input. 
4.  Interacts with the caller, if requested.  Intervention can be requested 
    via the parse node definitions, before or after parsing of the node 
    occurs.  Intervention can also be requested via the PCB at the call to 
    X$PARSE for conditions such as command continuation and parser work area 
    expansion.  Parameters are passed between X$PARSE and the user 
    intervention procedure via a structure (PARAM) that may be generated via 
    the PARSE$PARAM macro. 
Error Conditions: 
X$PARSE detects the following error conditions and takes the specified 
alternate return.  The error code is specified in P_PCB.ERROR in standard 
error code format. 
Error Name       Meaning 
E$SYNERR         X$PARSE failed to match any branch of the syntax tree. 
E$NULLROOT       Caller did not supply the pointer to the syntax tree. 
E$BADNODE        An undefined node type was encountered in the syntax tree. 
E$WKOVERFLOW     The work area is too small to contain the output. 
E$SMALLWORK      The work area is not large enough to begin the parse. 
E$NULLU$$        The caller did not provide a U$ routine. 
00002
00003
00001
Format: 
CALL X$PRE_PROCESS (xue_ppcb) ALTRET (label); 
Parameters: 
xue_ppcb    specifies a structure generated by the XUE_PPCB macro. 
Significant parameters in that structure are:  INBUF, ICHARS, OUTBUF, OCHARS, 
ROOT, and all XUE_ECB except TREE. 
Description: 
The X$PRE_PROCESS service receives command text in an input buffer and 
performs the necessary substitutions for a %expression; it returns the command 
text with substitutions in an output buffer.  The input and output buffers may 
be the same physical memory.  The XUE_PPCB structure passed to X$PRE_PROCESS 
contains a copy of XUE_ECB to permit X$PRE_PROCESS to call X$EVAL for 
evaluation functions.  After successful preprocessing, the following fields in 
XUE_PPCB are significant:  XUE_PPCB.OUTBUF$ and XUE_PPCB.RCHARS#. 
Error Condition: 
If X$PRE_PROCESS detects an error, it takes the alternate return.  Error 
information is contained in XUE_PPCB.ECB.ERR, XUE_PPCB.ECB.ERR_POS#, and 
XUE_PPCB.ECB.ERR_DCB#.  In case of an error, the output buffer rather than the 
input buffer should be echoed. 
00002
00003
00001
Format: 
CALL X$PUT_VAR (var_name$, var_value$, xue_ecb[,charpos]) ALTRET (label); 
Parameters: 
var_name$    points to the TEXTC variable name. 
var_value$    points to the 512 byte TEXTC result area. 
xue_ecb    specifies an XUE_ECB structure in which these parameters are 
significant:  CMDVAR, PRIVATE, PROCNAME, PROCACCT, VAR, and USER. 
charpos    is an optional parameter (SBIN WORD) that indicates the location in 
the source string where the variable name (referenced by var_name$) was 
encountered. 
Description: 
The X$PUT_VAR service stores a value in a specified command variable. 
X$PUT_VAR calls M$CMDVAR for standard or private command variables, or the 
user User-Managed Command Variables Routine, as needed. 
Error Conditions: 
If the X$PUT_VAR service detects an error, it takes the alternate return; in 
that case, these fields are significant:  XUE_ECB.ERR, XUE_ECB.ERR_POS#, 
XUE_ECB.ERR_DCB#. 
00002
00003
00001
Format: 
CALL X$STRIP_BLANKS (textc$); 
Parameters: 
textc$    points to the TEXTC string to be stripped. 
Description: 
The X$STRIP_BLANKS service strips the leading and trailing blanks from a TEXTC 
string. 
00002
00001
Format: 
CALL X$WILDCMP (xuw_wildcard) ALTRET (label); 
Parameters: 
xuw_wildcard    specifies a structure generated by the XUW_WILDCARD macro. 
Significant parameters in that structure are PATTERN and INPUT. 
Description: 
The X$WILDCMP service compares a wildcarded pattern string with an input 
string and returns the results in XUW_WILDCARD.ERROR.ERR#.  If the pattern 
string and input string match, XUW_WILDCARD.ERROR.ERR# will be set to 
E$XUW#WILD_OK and the normal return will be taken. 
In the pattern string, sequences of ? characters are treated as a single ? 
character.  For example, the pattern string A??B? is equivalent to A?B?. 
Error Conditions: 
On an alternate return, XUW_WILDCARD.ERROR.ERR# will be set according to the 
values given in XUW Error Codes. 
00002
00003
00001
Format: 
CALL X$WILDFMT (xuw_wildcard) ALTRET (label); 
Parameters: 
xuw_wildcard    specifies a structure generated by the XUW_WILDCARD macro. 
Significant parameters in that structure are PATTERN, INPUT, TEMPLATE, and 
OUTPUT. 
Description: 
The X$WILDFMT service compares a wildcarded pattern string with an input 
string.  If a match is found, an output string is formed using the input and 
template strings.  On a normal return, XUW_WILDCARD.ERROR.ERR# will be set to 
E$XUW#WILD_OK. 
In the pattern string, sequences of ? characters are treated as a single ? 
character.  For example, the pattern string A??B? is equivalent to A?B?.  In 
the template string, however, sequences of ? characters are treated as 
multiple ? characters.  For example, an input string AXBY (that matches the 
pattern string A?B?) formatted according to the template string C??D appears 
as CXYD. 
Note:  If the output string is zero-length, X$WILDFMT does not ALTRET.  The 
user is responsible for checking the length of the output string, since this 
is considered normal in many cases. For example: 
    pattern = 'XX?'        template = '?' 
    input   = 'XX'         output   = ' ' 
Error Conditions: 
On an alternate return, XUW_WILDCARD.ERROR.ERR# will be set according to the 
values indicated in XUW Error Codes. 
00002
00003
00001
Format: 
CALL X$WRITE (fdsname,VECTOR(fmt)[,dv1[,dv2]...[,dv20]]; 
Parameters: 
fdsname    specifies a structure generated via the F_FDS macro.  This 
structure must contain the BUF parameter at the time of the call and may 
contain additional optional parameters. 
fmt    locates the format (FMT) string to be used.  This vector is stored in 
the structure identified by fdsname when X$WRITE is performed. 
dv    is a vector that frames an item of data to be formatted.  Up to 20 
vectors may be specified.  Any data vector specified is stored in the 
structure identified by fdsname as an array when X$WRITE is performed and the 
number of vectors is stored in that structure also. 
Description: 
The X$WRITE service sets up the F_FDS structure and calls the X$FORMAT 
service.  This services provides a simpler method of calling the Formatter. 
Error Conditions: 
For a description of error conditions, type: 
HELP (HOSTLIB) X$FORMAT ERROR 
00002
00003
00001
The Fast Sequential File Access method (FSFA) exists as a set of library 
routines which may be used to access records from CONSEC, KEYED, RELATIVE, 
INDEXED, or IREL disk files in a sequential manner.  The primary advantage of 
using XSA routines is the substantial reduction of monitor service call time 
at the expense of functions available. 
XSA services include: 
    Service           Description 
    -------           ----------- 
    XSA$CLOSE         close file 
    XSA$OPEN          open file and determine suitability to Fast 
                      Sequential File Access 
    XSA$PFIL          position file 
    XSA$PRECORD       position file by record 
    XSA$READ          read file 
    XSA$WRITE         write file 
Each of these services has two parameters, the FPT which would ordinarily be 
used with the standard monitor service and a parameter block, XSA_PARAM. 
Format: 
CALL XSA$CLOSE (fpt_close,xsa_param) ALTRET (label); 
Parameters: 
fpt_close    is the standard M$CLOSE FPT. 
xsa_param    is an XSA_PARAM structure in which BBUF and KBUF have not been 
modified by the user after the XSA$OPEN call. 
Description: 
The XSA$CLOSE service closes a specified file.  XSA$CLOSE must be called with 
DISP=SAVE when a newly created file is to be closed to ensure that the file 
remains intact. 
Error Conditions: 
On an alternate return, the service returns XSA_PARAM.ERR, an error code in 
standard CP-6 error code format. 
00002
00003
00001
Format: 
CALL XSA$OPEN (fpt_open,xsa_param) ALTRET (label); 
Parameters: 
fpt_open    is the standard M$OPEN FPT. 
xsa_param    is an XSA_PARAM structure that can be initialized with the BBUF 
and KBUF parameters but no other parameters should be specified. 
Description: 
The XSA$OPEN service opens a specified file and determines if it is suitable 
for FSFA.  The criteria are as follows: 
1.  The file must be accessed sequentially (ACS = SEQUEN). 
2.  The file must have an organization (ORG) of CONSEC, KEYED, RELATIVE, 
    INDEXED, or IREL. 
3.  FUN must be IN except for CONSEC files for which FUN can be CREATE (CTG = 
    NO). 
4.  The file can not be compressed (COMP = NO). 
5.  The file must be a disk file. 
6.  The file can not be opened SHARE = ALL. 
If a file does not meet the above criteria, the XSA services can still be 
used, but there is no advantage. 
Neither KBUF nor BBUF needs to be specified on the XSA$OPEN call if the user 
desires to only get buffer space when files are indeed suitable for FSFA. 
On a normal return, the XSA$OPEN service returns information in the parameter 
block as follows: 
    XSA_PARAM.ORG = VALUE-DEC(0-?)    is zero if the file was not suitable for 
    FSFA.  Subsequent calls to XSA services only cause the FPT to be passed to 
    the appropriate monitor service.  In this case, results of the call 
    (ARS#,DVBYTE) are returned in XSA_PARAM.  If the file is suitable for 
    FSFA, ORG is set from the DCB, and XSA$ calls must be used to access 
    records from the file.  Buffers must be specified on subsequent XSA$ calls 
    and must not be modified between calls.  KBUF is only necessary if ORG is 
    KEYED, INDEXED, or IREL. 
Error Conditions: 
On an alternate return, the service returns XSA_PARAM.ERR, an error code in 
standard CP-6 error code format. 
00002
00003
00001
Format: 
CALL XSA$PFIL (fpt_pfil,xsa_param) ALTRET (label); 
Parameters: 
fpt_pfil    is the standard M$PFIL FPT.  Only the BOF parameter is significant 
for XSA file access. 
xsa_param    is an XSA_PARAM structure in which BBUF and KBUF have not been 
modified by the user after the XSA$OPEN call. 
Description: 
The XSA$PFIL service positions to the beginning or end of a file.  The 
XSA$PFIL service may be used for Consecutive, Keyed, Indexed, IREL, and 
Relative files.  This service is primarily useful when positioning to the 
beginning of a scratch file which has just been created using XSA$WRITE. 
If the BBUF in XSA_PARAM is set and the vector is NIL or ERASE, the fast mode 
will be overridden and all subsequent processing will revert to normal monitor 
calls.  In this case, the file will be closed, re-opened, and re-positioned 
prior to issuing the monitor service call. 
Error Conditions: 
On an alternate return, the service returns XSA_PARAM.ERR, an error code in 
standard CP-6 error code format. 
00002
00003
00001
Format: 
CALL XSA$PRECORD (fpt_precord,xsa_param) ALTRET (label); 
Parameters: 
fpt_precord    is the standard PRECORD FPT.  Only the N and KEY (if KEYR=YES) 
parameters are significant for XSA file access. 
xsa_param    is an XSA_PARAM structure in which BBUF and KBUF have not been 
modified by the user after the XSA$OPEN call. 
Description: 
The XSA$PRECORD service positions forward by the specified number of records. 
Specifying KEYS=YES or N<=0 when calling XSA$PRECORD causes processing to 
revert to normal monitor service calls. 
On a normal return, the XSA$PRECORD service returns information in the 
parameter block as follows: 
    XSA_PARAM.ARS#    specifies the number of records skipped. 
Error Conditions: 
On an alternate return, the service returns XSA_PARAM.ERR, an error code in 
standard CP-6 error code format. 
00002
00003
00001
Format: 
CALL XSA$READ (fpt_read,xsa_param) ALTRET (label); 
Parameters: 
fpt_read    is the standard M$READ FPT.  Only the BUF and KEY (if KEYR=YES) 
parameters are significant for XSA file access. 
xsa_param    is an XSA_PARAM structure in which BBUF and KBUF have not been 
modified by the user after the XSA$OPEN call. 
Description: 
The XSA$READ service reads the next sequential record from the file. 
Specifying KEYS=YES when calling XSA$READ causes processing to revert to 
normal monitor service calls.  In addition, if the BBUF in XSA_PARAM is set to 
NIL or ERASE, the fast mode is overridden and all subsequent processing 
reverts to normal monitor calls.  In this case, the files are closed, 
re-opened, and re-positioned prior to issuing the monitor service call. 
On a normal return, the XSA$READ service returns information in the parameter 
block as follows: 
    XSA_PARAM.ARS#    specifies the size of the record in bytes. 
    XSA_PARAM.DVBYTE    contains the record's DVBYTE. 
Error Conditions: 
On an alternate return, the service returns XSA_PARAM.ERR, an error code in 
standard CP-6 error code format. 
00002
00003
00001
Format: 
CALL XSA$WRITE (fpt_write,xsa_param) ALTRET (label); 
Parameters: 
fpt_write    is the standard M$WRITE FPT.  Only the BUF and DVBYTE parameters 
are significant for XSA file access. 
xsa_param    is an XSA_PARAM structure in which BBUF and KBUF have not been 
modified by the user after the XSA$OPEN call. 
Description: 
The XSA$WRITE service writes the next sequential record.  This service can 
only be used for files with ORG = CONSEC and FUN = CREATE. 
Error Conditions: 
On an alternate return, the service returns XSA_PARAM.ERR, an error code in 
standard CP-6 error code format. 
00002
00003
00001
The user supplies parameters to the XSA services in a parameter block.  The 
services also return data to the user in the same block.  The XSA_PARAM macro 
should be invoked to generate the structure of the block. 
The user can use a single parameter block and reset appropriate fields, or can 
generate multiple parameter blocks.  However, the same parameter block must be 
used with all services dealing with a particular DCB since contextual 
information is kept in the parameter block. 
For a description of each parameter, type: 
HELP (HOSTLIB) XSA_PARAM param 
where param is BBUF or KBUF. 
BBUF = VARIABLE    specifies the buffer to be used for data granules.  This 
buffer must be a multiple of 1024 words in size.  A large buffer results in 
fewer monitor service calls.  BBUF_ contains two subfields:  BOUND and BUF$. 
BOUND contains the buffer size minus one; BUF$ is a pointer to the start of 
the buffer.  The default is NIL. 
KBUF = VARIABLE    specifies the buffer to be used for key granules if the 
file is KEYED, INDEXED, or IREL.  This buffer must be 1024 words in size. 
KBUF_ contains two subfields:  BOUND and BUF$.  BOUND contains the buffer size 
minus one; BUF$ is a pointer to the start of the buffer. 
UNFAST = {MONITOR|ALTRET}    specifies whether, when an operation is attempted 
that XSA does not support, to complete the operation using standard monitor 
services (UNFAST=MONITOR), or to take the alternate return to the user 
(UNFAST=ALTRET).  This flag may be set or reset at any time.  The default is 
MONITOR. 
00001
00002
00003
    The XSF services are used to access the File Information Table (FIT). 
    These services are used to set a pointer or index to significant 
    information on specified FIT data. 
    Portions of the File Information Table (FIT) can be viewed by calling the 
    M$OPEN monitor service specifying FPARAM.  XSF services give access to the 
    FIT data returned in the FPARAM buffer. 
    FIT data is organized by sections each of which is associated with a code. 
    The FIT content varies for each file type.  The FIT for one file type may 
    include 02 and 03 data; whereas the FIT for another file type may include 
    03 and 04 data. 
    After file opening, the user calls one of the library services provided to 
    obtain access to the desired data section within the FPARAM buffer.  By 
    invoking a macro for the appropriate data section (e.g., %CODE03;), the 
    user can access the data using the defined names (e.g., CODE03.DESC.QS) 
    for that particular section of the FIT. 
    The FPARAM buffer also includes a header preceding the data section(s). 
    The structure of the header, which may be of interest to some users, can 
    be generated by invoking the FM$FIT macro. 
    XSF services include: 
    XSF$LOCCODE    Sets pointer to a specified FIT data section and 
                   returns the index of the data section in FIT header. 
    XSF$LOCCODP    Sets pointer to a specified FIT section. 
    XSF$LOCCODT    Sets pointer to a specified section only if 
                   there is significant data in the section. 
    XSF$LOCCODX    Returns index of the data section in the FIT header. 
Format: 
CALL XSF$LOCCODE (fit$,code) ALTRET (label); 
Parameters: 
fit$    is a pointer to the beginning of the FPARAM buffer. 
code    contains the UBIN number (1-20) of a FIT data section, right-justified 
in one word. 
Description: 
The XSF$LOCCODE service sets fit$ to point to the FIT data section specified 
and returns in code the index of the specified data section entry in the FIT 
header array (FM$FIT.CODES). 
Error Conditions: 
The alternate return is taken if the data section requested by code is not 
contained in the FPARAM buffer. 
00002
00003
00001
Format: 
CALL XSF$LOCCODP (fit$,code) ALTRET (label); 
Parameters: 
fit$    is a pointer to the beginning of the FPARAM buffer. 
code    contains the UBIN number (1-20) of a FIT data section, right-justified 
in one word. 
Description: 
The XSF$LOCCODP sets fit$ to point to the data section specified.  code is 
left unchanged. 
Error Conditions: 
The alternate return is taken if the data section requested by code is not 
contained in the FPARAM buffer. 
00002
00003
00001
Format: 
CALL XSF$LOCCODT (fit$,code) ALTRET (label); 
Parameters: 
fit$    is a pointer to the beginning of the FPARAM buffer. 
code    contains the UBIN number (1-20) of a FIT data section, right-justified 
in one word. 
Description: 
The XSF$LOCCODT service sets fit$ to point to the data section specified by 
code if there is significant data in the section (i.e., if FM$FIT.CODES.NDW 
for that data section is not zero).  code is left unchanged. 
Error Conditions: 
The alternate return is taken if the data section requested by code is not 
contained in the FPARAM buffer, or if the requested data section contains no 
significant data. 
00002
00003
00001
Format: 
CALL XSF$LOCCODX (fit$,code) ALTRET (label); 
Parameters: 
fit$    is a pointer to the beginning of the FPARAM buffer. 
code    contains the UBIN number (1-20) of a FIT data section, right-justified 
in one word. 
Description: 
The XSF$LOCCODX service returns a value (code) that is an index into 
FM$FIT.CODES (the FIT header array).  fit$ is left unchanged. 
Error Conditions: 
The alternate return is taken if the data section requested by code is not 
contained in the FPARAM buffer. 
00002
00003
00001
    The XUD services provide a facility for handling dates and times that is 
    considerably more flexible than the M$TIME monitor service.  The XUD 
    services feature the following capabilities: 
 o  Conversion of dates and times to and from character strings in a wide 
    variety of formats. 
 o  Support for an internal data type that allows a considerably wider range 
    of values than a UTS, in addition to support for UTS. 
 o  Manipulation of intervals of time, in addition to date and time of day. 
The XUD services are summarized in Table 3-1. 
  Service                    Description 
  XUD$ADD_DATE_TICS 
                             Adds clock ticks to a DATE 
  XUD$ADD_DATE_DATE 
                             Adds two DATEs together. 
  XUD$CHAR_DATE 
                             Converts a character string to a DATE. 
  XUD$CHAR_UTS 
                             Converts a character string to a UTS. 
  XUD$CLOCK_CHAR 
                             Returns the current date and time as a character 
                             string. 
  XUD$CLOCK_DATE 
                             Returns the current date and time as a DATE 
  XUD$CLOCK_UTS 
                             Returns the current date and time as a UTS. 
  XUD$CMPR_DATES 
                             Compares two dates. 
  XUD$DATE_CHAR 
                             Converts a DATE to a character string. 
  XUD$DATE_UTS 
                             Converts a DATE to a UTS. 
  XUD$FROM_DATE 
                             Converts a DATE into days + clock ticks. 
  XUD$INIT_PIC 
                             Initializes a date/time picture. 
  XUD$SUB_DATE_DATE 
                             Subtracts one DATE from another DATE. 
  XUD$SUB_DATE_TICS 
                             Subtracts clock ticks from a DATE. 
  XUD$TO_DATE 
                             Converts days + clock ticks to a DATE. 
  XUD$UTS_ADJUST 
                             Adds a centisecond timespan to a UTS. 
  XUD$UTS_ADJ_25TH 
                             Adds a 1/25th second timespan to a UTS. 
  XUD$UTS_CHAR 
                             Converts a UTS to a character string. 
  XUD$UTS_DATE 
                             Converts a UTS to a DATE. 
  XUD$UTS_DIFF 
                             Subtracts two UTSes, yielding a timespan in 
                             centiseconds. 
  XUD$UTS_DIFF_25TH 
                             Subtracts two UTSes, yielding a timespan in 
                             1/25th second units. 
  XUD$UTS_DIFF_SECS 
                             Subtracts two UTSes, yielding a timespan in 
                             seconds. 
00002
00001
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
Format: 
CALL XUD$ADD_DATE_DATE ( date1, date2 ) ALTRET ( error ); 
Parameters: 
date1   a DATE containing the first addend, and returning the sum 
date2   a DATE containing the second addend 
Description: 
XUD$ADD_DATE_DATE adds two DATEs and replaces the first addend with the sum. 
Rules: 
1.  Both operands may be either a date and time or a timespan.  It is up to 
    the user to treat the result as the appropriate type of value. 
    If both operands are timespans, the result should also be treated as a 
    timespan.  If one operand is a timespan and the other is a date and time, 
    the result should be treated as a date and time.  If both operands are 
    dates, the result is probably not very meaningful. 
2.  The service ALTRETURNs if the sum is outside the range for a DATE.  The 
    result is undefined in this case. 
00002
00001
00003
Format: 
CALL XUD$ADD_DATE_TICS ( date, ticks ) ALTRET ( error ); 
Parameters: 
date    a DATE containing the first addend, and returning the sum 
ticks    an SBIN WORD containing the second addend 
Description: 
XUD$ADD_DATE_TICS adds a binary number of centisecond clock ticks (i.e., 
hundredths of seconds) to a DATE and replaces the DATE with the sum. 
Rules: 
1.  The first operand may be either a date and time or a timespan.  The result 
    should be treated as the same type of value as the first operand. 
2.  The service ALTRETURNs if the sum is outside the range for a DATE.  The 
    result is undefined in this case. 
00002
00001
00003
Format: 
CALL XUD$CHAR_DATE ( XUD_PARAM, char, date ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
char        the character string to be converted 
date        returns the equivalent DATE 
Description: 
This service converts a character string to a DATE. 
Rules: 
1.  The string is treated either as a date and time or a timespan, depending 
    on XUD_PARAM.TIMESPAN. 
2.  The string to be converted can be a fixed length or TEXTC string, 
    depending on XUD_PARAM.TEXTC. 
3.  The string can be converted under control of a picture or using default 
    parsing rules, depending on XUD_PARAM.PIC$. 
4.  If the string does not correspond to the picture, or if there is no 
    picture and the string cannot be recognized as one of the default formats, 
    an appropriate error code is set in XUD_PARAM.ERR and the service 
    ALTRETURNs.  The date returned in this case will have an absolute value of 
    zero (corresponding to midnight on Jan. 1, 1 A.D.).  The same is true if 
    an incorrect picture is provided. 
5.  If the string represents a value outside of the valid range for DATE, the 
    service will set XUD_PARAM.ERR and ALTRETURN with the result set to the 
    minimum or maximum allowable value. 
6.  If the string contains a valid date/time or timespan value, but there are 
    characters left over at the end of the string, XUD_PARAM.ERR is set to 
    E$XUD#EXCESS_CHARS; the service ALTRETURNs, and the date that was parsed 
    is returned. 
00002
00001
00003
Format: 
CALL XUD$CHAR_UTS ( XUD_PARAM, char, uts ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
char        the character string to be converted 
uts         returns the equivalent UTS 
Description: 
This service converts a character string to a UTS. 
Rules: 
1.  The string is treated either as a date and time or a timespan, depending 
    on XUD_PARAM.TIMESPAN. 
2.  The string to be converted can be a fixed length or TEXTC string, 
    depending on XUD_PARAM.TEXTC. 
3.  The string can be converted under control of a picture or using default 
    parsing rules, depending on XUD_PARAM.PIC$. 
4.  If the string does not correspond to the picture, or if there is no 
    picture and the string cannot be recognized as one of the default formats, 
    an appropriate error code is set in XUD_PARAM.ERR and the service 
    ALTRETURNs.  The date returned in this case will have an absolute value of 
    zero (corresponding to midnight on Jan. 1, 1978).  The same is true if an 
    incorrect picture is provided. 
5.  If the string represents a value outside of the valid range for a UTS, the 
    service will set XUD_PARAM.ERR and ALTRETURN with the result set to the 
    minimum or maximum allowable value. 
6.  If the string contains a valid date/time or timespan value, but there are 
    characters left over at the end of the string, XUD_PARAM.ERR is set to 
    E$XUD#EXCESS_CHARS; the service ALTRETURNs, and the date that was parsed 
    is returned. 
7.  Unpredictable results may occur when using timespans in excess of a few 
    years.  If this occurs, use CHAR_DATE to parse the string, and FROM_DATE 
    to get days and centiseconds as binary values. 
00002
00001
00003
Format: 
CALL XUD$CLOCK_CHAR ( XUD_PARAM, char ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
char        returns the current date and time as a character string 
Description: 
This service returns the current date and time as a character string. 
Rules: 
1.  The current date and time can be returned as a fixed length or TEXTC 
    string, depending on XUD_PARAM.TEXTC. 
2.  If XUD_PARAM.PIC$ does not contain the address of a picture to control the 
    conversion, the current date and time is returned in MM/DD/YY format. 
3.  If the receiving field is too short to hold the converted value, 
    XUD_PARAM.ERR is set to E$XUD#SHORT_CHAR and the service ALTRETURNs.  As 
    many subfields and punctuation characters as will fit are returned in the 
    receiving character string. 
4.  If an invalid picture is provided, XUD_PARAM.ERR is set and the service 
    ALTRETURNs with the receiving string cleared to blanks. 
00002
00001
00003
Format: 
CALL XUD$CLOCK_DATE ( XUD_PARAM, date ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
date        returns the current date and time as a DATE 
Description: 
This service returns the current date and time as a DATE.  No picture is 
involved. 
Rules: 
1.  The service supports an ALTRET clause to be consistent with other XUD 
    services, but no errors should be expected. 
00002
00001
00003
Format: 
CALL XUD$CLOCK_UTS ( XUD_PARAM, uts ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
uts         returns the current date and time as a UTS 
Description: 
This service returns the current date and time as a UTS.  No picture is 
involved. 
Rules: 
1.  The service supports an ALTRET clause to be consistent with other XUD 
    services, but no errors should be expected. 
00002
00001
00003
Format: 
CALL XUD$CMPR_DATES ( result, date1, date2 ) ALTRET (error); 
Parameters: 
result  an SBIN WORD that indicates the result of the comparison: 
            -1 indicates date1 < date2 
             0 indicates date1 = date2 
             1 indicates date1 > date2 
date1   a DATE to be compared 
date2   a DATE to be compared 
Description: 
XUD$CMPR_DATES compares two DATEs and returns a signed binary integer that 
indicates the result of the comparison. 
00002
00001
Format: 
CALL XUD$DATE_CHAR ( XUD_PARAM, date, char ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
date        the date to be converted 
char        returns the equivalent character string 
Description: 
This service converts a DATE into a character string. 
Rules: 
1.  The date is converted either as a date and time or a timespan, depending 
    on XUD_PARAM.TIMESPAN. 
2.  The date can be converted to a fixed length or TEXTC string, depending on 
    XUD_PARAM.TEXTC. 
3.  The date can be converted under control of a picture or using default 
    picture, depending on XUD_PARAM.PIC$. 
4.  If the receiving field is too short to hold the converted value, 
    XUD_PARAM.ERR is set to E$XUD#SHORT_CHAR and the service ALTRETURNs.  As 
    many subfields and punctuation characters as will fit are returned in the 
    receiving character string. 
5.  If an invalid picture is provided, XUD_PARAM.ERR is set and the service 
    ALTRETURNs with the receiving string cleared to blanks. 
00002
00001
00003
Format: 
CALL XUD$DATE_UTS ( XUD_PARAM, date, uts ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
date        the DATE to be converted 
uts         returns the equivalent UTS 
Description: 
This service converts a DATE into a UTS.  No picture is involved. 
Rules: 
1.  If XUD_PARAM.TIMESPAN is set, the UTS is treated as a number of 
    centiseconds, not a date and time.  This means that the base value for a 
    UTS is not added to the converted value.  Unpredictable results may occur 
    if the timespan exceeds a few years.  If this occurs, use FROM_DATE to 
    obtain the interval in days and centiseconds. 
2.  If the DATE is outside the UTS range, the service ALTRETURNs with 
    XUD_PARAM.ERR set to indicate overflow or underflow.  The maximum or 
    minimum UTS value will be returned in case of error. 
00002
00001
00003
Format: 
CALL XUD$FROM_DATE ( date, days, ticks ) ALTRET (error); 
Parameters: 
date    the DATE to be converted 
days    returns the number of days in an SBIN WORD 
ticks    returns the number of clock ticks in an SBIN WORD 
Description: 
XUD$FROM_DATE converts a DATE into a number of days and the number of clock 
ticks (i.e., hundredths of seconds). 
Rules: 
1.  If the first operand is a date and time, the number of days since Jan. 1, 
    1 A.D. and the number of clock ticks since midnight on that day will be 
    returned. 
2.  If the first operand is a timespan, the number of full days and the number 
    of clock ticks into the next day will be returned. 
00002
00001
00003
Format: 
CALL XUD$INIT_PIC ( XUD_PARAM, external, internal ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
external    the picture to be initialized 
internal    the initialized picture 
Description: 
Before a picture can be used by a conversion service, it must be translated 
into an internal form in which each subfield identifier is replaced by a 
one-byte code.  This is done automatically by conversion services if the 
XUD_PARAM.INIT_PIC bit is set.  When the same picture will be used repeatedly, 
it is more efficient to initialize it once before it is used with a conversion 
service.  The XUD$INIT_PIC service is provided for this purpose. 
Rules: 
1.  XUD_PARAM.PIC$ is ignored.  Both the uninitialized and internal pictures 
    are specified as parameters. 
2.  The uninitialized picture may be a fixed length or TEXTC string, depending 
    on the XUD_PARAM.PIC_TEXTC bit. 
3.  The internal picture is always a TEXTC string, and is guaranteed not to 
    exceed the size of the uninitialized picture (except for the possible 
    addition of a TEXTC count byte). 
4.  The picture can be initialized as a date/time picture or a timespan 
    picture, depending on XUD_PARAM.TIMESPAN. 
5.  If an error occurs, the service will ALTRETURN with an appropriate error 
    code in XUD_PARAM.ERR.  The contents of the initialized picture are 
    undefined on ALTRETURN. 
00002
00001
00003
Format: 
CALL XUD$SUB_DATE_DATE ( date1, date2 ) ALTRET ( error ); 
Parameters: 
date1   a DATE containing the minuend, and returning the difference 
date2   a DATE containing the subtrahend 
Description: 
XUD$SUB_DATE_DATE subtracts two DATEs and replaces the minuend with the 
difference. 
Rules: 
1.  Both operands may be either a date and time or a timespan.  It is up to 
    the user to treat the result as the appropriate type of value. 
    If both operands are timespans, the result should also be treated as a 
    timespan.  If one operand is a timespan and the other is a date and time, 
    the result should be treated as a date and time.  If both operands are 
    dates, the result should be treated as a timespan. 
2.  The service ALTRETURNs if the result is outside the range for a DATE.  The 
    result is undefined in this case. 
00002
00001
00003
Format: 
CALL XUD$SUB_DATE_TICS ( date, ticks ) ALTRET ( error ); 
Parameters: 
date    a DATE containing the minuend, and returning the difference 
ticks    an SBIN WORD containing the subtrahend 
Description: 
XUD$SUB_DATE_TICS subtracts a binary number of centisecond clock ticks (i.e., 
hundredths of seconds) from a DATE and replaces the DATE with the result. 
Rules: 
1.  The first operand may be either a date and time or a timespan.  The result 
    should be treated as the same type of value as the first operand. 
2.  The service ALTRETURNs if the result is outside the range for a DATE.  The 
    result is undefined in this case. 
00002
00001
00003
Format: 
CALL XUD$TO_DATE ( days, ticks, date ) ALTRET ( error ); 
Parameters: 
days    an SBIN WORD containing a number of days 
ticks    an SBIN WORD containing a number of clock ticks 
date    returns days + ticks as a DATE 
Description: 
XUD$TO_DATE returns a DATE corresponding to a number of days plus a number of 
clock ticks (i.e., hundredths of seconds). 
Rules: 
1.  To return a date and time, a number of days since Jan. 1, 1 A.D. and a 
    number of clock ticks since midnight on that day should be passed. 
2.  To return a timespan, a number of full days and a number of clock ticks 
    into the next day should be passed. 
3.  The service ALTRETURNs if the result is outside the range for a DATE.  The 
    result is undefined in this case. 
00002
00001
00003
Format: 
CALL XUD$UTS_ADJUST ( uts1, uts2, interval ) ALTRET ( error ); 
Parameters: 
uts1        returns the target UTS 
uts2        the source UTS 
interval    the interval to be added to uts2 in an SBIN word 
Description: 
This service computes a new UTS by adding a specified interval (in 
centiseconds) to a source UTS. 
Rules: 
1.  If the result is outside the range of valid UTS values (from 01/01/78 
    00:00:00.00 to 02/06/20 23:59:59.96) the service will ALTRETURN. 
2.  To convert a pre-E03 UTS falling after midnight of 12/31/92 to E03 
    compatible form, use the following code: 
    if UTS > %UTS_CUSP# then 
         call XUD$UTS_ADJUST (UTS, %UTS_CUSP#, UTS-%UTS_CUSP#); 
00002
00001
00003
Format: 
CALL XUD$UTS_ADJ_25TH ( uts1, uts2, interval ) ALTRET ( error ); 
Parameters: 
uts1        returns the target UTS 
uts2        the source UTS 
interval    the interval to be added to uts2 in an SBIN word 
Description: 
This service computes a new UTS by adding a specified interval (in 1/25th of a 
second units) to a source UTS. 
Rules: 
1.  If the result is outside the range of valid UTS values (from 01/01/78 
    00:00:00.00 to 02/06/20 23:59:59.96) the service will ALTRETURN. 
00002
00001
00003
Format: 
CALL XUD$UTS_CHAR ( XUD_PARAM, uts, char ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
uts         the UTS to be converted 
char        returns the equivalent character string 
Description: 
This service converts a UTS into a character string. 
Rules: 
1.  The UTS is converted either as a date and time or a timespan, depending on 
    XUD_PARAM.TIMESPAN. 
2.  The UTS can be converted to a fixed length or TEXTC string, depending on 
    XUD_PARAM.TEXTC. 
3.  The UTS can be converted under control of a picture or using a default 
    picture, depending on XUD_PARAM.PIC$. 
4.  If the receiving field is too short to hold the converted value, 
    XUD_PARAM.ERR is set to E$XUD#SHORT_CHAR and the service ALTRETURNs.  As 
    many subfields and punctuation characters as will fit are returned in the 
    receiving character string. 
5.  If an invalid picture is provided, XUD_PARAM.ERR is set and the service 
    ALTRETURNs with the receiving string cleared to blanks. 
6.  Unpredictable results may occur if the UTS is a timespan and exceeds a few 
    years.  If this occurs, the UTS timespan is invalid and the calling 
    program must be modified to allow for the extended UTS values introduced 
    in host release E03. 
00002
00001
00003
Format: 
CALL XUD$UTS_DATE ( XUD_PARAM, uts, date ) ALTRET ( error ); 
Parameters: 
XUD_PARAM   an XUD_PARAM structure 
uts         the UTS to be converted 
date        returns the equivalent DATE 
Description: 
This service converts a UTS into a DATE.  No picture is involved. 
Rules: 
1.  If XUD_PARAM.TIMESPAN is set, the UTS is treated as a number of clock 
    ticks, not a date and time.  This means that the UTS base value is not 
    subtracted from the converted value.  Unpredictable results may occur if 
    the timespan exceeds a few years.  If this occurs, the UTS timespan is 
    invalid and the calling program must be modified to allow for the extended 
    UTS values introduced in host release E03. 
2.  The service supports an ALTRET clause to be consistent with other XUD 
    services, but no errors should be expected. 
00002
00001
00003
Format: 
CALL XUD$UTS_DIFF ( diff, uts1, uts2 ) ALTRET ( error ); 
Parameters: 
diff    returns the interval between uts1 and uts2 in 
        an SBIN word 
uts1    the UTS for the start of the interval 
uts2    the UTS for the end of the interval 
Description: 
This service computes the interval between uts1 and uts2, taking into account 
differing UTS formats.  The result is returned in centiseconds, as an SBIN. 
Rules: 
1.  If the computed interval overflows the bounds of an SBIN, the service 
    ALTRETURNs.  The largest interval value returned is approximately 11 
    years. 
00002
00001
00003
Format: 
CALL XUD$UTS_DIFF_25TH ( diff, uts1, uts2 ) ALTRET ( error ); 
Parameters: 
diff    returns the interval between uts1 and uts2 in 
        an SBIN word 
uts1    the UTS for the start of the interval 
uts2    the UTS for the end of the interval 
Description: 
This service computes the interval between uts1 and uts2, taking into account 
differing UTS formats.  The result is returned in 1/25th of a second units, as 
an SBIN. 
Rules: 
1.  This service supports an ALTRET clause to be consistent with other XUD 
    services, but no errors should be expected. 
00002
00001
00003
Format: 
CALL XUD$UTS_DIFF_SEC ( diff, uts1, uts2 ) ALTRET ( error ); 
Parameters: 
diff    returns the interval between uts1 and uts2 in an SBIN word 
uts1    the UTS for the start of the interval 
uts2    the UTS for the end of the interval 
Description: 
This service computes the interval between uts1 and uts2, taking into account 
differing UTS formats.  The result is returned in seconds, as an SBIN. 
Rules: 
1.  This service supports an ALTRET clause to be consistent with other XUD 
    services, but no errors should be expected. 
00002
00001
00003
The XUD_PARAM macro describes the structure that is used with most XUD 
services to pass and return various fields.  Parameters may be used to 
initialize all fields that pass values to the services.  These fields will not 
be altered by the XUD services.  Note that an XUD_PARAM structure in constant 
storage must not be passed to an XUD service, since some fields are used to 
return values to the caller. 
    DATA_SIZE - UBIN BYTE 
    On calls for conversion to character, returns the actual size in 
    characters of the converted string.  Note that if TEXTC is set, the same 
    value is saved in the count byte of the resulting TEXTC string. 
    ERR - A standard CP-6 error code 
    Contains the error code in case of an ALTRETURN.  The error code is set to 
    zero on a normal return. 
    INIT_PIC - BIT(1) 
    When PIC is not NIL on calls for conversion to or from character, 
    specifies whether or not the picture has been previously initialized.  If 
    INIT_PIC is set, the picture will be initialized.  Otherwise, it is 
    assumed to have been initialized by a prior call to XUD$INIT_PIC. 
    If the same picture is to be used repetitively, considerable execution 
    time can be saved by initializing the picture one time only, before it is 
    used by any conversion service. 
    This field is initialized in the XUD_PARAM block with INIT_PIC={YES|NO}. 
    The default is NO. 
    MAX_SIZE - UBIN BYTE 
    On calls to XUD$INIT_PIC, returns the nominal maximum size in characters 
    for strings to be converted using the initialized picture. 
    PIC$ - PTR 
    On calls for conversion to or from character, specifies the picture to be 
    used to control the conversion. 
    This field is initialized in the XUD_PARAM block with PIC=picture. The 
    default is NIL. 
    PIC_SIZE - UBIN BYTE 
    If PIC_TEXTC is not set on calls that involve picture initialization, 
    specifies the size in characters of the picture to be initialized.  The 
    size must be between 1 and 63. 
    This field is initialized in the XUD_PARAM block with PIC_SIZE=number. 
    The default is zero. 
    PIC_TEXTC - BIT(1) 
    On calls that involve picture initialization, specifies whether the 
    picture to be initialized is a fixed length string or is in TEXTC form. 
    If PIC_TEXTC is set, the picture is treated as a TEXTC string, otherwise 
    it is assumed to be a fixed length string. 
    This field is initialized in the XUD_PARAM block with PIC_TEXTC={YES|NO}. 
    The default is NO. 
    SIZE - UBIN BYTE 
    If TEXTC is not set on calls for conversion from character, specifies the 
    size in characters of the string to be converted.  On calls for conversion 
    to character, specifies the maximum number of characters in the converted 
    string.  The size must be between 1 and 63. 
    This field is initialized in the XUD_PARAM block with SIZE=number.  The 
    default is zero. 
    TEXTC - BIT(1) 
    On calls for conversion to or from character, specifies whether the 
    character operand is a fixed length or a TEXTC string.  If TEXTC is set, 
    the string is in TEXTC format, otherwise it is a fixed length string. 
    This field is initialized in the XUD_PARAM block with TEXTC={YES|NO}.  The 
    default is NO. 
    TIMESPAN - BIT(1) 
    If set, specifies that the conversion involves a time span value. 
    Otherwise, the conversion is assumed to involve a date/time value. 
    This field is initialized in the XUD_PARAM block with TIMESPAN={YES|NO}. 
    The default is NO. 
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
          The XUE services permit preprocessing and evaluation of command 
          input as well as several related functions.  The primary services 
          are 
o   X$PRE_PROCESS to do substitutions for preprocessor expressions (i.e., 
    %expression) in command text. 
o   X$EVAL to do evaluation of expressions in command text.  Expressions may 
    include IBEX-style expressions; user-defined functions; and standard, 
    private or user-managed command variables. 
In addition several services called by X$EVAL (X$GET_VAR, X$PUT_VAR, 
X$STRIP_BLANKS, and X$DEC_CONVERT) can be called directly by the user. 
For a summary of each XUE service, type: 
HELP (HOSTLIB) XUE service 
where service is one of the following:  X$DEC_CONVERT, X$EVAL, X$GET_VAR, 
X$PUT_VAR, X$PRE_PROCESS, X$STRIP_BLANKS, or XUE$PPSUCCESS. 
  Service                 Function 
  X$DEC_CONVERT 
                          Converts a string to a decimal value, if possible. 
  X$EVAL 
                          Performs evaluation of expressions in command text. 
                          (Expressions may include IBEX-style expressions, 
                          user-defined functions and standard, private or 
                          user-managed command variables.) 
  X$GET_VAR 
                          Obtains the value of a specified command variable. 
  X$PUT_VAR 
                          Stores the value of a specified command variable. 
  X$PRE_PROCESS 
                          Performs substitutions for preprocessor expressions 
                          (i.e., %expression) contained in command text. 
  X$STRIP_BLANKS 
                          Strips leading and trailing blanks from a TEXTC 
                          string. 
  XUE$PP_SUCCESS 
                          Checks for valid built-in function names. 
00001
00002
00003
00005
00004
00006
00007
Format: 
CALL XUE$PP_SUCCESS (parse$param); 
Parameters: 
parse$param    A parser user exit routine parameter block.  See the 
description of PARSE$PARAM in Section 10 for additional information. 
Description: 
XUE$PP_SUCCESS is a parser user exit routine that is intended to be called 
when X$PARSE has successfully parsed a predefined function name.  It insures 
that the name just parsed is really a function name, rather than part of a 
variable name whose first few characters are identical to a function name. 
For example, it will accept $ACCT as a valid function name, but reject 
$ACCTNAME. 
Those who use only X$PRE_PROCESS need not be concerned with this routine.  It 
will be automatically called when needed. 
X$EVAL users who have no need of a parser user exit routine of their own 
should use this routine for that purpose.  (This is done by setting p_pcb.U$$, 
or using the U$ parameter on the P_PCB macro.  See Section 10 for additional 
information.) 
X$EVAL users who do need their own parser user exit routine should call this 
routine from their own routine when it is entered for success processing of a 
node whose code is reserved for use by XUE (those between 1 and 125). 
00002
00001
For a description of each field, type: 
HELP (HOSTLIB) XUE_ECB field 
where field is one of the following:  CMDVAR, ERR, ERR_DCB, ERR_POS, FUN, OUT, 
PRIVATE, PROCACCT, PROCNAME, PROMPT, TREE, USER, VAR, WKSZ, WORK, or WORK_DCB. 
CMDVAR = {YES|NO} if YES is specified, then all variables will refer to 
    standard or private command variables.  If NO is specified, the user 
    routine pointed to by VAR$$ will be called to handle variable references. 
    The fully qualified name of this field is XUE_ECB.FLAGS.CMDVAR#.  The 
    default is YES. 
    ERR - VALUE-BIT(36) on return, contains the error code associated with the 
    first error detected. If ERR is equal to E$XUE#SMALLWORK, then the 
    workspace should be enlarged and X$EVAL called again.  Otherwise, the 
    error should be printed.  See ERR_POS for more information. 
    ERR_DCB - VALUE-DEC(0-?) on return, this variable holds the DCB number on 
    which the error occurred.  It is valid only when ERR is non-zero.  The 
    fully qualified name of this field is XUE_ECB.ERR_DCB#. 
    ERR_POS - VALUE-DEC(0-?) on return, this variable holds the character 
    position in the expression where the first error was found.  It is valid 
    only when ERR is non-zero.  The fully qualified name of this field is 
    XUE_ECB.ERR_POS#. 
    FUN = {ENTRY|NIL} specifies the address of the user-supplied routine which 
    will handle any user-defined functions.  If there are no user-defined 
    functions then this routine is unnecessary.  The fully qualified name of 
    this field is XUE_ECB.FUN$$. 
    INPUT_DCB = DCB is the dcb to be used by the $INPUT function.  The default 
    is NIL, in which case M$UC will be used. 
    LEAD = VALUE-CHAR(2) is the 2-character value of the leading delimiter of 
    comments included in command input.  A single character delimiter must 
    include a leading blank.  The fully qualified name of this field is 
    XUE_ECB.LEAD#.  The default is ' "'. 
    OUT - VARIABLE points to a TEXTC field in the work area which contains the 
    result of the expression evaluation.  The fully qualified name of this 
    field is XUE_ECB.OUT$. 
    PRIVATE = {YES|NO} specifies whether command variables are to be private 
    (YES) or standard (NO).  This flag is meaningful only if CMDVAR is YES. 
    The fully qualified name of this field is XUE_ECB.FLAGS.PRIVATE#.  The 
    default is NO. 
    PROCACCT = VARIABLE this vector frames the account where the processor 
    named in PROCNAME resides.  If NIL, the default will be taken from M$LM. 
    The fully qualified name of this field is XUE_ECB.PROCACCT_. 
    PROCNAME = VARIABLE this vector frames the name of the processor that is 
    using X$EVAL.  The name must be in TEXTC form, preferably stored in a 
    VLP_NAME structure.  This information is used when accessing command 
    variables if FLAGS.PRIVATE# is set.  Otherwise, standard command variables 
    will be used.  If PROCNAME is NIL then the default will be taken from 
    M$LM.  This field will not be used if the user program handles all 
    variable references.  See CMDVAR.  The fully qualified name of this field 
    is XUE_ECB.PROCNAME_. 
    PROMPT - {YES|NO} this flag will be set by X$EVAL when an M$PROMPT monitor 
    service was issued.  In this case the user must reset the prompt before 
    doing any reads or writes to the terminal.  Since XUE$EVAL restores the 
    user's prompt whenever possible, this flag will seldom be set.  The fully 
    qualified name of this field is XUE_ECB.RESULTS.PROMPT#. 
    TRAIL = VALUE-CHAR(2) is the 2-character value of the trailing delimiter 
    of comments included in command input.  A single character delimiter must 
    include a leading blank.  The fully qualified name of this field is 
    XUE_ECB.TRAIL#.  The default is ' "'. 
    TREE = PTR points to the parse tree of an expression to be evaluated.  The 
    fully qualified name of this field is XUE_ECB.TREE$. 
    USER = PTR this field is available for the user's use.  It will be passed 
    in XUE_FUNPARAM.USER$ and XUE_VARPARAM.USER$ to the user-supplied 
    routines.  The fully qualified name of this field is XUE_ECB.USER$. 
    VAR = {ENTRY|NIL} specifies the address of the user-supplied routine which 
    will store/return the values for any user-managed command variables in the 
    expression to be evaluated.  If standard or private command variables are 
    to be used VAR should be NIL.  The fully qualified name of this field is 
    XUE_ECB.VAR$$. 
    WKSZ = VALUE-DEC(150-?) specifies the size of the work area pointed to by 
    WORK$ in words.  The fully qualified name of this field is XUE_ECB.WKSZ#. 
    The default is 0. 
    WORK = PTR locates a work area.  The fully qualified name of this field is 
    XUE_ECB.WORK$. 
    WORK_DCB = DCBNAME is the name of the scratch DCB that X$EVAL may use.  It 
    should always be closed upon the initial call to X$EVAL and the user 
    program must close it at exit time as required.  The user program must not 
    use this DCB.  The fully qualified name of this field is 
    XUE_ECB.WORK_DCB#. 
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
For a description of each field, type: 
HELP (HOSTLIB) XUE_FUNPARAM param 
where param is one of the following:  CODE, CPOS, ERR, ERR_DCB, ERR_POS, 
NOPTS, OPTION, OUT, or USER. 
CODE - VALUE-DEC(0-?) this field will contain the code of the root node of the 
    user-defined function to be processed.  The fully qualified name of this 
    field is XUE_FUNPARAM.CODE#. 
    CPOS - VALUE-DEC(0-?) contains the character position of the function 
    name.  The fully qualified name of this field is XUE_FUNPARAM.CPOS#. 
    ERR - standard CP-6 error code.  This field may be set by the 
    user-supplied routine to any error code.  When this routine returns to 
    X$EVAL this field will be checked and if non-zero this error code and 
    ERR_POS will be moved into XUE_ECB.  X$EVAL will then ALTRETURN to the 
    calling routine. 
    ERR_DCB - VALUE-DEC(0-?) this variable holds the DCB number on which the 
    error occurred.  It is valid only when ERR is non-zero.  The fully 
    qualified name of this field is XUE_FUNPARAM.ERR_DCB#. 
    ERR_POS - VALUE-DEC(0-?) this field may be set by the user-supplied 
    routine.  It will be passed back thru XUE_ECB.ERR_POS# to the calling 
    routine if XUE_FUNPARAM.ERR is non-zero.  The fully qualified name of this 
    field is XUE_FUNPARAM.ERR_POS#. 
    NOPTS - VALUE-DEC(0-?) specifies how many OPTION pointers are in this 
    structure.  The fully qualified name of this field is XUE_FUNPARAM.NOPTS#. 
    OPTION - PTR each pointer in this array points to an XUE_OPTION structure. 
    Each of these structures contains information about a parameter for this 
    function.  The fully qualified name of this field is XUE_FUNPARAM.OPTION$. 
    OUT - PTR Points to a 512 byte buffer where the user-supplied routine is 
    to put the result of evaluating the function.  The field is considered to 
    be a TEXTC field, i.e., the first byte will specify how many bytes are 
    significant.  The fully qualified name of this field is XUE_FUNPARAM.OUT$. 
    USER - PTR this pointer will contain the same data as XUE_ECB.USER$ (or 
    XUE_PPCB.USER$).  The fully qualified name of this field is 
    XUE_FUNPARAM.USER$. 
00001
00002
00003
00004
00005
00006
00007
00008
For a description of each field, type: 
HELP (HOSTLIB) XUE_OPTION field 
where field is one of the following:  CODE, COUNT, CPOS, or TEXT 
CODE - VALUE-DEC(0-?) this field will contain the user-defined code for this 
    option.  The fully qualified name of this field is XUE_OPTION.CODE#. 
    COUNT - VALUE-DEC(0-?) contains the number of characters in the field 
    TEXT.  The fully qualified name of this field is XUE_OPTION.COUNT#.  Will 
    be zero for a valueless argument. 
    CPOS - VALUE-DEC(0-?) contains the character position of the expression 
    part of this option.  The fully qualified name of this field is 
    XUE_OPTION.CPOS#. 
    TEXT - VALUE-CHAR(0-?) contains a text string resulting from evaluation of 
    the expression represented by XUE_VALUE or XUE_PARAMETER in the parse 
    nodes.  The fully qualified name of this field is XUE_OPTION.TEXT#. 
00001
00002
00003
The structure XUE_ECB is appended to XUE_PPCB.  Fields in that structure are 
accessed by the fully qualified name XUE_PPCB.ECB.ERR, for example, which is 
analogous to XUE_ECB.ERR in the XUE_ECB structure.  For a description of each 
field, type: 
HELP (HOSTLIB) XUE_PPCB field 
where field is one of the following:  ICHARS, INBUF, OCHARS, OUTBUF, RCHARS, 
or ROOT. 
ICHARS = VALUE-DEC(0-?) specifies the number of characters in INBUF that are 
    to be considered by X$PRE_PROCESS.  The fully qualified name of this field 
    is XUE_PPCB.ICHARS#.  The default is 0. 
    INBUF = PTR locates the buffer to be preprocessed.  The fully qualified 
    name of this field is XUE_PPCB.INBUF$. 
    OCHARS = VALUE-DEC(0-?) specifies the maximum number of characters that 
    may be stored in the result buffer.  The fully qualified name of this 
    field is XUE_PPCB.OCHARS#.  The default is 0. 
    OUTBUF = VARIABLE locates the buffer where the result of X$PRE_PROCESS is 
    to be stored.  This buffer may be the same as used for input.  The fully 
    qualified name of this field is XUE_PPCB.OUTBUF$. 
    RCHARS - VALUE-DEC(0-?) on return, contains the actual number of 
    meaningful characters in OUTBUF.  The fully qualified name of this field 
    is XUE_PPCB.RCHARS#. 
    ROOT = VARIABLE specifies the address of the parse root node that defines 
    the syntax of a preprocessor expression.  Unless the user has his own 
    preprocessing tree, the ROOT should be set to XUE_PREEXP.  The fully 
    qualified name of this field is XUE_PPCB.ROOT$. 
00001
00002
00003
00004
00005
For a description of each field, type: 
HELP (HOSTLIB) XUE_VARPARAM param 
where param is one of the following:  CODE, COUNT, ERR, ERR_DCB, ERR_POS, 
TEXT, USER, or VALUE. 
CODE - {%XUE_FETCH#|%XUE_STORE#} specifies the function to perform.  The fully 
    qualified name of this field is XUE_VARPARAM.CODE#. 
    COUNT - VALUE-DEC(0-?) specifies the length of the name of the variable. 
    The fully qualified name of this field is XUE_VARPARAM.COUNT#. 
    CPOS = VALUE contains the character position of the variable name.  The 
    fully qualified name of this field is XUE_VARPARAM.CPOS#. 
    ERR - standard CP-6 error code.  May be set by the user-supplied routine 
    to any error code.  When this routine returns to X$EVAL this field will be 
    checked and if non-zero this error code and ERR_POS will be moved into 
    XUE_ECB. X$EVAL will then ALTRETURN to the calling routine. 
    ERR_DCB - VALUE-DEC(0-?) specifies the DCB number on which the error 
    occurred.  It is valid only when ERR is non-zero.  The fully qualified 
    name of this field is XUE_VARPARAM.ERR_DCB#. 
    ERR_POS - VALUE-DEC(0-?) may be set by the user-supplied routine.  It will 
    be passed back through XUE_ECB.ERR_POS# to the calling routine if 
    XUE_FUNPARAM.ERR is non-zero.  The fully qualified name of this field is 
    XUE_VARPARAM.ERR_POS#. 
    TEXT - VALUE-CHAR(0-?) contains the name of the variable that the user 
    service routine is to return.  The fully qualified name of this field is 
    XUE_VARPARAM.TEXT#. 
    USER - PTR contains the same data as XUE_ECB.USER$ (or XUE_PPCB.USER$). 
    The fully qualified name of this field is XUE_VARPARAM.USER$. 
    VALUE - PTR contains the address of a TEXTC buffer.  On a STORE operation 
    this buffer will contain the value associated with the variable named in 
    XUE_VARPARAM.TEXT#.  For a FETCH operation, the buffer is to be used to 
    return the TEXTC value of the specified command variable.  The maximum 
    size is 512 bytes including count.  The fully qualified name of this field 
    is XUE_VARPARAM.VALUE$. 
00001
00002
00003
00004
00005
00006
00007
00008
The XUF services perform formatted writes.  Typically these services are used 
to format lines of unit record text.  The X$FORMAT service may be called 
directly, or via the X$WRITE service which is somewhat simpler to invoke. 
Because the XUF services perform the same functions, they are referred to 
collectively as the Formatter.  For information on the FMT structure, type: 
HELP (HOSTLIB) F_FDS FMT For more information, type ? 
Formatting involves these elements: 
o   Variable data to be formatted - A number of individual items of data may 
    be specified when the Formatter is invoked.  The number of items passed to 
    X$FORMAT is unlimited; X$WRITE permits up to 20 items. 
o   A Format (FMT) string - A FMT string is a character variable consisting of 
    a sequence of characters including the % symbol that delimits formatting 
    codes, and optionally ASCII text to be added as is to the formatted data. 
o   An output buffer - As the FMT string and data are processed, the results 
    are moved to the output buffer. 
When invoked the Formatter scans the FMT string from left to right.  On 
encountering the % delimiter and following formatting codes, it performs the 
requested formatting function for the data referenced.  The amount of data 
formatted and moved to the output buffer is implicit in the format codes as 
explained later.  If the FMT string contains ASCII text, the Formatter moves 
those characters to the output buffer as it encounters them in scanning the 
FMT string. 
The XUG services provide processors a uniform method of reading and parsing 
command input and of handling errors in command text.  The XUG services free 
the programmer from the details of obtaining command input.  For instance, XUG 
services: 
o   Provide an input DCB and input buffer for use in obtaining command input. 
o   Can identify the location of syntactical errors (in context or by a 
    pointer under the user's input). 
o   Can list legal alternatives for a syntactical element in error. 
o   Facilitate display of standard, multi-level error messages. 
o   Facilitate display of standard, multi-level HELP messages. 
o   Supply optional built-in commands (such as PRINT, DIR, etc.). 
The services are categorized as follows: 
    CATEGORY                  SERVICE 
    Get and parse             XUG$INIT 
    a command                 XUG$GETCMD 
                              XUG$BLANK_PASSWORD 
    Echo                      XUG$ECHO 
                              XUG$ECHOIF 
                              XUG$ECHOLAST 
    Error reporting           XUG$ERRMSG 
                              XUG$SETERRMSG 
                              XUG$ERRPTR 
                              XUG$ERRCNVRT 
                              XUG$ERRTOLCP6 
    HELP message reporting    XUG$HELP 
                              XUG$MOREMSG 
                              XUG$ALLMSG 
    DCB manipulation          XUG$CORRES 
                              XUG$FINDDCB 
                              XUG$GETDCB 
                              XUG$CLOSE_DCBS 
                              XUG$OPENOUT 
    Break control             XUG$BREAK 
                              XUG$DISABLE 
                              XUG$ENABLE 
                              XUG$CLRENABLE 
                              XUG$SIMULATE_BREAK 
Format: 
CALL XUG$ALLMSG (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure in which the XUH parameter is 
meaningful. 
Description: 
The XUG$ALLMSG service calls XUG$ERRMSG or X$HELP service to get all remaining 
messages.  This service consults a flag which is set via XUG$HELP and reset 
via XUG$ERRMSG to determine which service to call. 
Error Conditions: 
Error codes returned by XUG$ALLMSG include those returned by the X$HELP 
library service. 
00002
00003
00001
Format: 
CALL XUG$BLANK_PASSWORD (xug_getcmd,p$block) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure. 
p$block    is either a PARSE$OUT or PARSE$SYM structure. 
Description: 
The XUG$BLANK_PASSWORD service blanks the passwords of FIDs in the input 
buffer.  If PASS=BLANK in the XUG_INIT structure, XUG$GETCMD calls 
XUG$BLANK_PASSWORD automatically. 
If a PARSE$OUT structure is specified, XUG$BLANK_PASSWORD runs down the parse 
tree to each end node.  If an end node is a FID, XUG$BLANK_PASSWORD calls 
M$FID (passing the FID) to determine if a password was specified.  If a 
password was specified, XUG$BLANK_PASSWORD blanks out the password and the 
period (.) preceding the password in the input buffer.  If a PARSE$SYM 
structure is specified, XUG$BLANK_PASSWORD only examines that branch of the 
tree.  For more information, type: 
HELP (HOSTLIB) OUT$BLK 
Error Conditions: 
XUG$BLANK_PASSWORD takes the alternate return if M$FID takes the alternate 
return.  The error code can be found in xug_getcmd.ERR#. 
00002
00003
00001
Description: 
The XUG$BREAK service is a generalized break handler available to programs 
using XUG$GETCMD.  It is entered asynchronously upon occurrence of a break. 
XUG$BREAK is established as the break service through a user call to M$INT. 
If XUG$BREAK is to be used, the user must establish (via a call to XUG$INIT) 
the identity of a routine to be called when the command in progress is aborted 
by a break event. 
When a break occurs, XUG$BREAK checks to see if the user has established a 
break-message routine via the BRKMSG parameter in the XUG_INIT structure 
passed to XUG$INIT.  If so, the specified routine is called; if not, the 
message 
    "Break!   C to continue" 
is issued through M$UC.  A read is then issued through M$UC; the action taken 
depends on the user's response to the read: 
  o  If the user responds with the single character 'C' or 'c', the routine 
     specified by XUG_INIT.CONTINUE$ is called (if it is non-NIL); an M$TRTN 
     is then issued to permit the routine which was interrupted by the break 
     to continue. 
  o  If the user enters a null response (simply a carriage return, line feed, 
     or other activation character), XUG$BREAK issues an M$CLRSTK and then 
     calls the routine specified by XUG_INIT.ABORT$, which must not be NIL. 
     This routine typically terminates with an UNWIND to continue execution at 
     some clean point in the user's program.  The routine must not RETURN or 
     ALTRETURN to XUG$BREAK. 
  o  If the user responds with anything other than a 'C', 'c', or a null 
     response, XUG$BREAK "remembers" the user's response and then proceeds as 
     though a null response had been entered (i.e., issue an M$CLRSTK and then 
     call XUG_INIT.ABORT$).  When the user's program issues its next call to 
     XUG$GETCMD, the "remembered" response is parsed as though it had been 
     entered in response to the XUG$GETCMD prompt. 
  o  If the user wishes to totally bypass the "Break!  C to continue" 
     processing, the routine specified in XUG_INIT.BRKMSG$ may opt to call the 
     system routine X66_TRTN.  This routine "unwinds" back to the routine 
     which was interrupted by the break; execution resumes at the point of 
     interruption with breaks disabled (via XUG$DISABLE).  The 
     XUG_INIT.BRKMSG$ routine may call XUG$CLRENABLE before calling X66_TRTN 
     to re-enable breaks, if desired. 
Breaks are ignored: 
  o  From the time XUG$BREAK is entered until it is exited. 
  o  If input while reading a command. 
Format: 
CALL XUG$CLOSE_DCBS (xug_getcmd); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure in which these parameters are 
meaningful:  DISP, DCB_PARAM.  For details, type: 
HELP (HOSTLIB) XUG_GETCMD 
Description: 
The XUG$CLOSE_DCBS service closes open DCBs.  If DCB_PARAM is not equal to 
DCBNUM(NIL), then only that DCB will be closed.  Otherwise, all DCBs will be 
closed.  If DISP is not equal to zero, then the DCBs will be closed with that 
DISP.  Otherwise, they will be closed with DISP=SAVE, except for DCBs for 
FPRGs which are closed with DISP=RELEASE.  XUG$CLOSE_DCBS ignores 
XUG_GETCMD.INDCB# and XUG_GETCMD.OUTDCB#.  If XUG_GETCMD.DCB_PARAM# ~= 
DCBNUM(NIL), then only the DCB whose DCBNUM is in .DCB_PARAM# is closed. 
00002
00001
Format: 
CALL XUG$CLRENABLE (xug_getcmd); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure. 
Description: 
The XUG$CLRENABLE service re-enables breaks disabled by a call to XUG$DISABLE. 
Breaks that occurred while break processing was disabled are ignored when 
XUG$CLRENABLE is called. 
00002
00001
Format: 
CALL XUG$CORRES (dcb1,dcb2) ALTRET (label); 
Parameters: 
dcb1    is a variable containing DCB number (UBIN WORD). 
dcb2    is a variable containing DCB number (UBIN WORD). 
Description: 
The XUG$CORRES service performs a correspondence check of the specified DCBs. 
A default open is performed on the DCBs if they are not open. 
Error Conditions: 
If the DCB assignments correspond, the alternate return is taken. 
00002
00003
00001
Format: 
CALL XUG$DISABLE (xug_getcmd); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure. 
Description: 
The XUG$DISABLE service disables breaks for critical code.  Calls to 
XUG$DISABLE may be nested.  If a break occurs while breaks are disabled, the 
break will not be processed immediately. 
00002
00001
Format: 
CALL XUG$ECHO (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure in which the DCB_PARAM parameter is 
meaningful.  For details, type: 
HELP (HOSTLIB) XUG_GETCMD 
Description: 
The XUG$ECHO service is used to write the last command through the output DCB 
specified by DCB_PARAM.  If DCB_PARAM is NIL, then M$LO will be used.  If the 
command is continued over several lines, all lines will be echoed. 
Error Conditions: 
XUG$ECHO takes the ALTRETURN if DCB_PARAM is NIL and M$LO is not found. 
00002
00003
00001
Format: 
CALL XUG$ECHOIF (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure in which the DCB_PARAM parameter is 
meaningful.  For details, type: 
HELP (HOSTLIB) XUG_GETCMD 
Description: 
The XUG$ECHOIF service performs a check to determine if the output DCB 
specified by DCB_PARAM corresponds with any DCB on which the current command 
has been displayed.  If DCB_PARAM is NIL, M$LO is assumed to be the output 
DCB.  This check includes the input DCB (XUG_GETCMD.INDCB#) and any other DCB 
through which the command has been echoed via calls to XUG$ECHO or XUG$ECHOIF. 
The command is written through the output DCB if it has not already been 
output.  If the command is continued over several lines, all lines will be 
echoed. 
Error Conditions: 
XUG$ECHOIF takes the ALTRETURN if DCB_PARAM is NIL and M$LO is not found. 
00002
00003
00001
Format: 
CALL XUG$ECHOLAST (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure; the DCB_PARAM parameter in that 
structure is meaningful.  For details, type: 
HELP (HOSTLIB) XUG_GETCMD 
Description: 
The XUG$ECHOLAST service writes the last command line, which may be one line 
of a continued command, through the DCB specified by DCB_PARAM.  If DCB_PARAM 
is NIL, then M$LO will be used. 
Error Conditions: 
XUG$ECHOLAST takes the ALTRETURN if DCB_PARAM is NIL and M$LO is not found. 
00002
00003
00001
Format: 
CALL XUG$ENABLE (xug_getcmd); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure. 
Description: 
The XUG$ENABLE service re-enables breaks disabled by a call to XUG$DISABLE. 
Breaks that occurred while break processing was disabled will be honored when 
XUG$ENABLE is called. 
00002
00001
Format: 
CALL XUG$ERRCNVRT (lcp6_error_code,error_code); 
Parameters: 
lcp6_error_code    is a variable containing an LCP-6 error code 
(fcg/mid/m/err/sev) as passed through the coupler. 
error_code    is a variable to contain the error code converted to CP-6 
standard format. 
Description: 
The XUG$ERRCNVRT service converts an LCP-6 error code (32 bits, stored in 36 
bits with the high-order bit in each byte being zero) into the equivalent CP-6 
standard error code format (36 bits). 
00002
00001
Format: 
CALL XUG$ERRMSG (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure in which these parameters are 
meaningful:  DCB_PARAM, DCB2_PARAM, ERR_CODE, ERRDCB, F1, F2, F3, FLGLEV, 
INFOMSG, OUTDCB.  For details, type: 
HELP (HOSTLIB) XUG_GETCMD 
Description: 
The XUG$ERRMSG service controls error processing by passing parameters to 
M$ERRMSG.  The error message is written through DCB_PARAM and DCB_PARAM2, with 
correspondence checking.  If one of these is NIL and the other is not, the 
message is written through the non-NIL DCB only.  If both DCB parameters are 
NIL, the message is written through OUTDCB and M$DO. 
Error Conditions: 
When ERR_CODE in XUG_GETCMD is zero, the severity field of the last code is 
incremented.  If the severity field exceeds 7 or no message is found, the 
alternate return is taken. 
00002
00003
00001
Format: 
CALL XUG$ERRPTR (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure.  The meaningful parameters in 
XUG_GETCMD are DCB_PARAM, EPOS, OUTDCB, and USE_EPOS.  For details, type: 
HELP (HOSTLIB) XUG_GETCMD 
Description: 
The XUG$ERRPTR service displays a message identifying where an error detected 
by XUG$GETCMD occurred within command text.  The message "Error at <?>:" 
followed by a portion of the command text with <?> inserted where the error 
was detected in output.  This pointer is written through the DCB specified by 
DCB_PARAM.  If DCB_PARAM is NIL, OUTDCB will be used instead. 
If USE_EPOS# is set, then XUG$ERRPTR will use the value in EPOS#, otherwise 
XUG$ERRPTR will use P_PCB.HI_CHAR for the character position. 
NOTE:  Instead of the partial line error message described in the previous 
paragraph, the error pointer (^) may be displayed at the point of the error. 
This can be done by issuing the IBEX command "!POINT" before calling 
XUG$ERRPTR.  However, displaying "^" is appropriate only if EPOS# is within 
the last line of the command. 
Error Conditions: 
XUG$ERRPTR takes the ALTRETURN if both DCB_PARAM and OUTDCB are NIL and M$LO 
is not found. 
00002
00003
00001
Format: 
CALL XUG$ERRTOLCP6 (lcp6_err,cp6_err); 
Parameters: 
lcp6_err    is a variable to contain an LCP-6 error code (fcg/mid/m/err/sev) 
to be passed back through the coupler. 
cp6_err    is a variable containing the error code in CP-6 standard format. 
Description: 
The XUG$ERRTOLCP6 service converts error code to the LCP-6 equivalent. 
00002
00001
Format: 
CALL XUG$FINDDCB (dcbname,dcbloc) ALTRET (label); 
Parameters: 
dcbname    is a variable containing a DCB name (in TEXTC format) that 
identifies a DCB to be searched for in the DCB table. 
dcbloc    is a variable that identifies where the DCB number is to be 
returned.  The DCB number is returned as an SBIN WORD value. 
Description: 
The XUG$FINDDCB service returns a DCB number. 
Error Conditions: 
The alternate return is taken if the DCB name is not found in the table. 
00002
00003
00001
Format: 
CALL XUG$GETCMD (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure.  The meaningful parameters in 
XUG_GETCMD are ALWAYS_SET_PROMPT, NODES, PROMPT, PROMPT_VFC, RPROMPT, TEXT, 
SFROUTINE, CONTINUE_OK, INDCB, OUTDCB, READR, and SKIP_PREPROCESS.  For 
details, type: 
HELP (HOSTLIB) XUG_GETCMD 
Description: 
XUG$GETCMD reads the command text and calls the X$PARSE library service, 
passing it the xug_getcmd parameter.  XUG$GETCMD can parse commands described 
in user-defined parse nodes and, optionally, can parse and perform a set of 
built-in commands.  XUG$GETCMD also has capabilities to echo command input, to 
recall a previous command line, or to display a pointer at an error detected 
by a calling processor. 
If the command entered is syntactically correct, XUG$GETCMD takes these 
actions: 
o   For a user-defined command, it returns a parse output tree via the OUT$ 
    field in XUG_GETCMD. 
o   For a built-in command, unless all or specific built-in commands are 
    inhibited (by COMMANDS=NO or INHIBIT_commandname=YES in the XUG_INIT 
    structure), it performs the built-in function.  See the XUG_INIT subtopic 
    for the list of built-in commands.  For the DO or ! command, XUG$GETCMD 
    passes control to the command processor for execution of the command. 
    In addition, before or after any built-in command, the command processor 
    may take control if PRE_EXEC or POST_EXEC is specified in the XUG_INIT 
    structure.  In either case, two parameters are passed by XUG$GETCMD:  the 
    first parameter is used by XUG$GETCMD and should be ignored; the second 
    parameter is a code defined in XU_SUBS_C.:LIBRARY that identifies the 
    built-in command in the buffer.  (The relevant EQUs in XU_SUBS_C contain 
    the prefix XUG_CMD.) 
If the command entered is syntactically incorrect, how XUG$GETCMD functions 
depends on the setting of several flags in the XUG_INIT structure. 
o   If GOODCMD=YES, XUG$GETCMD returns to the caller only when the command 
    received is syntactically correct, and causes a dialog with the 
    time-sharing user in the case of syntax errors.  The dialog conducted at a 
    syntax error depends on the command input and the setting of the SYNTAX 
    flag. 
o   If GOODCMD=NO, XUG$GETCMD returns to the caller when the command received 
    is syntactically correct, and takes the alternate return in case of a 
    syntax error. 
Setting SYNTAX=YES requests XUG$GETCMD to retain information about the 
previous parsing operation in order to display a list of legal alternatives to 
the last element parsed.  The following situations illustrate the dialog that 
XUG$GETCMD can conduct on behalf of the caller: 
Case 1:  Assume GOODCMD=YES, SYNTAX=YES, and a syntax error is detected 
    because of a misspelling that causes a mismatch to the parse nodes: 
    o   A message is displayed to identify the location of the syntax error 
        (via an internal call to XUG$ERRPTR). 
    o   If the time-sharing user enters ? to obtain more information, the list 
        of legal alternatives is output via M$DO (by means of an internal call 
        to XUG$GETCMD with the NXT flag set in the Parse Control Block that 
        reparses the command containing the syntax error). 
Case 2:  Assume GOODCMD=YES, SYNTAX=YES, and a syntax error is detected 
    because the command includes the ? character causing a mismatch to the 
    parse nodes: 
    o   The list of legal alternatives is output via M$DO.  (This is done by 
        means of a call to XUG$GETCMD by XUG$GETCMD with the NXT flag in the 
        Parse Control Block set to cause reparsing of the command containing 
        the syntax error). 
Both cases illustrate the simplest way to take advantage of the features of 
XUG$GETCMD and reduce the amount of command input processing required in the 
user's code.  If GOODCMD=NO, the internal calls can be performed by the caller 
instead.  If SYNTAX=NO, the caller can take charge of supplying the error 
diagnostic information (i.e., via calls to XUG$ERRMSG or XUG$MOREMSG). 
Error Conditions: 
On an alternate return, the field ERR# in XUG_GETCMD contains a standard CP-6 
error code. 
Usage Notes: 
1.  If XUG$GETCMD returns normally and XUG_GETCMD.OUT$ contains anything other 
    than ADDR(NIL), the OUT$ points to the tree of parse blocks which describe 
    the user's commands; the caller should process the command.  If XUG$GETCMD 
    returns normally and XUG_GETCMD.OUT$ contains ADDR(NIL), then GETCMD has 
    completely processed whatever input was passed (i.e., a built-in command); 
    the caller need take no further action with this command. 
2.  Echoing of command input is subject to the ECHO flag in the XUG_INIT 
    structure and the ECHO flag set via the command processor ECHO command. 
    ECHO Flag in XUG_INIT      Action of XUG$GETCMD 
    ECHO=NEVER_ECHO            Never echo the command. 
    ECHO=ALWAYS_ECHO           Echo the command except if the command is read 
                               from the terminal or if the DVBYTE.TRANS# bit 
                               is set. 
    ECHO=HONOR_FLAG            Echo the command if the input DCB is assigned 
                               to a file. 
                               Echo the command if the output DCB is not 
                               assigned to a terminal. 
                               Echo the command if the input DCB is reading 
                               from the command stream and ECHO is on (i.e., 
                               is set via the command processor ECHO command). 
3.  XUG$GETCMD facilitates error correction by saving command text that the 
    time-sharing user may recall; this feature is provided only for commands 
    of 255 characters or less and for commands entered on one line (without 
    the continuation (;) character).  For example, following a syntax error 
    entering the Escape-D sequence redisplays the command and repositions the 
    cursor to the first reported error. 
4.  XUG$GETCMD can be used to set a pointer to an error in a command which it 
    has not itself read and parsed.  If XUG$GETCMD is called with 
    XUG_GETCMD.ROOT$=ADDR(NIL) (meaning that there is no parse tree) and with 
    XUG_GETCMD.TEXT_ framing the command in error, the XUG$GETCMD service 
    moves the command string into its internal command buffers, sets NCHARS in 
    its parse control block equal to VBOUND(XUG_GETCMD.TEXT_)+1, sets XUG 
    GETCMD.OUT$ equal to ADDR(NIL) (meaning no result), and RETURNs normally. 
    Subsequent calls can be made to XUG$ERRPTR which may set EPOS and USE_EPOS 
    in XUG_GETCMD and echo appropriate portions of the stored command string, 
    as necessary. 
00002
00003
00001
00004
Format: 
CALL XUG$GETDCB (dcbname,dcbloc) ALTRET (label); 
Parameters: 
dcbname    is a TEXTC structure containing a DCB name of the DCB that is to be 
searched for in the DCB table. 
dcbloc    is a variable that identifies where the DCB number is to be 
returned.  The DCB number is returned as an SBIN WORD value. 
Description: 
The XUG$GETDCB service returns a DCB number for an existing DCB or calls 
M$GETDCB to return the DCB number for a DCB which it allocates. 
This service searches the DCB table for the specified DCB.  If it is not 
found, M$GETDCB is called to create it. 
Error Conditions: 
If M$GETDCB takes an alternate return, XUG$GETDCB takes an alternate return 
also, and the error code can be found in the ALTRET frame. 
00002
00003
00001
Format: 
CALL XUG$HELP (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure in which the XUH parameter is 
meaningful.  For details, type: 
HELP (HOSTLIB) XUG_GETCMD 
Description: 
The XUG$HELP service keeps track of whether the last message operation was 
performed by M$ERRMSG or M$HELP; this service calls X$HELP passing parameters 
in the structure XUH_PARAM.  Based on a flag set by XUG$HELP and reset by 
XUG$ERRMSG, the XUG$MOREMSG and XUG$ALLMSG services can determine whether to 
obtain a HELP or an error message. 
Error Conditions: 
If X$HELP takes an alternate return, XUG$HELP calls XUG$ERRMSG with the error 
code in XUH_PARAM and takes the alternate return. 
00002
00003
00001
Format: 
CALL XUG$INIT (xug_getcmd,xug_init) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure. 
xug_init    is the structure built by the %XUG_INIT macro which is described 
in the topic XUG_INIT. 
Description: 
The XUG$INIT service may be used to initialize parameters or flags used by 
XUG$GETCMD.  The user may: 
o   Provide entry pointers designating routines that are to be called by 
    XUG$GETBREAK if a break event occurs; 
o   Set or reset the SYNTAX, COMMANDS, GOODCMD, and/or SPELLING flags; 
o   Specify the address of a PCB (parse control block) which XUG$GETCMD is to 
    use while parsing commands, or request that XUG$INIT allocate a PCB for 
    its own use and return the address of the PCB to the user; 
o   Provide a vector framing a block of memory which XUG$GETCMD is to use for 
    its PCB, input buffer, and parse work area. 
In addition to resetting all parameters that can be specified on the XUG_INIT 
macro, XUG$INIT reinitializes various internal values that are supplied by 
other XUG services.  However, values that are kept in the XUG_GETCMD block are 
not changed, unless there is a corresponding field in the XUG_INIT macro. 
00002
00001
Format: 
CALL XUG$MOREMSG (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure in which the XUH parameter is 
meaningful.  For details, type: 
HELP (HOSTLIB) XUG_GETCMD 
Description: 
The XUG$MOREMSG service calls XUG$ERRMSG or X$HELP as appropriate to get the 
next level message.  The XUG$MOREMSG service consults a flag which is set via 
XUG$HELP and reset via XUG$ERRMSG to determine which service to call. 
Error Conditions: 
Error codes returned by XUG$MOREMSG include those returned by the X$HELP 
library service.  For details, type: 
HELP (HOSTLIB) X$HELP 
00002
00003
00001
Format: 
CALL XUG$OPENOUT (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure in which these parameters are 
meaningful:  FPT, DCB_PARAM, UTIL. 
FPT is an FPT for M$OPEN.  FPT_OPEN.V.DCB# must be set to the number of the 
DCB to be opened, if DCB_PARAM is omitted.  The remaining M$OPEN parameters 
should be set to the desired values.  If omitted, the following default 
values, typical for the OUTPUT command, will be used: 
    %FPT_OPEN (DCB=M$LO, SCRUB=YES, ORG=UR, ACS=SEQUEN, ASN=DEVICE, RES='ME', 
    FUN=CREATE, EXIST=ERROR); 
Other parameters such as SETDCB and REASSIGN may also be specified. 
DCB_PARAM is the number of the DCB to be opened.  This parameter overrides the 
DCB in the FPT_OPEN when both are passed. 
UTIL points to the output block returned by X$PARSE (usually via a prior call 
to XUG$GETCMD) that corresponds to the XUR$OPENOUT_SPEC or XUR$OPENOUT_OPT 
parse node.  See Usage Note 1 for further description of these parse nodes. 
The parse output block overrides the FPT defaults when conflicting information 
is passed by the user. 
Description: 
The XUG$OPENOUT service opens the specified DCB in preparation for a simple 
output function, based on information in the output block referenced by 
out$blk. 
Error Condition: 
If an error occurs, the DCB is left closed and the error is described by 
GETCMD.ERRDCB# and GETCMD.ERR#.  It is the responsibility of the calling 
program to re-open the DCB after an error, if required. 
Usage Notes: 
1.  SYMDEFed parse nodes provided for simple output functions are included in 
    :LIB_SYSTEM.  The following parse nodes are available to direct only the 
    results of one command to another output stream without affecting normal 
    output of the processor: 
    XUR$OPENOUT_OPT which defines the syntax: 
        [[{ON|TO|OVER|INTO}] fid [(optionlist)]] 
    XUR$OPENOUT_SPEC which defines the syntax: 
        {ON|TO|OVER|INTO} fid [(optionlist)] 
    For example, the user's parse nodes could define an output command 
    as follows: 
        OUT_CMD(%T$OUT)    = 'OUT/PUT' XUR$OPENOUT_OPT 
    The parse nodes XUR$OPENOUT_OPT and XUR$OPENOUT_SPEC imply the following: 
    a.  ON|TO    specify that the command is to be errored if the fid 
        references a file which already exists. 
        OVER    specifies that is the fid references an existing file, that 
        file is to be replaced by the output. 
        INTO    specifies that if the fid references an existing file, the 
        output is to be appended to the end of that file. 
        The default is ON. 
    b.  The fid, that specifies the destination of the output, may be any 
        standard CP-6 fid. 
    c.  The optionlist may include any of the following: 
        O[RGANIZATION]={C[ONSECUTIVE]|U[NIT]R[ECORD]} 
        F[ORM]={formname|'formname'} 
        I[XTNSIZE]=number 
        N[TNSIZE]=number 
00002
00003
00001
00004
Format: 
CALL XUG$SETERRMSG (xug_getcmd) ALTRET (label); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure in which the ERRMFID and ERR_CODE 
parameters are meaningful. 
Description: 
The XUG$SETERRMSG service is normally used to establish the error message file 
(ERRMFID) to be used on subsequent calls to XUG$ERRMSG.  M$FID is called to 
obtain the name, account and password of the msgfile-fid.  If ERRMFID is NIL, 
the current error message file is not changed. 
If XUG$SETERRMSG is called with a non-zero error code in ERR_CODE, the value 
in ERR_CODE is saved for use by a subsequent call to XUG$ALLMSG or 
XUG$MOREMSG.  The message displayed when one of these routines is called will 
be the one for the error code itself, not (as is usually the case) the one for 
the next message level.  A call to XUG$ERRMSG with an ERR_CODE of zero is 
equivalent to a call to XUG$MOREMSG.  A call to XUG$ERRMSG with a non-zero 
ERR_CODE will replace the saved error code with the one specified for that 
call. 
Error Conditions: 
If XUG$SETERRMSG takes the alternate return, the error code is stored in the 
ALTRET frame. 
00002
00003
00001
Format: 
CALL XUG$SIMULATE_BREAK (xug_getcmd); 
Parameters: 
xug_getcmd    is an XUG_GETCMD structure. 
Description: 
The XUG$SIMULATE_BREAK service causes a break event to be simulated.  If break 
processing is enabled, the XUG$BREAK routine will be entered as if the user 
had pressed the BREAK key.  If break processing is disabled (see the 
XUG$DISABLE topic), the break event will be recorded for processing at a later 
time (once breaks are re-enabled through a call to XUG$ENABLE). 
00002
00001
Parameters that may be initialized are shown as 'keyword = ' .  Fields that 
are initialized by XUG$INIT or contain returned values are shown in the form 
'fieldname -' .  For a description of each parameter, type: 
HELP (HOSTLIB) XUG_GETCMD param 
where param is:  ALWAYS_SET_PROMPT, BUF$, CONTINUED#, CONTINUE_OK, DCB2_PARAM, 
DCB_PARAM, DISP, ECHO, EOMCHAR#, EPOS, ERR#, ERRDCB#, ERRMFID, ERRMSG_VFC, 
ERR_CODE, F1, F2, F3, FLGLEV, FPT$, INDCB, INFOMSG, NLINES, NODES, OUT$, 
OUTDCB, PASS, PCB$, PP_FUN, PP_ROOT$, PROMPT, PROMPT_VFC, RCVD_PROMPT#, READR, 
RLT$, RPROMPT, SFROUTINE, SKIP_PREPROCESS, SYNERR_NODES$, TEXT, TREAD, 
USE_EPOS, UTIL, XT_PARAM$, or XUH. 
    ALWAYS_SET_PROMPT = {YES|NO} Is initialized by XUG$INIT from the 
    ALWAYS_SET_PROMPT field in the XUG_INIT structure.  This field indicates 
    that XUG$GETCMD must always issue an M$PROMPT before reading a command, 
    even if the prompt specified does not appear to have been changed. 
    BUF$ - PTR Returns the address of the buffer containing the command read 
    by XUG$GETCMD.  RLT$ points to an array containing information on how to 
    interpret this buffer. 
    CONTINUED# - BIT(1) Specifies, if set, that XUG$GETCMD has read a 
    continued command.  This flag is maintained by XUG$GETCMD. 
    CONTINUE_OK = {YES|NO} Specifies, if set, that the command can be 
    continued. The default is YES. If NO is specified, XUG$GETCMD will return 
    to the calling routine without getting another record.  The flag 
    CONTINUED# will be set. 
    DCB2_PARAM = VALUE-DEC(0-?)  Is the DCB number of the second DCB parameter 
    to be used by a routine that has two DCB parameters, e.g., XUG$ERRMSG. 
    The default is DCBNUM(NIL). 
    DCB_PARAM = VALUE-DEC(0-?)  The DCB number of the DCB to be used by the 
    routine being called as the output DCB.  The default is DCBNUM(NIL). 
    DISP = {SAVE|RELEASE} Is the DISP to be used by XUG$CLOSE_DCBS. For legal 
    %EQUs, see M$CLOSE in the Host Monitor Services Reference Manual (CE74). 
    The default is 0, which means SAVE unless FPRG. 
    ECHO - {HONOR_FLAG|ALWAYS_ECHO|NEVER_ECHO} Is initialized by XUG$INIT from 
    the ECHO field in the XUG_INIT structure.  HONOR_FLAG indicates that 
    XUG$GETCMD will echo the command if, and only if the user's echo flag is 
    set.  ALWAYS_ECHO indicates that XUG$GETCMD will echo the command through 
    the user's echo DCB.  NEVER_ECHO indicates that XUG$GETCMD will not echo 
    the command. 
    EOMCHAR# - CHAR(1).  Is a value maintained by XUG$GETCMD which contains 
    the activation character that completed the most recent command.  If 
    XUG$GETCMD receives its command from an activation-less source (e.g., a 
    disk file), EOMCHAR# will contain %EOM_EOR# ('501'O). 
    EPOS = VALUE-DEC(0-?)  On return, specifies the character position at 
    which an error occurred. Refer to USE_EPOS#. 
    ERR# - standard CP-6 error code.  Is the error code that caused XUG$GETCMD 
    to ALTRETURN. 
    ERRDCB = VALUE-DEC(0-?)  Is the DCB number of the DCB on which the error 
    occurred. ERRDCB# is used to obtain variable information which is 
    substituted into the message for special strings %FN, %AC, etc.  If an 
    error message contains those special strings and ERRDCB# = DCBNUM(NIL), 
    the default, then blanks are substituted, or the conditional phrase is not 
    printed.  For a discussion of Field and Phrase Substitution, see M$ERRMSG 
    in the Host Monitor Services Reference Manual (CE74). 
    ERRMFID = PTR Points to the TEXTC string containing the fid of the error 
    message file to be used on subsequent calls to XUG$ERRMSG. If ERRMFID$ = 
    ADDR(NIL), the default error message file will be used. 
    ERRMSG_VFC = VALUE-CHAR(1) Specifies a VFC character to be used by 
    M$ERRMSG.  If ERRMSG_VFC = ' ', the default VFC character will be used. 
    ERR_CODE - standard CP-6 error code.  If set to '0'B, causes the severity 
    field of the last code to be incremented.  In this case, if the severity 
    field exceeds 7 or no message is found, the alternate return is taken. 
    F1 = VARIABLE   Is a vector framing the TEXTC string for %U1 substitution. 
    F2 = VARIABLE   Is a vector framing the TEXTC string for %U2 substitution. 
    F3 = VARIABLE   Is a vector framing the TEXTC string for %U3 substitution. 
    FLGLEV = VALUE-DEC(0-4) Specifies the number of asterisks to print in 
    front of the error message.  The default is 0. 
    FPT$ - PTR  Points to a monitor service FPT for use by the routine called. 
    INDCB = VALUE-DEC(0-?)  Is the DCB number of the input DCB.  The default 
    is DCBNUM(NIL), in which case M$SI is used. 
    INFOMSG = {YES|NO} Specifies that XUG$ERRMSG is not to save the error code 
    of the message issued.  The prior saved error code, if any, remains 
    unchanged.  (The saved error code controls display of additional message 
    levels in response to a "?" command, and is passed to the dialog manager 
    to indicate command errors.)  It is reset on each call to XUG$ERRMSG after 
    it has been examined.  The default is NO. 
    NLINES - SBIN HALF Returns the number of lines of a command read by 
    XUG$GETCMD. 
    NODES = PTR  Points to the top of the parse nodes. 
    OUT$ - PTR Is a pointer returned by XUG$GETCMD into which either 
    P_PCB.OUT$ or an error code is stored.  ERR# is a REDEF of OUT$ for the 
    error code. 
    OUTDCB = VALUE-DEC(0-?)  Is the DCB number of the output DCB.  The default 
    is DCBNUM(NIL). 
    PASS - {LEAVE|BLANK|MODE} Is initialized by XUG$INIT from the PASS field 
    in the XUG_INIT structure.  BLANK indicates the passwords will be blanked. 
    LEAVE indicates that the passwords should not be blanked.  MODE means that 
    passwords will be blanked according to the mode:  they will be blanked for 
    all modes except ONLINE. 
    PCB$ - PTR Is a pointer which will be set to the address of the X$PARSE 
    Parse Control Block which was used by XUG$GETCMD.  If the PCB$ field in 
    the XUG_INIT structure was non-NIL when XUG$INIT was called, PCB$ will be 
    set equal to XUG_INIT.PCB$; otherwise, PCB$ will be set to the address of 
    a PCB built in the XUG$GETCMD work area. 
    PP_FUN = EPTR Points to the user-supplied routine to handle user-defined 
    preprocessor functions, as described under the X$EVAL service. 
    PP_ROOT$ - PTR Is initialized by XUG$INIT from the PP_ROOT parameter of 
    XUG_INIT.  Holds a pointer to the root of the function tree which is to be 
    passed to X$PRE_PROCESS.  (See XUE_PPCB.ROOT$ for details).  If PP_ROOT$ 
    is NIL, GETCMD will pass the standard function tree (XUE_PREEXP) to 
    X$PRE_PROCESS.  This field is ignored if a non-NIL PPCB was specified in 
    the XUG_INIT structure; in this case, the ROOT$ field in that PPCB is 
    honored. 
    PROMPT = CHAR(*) Frames the prompt to use when reading commands from the 
    terminal. 
    PROMPT_VFC = {YES|NO} Specifies, if set, that the first character of the 
    prompt and replacement prompt text is to be used as a VFC character.  The 
    default is NO. 
    RCVD_PROMPT# - BIT(1) If set, specifies that XUG$GETCMD received the 
    prompt specified by XUR_GETCMD.PROMPT_.  This flag is maintained by 
    XUG$GETCMD. 
    READR = EPTR Points to a procedure to be called to get the command record 
    to be parsed, usually NOT from COMMAND STREAM.  If the last record is 
    continued, XUG$GETCMD will use FPT_GETCMD.READR$$ to decide where to get 
    the next record.  Every time that the READR$ is called, XUG$GETCMD must 
    receive a record.  It is the READR$ routine's responsibility to set the 
    XUG_GETCMD.TREAD# flag to indicate whether the command was read from the 
    terminal or not.  All VFC and PROMPT characters must be removed from the 
    buffer before return to XUG$GETCMD. 
    The READR$ routine is called as follows: 
    CALL READR$ (buf,ars,readr$[,err][,eomchar]) ALTRET (label); 
    where: 
    buf    is a vector framing a 300 character buffer to contain the record 
    read. 
    ars     is an SBIN word to contain the actual record size of the record 
    read. 
    readr$    is an EPTR initialized to the address of the READR$ routine, 
    that is used to reset SUB_GETCMD.READR$ on return. 
    err    returns a standard CP-6 error code to be passed on to the caller of 
    XUG$GETCMD when the routine altreturns. 
    eomchar    returns the activation character that completes the read. 
    RLT$ - PTR Returns the address of an array containing the length of each 
    line of a command read by XUG$GETCMD.  The XUG_RLT macro describes the 
    structure of this array.  The NLINES field in this structure defines the 
    size of the array. 
    RPROMPT = CHAR(*) Is a vector framing the replacement prompt. If 
    specified, this string replaces the actual prompt when the command is 
    echoed. 
    SFROUTINE = EPTR Points to a procedure to be called for success, failure, 
    and preparse nodes. 
    The calling sequence is 
    CALL user_routine ( parse_param ); 
    where: 
    parse_param    is the PARSE$PARAM parameter block supplied by X$PARSE, as 
    described in HELP (HOSTLIB) X$PARSE. 
    SKIP_PREPROCESS = {YES|NO} Specifies that XUG$GETCMD is not to do 
    PRE-PROCESSing on the first record, but to do PRE-PROCESSing on subsequent 
    reads.  XUG$GETCMD will reset this bit after XUG$GETCMD recognizes that it 
    was set and XUG$GETCMD passed on doing the PRE-PROCESSing. 
    SYNERR_NODES$ - PTR Is a pointer returned by GETCMD, which points to the 
    root of the syntax tree on which the most recent syntax error occurred. 
    This value is retained so that the "enter a ? for spelling correction 
    and/or legal choices" code will work correctly even if the NODES$ pointer 
    is altered by the user between calls to XUG$GETCMD. 
    TEXT = VARIABLE Is a vector framing a text string to be used as the first 
    line of input to the parser when input is to be read from other than the 
    input DCB (e.g., from JIT.CCBUF).  The default is VECTOR(NIL). 
    TREAD = {YES|NO} Specifies whether the command was read from a terminal or 
    a file.  This determines whether or not the command line needs to be 
    echoed.  If TREAD is set, the command came directly from the user's 
    terminal, so it does not need to be echoed.  If TREAD is reset, the 
    command may need to be echoed, subject to the setting of ECHO.  TREAD is 
    maintained by the routine that reads command lines.  If that is a READR$ 
    routine, that routine must set or reset XUG_GETCMD.TREAD# each time it is 
    called. 
    USE_EPOS = {YES|NO} Specifies, if set, to use EPOS# for the character 
    position at which the error occurred.  If reset, then P_PCB.HI_CHAR is to 
    be used. The default is NO. 
    UTIL = VARIABLE Locates an additional parameter for use by the routine 
    called. 
    XT_PARAM$ - PTR Points to the parameter block passed to XTX$ADAPT when the 
    program is running under a dialog.  See the CP-6 ADAPT Reference (HA12) 
    for more information. 
    XUH = PTR Points to the parameter block passed to X$HELP and described in 
    the discussion of the X$HELP service. 
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
00041
00042
00043
00044
00045
For a description of each parameter, type: 
HELP (HOSTLIB) XUG_INIT param 
where param is one of the following:  ABORT, ADAPT, ADDL_NRECS, 
ALWAYS_SET_PROMPT, BRKMSG, CMDSZ, COMMANDS, CONTINUE, DONT_REREAD_CCBUF, 
DONT_STRIP_PROMPT, ECHO, GOODCMD, INHIBIT_DATE, INHIBIT_DIRECTORY, INHIBIT_DO, 
INHIBIT_END, INHIBIT_ENTER, INHIBIT_ERASE, INHIBIT_HELP, INHIBIT_NULL, 
INHIBIT_OUTPUT, INHIBIT_PRINT, INHIBIT_QMARK, INIT_NRECS, MOREMEM, 
NO_DOWNGRADE, PARAMS$ PASS, PCB, POST_EXEC, PPCB, PP_DCB, PP_PROCNAME, 
PP_ROOT, PREPROCESS, PREPROCESSOR PRE_EXEC, PROCACCT, PROCNAME, REQ_PROMPT, 
SPELLING, SPHANDLE, SYNTAX, WORK, or WSEG. 
    ABORT = EPTR Points to a procedure to be called when the user wants to 
    abort the command being read.  ABORT must not be NIL and must not RETURN 
    or ALTRETURN if XUG$BREAK is to be used.  The BREAK frame will be removed 
    from the TCB before XUG$GETCMD_COMMON calls the ABORT routine. 
    ADAPT = EPTR Points to the dialog manager procedure to be called if the 
    program is started under an ADAPT dialog, or if the ENTER built-in command 
    is used to start a dialog within the program.  The default is XTX$ADAPT. 
    Programs that cannot run under ADAPT dialogs must specify ADAPT=NIL.  See 
    the CP-6 ADAPT Reference (HA12) for more information. 
    ADDL_NRECS = VALUE-DEC(0-?)  Specifies the number of entries to be added 
    to the array for the character position table of the records read due to 
    continuation. The default is 100.  This number specifies how many 
    continued records can be read before having to expand the table again. 
    ALWAYS_SET_PROMPT = {YES|NO} Indicates whether XUG$GETCMD should always 
    issue an M$PROMPT before reading, even if the current prompt maintained by 
    XUG$GETCMD does not appear to have been changed.  The default is NO. 
    BRKMSG = EPTR Points to a procedure to be called to output a break message 
    when a break has been received.  BRKMSG is optional; if it is not 
    supplied, or if the BRKMSG routine altreturns, the standard message 
    "Break!  C to continue." is output. 
    CMDSZ = VALUE-DEC(0-?)  Specifies the length of a command line.  For 
    commands greater than CMDSZ# in length the command will have to be 
    continued. The maximum value possible for CMDSZ# is 300, the default. 
    COMMANDS = {YES|NO} Indicates that if the command has failed to match any 
    of the syntax of the user's parse nodes, then XUG$GETCMD should compare 
    the command to its parse nodes of built-in commands.  The parse nodes 
    describe the commands listed below, except for commands eliminated by 
    INHIBIT_commandname=YES options.  The default is COMMANDS=YES.  The 
    built-in commands are as follows: 
      DATE 
      {DIR|DIRECTORY} 
      {DO|!} 
      {E|EN|END} 
      ENTER 
      ERASE 
      {[E]X|[E]XI|[E]XIT} 
      TIME 
      {H|HE|HEL|HELP} 
      {OUT|OUTP|OUTPU|OUTPUT} 
      PRINT 
      {Q|QU|QUI|QUIT} 
      ? 
      ?? 
    The functions performed by these commands are as described for IBEX.  See 
    the IBEX HELP facility for details.  The {DO|!} passes the command to the 
    command processor for processing.  If used in an XEQ or BATCH job, the "!" 
    must not be in column one or the user can use DO.  The ! command may be 
    preceded by blanks or by the processor's prompt. 
    CONTINUE = EPTR Points to a procedure to be called when a user wants to 
    continue after interruption due to a break. CONTINUE is optional.  The 
    BREAK frame will still be present on the TCB when the continue routine is 
    entered after the call by XUG$GETCMD_COMMON. 
    DONT_REREAD_CCBUF = {YES|NO} Specifies, if YES, that only the text 
    actually parsed is to be placed in the reread buffer after a syntax error 
    parsing the program's invocation command line.  The default is NO, 
    indicating that the entire command line is to be reread, even if only the 
    options portion of it was parsed. 
    DONT_STRIP_PROMPT = {YES|NO} Specifies whether the logic to remove the 
    program's prompt from the beginning of commands is to be overridden.  YES 
    specifies no check for a prompt at the beginning of each command line.  NO 
    specifies that the prompt is to be removed if it is present.  The default 
    is NO. 
    ECHO = {HONOR_FLAG|ALWAYS_ECHO|NEVER_ECHO} Indicates whether to ECHO the 
    command or not.  HONOR_FLAG indicates that XUG$GETCMD will echo the 
    command if, and only if the user's ECHO flags is set.  ALWAYS_ECHO 
    indicates that XUG$GETCMD will echo the command through the user's echo 
    DCB.  NEVER_ECHO indicates that XUG$GETCMD will not echo the command.  The 
    default is HONOR_FLAG. 
    GOODCMD = {YES|NO} Specifies, if YES, that XUG$GETCMD should detect errors 
    itself, without returning to the caller.  Note that XUG$GETCMD can only 
    process "simple" errors (syntax errors, invalid preprocessor expressions, 
    errors in built-in commands, etc.)  in commands entered from the terminal 
    (i.e., the TREAD# flag is set).  Errors occurring in non-interactive 
    commands, and serious (monitor) errors occurring in any command, will 
    result in an ALTRETURN regardless of the setting of the GOODCMD flag.  The 
    default is NO. 
    INHIBIT_DATE = {YES|NO} Specifies that the built-in commands DATE and TIME 
    should not be recognized or executed.  The default is NO. 
    INHIBIT_DIRECTORY = {YES|NO} Specifies that the built-in command DIRECTORY 
    should not be recognized or executed.  The default is NO. 
    INHIBIT_DO = {YES|NO} Specifies that the built-in commands DO and ! should 
    not be recognized or executed.  The default is NO. 
    INHIBIT_END = {YES|NO} Specifies that the built-in commands END, XIT, and 
    QUIT should not be recognized or executed.  The default is NO. 
    INHIBIT_ENTER = {YES|NO} Specifies that the built-in command ENTER should 
    not be recognized or executed. 
    INHIBIT_ERASE = {YES|NO} Specifies that the built-in command ERASE should 
    not be recognized or executed.  The default is NO. 
    INHIBIT_HELP = {YES|NO} Specifies that the built-in command HELP should 
    not be recognized or executed.  The default is NO. 
    INHIBIT_NULL = {YES|NO} Specifies that the built-in null (empty) command 
    should not be recognized or executed.  The default is NO. 
    INHIBIT_OUTPUT = {YES|NO} Specifies that the built-in command OUTPUT 
    should not be recognized or executed.  The default is NO. 
    INHIBIT_PRINT = {YES|NO} Specifies that the built-in command PRINT should 
    not be recognized or executed.  The default is NO. 
    INHIBIT_QMARK = {YES|NO} Specifies that the built-in commands ? and ?? 
    should not be recognized or executed.  The default is NO. 
    INIT_NRECS = VALUE-DEC(0-?)  Specifies the initial number of entries in 
    the array for the character position table of the records read due to 
    continuation.  This number specifies how many continued records can be 
    read before having to expand the table.  The default is 100. 
    MOREMEM = EPTR Points to a procedure to be called if XUG$GETCMD needs more 
    memory and the user maintains the memory for XUG$GETCMD. 
    The calling sequence is 
    CALL user_routine ( words-needed , work-vector , errcode ) [ALTRET ( label 
    )]; 
    where: 
    words-needed    is a SBIN WORD containing the number of words needed. If 
    positive, this is a request to allocate more memory.  If negative, this is 
    a request to free memory. 
    work-vector    returns a vector framing the entire work area on a normal 
    return.  The returned vector is checked to insure that an area of the 
    proper size has been allocated or freed contiguous with the old work area. 
    errcode    returns a standard CP-6 error code to be passed back to the 
    caller of XUG$GETCMD when the MOREMEM routine altreturns. 
    NO_DOWNGRADE = {YES|NO} Specifies, if YES, that only the most-severe 
    (highest flaglevel) error message for each command should be remembered; 
    less-severe messages will be considered to be additional information, and 
    will not be remembered for display of additional message levels if the 
    user subsequently enters "?" or "??".  The default is NO. 
    PARAMS$ - PTR Is a pointer into which the address of the XUG_PARAMS 
    structure will be returned. 
    PASS = {LEAVE|BLANK|MODE} Indicates whether the PASSWORD should be blanked 
    or not.  BLANK indicates the passwords will be blanked.  LEAVE indicates 
    that the passwords should not be blanked.  MODE means that passwords will 
    be blanked according to the mode:  they will be blanked for all modes 
    except ONLINE.  The default is LEAVE. 
    PCB = PTR Is an optional pointer which, if present, will point to the 
    Parse Control Block which XUG$GETCMD is to use when calling X$PARSE. The 
    default is NIL, which indicates that XUG$INIT is to build a PCB in its 
    work area. 
    POST_EXEC = EPTR Points to a procedure to be called AFTER one of the 
    built-in commands is executed. 
    The calling sequence is 
    CALL user_routine ( xug_getcmd , node-code ) [ ALTRET ( label ) ]; 
    where: 
    xug_getcmd    is the XUG_GETCMD structure passed to XUG$GETCMD. 
    node-code    is the parse node code for the built-in command being 
    processed, as defined by EQUs of the form %XUG_CMD_? in the XU_SUBS_C 
    include file. 
    Note:  If an ALTRETurn occurs, the error code in xug_getcmd.ERR# will be 
    reported in the same way as other errors in processing a built-in command. 
    PPCB = PTR Points to the Preprocessor's Control Block. This is passed to 
    X$PRE_PROCESS if the flag PREPROCESS# is set. 
    PP_DCB = VALUE-DEC(0-?)  Is a DCB number for X$PRE_PROCESS to use for test 
    opens on such functions as $FID_EXIST.  If X$PRE_PROCESS needs a DCB 
    (e.g., for a test open), and the user has not specified a DCB number, then 
    XUG$GETCMD acquires a DCB and passes its number to X$PRE_PROCESS.  (The 
    dynamically acquired DCB is released when X$PREPROCESS returns control to 
    XUG$GETCMD.) 
    PP_PROCNAME = VARIABLE Is a vector framing the name of the processor that 
    is using X$EVAL. The name must be in TEXTC form, preferably stored in a 
    VLP_NAME structure.  If PP_PROCNAME is NIL then the default will be taken 
    from M$LM. 
    PP_ROOT = VARIABLE Identifies the node which lies at the root of a PARTRGE 
    tree that defines non-standard preprocessor functions (see XUE_PPCB.ROOT$ 
    for details). 
    PREPROCESS = {YES|NO} Indicates, if YES, that the user wants XUG$GETCMD to 
    do preprocessing on lines containing a percent (%) sign.  The type of 
    preprocessing depends on the value given for PREPROCESSOR.  The default is 
    NO. 
    PREPROCESSOR = EPTR Provides the name of a routine to be called to do 
    preprocessing of commands.  This is meaningful only if PREPROCESS = YES is 
    also specified.  If PREPROCESSOR=NIL, command variable substitution will 
    be performed; if the word immediately following a percent (%) sign is the 
    name of an IBEX command variable, the value of that variable is 
    substituted before the command is parsed.  Otherwise, the specified 
    routine (usually X$PRE_PROCESS) is called to perform any necessary 
    preprocessing.  The default is NIL. 
    PRE_EXEC = EPTR Points to a procedure to be called BEFORE one of the 
    built-in commands is executed. 
    The calling sequence is 
    CALL user_routine ( xug_getcmd , node-code ) [ ALTRET ( label ) ]; 
    where: 
    xug_getcmd    is the XUG_GETCMD structure passed to XUG$GETCMD. 
    node-code    is the parse node code for the built-in command being 
    processed, as defined by EQUs of the form %XUG_CMD_? in the XU_SUBS_C 
    include file. 
    Note:  If an ALTRETurn occurs, the error code in xug_getcmd.ERR# will be 
    reported in the same way as other errors in processing a built-in command. 
    PROCACCT_ = VARIABLE Locates a VLP_ACCT area containing the account of the 
    processor for which a HELP message is requested.  The default, NIL, is the 
    account of the currently running processor. 
    PROCNAME_ = VARIABLE Locates a VLP_NAME area containing the name of the 
    processor for which a HELP message is requested. 
    REQ_PROMPT = {YES|NO} Indicates that the prompt must be the first 
    character(s) of the command line, beginning in column 1. Default is NO. If 
    REQ_PROMPT is set to YES, and the prompt is not at the beginning of the 
    command line, XUG$GETCMD will ALTRETURN without doing any parsing. 
    SPELLING = {YES|NO} Indicates whether XUG$GETCMD should attempt to 
    identify and report misspelled keywords in commands.  The default is YES. 
    SPHANDLE = EPTR Points to a procedure to be called before another record 
    is read on a continued command. 
    The calling sequence is 
    CALL user_routine ( xug_getcmd , parse_param ); 
    where: 
    xug_getcmd    is the XUG_GETCMD structure passed to XUG$GETCMD. 
    parse_param    is the PARSE$PARAM parameter block supplied by X$PARSE, as 
    described in HELP (HOSTLIB) X$PARSE. 
    NOTE:  If this routine is being used to setup a continuation prompt, the 
    PROMPT and/or RPROMPT parameters should be reset to frame the continuation 
    prompt.  When the continuation reads are finished, the original prompts 
    will be restored by XUG. 
    SYNTAX = {YES|NO} Specifies whether the special command-syntax feature of 
    XUG$GETCMD is to be used. The default is YES. 
    WORK = VARIABLE Locates an area of memory (which must be at least 500 
    words long and must contain an integral number of doublewords) which 
    XUG$GETCMD is to use for its parse control block, input buffer, parse work 
    area, and other data.  This field is optional.  If WORK_ is set to 
    VECTOR(NIL), the default, then XUG$GETCMD will allocate a work area using 
    the segment number specified in XUG_INIT.WSEG#.  If the user specifies a 
    work area through WORK_, this area will not be expanded by 
    XUG$GETCMD_COMMON. 
    WSEG = VALUE-DEC(0-8) Specifies what data segment to use as the work area 
    instead of the user supplying one.  Acceptable values are (0, 3, 4, 5, 6, 
    7, 8) (i.e. 3 specifies that Data Segment 3 is to be used to allocate are 
    to use for the work space.) If 0 is specified, then the XUG$INIT_COMMON 
    will use the next available data segment.  XUG_INIT.WSEG# will only be 
    used if XUG_INIT.WORK$ is set to VECTOR(NIL). 
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
00041
00042
00043
00044
00045
The CP-6 system provides a comprehensive HELP facility for display of 
information stored in a central location.  HELP is used primarily to provide 
quick reference information on system or user processors.  HELP messages for 
each processor can be stored in a separate data base which may be available 
throughout the system and which may be utilized to produce other forms of 
documentation. 
The user calls the X$HELP library service specifying the text of the HELP 
command and some additional information.  X$HELP in turn calls X$PARSE to 
parse the text and then calls M$HELP to access the data base.  The X$HELP 
service isolates the caller from the complexities of M$HELP and provides 
uniform handling of HELP commands by all processors.  The X$HELP service 
itself may be called by means of the XUG$HELP or XUR$HELP services which 
further simplify the task of the calling processor. 
For a description of each parameter, type: 
HELP (HOSTLIB) XUH_PARAM param 
where param is:  ALL, CHARPOS, ERR, ERRDCB, HELP, KEYWORD, MORE, NAME, 
OUTDCB1, OUTDCB2, PROCACCT, PROCNAME, PROCPASS, TOPICS_PARAM, or VFC. 
ALL 
ALL = {YES|NO}    indicates, if YES, that the user submitted the ??  command 
requesting all remaining help messages following the message previously 
requested.  When ALL is set, the XUH_PARAM structure must be unchanged since 
the previous call to X$HELP.  ALL is reset to NO on exit from X$HELP. 
CHARPOS 
CHARPOS = VALUE-DEC(0-n)    on return from X$HELP, contains the position in 
the text string (i.e., HELP=variable) where X$PARSE detected a syntax error. 
ERR 
ERR - VALUE-BIT(36)    on return from X$HELP, contains an error code in 
standard CP-6 error code format if an error occurred. 
ERRDCB 
ERRDCB = VALUE-DEC(0-n)    on return from X$HELP, specifies the number of the 
DCB on which an error occurred on output.  The fully specified name of the 
field is XUH_PARAM.ERR_DCB#. 
HELP 
HELP = VARIABLE    locates a buffer containing the text of the HELP command 
(without the HELP keyword) in TEXTC format.  If HELP is specified, the KEYWORD 
parameter must not be specified. 
KEYWORD 
KEYWORD = VARIABLE    locates an area containing a keyword.  The keyword is 
typically the verb of a command or an option.  This parameter allows programs 
to ask explicitly for HELP for a particular topic.  For example, after a 
syntax error or command, it can call X$HELP specifying KEYWORD to report the 
correct syntax to the user.  If KEYWORD is specified, the HELP parameter must 
not be specified.  The default is NIL. 
MORE 
MORE = {YES|NO}    indicates, if YES, that the user submitted the ?  command 
requesting the next help message following the message previously requested. 
When MORE is set, the XUH_PARAM structure must be unchanged since the previous 
call to X$HELP.  MORE is reset to NO on exit from X$HELP. 
NAME 
NAME = VALUE-CHAR(30)    is the name for the structure.  The default is 
XUH_PARAM. 
OUTDCB1 
OUTDCB1 = DCBNAME    is the first DCB through which to output the HELP 
message.  If both OUTDCB1 and OUTDCB2 are omitted, then M$DO is used. 
OUTDCB2 
OUTDCB2 = DCBNAME    is the second DCB through which to output the HELP 
message.  Correspondence checking of OUTDCB1 and OUTDCB2 DCBs is performed. 
PROCACCT 
PROCACCT = VARIABLE    locates a VLP_ACCT area containing the account of the 
data base from which HELP is requested.  The default is the account of the 
currently running processor. 
PROCNAME 
PROCNAME = VARIABLE    locates a VLP_NAME area containing the name of the 
processor for which a HELP message is requested.  The processor name must not 
exceed 24 characters.  This name is used by M$HELP to find the data base which 
by convention is of the form HELP:processorname:l (where l is the optional 
native language byte from the JIT).  The default is the name of the currently 
running processor. 
PROCPASS 
PROCPASS = VARIABLE    locates a VLP_PASS area containing the password for the 
data base from which HELP is requested.  The default is NIL. 
PROCPSN 
PROCPSN = VARIABLE    locates an area containing the packset name of the 
database from which HELP is being requested.  The default is NIL. 
TOPICS 
TOPICS = {YES|NO}    indicates, if YES, that all available topics are to be 
listed for the user.  TOPICS=YES is used if a topic specified on a previous 
HELP command is unknown and the user then enters a ? or ?? command.  TOPICS is 
reset to NO on exit from X$HELP. 
VFC 
VFC = VALUE-CHAR(1)    specifies a vertical format control character.  This 
field is currently unused. 
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
The XUM services maintain a Least Recently Used (LRU) list. 
The LRU list operates under these assumptions: 
o   When the user declares a new item to be inserted into the list (via 
    XUM$CREATE_NEW_ITEM), that item will become the least recently used. 
o   When the user requests the least recently used item (via 
    XUM$GET_LRU_ITEM), that item becomes the most recently used in the list. 
Entries in the LRU list consist of two words:  one of these words is available 
for user access; the other word must not be altered by the user.  A pointer is 
passed back to the user giving access to the one word of storage for a newly 
created item; the user must store this pointer as it is the only way of 
communicating to the XUM services the location of a specific item in the list. 
The user must provide a workspace for use in conjunction with the XUM 
services, via a call to XUM$INIT_WORKSPACE. 
For a brief description of each XUM service, type: 
HELP (HOSTLIB) XUM service 
where service is one of the following:  XUM$CREATE_NEW_ITEM, XUM$DELETE_ITEM, 
XUM$GET_LRU_ITEM, XUM$GET_MRU_ITEM, XUM$INIT_WORKSPACE, XUM$MAKE_ITEM_LRU, or 
XUM$MAKE_ITEM_MRU. 
  Service        Purpose 
  XUM$CREATE_NEW_ITEM 
                 Create an entry in the Least Recently Used (LRU) list for a 
                 new item. 
  XUM$DELETE_ITEM 
                 Delete a specified item in the LRU list. 
  XUM$GET_LRU_ITEM 
                 Return the least recently used item from the LRU list and 
                 make the new item the most recently used item. 
  XUM$GET_MRU_ITEM 
                 Return the most recently used item in the LRU list. 
  XUM$INIT_WORKSPACE 
                 Format the workspace into the LRU list. 
  XUM$MAKE_ITEM_LRU 
                 Move any specified item to the LRU position. 
  XUM$MAKE_ITEM_MRU 
                 Move any specified item to the most recently used position. 
00001
00002
00003
00004
00005
00006
00007
Format: 
CALL XUM$CREATE_NEW_ITEM (item_ptr,workspace) ALTRET (label); 
Parameters: 
item_ptr    is the pointer the user receives which can be used to reference 
this specific LRU item.  This is also the pointer the user receives which 
points to the area in which the user can store one word of information. 
workspace    is a vector framing the LRU list workspace. 
Description: 
The XUM$CREATE_NEW_ITEM service creates an entry in the LRU list for a new 
item.  The new item becomes the least recently used item in the list.  After 
the item is created, the user is passed a pointer which is used both as a 
reference to this LRU item and as pointer to the area where the user can store 
one word of data.  This pointer should be stored so that the user can 
reference this item later. 
Error Conditions: 
The ALTRETurn is taken if the workspace has been used up with previous 
creates, or if the user did not pass two parameters. 
00002
00003
00001
Format: 
CALL XUM$DELETE_ITEM (item_ptr,workspace) ALTRET (label); 
Parameters: 
item_ptr    is a pointer that references the LRU item to be deleted.  It is 
the same pointer as returned from XUM$CREATE_NEW_ITEM, when this item was 
created.  On return, this pointer will be ADDR(NIL). 
workspace    is a vector framing the LRU list workspace. 
Description: 
The XUM$DELETE_ITEM service deletes any specified item in the LRU list. 
Error Conditions: 
The ALTRETurn is taken if the item to be deleted does not exist in the LRU 
list. 
00002
00003
00001
Format: 
CALL XUM$GET_LRU_ITEM (item_ptr,workspace) ALTRET (label); 
Parameters: 
item_ptr    is a pointer returned to the user that points to the word of user 
storage that was the least recently used item. 
workspace    is a vector framing the LRU list workspace. 
Description: 
The XUM$GET_LUR_ITEM service returns the least recently used item from the LRU 
list and also makes this item the most recently used. 
Error Conditions: 
The ALTRETurn is taken when the LRU list is empty, or two parameters were not 
passed to the routine. 
00002
00003
00001
Format: 
CALL XUM$GET_MRU_ITEM (item_ptr,workspace) ALTRET (label); 
Parameters: 
item_ptr    is a pointer returned to the user that points to the item that was 
most recently used. 
workspace    is a vector framing the LRU list workspace. 
Description: 
The XUM$GET_MRU_ITEM service returns the most recently used item in the LRU 
list. 
Error Conditions: 
The ALTRETurn is taken if the LRU list is empty, or if two parameters were not 
passed to the routine. 
00002
00003
00001
Format: 
CALL XUM$INIT_WORKSPACE (workspace) ALTRET (label); 
Parameters: 
workspace    is a vector framing an area of size (number of items * 2 + 3). 
The workspace must be word-aligned.  The number of items must be the maximum 
value the list is going to be requested to maintain. 
Description: 
The XUM$INIT_WORKSPACE service formats the workspace into a Least Recently 
Used (LRU) list.  Each entry in the list consists of two words.  This service 
is called only once, to initialize the LRU list. 
Error Conditions: 
The ALTRETurn is taken if the workspace size is less than five or not word 
aligned, or if the user didn't pass a parameter (vector). 
00002
00003
00001
Format: 
CALL XUM$MAKE_ITEM_LRU (item_ptr,workspace) ALTRET (label); 
Parameters: 
item_ptr    is a pointer which references a particular item in the LRU list 
(this is also the pointer to the user's one word data area) and makes this 
item the least recently used. 
workspace    is a vector framing the LRU list workspace. 
Description: 
The XUM$MAKE_ITEM_LRU service moves any specified item to the least recently 
used position.  A subsequent call to XUM$GET_LRU_ITEM returns this same 
pointer. 
Error Conditions: 
The ALTRETurn is taken if the LRU list is empty, or two parameters were not 
passed to the routine. 
00002
00003
00001
Format: 
CALL XUM$MAKE_ITEM_MRU (item_ptr,workspace) ALTRET (label); 
Parameters: 
item_ptr    is the same pointer that the XUM$CREATE_NEW_ITEM service returns. 
It is used to reference the item which the user placed into the LRU list. 
workspace    is a vector framing the LRU list workspace. 
Description: 
The XUM$MAKE_ITEM_MRU service takes any item in the LRU list which is 
referenced by item_ptr and logically moves it to the most recently used 
position. 
Error Conditions: 
The ALTRETurn is taken if the LRU list is empty, or two parameters were not 
passed to the routine. 
00002
00003
00001
The XUO routines can be categorized as follows: 
Initialization Services:  XUO$OUINIT, XUO$BUFINIT. 
Services to Resolve Forward References:  XUO$FRWD_REF. 
Services to Build Object Unit Records: 
XUO$DBGNAME             XUO$RELOC 
XUO$DNAME               XUO$RNAME 
XUO$EDEF                XUO$SDEF 
XUO$EREF                XUO$SDEF_CONST 
XUO$EXST                XUO$SECTBUILD 
XUO$EXSTNUM             XUO$SECTNAME 
XUO$HEADNAME            XUO$SECTSIZE 
XUO$HEADSTART           XUO$SEGDEF 
XUO$HEAD_SEVERITY       XUO$SEGDEF_CONST 
XUO$INTNTRY             XUO$SEGREF 
XUO$LOGBLKALLOC         XUO$SREF 
XUO$LOGBLKEXSTINIT      XUO$VREBL 
XUO$LOGBLKEXSTTERM      XUO$VREBLNUM 
XUO$LOGBLKNOAUTO        XUO$VREBL_CONT 
XUO$LOGBLKVREBLINIT     XUO$VREBL_CONT_ADJ 
XUO$LOGBLKVREBLTERM     XUO$VREBL_CONT_ET 
XUO$PRGM                XUO$VREBL_CONT_SET 
Termination Services:  XUO$OUTERM. 
For the description of a specific service, type: 
HELP (HOSTLIB) XUO servicename 
  Service       Purpose 
  XUO$BUFINIT 
                Change the default buffer sizes. 
  XUO$DBGNAME 
                Build an entry in the Procedure Names Debug Record (record 
                type %TYPDBGNAM). 
  XUO$DNAME 
                Build an entry in the Externally Defined Names Record (record 
                type %TYPDNAM). 
  XUO$EDEF 
                Build an entry in the External Procedure Definition Record 
                (record type %TYPEDEF). 
  XUO$EREF 
                Build an entry in the External Procedure Reference Record 
                (record type %TYPEREF). 
  XUO$EXST 
                Build an entry in the Executable Statements Debug Record 
                (record type %TYPEXST). 
  XUO$EXSTNUM 
                Return the number of the next executable statement debug 
                entry. 
  XUO$FRWD_REF 
                Resolve forward references. 
  XUO$HEADNAME 
                Build the Head Record key. 
  XUO$HEADSTART 
                Build the start address field of the Head Record. 
  XUO$HEAD_SEVERITY 
                Build the severity level field of the Head Record. 
  XUO$INTNTRY 
                Add entries to the Internal Entry Debug Record (record type 
                %TYPINTNTRY). 
  XUO$LOGBLKALLOC 
                Used in building Logical Block Debug Records (record type 
                %TYPLOGBLK). 
  XUO$LOGBLKEXSTINIT 
                Build Logical Block Debug Records (record type %TYPLOGBLK). 
  XUO$LOGBLKEXSTTERM 
                Finish building the Logical Block Debug Record (record type 
                %TYPLOGBLK). 
  XUO$LOGBLKNOAUTO 
                Used in building Logical Block Debug Records (record type 
                %TYPLOGBLK). 
  XUO$LOGBLKTERM 
                Used in building Logical Block Debug Records (record type 
                %TYPLOGBLK). 
  XUO$LOGBLKVREBLINIT 
                Used in building the Logical Block Debug Records (record type 
                %TYPLOGBLK). 
  XUO$LOGBLKVREBLTERM 
                Used in building Logical Block Debug Records (Record type 
                %TYPLOGBLK). 
  XUO$OUINIT 
                Perform initialization prior to building the object unit. 
  XUO$OUTERM 
                Terminate object unit generation. 
  XUO$PRGM 
                Generate Program Record entries (record type %TYPPROG). 
  XUO$PRGM_TEXT 
                Generate Program Record entries (record type %TYPPROG, subtype 
                %SUBTYPPROG). 
  XUO$RELOC 
                Generate Relocation Directives record entries (record type 
                %TYPPROG, subtype %SUBTYPREL). 
  XUO$RNAME 
                Build an entry into the Externally Referenced Names Record 
                (record type %TYPRNAM). 
  XUO$SDEF 
                Build an entry in the External Data Definition Record (record 
                type %TYPSDEF). 
  XUO$SDEF_CONST 
                Build an entry in the External Data Definition Record (record 
                type %TYPSDEF) for CONSTANT entries. 
  XUO$SECTBUILD 
                Build an entry in the Section Record (record type %TYPSECT). 
  XUO$SECTNAME 
                This routine enters the section name pointer into a previously 
                created Section Record entry. 
  XUO$SECTSIZE 
                Enter the section size into a previously created entry in the 
                Section Record. 
  XUO$SEGDEF 
                Build an entry in the External Segment Definition Record 
                (record type %TYPSEGDEF). 
  XUO$SEGDEF_CONST 
                Build an entry in the External Segment.  Definition Record 
                (record type %TYPSEGDEF). 
  XUO$SEGREF 
                Build an entry in the External Segment Reference Record 
                (record type %TYPSEGREF). 
  XUO$SREF 
                Build an entry in the External Data Reference Record (record 
                type %TYPSREF). 
  XUO$VREBL 
                To build entries in the Variable Debug Record (record type 
                %TYPVREBL). 
  XUO$VREBLNUM 
                Return the number of the next entry in the Variable Debug 
                Record (record type %TYPVREBL). 
  XUO$VREBL_CONT 
                Build continuation entries in the Variable Debug Record 
                (record type %TYPVREBL). 
  XUO$VREBL_CONT_ADJ 
                Build Variable Debug Record continuation entries (record type 
                %TYPVREBL). 
  XUO$VREBL_CONT_ET 
                Build continuation entries in Variable Debug Record (record 
                type %TYPVREBL) for variables with Data Type = Enumerated 
                Type. 
  XUO$VREBL_CONT_SET 
                Build continuation entries in the Variable Debug Record 
                (record type %TYPVREBL) for variables with Data Type = Set. 
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
Format: 
CALL XUO$BUFINIT (Defined Names Word Count, 
                  Referenced Names Word Count, 
                  Section Entry Count, 
                  Procedure Definition Entry Count, 
                  Procedure Reference Entry Count, 
                  Data Definition Entry Count, 
                  Data Reference Entry Count, 
                  Segment Definition Entry Count, 
                  Segment Reference Entry Count, 
                  Program Buffer Size, 
                  Relocation Buffer Size, 
                  Logical Block Entry Count, 
                  Internal Entries Entry Count, 
                  Executable Statements Entry Count, 
                  Debug Variable Entry Count, 
                  Debug Name Word Count, 
                  Number of Buffers); 
Input: 
    Defined Names Word Count  UBIN ALIGNED 
                          Represents the page size in words of 
                          the Externally Defined Names Record 
                          (type %TYPDNAM).  Default is 100, Minimum is 8. 
    Referenced Names Word Count UBIN ALIGNED 
                          Represents the page size in words of 
                          the Externally Referenced Names Record 
                          (type %TYPRNAM).  Default is 100, Minimum is 8. 
    Section Entry Count  UBIN ALIGNED 
                          Represents the total number of entries 
                          in the Section Record (type %TYPSECT). 
                          NOTE:  Since this record is not paged, 
                          the maximum number of section entries 
                          that is expected to be generated must 
                          be specified.  Default is 30. 
    Procedure Definition Entry Count  UBIN ALIGNED 
                          Represents the number of entries in 
                          the External Procedure Definition 
                          Record (type %TYPEDEF).  Default is 10. 
    Procedure Reference Entry Count  UBIN ALIGNED 
                          Represents the number of entries in 
                          the External Procedure Reference 
                          Record (type %TYPEREF).  Default is 10. 
    Data Definition Entry Count  UBIN ALIGNED 
                          Represents the number of entries in 
                          the External Data Definition Record 
                          (type %TYPSDEF).  Default is 10. 
    Data Reference Entry Count  UBIN ALIGNED 
                          Represents the number of entries in 
                          the External Data Reference Record 
                          (type %TYPSREF).  Default is 30. 
    Segment Definition Entry Count  UBIN ALIGNED 
                          Represents the number of entries in 
                          the External Segment Definition 
                          Record (type %TYPSEGDEF).  Default is 1. 
    Segment Reference Entry Count UBIN ALIGNED 
                          Represents the number of entries in 
                          the External Segment Reference 
                          Record (type %TYPSEGREF).  Default is 3. 
    Program Buffer Size  UBIN ALIGNED 
                          Represents the number of words to be 
                          reserved for the buffer.  Default is 
                          1022 words. 
    Relocation Buffer Size  UBIN ALIGNED 
                          Represents the number of words to be 
                          reserved for the buffer.  Default is 
                          1022 words. 
    Logical Block Entry Count  UBIN ALIGNED 
                          Represents the total number of 
                          entries in the Logical Block Record 
                          (type %TYPLOGBLK). 
                          NOTE:  Since this record is not 
                          paged, the maximum number of logical 
                          block entries desired must be specified. 
                          Two header entries are required in 
                          addition to the normal count. 
                          Default is 3, minimum is 3. 
    Internal Entries Entry Count UBIN ALIGNED 
                          Represents the number of entries in 
                          the Internal Entry Debug Record 
                          (type %TYPINTNTRY).  Default is 1. 
    Executable Statements Entry Count UBIN ALIGNED 
                          Represents the number of entries in 
                          the Executable Statements Debug 
                          Record (type %TYPEXST).  Default is 341. 
    Debug Variable Entry Count UBIN ALIGNED 
                          Represents the number of entries in 
                          the Variable Debug Record (type %TYPVREBL) 
                          Default is 204. 
    Debug Name Word Count UBIN ALIGNED 
                          Represents the number of entries in 
                          the Debug Names Record (type %TYPDBGNAM). 
                          Default is 1024, minimum is 8. 
    Number of Buffers  UBIN ALIGNED 
                          Represents the number of sets of buffers 
                          to be used.  If call to XUO$FRWD_REF are 
                          intermixed with calls to XUO$PRGM and 
                          XUO$RELOC, then a minimum of two sets of 
                          buffers must be specified.  Default is one. 
Output: 
None. 
Description: 
This routine allows the user to change the default buffer sizes.  The routine 
needs to be called only if the default sizes are to be changed and should be 
called before XUO$OUINIT.  All parameters are optional and if not specified, 
the size of the buffer will be the default.  With the exception of several 
records, all parameters are in terms of number of entries desired per buffer. 
In the case of name records, program records, and relocation records, the 
parameter passed represents the number of words to be reserved for the buffer. 
00003
00001
00002
Format: 
CALL XUO$DBGNAME (Name, 
                  Name Pointer); 
Input: 
    Name 
        .Size           UBIN HALF UNALIGNED 
                        The number of characters in the name. 
        .Text           CHAR(Size) 
                        The character string that is the 
                        name. 
Output: 
    Name Pointer        UBIN ALIGNED 
                        The word offset to the entry in the 
                        Procedure Names Debug record 
                        locating the added text. 
Description: 
This routine builds entries in the Procedure Names Debug Record (record type 
%TYPDBGNAM).  This record contains all debug names; that is, all procedure 
names, entry names, statement labels, and variable names. 
B$OBJECT Reference: 
B$DNAME 
00004
00003
00001
00002
Format: 
CALL XUO$DNAME (Name, 
                Name Pointer); 
Input: 
    Name 
        .Size           UBIN HALF UNALIGNED 
                        The number of characters in the name. 
        .Text           CHAR (Size) 
                        The character string that is the 
                        externally defined name. 
Output: 
    Name Pointer        UBIN 
                        The value that represents the word 
                        offset to the entry in the Defined 
                        Names Text record. 
Description: 
This routine is used to build an entry in the Externally Defined Names record 
(record type %TYPDNAM).  The record is the collection of names pointed to by 
the following records: 
    Sections   (type %TYPSECT) 
    ENTDEF     (type %TYPEDEF) 
    SYMDEF     (type %TYPSDEF) 
    SEGDEF     (type %TYPSEGDEF) 
B$OBJECT Reference: 
B$DNAME 
00004
00003
00001
00002
Format: 
CALL XUO$EDEF (Section Number, 
               Section Offset, 
               Name Pointer, 
               Entry Flags, 
               Altreturn Flag, 
               Argument Check Flag, 
               Call Type, 
               Number Arguments); 
Input: 
    Section Number      UBIN 
                        Contains an entry number into the section 
                        table (type %TYPSECT). 
    Section Offset      UBIN 
                        Word offset from the origin of the section. 
    Name Pointer        SBIN ALIGNED 
                        The word displacement into the name record 
                        (type %TYPDNAM) locating the name of this entry. 
    Entry Flag          BIT (1) UNALIGNED 
                        A flag denoting primary entry definition. 
                           '0'B = not a primary name 
                           '1'B = a primary name (object unit name) 
    Altreturn Flag      BIT (1) UNALIGNED 
                        A flag denoting permissible alternate 
                        return. 
                           '0'B = alternate return not allowed 
                           '1'B = alternate return allowed 
    Argument Check Flag BIT (1) UNALIGNED 
                        CHECK is a one-bit flag denoting 
                        arguments/parameters check and alternate 
                        return specification check. 
                           '0'B = do not check for matching 
                                  arguments/parameters and alternate 
                                  return specification check. 
                           '1'B = check for matching arguments/parameters 
                                  and alternate return specification. 
    Call Type           UBIN 
                        Denotes the calling sequence type. 
                        EQUs for Call Type can be found in macro SUB_CST 
                        in B$OBJECT_C. 
    Number Arguments    UBIN 
                        Denotes the number of parameters. 
Output: 
None. 
Description: 
This routine builds an entry in the External Procedure Definition Record 
(record type %TYPEDEF).  There is one record per object unit which defines the 
external procedure definitions.  The record for External Procedure Definition 
contains one entry per external procedure name within the object unit.  A PL6 
module with no ENTRY statements will contain one entry.  Three level-0 ENTRY 
statements would produce an ENTDEF record with four entries (one for the 
primary procedure name, three for the three ENTRY names). 
B$OBJECT Reference: 
B$EDEF 
00004
00003
00001
00002
Format: 
CALL XUO$EREF (Name Pointer, 
               Secondary Reference Flag, 
               Altreturn Flag, 
               Argument Check Flag, 
               Call Type, 
               Number Arguments, 
               Eref Number); 
Input: 
    Name Pointer        SBIN 
                        The word displacement into the record of 
                        referenced names (Record Type %TYPRNAM) locating 
                        the name. 
    Secondary Reference Flag BIT(1) UNALIGNED 
                        Indicates that the reference is a secondary 
                        reference and should not cause loading of a 
                        library routine. 
    Altreturn Flag      BIT(1) UNALIGNED 
                        Denotes permissible alternate return. 
                           '0'B - alternate return not allowed 
                           '1'B - alternate return allowed 
    Argument Check Flag BIT(1) UNALIGNED 
                        Denotes arguments/parameter check and alternate 
                        return specification check. 
                           '0'B - do not check for matching arguments/ 
                                  parameters and alternate return 
                                  specification 
                           '1'B - check for matching arguments/parameters 
                                  and alternate return specification 
   Call Type            UBIN 
                        Denotes the calling sequence type. 
                        EQUs for Call Type can be found in macro SUB_CST 
                        in B$OBJECT_C. 
   Number Arguments     UBIN 
                        Denotes the number of parameters 
Output: 
   Eref Number          UBIN 
                        The table entry number for the current External 
                        Procedure Reference to be entered into the 
                        External Procedure Reference record.  This value 
                        is returned by the called routine. 
Description: 
This routine builds an entry in the External Procedure Reference Record 
(record type %TYPEREF).  There is one record per object unit for external 
procedure references.  There is one entry per name. 
B$OBJECT Reference: 
B$EREF 
00004
00003
00001
00002
Format: 
CALL XUO$EXST (Section Number, 
               Offset, 
               Name Pointer, 
               Logical Block Entry Number, 
               Compiler Optimized Flag, 
               Statement Type, 
               Line Number, 
               Label Array Flag, 
               Label Index); 
Input: 
    Section Number      UBIN 
                        Contains an entry number into the 
                        control section type (type %TYPSECT) 
                        (OU only). 
    Offset              UBIN 
                        Word offset from the origin of the 
                        section. (OU) 
    Name Pointer        SBIN 
                        The word displacement into the debug 
                        name record (type %TYPDBGNAM) locating the 
                        statement label.  A value of -1 
                        indicates no label. 
    Logical Block Entry Number  UBIN 
                        This is the entry number in the logical 
                        block table of the logical block of the 
                        highest lexical level containing this 
                        statement. 
    Compiler Optimized Flag  BIT (1) UNALIGNED 
                        This flag indicates a compiler optimized 
                        statement;  when set, it indicates this 
                        statement may not produce correct results 
                        if the compiled program flow has been 
                        altered. 
    Statement Type      UBIN 
                        This is the code which indicates the generic 
                        class of statement for use by the debugger. 
                        The EQUs for statement types can be found in 
                        the macro B$STTYPESUBS in B$OBJECT_C. 
    Line Number         UBIN 
                        The line number of this executable 
                        statement. 
    Label Array Flag    UBIN 
                        This flag is the label array indicator. 
                        When it is set to 1, the Subscript field 
                        contains the associated subscript value; 
                        otherwise, the Subscript field contains 
                        all zeros. 
    Label Index         UBIN 
                        When the Label Array Flag is 1, this 
                        field contains the associated subscript 
                        value; otherwise, it contains all zeros. 
Output: 
None. 
Description: 
The record contains one entry for every executable statement and sub-statement 
(record type %TYPEXST) in the module.  Note that the logical block table 
scopes the statement set for every logical block.  The statement table must be 
in order of ascending line numbers, and includes all labeled statements that 
can be branched to. 
B$OBJECT Reference: 
B$EXST 
00004
00003
00001
00002
Format: 
CALL XUO$EXSTNUM (Executable Statement Number); 
Input: 
None. 
Output: 
    Executable Statement number UBIN. 
                        The number of the next executable 
                        statement entry to be allocated. 
Description: 
This routine returns the number of the next Executable Statement Debug (record 
type %TYPEXST) entry to be allocated.  The returned value is used as input in 
the calls to XUO$LOGBLKEXSTINIT and XUO$LOGBLKEXSTTERM where starting and 
ending Executable Statement debug entry number is required. 
B$OBJECT Reference: 
none 
00004
00003
00001
00002
Format: 
CALL XUO$FRWD_REF (Section Number, 
                   Lookup Routine, 
                   DCB Pointer); 
Input: 
    Section Number      UBIN ALIGNED 
                        The number of the control section in 
                        which to resolve forward references. 
    Lookup Routine      EPTR 
                        The entry pointer to the routine 
                        which will look up the operand. 
    DCB Pointer         PTR 
                        Pointer to the DCB through which 
                        the object unit is being written. 
Output: 
None. 
Description: 
This routine will position itself to the beginning of the control section 
indicated by the input parameter Section Number.  The control section will be 
read sequentially ignoring all program records.  When a relocation record is 
found, it will be searched for operands of type %OPERFREF.  If no operands of 
that type are found, the next sequential record is read.  If operand type 
%OPERFREF is found the routine specified by the parameter Lookup Routine will 
be called as follows: 
    CALL Lookup Routine (Old Operand    UBIN   input 
                 Operand Type           UBIN   input 
                 New Operand            UBIN   output 
                 Relocation operator    SBIN   output 
                 Starting Bit           SBIN   output 
                 Ending Bit)            SBIN   output 
The called routine must return the correct operand value to be used and the 
correct operand type to be used.  If these fields are not modified, an operand 
type of %OPERSEGREF and a value of 0 will be used. 
The B$RELOCSUBS macro in B$OBJECT contains EQUs for specifying the operand 
type and relocation operator. 
XUO$FRWD_REF routine will initialize the relocation operator, the starting bit 
and ending bit to -1.  If these fields contain values greater than -1 then the 
fields in the relocation directive will be updated with the new data. 
If any relocation directives have changed due to calling the Lookup Routine, 
then the relocation directive buffer will be rewritten. 
This routine will continue until all relocation records have been processed 
for the specified control section. 
If calls to XUO$FRWD_REF are intermixed with calls to XUO$PRGM and XUO$RELOC 
then a minimum of two sets of buffers must be specified on the call to 
XUO$BUFINIT. 
B$OBJECT Reference: 
None. 
00004
00003
00001
00002
Format: 
CALL XUO$HEADNAME (Name); 
Input: 
    Name 
      .Size             UBIN HALF UNALIGNED 
                        The number of bytes in the object unit 
                        name. 
      .Text             CHAR(Size) 
                        The character string which is the name 
                        of the object unit.  This name is equal 
                        to the entry definition name with the 
                        attribute 'object unit name'. 
Output: 
Updated Head Key. 
Description: 
This routine builds the Head Record Key.  Each object unit is uniquely 
identified by its head record key.  Byte 0 of the key contains the name size 
followed by the character string which is the object unit name. 
B$OBJECT Reference: 
B$HEADKEY 
00004
00003
00001
00002
Format: 
CALL XUO$HEADSTART (Operand Type, 
                    Operand, 
                    Offset); 
Input: 
    Operand Type        UBIN 
                        An operand type of 0 indicates that 
                        the object unit is not the main 
                        program.  For the main program the 
                        operand type may be specified by using 
                        the EQUs, %OPERxxxx, defined in the macro 
                        B$RELOCSUBS in B$OBJECT_C. 
    Operand             UBIN 
                        If the operand type = %OPERCONST, the 
                        operand field is an unsigned constant. 
                        If the operand type is not 0 or %OPERCONST 
                        then the operand field is an entry number 
                        into the table specified by the operand 
                        type. 
    Offset              UBIN 
                        The word displacement from offset found in 
                        the key to the relocatable item.  (The 
                        offset found in the record key is the 
                        offset from the origin of the section.) 
Output: 
The updated Head Record. 
Description: 
This routine will fill in the start address of a module.  It should be called 
only in the case of the main program.  The remaining fields of the Head Record 
are filled in by calling XUO$OUTERM after all the records have been processed. 
B$OBJECT Reference: 
B$OUHEAD 
00004
00003
00001
00002
Format: 
CALL XUO$HEAD_SEVERITY (Severity); 
Input: 
    Severity            UBIN ALIGNED 
                        The value that represents the severity 
                        to be associated with the object unit. 
                        The routine will maintain the maximum 
                        severity received. 
                        Severity levels assigned to an object unit 
                        should conform to the following values: 
                           0 - no error or warning messages 
                           4 - warning messages issued during 
                               compilation 
                           7 - errors were detected which may be 
                               sufficient to cause execution failure 
                          11 - fatal error; the object unit contains 
                               flaws which will almost certainly 
                               prevent proper execution. 
Output: 
Updated Head Record. 
Description: 
This routine builds the severity level field in the Head Record.  The severity 
level indicates the maximum severity of errors encountered during compilation. 
B$OBJECT Reference: 
B$OUHEAD 
00004
00003
00001
00002
Format: 
CALL XUO$INTNTRY (Logical Block Number, 
                  Section Number, 
                  Section Offset, 
                  Name Pointer, 
                  Entry Flag, 
                  Altreturn Flag, 
                  Argument Check Flag, 
                  Call Type, 
                  Number of Arguments); 
Input: 
    Logical Block Number UBIN 
                        The entry number of the logical block 
                        table entry which describes this 
                        procedure. 
    Section Number      UBIN 
                        The entry number into the control 
                        section table (type %TYPSECT) (OU only). 
    Section Offset      UBIN 
                        The word offset from the origin of 
                        the section. 
    Name Pointer        SBIN 
                        The word displacement into the debug 
                        name record (type %TYPDBGNAM) locating the 
                        name of this entry. 
    Entry Flag          BIT (1) UNALIGNED 
                        A flag denoting primary entry definition. 
                           '0'B = not a primary name 
                           '1'B = a primary name (object unit name) 
    Altreturn Flag      BIT (1) UNALIGNED 
                        A flag denoting permissible alternate 
                        return. 
                           '0'B = alternate return not allowed 
                           '1'B = alternate return allowed 
    Argument Check Flag BIT (1) UNALIGNED 
                        CHECK is a one-bit flag denoting 
                        arguments/parameters check and alternate 
                        return specification check. 
                           '0'B = do not check for matching 
                                  arguments/parameters and alternate 
                                  return specification check. 
                           '1'B = check for matching arguments/parameters 
                                  and alternate return specification. 
    Call Type           UBIN 
                        Denotes the calling sequence type. 
                        The call type may be specified using the EQUs 
                        defined in the macro SUB_CST in B$OBJECT_C. 
    Number Arguments    UBIN 
                        Denotes the number of parameters. 
Output: 
None. 
Description: 
This routine adds entries to the Internal Entry Debug Record (record type 
%TYPINTNTRY).  There is one entry for every internal procedure entry point 
within the program.  In PL6 these are generated by PROC and ENTRY statements. 
Entries are ordered such that the internal logical block structure of the 
module is reflected. 
B$OBJECT Reference: 
B$INTNTRY 
00004
00003
00001
00002
Format: 
CALL XUO$LOGBLKALLOC (Logical Block Number) ALTRET (label); 
Input: 
None. 
Output: 
    Logical Block Number UBIN ALIGNED 
                        The entry number into the logical 
                        block debug record. 
Description: 
This routine is used in building Logical Block Debug Records (record type 
%TYPLOGBLK).  It must be called before any other of the logical block creation 
routines are called.  It need not be called before XUO$LOGBLKTERM, the 
termination routine.  This routine allocates a Logical Block entry.  If one is 
not available, it will altreturn. 
B$OBJECT Reference: 
B$LOGBLK 
00004
00003
00001
00002
Format: 
CALL XUO$LOGBLKEXSTINIT (Logical Block Number, 
                         Starting executable statement number, 
                         Starting line number, 
                         Name Pointer, 
                         Lexical Level) ALTRET (label); 
Input: 
    Logical Block Number UBIN 
                        The number returned by the call to 
                        XUO$LOGBLKALLOC. 
    Starting executable statement number  UBIN 
                        The word offset into the statement 
                        record (type %TYPEXST) to the statement 
                        descriptions for this logical block. 
                        It is the starting number of the first 
                        executable statement of the block. 
    Starting Line number UBIN 
                        The beginning line number of this 
                        logical block. 
    Name Pointer        SBIN 
                        The word displacement into the debug 
                        name record (type %TYPDBGNAM) locating the 
                        name of this logical block. 
    Lexical Level       UBIN 
                        The nesting level of the block. 
                        A contained procedure has a higher 
                        lexical level than the procedure which 
                        contains it. 
Output: 
Updated logical block record. 
Description: 
This routine is used in building Logical Block Debug records (record type 
%TYPLOGBLK).  It fills in initial data that relates to the executable 
information.  The routine altreturns if the logical block number is invalid. 
B$OBJECT Reference: 
B$LOGBLK 
00004
00003
00001
00002
Format: 
CALL XUO$LOGBLKEXSTTERM (Logical Block Number, 
                         Ending Executable Statement Number, 
                         Ending Line Number) ALTRET (label); 
Input: 
    Logical Block Number UBIN 
                        The logical block number returned from 
                        the call to XUO$LOGBLKALLOC. 
    Ending Executable Statement Number  SBIN 
                        This is the size in entries of the 
                        statement descriptions for this logical 
                        block.  It is used to calculate the 
                        statements offset. 
    Ending Line Number  UBIN 
                        The ending line number for this logical 
                        block. 
Output: 
Updated logical block record. 
Description: 
This routine finishes setting up of the executable statement information in 
the Logical Block (record type %TYPLOGBLK) entry.  If the logical block number 
passed to it is invalid, this routine will altreturn. 
B$OBJECT Reference: 
B$LOGBLK 
00004
00003
00001
00002
Format: 
CALL XUO$LOGBLKNOAUTO (Operand Type, 
                       Operand, 
                       Offset) ALTRET (label); 
Input: 
    Operand Type        UBIN     These three fields comprise 
    Operand             UBIN     the Noauto frame address 
    Offset              UBIN 
Output: 
Updated Logical block header for static auto pointer. 
Description: 
This routine is used in building Logical Block Debug Records (record type 
%TYPLOGBLK).  It fills in the static auto pointer for procedures that do not 
use a dynamic segment for auto. 
B$OBJECT Reference: 
B$LBNTRY0 
00004
00003
00001
00002
Format: 
CALL XUO$LOGBLKTERM ALTRET (label); 
Input: 
None. 
Output: 
Updated logical block headers. 
Description: 
This routine must only be called after all logical blocks have been filled in. 
It sets up the two headers (record type %TYPLOGBLK) that describe the total 
sizes of the debug records. 
B$OBJECT Reference: 
B$LBNTRY0, B$LBNTRY1 
00004
00003
00001
00002
Format: 
CALL XUO$LOGBLKVREBLINIT (Logical Block Number, 
                          Starting Variable Number) ALTRET (label); 
Input: 
    Logical Block Number UBIN 
                        The logical block number returned from 
                        the call to XUO$LOGBLKALLOC. 
    Starting Variable Number  UBIN 
                        The word offset into the variable record 
                        (type %TYPVREBL) to the variable descriptions 
                        for this logical block. 
Output: 
Updated logical block record. 
Description: 
This routine fills in the initial data that relates to the variable records in 
the Logical Block (record type %TYPLOGBLK) entry.  If the logical block number 
passed is invalid, this routine will altreturn. 
B$OBJECT Reference: 
B$LOGBLK 
00004
00003
00001
00002
Format: 
CALL XUO$LOGBLKVREBLTERM (Logical Block Number, 
                          Ending Variable Number) ALTRET (label); 
Input: 
    Logical Block Number UBIN 
                        The logical block number that is 
                        returned from the call to XUO$LOGBLKALLOC. 
    Ending Variable Number SBIN 
                        The index number of the last variable 
                        (type %TYPVREBL) for this logical block. 
                        It is used to calculate the variable size. 
Output: 
Updated logical block record. 
Description: 
This routine is used in building Logical Block Debug Records (record type 
%TYPLOGBLK).  It finishes setting up the variable data information in the 
Logical Block entry.  If the logical block number passed is invalid, this 
routine will altreturn. 
B$OBJECT Reference: 
B$LOGBLK 
00004
00003
00001
00002
Format: 
CALL XUO$OUINIT (DCB Number, 
                 Close Required Flag, 
                 Schema Required Flag, 
                 Compiler ID, 
                 Version, 
                 Library Name, 
                 UTS, 
                 Error Routine, 
                 Word Size, 
                 Trust Me, 
                 Alternate Shared Library) ALTRET (label); 
Input: 
    DCB Number          UBIN ALIGNED 
                        The DCB number to which the object unit 
                        will be written.  If DCBNUM(nil) is 
                        passed, the object unit will not be 
                        written. 
    Close Required Flag BIT(1) 
                        When set, this flag implies that the 
                        M$OU DCB is to be closed by the object 
                        unit routine, XUO$OUTERM.  Otherwise, it 
                        will remain open. 
    Schema Required Flag  BIT(1) 
                        When set, this flag implies that debug 
                        records are to be output.  When reset, no 
                        no debug data will be included in the 
                        object unit. 
    Compiler ID         UBIN ALIGNED 
                        EQUs to identify the language may be found 
                        in the macro COMPILERIDSUBS in B$OBJECT_C. 
     Version            UBIN ALIGNED 
                        Version number of the compiler conforming 
                        to release standards. 
     Library Name 
         .Size          UBIN BYTE UNALIGNED 
                        Size in bytes of the library name 
         .Text          CHAR(Size) 
                        Character string representing the 
                        library name to be associated. 
     UTS                UBIN ALIGNED 
                        The Universal Time Stamp value to be used 
                        in the object unit keys.  This parameter is 
                        optional.  If it is not specified, a new 
                        value will be obtained and used. 
     Error Routine      EPTR 
                        Represents the entry point of an error 
                        routine to call when an I/O error or 
                        memory allocation error occurs.  This 
                        routine will be passed B$ALT.ERR.  This 
                        parameter is optional.  If it is not 
                        specified, ENTADDR(nil) will be the 
                        default and no attempt will be made to 
                        call the routine. 
     Word Size          UBIN ALIGNED 
                        Represents the word size of the object 
                        code.  If not specified, word size 
                        will be set to 36. 
     Trust Me           BIT(1) 
                        When set, this bit allows the user 
                        to write program records out of order. 
                        If not set, checking will be done to 
                        ensure program records are written 
                        in sequence. 
     Alternate Shared Library 
          .Size         UBIN BYTE ALIGNED 
                        Represents the number of characters 
                        in the Alternate Shared Library name.v 
          .Text         CHAR (Size) 
                        The character string that is the name 
                        of the Alternate Shared Library that 
                        is to be associated with this object unit. 
Output: 
None. 
Description: 
This routine performs the initialization necessary prior to building the 
object unit.  This module must be called before any object unit building 
routines can be called.  If XUO$BUFINIT has not been called by the user, then 
this routine will call it with all arguments = addr(nil).  A dynamic segment 
is allocated for the object unit and buffers.  This routine altreturns if it 
is unable to get a dynamic segment.  Pointers to the buffers are initialized. 
All fields of the following four keys are initialized:  Head Key, OU Key, 
Program Key, and Relocation Key.  The object unit file is opened.  If any 
unexpected I/O errors occur while trying to write the object unit, the DCB 
will be closed in accordance with the OU Close Required Flag. 
B$OBJECT Reference: 
B$OUKEY, B$PRGKEY, B$RELKEY 
00004
00003
00001
00002
Format: 
CALL XUO$OUTERM ALTRET (label); 
Input: 
None. 
Output: 
Completed object unit. 
Description: 
This routine terminates object unit generation.  Any partially filled records 
will be written.  This routine will call XUO$LOGBLKTERM to fill in the Logical 
Block Record and write it out.  It will then call XUO$HEADTERM to fill in the 
Head Record and write it out.  The object unit is now complete.  XUO$OUCLOSE 
is called to close the current object unit file if the OU Close Required Flag 
was set in the initial call to XUO$INIT.  At this time all the space for 
object unit buffers is released back to the system. 
B$OBJECT Reference: 
    B$DNAME 
    B$EDEF 
    B$EREF 
    B$SDEF 
    B$SREF 
    B$SEGDEF 
    B$SEGREF 
    B$INTNTRY 
    B$EXST 
    B$VREBL 
00004
00003
00001
00002
Format: 
CALL XUO$PRGM (Section Number, 
               Offset, 
               Value) ALTRET (label); 
Input: 
    Section Number      UBIN ALIGNED 
                        Specifies the section into which Value 
                        will be inserted.  The XUO$SECTBUILD 
                        service returns the numbers of newly 
                        created sections. 
    Offset              UBIN 
                        The offset in words from the start 
                        of the section where the Value is 
                        to be inserted 
    Value               BIT (36) ALIGNED 
                        The entity that is to be inserted 
                        into the specified section. 
Output: 
Value is stored in program record. 
Description: 
This routine generates Program record (record type %TYPPROG, subtype 
%SUBTYPPROG) entries.  The record contains pure program (no control words). 
This routine altreturns if the Section Number is invalid.  The current program 
record is output if the following conditions are met: 
1.  The section number passed is not the same as the current record. 
2.  The offset is not the next location in the current buffer. 
3.  There is insufficient space to put the value in the current buffer.  If 
    the relocation buffer has any records in it, it will also be written. 
The passed value is then added to the program buffer. 
B$OBJECT Reference: 
B$PRGKEY 
00004
00003
00001
00002
Format: 
CALL XUO$PRGM_TEXT (Section Number, 
                    Offset, 
                    Value) ALTRET (label); 
Input: 
    Section Number      UBIN ALIGNED 
                        Specifies the section into which Value 
                        will be inserted.  The XUO$SECTBUILD 
                        service returns the numbers of newly 
                        created sections. 
    Offset              UBIN 
                        The offset in words from the start 
                        of the section where the Value is 
                        to be inserted 
    Value               BIT (36) ALIGNED 
                        The entity that is to be inserted 
                        into the specified section. 
Output: 
Value is stored in program record. 
Description: 
This routine will convert a Value containing two 9-bit characters into two 
8-bit characters (one 16-bit word).  The conversion takes place if the word 
size, as specified in XUO$OUINIT, is not 36 bits. 
This routine generates Program record (record type %TYPPROG, subtype 
%SUBTYPPROG) entries.  The record contains pure program (no control words). 
This routine altreturns if the Section Number is invalid.  The current program 
record is output if the following conditions are met: 
1.  The section number passed is not the same as the current record. 
2.  The offset is not the next location in the current buffer. 
3.  There is insufficient space to put the value in the current buffer.  If 
    the relocation buffer has any records in it, it will also be written. 
The passed value is then added to the program buffer. 
B$OBJECT Reference: 
B$PRGKEY 
00004
00003
00001
00002
Format: 
CALL XUO$RELOC (Section Number, 
                Offset, 
                Operand Type, 
                Operand, 
                Relocation Operator, 
                Starting Bit, 
                Ending Bit, 
                Evaluation Operator, 
                Value) ALTRET (label); 
Input: 
    Section Number      UBIN ALIGNED 
                        The value representing the section 
                        number to which the relocatable 
                        record is to be applied. 
    Offset              UBIN ALIGNED 
                        The value representing the offset 
                        within the Control Section where 
                        the relocatable item is to be 
                        applied. 
    Operand Type        UBIN ALIGNED 
                        The value representing the type of this 
                        operand.  EQUs defining valid operand types 
                        can be found in the macro B$RELOCSUBS is 
                        B$OBJECT_C. 
    Operand             UBIN ALIGNED 
                        If the operand type = %OPERCONST, the operand 
                        field is an unsigned constant.  If the 
                        operand type is not 0 or %OPERCONST, then 
                        the operand field is an entry number into 
                        the table specified by the operand type. 
    Relocation Operator  UBIN ALIGNED 
                        The operator to be applied to the 
                        intermediate result and the field 
                        defined by Starting Bit and Ending 
                        Bit within the current program 
                        record. 
                        EQUs (%RELOCOPxxxx) defining valid 
                        relocation operators can be found in 
                        the macro B$RELOCSUBS in B$OBJECT_C. 
    Starting Bit        UBIN ALIGNED 
                        The starting bit offset from the 
                        word locating the relocatable item. 
    Ending Bit          UBIN ALIGNED 
                        The ending bit offset from the 
                        word locating the relocatable item. 
    Evaluation Operator UBIN ALIGNED  optional 
                        The operator to be applied to the 
                        value and the evaluation of the 
                        operand. 
                        EQUs (%EVALOPxxxx) defining valid 
                        evaluation operators can be found in 
                        macro B$RELOCSUBS in B$OBJECT_C. 
    Value               UBIN ALIGNED  optional 
                        A constant to be used in the 
                        intermediate result.  This word is 
                        present only if the Evaluation 
                        Operator has been passed. 
Output: 
Relocation entry. 
Description: 
This routine generates entries for the Relocation Directives record (record 
type %TYPPROG, subtype %SUBTYPREL).  The relocation buffer will be flushed if 
the following conditions are met: 
1.  There is insufficient room for 3 word entry in buffer. 
2.  Relocating a new section. 
3.  The offset is less than the current key offset. 
The program buffer will be flushed if the relocation entry does not apply to 
the text buffer.  In addition, any relocation records currently in the 
relocation buffer will also be flushed. 
Then either 1 one word, two word, or three word entry will be made in the 
current buffer.  If the Eval operator is passed, it is assumed that a three 
word relocation entry is required.  Therefore Value must also be passed. 
B$OBJECT Reference: 
B$RELOC1, B$RELOC2 
00004
00003
00001
00002
Format: 
CALL XUO$RNAME (Name, 
                Name Pointer); 
Input: 
    Name 
        .Size          UBIN HALF UNALIGNED 
                       The number of characters in the name. 
        .Text          CHAR(Size) 
                       The character string that is the 
                       externally referenced name. 
Output: 
    Name Pointer       UBIN ALIGNED 
                       The word offset to the entry in the 
                       Externally Referenced Names record 
                       locating the added text. 
Description: 
This routine builds an entry in the Externally Referenced Names Record (record 
type %TYPRNAM).  The record is the collection of names pointed to by the 
following records: 
    ENTREF    (type %TYPEREF) 
    SYMREF    (type %TYPSREF) 
    SEGREF    (type %TYPSEGREF) 
B$OBJECT Reference: 
B$RNAME 
00004
00003
00001
00002
Format: 
CALL XUO$SDEF (Name Pointer, 
               Section Number, 
               Section Offset); 
Input: 
    Name Pointer        UBIN ALIGNED 
                        Word offset into the Externally 
                        Defined Names record (type %TYPDNAM) 
                        locating the name. 
    Section Number      UBIN ALIGNED 
                        An entry into the Control Section 
                        record. 
    Section Offset      UBIN ALIGNED 
                        Word offset from the origin of 
                        the section. 
Output: 
None. 
Description: 
This routine builds an entry in the External Data Definition record (record 
type %TYPSDEF) for non-constant entries. 
B$OBJECT Reference: 
B$SDEF 
00004
00003
00001
00002
Format: 
CALL XUO$SDEF_CONST (Name Pointer, 
                     Constant Value); 
Input: 
    Name Pointer        UBIN ALIGNED 
                        Word offset into the Externally 
                        Defined Names record (type %TYPDNAM) 
                        locating the name. 
    Constant Value      UBIN ALIGNED 
                        The constant SYMDEF 
Output: 
None. 
Description: 
This routine generates entries in the External Data Definition record (record 
type %TYPSDEF) for constant entries. 
B$OBJECT Reference: 
B$SDEF 
00004
00003
00001
00002
Format: 
CALL XUO$SECTBUILD (Section Type, 
                    Name Pointer, 
                    Section Number, 
                    Init, 
                    Bound, 
                    Segment Name Pointer) ALTRET (label); 
Input: 
    Section Type        UBIN ALIGNED 
                        The code specifying the type of 
                        section. 
                        The section type may be specified using the 
                        EQUs in the B$SECTIONSUBS macro in B$OBJECT_C. 
    Name Pointer        SBIN ALIGNED 
                        Word offset into the Externally 
                        Defined Names record (Type %TYPDNAM) 
                        locating the name of this 
                        control section.  If the field is 
                        negative, the section has no name. 
    Init                BIT(3) UNALIGNED 
        .Zero           BIT(1) UNALIGNED 
                        Initialize with zero. 
        .UTS            BIT(1) UNALIGNED 
                        Initialize with UTS. 
        .Segment        BIT(1) UNALIGNED 
                        Indicates that this section is 
                        to be placed in the segment specified 
                        by Segment Name Pointer. 
    Bound               UBIN ALIGNED 
                        Represents the bound field of the 
                        section.  This is optional and if 
                        not specified will default to even 
                        boundary. 
                        The bound field may be specified using EQUs 
                        defined in the B$SECTIONSUBS in B$OBJECT_C. 
    Segment Name Pointer SBIN 
                        Word offset into the Externally 
                        Defined Names record (type %TYPDNAM).  The 
                        name defined must match one of the 
                        legal names recognized by the linker. 
                        These can be found in the file 
                        B_SEGIDS_C.:LIBRARY. 
                        If Segment Name Pointer is not 
                        specified, the linker will allocate 
                        the control section in the 'default 
                        data segment'. 
Output: 
    Section Number      UBIN ALIGNED 
                        The number of the newly created 
                        section entry in the Section Record 
Description: 
This routine builds a new entry in the Section Record (record type %TYPSECT) 
and returns the number of the section.  This routine will altreturn if a new 
section cannot be allocated.  There is one record per object unit which 
defines the size and type of sections.  The section record contains one entry 
per section within the object unit. 
B$OBJECT Reference: 
B$SECTION 
00004
00003
00001
00002
Format: 
CALL XUO$SECTNAME (Section Number, 
                   Name Pointer) ALTRET (label); 
Input: 
    Section Number      UBIN ALIGNED 
                        The number of the Section Record entry 
                        that is to be modified. 
    Name Pointer        SBIN ALIGNED 
                        Word displacement into the Externally 
                        Defined Names Record (type %TYPDNAM) locating 
                        the name of this section.  If the field 
                        is negative, the section has no name. 
Output: 
Updated entry in the Section Record. 
Description: 
This routine enters the section name pointer into the previously created 
Section Record (record type %TYPSECT) entry.  If an invalid section number is 
passed in, this routine will altreturn. 
B$OBJECT Reference: 
B$SECTION 
00004
00003
00001
00002
Format: 
CALL XUO$SECTSIZE (Section Number, 
                   Section Size) ALTRET (label); 
Input: 
    Section Number      UBIN ALIGNED 
                        The number of the Section Record entry 
                        that is to be modified. 
    Section Size        UBIN ALIGNED 
                        The size in words of the section. 
Output: 
Updated Section Record entry. 
Description: 
This routine is used to enter the size of a section into a previously created 
entry in the Section Record (record type %TYPSECT).  This routine will 
altreturn if an invalid Section Number is passed. 
B$OBJECT Reference: 
B$SECTION 
00004
00003
00001
00002
Format: 
CALL XUO$SEGDEF (Name Pointer, 
                 Section Number, 
                 Section Offset); 
Input: 
    Name Pointer        UBIN ALIGNED 
                        The word offset into the Externally 
                        Defined Names Record (type %TYPDNAM). 
    Section Number      UBIN ALIGNED 
                        The control Section number. 
    Section Offset      UBIN ALIGNED 
                        Offset from the origin of the section. 
Output: 
None. 
Description: 
This routine builds a non-constant entry in the External Segment Definition 
Record (record type %TYPSEGDEF).  There is one record per object unit for 
Initialized Segment Definitions. 
B$OBJECT Reference: 
B$SEGDEF 
00004
00003
00001
00002
Format: 
CALL XUO$SEGDEF_CONST (Name Pointer, 
                       Constant Value); 
Input: 
    Name Pointer        UBIN ALIGNED 
                        The word displacement into the 
                        Externally Defined Names Record 
                        (type %TYPDNAM). 
    Constant Value      UBIN ALIGNED 
                        The value of the constant segment 
                        definition pointer. 
Output: 
None. 
Description: 
This routine builds a constant entry in the External Segment Definition Record 
(record type %TYPSEGDEF).  There is one record per object unit for Initialized 
Segment Definitions. 
B$OBJECT Reference: 
B$SEGDEF 
00004
00003
00001
00002
Format: 
CALL XUO$SEGREF (Name Pointer, 
                 Segment Reference Number, 
                 Nsab, 
                 Secondary Reference Flag, 
                 Read Only Flag); 
Input: 
    Name Pointer        SBIN 
                        The word displacement into the 
                        Externally Referenced Names Record 
                        (type %TYPRNAM) locating the segment 
                        reference name. 
    Nsab                BIT(4) UNALIGNED  optional 
                        Not used for CP6 
    Secondary Reference Flag  BIT(1) UNALIGNED 
                        Indicates that the reference is a 
                        secondary reference and the lack of a 
                        matching definition should not be 
                        considered an error by the linker. 
    Read Only Flag      BIT(1) UNALIGNED 
                        Specifies that the corresponding 
                        SEGDEF must be in a constant section. 
                        If the section that the Segment 
                        Definition applies to is not of 
                        type %TYPDNAM (procedure) or type %TYPSDEF (read 
                        only data), the linker will issue a 
                        warning diagnostic. 
Output: 
    Segment Reference Number  UBIN ALIGNED 
                        It is the number of the entry that 
                        was just added to the External 
                        Segment Reference Record. 
Description: 
This routine adds an entry to the External Segment Reference Record (record 
type %TYPSEGREF).  There is one record per object unit for external references 
to segment names.  The value of a segment name is a segment id.  The 
definitions of all referenced segment ids will be provided by the linker.  A 
set of conventional, non-conflicting segment names will be established for 
such things as dcb segment, automatic segment, instruction segment, JIT 
segment, etc. 
B$OBJECT Reference: 
B$SEGREF 
00004
00003
00001
00002
Format: 
CALL XUO$SREF (Name Pointer, 
               Secondary Reference Flag, 
               SYMREF Number, 
               Read Only Flag); 
Input: 
    Name Pointer        UBIN ALIGNED 
                        The word displacement into the 
                        record of Externally Referenced 
                        Names (type %TYPRNAM) locating the name. 
    Secondary Reference Flag BIT(1) UNALIGNED 
                        Indicates that the reference is a 
                        secondary reference and the lack of a 
                        matching definition should not be 
                        considered an error by the linker. 
    Read Only Flag      BIT(1) 
                        Indicates that the corresponding 
                        SYMDEF item is in a read only section. 
                        If the section that the SYMREF applies 
                        to is not of type %TYPDNAM (procedure) or 
                        type %TYPSDEF (read only data) the linker will 
                        issue a warning diagnostic. 
Output: 
    SYMREF Number       UBIN ALIGNED 
                        The entry number of the External Data 
                        Reference that was just added to the 
                        External Data Reference Record. 
Description: 
This routine adds an entry to the External Data Reference Record (record type 
%TYPSREF).  There is one record per object unit for external data references 
(i.e., SYMREF).  There is one entry per name. 
B$OBJECT Reference: 
B$SREF 
00004
00003
00001
00002
Format: 
CALL XUO$VREBL (Address, 
                Address Type, 
                Data Type, 
                Reference Flag, 
                Modified Flag, 
                Logical Size, 
                Level Number, 
                Alignment Type, 
                Size Type Flag, 
                Array Type, 
                Operand Type, 
                Implied Pointer, 
                Operand, 
                Element Size, 
                Scale Factor, 
                Dimensions, 
                Name Pointer, 
                Entry Number, 
                Status Exists); 
Input: 
    Address             UBIN ALIGNED 
                        Address of the variable. 
    Address Type        UBIN ALIGNED 
                        The address type determines how to 
                        use the address and possible other 
                        information to locate the data described 
                        by the entry.  Address type can have 
                        the following values: 
                          1 - Static data - address is an offset 
                              within ISR. 
                          2 - Automatic Data - address is an offset 
                              within the current 
                              AUTO frame located by PR2. 
                          3 - Based data - address is an offset 
                              from user pointer 
                              (possibly defined by implied pointer). 
                          4 - DCB - address is an offset from the 
                              beginning of the DCB 
                              (which is located by implied pointer). 
                          5 - Parameter - address is an offset 
                              from the data located 
                              by the Implied Pointer into 
                              Automatic Storage. 
                          6 - Constant - address is an 18 bit constant. 
                          7 - Parameter in static - address is an 
                              offset from the data located by 
                              the Implied Pointer into Static 
                              Storage.  In this case relocation 
                              information applies to implied pointer. 
                          8 - AREADEF - address is the offset into 
                              the segment for this item. 
                          9 - Virtual array - address is the IS 
                              IS offset in static of the descriptor 
                              block for this virtual array. 
                         10 - 15 - Reserved for future use. 
    Data Type           UBIN ALIGNED 
                        Indicates the type of data described 
                        by this entry.  EQUs for specifying data 
                        types can be found in the VREBL_DATATYPES 
                        macro in B$OBJECT_C. 
    Reference Flag      BIT(1) UNALIGNED 
                        Indicates whether the variable is 
                        referenced or is not referenced by 
                        this module. 
    Modified Flag       BIT(1) UNALIGNED 
                        Indicates whether the variable is 
                        explicitly modified or not modified 
                        by this module. 
    Logical Size        UBIN ALIGNED 
                        Contains the size of the data item or 
                        a locator of the variable containing the 
                        size.  If the Size Type Flag = '0'B, this 
                        field contains the number of basic 
                        elements of this data type contained in 
                        the variable, e.g., the field contains 
                        five for a CHAR(5) variable.  If the Size 
                        Type Flag = '1'B this field contains the 
                        entry number of the variable which 
                        contains the size. 
    Level Number        UBIN ALIGNED 
                        Contains the level number of the data 
                        item (for structures). 
    Alignment Type      UBIN ALIGNED 
                        Defines the explicit alignment of the 
                        data item.  The possible alignment type 
                        values are: 
                           0 = Double Word Aligned 
                           1 = Word Aligned 
                           2 = Half Word Aligned 
                           3 = Byte Aligned 
                           4 = Bit Aligned 
                           5 = Digit Aligned 
    Size Type Flag      BIT(1) UNALIGNED 
                        If Size Type Flag = '0'B then Logical 
                        Size contains the number of basic elements 
                        of this data type contained in the variable, 
                        e.g., the field contains five for a CHAR(5) 
                        variable.  If Size Type Flag = '1'B 
                        then Logical Size contains the entry 
                        number of the variable which contains 
                        the size. 
    Array Type          UBIN ALIGNED 
                        Determines the array characteristics 
                        of this variable and thus determines 
                        whether continuation entry(ies) exist 
                        for this item. 
                        EQUs for specifying valid array types can 
                        be found in the VREBLSUBS macro in B$OBJECT_C. 
    Operand Type        UBIN ALIGNED 
                        The value representing the type of this 
                        operand.  EQUs defining valid operand types 
                        can be found in the macro B$RELOCSUBS in 
                        B$OBJECT_C. 
    Implied Pointer     SBIN ALIGNED 
                        This is unused for Address Types 1, 2, 
                        and 6. 
                        If Address Type is 3 (Based) and bit 0 
                        = 1, this based variable has no implied 
                        pointer.  If Address Type is 3 (Based) 
                        and bit 0 = 0, then the remaining bits 
                        contain the entry number of the variable 
                        table entry for the implied pointer 
                        to this variable. 
                        If Address Type is 4 (DCB) then this field 
                        contains the SYMREF number of the DCB. 
                        If Address Type is 5 this field contains 
                        the offset in the current automatic frame 
                        of the pointer to this parameter. 
                        If Address Type is 7, this field contains 
                        the address in the Instruction Segment 
                        of the pointer to this parameter. 
    Operand             UBIN ALIGNED 
                        If Operand Type is 4, the Operand is 
                        an unsigned constant. 
                        If Operand Type is not 4 (or 0) the 
                        Operand is an entry number in the table 
                        specified by type. 
    Element Size        UBIN ALIGNED 
                        This defines the physical size (in bits) 
                        of the item or of an element of the item, 
                        if an array.  This includes all slack bits. 
                        This is the multiplier needed to determine 
                        the bit offset in an array given the 
                        element offset. 
    Scale Factor        SBIN ALIGNED 
                        The number of units by which this data 
                        is assumed to be scaled.  The units depend 
                        on the data type.  If this is a binary 
                        data type, the units are binary digits. 
                        If this is a decimal data type, the units 
                        are decimal digits.  The field is meaningless 
                        for other data types. 
    Dimensions          UBIN ALIGNED 
                        Contains the number of dimensions for an 
                        array if Array Type is either 3 or 4.  If 
                        Array Type is 1 or 2, this contains the 
                        number of elements in the array. 
    Name Pointer        UBIN ALIGNED 
                        Contains the word offset into the 
                        Procedure Names Debug Record (type %TYPDBGNAM) 
                        locating the name of this variable. 
    Status Exists       BIT (1) UNALIGNED 
                        Status Exists = '1'B indicates this variable 
                        has a Status Variable associated with it. 
Output: 
    Entry Number        UBIN ALIGNED  optional 
                        The entry number of the Variable 
                        Debug entry just created.  This value 
                        must be used to determine the entry 
                        number of variables that have dimension 
                        greater than 1 and an array type other 
                        than 1 or 2.  In other cases the entry 
                        number of the next Variable Debug Record 
                        to be allocated can be determined by 
                        calling XUO$VREBLNUM. 
Description: 
This routine builds an entry into the Variable Debug Record (record type 
%TYPVREBL).  The record contains descriptions for every variable in the 
module.  Note that the logical block table scopes the variable set for each 
logical block.  A complete variable description may require more than one 
entry. 
B$OBJECT Reference: 
B$VREBL 
00004
00003
00001
00002
Format: 
CALL XUO$VREBLNUM (Variable Debug Record entry number); 
Input: 
 None. 
Output: 
    Variable Debug Record entry number  UBIN ALIGNED 
                        The number of the next entry in 
                        the Variable Debug Record. 
Description: 
This routine returns the number of the next Variable Debug Record (record type 
%TYPVREBL) entry.  The returned value is used in the calls to 
XUO$LOGBLKVREBLINIT and XUO$LOGBLKVREBLTERM where starting and ending Variable 
Debug Record entry numbers are required.  This routine is used only in the 
case of getting the next number for the logical block calls.  In all other 
cases, the entry number should be obtained by use of the parameter Entry 
Number returned by the call to XUO$VREBL. 
B$OBJECT Reference: 
B$VREBL 
00004
00003
00001
00002
Format: 
CALL XUO$VREBL_CONT (Offset, 
                     Data Type, 
                     Elements, 
                     Multiplier 1, 
                     Multiplier 2, 
                     Multiplier 3, 
                     Multiplier 4, 
                     Multiplier 5, 
                     Multiplier 6); 
Input: 
    Offset              UBIN ALIGNED 
                        Contains the value to be subtracted 
                        from the composite index calculated 
                        from index values and multipliers 
                        before multiplying by Element Size. 
    Data Type           UBIN ALIGNED 
                        Indicates the type of data described 
                        by this entry. 
                        EQUs for specifying data type can be found 
                        in the VREBL_DATATYPES macro in B$OBJECT_C. 
    Elements            UBIN ALIGNED 
                        Contains the total number of elements 
                        in the array, i.e., the product of all 
                        dimensions. 
    Multiplier N        UBIN ALIGNED 
                        The coefficient to be applied 
                        to index n in an array reference 
                        to be used in locating a particular 
                        element of an array. 
    The following example is included to clarify the use 
    of the various array parameters. 
    Assume an array A(LB1:UB1, LB2:UB2, ..., LBn:UBn). 
    Then for languages which vary the first dimension 
    most rapidly (e.g., FORTRAN): 
         Multiplier(1)= 1 
         Multiplier(j)= Multiplier(j-1) * (UB(j-1) -LB(j-1) +1) 
                        2 <= j <= N 
         Elements = Multiplier n * (UBn -LBn *1) 
    And for languages which vary the last dimension most 
    rapidly (e.g., PL1): 
         Multiplier(n)= 1 
         Multiplier(j)= Multiplier(j+1) * (UB(j+1) -LB(j-1) +1) 
                        1 <= j <= N-1 
         Elements = Multiplier(1) * (UB1 -LB1 +1) 
    In either case: 
         Offset = The sum of (Multiplier(j) * LB(j)) 
                  for j=1 to N 
    and the bit displacement from address to any element 
    A(x1, x2, ..., xn) is given by: 
        Bit displacement = 
            The sum of (Multiplier(j)* X(j) -Offset) 
                        for j = 1 to N) * Element Size 
Output: 
None. 
Description: 
This routine builds continuation entries in the Variable Debug Record (record 
type %TYPVREBL).  It is used for dimensioned entries of Array Type %TYPSECT or 
Array Type %TYPEDEF to describe the dimension attributes of the variable. 
B$OBJECT Reference: 
B$VREBLC 
00004
00003
00001
00002
Format: 
CALL XUO$VREBL_CONT_ADJ (Offset Flag, 
                         Offset, 
                         Data Type, 
                         Elements Flag, 
                         Elements, 
                         Multiplier 1 Flag, 
                         Multiplier 1, 
                         Multiplier 2 Flag, 
                         Multiplier 2, 
                         Multiplier 3 Flag, 
                         Multiplier 3); 
Input: 
    Offset Flag          BIT(1) UNALIGNED 
                         Denotes the interpretation of the 
                         Offset field.  If the Flag = '0'B 
                         then Offset contains the value to 
                         be subtracted from the composite 
                         index calculated from index values 
                         and multipliers before multiplying 
                         by Element Size.  If the Flag = '1'B 
                         then Offset contains the variable 
                         table entry number of the variable 
                         containing the value to be subtracted 
                         from the composite index calculated 
                         from index values and multipliers 
                         before multiplying by Element Size. 
    Offset               UBIN ALIGNED 
                         Either a value or an entry number 
                         determined by the Offset Flag. 
    Data Type            UBIN ALIGNED 
                         Indicates the type of data described 
                         by this entry.  EQUs for specifying data 
                         types can be found in the VREBL_DATATYPES 
                         macro in B$OBJECT_C. 
     Elements Flag       BIT(1) UNALIGNED 
                         Denotes the interpretation of the 
                         Elements field.  If Flag = '0'B 
                         then Elements contains the total 
                         number of elements in the array. 
                         If Flag = '1'B then Elements contains 
                         the variable record entry number 
                         of the variable containing the 
                         total number of elements in the array. 
     Elements            UBIN ALIGNED 
                         Contains a value or an entry number 
                         depending on the Elements Flag. 
     Multiplier Flag n   BIT(1) UNALIGNED 
                         Denotes the interpretation of the 
                         Multiplier n field.  If Flag = '0'B 
                         then the Multiplier field contains 
                         the actual multiplier.  If Flag = '1'B 
                         then the Multiplier field contains 
                         the variable record entry number of 
                         the variable containing the actual 
                         multiplier. 
     Multiplier n        UBIN ALIGNED 
                         Contains the multiplier for the array 
                         or a variable record entry number 
                         as determined by the Multiplier Flag. 
    For examples of the use of the various array parameters, see 
    the XUO$VRELB_CONT service. 
Output: 
None. 
Description: 
This routine builds continuation entries in the Variable Debug Record (record 
type %TYPVREBL).  It is used for dimensioned entries of Array Type %TYPEREF 
that have adjustable offsets, elements or multipliers, to describe the 
dimension attributes of the variable. 
B$OBJECT Reference: 
B$VREBLCA 
00004
00003
00001
00002
Format: 
CALL XUO$VREBL_CONT_ET (Minimum Value, 
                        Maximum Value, 
                        Name Pointer); 
Input: 
    Minimum Value  UBIN ALIGNED 
                   The starting value for this variable. 
    Maximum Value  UBIN ALIGNED 
                   The maximum value for this variable. 
    Name Pointer   SBIN 
                   The word offset into the debug names 
                   record locating the start of the 
                   text strings for the values of this 
                   variable.  The text strings for the 
                   values must be in order in the debug 
                   names starting at Name Pointer. 
Output: 
None. 
Description: 
This routine builds continuation entries in the Variable Debug Record (record 
type %TYPVREBL).  It is used to show the correspondence between the value of 
an enumerated type variable and the text string associated with that value. 
The continuation entry will describe the minimum and maximum values of the 
enumerated type.  If this variable is also an array, this continuation entry 
should be the first continuation entry. 
B$OBJECT Reference: 
B$VREBLCET 
00004
00003
00001
00002
Format: 
CALL XUO$VREBL_CONT_SET (Significant Bits, 
                         Data Type, 
                         Minimum Value, 
                         Pointer True, 
                         Pointer False); 
Input: 
    Significant Bits    UBIN ALIGNED 
                        The number of significant bits in 
                        the value of this data item if the 
                        data type of the set is enumerated 
                        type.  For other data types, Significant 
                        Bits contains the maximum value for the 
                        Set. 
    Data Type           UBIN ALIGNED 
                        The data type of the elements of the 
                        Set.  EQUs for specifying data types can be 
                        found in the VREBL_DATATYPES macro in 
                        B$OBJECT_C. 
    Minimum Value       UBIN ALIGNED 
                        Contains the minimum value for an 
                        element of the set. 
    Pointer True        SBIN ALIGNED 
                        Word offset into the Debug Names Record 
                        (Type %TYPDBGNAM) locating the start of the 
                        text string for the true value of each 
                        bit in the Set.  The text strings for 
                        all significant bits must be in order in 
                        the debug names starting at Pointer True. 
                        A value of -1 means not to print the 
                        text for the true value of each bit. 
    Pointer False       SBIN ALIGNED 
                        Word offset into the Debug Names Record 
                        (Type %TYPDBGNAM) locating the start of the 
                        text string for the false value of 
                        each bit in the Set.  The text strings 
                        for all significant bits must be in 
                        order in the Debug names starting at 
                        Pointer False.  A value of -1 means not 
                        to print the text for the false value of 
                        each bit. 
Output: 
None. 
Description: 
This routine builds continuation entries in the Variable Debug Record (record 
type %TYPVREBL).  It is used for FPL status variables and for variables with 
Data Type = SET.  The continuation entry locates the text strings associated 
with the true and false settings of each bit.  If this variable is also an 
array, this continuation entry should be the first continuation entry. 
B$OBJECT Reference: 
B$VREBLCSET 
00004
00003
00001
00002
A parser is a tool capable of breaking down input according to a known set of 
rules and generating an analysis of the string in a usable form.  The X$PARSE 
library service, the CP-6 common parser, analyzes a string of ASCII characters 
according to user-defined rules and generates a tree of output blocks. 
X$PARSE is used by many CP-6 processors (other library services, EDIT, PCL, 
etc.), but not for complex applications such as the FORTRAN compiler.  For 
further information, type: 
!HELP (HOSTLIB) X$PARSE 
!HELP (HOSTLIB) P_PCB 
!HELP (HOSTLIB) OUT$BLK 
!HELP (HOSTLIB) OUT$SYM 
!HELP (HOSTLIB) PARAM 
!HELP (HOSTLIB) PARSING_TOOLS 
!HELP (HOSTLIB) P$KEYWORDS 
!HELP (HOSTLIB) PARTRGE_STRUCTURES 
!HELP (HOSTLIB) P$NODE 
!HELP (HOSTLIB) P$LIT 
!HELP (HOSTLIB) P$SYM 
!HELP (HOSTLIB) P$DSTR 
The XUR services provide processors a uniform method of reading and parsing 
command input and of handling errors in command text.  The XUR services free 
the programmer from the details of obtaining command input.  For instance, XUR 
services: 
o   Provide an input DCB and input buffer for use in obtaining command input. 
o   Can identify the location of syntactical errors (in context or by a 
    pointer under the user's input). 
o   Can list legal alternatives for a syntactical element in error. 
o   Facilitate display of standard, multi-level error messages. 
o   Facilitate display of standard, multi-level HELP messages. 
o   Supply optional built-in commands (such as PRINT, DIR, etc.). 
The XUR services are provided for use in processors that run on software 
release B03 or prior releases.  The functions provided by XUR services are a 
subset of the functions provided by the XUG services.  The XUG services, 
instead of providing a complex call format as is done in the XUR services, use 
a function parameter table to store parameters and results.  The XUR services 
can be thought of as a "shell" around the XUG services that provides more 
convenient calling sequences.  All XUR services operate by calling the 
corresponding XUG service.  In some cases, additional information about the 
operation of a service can be found in the description of the XUG services. 
The services are categorized as follows: 
    CATEGORY                  SERVICE 
    Get and parse             XUR$INIT 
    a command                 XUR$GETCMD 
    Echo                      XUR$ECHO 
                              XUR$ECHOIF 
                              XUR$ECHOLAST 
    Error reporting           XUR$ERRMSG 
                              XUR$INFOMSG 
                              XUR$SETERRMSG 
                              XUR$ERRPTR 
                              XUR$ERRCNVRT 
                              XUR$ERRTOLCP6 
    HELP message reporting    XUR$HELP 
                              XUR$MOREMSG 
                              XUR$ALLMSG 
    DCB manipulation          XUR$SETDCBS 
                              XUR$CORRES 
                              XUR$FINDDCB 
                              XUR$GETDCB 
                              XUR$CLOSE_DCBS 
                              XUR$OPENOUT 
    Break control             XUR$BREAK 
                              XUR$DISABLE 
                              XUR$ENABLE 
                              XUR$CLRENABLE 
                              XUR$SIMULATE_BREAK 
Format: 
CALL XUR$ALLMSG [(xuh_param)] ALTRET (label); 
Parameters: 
xuh_param    is as described for XUR$HELP.  See the topic XUH_PARAM for 
details.  If xuh_param is not specified, the XUH_PARAM passed in the last call 
to XUR$HELP will be used. 
Description: 
The XUR$ALLMSG service calls XUR$ERRMSG or X$HELP service to get all remaining 
messages.  This service consults a flag which is set via XUR$HELP and reset 
via XUR$ERRMSG to determine which service to call. 
Error Conditions: 
Error codes returned by XUR$ALLMSG include those returned by the X$HELP 
library service. 
00002
00003
00001
Format: 
This service is entered asynchronously.  Type ?? for additional information. 
Parameters: 
None 
Description: 
The XUR$BREAK service is a generalized break handler available to programs 
using XUR$GETCMD.  It is entered asynchronously upon occurrence of a break. 
XUR$BREAK is established as the break service through a user call to M$INT. 
If XUR$BREAK is to be used, the user must establish (via a call to XUR$INIT) 
the identity of a routine to be called when the command in progress is aborted 
by a break event. 
When a break occurs, XUR$BREAK checks to see if the user has established a 
break-message routine via the BRKMSG parameter in the XUR_INIT structure 
passed to XUR$INIT.  If so, the specified routine is called; if not, the 
message 
    "Break!   C to continue" 
is issued through M$UC.  A read is then issued through M$UC; the action taken 
depends on the user's response to the read: 
  o  If the user responds with the single character 'C' or 'c', the routine 
     specified by XUR_INIT.CONTINUE$ is called (if it is non-NIL); an M$TRTN 
     is then issued to permit the routine which was interrupted by the break 
     to continue. 
  o  If the user enters a null response (simply a carriage return, line feed, 
     or other activation character), XUR$BREAK issues an M$CLRSTK and then 
     calls the routine specified by XUR_INIT.ABORT$, which must not be NIL. 
     This routine typically terminates with an UNWIND to continue execution at 
     some clean point in the user's program.  It can also call M$EXIT to 
     terminate the program.  It must not RETURN or ALTRETURN to XUR$BREAK. 
  o  If the user responds with anything other than a 'C', 'c', or a null 
     response, XUR$BREAK "remembers" the user's response and then proceeds as 
     though a null response had been entered (i.e., issue an M$CLRSTK and then 
     call XUR_INIT.ABORT$).  When the user's program issues its next call to 
     XUR$GETCMD, the "remembered" response is parsed as though it had been 
     entered in response to the XUR$GETCMD prompt. 
  o  If the user wishes to totally bypass the "Break!  C to continue" 
     processing, the routine specified in XUR_INIT.BRKMSG$ may opt to call the 
     system routine X66_TRTN.  This routine "unwinds" back to the routine 
     which was interrupted by the break; execution resumes at the point of 
     interruption with breaks disabled (via XUR$DISABLE).  The 
     XUR_INIT.BRKMSG$ routine may call XUR$CLRENABLE before calling X66_TRTN 
     to re-enable breaks, if desired. 
Breaks are ignored: 
  o  From the time XUR$BREAK is entered until it is exited. 
  o  If input while reading a command. 
00002
00001
Format: 
CALL XUR$CLOSE_DCBS ([dcb],[disp]) 
Parameters: 
dcb    is a variable containing the DCB number (UBIN WORD) of the DCB to 
close. 
disp    is a UBIN WORD value to be used for the DISP field on the close.  In 
CP_6_SUBS there are two EQUs that can be used for DISP, %SAVE# and %RELEASE#. 
Description: 
The XUR$CLOSE_DCBS service closes open DCBs.  If dcb is specified, then only 
that DCB will be closed.  Otherwise, all DCBs will be closed.  If disp is 
specified, then the DCBs will be closed with that DISP.  Otherwise, they will 
be closed with DISP=SAVE except for DCBs for FPRGs, which are closed with 
DISP=RELEASE. 
00002
00001
Format: 
CALL XUR$CLRENABLE; 
Parameters: 
None. 
Description: 
The XUR$CLRENABLE service re-enables breaks disabled by a call to XUR$DISABLE. 
Breaks that occurred while break processing was disabled are ignored when 
XUR$CLRENABLE is called. 
00002
00001
Format: 
CALL XUR$CORRES (dcb1,dcb2) ALTRET (label); 
Parameters: 
dcb1    is a variable containing DCB number (UBIN WORD). 
dcb2    is a variable containing DCB number (UBIN WORD). 
Description: 
The XUR$CORRES service performs a correspondence check of the specified DCBs. 
A default open is performed on the DCBs if they are not open. 
Error Conditions: 
If the DCB assignments correspond, the alternate return is taken. 
00002
00003
00001
Format: 
CALL XUR$DISABLE; 
Parameters: 
None 
Description: 
This XUR$DISABLE service disables breaks for critical code.  Calls to 
XUR$DISABLE may be nested. 
00002
00001
Format: 
CALL XUR$ECHO [(outdcb)] ALTRET (label); 
Parameters: 
outdcb    is a variable containing DCB number (UBIN WORD) for the output DCB. 
If outdcb is not specified, then M$LO will be used. 
Description: 
The XUR$ECHO service is used to write the last command through the output DCB. 
Error Conditions: 
XUR$ECHO takes the ALTRETurn if outdcb is omitted and an M$LO DCB is not 
found. 
00002
00003
00001
Format: 
CALL XUR$ECHOIF [(outdcb)] ALTRET (label); 
Parameters: 
outdcb    is a variable containing DCB number (UBIN WORD) of the output DCB. 
If outdcb is not specified, then M$DO is used. 
Description: 
The XUR$ECHOIF service performs a check to determine if the DCB identified by 
XUR_GETCMD.OUTDCB# corresponds with any DCB on which the current command has 
been displayed.  This will include the input DCB (XUR_GETCMD.INDCB#) and any 
other DCB through which the command has been echoed via calls to XUR$ECHO or 
XUR$ECHOIF. 
Error Conditions: 
XUR$ECHOIF takes the ALTRETurn if outdcb is omitted and an M$LO DCB is not 
found. 
00002
00003
00001
Format: 
CALL XUR$ECHOLAST [(outdcb)] ALTRET (label); 
Parameters: 
outdcb    is a variable containing DCB number (UBIN WORD) of the output DCB. 
If outdcb is not specified, then M$LO is used. 
Description: 
The XUR$ECHOLAST service writes the last command line through the output DCB. 
Error Conditions: 
XUR$ECHOLAST takes the ALTRETurn if outdcb is omitted and an M$LO DCB is not 
found. 
00002
00003
00001
Format: 
CALL XUR$ENABLE; 
Parameters: 
None 
Description: 
The XUR$ENABLE service re-enables breaks disabled by a call to XUR$DISABLE. 
Breaks that occurred while break processing was disabled will be honored when 
XUR$ENABLE is called. 
00002
00001
Format: 
CALL XUR$ERRCNVRT (lcp6_error_code, error_code); 
Parameters: 
lcp6_error_code    is a variable containing lcp-6 error code 
(fcg/mid/m/err/sev) to be passed back through the coupler. 
error_code    is a variable containing error code in CP-6 standard format. 
Description: 
This routine will convert an LCP-6 error code (32 bits, stored in 36 bits with 
the high-order bit in each byte being zero) into the equivalent CP-6 standard 
error code format (36 bits). 
00002
00001
Format: 
CALL XUR$ERRMSG ([code],[errdcb],[erroutdcb],[f1],[f2],[f3],[flaglev]) 
    ALTRET (label); 
Parameters: 
code    is a variable containing standard CP-6 error code. 
errdcb    is a variable containing the number (UBIN WORD) of the DCB on which 
the error occurred.  errdcb is used to obtain variable information which is 
substituted into the message for special strings %FN, %AC, etc.  If an error 
message contains those special strings and errdcb is not specified, then 
blanks are substituted, or the conditional phrase is not printed. 
erroutdcb    is a variable containing the number (UBIN WORD) of the DCB 
through which the error message is to be written.  The default is M$DO and 
M$LO with correspondence checking. 
f1    is a vector framing a TEXTC string for %U1 substitution. 
f2    is a vector framing a TEXTC string for %U2 substitution. 
f3    is a vector framing a TEXTC string for %U3 substitution. 
flaglev    is a value (1-4) that specifies the number of asterisks to print in 
front of the message.  The default is 0. 
Description: 
The XUR$ERRMSG service controls error processing by passing parameters to 
M$ERRMSG. 
Error Conditions: 
When the "code" parameter is omitted, the severity field of the last code is 
incremented.  If the severity field exceeds 7 or no message is found, the 
alternate return is taken. 
00002
00003
00001
Format: 
CALL XUR$ERRPTR ([cpos],[outdcb]) ALTRET (label); 
Parameters: 
cpos    is a UBIN WORD value that specifies the character position at which 
the error occurred.  This value is usually obtained from either the Parse 
Control Block field P_PCB.HI_CHAR or the output block field OUT$BLK.CPOS.  If 
cpos is omitted, P_PCB.HI_CHAR is used. 
outdcb    is a variable containing the DCB number (UBIN WORD) of the output 
DCB.  If outdcb is not specified, then M$DO is used. 
Description: 
The XUR$ERRPTR service displays a message identifying where an error detected 
by XUR$GETCMD occurred within command text.  The message "Error at <?>:" 
followed by a portion of the command text with <?> inserted where the error 
was detected in output. 
NOTE:  Instead of the partial line error message described in the previous 
paragraph, the error pointer (^) may be displayed at the point of the error. 
This can be done by issuing the IBEX command "!POINT" before calling 
XUR$ERRPTR.  However, displaying "^" is appropriate only if CPOS is within the 
last line of the command. 
Error Conditions: 
XUR$ERRPTR takes the ALTRETurn if outdcb is omitted and an M$LO DCB is not 
found. 
00002
00003
00001
Format: 
CALL XUR$ERRTOLCP6 (lcp6_err, cp6_err); 
Parameters: 
lcp6_err    is a variable containing lcp-6 error code (fcg/mid/m/err/sev) to 
be passed back through the coupler. 
cp6_err    is a variable containing error code in CP-6 standard format. 
Description: 
The XUR$ERRTOLCP6 service converts error code to lcp-6 equivalent. 
00002
00001
Format: 
CALL XUR$FINDDCB (dcbname,dcbloc) ALTRET (label); 
Parameters: 
dcbname    is a variable containing a DCB name (in TEXTC format) that 
identifies a DCB to be searched for in the DCB table. 
dcbloc    is a variable that identifies where the DCB number is to be 
returned.  The DCB number is returned as an SBIN WORD value. 
Description: 
The XUR$FINDDCB service returns a DCB number. 
Error Conditions: 
The alternate return is taken if the DCB name is not found in the table. 
00002
00003
00001
Format: 
CALL XUR$GETCMD (node,out$,[prompt],[text],[tsize],[eptr]) ALTRET (label); 
Parameters: 
node    is the name of the top parse node.  Refer to the discussion of the 
parsing service (XUP topic) for details. 
out$    identifies a POINTER variable into which either P_PCB.OUT$ or an error 
code is stored. 
NOTE:  The following parameters are optional.  A comma indicates the omission 
of each of the following parameters.  Commas are required preceding any 
optional parameter specified. 
prompt    is the character string to be used as the prompt for command input. 
If prompt is passed then prompt is either (a) a TEXTC prompt string, or (b) a 
vector framing a text prompt string.  In case (a) if the high order bit in the 
first byte of the string is set, (i.e., if the first byte contains the actual 
length of the prompt string plus 256), the first character in the text portion 
of the string will be used as the VFC character for the prompt string.  If 
prompt is omitted, then XUR$GETCMD will not set the prompt.  If 
prompt=VECTOR(NIL), then XUR$GETCMD will reset the prompt to the default 
prompt.  If prompt=VECTOR(ERASE), then XUR$GETCMD will not set the prompt. 
text    specifies the text string to be used as the first line of input to the 
parser when input is to be read from other than the input DCB (e.g., from 
JIT.CCBUF). 
tsize    is a UBIN WORD value that defines the size of the full text string in 
characters.  tsize is only meaningful when the text parameter is specified. 
If tsize is omitted and text is present, the Parse Control Block field 
P_PCB.NCHARS is used. 
eptr    identifies an entry pointer to a procedure to be called for success, 
failure, and pre-parse nodes. 
Description: 
XUR$GETCMD reads the command text and calls the X$PARSE library service, 
passing it parse nodes in addition to other possible parameters.  XUR$GETCMD 
can parse commands described in user-defined parse nodes and, optionally, can 
parse and perform a set of built-in commands.  XUR$GETCMD also has 
capabilities to echo command input and to recall a previous command line; see 
Usage Notes for details. 
If the command entered is syntactically correct, XUR$GETCMD takes these 
actions: 
o   For a user-defined command, it returns a parse output tree via the out$ 
    parameter. 
o   For a built-in command, if COMMANDS=YES in the XUR_INIT structure (the 
    default), it performs the built-in function.  See the XUR_INIT subtopic 
    for the list of built-in commands.  For the DO or ! command, XUR$GETCMD 
    passes control to the command processor for execution of the command. 
    In addition, before or after any built-in command, the command processor 
    may take control if PRE_EXEC or POST_EXEC is specified in the XUR_INIT 
    structure.  In either case, two parameters are passed by XUR$GETCMD:  the 
    first parameter is used by XUG$GETCMD and should be ignored; the second 
    parameter is a code defined in XU_SUBS_C.:LIBRARY that identifies the 
    built-in command in the buffer.  (The relevant EQUs in XU_SUBS_C contain 
    the prefix XUG_CMD.) 
If the command entered is syntactically incorrect, how XUR$GETCMD functions 
depends on the setting of several flags in the XUR_INIT structure. 
o   If GOODCMD=YES, XUR$GETCMD returns to the caller only when the command 
    received is syntactically correct, and causes a dialog with the 
    time-sharing user in the case of syntax errors.  The dialog conducted at a 
    syntax error depends on the command input and the setting of the SYNTAX 
    flag. 
o   If GOODCMD=NO, XUR$GETCMD returns to the caller when the command received 
    is syntactically correct, and takes the alternate return in case of a 
    syntax error. 
Setting SYNTAX=YES requests XUR$GETCMD to retain information about the 
previous parsing operation in order to display a list of legal alternatives to 
the last element parsed.  The following situations illustrate the dialog that 
XUR$GETCMD can conduct on behalf of the caller: 
Case 1:  Assume GOODCMD=YES, SYNTAX=YES, and a syntax error is detected 
    because of a misspelling that causes a mismatch to the parse nodes: 
    o   A message is displayed to identify the location of the syntax error 
        (via an internal call to XUR$ERRPTR). 
    o   If the time-sharing user enters ? to obtain more information, the list 
        of legal alternatives is output via M$DO.  (This is done by XUR$GETCMD 
        with the NXT flag in the Parse Control Block set to cause reparsing of 
        the command containing the syntax error.) 
Case 2:  Assume GOODCMD=YES, SYNTAX=YES, and a syntax error is detected 
    because the command includes the ? character causing a mismatch to the 
    parse nodes: 
    o   The list of legal alternatives is output via M$DO (by means of an 
        internal call to XUR$GETCMD with the NXT flag set in the Parse Control 
        Block that reparses the command containing the syntax error). 
Both cases illustrate the simplest way to take advantage of the features of 
XUR$GETCMD and reduce the amount of command input processing required in the 
user's code.  If GOODCMD=NO, the internal calls can be performed by the caller 
instead.  If SYNTAX=NO, the caller can take charge of supplying the error 
diagnostic information (i.e., via calls to XUR$ERRMSG or XUR$MOREMSG). 
Error Conditions: 
When an error occurs during an XUR$GETCMD operation, XUR$GETCMD will ALTRETurn 
with the error code in the OUT$ parameter. 
Usage Notes: 
1.  If XUR$GETCMD returns normally and out$ contains anything other than 
    ADDR(NIL), then out$ points to the tree of parse blocks which describe the 
    user's commands; the caller should process the command.  If XUR$GETCMD 
    returns normally and out$ contains ADDR(NIL), then GETCMD has completely 
    processed whatever input was passed (i.e., a built-in command); the caller 
    need take no further action with this command. 
2.  Echoing of command input is subject to the ECHO flag in the XUR_INIT 
    structure and the ECHO flag set via the command processor ECHO command. 
    ECHO Flag in XUR_INIT      Action of XUR$GETCMD 
    ECHO=NEVER_ECHO            Never echo the command. 
    ECHO=ALWAYS_ECHO           Echo the command except if the command is read 
                               from the terminal or if the DVBYTE.TRANS# bit 
                               is set. 
    ECHO=HONOR_FLAG            Echo the command if the input DCB is assigned 
                               to a file. 
                               Echo the command if the output DCB is not 
                               assigned to a terminal. 
                               Echo the command if the input DCB is reading 
                               from the command stream and ECHO is on (i.e., 
                               is set via the command processor ECHO command). 
3.  XUR$GETCMD facilitates error correction by saving command text that the 
    time-sharing user may recall; this feature is provided only for commands 
    of 255 characters or less and for commands entered on one line (without 
    the continuation (;) character).  For example, following a syntax error 
    entering the Escape-D sequence redisplays the command and repositions the 
    cursor to the first reported error. 
00002
00003
00001
00004
Format: 
CALL XUR$GETDCB (dcbname,dcbloc) ALTRET (label); 
Parameters: 
dcbname    is a variable containing a DCB name in TEXTC format of the DCB that 
is to be searched for in the DCB table. 
dcbloc    is a variable that identifies where the DCB number is to be 
returned.  The DCB number is returned as an SBIN WORD value. 
Description: 
The XUR$GETDCB service returns a DCB number for an existing DCB or calls 
M$GETDCB to return the DCB number for a DCB which it allocates. 
This service searches the DCB table for the specified DCB.  If it is not 
found, M$GETDCB is called to create it. 
Error Conditions: 
If M$GETDCB takes an alternate return, XUR$GETDCB takes an alternate return 
also, and the error code can be found in the ALTRET frame. 
00002
00003
00001
Format: 
CALL XUR$HELP (xuh_param) ALTRET (label); 
Parameters: 
xuh_param    is the parameter block passed to X$HELP.  See topic XUH_PARAM for 
details. 
Description: 
The XUR$HELP service keeps track of whether the last message operation was 
performed by M$ERRMSG or M$HELP; this service calls X$HELP passing parameters 
in the structure XUH_PARAM.  Based on a flag set by XUR$HELP and reset by 
XUR$ERRMSG, the XUR$MOREMSG and XUR$ALLMSG services can determine whether to 
obtain a HELP or an error message. 
Error Conditions: 
If X$HELP takes an alternate return, XUR$HELP calls XUR$ERRMSG with the error 
code in XUH_PARAM and takes the alternate return. 
00002
00003
00001
Format: 
CALL XUR$INFOMSG ([code],[errdcb],[erroutdcb],[f1],[f2],[f3],[flaglev]) 
    ALTRET (label); 
Parameters: 
code    is a variable containing standard CP-6 error code. 
errdcb    is a variable containing the number (UBIN WORD) of the DCB on which 
the error occurred.  errdcb is used to obtain variable information which is 
substituted into the message for special strings %FN, %AC, etc.  If an error 
message contains those special strings and errdcb is not specified, then 
blanks are substituted, or the conditional phrase is not printed. 
erroutdcb    is a variable containing the number (UBIN WORD) of the DCB 
through which the error message is to be written.  The default is M$DO and 
M$LO with correspondence checking. 
f1    is a vector framing a TEXTC string for %U1 substitution. 
f2    is a vector framing a TEXTC string for %U2 substitution. 
f3    is a vector framing a TEXTC string for %U3 substitution. 
flaglev    is a value (1-4) that specifies the number of asterisks to print in 
front of the message.  The default is 0. 
Description: 
The XUR$INFOMSG service controls error processing by passing parameters to 
M$ERRMSG.  The XUR$INFOMSG service is identical to the XUR$ERRMSG service, 
except that the error code is not saved for use with a subsequent "?" or "??" 
command, nor is it passed to the dialog manager. 
Error Conditions: 
When the "code" parameter is omitted, the severity field of the last code is 
incremented.  If the severity field exceeds 7 or no message is found, the 
alternate return is taken. 
00002
00003
00001
Format: 
CALL XUR$INIT (XUR_INIT,[p_pcb$],[param$]) ALTRET (label)]; 
Parameters: 
XUR_INIT    is the structure built by the %XUR_INIT macro which is described 
under the topic XUR_INIT. 
p_pcb$    is an optional pointer which, if present, will be set to the address 
of the X$PARSE Parse Control Block which will be used by XUR$GETCMD.  If the 
PCB$ field in the XUR_INIT structure is non-NIL when XUR$INIT is called, 
P_PCB$ will be set equal XUR_INIT.PCB$; otherwise, P_PCB$ will be set to the 
address of a PCB built in the XUR$GETCMD work area. 
param$    is an optional pointer to the XUG_GETCMD structure. 
Description: 
The XUR$INIT service may be used to initialize parameters or flags used by 
XUR$GETCMD.  The user may: 
o   Provide entry pointers designating routines that are to be called by 
    XUR$GETBREAK if a break event occurs; 
o   Set or reset the SYNTAX, COMMANDS, GOODCMD, and/or SPELLING flags; 
o   Specify the address of a PCB (parse control block) which XUR$GETCMD is to 
    use while parsing commands, or request that XUR$INIT allocate a PCB for 
    its own use and return the address of the PCB to the user; 
o   Provide a vector framing a block of memory which XUR$GETCMD is to use for 
    its PCB, input buffer, and parse work area. 
In addition to resetting all parameters that can be specified on the XUR$INIT 
macro, XUR$INIT reinitializes various internal values that are supplied by 
other XUR services.  However, values that are kept in the XUG_GETCMD block are 
not changed, unless there is a corresponding field in the XUR_INIT macro. 
00002
00001
Format: 
CALL XUR$MOREMSG ([xuh_param]) ALTRET (label); 
Parameters: 
xuh_param    is the parameter block passed to X$HELP.  See the topic XUH_PARAM 
for details.  If xuh_param is omitted, XUR$MOREMSG will use the XUH_PARAM used 
in the last call to XUR$HELP. 
Description: 
The XUR$MOREMSG service calls XUR$ERRMSG or X$HELP as appropriate to get the 
next level message.  The XUR$MOREMSG service consults a flag which is set via 
XUR$HELP and reset via XUR$ERRMSG to determine which service to call. 
Error Conditions: 
Error codes returned by XUR$MOREMSG include those returned by the X$HELP 
library service. 
00002
00003
00001
Format: 
CALL XUR$OPENOUT (dcb#,out$blk,fpt_open) ALTRET (label); 
CALL XUR$OPENOUT (dcb#,out$blk,fpt_open[,err_code]) ALTRET (label); 
Parameters: 
dcb#    is the number of the DCB to be opened.  This parameter overrides the 
DCB in the FPT_OPEN when both are passed. 
fpt_open    is an FPT for M$OPEN.  FPT_OPEN.V.DCB# must be set to the number 
of the DCB to be opened, if the dcb# argument is omitted.  The remaining 
M$OPEN parameters should be set to the desired values.  If omitted, the 
following default values, typical for the OUTPUT command, will be used: 
    %FPT_OPEN (DCB=M$LO, SCRUB=YES, ORG=UR, ACS=SEQUEN, ASN=DEVICE, RES='ME', 
    FUN=CREATE, EXIST=ERROR); 
Other parameters such as SETDCB and REASSIGN may also be specified. 
out$blk    is the output block returned by X$PARSE (usually via a prior call 
to XUR$GETCMD) that corresponds to the XUR$OPENOUT_SPEC or XUR$OPENOUT_OPT 
parse node.  See Usage Note 1 for further description of these parse nodes. 
The parse output block overrides the FPT defaults when conflicting information 
is passed by the user. 
err_code    returns a standard CP-6 error code if the call ALTRETurns. 
Description: 
The XUR$OPENOUT service opens the specified DCB in preparation for a simple 
output function, based on information in the output block referenced by 
out$blk. 
Error Condition: 
If an error occurs, the DCB is left closed and the error code is returned in 
err_code, if present.  It is the responsibility of the calling program to 
re-open the DCB after an error, if required. 
Usage Notes: 
1.  SYMDEFed parse nodes provided for simple output functions are included in 
    :LIB_SYSTEM.  The following parse nodes are available to direct only the 
    results of one command to another output stream without affecting normal 
    output of the processor: 
    XUR$OPENOUT_OPT which defines the syntax: 
        [[{ON|TO|OVER|INTO}] fid [(optionlist)]] 
    XUR$OPENOUT_SPEC which defines the syntax: 
        {ON|TO|OVER|INTO} fid [(optionlist)] 
    For example, the user's parse nodes could define an output command 
    as follows: 
        OUT_CMD(%T$OUT)    = 'OUT/PUT' XUR$OPENOUT_OPT 
    The parse nodes XUR$OPENOUT_OPT and XUR$OPENOUT_SPEC imply the following: 
    a.  ON|TO    specify that the command is to be errored if the fid 
        references a file which already exists. 
        OVER    specifies that is the fid references an existing file, that 
        file is to be replaced by the output. 
        INTO    specifies that if the fid references an existing file, the 
        output is to be appended to the end of that file. 
        The default is ON. 
    b.  The fid, that specifies the destination of the output, may be any 
        standard CP-6 fid. 
    c.  The optionlist may include any of the following: 
        O[RGANIZATION]={C[ONSECUTIVE]|U[NIT]R[ECORD]} 
        F[ORM]={formname|'formname'} 
        I[XTNSIZE]=number 
        N[TNSIZE]=number 
00002
00003
00001
00004
Format: 
CALL XUR$SETDCBS ([indcb],[outdcb],[erroutdcb1],[erroutdcb2]); 
Parameters: 
indcb    is a variable containing a DCB number (UBIN WORD) of the input DCB. 
outdcb    is a variable containing a DCB number (UBIN WORD) of the output DCB. 
erroutdcb1    is a variable containing a DCB number (UBIN WORD) of the default 
DCB for XUR$ERRMSG DCB correspondence. 
erroutdcb2    is a variable containing a DCB number (UBIN WORD) of the default 
DCB for XUR$ERRMSG DCB correspondence. 
Description: 
The XUR$SETDCBS service changes the input and output DCBs used by XUR$GETCMD, 
and default output DCBs, used by XUR$ERRMSG.  Any parameter may be omitted if 
that DCB is not to be changed.  The default DCB assignments are M$SI for 
reading, M$ME for echoing, M$LO for erroutdcb1, and M$DO for erroutdcb2. 
00002
00001
Format: 
CALL XUR$SETERRMSG [(msgfile-fid)] ALTRET (label); 
Parameters: 
msgfile-fid    is a variable containing a TEXTC string containing the fid of 
the error message file to be used on subsequent calls to XUR$ERRMSG.  If this 
string is not specified, the default error message file is used. 
Description: 
The XUR$SETERRMSG service establishes the error message file to be used on 
subsequent calls to XUR$ERRMSG.  M$FID is called to obtain the name, account 
and password of the msgfile-fid. 
Error Conditions: 
If XUR$SETERRMSG takes the alternate return, the error code is stored in the 
ALTRET frame. 
00002
00003
00001
Format: 
CALL XUR$SIMULATE_BREAK; 
Parameters: 
None 
Description: 
The XUR$SIMULATE_BREAK service causes a break event to be simulated.  If break 
processing is enabled, the XUR$BREAK routine will be entered as if the user 
had pressed the BREAK key.  If break processing is disabled (see the 
XUR$DISABLE topic), the break event will be recorded for processing at a later 
time (once breaks are re-enabled through a call to XUR$ENABLE). 
00002
00001
For a description of each parameter, type: 
HELP (HOSTLIB) XUR_INIT param 
where param is one of the following:  ABORT, ADAPT, BRKMSG, CONTINUE, 
COMMANDS, DONT_REREAD_CCBUF, DONT_STRIP_PROMPT, ECHO, GOODCMD, INHIBIT_DATE, 
INHIBIT_DIRECTORY, INHIBIT_DO, INHIBIT_END, INHIBIT_ERASE, INHIBIT_HELP, 
INHIBIT_NULL, INHIBIT_OUTPUT, INHIBIT_PRINT, INHIBIT_QMARK, PASS, PCB, 
POST_EXEC, PP_DCB, PPCB, PRE_EXEC, PREPROCESS, PREPROCESSOR, PROCNAME, 
SPELLING, SYNTAX, or WORK. 
    ABORT|BRKMSG|CONTINUE = ENTRY    specifies a user procedure to be called 
    by XUR$BREAK as appropriate.  The ABORT, BRKMSG, and CONTINUE parameters 
    initialize the EPTR fields named "name.ABORT$", "name.BRKMSG$, and 
    "name.CONTINUE$" respectively, and must be specified if XUR$BREAK is to be 
    used.  The default is NIL. 
    ADAPT = EPRT    points to the dialog manager procedure to be called if the 
    program is started under an ADAPT dialog, or if the ENTER built-in command 
    is used to start a dialog within the program.  The default is XTX$ADAPT. 
    Programs that cannot run under ADAPT dialogs must specify ADAPT=NIL.  See 
    the CP-6 ADAPT Reference (HA12) for more information. 
    COMMANDS = {YES|NO}    if YES, specifies that XUR$GETCMD is to perform 
    built-in commands.  When COMMANDS=YES the parse nodes for the built-in 
    commands are to be combined with the user's parse nodes.  The built-in 
    command nodes are added after the user nodes.  The default is YES. 
    The built-in commands are as follows: 
      DATE 
      {DIR|DIRECTORY} 
      {DO|!} 
      {E|EN|END} 
      ERASE 
      {[E]X|[E]XI|[E]XIT} 
      TIME 
      {H|HE|HEL|HELP} 
      {OUT|OUTP|OUTPU|OUTPUT} 
      PRINT 
      {Q|QU|QUI|QUIT} 
      ? 
      ?? 
    The functions performed by these commands are as described for IBEX.  See 
    the IBEX HELP facility for details.  The {DO|!} passes the command to the 
    command processor for processing.  If used in an XEQ or BATCH job, the "!" 
    must not be in column one or the user can use DO.  The ! command may be 
    preceded by blanks or by the processor's prompt. 
    DONT_REREAD_CCBUF = {YES|NO} specifies, if YES, that only the text 
    actually parsed is to be placed in the reread buffer after syntax error 
    parsing the program's invocation command line.  The default is NO, 
    indicating that the entire command line is to be reread, even if only the 
    options portion of it was parsed. 
    DONT_STRIP_PROMPT = {YES|NO} specifies whether the logic to remove the 
    program's prompt from the beginning of commands is to be overridden.  YES 
    specifies no check for a prompt at the beginning of each command line.  NO 
    specifies that the prompt is to be removed if it is present.  The default 
    is NO. 
    ECHO = {HONOR_FLAG|ALWAYS_ECHO|NEVER_ECHO}    indicates whether to ECHO 
    the command or not.  Default is HONOR_FLAG.  HONOR_FLAG indicates that 
    XUR$GETCMD will echo the command if, and only if the user's ECHO flag is 
    set.  ALWAYS_ECHO indicates that XUR$GETCMD will echo the command through 
    the user's echo DCB.  NEVER_ECHO indicates that XUR$GETCMD will not echo 
    the command. 
    GOODCMD = {YES|NO}    specifies that XUR$GETCMD should only return after a 
    syntactically correct command has been received.  The default is NO. 
    INHIBIT_DATE = {YES | NO} Specifies that the built-in commands DATE and 
    TIME should not be recognized or executed.  The default is NO. 
    INHIBIT_DIRECTORY = {YES | NO} Specifies that the built-in command 
    DIRECTORY should not be recognized or executed.  The default is NO. 
    INHIBIT_DO = {YES | NO} Specifies that the built-in commands DO and ! 
    should not be recognized or executed.  The default is NO. 
    INHIBIT_END = {YES | NO} Specifies that the built-in commands END, XIT, 
    and QUIT should not be recognized or executed.  The default is NO. 
    INHIBIT_ERASE = {YES | NO} Specifies that the built-in command ERASE 
    should not be recognized or executed.  The default is NO. 
    INHIBIT_HELP = {YES | NO} Specifies that the built-in command HELP should 
    not be recognized or executed.  The default is NO. 
    INHIBIT_NULL = {YES | NO} Specifies that the built-in null (empty) command 
    should not be recognized or executed.  The default is NO. 
    INHIBIT_OUTPUT = {YES | NO} Specifies that the built-in command OUTPUT 
    should not be recognized or executed.  The default is NO. 
    INHIBIT_PRINT = {YES | NO} Specifies that the built-in command PRINT 
    should not be recognized or executed.  The default is NO. 
    INHIBIT_QMARK = {YES | NO} Specifies that the built-in commands ? and ?? 
    should not be recognized or executed.  The default is NO. 
    MOREMEM = EPTR points to a procedure to be called if XUR$GETCMD needs more 
    memory and the user maintains the memory for XUR$GETCMD. 
    The calling sequence is as follows: 
    CALL user-routine ( words-needed , work-vector , errcode ) [ALTRET ( label 
    )]; 
    where: 
    words-needed    is an SBIN WORD containing the number of words needed.  If 
    positive, this is a request to allocate more memory.  If negative, this is 
    a request to free memory. 
    work-vector    returns a vector framing the entire work area on a normal 
    return.  The returned vector is checked to insure that an area of the 
    proper size has been allocated or freed contiguous with the old work area. 
    errcode    returns a standard CP-6 error code to be passed back to the 
    caller of XUR$GETCMD when the MOREMEM routine takes the ALTRETurn. 
    PASS = {LEAVE|BLANK|MODE}    indicates whether or not the password will be 
    blanked.  BLANK indicates the password will be blanked.  LEAVE indicates 
    that the password should not be blanked.  MODE means that the password 
    will be blanked according to the mode, they will be blanked for all modes 
    except ONLINE.  The default is LEAVE. 
    PCB = VARIABLE    initializes the field "name.PCB$", and is used to 
    specify the address of a Parse Control Block which XUR$GETCMD is to use 
    when calling X$PARSE.  The default is NIL, which indicates that XUR$INIT 
    is to build a PCB in its work area. 
    POST_EXEC = ENTRY    is an entry pointer to a procedure that is to be 
    called after one of the built-in commands is executed.  The default is 
    NIL. 
    The calling sequence is as follows: 
    CALL user_routine ( xur_getcmd , node-code ) [ALTRET ( label ) ] ; 
    where: 
    xur_getcmd    is the structure returned by XUR$INIT. 
    node-code    is the parse node code for the built-in command being 
    processed, as defined by EQUs of the form %XUG_CMD_? in the XU_SUBS_C 
    include file. 
    Note:  If an ALTRETurn occurs, the error code in xug_getcmd.ERR# will be 
    reported in the same way as other errors in processing a built-in command. 
    PP_DCB = VALUE-DEC(0-?)    is a DCB number for X$PRE_PROCESS to use for 
    test opens on such function as $FID_EXIST.  If X$PRE_PROCESS needs a DCB 
    for a test open, and the user has not specified a DCB number, then 
    XUR$GETCMD acquires a DCB and passes its number to X$PRE_PROCESS.  (The 
    dynamically acquired DCB is released when X$PREPROCESS returns control to 
    XUR$GETCMD.)  The default is 0. 
    PPCB = VARIABLE    specifies the identity of the preprocessor's control 
    block.  This is passed to X$PRE_PROCESS if the flag PREPROCESS# is set. 
    The default is NIL. 
    PRE_EXEC = ENTRY    is an entry pointer to a procedure which is to be 
    called before one of the built-in commands is executed.  The default is 
    NIL. 
    The calling sequence is as follows: 
    CALL user_routine ( xur_getcmd , node-code ) [ ALTRET ( label ) ] ; 
    where: 
    xur_getcmd    is the structure returned by XUR$INIT. 
    node-code    is the parse node code for the built-in command being 
    processed, as defined by EQUs of the form %XUG_CMD_? in the XU_SUBS_C 
    include file. 
    Note:  If an ALTRETurn occurs, the error code in xug_getcmd.ERR# will be 
    reported in the same way as other errors in processing a built-in command. 
    PREPROCESS = {YES|NO}    indicates, if YES, that the user wants XUR$GETCMD 
    to do preprocessing on lines containing a percent (%) sign.  The type of 
    preprocessing depends on the value given for PREPROCESSOR.  The default is 
    NO. 
    PREPROCESSOR = EPTR provides the name of a routine to be called to do 
    preprocessing of commands.  This is meaningful only if PREPROCESS=YES is 
    also specified.  If PREPROCESSOR=NIL, command variable substitution will 
    be performed; if the word immediately following a (%) percent sign is the 
    name of an IBEX command variable, the value of that variable is 
    substituted before the command is parsed.  Otherwise, the specified 
    routine (usually X$PRE_PROCESS) is called to perform any necessary 
    preprocessing.  The default is NIL. 
    PROCNAME = VARIABLE    locates a VLP_NAME area containing the name of the 
    processor for which a help message is requested.  The default is NIL. 
    SPELLING = {YES|NO}    specifies whether the spelling-error-detection 
    feature of XUR$GETCMD is to be used.  Meaningful only if SYNTAX=YES.  The 
    default is YES. 
    SYNTAX = {YES|NO}    initializes the field "name.SYNTAX#, and is used to 
    specify whether the special command-syntax feature of XUR$GETCMD is to be 
    used.  The default is YES. 
    WORK = VARIABLE    specifies an area of memory (which must be at least 500 
    words long and must contain an integral number of doublewords) which 
    XUR$GETCMD is to use for its parse control block, input buffer, and parse 
    work area.  Workarea initializes the vector "name.WORK_" and has a default 
    value of NIL.  To be honored, the work area must be specified on the first 
    call to XUR$INIT and before any other call to any XUR routine.  If a work 
    area is not specified, XUR$GETCMD acquires a 1-page work area in the first 
    available dynamic segment, and extends the segment as necessary to provide 
    enough work area to successfully input and parse any command up to 49 
    lines long. 
00001
00002
00001
00003
00001
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
00023
00022
00025
00026
00024
00027
00028
00029
00030
The XUS service, XUS$CORRECT_SPELLING, can provide possible alternatives for 
slight misspellings, based on a user-supplied list of legal words.  The 
XUS$CORRECT_SPELLING service also provides an option to recognize 
abbreviations. 
Format: 
CALL XUS$CORRECT_SPELLING (n_legal, legal$, user_word, abbrev, possibles) 
    ALTRET (label); 
Parameters: 
n_legal    is an SBIN WORD containing the number of words in the legal-word 
list identified by legal$.  On return, n_legal will contain the number of 
matches found (i.e., the number of bits set in possibles). 
legal$    is an array of pointers; n_legal specifies the number of entries in 
the array.  Each pointer points to a TEXTC string containing a legal word (the 
TEXTC string can be declared using the VLP_NAME macro).  This word should be 
fully spelled out; initial-substring abbreviations should not have separate 
entries in legal$, although contraction and mnemonic abbreviations should have 
separate entries. 
user_word    is a TEXTC string containing the user-entered word to be checked 
against the legal-word list. 
abbrev    is a BIT(1) ALIGNED flag; if set, user_word is matched as an initial 
substring of the legal words; if reset, all of user_word is matched against 
the legal words. 
possibles    is an array of n_legal bits.  It may be uninitialized at entry. 
On return, a bit will be set in possibles for each word in the legal$ array 
which could match user_word.  Specifically, possibles(n) will be set if 
user_word could match the word pointed to by legal$(n). 
Description: 
Given a user-entered word and a list of legal words, XUS$CORRECT_SPELLING 
determines if the user-word is a slight misspelling of one of the legal words. 
Each word in the legal-word list is checked against the user-word; the legal 
word is considered a match if it differs from the user-word in only one place 
(one error in the user-word), and the difference (error) is one of the 
following: 
o   Transposition of two adjacent characters 
o   One character wrong 
o   One extra character 
o   One character missing 
If the legal word and the user word are equal except for one of the above 
differences, then the legal word is considered a match, or possible 
correction, for the user word. 
Note:  If the user word is correctly spelled, that word is returned, as well 
as any other legal words which are considered a match. 
The caller can allow or disallow abbreviations.  If abbreviation is allowed, 
the user word can be any initial substring of a legal word (and abbreviation 
does not count as the one difference allowed for a match). 
One-character user-words never result in any possible corrections; 
two-character user-words are only checked for transposition or 
missing-character errors, because the extra-character and wrong-character 
error checks would match too many of the legal words. 
On normal return, XUS$CORRECT_SPELLING returns a list of the legal words which 
could match the user-word, and a count of the number of matches. 
Error Conditions: 
If no possible spelling corrections are found, XUS$CORRECT_SPELLING will take 
the alternate return. 
Usage Notes: 
1.  If the caller wants to be insensitive to alphabetic case (e.g., consider T 
    and t to be equal), the caller should convert both the legal list and the 
    user word to the same alphabetic case (upper case or lower case) before 
    calling XUS$CORRECT_SPELLING. 
00002
00003
00001
00004
The Source Update Package provides input management services.  These services 
are used by CP-6 language processors to read source, update and INCLUDE (COPY) 
files.  The XUU services allow a language processor to obtain source records 
from several sources (all keyed or consecutive files): 
o   A base source file 
o   An update file (that follows conventions described in "Format of the 
    Update File") 
o   One or more files referenced by a "read source library file" directive 
    (e.g., the PL-6 %INCLUDE directive) referred to here as INCLUDE files. 
    INCLUDE files may be nested to a level of ten.  INCLUDE files are 
    referenced in COBOL by the COPY verb, in FORTRAN by the INCLUDE statement, 
    and in GMAP6 by the LODM pseudo-operation. 
The processor calling the XUU services can obtain records sequentially, with 
update records substituted as necessary for obsolete source base records and 
with INCLUDE records inserted as necessary.  The XUU$READ service maintains 
its place in the various files simultaneously and provides source output and 
update listing options. 
The XUU services are serially re-usable.  For instance, XUU$OPEN can be called 
repeatedly for separate sets of source update files. 
For a summary of XUU services, type: 
HELP (HOSTLIB) XUU service 
where service is: XUU$CLOSE, XUU$OPEN, or XUU$READ. 
  Service        Description 
  XUU$CLOSE 
                 Close source input and/or output files. 
  XUU$OPEN 
                 Open source input files; set parameters controlling listing 
                 of updates and "no update file" condition. 
  XUU$READ 
                 Obtain next sequential input record from one of three 
                 sources:  base source file, update file, or INCLUDE file; 
                 return flags identifying source and key/sequential record 
                 number; optionally write source output file. 
00001
00002
00003
Format: 
CALL XUU$CLOSE (XUU_PARAM) ALTRET(label); 
Parameters: 
XUU_PARAM    an XUU_PARAM structure. 
Description: 
The XUU$CLOSE service closes files (opened by XUU$OPEN) as specified in the 
XUU_PARAM passed to it. 
XUU$CLOSE expects the following fields to be assigned appropriate values in 
XUU_PARAM: 
o   FLAGS.CLOSE_ALL#, FLAGS.BASE#, FLAGS.UP_DATE#, FLAGS.INCLUDE# 
    and FLAGS.SOURCE_OUT# 
o   ALLOCATE$$ and RELEASE$$ 
o   ERROR_PROC$$ 
Error Conditions: 
When an error occurs during an XUU$CLOSE operation, XUU$CLOSE will: 
o   Close all DCBs opened by XUU 
o   Release any fast file I/O context areas 
o   ALTRETURN to the user with the following fields set in XUU_PARAM: 
        ERRCODE 
        One of: FLAGS.BASE#, FLAGS.UP_DATE#, FLAGS.INCLUDE#, FLAGS.XUU_ERR# 
        LEVEL 
        DCB# 
If XUU$CLOSE ALTRETURNs, any use of an XUU service other than calling XUU$OPEN 
with FLAGS.BASE# set will result in an error. 
00002
00003
00001
Format: 
CALL XUU$OPEN (XUU_PARAM) ALTRET(label); 
Parameters: 
XUU_PARAM    an XUU_PARAM structure. 
Description: 
The XUU$OPEN service opens files for use by the other XUU services. 
XUU$OPEN expects the following fields to be assigned appropriate values in 
XUU_PARAM: 
    FLAGS.BASE#, FLAGS.UP_DATE# and FLAGS.INCLUDE# 
    FLAGS.FAST_BASE#, FLAGS.FAST_UPDATE# and FLAGS.FAST_INCLUDE# 
    O.FPT_PTR$ 
    ALLOCATE$$ and RELEASE$$ 
    FLAGS.LU_FIRST# and FLAGS.LU_WHILE# 
    FLAGS.OPT_UI# 
    DCB# 
    ERROR_PROC$$ 
On a normal return, the following fields in XUU_PARAM will contain returned 
information which is possibly useful to the user: 
    LEVEL 
Error Conditions: 
When an error occurs during an XUU$OPEN operation, XUU$OPEN will: 
o   Close all DCBs opened by XUU 
o   Release any fast file I/O context areas 
o   ALTRETURN to the user with the following fields set in XUU_PARAM: 
        ERRCODE 
        One of: FLAGS.BASE#, FLAGS.UP_DATE#, FLAGS.INCLUDE#, 
                FLAGS.SO_ERR#, FLAGS.XUU_ERR# 
        LEVEL 
        DCB# 
If XUU$OPEN ALTRETURNs, any use of an XUU service other than calling XUU$OPEN 
with FLAGS.BASE# set will result in an error. 
An exception to this is an ALTRETURN on an OPEN to an INCLUDE file.  In this 
case, the INCLUDE file will not be opened but any other files currently open 
will not be affected. 
00002
00003
00001
Format: 
CALL XUU$READ (XUU_PARAM,buf_vec) ALTRET(label); 
Parameters: 
XUU_PARAM    an XUU_PARAM structure. 
buf_vec    specifies a vector framing a buffer where the next source record in 
sequence is to be returned.  buf_vec 
Description: 
The XUU$READ service reads a record into the user buffer from one of three 
possible input sources:  a base source file, an update file, one or more 
INCLUDE files.  XUU$READ maintains its place in all these files 
simultaneously:  it obtains records in sequence, substituting update records 
as necessary and reading records from referenced INCLUDE files as necessary. 
If requested by SOURCE_OUT=YES, the record read is written to M$SO, with the 
exception of INCLUDE file records.  If M$SO is not already open, it is opened 
with EXIST=NEWFILE which causes an existing file to be overwritten.  If M$SO 
is set to a keyed file, then the new source output file is created with EDIT 
format keys beginning with 1.000 and incremented by 1.000 with each write. 
Reaching end-of-file in an INCLUDE or update file is not considered an error 
(when it detects this condition, XUU$READ closes the file).  Reaching 
end-of-file for the base source file causes all open files to be closed and 
causes an alternate return. 
XUU$READ expects the following fields to be assigned appropriate values in 
XUU_PARAM: 
    ALLOCATE$$ and RELEASE$$ 
    FLAGS.BLANK_FILL# 
    FLAGS.SOURCE_OUT# 
    ERROR_PROC$$ 
On a normal return, the following fields in XUU_PARAM will contain returned 
information which is possibly useful to the user: 
    ARS 
    ASCII_KEY 
    FLAGS.BASE#, FLAGS.UP_DATE# and FLAGS.INCLUDE# 
    SEQ_REC#.BASE# and SEQ_REC#.UP_INCL# 
    LEVEL 
    FLAGS.KEY_REC# 
Error Conditions: 
When an error occurs during an XUU$READ operation, XUU$READ will either call 
the user specified error routine or will ALTRETURN. 
If the user specified an ERROR_PROC$$ in XUU_PARAM and the error is deemed to 
be recoverable by XUU, then XUU$READ will call the user's error routine.  When 
the routine returns, XUU$READ will assume that the user has reported the error 
condition and will continue to process as normally as possible.  Recoverable 
errors include; lost data (E$LD) from an M$READ and almost all plus record 
errors. 
If the user does not supply an error routine or the user's error routine 
ALTRETURNs to XUU or the error is considered to be a fatal one, then XUU$READ 
will: 
o   Close all DCBs opened by XUU 
o   Release any fast file I/O context areas 
o   ALTRETURN to the user with the following fields set in XUU_PARAM: 
        ERRCODE 
        One of: FLAGS.BASE#, FLAGS.UP_DATE#, FLAGS.INCLUDE#, 
                FLAGS.SO_ERR#, FLAGS.XUU_ERR# 
        LEVEL 
        DCB# 
        FLAGS.BAD_UPDATE# 
If XUU$READ ALTRETURNs, any use of an XUU service other than calling XUU$OPEN 
with FLAGS.BASE# set will result in an error. 
00002
00003
00001
XUU_PARAM is a macro invoked to build and initialize the parameter block 
passed to XUU$OPEN, XUU$READ and XUU$CLOSE. 
It should be noted that the XUU services use the fields in the parameter block 
extensively for returning values to the user.  This means that the XUU_PARAM 
block passed to an XUU service should not be defined in constant storage and 
initialized values should not be counted upon once the PARAM block has been 
passed to an XUU service.  For a description of each XUU_PARAM field, type: 
HELP (HOSTLIB) XUU_PARAM field 
where field is one of the following:  ALLOCATE$$, ARS, ASCII_KEY, 
C.INCL_ERRCODE, C.INCL_ERRCODE, C.SO_ERRCODE, DCB#, ERRCODE, ERROR_PROC$$, 
FLAGS.BAD_UPDATE#, FLAGS.BASE#, FLAGS.BLANK_FILL, FLAGS.CLOSE_ALL#, 
FLAGS.FAST_BASE#, FLAGS.FAST_INCLUDE#, FLAGS.FAST_UPDATE#, FLAGS.INCLUDE#, 
FLAGS.FAST_UPDATE#, FLAGS.INCLUDE#, FLAGS.KEY_REC#, FLAGS.LU_FIRST#, 
FLAGS.LU_WHILE#, FLAGS.OPT_UI#, FLAGS.SOURCE_OUT#, FLAGS.SO_ERR#, 
FLAGS.UP_DATE#, FLAGS.XUU_ERR#, LEVEL, O.FPT_PTR$, O.INCL_ERRCODE, RELEASE$$, 
RE_ASCII_KEY, SEQ_REC#.BASE#, SEQ_REC#.UP_INCL#, SI_ERRCODE, or UI_ERRCODE. 
    ALLOCATE$$ - EPTR 
    At a call to XUU$OPEN or XUU$READ, specifies a routine to be called to 
    allocate fast I/O context buffers.  This routine will be called as 
    follows: 
    CALL XUU_PARAM.ALLOCATE$$(ret_vect, alloc_type); 
    Where: 
    ret_vect    VECTOR ALIGNED which is to be filled in by the user's routine 
    with a VECTOR framing the allocated area. 
    alloc_type    a suggestion by XUU on the useful size of the area (see the 
    macro XUU$ALLOC_TYPES).  This is only a suggested size; XUU will use 
    whatever is framed by the returned vector as long as it is aligned on a 
    word boundary and frames a multiple of 1024 words. 
    If ALLOCATE$$ is not specified and if one or more of the flags: 
    FLAGS.FAST_BASE# 
    FLAGS.FAST_INCLUDE# 
    FLAGS.FAST_UPDATE# 
    is set, an error or IPR fault will result. 
    The ALLOCATE$$ field may be initialized in XUU_PARAM with 
    ALLOCATE=proc-name.  The default is NIL. 
    ARS - UBIN BYTE 
    On return from XUU$READ, contains the size of the returned record in 
    bytes. 
    ASCII_KEY - CHAR(10) 
    On return from XUU$READ, contains the ASCII text for the EDIT key or 
    sequential record number of the record read.  The format may be determined 
    from FLAGS.KEY_REC#. 
    C.INCL_ERRCODE - Standard CP-6 error code 
    This field exists for backward compatibility reasons only.  It contains 
    the errcode of an error encountered on an include file.  It is only valid 
    on an ALTRETURN from an XUU service and only when FLAGS.INCLUDE# is also 
    set.  New users should always use ERRCODE to find their error codes. 
    C.SO_ERRCODE - Standard CP-6 error code 
    This field exists for backward compatibility reasons only.  It contains 
    the errcode of an error encountered on the source output file.  It is only 
    valid on an ALTRETURN from an XUU service and only when FLAGS.SO_ERR# is 
    also set.  New users should always use ERRCODE to find their error codes. 
    DCB# - UBIN HALF 
    At a call to XUU$OPEN, specifies the number of the DCB through which to 
    list updates when LU_FIRST or LU_WHILE is set.  The specified DCB must be 
    initialized with any header image, page number, default VFC character, 
    etc.  The M$LO DCB is typically used for LU_FIRST. 
    The DCB# field may be initialized in the XUU_PARAM structure with 
    DCB=dcbnum. 
    On any altreturn condition involving an I/O error on a file, DCB# will be 
    set with the DCBNUM of the error so that the user may pass it on to 
    M$ERRMSG in order to get the fields placed properly in the message.  The 
    user should pass DCB# on to M$ERRMSG with ERRCODE if DCB#~=DCBADDR(NIL) 
    and FLAGS.BASE#, .UP_DATE#, .INCLUDE#, or .SO_ERR# are set. 
    ERRCODE - A standard CP-6 error code 
    This field is always set with a standard CP-6 error code when an XUU 
    service ALTRETURNS.  The source of the error is indicated by one of these 
    flags: 
    FLAGS.BASE# 
    FLAGS.UP_DATE# 
    FLAGS.INCLUDE# 
    FLAGS.SO_ERR# 
    FLAGS.XUU_ERR# 
    The DCB# field may be necessary, in addition to ERRCODE, in order to 
    report the complete error message. 
    ERROR_PROC$$ - EPTR 
    The ERROR_PROC$$ field specifies an optional routine to be called to allow 
    the user's program to report a recoverable error encountered during XUU 
    processing.  It will be called as follows: 
    CALL XUU_PARAM.ERROR_PROC$$(errcode [,buf_vect]) ALTRET(QUIT) 
    Where: 
    errcode    is an error code parameter in standard VLP_ERRCODE format 
    containing the error. 
    buf_vect    is an optional parameter which, if passed, is a vector framing 
    the record that caused the error. 
    If no ERROR_PROC is supplied to XUU, or the ERROR_PROC altreturns to XUU, 
    XUU will assume that the error is fatal. 
    FLAGS.BAD_UPDATE# - BIT(1) 
    On return from XUU$READ, if set, indicates that there currently is a bad 
    "plus" record in the buffer that the user may want to print. 
    FLAGS.BASE# - BIT(1) 
    At a call to XUU$OPEN, specifies that a base source file is to be opened 
    using M$SI. 
    On return from XUU$READ, is set if the record was read from the base 
    source file. 
    At a call to XUU$CLOSE, specifies that the base source file is to be 
    closed. 
    If FLAGS.BASE# is set on ALTRETURN from any XUU service, the ERRCODE field 
    contains an error that was encountered while operating on the base source 
    file. 
    The field is initialized in the XUU_PARAM block with BASE={YES|NO}.  The 
    default is NO. 
    FLAGS.BLANK_FILL - BIT(1) 
    At a call to XUU$READ, specifies that the buffer is to be blank-filled 
    from the end of the record read to the end of the buffer. 
    The field is initialized in the XUU_PARAM block with BLANK_FILL={YES|NO}. 
    The default is NO. 
    FLAGS.CLOSE_ALL# - BIT(1) 
    At a call to XUU$CLOSE, specifies that all open files used in the source 
    update process are to be closed. 
    The field is initialized in the XUU_PARAM block with CLOSE_ALL={YES|NO}. 
    The default is NO. 
    FLAGS.FAST_BASE# - BIT(1) 
    At a call to XUU$OPEN, if set, specifies that fast I/O is to be used for 
    the base source file, if possible.  If this flag is set, the fields 
    ALLOCATE$$ and RELEASE$$ must also be set.  Failure to do so will result 
    in an error or an IPR fault. 
    The field is initialized in the XUU_PARAM block with FAST_BASE={YES|NO}. 
    The default is NO. 
    FLAGS.FAST_INCLUDE# - BIT(1) 
    At a call to XUU$OPEN, if set, specifies that fast I/O is to be used for 
    the include files, if possible.  If this flag is set, the fields 
    ALLOCATE$$ and RELEASE$$ must also be set.  Failure to do so will result 
    in an error or an IPR fault. 
    The field is initialized in the XUU_PARAM block with 
    FAST_INCLUDE={YES|NO}.  The default is NO. 
    FLAGS.FAST_UPDATE# - BIT(1) 
    At a call to XUU$OPEN, if set, specifies that fast I/O is to be used for 
    the update file, if possible.  If this flag is set, the fields ALLOCATE$$ 
    and RELEASE$$ must also be set.  Failure to do so will result in an error 
    or an IPR fault. 
    The field is initialized in the XUU_PARAM block with FAST_UPDATE={YES|NO}. 
    The default is NO. 
    FLAGS.INCLUDE# - BIT(1) 
    At a call to XUU$OPEN, specifies that a DCB is to be dynamically acquired 
    and opened to the INCLUDE file.  The field XUU_PARAM.O.FPT_PTR$ must 
    contain a pointer to an FPT_OPEN for the INCLUDE file.  (The FPT must not 
    be in constant storage.)  Include files must be opened separately from the 
    source and update files.  Setting FLAGS.INCLUDE# and either FLAGS.BASE# or 
    FLAGS.UP_DATE# will result in an error. 
    On return from XUU$READ, is set if the record was read from an include 
    file. 
    At a call to XUU$CLOSE, specifies that the highest level include file is 
    to be closed. 
    If FLAGS.INCLUDE# is set on ALTRETURN from any XUU service, the ERRCODE 
    field contains an error that was encountered while operating on the 
    include file at level LEVEL. 
    The field is initialized in the XUU_PARAM block with INCLUDE={YES|NO}. 
    The default is NO. 
    FLAGS.KEY_REC# - BIT(1) 
    On return from XUU$READ, set if the returned record came from a keyed 
    file. 
    FLAGS.LU_FIRST# - BIT(1) 
    At a call to XUU$OPEN, specifies that a list of updates is to be made 
    through the DCB specified (via the parameter DCB) when M$UI is first 
    opened.  For CP-6 managed files, each record is read from M$UI, formatted 
    and written through the specified DCB until an end-of-file on M$UI is 
    encountered.  Then M$UI is positioned to the beginning of the file.  For 
    unmanaged files, an intermediate file must be created by XUU$OPEN to 
    produce the LU_FIRST type of LU listing.  A dynamic DCB will be acquired 
    for this purpose, and the M$UI records will be written to a scratch file 
    through this DCB. 
    The field is initialized in the XUU_PARAM block with LU_FIRST={YES|NO}. 
    The default is NO. 
    FLAGS.LU_WHILE# - BIT(1) 
    At a call to XUU$OPEN, specifies that a listing of updates is to be made 
    through the DCB specified (via the parameter DCB) concurrently with 
    processing of source/update records. 
    The processor must produce the source listing in an intermediate file to 
    avoid the update record images being inter-mixed with the source listing. 
    Most CP-6 language processors already do this, thus the LU_WHILE option is 
    meaningful to them. 
    Updates will be listed as they are used rather than as-read which means 
    that they will be listed in sync with the lines returned to the user of 
    XUU$READ. 
    The field is initialized in the XUU_PARAM block with LU_WHILE={YES|NO}. 
    The default is NO. 
    FLAGS.OPT_UI# - BIT(1) 
    At a call to XUU$OPEN, specifies that when UPDATE=YES is specified and the 
    update file does not exist, the error is to be ignored. 
    The field is initialized in the XUU_PARAM block with OPT_UI={YES|NO}.  The 
    default is NO. 
    FLAGS.SOURCE_OUT# - BIT(1) 
    At a call to XUU$READ, specifies that the source records, with the 
    exception of INCLUDE file records, are to be written through M$SO.  If 
    M$SO is not already open, it is opened with EXIST=NEWFILE which causes an 
    existing file to be overwritten.  If M$SO is set to a keyed file, then the 
    new source output file is created with EDIT format keys beginning with 
    1.000 and incremented by 1.000 with each write.  This flag, if used, 
    should be set for all calls to XUU$READ.  Failure to do so will result in 
    missing records in the source output file. 
    At a call to XUU$CLOSE, specifies that the source output file is to be 
    closed. 
    The field is initialized in the XUU_PARAM block with SOURCE_OUT={YES|NO}. 
    The default is NO. 
    FLAGS.SO_ERR# - BIT(1) 
    If FLAGS.SO_ERR# is set on ALTRETURN from any XUU service, the ERRCODE 
    field contains an error that was encountered while operating on the source 
    output file. 
    FLAGS.UP_DATE# - BIT(1) 
    At a call to XUU$OPEN, specifies that an update file is to be opened using 
    M$UI.  If both a base source file and an update file are to be opened, 
    they both must be opened on the same call to XUU$OPEN.  (Set both 
    FLAGS.BASE# and FLAGS.UP_DATE# for the call.) 
    On return from XUU$READ, is set if the record was read from the update 
    file. 
    At a call to XUU$CLOSE, specifies that the update file is to be closed. 
    If FLAGS.UP_DATE# is set on ALTRETURN from any XUU service, the ERRCODE 
    field contains an error that was encountered while operating on the update 
    file. 
    The field is initialized in the XUU_PARAM block with UPDATE={YES|NO}.  The 
    default is NO. 
    FLAGS.XUU_ERR# - BIT(1) 
    If FLAGS.XUU_ERR# is set on ALTRETURN from any XUU service, the ERRCODE 
    field contains an error that was not attributable to a specific file being 
    operated upon.  This will include plus card errors, XUU_PARAM errors and 
    internal errors. 
    LEVEL - UBIN BYTE 
    On return from XUU$OPEN, returns the nesting level of the include file if 
    an include file was just opened. 
    On return from XUU$READ, returns the nesting level of the include file 
    which the returned record was read from.  Valid only if FLAGS.INCLUDE# is 
    set. 
    FLAGS.LEVEL is set on any ALTRETURN from an XUU service which also has 
    FLAGS.INCLUDE# set. 
    O.FPT_PTR$ - PTR 
    At a call to XUU$OPEN, supplies XUU$OPEN with a pointer to an FPT_OPEN 
    containing all the information necessary to open an include file.  It is 
    required that the FPT be supplied when calling XUU$OPEN with 
    FLAGS.INCLUDE# set.  It is also required that the FPT not be in constant 
    storage. 
    O.INCL_ERRCODE - Standard CP-6 error code 
    This field exists for backward compatibility reasons only.  It contains 
    the errcode of an error encountered on an include file.  It is only valid 
    on an ALTRETURN from an XUU service and only when FLAGS.INCLUDE# is also 
    set.  New users should always use ERRCODE to find their error codes. 
    RELEASE$$ - EPTR 
    At a call to XUU$OPEN, XUU$READ or XUU$CLOSE, specifies a procedure to be 
    called to release fast I/O context buffers.  The routine will be called as 
    follows: 
    CALL XUU_PARAM.RELEASE$$(rel_vect); 
    Where: 
    rel_vect    a VECTOR ALIGNED which frames the area to be released. 
    The context areas will always be released in the exact opposite order that 
    they were allocated, thus the user may assume that the memory that XUU is 
    allocating and releasing is being treated as a stack. 
    If RELEASE$$ is not specified and one or more of the flags: 
    FLAGS.FAST_BASE# 
    FLAGS.FAST_INCLUDE# 
    FLAGS.FAST_UPDATE# 
    is set, an error or IPR fault will result. 
    The RELEASE$$ field in the XUU_PARAM structure may be initialized with 
    RELEASE=proc name.  The default is NIL. 
    RE_ASCII_KEY - Structure 
    RE_ASCII_KEY is an alternate definition of ASCII_KEY. 
    RE_ASCII_KEY.CHAR1_9 contains the text of the key. 
    RE_ASCII_KEY.CHAR(10) contains a 1 character code as follows: 
    Blank - from source file 
    *     - from update file 
     +     - from include file 
    SEQ_REC#.BASE# - UBIN(18) 
    On return from XUU$READ, returns the sequential record number last read 
    from the base source file. 
    SEQ_REC#.UP_INCL# - UBIN(18) 
    On return from XUU$READ, returns the sequential record number last read 
    from the update file if FLAGS.UP_DATE# is set or from an include file if 
    FLAGS.INCLUDE# is set. 
    SI_ERRCODE - Standard CP-6 error code 
    This field exists for backward compatibility reasons only.  It contains 
    the errcode of an error encountered on the base source file.  It is only 
    valid on an ALTRETURN from an XUU service and only when FLAGS.BASE# is 
    also set.  New users should always use ERRCODE to find their error codes. 
    UI_ERRCODE - Standard CP-6 error code 
    This field exists for backward compatibility reasons only.  It contains 
    the errcode of an error encountered on the update file.  It is only valid 
    on an ALTRETURN from an XUU service and only when FLAGS.UP_DATE# is also 
    set.  New users should always use ERRCODE to find their error codes. 
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
00029
00030
00031
00032
00033
The XUW services compare a wildcarded pattern string with an input string, and 
optionally produce an output string based on a wildcarded template.  The XUW 
services include: 
    X$WILDCMP  -  compares a pattern string to an input string. 
    X$WILDFMT  -  compares a pattern string to an input string.  A match 
                  produces an output string based on the template string. 
The wildcard character is assumed to be the question mark symbol (?)  unless 
otherwise specified (by the WILD_CHAR parameter). 
The XUW structure may be generated by %INCLUDing file XUW_MACRO_C and invoking 
%XUW_WILDCARD.  For a description of each parameter type: 
HELP (HOSTLIB) XUW_WILDCARD param 
where param is one of the following:  CONTAINS, ERROR, OUTPUT, OUTPUT_LEN, or 
WILD_CHAR. 
CONTAINS = {YES|NO}    specifies, if YES, that this option will search for the 
wildcarded pattern anywhere in the input string.  If CONTAINS = NO, the input 
string must exactly match the pattern with no additional characters to the 
right or left.  For example: 
    INPUT = 'I am a Duckie!' 
    PATTERN = 'Duck?' 
The PATTERN will match INPUT if CONTAINS = YES.  The default is NO. 
ERROR - VALUE-BIT(36)    contains the result of the string match/format 
operation in standard CP-6 error code form.  The field ERROR.ERR# reflects the 
results of the XUW service. 
INPUT = VARIABLE    locates the input string to be compared.  The input string 
may not exceed 511 bytes or be zero.  The default is NIL. 
OUTPUT = VARIABLE    locates the output string produced by X$WILDFMT. 
OUTPUT_LEN - VALUE-DEC(0-?)    specifies the length (UBIN WORD) of the output 
string produced by X$WILDFMT. 
PATTERN = VARIABLE    locates the pattern to be compared with the input 
string.  The pattern includes one or more wildcard characters.  This string 
may not be zero or exceed 511 bytes.  The default is NIL. 
TEMPLATE = VARIABLE    specifies a wildcarded string used to format the output 
string.  The template string may not be zero or exceed 511 bytes.  The default 
is NIL. 
WILD_CHAR = VALUE-CHAR(1)    specifies the wildcard character.  The default is 
?. 
The XUX services facilitate reading and parsing of a processor invocation 
command.  The services can be used in two ways: 
  o  The command line options are parsed using X$PARSE and a data structure is 
     returned to the caller indicating which of the standard command line 
     options were found, as well as any non-standard options found.  This 
     function is performed by calling the XUX$COMMON_OPTIONS service. 
  o  The command lines found are returned to the calling routine. 
     Continuation lines are automatically retrieved.  No parsing is performed. 
     This function is performed by calling the XUX$GETLINE service for each 
     line.  The XUX$CLEANUP service must be called after reading a command. 
For a brief description of each service, type 
!HELP (HOSTLIB) XUX service 
service may be XUX$CLEANUP, XUX$COMMON_OPTIONS, or XUX$GETLINE. 
  Service   Description 
  XUX$CLEANUP 
            Performs internal housekeeping; required after a complete command 
            has been read via calls to XUX$GETLINE. 
  XUX$COMMON_OPTIONS 
            Retrieves and parses a complete processor invocation command.  Can 
            parse the standard form of the processor invocation, and, with 
            user-supplied parse nodes, can parse non-standard processor 
            invocations. 
  XUX$GETLINE 
            Facilitates reading command line options, but performs no parsing. 
00001
00002
00003
This macro defines a data item that contains the numbers of the BC units that 
are specified on the command line, if any.  The item is an array from 0 to 
%XUX$MAX_BC_UNITS.  Note that this is one element more than the number needed. 
It is defined this way for ease of access, so that the user may use an indexed 
loop through the structure that starts at 1 and ends at XUX$STD_OPTIONS.BC. 
XUX$BC_UNIT - This array contains the numbers of the BC units that are 
    specified on the command line.  These numbers are only meaningful if 
    XUX$STD_OPTIONS.BC is greater than zero.  The numbers in the array are 
    sorted. 
Format: 
CALL XUX$CLEANUP; 
Parameters: 
None 
Description: 
The XUX$CLEANUP service should be called after a complete command has been 
read via calls to XUX$GETLINE.  This service makes it appear that XUX$GETLINE 
was never called.  This is useful if the command line needs to be re-read, for 
instance. 
Error Conditions: 
None. 
00002
00003
00001
Format: 
CALL XUX$COMMON_OPTIONS (name) ALTRET (label); 
Parameters: 
name    can be generated by invoking the macro %XUX$PARAM.  That structure 
points to a number of other parameter blocks which may be generated by the 
following macros:  XUX$LEGAL_OPTIONS, XUX$STD_OPTIONS, XUX$BC_UNIT, 
XUX$SRCH_LIST. 
Description: 
The XUX$COMMON_OPTIONS service parses the processor invocation, based on 
various parameters that the caller supplies.  These parameters include which 
(if any) of the standard options are to be considered legal.  Other parameters 
are pointers to the parse results block, the list of accounts to search (if 
this is legal), the BC compile unit numbers, and the user's non-standard node 
handler, if supplied. 
On return from XUX$COMMON_OPTIONS, the XUX$STD_OPTIONS block bits are set 
corresponding to the options found on the processor invocation.  If no options 
are specified, then the CP-6 system defaults of UI, LS, OU, BC(ALL), MSCHEMA, 
and NWARN are set.  The UI, LS, and OU options are also set by examining the 
JIT flags to determine if anything was present in the UI, OU and/or LS DCB 
positions.  In addition, MSCHEMA will be forced (and will override 
user-specified NSCHEMA) if any of the following are specified:  DMAP, MDMAP, 
PMAP, MPMAP. 
If non-standard options are to be used, then the proper bit in 
XUX$LEGAL_OPTIONS must be set indicating this, and the user-supplied nodes 
must be linked together with the program.  The user nodes should be produced 
using the PARTRGE processor to produce an object unit.  (Type !HELP (PARTRGE) 
for information on PARTRGE.)  The user sets XUX$PARAM.USER_NODES$ to 
ADDR(his_nodes).  When any non-standard option is encountered, the user 
routine pointed to by XUX$PARAM.USER_ROUTINE$$ is entered with a pointer to 
the head of the non-standard node, and with a BIT(1) variable as a parameter. 
The user's routine should then process this node and return, or ALTRETurn if 
the command cannot be processed.  The BIT(1) variable should be set to '1'B if 
the user's routine desires further processing by XUX$COMMON_OPTIONS to cease 
and ALTRETurn to occur immediately, or '0'B if processing is to continue. 
When the variable is set to '1'B, XUX$COMMON_OPTIONS takes the ALTRETurn with 
the XUX$PARAM.ERROR# flag set, and XUX$ERROR_CODE indicates that an internal 
error occurred. 
Error Conditions: 
If the XUX$COMMON_OPTIONS service encounters any errors while parsing, one of 
several things may occur.  If the user specified either DCB1 or DCB2 or both 
on the XUX$PARAM macro, then if the error is a user error (such as a syntax 
error), XUX$COMMON_OPTIONS writes an appropriate error message through the 
DCB(s) and attempts to continue processing.  If the error is internal (such as 
specifying that BC is a valid option but failing to provide an XUX$BC_UNIT 
structure) or if DCBs are specified for neither DCB1 nor DCB2, the 
XUX$COMMON_OPTIONS service ALTRETurns immediately upon encountering the error, 
with the error code in XUX$PARAM.ERROR_CODE and with XUX$PARAM.ERROR# set to 
'1'B indicating unprocessed errors. 
It is the calling program's responsibility to handle and report these errors. 
Note that in the case where no DCBs are specified and a user error occurs, the 
error code returned may be of little use since there is no way to supply the 
error message substitution fields, nor is there any way to determine exactly 
where the error occurred, since continuation lines may have been involved. 
If any errors occur at all, the XUX$COMMON_OPTIONS service ALTRETurns after 
all processing is complete with the error code in XUX$PARAM.ERROR_CODE 
regardless of whether DCB1/DCB2 are used. 
00002
00003
00001
Format: 
CALL XUX$GETLINE (name) ALTRET (label); 
Parameters: 
name    can be generated by invoking the macro %XUX$PARAM_NO_PARSE. 
Description: 
The XUX$GETLINE service retrieves a command line.  XUX$GETLINE can be called 
and re-called to obtain a multi-line command; it obtains continuation lines 
from the *CONTINUATION_COMMANDS file, if they are present.  The caller may 
choose to receive the entire command by default, or only the portion from 
B$JIT.CCDISP on (i.e., starting at the processor options) by setting 
XUX$PARAM_NO_PARSE.DISP_ONLY. 
After a call to XUX$GETLINE, either the buffer framed by 
XUX$PARAM_NO_PARSE.BUFFER_ contains a line of the command with the length set 
in CMD_LEN, or XUX$PARAM_NO_PARSE.CMD_COMPLETE is set indicating that there is 
no command line left to return.  (It is illegal to call XUX$GETLINE after 
CMD_COMPLETE is set.  The user must first call XUX$CLEANUP before program 
termination or before attempting to re-read or re-parse the command.) 
Error Conditions: 
If an error occurs, XUX$GETLINE ALTRETurns with the error code set in 
XUX$PARAM_NO_PARSE.ERROR_CODE. 
00002
00003
00001
This macro defines the structure that tells which of the standard options are 
legal on the command line to be parsed. 
The structure defined has one bit for each of the legal standard options, and 
one extra bit that may be set to allow non-standard options.  The default is 
that all standard CP-6 options are allowed, and no non-standard options are 
allowed.  Note that setting the bit associated with the option merely allows 
that option (or any of its permutations [e.g., XREF, MXREF, or NXREF]) to be 
specified on the command line, and does not actually set that option in the 
XUX$STD_OPTIONS structure.  To access any data item, use the name followed by 
a # (e.g., XUX$LEGAL_OPTIONS.LS# ). 
    BC = {YES|NO}    if YES, allows the Batch Compile (BC) option to be 
    specified.  The default is YES. 
    DCB_LS = {YES|NO}    if YES, allows a fid in the LS position on the 
    command line.  The default is YES. 
    DCB_OU = {YES|NO}    if YES, allows a fid in the OU position on the 
    command line.  The default is YES. 
    DCB_UI = {YES|NO}    if YES, allows a fid in the UI position on the 
    command line.  The default is YES. 
    DMAP = {YES|NO}    if YES, allows the Data Map(DM), No Data Map (NDM) or 
    Mini Data Map (MDM) option to be specified.  The default is YES. 
    LO = {YES|NO}    if YES, allows the List Object (LO) option or No List 
    Object (NLO) option to be specified.  The default is YES. 
    LS = {YES|NO}    if YES, allows the List Source (LS) option or No List 
    Source (NLS) option to be specified.  The default is YES. 
    NSTD = {YES|NO}    if YES, allows Non-standard options to be specified. 
    The default is NO. 
    OU = {YES|NO}    If YES, allows the Object Unit (OU) generation or No 
    Object Unit generation (NOU) option to be specified.  The default is YES. 
    PMAP = {YES|NO}    if YES, allows the Procedure MAP (PMAP), No Procedure 
    MAP (NPMAP), or Mini Procedure MAP (MPMAP) to be specified.  The default 
    is YES. 
    SCHEMA = {YES|NO}    if YES, allows the Schema (SC), No Schema (NSCHEMA) 
    or Mini Schema (MSCHEMA) option to be specified.  The default is YES. 
    SO = {YES|NO}    if YES, allows the Source Output (SO) option or No Source 
    Output (NSO) option to be specified.  The default is YES. 
    SRCH = {YES|NO}    if YES, allows the Search (SRCH) option to be 
    specified.  The default is YES. 
    UI = {YES|NO}    if YES, allows the Update Input (UI) option or No Update 
    Input (NUI) option to be specified.  The default is YES. 
    UREF = {YES|NO}    if YES, allows the Unreferenced Data listing option 
    (UREF) to be specified.  The default is YES. 
    WARN = {YES|NO}    if YES, allows the Warning message (WARN) or No Warning 
    message (NWARN) option to be specified.  The default is YES. 
    XREF = {YES|NO}    if YES, allows the cross reference (XREF), Mini cross 
    reference (MXREF), or No cross reference (NXREF) option to be specified. 
    The default is YES. 
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
This macro generates a data structure that is to be passed to the 
XUX$COMMON_OPTIONS service.  The data structure generated is largely a block 
of pointers to other data structures that are used by XUX$COMMON_OPTIONS. 
    BC_UNIT = VARIABLE    is a pointer to the XUX$BC_UNIT structure. 
    ADDR(XUX$BC_UNIT) is used to initialize BC_UNIT$. 
    DCB1 = DCBNAME    is a UBIN HALF variable that contains the DCBNUM of the 
    first DCB through which any error messages are written by 
    XUX$COMMON_OPTIONS.  If no DCB is specified for either DCB1 or DCB2, then 
    any errors cause XUX$COMMON_OPTIONS to ALTRETurn with the error code in 
    XUX$PARAM.ERROR_CODE.  This field can be accessed as DCB1#. 
    DCB2 = DCBNAME    is the second DCB through which error messages are 
    written. See DCB1 for more information.  This field can be accessed as 
    DCB2#. 
    ERROR# - is a BIT(1) variable that is set to '1'B when a fatal error has 
    occured.  This happens if no DCBs are specified for error message 
    handling, an internal (non-user) error occured, or a syntax error was 
    encountered. 
    ERROR_CODE - contains an error code when an error occured that has not 
    already been diagnosed.  The error code is in the standard CP-6 format 
    that is generated by VLP_ERRCODE.  The error message corresponding to this 
    code may be found in :XUERRMSG.:SYS 
    LEGAL_OPTIONS = VARIABLE    is a pointer to the XUX$LEGAL_OPTIONS 
    structure.  ADDR(XUX$LEGAL_OPTIONS) is used to initialize LEGAL_OPTIONS$. 
    SRCH_LIST = VARIABLE    is a pointer to the XUX$SRCH_LIST structure. 
    ADDR(XUX$SRCH_LIST) is used to initialize SRCH_LIST$. 
    STD_OPTIONS = VARIABLE    is a pointer to the XUX$STD_OPTIONS structure. 
    ADDR(XUX$STD_OPTIONS) is used to initialize STD_OPTIONS$. 
    USER_NODES$ = VARIABLE    is a pointer to the user's non-standard nodes 
    (if any).  The default (ADDR(NIL)) may be used if no non-standard nodes 
    are used. 
    USER_ROUTINE = ENTRY    points to a user-supplied routine that is to be 
    called when XUX$COMMON_OPTIONS encounters any non-standard options while 
    processing the command line.  ENTADDR(NIL) is used to initialize 
    USER_ROUTINE$$ if no user routine is specified.  This routine should have 
    two parameters, a pointer to the head node of the non-standard option that 
    was found, and a BIT(1) variable.  The BIT(1) variable should be set to 
    '1'B if the user's routine desires further processing by 
    XUX$COMMON_OPTIONS to cease and ALTRETurn to occur immediately, or '0'B if 
    processing is to continue.  A user routine must be present if any 
    non-standard nodes are used. 
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
This macro defines the data structure to be used when no parsing is to be done 
to the command line.  This is used when the actual text of the command line is 
needed. 
The data structure defined is passed as a parameter to XUX$GETLINE which 
returns the command line text.  An indication is provided whether or not the 
entire command is present, as it may be continued. 
    BUFFER = VARIABLE    is a vector to a user provided buffer.  The buffer 
    contains the command text upon return from the call.  VECTOR(BUFFER) is 
    used to initialize BUFFER_.  A buffer of 256 characters is recommended. 
    CMD_COMPLETE - when set, this bit indicates that there is no more command 
    line left to return.  Once this bit has been set by XUX$GETLINE, it is 
    illegal to call XUX$GETLINE again.  Also, a call to XUX$CLEANUP should be 
    performed before the end of the program. 
    CMD_LEN - contains the length of the text returned in the buffer framed by 
    BUFFER_. 
    DISP_ONLY = {YES|NO}    if set, indicates that only the portion of the 
    command line that starts at B$JIT.CCDISP is returned.  If DISP_ONLY = NO, 
    then the entire command line is returned to the user.  This item may be 
    accessed as DISP_ONLY#.  The default is YES. 
    ERROR_CODE - contains an error code if the call to XUX$GETLINE 
    ALTRETURNed.  The error code is in the standard CP-6 error code format 
    generated by VLP_ERROR.  The error message corresponding to this code may 
    be found in :XUERRMSG.:SYS. 
00001
00002
00003
00004
00005
This macro defines a structure to contain the account names specified on the 
SRCH option.  The default values of .:LIBRARY and the user's current directory 
are always present, unless the SRCH option is made illegal by setting 
XUX$LEGAL_OPTIONS.SRCH to NO. 
This structure is an array of information about the account(s) that were 
specified on the SRCH option of the command line.  The current limit is ten 
account specifications.  Since two of those are used all the time for 
.:LIBRARY and the current directory account, eight are available for user 
specification. 
An alternate use of the XUX$SRCH_LIST structure is to generate a structure for 
a single FID. 
    ACCT - is the account name.  The size of this field is specified by the 
    ACCT_SIZE parameter which defaults to 8. 
    ACCT_LIST (0:n) - is the list of account names (ACCT) and possibly 
    attributes (ASN, PASS, RES, SN, WSN) that have been specified.  For 
    example, the account name is stored in XUX$SRCH_LIST.ACCT_LIST.ACCT(n). 
    The number of items in the list is specified by the SRCH_ACCTS parameter 
    which defaults to 10. 
    ASN - specifies file organization (see M$OPEN in the Host Monitor Services 
    Reference Manual, CE74). 
    FID_ONLY = {YES|NO}    if set, specifies that a structure containing only 
    a single instance of FID information (ACCT, ASN, PASS, RES, SN, WSN) is 
    generated.  For example, the account name is stored in XUX$SRCH.ACCT.  If 
    FID_ONLY = YES, the fields NUM and RCVD are not generated; the array 
    ACCT_LIST is also not generated. 
    NUM - contains the number of accounts contained within the SRCH structure. 
    This number can range from two to the maximum number of possible accounts, 
    currently ten. 
    PASS - is the password that was specified, if any. 
    RCVD - contains the number of SRCH accounts that were actually specified 
    on the command line.  This may be less than NUM if the current account 
    and/or .:LIBRARY were specified in the SRCH list. 
    RES - is the RES of the file (see M$OPEN). 
    SN - is the serial number of a tape. 
    WSN - is the Workstation Name specified. 
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
This macro defines a structure that tells the user program which of the 
standard options were found on the command line.  If no options are specified, 
then the CP-6 system defaults of UI, LS, OU, BC(ALL), MSCHEMA and NWARN are 
set.  The UI, LS and OU options are also set by examining the JIT flags to 
determine if anything was present in the UI, OU and/or LS DCB positions. 
Each of the following items, when set, indicates that the corresponding option 
was either found on the command line, or was a default. The non-BIT(1) items 
are set as indicated.  Note that an item can only be set if the corresponding 
bit in XUX$LEGAL_OPTIONS is set.  See the CP-6 System Programmer Guide (CE62), 
Compilers and Language Utilities, for a description of the CP-6 standard 
options. 
    BC - indicates how many (if any) compile units are specified on the 
    command line, and is always a value from 1 to 8, unless BC(ALL) is 
    specified, in which case the value is zero.  An equate (%XUX$ALL) may be 
    used to test for the BC(ALL) case.  The actual BC unit numbers may be 
    found in XUX$BC_UNIT, which is an array (0:8) that is specified on the 
    BC_UNIT parameter of the XUX$PARAM macro.  If BC is not specified on the 
    command line then the default value is %XUX$ALL, indicating BC(ALL).  If 
    BC is greater than 0, then each element of XUX$BC_UNIT (from 1 to BC) 
    contains a value from 1 to 131071 representing the BC unit that was 
    specified. The value of element zero of XUX$BC_UNIT is not significant. 
    DMAP - contains four bits - STATIC#, AUTO#, SYMREF#, and BASED#, each 
    corresponding to the type of DMAP that was requested.  If no DMAP was 
    requested, then the default value for all of these bits is '0'B.  No 
    translation of this field is needed to pass it to UNGMAP for generation of 
    the listings. 
    LO - contains two bits - CODE and DATA.  If LO alone is specified on the 
    command line, then both of these bits are set; otherwise LO(CODE) sets the 
    CODE bit, and LO(DATA) sets the DATA bit.  The default is that both bits 
    are set to '0'B.  No translation of this field is needed to pass it to 
    UNGMAP for generation of this listing. 
    LS - indicates that the LS option was specified or assumed by default. 
    The default is '1'B. 
    MDMAP - contains four bits - STATIC#, AUTO#, SYMREF#, and BASED#, each 
    corresponding to the type of MDMAP that was requested.  If no MDMAP was 
    requested, then the default value for all of these bits is '0'B.  No 
    translation of this field is needed to pass it to UNGMAP for generation of 
    this listing. 
    NSTD - indicates that non-standard options are specified on the command 
    line. The default is '0'B. 
    OPTUI - indicates the the OPTUI option is specified on the command line, 
    meaning that if the UI file is present, that it is to be used, otherwise 
    no error message is produced. If specified the UI bit is also set.  The 
    default is '0'B. 
    OU - indicates that the OU option was specified or assumed by default. 
    The default is '1'B. 
    PMAP - contains two bits, FULL and MINI indicating what type of PMAP has 
    been requested.  The default for both bits is '0'B.  No translation of 
    this field is needed to pass it to UNGMAP for generation of this listing. 
    SCHEMA - indicates that SCHEMA is specified on the command line.  Three 
    equates are provided to test the value, %XUX$NONE for NSCHEMA, %XUX$FULL 
    for SCHEMA, and %XUX$MINI for MSCHEMA. The default is %XUX$MINI. 
    SO - indicates that the SO option is specified on the command line. The 
    default is '0'B. 
    SRCH - indicates that a SRCH list is specified on the command line.  If 
    set, it indicates that the list of accounts specified may be found in the 
    structure XUX$SRCH_LIST.  The default is '1'B with .:LIBRARY and the 
    user's current directory specified in that order.  Note that this bit is 
    never set to NO unless the user specifies that XUX$LEGAL_OPTIONS.SRCH is 
    NO. 
    UI - indicates that the UI option is specified on the command line or, if 
    using the standard invocation syntax, a filename is specified in the UI 
    position on the command line.  The default is '0'B. 
    UREF - indicates that UREF is specified on the command line.  Three 
    equates are provided to test the value, %XUX$NONE for NUREF, %XUX$FULL for 
    UREF, and %XUX$MINI for MUREF. The default is %XUX$NONE. 
    WARN - indicates that the WARN option is specified on the command line. 
    The default is '0'B. 
    XREF - indicates that XREF is specified on the command line.  Three 
    equates are provided to test the value, %XUX$NONE for NXREF, %XUX$FULL for 
    XREF, and %XUX$MINI for MXREF. The default is %XUX$NONE. 
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
