ELSIE is a cross assembler for the MLCP/MLC16 (Multi-Line Communications 
Processor).  ELSIE supports an instruction set designed for simple 
manipulation and input/output of data.  The ELSIE program for the MLCP/MLC16 
and associated data may be considered as a collection of the following items, 
some of which are optional: 
o   A set of LCTs (Line Control Tables) for each line; these tables are 
    defined partially by the MLCP/MLC16 firmware and partially by the 
    programmer.  Each line possesses 64 (for MLCPs) or 256 (for MLC16s) LCT 
    bytes. 
o   One or more CCPs (Channel Control Programs) written by the user.  These 
    CCP's must contain executable MLCP/MLC16 instructions, and may contain 
    constant data and/or look-up tables.  More than one CCP may exist within a 
    particular MLCP/MLC16. 
    For more HELP see: 
    HELP (ELSIE) TOPICS    for a complete list of topics. 
    HELP (ELSIE) MNEMONIC for a list of the mnemonics. 
    ?                      displays the next level of HELP message. 
    ??                     displays all levels of the current 
                           HELP message. 
  ************************************************************** 
  *   Copyright (c) Honeywell Bull Inc., 1988 
  ************************************************************** 
Format: 
ADDR LOC=expression,REF=expression [comments] 
Parameters: 
LOC=expression    specifies a value in the range 0 to 62 for MLCP or in the 
range 0 to 254 for MLC16.  ELSIE produces a warning diagnostic (severity 0) if 
the ADDR statement initializes any LCT byte defined as "reserved for 
firmware". 
REF=expression    specifies a value which falls within the address range of 
the TLU or CCP sections of the ELSIE program. 
Description: 
The ADDR statement is used to specify the initial value for a pair of LCT 
bytes which are to contain the address of (generally) a look-up table for use 
by the TLU instruction. 
Rules: 
1.  One or more blanks must appear before the statement. 
2.  The ADDR statement is legal only between the LCTS and ENDLCTS statements. 
3.  As many ADDR statements may be specified as are needed to initialize the 
    LCT. 
00002
00001
00003
Format: 
ASCII [TEXT=textconstruct,] EOS=label [comments] 
Parameters: 
textconstruct    specifies the ASCII character string which is to be 
represented in the look-up table.  Values may be either: 
o   A single string or 
o   A sequence of strings or expressions, enclosed in parentheses and 
    separated by commas. 
EOS=label    specifies the label to which control should be transferred when 
the ELSIE program attempts to access the byte following the end of the ASCII 
string. 
Description: 
The ASCII statement may be used to place an ASCII character string into the 
look-up table, in a fashion that permits easy access by an ELSIE program. 
Rules: 
1.  One or more blanks must appear before the statement. 
2.  ASCII may be used only within a table which was defined with both the 
    STRINGAREA and TLU options.  A description of the layout of the string 
    text, including its reference byte and exit offset byte, may be found 
    under the section entitled, "Table Generating Statements". 
3.  If the TEXT component is not present, then no offset byte will be 
    generated. 
00002
00001
00003
Format: 
[label] ASSIGN dest,source [comments] 
Parameters: 
dest    an LCT location. 
source    an LCT location or an immediate operand. 
Code Generated: 
    LD    source 
    ST    dest 
Description: 
Moves the contents of LCT location at source to LCT location destination. 
00002
00003
00001
Format: 
BIAS optionlist [comments] 
Parameters: 
optionlist    is a list of one or both of the following options, separated by 
commas: 
o   START=value    specifies the address at which the tables, ASCII strings, 
    and the CCP program are to begin.  The value specified must be in the 
    range '200'X to '0DFF'X (or 512 to 3583 decimal) for MLCP mode, and in the 
    range '0'X to '10000'X (or 0 to 65536 decimal) for MLC16 mode. 
o   END=value    specifies the upper limit of the addresses available for this 
    ELSIE program's tables, ASCII strings, and CCP instructions.  "value" must 
    be in the same range as the START value, and must not be less than the 
    START value.  ELSIE diagnoses any ELSIE program whose CCP area exceeds its 
    address limit. 
Description: 
The BIAS statement is used to specify the beginning and ending locations in 
the CCP area within which this ELSIE program's CCP area is to reside. 
Rules: 
1.  One or more blanks must appear before the statement. 
2.  If the BIAS statement is used, it must appear before the first TABLE, 
    ASCII, or CCP statement.  If the BIAS statement is not used, ELSIE assumes 
    START=512 to END=3583. 
00002
00001
00003
BRANCH_MLCP_MLC16
Format: 
[label] mnemonic expression 
Parameters: 
address    specifies the address to which program control should transfer.  It 
may be an Internal or External expression. 
mnemonic    specifies one of the mnemonics described in the following table. 
Enter ?? for the complete table. 
  Mnemonic    Instruction 
  BCF 
              Branch on carry false 
  BCT 
              Branch on carry true 
  BMI 
              Branch on sign negative 
  BPL 
              Branch on sign positive 
  JSR 
              Long relative jump to subroutine 
Description: 
The branch instruction causes a transfer of program control. 
Rules: 
1.  A diagnostic is produced if the target address lies outside of the 
    displacement supported by the branch instruction requested. 
00002
00003
00004
00005
00007
00006
00001
00008
Format: 
[label]  mnemonic  expression 
Parameters: 
expressions    specifies the address to which program control should transfer. 
It may be an internal or external expression.  mnemonic    specifies one of 
the following mnemonics: 
B BARF BART BEF BET BLBF BLBT BLCF BLCT BS BVBF BVBT BZF BZT JUMP 
To obtain HELP messages for the mnemonics enter HELP BRANCH mnemonic.  For 
example, HELP BRANCH BART Descriptions are in a tabular format with two 
columns like so: 
  Mnemonic     Instruction 
  B 
               Unconditional Branch 
  BARF 
               Branch if Adapter Ready False 
               Synonymous Mnemonic: BANR 
  BART 
               Branch if Adapter Ready True 
               Synonymous Mnemonic: BAR 
  BEF 
               Branch if Equal False (.. Not Equal) 
               Synonymous Mnemonic: BNE 
  BET 
               Branch if Equal True 
               Synonymous Mnemonic: BE 
  BLBF 
               Branch if Last Block False 
               Synonymous Mnemonic: BNLB 
  BLBT 
               Branch if Last Block True 
               Synonymous Mnemonic: BLB 
  BLCF 
               Branch if Last Character False 
               Synonymous Mnemonic: BNLC 
  BLCT 
               Branch if Last Character True 
               Synonymous Mnemonic: BLC 
  BS 
               Branch to Subroutine (.. And Link) 
               Synonymous Mnemonic: BAL 
  BVBF 
               Branch if Valid Block False 
               Synonymous Mnemonic: BNVB 
  BVBT 
               Branch if Valid Block True 
               Synonymous Mnemonic: BVB 
  BZF 
               Branch if Zero False 
               Synonymous Mnemonic: BNZ 
  BZT 
               Branch if Zero True 
               Synonymous Mnemonic: BZ 
  JUMP 
               Jump 
               Synonymous Mnemonic: J 
Description: 
The branch instruction causes a transfer of program control. 
Rules: 
1.  ELSIE produces a diagnostic if the target address lies outside of the 
    displacement supported by the branch instruction requested. 
00002
00011
00003
00004
00003
00004
00006
00005
00006
00008
00007
00008
00010
00009
00010
00005
00007
00009
00012
00014
00011
00013
00012
00013
00015
00014
00015
00017
00016
00016
00001
00018
Format: 
[label] BRESET lctlocation,bitvalue,targetloc 
Parameters: 
lctlocation    specifies an LCT symbol. 
bitvalue    specifies an LCT symbol or an immediate value in the form =value. 
targetloc     must be a label defined within the CCP section. 
Code Generated: 
    LD       lctlocation 
    AND      bitvalue 
    BZ       targetloc 
Description: 
Causes a branch to targetloc if the bit values specified by bit value at 
lctlocation are 0. 
00002
00003
00001
Format: 
[label] BSET lctlocation,bitvalue,targetloc 
Parameters: 
lctlocation    specifies an LCT symbol. 
bitvalue    specifies an LCT symbol or an immediate value in the form =value. 
targetloc     must be a label defined within the CCP section. 
Code Generated: 
    LD       lctlocation 
    AND      bitvalue 
    BNZ      targetloc 
Description: 
Causes a branch to targetloc if the bit values specified by bit value at 
lctlocation are 1. 
00002
00003
00001
Format: 
label CCP [comments] 
Note: 
1.  label is required.  If the location counter contains an odd value, a byte 
    containing '00'X shall be generated and the instruction counter 
    incremented.  The specified label is defined as a symbol having the value 
    of the (possibly incremented) location counter. 
Description: 
The CCP statement is used to define the beginning of the Channel Control 
Program.  Each ELSIE program must have only one CCP statement. 
00002
00001
1.  A comment is a character string formatted as follows: 
    /* comment string */ 
    unless the /* */ is delimited by apostrophes ('), in which case it is a 
    character string. 
2.  A comment record must contain an asterisk (*) in the first character 
    position or a comment introducer (/*) in the first two character 
    positions. 
3.  A blank record cannot contain any non-blank characters. 
4.  Comment and blank records may appear anywhere in an ELSIE source program 
    (even between the lines of a continued statement).  Comments appear on the 
    program listing but otherwise have no meaning to ELSIE. 
5.  Comments can follow the end of a statement. 
%IF provides conditional inclusion, or exclusion of a number of source 
records. 
Format: 
%IF [ %MLCP | %MLC16 ] 
      : 
      :   any valid Elsie statements 
      :   except END 
[ %ELSE ] 
[     :                              ] 
[     :   any valid Elsie statements ] 
[     :   except END                 ] 
%ENDIF 
Parameters: 
%MLCP    if the MLCP option is specified on the ELSIE invocation line, or if 
no option is specified (MLCP is the default option), then the %IF condition is 
evaluated as true; otherwise, the %IF condition is evaluated as false. 
%MLC16    if the MLC16 option is specified on the ELSIE invocation line, then 
the %IF condition is evaluated as true; otherwise, it is evaluated as false. 
Rules: 
1.  When a %IF is encountered, the condition is evaluated. 
2.  If the condition evaluates to true then all instructions between the %IF 
    and %ELSE/%ENDIF will be assembled.  If a %ELSE exists, the instructions 
    following it will be skipped until the %ENDIF is reached. 
3.  If the condition evaluates to false, then all instructions between the %IF 
    and %ELSE/%ENDIF will be skipped.  If a %ELSE exists, the instructions 
    following it will be assembled until the %ENDIF is reached. 
4.  A %ENDIF causes normal assembly to be resumed. 
5.  %IF...%ENDIF blocks can not be nested.  Each %IF must correspond to one 
    and only one %ENDIF.  Each %ELSE must correspond to one and only one %IF. 
00001
00002
00003
    An ELSIE constant has one of three formats: 
1.  decimal constants -- sequences of decimal digits. 
2.  character string constants -- strings of arbitrary ASCII characters 
    delimited by single quote (') characters.  If the string is to contain a 
    single quote character, two adjacent single quotes should be used, for 
    example: 
        'He said, "I didn''t do it."'. 
    Strings of more than one character may be used only with the TITLE and 
    ASCII statements.  Strings of one character may be used in any context in 
    which a constant is legal. 
3.  bit string constants -- quoted strings followed by a single character 
    indicating the base (radix) of the bit string representation: 
        B -- binary (base 2) 
        O -- octal (base 8) 
        X -- hexadecimal (base 16) 
    The legal characters in the quoted string are 
        0, 1             for binary 
        0 - 7            for octal 
        0 - 9, A - F     for hexadecimal. 
    Examples: 
        '1234'O 
        '29C'X 
        '001010011100'B 
    Bit strings which appear in the second ("%EQU") form of the EQU statement 
    must specify exactly 8 or exactly 16 bits (and thus must be in either hex 
    or binary radix); bit strings appearing in other contexts may specify any 
    number of bits in the range 1 to 36. 
Format: 
[label] mnemonic [comments] 
Parameters: 
mnemonic    specifies one of the following mnemonics: 
LD    ST 
To obtain HELP messages for the mnemonics enter HELP DO1 mnemonic.  For 
example, HELP DO1 LD.  Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  LD 
               Load R register 
  ST 
               Store R register 
Description: 
The DO1 format is used to transfer data to or from the next byte in the 
current Communication Data Block (CDB) in the FEP's memory. 
00004
00002
00001
00003
Format: 
[label] mnemonic lctvalue [comments] 
Parameters: 
mnemonic    specifies one of the following mnemonics: 
AND   C     LD    OR ST    TLU   XOR 
lctvalue    specifies an assembler constant or expression whose value lies in 
the range 0 to 63. 
To obtain HELP messages for the mnemonics enter HELP DO2 mnemonic.  For 
example, HELP DO2 TLU.  Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  AND 
               AND R register 
  C 
               Compare R register 
  LD 
               Load R register 
  OR 
               OR R register 
  ST 
               Store R register 
  TLU 
               Table look-up 
  XOR 
               Exclusive-OR R register 
Description: 
The DO2 format is used to move data to or from a specified LCT byte for the 
currently active line. 
00002
00003
00009
00004
00005
00001
00006
00007
00008
Format: 
[label] mnemonic =immediate_constant [comments] 
Parameters: 
immediate_constant     must be an assembler constant or expression whose value 
lies in the range -128 to 255.  mnemonic    specifies one of the following 
mnemonics: 
AND   C     LD    OR XOR 
To obtain HELP messages for the mnemonics enter HELP DOUBLE_OPERAND mnemonic. 
For example, HELP DOUBLE_OPERAND TLU.  Descriptions are in a tabular format 
with two columns like so: 
  Mnemonic     Instruction 
  AND 
               AND R register 
  C 
               Compare R register 
  LD 
               Load R register 
  OR 
               OR R register 
  XOR 
               Exclusive-OR R register 
Description: 
The DO3 Instruction format is used to move a constant value, contained within 
the instruction itself, to the R register, or to use the immediate constant as 
a boolean value which is compared with or OR'ed, AND'ed, or XOR'ed against the 
value currently in R. 
00002
00003
00007
00004
00005
00001
00006
    Double operand instructions are used to manipulate the MLCP's 8-bit R 
    register.  Data may be moved from the R register to or from certain 
    storage areas, or may be compared with, or OR'ed, AND'ed, or XOR'ed with 
    data from storage or from within the instruction itself. 
    The three different formats for Double Operand Instructions are accessed 
    by typing HELP D01, HELP D02 or HELP D03.  Not all double operand 
    instructions may be used in all three formats.  ELSIE diagnoses any 
    attempt to generate a semantically meaningless instruction, and produces a 
    warning message (severity 0) if a ST instruction is generated which will 
    cause the modification of any LCT byte which is defined as "reserved for 
    firmware use". 
Format: 
EJECT [INVIS] [comments] 
Parameters: 
INVIS    specifies that the EJECT statement will not appear on the listing. 
Description: 
The EJECT command may be used to force the assembly listing to proceed on a 
new page.  The EJECT command will be the first command printed on the new page 
(if INVIS is not specified), and will not cause the page title (if any) to be 
modified. 
Rules: 
1.  One or more blanks must appear before the statement. 
00002
00001
00003
    An ELSIE program consists of the following segments: 
1.  The LCT section, which is optional.  This section begins with the LCTS 
    statement and terminates with the ENDLCTS statement.  Within the LCT 
    section, the only data-generating statements permitted are the LCT and 
    ADDR statements. 
2.  The TLU section, which is optional.  This section consists of one or more 
    tables.  Each table consists of one or more TABLE statements, and a 
    mixture of TRANSLATE, TRANSFER, and ASCII statements, and is terminated by 
    an ENDTABLE statement. 
3.  The CCP section.  This section begins with the CCP statement and ends with 
    the END statement which terminates the ELSIE source unit.  The CCP section 
    contains executable instructions only. 
Format: 
END [comments] 
Description: 
The END statement terminates both the CCP section and the ELSIE program.  The 
END statement is required. 
Rules: 
1.  One or more blanks must appear before the statement. 
00001
00002
Format: 
ENDLCTS [comments] 
Description: 
The ENDLCTS statement is used to terminate the definition of the Line Control 
Table area.  This statement is required if an LCT section has been specified. 
At the ENDLCTS statement, the LCT is printed out. 
Rules: 
One or more blanks must appear before the statement. 
Example: 
               DBK     LCTS 
                       LCT     LOC=2,VALUE='C0'X 
                       ADDR    LOC=6,REF=RCV 
                       LCT     LOC=8,VALUE='80'X 
                       LCT     LOC=15,VALUE='80'X 
                       ADDR    LOC=38,REF=TRN 
                       LCT     LOC=47,VALUE='40'X 
                       LCT     LOC=60,VALUE='18'X 
    0000C000           ENDLCTS 
    00000206 
    80000000 
    00000080 
    00000000 
    00000000 
    00000000 
    00000000 
    00000000 
    0000021F 
    00000000 
    00000040 
    00000000 
    00000000 
    00000000 
    18000000 
00001
00003
00002
Format: 
label ENDTABLE [comments] 
Note: 
1.  label must match the label of the table currently under construction. 
Description: 
The ENDTABLE instruction terminates a look-up table.  The table generated is 
listed after the ENDTABLE statement. 
Example: 
    18.000      16 200             TRNTAB  TABLE   NODEFAULT,SIZE=5,TLU=MYTLU 
    19.000      17                         TRANSFER   IN=0,TARGET=BR1 
    20.000      18                         TRANSFER   IN=1,TARGET=BR2 
    21.000      19                         TRANSFER   IN=2,TARGET=BR3 
    22.000      20                         TRANSFER   IN=3,TARGET=LWR 
    23.000      21                         TRANSFER   IN=4,TARGET=LASTBR 
    24.000      22 200  80818283   TRNTAB  ENDTABLE 
                        84 
00002
00003
00001
Format: 
label EQU expression [comments] 
   or 
%EQU label = expression ; [comments] 
Parameters: 
label    this field is required. 
expression    is any valid expression. 
Description: 
The EQU command may be used to define a symbol whose value is that of an 
arbitrary ELSIE constant or expression. 
Rules: 
1.  The specified expression will be evaluated, and its value will be assigned 
    to the specified symbol (which must not already have been defined).  The 
    expression is evaluated during Pass 1 of the assembly, and thus may 
    contain only constants or symbols which have already been defined within 
    the current assembly. 
2.  The second ("%EQU") form of the EQU command is provided to permit sharing 
    of pre-processor-compatible data equates with PL-6 programs written for 
    the Front-end.  To ensure compatibility, any bit-string constants 
    appearing in an %EQU statement must define a value of either exactly 8 or 
    exactly 16 significant bits; use of bit strings of any other length will 
    result in a severity 2 diagnostic message "Constant not compatible with 
    PL-6". 
00002
00001
00003
    ELSIE expressions look very much like expressions in other languages. 
    There are dyadic and monadic operators.  Evaluation is from left to right 
    except for the priority of the various operators.  Parentheses may be used 
    to control the order of evaluation. 
    Expressions may include constants or symbols, or both, as operands. 
    Expressions are evaluated to 36 bits of precision.  However, the statement 
    which makes use of an expression will generally use only the rightmost 3 
    or 8 bits of the expression's value. 
    Legal expression operators are in a tabular format with three columns like 
    so: 
  Priority     Operator        Description 
7            ~ arg1          ones complement arg1 
7            + arg1          returns arg1 
7            - arg1          negate arg1 
6            arg1 ** arg2    if arg2 > 0, then shift arg1 left arg2 bits; 
                             otherwise shift arg1 right -arg2 bits.  arg2 
                             must be in the range of -32 to +32. 
5            arg1  * arg2    arg1 times arg2 
5            arg1  / arg2    arg1 divided by arg2 
5            arg1 // arg2    covered quotient -- (arg1 + arg2 - 1) / arg2 
4            arg1  + arg2    arg1 plus arg2 
4            arg1  - arg2    arg1 minus arg2 
3 *          arg1  < arg2    arg 1 is less than arg2 
3 *          arg1 <= arg2    arg 1 is less than or equal to arg2 
3 *          arg1  = arg2    arg 1 is equal to arg2 
3 *          arg1 ~= arg2    arg1 is not equal to arg2 
3 *          arg1 >= arg2    arg1 is greater than or equal to arg2 
3 *          arg1  > arg2    arg1 is greater than arg2 
2            arg1  & arg2    arg1 boolean and arg2 
1            arg1  | arg2    arg1 boolean inclusive or arg2 
1            arg1  \ arg2    arg1 boolean exclusive or arg2 
*   Relational operators.  Return 1 if the relationship is true and return 0 
    if the relationship is false. 
Format: 
[label] mnemonic LCT value 
Parameters: 
LCT value    specifies an assembler constant or expression whose value lies in 
the range 0 to 255. 
mnemonic    specifies one of the mnemonics described in the following table. 
Enter ?? for the complete table. 
  MNEMONIC    INSTRUCTION 
  DECX 
              Decrement extended 
  INCX 
              Increment extended 
  LDX 
              Load extended to R 
  STX 
              Store extended to R 
Description: 
These instructions are used to move data to or from a specified LCT byte for 
the currently active line.  The instruction specifies an LCT in the channel's 
basic LCT area; the 8 bit contents of this LCT is then concatenated with the 8 
low order bits from the contents of the B register to obtain the 16 bit 
address. 
00002
00006
00003
00004
00001
00005
Format: 
[label] mnemonic flap_reg# 
Parameters: 
mnemonic    is FIN for input flap register and FOUT for output flap register. 
flap_reg#    specifies the number of the flap register. 
Description: 
These instructions operate on the FLAP (Flexible Line Adapter Packages) 
control registers.  The register number specifies a value in the range 0 to 
15. 
00002
00001
GENERIC_MLCP
Format: 
[label] mnemonic 
Parameters: 
mnemonic    specifes one of the mnemonics described in the following table. 
Enter ?? for the complete table. 
  Mnemonic    Instruction 
  ACTL 
              Output Adapter Control from R 
  ADDRN 
              Add to R 
  ANDRN 
              AND to R 
  AST 
              Input Adapter Status to R 
  CADRN 
              Add with carry to R 
  CANB 
              Cancel Block 
  CANC 
              Cancel character 
  CLB 
              Clear B 
  CLN 
              Clear LCT 
  CLR 
              Clear R 
  CRN 
              Arithmetic compare R 
  DECB 
              Decrement B 
  DECN 
              Decrement LCT 
  GIVE 
              Give CCP to CPU 
  INC 
              Increment R 
  INCB 
              Increment B 
  INCN 
              Increment LCT 
  LDBR 
              Load B to R 
  LDRB 
              Load R to B 
  LDRN 
              Load R 
  MC 
              Master Clear 
  NEGR 
              Negate R 
  ORRN 
              OR to R 
  POPB 
              Pop B from stack 
  POPR 
              Pop R from stack 
  PULLF 
              Pull R from FIFO 
  PUSHB 
              Push B to stack 
  PUSHF 
              Push R to FIFO 
  PUSHR 
              Push R to stack 
  RETJSR 
              Return from stacked subroutine 
  RHB 
              Return held blocks to next 
  SCF 
              Set carry false 
  SCLB 
              Shift closed left B 
  SCLR 
              Shift closed left R 
  SCRB 
              Shift closed right B 
  SCRR 
              Shift closed right R 
  SCT 
              Set carry true 
  SOLB 
              Shift open left B 
  SOLR 
              Shift open left R 
  SORB 
              Shift open right B 
  SR 
              Shift open right R 
  STRN 
              Store R 
  SUBRN 
              Subtract from R 
  TSTFE 
              Test FIFO empty 
  TSTFF 
              Test FIFO full 
  XORN 
              Exclusive OR LCT with R 
Description: 
Generic Instructions have no operands and are used for the purpose stated. 
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
00048
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
00001
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
Format: 
[label] mnemonic   [comments] 
Parameters: 
mnemonic    specifies one of the following mnemonics: 
CCH   DEC   GNB   INTR INZ   NOP   RET   SFS SR    WAIT 
To obtain HELP messages for the mnemonics enter HELP GENERIC mnemonic.  For 
example, HELP GENERIC CCH.  Descriptions are in a tabular format with two 
columns like so: 
  Mnemonic     Instruction 
  CCH 
               Calculate Block Check 
               Synonymous Mnemonic: CRC 
  DEC 
               Decrement R register 
  GNB GNCCB 
               Get Next Block (.. Next CCB) 
               Synonymous Mnemonic: GNCCB 
  INTR 
               Interrupt CPU 
               Synonymous Mnemonic: INT 
  INZ 
               Soft-initialize all channels 
               Synonymous Mnemonic: INIT 
  NOP 
               No operation 
  RET 
               Return from subroutine 
               Synonymous Mnemonic: RETURN 
  SFS 
               Search For Synchronization 
               Synonymous Mnemonic: SYNC 
  SR 
               Shift R register right 
               Synonymous Mnemonic: SHIFT 
  WAIT 
               Wait 
Description: 
Generic instructions are operand-less instructions used for purposes not 
covered by the instructions listed above. 
00002
00002
00003
00012
00004
00006
00005
00005
00006
00007
00001
00008
00008
00009
00010
00010
00009
00011
The ELSIE and CALF HELP facilities provide on-line documentation of ELSIE and 
CALF.  HELP issues messages in response to the user's request for information. 
The ELSIE and CALF HELP facilities contain the descriptions, format, 
parameters and rules of the various instruction formats.  In some cases, 
examples are also given.  Information on the processor invocation is also 
available. 
When requesting information, the first word of an instruction format is 
usually sufficient to identify it; the second word is also necessary in cases 
where more than one topic begins with the same word.  When in doubt, use the 
most complete form.  Always separate words with an underscore (_) when 
requesting topics with more than one word. 
To obtain more HELP information: 
HELP (CALF|ELSIE) TOPICS    provides a list of available topics. 
?    means give the next level of HELP message 
??    means give all levels of the current message 
HELP (CALF|ELSIE) MNEMONICS mnemonic    provides the instruction 
and the HELP that will provide the Instruction Format. 
HELP (CALF|ELSIE) instruction_format    provides the syntax 
of the specified instruction format. 
HELP (CALF|ELSIE) instruction_format description    provides 
a description of the specified instruction format. 
A 
  ADDR Statement - 
      HELP ADDR 
  AND -   
    DO2 Instruction - 
      HELP DO2 AND 
    DO3 Instruction - 
      HELP DO3 AND 
  AND - 
      HELP DO2 AND 
      HELP DO3 AND 
  ASCII Statement - 
      HELP ASCII 
  ASSIGN Statement - 
      HELP ASSIGN 
B 
  B -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16  B 
  B - 
      HELP BRANCH_MLCP_MLC16  B 
  BAL -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BS 
  BAL - 
      HELP BRANCH_MLCP_MLC16 BS 
  BANR -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BARF 
  BANR - 
      HELP BRANCH_MLCP_MLC16 BARF 
  BAR -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BART 
  BAR - 
      HELP BRANCH_MLCP_MLC16 BART 
  BARF -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BARF 
  BARF - 
      HELP BRANCH_MLCP_MLC16 BARF 
  BART -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BART 
  BART - 
      HELP BRANCH_MLCP_MLC16 BART 
  BE -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BET 
  BE - 
      HELP BRANCH_MLCP_MLC16 BET 
  BEF -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BEF 
  BEF - 
      HELP BRANCH_MLCP_MLC16 BEF 
  BET -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BET 
  BET - 
      HELP BRANCH_MLCP_MLC16 BET 
  BIAS Statement - 
      HELP BIAS 
  BLB -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BLBT 
  BLB - 
      HELP BRANCH_MLCP_MLC16 BLBT 
  BLBF -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BLBF 
  BLBF - 
      HELP BRANCH_MLCP_MLC16 BLBF 
  BLBT -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BLBT 
  BLBT - 
      HELP BRANCH_MLCP_MLC16 BLBT 
  BLC -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BLCT 
  BLC - 
      HELP BRANCH_MLCP_MLC16 BLCT 
  BLCF -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BLCF 
  BLCF - 
      HELP BRANCH_MLCP_MLC16 BLCF 
  BLCT -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BLCT 
  BLCT - 
      HELP BRANCH_MLCP_MLC16 BLCT 
  BNE -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BEF 
  BNE - 
      HELP BRANCH_MLCP_MLC16 BEF 
  BNLB -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BLBF 
  BNLB - 
      HELP BRANCH_MLCP_MLC16 BLBF 
  BNLC -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BLCF 
  BNLC - 
      HELP BRANCH_MLCP_MLC16 BLCF 
  BNVB -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BVBF 
  BNVB - 
      HELP BRANCH_MLCP_MLC16 BVBF 
  BNZ -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BZF 
  BNZ - 
      HELP BRANCH_MLCP_MLC16 BZF 
  Branch Instructions - 
      HELP BRANCH_MLCP_MLC16 
      HELP BRANCH_MLC16 
  BRESET Statement - 
      HELP BRESET 
  BS -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BS 
  BS - 
      HELP BRANCH_MLCP_MLC16 BS 
  BSET Statement - 
      HELP BSET 
  BVB -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BVBF 
      HELP BRANCH_MLCP_MLC16 BVBT 
  BVB - 
      HELP BRANCH_MLCP_MLC16 BVBT 
  BVBF - 
      HELP BRANCH_MLCP_MLC16 BVBF 
  BVBT -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BVBT 
  BVBT - 
      HELP BRANCH_MLCP_MLC16 BVBT 
  BZ -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BZT 
  BZ - 
      HELP BRANCH_MLCP_MLC16 BZT 
  BZF -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BZF 
  BZF - 
      HELP BRANCH_MLCP_MLC16 BZF 
  BZT -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 BZT 
  BZT - 
      HELP BRANCH_MLCP_MLC16 BZT 
C 
  C -   
    DO2 Instruction - 
      HELP DO2 C 
    DO3 Instruction - 
      HELP DO3 C 
  C - 
      HELP DO2 C 
      HELP DO3 C 
  CCH -   
    Generic - 
      HELP GENERIC_MLCP CCH 
  CCH - 
      HELP GENERIC_MLCP CCH 
  CCP Statement - 
      HELP CCP 
  Comment and Blank Records - 
      HELP COMMENT_BLANK_RECORDS 
  Conditional Assembly - 
      HELP CONDITIONAL_ASSEMBLY 
  Constants - 
      HELP CONSTANTS 
  CRC -   
    Generic Instruction - 
      HELP GENERIC_MLCP CCH 
  CRC - 
      HELP GENERIC_MLCP CCH 
D 
  DEC -   
    Generic - 
      HELP GENERIC_MLCP DEC 
  DEC - 
      HELP GENERIC_MLCP DEC 
  DO1 Double Operand Instruction - 
      HELP DO1 
  DO2 Double Operand Instruction - 
      HELP DO2 
  DO3 Double Operand Instruction - 
      HELP DO3 
  Double Operand Instructions - 
      HELP DOUBLE_OPERAND 
E 
  EJECT Command - 
      HELP EJECT 
  ELSIE and CALF HELP Facilities - 
      HELP HELP 
  ELSIE Program Definition - 
      HELP ELSIE_PROGRAM 
  END Statement - 
      HELP END 
  ENDLCTS Statement - 
      HELP ENDLCTS 
  ENDTABLE Statement - 
      HELP ENDTABLE 
  EQU Command - 
      HELP EQU 
  Expressions - 
      HELP EXPRESSIONS 
  Extended LCT Instructions - 
      HELP EXTENDED_LCT_MLC16 
F 
  FLAP Register Instructions - 
      HELP FLAP_REGISTER_MLC16 
G 
  Generic Instructions - 
      HELP GENERIC_MLCP 
      HELP GENERIC_MLC16 
  GNB -   
    Generic - 
      HELP GENERIC_MLCP GNB_GNCCB 
  GNB - 
      HELP GENERIC_MLCP GNB_GNCCB 
  GNCCB -   
    Generic Instruction - 
      HELP GENERIC_MLCP GNB_GNCCB 
  GNCCB - 
      HELP GENERIC_MLCP GNB_GNCCB 
I 
  Immediate Operand Instructions - 
      HELP IMMEDIDATE_OPERAND_MLC16 
  IN -   
    Input/Output Instruction - 
      HELP INPUT_OUTPUT IN 
  IN - 
      HELP INPUT_OUTPUT IN 
  INCLUDE Statement - 
      HELP INCLUDE 
  INIT -   
    Generic Instruction - 
      HELP GENERIC_MLCP INZ 
  INIT - 
      HELP GENERIC_MLCP INZ 
  Initialize LCT Pointer Instruction - 
      HELP INITIALIZE_LCT_POINTER_MLC16 
  Input/Output Instructions - 
      HELP INPUT_OUTPUT 
  INT -   
    Generic Instruction - 
      HELP GENERIC_MLCP INTR 
  INT - 
      HELP GENERIC_MLCP INTR 
  INTR -   
    Generic - 
      HELP GENERIC_MLCP INTR 
  INTR - 
      HELP GENERIC_MLCP INTR 
  Introduction - 
      HELP INTRODUCTION 
  Invocation and Options - 
      HELP INVOCATION 
  INZ -   
    Generic - 
      HELP GENERIC_MLCP INZ 
  INZ - 
      HELP GENERIC_MLCP INZ 
J 
  J -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 JUMP 
  J - 
      HELP BRANCH_MLCP_MLC16 JUMP 
  JUMP -   
    Branch Instruction - 
      HELP BRANCH_MLCP_MLC16 JUMP 
  JUMP - 
      HELP BRANCH_MLCP_MLC16 JUMP 
L 
  LABEL Statement - 
      HELP LABEL 
  LCT and Immediate Operand Instructions - 
      HELP LCT_IMMEDIATE_MLC16 
  LCT Instructions - 
      HELP LCT_MLC16 
  LCT Statement - 
      HELP LCT 
  LCTS Statement - 
      HELP LCTS 
  LD -   
    DO1 Instruction - 
      HELP DO1 LD 
    DO2 Instruction - 
      HELP DO2 LD 
    DO3 Instruction - 
      HELP DO3 LD 
  LD - 
      HELP DO1 LD 
      HELP DO2 LD 
      HELP DO3 LD 
  LDLR -   
    Input/Output Instruction - 
      HELP INPUT_OUTPUT IN 
  LDLR - 
      HELP INPUT_OUTPUT IN 
  LIST Statement - 
      HELP LIST 
  LISTINC Statement - 
      HELP LISTINC 
  LS option - 
      HELP INVOCATION LS 
  LU option - 
      HELP INVOCATION LU 
M 
  MNEMONIC Codes - 
      HELP MNEMONICS 
N 
  NLS option - 
      HELP INVOCATION NLS 
  NOP -   
    Generic - 
      HELP GENERIC_MLCP NOP 
  NOP - 
      HELP GENERIC_MLCP NOP 
  NOU option - 
      HELP INVOCATION NOU 
  NSO option - 
      HELP INVOCATION NSO 
  NUI option - 
      HELP INVOCATION NUI 
O 
  OPTUI option - 
      HELP INVOCATION OPTUI 
  OR -   
    DO2 Instruction - 
      HELP DO2 OR 
    DO3 Instruction - 
      HELP DO3 OR 
  OR - 
      HELP DO2 OR 
      HELP DO3 OR 
  OU - 
      HELP INVOCATION OU 
  OUNAME Statement - 
      HELP OUNAME 
  OUT -   
    Input/Output Instruction - 
      HELP INPUT_OUTPUT OUT 
  OUT - 
      HELP INPUT_OUTPUT OUT 
R 
  RECV -   
    Send/Receive Instruction - 
      HELP SEND_RECEIVE RECV 
  RECV - 
      HELP SEND_RECEIVE RECV 
  RESET Statement - 
      HELP RESET 
  RET -   
    Generic - 
      HELP GENERIC_MLCP RET 
  RET - 
      HELP GENERIC_MLCP RET 
  Return -   
    Generic Instruction - 
      HELP GENERIC_MLCP RET 
  Return - 
      HELP GENERIC_MLCP RET 
S 
  SEND -   
    Send/Receive Instruction - 
      HELP SEND_RECEIVE SEND 
  SEND - 
      HELP SEND_RECEIVE SEND 
  Send/Receive Instructions - 
      HELP SEND_RECEIVE 
  SET Statement - 
      HELP SET 
  SETADDR Statement - 
      HELP SETADDR 
  SFS -   
    Generic - 
      HELP GENERIC_MLCP SFS 
  SFS - 
      HELP GENERIC_MLCP SFS 
  SHIFT -   
    Generic Instruction - 
      HELP GENERIC_MLCP SR 
  SHIFT - 
      HELP GENERIC_MLCP SR 
  SO option - 
      HELP INVOCATION SO 
  SR -   
    Generic - 
      HELP GENERIC_MLCP SR 
  SR - 
      HELP GENERIC_MLCP SR 
  SRCH (list) option - 
      HELP INVOCATION SRCH 
  ST -   
    DO1 Instruction - 
      HELP DO1 ST 
    DO2 Instruction - 
      HELP DO2 ST 
  ST - 
      HELP DO1 ST 
      HELP DO2 ST 
  Statement Format - 
      HELP STATEMENT 
  STLR -   
    Input/Output Instruction - 
      HELP INPUT_OUTPUT OUT 
  STLR - 
      HELP INPUT_OUTPUT OUT 
  Symbols - 
      HELP SYMBOLS 
  SYMDEF Statement - 
      HELP SYMDEF 
  SYNC -   
    Generic Instruction - 
      HELP GENERIC_MLCP SFS 
  SYNC - 
      HELP GENERIC_MLCP SFS 
T 
  TABLE Statement - 
      HELP TABLE 
  TARGET Statement - 
      HELP TARGET 
  TITLE Statement - 
      HELP TITLE 
  TLU -   
    DO2 Instruction - 
      HELP DO2 TLU 
  TLU - 
      HELP DO2 TLU 
  TRANSFER Statement - 
      HELP TRANSFER 
  TRANSLATE Statement - 
      HELP TRANSLATE 
U 
  UI option - 
      HELP INVOCATION UI 
W 
  WAIT -   
    Generic - 
      HELP GENERIC_MLCP WAIT 
  WAIT - 
      HELP GENERIC_MLCP WAIT 
X 
  XOR -   
    DO2 Instruction - 
      HELP DO2 XOR 
    DO3 Instruction - 
      HELP DO3 XOR 
  XOR - 
      HELP DO2 XOR 
      HELP DO3 XOR 
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
HELP_INDEX
Format: 
[label] mnemonic =immediate_constant 
Parameters: 
mnemonic    specifes one of the mnemonics described in the following table. 
immediate_constant    must be an assembler constant or expression whose value 
lies in the range -128 to 255.  Enter ?? for the complete table. 
  Instruction   Mnemonic 
  ADIB 
                Add immediate to B 
  ADIR 
                Add immediate to R 
  ANIB 
                And immediate with B 
  CADIB 
                Add with carry immediate to B 
  CADIR 
                Add with carry immediate to R 
  CBI 
                Arithmetic compare B with immediate. 
  DADDI 
                Decimal add immediate to R 
  LBB 
                Bit test B with immediate 
  LBFN 
                Test and clear LCT 
  LBN 
                Bit test LCT 
  LBR 
                Bit test R with immediate 
  LBTN 
                Test and set LCT 
  LDIB 
                Load immediate to B 
  ORIB 
                OR immediate with B 
  SBIB 
                Subtract immediate from B 
  SBIR 
                Subtract immediate from R 
  XRIB 
                Exclusive-OR immediate with B 
Description: 
The Immediate operand instructions perform the operation using the constant 
specified within the instruction itself. 
00002
00003
00004
00005
00006
00007
00008
00019
00009
00010
00011
00012
00013
00014
00015
00001
00016
00017
00018
Format: 
INCLUDE filename[,LIST] [comments] 
Parameters: 
filename    specifies the name of the file to be read. The file will be 
located according to the SRCH options specified by the user on the ELSIE 
invocation command line.  If the LIST option is specified, the lines read from 
the specified file will be listed.  If the LIST option is not specified, the 
setting of the LISTINC command will control whether the lines are listed. 
Description: 
The INCLUDE statement directs ELSIE to include source text from a specified 
file. 
Rules: 
1.  One or more blanks must appear before the statement. 
00002
00001
00003
Format: 
[label] mnemonic lctvalue,labelname 
Parameters: 
mnemonic    is ILP. 
lctvalue    specifies an assembler constant or expression whose value lies in 
the range 0 to 255. 
labelname    any valid label 
Description: 
This instruction initializes the specified LCT with the label value. 
00002
00001
Format: 
[label] mnemonic IO_constant 
Parameters: 
IO_constant    specifies an expression whose value lies in the range 0 to 7. 
mnemonic    specifies one of the following mnemonics: 
IN   OUT 
To obtain HELP messages for the mnemonics enter HELP I_O mnemonic.  For 
example, HELP INPUT_OUTPUT IN.  Descriptions are in a tabular format with two 
columns like so: 
  Mnemonic     Instruction 
  IN 
               Load line register IO_constant into R 
               Synonymous Mnemonic: LDLR 
  OUT 
               Store R into line register IO_constant 
               Synonymous Mnemonic: STLR 
Description: 
Input/output instructions move line control data between the R register and 
the external line registers. 
00004
00002
00002
00003
00001
00003

    ELSIE is invoked via the CP-6 standard processor invocation syntax: 
    !ELSIE [sifid][,uifid] [{ON|OVER|INTO} [oufid][,lsfid]] [(options)] 
    The default options are: LS, MLCP, NLU, NSO, NUI, OU and RELOC.  Available 
    options are:  LS   LU   NLS  NOU  NSO  NUI  OPTUI OU SO   SRCH UI 
    These can be accessed by typing HELP INVOCATION option. For example HELP 
    INVOCATION SRCH.  Descriptions are in a tabular format with two columns 
    like so: 
  Option     Explanation 
  LS 
             List source program.  The default is LS. 
  LU 
             List the update file before listing the source.  The default is 
             NLU. 
  MLCP 
             Error checking is provided to ensure instructions are valid MLCP 
             instructions and LCT space is limited to 64 bytes.  This is the 
             default. 
  MLC16 
             Specifies a program containing MLC16 instructions.  This option 
             may be used for MLCP code/controllers but specific error checking 
             for the MLCP is not provided. 
             256 bytes are allowed for LCT space. 
  NLS 
             Do not list source program. 
  NLU 
             Do not list the update file.  This is the default. 
  NOU 
             Do not generate object unit. 
  NRELOC 
             Do not generate relocation information in the object unit. 
  NSO 
             Do not produce updated source.  This is the default. 
  NUI 
             Do not use update input.  This is the default. 
  OPTUI 
             Use Update Input, if it exists.  If not, proceed without 
             producing any diagnostics. 
  OU 
             Generate object unit.  The default is OU. 
  RELOC 
             Generate relocation information in the object unit.  This is the 
             default. 
  SO 
             Produce updated source.  The default is NSO. 
  SR[CH] (list) 
             This option augments the specification of the accounts and 
             packsets to be searched if the ELSIE processor encounters an 
             INCLUDE preprocessor directive which specifies a file only by 
             file name. The list is a list of accounts, possibly qualified by 
             packset,separated by commas.  Each account designation must have 
             a leading period.  A maximum of eight accounts may be specified. 
             If the file is not found in any of these accounts, the :LIBRARY 
             account and the user's running account will then be searched. 
  UI 
             Use update input.  The default is NUI unless UI fid is specified 
             on invocation. 
00001
00002
00004
00003
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
INPUT_OUTPUT
Format: 
label LABEL [comments] 
Note: 
1.  label is a required field.  If the location counter contains an odd value, 
    a 1-byte "NOP" instruction shall be generated and the instruction counter 
    incremented.  The specified label is defined as a symbol having the value 
    of the (possibly incremented) location counter. 
Description: 
The LABEL statement may be used to define a label within the CCP section 
suitable for use with the SYMDEF statement. 
00002
00001
Format: 
LCT LOC=expression,VALUE=expression [comments] 
Parameter 
LOC=expression    specifies a value in the range 0 to 63 for MLCP or in the 
range 0 to 255 for MLC16. 
VALUE=expression    specifies a value in the range 0 to 255.  ELSIE produces a 
warning diagnostic (of severity 0) if the programmer initializes to a non-zero 
value any LCT byte which is defined as "reserved for firmware use". 
Description: 
The LCT statement is used to specify the initial values for the Line Control 
Table bytes for an ELSIE program. 
Rules: 
1.  One or more blanks must appear before the statement. 
2.  The LCT statement is legal only between the LCTS and ENDLCTS statement. 
3.  As many LCT statements may be specified as are needed to initialize the 
    LCT. 
00002
00001
00003
Format: 
[label] LCTS [comments] 
Description: 
The LCTS statement is used to declare the beginning of the Line Control Table 
section of an ELSIE program. 
Rules: 
1.  The LCTS statement, if used in an ELSIE program, must appear before the 
    first LCT, TABLE, ASCII, or executable instruction statement. 
2.  Only one LCTS statement may appear in each MLCP/MLC16 assembly.  The 
    specified label, if present, will be defined as having the address of the 
    beginning of the LCT table. 
00001
00002
Format: 
[label] mnemonic lctval, =immediate_constant 
Parameters: 
mnemonic    specifies one of the mnemonics described in the following table. 
lctval    specifies an assembler constant or expression whose value lies in 
the range 0 to 255. 
immediate_constant    must be an assembler constant or expression whose value 
lies in the range -128 to 255.  Enter ?? for the complete table. 
  Mnemonic   Instruction 
  LBFL 
             Test and Clear LCT 
  LBFX 
             Test and Clear Extended 
  LBL 
             Bit Test LCT 
  LBTL 
             Test and Set LCT 
  LBTX 
             Test and Set Extended 
  LBX 
             Bit Test Extended 
Description: 
These instructions are used to test, with a specified LCT byte, a constant 
value contained within the instruction itself, set or reset the indicators and 
to update the value contained in that LCT byte. 
00008
00002
00003
00004
00005
00006
00007
00001
Format: 
[label] mnemonic lctvalue 
Parameter: 
mnemonic    specifies one of the mnemonics described in the following table. 
lctvalue    specifies an assembler constant or expression whose value lies in 
the range 0 to 255.  Enter ?? for the complete table. 
  Mnemonic   Instruction 
  ADD 
             Add to R 
  ADDB 
             Add to B 
  ANDB 
             AND to B register 
  CAD 
             Add to carry with R 
  CADB 
             Add with carry to B 
  CB 
             Arithmetic compare B 
  CLL 
             Clear LCT 
  DADD 
             Decimal add to R 
  DECL 
             Decrement LCT 
  INCL 
             Increment LCT 
  JSRV 
             Jump to subroutine via vector 
  JV 
             Jump via vector 
  LDB 
             Load B 
  ORB 
             OR to B register 
  STB 
             Store B 
  SUB 
             Subtract from R 
  SUBB 
             Subtract from B 
  XORB 
             Exclusive OR to B register 
Description: 
The LCT instructions are used to move data to or from a specified LCT byte for 
the currently active line. 
00002
00003
00004
00005
00006
00007
00008
00009
00010
00020
00011
00012
00013
00014
00015
00001
00016
00017
00018
00019
Format: 
LIST [listoptions] [comments] 
Parameters: 
listoptions    specifies between one and three of the following options, 
separated by commas: 
o   ON    list source/update. 
o   OFF    do not list source/update. 
o   PUSH    push the current listing state (on/off) onto a stack, before 
    honoring ON or OFF if present. 
o   PULL    pull listing state off top of "push" stack before honoring ON or 
    OFF if present. 
o   INVIS    do not print the LIST statement itself. 
Note:  ON and OFF are mutually exclusive, as are PUSH and PULL.  The initial 
setting is "LIST ON".  If the LIST statement is invoked with no options, "LIST 
ON" is assumed. 
Description: 
The LIST statement is used to control the listing of the source and update 
lines. 
Rules: 
1.  One or more blanks must appear before the statement. 
00002
00001
00003
Format: 
LISTINC [listoptions] [comments] 
Parameters: 
The LISTINC statement accepts the same options as the LIST statement, and 
behaves similarly except that the initial setting is "LISTINC OFF". 
Description: 
The LISTINC statement is used to control the listing of lines read from an 
INCLUDE file. 
Rules: 
1.  One or more blanks must appear before the statement. 
00002
00001
00003
MNEMONICS
The following portions of this HELP message contain the Mnemonic Codes, their 
instruction and the HELP that will provide the Instruction Format.  This 
information can be accessed by either typing a ? or ?? after this message, or 
by typing: 
    HELP MNEMONIC mnemonic 
    Example: HELP MNEMONIC AND 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic       Instruction 
  AND 
                 AND R register 
                 See HELP DO2, DO3 
  B 
                 Unconditional Branch 
                 See HELP BRANCH. 
  BAL 
                 See HELP BRANCH 
  BANR 
                 See HELP BRANCH 
  BAR 
                 See HELP BRANCH 
  BARF 
                 Branch if Adapter Ready False 
                 Synonymous Mnemonic: BANR 
                 See HELP BRANCH 
  BART 
                 Branch if Adapter Ready True 
                 Synonymous Mnemonic: BAR 
                 See HELP BRANCH 
  BE 
                 See HELP BRANCH 
  BEF 
                 Branch if Equal False (.. Not Equal) 
                 Synonymous Mnemonic: BNE 
                 See HELP BRANCH. 
  BET 
                 Branch if Equal True 
                 Synonymous Mnemonic: BE 
                 See HELP BRANCH. 
  BLB 
                 See HELP BRANCH 
  BLBF 
                 Branch if Last Block False 
                 Synonymous Mnemonic: BNLB 
                 See HELP BRANCH 
  BLBT 
                 Branch if Last Block True 
                 Synonymous Mnemonic: BLB 
                 See HELP BRANCH 
  BLC 
                 See HELP BRANCH 
  BLCF 
                 Branch if Last Character False 
                 Synonymous Mnemonic: BNLC 
                 See HELP BRANCH 
  BLCT 
                 Branch if Last Character True 
                 Synonymous Mnemonic: BLC 
                 See HELP BRANCH 
  BNE 
                 See HELP BRANCH 
  BNLB 
                 See HELP BRANCH 
  BNLC 
                 See HELP BRANCH 
  BNVB 
                 See HELP BRANCH 
  BNZ 
                 See HELP BRANCH 
  BS 
                 Branch to Subroutine (.. And Link) 
                 Synonymous Mnemonic: BAL 
                 See HELP BRANCH. 
  BVB 
                 See HELP BRANCH 
  BVBF 
                 Branch if Valid Block False 
                 Synonymous Mnemonic: BNVB 
                 See HELP BRANCH 
  BVBT 
                 Branch if Valid Block True 
                 Synonymous Mnemonic: BVB 
                 See HELP BRANCH 
  BZ 
                 See HELP BRANCH 
  BZF 
                 Branch if Zero False (.. Not Zero) 
                 Synonymous Mnemonic: BNZ 
                 See HELP BRANCH. 
  BZT 
                 Branch if Zero True 
                 Synonymous Mnemonic: BZ 
                 See HELP BRANCH. 
  C 
                 Compare R register 
                 See HELP DO2, DO3 
  CCH 
                 Calculate Cyclic Check 
                 Synonymous Mnemonic: CRC 
                 See HELP GENERIC 
  CRC 
                 See HELP GENERIC 
  DEC 
                 Decrement R register 
                 See HELP GENERIC 
  GNB 
                 Get Next Block (.. Next CCB) 
                 Synonymous Mnemonic: GNCCB 
                 See HELP GENERIC 
  GNCCB 
                 See HELP GENERIC 
  IN 
                 Load line register "n" into R 
                 Synonymous Mnemonic: LDLR 
                 See HELP I_O 
  INIT 
                 See HELP GENERIC 
  INT 
                 See HELP GENERIC 
  INTR 
                 Interrupt FEP CPU 
                 Synonymous Mnemonic: INT 
                 See HELP GENERIC 
  INZ 
                 Soft-initialize MLCP 
                 Synonymous Mnemonic: INIT 
                 See HELP GENERIC 
  J 
                 See HELP BRANCH 
  JUMP 
                 Jump 
                 Synonymous Mnemonic: J 
                 See HELP BRANCH 
  LD 
                 Load R register 
                 See HELP DO1, DO2, DO3 
  LDLR 
                 See HELP INPUT_OUTPUT 
  NOP 
                 No operation 
                 See HELP GENERIC 
  OR 
                 OR R register 
                 See HELP DO2, DO3 
  OUT 
                 Store R into line register "n" 
                 Synonymous Mnemonic: STLR 
                 See HELP I_O 
  RECV 
                 Receive data into R 
                 See HELP SEND_RECEIVE 
  RET 
                 Return from BS or BAL 
                 Synonymous Mnemonic: Return 
                 See HELP GENERIC 
  RETURN 
                 See HELP GENERIC 
  SEND 
                 Transmit data from R 
                 See HELP SEND_RECEIVE 
  SFS 
                 Search For Synchronization 
                 Synonymous Mnemonic: SYNC 
                 See HELP GENERIC 
  SHIFT 
                 See HELP GENERIC 
  SR 
                 Shift R register right 1 bit 
                 Synonymous Mnemonic: SHIFT 
                 See HELP GENERIC 
  ST 
                 Store R register 
                 See HELP DO1, DO2 
  SYNC 
                 See HELP GENERIC 
  TLU 
                 Table look-up 
                 See HELP DO2 
  WAIT 
                 Suspend CCP 
                 See HELP GENERIC 
  XOR 
                 XOR R register 
                 See HELP DO2, DO3 
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
00046
00047
00048
00049
00050
00051
00052
00053
00054
00055
00056
00057
00058
MNEMONICS
NOTATION_CONVENTIONS
The following table gives notation conventions used in this manual to describe 
commands, statements, directives, and other language elements.  The 
information can be accessed by either typing a ? or ??, or by typing: 
HELP (CALF|ELSIE) NOTATION_CONVENTIONS convention 
where LOWER_CASE, CAPITAL_LETTERS, SPECIAL_CHARACTERS, NUMERALS, BRACES, 
OR_BAR, VERTICAL_ELLIPSIS and BLANKS are the available conventions. Example: 
HELP (ELSIE) NOTATION BRACES 
  Notation      Description 
  Lower-case Letters 
                Lower-case letters indicate that the element is a variable, to 
                be replaced with the desired value. 
  CAPITAL LETTERS 
                Capital letters indicate a literal, to be entered as shown. 
  Special Characters 
                Special characters are literals, to be entered as shown. 
  Numerals 
                Numerals standing alone are literals, to be entered as shown. 
                Numerals embedded in or affixed to a string of capital letters 
                are also literals, to be entered as shown, for example, PL6. 
                Numerals embedded in or affixed to a string of lower case 
                letters are part of the variable name to be replaced with a 
                desired value, for example, fid1. 
  Brackets 
                An element inside brackets is optional. 
  Braces 
                Elements stacked inside a pair of braces identify a required 
                choice.  The braces may be elongated to contain the possible 
                choices, or may be represented by vertically-stacked printed 
                braces. 
                    {shift_count}   means that either a value for 
                    {R1}            shift_count or the word R1 must be 
                                    entered. 
                Alternatively, the vertical OR bar is used to separate the 
                choices, thus:  {shift_count|R1} 
  OR Bar 
                The OR bar separates elements in a list from which one element 
                may be, or must be, chosen. 
                    {R1|shift_count}  means that either the word R1 or the 
                                      value of shift_count must be entered. 
  Vertical Ellipsis 
                The vertical ellipsis indicates that zero or more commands or 
                instructions have been omitted. 
                    START CCP 
                         .              means that there are zero or more 
                         .              statements omitted between the 
                         .              CCP and END statements. 
                          END 
  Blanks 
                Where blanks are shown in syntax formats, one or more blanks 
                must be used except inside character literal strings. 
00009
00006
00005
00002
00002
00001
00004
00007
00003
00008
00008
Format: 
OUNAME name [comments] 
Parameters: 
name    specifies a valid ELSIE symbol name. 
Description: 
The OUNAME statement may be used to specify the name to be inserted into the 
ELSIE object unit's head record.  Only one OUNAME statement may be used per 
program.  If no OUNAME statement appears, the object unit will be named 
"MLCP". 
Rules: 
1.  One or more blanks must appear before the statement. 
00002
00001
00003
SEND_RECEIVE
Format: 
[label] RESET lctlocation,bitvalue [comments] 
Parameters: 
lctlocation    specifies an LCT symbol. 
bitvalue    specifies an immediate value in the form =value. 
Code Generated: 
    LD       ~ bitvalue 
    AND      lctlocation 
    ST       lctlocation 
Description: 
Resets the bits specified by bit value at lct location to 0. 
Example: 
    33.000      30 216  90025314           RESET  LCT20,=253 
                        5114 
00002
00003
00004
00001
SEND_RECEIVE
Format: 
[label] mnemonic [optionlist] [comments] 
Parameters: 
optionlist    specifies one or more of the following options, separated by 
commas: 
o   PARITY    sets the '02'X bit in the SEND or RECV instruction, causing the 
    MLCP to apply parity characteristics as specified by the appropriate LCT 
    byte to the I/O operation. 
o   CRC    sets the '01'X bit in the SEND or RECV instruction, causing the 
    MLCP to apply the cyclic redundancy checks to the I/O operation. 
o   WAIT    causes the SEND instruction (or sequence) to be followed by a WAIT 
    instruction; for a RECV operation, causes the RECV instruction (or 
    sequence) to be preceded by a WAIT instruction. 
o   REPEAT=expression    causes ELSIE to generate the specified number of SEND 
    or RECV instructions, separated by WAIT instructions.  If the REPEAT 
    option is used, the WAIT option will control whether or not the entire 
    sequence of SEND (or RECV) and WAIT instructions will be preceded or 
    followed by a WAIT instruction. 
o   BROADBAND    specifies that each WAIT instruction generated (before, 
    after, or within the generated instruction sequence) is to be preceded by 
    a BART (Branch on Adapter Ready True) instruction which will cause the 
    WAIT to be bypassed if the adapter's buffer is ready to accept or provide 
    data. 
mnemonic    specifies one of the following mnemonics: 
SEND RECV 
To obtain HELP messages for the mnemonics enter HELP SEND mnemonic.  For 
example, HELP SEND SEND.  Descriptions are in a tabular format with two 
columns like so: 
  Mnemonic     Instruction 
  SEND 
               Transmit data from R 
  RECV 
               Receive data into R 
Description: 
The send and receive instructions are used to transfer data between the MLCP's 
R register and line register 1 for the current communication line. 
Notes: 
1.  While Send and Receive Instructions are mnemonics that correspond to a 
    certain opcode, some combinations of Send and Receive with options cause 
    more than one instruction to be generated. 
Example: 
    35.000      32 21F  60E50201   TRN     SEND   WAIT,BROADBAND,REPEAT=2 
                        60E50201 
00004
00006
00005
00001
00003
00002
Format: 
[label] SET lctlocation,bitvalue [comments] 
Parameters: 
lctlocation    specifies an LCT symbol. 
bitvalue    specifies an immediate value in the form =value. 
Code Generated: 
    LD       bitvalue 
    OR       lctlocation 
    ST       lctlocation 
Description: 
Sets the bits specified by bit value at lctlocation to 1. 
00002
00003
00001
Format: 
[label] SETADDR lctlocation,labelname [comments] 
Parameters: 
lctlocation    specifies an LCT symbol. 
labelname    specifies a label that appears on a TABLE statement or on a CCP 
instruction. 
Code Generated: 
    LD    =LABELNAME/'FF00'X 
    ST    lctlocation 
    LD    =LABLENAME&'00FF'X 
    ST    lctlocation+1 
Description: 
Stores the address specified by label name at lct location. 
00002
00003
00001
    The ELSIE statement format and general rules pertaining to its usage 
    appear below. 
Format: 
label  command  argument 
Rules: 
1.  Each statement must begin on a new record. 
2.  Each statement must follow the statement format exactly.  Statements are 
    terminated by a blank or an end-of-record after the argument field.  All 
    characters after this point are considered comments. 
    NOTE:  Certain statements have optional argument fields (e.g., D01 
    instructions and the LCT, EJECT, and LIST statements).  If such a 
    statement is invoked without an argument field, any comments on the 
    statement must begin with the comment introducer "/*". 
3.  Comments may be placed at any point within a statement where a blank is 
    legal.  A comment must begin with a comment introducer "/*" and must end 
    with "*/". 
4.  The presence of a semicolon in the record indicates that the statement 
    will be continued on the next record.  All characters between the 
    semicolon and end-of-record are considered comments. 
5.  A statement may be continued on as many records as necessary.  At least 
    the first position of each continuation record must be blank.  Processing 
    of each continuation record begins with the first non-blank character. 
6.  When a label is permitted by the statement's syntax and is present, it 
    must begin in the first position of the first record of the statement. 
    When a label is not permitted by the statement's syntax, or is permitted 
    but not present, at least the first character of the first record of the 
    statement must be blank. 
7.  The label, if present, must consist of a legal ELSIE symbol. 
8.  Any place that a blank is legal, any number of blanks may be used, except 
    within character string constants. 
9.  Both the label and argument fields may be optional, required or not 
    allowed depending on the particular command used.  Refer to the command 
    format for rules pertaining to the individual command. 
00001
Format: 
An ELSIE symbol is any legal PL-6 symbol.  See the CP-6 PL-6 Reference Manual 
(CE44). 
Rules: 
1.  Symbols in ELSIE can only be associated with values that can be determined 
    at assembly time. 
2.  Symbols must be unique. 
00001
Format: 
SYMDEF label[,label, ... ] [comments] 
Parameters: 
label    specifies one of the following: 
o   The beginning of the LCT area (i.e., the label on the LCTS statement); 
o   The beginning of a look-up table (i.e., the label on a TABLE statement); 
o   The beginning of a block of code in the CCP section (i.e., the label on a 
    CCP or LABEL statement). 
Labels which fall into one of these classes are guaranteed to be defined at 
locations on even-byte boundaries, and thus to have integral word addresses 
from the FEP point of view.  Labels which have been SYMDEF'ed within an ELSIE 
program may be accessed from PL-6 or CALF programs by declaring them as 
SYMREF'ed data items.  ELSIE has no equivalent for the CP-6 ENTDEF and ENTREF 
capabilities. 
Description: 
The SYMDEF statement may be used to make labels within the ELSIE program 
accessible to other programs. 
Rules: 
1.  One or more blanks must appear before the statement. 
00002
00001
00003
Format: 
label TABLE optionlist [comments] 
Parameters: 
optionlist    is one or more of the options described in Table 2-9, separated 
by commas. 
Note: 
1.  label    is a required field.  In a multi-segment table, the labels on the 
    TABLE statements must be identical. 
    optionlist    is one or more of the following options: 
    SIZE, TLU, DTRANSLATE, DTRANSFER, NODEFAULT, STRINGAREA 
    These may be accessed by typing HELP TABLE option.  For example, HELP 
    TABLE TLU.  Descriptions are in a tabular format with two columns like so: 
  Option     Description 
  DTRANSFER=label 
             Specifies that values in the look-up table which are not defined 
             via TRANSFER or TRANSLATE statements are to be initialized with a 
             value which will cause control to be transferred to "label" when 
             the TLU instruction is issued.  If the DTRANSFER option is used, 
             the DTRANSLATE option may not be used. 
  DTRANSLATE=value 
             Specifies that values in the look-up table which are not defined 
             via TRANSFER or TRANSLATE statements are to be initialized with 
             the specified value, which must be in the range 0 to 127.  If the 
             DTRANSLATE option is used, the DTRANSFER option may not be used. 
  NODEFAULT 
             Specifies that ELSIE should not attempt to provide default values 
             for the table; instead, a diagnostic (severity 2) is produced if 
             the programmer does not provide values for all bytes within the 
             table. 
  SIZE=value 
             Specifies the number of bytes to be reserved for the look-up 
             table.  If the "size" option is not specified, a value of 256 
             shall be assumed.  "value" must be an ELSIE constant or 
             expression in the range 1 to 256.  In a multi-segment table, the 
             SIZE option is legal only on the first TABLE statement. 
  STRINGAREA=expression 
             Specifies the point within the table at which ASCII string 
             structures are to be allocated.  The specified expression must 
             have a value which is less than 128 or the value specified on the 
             SIZE option, whichever is smaller. If no SIZE option was 
             specified, the value must be less than 128. 
  TLU=label 
             Specifies the label of a TLU instruction in the CCP section which 
             will be used to access this table (or table segment).  The TLU 
             option is required for any TRANSFER statement appearing in the 
             table definition. 
Rules: 
1.  If neither the DTRANSLATE, DTRANSFER, nor the NODEFAULT option appears on 
    the TABLE command, ELSIE will initialize any byte of the table for which 
    no TRANSLATE or TRANSFER statement exists with a value equal to the byte's 
    index into the table, taken modulo 128.  This will cause any TLU 
    instruction which accesses such a byte in the table to behave as a "set 
    high-order bit to zero" instruction. 
2.  ELSIE allocates each table starting at an even-numbered byte address, to 
    ensure that the table (as stored in FEP memory) begins on a word boundary. 
Rules for Building Multi-segment Tables: 
The following rules apply to building a multi-segment table. 
1.  The options SIZE, DTRANSLATE, NODEFAULT, and STRINGAREA, if used, must 
    appear on the TABLE statement defining the first segment of the table, and 
    may not appear on the second (or subsequent) TABLE statements in the 
    table. 
2.  DTRANSFER may not be used. 
3.  If the TRANSFER or ASCII statements are used within a particular table 
    segment, the TABLE statement which begins the segment must specify the TLU 
    option. 
4.  The rules defined in the section entitled, "Table Format and Layout" 
    concerning conflicts between segment definitions must be adhered to. 
Description: 
The TABLE statement is used to define the beginning of a look-up table or 
beginning of a segment of a multi-segment look-up table. 
00010
00003
00004
00005
00002
00001
00009
00006
00007
00008
Format: 
label TARGET tlulabel [comments] 
Parameters: 
tlulabel    a label that occurs on a TLU statement. 
Description: 
The TARGET statement may be used to declare a label suitable for use as the 
target of a TLU instruction's indexed branch table. 
Notes: 
The following steps occur when a TARGET statement is encountered: 
1.  If the specified TLU label has not yet been encountered, proceed to step 
    (3).  This is an error, but will be reported by the table builder during 
    the second assembly pass. 
2.  Calculate the offset between the TLU label and the current location 
    counter value.  If the offset is even, generate a NOP instruction and bump 
    the location counter. 
3.  Define the specified label as a symbol having the value of the location 
    counter. 
00002
00003
00001
Format: 
TITLE 'title'[,INVIS] [comments] 
Parameters: 
INVIS    specifies that the TITLE statement will not appear on the listing, 
although the page eject will occur according to the rules specified below. 
'title'    specifies a character string. 
Description: 
The TITLE statement specifies the title to be printed on the assembly listing. 
Any number of TITLE statements may appear in an ELSIE program.  The specified 
title will be printed at the top of each page of the listing, starting with 
the page on which the TITLE statement appears and continuing up to the end of 
the program or up to (but not including) the page on which the next TITLE 
statement is printed.  Normally, each TITLE statement will cause a page eject 
to occur before the statement is printed.  However, if the first statement of 
an ELSIE program (not including blank and comment lines) is a TITLE, the title 
specified in the statement will appear on page one of the listing, and the 
statement will not cause a page eject. 
Rules: 
1.  One or more blanks must appear before the statement. 
00002
00001
00003
Format: 
TRANSFER IN=value,TARGET=label[,selection] [comments] 
Parameters: 
IN=value    specifies the look-up table index, as in the TRANSLATE command. 
TARGET=label    specifies the label (in the CCP section) to which control 
should be transferred by the TLU instruction if this value in the table is 
accessed. 
selection    is optional, operates as described for the TRANSLATE command. 
Description: 
The TRANSFER statement is used to place an indexed branch value into a look-up 
table.  The following process occurs: 
o   If the "TLU=label" option did not appear on the most recent TABLE 
    statement, diagnose and proceed to the next statement; 
o   Calculate OFFSET = ADDR(TARGET) - (ADDR(TLU) + 5); 
o   If OFFSET < 0, or OFFSET > 254, diagnose "out of range" condition and 
    proceed to the next statement; 
o   If MOD (OFFSET, 2) = 1, diagnose "addressing error" and proceed to the 
    next statement; 
o   Store the value (OFFSET / 2) + '80'X in the appropriate entry (or entries) 
    in the look-up table. 
Rules: 
1.  One or more blanks must appear before the statement. 
00002
00001
00003
Format: 
TRANSLATE IN=value,OUT=value[,selection] [comments] 
Parameters: 
IN=value    specifies the basic index into the look-up table for which this 
translation character is to apply. Its value must be in the range 0 to 255, or 
0 to tablesize - 1 if the SIZE option was specified on the TABLE statement. 
OUT=value    specifies the value to be inserted into the look-up table.  It 
must lie in the range 0 to 127. 
selection    indicates that an entire class of table items (described by a bit 
mask) are to be set to a specified value.  The value is hereafter referred to 
as a "wildcard" value.  If present, the selection clause consists of one of 
the following forms: 
o   SELECT=expression    specifies a bit mask indicating which of the bits in 
    the index are "important".  ELSIE places the indicated OUT value into 
    every entry in the table for which the criteria: 
        (table_index & select_expression) = in_value 
    is true.  Rules for resolving conflicts between multiple SELECT'ed 
    translation or transfer commands may be found in the section entitled, 
    "Table Format and Layout." 
o   DONTCARE=expression    specifies a bit mask indicating which of the bits 
    in the index are "unimportant".  ELSIE places the indicated OUT value into 
    every entry in the table for which the criteria:  (table_index & 
    ~dontcare_expression) = in_value is true. 
If neither form of the selection clause appears, the specified OUT value shall 
be placed only in the single table entry specified by the IN value. 
Description: 
The TRANSLATE statement is used to place a character translation value into a 
look-up table. 
Rules: 
1.  One or more blanks must appear before the statements. 
00002
00001
00003
