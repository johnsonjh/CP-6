CALF is a Cross Assembly Language for the Front-end minicomputer. 
The assembler processes FEP CPU and Commercial Instruction Processor (CIP) 
instructions in long address form (LAF).  It handles a number of assembler 
pseudo operations but has no macro facility of its own. 
CALF is a classic two pass assembler.  The first pass assigns values to all 
the symbols in the program.  The second pass uses this information to create 
the object program.  In order to perform its function, the first pass must be 
able to determine the amount of memory used by all data-generating and machine 
operations.  Instances in which an expression may not contain any references 
to items that are yet to be declared are noted. 
For more HELP see: 
HELP (CALF) TOPICS    for a complete list of topics. 
HELP (CALF) MNEMONIC   for a complete list of mnemonics. 
?                      displays the next level of HELP message. 
??                     displays all levels of the current 
                       HELP message. 
Examples: 
1.  ....|....1....|....2....|....3....|....4 
    NB       EQU       4 
             DATA,NB   NB 
2.           DATA,NB   NB 
    NB       EQU       4 
3.  NB       EQU       4 
             SBIN,NB   FORWARD_VALUE 
             ... 
The above examples attempt to make a 4 byte (2 word) data object with an 
initial value.  Examples 1 and 3 are legal.  Example 3 illustrates that the 
initializing value isn't needed until the second pass of the assembly. 
Example 2 is illegal because it is a forward reference (it contains references 
to items that are yet to be declared) and the first pass cannot determine how 
many bytes of memory to reserve. 
  ************************************************************** 
  *   Copyright (c) Honeywell Bull Inc., 1988 
  ************************************************************** 
Format: 
[label]  ALIGN  [alignment_word] 
Parameters: 
label    is as an external value symbol whose value is the new value of the 
location counter. 
alignment_word    is one of the following words which specifies what kind of 
alignment is to be performed. 
    Word                Alignment Modulus 
    BYTE                8-bits / 1-byte 
    WORD                1-word 
    DOUBLE              2-words (even) 
    PAGE                256-words 
If an alignment_word is not supplied, the location counter is aligned at the 
next word boundary. 
Description: 
The ALIGN pseudo operation aligns the location counter for the current section 
to the specified boundary. 
00002
00001
    The following rules describe the argument field: 
1.  Each machine instruction and pseudo operation defines the format of its 
    argument field. 
2.  In some cases the argument field is a comma-separated list.  In such 
    cases, the m-th element of the argument will be denoted AF[m]. 
CPU_ADDRESS_SYLLABLES
The following list contains the symbols which are predefined by the assembler: 
    R1 - R7          FEP hardware arithmetic (R) registers 
    DR23, DR45,      Paired FEP hardware R registers 
    DR67 
    M1 - M7          FEP hardware mode (M) registers 
    B1 - B7          FEP hardware base (B) registers 
    $AF              The address form symbol (set to 2 for LAF) 
    K1 - K7          DPS6 hardware 32-bit arithmetic (K) registers 
    S1 - S3          Reserved for future use 
Format: 
[label]  mnemonic  branch_AS 
Parameters: 
Mnemonics beginning with B are Branch on Indicator format.  Mnemonics 
beginning with CB are Commerical Branch format. 
branch_AS    specifies the address of the instruction which will be executed 
after the branch. 
mnemonic    specifies one of the following mnemonics: 
    B       BAG     BAGE    BAL     BALE 
    BBF     BBT     BCF     BCT     BE 
    BG      BGE     BIOF    BIOT    BL 
    BLE     BNE     BNOV    BOV     BSE 
    BSU     CBE     CBG     CBGE    CBL 
    CBLE    CBNE    CBNOV   CBNSF   CBNTR 
    CBOV    CBSF    CBTR    CSNCB   CSYNC 
    NOP 
To obtain HELP messages for the mnemonics enter HELP BI mnemonic. 
For example, HELP BI BBT. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  B 
               Branch unconditionally 
  BAG 
               Branch if algebraically greater than 
  BAGE 
               Branch if algebraically greater than or equal to 
  BAL 
               Branch if algebraically less than 
  BALE 
               Branch if algebraically less than or equal to 
  BBF 
               Branch if bit-test indicator false 
  BBT 
               Branch if bit-test indicator true 
  BCF 
               Branch if carry false 
  BCT 
               Branch if carry true 
  BE 
               Branch if equal 
  BG 
               Branch if greater than 
  BGE 
               Branch if greater than or equal to 
  BIOF 
               Branch if I/O indicator false 
  BIOT 
               Branch if I/O indicator true 
  BL 
               Branch if less than 
  BLE 
               Branch if less than or equal to 
  BNE 
               Branch if not equal 
  BNOV 
               Branch if no overflow 
  BOV 
               Branch if overflow 
  BSE 
               Branch if signs equal 
  BSU 
               Branch if signs unlike 
  CBE 
               Branch if equal 
  CBG 
               Branch if greater than 
  CBGE 
               Branch if greater than or equal 
  CBL 
               Branch if less 
  CBLE 
               Branch if less than or equal 
  CBNE 
               Branch if not equal 
  CBNOV 
               Branch on no overflow 
  CBNSF 
               Branch on sign fault 
  CBNTR 
               Branch on no truncation 
  CBOV 
               Branch on overflow 
  CBSF 
               Branch on sign fault 
  CBTR 
               Branch on truncation 
  CSNCB 
               Synchronize and Branch 
  CSYNC 
               Synchronize 
  NOP 
               No operation 
Description: 
All instructions in this group are either Branch on Indicator or Commercial 
Branch format. 
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
00038
00037
00001
Format: 
[label]  mnemonic,R_reg  branch_AS 
Parameters: 
R_reg    Front-end hardware arithmetic (R) registers. 
branch_AS    specifies the address of the instruction which will be executed 
after the branch. 
mnemonic    specifies one of the following mnemonics: 
    BDEC    BEVN    BEZ     BGEZ    BGZ 
    BINC    BLEZ    BLZ     BNEZ    BODD 
To obtain HELP messages for the mnemonics enter HELP BR mnemonic. 
For example, HELP BR BDEC 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  BDEC 
               Branch and decrement 
  BEVN 
               Branch if R register even 
  BEZ 
               Branch if R register equal to zero 
  BGEZ 
               Branch if R register greater than or equal to zero 
  BGZ 
               Branch if R register greater than 0 
  BINC 
               Branch and increment 
  BLEZ 
               Branch if R register less than or equal to zero 
  BLZ 
               Branch if R register less than zero 
  BNEZ 
               Branch if R register not equal to zero 
  BODD 
               Branch if R register odd 
Description: 
All instructions in this group are Branch on Register format. 
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
00001
Format: 
[label]  mnemonic A_desc,A_desc[,A_desc] 
Parameters: 
A_desc    any legal alphanumeric descriptor. 
mnemonic    specifies one of the following mnemonics: 
    ACM     ALR     AME     MAT    SRCH    VRFY 
To obtain HELP messages for the mnemonics enter HELP CB2 mnemonic. 
For example, HELP CB1 MAT 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  ACM 
               Alphanumeric compare 
  ALR 
               Alphanumeric Move 
  AME 
               Alphnumeric move and edit 
  MAT 
               Alphanumeric move and translate 
  SRCH 
               Alphanumeric search 
  VRF 
               Alphanumeric verify 
Description: 
All instructions in this group require two or three alphanumeric descriptors. 
ACM and ALR require two descriptors; all others require three. 
00002
00003
00004
00008
00005
00001
00006
00007
Format: 
[label]  CBD  B_desc,N_desc 
[label]  CDB  N_desc,B_desc 
[label]  DME  N_desc,A_desc,A_desc 
Parameters: 
B_desc    any legal binary descriptor. 
N_desc    any legal numeric descriptor. 
A_desc    any legal alpha-numeric descriptor. 
mnemonic    is one of the following mnemonics: 
    CBD     CDB     DME 
To obtain HELP messages for the mnemonics enter HELP CB2 mnemonic. 
For example, HELP CB2 CBD. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  CBD 
               Convert binary to decimal 
  CDB 
               Convert decimal to binary 
  DME 
               Decimal move and edit 
Description: 
The instructions in this group all have different descriptor requirements. 
00002
00003
00005
00004
00001
Format: 
[label]  mnemonic N_desc,N_desc[,N_desc] 
Parameters: 
N_desc    any legal numeric descriptor. 
mnemonic    specifies one of the following mnemonics: 
    DAD     DCM     DDV    DMC     DML     DSB 
To obtain HELP messages for the mnemonics enter HELP CB3 mnemonic. 
For example, HELP CB3 DDV. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  DAD 
               Decimal add 
  DCM 
               Decimal compare 
  DDV 
               Decimal divide 
  DMC 
               Decimal move and convert 
  DML 
               Decimal multiply 
  DSB 
               Decimal subtract 
Description: 
All instructions in this group require two or three numeric descriptors.  DDV 
requires three descriptors; all others require two. 
00002
00003
00004
00008
00005
00006
00007
00001
Format: 
[label]  mnemonic N_desc[,dec_syllable] 
Parameters: 
N_desc    any legal numeric descriptor. 
dec_syllable    is an expression or an R register. 
mnemonic    specifies one of the following mnemonics: 
    DLS     DRS     DSH 
To obtain HELP messages for the mnemonics enter HELP CB4 mnemonic. 
For example, HELP CB4 DSH. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  DLS 
               Decimal left shift 
  DRS 
               Decimal right shift 
  DSH 
               Decimal shift 
Description: 
All the instructions in this group implement the CIP decimal shift operation. 
They require one numeric descriptor and shift count information. 
00005
00002
00003
00004
00001
Format: 
PACKED(AS,[digit_offset],[length],sign_type) 
UNPACKED(AS,[digit_offset],[length],sign_type) 
ALPHANUM(AS,[byte_offset],[length],[fill_option]) 
BINARY(AS[,length]) 
REMOTE(remote_descriptor_number) 
Parameters: 
AS    any legal CIP address syllable, specified as offset [,Bn[,Rn]]. 
digit_offset    an internal value expression that specifies the distance in 
digits, packed or unpacked from the word addressed by the CIP address 
syllable. 
length    an internal value expression that specifies the length in digits or 
bytes of the operand. 
sign_type    a word specifying the type and placement of the sign in the 
decimal number. 
For packed numbers it is: 
    UNSIGNED 
    TRAILING 
For unpacked numbers it is: 
    UNSIGNED        LEADING 
    TRAILING        OVERPUNCHED 
byte_offset    an internal value expression that specifies the distance in 
bytes from the word addressed by the CIP address syllable. 
fill_option    a word that specifies whether or not filling of short 
alphanumeric operands is to be done.  The legal values are FILL or NO_FILL. 
remote_descriptor_number    a non-negative internal value expression that 
specifies a remote descriptor to be used in a CIP operation. 
00001
    CIP instructions generate address references through a field called the 
    address syllable (AS).  The resolution of the AS field for non branch 
    instructions usually results in the formation of an effective address (EA) 
    which points to an operand but can also directly describe an operand. 
     0             8 9     11  12  13    15 
    - - - - - - - - ------------------------ 
    |               |   m    | @ |    n    | 
    - - - - - - - - ------------------------ 
m - Address modifier. 
@ - Direct/indirect address indicator (when m = 0 through 4); otherwise, 
    secondary address modifier. 
n - Register number (when 1 through 7). 
    The following rules describe the command field: 
1.  The command field is required for all statements. 
2.  The command field may be a one, two, or three element comma-separated 
    list.  The first element (often the only element) of the list identifies 
    the machine operation or pseudo operation to be performed.  The remaining 
    elements of the list typically identify registers and/or masks that are 
    part of the machine operation. 
3.  The second and third command field elements are denoted by CF[2] and CF[3] 
    respectively. 
1.  A comment record must begin with an asterisk (*) in the first character 
    position.  A comment record is not a statement and it cannot be continued. 
2.  A blank record cannot contain any non-blank characters. 
3.  Comment and blank records may occur anywhere (including between 
    continuation lines of a continued statement) in an CALF source program. 
    Comments appear on the program listing but otherwise have no meaning to 
    the assembler. 
4.  Comments can follow the end of a statement. 
    The single and double operand instructions generate address references 
    through a field called the Address Syllable.  The Address Syllable 
    defines: 
o   A location in memory that contains an operand; or 
o   A register that contains an operand; or 
o   An immediate operand where the operand is contained in the subsequent 
    word(s) of the instruction. 
The address syllable defines the addressing mode; these are as follows: 
o   Absolute addressing 
o   Base addressing 
o   Relative addressing 
Format: 
[label]  DATA[,unit_size]  [AF_list] 
      each element of the list, AF[i], looks like 
           value 
Parameters: 
label    will be defined as the address of the next available byte in the 
current section.  This will be the first byte reserved by DATA. 
unit_size    is an internal value expression without any forward references. 
It determines the unit size in bytes of each of the values initialized by the 
pseudo operation.  Valid values for unit_size are from 1 thru 4 bytes.  If 
unit_size is not supplied, then a unit size of 2 bytes (1 word) is assumed. 
value    is an internal or external value expression whose low-order bytes are 
used to initialize the reserved memory. 
Description: 
The DATA pseudo operation reserves a byte or bytes of memory and specifies 
initial values for it.  All the parts of the DATA pseudo operation are 
optional. 
Example: 
     ....|....1....|....2....|....3....|....4 
              DATA 
    Reserve 1 word (2 bytes) of memory and initialize it to zero. 
     NBYTES   EQU       3 
              DATA,NBYTES 1 
    Reserve 3 bytes of memory initialized to: 
        00 00 01 
              DATA      1,29,-1,NBYTES 
    Reserve 4 words (8 bytes) of memory initialized to: 
        0001 001D FFFF 0003 
              DATA,1    1,NBYTES+10,-2 
    Reserve 3 bytes of memory initialized to: 
        01 0D FE 
              DATA,4    9,':LSE','RRMS','G   ' 
    Reserve 16 bytes of memory initialized to: 
        0000 0009 3A4C 5345 5252 4D53 4720 2020 
00002
00003
00001
Format: 
[label] mnemonic,R_reg AS 
Parameters: 
R_reg    Front-end hardware arithmetic (R) registers. 
AS    any address syllable is legal.  mnemonic    specifies one of the 
following mnemonics: 
    ADD     AND     ANH     CMH     CMR 
    LDH     LDR     LLH     OR      ORH 
    STH x   STR x   SUB     SWR x   XOH 
    XOR 
x   Stores into the operand specified by the address syllable. 
To obtain HELP messages for the mnemonics enter HELP DO1 mnemonic.  For 
example, HELP DO1 ADD.  Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  ADD 
               Add to R register 
  AND 
               AND with R register 
  ANH 
               AND half-word (byte) with R register 
  CMH 
               Compare half-word (byte) to R register 
  CMR 
               Compare to R register 
  LDH 
               Load half-word (byte) into R register 
  LDR 
               Load R register 
  LLH 
               Load logical half-word (byte) into R register 
  OR 
               Inclusive OR with R register 
  ORH 
               Inclusive OR or half-word (byte) 
  STH x 
               Store R register half-word (byte) 
  STR x 
               Store R register 
  SUB 
               Subtract from R register 
  SWR x 
               Swap R register 
  XOH 
               Half-word (byte) exclusive or with R register. 
  XOR 
               Exclusive or with R register. 
Description: 
All instructions in this group are Double Operand (DO) format.  Immediate 
Register references must be to R registers. 
00002
00003
00004
00005
00006
00018
00007
00008
00009
00010
00011
00001
00012
00013
00014
00015
00016
00017
Format: 
[label]  mnemonic,B_reg  AS 
Parameters: 
B_reg    Front-end hardware base (B) register. 
AS    any address syllable is legal.  mnemonic    specifies one of the 
following mnemonics: 
    CMB     LDB     STB x   SWB x 
x   Stores into the operand specified by the address syllable. 
To obtain HELP messages for the mnemonics enter HELP DO2 mnemonic.  For 
example, HELP DO2 CMB.  Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  CMB 
               Compare to B register 
  LDB 
               Load B register 
  STB x 
               Store B register 
  SWB x 
               Swap B register 
x   Stores into the operand specified by the address syllable. 
Description: 
All instructions in this group are Double Operand (DO) format.  Immediate 
Register references must be to B_registers. 
00002
00006
00003
00001
00004
00005
Format: 
[label]  mnemonic,{R_reg|DR67}  AS 
Parameters: 
R_reg    Front-end arithmetic (R) registers. 
DR67    paired Front-end hardware R registers. 
AS    any address syllable is legal.  mnemonic    specifies one of the 
following mnemonics: 
    DIV     MUL 
To obtain HELP messages for the mnemonics enter HELP DO3 mnemonic. 
For example, HELP DO3 DIV. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  DIV 
               Divide R register 
  MUL 
               Multiply R register 
Description: 
The two instructions in this group are Double Operand (DO) format.  Immediate 
register references must be to R registers.  A DR67 register reference for 
these instructions has special significance in terms of operation of the 
instructions and what registers are used. 
00004
00002
00003
00001
Format: 
[label]  mnemonic,B_reg  mem_ref_AS 
Parameters: 
B_reg    Front-end hardware base (B) register. 
mem_ref_AS    an address syllable that may not be in either Immediate Register 
or Operand form. 
mnemonic    specifies one of the following mnemonics: 
    LAB     LNJ 
To obtain HELP messages for the mnemonics enter HELP DO4 mnemonic. 
For example, HELP DO4 LAB. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  LAB 
               Load effective address into B register 
  LNJ 
               Load B register and jump (link jump) 
Description: 
The two instructions in this group are Double Operand (DO) format.  For the 
LAB instruction, mem_ref_AS may not specify an Immediate Register.  For the 
LNJ instruction, mem_ref_AS may not specify either an Immediate Register or 
Immediate Operand. 
00004
00002
00003
00001
Format: 
[label]  mnemonic,M_reg  AS 
Parameters: 
M_reg    Front-end hardware mode (M) register. 
AS    any address syllable is legal. 
mnemonic    specifies one of the following mnemonics: 
    MTM     STM 
To obtain HELP messages for the mnemonics enter HELP DO5 mnemonic. 
For example, HELP DO5 MTM 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  MTM 
               Modify/test M register 
  STM 
               Store M register 
Description: 
The two instructions in this group are Double Operand (DO) format.  Note that 
the register operand is an M register.  Immediate Register references must be 
to R registers. 
00004
00002
00001
00003
Format: 
EJECT [INVIS] 
Parameters: 
INVIS    causes the pseudo option not to appear in the listing. 
Description: 
The EJECT pseudo option will cause a skip to next page to be generated while 
listing. 
00002
00001
Format: 
END  [start_address] 
Parameters: 
start_address    defines an address in one of the sections of the assembly. 
This address will be forwarded to the linker as the starting address of the 
program.  The actual function of the start address is determined by the 
linker. 
Description: 
The END pseudo operation terminates the assembly.  It must be the last 
statement in the assembly. 
00002
00001
SYMDEF_ENTDEF
SYMREF_ENTREF
Format: 
symbol  EQU  expression 
Parameters: 
symbol    is the symbol being defined. 
expression    is an internal, external, or register value expression without 
any forward references.  Its value and the kind of value it is defines the 
symbol. 
Description: 
The EQU pseudo operation defines a symbol.  The value associated with that 
symbol is determined by the expression. 
Rules: 
1.  The EQU pseudo operation can define internal, external, or register 
    symbols.  Internal and external symbols are defined by specifying an 
    expression of that type.  Register symbols may be defined from other 
    register symbols. 
2.  A symbol may not be defined twice. 
00002
00001
00003
    Expressions are sequences of operands and operators which can be evaluated 
    to produce a result.  The kind of result produced is used to describe the 
    kind of expression.  CALF currently recognizes two kinds of expressions: 
    internal and external value expressions. 
    Expressions in CALF look very much like expressions in other languages. 
    There are dyadic and monadic operators.  Evaluation is from left to right 
    except for the priority of the various operators.  Parentheses may be used 
    to control the order of evaluation. 
    Legal expression operands are: 
o   constants -- For bit string and character string constants the low-order 
    32 bits, possibly padded with high-order zeros, are used. 
o   symbols whose associated value is internal or external -- Names of 
    sections and register values cannot be manipulated in expressions. 
o   all predefined assembler symbols. 
Legal expression operators are in a tabular format with three columns like so: 
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
    The following rules apply to the use of fields: 
1.  A statement can contain three fields:  label (LF), command (CF) and 
    argument (AF). 
2.  Fields are separated from each other by one or more blanks. 
3.  Except for some types of constants, fields do not contain blanks. 
Format: 
[label] mnemonic 
Parameters: 
mnemonic    specifies one of the following mnemonics: 
    ASD     BRK     CNFG    DQA     DQH 
    HLT     LRDB    MCL     MMM     QOH 
    QOT     RSC     RTCF    RTCN    RTT 
    SRDB    VLD     WDTF    WDTN 
To obtain HELP messages for the mnemonics enter HELP GE1 mnemonic. 
For example, HELP GE1 ASD. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  ASD 
               Activate segment descriptor 
  BRK 
               Breakpoint trap 
  CNFG 
               Configure 
  DQA 
               Dequeue on address 
  DQH 
               Dequeue from head 
  HLT 
               Halt 
  LRDB 
               Load remote descriptor base 
  MCL 
               Monitor call 
  MMM 
               Memory to memory move 
  QOH 
               Queue on head 
  QOT 
               Queue on tail 
  RSC 
               Rescan configuration 
  RTCF 
               Real-time clock off 
  RTCN 
               Real-time clock on 
  RTT 
               Return from trap 
  SRDB 
               Store remote descriptor base 
  VLD 
               Validate address, range and access rights 
  WDTF 
               Watchdog timer off 
  WDTN 
               Watchdog timer on 
Description: 
All instructions in this group are GEN format with no explicit arguments. 
00002
00003
00004
00021
00005
00006
00007
00008
00009
00010
00001
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
Format: 
[label]  mnemonic,R_reg B_reg 
Parameters: 
R_reg    Front-end hardware arithmetic (R) registers. 
B_reg    Front-end hardware base (B) registers. 
mnemonic    specifies one of the following mnemonics: 
    ACQ *x  LDT x   RLQ x   STT 
*   ACQ requires an R register in the CF[2] position.  It is illegal for all 
    others. 
x   Requires a B_register in the AF1 position. 
To obtain HELP messages for the mnemonics enter HELP GE2 mnemonic.  For 
example, HELP GE2 LDT.  Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  ACQ *x 
               Acquire stack space 
  LDT x 
               Load stack address register 
  RLQ x 
               Relinquish stack space 
  STT 
               Store stack register 
*   ACQ requires an R register in the CF[2] position.  It is illegal for all 
    others. 
x   Requires a B register in the AF1 position. 
Description: 
All the instructions in the group are GEN format, and they all have the same 
opcode.  The instructions are distinguished by the second word of the 
instruction. 
00002
00006
00003
00001
00004
00005
Format: 
[label]  GEN  [AF_list] 
where AF_list is value or (number_of_bits,value) 
Parameters: 
label    will be defined as the address of the next available byte in the 
current section.  This will be the first byte reserved by GEN. 
number_of_bits    is an internal value expression without any forward 
references.  It determines how many of the low-order bits of its corresponding 
value are used to initialize reserved memory.  If supplied it must be between 
1 and 32. If not supplied, the 16 low-order bits are used. 
value    is an internal or external value expression whose low-order bits are 
used to initialize the reserved memory. 
Description: 
The GEN pseudo operation reserves bits of memory and specifies initial values 
for them. 
Rules: 
1.  The GEN pseudo operation reserves only the number of bits specified.  The 
    sum of all the number_of_bits need not be a multiple of eight. When 
    necessary for alignment, the rest of an incomplete byte is set to zeros. 
Example: 
     ....|....1....|....2....|....3....|....4 
              GEN 
    Reserve 1 word (2 bytes) of memory and initialize it to zero. 
     NBITS    EQU       17 
              GEN       (NBITS,1) 
    Reserve 3 bytes of memory initialized to: 
       00 00 80  (the last 7 uninitialized bits are zeroed) 
              GEN       1,29,-1,NBITS 
    Reserve 4 words (8 bytes) of memory initialized to: 
       0001 001D FFFF 0011 
              GEN       (3,1),(6,13),(7,-2) 
    Reserve 1 word (2 bytes) of memory initialized to: 
        26FE 
              GEN       (8,9),(32,':LSE'),(32,'RRMS'),(8,'G') 
    Reserve 10 bytes of memory initialized to: 
        093A 4C53 4552 524D 5347 
00002
00004
00001
00003
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
  ACM -   
    CB1 Instruction Format - 
      HELP CB1 ACM 
  ACM - 
      HELP CB1 ACM 
  ACQ -   
    GE2 Instruction Format - 
      HELP GE2 ACQ 
  ACQ - 
      HELP GE2 ACQ 
  ADD -   
    DO1 Instruction Format - 
      HELP DO1 ADD 
  ADD - 
      HELP DO1 ADD 
  ADV -   
    SI1 Instruction Format - 
      HELP SI1 ADV 
  ADV - 
      HELP SI1 ADV 
  AID -   
    SO3 Instruction Format - 
      HELP SO3 AID 
  AID - 
      HELP SO3 AID 
  ALIGN Pseudo Operation - 
      HELP ALIGN 
  ALR -   
    CB1 Instruction Format - 
      HELP CB1 ALR 
  ALR - 
      HELP CB1 ALR 
  AME -   
    CB1 Instruction Format - 
      HELP CB1 AME 
  AME - 
      HELP CB1 AME 
  AND -   
    DO1 Instruction Format - 
      HELP DO1 AND 
  AND - 
      HELP DO1 AND 
  ANH -   
    DO1 Instruction Format - 
      HELP DO1 ANH 
  ANH - 
      HELP DO1 ANH 
  Argument Field - 
      HELP ARGUMENT_FIELD 
  ASD -   
    GE1 Instruction Format - 
      HELP GE1 ASD 
  ASD - 
      HELP GE1 ASD 
B 
  B -   
    BI Instruction Format - 
      HELP BI  B 
  B - 
      HELP BI  B 
  BAG -   
    BI Instruction Format - 
      HELP BI BAG 
  BAG - 
      HELP BI BAG 
  BAGE -   
    BI Instruction Format - 
      HELP BI BAGE 
  BAGE - 
      HELP BI BAGE 
  BAL -   
    BI Instruction Format - 
      HELP BI BAL 
  BAL - 
      HELP BI BAL 
  BALE -   
    BI Instruction Format - 
      HELP BI BALE 
  BALE - 
      HELP BI BALE 
  BBF -   
    BI Instruction Format - 
      HELP BI BBF 
  BBF - 
      HELP BI BBF 
  BBT -   
    BI Instruction Format - 
      HELP BI BBT 
  BBT - 
      HELP BI BBT 
  BCF -   
    BI Instruction Format - 
      HELP BI BCF 
  BCF - 
      HELP BI BCF 
  BCT -   
    BI Instruction Format - 
      HELP BI BCT 
  BDEC -   
    BR Instruction Format - 
      HELP BR BDEC 
  BDEC - 
      HELP BR BDEC 
  BE -   
    BI Instruction Format - 
      HELP BI BE 
  BE - 
      HELP BI BE 
  BEVN -   
    BR Instruction Format - 
      HELP BR BEVN 
  BEVN - 
      HELP BR BEVN 
  BEZ -   
    BR Instruction Format - 
      HELP BR BEZ 
  BEZ - 
      HELP BR BEZ 
  BG -   
    BI Instruction Format - 
      HELP BI BG 
  BG - 
      HELP BI BG 
  BGE -   
    BI Instruction Format - 
      HELP BI BGE 
  BGE - 
      HELP BI BGE 
  BGEZ -   
    BR Instruction Format - 
      HELP BR BGEZ 
  BGEZ - 
      HELP BR BGEZ 
  BGZ -   
    BR Instruction Format - 
      HELP BR BGZ 
  BGZ - 
      HELP BR BGZ 
  BI CPU Instruction Format - 
      HELP BI 
  BINC -   
    BR Instruction Format - 
      HELP BR BINC 
  BINC - 
      HELP BR BINC 
  BIOF -   
    BI Instruction Format - 
      HELP BI BIOF 
  BIOF - 
      HELP BI BIOF 
  BIOT -   
    BI Instruction Format - 
      HELP BI BIOT 
  BIOT - 
      HELP BI BIOT 
  BL -   
    BI Instruction Format - 
      HELP BI BL 
  BL - 
      HELP BI BL 
  BLE -   
    BI Instruction Format - 
      HELP BI BLE 
  BLE - 
      HELP BI BLE 
  BLEZ -   
    BR Instruction Format - 
      HELP BR BLEZ 
  BLEZ - 
      HELP BR BLEZ 
  BLZ -   
    BR Instruction Format - 
      HELP BR BLZ 
  BLZ - 
      HELP BR BLZ 
  BNE -   
    BI Instruction Format - 
      HELP BI BNE 
  BNE - 
      HELP BI BNE 
  BNEZ -   
    BR Instruction Format - 
      HELP BR BNEZ 
  BNEZ - 
      HELP BR BNEZ 
  BNOV -   
    BI Instruction Format - 
      HELP BI BNOV 
  BNOV - 
      HELP BI BNOV 
  BODD -   
    BR Instruction Format - 
      HELP BR BODD 
  BODD - 
      HELP BR BODD 
  BOV -   
    BI Instruction Format - 
      HELP BI BOV 
  BOV - 
      HELP BI BOV 
  BR CPU Instruction Format - 
      HELP BR 
  BRK -   
    GE1 Instruction Format - 
      HELP GE1 BRK 
  BRK - 
      HELP GE1 BRK 
  BSE -   
    BI Instruction Format - 
      HELP BI BSE 
  BSE - 
      HELP BI BSE 
  BSU -   
    BI Instruction Format - 
      HELP BI BSU 
  BSU - 
      HELP BI BSU 
C 
  CAD -   
    SO1 Instruction Format - 
      HELP SO1 CAD 
  CAD - 
      HELP SO1 CAD 
  CB1 CIP Instruction Format - 
      HELP CB1 
  CB2 CIP Instruction Format - 
      HELP CB2 
  CB3 CIP Instruction Format - 
      HELP CB3 
  CB4 CIP Instruction Format - 
      HELP CB4 
  CBD -   
    CB2 Instruction Format - 
      HELP CB2 CBD 
  CBD - 
      HELP CB2 CBD 
  CBE -   
    BI Instruction Format - 
      HELP BI CBE 
  CBE - 
      HELP BI CBE 
  CBG -   
    BI Instruction Format - 
      HELP BI CBG 
  CBG - 
      HELP BI CBG 
  CBGE -   
    BI Instruction Format - 
      HELP BI CBGE 
  CBGE - 
      HELP BI CBGE 
  CBL -   
    BI Instruction Format - 
      HELP BI CBL 
  CBL - 
      HELP BI CBL 
  CBLE -   
    BI Instruction Format - 
      HELP BI CBLE 
  CBLE - 
      HELP BI CBLE 
  CBNE -   
    BI Instruction Format - 
      HELP BI CBNE 
  CBNE - 
      HELP BI CBNE 
  CBNOV -   
    BI Instruction Format - 
      HELP BI CBNOV 
  CBNOV - 
      HELP BI CBNOV 
  CBNSF -   
    BI Instruction Format - 
      HELP BI CBNSF 
  CBNSF - 
      HELP BI CBNSF 
  CBNTR -   
    BI Instruction Format - 
      HELP BI CBNTR 
  CBNTR - 
      HELP BI CBNTR 
  CBOV -   
    BI Instruction Format - 
      HELP BI CBOV 
  CBOV - 
      HELP BI CBOV 
  CBSF -   
    BI Instruction Format - 
      HELP BI CBSF 
  CBSF - 
      HELP BI CBSF 
  CBTR -   
    BI Instruction Format - 
      HELP BI CBTR 
  CBTR - 
      HELP BI CBTR 
  CDB -   
    CB2 Instruction Format - 
      HELP CB2 CDB 
  CDB - 
      HELP CB2 CDB 
  CIP Descriptor Formats - 
      HELP CIP 
  CL -   
    SO1 Instruction Format - 
      HELP SO1 CL 
  CL - 
      HELP SO1 CL 
  CLH -   
    SO1 Instruction Format - 
      HELP SO1 CLH 
  CLH - 
      HELP SO1 CLH 
  CMB -   
    DO2 Instruction Format - 
      HELP DO2 CMB 
  CMB - 
      HELP DO2 CMB 
  CMH -   
    DO1 Instruction Format - 
      HELP DO1 CMH 
  CMH - 
      HELP DO1 CMH 
  CMN -   
    SO1 Instruction Format - 
      HELP SO1 CMN 
  CMN - 
      HELP SO1 CMN 
  CMR -   
    DO1 Instruction Format - 
      HELP DO1 CMR 
  CMR - 
      HELP DO1 CMR 
  CMV -   
    SI1 Instruction Format - 
      HELP SI1 CMV 
  CMV - 
      HELP SI1 CMV 
  CMZ -   
    SO1 Instruction Format - 
      HELP SO1 CMZ 
  CMZ - 
      HELP SO1 CMZ 
  CNFG -   
    GE1 Instruction Format - 
      HELP GE1 CNFG 
  CNFG - 
      HELP GE1 CNFG 
  Command Field - 
      HELP COMMAND_FIELD 
  Comment and Blank Records - 
      HELP COMMENT_BLANK_RECORDS 
  Commercial (CIP) Address Syllable - 
      HELP CIP_ADDRESS_SYLLABLE 
  CPL -   
    SO1 Instruction Format - 
      HELP SO1 CPL 
  CPL - 
      HELP SO1 CPL 
  CPU Address Syllables - 
      HELP CPU_ADDRESS_SYLLABLES 
  CSNCB -   
    BI Instruction Format - 
      HELP BI CSNCB 
  CSNCB - 
      HELP BI CSNCB 
  CSYNC -   
    BI Instruction Format - 
      HELP BI CSYNC 
  CSYNC - 
      HELP BI CSYNC 
D 
  DAD -   
    CB3 Instruction Format - 
      HELP CB3 DAD 
  DAD - 
      HELP CB3 DAD 
  DAL -   
    SHL Instruction Format - 
      HELP SHL DAL 
  DAL - 
      HELP SHL DAL 
  DAR -   
    SHL Instruction Format - 
      HELP SHL DAR 
  DAR - 
      HELP SHL DAR 
  DATA Pseudo Operation - 
      HELP DATA 
  DCL -   
    SHL Instruction Format - 
      HELP SHL DCL 
  DCL - 
      HELP SHL DCL 
  DCM -   
    CB3 Instruction Format - 
      HELP CB3 DCM 
  DCM - 
      HELP CB3 DCM 
  DCR -   
    SHL Instruction Format - 
      HELP SHL DCR 
  DCR - 
      HELP SHL DCR 
  DDV -   
    CB3 Instruction Format - 
      HELP CB3 DDV 
  DDV - 
      HELP CB3 DDV 
  DEC -   
    SO1 Instruction Format - 
      HELP SO1 DEC 
  DEC - 
      HELP SO1 DEC 
  DIV -   
    DO3 Instruction Format - 
      HELP DO3 DIV 
  DIV - 
      HELP DO3 DIV 
  DLS -   
    CB4 Instruction Format - 
      HELP CB4 DLS 
  DLS - 
      HELP CB4 DLS 
  DMC -   
    CB3 Instruction Format - 
      HELP CB3 DMC 
  DMC - 
      HELP CB3 DMC 
  DME -   
    CB2 Instruction Format - 
      HELP CB2 DME 
  DME - 
      HELP CB2 DME 
  DML -   
    CB3 Instruction Format - 
      HELP CB3 DML 
  DML - 
      HELP CB3 DML 
  DO1 CPU Instruction Format - 
      HELP DO1 
  DO2 CPU Instruction Format - 
      HELP DO2 
  DO3 CPU Instruction Format - 
      HELP DO3 
  DO4 CPU Instruction Format - 
      HELP DO4 
  DO5 CPU Instruction Format - 
      HELP DO5 
  DOL -   
    SHL Instruction Format - 
      HELP SHL DOL 
  DOL - 
      HELP SHL DOL 
  DOR -   
    SHL Instruction Format - 
      HELP SHL DOR 
  DOR - 
      HELP SHL DOR 
  DQA -   
    GE1 Instruction Format - 
      HELP GE1 DQA 
  DQA - 
      HELP GE1 DQA 
  DQH -   
    GE1 Instruction Format - 
      HELP GE1 DQH 
  DQH - 
      HELP GE1 DQH 
  DRS -   
    CB4 Instruction Format - 
      HELP CB4 DRS 
  DRS - 
      HELP CB4 DRS 
  DSB -   
    CB3 Instruction Format - 
      HELP CB3 DSB 
  DSB - 
      HELP CB3 DSB 
  DSH -   
    CB4 Instruction Format - 
      HELP CB4 DSH 
  DSH - 
      HELP CB4 DSH 
E 
  EJECT Pseudo Operation - 
      HELP EJECT 
  ELSIE and CALF HELP Facilities - 
      HELP HELP 
  END Pseudo Operation - 
      HELP END 
  ENT -   
    SO4 Instruction Format - 
      HELP SO4 ENT 
  ENT - 
      HELP SO4 ENT 
  EQU Pseudo Operation - 
      HELP EQU 
  Expressions - 
      HELP EXPRESSIONS 
F 
  Fields - 
      HELP FIELDS 
G 
  GE1 CPU Instruction Format - 
      HELP GE1 
  GE2 CPU Instruction Format - 
      HELP GE2 
  GEN Pseudo Operation - 
      HELP GEN 
H 
  HLT -   
    GE1 Instruction Format - 
      HELP GE1 HLT 
  HLT - 
      HELP GE1 HLT 
I 
  INC -   
    SO1 Instruction Format - 
      HELP SO1 INC 
  INC - 
      HELP SO1 INC 
  INCLUDE Pseudo Operation - 
      HELP INCLUDE 
  Introduction - 
      HELP INTRODUCTION 
  Invocation and Options - 
      HELP INVOCATION 
  IO -   
    IO1 Instruction Format - 
      HELP IO1 IO 
  IO - 
      HELP IO1 IO 
  IO1 CPU Instruction Format - 
      HELP IO1 
  IO2 CPU Instruction Format - 
      HELP IO2 
  IOH -   
    IO1 Instruction Format - 
      HELP IO1 IOH 
  IOH - 
      HELP IO1 IOH 
  IOLD -   
    IO2 Instruction Format - 
      HELP IO2 IOLD 
  IOLD - 
      HELP IO2 IOLD 
J 
  JMP -   
    SO4 Instruction Format - 
      HELP SO4 JMP 
  JMP - 
      HELP SO4 JMP 
L 
  LAB -   
    DO4 Instruction Format - 
      HELP DO4 LAB 
  LAB - 
      HELP DO4 LAB 
  Label Field - 
      HELP LABEL_FIELD 
  LB -   
    SO2 Instruction Format - 
      HELP SO2 LB 
  LB - 
      HELP SO2 LB 
  LBC -   
    SO2 Instruction Format - 
      HELP SO2 LBC 
  LBC - 
      HELP SO2 LBC 
  LBF -   
    SO2 Instruction Format - 
      HELP SO2 LBF 
  LBF - 
      HELP SO2 LBF 
  LBS -   
    SO2 Instruction Format - 
      HELP SO2 LBS 
  LBS - 
      HELP SO2 LBS 
  LBT -   
    SO2 Instruction Format - 
      HELP SO2 LBT 
  LBT - 
      HELP SO2 LBT 
  LDB -   
    DO2 Instruction Format - 
      HELP DO2 LDB 
  LDB - 
      HELP DO2 LDB 
  LDH -   
    DO1 Instruction Format - 
      HELP DO1 LDH 
  LDH - 
      HELP DO1 LDH 
  LDI -   
    SO3 Instruction Format - 
      HELP SO3 LDI 
  LDI - 
      HELP SO3 LDI 
  LDR -   
    DO1 Instruction Format - 
      HELP DO1 LDR 
  LDR - 
      HELP DO1 LDR 
  LDT -   
    GE2 Instruction Format - 
      HELP GE2 LDT 
  LDT - 
      HELP GE2 LDT 
  LDV -   
    SI1 Instruction Format - 
      HELP SI1 LDV 
  LDV - 
      HELP SI1 LDV 
  LEV -   
    SO1 Instruction Format - 
      HELP SO1 LEV 
  LEV - 
      HELP SO1 LEV 
  LIST Pseudo Operation - 
      HELP LIST 
  LISTINC Pseudo Operation - 
      HELP LISTINC 
  LLH -   
    DO1 Instruction Format - 
      HELP DO1 LLH 
  LLH - 
      HELP DO1 LLH 
  LNJ -   
    DO4 Instruction Format - 
      HELP DO4 LNJ 
  LNJ - 
      HELP DO4 LNJ 
  LRDB -   
    GE1 Instruction Format - 
      HELP GE1 LRDB 
  LRDB - 
      HELP GE1 LRDB 
  LS option - 
      HELP INVOCATION LS 
  LU option - 
      HELP INVOCATION LU 
M 
  MAT -   
    CB1 Instruction Format - 
      HELP CB1 MAT 
  MAT - 
      HELP CB1 MAT 
  MCL -   
    GE1 Instruction Format - 
      HELP GE1 MCL 
  MCL - 
      HELP GE1 MCL 
  MLV -   
    SI1 Instruction Format - 
      HELP SI1 MLV 
  MLV - 
      HELP SI1 MLV 
  MMM -   
    GE1 Instruction Format - 
      HELP GE1 MMM 
  MMM - 
      HELP GE1 MMM 
  Mnemonic Codes - 
      HELP MNEMONICS 
  MTM -   
    DO5 Instruction Format - 
      HELP DO5 MTM 
  MTM - 
      HELP DO5 MTM 
  MUL -   
    DO3 Instruction Format - 
      HELP DO3 MUL 
  MUL - 
      HELP DO3 MUL 
N 
  NEG -   
    SO1 Instruction Format - 
      HELP SO1 NEG 
  NEG - 
      HELP SO1 NEG 
  NLS option - 
      HELP INVOCATION NLS 
  NOP -   
    BI Instruction Format - 
      HELP BI NOP 
  NOP - 
      HELP BI NOP 
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
    DO1 Instruction Format - 
      HELP DO1 OR 
  OR - 
      HELP DO1 OR 
  ORG Pseudo Operation - 
      HELP ORG 
  ORH -   
    DO1 Instruction Format - 
      HELP DO1 ORH 
  ORH - 
      HELP DO1 ORH 
  OU - 
      HELP INVOCATION OU 
  OUNAME Pseudo Operation - 
      HELP OUNAME 
Q 
  QOH -   
    GE1 Instruction Format - 
      HELP GE1 QOH 
  QOH - 
      HELP GE1 QOH 
  QOT -   
    GE1 Instruction Format - 
      HELP GE1 QOT 
  QOT - 
      HELP GE1 QOT 
R 
  RES Pseudo Operation - 
      HELP RES 
  RLQ -   
    GE2 Instruction Format - 
      HELP GE2 RLQ 
  RLQ - 
      HELP GE2 RLQ 
  RSC -   
    GE1 Instruction Format - 
      HELP GE1 RSC 
  RSC - 
      HELP GE1 RSC 
  RSTR -   
    SO5 Instruction Format - 
      HELP SO5 RSTR 
  RSTR - 
      HELP SO5 RSTR 
  RTCF -   
    GE1 Instruction Format - 
      HELP GE1 RTCF 
  RTCF - 
      HELP GE1 RTCF 
  RTCN -   
    GE1 Instruction Format - 
      HELP GE1 RTCN 
  RTCN - 
      HELP GE1 RTCN 
  RTT -   
    GE1 Instruction Format - 
      HELP GE1 RTT 
  RTT - 
      HELP GE1 RTT 
S 
  SAL -   
    SHS Instruction Format - 
      HELP SHS SAL 
  SAL - 
      HELP SHS SAL 
  SAR -   
    SHS Instruction Format - 
      HELP SHS SAR 
  SAR - 
      HELP SHS SAR 
  SAVE -   
    SO5 Instruction Format - 
      HELP SO5 SAVE 
  SAVE - 
      HELP SO5 SAVE 
  SCL -   
    SHS Instruction Format - 
      HELP SHS SCL 
  SCL - 
      HELP SHS SCL 
  SCR -   
    SHS Instruction Format - 
      HELP SHS SCR 
  SCR - 
      HELP SHS SCR 
  SDI -   
    SO3 Instruction Format - 
      HELP SO3 SDI 
  SDI - 
      HELP SO3 SDI 
  SECT Pseudo Operation - 
      HELP SECT 
  SHL CPU Instruction Format - 
      HELP SHL 
  SHS CPU Instruction Format - 
      HELP SHS 
  SI1 CPU Instruction Format - 
      HELP SI1 
  SID -   
    SO3 Instruction Format - 
      HELP SO3 SID 
  SID - 
      HELP SO3 SID 
  SO option - 
      HELP INVOCATION SO 
  SO1 CPU Instruction Format - 
      HELP SO1 
  SO2 CPU Instruction Format - 
      HELP SO2 
  SO3 CPU Instruction Format - 
      HELP SO3 
  SO4 CPU Instruction Format - 
      HELP SO4 
  SO5 CPU Instruction Format - 
      HELP SO5 
  SOL -   
    SHS Instruction Format - 
      HELP SHS SOL 
  SOL - 
      HELP SHS SOL 
  SOR -   
    SHS Instruction Format - 
      HELP SHS SOR 
  SOR - 
      HELP SHS SOR 
  SRCH -   
    CB1 Instruction Format - 
      HELP CB1 SRCH 
  SRCH - 
      HELP CB1 SRCH 
  SRCH (list) option - 
      HELP INVOCATION SRCH 
  SRDB -   
    GE1 Instruction Format - 
      HELP GE1 SRDB 
  SRDB - 
      HELP GE1 SRDB 
  SRM -   
    SRM Instruction Format - 
      HELP SRM SRM 
  SRM - 
      HELP SRM SRM 
  SRM CPU Instruction Format - 
      HELP SRM 
  Statement Format - 
      HELP STATEMENT 
  STB -   
    DO2 Instruction Format - 
      HELP DO2 STB 
  STB - 
      HELP DO2 STB 
  STH -   
    DO1 Instruction Format - 
      HELP DO1 STH 
  STH - 
      HELP DO1 STH 
  STM -   
    DO5 Instruction Format - 
      HELP DO5 STM 
  STM - 
      HELP DO5 STM 
  STR -   
    DO1 Instruction Format - 
      HELP DO1 STR 
  STR - 
      HELP DO1 STR 
  STS -   
    SO1 Instruction Format - 
      HELP SO1 STS 
  STS - 
      HELP SO1 STS 
  STT -   
    GE2 Instruction Format - 
      HELP GE2 STT 
  STT - 
      HELP GE2 STT 
  SUB -   
    DO1 Instruction Format - 
      HELP DO1 SUB 
  SUB - 
      HELP DO1 SUB 
  SWB -   
    DO2 Instruction Format - 
      HELP DO2 SWB 
  SWB - 
      HELP DO2 SWB 
  SWR -   
    DO1 Instruction Format - 
      HELP DO1 SWR 
  SWR - 
      HELP DO1 SWR 
  Symbols - 
      HELP SYMBOLS 
  SYMDEF/ENTDEF Pseudo Operations - 
      HELP SYMDEF_ENTDEF 
  SYMREF/ENTREF Pseudo Operations - 
      HELP SYMREF_ENTREF 
T 
  TITLE Pseudo Operation - 
      HELP TITLE 
U 
  UI option - 
      HELP INVOCATION UI 
V 
  VLD -   
    GE1 Instruction Format - 
      HELP GE1 VLD 
  VLD - 
      HELP GE1 VLD 
  VRF -   
    CB1 Instruction Format - 
      HELP CB1 VRF 
  VRF - 
      HELP CB1 VRF 
W 
  WDTF -   
    GE1 Instruction Format - 
      HELP GE1 WDTF 
  WDTF - 
      HELP GE1 WDTF 
  WDTN -   
    GE1 Instruction Format - 
      HELP GE1 WDTN 
  WDTN - 
      HELP GE1 WDTN 
X 
  XOH -   
    DO1 Instruction Format - 
      HELP DO1 XOH 
  XOH - 
      HELP DO1 XOH 
  XOR -   
    DO1 Instruction Format - 
      HELP DO1 XOR 
  XOR - 
      HELP DO1 XOR 
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
00001
HELP_INDEX
Format: 
INCLUDE  include_file_fid[,LIST] 
Parameters: 
include_file_fid    identifies a file in combination with the contents of the 
SRCH option in the standard CP-6 way. 
LIST    requests that the contents of the included file be listed. 
Description: 
The INCLUDE pseudo operation directs the assembler to include source text from 
the referenced file. 
00002
00001

CALF is invoked according to the standard CP-6 processor invocation syntax: 
!CALF [sifid][,uifid] [{ON|OVER|INTO} [oufid][,lsfid]] [(options)] 
The default options are LS, NLU, NSO, and NVI.  Available options are:  LS LU 
NLS NOU NSO NUI OPTUI OU SO   SRCH UI 
These can be accessed by typing HELP INVOCATION option. For example HELP 
INVOCATION SRCH.  Descriptions are in a tabular format with two columns like 
so: 
  Option     Explanation 
  LS 
             List source program.  The default is LS. 
  LU 
             List the update file before listing the source.  The default is 
             NLU. 
  NLS 
             Do not list source program. 
  NLV 
             Do not list the update file.  This is the default. 
  NOU 
             Do not generate object unit. 
  NSO 
             Do not produce updated source.  This is the default. 
  NUI 
             Do not use update input.  This is the default. 
  OPTUI 
             Use Update Input, if it exists.  If not, proceed without erroring 
             the compiler. 
  OU 
             Generate object unit.  The default is OU. 
  SO 
             Produce updated source.  The default is NSO. 
  SR[CH] (list) 
             This option augments the specification of the accounts and 
             packsets to be searched if the CALF processor encounters an 
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
Format: 
[label]  mnemonic (data_AS),(channel_AS) 
Parameters: 
data_AS    may be any address syllable.  Immediate Register references must be 
to an R register. 
channel_AS    may be an address syllable.  Immediate Register references must 
be to an R register.  If an Immediate Operand is specified and if it can be 
determined in the first pass that its first six bits are non-zero, then the 
channel-function word is placed directly in the instruction. 
mnemonic    specifies one of the following mnemonics: 
    IO      IOH 
To obtain HELP messages for the mnemonics enter HELP IO1 mnemonic. 
For example, HELP IO1 IOH. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  IO 
               Input/output (word) 
  IOH 
               Input/output half-word 
Description: 
The two instructions in this group are IO format. 
00004
00002
00003
00001
Format: 
[label]  mnemonic (buffer_AS),(channel_AS),(range_AS) 
Parameters: 
buffer_AS    must specify a memory address. 
channel_AS    any address syllable.  Immediate References must be to an R 
register. 
range_AS    any address syllable.  Immediate References must be to an R 
register.  If the channel_AS specifies an Immediate Operand and it can be 
determined in the first pass that its first six bits are non-zero, then the 
channel-function word is placed directly in the instruction.  The function 
portion of the channel-function word must have a value of 9. 
mnemonic    specifies one of the following mnemonics: 
    IOLD 
To obtain HELP messages for the mnemonics enter HELP IO2 mnemonic.  For 
example, HELP IO2 IOLD Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  IOLD 
               Input/output load 
Description: 
This instruction is in IO format.  Immediate Register and Immediate Operand 
addressing are not legal. 
00003
00002
00001
    The following rules pertain to the label field: 
1.  When the label field is present it must begin in the first character of 
    the first record of a statement.  When there is no label field, at least 
    the first character of the first record of a statement must be blank. 
2.  A label field may only be a legal CALF symbol. 
Format: 
LIST [listoptions] 
Parameters: 
listoptions    contain from zero to three of the following: 
    ON    turn the listing on 
    OFF    turn the listing off 
    PUSH    push the current listing state ( on | off ) onto a stack 
    PULL    pull the current listing state ( on | off ) onto a stack 
    INVIS    make this pseudo op invisible 
Note that ON and OFF are mutually exclusive, as are PUSH and PULL, and only 
one of each may be specified on each use of LIST.  The initial setting is LIST 
ON.  If no options are specified then LIST ON is assumed. 
Description: 
The LIST pseudo option controls the listing of the base and update input. 
00002
00001
Format: 
LISTINC listoptions 
Parameters: 
listoptions    the same as for the LIST pseudo option. 
Description: 
The LISTINC pseudo option controls the listing of include files.  The initial 
setting is LISTINC OFF.  If no options are specified, then LISTINC ON is 
assumed. 
00002
00001
MNEMONICS
The following portions of this HELP message contain the Mnemonic Codes, their 
instruction and the HELP that will provide the Instruction Format.  This 
information can be accessed by either typing a ? or ?? after this message, or 
by typing: 
    HELP MNEMONICS mnemonic 
    Example: HELP MNEMONIC ADD 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  ACM 
               Alphanumeric compare - See HELP CB1 
  ACQ 
               Acquire stack space - See HELP GE2 
  ADD 
               Add to R register - See HELP DO1 
  ADV 
               Add value to R register - See HELP SI1 
  AID 
               Add double-word integer - See HELP SO3 
  ALR 
               Alphanumeric Move - See HELP CB1 
  AME 
               Alphanumeric move and edit - See HELP CB1 
  AND 
               AND with R register - See HELP DO1 
  ANH 
               AND half-word (byte) with R register - See HELP DO1 
  ASD 
               Activate segment descriptor - See HELP GE1 ASD 
  B 
               Branch unconditionally - See HELP BI 
  BAG 
               Branch if algebraically greater than - See HELP BI 
  BAGE 
               Branch if algebraically greater than or equal to - See HELP BI 
  BAL 
               Branch if algebraically less than - See HELP BI 
  BALE 
               Branch if algebraically less than or equal to - See HELP BI 
  BBF 
               Branch if bit-test indicator false - See HELP BI 
  BBT 
               Branch if bit-test indicator true - See HELP BI 
  BCF 
               Branch if carry false - See HELP BI 
  BCT 
               Branch if carry true - See HELP BI 
  BDEC 
               Branch and decrement - See HELP BR 
  BE 
               Branch if equal - See HELP BI 
  BEVN 
               Branch if R register even - See HELP BR 
  BEZ 
               Branch if R register equal to zero - See HELP BR 
  BG 
               Branch if greater than - See HELP BI 
  BGE 
               Branch if greater than or equal to - See HELP BI 
  BGEZ 
               Branch if R register greater than or equal to zero - See HELP 
               BR 
  BGZ 
               Branch if R register greater than 0 - See HELP BR 
  BINC 
               Branch and increment - See HELP BR 
  BIOF 
               Branch if I/O indicator false - See HELP BI 
  BIOT 
               Branch if I/O indicator true - See HELP BI 
  BL 
               Branch if less than - See HELP BI 
  BLE 
               Branch if less than or equal to - See HELP BI 
  BLEZ 
               Branch if R register less than or equal to zero - See HELP BR 
  BLZ 
               Branch if R register less than zero - See HELP BR 
  BNE 
               Branch if not equal - See HELP BI 
  BNEZ 
               Branch if R register not equal to zero - See HELP BR 
  BNOV 
               Branch if no overflow - See HELP BI 
  BODD 
               Branch if R register odd - See HELP BR 
  BOV 
               Branch if overflow - See HELP BI 
  BRK 
               Breakpoint trap - See HELP GE1 
  BSE 
               Branch if signs equal - See HELP BI 
  BSU 
               Branch if signs unlike - See HELP BI 
  CAD 
               Add carry bit - See HELP SO1 
  CBD 
               Convert binary to decimal - See HELP CB2 
  CBE 
               Branch if equal - See HELP BI 
  CBG 
               Branch if greater - See HELP BI 
  CBGE 
               Branch if greater than or equal - See HELP BI 
  CBL 
               Branch if less - See HELP BI 
  CBLE 
               Branch if less than or equal - See HELP BI 
  CBNE 
               Branch if not equal - See HELP BI 
  CBNOV 
               Branch on no overflow - See HELP BI 
  CBNSF 
               Branch on no sign fault - See HELP BI 
  CBNTR 
               Branch on no truncation - See HELP BI 
  CBOV 
               Branch on overflow - See HELP BI 
  CBSF 
               Branch on sign fault - See HELP BI 
  CBTR 
               Branch on truncation - See HELP BI 
  CDB 
               Convert decimal to binary - See HELP CB2 
  CL 
               Clear - See HELP SO1 
  CLH 
               Clear half-word - See HELP SO1 
  CMB 
               Compare to B register - See HELP DO2 
  CMH 
               Compare half-word (byte) to R register - See HELP DO1 
  CMN 
               Compare address to null - See HELP SO1 
  CMR 
               Compare to R register - See HELP DO1 
  CMV 
               Compare value to R register - See HELP DO1 
  CMZ 
               Compare to zero - See HELP SO1 
  CNFG 
               Configure - See HELP GE1 
  CPL 
               Complement - See HELP SO1 
  CSNCB 
               Synchronize and Branch - See HELP BI 
  CSYNC 
               Synchronize - See HELP BI 
  DAD 
               Decimal add - See HELP CB3 
  DAL 
               Double-shift arithmetic-left - See HELP SHL 
  DAR 
               Double-shift arithmetic-right - See HELP SHL 
  DCL 
               Double-shift closed-left - See HELP SHL 
  DCM 
               Decimal compare - See HELP CB3 
  DDV 
               Decimal divide - See HELP CB3 
  DCR 
               Double-shift closed-right - See HELP SHL 
  DEC 
               Decrement - See HELP SO1 
  DIV 
               Divide R register - See HELP DO3 
  DMC 
               Decimal move and convert - See HELP CB3 
  DME 
               Decimal move and edit - See HELP CB2 
  DML 
               Decimal multiply - See HELP CB3 
  DOL 
               Double-shift open-left - See HELP SHL 
  DOR 
               Double-shift open-right - See HELP SHL 
  DQA 
               Dequeue on address - See HELP GE1 
  DQH 
               Dequeue from head - See HELP GE1 
  DSB 
               Decimal subtract - See HELP CB3 
  DSH 
               Decimal shift - See HELP CB4 
  ENT 
               Enter - See HELP SO4 
  HLT 
               Halt - See HELP GE1 
  INC 
               Increment - See HELP SO1 
  IO 
               Input/output (word) - See HELP IO1 
  IOH 
               Input/output half-word - See HELP IO1 
  IOLD 
               Input/output load - See HELP IO2 
  JMP 
               Jump - See HELP SO4 
  LAB 
               Load effective address into B register - See HELP DO4 
  LB 
               Load bit - See HELP SO2 
  LBC 
               Load bit and complement - See HELP SO2 
  LBF 
               Load bit and set false - See HELP SO2 
  LBS 
               Load bit and swap - See HELP SO2 
  LBT 
               Load bit and set true - See HELP SO2 
  LDB 
               Load B register - See HELP DO2 
  LDH 
               Load half-word (byte) into R register - See HELP DO1 
  LDI 
               Load double-word integer - See HELP SO3 
  LDR 
               Load R register - See HELP DO1 
  LDT 
               Load stack address register - See HELP GE2 
  LDV 
               Load value into R register - See HELP SI1 
  LEV 
               Level change - See HELP SO1 
  LLH 
               Load logical half-word (byte) into R register - See HELP DO1 
  LNJ 
               Load B register and jump (link jump) - See HELP DO4 
  LRDB 
               Load remote descriptor base - See HELP GE1 
  MAT 
               Alphanumeric move and translate - See HELP CB1 
  MCL 
               Monitor call - See HELP GE1 
  MLV 
               Multiply R register by value - See HELP SI1 
  MMM 
               Memory to memory move - See HELP GE1 
  MTM 
               Modify/test M register - See HELP DO5 
  MUL 
               Multiply R register - See HELP DO3 
  NEG 
               Negate - See HELP SO1 
  NOP 
               No operation - See HELP BI 
  OR 
               Inclusive OR with R register - See HELP DO1 
  ORH 
               Inclusive OR or half-word (byte) - See HELP DO1 
  QOH 
               Queue on head - See HELP GE1 
  QOT 
               Queue on tail - See HELP GE1 
  RLQ 
               Relinquish stack space - See HELP GE2 
  RSC 
               Rescan configuration - See HELP GE1 
  RSTR 
               Restore context - See HELP SO5 
  RTCF 
               Real-time clock off - See HELP GE1 
  RTCN 
               Real-time clock on - See HELP GE1 
  RTT 
               Return from trap - See HELP GE1 
  SAL 
               Single-shift arithmetic-left - See HELP SHS 
  SAR 
               Single-shift arithmetic-right - See HELP SHS 
  SAVE 
               Save context - See HELP SO5 
  SCL 
               Single-shift closed-left - See HELP SHS 
  SCR 
               Single-shift closed-right - See HELP SHS 
  SDI 
               Store double-word integer - See HELP SO3 
  SOL 
               Single-shift open-left - See HELP SHS 
  SOR 
               Single-shift open-right - See HELP SHS 
  SID 
               Subtract double-word integer - See HELP SO3 
  SRCH 
               Alphanumeric search - See HELP CB1 
  SRDB 
               Store remote descriptor base - See HELP GE1 
  SRM 
               Store register masked - See HELP SRM 
  STB 
               Store B register - See HELP DO1 
  STH 
               Store R register half-word (byte) - See HELP DO1 
  STM 
               Store M register - See HELP DO5 
  STR 
               Store R register - See HELP DO1 
  STS 
               Store S register - See HELP SO1 
  STT 
               Store stack register - See HELP GE2 
  SUB 
               Subtract from R register - See HELP DO1 
  SWB 
               Swap B register - See HELP DO2 
  SWR 
               Swap R register - See HELP DO1 
  VLD 
               Validate address, range and access rights - See HELP GE1 
  VRF 
               Alphanumeric verify - See HELP CB1 
  WDTF 
               Watchdog timer off - See HELP GE1 
  WDTN 
               Watchdog timer on - See HELP GE1 
  XOH 
               Half-word (byte) exclusive OR with R register - See HELP DO1 
  XOR 
               Exclusive OR with R register - See HELP DO1 
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
00070
00071
00072
00073
00074
00076
00075
00077
00078
00079
00080
00081
00082
00083
00084
00085
00086
00087
00088
00089
00090
00091
00092
00093
00094
00095
00096
00097
00098
00099
00100
00101
00102
00103
00104
00105
00106
00107
00108
00109
00110
00111
00112
00113
00114
00115
00116
00117
00118
00119
00120
00121
00122
00123
00124
00125
00126
00127
00128
00129
00130
00131
00132
00133
00134
00137
00135
00136
00138
00139
00140
00141
00142
00143
00144
00145
00146
00147
00148
00149
00150
00151
00152
00153
00154
00155
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
[label]  ORG  [new_location] 
Parameters: 
label    is the address of the new location. 
new_location    is an internal or external value expression without any 
forward references.  If it is an internal value expression, then the 
external-id portion of the location counter is unchanged and the new_location 
value becomes the new word offset.  If it is an external value expression, 
then both the external-id and offset portion change.  In this case external-id 
must identify a section, not a SYMREF or ENTREF symbol.  If new_location is 
not supplied, then the offset portion of the location counter is set to the 
size of the current section, that is, to the next unused byte of the section. 
Description: 
The ORG pseudo operation changes the value of the location counter.  All the 
parts of the ORG pseudo operation are optional. 
00002
00001
Format: 
OUNAME  object_unit_name 
Parameters: 
object_unit_name    is the symbol which will be defined as the object unit 
name. 
Description: 
The OUNAME pseudo operation defines the name of the object unit.  It may 
appear only once in the assembly and it may be placed anywhere. 
00002
00001
Format: 
[label] RES[,unit_size]  [number_of_units] 
Parameters: 
label    is the address of the next available byte in the current section. 
This will be the first byte reserved by RES. 
unit_size    is an internal value expression without any forward references. 
It determines the unit size in bytes of the storage units reserved by the 
pseudo operation.  If unit-size is not supplied, then a unit size of 2 bytes 
(1 word) is assumed. 
number_of_units    is an internal value expression without any forward 
references.  It determines the number of storage units (of size unit_size) 
that are reserved.  If number_of_units is not supplied, then 1 storage unit is 
reserved. 
Description: 
The RES pseudo operation reserves a number of bytes of memory.  No 
initializing value is provided. 
Example: 
             RES 
    Reserve 2 bytes of memory. 
             RES,4 
             RES       2 
    Each statement reserves 4 bytes of memory. 
             RES,4     11 
    Reserve 44 bytes of memory. 
00002
00003
00001
Format: 
[label]  SECT  [section_type][,init_type] 
Parameters: 
label    specifies the name of the section being defined.  If label is not 
supplied, then the programmer is specifying a section with a blank name. 
section_type    specifies the type of the section being defined.  Section_type 
identifiers are: 
    PROC     (the default) 
    DATA 
    CONSTANT 
    EXT 
    DCB 
init_type    specifies the default initialization to be applied to portions of 
the section which are not explicitly initialized.  Initialization type 
identifiers are: 
    UTS     (the default) 
    ZERO 
A SECT pseudo operation should precede any operations which generate object 
program text.  If this is not so, a " SECT PROC " statement is simulated. 
Description: 
The SECT pseudo operation defines a new section.  All the parts of the SECT 
pseudo operation are optional. 
00002
00001
Format: 
[label]  mnemonic,DR_reg  {shift_count|R1} 
Parameters: 
DR_reg    a register value representing R3, R5, R7, DR23, DR45 or DR67. 
shift_count    an internal value expression with legal values from 0 through 
31, except for DCL and DCR, whose legal values are 0 through 15. 
R1    Front-end hardware arithmetic (R) register. 
mnemonic    specifies one of the following mnemonics: 
    DAL     DAR     DCL *   DCR *   DOL 
    DOR 
*   The legal range of shift_count is 0 through 15. 
To obtain HELP messages for the mnemonics enter HELP SHL mnemonic.  For 
example, HELP SHL DAR.  Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  DAL 
               Double-shift arithmetic-left 
  DAR 
               Double-shift arithmetic-right 
  DCL 
               Double-shift closed-left 
  DCR 
               Double-shift closed-right 
  DOL 
               Double-shift open-left 
  DOR 
               Double-shift open-right 
Description: 
All instructions in this group are Shift Long format. 
00002
00003
00004
00005
00008
00006
00007
00001
Format: 
[label]  mnemonic,R_reg  {shift_count|R1} 
Parameters: 
R_reg    Front-end hardware arithmetic (R) registers. 
shift_count    an internal value expression with legal values from 0 through 
15. 
R1    Front-end hardware arithmetic (R) register. 
mnemonic    specifies one of the following mnemonics: 
    SAL     SAR     SCL     SCR     SOL 
    SOR 
To obtain HELP messages for the mnemonics enter HELP SHS mnemonic. 
For example, HELP SHS SCL. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  SAL 
               Single-shift arithmetic-left 
  SAR 
               Single-shift arithmetic-right 
  SCL 
               Single-shift closed-left 
  SCR 
               Single-shift closed-right 
  SOL 
               Single-shift open-left 
  SOR 
               Single-shift open-right 
Description: 
All instructions in this group are Shift Short format. 
00008
00001
00002
00003
00004
00005
00006
00007
Format: 
[label]  mnemonic,{R_reg|DR67}  [=]immediate_value 
Parameters: 
R_reg    Front-end hardware arithmetic (R) registers. 
DR67    paired Front-end hardware R registers. 
immediate_value    an expression. 
mnemonic    specifies one of the following mnemonics: 
    ADV     CMV     LDV     MLV * 
*   MLV may have a DR67 value in the CF[2] position.  It has special 
    significance for this instruction. 
To obtain HELP messages for the mnemonics enter HELP SI1 mnemonic.  For 
example, HELP SI1 LDV.  Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  ADV 
               Add value to R register 
  CMV 
               Compare value to R register 
  LDV 
               Load value into R register 
  MLV * 
               Multiply R_register by value 
*   MLV may have a DR67 value in the CF[2] position.  It has special 
    significance for this instruction. 
Description: 
All instructions in this group are Short Value Immediate (SVI) format. 
00002
00003
00006
00004
00005
00001
Format: 
[label]  mnemonic  AS 
Parameters: 
AS    any address syllable is legal. 
mnemonic    specifies one of the following mnemonics: 
    CAD x   CL x    CLH x   CMN     CMZ 
    CPL x   DEC x   INC x   LEV     NEG x 
    STS x 
x   Stores into the operand specified by the address syllable. 
To obtain HELP messages for the mnemonics enter HELP SO1 mnemonic.  For 
example, HELP SO1 CPL.  Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  CAD x 
               Add carry bit 
  CL x 
               Clear 
  CLH x 
               Clear half-word 
  CMN 
               Compare address to null 
  CMZ 
               Compare to zero 
  CPL x 
               Complement 
  DEC x 
               Decrement 
  INC x 
               Increment 
  LEV 
               Level change 
  NEG x 
               Negate 
  STS x 
               Store S register 
x   Stores into the operand specified by the address syllable. 
Description: 
All instructions in this group are Single Operand (SO) format.  Immediate 
register references must be to R registers except for the CMN instruction for 
which Immediate Register references must be to B_registers. 
00002
00003
00004
00005
00006
00007
00008
00013
00009
00010
00011
00001
00012
Format: 
[label]  mnemonic,{bit-mask|R1} {not_indexed_AS|indexed_AS} 
Parameters: 
bit_mask    bit positions in the word at the effective address that 
corresponds to 1 bits in the mask are tested. 
R1    Front-end hardware arithmetic (R) register. 
not_indexed_AS    an address syllable that does not involve an index register. 
This includes Immediate Register(in this case R register) addressing. 
indexed_AS    an address syllable which must involve indexing.  In this case, 
an Immediate Register is impossible.  All instructions, except LB, store into 
their operand. 
mnemonic    specifies one of the following mnemonics: 
    LB      LBC     LBF     LBS     LBT 
To obtain HELP messages for the mnemonics enter HELP SO2 mnemonic. 
For example, HELP SO2 LBF. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  LB 
               Load bit 
  LBC 
               Load bit and complement 
  LBF 
               Load bit and set false 
  LBS 
               Load bit and swap 
  LBT 
               Load bit and set true 
Description: 
All the instructions in this group are Single Operand (SO) format.  They 
manipulate one or more bits in a word. 
Rules: 
1.  Bit-mask or R1 is permitted only if AS is not indexed. 
00007
00002
00003
00004
00005
00006
00001
00008
Format: 
[label]  mnemonic AS 
Parameters: 
mnemonic    specifies one of the following mnemonics: 
AS    any address syllable is legal. 
    AID     LDI     SDI     SID 
To obtain HELP messages for the mnemonics enter HELP SO3 mnemonic. 
For example, HELP SO3 SDI. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  AID 
               Add double-word integer 
  LDI 
               Load double-word integer 
  SDI 
               Store double-word integer 
  SID 
               Subtract double-word integer 
Description: 
All the instructions in this group are Single Operand (SO) format.  They 
manipulate 2-word operands.  Immediate Register references must be to a double 
register value:  R3, R5, R7, DR23, DR45, or DR67.  Only the SDI (Store Double 
Integer) instruction stores into its operand. 
00002
00006
00003
00001
00004
00005
Format: 
[label]  mnemonic  mem_ref_AS 
Parameters: 
mem_ref_AS    an address syllable that may not be in either Immediate Register 
or Immediate Operand form. 
mnemonic    specifies one of the following mnemonics: 
    ENT     JMP 
To obtain HELP messages for the mnemonics enter HELP SO4 mnemonic. 
For example, HELP SO4 JMP. 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  ENT 
               Enter 
  JMP 
               Jump 
Description: 
The two instructions in this group are Single Operand (SO) format.  They cause 
a transfer of control to the address specified by the operand. 
00004
00002
00003
00001
Format: 
[label]  mnemonic,{save_mask|rstr_mask}  mem_ref_AS 
Parameters: 
save_mask|rstr_mask    is a 1-word mask directing which registers are to be 
saved or restored. 
mem_ref_AS    may be one of the following forms: Immediate Memory Address, 
B-relative Address, Program-relative address, or $IV-relative address. 
mnemonic    specifies one of the following mnemonics: 
    RSTR    SAVE 
To obtain HELP messages for the mnemonics enter HELP SO5 mnemonic. 
For example, HELP SO5 SAVE 
Descriptions are in a tabular format with two columns like so: 
  Mnemonic     Instruction 
  RSTR 
               Restore context 
  SAVE 
               Save context 
Description: 
The two instructions in this group are Single Operand (SO) format. 
00004
00001
00002
00003
Format: 
[label] mnemonic,R_reg,mask AS 
Parameters: 
R_reg    Front-end hardware arithmetic (R) registers. 
mask    a 16-bit value.  Every bit (zero or one) in the register with a 
corresponding mask bit of one is stored; those corresponding to zero bits in 
the mask are not transferred and the original bits in the effective address 
remain unchanged. 
AS    any address syllable is legal. 
mnemonic    specifies one of the following mnemonics: 
    SRM 
To obtain HELP messages for the mnemonics enter HELP SRM mnemonic.  For 
example, HELP SRM SRM.  Descriptions are in a tabular format with two columns 
like so: 
  Mnemonic     Instruction 
  SRM 
               Store register masked 
Description: 
All instructions in this group are Double Operand (DO) format.  Immediate 
Register references must be to R registers. 
00003
00001
00002
The CALF statement format and general rules pertaining to its usage appear 
below. 
Format: 
label   command   argument 
Rules: 
1.  Each statement must begin on a new record. 
2.  Each statement must follow the statement format exactly.  Statements are 
    terminated by a blank or an end-of-record after the argument field.  All 
    characters after this point are considered comments. 
3.  The presence of a ";" in the record indicates that the statement will be 
    continued on the next record.  All characters after the ";" are considered 
    comments. 
4.  A statement may be continued on as many records as necessary.  At least 
    the first character of each continuation record must be blank.  Processing 
    of each continuation record begins with the first non-blank character. 
00001
00002
ASSEMBLER_SYMBOLS
Format: 
A CALF symbol is any legal PL-6 symbol. 
Rules: 
Symbols in CALF may be associated with the following kinds of values: 
o   internal values    A real value that can be determined at assembly time. 
o   external values    A value that cannot be calculated by the assembler at 
    assembly time. 
o   register values    A register.  See Table 3-1 for a list of the predefined 
    assembler symbols and their corresponding registers. 
o   names of sections     These names are used in assembler operations to 
    determine how most relocatable symbols are defined. 
o   assembler special values     These special symbols are predefined symbols 
    of the assembler that are associated with internal or relocatable values. 
In general all symbols must be unique.  However, the exception is that the 
names of sections must only be unique with respect to sections of the same 
type.  It is legal to have a code section, a data section, and a regular 
relocatable symbol all with the same name. 
00001
SYMDEF_ENTDEF
Format: 
SYMDEF  AF_list 
ENTDEF  AF_list 
Parameters: 
AF_list    is any legal symbol. 
Description: 
The SYMDEF and ENTDEF pseudo operations are used to designate symbols which 
are to be externally defined.  This makes the symbols visible to separately 
compiled or assembled object units.  Two distinct tables are maintained.  By 
convention SYMDEFs designate external data definitions and ENTDEFs designate 
external procedure definitions. 
Each AF[i] is a symbol which must be assigned an internal or locally external 
value somewhere in the assembly.  "Locally" external means that the DEFed 
symbol can not be defined in terms of other REFed symbols. 
If the OUNAME pseudo operation is not present in the assembly, then the first 
symbol which is ENTDEFed in the assembly is used as the name of the object 
unit produced by the assembly and designated as the primary entry point of the 
object unit. 
A symbol may be both ENTDEFed and SYMDEFed.  It may also be ENTDEFed or 
SYMDEFed twice without error.  Such subsequent DEFs have no effect. 
00002
00001
SYMREF_ENTREF
Format: 
SYMREF  AF_list 
ENTREF  AF_list 
Parameters: 
AF_list    is symbol or (symbol,OPTIONAL) 
Description: 
The SYMREF and ENTREF pseudo operations are used to designate symbols which 
are to be externally referenced.  This allows the programmer to see data and 
procedure which were defined in other object units.  Two distinct tables are 
maintained. 
Rules: 
1.  SYMREFed symbols may be defined only by SYMDEFed symbols, etc. 
2.  Each symbol may not be defined anywhere else in the assembly. 
3.  A symbol may not be both SYMREFed or ENTREFed, but it may be SYMREFed 
    twice or ENTREFed twice.  Such subsequent REFs have no effect. 
4.  The OPTIONAL word indicates that special action be taken by the linker 
    with respect to this symbol.  The linker will not attempt to include any 
    further object units from libraries to resolve this reference and if this 
    means that it remains unresolved, then the linker will not consider this 
    an error. 
00002
00001
00003
Format: 
TITLE 'title'[,INVIS] 
Parameters: 
'title'    specifies a character string in quotes. 
INVIS    causes the pseudo option not to appear in the listing. 
Description: 
The TITLE pseudo option causes a title to be printed on the first line of each 
page of the listing. If a TITLE is the first statement in the assembly, then 
it actually appears as the title starting on the first page, otherwise a page 
is ejected and the title appears starting on that page. 
00002
00001
