6Edit is entered from IBEX using the following command: 
    !{6E[DIT]|6B[UILD]|6X} [fid] [(command list[)]] 
Parameters: 
fid    identifies the initial file to be edited. 
command list    specifies one or more initial commands.  If a READ command is 
included in the command list, the trailing right parenthesis must be omitted. 
Description: 
Note that the context file is read and executed before the IBEX command line's 
command list is executed.  This means, for example, that synonyms defined in 
the context file can be used in the command list. 
If a command list includes more than one command, the commands must be 
separated by semicolons (;). 
When started, 6Edit displays a greeting: 
    6Edit A04 Here. 
There is a delay while 6Edit reads the context file appropriate for this 
session, based on your terminal profile name and your current file management 
(DIR) account.  If fid is included in the IBEX command line, 6Edit displays it 
after clearing the terminal screen.  If fid is omitted from the IBEX command 
line, 6Edit prompts for a command.  When waiting for a command to be entered, 
6Edit displays an asterisk (*) on the terminal screen.  For more help on 
6Edit, enter: 
or  HELP (6EDIT) INPUT_EDITING 
or  HELP (6EDIT) COMMAND_LINES 
Examples: 
    !6EDIT DAILY_JOB 
or 
    !6EDIT (FILE DAILY_JOB 
or 
    !6E DAILY JOB 
starts 6Edit, editing the file DAILY_JOB, the beginning of which is displayed 
in the editing window. 
    !6EDIT (NEW FILE WEEKLY_JOB.MYACCT 
or 
    !6BUILD WEEKLY_JOB.MYACCT 
starts 6Edit, creating a new file named "WEEKLY_JOB" in account "MYACCT".  The 
editing window is initially empty, ready for you to enter text into the file. 
    !6EDIT (PROTECT FILE YEAR_END_JOB) 
or 
    !6X YEAR_END_JOB 
starts 6Edit, editing the file YEAR_END_JOB.  This file is "protected", that 
is, you cannot make changes to the file, you can only view the file in the 
editing window. 
    !6EDIT DB_UPDATES (28.4) 
starts 6Edit, editing file DB_UPDATES.  The command list specifies that 6Edit 
is to put the cursor on the record with key 28.4.  Instead of displaying the 
beginning of the file, 6Edit displays the records near record 28.4 in the 
editing window.  or  HELP (6EDIT) DCBS 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
The $COMMENT identifier is used to denote commentary in command lines.  The 
quotation mark (") is the initial $COMMENT identifier. 
When the $COMMENT identifier appears in a command line outside of a quoted 
string, 6Edit ignores the following text, until the next appearance of the 
$COMMENT identifier or the end of the command line.  This allows you to append 
commentary to command lines by separating the commentary from the actual 
command(s) with the $COMMENT identifier. 
Note that the $COMMENT identifier is not recognized inside quoted literal 
strings. 
Example: 
CASE EQ OFF  "This is commentary 
is not concluded by a quotation mark, because the commentary occurs at the end 
of the command line. 
LOCATION CHAPTER_1 IS "Definition follows:" BO CURRENT THRU  '.brp' 
differs from the former command line.  Here, the commentary occurs in the 
middle of the command line, and is therefore enclosed by quotation marks. 
To change the identifier which invokes $COMMENT functions, you assign a 
different character value to the $COMMENT predefined name.  The characters 
assigned to the $COMMENT name must reside in the following set: 
    !   "   #   $   %   &   *   +   -   @   :   < 
    =   >   /   [   \   ]   ^   _   '   {   |   }   ~ 
However, the characters which represent the current value of the $CONTROL 
predefined name (initially %) cannot be used in the value of the $COMMENT 
predefined name. 
00001
The $CONTROL identifier is used to invoke several functions which are called 
"$CONTROL functions".  Initially, the value of $CONTROL is the percent sign 
(%). 
The character following the $CONTROL identifier is called the 
"function identifier". 
Some of the $CONTROL functions require an operand to be included along with 
the function identifier.  Normally, a $CONTROL function is specified as 
follows: 
    $CONTROL_identifier  function_identifier 
These characters are to be entered together; there is no space between them. 
Parameters: 
$CONTROL_identifier    represents one or two characters designating the 
current value of the $CONTROL predefined name. 
function_identifier    specifies the function 6Edit is to perform. 
For example, assume that the $CONTROL identifier is %: 
    %%    invokes the $CONTROL-Literal function 
    %R    invokes the $CONTROL-Record function 
    %V    invokes the $CONTROL-Value function 
Note:  $CONTROL functions used in EQUALS commands are not interpreted when 
assigned, but only when the resulting variable is used in a different command. 
Certain $CONTROL functions require one or two operands along with the function 
identifier.  Enclose both in parentheses following the function identifier: 
    $CONTROL_identifier function_identifier ([operand]) 
For example: 
    %V()       invokes the $CONTROL-Value function with no operands 
    %V(23)     invokes the $CONTROL-Value function with one operand: 23 
    %V(23,255) invokes the $CONTROL-Value function with two operands: 
               23 and 255 
To change the identifier which invokes $CONTROL functions, you assign a 
different character value to the $CONTROL predefined name.  The characters 
assigned to the $CONTROL name must reside in the following set: 
    !   "   #   $   %   &   *   +   -   @   :   < 
    =   >   /   [   \   ]   ^   _   `   {   |   }   ~ 
However, the characters which represent the current value of the $COMMENT 
predefined name (initially "), cannot be used in the value of the $CONTROL 
predefined name. 
For help on the $CONTROL functions, enter: 
    ??          (to view all $CONTROL functions) 
or  HELP (6EDIT) $CONTROL_LITERAL 
or  HELP (6EDIT) $CONTROL_RECORD 
or  HELP (6EDIT) $CONTROL_VALUE 
or  HELP (6EDIT) $CONTROL_VALUE_PATT 
or  HELP (6EDIT) $CONTROL_QUESTION_PATT 
or  HELP (6EDIT) PATTERN_STRING   (for $CONTROL used in pattern strings) 
00001
Function Identifier:  B 
This pattern function should appear only once in a pattern string.  It 
specifies what point in the matching file data is to be considered the 
beginning of the match.  If $CONTROL-Beginning of Match is not included in a 
pattern string, the first character of the matching file data is considered 
the beginning of the match. 
For example, assuming the $CONTROL character is percent (%): 
COPY STRING 'memo' OVER REPEAT SELECT PATTERN 'my %Breport' 
searches for the string 'my report' in the file.  However, the beginning of 
the match is the "r" of "report":  the block found and replaced by this 
command will be the word "report", but only if it appears after the word "my 
". 
Function Identifier:  E 
This pattern function should appear only once in a pattern string.  It 
specifies what point in the matching file data is to be considered the end of 
the match.  If $CONTROL-End of Match is not included in a pattern string, the 
character immediately following the matching file data is considered the end 
of the match. 
For example, assuming the $CONTROL character is percent (%): 
CO STRING 'memo' OVER REPEAT SELECT PATTERN 'report%Es from this office' 
searches for the string 'reports from this office' in the file.  However, the 
end of the match is the "s" of "reports":  the block replaced by this command 
will be the word "report", but only if it appears before the string "s from 
this office". 
Function Identifier:  the $CONTROL identifier itself. 
This $CONTROL function allows you to include the $CONTROL identifier itself in 
quoted strings.  6Edit recognizes two adjacent occurrences of the $CONTROL 
identifier as representing a single $CONTROL identifier; no other lexical 
function is performed. 
Example: 
COPY STRING '48%% are qualified' AFTER HERE 
inserts the string "48% are qualified" into the file. 
00001
Function Identifier:  ?  (question mark). 
No parameters may be included in the $CONTROL-Question function. 
The $CONTROL-Question function specifies that a sequence of any number of 
characters in the enclosing block (including 0) is considered a match. 
For example, consider the following pattern string, assuming the $CONTROL 
character is the percent symbol (%). 
    abcde%?fghijkl 
This pattern string matches the following strings in the enclosing block: 
    abcde1234fghijkl 
    abcde'tfghijkl 
    abcdefghijkl 
    abcde  fghijkl 
Multiple instances of the $CONTROL-Question function are permitted.  For 
example, 
     COPY STRING 'from%W(2)any%W(1)to' OVER 'to%?any%?from' 
substitutes the COPY string for the OVER string for each string that matches 
the pattern of the OVER string, retaining the portions of the pattern string 
represent by %?s.  Up to 10 instances of %W are permitted in a COPY or MOVE 
string; any number of %?s are permitted in the pattern string. 
Function Identifier:  R 
The $CONTROL-Record function represents an "end-of-record boundary." 
This function may be invoked in quoted strings.  The $CONTROL-Record function 
is the only way to represent an end-of-record boundary in quoted strings. 
Example: 
COPY STRING 'The quick brown fox%Rjumped over the lazy dog%R' AFTER 10 
inserts two records after record 10.0 in the file being edited.  The first 
record contains "The quick brown fox"; the second record contains 
"jumped over the lazy dog". 
COPY STRING 'whenever available ' AFTER 10 SELECT 'respond ' 
inserts two words into record 10.0 after the word "respond".  Note the absence 
of any $CONTROL-Record function:  the quoted string does not represent a 
record, but just a string of characters.  This command creates no new records. 
Record 10.0 is simply lengthened. 
 We would appreciate an itemized inventory sheet from your 
                      ----------- 
 department.  You can | respond | stock 
                      ----------- 
 arrives from the Omaha branch.  We will expect a complete 
 list, signed and dated by the area manager, at that time. 
COPY STRING 'whenever available%R' AFTER 10 SELECT 'respond ' 
inserts two words into record 10.0 after the word "respond".  Also, because 
the $CONTROL-Record function is included in the quoted string, a new record is 
inserted after record 10.0. 
CO ST 'whenever available ' AF 10 SE 'respond ' 
 We would appreciate an itemized inventory sheet from your 
                              ---------------------- 
 department.  You can respond | whenever available | stock 
                              ---------------------- 
 arrives from the Omaha branch.  We will expect a complete 
 list, signed and dated by the area manager, at that time. 
CO ST 'whenever available%R' AF 10 SE 'respond ' 
 We would appreciate an itemized inventory sheet from your 
                      ------------------------------ 
 department.  You can | respond whenever available | 
                      ------------------------------ 
 stock 
 arrives from the Omaha branch.  We will expect a complete 
 list, signed and dated by the area manager, at that time. 
00001
Function Identifier:  V 
Parameters: 
value    is a decimal number between 0 and 511, inclusive. 
The $CONTROL-Value function allows you to enter any 9-bit byte value in quoted 
strings. 
This function requires an operand following the function identifier. 
For example, assuming that $CONTROL is %, to enter a quoted string which 
contains a single byte with a value of 23, you would type: 
    '%V(23)' 
Example: 
ESC EQ '%V(27)' 
defines a name, ESC, with the value of the escape character.  The number 27 is 
the decimal ASCII code for the Escape character. 
KEYIN '%V(27)A' IS 'harbinger of glad tidings' 
redefines the terminal key sequence Escape A.  Hereafter, whenever <ESC> <A> 
is typed at the terminal keyboard, it appears as the phrase "harbinger of glad 
tidings". 
00002
00001
Function Identifier:  V 
If the $CONTROL-Value function appears in the pattern string, it may include 
one or two parameters.  Assuming the $CONTROL character is the percent symbol 
(%): 
o   '%V()' - If no parameters are included, a character in the enclosing block 
    whose ASCII code is zero is considered a match.  This is identical to 
    %V(0). 
o   '%V(m)' - If one parameter is included, it must be a decimal number; a 
    character in the enclosing block whose ASCII code equals the number is 
    considered a match. 
o   '%V(m,)' - If one parameter is included, it must be a decimal number.  If 
    a comma follows it, a character in the enclosing block whose ASCII code 
    equals or is greater than the number is considered a match. 
o   '%V(m,n)' - If two parameters are included, they must be decimal numbers. 
    The first specifies a minimum value, the second a maximum value.  A 
    character in the enclosing block whose ASCII code is between the two 
    values, or equal to either, is considered a match. 
o   '%V(,n)' - If the second parameter is included but not the first, it must 
    be a decimal number, and it must be preceded by a comma.  A character in 
    the enclosing block whose ASCII code is less than or equal to the number 
    is considered a match.  For example: 
    DELETE REPEAT SELECT '%V(,31)' 
    Searches forward in the file for ASCII control characters, and deletes any 
    it finds.  The ASCII control characters have decimal codes in the range 0 
    to 31.  The pattern '%V(,31)' matches any single character whose ASCII 
    decimal code is in that range. 
Function Identifier:  W 
The $CONTROL-Wildcard function is similar to the $CONTROL-Question function 
(%?), except that it allows restrictions on the length of the string. 
Assuming the $CONTROL character is the percent symbol (%), the wildcard 
function is used in the following form: 
%W(min,max) 
The min and max parameters are the minimum and maximum lengths, respectively, 
of the wildcard string and are always numbers which represent character 
positions.  Both parameters or a single parameter may be included. 
%W is most logically used between two specific strings.  For example: 
DISPLAY 'from%W(4,10)any' 
finds the next occurrence of "from" followed by "any" at least 4 positions 
later, but not more than 10 positions later in the enclosing block. 
DISPLAY 'from%W(4,)any' 
finds the next occurrence of "from" followed by "any" at least four positions 
later in the enclosing block, with no restriction on the maximum number of 
positions within the block. 
DISPLAY 'from%W(,10)any' 
finds the next occurrence of "from" followed by "any" not more than 10 
positions later in the enclosing block.  There is no restriction here on the 
minimum number of positions after which "any" should follow "from". 
An "absolute" block operand is one which has a specific location.  The 
absolute block operands are: 
    FILE fid 
    STRING string_expression 
    PREVIOUS 
    NEXT 
    location_name 
    record_key 
When evaluating an absolute block operand, the location of the file pointer 
after evaluating the operand has absolutely nothing to do with the location of 
the file pointer before evaluating the operand.  For instance, record 62 of 
file "ABC" is an absolute block operand; there is only one location specified 
by that block. 
o   FILE specifies a file to be used as a block operand.  A block expression 
    can contain only one FILE operand, which must be the first block operand 
    in the expression. 
o   STRING specifies a string expression whose value is to be treated as a 
    file, and used as a block operand.  Usually the string expression value is 
    treated as record 0 of a one-record file; however, by including the 
    $CONTROL-Record function in the string expression, a multi-record "file" 
    may be specified. 
    Like FILE, STRING may be used only once in a block expression, and only as 
    the first block operand in the expression. 
o   PREVIOUS designates the previous edit block as a block operand.  There may 
    be only one PREVIOUS operand in a block expression, and it must be the 
    first block operand in the expression. 
o   NEXT designates the next edit block in the edit block stack as a block 
    operand.  There may be only one NEXT operand in a block expression, and it 
    must be the first block operand in the expression. 
o   The "location_name" specifies a previously-specified and named block to be 
    used as an absolute block operand.  This allows you to define your own 
    absolute block operands and give a name to them (with the LOCATION 
    command); thereafter, that name can be used in other block expressions as 
    an absolute block operand. 
    The location_names may be used more than once in block expressions; 
    however, all location_names used in a block expression must specify blocks 
    residing in the same file.  If a location_name is not the first operand in 
    a block expression, then all location_names in the expression must specify 
    blocks residing in the same file as the current edit block. 
o   A "record_key" identifies a specific record within the current enclosing 
    block which is to be used as a block operand. 
Syntax: 
AD[JUST] [movement_expression] 
Parameters: 
movement_expression    is a movement expression. 
Description: 
ADJUST allows you to change either boundary location of the block being 
specified.  It tells 6Edit that "movement_expression" specifies the location 
of the boundary opposite to the one currently being specified. 
Records in file INVENTORY: 
    40 
    41 
    42 
    . 
    . 
    . 
    . 
    48 
    49 
  Commands in command window: 
    41          moves the cursor to the beginning of record 41. 
    TH          begins block selection. 
    48          selected block is 41 TH 48; cursor is at the beginning of 
                record 49. 
    ADJUST      moves the cursor back to the beginning of record 41; 
                it does not change the selected block. 
    BA SK 1 RE  moves the cursor to beginning of record 40.  The selected 
                block is now beginning of 40 thru end of 48. 
    ADJUST      moves the cursor back to the end of the selected block: 
                beginning of 49. 
    DE THAT     deletes beginning of 40 thru end of 48. 
ADJUST is most useful after a THRU clause.  When 6Edit sees the THRU clause, 
its movement expression moves the file pointer to the end of the block being 
specified.  When the first ADJUST following THRU is given, 6Edit remembers the 
current file pointer location as the ending location of the block being 
specified, and moves the file pointer to the beginning location of the block. 
The movement expression following this first ADJUST then changes the beginning 
location of the block, by moving the file pointer (from its initial location 
at the beginning of the block) to a new beginning location. 
The second ADJUST after THRU acts similarly.  6Edit remembers the current file 
pointer location as the beginning location of the block, and moves the file 
pointer to the ending location of the block; the movement expression following 
the ADJUST changes the ending location of the block. 
Each successive ADJUST repeats this process.  Odd-numbered ADJUSTs after THRU 
(i.e., the first, third, fifth, etc.) change the beginning location of the 
block being specified; even-numbered ADJUSTs after a THRU change the ending 
location of the block being specified. 
At any time in a block expression, you can use THRU.  This clause renders the 
current file pointer location the beginning location of the block being 
specified; the movement expression following THRU always modifies the ending 
location of the block.  Enter 
HELP (6EDIT) THRU 
for more information regarding the THRU command. 
00002
00001
Syntax: 
AF[TER] [BL[OCK]] block_expression 
Parameters: 
block_expression    specifies the location at which to insert the source 
block. 
Description: 
The AFTER command is used to insert a block of data into a file.  The 
block_expression specifies the destination location for the insertion 
operation.  The current source block is inserted into a location just after 
the end of the block specified by block_expression.  (The source block was set 
by the last COPY or MOVE command.) 
The source and destination blocks may be whole records, parts of records, or 
any combination of these. 
Example: 
COPY 1 THRU 5 AFTER 10 
inserts a copy of records 1 through 5 after record 10. 
COPY 1 THRU 5 AFTER FILE OCTOBER_BILLS 42 
copies records 1 through 5 to record 42 of the specified file. 
Related Topics: 
Copy/Move Operations 
COPY Command 
MOVE Command 
OVER Command 
00002
00003
00001
00004
Syntax: 
{AL[L] OF|AO} block_operand 
Parameters: 
block_operand    may be any absolute or relative block operand, possibly 
modified by other block options (only one of the three "point" options -- ALL 
OF, BEGINNING OF, and END OF -- may be used with a block_operand). 
Description: 
ALL OF tells 6Edit to move the file pointer to either the beginning or the end 
of "block_operand," depending on the context: 
o   In the first movement expression of a SELECT clause or in an ADJUST 
    clause, this construct will move the file pointer to the beginning of 
    block_operand. 
o   In the last operand of a THRU clause, this construct will move the file 
    pointer to the end of block_operand. 
Example: 
DELETE AO 5 THRU AO 6 
deletes the records between record 5.0 and 6.0, including all of records 5.0 
and 6.0. 
00002
00003
00001
LOGICAL_OPERATORS
ALL_OF
To obtain more information about the ASCII character set, enter: 
!HELP (IBEX) ASCII character 
where character is: 
    A character or mnemonic (for unprintables) 
    An octal value in the form          O'ooo' 
    A decimal value in the form         D'ddd' 
    An hexadecimal value in the form    X'xx' 
To list the entire ASCII character set, merely type ??<CR> at the next prompt. 
  ASCII NAME         CHARACTER ENTRY         DECIMAL CODE 
 NULL              <CNTL-@>                  0 
 SOH               <CNTL-A>                  1 
 STX               <CNTL-B>                  2 
 ETX               <CNTL-C>                  3 
 ECT               <CNTL-D>                  4 
 ENQ               <CNTL-E>                  5 
 ACK               <CNTL-F>                  6 
 BEL               <CNTL-G>                  7 
 BS                <CNTL-H>                  8 
 HT                <CNTL-I>                  9 
 LF                <CNTL-J>                 10 
 VT                <CNTL-K>                 11 
 FF                <CNTL-L>                 12 
 CR                <CNTL-M>                 13 
 SO                <CNTL-N>                 14 
 SI                <CNTL-O>                 15 
 DLE               <CNTL-P>                 16 
 DC1               <CNTL-Q>                 17 
 DC2               <CNTL-R>                 18 
 DC3               <CNTL-S>                 19 
 DC4               <CNTL-T>                 20 
 NAK               <CNTL-U>                 21 
 SYN               <CNTL-V>                 22 
 ETB               <CNTL-W>                 23 
 CAN               <CNTL-X>                 24 
 EM                <CNTL-Y>                 25 
 SUB               <CNTL-Z>                 26 
 ESC               <CNTL-[>                 27 
 FS                <CNTL-\>                 28 
 GS                <CNTL-]>                 29 
 RS                <CNTL-^>                 30 
 US                <CNTL-_>                 31 
 SP                < >                      32 
 !                 <!>                      33 
 "                 <">                      34 
 #                 <#>                      35 
 $                 <$>                      36 
 %                 <%>                      37 
 &                 <&>                      38 
 '                 <'>                      39 
 (                 <(>                      40 
 )                 <)>                      41 
 *                 <*>                      42 
 +                 <+>                      43 
 '                 <'>                      44 
 -                 <->                      45 
 .                 <.>                      46 
 /                 </>                      47 
 0                 <0>                      48 
 1                 <1>                      49 
 2                 <2>                      50 
 3                 <3>                      51 
 4                 <4>                      52 
 5                 <5>                      53 
 6                 <6>                      54 
 7                 <7>                      55 
 8                 <8>                      56 
 9                 <9>                      57 
 :                 <:>                      58 
 ;                 <;>                      59 
 <                 <<>                      60 
 =                 <=>                      61 
 >                 <>>                      62 
 ?                 <?>                      63 
 @   (at sign)     <@>                      64 
 A                 <A>                      65 
 B                 <B>                      66 
 C                 <C>                      67 
 D                 <D>                      68 
 E                 <E>                      69 
 F                 <F>                      70 
 G                 <G>                      71 
 H                 <H>                      72 
 I                 <I>                      73 
 J                 <J>                      74 
 K                 <K>                      75 
 L                 <L>                      76 
 M                 <M>                      77 
 N                 <N>                      78 
 O                 <O>                      79 
 P                 <P>                      80 
 Q                 <Q>                      81 
 R                 <R>                      82 
 S                 <S>                      83 
 T                 <T>                      84 
 U                 <U>                      85 
 V                 <V>                      86 
 W                 <W>                      87 
 X                 <X>                      88 
 Y                 <Y>                      89 
 Z                 <Z>                      90 
 [ (left bracket)  <[>                      91 
 \ (backslash)     <\>                      92 
 ] (right bracket) <]>                      93 
 ^ (circumflex)    <^>                      94 
 _                 <_>                      95 
 '                 <'>                      96 
 a                 <a>                      97 
 b                 <b>                      98 
 c                 <c>                      99 
 d                 <d>                     100 
 e                 <e>                     101 
 f                 <f>                     102 
 g                 <g>                     103 
 h                 <h>                     104 
 i                 <i>                     105 
 j                 <j>                     106 
 k                 <k>                     107 
 l                 <l>                     108 
 m                 <m>                     109 
 n                 <n>                     110 
 o                 <o>                     111 
 p                 <p>                     112 
 q                 <q>                     113 
 r                 <r>                     114 
 s                 <s>                     115 
 t                 <t>                     116 
 u                 <u>                     117 
 v                 <v>                     118 
 w                 <w>                     119 
 x                 <x>                     120 
 y                 <y>                     121 
 z                 <z>                     122 
 { (left brace)    <{>                     123 
 | (or bar)        <|>                     124 
 } (right brace)   <}>                     125 
 ~ (tilde)         <~>                     126 
 DEL               <DEL>                   127 
Syntax: 
BA[CKWARD] relative_block 
Parameters: 
relative_block    must be a relative block operand. 
Description: 
BACKWARD tells 6Edit in which direction in the file to move the file pointer 
when searching for a relative block operand. 
Relative_block must be a record, position, or pattern-string operand; 6Edit 
moves the file pointer backward accordingly. 
Examples: 
BACKWARD SKIP 8 RECORDS 
moves the file pointer backward in the file, skipping over 8 records. 
BACKWARD SKIP 28 POSITIONS 
moves the file pointer backward in the file, skipping over 28 positions 
(characters in records). 
BACKWARD 'abc' 
moves the file pointer backward in the file, searching for the string "abc" in 
the file. 
00002
00003
00001
Syntax: 
{BE[GINNING] OF|BO} block_operand 
Parameters: 
block_operand    may be any absolute or relative block operand, possibly 
modified by other block options (only one of the three "point" options -- ALL 
OF, BEGINNING OF, and END OF -- may be used with a block_operand). 
Description: 
BEGINNING OF tells 6Edit to move the file pointer to the beginning of 
block_operand.  For instance, if block_operand was a block comprising three 
records, BEGINNING OF tells 6Edit to move the file pointer to the first 
character of the first of the three records. 
Example: 
DELETE BO 5 THRU BO 6 
deletes the records between record 5.0 and 6.0, including record 5.0. 
However, record 6.0 will not be affected. 
00002
00003
00001
BEGINNING_OF
The 6Edit editing commands work with "blocks" of data.  A block can be an 
entire file, or any portion of a file.  A block is usually a string of 
characters taken from one or several records in a file.  For more help on 
blocks, enter the following: 
    ??         (to view all following topics) 
    HELP (6EDIT) EDIT_BLOCK (defines the edit block) or 
HELP (6EDIT) SELECTED_BLOCK (defines the selected block) 
or  HELP (6EDIT) REPEATED_BLOCKS 
or  HELP (6EDIT) ENCLOSED_BLOCKS 
There are two special blocks used in 6Edit:  the edit block and the 
selected block. 
A block expression specifies a block of data in a file.  All editing commands 
have a single block expression as a parameter.  This expression specifies the 
block of data upon which the editing command is to operate (to delete the 
block, to copy the block, to replace the block, etc.) 
Block expressions can indicate whether the block resides in a specific file, 
or if it resides in the edit block (the block currently being edited).  The 
boundaries of a block can be given in absolute terms, such as a specific 
location in a file, or in relative terms, such as forward or backward from the 
current file pointer location, or in a combination of these. 
The LOCATION command allows you to give a name to the location of a block. 
Later, you can use that name in a block expression to refer to the designated 
block. 
Block expressions can be enclosed and repeated.  When a block expression 
specifies a repeated block, the entire editing operation of which the block 
expression is a parameter is repeated. 
BLOCK_EXPRESS_SYNTAX
General Form: 
[enclosing_block] [REPEAT] SELECT [movement] 
    {THRU|ADJUST} [movement] [{THRU|ADJUST} [movement]]... 
        [[REPEAT] SELECT [movement] 
            {THRU|ADJUST} [movement] [{THRU|ADJUST} [movement]]...]... 
Parameters: 
enclosing_block    is any block expression.  An "enclosing_block" may be 
omitted; if it is, the current edit block is used as the enclosing block for 
the expression. 
REPEAT SELECT    serves two purposes:  it may be used to enclose block 
expressions, and/or to specify a repeated block. 
movement    is a "movement expression":  a list of block operands, possibly 
modified by evaluation options.  A "movement expression" moves the file 
pointer to a new location. 
THRU    tells 6Edit that the next movement (movement expression) moves the 
file pointer to the end of the block being specified. 
ADJUST    tells 6Edit that the next movement (movement expression) moves the 
file pointer to the opposite end of the block being specified. 
Description: 
As described earlier, block expressions specify three things:  the enclosing 
block, the beginning point of the block, and the ending point of the block. 
The first SELECT clause is needed only when "enclosing_block" is given, or 
when the SELECT clause specifies a repeated block. 
Each "SELECT ... {THRU|ADJUST} ... {THRU|ADJUST} ..."  group specifies the 
beginning and ending points of a block; each such group except the last 
specifies the enclosing block for the next SELECT group. 
Note that all components of a block expression are optional, but at least one 
component must be given. 
00002
00001
You can modify block operands with "block options." 
If a block operand is given without a particular option, 6Edit uses as the 
default the current value of the predefined name for that option.  There is a 
specific predefined name for each option.  The value assigned to these names, 
if any, is usually the keyword for the desired option (for more HELP, type 
HELP (6EDIT) EQUALS).  If the predefined name for an option has no value and 
the option was not specified with a block operand, 6Edit uses a standard 
default. 
There are two kinds of block options:  "evaluation options" and "processing 
options." 
BEGINNING_OF
Syntax: 
block_expression  BY  edit_key 
Parameters: 
edit_key    is a CP-6 edit key, that is, a string of 1 to 8 digits; if a 
decimal point is included in the string, there may be 0 to 3 digits to the 
right of the decimal point. 
Description: 
BY specifies a value to be used when 6Edit generates new record keys for a 
keyed file. 
BY may be included in block expressions which specify destination block 
operands only; this only includes the operands of the AFTER and OVER commands. 
If block_expression resides in an edit-keyed file and 6Edit must insert new 
records in that file, 6Edit must generate new record keys for the new records. 
6Edit does this by adding the value of edit_key to the record key of the last 
existing record in front of the location in the file into which 6Edit is 
inserting records.  Therefore, for edit-keyed files, edit_key must evaluate to 
a numeric operand whose value is between 0 and 99999.999, inclusive.  If the 
generated key is greater than or equal to an existing key in the file, then 
6Edit discontinues the operation, and displays an error message. 
Example: 
CO FILE ACCTS_PAYABLE 1 TH 50 AF FILE ACCTS_RECEIVABLE 1024 BY .1 
If the BY option is not specified with a block operand, the current value of 
$BY is used as the record key increment. 
CO FILE *1 OVER NEW FILE *2 BY 1 
If the BY option is used for a block expression that also creates a new edit 
block as in the example above, that key increment value overrides the value in 
the $BY predefined name for the rest of the life of that edit block. 
00002
00003
00001
Changes have been made to this manual to answer STARs and to correct spelling, 
format, and the HELP facility.  These changes have been marked with change 
bars.  Significant content changes are listed below: 
o   The option $ONESPACEEDIT has been added to the FORMAT command ESC-2-LF. 
    Type 'HELP (6EDIT) PREDEFINED_NAMES $ONESPACEEDIT'. 
o   The description under the subtopic $TEXTEDIT of the topic PREDEFINED_NAMES 
    has been clarified. 
COPY
There are three categories of commands in 6Edit:  editing, assignment, and 
housekeeping.  Help for the 6Edit commands can be obtained by entering: 
    HELP (6EDIT) command 
where 'command' is a verb from the list below:  Use HELP (6EDIT) EDIT for both 
the EDIT and EDIT PREVIOUS commands. 
  Type   Syntax                          Description 
Editing Commands 
       6E[DIT] file                    Begin editing (by displaying the 
                                       specified block) 
       6B[UILD] file                   Create a new file 
       6X file                         Edit block in protected mode 
       ED[IT]  block                   Begin editing (sets edit block) 
       [DI[SPLAY]]  block              Display a block 
       CO[PY]  {block|string}          Set source for copy operation 
       MO[VE]  block                   Set source for copy; delete 
                                       after copy 
       AF[TER]  block                  Copy source, inserting after block 
       OV[ER]  block                   Copy source, replacing block 
       DE[LETE]  block                 Delete a block 
Assignment Commands 
       name  EQ[UAL[S]]  string        Assign string value to name 
       LO[CATION]  name [IS] block     Make name refer to block 
       SY[NONYM]  name [IS] fragment   Make name a synonym for fragment 
       KE[YIN]  str_1 IS str_2         Redefine a terminal key 
Housekeeping Commands 
       TIME                            Display current date and time 
       DA[TE]                          Display current date and time 
       DIR[ECTORY] [fid|R[ESET]]       Change default account and 
                                       packset name 
       {DO|!} command                  Call another processor 
       H[ELP] [(processor)] [topic]    Display specified on-line 
                                       information 
       IF str [cd];cds[;ELSE [cd];cds] Conditionally execute commands. 
       READ fid                        Read 6Edit commands from fid 
       OUT[PUT] [location] [optlist]   Send output to specified location 
       PRINT [ALL|ldevlist]            Direct accumulated output to 
                                       destination 
       ERASE [ALL|ldevlist]            Delete specified output 
       EN[D]|X[IT]|Q[UIT]              Exit 6Edit 
       REST[ORE] fid                   Restore context information from 
                                       fid 
       SAVE [option] {TO|ON|OVER} fid  Save current context information 
       SH[OW] option                   Displays strings, assigned 
                                       names, records in a block, keyin 
                                       definitions, and windows 
       [function] WI[NDOW] [option]    Creates a new editing window, 
                                       changes current editing window, 
                                       or switches to another editing 
                                       window 
A "command line" is one record from the "command stream."  The command stream 
usually originates from the keyboard of your terminal. 
Command lines contain one or more commands.  Multiple commands in one command 
line are separated by a semicolon (;). 
If the command you type is longer than one line, type a semicolon as the last 
character of each ongoing line (except the last line of the command). 
Example: 
CO ST 'This drawn-out line renders the command lengthy' AFTER; 
FI XYZ 20.5 
For more help on commands and command entry, enter: 
    HELP (6EDIT) LEXICAL_FUNCTIONS 
or  HELP (6EDIT) COMMANDS 
or  HELP (6EDIT) STRING_EXPRESSIONS 
or  HELP (6EDIT) NAMES 
00001
Lines at the top of your screen (above the border line) comprise the command 
window.  The number of lines in this window changes depending on the window's 
usage.  When the command window displays messages, it grows larger; when you 
type commands in this window, it remains small. 
When the cursor is in the command window, you can type 6Edit commands. 
You can control the minimum and maximum size of the command window by 
assigning values to the predefined names "$MIN_COMMAND" and "$MAX_COMMAND". 
The stream name for the 6Edit command window is the lowest unused UC stream 
greater than UC09 (usually UC10). 
$COMMENT
Below is a list of the common function names. 
ADJUST              COPY_THAT           L_IS_THAT 
AFTER_HERE          DELETE_THAT         M_L_AFTER_HERE 
BACKWARD_8_RECORDS  EDIT_NEXT           MOVE_RECORD 
BACKWARD_20_RECORDS EDIT_PREVIOUS       MOVE_THAT 
BACKWARD_PATTERN    EDIT_THAT           OVER_THAT 
BO_CURRENT          EO_CURRENT          PATTERN_SEARCH 
C_L_AFTER_HERE      FORWARD_8_RECORDS   THRU 
COMMAND_WINDOW      FORWARD_20_RECORDS  SUBSTITUTE 
COPY_RECORD         L 
The table below gives the function name, its description, and HELP information 
about key functions in each context file. 
For more information about an actual function key sequence in your particular 
context file, type: 
HELP COMMON_FUNCTIONS function_name 
For example: 
HELP COMMON_FUNCTIONS ADJUST 
or 
HELP COMMON_FUNCTIONS PATTERN_SEARCH 
This command sequence renders each common command's key 
invocation for all the context files. 
  Function    Description 
  ADJUST 
              Move the cursor to the other end of the block currently being 
              selected.  If you type the ADJUST function repeatedly, the 
              cursor bounces back and forth from one end of the current 
              selected block to the other.  While the cursor is at an end of 
              the selected block, moving the cursor changes the specification 
              of the block. 
              Standard Context File ADJUST: CNTL-A 
              DECVT100 Context File ADJUST: *** 
              PCTV7800 Context File ADJUST: CNTL-K 
              PCTX364 Context File ADJUST: CNTL-K 
              VIP7205 ADJUST: CNTL-A 
              VIP7801/VIP7802 ADJUST: Esc   
              ZENITH Z19 ADJUST: Esc T 
  AFTER HERE 
              Insert the source block at the current cursor location.  You 
              must have set the source block previously with some COPY or MOVE 
              command. 
              Standard Context File After Here: Esc / 
              DECVT100 Context File After Here: Pad 8 / 
              PCTV7800 Context File After Here: CNTL-A / 
              PCTX364 Context File After Here: CNTL-A / 
              VIP7205 After Here: Esc < 
              VIP7801/VIP7802 After Here: Esc < 
              ZENITH Z19 After Here: Esc Q 
  BACKWARD 8 RECORDS 
              Move the cursor backward (up) 8 records. 
              Standard Context File BACKWARD 8 RECORDS: Esc W 
              DECVT100 Context File BACKWARD 8 RECORDS: PF3 
              PCTV7800 Context File BACKWARD 8 RECORDS: CNTL-Page Up 
              PCTX364 Context File BACKWARD 8 RECORDS: CNTL-Page Up 
              VIP7205 BACKWARD 8 RECORDS: Esc 5 
              VIP7801/VIP7802 BACKWARD 8 RECORDS: Esc [I 
              ZENITH Z19 BACKWARD 8 RECORDS: Esc ! 
  BACKWARD 20 RECORDS 
              Move the cursor backward 20 records. 
              Standard Context File BACKWARD 20 RECORDS: Esc A 
              DECVT100 Context File BACKWARD 20 RECORDS: PF1 
              PCTV7800 Context File BACKWARD 20 RECORDS: Page Up 
              PCTX364 Context File BACKWARD 20 RECORDS: Page Up 
              VIP7205 BACKWARD 20 RECORDS: Esc 7 
              VIP7801/VIP7802 BACKWARD 20 RECORDS: Esc [P 
              ZENITH Z19 BACKWARD 20 RECORDS: Esc ' 
  Backward Pattern Search 
              Search backward for a match of a pattern.  This resembles the 
              Pattern Search key, searching backward in the file from the 
              current cursor location. 
              Standard Context File Backward Pattern Search: Esc P 
              DECVT100 Context File Backward Pattern Search: Pad , 
              PCTV7800 Context File Backward Pattern Search: CNTL-F1 
              PCTX364 Context File Backward Pattern Search: CNTL-F1 
              VIP7205 Backward Pattern Search: Esc 1 
              VIP7801/VIP7802 Backward Pattern Search: Esc 1 
              ZENITH Z19 Backward Pattern Search: Esc V 
  BO CURRENT 
              Move the cursor to the beginning of the current edit block. 
              Standard Context File BO CURRENT: Esc B 
              DECVT100 Context File BO CURRENT: Pad 5 
              PCTV7800 Context File BO CURRENT: Home 
              PCTX364 Context File BO CURRENT: Home 
              VIP7205 BO CURRENT: Esc F 
              VIP7801/VIP7802 BO CURRENT: Esc 5 
              ZENITH Z19 BO CURRENT: Esc O 
  Command Window 
              Move the cursor to the command window. 
              Standard Context File COMMAND WINDOW: CNTL-G 
              DECVT100 Context File COMMAND WINDOW: CNTL-A 
              PCTV7800 Context File COMMAND WINDOW: CNTL-G 
              PCTX364 Context File COMMAND WINDOW: CNTL-G 
              VIP7205 COMMAND WINDOW: Esc   
              VIP7801/VIP7802 COMMAND WINDOW: Esc e 
              ZENITH Z19 COMMAND WINDOW: Esc S 
  COPY L AFTER HERE 
              Insert the block named L at the current cursor location.  You 
              should have given a block the name L previously, using the 
              LOCATION command. 
              Standard Context File COPY L AFTER HERE: Esc 4 
              DECVT100 Context File COPY L AFTER HERE: Pad 9 
              PCTV7800 Context File COPY L AFTER HERE: F4 
              PCTX364 Context File COPY L AFTER HERE: F4 
              VIP7205 COPY L AFTER HERE: *** 
              VIP7801/VIP7802 COPY L AFTER HERE: *** 
              ZENITH Z19 COPY L AFTER HERE: Esc 4 
  COPY RECORD 
              The record on which the cursor is sitting becomes the source 
              block for the next AFTER/OVER command. 
              Standard Context File COPY RECORD: Esc 3 
              DECVT100 Context File COPY RECORD: Pad 4 
              PCTV7800 Context File COPY RECORD: F1 
              PCTX364 Context File COPY RECORD: F1 
              VIP7205 COPY RECORD: *** 
              VIP7801/VIP7802 COPY RECORD: *** 
              ZENITH Z19 COPY RECORD: Esc 3 
  COPY THAT 
              The selected block becomes the source block for the next 
              AFTER/OVER operation.  Before typing the COPY key you should 
              select a block of data. 
              Standard Context File COPY THAT: Esc 1 
              DECVT100 Context File COPY THAT: Pad 7 
              PCTV7800 Context File COPY THAT: CNTL-C 
              PCTX364 Context File COPY THAT: CNTL-C 
              VIP7205 COPY THAT: Esc : 
              VIP7801/VIP7802 COPY THAT: Esc : 
              ZENITH Z19 COPY THAT: Esc R 
  DELETE THAT 
              Delete the selected block.  Before typing the DELETE key you 
              should select the block of data to be deleted. 
              Standard Context File Delete That: Esc * 
              DECVT100 Context File Delete That: *** 
              PCTV7800 Context File Delete That: CNTL-D 
              PCTX364 Context File Delete That: CNTL-D 
              VIP7205 Delete That: Esc = 
              VIP7801/VIP7802 Delete That: Esc = 
              ZENITH Z19 Delete That: Esc E 
  EDIT NEXT 
              EDIT NEXT advances you to the next edit block.  This allows you 
              to refer to the block specification following your current edit 
              block. 
              Standard Context File EDIT NEXT: Esc ] 
              DECVT100 Context File EDIT NEXT: Pad 3 
              PCTV7800 Context File EDIT NEXT: CNTL-N 
              PCTX364 Context File EDIT NEXT: CNTL-N 
              VIP7205 EDIT NEXT: *** 
              VIP7801/VIP7802 EDIT NEXT: *** 
              ZENITH Z19 EDIT NEXT: Esc ] 
  EDIT PREVIOUS 
              EDIT PREVIOUS restores the old edit block from a previous EDIT 
              command.  This becomes the new edit block.  EDIT THAT and EDIT 
              PREVIOUS can be used together to make editing easier. 
              For example, to change all occurrences of "giraffe" to "horse" 
              only in a specific group of records, use the following 
              procedure: 
              o   Select the group of records:  move the cursor to the 
                  beginning of the first record in the group, type THRU, then 
                  move the cursor to the beginning of the record after the 
                  last record in the group. 
              o   Type EDIT THAT. 
              o   Type the Substitute key, fill in the new and old strings, 
                  and perform the operation. 
              o   Type EDIT PREVIOUS. 
                  Standard Context File EDIT PREVIOUS: Esc [ 
                  DECVT100 Context File EDIT PREVIOUS: Pad 1 
                  PCTV7800 Context File EDIT PREVIOUS: CNTL-P 
                  PCTX364 Context File EDIT PREVIOUS: CNTL-P 
                  VIP7205 EDIT PREVIOUS: *** 
                  VIP7801/VIP7802 EDIT PREVIOUS: *** 
                  ZENITH Z19 EDIT PREVIOUS: Esc [ 
  EDIT THAT 
              The selected block becomes the new edit block.  6Edit remembers 
              the old edit block so it can restore it later.  The selected 
              block must begin and end at the beginning of the records you 
              want to include in the new edit block.  This key is useful 
              before using the Substitute key to limit the string 
              substitutions to the records in the selected block. 
              Standard Context File EDIT THAT: Esc _ 
              DECVT100 Context File EDIT THAT: Pad 2 
              PCTV7800 Context File EDIT THAT: CNTL-E 
              PCTX364 Context File EDIT THAT: CNTL-E 
              VIP7205 EDIT THAT: *** 
              VIP7801/VIP7802 EDIT THAT: *** 
              ZENITH Z19 EDIT THAT: Esc _ 
  EO CURRENT 
              Move the cursor to the end of the current edit block. 
              Standard Context File EO CURRENT: Esc F 
              DECVT100 Context File EO CURRENT: Pad 6 
              PCTV7800 Context File EO CURRENT: End 
              PCTX364 Context File EO CURRENT: End 
              VIP7205 EO CURRENT: Esc F 
              VIP7801/VIP7802 EO CURRENT: Esc 2 
              ZENITH Z19 EO CURRENT: Esc F 
  FORWARD 8 RECORDS 
              Move the cursor forward (down) 8 records. 
              Standard Context File FORWARD 8 RECORDS: Esc E 
              DECVT100 Context File FORWARD 8 RECORDS: PF4 
              PCTV7800 Context File FORWARD 8 RECORDS: CNTL-Page Down 
              PCTX364 Context File FORWARD 8 RECORDS: CNTL-Page Down 
              VIP7205 FORWARD 8 RECORDS: Esc 2 
              VIP7801/VIP7802 FORWARD 8 RECORDS: Esc [L 
              ZENITH Z19 FORWARD 8 RECORDS: Esc 1 
  FORWARD 20 RECORDS 
              Move the cursor forward 20 records (about a screen-full). 
              Standard Context File FORWARD 20 RECORDS: Esc L 
              DECVT100 Context File FORWARD 20 RECORDS: PF2 
              PCTV7800 Context File FORWARD 20 RECORDS: Page Down 
              PCTX364 Context File FORWARD 20 RECORDS: Page Down 
              VIP7205 FORWARD 20 RECORDS: Esc 6 
              VIP7801/VIP7802 FORWARD 20 RECORDS: Esc [M 
              ZENITH Z19 FORWARD 20 RECORDS: Esc 2 
  Move to L 
              Move the cursor to the block named L.  You should have 
              previously located a block, giving it the name L.  This is done 
              with Location L function.  Having named a block L, you can 
              return to it at any time (in the same editing session) using L. 
              Standard Context File Move to L: Esc . 
              DECVT100 Context File Move to L: CNTL-L 
              PCTV7800 Context File Move to L: CNTL-L 
              PCTX364 Context File Move to L: CNTL-L 
              VIP7205 Move to L: *** 
              VIP7801/VIP7802 Move to L: *** 
              ZENITH Z19 Move to L: Esc . 
  LOCATION L IS THAT 
              Gives the name L to the location of the selected block. 
              Standard Context File LOCATION L IS THAT: Esc : 
              DECVT100 Context File LOCATION L IS THAT: Pad . 
              PCTV7800 Context File LOCATION L IS THAT: F3 
              PCTX364 Context File LOCATION L IS THAT: F3 
              VIP7205 LOCATION L IS THAT: Esc 9 
              VIP7801/VIP7802 LOCATION L IS THAT: Esc 9 
              ZENITH Z19 LOCATION L IS THAT: Esc : 
  MOVE L AFTER HERE 
              Insert the block named L at the current cursor location.  This 
              is the same as the "COPY L AFTER HERE" key except that after 
              inserting the block at the cursor location the block named L is 
              deleted.  (Note that after this deletion, the name L still 
              refers to the same location in the file.)  You should have given 
              a block the name L previously, using the LOCATION command. 
              Standard Context File Move L After Here: Esc $ 
              DECVT100 Context File Move L After Here: *** 
              PCTV7800 Context File Move L After Here: F5 
              PCTX364 Context File Move L After Here: F5 
              VIP7205 Move L After Here: *** 
              VIP7801/VIP7802 Move L After Here: *** 
              ZENITH Z19 Move L After Here: Esc $ 
  MOVE RECORD 
              The record on which the cursor is sitting becomes the source 
              block for the next AFTER/OVER command.  Also, after performing 
              the next AFTER/OVER command, 6Edit deletes this record. 
              Standard Context File Move Record: Esc # 
              DECVT100 Context File Move Record: Esc # 
              PCTV7800 Context File Move Record: F2 
              PCTX364 Context File Move Record: F2 
              VIP7205 Move Record: *** 
              VIP7801/VIP7802 Move Record: *** 
              ZENITH Z19 Move Record: Esc # 
  MOVE THAT 
              The selected block becomes the source block for the next 
              AFTER/OVER operation.  This is the same as the COPY key, except 
              that after the next AFTER/OVER operation the source block is 
              deleted. 
              Standard Context File Move That: Esc ! 
              DECVT100 Context File Move That: Esc ! 
              PCTV7800 Context File Move That: CNTL-V 
              PCTX364 Context File Move That: CNTL-V 
              VIP7205 Move That: Esc \ 
              VIP7801/VIP7802 Move That: Esc \ 
              ZENITH Z19 Move That: Esc P 
  OVER THAT 
              Replace the selected block with the source block.  Before typing 
              the OVER key you should select the block of data which is to be 
              replaced. 
              Standard Context File Over That: Esc @ 
              DECVT100 Context File Over That: *** 
              PCTV7800 Context File Over That: CNTL-O 
              PCTX364 Context File Over That: CNTL-O 
              VIP7205 Over That: *** 
              VIP7801/VIP7802 Over That: *** 
              ZENITH Z19 Over That: Esc *** 
  Pattern Search 
              Search forward for a match of a pattern.  When you type the 
              Pattern Search key, the cursor moves to the command window, and 
              the one of following message displays appears. 
              o   The message 
                  SKIP 1 '' 
                  appears and the cursor moves to the second apostrophe ('), 
                  ready for you to type a pattern string.  After you have 
                  typed the pattern string, press the Return key. 
              o   Or, the message 
                  Pattern string: 
                  appears; you type the pattern string and press the Return 
                  key. 
              6Edit searches for the pattern, moving forward in the file from 
              the current cursor location.  If 6Edit finds a match, it places 
              the cursor on the match and fills the screen with data from the 
              area of the file surrounding the match; if 6Edit does not find a 
              match, it does not move the cursor from its location when the 
              Pattern Search key is typed. 
              If you want to search for the same pattern string that was used 
              in the last pattern search, just type Return immediately after 
              typing the Pattern Search key.  This enters an empty pattern 
              string, which tells 6Edit to use the last pattern string typed. 
              Standard Context File PATTERN SEARCH: CNTL-P 
              DECVT100 Context File PATTERN SEARCH: Pad Enter 
              PCTV7800 Context File PATTERN SEARCH: CNTL-F2 
              PCTX364 Context File PATTERN SEARCH: CNTL-F2 
              VIP7205 PATTERN SEARCH: Esc O 
              VIP7801/VIP7802 PATTERN SEARCH: Esc O 
              ZENITH Z19 PATTERN SEARCH: Esc W 
  THRU 
              Type this key when the current cursor location is the beginning 
              of a block of data you want to select.  This block becomes the 
              selected block.  To complete the selection after typing the THRU 
              key, move the cursor to the end of the block you want to select. 
              At that time, you can either: 
              Type a key which performs some operation with the selected 
              block, such as COPY, DELETE, AFTER, or LOCATION, or 
              move the cursor to the command window, and enter an editing 
              command.  In the command, you can use the predefined name THAT 
              to refer to the selected block, the block of data which you just 
              selected. 
              Standard Context File THRU: CNTL-T 
              DECVT100 Context File THRU: Pad 0 
              PCTV7800 Context File THRU: CNTL-B 
              PCTX364 Context File THRU: CNTL-B 
              VIP7205 THRU: Esc i 
              VIP7801/VIP7802 THRU: Esc i 
              ZENITH Z19 THRU: Esc H 
  Substitute 
              Substitute a string for all pattern matches.  When you type this 
              key, the cursor moves to the command window, and one of the 
              following displays occurs. 
              o   The message 
                  COPY STRING '' OVER REPEAT SELECT PATTERN '' 
                  appears with the cursor on the second apostrophe ('), ready 
                  for you to type a replacement string for all pattern 
                  matches.  You can also type a pattern string between the 
                  second pair of apostrophes (''). 
              o   Or, the message 
                  New string: 
                  appears; you then type the new string and press the Return 
                  key.  Then 6Edit displays the message: 
                  Old string: 
                  to which you enter the old string and press the Return key. 
              This key can be used to replace all matches of a pattern string 
              with a different string. 
              You do not have to type a pattern string if the last pattern you 
              searched for is the one you want to use for the substitution 
              operation. 
              The replacement is done over the remainder of the edit block, 
              from the current cursor location to the end of the edit block. 
              If you want to limit the replacement to some block of data in 
              the file, insert the specification of that block between the 
              keywords OVER and REPEAT. 
              Example: 
              COPY STRING 'xyz' OVER REPEAT SELECT PATTERN 'abc' 
              replaces the remaining occurrences of the string "abc" with the 
              replacement string "xyz". 
              COPY STRING 'xyz' OVER THAT REPEAT SELECT PATTERN 'abc' 
              limits replacement to the current selected block.  You can 
              specify the selected block (prior to typing the Substitute key) 
              by moving the cursor and using the THRU key or the ADJUST key. 
              COPY STRING 'xyz' OVER 10 THRU 20 REPEAT SELECT PATTERN 'abc' 
              searches between records 10.0 and 20.0; in that range, it 
              replaces all appearances of "abc" with "xyz". 
              COPY STRING 'xyz' OVER SECTION_4 REPEAT SELECT PATTERN 'abc' 
              assumes that you have created a name "SECTION_4" with the 
              LOCATION command; it limits replacement to the block of data 
              which you located as "SECTION_4". 
              Standard Context File SUBSTITUTE: Esc = 
              DECVT100 Context File SUBSTITUTE: CNTL-T 
              PCTV7800 Context File SUBSTITUTE: CNTL-T 
              PCTX364 Context File SUBSTITUTE: CNTL-T 
              VIP7205 SUBSTITUTE: Esc 8 
              VIP7801/VIP7802 SUBSTITUTE: Esc 8 
              ZENITH Z19 SUBSTITUTE: Esc U 
00001
00002
00004
00003
00005
00006
00008
00007
00009
00010
00011
00012
00013
00014
00015
00017
00016
00018
00019
00020
00021
00022
00023
00024
00026
00025
Syntax: 
string-1 {|| or !! or .CONCAT.} string-2 
Parameters: 
string    identifies the character or characters to be joined. 
Description: 
The .CONCAT. operator joins its two string operands into one string. 
00002
00001
IMB
A context file defines: 
o   The keys and key sequences used on your terminal to invoke 6Edit's special 
    input editing functions (such as "move cursor to command window"), as well 
    as many common commands. 
o   Names for the ASCII control characters used to invoke 6Edit's special 
    input editing functions.  These are helpful when you use the KEYIN command 
    interactively to define keys on your terminal. 
o   Synonyms for several commonly-used phrases in the 6Edit command language. 
COMMAND_LINES
$CONTROL
Syntax: 
CO[PY] {[BL[OCK]] block_expression} 
       {ST[RING] string_expression} 
Parameters: 
block_expression    is the block of data to be copied. 
string_expression    is the string of characters to be copied. 
Description: 
The COPY command specifies the source block for the next AFTER or OVER 
command. 
The COPY command is a passive command.  To have any effect, it must be 
followed by an AFTER or OVER command. 
6Edit remembers the location of the source block for use later by the AFTER 
and OVER commands. 
If block_expression is given, then 6Edit simply remembers the location of the 
block specified, it does not keep a separate copy of the data.  If 
string_expression is given, then 6Edit keeps a copy of the value of 
string_expression for later use by the AFTER and OVER commands. 
Example: 
COPY 2 PO 10 THRU EO 4 
specifies a source block which begins at position 10 of record 2, and ends at 
the end of record 4.  6Edit ignores this data until it receives the next AFTER 
or OVER command. 
COPY ST 'X' OVER REPEAT SELECT 'Y' 
replaces all 'Y's with 'X's.  This command searches for 'Y's starting at the 
current file pointer location, and proceeds to the end of the edit block. 
Related Topics: 
Copy/Move Operations 
MOVE Command 
AFTER Command 
OVER Command 
00002
00003
00001
00004
In 6Edit, you can copy or move a block of data from one location to another. 
This is done in two steps: 
1.  First, you specify the block you want to copy or move; this is called the 
    "source block."  The COPY and MOVE commands specify the source block for 
    the operation. 
2.  Then, you specify the "destination" for the copy/move.  Use the AFTER 
    command to insert the source block at a location in a file.  Or, use the 
    OVER command to replace a destination block with the source block. 
The COPY and MOVE commands do not make any changes to the file; they just 
specify the source block for the copy/move operation.  Only when you enter an 
AFTER or OVER command is the copy/move operation performed. 
Both the source and destination blocks can be any sequence of characters, 
records, or parts of records.  6Edit uses the same commands to copy/move one 
characters, an entire file, a sentence, or a few words. 
When copying a block of data, 6Edit maintains any "record boundaries" in the 
block; that is, characters which were together in one record in the source 
block remain together in one record after the operation, at the destination 
location. 
Syntax: 
DATE 
Parameters: 
None 
Description: 
DATE (a synonym for the TIME command) displays the current date and time. 
Example: 
DATE 
requests a display of the current data and time.  A sample display is: 
MAY 22  '81  14:39 
Related Commands: 
TIME 
00002
00003
00001
00004
6Edit uses eleven DCBs.  Before starting 6Edit, you can set some of the DCBs 
to other files or devices, using the IBEX SET command.  The following list 
describes each DCB. 
M$SI 
can be set to a file containing 6Edit commands.  6Edit executes these commands 
after it reads the context file. 
M$6E 
can be set to the window which 6Edit is to use as the terminal screen.  If it 
is not set, 6Edit uses all but the top line of UC01. 
M$FILE 
can be set to correspond to the file to be initially edited.  You may also 
designate the initial file on the IBEX command line. 
M$DO 
receives error messages from 6Edit in non-interactive mode (BATCH or XEQ), or 
if set to a file. 
M$EI, M$E9, M$6E00, M$6E01, M$EW 
are reset (or "scrubbed") by 6Edit.  You should not set them. 
M$ME 
receives information messages in non-interactive mode, and accepts command 
input in interactive but not full-screen mode (e.g., $SCREEN EQ 0). 
M$LO 
is used in non-interactive mode to echo commands if echoing is enabled (in 
IBEX), to display error messages, and to display information from the SHOW 
command.  It is normally assigned to the command window, but may be redirected 
via the OUTPUT command. 
Syntax: 
DE[LETE] [BL[OCK]] block_expression 
Parameters: 
block_expression    is the block of data to be deleted. 
Description: 
The DELETE command deletes its operand.  After deleting the block, the 
location vacated by the block becomes the new selected block.  Note that this 
is an "empty" block:  it contains no data characters. 
Note that "block_expression" can explicitly specify an entire file (e.g., 
"FILE filename").  In this case, the file itself is deleted, not just the 
records in it. 
If a file is open for editing when DELETE FILE is entered, the editing window 
is cleared, and the following messages appear in the command window: 
* File filename deleted. 
* EDIT PREVIOUS will restore the Edit Block. 
If the file open for editing was the one deleted and no other files are in the 
edit block stack, the EDIT PREVIOUS message is not issued.  A deleted file 
cannot be restored by 6Edit. 
If the file open for editing was a file other than the one deleted, then 
entering EDIT PREVIOUS will return that file to the screen. 
Example: 
DELETE 5 
means delete record 5. 
DELETE BO CURRENT THRU 5 PO 20 
means delete everything from the beginning of the current edit block through 
record 5 position 20. 
DELETE FILE TRANS 
means delete the file TRANS and all the records in it. 
00002
00003
00001
You can delete characters in several ways.  Type ?? to view the various ways. 
  Command    Function and Description 
  <DEL> 
             Delete character. 
             Usually deletes the character under the cursor.  However, in the 
             replacement mode only, if the cursor is at the end of the 
             insertion window, <DEL> deletes the character to the left of the 
             cursor. 
  <ESC> <DEL> 
             Delete left character. 
             Always deletes the character to the left of the cursor. 
  <ESC> <CNTL-K> 
             Delete characters from the beginning of the record up to the 
             character just to the left of the cursor. 
  <ESC> <K> 
             Delete the character under the cursor and all characters to the 
             right to the end of the record. 
  <ESC> <CNTL-L> 
             Delete the record from the file. 
             This is the same as <ESC> <X>, but it also deletes the record 
             from the file. 
  <ESC> <CNTL-W> 
             Delete word. 
             Deletes the character under the cursor, and all characters to the 
             right up to the start of the next word. 
             You can use the KEYIN command to define keys that can delete 
             either the previous or the next word. 
  <ESC> <X> 
             Delete the entire record. 
             This does not remove the record key from the file, but does 
             delete all characters in the record. 
  <CNTL-X> 
             Same as <ESC> <X>. 
00008
00001
00003
00005
00006
00002
00004
00007
DISPLAY
Syntax: 
DIR[ECTORY] [fid|R[ESET]] 
Parameters: 
fid    is a fid containing only an account name, and an optional packset name. 
Description: 
The DIRECTORY command changes the default account and packset for fids.  These 
defaults are used if a fid in any later command does not include an account 
and packset name.  If neither the fid nor the RESET option is included, 6Edit 
simply displays the current directory. 
The RESET keyword specifies that the default account and packset name are to 
be reset to the user defaults (i.e., the defaults in effect when you logged on 
to the system). 
Example: 
DIR .SYSLIB 
directs subsequent fids that do not include an account to default to the 
.SYSLIB account and to the packset associated with that account. 
00002
00003
00001
Syntax: 
[DI[SPLAY]]  [BL[OCK]] block_expression 
Parameters: 
block_expression    is the block of data to be displayed. 
Description: 
The DISPLAY command displays the value of its operand. 
DISPLAY SKIP 20 RECORDS 
means move the cursor to the record which is 20 records beyond the current 
cursor record.  A section of the file surrounding this record is displayed in 
the editing window. 
SKIP 20 RECORDS 
performs the same function as the above command, except that 6Edit does not 
forget the block selected before the command; it simply changes the block's 
boundaries. 
DISPLAY 428.5 
means move the cursor to the record in the current edit block with key 428.5. 
The verb DISPLAY may be omitted from the command line.  However, there is a 
variation in the command's effect:  when the verb DISPLAY is given, 6Edit 
forgets any block selected prior to the command, and the block_expression in 
the DISPLAY command becomes the new selected block. 
On the other hand, when the verb DISPLAY is omitted, block_expression only 
changes part of the specification of the block being selected (if any) prior 
to this command.  For example: 
Form                Result 
5                   Moves the cursor to record 5.0 
THRU                Begins selecting a block 
10                  The selected block is now 5.0 THRU 10.0 
SKIP 3 RECORDS      The selected block is now 5.0 THRU 
                    the third record after 10.0 
Compare the above sequence of commands with the following: 
5                   Moves the cursor to record 5.0 
THRU                Begins selecting a block 
10                  The selected block is now 5.0 THRU 10.0 
DI SKIP 3 RECORDS   Forgets the former selected block; 
                    the selected block is now the third 
                    record after record 10.0 
In serial editing mode, the DISPLAY command displays only the complete records 
constituting the selected block (through M$LO), and only if the verb DISPLAY 
is used explicitly. 
00002
00001
PLUS
PLUS
Syntax: 
{DO|!} command 
Parameters: 
command    specifies an IBEX-level command. 
Description: 
The DO command is used to call another processor from within 6Edit. 
00002
00001
Syntax: 
ED[IT] [BL[OCK]] block_expression 
Parameters: 
block_expression    is the block of data to be edited. 
Description: 
The EDIT command causes its operand to become the new "edit block."  The edit 
block is used by 6Edit in block expressions; it limits pattern searches, and 
is the implicit file in which you move the file pointer. 
The previous edit block is not forgotten.  Its specification remains in the 
edit block stack. 
The block_expression is not required to specify an entire file; however, the 
block it specifies must begin and end on record boundaries, that is, 
block_expression must specify some number of complete records. 
Sometimes it is convenient to limit file pointer movement to some sub-portion 
of the file.  EDITing a sub-portion of a file also limits the display of data 
around the file pointer, which can be useful when your terminal operates at a 
low speed (thus displaying data takes longer). 
The predefined name "CURRENT" is set by 6Edit automatically whenever the EDIT 
command is given.  The value of "CURRENT" is the location of the current edit 
block.  For example, the block expression "EO CURRENT" moves the file pointer 
to the end of the current edit block. 
You use the EDIT command when creating a new file.  Type the command 
    EDIT NEW FILE fid 
at the asterisk prompt. 
Example: 
EDIT FILE OPPORTUNITY_KNOCKS 
begins editing the file "OPPORTUNITY_KNOCKS".  An entry for this new edit 
block is added to the edit block stack. 
EDIT NEW FILE ACCEPTANCE_LETTER 
creates a new file "ACCEPTANCE_LETTER", and begins editing it.  An entry for 
this new edit block is added to the edit block stack. 
EDIT 50 THRU 15286 
edits a sub-portion of the current edit block.  Specifically, the new edit 
block starts at record 50.0 and continues through (and including) record 
15286.0.  An entry for this new edit block is added to the edit block stack. 
EDIT PREVIOUS 
reverts to editing the block whose specification was saved in the edit block 
stack immediately prior to the current edit block.  The edit block stack is 
not altered, but the "CURRENT" entry changes. 
Related Topics: 
Edit Block 
Edit Block Stack 
00002
00003
00001
00004
The editing window occupies the lower portion of your terminal screen (below 
the border line).  It displays records from the file being edited. 
Besides using the input editing functions, you can edit the data in the 
editing window using the editing commands. 
To move the cursor from the editing window to the command window, type 
<CNTL-C> (hold down the Control key, while typing the letter C once).  To 
return to the editing window without typing a command, type <CR> on an empty 
command line.  To type a command and leave the cursor in the command window, 
terminate the command with <CNTL-C>.  These functions may differ according to 
your context file. 
The stream name for the 6Edit editing window is the second lowest unused UC 
stream greater than UC09 (usually UC11).  Additional editing windows start at 
the next unused UC stream (usually UC12 and higher). 
The implicit subject of all editing operations is the "edit block."  The edit 
block is any set of records in any file.  It can comprise one record or an 
entire file.  Usually the edit block is all or a large portion of a file. 
You can edit less than an entire file, simply by telling 6Edit which portion 
of the file, or block, you want to edit.  This is useful when you want to 
limit editing operations to one portion of the file. 
You can set the edit block explicitly with the EDIT command; you can refer to 
it explicitly using the "CURRENT" predefined name. 
The default for all editing commands is to edit a block which is located 
entirely inside the edit block.  You can override this limitation, and specify 
a block anywhere in any file. 
When you specify a file, or some other block operand which is located outside 
the current edit block, 6Edit automatically changes the edit block to the 
specified file.  This is called an "implicit EDIT" because it is as though 
6Edit automatically inserted an EDIT command in front of the command you 
entered.  An implicit EDIT can occur during the following commands: 
    AFTER 
    DELETE 
    DISPLAY 
    LOCATION 
    OVER 
For example, assume you have typed the following command: 
    EDIT FILE ACCTS_PAYABLE 
The edit block is now all of file "ACCTS_PAYABLE".  If you type the command: 
    DISPLAY 23 
it displays record 23 from file ACCTS_PAYABLE.  Your search is limited to the 
material within the existing edit block only; 6Edit does not search for record 
23 before the first record, or beyond the last record of the current edit 
block. 
Now, you type this command: 
    DISPLAY FILE INVENTORY 23 
Because you explicitly specified a file, it becomes the new edit block; the 
command displays record 23 from file "INVENTORY", and the new edit block is 
all of file INVENTORY. 
Note that the following two commands have the same effect on the edit block: 
    EDIT FILE ACCTS_PAYABLE 
    DISPLAY FILE ACCTS_PAYABLE 
Contrast with this the very different effects of the following two commands on 
the edit block: 
    EDIT FILE ACCTS_PAYABLE 23 
    DISPLAY FILE ACCTS_PAYABLE 23 
The EDIT command in this example sets the edit block to just record 23 of file 
ACCTS_PAYABLE; the DISPLAY command in the example sets the edit block to all 
of the ACCTS_PAYABLE file, then displays record 23. 
When you change to a new edit block, the previous edit block is not forgotten. 
6Edit maintains an "edit block stack", which holds the specifications of 
previous edit blocks. 
The edit block stack has a pointer, which refers to the current edit block 
specification (the "CURRENT" predefined name).  When the edit block changes, 
either explicitly (EDIT command) or implicitly, 6Edit adds an entry to the 
edit block stack, and stores the specification of the new edit block in that 
entry. 
You can easily refer to the block specification in the previous entry in the 
edit block stack by using the PREVIOUS block operand in a block expression. 
The PREVIOUS block operand always changes the edit block, but instead of 
appending the new edit block specification to the end of the edit block stack, 
6Edit simply moves the edit block stack's pointer backward one entry.  The new 
edit block is the previous edit block specification from the edit block stack. 
Once you have used PREVIOUS, you can similarly use the NEXT block operand to 
advance the edit block stack's pointer.  The following examples illustrate 
responses generated by the edit block stack. 
Note that when you change to a new edit block, thus adding a new entry to the 
stack, any entries from the current entry to the end of the stack are removed 
from the stack.  Thus, you may not EDIT NEXT after introducing a new entry 
into the stack, since there is no longer a NEXT file in the stack. 
     You type:                 Edit Block Stack: 
                                ----------- 
     EDIT  FILE  ABC           | FILE  ABC | 
                                ----------- 
                                 current 
                                ----------------------- 
     EDIT  FILE  DEF           | FILE  ABC | FILE  DEF | 
                                ----------------------- 
                                             current 
                                ----------------------- 
     EDIT  PREVIOUS            | FILE  ABC | FILE  DEF | 
                                ----------------------- 
                                 current 
                                ----------------------- 
     EDIT  NEXT                | FILE  ABC | FILE  DEF | 
                                ----------------------- 
                                             current 
                                ----------------------------------- 
     EDIT  FILE  GHI           | FILE  ABC | FILE  DEF | FILE  GHI | 
                                ----------------------------------- 
                                                         current 
                                ----------------------------------- 
     EDIT  PREVIOUS            | FILE  ABC | FILE  DEF | FILE  GHI | 
                                ----------------------------------- 
                                             current 
                                ----------------------------------- 
     EDIT  PREVIOUS            | FILE  ABC | FILE  DEF | FILE  GHI | 
                                ----------------------------------- 
                                 current 
                                ----------------------- 
     EDIT  FILE  XYZ           | FILE  ABC | FILE  XYZ | 
                                ----------------------- 
                                             current 
IF
END
An "enclosed block" is one which is entirely contained within another block. 
The outer block is called the "enclosing block"; the enclosed block is the 
block being specified, which is located entirely inside the enclosing block. 
To specify an enclosed block, follow the specification of the enclosing block 
with the SELECT clause, followed by the specification of the enclosed block. 
(If the edit block is the enclosing block, then the SELECT clause is not 
necessary, unless a repeated block is desired.) 
Enclosed blocks are useful when you want to limit the movement of the file 
pointer to some block smaller than the edit block.  The edit block always 
limits all file pointer movement. 
Example: 
Assume you want to insert a string of characters "xxx" at the beginning of 
every record between records 10.0 and 50.0, inclusive.  To do this, you type 
the following commands. 
COPY STRING 'xxx' 
AFTER 10 THRU 50 REPEAT SELECT RECORD SELECT BO RECORD 
The first command, COPY STRING 'xxx', sets up the source block for the copy 
operation. 
The AFTER command contains a complex block expression, including both enclosed 
blocks and repeated blocks: 
10 THRU 50 
First, the enclosing block is specified:  the block comprising records 10.0 
through 50.0 inclusive in the current edit block. 
REPEAT SELECT RECORD 
is a repeated block expression, specifying a block for every record between 
10.0 through 50.0.  A repeated block specification evaluates to several 
blocks; these blocks are enclosed within the enclosing block.  In this case, 
the enclosing block is 10.0 through 50.0; the enclosed blocks will be each 
whole record which appears in the enclosing block. 
SELECT BO RECORD 
specifies an enclosed block:  an empty block at the start of each record. 
Note that each block specified in the previous step becomes the enclosing 
block for this step. 
00001
Syntax: 
{E[ND]|EX[IT]|Q[UIT]|X[IT]} 
Parameters: 
None 
Description: 
This command terminates 6Edit.  Control is returned to the command processor 
(IBEX). 
The keywords, END, EXIT, QUIT, and XIT perform exactly the same function.  All 
editing changes you made during an editing session take effect when you change 
the record.  Therefore, you can terminate 6Edit at any time without losing any 
of the editing work you have done. 
However, any name settings (such as KEYINS, SYNONYMS, EQUALS, and LOCATION 
names) that you made during the session will be lost when you type the END 
command and leave 6Edit. 
00002
00001
Syntax: 
{EN[D] OF|EO} block_operand 
Parameters: 
block_operand    may be any absolute or relative block operand, possibly 
modified by other block options (only one of the three "point" options -- ALL 
OF, BEGINNING OF, and END OF -- may be used with a block_operand). 
Description: 
END OF tells 6Edit to move the file pointer to the end of block_operand.  For 
instance, if block_operand was a block comprising three records, END OF tells 
6Edit to move the file pointer to the first character of the record following 
the three-record block. 
00002
00001
END_OF
Syntax: 
                                [   {CO[MMAND] [WI[NDOW]] }] 
name EQ[UALS] string_expression [IN {ED[ITING] [WI[NDOWS]]}] 
                                [   {WI[NDOW] window_num  }] 
Parameters: 
name    is any name; it must be between 1 and 31 characters in length.  The 
"name" may include: 
    o   Alphabetic characters 
    o   Digits (except as the first character of name) 
    o   $  _  #  and  @ 
string_expression    is any string expression. 
window_num    is a number between 1 and the number of editing windows. 
Description: 
The EQUALS command assigns the value of string_expression to name.  The name 
may be a predefined name, a name you previously created with an assignment 
command, or a new name you are creating now. 
When you type an EQUALS command, 6Edit evaluates string_expression to yield a 
string of characters.  (If numbers were used or computed in string_expression, 
6Edit converts them to character form using decimal representation.)  6Edit 
assigns this character string to name.  Thereafter, name can be used in string 
or block expressions; 6Edit replaces it with the character string which was 
assigned to it by this EQUALS command. 
Note:  Except when name is $INTRO_1 or $INTRO_2, $CONTROL functions in the 
character string are not interpreted when assigned but only when the resulting 
variable is used in a different command. 
The value of name will not change until you explicitly assign a new value to 
it.  (Certain predefined names disobey this rule; 6Edit updates their values 
internally at certain points in the processing of commands.) 
The IN-clause can be appended to the EQUALS command only when name is one of 
the following predefined names: 
    $AUTOTAB                     $KEY_GENERATION 
    $END_MARK                    $ONESPACEEDIT 
    $EZ_APPEND                   $RECORDWRAP 
    $HSALL                       $SCROLL 
    $HSCROLL                     $TEXTEDIT 
    $HSCROLL_MARGIN              $VSCROLL 
    $INSERT                      $VSCROLL_MARGIN 
    $INTRO_1                     $WORDWRAP 
    $INTRO_2 
If you include the IN-clause when assigning a value to one of these predefined 
names, then the value affects only the command or editing window, depending on 
which is specified.  If you omit the IN-clause when assigning a value to one 
of these predefined names, then the value affects both the command and editing 
windows.  Note that $SCROLL works only in the command window.  "IN EDITING 
WINDOW" causes all editing windows to be affected.  "IN WINDOW window_num" 
affects only the specified window. 
Example: 
MODEL EQUALS MODEL .PLUS. 3 
increments the value of MODEL (a hypothetical name you have already defined) 
by 3. 
$WORDWRAP EQUALS 76 
sets the value of the predefined name $WORDWRAP to 76 (i.e., enables wordwrap 
mode, limiting lines to 76 characters). 
$HSCROLL_MARGIN EQUALS 5 IN COMMAND WINDOW 
enables horizontal scrolling in the command window only.  It does not affect 
horizontal scrolling in the editing window. 
$INTRO_1 EQUALS $KEY(F4) 
sets the primary introducer for KEYIN names to $KEY(F4).  This permits 
definitions of keyins such as KEYIN $KEY(F4)||'R' IS ... to establish the 
actions taken when you type F4 followed by R.  For more information on the use 
of KEYIN and the $KEY(keyname) predefined string function, enter: 
    HELP (6EDIT) KEYIN 
Related Topics: 
Substitution 
00002
00003
00001
00004
Syntax: 
ERASE [ALL|ldevlist] 
Parameters: 
ALL    specifies that the accumulated outputs for all logical devices are to 
be deleted.  This is the default. 
ldevlist    specifies that the accumulated outputs for the specified logical 
device or devices are to be deleted.  The list is entered in the format 
    ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
ERASE deletes the accumulated output for logical devices. 
Example: 
ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
Related Commands: 
PRINT 
00002
00003
00001
00004
Following is a list of input editing functions available when the cursor is in 
the editing window. 
ESC_A               ESC_O               ESC_LESS_THAN 
ESC_B               ESC_P               ESC_GREATER_THAN 
ESC_CNTL_B          ESC_Q               ESC_UPARROW 
ESC_C               ESC_R               ESC_BS 
ESC_D               ESC_CNTL_R          ESC_CR 
ESC_CNTL_D          ESC_S               ESC_LF 
ESC_E               ESC_T               ESC_ESC 
ESC_G               ESC_U               ESC_DEL 
ESC_H               ESC_V               CNTL_H 
ESC_value_H         ESC_CNTL_W          CNTL_I 
ESC_HT              ESC_X               CNTL_J 
ESC_I               ESC_Y               CNTL_M 
ESC_J               ESC_APOSTROPHE      CNTL_R 
ESC_K               ESC_*               CNTL_X 
ESC_CNTL_K          ESC_COLON           CNTL_W 
ESC_CNTL_L          ESC_.               CNTL_Y 
ESC_M               ESC_LEFT_PAREN      DEL 
ESC_value_M         ESC_RIGHT_PAREN     BREAK 
ESC_N               ESC_DASH 
For more information about a specific input editing function, type: 
HELP ESC_AND_CNTL_FUNCTIONS function 
For example: 
HELP ESC_AND_CNTL_FUNCTIONS ESC_B 
or 
HELP ESC_AND_CNTL_FUNCTIONS CNTL_X 
Note that the right and left parenthesis, dash, apostrophe, colon, and 
uparrow characters must be spelled out.  For example, 
HELP ESC_AND_CNTL_FUNCTIONS ESC_RIGHT_PAREN 
  Name       Function 
  <ESC> <A> 
             When the cursor is in the 6Edit editing window:  move the cursor 
             up one record.  When the cursor is in the 6Edit command window: 
             toggle pagehalt.  (Note, however, that 6Edit continuously toggles 
             pagehalt in the command window automatically, overriding your 
             selection.)  In the editing window only: <ESC> <n> <A> moves the 
             cursor up "n" records.  The n parameter is any 1 or 2 decimal 
             digits. 
  <ESC> <B> 
             In the 6Edit editing window:  move cursor down one record.  In 
             the 6Edit command window:  simulate Break function.  In the 
             editing window only:  <ESC> <n> <B> moves the cursor down "n" 
             records.  The n parameter is any 1 or 2 decimal digits. 
  <ESC> <CNTL-B> 
             Simulates the Break function.  Does not delete typeahead. 
  <ESC> <C> 
             In the 6Edit editing window:  move cursor right one position 
             (same as <CNTL-R>).  In the 6Edit command window:  toggles 
             relative tabbing mode.  In the editing window only:  <ESC> <n> 
             <C> moves the cursor right "n" positions.  The n parameter is any 
             1, 2, 3, or 4 decimal digits. 
  <ESC> <D> 
             In the 6Edit editing window:  move cursor left one position (same 
             as <BS>).  In the 6Edit command window:  recalls the last saved 
             input record.  In the editing window only:  <ESC> <n> <D> moves 
             the cursor left "n" positions.  The n parameter is any 1, 2, 3, 
             or 4 decimal digits. 
  <ESC> <CNTL-D> 
             Recall last input saved in command or IBEX window. 
  <ESC> <n> <E> 
             Position to the top, middle, or bottom of the window for n less 
             than, equal to, or greater than one, respectively. 
  <ESC> <G> 
             Display FEP information. 
  <ESC> <H> 
             Halt output immediately.  Type <CR> to resume output. 
  <ESC> <n> <H> 
             Set HSSHIFT (the number of columns that an input image is to be 
             shifted) to the value n.  For this sequence to work, the $HSCROLL 
             predefined name must be set non-zero. 
  <ESC> <I> 
             Simulate Tab. 
             <ESC> <n> <I> moves the cursor to position "n" of the current 
             record.  <ESC> <-> <I> moves the cursor to the previous tab stop. 
             The n parameter is any 1, 2, 3, or 4 decimal digits. 
  <ESC> <J> 
             Define or reset the insertion window. 
  <ESC> <K> 
             Delete record (or insertion window) to right of cursor. 
  <ESC> <CNTL-K> 
             Delete record (or insertion window) to left of cursor. 
  <ESC> <CNTL-L> 
             Delete record, leaving the cursor at the next record. 
  <ESC> <M> 
             Set replacement mode.  Resets overstrike and insertion mode. 
  <ESC> <n> <M> 
             Set HSMARGIN (the closest the cursor is to be allowed to approach 
             the end of an input area) to the value n.  For this sequence to 
             work, the $HSCROLL predefined name must be set non-zero. 
  <ESC> <N> 
             Move cursor to the end of record (or insertion window). 
  <ESC> <O> 
             Set overstrike mode.  Resets replacement and insertion modes. 
  <ESC> <P> 
             Recall record as it was when the cursor was last moved onto 
             record.  This function is only available in the 6Edit editing 
             window.  <ESC> <n> <P> copies the nth record below the current 
             record over the current record. 
             <ESC> <n> <-> <P> copies the nth record above the current record 
             over the current record.  The n parameter is any 1 or 2 decimal 
             digits. 
  <ESC> <Q> 
             Display system status. 
  <ESC> <R> 
             Retype record; reset insertion window. 
             <ESC> <n> <R> resets the parameter identified by "n" (turns off 
             the parameter).  The n parameter is any 1 or 2 decimal digits. 
             The table below lists the values for n: 
                 n   Meaning 
                --   --------------------------------------------- 
                 1   Autotab mode (see $AUTOTAB under PREDEFINED_NAMES). 
                     Can only be used to disable autotabing. 
                     Setting this parameter (via <ESC> <1> <S>) or 
                     toggling the parameter on (via <ESC> <1> <T>) 
                     has the same effect as <ESC> <1> <R> -- 
                     the parameter is reset. 
                 2   Insert mode (see $INSERT under PREDEFINED_NAMES). 
                 3   Message line for operator messages. 
                 4   Wordwrap mode (see $WORDWRAP under PREDEFINED_NAMES). 
                     Can only be used to disable wordwrap mode.  Setting 
                     this parameter (via <ESC> <4> <S>) or toggling 
                     the parameter on (via <ESC> <4> <T>) has the same 
                     effect as <ESC> <4> <R> -- the parameter is reset. 
                 5   Search to the right.  Establishes the direction for 
                     word and character searches. 
                 6   Truncate mode (see the IBEX TERMINAL command). 
                 7   Actontrn (see the IBEX TERMINAL command). 
                 8   Wordwrap toggle (see $WORDWRAP under PREDEFINED_NAMES). 
                     Resetting this parameter disables wordwrap mode 
                     but remembers the column.  Setting this parameter 
                     enables wordwrap mode at the remembered column. 
                 9   Recordwrap mode (see $RECORDWRAP under PREDEFINED_NAMES). 
                10   Textedit mode.  Attempts to preserve spaces 
                     between words when splitting and joining records. 
                11   Easyappend.  Allows records to be appended to the 
                     end of the file simply by moving the cursor down 
                     past the end-of-file position. 
                12   Changecase.  Makes forward cursor movement change 
                     the case of the characters under it. 
                13   Parkcursor.  Moves the cursor to the window's home 
                     position when activation occurs in screen-editing 
                     mode. 
             The following values of "n" are only available in the command 
             window: 
                 n   Meaning 
                --   ------------------- 
                20   Overstrike mode 
                21   Echo 
                22   Paritycheck 
                23   Outputdiscard 
                24   Uppercase 
                25   Apllcnrm 
                26   Retypovr 
                27   Editovr 
                29   Pagehalt 
                30   Printhalt 
                31   Relpage 
                32   Simper 
                33   Nooptimiz 
                34   Wrappage 
                35   Localech 
                36   Messagehalt 
                37   Autocursor 
                38   Truovrprt 
                39   Cursorread 
                40   Keeptypahd 
             See the IBEX TERMINAL command for descriptions of these 
             parameters. 
             The following values of "n" are available only in the command 
             window, and when FCNTBL=CP5: 
                 n   Meaning 
                --   ----------------- 
                50   Tabsim 
                51   Tabrelative 
                52   Spaceinsert 
                53   Lowercase 
                54   Fullduxpapertape 
                55   Halfduxpapertap 
             See the IBEX TERMINAL command for descriptions of these 
             parameters. 
  <ESC> <CNTL-R> 
             Reset insertion window. 
  <ESC> <n> <S> 
             Sets the parameter identified by "n" (turns on the parameter). 
             The n parameter is any 1 or 2 decimal digits.  See ESC_R for the 
             table of values for n. 
  <ESC> <n> <T> 
             Toggles the parameter identified by "n".  If the parameter was 
             set, it will be reset; if it was reset, it will be set.  The n 
             parameter is any 1 or 2 decimal digits.  See ESC_R for the table 
             of values for n. 
  <ESC> <U> 
             Toggle uppercase restriction. 
  <ESC> <V> 
             Search record (or insertion window) for character. 
  <ESC> <CNTL-W> 
             Delete word, beginning with the character under the cursor, and 
             proceeding to the right, up to the beginning of the next word. 
  <ESC> <X> 
             Erase contents of record. 
  <ESC> <Y> 
             Monitor attention. 
  <ESC> <'> 
             Set insertion mode.  Resets overstrike and replacement modes. 
  <ESC> <*> 
             Save contents of the insertion window. 
  <ESC> <:> 
             Recall the data saved by the last <ESC> <*> function. 
  <ESC> <.> 
             When more than one session has been started on this terminal, 
             <ESC> <.> moves the cursor to the next session reading from the 
             terminal. 
  <ESC> <(> 
             Enter lowercase shift. 
  <ESC> <)> 
             Exit lowercase shift. 
  <ESC> <-> 
             Redisplay entire editing window.  This function is only available 
             in the 6Edit editing window. 
  <ESC> <>> and <<> 
             Set limits of insertion window. 
  <ESC> <^> 
             Set wordwrap column. 
             <ESC> <n> <^> sets the wordwrap mode column to position "n".  The 
             n parameter is any 1, 2, 3, or 4 decimal digits.  For example, 
             <ESC> <8> <@> sets the wordwrap column to position 8. 
  <ESC> <BS> 
             If cursor is at beginning of record, join record to previous 
             record.  If cursor is at end of record, join next record to 
             current record.  This function is only available in the 6Edit 
             editing window. 
  <ESC> <HT> 
             Set autotab column. 
             <ESC> <n> <HT> sets the autotab column to position "n".  The n 
             parameter is any 1, 2, 3, or 4 decimal digits. 
  <ESC> <CR> 
             Move cursor to beginning of record (or insertion window). 
  <ESC> <LF> 
             In the 6Edit editing window:  split record, inserting the portion 
             of the record to the right of the cursor as a new record to 
             follow the current record.  In the 6Edit command window:  local 
             linefeed. 
             In the editing window only:  <ESC> <2> <LF> will fill or shorten 
             the current record to the wordwrap column.  If the record is 
             shorter than the wordwrap column, words from the next record will 
             be moved onto the current record.  If the record is longer than 
             the wordwrap column, it will be split near the wordwrap column. 
             (See $WORDWRAP under PREDEFINED_NAMES.) 
             In the editing window only:  <ESC> <1> <LF> will perform the 
             <ESC> <2> <LF> actions repeatedly until the cursor reaches the 
             next paragraph, or the bottom of the editing window. 
  <ESC> <ESC> 
             Monitor attention (same as <ESC> <Y>). 
  <ESC> <DEL> 
             Delete the character to the left of the cursor; if at the 
             beginning of record, do nothing. 
             If the recordwrap mode is set and the cursor is at the beginning 
             of the record, acts like <ESC> <BS>.  It joins the current record 
             to the previous record.  (See $RECORDWRAP under 
             PREDEFINED_NAMES). 
  <CNTL-H> 
             (BS) 
             Move cursor left one position; if at the beginning of record, 
             action depends on the record wrap mode (see $RECORDWRAP).  If the 
             record wrap mode is disabled (the initial setting) or the cursor 
             is in the command window, <CNTL-H> when at the beginning of a 
             record does nothing.  If the record wrap mode is enabled and the 
             cursor is in the editing window, <CNTL-H> when at the beginning 
             of a record moves the cursor to just beyond the end of the 
             previous record. 
  <CNTL-I> 
             (TAB) 
             Move cursor to the next tab stop.  Extend record if necessary. 
  <CNTL-J> 
             (LF) 
             In the 6Edit editing window:  move cursor down one record (same 
             as <ESC> <B>).  In the 6Edit command window:  activates a command 
             entry. 
  <CNTL-M> 
             (CR) 
             In the 6Edit editing window:  move cursor to the beginning of the 
             next record.  If at the end of the file, append a zero-length 
             record to the file.  In the 6Edit command window:  activates a 
             command entry. 
  <CNTL-R> 
             (DC2) 
             Move cursor right one position; if at the end of record, action 
             depends on the record wrap mode (see $RECORDWRAP).  If the record 
             wrap mode is disabled (the initial setting) or the cursor is in 
             the command window, <CNTL-R> when at the end of a record appends 
             a space character to the record.  If the record wrap mode is 
             enabled and the cursor is in the editing window, <CNTL-R> when at 
             the end of a record moves the cursor to the beginning of the next 
             record. 
  <CNTL-U> 
             (NAK) 
             Move cursor right one character, changing the case of the 
             character under the cursor. 
  <CNTL-X> 
             (CAN) 
             Same as <ESC> <X>, but acts immediately.  (Also deletes typeahead 
             and queued output.) 
  <CNTL-W> 
             (ETB) 
             Move cursor to the next or previous word, depending on current 
             direction, set by the last <BS> or <CNTL-R>. 
  <CNTL-Y> 
             (EM) 
             Monitor attention.  (Also deletes typeahead and queued output.) 
  <DEL> 
             Delete character under cursor.  If in the replacement mode and at 
             end of record (or insertion window), delete character to left of 
             cursor; if in the insertion mode and at end of record (or 
             insertion window), <DEL> is ignored. 
  <BREAK> 
             Interrupt program. 
00056
00046
00047
00048
00049
00050
00051
00053
00052
00054
00055
00032
00034
00001
00031
00002
00040
00004
00003
00006
00014
00015
00023
00028
00033
00042
00005
00037
00045
00007
00044
00008
00038
00009
00041
00011
00012
00013
00035
00038
00043
00016
00018
00019
00020
00021
00022
00036
00024
00025
00026
00039
00027
00010
00017
00029
00030
The evaluation options tell 6Edit how to evaluate the block operand with which 
they are specified, that is, how to move the file pointer through the file 
looking for an instance of the block operand. 
In a command line, the evaluation options are typed before the block operand 
to which they apply. 
o   The point option specifies to what point in the block operand the file 
    pointer is to be moved.  ALL OF moves the file pointer to either the start 
    or the end of the block operand, as appropriate, and selects the entire 
    block operand.  BEGINNING OF always moves the file pointer to the 
    beginning of the block operand.  END OF always moves the file pointer to 
    the end of the block operand.  Both of the latter select only the end 
    point of the operand.  The default is $POINT. 
o   The direction option tells 6Edit in which direction the file pointer is to 
    be moved from its current location, forward or backward.  The default is 
    $DIRECTION. 
o   The skip option specifies which instance of a relative block operand is to 
    be located.  For example, if you specify a skip option (with its skip 
    count) with a pattern-string block operand, then 6Edit does not treat the 
    first match of the pattern string as the block operand, but instead the 
    "nth" match (where "n" is the skip count).  The default is $SKIP. 
END
6Edit commands involve two types of expressions: string expressions and block 
expressions. 
Syntax: 
[ { NE[W] }  { ST[RING]KEY  } ] 
[ { OL[D] }  { SE[QUENTIAL] } ] FI[LE] fid 
[ { AN[Y] }  { ED[IT]KEY    } ] 
Parameters: 
fid    is a CP-6 file identifier and must refer to a file. 
Description: 
The FILE operand specifies a certain file to be the enclosing block for the 
rest of the block expression. 
NEW tells 6Edit that fid must specify a file that does not exist.  6Edit will 
create the file as an edit-keyed file.  $FILETYPE specifies the value to use 
for the type attribute of the new file. 
OLD tells 6Edit that fid must specify a file which currently exists. 
ANY tells 6Edit to create the specified file if it does not already exist. 
STRINGKEY tells 6Edit that the file to be created or modified must have keys, 
and that the keys are presumed to be textual names.  Insertion of new records 
is permitted only if the key of the new record is explicitly specified. 
Record keys are specified using the KEY option. 
SEQUENTIAL tells 6Edit that the file to be created or modified must be 
unkeyed.  Records may be added or deleted only at the end of the file.  Record 
keys are sequential record numbers starting at 1. 
EDITKEY tells 6Edit that the file to be created or modified must have standard 
(3-byte) edit keys.  Records may be inserted or deleted anywhere.  Record keys 
must evaluate to 3-place decimal numbers up to 99999.999. 
The FILE block operand may not be modified by the following block options: 
    SKIP 
    FORWARD 
    BACKWARD 
The default "point" option for the FILE block operand is ALL OF, regardless of 
the current value of $POINT.  To begin editing a file at its end, use two 
commands:  EDIT FILE fid; EO CURR  . 
Example: 
COPY REPEAT SELECT SKIP 2 'The %? we sold' AFTER ANY FILE SALES 
creates the file SALES if it does not already exist, then searches forward in 
the current edit block for matches of the pattern "The %? we sold", and copies 
every other such match to the end of the SALES file starting with the second 
match.  After searching to the end of the current edit block, 6Edit displays 
the SALES file in the editing window. 
00002
00003
00001
6Edit keeps track of a "file pointer" which "points" to a location in a file. 
You can move the file pointer in three ways: 
o   When full-screen editing, the cursor is effectively the file pointer. 
    When you move the cursor (with, for example, the backspace key on the 
    terminal), you are moving 6Edit's file pointer. 
o   You can use the terminal's function keys to move the file pointer, by 
    moving forward or backward in a file in units of characters, words, 
    records, matches of a pattern string, etc.  You must first tell 6Edit what 
    the terminal's function keys mean, usually in a "context file." 
o   You can enter commands to move the file pointer in the same way as the 
    terminal function keys.  (Actually, the terminal function keys simply 
    generate commands; anything you can do with commands, you can make your 
    terminal function keys do).  You can also enter commands to move the file 
    pointer to a specific file, or a record within a file, by typing the 
    specific file name and/or record key in a command. 
Syntax: 
FO[RWARD] relative_block 
Parameters: 
relative_block    must be a relative block operand. 
Description: 
FORWARD tells 6Edit in which direction in the file to move the file pointer 
when searching for a relative block operand. 
Relative_block must be a record, position, or pattern-string operand; 6Edit 
moves the file pointer forward in the file (toward the end of the file) 
accordingly. 
00002
00001
Format: 
H[ELP] [(fid)] [TOPICS] [keyword1 [-] [keyword2] 
Note:  The following elements can be specified in any order: 
         (fid) 
         TOPICS 
         [keyword1] [-] [keyword2] 
For example, HELP (fid) keyword1  - keyword2 TOPICS is acceptable. 
Parameters: 
(fid)    specifies the processor name (for example, 6EDIT).  If (fid) is 
omitted, the current processor is assumed. 
TOPICS    requests a list of topic or subtopic names, rather than an 
information message. 
Form                                     Result 
HELP (fid) TOPICS                        Lists all topics 
HELP (fid) TOPICS keyword1 - keyword2    Lists all topics in the range 
                                         specified by keyword1 - keyword 2 
HELP (fid) TOPICS keyword1?              Lists all topics beginning with 
                                         the prefix specified by keyword1 
HELP (fid) TOPICS keyword1               Lists all subtopics for the 
                                         topic specified by keyword1 
keyword1 [- [keyword2]]    specifies a topic, a range of topics, or a topic 
and subtopic to identify what HELP information is requested. 
Form                                     Result 
HELP (fid) keyword1                      Displays the first level 
                                         information message for 
                                         the topic keyword1 
HELP (fid) keyword1 keyword2             Displays the information 
                                         message for keyword1, but only 
                                         the level identified by the 
                                         subtopic keyword2 
HELP (fid) TOPICS keyword1 [-] [keyword2]Lists topic or subtopic 
                                         names.  See TOPICS parameter. 
keyword1 may include the wildcard (?) character as the rightmost character, if 
TOPICS is specified. 
Description: 
HELP displays information. 
HELP messages have levels.  Once the initial level has been displayed, 
entering a question mark displays the next level, usually containing greater 
detail.  Entering two question marks displays the entire message. 
The standard HELP command is provided by most processors.  The HELP facility 
for each processor is available only to users with sufficient privilege to use 
the processor itself.  The HELP command can be used either within the 
processor or in IBEX. 
00002
00001
HELP
A 
  Abbreviations - 
      HELP KEYWORDS_AND_ABBREVIATIONS 
  Absolute Block Operands -   
    FILE - 
      HELP ABSOLUTE_BLOCK_OPERANDS 
    Location_Name - 
      HELP ABSOLUTE_BLOCK_OPERANDS 
    NEXT - 
      HELP ABSOLUTE_BLOCK_OPERANDS 
    PREVIOUS - 
      HELP ABSOLUTE_BLOCK_OPERANDS 
    Record_Key - 
      HELP ABSOLUTE_BLOCK_OPERANDS 
    STRING - 
      HELP ABSOLUTE_BLOCK_OPERANDS 
  Absolute Block Operands - 
      HELP ABSOLUTE_BLOCK_OPERANDS 
  ADJUST Clause - 
      HELP ADJUST 
      HELP ADJUST DESCRIPTION: 
  AFTER Command - 
      HELP AFTER 
  ALL OF Option - 
      HELP ALL_OF 
  ANY - 
      HELP PREDEFINED_NAMES ANY 
  AO - 
      HELP PREDEFINED_NAMES AO 
  Arithmetic Operators - 
      HELP PLUS 
  $AUTOTAB - 
      HELP PREDEFINED_NAMES $AUTOTAB 
B 
  BACKWARD - 
      HELP PREDEFINED_NAMES BACKWARD 
  BACKWARD Option - 
      HELP BACKWARD 
  BEGINNING OF Option - 
      HELP BEGINNING_OF 
      HELP BEGINNING_OF EXAMPLE: 
  BIN10 - 
      HELP PREDEFINED_NAMES BIN10 
  BIN521 - 
      HELP PREDEFINED_NAMES BIN521 
  BINHLF - 
      HELP PREDEFINED_NAMES BINHLF 
  Block Expressions - 
      HELP BLOCK_EXPRESSIONS 
  Block Operands - 
      HELP USING_BLOCK_EXPRESSIONS 
  Block Operators - 
      HELP USING_BLOCK_EXPRESSIONS 
  Block Options - 
      HELP BLOCK_OPTIONS 
  Blocks - 
      HELP BLOCKS 
  BO - 
      HELP PREDEFINED_NAMES BO 
  Building a File - 
      HELP EDIT DESCRIPTION: 
  $BY - 
      HELP PREDEFINED_NAMES $BY 
  BY Option - 
      HELP BY 
C 
  $CASE - 
      HELP PREDEFINED_NAMES $CASE 
  Changes Since Last Release - 
      HELP CHANGES 
  $CNTL - 
      HELP PREDEFINED_STRING_FUNCTIONS $CNTL 
  $COMMAND - 
      HELP PREDEFINED_NAMES $COMMAND 
  Command Lines and Continuation - 
      HELP COMMAND_LINES 
  Command Stream - 
      HELP COMMAND_LINES 
  Command Summary - 
      HELP COMMANDS 
  Command Window - 
      HELP COMMAND_WINDOW 
  $COMMENT - 
      HELP PREDEFINED_NAMES $COMMENT 
  $COMMENT identifier - 
      HELP LEXICAL_FUNCTIONS 
      HELP $COMMENT 
      HELP $COMMENT 
  $COMMENT predefined name - 
      HELP LEXICAL_FUNCTIONS 
  Compound Blocks -   
    Enclosed Blocks - 
      HELP COMPOUND_BLOCKS 
    Repeated Blocks - 
      HELP COMPOUND_BLOCKS 
  CONCATENATE Operator - 
      HELP CONCATENATE 
  $CONTEXT - 
      HELP PREDEFINED_NAMES $CONTEXT 
  Context File - 
      HELP FILE_POINTER 
  Context Files -   
    DECVT100 Context File - 
      HELP CONTEXT_FILE 
    Example PCTX364 Context File - 
      HELP CONTEXT_FILE 
    Standard Context File - 
      HELP CONTEXT_FILE 
    VIP7205 Context File - 
      HELP CONTEXT_FILE 
    VIP7801/VIP7802 Context File - 
      HELP CONTEXT_FILE 
    Zenith Z19 Context File - 
      HELP CONTEXT_FILE 
  $CONTROL - 
      HELP PREDEFINED_NAMES $CONTROL 
  $CONTROL Functions -   
    $CONTROL-Beginning of Match - 
      HELP $CONTROL_BEGINNING_OF_MATCH 
    $CONTROL-End of Match - 
      HELP $CONTROL_END_OF_MATCH 
    $CONTROL-Literal Function - 
      HELP $CONTROL_LITERAL EXAMPLE: 
    $CONTROL-Question Function - 
      HELP $CONTROL_QUESTION_PATT 
    $CONTROL-Record Function - 
      HELP $CONTROL_RECORD EXAMPLE: 
      HELP STRING DESCRIPTION: 
    $CONTROL-Value Function - 
      HELP $CONTROL_VALUE EXAMPLE: 
      HELP KEYIN DESCRIPTION: 
      HELP $CONTROL_VALUE_PATT 
    $CONTROL-Wildcard Function - 
      HELP $CONTROL_WILDCARD_PATT 
  $CONTROL identifier - 
      HELP LEXICAL_FUNCTIONS 
      HELP $CONTROL 
      HELP $CONTROL 
  $CONTROL predefined name - 
      HELP LEXICAL_FUNCTIONS 
  $CONTROL-Beginning of Match Pattern Function - 
      HELP $CONTROL_BEGINNING_OF_MATCH 
  $CONTROL-End of Match Pattern Function - 
      HELP $CONTROL_END_OF_MATCH 
  $CONTROL-Literal Function - 
      HELP $CONTROL_LITERAL 
  $CONTROL-Question Pattern Function - 
      HELP $CONTROL_QUESTION_PATT 
  $CONTROL-Record Function - 
      HELP $CONTROL_RECORD 
  $CONTROL-Value Function - 
      HELP $CONTROL_VALUE 
  $CONTROL-Value Function in the Pattern String - 
      HELP $CONTROL_VALUE_PATT 
  $CONTROL-Wildcard Pattern Function - 
      HELP $CONTROL_WILDCARD_PATT 
  Copy and Move Operations - 
      HELP COPY_AND_MOVE_OPERATIONS 
  COPY Command - 
      HELP COPY 
  Creating a New File - 
      HELP EDIT DESCRIPTION: 
  CURRENT - 
      HELP PREDEFINED_NAMES CURRENT 
  CURRENT Name - 
      HELP EDIT_BLOCK 
D 
  DATE Command - 
      HELP DATE 
  DCBs - 
      HELP DCBS 
  DELETE Command - 
      HELP DELETE 
  Deleting Characters - 
      HELP DELETING_CHARACTERS 
  Deleting Files - 
      HELP DELETE DESCRIPTION: 
  Deleting Records from a File - 
      HELP SPLITTING_AND_JOINING_RECORDS 
  $DIRECTION - 
      HELP PREDEFINED_NAMES $DIRECTION 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DISPLAY Command - 
      HELP DISPLAY 
  DO Command - 
      HELP DO 
  DONT_PROTECT - 
      HELP PREDEFINED_NAMES DONT_PROTECT 
E 
  Edit Block - 
      HELP EDIT_BLOCK 
  Edit Block Stack - 
      HELP EDIT_BLOCK_STACK 
  EDIT Command - 
      HELP EDIT_BLOCK 
      HELP EDIT 
      HELP EDIT DESCRIPTION: 
  Editing Window - 
      HELP EDITING_WINDOW 
  Enclosed Blocks - 
      HELP ENCLOSED_BLOCKS 
  END - 
      HELP END DESCRIPTION: 
  END OF Option - 
      HELP END_OF 
  END, EXIT, QUIT and XIT Commands - 
      HELP END 
  $END_MARK - 
      HELP PREDEFINED_NAMES $END_MARK 
  EO - 
      HELP PREDEFINED_NAMES EO 
  EQUALS Command - 
      HELP EQUALS 
  EQUALS-Values - 
      HELP SUBSTITUTION 
  ERASE Command -   
    IBEX - 
      HELP ERASE SYNTAX: 
  ERASE Command - 
      HELP ERASE 
  Escape Sequences - 
      HELP ESC_AND_CNTL_FUNCTIONS 
  Evaluation Options -   
    Direction - 
      HELP EVALUATION_OPTIONS 
    Point - 
      HELP EVALUATION_OPTIONS 
    Skip - 
      HELP EVALUATION_OPTIONS 
  Evaluation Options - 
      HELP EVALUATION_OPTIONS 
  $EXIST - 
      HELP PREDEFINED_NAMES $EXIST 
  EXIT - 
      HELP END DESCRIPTION: 
  Expressions -   
    Block Expressions - 
      HELP BLOCK_EXPRESSIONS 
  Expressions - 
      HELP EXPRESSIONS 
  $EZ_APPEND - 
      HELP PREDEFINED_NAMES $EZ_APPEND 
F 
  FILE Block Operand - 
      HELP FILE 
  File Pointer - 
      HELP FILE_POINTER 
      HELP SPECIFYING_A_BLOCK 
      HELP SELECTED_BLOCK 
  $FILEORG - 
      HELP PREDEFINED_NAMES $FILEORG 
  FILERECORDS - 
      HELP PREDEFINED_NAMES $FILERECORDS 
  $FILETYPE - 
      HELP PREDEFINED_NAMES $FILETYPE 
  FORWARD - 
      HELP PREDEFINED_NAMES FORWARD 
  FORWARD Block Operand - 
      HELP FORWARD DESCRIPTION: 
  FORWARD Option - 
      HELP FORWARD 
  Function Key and Control Key Notation - 
      HELP KEY_NOTATION 
  Function Keys - 
      HELP KEYIN DESCRIPTION: 
G 
  General Form of Block Expressions - 
      HELP BLOCK_EXPRESS_SYNTAX 
H 
  HELP Command - 
      HELP HELP 
  HERE - 
      HELP PREDEFINED_NAMES HERE 
  Horizontal Scroll Margins - 
      HELP HORIZONTAL_SCROLL_MARGINS 
  $HSALL - 
      HELP PREDEFINED_NAMES $HSALL 
  $HSCROLL - 
      HELP PREDEFINED_NAMES $HSCROLL 
  $HSCROLL_MARGIN - 
      HELP PREDEFINED_NAMES $HSCROLL_MARGIN 
I 
  IBEX Window - 
      HELP IBEX_WINDOW 
  Identifiers -   
    $COMMENT - 
      HELP LEXICAL_FUNCTIONS 
      HELP $COMMENT 
    $CONTROL - 
      HELP LEXICAL_FUNCTIONS 
      HELP $CONTROL 
  IF and ELSE Commands - 
      HELP IF 
  Implicit EDIT - 
      HELP EDIT_BLOCK 
  $INITIALIZE - 
      HELP PREDEFINED_NAMES $INITIALIZE 
  Input Editing Functions - 
      HELP INPUT_EDITING_FUNCTIONS 
  $INSERT - 
      HELP PREDEFINED_NAMES $INSERT 
  Inserting Records into a File - 
      HELP SPLITTING_AND_JOINING_RECORDS 
  Insertion Mode - 
      HELP INSERTION_MODE 
  Introducer - 
      HELP KEYIN DESCRIPTION: 
  $INTRO_1 - 
      HELP PREDEFINED_NAMES $INTRO_1 
  $INTRO_2 - 
      HELP PREDEFINED_NAMES $INTRO_2 
K 
  $KEY Predefined String Function - 
      HELP EQUALS EXAMPLE: 
      HELP KEYIN DESCRIPTION: 
  KEYIN Command - 
      HELP EQUALS EXAMPLE: 
  KEYIN Command - 
      HELP KEYIN 
  KEYIN-Values - 
      HELP SUBSTITUTION 
  Keywords and Abbreviations - 
      HELP KEYWORDS_AND_ABBREVIATIONS 
  $KEY_GENERATION - 
      HELP PREDEFINED_NAMES $KEY_GENERATION 
L 
  $LEFTOVER - 
      HELP PREDEFINED_NAMES $LEFTOVER 
  Lexical Functions - 
      HELP LEXICAL_FUNCTIONS 
  LOCATION Command - 
      HELP LOCATION 
      HELP LOCATION EXAMPLE: 
  LOCATION-Values - 
      HELP SUBSTITUTION 
  Logical Operators - 
      HELP LOGICAL_OPERATORS 
M 
  Manipulating Data in Serial Editing Mode - 
      HELP MANIPULATING_DATA_IN_SERIAL_EDITING_MODE 
  $MATCHES - 
      HELP PREDEFINED_NAMES $MATCHES 
  $MATCH_LIMIT - 
      HELP PREDEFINED_NAMES $MATCH_LIMIT 
  $MAX_COMMAND - 
      HELP PREDEFINED_NAMES $MAX_COMMAND 
  $MAX_RECORD - 
      HELP PREDEFINED_NAMES $MAX_RECORD 
  $MIN_COMMAND - 
      HELP PREDEFINED_NAMES $MIN_COMMAND 
  $MIN_RECORD - 
      HELP PREDEFINED_NAMES $MIN_RECORD 
  MOVE Command - 
      HELP MOVE 
      HELP MOVE RELATED_TOPICS: 
  Movement Expressions - 
      HELP MOVEMENT_EXPRESSIONS 
  Moving the Cursor - 
      HELP MOVING_THE_CURSOR 
  Multiple Editing Windows - 
      HELP MULTIPLE_EDITING_WINDOWS 
N 
  Names - 
      HELP NAMES 
  Names as Block Operands - 
      HELP NAMES_AS_BLOCK_OPERANDS 
  NEW - 
      HELP PREDEFINED_NAMES NEW 
  NEXT Block Operand - 
      HELP EDIT_BLOCK_STACK 
  $NOT_COPIED - 
      HELP PREDEFINED_NAMES $NOT_COPIED 
O 
  OFF - 
      HELP PREDEFINED_NAMES OFF 
  OLD - 
      HELP PREDEFINED_NAMES OLD 
  ON - 
      HELP PREDEFINED_NAMES ON 
  $ONESPACEEDIT - 
      HELP PREDEFINED_NAMES $ONESPACEEDIT 
  OUTPUT Command - 
      HELP OUTPUT 
  OVER Command - 
      HELP OVER 
P 
  $PAD - 
      HELP PREDEFINED_NAMES $PAD 
  Pattern Functions - 
      HELP SYNTAX_OF_THE_PATTERN_STRING 
  Pattern-String Block Operand - 
      HELP PATTERN_STRING_BLOCK_OPERAND 
  $POINT - 
      HELP PREDEFINED_NAMES $POINT 
  POSITION Block Operand - 
      HELP POSITION 
  Predefined Names -   
    $COMMENT - 
      HELP LEXICAL_FUNCTIONS 
    $CONTROL - 
      HELP LEXICAL_FUNCTIONS 
  Predefined Names - 
      HELP PREDEFINED_NAMES 
  PREVIOUS Block Operand - 
      HELP EDIT_BLOCK_STACK 
  PRINT Command - 
      HELP PRINT 
  Processing Options -   
    Exist - 
      HELP PROCESSING_OPTIONS 
    Key Increment - 
      HELP PROCESSING_OPTIONS 
    Protect - 
      HELP PROCESSING_OPTIONS 
  Processing Options - 
      HELP PROCESSING_OPTIONS 
  $PROTECT - 
      HELP PREDEFINED_NAMES $PROTECT 
  PROTECT - 
      HELP PREDEFINED_NAMES PROTECT 
  PROTECT Option - 
      HELP PROTECT 
Q 
  QUIT - 
      HELP END DESCRIPTION: 
R 
  READ Command - 
      HELP READ 
      HELP READ DESCRIPTION: 
  RECORD Block Operand - 
      HELP RECORD 
  Record Keys as Block Operands - 
      HELP NUMERIC_KEY 
  $RECORDS_DELETED - 
      HELP PREDEFINED_NAMES $RECORDS_DELETED 
  $RECORDS_INSERTED - 
      HELP PREDEFINED_NAMES $RECORDS_INSERTED 
  $RECORDWRAP - 
      HELP PREDEFINED_NAMES $RECORDWRAP 
  $REKEY - 
      HELP PREDEFINED_NAMES $REKEY 
  Rekeying a Keyed File - 
      HELP REKEYING_KEYED_FILE 
  Relational Operators - 
      HELP RELATIONAL_OPERATORS 
  Relative Block Operands -   
    Pattern-string - 
      HELP RELATIVE_BLOCK_OPERANDS 
    POSITION - 
      HELP RELATIVE_BLOCK_OPERANDS 
    RECORD - 
      HELP RELATIVE_BLOCK_OPERANDS 
  Relative Block Operands - 
      HELP RELATIVE_BLOCK_OPERANDS 
  Repeat Count - 
      HELP SKIP EXAMPLE: 
  REPEAT SELECT Clause - 
      HELP REPEATED_BLOCKS EXAMPLE: 
  Repeated Block - 
      HELP USER_DEFINED_BLOCK_OPERANDS 
  Repeated Blocks - 
      HELP REPEATED_BLOCKS 
  Replacement Mode - 
      HELP REPLACEMENT_MODE 
  Replacing and Inserting Characters - 
      HELP REPLACEMENT_INSERTION 
  $RESTORE - 
      HELP PREDEFINED_NAMES $RESTORE 
  RESTORE Command - 
      HELP RESTORE 
S 
  SAVE Command - 
      HELP SAVE 
  $SCREEN - 
      HELP PREDEFINED_NAMES $SCREEN 
  Screen Appearance - 
      HELP SCREEN_APPEARANCE 
  $SCROLL - 
      HELP PREDEFINED_NAMES $SCROLL 
  SELECT Clause - 
      HELP SELECT 
      HELP SELECT DESCRIPTION: 
      HELP ENCLOSED_BLOCKS EXAMPLE: 
  Selected Block - 
      HELP SELECTED_BLOCK 
  Serial Editing - 
      HELP SERIAL_EDITING 
  SHOW Command - 
      HELP SHOW 
  Signals - 
      HELP SIGNALS 
  $SITES - 
      HELP PREDEFINED_NAMES $SITES 
  $SKIP - 
      HELP PREDEFINED_NAMES $SKIP 
  SKIP Option - 
      HELP SKIP 
  Special Location Names -   
    $LEFTOVER - 
      HELP SPECIAL_LOCATION_NAMES $LEFTOVER 
    $NOT_COPIED - 
      HELP SPECIAL_LOCATION_NAMES $NOT_COPIED 
    CURRENT - 
      HELP SPECIAL_LOCATION_NAMES CURRENT 
    HERE - 
      HELP SPECIAL_LOCATION_NAMES HERE 
    THAT - 
      HELP SPECIAL_LOCATION_NAMES THAT 
  Special location_names - 
      HELP SPECIAL_LOCATION_NAMES 
  Specifying User-Defined Block Operands - 
      HELP USER_DEFINED_BLOCK_OPERANDS 
  Splitting and Joining Records - 
      HELP SPLITTING_AND_JOINING_RECORDS 
  Starting 6Edit - 
      HELP STARTING_6EDIT 
  STRING - 
      HELP PREDEFINED_NAMES STRING 
  STRING Block Operand - 
      HELP STRING 
  String Expressions - 
      HELP STRING_EXPRESSIONS 
  String-Keyed Files - 
      HELP RECORD_KEY_GENERATION 
  $STRIP_BLANKS - 
      HELP PREDEFINED_NAMES $STRIP_BLANKS 
  Substitution - 
      HELP SUBSTITUTION 
  Switching between Serial and Screen Editing - 
      HELP SWITCHING_BETWEEN_SERIAL_AND_SCREEN_EDITING 
  SYNONYM Command - 
      HELP SYNONYM 
      HELP SYNONYM EXAMPLE: 
  SYNONYM-Values - 
      HELP SUBSTITUTION 
  Syntax of the Pattern String - 
      HELP SYNTAX_OF_THE_PATTERN_STRING 
T 
  $TEXTEDIT - 
      HELP PREDEFINED_NAMES $TEXTEDIT 
  THAT - 
      HELP PREDEFINED_NAMES THAT 
  THRU Clause - 
      HELP THRU 
      HELP ADJUST DESCRIPTION: 
  TIME Command - 
      HELP TIME 
U 
  Using Block Expressions - 
      HELP USING_BLOCK_EXPRESSIONS 
  Using Predefined Names - 
      HELP PREDEFINED_USAGE 
V 
  Values -   
    EQUALS - 
      HELP SUBSTITUTION 
    KEYIN - 
      HELP SUBSTITUTION 
    LOCATION - 
      HELP SUBSTITUTION 
    SYNONYM - 
      HELP SUBSTITUTION 
  Vertical Scroll Margins - 
      HELP VERTICAL_SCROLL_MARGINS 
  $VSCROLL - 
      HELP PREDEFINED_NAMES $VSCROLL 
  $VSCROLL_MARGIN - 
      HELP PREDEFINED_NAMES $VSCROLL_MARGIN 
W 
  Wildcard Operators - 
      HELP IMB 
  WINDOW Command - 
      HELP WINDOW 
  $WI_BORDER - 
      HELP PREDEFINED_NAMES $WI_BORDER 
  $WI_PERCENT - 
      HELP PREDEFINED_NAMES $WI_PERCENT 
  Wordwrap - 
      HELP WORDWRAP 
  $WORDWRAP - 
      HELP PREDEFINED_NAMES $WORDWRAP 
X 
  XIT - 
      HELP END DESCRIPTION: 
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
In addition to scrolling vertically, the 6Edit window can also scroll 
horizontally.  Horizontal scroll margins act on the same principle as vertical 
scroll margins; however, horizontal margins scroll from right to left, or from 
left to right. 
These margins are located at the right and left of the editing window: 
               ------------------------- 
               |*                      |  command window 
               |                       | 
               |-----------------------| 
               | s  m |         | s  m | 
               | c  a |         | c  a | 
               | r  r |         | r  r |  editing window 
               | o  g |         | o  g | 
               | l  i |         | l  i | 
               | l  n |         | l  n | 
               ------------------------- 
6Edit keeps the cursor out of the scroll margins whenever possible.  If you 
try to move the cursor into the margin, 6Edit scrolls the data so that the 
cursor is no longer in the margin. 
You can change the size of a horizontal scroll margin, from a minimum of zero 
columns to a maximum of half the editing window width.  To do this, assign a 
number to the predefined name "$HSCROLL_MARGIN". 
The IBEX window is represented by one line above the command window at the top 
of your terminal screen.  The IBEX window processes certain global commands 
when you are in 6Edit.  It is an option. 
To remove the IBEX window from your screen, enter the following command at the 
IBEX prompt before starting 6Edit: 
    !SET M$6E UC01 
or 
    !ADJUST M$6E UC01 
before any editing command. 
If you remove the IBEX window, you have an extra line for editing.  Also, 
since what you've really done is to combine the IBEX window and the command 
window, any commands that need to use the IBEX window will probably have more 
lines available.  The disadvantage of combining the IBEX and command windows 
is that since keyins and IMPs are really the same thing, any keyins that you 
define in 6Edit for the command window will remain in the IBEX window after 
you exit 6Edit.  You will have to restore any needed IMPs either manually or 
via the $RESTORE predefined name.  This problem can be eliminated if you do 
not need to use keyins in the command window by specifying "IN EDITING" for 
all your keyin definitions. 
If you do not remove the IBEX window, any IMPs or keyins used in your context 
file during that session are removed when you exit 6Edit.  6Edit restores your 
terminal environment to its former status. 
By not removing the IBEX window, you give up screen space.  Since the window 
uses a line at the top of your screen, you are short one editing window line 
at the bottom. 
For example, if you normally define <ESC> <1> to issue a CHECK command, and 
you redefine Escape 1 during a 6Edit session to generate a COPY THAT command, 
then when you leave 6Edit: 
o   If you had an IBEX window during the 6Edit session (the default), <ESC> 
    <1> reverts back to generating the CHECK command. 
o   If you did not have an IBEX window during the 6Edit session (i.e., you 
    !SET M$6E UC01 before starting 6Edit), <ESC> <1> still generates the COPY 
    THAT command. 
Format: 
IF string_expr [command] ; commands [; ELSE [command] ; commands] 
Parameters: 
string_expr    specifies an expression that evaluates to a number. 
command    specifies any 6Edit command. 
commands    specifies any 6Edit commands. 
Description: 
The IF and ELSE commands permit conditional execution of multiple commands in 
a single command line.  If the string expression evaluates to a number greater 
than zero, any commands preceding the corresponding ELSE are executed, and the 
rest of the line (ELSE and beyond) is ignored.  If the string expression 
evaluates to zero, the commands following ELSE are executed. 
The IF/ELSE construct can be nested to any depth. 
Examples: 
IF $AUTOTAB PO NU $AUTOTAB; ELSE PO NU 1 
positions to the autotab column of the current record. 
RE 'bird'; IF $MATCHES COPY STRING 'bath' AFTER BO '%R' 
appends the word "bath" to the next record containing the word "bird". 
00002
00003
00001
Syntax: 
string-1 {?=|.IMB.} string-2 
string-1 {=?|.MATCHES.} string-2 
string-1 {?>|.IN.} string-2 
string-1 {<?|.CONTAINS.} string-2 
Parameters: 
string-1    is a string expression.  It evaluates to the operand to be 
compared. 
string-2    is a string expression.  It represents the value to which string-1 
is compared. 
Description: 
These operators compare their two operands, taking the wildcard function into 
account. 
Wildcard operators resemble relational operators, but allow one string to 
contain one or more "wildcard" characters, the question mark (?).  A wildcard 
character (?) appearing in one string matches a sequence of any number of 
characters (including 0 characters) in the other string.  For example: 
If the wildcarded string is 
    'Product is ? stock' 
then it equals both of the following strings: 
    'Product is in stock' 
    'Product is out of stock' 
Note that the wildcard character (?) used by these operators appears 
differently than the $CONTROL-Question Pattern function.  In the latter 
instance, the $CONTROL character is used, whereas for wildcard operators, the 
question mark is used alone. 
Like the relational operators, the result computed by each of these wildcard 
operators is a numeric operand:  either 1, indicating that the relation is 
true, or 0, indicating that the relation is false.  Unlike the relational 
operators, string-1 and string-2 are always treated as sequences of 
characters: a character-by-character string comparison is always performed. 
The .IMB. and .MATCHES. operators look for the complete match of a wildcarded 
string.  The .IN. and .CONTAINS. operators look for a contained wildcarded 
string. 
The result of the .IMB. ("Is Matched By") operator, accounting for wildcard 
characters, is true if the two strings are equal, false otherwise.  Question 
marks appearing in string-1 represent wildcard characters; however, question 
marks appearing in string-2 are given no special interpretation, they are 
taken at face value. 
The result of the .MATCHES. operator, accounting for wildcard characters, is 
true if the two strings are equal, false otherwise.  Question marks appearing 
in string-2 represent wildcard characters; however, question marks appearing 
in string-1 are given no special interpretation, they are taken at face value. 
The result of the .IN. operator, accounting for wildcard characters, is true 
if string-1 is a substring of string-2, false otherwise.  Question marks 
appearing in string-1 represent wildcard characters; however, question marks 
appearing in string-2 are given no special interpretation, they are taken at 
face value. 
The result of the .CONTAINS. operator, accounting for wildcard characters, is 
true if string-1 contains string-2 as a substring, false otherwise.  Question 
marks appearing in string-2 represent wildcard characters; however, question 
marks appearing in string-1 are given no special interpretation, they are 
taken at face value. 
00002
00001
IMB
Generally, input editing functions affect characters under or near the cursor 
by moving, deleting, etc. 
These key sequences are those in effect at logon, before any new IMP keys are 
designated.  You, the user, may redefine these keys on your terminal keyboard. 
If you decide to redefine the standard key sequences, those listed here may 
not work as described. 
Input editing functions may be typed at the keyboard directly, by typing a 
sequence of one, two, or three keys. 
These input editing functions are executed by the Front End Processor.  For 
more information about input editing functions, type: 
HELP (6EDIT) ESC_AND_CNTL_FUNCTIONS 
The following key functions move the cursor (and, when necessary, scroll the 
data in the editing window).  These functions do not change the data in the 
file. 
  Command    Function and Description 
  <BS> or <CNTL-H> 
             Backspace. 
  <CNTL-R> 
             Forward space. 
  <TAB> or <CNTL-I> 
             Tab. 
  <CNTL-W> 
             Move to right/left word. 
             Moves the cursor to the right or left word.  The direction in 
             which the cursor moves depends on the last <BS> or <CNTL-R> key 
             typed. 
             A "word" represents a contiguous string of non-space characters. 
             Any number of spaces may appear between words.  All spaces are 
             skipped when moving to the next word.  If the recordwrap mode is 
             disabled, this key function is limited to the current record; 
             when you reach the beginning or end of the record, this function 
             changes direction and moves to the next word in the opposite 
             direction.  If the recordwrap mode is enabled, this key function 
             will move to the next or previous record when it hits the edges 
             of the current record.  (See the $RECORDWRAP predefined name 
             under PREDEFINED_NAMES.) 
             You can use the KEYIN command to define keys that can move either 
             left or right to the previous or next word. 
  <ESC> <CR> 
             Move cursor to beginning of current record. 
  <ESC> <N> 
             Move cursor to the end of current record. 
  <CR> 
             Move cursor to beginning of next record.  If the cursor is in the 
             command window, <CR> returns the cursor to the current editing 
             window. 
  <ESC> <A> 
             Move cursor up one record. 
  <ESC> <B> 
             Move cursor down one record. 
             For <CR>, <ESC> <A>, and <ESC> <B>, the cursor moves by records, 
             not by lines on your terminal.  If a record occupies more than 
             one line of the display, "move cursor up" moves the cursor to the 
             same position of the previous record, (not the previous line). 
             This movement may appear to jump over terminal lines.  The same 
             is true of "move cursor to beginning of next record" and "move 
             cursor down". 
  <CNTL-C> 
             Moves the cursor to the command window.  This function may also 
             be used to terminate a command and keep the cursor in the command 
             window. 
  <CNTL-N> 
             Moves the cursor from the current editing window to the next one. 
             If the current editing window is the last one, it moves the 
             cursor to the first one.  From the command window, <CNTL-N> is 
             equivalent to <CR><CNTL-N>. 
The context file that 6Edit reads initially may have defined other keys on 
your terminal keyboard, to move the cursor over groups of records, or to 
search the file for specific data. 
00001
00010
00001
00003
00011
00002
00004
00007
00008
00009
00005
00006
00003
As an alternative to the replacement mode, you can use the insertion mode.  To 
tell the system to use the insertion mode, enter <ESC> <'>.  Later, to return 
to the replacement mode, enter <ESC> <M>.  Or use the $INSERT predefined name. 
The insertion mode inserts characters into the record; it never replaces 
characters.  To replace characters in the insertion mode, you must first 
delete the characters you want replaced, then insert the new characters. 
If you define an insertion window in the insertion mode, it maintains many of 
the same effects as in the replacement mode.  For example, many of the input 
editing functions are limited to the insertion window.  However, regardless of 
whether the cursor is at the end of the insertion window, all characters typed 
are inserted into the record, they never replace characters already there. 
Syntax: 
KE[YIN] string_expression_1 IS string_expression_2 
    [   {CO[MMAND] [WI[NDOW]] }] 
    [IN {ED[ITING] [WI[NDOWS]]}] 
    [   {WI[NDOW] window_num  }] 
Parameters: 
string_expression_1    specifies the character or character sequence to be 
typed on the terminal keyboard.  It must evaluate to one, two, or three 
characters, or a function key name possibly followed by one character. 
Additional rules governing string_expression_1 are explained under 
"Description" below. 
string_expression_2    specifies the characters to be substituted for 
string_expression_1 when the latter is typed at the terminal keyboard. 
Information on expressing non-displayable characters in string_expression_2 
are explained under "Description" below. 
window_num    is a window number between 1 and the number of editing windows. 
Description: 
The KEYIN command redefines the keys on your terminal.  It is only effective 
when 6Edit is being used in the screen-editing mode, and the command stream is 
originating from your terminal.  6Edit uses the CP-6 IMP facility to perform 
substitution. 
After using this command, whenever the CP-6 system sees the 
string_expression_1 character(s) coming from your terminal, it acts as though 
you had typed string_expression_2 instead.  The system even displays 
string_expression_2 on your terminal, instead of the characters you had typed 
(that is, instead of string_expression_1). 
Any character value may appear in either string_expression_1 or 
string_expression_2, including non-displayable characters.  In 
string_expression_1, non-displayable characters represent control keys; in 
string_expression_2, they represent input editing functions.  This distinction 
is important.  For example: 
    18 is the ASCII decimal code for <CNTL-R>.  When "%V(18)" appears in 
    string_expression_1, it represents the <CNTL-R> key on the keyboard, the 
    meaning of which you can define using the KEYIN command.  However, when 
    "%V(18)" appears in string_expression_2, it always represents the "move 
    right one character" input editing function, no matter how you have 
    redefined <CNTL-R>. 
The IN-clause can be appended to any KEYIN command.  If you include the 
IN-clause, the string_expression_1 key or key sequence is defined only in the 
command or editing window, depending on which is specified.  If you omit the 
IN-clause, then string_expression_1 is defined in both the command and editing 
windows. 
NOTE:  Typing an immediate-type function before 6Edit has IMPed the key 
    sequence to a typeahead-type function invokes an immediate-type function 
    rather than the 6Edit definition of the key sequence. 
    This situation occurs only when using immediate-type input editing 
    functions.  The immediate-type input editing functions are: 
        ESC Sequences                   Control Characters 
        --------------------------      ------------------ 
        <ESC><A>   <ESC> <CNTL-A>       <CNTL-Q> 
        <ESC><B>   <ESC> <CNTL-B>       <CNTL-S> 
        <ESC><G>   <ESC> <ESC>          <CNTL-X> 
        <ESC><H>                        <CNTL-Y> 
        <ESC><Q> 
        <ESC><W> 
        <ESC><Y> 
    To avoid this situation, use FCNTBL=CP5S2 with the IBEX TERMINAL command 
    before invoking 6Edit. 
    Defining a key sequence to be immediate-type in one window but 
    typeahead-type in another window may give unpredictable results.  Either 
    key sequence definition could be used by the FEP, depending on where 6Edit 
    is in its processing of the last terminal input. 
Several rules apply to string_expression_1. 
o   If string_expression_1 evaluates to exactly one token (character or 
    function key name), it may be any token value which can be generated at 
    your terminal keyboard. 
o   If string_expression_1 evaluates to two tokens the first must equal either 
    the "primary introducer" or the "secondary introducer."  These one- or 
    two-token values are set by the predefined names "$INTRO_1" and 
    "$INTRO_2"; initially, $INTRO_1 is the Escape character and $INTRO_2 has 
    no value. 
In addition, the following rules apply.  If string_expression_1 is 
o   1 token long: string_expression_1 need not match either $INTRO_1 or 
    $INTRO_2. 
o   2 tokens long: the first character must equal either $INTRO_1 or $INTRO_2 
    and the second must be a character (not a function key name). 
o   3 tokens long:  the first two characters must equal $INTRO_1 or $INTRO_2. 
    Only the first can be a function key name. 
The last or only character of string_expression_1 may be any character value 
which can be generated at your terminal keyboard. 
Non-displayable tokens may be included in either string_expression_1 or 
string_expression_2.  You can enter these tokens in string_expression_1 or 
string_expression_2 in one of these ways: 
o   Using the $KEY(keyname) predefined string function or its equivalent 
    notation:  <keyname>.  The parameter for this function is a keyname, such 
    as ESC.  For example, the F1 function key may be represented as $KEY(F1) 
    or as <F1>.  To obtain the spelling for any non-displayable key, use the 
    IMP command SPELL. 
    A unique feature of the $KEY predefined string function is that it can be 
    used to represent a function key that sends one, two, three, or even four 
    characters.  These keys may be functions keys such as F1 or SF1 (i.e., 
    Shift F1).  For PCs operating with PCT, $KEY may be used to assign meaning 
    to Alt-Fn or Cntl-Fn keys (for more information, enter: 
        HELP (6EDIT) PC_KEYINS ) 
o   Using the $CNTL('char') predefined string function or its equivalent 
    notation:  <CNTL-char>.  The parameter for this function, "char", is any 
    character which when pressed with the CNTL key sends a control character. 
o   Using the $CONTROL-Value function.  The parameter for the function is the 
    ASCII decimal code for the control key (e.g., <CNTL-D>), or the ASCII 
    control character (e.g., <ESC>) that you are defining.  In the example, 
    KEYIN '%V(27)0' IS ... 
    %V(27) represents the <ESC> control character; %V is the $CONTROL-Value 
    function and (27) is the ASCII decimal code for <ESC>, which in this 
    example is defined as being followed by the zero character. 
o   Using EQUALS names that you have previously defined, usually in your 
    context file.  The standard context file defines names for the most common 
    non-displayable characters:  ESC for <ESC> and CR for <CR>.  Then, use the 
    CONCATENATE operator to combine the name with other characters to comprise 
    string_expression_1.  For example: 
    KEYIN ESC||'L' IS... 
$KEY and $CNTL or their angle bracket notations provide advantages over the 
other two methods of expressing non-displayable characters.  The chief 
advantages are as follows: 
o   Self-documenting commands. 
    Expressing keystrokes as you see them on the keyboard makes it easier to 
    remember how to invoke the keyin by looking at the command again, or 
    displaying the available keyins with the SHOW command. 
o   Expanded number of special sequences available at the terminal. 
    Your terminal probably has keys that send two-, three-, or even 
    four-character sequences when pressed; you can assign meanings within 
    6Edit to many of these keys.  Without $KEY, you would need to use both 
    $INTRO_1 and $INTRO_2 if you assign both two- and three-character 
    sequences, and you would find it quite difficult, if not impossible, to 
    assign meanings to the four-character keys. 
    Using the default single-character introducer, <ESC>, you might not be 
    able to define enough functions to make editing convenient in your 
    environment.  You would then need to define some that require more than 
    one keystroke to enter.  Since most of the two-stroke sequences using 
    <ESC> are already defined for input editing functions in the FEP, you 
    would have to either give up some of those or use less-convenient 
    three-stroke keyins. 
    With $KEY, however, you can define all the single-stroke keyins without 
    using either $INTRO_1 or $INTRO_2 at all.  With the introducer names still 
    free, you can then use any key as the introducer for up to two sets of 
    two-stroke keyins.  You can also choose as the introducer a key that sends 
    more than one character.  This is much more convenient to type than a 
    control character, and does not force you to use a printing character. 
    You then have the equivalent of four sets of keyins available instead of 
    two. 
Examples: 
The examples below are numbered for ease of use. 
Example 1a. 
    KE <ESC>||'L' IS <CNTL-C>||'SKIP 20 BO RECORDS'||<CR> 
    causes the key sequence Escape-L to generate the characters ETX, SKIP 20 
    BO RECORDS, and CR.  When <ESC> <L> is typed at the keyboard, three things 
    happen: 
    1.  The <CNTL-C> character causes the cursor to move to the command 
        window.  This occurs because <CNTL-C> is 6Edit's input activation 
        function to move the cursor to the command window. 
    2.  The command "SKIP 20 BO RECORDS" is entered in the command window. 
    3.  The <CR> character causes the command to be executed by 6Edit. 
Example 1b. 
    KE ESC||'L' IS CMD||'SKIP 20 BO RECORDS'||CR 
    is identical to the previous command, but it takes advantage of EQUALS 
    names.  This command assumes that you have already entered the following 
    command: 
    ESC EQUALS <ESC>; CMD EQUALS <CNTL-C>; CR EQUALS <CR> 
    Note that since string_expression_1 is two characters long in both of the 
    above examples, $INTRO_1 or $INTRO_2 must be set to <ESC> for the key 
    definitions to work. 
Example 1c. 
    By using the $KEY function in the above examples, $INTRO_1 or $INTRO_2 do 
    not have to be used.  With $KEY, any available single function key that 
    sends a character sequence (usually ESC and something else) can be used 
    instead of the Escape-L sequence to perform the "SKIP 20 BO RECORDS" 
    function. 
    Suppose F2 is the desired key for this function.  The following KEYIN 
    command can then be entered: 
    KE <F2> IS <CNTL-C>||'SKIP 20 BO RECORDS'||<CR> 
    With the EQUALS names defined as above, this command could also be entered 
    as: 
    KE <F2> IS CMD||'SKIP 20 BO RECORDS'||CR 
    If the F2 key on your keyboard sends <ESC><L>, these commands perform the 
    same functions as the first two KEYIN commands above, but with a single 
    keystroke, F2, and without having to first set an introducer character 
    with $INTRO_1 or $INTRO_2. 
Example 2: 
    KEYIN '%V(23)' IS '%V(27)5R%V(23)' 
            or 
    KEYIN $CNTL(W) IS '%V(27)5R%V(23)' 
    defines the <CNTL-W> key, specified by %V(23), to move the cursor left by 
    one word.  In this command: 
    o   %V(27)5R is the ASCII decimal code for escape (<ESC>), followed by 
        "5R".  This input editing function sets the "left" direction for the 
        "move one word" function to follow.  (See INPUT_EDITING_FUNCTIONS for 
        more information.) 
    o   %V(23) is the ASCII decimal code for <CNTL-W>.  <CNTL-W> is the "move 
        one word" input editing function. 
    If all the "one-stroke" function keys in your environment were already 
    defined, and you might want to use a shifted function key instead of 
    <CNTL-W>, so you could enter the following KEYIN command: 
    KEYIN $KEY(SF3) IS '%V(27)5R%V(23)' 
    This performs the "move left one word" function with two keystrokes, 
    Shift-F3.  Single and shifted function keys can be defined in a similar 
    manner for the rest of the examples below. 
Example 3: 
    KEYIN <CNTL-E> IS '%V(27)5S%V(23)' 
    defines the <CNTL-E> key to move the cursor right by one word.  In this 
    command, similarly to Example 2, %V(27)5S sets the "right" direction for 
    the "move one word" function to follow. 
Example 4: 
    KEYIN <CNTL-D> IS <ESC>||'5R'||<ETB>||<ESC>||<ETB> 
    defines the <CNTL-D> key to delete the word to the left of the cursor.  In 
    this command: 
    o   <ESC>||'5R' is an input editing function that sets the "left" 
        direction for the "move one word" function to follow.  (See 
        INPUT_EDITING_FUNCTIONS for more information.) 
    o   <ETB> is the ASCII character code for <CNTL-W>.  This is the "move one 
        word" input editing function; the cursor moves to the beginning of the 
        previous word in the record. 
    o   <ESC>||<ETB> are the ASCII character codes which comprise the "delete 
        word" input editing function. 
Example 5: 
    KEYIN <FF> IS <ESC>||<CNTL-W> 
    defines the <CNTL-L> key to delete the word under and to the right of the 
    cursor.  <FF> is the ASCII character code for <CNTL-L>. 
Example 6: 
    KEYIN <CR> IS <ESC>||<LF> IN EDITING 
    causes the carriage return key to generate the characters Escape and 
    Linefeed, in the editing window only; it does not affect the carriage 
    return key when the cursor is in the command window. 
    This KEYIN is useful when you want to add several lines of text in the 
    middle of a file, or if you are used to PC or UNIX editors where <CR> 
    represents a record boundary.  Normally, the carriage return key simply 
    moves the cursor to the beginning of the next record; to add a new record, 
    you must type <ESC> <LF> (the Escape and Linefeed keys).  However, this 
    KEYIN command allows you to use the carriage return key to generate the 
    Escape Linefeed sequence.  You must include an IN-clause in this KEYIN 
    command because you do not want the carriage return key to generate <ESC> 
    <LF> when you type it in the command window.  By adding "IN EDITING" to 
    the KEYIN command, the definition of the carriage return key in the 
    command window is unchanged. 
Related Topics: 
Substitution 
00002
00003
00001
00004
COMMON_FUNCTIONS
6Edit commands use a keyword-style notation.  All keywords may be spelled out 
fully, or abbreviated.  You can choose any editing function by simply using 
the alphabetic characters, the numerals, and seven special characters.  The 
following figure summarizes the keywords and non-alphabetic characters used. 
Keywords 
        6BUILD       * DONT           MOVE         * REPEAT 
        6EDIT          EDIT           NEW            RESET 
        6X             EDITING      * NEXT         * RESTORE 
        ADJUST         END            NUMBER       * SAVE 
        AFTER          EO             OF             SELECT 
        ALL            EQUALS         OLD          * SESSION 
        ANY         ** ERASE          ON           * SETUP 
        AO             EXIT       *** OUTPUT         SHOW 
        BACKWARD       FILE           OVER           SKIP 
        BEGINNING      FORWARD        PATTERN        STRING 
        BLOCK        * HELP           PATTERNS       SYNONYM 
        BO           * HERE           PERCENT        SYNONYMS 
        BY             IN             POSITION     * THAT 
        COMMAND        IS             POSITIONS      THROUGH 
        COPY         * KEY          * PREVIOUS       THRU 
      * CURRENT        KEYIN       ** PRINT        * TIME 
      * DATE           KEYINS         PROTECT        TO 
        DELETE         LINES          QUIT        ** TOPICS 
    *** DIRECTORY      LOCATION       READ           WINDOW 
        DISPLAY        LOCATIONS      RECORD         WINDOWS 
                                      RECORDS        XIT 
    All of the above may be entered in upper or lower case and may 
    be abbreviated to exactly the first two characters, except 
    those preceded by one or more asterisks. 
    * - must be abbreviated to exactly the first four characters. 
    ** - abbreviation is not permitted. 
    *** - may be abbreviated with three or more characters. 
Non-alphabetic Characters 
    Numerals:  0 through 9 
    Special Characters:  '  (  )  ,  .  ;  ? 
6Edit recognizes function keys, control keys, and ASCII control codes as 
string expressions.  The key or code name must be enclosed in angle brackets 
("<", ">") or be the argument of the $KEY function, for example: 
    KEYIN <F1> IS ... 
    KEYIN <UPARROW> IS ... 
    KEYIN <ENT> IS ... 
    KEYIN <F1>||'A' IS ... 
Note that abbreviations accepted by IMP (such as "ENT" for "ENTER" above) will 
also be accepted by 6Edit. 
Also note the last example above:  function keys may be used as introducers 
for multi-key sequences. 
6Edit accepts the name of any key on the terminal keyboard inside the angle 
brackets.  This includes not only the FEP/profile-defined function keys, but 
also the ASCII control characters (plus the DEL character) as mnemonics: 
    NUL     ENQ     LF      SI      DC4     EM      RS 
    SOH     ACK     VT      DLE     NAK     SUB     US 
    STX     BEL     FF      DC1     SYN     ESC     DEL 
    ETX     BS      CR      DC2     ETB     FS 
    EOT     HT      SO      DC3     CAN     GS 
Also, ASCII control keys can be included inside the angle brackets, using the 
identifier "CNTL": 
    <CNTL-x> 
where "x" is any one of:  @, A-Z, [, \, ], ^, _ 
                          `, a-z, {, |, }, ~ 
The ASCII mnemonics evaluate to the corresponding ASCII code (0 - 31 and 127). 
However, use of the function key elements in a numeric expression yields an 
error; use of the function key elements in an expression not used (eventually) 
by the KEYIN command yields unpredictable results. 
The angle bracket notation is intended to reinforce the notation used in the 
manuals when referring to keystrokes at the terminal keyboard.  See CE70 and 
CE73, Notation Conventions. 
Additionally, the $CNTL predefined string function is permitted in string 
expressions: 
    $CNTL 
$CNTL is much like the <CNTL-x> expression element; it is included as a 
computational form of <CNTL-x>:  $CNTL takes a string argument possibly longer 
than one character, whereas the angle bracket notation is limited to a single 
character.  $CNTL returns a string which contains the ASCII control-codes for 
the characters in the original string. 
Examples: 
KEYIN <ESC>||'A' IS <CNTL-C>||'BA SK 20 RE'||<CR> 
KEYIN ESC||'A' IS <ETX>||'BA SK 20 RE'||CR 
The above two examples are identical; the second assumes that the names "ESC" 
and "CR" have been defined by the user, probably in the context file as they 
are now. 
DOITTOIT EQ $INPUT('Type control char to define: ') 
KEYIN $CNTL(DOITTOIT) IS <ESC>||'5R'||$CNTL('[W') 
Note that <CNTL-[> is Escape, so "$CNTL('[W')" is the sequence <ESC> <CNTL-W>. 
00001
You can instruct 6Edit to perform certain lexical functions during command 
entry.  You can invoke these functions by using identifier characters, which 
are the values of two predefined names:  $CONTROL and $COMMENT. 
Initially, 6Edit uses the following default identifier characters for the 
$CONTROL and $COMMENT functions: 
    %    invokes the $CONTROL function 
    "    invokes the $COMMENT function 
6Edit looks for the $COMMENT identifier in command input and READ-file 
records, and for the $CONTROL identifier in quoted strings.  It does not look 
for these identifiers (nor perform their functions) in records read from data 
files. 
It is possible to use the $CONTROL or $COMMENT identifier without invoking its 
lexical function.  This can be accomplished in two ways.  One is to disable 
the name.  To do this, you assign an empty string to the predefined name 
$CONTROL or $COMMENT.  Thereafter, 6Edit does not support the functions 
invoked by $CONTROL or $COMMENT, and will not look for the identifier in 
command lines, READ-file records, or quoted strings. 
Or, when using the $CONTROL identifier, you can enter it twice in succession. 
For more help, enter: 
    HELP (6EDIT) $CONTROL 
or  HELP (6EDIT) $COMMENT 
$CONTROL_LITERAL
Syntax: 
LO[CATION] name [IS] [BL[OCK]] block_expression 
Parameters: 
name    is any name; it must be between 1 and 31 characters in length.  A name 
may include: 
    o   Alphabetic characters 
    o   Digits (except as the first character of name) 
    o   $   _    #    and   @ 
block_expression    specifies the block description of the new value of name. 
Description: 
The LOCATION command remembers the boundaries of its block operand as the 
value of name.  Thereafter, you can use name in a block expression, and 6Edit 
interprets it to refer to the block specified by block_expression in this 
LOCATION command. 
The name parameter is required.  It must be a name you create. 
The operand of the LOCATION command is called a "named block." 
Between the time the LOCATION command is given and the time of a reference to 
name, you should be aware that changes to the contents or location of the 
named block will effectively change the value of name as well, since name 
simply refers to the "location" of the named block, it does not hold a copy of 
the block's contents. 
Example: 
LOCATION C1 IS BO 1 THRU 4 POSITION 15 
finds the specified block, and assigns the location of that block to the name 
C1.  In subsequent commands, 6Edit evaluates C1 as representing this location. 
For example: 
COPY C1 AFTER 7 
copies from the beginning of record 1 through column 15 of record 4.  The data 
is inserted after record 7.  C1 still refers to the block located at 
BO 1 THRU 4 POSITION 15.  It did not move with the data. 
Related Topics: 
Substitution 
00002
00003
00001
00004
Syntax: 
number {&|.AND.} number 
number {||.OR.} number 
{~|.NOT.} number 
Parameters: 
number    is a string expression.  It evaluates to a logical value, and must 
consist of one or more numerals. 
Description: 
These operators compute Boolean values from their operands.  All operands are 
assumed to represent logical values, that is, either a true value or a false 
value.  All operands must be numeric; 6Edit interprets their values as: 
o   True, if number is non-zero (either greater than zero or less than zero). 
o   False, if number is exactly zero. 
The .AND. operator forms the logical conjunction of its two operands.  The 
result is either one or zero, representing true or false respectively.  The 
result is one if both operands are true.  The result will be zero if either or 
both operands are false. 
The .OR. operator forms the logical union of its two operands.  The result is 
either one or zero, representing true or false respectively.  The result is 
zero if both operands are false.  The result is one if either or both operands 
are true. 
The .NOT. operator forms the logical inverse of its operand.  The result is 
either one or zero, representing true or false respectively.  The result is 
zero if the operand is true.  The result is one if the operand is false. 
00002
00001
IMB
PLUS
Syntax: 
MO[VE] [BL[OCK]] block_expression 
Parameters: 
block_expression    is the block of data to be moved. 
Description: 
The basic operation of the MOVE command is the same as for the COPY command. 
The operand becomes the new source block. 
For the MOVE command, however, 6Edit remembers that the source block is to be 
deleted after use.  Later, when an AFTER or OVER command refers to the source 
block, it will delete the source block after copying it to the specified 
destination. 
After receiving this command, the operand becomes the new selected block. 
Example: 
MOVE 2 THRU 22 AFTER 40 
moves the records 2 through 22 to a new position after record 40.  The source 
block (records 2 through 22) is deleted after being copied to its new location 
(after 40). 
Related Topics: 
Copy/Move Operations 
COPY Command 
AFTER Command 
OVER Command 
00002
00003
00001
00004
Syntax: 
[block_options] block_operand  ... 
Description: 
A "movement expression" is a sequence of block operands, optionally modified 
by block options.  These tell 6Edit how to move the file pointer through the 
current enclosing block. 
In its simplest form, a movement expression is a list of block operands.  In 
front of each block operand, you can give block options to be applied to that 
operand. 
Example: 
20.3  BACKWARD SKIP 30 RECORDS POSITION 18 
Three block operands compose this movement expression:  the record key "20.3", 
"RECORDS", and "POSITION 18".  The "RECORDS" operand is modified by two block 
options:  "BACKWARD" and "SKIP 30". 
This expression causes 6Edit to move the file pointer to record 20.3, then 
back up 30 records in the file, and finally move the file pointer to position 
18 of that record. 
00001
00002
In 6Edit, you can create your own names for things.  This makes it easier to 
remember specific details, such as the location of data.  Names also make it 
easier to refer to something repeatedly, such as an often-used sequence of 
keywords. 
Each name has a value associated with it; the value is the location or object 
to which the name refers. 
You create names with the assignment commands; these commands are 
    EQUALS 
    LOCATION 
    SYNONYM 
    KEYIN 
Some names are "predefined" by 6Edit; that is, whenever you run 6Edit the 
names have already been created.  These names are used to communicate details 
between you and 6Edit.  You can change the value of some of the predefined 
names; others may not be changed by you, their values are changed internally 
by 6Edit. 
Names are used in several ways in 6Edit: 
o   The EQUALS command assigns a reasonably short value (up to 511 characters) 
    to a name.  The value is stored as a string of characters, which may 
    represent numeric or character data, depending on how the name is later 
    used.  The name can be used in the expression component of a command; 
    6Edit uses the name's value in place of the name when evaluating the 
    expression. 
o   The LOCATION command assigns to a name the boundaries of a block of data 
    in a file.  To later refer to that location in the file, include the name 
    in an editing command; 6Edit treats the name as a reference to the block. 
o   The SYNONYM command assigns a fragment of a 6Edit command line to a name. 
    If 6Edit later sees the name in a command line, it replaces it with the 
    fragment which is the name's value. 
o   The KEYIN command redefines a key on your terminal.  Here, the name being 
    assigned is the actual character or sequence of characters generated by 
    the terminal key, or an encoded representation of the name of the key. 
    When a terminal key is redefined, the CP-6 system will cause it to 
    generate any sequence of characters that you specify.  When you type the 
    key (or sequence of keys), the system will echo on your terminal the 
    sequence of characters which represent the name's value. 
Syntax: 
location_name 
Parameters: 
location_name    is a name.  It may be either a predefined name ($LEFTOVER, 
$NOT_COPIED, HERE, THAT, or CURRENT), or a name you created whose value has 
previously been set with the LOCATION command. 
Description: 
A location_name can be used as an absolute block operand.  This operand 
specifies a block which you specified and named earlier (or a block predefined 
by 6Edit itself). 
If location_name is the first operand of a block expression, then the file to 
which the name refers becomes the enclosing block for the rest of the block 
expression.  If location_name is not the first operand of a block expression, 
then it must refer to the same file as the enclosing block for the block 
expression. 
If the first block operand in a block expression is not one of the following 
block operands, then the edit block is used as the enclosing block for the 
rest of the block expression: 
    PREVIOUS 
    NEXT 
    FILE 
    STRING 
    location_name 
The location_name operand may not be modified by the following block options: 
    SKIP 
    FORWARD 
    BACKWARD 
The default "point" option for the names as block operands is ALL OF. 
00002
00001
The following topics categorize 6Edit's predefined names.  For a list of the 
predefined names under each topic, type: 
HELP NAME_SET set 
For example: 
HELP NAME_SET PATTERN_SEARCHING 
or 
HELP NAME_SET BLOCK_DEFAULTS 
  Category   Names 
  Constant Values Provided by 6Edit 
             ANY                BO                   OLD 
             AO                 DONT_PROTECT         ON 
             BACKWARD           EO                   PROTECT 
             BIN10              FORWARD              STRING 
             BINHLF             NEW 
             BIN521             OFF 
  Values Set by 6Edit 
             $CONTEXT           $RECORDS_INSERTED    $FILERECORDS 
             $MATCHES           $SITES             * $FILETYPE 
             $RECORDS_DELETED   $FILEORG 
             * $FILETYPE can also be used to set the file type of files 
               being edited. 
  Location Names Set By 6Edit 
             $LEFTOVER          THAT 
             $NOT_COPIED        HERE 
             CURRENT 
  Terminal Control 
             $AUTOTAB           $HSCROLL_MARGIN      $SCROLL 
             $END_MARK          $INSERT              $TEXTEDIT 
             $EZ_APPEND         $INTRO_1             $VSCROLL 
             $HSALL             $INTRO_2             $VSCROLL_MARGIN 
             $HSCROLL           $ONESPACEEDIT        $WORDWRAP 
                                $RECORDWRAP 
  Session Control 
             $INITIALIZE        $RESTORE 
  Window Control 
             $COMMAND           $MIN_COMMAND         $WI_BORDER 
             $MAX_COMMAND       $SCREEN              $WI_PERCENT 
  Record Control 
             $BY                $MIN_RECORD          $STRIP_BLANKS 
             $KEY_GENERATION    $PAD 
             $MAX_RECORD        $REKEY 
  Block Expression Defaults 
             $DIRECTION         $POINT               $SKIP 
             $EXIST             $PROTECT 
  Pattern Searching 
             $CASE 
             $MATCH_LIMIT 
  Lexical Characters 
             $COMMENT 
             $CONTROL 
00008
00001
00010
00003
00009
00007
00005
00004
00002
00006
LOGICAL_OPERATORS
Syntax: 
{ numeric_key | KEY string_expression } 
Parameters: 
numeric_key    is either: 
o   A string of 1 to 9 digits; a decimal point (period) may appear in the 
    string such that there are 0-3 digits to the right of the decimal point 
    and not more than 5 to the left. 
o   A string of 1 to 9 digits with no decimal point for sequential files. 
string_expression    specifies the key to be used for a string-keyed file. 
Description: 
A record key may be used as an absolute block operand.  6Edit moves the file 
pointer to the specified record in the enclosing block. 
If an edit-keyed file is being used, numeric_key must be a number between 0 
and 99999.999; a decimal point (period) may appear in the string, with 0 to 3 
digits to the right of the decimal point.  The numeric_key is interpreted as 
the actual record key of the record which is the block operand represented by 
numeric_key.  Note that this record key need not actually exist in the file; 
if the specified record does not exist, then numeric_key represents an empty 
block at the specified record key.  In any case, the record key must be within 
the range of record keys of the current enclosing block. 
If a non-keyed (consecutive) file is being used, numeric_key must be a string 
of 1 to 9 digits with no decimal point.  It is interpreted as the record 
number within the file of the record which is the block operand represented by 
numeric_key.  The record number must be within the range of record numbers of 
the current enclosing block. 
The record key operand may not be modified by the following block options: 
    SKIP 
    FORWARD 
    BACKWARD 
The default "point" option for the record key operand is $POINT. 
Examples: 
48 
moves the file pointer to the record with key "48", when using an edit-keyed 
file.  In a consecutive or unit-record file, specifying a numeric key moves 
the file pointer to the 48th record in the file. 
COPY 52.1 AFTER HERE 
copies the record with key "52.1" to the current file pointer (cursor) 
location.  This command can only be used in an edit-keyed file, because the 
record key contains a decimal point. 
COPY ST 'NEW RECORD%R' AFTER KEY 'HELLO' 
creates a new record at "HELLO" in a string-keyed file. 
00002
00003
00001
LOGICAL_OPERATORS
Syntax: 
         [[ON  ] LP[@location]] 
OUT[PUT] [[OVER] fid          ] [(option[,option]...[)]] 
         [[INTO] ME           ] 
         [[TO]                ] 
Parameters: 
{ON|OVER|INTO|TO}    directs output processing.  OVER causes an existing file 
to the overwritten.  INTO causes file extension. ON and TO are synonyms used 
to create a new file.  If the file exists, an error will occur.  The default 
is ON. 
fid    any valid CP-6 file identifier. 
LP    directs output to the default line printer. @location identifies a 
specific line printer. 
ME    redirects output to the user's terminal. 
option    is one of the following: 
    F[ORM]={formname|'formname'}    FORM applies to unit record files and unit 
    record devices.  Specifies the name of a form to be mounted on a unit 
    record device. formname is a 1-6 character string, which can be quoted. 
    The name must have been defined to the system by the system manager (via 
    the Form Definition File). The default is blank, which means the default 
    form for a unit record device and form 'STDLP' for unit record files. 
    I[XTNSIZE]=value    Specifies an initial disk storage allocation (in 
    blocks) for the output file.  value must be in the range of 1 through 
    134217727.  The default is 2. 
    O[RGANIZATION={C[ONSECUTIVE]|U[NIT]R[ECORD]}    Specifies the organization 
    of the output file as either CONSECUTIVE or UNIT RECORD.  If this option 
    is not specified, the output file is created as a UR file. 
    X[TNSIZE]=value    Use of this option causes an automatic M$EXTEND when 
    needed. value specifies a secondary disk storage allocation (in blocks) 
    for the output file, and must be in the range 1 through 32000.  The 
    default is 2. 
Description: 
This command sends subsequent output to the specified file. 
00002
00001
Syntax: 
OV[ER] [BL[OCK]] block_expression 
Parameters: 
block_expression    is the block of data to be replaced by the source block. 
Description: 
The OVER command is used for replacement.  It is generally equivalent to first 
deleting the destination block by using block_expression, then inserting the 
source block into the location vacated by the destination block.  (The source 
block was set by the last COPY or MOVE command.) 
The source and destination blocks may be whole records, parts of records, or 
any combination of these. 
Example: 
COPY 5 THRU 45 PO 10 OVER 230 THRU 460 
deletes any data characters that previously existed in records 230 through 
460.  It then inserts the new data (from the beginning of record 5 through 
position 10 of record 45) at record 230. 
Related Topics: 
Copy/Move Operations 
COPY Command 
MOVE Command 
AFTER Command 
00002
00003
00001
00004
Syntax: 
{ PA[TTERN] string_expression | 'string' } 
Parameters: 
string_expression    is a string expression which may be empty, (i.e., have no 
characters in its value).  It specifies the pattern to search for in the file. 
string    is a quoted string of characters which may be empty (i.e., '').  It 
specifies the pattern to search for in the file.  If a quote character is to 
be included in string as part of the pattern to search for, then it must 
appear twice (e.g. 'don''t' searches for the word "don't"). 
Description: 
The pattern-string block operand finds a match for a pattern string 
(string_expression) in the enclosing block.  The file pointer is moved to the 
matching data. 
The search for a match is bounded by the enclosing block for the block 
expression.  If a match is not found within the enclosing block, then 6Edit 
will not move the file pointer from its starting location. 
The search for a match of the pattern string ignores record boundaries in the 
enclosing block up to the limit specified by the $MATCH_LIMIT predefined name. 
The $CASE predefined name tells 6Edit how to treat alphabetic characters while 
searching for a match of the pattern string.  If the current value of $CASE is 
ON (or any number >= 1), then file data characters are compared directly with 
characters from the pattern string.  If the current value of $CASE is OFF (or 
any number <= 0), then lower-case alphabetic characters in both the file data 
characters and the pattern string are treated as though they were upper-case. 
The only difference between the two forms of this block operand (use of string 
expression vs. 'string') is that the string_expression form allows you to 
combine strings using the concatenate operator, and/or use EQUALS-names to 
specify the pattern to search for.  The 'string' form is easier to type, 
however, and can be used when the facilities of string expressions are not 
needed. 
The default "point", "direction", and "skip" options for the pattern-string 
operand are $POINT, $DIRECTION, and $SKIP, respectively.  SKIP 0 tests for a 
match at the current cursor location.  SKIP 1 moves forward/backward one 
position before beginning the search. 
00002
00001
Syntax: 
[number-1] {+|.PLUS.} number-2 
[number-1] {-|.MINUS.} number-2 
number-1 {*|.TIMES.} number-2 
number-1 {/|.DIVIDED.} number-2 
Parameters: 
number-1 and number-2    represent the operands to be combined. 
Description: 
These operators perform arithmetic functions with their operands.  All 
operands must be numeric. 
The .PLUS. operator adds its two operands.  If number-1 is omitted, the result 
is number-2 itself. 
The .MINUS. operator subtracts number-2 from number-1, or, if number-1 is 
omitted, from zero. 
The .TIMES. operator multiplies its two operands. 
The .DIVIDED. operator divides number-1 by number-2. 
00002
00001
Syntax: 
PO[SITION[S]] [number                    ] 
              [NU[MBER] string_expression] 
Parameters: 
number    is a decimal number between 1 and 2048, inclusive. 
string_expression    is a string expression.  It must evaluate to a number 
between 1 and 2048, inclusive. 
Description: 
This block operand actually has two forms, with different effects. 
Skipping Over Existing Positions 
The first form of the position operand moves the file pointer over existing 
positions in records: 
    PO[SITION[S]] 
moves the file pointer forward or backward in the current Edit Block some 
number of positions.  The SKIP block option is used to specify the number of 
positions to move; if no SKIP option is used, 6Edit will move the file pointer 
by the number of positions in the $SKIP predefined name. 
This form of the position operand only specifies existing positions in 
records; it will not extend a record.  This means the following: 
o   If the file pointer is at the beginning of a record when a BACKWARD 
    POSITION expression is given, it moves to the end-of-record boundary of 
    the previous record in the enclosing block. 
o   If the file pointer is in the last position of a record when a FORWARD 
    POSITION expression is given, it moves to the end-of-record boundary of 
    that record.  From the end-of-record boundary of a record, this form of 
    the position block operand moves the file pointer either (for BACKWARD) to 
    the last position of that record, or (for FORWARD) to the first position 
    of the next record. 
Moving To a Specific Position In a Record 
The second form of the position operand includes a position number: 
    PO[SITION]  { number | NU[MBER] string_expression } 
moves the file pointer to the specified position in the current record.  If 
the current record is too short, it is lengthened (the value of the $PAD 
predefined name is appended to the record repeatedly until the record is long 
enough). 
The position to move to can be specified either as a number, or as a string 
expression.  Position numbers range from 1 to 2048.  To move the file pointer 
to the first position of a record, use "POSITION 1". 
The second form of the position operand may not be modified by the following 
block options: 
    SKIP 
    FORWARD 
    BACKWARD 
The default "point" option for the second form of the position operand is 
$POINT. 
Examples: 
SKIP 5 POSITIONS 
moves the file pointer forward five positions.  If this moves the file pointer 
beyond the end of the current record, then the file pointer moves to the 
beginning of the next record, and continues movement from there. 
BACKWARD SKIP 3 POSITIONS 
moves the file pointer backward five positions.  If the file pointer starts 
out less than five positions from the beginning of the record, it moves to the 
end of the previous record and continues movement from there. 
POSITION 28 
moves the file pointer to position 28 of the current record.  If the current 
record is shorter than 28 characters long, it is extended to 28 characters, 
using the value of the $PAD predefined name (usually a space character) to 
extend the record. 
POSITION NUMBER MYTAB .MINUS. 8 
subtracts 8 from the current value of the user-created name MYTAB, and uses 
the result as the position number in the current record to move the file 
pointer to.  If the current record is too short, it is extended. 
00002
00005
00004
00001
00003
PROTECT
The following is a list of predefined names: 
$AUTOTAB            $INITIALIZE          $RECORDS_INSERTED   BACKWARD 
$BY                 $INSERT              $RECORDWRAP         BIN10 
$CASE               $INTRO_1             $REKEY              BINHLF 
$COMMAND            $INTRO_2             $RESTORE            BIN521 
$COMMENT            $KEY_GENERATION      $SCREEN             BO 
$CONTEXT            $LEFTOVER            $SCROLL             CURRENT 
$CONTROL            $MATCH_LIMIT         $SITES              DONT_PROTECT 
$DIRECTION          $MATCHES             $SKIP               EO 
$END_MARK           $MAX_COMMAND         $STRIP_BLANKS       FORWARD 
$EXIST              $MAX_RECORD          $TEXTEDIT           HERE 
$EZ_APPEND          $MIN_COMMAND         $VSCROLL            NEW 
$FILEORG            $MIN_RECORD          $VSCROLL_MARGIN     OFF 
$FILERECORDS        $NOT_COPIED          $WI_BORDER          OLD 
$FILETYPE           $PAD                 $WI_PERCENT         ON 
$HSALL              $POINT               $WORDWRAP           PROTECT 
$HSCROLL            $PROTECT             ANY                 STRING 
$HSCROLL_MARGIN     $RECORDS_DELETED     AO                  THAT 
For help on individual predefined names, enter: 
    HELP (6EDIT) PREDEFINED_NAMES name 
Also, the predefined string functions are described under 
    HELP (6EDIT) PREDEFINED_STRING_FUNCTIONS. 
  Name    Assignment Command and Description 
  $AUTOTAB 
          EQUALS a number between 0 and 254, inclusive. 
          The number assigned to this name designates the "autotab position." 
          A value greater than 1 implements automatic tabbing.  Henceforth, 
          the system always begins new records at the autotab position.  To 
          discontinue automatic tabbing, set $AUTOTAB to 0 or 1.  Initially, 
          $AUTOTAB is set to 0. 
          Note that you can also use "Escape Tab" to control automatic 
          tabbing.  Move the cursor to the desired autotab position, and type 
          <ESC> <TAB>.  To discontinue tabbing, move the cursor to the 
          beginning of the record, and type <ESC> <TAB>.  If $TEXTEDIT is set 
          to ON, then any attempt to move into a record (old or new) in a 
          position to the left of the autotab causes an autotab. 
  $BY 
          EQUALS an edit key from 0 to 65.534. 
          The number assigned to this name is the default key increment for 
          new records.  The default is 10.0.  $BY is set and displayed as an 
          edit key.  An edit key is a valid component of a string expression, 
          but cannot be combined with other component values. 
  $CASE 
          EQUALS ON or OFF. 
          This name tells 6Edit how to handle alphabetic case in pattern 
          comparison.  If $CASE equals ON, then data bytes must equal pattern 
          bytes to be considered a match.  If $CASE equals OFF, then data 
          bytes must either equal pattern bytes, or if alphabetic, equal the 
          pattern byte when converted to the opposite case, to be considered a 
          match.  Initially, $CASE is set ON. 
  $COMMAND 
          EQUALS ON or OFF. 
          This name controls which window 6Edit reads.  If $COMMAND EQUALS OFF 
          (the initial setting), 6Edit reads from the editing window.  If 
          $COMMAND EQUALS ON, 6Edit reads from the command window. 
          If you want to type several commands in succession, setting $COMMAND 
          to ON ahead of time eliminates repeatedly telling 6Edit to move the 
          cursor to the command window.  When you finish typing the series of 
          commands, set $COMMAND to OFF.  6Edit then resumes its normal 
          operation. 
  $COMMENT 
          EQUALS one or two characters. 
          The character assigned to this name is used to mark the beginning of 
          commentary in command lines.  When this character appears in a 
          command line but outside of a literal string, 6Edit ignores 
          characters up to the next appearance of the $COMMENT value, or up to 
          the end of the command line.  Characters between the $COMMENT value 
          are assumed to be commentary (arbitrary text meaningful only to you, 
          not to 6Edit).  Initially, the value of $COMMENT is the quotation 
          mark character ("). 
          Enter HELP (6EDIT) $COMMENT for restrictions on the character 
          assigned to $COMMENT and a description of the $COMMENT character's 
          function. 
  $CONTEXT 
          (You cannot assign a value directly.) 
          This variable is a read-only value that returns the fid of the file 
          used as the 6Edit context file. 
  $CONTROL 
          EQUALS one or two characters. 
          Use the character(s) assigned to this name for certain control 
          functions.  If you wish to include the character itself in command 
          lines or string literals, you must enter it twice in succession. 
          You can effectively disable all $CONTROL functions by assigning an 
          empty string to $CONTROL.  Initially, the value of $CONTROL is the 
          percent character (%). 
          Enter HELP (6EDIT) $CONTROL for restrictions on the character 
          assigned to $CONTROL and for a description of the $CONTROL 
          character's function. 
  $DIRECTION 
          EQUALS FORWARD or BACKWARD. 
          This name specifies the default direction in the file in which 
          pattern searching and the SKIP option in block expressions are to 
          proceed.  The initial value is FORWARD. 
  $END_MARK 
          EQUALS a character string. 
          The string assigned to this name defines a line of text to be 
          displayed at end-of-file in the editing window.  The initial value 
          is a blank string (no display).  The maximum length of the string is 
          80 characters.  Any characters can be used; 0 characters or all 
          blanks turns off an existing display.  For example: 
          $END_MARK EQ 'File Ends Here' 
          defines "File Ends Here" as the end-of-file marker. 
          $END_MARK EQ '' 
          resets the marker to blank. 
  $EXIST 
          EQUALS OLD, NEW, or ANY. 
          This name controls the default existence specification for files. 
          $EXIST can be set to suit your particular usage of 6Edit.  For 
          example, if most of your usage of 6Edit is to build new files, 
          setting $EXIST to NEW allows you to open a file with EDIT FILE 
          filename instead of EDIT NEW FILE filename.  Conversely, if most of 
          the files you edit already exist, you could set $EXIST to OLD (which 
          is the default value).  If you work with an equal number of existing 
          and new files, setting $EXIST to ANY eliminates the need for either 
          the OLD or NEW keyword with EDIT FILE. 
  $EZ_APPEND 
          EQUALS ON or OFF. 
          This name controls what is needed to extend (insert a blank line at 
          the end of) a file in the editing window.  When $EZ_APPEND is set to 
          ON, any attempt (such as a carriage return) to position the cursor 
          to column 1 of the line below the last record in the file will 
          extend the file.  When this feature is OFF, the last record in the 
          file must not be empty for the file to be extended.  The default is 
          OFF. 
  $FILEORG 
          (You cannot assign a value directly.) 
          This variable is a read-only value that returns the file 
          organization of the file currently being edited (corresponding to 
          the CURR location variable). 
  $FILERECORDS 
          (You cannot assign a value directly.) 
          This variable is a read-only value that returns the number of 
          records in the file currently being edited (corresponding to the 
          CURR location variable). 
  $FILETYPE 
          EQUALS a 2-character string. 
          The characters assigned to this name are used to change the file 
          type for the current file, if it is changeable, and to set the 
          default for any NEW FILEs created thereafter.  (The current file is 
          the file being edited [corresponding to the CURR location 
          variable].)  This variable may also be used to return the file type 
          of the file currently being edited.  Note that the default for NEW 
          FILEs may not be the same as the value displayed by SHOW $FILETYPE, 
          since that command always displays the current file's type.  DELETE 
          WINDOW can be used to obtain access to the default value or to set 
          the default without changing the current file. 
  $HSALL 
          EQUALS ON or OFF. 
          This name controls how lines are to be scrolled when horizontal 
          scrolling is in effect.  When $HSALL is ON, all the lines of a 
          screen editing window are scrolled when a horizontal shift occurs. 
          A value of OFF specifies to scroll only the record containing the 
          cursor.  The default is OFF. 
  $HSCROLL 
          EQUALS a number between 0 and half the screen width, inclusive. 
          The number assigned to this name specifies how many columns to 
          scroll the editing window when trying to move the cursor into a 
          horizontal scrolling margin.  Initially, $HSCROLL is 0. 
          If $HSCROLL is greater than 0, that is, if horizontal scrolling is 
          enabled, 6Edit scrolls the the editing window horizontally so that 
          the character on which the cursor lies is at the center of the 
          editing window. 
  $HSCROLL_MARGIN 
          EQUALS a number between 0 and half the screen width, inclusive. 
          The number assigned to this name specifies the number of columns in 
          the horizontal scrolling margins.  A designated number of columns 
          represents these margins at the right and left of the editing 
          window. 
          Initially, $HSCROLL_MARGIN is set to 0; there are no horizontal 
          scrolling margins, and horizontal scrolling is disabled.  Setting 
          $HSCROLL_MARGIN to a particular number of columns forces the window 
          to scroll horizontally when the cursor reaches the designated 
          column, for example the fourth column from the left or right edge of 
          the screen when $HSCROLL_MARGIN is set to 4. 
  $INITIALIZE 
          EQUALS a string expression consisting of 6Edit commands separated by 
          the $CONTROL-record function. 
          The commands assigned to this name are interpreted immediately 
          following restoration of the context file at startup, thus allowing 
          "active" commands such as SHOW or IBEX commands to be included in 
          saved context files.  Note that any $CONTROL-functions in the 
          commands other than those that separate the commands must use the 
          $CONTROL-literal function to express the $CONTROL identifier (e.g., 
          the command SHOW STRING '%V(33)A' would be specified for use in 
          $INITIALIZE as 'SH STRING ''%%V(33)A'''. 
          At startup, until the first editing command is given, 6Edit remains 
          in serial mode ($SCREEN EQ 0), using the window set in M$6E (the 
          default is ME, which uses UC01).  So, until the first editing 
          command that needs to build an editing window, any operations that 
          affect the building of windows will continue to have an effect when 
          the windows are finally built.  For example, $INITIALIZE can be used 
          to move the IBEX window to the bottom of the screen by setting it to 
          '!LDEV UC98,POSITION=BOTTOM,WL=1%R!ADJUST M$6E UC01' 
          The second command (!ADJUST M$6E UC01) tells 6Edit to use all the 
          rest of the screen for editing, instead of its default, which is 
          "all-but-the-top-line". 
  $INSERT 
          EQUALS ON or OFF. 
          This name controls the insertion mode.  Initially, the insertion 
          mode is disabled by its initial setting ($INSERT EQUALS OFF).  In 
          this case, the characters typed replace the characters beneath the 
          cursor, unless the cursor is at the end of the "insertion window" 
          established with the Escape > or Escape J functions.  When the 
          insertion mode is enabled ($INSERT EQUALS ON), characters typed are 
          always inserted at the cursor location; they never replace 
          characters at the cursor. 
          Note that the insertion mode is also enabled with the Escape ' 
          function, and disabled with either the Escape M or Escape O 
          function. 
  $INTRO_1 
          EQUALS one or two tokens.  The first may be a $KEY function.  The 
          second, if present, must be a character. 
          The characters assigned to this name represent the primary 
          introducer for KEYIN names (IMP functions).  Initially, 6Edit uses 
          the escape character <ESC> as the primary introducer. 
  $INTRO_2 
          EQUALS one or two tokens.  The first may be a $KEY function.  The 
          second, if present, must be a character. 
          The characters assigned to this name represent the secondary 
          introducer for KEYIN names (IMP functions).  Initially, 6Edit 
          assumes no secondary introducer.  If your KEYIN names use a 
          secondary introducer, you must tell 6Edit (by setting $INTRO_2) 
          before you use the KEYIN command. 
  $KEY_GENERATION 
          EQUALS BIN10, BINHLF, BIN521, or STRING. 
          This name specifies how the FEP is to generate keys for new records 
          inserted by means other than 6Edit's COPY or MOVE commands.  If 
          $KEY_GENERATION is set to BIN10 (the default), the key increment is 
          divided by 10 repeatedly to find a usable increment.  For the 6Edit 
          default key increment of 10, inserted records would be separated by 
          one of 10.000, 1.000, .100, .010, or .001 whichever works first.  If 
          $KEY_GENERATION is set to BINHLF, the key increment is halved 
          repeatedly.  For the key increment of 10, the inserted records would 
          be separated by 10.000, 5.000, 2.500, 1.250, .625, etc.  If 
          $KEY_GENERATION is set to BIN521, the key increment is divided by 5, 
          2.5, and 2, and is then repeated.  For the key increment of 10, the 
          inserted records would be separated by 10.000, 5.000, 2.000, 1.000, 
          .500, .200, .100, etc.  If $KEY_GENERATION is set to STRING, 
          insertion of new records is not permitted.  STRING overrides any 
          specification for string-keyed files. 
          In general, the BIN10 default may permit inserting a larger number 
          of records in the same spot than would BINHLF or BIN521.  Those 
          values may be useful for inserting one or two records at a time and 
          will tend to have a more even distribution of key numbers, but with 
          more fractional keys. 
  $LEFTOVER 
          (You cannot assign value directly.) 
          Whenever the source data for a copy operation does not fit into the 
          destination block and $REKEY does not permit automatic rekeying, 
          some portion of a single record of the source data may be saved as 
          the value of the $LEFTOVER name.  (6Edit does this internally when 
          such an error occurs.)  6Edit tells you that it has stored some of 
          the source data in $LEFTOVER.  Once you have corrected the original 
          problem, you may use $LEFTOVER as the source for another copy 
          operation. 
          When such an error occurs, either $LEFTOVER or $NOT_COPIED, or both, 
          may be set.  If $LEFTOVER is set, the data contained therein no 
          longer remains in the file.  If $NOT_COPIED is set, it simply refers 
          to the location of the data that remains in the file. 
  $MATCH_LIMIT 
          EQUALS a number. 
          The value assigned to this name specifies the maximum number of 
          records which the match of a pattern expression can span. 
          Initially, the value of $MATCH_LIMIT is 1; the entire pattern 
          expression must match data residing in, at most, one record.  If, 
          for example, you were to set $MATCH_LIMIT to three, then all pattern 
          expressions may match up to a three record span anywhere in the 
          enclosing block. 
          $MATCH_LIMIT limits any $CONTROL pattern-match function except 
          $CONTROL-Record; $MATCH_LIMIT applies independently to each pattern 
          substring between any $CONTROL-Record functions. 
          When $MATCH_LIMIT is greater than 1, adjacent strings may match the 
          pattern even if the strings span a record boundary.  For instance, 
          if the pattern is "reports from this office" and the file contains 
          these strings split between two records: 
               ................reports from 
               this office................. 
          then the occurrence in the file is considered a match, even though 
          the pattern string contains a blank between "from" and "the", while 
          the occurrence in the file contains only a record boundary there. 
          For example, consider the following pattern string: 
              'abc%?def' 
          If, when this is evaluated: 
          $MATCH_LIMIT = 1 - Both "abc" and "def" must be found in the same 
          record for a match to be found. 
          $MATCH_LIMIT = 5 - "abc" must match in one record or two adjacent 
          ones, and "def" must match in one record or two adjacent ones; 
          however, there may be up to three records between the "a" record and 
          the "f" record, so that the entire match spans five records. 
  $MATCHES 
          (You cannot assign value directly.) 
          After each pattern search, 6Edit assigns a value to $MATCHES.  This 
          value represents the number of matches found for patterns in this 
          evaluation of the block expression.  Note that if a block expression 
          contains more than one pattern operand, the value assigned to 
          $MATCHES will be the sum of the matches found for both patterns. 
  $MAX_COMMAND 
          EQUALS a number. 
          This name tells 6Edit how large to expand the command window when it 
          displays messages (i.e. error or HELP messages).  The number 
          assigned to this name is the number of lines on the terminal screen 
          of the largest command window.  The minimum value is 1; the maximum 
          value is the height (in lines) of your terminal screen.  Initially, 
          $MAX_COMMAND is set to approximately half the height of the terminal 
          screen. 
  $MAX_RECORD 
          EQUALS a number between 0 and 2048, inclusive. 
          The value of this name is the maximum length, in bytes, of records 
          written to files in 6Edit.  If you change a record, and its length 
          is greater than $MAX_RECORD, 6Edit truncates bytes from the end of 
          the record so that it is $MAX_RECORD bytes long.  Initially, 
          $MAX_RECORD is set to 2048. 
  $MIN_COMMAND 
          EQUALS a number. 
          This name tells 6Edit how small to diminish the size of the command 
          window when you type commands, or when you are editing in the 
          editing window.  The number assigned to this name is the number of 
          lines in the smallest command window.  The minimum value is 0; the 
          maximum value is the height (in lines) of your terminal screen. 
          Initially, $MIN_COMMAND is set to 2. 
  $MIN_RECORD 
          Equals a number between 0 and 2048, inclusive. 
          The value of this name is the minimum length, in bytes, of records 
          written to files by 6Edit.  If you change a record, and its length 
          is less than $MIN_RECORD, 6Edit appends the value of the $PAD name 
          to the record repeatedly, until it is $MIN_RECORD bytes long. 
          Initially, $MIN_RECORD is set to 1.  In this case, all records will 
          be at least 1 byte long. 
  $NOT_COPIED 
          (You cannot assign value directly.) 
          When the source data for a copy operation does not fit into the 
          destination block, the location of some portion of the source data 
          may be saved as the $NOT_COPIED name.  (6Edit does this internally 
          when such an error occurs.)  $NOT_COPIED is a location name; it does 
          not hold the actual data, but rather remembers the location of that 
          part of the source block that was not copied to the destination due 
          to error.  6Edit tells you when it has saved the locations of some 
          of the source data in $NOT_COPIED.  Once you correct the original 
          problem, you may use $NOT_COPIED as the source for another copy 
          operation. 
          When such an error occurs, either $LEFTOVER or $NOT_COPIED, or both, 
          may be set.  If $LEFTOVER is set, the data contained therein no 
          longer remains in the file.  If $NOT_COPIED is set, it simply refers 
          to the location of the data that remains in the file. 
  $ONESPACEEDIT 
          EQUALS ON or OFF 
          This name controls the number of spaces used between sentences when 
          the format command ESC-2-LF is used.  When $ONESPACEEDIT is off, 2 
          spaces are used between sentences, otherwise 1 space is used. 
          Initially, $ONESPACEEDIT is OFF. 
  $PAD 
          EQUALS a character string. 
          The value of this name is used to "pad" records which are shorter 
          than the minimum specified by $MIN_RECORD.  The minimum length of 
          the value of $PAD is 1; the maximum length is 100.  Initially, $PAD 
          is set to a single space character. 
  $POINT 
          EQUALS AO, BO, or EO 
          This name specifies the default file position option for block 
          expressions.  AO (ALL OF, the default) causes the entire block to be 
          selected.  For example, a SELECT clause may move the cursor to the 
          beginning of the block; END OF THAT would move it to the other end. 
          BO (BEGINNING OF) causes only the beginning of the block to be 
          selected; EO (END OF) causes only the end of the block to be 
          selected. 
          Note:  $POINT must not be set to EO for commands such as SHOW which 
          select records by key, since EO RE is actually the beginning of the 
          record following the desired one. 
  $PROTECT 
          EQUALS PROTECT or DONT_PROTECT 
          This name controls the default protect status for files.  $PROTECT 
          can be set to suit your particular usage of 6Edit.  For example, if 
          you usually just read files without updating them (and want them 
          protected), setting $PROTECT to PROTECT allows you to open a file 
          with EDIT FILE filename instead of EDIT PROTECT FILE filename. 
          Conversely, if you usually update files rather than just read them, 
          setting $PROTECT to DONT_PROTECT (the default) allows you to open a 
          file with EDIT FILE filename instead of EDIT DONT PROTECT FILE 
          filename. 
  $RECORDS_DELETED 
          (You cannot assign value directly.) 
          After each DELETE, OVER, or MOVE command, 6Edit assigns a value to 
          $RECORDS_DELETED.  This value represents the number of records 
          deleted from the file by the command.  Note that only entire records 
          are counted; if only a portion of a record is deleted, it will not 
          be included in the $RECORDS_DELETED value. 
  $RECORDS_INSERTED 
          (You cannot assign value directly.) 
          Following each AFTER or OVER command, 6Edit assigns a value to 
          $RECORDS_INSERTED.  This value represents the number of new records 
          inserted into the file by the command. 
  $RECORDWRAP 
          EQUALS ON or OFF. 
          This name controls the record wrap mode.  Initially, the record wrap 
          mode is disabled ($RECORDWRAP EQUALS OFF).  In this case, any 
          attempt to move the cursor beyond the ends of a record is ignored. 
          When the record wrap mode is enabled ($RECORDWRAP EQUALS ON), the 
          actions of following input editing functions are modified when the 
          cursor is in the editing window. 
          <ESC> <D> or <CNTL-H> 
              (BS) 
              If the cursor is at the first position of a record, it will 
              move to just beyond the last position of the previous 
              record. 
          <ESC> <C> or <CNTL-R> 
              (DC2) 
              If the cursor is beyond the end of a record, it will move 
              to the first position of the next record. 
          <ESC> <V> 
              The search for the character typed after the <V> is not 
              limited to the current record; however, it is limited to 
              the records currently displayed in the editing window. 
          <CNTL-W> 
              (ETB) 
              Moves to the next or previous word in the record or, if 
              necessary, in the next or previous record. 
  $REKEY 
          EQUALS a number between 0 and 1000. 
          The value of this name controls automatic rekeying of the file.  If 
          $REKEY is set to zero, 6Edit never automatically rekeys the file. 
          If $REKEY is greater than zero, 6Edit tries to rekey as small a 
          range up to its value in first the forward direction and then 
          backwards as will permit the rekeyed records plus the inserted ones 
          to be separated by the current increment value (from a BY clause in 
          the command, or the $BY predefined name).  If neither direction is 
          successful, the entire file is rekeyed instead.  (No attempt is made 
          to find a combination of forward and backward records.)  Sometimes, 
          if the number of records involved is small, a smaller increment is 
          used.  The initial value is 100. 
  $RESTORE 
          EQUALS a character string. 
          The string assigned to this name is an IBEX command.  The IBEX 
          command should not begin with an exclamation character (!).  When 
          6Edit exits, the current value of $RESTORE is passed to IBEX to 
          execute.  Usually, this IBEX command causes your normal terminal 
          environment to be restored.  IBEX commands used frequently are the 
          IMP command, to process an IMP source or object file, and the XEQ 
          command, to perform several functions.  If $RESTORE has no value 
          assigned to it, (e.g., $RESTORE EQUALS ''), then no such action is 
          taken when 6Edit exits. 
  $SCREEN 
          EQUALS ON, OFF, or an integer. 
          This name controls the size of the editing screen.  Setting $SCREEN 
          to 0 (OFF) requests serial editing by removing from the screen all 
          editing windows.  At startup, 6Edit sets $SCREEN OFF if the user is 
          operating in batch mode or if the user's terminal profile indicates 
          that screen editing is impossible.  For an online CRT user running 
          with $SCREEN OFF, setting $SCREEN to ON (or 1) restores the terminal 
          to screen editing with editing windows in the same proportions as 
          before.  The size of the IBEX window can be increased (from 1 line) 
          by setting $SCREEN. 
          See Section 2, Serial Editing, for more information.  If screen 
          editing is not possible, $SCREEN may only be set to 0. 
  $SCROLL 
          EQUALS ON or OFF. 
          This name controls scrolling in the command window.  The default is 
          ON.  With scrolling on, consecutive entries in the command window 
          are scrolled upward.  With scrolling off, the asterisk (*) prompt 
          remains at the top of the command window; consecutive entries are 
          cleared when they reach the editing line.  OFF is particularly 
          useful on terminals where scrolling windows that do not extend to 
          the bottom of the screen are awkward. 
  $SITES 
          (You cannot assign value directly.) 
          After each command, 6Edit assigns a value to $SITES.  This value 
          represents the number of blocks found during evaluation of the 
          command.  If the command did not include the REPEAT keyword, the 
          $SITES will be set to either 0 or 1; only if REPEAT is used will 
          $SITES be greater than 1. 
  $SKIP 
          EQUALS a number from 0 to 131071. 
          This name specifies the number of times to repeat some relative 
          movement of the file pointer within the specified block.  The value 
          assigned to $SKIP is used if no SKIP option is present in the 
          PATTERN, POSITION, or RECORD block operands.  The default is zero. 
  $STRIP_BLANKS 
          EQUALS ON or OFF. 
          This name controls the stripping of trailing blanks from records 
          written by 6Edit.  If you change a record and $STRIP_BLANKS is set 
          to ON, any space characters at the end of the record (which are not 
          followed by any non-space characters) are removed from the record. 
          Initially, $STRIP_BLANKS is set ON. 
  $TEXTEDIT 
          EQUALS ON or OFF. 
          This name controls the spacing between words when joining or 
          splitting text lines.  With $TEXTEDIT ON, a blank space is 
          automatically added between words (the last word of the first line 
          and the first word of the next line) when joining two lines.  When 
          splitting a line at the blank space before a word, the blank is 
          automatically removed so that the new (next) line starts with the 
          word, not the blank.  If $AUTOTAB is set, then any attempt to move 
          into or create a record at a position to the to the left of the 
          autotab causes an autotab.  Initially, $TEXTEDIT is set OFF. 
  $VSCROLL 
          EQUALS a number between 0 and the length of the screen, inclusive. 
          The number assigned to this name specifies how many lines to scroll 
          the editing window when trying to move the cursor into a vertical 
          scrolling margin. 
          When you reset $VSCROLL to 0, 6Edit scrolls the editing window so 
          that the record in which the cursor lies is at the center of the 
          editing window.  Initially, $VSCROLL is set to 0. 
  $VSCROLL_MARGIN 
          EQUALS a number between 0 and half the length of the screen, 
          inclusive. 
          The number assigned to this name specifies the number of lines in 
          the vertical scrolling margins.  A designated number of lines 
          represents these margins at the top and bottom of the editing 
          window.  When you try to move the cursor into one of these margins, 
          the window scrolls in the opposite direction; the cursor will not 
          remain in the vertical scrolling margin. 
          Setting $VSCROLL_MARGIN to a particular number of lines forces the 
          window to scroll when the cursor reaches the designated line, for 
          example the sixth line from the top or the bottom when 
          $VSCROLL_MARGIN is set to 6.  Initially, $VSCROLL_MARGIN is set to 
          approximately 25% of the height of the editing window. 
  $WI_BORDER 
          EQUALS any single character. 
          This name specifies the character used for the border that divides 
          the command and editing windows.  The hyphen (-) is the default. 
          $WI_BORDER should be used in a context file, or set before any 
          editing commands are used in a 6Edit session.  If set to a null 
          string (''), no border is used.  This is useful with $MIN_COMMAND EQ 
          0, which then allows the entire screen to be used for editing.  (If 
          a PC is being used, this also lets the PC Terminal Facility save 
          lines that scroll off the top in its history buffer.) 
  $WI_PERCENT 
          EQUALS a number from 1 to 99. 
          The value assigned to this name is used in creation of windows. 
          Rather than specifying the size of the new window to create, this 
          name specifies the percentage of space remaining in the old window. 
          For example, to create three even-sized windows in a 21-line editing 
          space using the LINES option, "NE WI;NE WI LI 14;NE WI LI 7" would 
          be used (presuming that no editing windows existed previously). 
          Using the PERCENT option, "NE WI;NE WI 67;NE WI 33" would be used; 
          but using the defaults, "$WI_PERCENT EQ 33;NE WI;NE WI;NE WI" would 
          suffice.  The default for $WI_PERCENT is 50. 
  $WORDWRAP 
          EQUALS a number between 0 and 254, inclusive. 
          The number assigned to this name specifies the right margin for the 
          "wordwrap mode."  A value greater than 11 implements the wordwrap 
          mode.  The wordwrap mode removes a word which crosses the right 
          margin from its original record, and replaces it at the beginning of 
          a newly-inserted record.  To discontinue the wordwrap mode, set 
          $WORDWRAP to any value between 0 and 11. 
          Note that you can also use the Escape ^ function to control the 
          wordwrap mode.  Move the cursor to the intended right margin, and 
          type <ESC> <^>.  To discontinue this wordwrap mode, repeat this 
          sequence, positioning the cursor at the beginning of the record. 
          The wordwrap mode allows you to enter textual material without 
          concern with line length.  As you type the text, 6Edit only allows 
          you to type as far as the right margin.  When you cross that margin, 
          the system automatically begins a new record.  If a word crosses the 
          right margin, it moves that word to the new record also.  You may 
          thus type without ever touching the Return key.  Initially, the 
          $WORDWRAP mode is disabled. 
  ANY 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 3. 
  AO 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 1. 
  BACKWARD 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 2. 
  BIN10 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 4. 
  BINHLF 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 5. 
  BIN521 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 6. 
  BO 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 2. 
  CURRENT 
          (You cannot assign value directly.) 
          This name points to the current edit block.  You set it using the 
          EDIT command, and use it when block expressions specify no explicit 
          enclosing block.  You can use CURRENT to refer to the entire edit 
          block for movement, data selection, etc.  (See Section 5, Block 
          Expressions in 6Edit.)  6Edit accepts the "CURR" abbreviation. 
  DONT_PROTECT 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 2. 
  EO 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 3. 
  FORWARD 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 1. 
  HERE 
          (You cannot assign value directly.) 
          HERE points to the current location of 6Edit's file pointer.  6Edit 
          updates the value of HERE automatically after performing each 
          editing command. 
  NEW 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 1. 
  OFF 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 0. 
  OLD 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 2. 
  ON 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 1. 
  PROTECT 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 1. 
  STRING 
          (You cannot assign value.) 
          This is a predefined constant; the value is always 7. 
  THAT 
          (You cannot assign value directly.) 
          This name points to the current selected block, the block operated 
          on by the last editing command.  6Edit updates the value of this 
          name automatically after each editing command.  If the last editing 
          command deleted its operand, THAT points to the empty block where 
          the deleted operand resided.  This empty block can then be used as 
          the destination of a new insertion replacing the deleted operand. 
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
00025
00024
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
00046
00047
00048
00049
00050
00051
00052
00053
00054
00056
00055
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
00068
00069
PREDEFINED_STRING_FUNCTIONS
Following is a list of the predefined string functions supported by 6Edit. 
$ABS                $HSET               $RERUN 
$ACCT               $INDEX              $SEARCH 
$CMDVAR             $INPUT              $SITE 
$DATE               $KEY                $SUBSTR 
$DAY                $KEYIN              $SWITCH 
$DIR                $LASTBATCH          $SYSID 
$EOF                $LENGTH             $TERM_FEP 
$FID_ASN            $LOC                $TERM_LINE 
$FID_EXIST          $MAX                $TERM_PROFILE 
$FID_GRANS          $MIN                $TERM_SPEED 
$FID_NGAVAL         $MOD                $TIME 
$FID_ORG            $MODE               $UPC 
$FID_RECS           $NAME               $VERIFY 
$FID_TYPE           $PRIV_ACTIVE        $VERSION 
$FID_UGRANS         $PRIV_AUTH          $WOO 
$FLAG               $REM 
For more information about a specific predefined string 
function, type: 
HELP PREDEFINED_STRING_FUNCTION function 
For example: 
HELP PREDEFINED_STRING_FUNCTION $HSET 
or 
HELP PREDEFINED_STRING_FUNCTION $PRIV_AUTH 
  Name    Description 
  $ABS(expression) 
          Returns the absolute value of the expression.  The expression must 
          be numeric. 
  $ACCT 
          Returns the account portion of the current logon. 
  $CMDVAR(command_variable_name) 
          Returns the value of a command variable defined in IBEX with !LET, 
          which is compatible with the variables defined in 6Edit with EQUALS. 
          $CMDVAR(command_variable_name) allows access to the values of 
          variables defined in IBEX just as %command_variable_name is used in 
          IBEX. 
  $CNTL(expression) 
          Returns the expression string as though the control key had been 
          depressed.  For example, $CNTL('[W') is equivalent to 
          <ESC>||<CNTL-W>. 
  $DATE 
          Returns the date in the form YYMMDD.  An optional parameter 
          TYPE='type' may be supplied.  The 'type' expression may be EXT, ANS, 
          or LOCAL.  For example: 
          !OUTPUT $DATE (TYPE='ANS') 
          841203 
          !OUTPUT $DATE (TYPE='EXT') 
          DEC 03 '84 
          !OUTPUT $DATE (TYPE='LOCAL') 
          12/03/84 
  $DAY 
          Returns SUN, MON, TUE, WED, THU, FRI, or SAT. 
  $DIR 
          Returns the current directory account. 
  $EOF 
          Returns 1 if an end-of-file has been encountered on M$UC.  Returns 0 
          otherwise. 
  $FID_ASN(expression) 
          Expression is evaluated to a string that is treated as a file name. 
          $FID_ASN performs a call to M$FID, but does not try to OPEN the FID. 
          If the M$FID call was successful, the assignment type (ASN) is 
          returned.  Examples are FILE, DEVICE, and COMGROUP.  If the file 
          does not exist or cannot be accessed, then an error message is 
          displayed, and the command is aborted. 
  $FID_EXIST(expression) 
          Expression is evaluated as a string that is treated as a file name. 
          If an attempt by IBEX to open the file yields any result other than 
          "file does not exist", then $FID_EXIST returns a 1.  This is no 
          guarantee that the user may access the file.  Returns a 0 otherwise. 
          If the file does not exist or cannot be accessed, then an error 
          message is displayed, and the command is aborted. 
  $FID_GRANS(expression) 
          Expression is evaluated as a string that is treated as a file name. 
          $FID_GRANS specifies the size of the file in total number of 
          granules.  If the file does not exist or cannot be accessed, then an 
          error message is displayed, and the command is aborted. 
  $FID_NGAVAL(expression) 
          Expression is evaluated as a string that is treated as a file name. 
          $FID_NGAVAL specifies the size of the file in number of unused 
          granules in the file.  If the file does not exist or cannot be 
          accessed, then an error message is displayed, and the command is 
          aborted. 
  $FID_ORG(expression) 
          Expression is evaluated as a string that is treated as a file name. 
          CONSEC, KEYED, RANDOM, INDEXED, RELATIVE, IDS, etc.  If the file 
          does not exist or cannot be accessed, then an error message is 
          displayed, and the command is aborted. 
  $FID_RECS(expression) 
          Expression is evaluated as a string that is treated as a file name. 
          $FID_RECS specifies the size of the file in number of records.  If 
          the file does not exist or cannot be accessed, then an error message 
          is displayed, and the command is aborted. 
  $FID_TYPE(expression) 
          $FID_TYPE returns the two-character file type of the file.  If the 
          file does not exist or cannot be accessed, then an error message is 
          displayed, and the command is aborted. 
  $FID_UGRANS(expression) 
          Expression is evaluated as a string that is treated as a file name. 
          $FID_UGRANS specifies the size of the file in number of Ugranules. 
          If the file does not exist or cannot be accessed, then an error 
          message is displayed, and the command is aborted. 
  $FLAG(fname) 
          $FLAG returns YES if a particular IBEX flag is set; otherwise it 
          returns NO.  The fname may be any of the following: 
               PROTECT        DRIBBLE       AC/CEPT BRO/ADCAST 
               LIST           ECHO          AC/CEPT SEND 
               COMMENT        NOTIFY        AC/CEPT AN/NOUNCE 
  $HSET 
          Returns the home packset name. 
  $INDEX(expression 1,expression 2[,expression 3[,expression 4]]) 
          Expressions 1 and 2 are evaluated to strings of characters; 
          expressions 3 and 4, if given, must be numeric.  $INDEX returns the 
          index into expression 1 where expression 2 was found.  If expression 
          2 is not found, the length of expression 1 is returned.  If both 3 
          and 4 are omitted, then all of expression 1 is searched for 
          expression 2.  If expression 3 is included, then it specifies the 
          beginning position for the search within expression 1.  If 
          expression 4 is included, then it specifies the ending position for 
          the search within expression 1.  The first character in the string 
          is position 0. 
  $INPUT(expression) 
          Prompts through the command window (M$ME) with expression.  Returns 
          a reply from the user.  If the user's reply includes leading or 
          trailing blanks, these are stripped from the input.  When the user 
          desires the blanks not be stripped, the input string must be 
          enclosed in quotes (which will be stripped).  Doubled quotes within 
          a quote string are translated to a single quote in the resultant 
          string. 
  $KEY(keyname) 
          Specifies the keyin name (string_expression_1) in a KEYIN command; 
          can be used in an EQUALS command to define a KEYIN introducer.  $KEY 
          can also be used anywhere else with a standard ASCII control 
          character mnemonic or a hex value as the keyname parameter, and is 
          simply an alternate way to express the indicated character. 
          Enter HELP (6EDIT) KEYIN for more information on $KEY. 
  $KEYIN(expression) 
          Sends expression to the system consoles.  $KEYIN suspends execution 
          until it receives a reply from the system console.  $KEYIN then 
          takes on the value of the reply.  If the user's reply includes 
          leading or trailing blanks, these are stripped from the input.  When 
          the user desires the blanks not be stripped, the input string must 
          be enclosed in quotes (which will be stripped).  Doubled quotes 
          within a quote string are translated to a single quote in the 
          resultant string. 
  $LASTBATCH 
          The syntax for this command is $LASTBATCH.  Returns the sysid of the 
          last job issued via the BATCH command. 
  $LENGTH(expression) 
          The syntax for this command is $LENGTH.  Returns the number of 
          characters in expression.  The length of a string expression is one 
          greater than the last character used in that expression. 
  $LOC(expression) 
          Returns the string expression converted to lower case. 
  $MAX(exp1,exp2,...expn) 
          Returns the value of the largest expression.  All expressions must 
          be numeric. 
  $MIN(exp1,exp2,...expn) 
          Returns the value of the smallest expression.  All expressions must 
          be numeric. 
  $MOD(exp1, exp2) 
          Returns the arithmetic modulus of exp1 and exp2.  Both exp1 and exp2 
          must be numeric. 
  $MODE 
          Returns ONLINE, BATCH, GHOST, or TP, whatever mode in which the user 
          currently operates. 
  $NAME 
          Returns the name portion of the logon. 
  $PRIV_ACTIVE(pname) 
          Returns YES if a particular IBEX PRIV bit is turned on.  The pname 
          may be FMSEC, etc. 
  $PRIV_AUTH(pname) 
          Returns YES if a particular IBEX PRIV bit is authorized.  The pname 
          may be FMSEC, etc. 
  $REM(exp1, exp2) 
          Returns the remainder of exp1 and exp2.  Both exp1 and exp2 must be 
          numeric; exp2 may not be 0. 
  $RERUN 
          Returns 1 if this job is being rerun automatically by the system. 
          Otherwise, it returns 0. 
  $SEARCH(expression 1,expression 2[,expression 3[,expression 4]]) 
          Expressions 1 and 2 are evaluated to strings of characters; 
          expressions 3 and 4, if given, must be numeric.  $SEARCH checks each 
          character in expression 1 for membership in expression 2.  The index 
          of the first match is returned; if not found the length of 
          expression 1 is returned.  If expression 3 is included, then it 
          specifies the beginning position for the search within expression 1. 
          If expression 4 is included, then it specifies the ending position 
          for the search within expression 1.  The first character in the 
          string is position 0. 
  $SITE 
          Returns the textual site identification. 
  $SUBSTR(expression 1[,expression 2[,expression 3]]) 
          Expression 1 is evaluated to a string of characters; expressions 2 
          and 3, if given, must be numeric.  A character string is extracted 
          from expression 1 beginning at the nth position as specified by 
          expression 2 with a length specified by expression 3.  If expression 
          2 is not specified then the first character is assumed.  If 
          expression 3 is not specified then the length of expression 1 minus 
          expression 2 is assumed.  The first character in the string is 
          position 0. 
  $SWITCH(expression) 
          Returns the value 0 or 1 of the specified SWITCH.  The expression 
          must evaluate to a numeric value between 0 and 35.  Switches are set 
          by the IBEX SWITCH command. 
  $SYSID 
          Returns the user's sysid. 
  $TERM_FEP 
          Returns node of the user's FEP. 
  $TERM_LINE 
          Returns the channel to which the user is connected. 
  $TERM_PROFILE 
          Current terminal profile. 
  $TERM_SPEED 
          Returns communication speed in bits per second, e.g. 300, 1200, etc. 
          Note:  The TERM functions will return an error message if mode is 
          not ONLINE. 
  $TIME 
          Returns the current time in the form HHMM.  An optional parameter 
          TYPE='type' may be supplied.  The 'type' expression may be EXT, ANS, 
          or LOCAL.  For example: 
          !OUTPUT $TIME (TYPE='ANS') 
          1224 
          !OUTPUT $TIME (TYPE='EXT') 
          12:24 
          !OUTPUT $TIME (TYPE='LOCAL') 
          12:24 
  $UPC(expression) 
          Returns the string expression converted to upper case. 
  $VERIFY(expression 1,expression 2[,expression 3[,expression 4]]) 
          Expressions 1 and 2 are evaluated to strings of characters; 
          expressions 3 and 4, if given, must be numeric.  Each character of 
          expression 1 is checked for membership in expression 2.  $VERIFY 
          returns the first non-match; if not found, it returns the length of 
          the expression.  If expression 3 is included, then it specifies the 
          beginning position for the search within expression 1.  If 
          expression 4 is included, then it specifies the ending position for 
          the search within expression 1.  The first character in the string 
          is position 0. 
  $VERSION 
          Returns the current version of the CP-6 system. 
  $WOO 
          Returns the current workstation of origin. 
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
00046
00047
00048
00023
00024
Predefined names serve several purposes: 
o   They provide a shorthand notation for certain commonly-used values.  Some 
    of these values are constants, and some are changed by 6Edit internally. 
o   They allow you to give 6Edit certain operating values, and allow you to 
    request that 6Edit perform certain functions.  This method of telling 
    6Edit what to do is used only for those functions which do not change 
    often.  Thus, 6Edit equips you to control many small details. 
You refer to these names by using 6Edit's substitution facility.  You use most 
predefined names just like user-defined names. 
Predefined names differ from user-defined names in two respects: 
o   You cannot assign values to some of the predefined names in the usual way, 
    that is, with the assignment commands.  Of those predefined names which 
    cannot be assigned a value with the assignment commands, some have 
    constant values, and 6Edit assigns new values to others internally. 
o   Of the predefined names to which you can assign a value with the 
    assignment commands, most can only be assigned values by specific 
    assignment commands.  This is because different assignment commands assign 
    different types of values to names.  The legal assignment command for each 
    predefined name is listed in the names' descriptions below.  If you try to 
    use the wrong command to assign a value to a particular name, 6Edit will 
    reject the command. 
Syntax: 
PRINT [ALL|ldevlist] 
Parameters: 
ALL    specifies that the accumulated outputs for all logical devices are to 
be sent to their destinations immediately.  This is the default. 
ldevlist    specifies that the accumulated outputs for the specified logical 
device or devices are to be sent to their destination(s) immediately.  The 
list is entered in the format 
    ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
PRINT directs that output accumulated for logical devices be sent to its 
destination immediately. 
Example: 
PRINT LP01,LP02 
causes the accumulated output associated with logical devices LP01 and LP02 to 
be sent immediately to the associated destinations. 
Related Commands: 
ERASE 
00002
00003
00001
00004
The processing options give 6Edit additional instructions on how to process a 
block after evaluation. 
The processing options apply to the result of the evaluation of the entire 
block expression, not to just one operand in the expression.  Therefore, in a 
command line, the processing options are typed before or after the entire 
block expression. 
o   The protect option controls modification of the contents of the block 
    during editing.  PROTECT prohibits any modification of the data in the 
    block during the processing of the command which includes the block 
    expression.  DONT PROTECT explicitly allows modification.  The default is 
    $PROTECT. 
o   The exist option performs a test on the file you are about to process. 
    After locating the file specified by a block expression, 6Edit examines 
    the exist option (if any) included in the block expression.  NEW tells 
    6Edit that this block evaluation succeeds only if the file does not exist, 
    hence the file is created.  OLD tells 6Edit that the block evaluation 
    succeeds only if the file does exist.  ANY creates the file if it does not 
    exist, or uses it if it does exist.  The default is $EXIST. 
o   The structure option tells 6Edit how to treat the file in terms of record 
    keys and insertion techniques. 
o   The key increment option tells 6Edit how to generate new record keys when 
    inserting records into a file.  It is used on blocks which will be the 
    destination of a copy or move operation.  6Edit inserts records into 
    destination blocks; it needs to generate new record keys for these 
    inserted records.  BY tells 6Edit how to generate new record keys based on 
    the existing record keys of records in the block.  The default is $BY. 
Syntax: 
[DONT] PR[OTECT]  block_expression 
Parameters: 
block_expression    must begin with a FILE block operand. 
Description: 
When not preceded by DONT, PROTECT tells 6Edit that its block_expression is to 
be protected from any changes.  The block_expression may not be altered or 
deleted, and no new records may be added. 
DONT PROTECT tells 6Edit to allow modification of the block. 
When specifying the edit block in the EDIT command, giving the PROTECT option 
to the block expression will essentially provide read-only access to the file 
as long as that file is the current edit block. 
If an attempt is made to alter a PROTECTed block, 6Edit will reject the 
attempt and issue a beep at the terminal to inform the user of the attempted 
violation. 
00002
00001
END
RECORD
Syntax: 
READ fid 
Parameters: 
fid    is the fid of a file containing valid 6Edit commands. 
Description: 
This command directs 6Edit to read the specified file (fid).  The file 
specified by fid must contain one 6Edit command line in each record.  6Edit 
reads the command lines and executes them as if they had been typed at the 
terminal, except that KEYIN substitutions are not performed.  6Edit stops 
reading command lines from the file when it reaches the end of the file; then 
it reverts to reading command lines from the command stream. 
You may include a READ command as one of the commands in the file specified by 
fid.  You may nest READ commands in this way indefinitely. 
When using multiple commands on a line, the READ command can appear at any 
place on the command line. 
00002
00001
Syntax: 
RE[CORD[S]] 
Description: 
RECORD is a relative block operand.  It specifies a block whose starting point 
is POSITION 1 of a record and whose ending point is POSITION 1 of the next 
record (i.e., the end-of-record boundary is included in the block). 
When searching for this operand, the search for the starting point of the 
RECORD aims in the direction specified by any FORWARD or BACKWARD options for 
this operand; however, once the starting point is found, RECORD always 
specifies the record from that starting point forward to the end-of-record 
boundary, including that end-of-record boundary. 
The default "point", "direction", and "skip" options for the record operand 
are $POINT, $DIRECTION, and $SKIP, respectively.  SKIP 0 specifies the entire 
record that the cursor is positioned in.  SKIP 1 specifies the next/previous 
(forward/backward) record. 
Examples: 
SKIP 20 RECORDS 
moves the file pointer forward in the file, skipping over 20 records. 
DELETE RECORD 
deletes the entire record in which the file pointer currently lies. 
COPY RECORD AFTER L 
copies the record in which the file pointer currently lies to the location 
named "L", where "L" is assumed to be a name created by the user with the 
LOCATION command. 
00001
00002
NUMERIC_KEY
When 6Edit tries to create a new record key and is not able to and $REKEY is 
zero, it will abort the operation.  If the file is an edit-keyed file, you can 
rekey the file and resume the operation using the following command: 
    COPY CURRENT OVER CURRENT 
The synonym REKEY, defined in the standard context files, can be used instead: 
    REKEY 
This command can only be used when you are editing the entire file. 
Optionally, you can add the BY option to control the record keys used when 
rekeying the file as follows: 
    COPY CURRENT OVER CURRENT BY 5 
    or 
    REKEY BY 5 
uses 5.0 as the first record key in the rekeyed file.  Each successive record 
will have a key which is larger by five more increments than the previous key 
(i.e., the rekeyed file's keys will be 5.0, 10.0, 15.0, 20.0, ...). 
Syntax: 
string-1 {=|.EQ.} string-2 
string-1 {~=|.NE.} string-2 
string-1 {<|.LT.} string-2 
string-1 {<=|.LE.} string-2 
string-1 {>|.GT.} string-2 
string-1 {>=|.GE.} string-2 
Parameters: 
string-1    is a string expression.  It evaluates to the operand to be 
compared. 
string-2    is a string expression.  It represents the value to which string-1 
is compared. 
Description: 
These operators compare their two operands. 
If both operands are numeric, then a numeric comparison is performed (10 is 
equal to 010, 01 is less than 010).  If either operand is not numeric, a 
character-by-character string comparison is performed.  If one string is 
shorter than the other, 6Edit pads it with blanks. 
The result computed by each of these operators is a numeric operand:  either 
1, indicating that the relation is true, or 0, indicating that the relation is 
false. 
The result of the .EQ. operator is true if the two strings are equal, false 
otherwise. 
The result of the .NE. operator is true if the two strings are unequal, false 
otherwise. 
The result of the .LT. operator is true if string-1 is less than string-2, 
false otherwise. 
The result of the .LE. operator is true if string-1 is less than or equal to 
string-2, false otherwise. 
The result of the .GT. operator is true if string-1 is greater than string-2, 
false otherwise. 
The result of the .GE. operator is true if string-1 is greater than or equal 
to string-2, false otherwise. 
00002
00001
A "relative" block operand is a block which may be located anywhere in any 
file.  For instance, a record as a block (with no record key) may be located 
anywhere in a file.  A file is typically made up of many such records. 
The relative block operands are RECORD, POSITION, and pattern-string. 
Relative block operands are used to tell 6Edit in a relative way how to move 
the file pointer.  The location of the file pointer after evaluating the 
operand is relative to the location of the file pointer before evaluating the 
operand.  For example, assume that the file pointer is at position 21 of 
record 62 in file "ABC"; you can tell 6Edit to move forward five RECORD.  In 
this use, RECORD is a relative block operand; its actual location is relative 
to the current location of the file pointer.  No specific record key was 
given, only "direction" and "skip" block options ("forward" and "five" 
respectively). 
All the relative block operands specify a block located at or around the 
current file pointer location.  By preceding the operand with the SKIP option, 
you can move the file pointer forward or backward in units of the block 
operand; for example, SKIP moves by records with the RECORD operand, but by 
positions within a record when used with the POSITION operand, and by 
pattern-matches when used with the pattern-string operand. 
o   RECORD specifies the record to which the file pointer points as the block 
    operand. 
o   POSITION specifies as the block operand the one data character to which 
    the file pointer currently points.  It may also be used to specify a 
    position within the record to which the file pointer currently points. 
o   "Pattern-string" is a string expression; its value is a pattern to search 
    for within the enclosing block.  If a match is found, the matching data in 
    the enclosing block is the block operand specified by "pattern-string." 
To specify a repeated block, precede the block expression with a REPEAT SELECT 
clause. 
Including a repeated block expression in a command causes the entire command 
to be repeated until the end of the enclosing block is reached.  On each 
repetition of the command, the block expression evaluates to successive 
blocks. 
6Edit continuously evaluates repeated block expressions.  On the first 
evaluation, the file pointer starts at its current location.  The 
block_expression should contain movement expressions which move the file 
pointer through the enclosing block, first to the beginning, and then to the 
end of the block being specified. 
On successive evaluations, the file pointer starts at the end of the block 
specified by this block_expression on the previous evaluation.  The 
block_expression then moves the file pointer (relative to the end of the 
previously-found block) first to the beginning, and then to the end of the 
next block for block_expression. 
Example: 
Assume you want to replace whatever appears between the words "the Piercy " 
and " we sold", with the word "novel".  That is, the following strings in the 
file will be changed to "the Piercy novel we sold": 
    the Piercy book we sold 
    the Piercy picture we sold 
    the Piercy novella on urban renewal we sold 
However, the string "the Atwood book we sold" does not change. 
To do this, specify a repeated block, searching for the given patterns to find 
the start and the end of the block to be replaced: 
COPY STRING 'novel' OVER REPEAT SELECT EO 'the Piercy ' THRU BO ' we sold' 
contains a REPEAT SELECT clause.  This causes the COPY OVER command to be 
repeated as long as the block expression following SELECT can find a block in 
the file.  The block expression is: 
EO 'the Piercy ' THRU BO ' we sold' 
specifying two patterns to be searched for.  The block found by this block 
expression begins at the end of (EO) the next string in the file matching the 
first pattern, and ends at the beginning of (BO) the next string in the file 
matching the second pattern.  When these two patterns are found, all data 
between them is replaced with the string 'novel'. 
After each replacement, 6Edit repeats the pattern search (because REPEAT was 
specified).  Starting from the end of the found block (in this example, the 
beginning of " we sold"), 6Edit searches again for the first pattern ("the 
Piercy ").  If it finds a match, 6Edit searches for the second pattern, and if 
it finds a match for that pattern, another replacement is made.  Then, 6Edit 
repeats the evaluation of the block expression, searching for the first 
pattern again. 
This repetition continues until the end of the file (or other enclosing block) 
is reached in one of the pattern searches. 
00001
There are two modes available for typing data in 6Edit: the replacement mode 
and the insertion mode.  (There is another mode, the overstrike mode, but its 
use is more specialized, and is not described here.)  These modes are 
available whenever you use CP-6; they are described here only because they are 
particularly helpful when using 6Edit. 
You may do all your editing in either mode, or you may switch between modes. 
The technique you use is a matter of personal preference as well as the nature 
of your editing. 
When you logon to CP-6, you are initially in the replacement mode.  In this 
mode, each character you type replaces the character under the cursor.  You 
can insert characters into a record at the end of the record.  To insert 
characters anywhere else in the record, you must define an "insertion window" 
by typing <ESC> <J>, or <ESC> <>>; then, characters you type at the right end 
of the insertion window are inserted into the record at that point. 
The insertion window "encloses" the action of many input editing functions. 
For example, the <ESC> <CR> sequence moves the cursor to the beginning of the 
insertion window.  If you move the cursor beyond the insertion window, the 
window expands, encompassing the entire record. 
Syntax: 
REST[ORE]  fid 
Parameters: 
fid    specifies the fid of a file which was created with 6Edit's SAVE 
command. 
Description: 
The RESTORE command restores context information from a file which was created 
with the SAVE command.  It merges the information from the SAVE-file with the 
current context in the following way: 
o   SYNONYMs and KEYINs from the SAVE-file are added to those already defined 
    when the RESTORE command is given. 
o   Predefined EQUALS-names from the SAVE-file replace the values of all 
    predefined EQUALS-names at the time the RESTORE command is given.  That 
    is, the values of all predefined names are saved in the SAVE-file; 
    therefore, when the RESTORE command is given, all operating parameters are 
    restored to their values as saved in the SAVE-file. 
o   User-defined EQUALS-names from the SAVE-file are added to the EQUALS-names 
    already defined when the RESTORE command is given. 
o   LOCATION-names from the SAVE-file are added to those already defined when 
    the RESTORE command is given.  If the files to which these names refer no 
    longer exist, or if they have been rekeyed, then using such LOCATION-names 
    may give unexpected results. 
o   If the SAVE-file contains window information (i.e., if SAVE SESSION or 
    SAVE ALL was used to create the SAVE-file), then when the RESTORE command 
    is given, any editing windows and their edit block stacks are discarded. 
    In addition, the editing window information from the SAVE-file is used to 
    create a new editing window(s) and edit block stack(s).  Again, if the 
    files to which this window information refers no longer exist, or if they 
    have been rekeyed, then the RESTORE command may give unexpected results. 
Related Commands: 
SAVE 
00002
00001
00003
Syntax: 
     [ AL[L]     ] {  TO  } 
SAVE [ SETU[P]   ] {  ON  }  fid 
     [ SESS[ION] ] { OVER } 
Parameters: 
fid    is the fid of the file to save the requested context information in. 
ALL    saves all of the context file information. 
SETUP    saves the value of all EQUALS-names, KEYIN-names, and SYNONYM-names. 
It does not save the value of LOCATION-names or any window information. 
SESSION    saves the value of all LOCATION-names, as well as information about 
the windows currently on your terminal screen.  For the editing windows, this 
includes the window dimensions, the files you are currently editing, the 
current locations of the cursor, and the entire edit block stacks (the files 
you edited previously), for each editing window. 
Description: 
The SAVE command directs 6Edit to save current context information in a file. 
The file created by the SAVE command is called a "SAVE file".  The SAVE file 
can be used later to restore the saved context using the RESTORE command (or 
using the file as the context file which is read when 6Edit is started, see 
Context Files).  If you do not specify the type of information to be saved, 
all the current context file information is saved. 
If "TO fid" or "ON fid" is used, the file specified by fid must not yet exist; 
the SAVE command creates the file.  If "OVER fid" is used, then the SAVE 
command replaces the file if it already exists, or creates it if it does not 
yet exist. 
The file created by a SAVE command is a special encoded "workspace" file, with 
file type "We".  It cannot usefully be edited using EDIT or 6Edit, and should 
not be altered in any way by the user.  6Edit can detect most changes to the 
file, and will not restore an encoded context file which has been modified. 
Related Topics: 
RESTORE Command 
Context Files 
00002
00001
00003
6Edit typically divides the screen as illustrated in Figure 2-1 and explained 
in the following paragraphs.  Additional capabilities affecting screen 
appearance -- multiple editing windows and serial editing -- are described 
later in this section. 
6Edit normally divides the terminal screen into three "windows":  the "IBEX 
window" in the top line of the screen, the "command window" in the upper half 
of the screen, and the "editing window" in the lower half of the screen.  A 
straight line across the screen forms a "border" which separates the IBEX and 
command windows from the editing window. 
                     ------------------------ 
                     |    IBEX window       | 
                     |                      | 
                     |*   command window    | 
                     |                      | 
                     |                      | 
                     |----------------------| 
                     |                      | 
                     |                      | 
                     |    editing window    | 
                     |                      | 
                     |                      | 
                     ------------------------ 
You can edit the characters appearing in any window using the input editing 
functions.  Input editing functions (entered at the keyboard) are key 
sequences beginning with the control (<CNTL>) or escape (<ESC>) key. 
Syntax: 
[REPEAT] SE[LECT] block_expression 
Parameters: 
block_expression    must not include absolute block operands.  Only relative 
block operands may be included in "block_expression." 
Description: 
The SELECT clause is used for either or both of two purposes:  to specify 
repeated blocks, and/or to enclose blocks. 
If REPEAT is given, then block_expression is a 
 repeated block. 
00002
00001
The "selected block" is the last block you specified, either by moving the 
file pointer (cursor) or by entering commands.  You manipulate the selected 
block using the editing commands:  it can be deleted, moved, replaced, etc. 
For example, if you move the cursor to the beginning of a sentence, type THRU 
in the command window, then move the cursor to the end of the sentence, you 
have designated the new selected block.  If you then type DELETE THAT in the 
command window, 6Edit deletes the sentence from the file. 
6Edit provides the serial editing mode for circumstances when full-screen 
editing is inappropriate or inefficient.  These cases are as follows: 
o   When using 6Edit non-interactively (i.e., as a result of the IBEX BATCH or 
    XEQ commands) 
o   When using 6Edit online at a non-CRT terminal that permits neither full 
    screen display nor scrolling 
o   When using 6Edit to perform well-defined editing tasks such that it is 
    more efficient not to wait for the editing window to be filled with a full 
    screen of data every time the file pointer is pointed elsewhere within the 
    file. 
Note that in serial editing, window-specific values for EQUALS-names and 
KEYINs are ignored, as is the size and position of a new window created with 
the WINDOW command. 
When serial editing, a block expression by itself as a command (with no 
editing verb such as COPY or AFTER) moves the file pointer without displaying 
any data.  To display data, an explicit DISPLAY command is necessary. 
When 6Edit is started, it determines if the user is running online and if the 
terminal can support screen editing.  If the user is not online or if the 
terminal profile reveals that the terminal cannot screen edit, 6Edit forces 
the user into serial editing mode.  That is, it sets the predefined name 
$SCREEN to 0 (the height of the terminal "screen"). 
The online CRT user choose between serial editing and screen editing by 
setting $SCREEN back to the number of lines that 6Edit should use as the 
screen size.  Setting $SCREEN to ON (or 1) restores the current maximum screen 
size allowed.  Setting $SCREEN to OFF (or 0) enters serial mode. 
In serial editing mode, with $COMMAND set on (the default), 6Edit commands are 
used to manipulate the data.  With $COMMAND off, 6Edit prompts with the key of 
the "here" record, and uses reread mode for editing the data. 
Special activation characters perform special functions: 
<LF> terminates editing of the current record, and moves to the next one. 
    <LF> is <CNTL-J>. 
<EOT> terminates editing of the current record, and moves to the previous one. 
    <EOT> is <CNTL-D>. 
<SYN> splits the current record at the cursor position, and possibly moves to 
    the new one, depending on whether it is empty.  If wordwrap is set, typing 
    at the end, past the wordwrap position, will cause the insertion of a new 
    record just as it does in screen editing mode.  <SYN> is <CNTL-V>. 
Other activation characters (i.e., all normal ones plus <ETX>) cause a command 
prompt, just as in screen editing. 
CONTEXT_FILE
Syntax: 
SH[OW] option 
Parameters: 
option    is one of the following: 
ST[RING] string_expression    displays the string represented by 
string_expression. 
KE[YINS]    displays the keyin definitions. 
[EQ[UALS]] [name [TH[RU] name2]]    displays one, some, or all EQUALS 
definitions. 
LO[CATIONS] [name [TH[RU] name2]]    displays one, some, or all LOCATIONS 
definitions. 
SY[NONYMS] [name [TH[RU] name2]]    displays one, some, or all SYNONYMS 
definitions. 
[BL[OCK]] block_expression    displays complete records selected by a block 
expression, preceded by the record key in an appropriate format. 
[WI[NDOWS]]    displays window definitions. 
Description: 
The SHOW command is used for terminal display of string operands, the values 
of names created with assignment commands (KEYIN, EQUALS, LOCATION, and 
SYNONYM), and records within a selected block. 
The SHOW command displays its output through M$LO, which defaults to the 
command window.  Unless the command is activated with <LF> (instead of a 
carriage return), the command window is first expanded to occupy the space 
used by the editing window and the IBEX window, and one additional read from 
the command window is forced after the display.  With <LF>, the display is 
presented in the command window and the cursor returns immediately to the 
editing window. 
In SHOW displays of KEYIN definitions or EQUALS names for which different 
definitions exist for different windows, the window for which a definition 
applies is indicated in parentheses after the name.  (edt) represents the 
first editing window.  (cmd) represents the command window.  (edn) represents 
the nth editing window. 
Example: 
SHOW STRING $KEY(ESC)||'[36m' 
On a color ANSI-compatible terminal, changes the display to a light-blue 
color. 
SHOW STRING HERE||', '||$DATE(TY='LOCAL')<LF> 
displays the current file FID, record key, column, and date in the command 
window, without interrupting the editing window. 
SHOW $AUTOTAB 
displays the current setting of the $AUTOTAB EQUALS variable (predefined 
name). 
SHOW 'A' 
displays the next record in the current file that contains an "A". 
SHOW FILE :6EDIT_CONTEXT REPEAT SELECT RECORD SELECT 'A' 
displays all records in the file :6EDIT_CONTEXT that contain an "A". 
SHOW $NOT_COPIED 
displays the records that were not included in a failed copy operation. 
SHOW LO $NOT_COPIED 
displays a block expression describing the records that were not included in a 
failed copy operation. 
SHOW $INSERT 
displays the current setting of the $INSERT EQUALS variable.  If $INSERT is 
set to ON only in the command window, the display would be 
"$INSERT(cmd)      ON". 
SHOW WINDOWS 
displays the current window definitions. 
00002
00003
00001
A block operand yields a "signal."  The signal indicates the success or 
failure of the evaluation of the block operand. 
The evaluation of a block operand (as modified by any block options specified 
with it) fails in these four cases: 
o   An absolute operand specifies a block which is located completely outside 
    the boundaries of the current enclosing block.  For example, if the 
    enclosing block is records 50 through 100 of a file, a record key operand 
    specifying record 200 will fail when evaluated. 
o   A pattern-string operand fails when evaluated if 6Edit cannot find a match 
    for the pattern string inside the boundaries of the current enclosing 
    block. 
o   A repeated block has already been evaluated the specified number of times. 
o   The starting range for evaluation of the next instance of a repeated block 
    is outside the boundaries of the enclosing block. 
Failure in evaluating a block operand is not considered an error.  It is 
usually a perfectly normal occurrence, and controls evaluation of the block 
expression.  For example, to replace all appearances of a string in a file 
with another string, you specify a repeated block to COPY OVER all matches of 
a pattern string.  This repeated block causes the command which includes it 
(the COPY OVER command) to be repeated for each match of the pattern string. 
When 6Edit cannot find any more pattern string matches, evaluation of the 
pattern-string block operand fails, thus terminating processing of the 
command.  This failure is intended, and is not an error. 
Syntax: 
SK[IP] number relative_block 
Parameters: 
number    is a string expression.  It must evaluate to a number which is 
greater than or equal to zero. 
relative_block    must be a relative block operand. 
Description: 
The SKIP option tells 6Edit to repeat the relative movement specified by 
relative_block some number of times.  The number parameter specifies the 
"repeat count." 
Remember, movement of the file pointer is limited to the bounds of the 
enclosing block.  If you specify SKIP 10 RECORDS, but fewer than ten records 
remain in the enclosing block, the file pointer moves only to the end of the 
enclosing block. 
If the repeat count evaluates to zero, then 6Edit assumes that the current 
location of the file pointer lies within the bounds of the destination block. 
For example, if the file pointer is currently at position 10 of a record, then 
END OF SKIP 0 RECORDS moves it to the end of that same record. 
Example: 
SKIP 10 RECORDS 
6Edit moves the file pointer 10 records. 
00002
00003
00001
Several predefined names are reserved as special location_names.  They can be 
used in block expressions just like any other location_name, however, their 
value is determined by 6Edit (you cannot explicitly assign a value to these 
names).  As for all other names, they may be entered in either upper-, mixed-, 
or lower-case. 
CURRENT 
The CURRENT predefined name always specifies the current edit block.  The edit 
block is set by the EDIT command, the NEXT and PREVIOUS block operands, and 
implicitly whenever the enclosing block for a block expression is in a 
different file than the current edit block.  The name CURRENT can be 
abbreviated to CURR. 
THAT 
The THAT predefined name always specifies the current selected block.  The 
selected block is the block of data operated upon by the most recent editing 
command. 
HERE 
The HERE predefined name always specifies an empty block.  This block is 
located at the current file pointer location. 
$LEFTOVER 
The $LEFTOVER predefined name contains some portion of a single record of the 
source data that does not fit into the destination block on a copy operation. 
Once you have corrected the problem that caused the incomplete copy, you may 
use $LEFTOVER as the source for another copy operation. 
$NOT_COPIED 
The $NOT_COPIED predefined name contains the location of some portion of the 
source data that does not fit into the destination block on a copy operation. 
Once you have corrected the problem that caused the incomplete copy, you may 
use $NOT_COPIED (which is a location name but does not hold the actual data) 
to perform another copy operation. 
Examples: 
BO CURRENT 
moves the file pointer to the beginning of the current edit block (usually to 
the beginning of the file being edited). 
COPY THAT AFTER EO CURRENT 
contains two special location_names as block operands:  "THAT" and "CURRENT". 
Assuming the user has just selected a block, this COPY command copies that 
selected block to the end of the current edit block (usually to the end of the 
file being edited). 
COPY L AFTER HERE 
contains two names as block operands:  "L" and "HERE".  "L" is assumed to be a 
name created by the user with the LOCATION command, so that it names the 
location of a block (either in the current file or in any other file).  This 
COPY command copies the block at location "L" to the current file pointer 
(cursor) position. 
00004
00005
00001
00006
00003
00002
Splitting records allows you to insert blank lines, and add new records to the 
file.  Type <ESC> <LF> to "split" a record, i.e. break it up into two separate 
records.  The characters under and to the right of the cursor are removed from 
the current record and placed in a record which is inserted into the file 
following the current record.  To insert new records in the middle of a file, 
type <ESC> <N> to go to the end of the record, and then type <ESC> <LF>.  This 
creates a new record after the initial record. 
Another way to insert records in the middle of a file is from the beginning of 
the record.  Type <ESC> <CR> to go to the beginning of the record.  Then type 
<ESC> <LF>.  This creates a new record at the cursor line. 
To add data at the end of a file, go to the end of the file, using the EO CURR 
command in the command window.  This command positions the cursor on a blank 
line.  Type the new record.  Then type either <CR> or <ESC> <LF>. 
Using <ESC> <BS>, you can join two records together into one record.  This 
function works only when the cursor is at the beginning or the end of the 
record.  If the cursor is at the beginning of the record, it joins this record 
to the previous record.  If the cursor is at the end of the record, the 
following record attaches to the last character of the cursor record when you 
type <ESC> <BS>. 
The presence of a blank space between words when joining or splitting lines is 
controlled by the $TEXTEDIT predefined name. 
STRING

Syntax: 
ST[RING] string_expression 
Parameters: 
string_expression    is any string expression.  It may include 
$CONTROL-Record, $CONTROL-Value, $CONTROL-Wildcard, and $CONTROL-Question 
functions. 
Description: 
Any string specified as a string expression can be included in a block 
expression as a block operand. 
The string value of the string expression is treated as a file; it becomes the 
enclosing block for the rest of the block expression. 
The STRING operand must stand alone; you may not select a block within the 
value of the string expression, using the usual block operands.  The string is 
usually treated just like a one-record consecutive file; however, by including 
the $CONTROL-Record function in the string expression, you can create a 
multi-record file. 
Example: 
COPY STRING 'novels and literary criticism' OVER REPEAT SELECT 'books' 
searches forward in the file for any matches of the pattern "books", and 
replaces them with the string "novels and literary criticism". 
COPY STRING '%W(2) %?' OVER '%? %?' 
switches the current word in the file with the next one. 
When used in a string block operand, the $CONTROL-Wildcard function must have 
exactly one parameter whose value is greater than zero.  When the operand is 
eventually used by an AFTER or OVER command, the $CONTROL-Wildcard function is 
replaced by the string that matched a $CONTROL-Question or $CONTROL-Wildcard 
function in a pattern string for the command.  The parameter specifies which 
particular $CONTROL-Question or $CONTROL-Wildcard function in the pattern is 
to be substituted, counting from the beginning of the pattern string at one. 
For example, a $CONTROL-Wildcard function with a parameter value of 3 would be 
replaced by the string that matched the second occurrence of "%?" in the 
pattern string "begin%?mid1%W(5,10)mid2%?end".  If the parameter exceeds the 
number of wildcard strings in the pattern, the function is ignored. 
The $CONTROL-Question function, which permits no parameters, can also be used 
in a string block operand, and is exactly equivalent to a $CONTROL-Wildcard 
function with a parameter value of one. 
A maximum of ten combined $CONTROL-Wildcard and $CONTROL-Question functions 
may be used in any string block operand. 
00002
00003
00001
A string expression can specify either a character or a numeric value, 
depending on how it is used.  Certain commands and string operators anticipate 
character operands.  For them, an expression which evaluates to a numeric 
value is converted to a character string containing a decimal representation 
of the numeric value.  If a command or string operator expects a numeric 
operand and you supply a string expression which evaluates to a character 
value, then 6Edit assumes that the string contains a decimal representation of 
a number, and tries to convert the string to a numeric value.  If the string 
does not contain a reasonable decimal representation of a number, 6Edit 
rejects the expression and the command in which it is used.  The maximum 
length of a string expression is 511 characters. 
String expressions consist of functions, operators, constants, and variables. 
In 6Edit (and IBEX) string expressions, constants are either decimal numbers 
or quoted strings.  Variables are symbols whose values have been defined by 
6Edit EQUALS (and IBEX LET) commands, or by the processor itself (such as the 
6Edit predefined names and IBEX system variables). 
Most of the 6Edit's string operators and functions are also implemented by 
IBEX. 
        $ABS           $FID_ORG       $LOC           $SUBSTR 
        $ACCT          $FID_RECS      $MAX           $SWITCH 
        $CMDVAR        $FID_TYPE      $MIN           $SYSID 
        $CNTL          $FID_UGRANS    $MOD           $TERM_FEP 
        $DATE          $FLAG          $MODE          $TERM_LINE 
        $DAY           $HSET          $NAME          $TERM_PROFILE 
        $DIR           $INDEX         $PRIV_ACTIVE   $TERM_SPEED 
        $EOF           $INPUT         $PRIV_AUTH     $TIME 
        $FID_ASN       $KEY           $REM           $UPC 
        $FID_EXIST     $KEYIN         $RERUN         $VERIFY 
        $FID_GRANS     $LASTBATCH     $SEARCH        $VERSION 
        $FID_NGAVAL    $LENGTH        $SITE          $WOO 
        &   .AND.                       <=  .LE. 
        <?  .CONTAINS.                  <   .LT. 
        || !! .CONCAT.                  =?  .MATCHES. 
        /   .DIVIDED.                   -   .MINUS. 
        =   .EQ.                        ~=  .NE. 
        >=  .GE.                        ~   .NOT. 
        >   .GT.                        |   .OR. 
        ?=  .IMB.                       +   .PLUS. 
        ?>  .IN.                        *   .TIMES. 
Note that string operators can be typed as symbols, or words.  If words are 
used, however, they must be enclosed by periods. 
The special characters used as string operators are not reserved for this use. 
You can use the SYNONYM command to assign a special character to some other 
6Edit keyword or command. 
For example, the dash (-) is often interpreted to mean "through."  To use the 
dash in this way, you would define it as a synonym for the 6Edit THRU keyword: 
    SYNONYM - THRU 
After defining the dash to mean THRU, you cannot use it to mean subtract. 
Instead, use .MINUS. to perform subtraction functions, or define another 
synonym: 
    SYNONYM _ .MINUS. 
After defining these two synonyms, you can use a dash (-) to mean THRU, and an 
underscore (_) to mean subtract. 
Example: 
Using the above synonyms, 
DI 5-10 
means display records 5 through 10. 
SIZE EQ 5_10 
means the name SIZE now has the value -5. 
00001
"Substitution" refers to the substitution of the value of a name for the name 
itself.  Substitution may occur when you enter command lines and data to 
6Edit; substitution may also be performed on input from your terminal and from 
command files. 
In 6Edit, there are four methods of substitution.  These correspond to the 
four types of values which a name may have. 
Syntax: 
SY[NONYM] name [IS] fragment 
Parameters: 
name    can be any character other than $CONTROL, $COMMENT, semi-colon (;), or 
have a digit as the first character. 
fragment    is any set of words, quoted strings, or special characters, up to 
the end of the command line. 
Description: 
The SYNONYM command assigns to name any fragment of a 6Edit command line.  It 
is used to create your own variations of the basic syntax. 
Because name can be either a normal name (which looks like a keyword) or a 
string of special characters (which looks like an operator symbol), you can 
create your own syntax by defining name to be some series of already-defined 
names or symbols. 
The fragment parameter specifies any set of words, quoted strings, or special 
characters, up to the end of the command line. 
The following restrictions apply to the fragment parameter: 
o   Quoted strings must be completely specified (that is, you cannot have 
    unbalanced string delimiters in a fragment). 
o   The command separator character semicolon (;) has no effect in a fragment 
    when the SYNONYM command is processed.  That is, it does not mark the end 
    of the SYNONYM command; instead, it is included in a fragment.  Later, 
    when name is given in a command line, any semicolons included in the 
    fragment (along with the other characters in a fragment) are recognized, 
    and demarcate separate commands in the command line. 
    A semicolon appearing at the end of a command line normally indicates that 
    the command is continued on the next line.  However, this is not true when 
    a SYNONYM command appears in the command line.  As for the command 
    separator, the trailing semicolon is included in the fragment.  Later, 
    when the SYNONYM name is given in a command line, the trailing semicolon 
    in a fragment is treated as a command separator, if more characters follow 
    the SYNONYM name on the command line, or as a command line continuation 
    indicator, if no characters follow the SYNONYM name. 
o   Other substitutions can be used in a fragment.  Specifically, names 
    defined with previous SYNONYM commands may appear.  Substitutions for them 
    take place when this SYNONYM command is processed and before the new value 
    is assigned to name.  Names defined with the EQUALS and LOCATION commands 
    may also appear in a fragment; however, substitutions for them do not 
    occur until name is used later in a command line. 
o   The current $COMMENT character is recognized in a fragment, and has its 
    usual effect at the time the SYNONYM command is processed. 
o   6Edit does not recognize $CONTROL characters in quoted strings until the 
    synonym is used.  Then, only the current value of $CONTROL is 
    acknowledged.  Be careful when using $CONTROL functions in a fragment:  do 
    not change the value of $CONTROL, or unexpected results might occur. 
Example: 
SYNONYM EP IS EDIT PREVIOUS 
makes EP a synonym for EDIT PREVIOUS.  When EP is typed at the command prompt, 
6Edit will perform the EDIT PREVIOUS command. 
SYNONYM - THRU 
renders the dash (-) a synonym for THRU.  When you type <-> in a command, 
6Edit henceforth interprets it as the THRU keyword. 
Related Topics: 
Substitution 
00002
00003
00001
00004
The string_expression designates the pattern string.  It tells 6Edit how to 
identify a "match" in the enclosing block. 
Most characters in the pattern string specify values which must appear in 
identical form and identical order in the enclosing block in order to yield a 
"match."  For instance, if you say: 
     abc 
then the only match possible is a string of three characters in the enclosing 
block, whose values are the lowercase ASCII characters a, b, and c, in that 
order.  An exception to this "exact match" rule is made if the $CASE 
predefined name is OFF when the pattern search is made. 
The pattern string is specified by a string expression.  This allows 
non-displayable character values to be included in the string (using the 
$CONTROL-Value function). 
Several of the $CONTROL functions have special meaning when they appear in the 
pattern string.  Also, some additional $CONTROL functions are supported only 
when they appear in pattern strings; these are called "pattern functions." 
THRU
Syntax: 
{TH[RU]|TH[ROUGH]} [movement_expression] 
Parameters: 
movement_expression    is a movement expression. 
Description: 
THRU tells 6Edit that "movement_expression" specifies the ending location of 
the block being specified.  Whenever THRU is seen, the current file pointer 
location becomes the beginning of the block being specified. 
If "movement_expression" is omitted, the block being specified becomes an 
empty block (containing zero data characters) located at the current file 
pointer location.  If "movement_expression" is included, it should move the 
file pointer to the desired ending location for the block being specified. 
Enter: 
HELP (6EDIT) MOVEMENT_EXPRESSION 
for more information regarding movement expressions. 
Example: 
DE 20.1 
deletes the entire record 20.1. 
DE 20.1 THRU 25 
deletes all records between and including 20.1 and 25. 
5 THRU 
specifies a block beginning and ending at the start of record 5.0.  This is an 
empty block. 
THRU 6 
specifies a block beginning at the current file pointer location, and ending 
at the start of record 6.0. 
00002
00003
00001
PLUS
Syntax: 
TIME 
Parameters: 
None 
Description: 
TIME displays the current time and date.  The format of the display is: 
mmm dd 'yy hh:mm    (month)(day)(year)(hours)(minutes) 
Example: 
TIME 
displays the current time and date. 
Related Commands: 
DATE 
00002
00003
00001
00004
PLUS
In a block expression, you can use the basic block operands which are 
predefined by 6Edit, or you can define a block yourself and use it as a block 
operand.  For example, you can define a group of three contiguous records as a 
block, then use this block as a block operand in a block expression. 
In fact, the result of any block expression is a "user-defined block." 
By combining the basic block operands and other user-defined block operands 
with "block options" and "block operators," you can define a user-defined 
block to be any continguous set of data characters anywhere in any file.  This 
is done generally as follows. 
After indicating the file in which the data characters reside, you use block 
operators and operands to move a file pointer through the file.  The file 
pointer points to a single character in a record.  Usually, you delimit a 
block by: 
1.  Moving the file pointer to the first character of the block (the starting 
    point); 
2.  Typing the THRU keyword; 
3.  Moving the file pointer to the character following the last character of 
    the block (the ending point). 
Note that blocks need not start or end on record boundaries. 
Basically, a block expression specifies three things: 
o   The "enclosing block."  This is the file (or other block) in which the 
    block being specified resides.  If omitted, the edit block is used as the 
    enclosing block.  In commands, you can specify an enclosing block which is 
    different than the edit block by explicitly naming the file (or other 
    absolute block operand; see below) to use as the enclosing block for this 
    block expression. 
    The enclosing block limits the movement of the file pointer and hence the 
    bounds of the block being specified by the block expression.  The block 
    being specified must lie completely within the bounds of the enclosing 
    block. 
o   The starting point of the block.  If omitted and an enclosing block was 
    specified explicitly, then the starting point of the block defaults to the 
    start of the enclosing block; if omitted and no enclosing block was 
    explicitly specified, then the starting point of the block defaults to the 
    current location of the file pointer. 
    When moving the file pointer to the desired starting point, you are not 
    allowed to move it outside the bounds of the enclosing block.  Attempts to 
    do so will be rejected. 
o   The ending point of the block.  If omitted, the end of the last block 
    operand given in the starting point specification is assumed; if the 
    starting point was itself omitted, then the ending point of the block 
    defaults to the end of the current selected block. 
    When moving the file pointer to the desired ending point, you are not 
    allowed to move the file pointer outside the bounds of the enclosing 
    block.  Attempts to do so will be rejected. 
Block expressions allow you to specify these components in many different 
ways.  For example, after specifying a starting point and an ending point for 
the block being defined, you can change either or both boundaries (ADJUST 
clause).  This can be useful when you are specifying the block interactively, 
and you want to change the boundaries of the block being defined as you 
examine the data in the file. 
Also, you can specify a "repeated block."  A repeated block is a block which 
is repeated throughout a file.  It must not contain any absolute block 
operands.  For example, you can define three records of a file to be a block; 
you can also repeat that block expression, thus defining each three-record 
group in the file to be a block.  When a command includes a block expression 
which specifies a repeated block, then the command is repeated, once for each 
instance of the repeated block.  In the example just given, the command which 
included the repeated block expression would be repeated, each time operating 
on a different three-record group in the file. 
6Edit editing commands work with "blocks" of data.  A block can be an entire 
file, or any portion of a file. 
A "block expression" specifies a block in a file.  As with other types of 
expressions, a block expression consists of block operands, which are combined 
by block operators to yield a result.  The result of the evaluation of a block 
expression is itself a block operand. 
Block operands differ from operands in string expressions.  They not only have 
values associated with them, they have locations as well.  The "location" 
associated with a block operand is the location of a block within a file; the 
value of a block operand is the contents of the file at that location. 
Evaluation of block expressions also differs from evaluation of string 
expressions.  The evaluation of block operands results in not only a value and 
a location, but a signal as well.  This signal indicates the success or 
failure of the evaluation of the block operand.  Continued evaluation of the 
block expression depends on the success or failure of the evaluation of each 
block operand in the block expression. 
$CONTROL_VALUE
The editing window has two vertical "scroll margins."  These margins are the 
top and bottom subportions of the editing window: 
               ------------------------ 
               |*                     |   command window 
               |                      | 
               |----------------------| 
               |    scroll margin     | 
               |----------------------| 
               |                      |   editing window 
               |                      | 
               |----------------------| 
               |    scroll margin     | 
               ------------------------ 
6Edit keeps the cursor out of the scroll margins whenever possible.  (An 
exception is when the editing window displays the beginning or end of the 
file, so you cannot scroll any more in that direction.)  Thus, text surrounds 
the cursor at all times.  If you try to move the cursor into a scroll margin, 
6Edit scrolls the data so the cursor is no longer in the scroll margin. 
You can change the size of the scroll margin, from a minimum of zero lines to 
a maximum of half the editing window height.  To do this, assign a number to 
the predefined name "$VSCROLL_MARGIN". 
Syntax: 
Form 1, for creating a new editing window: 
                [      {PO[SITIONS]} ] 
NE[W]  WI[NDOW] [ expr {LI[NES]    } ] 
                [      {PE[RCENT]  } ] 
Form 2, for changing an existing editing window: 
                      [      {PO[SITIONS]} ] 
WI[NDOW] [window_num] [ expr {LI[NES]    } ] 
                      [      {PE[RCENT]  } ] 
Form 3, for switching to another editing window: 
{ NEXT       }            [      {PO[SITIONS]} ] 
{ PREV[IOUS] }  WI[NDOW]  [ expr {LI[NES]    } ] 
                          [      {PE[RCENT]  } ] 
Form 4, for deleting an editing window: 
DE[LETE] WI[NDOW] [window_num] 
Parameters: 
expr    is a 6Edit string expression which evaluates to a number. 
window_num    is a 6Edit string expression between 1 and the number of editing 
windows. 
Description: 
The WINDOW command can be used to create a new editing window, change or 
remove an existing editing window, or to switch to another editing window. 
o   Creating a New Editing Window 
    To create an editing window, form 1 of the WINDOW command is used: 
        NEW WINDOW expr POSITIONS    will create a new window which is "expr" 
        positions wide and the height of the editing window portion of the 
        6Edit screen.  The new window will be created at the right of the 
        rightmost editing window.  Not implemented for A03 version. 
        NEW WINDOW expr LINES    will create a new window which is "expr" 
        lines high and the width of the 6Edit screen.  The new window will be 
        created at the bottom of the bottom editing window. 
        NEW WINDOW expr PERCENT    will create a new window which is "expr" 
        percent of the size of the 6Edit screen, along the dimension of the 
        window creation mode.  The new window will be created at the bottom or 
        right of the bottom or rightmost editing window. 
    If expr is given but neither POSITIONS, LINES, nor PERCENT is given, then 
    PERCENT is assumed. 
    Examples: 
    NE WI 
    will create a new editing window in the current creation mode; if there 
    are no editing windows yet or just one, a new vertical window will be 
    created at the bottom of the current editing window.  $WI_PERCENT will 
    determine the window size. 
    NE WI; FI xxx 
    will create the new editing window, and will begin editing file "xxx" in 
    the new window. 
o   Changing or Removing an Editing Window 
    To change the size of the current editing window, form 2 of the WINDOW 
    command is used. 
    To remove the current editing window, use: 
        DELETE WINDOW 
    The window will be deleted, removing it from the screen.  The space it 
    occupied will be given to the editing window above it or to its left. 
    If expr (given as either a number of positions, a number of lines, or as a 
    percentage of the screen size) specifies the entire editing window portion 
    of the 6Edit screen (or anything larger), then 6Edit assumes you want to 
    remove all editing windows except the current one.  Thus: 
        WINDOW 100 PERCENT 
    will make the current editing window into the only one on the screen, 
    temporarily removing all others. 
o   Switching Between Editing Windows 
    There are two ways to switch to a different editing window:  using the 
    WINDOW command, or by typing an activation character. 
    In the command window, you can type form 3 of the WINDOW command: 
        { NEXT       } 
        { PREV[IOUS] }  WINDOW 
    This will move the cursor to the current file pointer location in the 
    window to the "next" or "previous" editing window.  NEXT means the window 
    to the right or below the current window; PREVIOUS means the window to the 
    left or above the current window.  This movement "wraps" at the edges of 
    the editing window portion of the 6Edit screen; for example, typing 
    "PREVIOUS WINDOW" when the cursor is in the left-most editing window will 
    move the cursor to the right-most editing window. 
    Also in the command window, you can type form 2 of the WINDOW command 
    specifying a window number but no size option: 
         WINDOW 2 
    This will move the cursor directly to the indicated editing window. 
    If 6Edit is being run on-line, the <CNTL-N> activation character can be 
    used to move the cursor to the next editing window.  "Wrapping" around the 
    screen at the edges occurs as described above. 
    Even if 6Edit is reading from the command window when <CNTL-N> is typed, 
    the cursor will be moved to the next editing window. 
Related Topics: 
Multiple Editing Windows 
EQUALS Command 
KEYIN Command 
00002
00001
00003
6Edit supports a special feature called "wordwrap."  As you type text, 6Edit 
allows you to type as far as the right margin; when you cross that margin, 
wordwrap automatically replaces the last word of the record at the beginning 
of a new record.  Thus you can enter text without ever pressing the Return 
key. 
You can enact the wordwrap mode with the $WORDWRAP predefined name.  The value 
assigned to $WORDWRAP is the right margin column number you choose.  A value 
greater than 11 implements the wordwrap mode.  To discontinue the wordwrap 
mode, set $WORDWRAP to 0 or 1; this is the default. 
Multiple editing windows are permitted.  The WINDOW commands allow you to 
create and remove editing windows.  (There will always be just one command 
window.)  At any one time, you're working with just one editing window, called 
the "current" editing window. 
Each editing window remembers its own instances of: 
    the edit block ("CURRENT"); 
    the edit block stack (for "EDIT PREVIOUS" and "EDIT NEXT"); 
    the file pointer ("HERE"); 
    the selected block ("THAT"). 
Different editing windows can be editing the same file or different files. 
You can select a block in one window, switch to a different editing window, 
and insert the data in the new window. 
The editing windows must be created either side-by-side (horizontal windows), 
or stacked one above the other (vertical windows).  The horizontal and 
vertical modes of window creation are illustrated in the following figure. 
    -----------------------------        ----------------------------- 
    | command window            |        | command window            | 
    |---------------------------|        |---------------------------| 
    |   ed.  | ed.  | editing   |        | editing window #1         | 
    |   win. | win. | window    |        |---------------------------| 
    |   #1   | #2   | #3        |        | editing window #2         | 
    |        |      |           |        |                           | 
    -----------------------------        ----------------------------- 
    Horizontal editing windows             Vertical editing windows 
The "mode" for creating new editing windows (horizontal or vertical) is 
determined when the second editing window is created.  To switch "modes", you 
must remove all but one editing window, and create a second editing window in 
the desired mode.  Only vertical mode is implemented in A03 6Edit, however. 
The minimum window size is:  for horizontal windows, ten positions; and for 
vertical windows, one line plus the border, if present.  The only practical 
limit on the number of windows which can be created is the size of the 6Edit 
screen. 
Editing windows are numbered starting at one, top-to-bottom or left-to-right. 
The predefined name $WI_BORDER controls borders between windows.  The value of 
$WI_BORDER is a single character, or no characters (the empty string); the 
initial value is "-".  This character will be used to form the border between 
windows; if $WI_BORDER is set to the empty string, then borders are not used. 
To move the cursor from the current editing window to the next one, type 
<CNTL-N> (hold down the Control key, while typing the letter N once).  The 
cursor can be in the current editing window or the command window.  If the 
current editing window is the last one, <CNTL-N> moves to the first one. 
END
