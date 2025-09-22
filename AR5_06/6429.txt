The PL6 compiler-invocation command is: 
!PL6 [sourcefid][,updatefid] [{ON|OVER|INTO} [oufid][,lsfid] 
    [(optionlist)] 
Note that the language processor for the PL-6 language is called PL6, with no 
embedded dash or other punctuation. 
For more HELP see: 
HELP (PL6) TOPICS           for a complete list of available topics. 
HELP (PL6) OPTIONS          for a complete list of available 
                            options. 
HELP (PL6) STATEMENTS       for a list of PL6 statements. 
HELP (PL6) ATTRIBUTES       for a list of PL6 attributes. 
HELP (PL6) BUILT_IN         for a list of PL6 built-in functions 
HELP (PL6) PREPROCESSOR     for a list of PL6 preprocessor directives. 
?                           displays the next level of HELP message. 
??                          displays all levels of the current HELP message. 
                            and subroutines. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
Description: 
The ADDR built-in function returns a pointer value which identifies the 
storage location of a given variable. 
Format: 
ADDR (ref) 
Parameters: 
ref    a location reference, NIL or ERASE. 
Rules: 
1.  ref must always be a reference with which a storage location is 
    associated.  It may be pointer-qualified, structure-qualified, or 
    subscripted. 
2.  In general, ref may be of any storage class.  However, it may not be a 
    non-pointer-qualified reference of storage class BASED or DCB. 
    Furthermore, if the ADDR function appears as the initial value of the INIT 
    attribute, then ref may only be of storage type SYMREF, SYMDEF, EXT, 
    EXTROOT, AREAREF, AREADEF, STATIC, or CONSTANT. 
3.  ref may be of any data type except ENTRY. 
4.  ADDR(NIL) and ADDR(ERASE) return the null pointer value. 
5.  ADDR may not be used on VECTOR qualified items. 
00001
00002
ALIGNMENT
Description: 
Alignment attributes are used to specify the way a variable is allocated in 
storage.  The alignment attributes are UNAL, CALIGNED, HALIGNED, ALIGNED, 
WALIGNED, and DALIGNED. 
Format: 
                    [ALIGNED ] 
                    [UNAL    ] 
DCL id a1[, a2] ... [CALIGNED]; 
                    [HALIGNED] 
                    [WALIGNED] 
                    [DALIGNED] 
Parameters: 
id    any valid identifier. 
a1,a2    any valid attributes. 
UNAL    Storage begins immediately following the storage for the previous 
variable except for CHAR data where UNAL is equivalent to CALIGNED.  No extra 
storage is used to contain the variable. 
CALIGNED    Storage is forced to begin and end on a character boundary. 
HALIGNED    Storage is forced to begin and end on a halfword boundary. 
ALIGNED    Storage is allocated in a way that facilitates access; that is, 
extra storage is used (where necessary) to permit the use of fast hardware 
operations to fetch or store the value of the variable.  The storage begins 
and ends on a word boundary. 
WALIGNED    Storage is forced to begin and end on a word boundary.  Synonymous 
with ALIGNED. 
DALIGNED    Storage is forced to begin and end on a doubleword boundary. 
Rules: 
1.  If an alignment attribute is not specified in the DCL statement, a 
    variable takes its alignment from the following default rules: 
    Storage Type          Default 
    ------------          ------- 
    Scalar 
      arithmetic          WALIGNED 
      character string    CALIGNED 
      bit string          UNAL 
      pointer             WALIGNED 
      entry variable      WALIGNED 
    Aggregate 
      structure           (same as the greatest aligned element) 
      array               (same as its elements) 
2.  The default base alignment of the memory allocated to a storage class is 
    defined as follows: 
                                          Variable 
    Storage Class       Default           Minimum 
    -------------       -------           ------- 
    STATIC              DALIGNED          WALIGNED 
    CONSTANT            DALIGNED          WALIGNED 
    AREAREF             WALIGNED          WALIGNED 
    EXT                 WALIGNED          WALIGNED 
    EXTROOT             WALIGNED          WALIGNED 
    DCB                 WALIGNED          WALIGNED 
    AUTO                DALIGNED          WALIGNED 
    PARAM               UNAL              UNAL 
    BASED               UNAL              UNAL 
    SYMREF              WALIGNED          WALIGNED 
    What this means is that the compiler will allocate all static variables in 
    a compile unit with a starting base of DALIGNED.  Within that base, a 
    single variable will be at a minimum WALIGNED and if DALIGNED is specified 
    will start on a double word boundary.  Even though a variable is described 
    as WALIGNED, if the base of the variable is known to be DALIGNED and the 
    variable's starting offset in the base is an even number, the variable 
    will be treated as if it had DALIGNED specified. 
3.  The storage for every level 1 variable will start on a word boundary as a 
    minimum.  Since the BASED and parameter storage classes only represent 
    templates, the start of the variable will be based totally on the explicit 
    or implicit alignment.  Generally, the greater the alignment resolution 
    is, the more efficient the generated code is. 
Example: 
    DCL X BIT (1) ALIGNED; 
    DCL X BIT (1) UNAL; 
    DCL X BIT (1) DALIGNED; 
00003
00001
00002
Description: 
The ALTRET attribute applies to the declaration of an entry name of a 
procedure.  It permits the procedure to be CALLed, via the specified entry 
name, by a CALL statement which specifies the ALTRET, WHENRETURN or 
WHENALTRETURN option. 
Format: 
DCL id ENTRY ALTRET; 
Rules: 
1.  The procedure invoked by the specified entry name must have the ALTRET 
    attribute specified on its PROC statement. 
2.  Use of the ALTRET attribute in an entry name declaration permits, but does 
    not require, the specification of the ALTRET, WHENRETURN or WHENALTRETURN 
    option on a CALL statement to this entry name.  However, if the ALTRET, 
    WHENRETURN or WHENALTRETURN are not specified at all, processing will 
    continue as if a normal return had been received. 
Cross Reference: 
See the CALL, PROC and ENTRY statements. 
00002
00001
RETURN_ALTRETURN
Description: 
The AREADEF attribute modifies the STATIC or CONSTANT attribute to allow 
specification of data to reside within a user-controlled data segment.  In 
another PROC, the same variable may be referenced with the storage class 
attribute AREAREF. 
Format: 
DCL [1] id ... {STATIC  } AREADEF [(DSn)]; 
               {CONSTANT} 
Rules: 
1.  The specification of AREADEF informs the linker that the variable is to be 
    allocated in one of the six user-controlled data segments.  For additional 
    information, see the CP-6 Monitor Services Reference manual concerning 
    memory management. 
2.  The optional DSn field allows the specification of the data segment to 
    which the variable is to be allocated.  The names that the linker 
    recognizes are: 
        DS3SID    DS6SID 
        DS4SID    DS7SID 
        DS5SID    DS8SID 
    The compiler does not verify the validity of DSn other than to ensure that 
    it conforms to the rules of a PL-6 identifier. 
3.  If the optional DSn field is not specified, then the linker will default 
    to DS3SID. 
00001
Description: 
The AREAREF attribute specifies that an identifier refers to the same storage 
location as the same identifier declared with the AREADEF attribute in another 
procedure. 
Format: 
DCL [1] id AREAREF; 
Rules: 
1.  AREAREF is a storage class attribute and may appear in the declaration of 
    any scalar, array, or structure where no other storage class attribute 
    appears or is implied. 
2.  The INIT clause is not allowed on AREAREF variables. 
00001
Description: 
The ASCBIN built-in function allows the ASCII value of a single character to 
be used as an integer. 
Format: 
ASCBIN (charexp) 
Parameters: 
charexp    any character expression. 
Rules: 
1.  ASCBIN returns a UBIN WORD result. 
2.  The LENGTHC (charexp) must be equal to one. 
00001
00002
Description: 
The ASCBIN preprocessor function allows a single ASCII character to be used as 
an SBIN value. 
Format: 
ASCBIN (exp) 
Parameters: 
exp    is a character string expression which results in a single character. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = ASCBIN ('A'); 
    DCL A SBIN; 
    A = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = 65; 
    DCL A SBIN; 
            A = 65; 
    END DEMO; 
00002
00001
Description: 
The ASCBIT built-in function allows the ASCII value of a single character to 
be used as a bit string. 
Format: 
ASCBIT (charexp) 
Parameters: 
charexp    any character expression. 
Rules: 
1.  ASCBIT returns a bit string defined as BIT(9). 
2.  The LENGTHC (charexp) must be be equal to one. 
00001
00002
Description: 
The ASCBIT preprocessor function allows a single ASCII character to be used as 
a bit string. 
Format: 
ASCBIT (exp) 
Parameters: 
exp    is a character string expression which evaluates to a single character. 
Rules: 
1.  The bit string returned by the function is of length n, where n is the 
    number of bits required to represent an ASCII character on the target 
    machine. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = ASCBIT ('A'); /* Note octal representation in listing.*/ 
    DCL ASCOMYCETE BIT (36); 
    ASCOMYCETE = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT  = '101'O; 
        /* Note the octal representation in the listing. */ 
    DCL ASCOMYCETE BIT (36); 
            ASCOMYCETE = '101'O; 
    END DEMO; 
00003
00001
00002
Description: 
The assignment statement assigns the value of an expression to a variable. 
Format: 
[label:] targetreference = expression; 
Parameters: 
targetreference    is the name of the variable to be assigned a value, and may 
include subscript and pointer qualifiers if required.  The following functions 
may appear on the left hand side of an assignment statement: 
    DBASE     SUBSTR    VFLAGS 
    DBOUND    VBASE     VTYPE 
    DTYPE     VBOUND 
Rules: 
1.  The statement is executed as follows:  First, the subscript and pointer 
    qualifiers, if any, of the target reference are evaluated and the storage 
    location of the target reference is determined.  Then, the expression on 
    the right-hand side of the assignment statement is evaluated.  Finally, 
    the value of the expression is placed in the target reference's storage 
    location. 
2.  If the target reference is an arithmetic variable, the expression can only 
    be an expression of arithmetic type.  If the target reference does not 
    have sufficient precision to contain the result of the expression 
    evaluation, loss of high-order bits will occur on assignment.  If both the 
    target and expression are of type SBIN, and the target reference has 
    greater precision than the expression, then the expression is 
    sign-extended. 
3.  If the target reference is a character-string variable, the expression can 
    only be of character-string type.  (It is also legal to use a SUBSTR 
    built-in function as a target reference) The expression value is truncated 
    on the right if it is longer than the target reference, and extended on 
    the right with blanks if it is shorter than the target reference.  The 
    storage of the target reference must not overlap the storage of the 
    expression value. 
4.  If the target reference is a bit-string variable, an array name without a 
    subscript, or a (sub) structure name, the expression can only be of 
    bit-string type.  The expression value is truncated on the right if it is 
    longer than the target reference, and extended on the right with '0'B if 
    it is shorter than the target reference.  The storage of the target 
    reference must not overlap the storage of the expression value. 
5.  If the target reference is a pointer, the expression can only be of 
    pointer type. 
6.  If the target reference is an entry variable (EPTR), then the expression 
    can only be another entry variable, or a reference to the ENTADDR built-in 
    function which returns an EPTR value. 
7.  No conversion of data type is performed during the assignment.  The data 
    type of the target and of the source must agree. 
8.  Functions for manipulation of fields within VECTOR items may appear on the 
    left hand side of an assignment statement.  These functions are: 
        VBASE      VBOUND      VTYPE 
        VFLAGS 
9.  Functions for manipulation of fields within DSCR 
    items may appear on the left hand side of an assignment 
    statement.  These functions are: 
        DBASE      DBOUND      DTYPE 
00001
00002
Description: 
The ASYNC attribute declares an entry constant as one that refers to an ASYNC 
procedure. 
Format: 
DCL id ENTRY ASYNC; 
Rules: 
1.  The declared entry name is taken to be that of an ASYNC procedure.  The 
    only context in which such an entry name may appear is as an argument of 
    the ENTADDR function.  Such an entry name may not be called.  This applies 
    both to explicit calls and to implicit calls using an EPTR. 
Cross Reference: 
See the discussion of the ASYNC option in the PROC statement. 
00002
00001
In a declare statement, attributes are separated by blanks and can appear in 
any order, with the following exceptions:  ENTRY must immediately follow an 
entry name; the dimension attribute must immediately follow the array name; 
REDEF must immediately follow the name or dimension attribute; length 
specifications must immediately follow their associated data type attributes. 
A semicolon follows the last attribute of a declare statement.  In a structure 
declaration, a comma follows the last attribute of each name and a semicolon 
follows the last attribute of the last name in the structure declaration. 
Available PL6 attributes are: 
ALIGNMENT      ALTRET        AREADEF       AREAREF 
ASYNC          AUTO          BASED         BIT 
BYTE           CHAR          CONSTANT      CONV 
DCB            DIMENSION     DSCR          ENTRY 
EPTR           EXT           EXTROOT       HALF 
INIT           OPTIONAL      PARAMETER     PTR 
READONLY       REDEF         REMEMBER      SBIN 
STATIC         SYMDEF        SYMREF        UBIN 
VECTOR         WORD 
For additional HELP topics, type: 
HELP (PL6) attribute    displays the format and description of. 
                        the specified PL6 attribute. 
HELP (PL6)CONV RULES    displays the rules pertaining to the 
                        CONV attribute. 
HELP (PL6) AUTO FORMAT  displays the format of the AUTO attribute. 
HELP (PL6) CHAR PARAMS  displays the parameter of the CHAR attribute. 
?                       displays the next level of HELP message. 
??                      displays all levels of the current HELP message. 
Description: 
The AUTO attribute assigns a class of storage, to a given data item, that 
specifies that a variable is to be allocated storage dynamically (during 
program execution). 
Format: 
DCL id a1 [a2] ... AUTO; 
Parameters: 
id    any valid identifier. 
a1,a2    any valid attributes. 
Rules: 
1.  AUTO specifies that storage is to be allocated upon each activation of the 
    external procedure in which the declaration is contained.  The storage is 
    released upon termination of the external procedure. 
2.  For structures, only the major structure may be given a storage class 
    attribute; the elements automatically receive the same attribute. 
3.  If a storage class is not specified, AUTO is the default. 
4.  AUTO is used when it is desired to allocate storage automatically. 
    Automatic storage is allocated upon entry to the external procedure to 
    which the declaration is internal, and freed when the external procedure 
    is terminated. 
5.  The length or bound of an AUTO variable may be specified only with a 
    decimal integer constant.  (Variables declared to have adjustable string 
    lengths must be BASED or parameters.) 
Automatic Variables and Recursion 
An automatic variable has a new storage location allocated each time the 
containing external procedure is invoked.  This allows recursion in external 
procedures except where NOAUTO was specified on the PROC statement for the 
external procedure. 
00001
00002
Description: 
The BASED attribute declares an identifier as a based variable. 
Format: 
DCL id a1 [a2] ... BASED [(ptr)]; 
Parameters: 
id    any valid identifier. 
a1,a2    any valid attributes. 
ptr    a PTR variable. 
Rules: 
1.  The identifier is defined as a based variable.  All references to the 
    based variable must be explicit pointer-qualified references unless 
    implicit pointer qualification is used.  (See Rule 8.)  Qualifications may 
    be specified by pointer qualification, or vector qualification (see Notes, 
    below). 
2.  The based variable may be a scalar variable, an array, or a structure. 
3.  The scope of the identifier is always internal to the block in which it is 
    declared. 
4.  The storage referred to by a based variable is located by the value of the 
    qualifier or qualifier expression that qualifies the reference.  The 
    maintenance of such qualifier values is the programmer's responsibility. 
5.  The resolution of a qualifier depends upon the data type of the qualifier. 
    Pointer-type qualifiers have a resolution to the bit boundary.  Therefore, 
    based variables qualified by this type can start at bit boundaries. 
    Descriptor-type qualifiers and vector-type qualifiers have a resolution to 
    the byte boundary.  When used to frame arguments for an inter-domain 
    reference, however, they are operationally restricted to a resolution to 
    the even word boundary (see Notes, below). 
6.  Based variables may not be specified with the PARAM, INIT, AUTO, STATIC, 
    CONSTANT, SYMREF, EXT, AREAREF, EXTROOT, DCB, REDEF or ENTRY attributes. 
7.  The length of a string declared with the BASED attribute is evaluated at 
    each reference to the based variable.  A based variable can be declared 
    with an adjustable character string length, CHAR (var), or adjustable bit 
    string length, BIT (var).  Such a declaration in a based structure can 
    only be given for the last element in the structure declaration. 
8.  If the optional PTR variable construct appears, then id is capable of 
    implicit pointer qualification.  This means that a reference to id with no 
    explicit pointer qualification implies qualification by the PTR variable 
    appearing in the declaration.  The PTR variable must be known in the scope 
    containing the declaration, and may not be BASED, array qualified or a PTR 
    generating function or expression.  The PTR variable may be a parameter to 
    the procedure containing the declaration of the corresponding BASED 
    structure. 
9.  The BASED attribute may be specified on an ENTRY DCL.  This type of entry 
    is used as a dummy target on a CALL statement which uses the THRU option. 
Notes: 
VECTOR data items may be used to qualify BASED items, subject to certain 
restrictions as follows: 
1.  Rule 5 points out that "... and vector-type qualifiers have a resolution 
    to the byte boundary".  Thus, you can't use a VECTOR datum to point to a 
    data structure which isn't at least CALIGNED. 
2.  You cannot use VECTOR items as "implicit" qualifiers (see VECTOR 
    Attribute, rule 3).  Thus, the following is illegal: 
        DCL V_ VECTOR; 
        DCL V_DATA UBIN WORD BASED (V_); 
        V_DATA = 1; 
    You may, however, do this: 
        DCL V_ VECTOR; 
        DCL V_DATA UBIN WORD BASED; 
        V_ -> V_DATA = 1; 
3.  You may not take the ADDR or VECTOR of a VECTOR-based item, either 
    directly (through the ADDR/VECTOR functions) or indirectly (by passing 
    such an item to a subroutine as a parameter) (see VECTOR Attribute, rule 
    7).  Thus, the following constructs are illegal: 
        DCL V_ VECTOR; 
        DCL V_DATA UBIN WORD BASED; 
        DCL P$ PTR; 
        P$ = ADDR(V_ -> V_DATA);   /* explicit ADDR(vector -> field) */ 
        CALL FRONT_DESK (V_ -> V_DATA);/*implicit ADDR(vector -> field)*/ 
    You may, however, do something like this: 
        P$ = ADDR (VBASE(V_) -> V_DATA); 
        CALL FRONT_DESK (VBASE(V_) -> V_DATA); 
    by using the VBASE function, which returns the PTR-flavored portion of a 
    VECTOR datum. 
4.  When you qualify a BASED structure with a VECTOR, the PL-6 compiler 
    generates a "LDDn" instruction (Load Descriptor) in place of the "LDPn" 
    (Load Pointer) used for PTR variables.  The NSA (virtual-memory) hardware 
    uses the "base address" and "byte bound" information in the VECTOR to 
    perform a "shrink" operation, creating a new descriptor which frames only 
    the data area specified by the VECTOR.  When your program actually uses 
    the descriptor to access data, the NSA hardware will limit access to the 
    portion of memory which you actually specified in the VECTOR; if your 
    program attempts to access beyond this limit, a fault will occur. 
    The following program fragment is guaranteed to cause a fault: 
        DCL V_ VECTOR; 
        DCL 1 V_DATA BASED ALIGNED, 
           2 PART1 UBIN WORD, 
           2 PART2 UBIN WORD; 
        DCL P$ PTR; 
        V_ = VECTOR (P$ -> V_DATA.PART1); /* bound will be 3 bytes */ 
        V_ -> V_DATA.PART2 = 0;          /* stores beyond bound; fault */ 
Example: 
    G:      PROC; 
      DCL P$ PTR; 
      DCL Q$ PTR; 
      DCL V UBIN BASED; 
      DCL W UBIN BASED(P$); 
            P$->V=8; 
            W=9; 
            Q$->W=10; 
            RETURN; 
    END G; 
00004
00003
00001
00002
Description: 
The BINASC built-in function allows an integer value to be used as an ASCII 
character. 
Format: 
BINASC (binexp) 
Parameters: 
binexp    any arithmetic expression. 
Rules: 
1.  Result is CHAR(1) obtained from the low order 9 bits of the result of the 
    arithmetic expression. 
2.  If the data type of the expression is UBIN and its length is less than 9 
    bits, the result will be extended on the left with zeros.  If the data 
    type of the expression is SBIN and its length is less than 9 bits, the 
    result will be extended on the left with the sign bit of the expression. 
00001
00002
Description: 
The BINASC preprocessor function allows an SBIN value to be used as an ASCII 
character. 
Format: 
BINASC (exp) 
Parameters: 
exp    is an sbin expression. 
Rules: 
1.  Only the low order n bits of the SBIN expression will be used when 
    evaluating BINASC, where n is the number of bits required to represent an 
    ASCII character on the target machine. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU CHARACTER= BINASC (65); 
    DCL ASCII_CHARACTER CHAR (1); 
    ASCII_CHARACTER = %CHARACTER; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU CHARACTER= 'A'; 
    DCL ASCII_CHARACTER CHAR (1); 
            ASCII_CHARACTER = 'A'; 
    END DEMO; 
00003
00001
00002
Description: 
The BINBIT built-in function allows an integer value to be used as a bit 
string. 
Format: 
BINBIT (binid, len) 
Parameters: 
binid    any arithmetic expression. 
len    any constant expression. 
Rules: 
1.  BINBIT will return a BIT (len) quantity. 
2.  len must be defined such that its value is known at compilation. 
3.  If len is equal to or less than the number of bits in the arithmetic 
    expression, then the result is the rightmost len bits of the arithmetic 
    expression.  If len is greater than the number of bits in the expression, 
    then the result will be based on the resultant data type of the 
    expression.  If it is SBIN, the high order bit will be extended on the 
    left such that the result is len bits long.  If it is UBIN, the expression 
    will be extended on the left with zeros such that the result is len bits 
    long. 
4.  Legal values for len are defined as follows: 
        1 <= len <= 36 
5.  When BINBIT is used in an INIT clause of a DCL statement, the len argument 
    is not required.  If len is not specified, its value is provided by the 
    size of the variable being declared. 
00001
00002
Description: 
The BINBIT preprocessor function allows a specified portion of an SBIN 
expression to be used as a bit string. 
Format: 
BINBIT ( exp1, exp2 ) 
Parameters: 
exp1 and exp2    are sbin expressions. 
Rules: 
1.  BINBIT returns the rightmost exp2 bits of exp1 as a bit string. 
2.  exp2 has a value of 0 to 36. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU TWENTY_FIVE_CENTS = BINBIT (249,5); 
    DCL TWO_BITS BIT (36); 
    TWO_BITS = %TWENTY_FIVE_CENTS; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU TWENTY_FIVE_CENTS = '11001'B; 
    DCL TWO_BITS BIT (36); 
            TWO_BITS = '11001'B; 
    END DEMO; 
00003
00001
00002
Description: 
The BINCHAR built-in subroutine converts a binary number to a CHAR string of 
all digit characters, with no spaces and no sign characters. 
Format: 
CALL BINCHAR (str, val); 
Parameters: 
str    any character location reference. 
val    any arithmetic expression. 
Rules: 
1.  str represents the resultant string and must be of data type CHAR.  Its 
    length must be within the range defined as: 
        1 <= LENGTHC (str) <= 63 
    or results will be unpredictable.  The resultant string will consist of 
    the digit characters representing the numeric value of val.  Leading zeros 
    are supplied to fill the field when necessary. 
2.  val may be of either UBIN or SBIN data type.  If the value is negative the 
    magnitude of val will be converted. 
3.  If the value of val will not fit into str, the result will be truncated or 
    an overflow fault will occur. 
4.  If string length is out of range the results are undefined. 
00001
00002
Description: 
The BINCHAR preprocessor function converts an SBIN expression to a numeric 
character string. 
Format: 
BINCHAR ( exp1 [, exp2 ]) 
Parameters: 
exp1 and exp2    are sbin expressions. 
Rules: 
1.  If exp2 is specified, the resultant character string will be exp2 
    characters long (zero filled to the left).  If exp2 is not specified, the 
    length of the character string produced will be the minimum required to 
    represent the value of exp1. 
2.  exp1 must not be negative.  If it is desired to convert a negative number, 
    BINXCHAR should be used. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU NUMBER = BINCHAR (12345,5); 
    DCL NUMBER_OF_CHARACTERS CHAR (10); 
    NUMBER_OF_CHARACTERS = %NUMBER; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU NUMBER = '12345'; 
    DCL NUMBER_OF_CHARACTERS CHAR (10); 
            NUMBER_OF_CHARACTERS = '12345'; 
    END DEMO; 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU NUMBER = BINCHAR (12345,9); 
    DCL NUMBER_OF_CHARACTERS CHAR (10); 
    NUMBER_OF_CHARACTERS = %NUMBER; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU NUMBER = '000012345'; 
    DCL NUMBER_OF_CHARACTERS CHAR (10); 
            NUMBER_OF_CHARACTERS = '000012345'; 
    END DEMO; 
00003
00001
00002
Description: 
The BINXCHAR built-in subroutine converts a signed binary number to a CHAR 
string of one leading sign character followed by digit  characters. 
Format: 
CALL BINXCHAR (str, val); 
Parameters: 
str    any character location reference. 
val    any arithmetic expression. 
Rules: 
1.  str represents the resultant string and must be of data type CHAR.  Its 
    length must be within the range defined as: 
        2 <= LENGTHC (str) <= 63 
    or results will be unpredictable.  The result string will be either the 
    '+' or '-' character, based on the sign of val, followed by the digit 
    characters representing the numeric value of val.  Leading zeros are 
    supplied to fill the field, if necessary. 
2.  val may be of either UBIN or SBIN data type. 
3.  If the value of val will not fit into str, the result will be truncated or 
    an overflow fault will occur. 
4.  If string length is out of range the results are undefined. 
00001
00002
Description: 
The BINXCHAR preprocessor function converts an SBIN expression to a numeric 
character string. 
Format: 
BINXCHAR ( exp1 [, exp2 ]) 
Parameters: 
exp1 and exp2    are sbin expressions. 
Rules: 
1.  If exp2 is specified, the resultant character string will be exp2 
    characters long (zero filled as necessary).  If exp2 is not specified, the 
    length of the character string produced will be the minimum required to 
    represent the value of exp1. 
2.  The sign will always preceed the value and it is included in the length of 
    the resultant string. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU NUMBER = BINXCHAR (-12345,9); 
    DCL NUMBER_OF_CHARACTERS CHAR (10); 
    NUMBER_OF_CHARACTERS = %NUMBER; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU NUMBER = '-00012345'; 
    DCL NUMBER_OF_CHARACTERS CHAR (10); 
            NUMBER_OF_CHARACTERS = '-00012345'; 
    END DEMO; 
00003
00001
00002
Description: 
The BIT attribute declares a variable to be of the bit-string data type. 
Format: 
DCL id BIT {(lengthconst)}; 
           {(lengthref  )} 
Parameters: 
id    any valid identifier. 
lengthconst    a decimal integer between 0 and 72, inclusive, indicating the 
length, in bits, of the string. 
lengthref    a possibly structure-qualified reference. 
Rules: 
1.  If the declaration of a variable contains the attribute BIT(0), then the 
    declaration must also contain the INIT attribute, specifying a bit-string 
    constant as an initial value.  The variable so declared will be assigned a 
    length equal to the length of its INIT value.  If the variable is an 
    array, all items in the array will be assigned a length equal to the 
    length of the longest item in the INIT list. 
2.  If the declaration of a variable contains the attribute BIT(lengthref), 
    then the length of the variable will be determined dynamically each time 
    the variable is referenced.  The value of the length will be the current 
    value of the length-defining reference.  Such a BIT variable is said to be 
    adjustable.  The run-time value of the length-defining reference may be 
    from 0 to (2**18)-1, inclusive.  An adjustable BIT variable must either be 
    a BASED, SYMREF, DCB, or PARAM scalar, or the last element in a BASED, 
    SYMREF, DCB, or PARAM structure. 
3.  The length-defining reference in the declaration of an adjustable BIT 
    variable must be of an arithmetic data type.  The length reference may not 
    be BASED or DCB, except in the case that the adjustable BIT variable is an 
    element of a structure and the length reference is an element of the same 
    structure. 
4.  The length-defining reference in the declaration of an adjustable BIT 
    variable must not be an array reference. 
Example: 
    DCL   B1   BIT(1); 
    DCL   B2   BIT(47); 
    DCL   L    UBIN; 
    DCL   B3   BIT (L) BASED; 
    DCL 1 A BASED, 
          2 B BIT(1), 
          2 C BIT(72), 
          2 D UBIN, 
          2 E BIT(A.D); 
00003
00001
00002
Description: 
The BITASC built-in function allows a bit string to be used as a single 
character. 
Format: 
BITASC (bitexp) 
Parameters: 
bitexp    any bit expression. 
Rules: 
1.  The result is CHAR(1) obtained from the high-order 9 bits of the 
    bit-expression.  If the size of the expression is less than 9 bits, then 
    the result will be extended on the right with zeros. 
00001
00002
Description: 
The BITASC preprocessor function allows a bit string to be used as an ASCII 
character. 
Format: 
BITASC (exp) 
Parameters: 
exp    is a bit string expression. 
Rules: 
1.  The low order n bits of the bit string will be used by BITASC, where n is 
    the number of bits required to represent an ASCII character on the target 
    machine. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU CHARACTER = BITASC ('001000010'B); 
    DCL ASCII_CHARACTER CHAR (1); 
    ASCII_CHARACTER = %CHARACTER; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU CHARACTER = 'B'; 
    DCL ASCII_CHARACTER CHAR (1); 
            ASCII_CHARACTER = 'B'; 
    END DEMO; 
00003
00001
00002
Description: 
The BITBIN built-in function allows a bit string to be used as an integer. 
Format: 
BITBIN (bitid) 
Parameters: 
bitid    any bit expression. 
Rules: 
1.  BITBIN will return a UBIN WORD value. 
2.  The low order bit of the resultant integer is the rightmost bit of the 
    bit-string expression. 
3.  If the length of the bit-string is greater than 36, only the rightmost 36 
    bits will be used.  If the length of the bit-string is less than 36, the 
    integer will be extended with high order zeros. 
00001
00002
Description: 
The BITBIN preprocessor function allows a bit string to be used as an SBIN 
value. 
Format: 
BITBIN (exp) 
Parameters: 
exp    is a bit string expression. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = BITBIN ('0101010'B); 
    DCL A SBIN; 
    A = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = 42; 
    DCL A SBIN; 
            A = 42; 
    END DEMO; 
00002
00001
Description: 
BITVECT allows a BIT(72) item to be used as a VECTOR. 
Format: 
BITVECT (bitid) 
Parameters: 
bitid    any bit expression. 
Rules: 
1.  The  length of the bit-string must be exactly 72 bits. 
2.  The low order bit of the resultant vector is the rightmost bit of the 
    bit-string expression. 
00001
00002
The built-in functions and subroutines provide additional operations and 
efficient use of the hardware facilities.  Such built-in functions and 
subroutines have some constraints.  Violation of these constraints will cause 
undefined results.  In this case, the appropriate Machine Level Reference 
Manual should be consulted. 
Available built-in functions and subroutines are: 
ADDR              ASCBIN         ASCBIT          BINASC 
BINBIT            BINCHAR        BINXCHAR        BITASC 
BITBIN            BITVECT        CHARBIN         CONCAT 
DBASE             DBOUND         DCBADDR         DCBNUM 
DTYPE             EDITCHAR       EDITSTR         EDITXCHAR 
ENTADDR           INDEX          INDEX1R         INDEX2R 
INSERT            LENGTHB        LENGTHC         LENGTHV 
LENGTHW           MAXIMUM        MINIMUM         MOD 
PALIGND           PALIGNW        PINCRB          PINCRC 
PINCRW            POFFC          POFFW           PTRDSCR 
SEARCH            SEARCHR        SIZEB           SIZEC 
SIZEV             SIZEW          SUBSTR          VECTOR 
VECTDSCR          VTYPE          XCHARBIN        XLATE 
XLATE_9_TO_6 
For additional HELP topics, type: 
HELP (PL6) built-in     displays the format and description 
                        of the specified function or subroutine. 
HELP (PL6) INDEX RULES  displays the rules pertaining to the INDEX subroutine. 
HELP (PL6) POFFW PARAM  displays the parameters of the POFFW function. 
HELP (PL6) SIZEW EXAM   displays an example illustrating the SIZEW function. 
?                       displays the next level of HELP message. 
??                      displays all levels of the current HELP message. 
BUILT_IN
BUILT_IN
Description: 
The BYTE attribute is used with SBIN or UBIN to specify that a binary integer 
occupies 9 bits. 
Format: 
DCL id {UBIN} BYTE; 
       {SBIN} 
Parameters: 
id    any valid identifier. 
Rules: 
1.  For SBIN, the BYTE attribute defines id to be a binary integer with a 
    precision of 8 bits plus a sign bit. 
2.  For UBIN, BYTE defines id to be a binary integer with a precision of 9 
    bits. 
Cross Reference: 
See SBIN and UBIN attributes. 
00003
00001
00002
ALIGNMENT
Description: 
The CALL statement causes control to be transferred to a specified entry point 
of a subroutine procedure and passes information to the invoked procedure. 
Format: 
[label:] CALL ref [(arg1[, arg2] ... )] [THRU eptr_exp] 
    [ALTRET (label)                                ] 
    [[WHENRETURN DO group] [WHENALTRETURN DO group]]; 
Parameters: 
ref    name of an entry point to a procedure, or an EPTR variable. 
arg1,arg2    any legal PL6 expression or variable. A maximum of 63 arguments 
is allowed. 
eptr_exp    an EPTR expression. 
DO group    see DO groups. 
Rules: 
1.  If ref is an entry point constant, the CALL statement must be within the 
    scope in which the name is known, and must not violate any restrictions on 
    recursion. 
2.  Each argument (arg1[, arg2] ... ) must agree with the corresponding 
    entry-point parameter in type, dimension (if any), structure (if any), and 
    alignment.  An unspecified argument is indicated by an empty position in 
    the argument list. 
3.  Labels, unqualified DCBs, unqualified BASED variables, and entry constants 
    may not be passed as arguments. 
4.  Arguments are passed by address (rather than by value); that is, a PTR to 
    the argument is created.  When an argument is not specified, a PTR with 
    the value ADDR (NIL) is supplied. 
5.  The ALTRET option specifies a label constant in the calling procedure to 
    which control will be transferred if the return from the CALLed procedure 
    is made with the ALTRETURN statement.  The label specified must be 
    immediately contained in the same procedure as the CALL statement. 
6.  The WHENRETURN and WHENALTRETURN clauses may be used to specify a DO block 
    to be executed if the return from the CALLed procedure is made with the 
    RETURN or ALTRETURN statements.  These clauses may be used when calling a 
    PROCedure which was defined with the ALTRET clause on its PROC or ENTRY 
    declaration. 
7.  The THRU option is used when CALLing with an EPTR.  When the THRU option 
    is used, the ENTRY DCL for the CALL ref must be BASED. 
8.  Any literals or expressions that require run-time evaluation will have the 
    following starting alignment and size based on data type: 
    Data Type        Alignment        Size 
    ---------        ---------        ---- 
    UBIN/SBIN          WORD           36 bits 
    PTR                WORD           36 bits 
    EPTR               WORD           36 bits 
    BIT                WORD           largest size specified 
    VECTOR             WORD           72 bits 
    REMEMBER           DWORD          72 bits 
    DSCR               DWORD          72 bits 
Example: 
    B:  CALL SAMPLE (J+1,F&'775'O,,P$->Q(3*K),BINASC(K)) ALTRET(S); 
    SAMPLE : PROC (I, M, K, STR, CHR); 
    DCL I UBIN WORD; 
    DCL M BIT(36); 
    DCL K SBIN; 
    DCL STR CHAR(8); 
    DCL CHR CHAR(1); 
      CALL TEST_ROUTINE (I, J) 
        WHENRETURN DO; 
          I = I * J; 
         END; 
         WHENALTRETURN 
          DO; 
             I = I - J; 
             J = J * (J - I); 
          END; 
       RETURN; 
    END SAMPLE; 
00003
00001
00002
Description: 
The CASE statement defines the start of a case which is to be executed when 
the expression in an encompassing DO CASE group evaluates to one of the 
arguments of the CASE statement. 
Format: 
CASE [(]const1[, const2] ... [)]; 
         or 
CASE [(][[yconst1, [yconst2, ] ... ] ELSE [[, zconst1], [zconst2] ... ][)]; 
Parameters: 
const    an arithmetic constant specifying a value of the DO CASE expression 
for which this case is to be executed; const must be greater than or equal to 
0. 
yconst,zconst    see Rule 4. 
Rules: 
1.  CASE statements are used between the DO CASE statement and its 
    corresponding END statement.  The code between a given CASE statement and 
    the next CASE statement, or END statement matching the DO CASE, will be 
    executed whenever that CASE statement specifies a constant equal to the 
    value of the DO CASE expression. 
2.  Since a jump table is created by the compiler, it is prudent to restrict 
    the range of values of const to small positive values.  The maximum range 
    allowed in a CASE statement is 1024. 
3.  A label is not permitted on the CASE statement. 
4.  If ELSE is specified, the code following the CASE/ELSE statement will be 
    executed if the value of the DO CASE exp does not match any of the 
    constants specified on any other CASE statement associated with the DO 
    CASE group. 
    The list of yconst(s) and zconst(s) do not affect the execution of the 
    statement.  Provision for these lists is made so that the programmer can 
    remind himself of certain possible values of the DO CASE expression for 
    which he has not written an ELSE-less CASE group and which, if they occur, 
    will cause execution of the CASE/ELSE group.  Note that there can be but 
    one CASE/ELSE statement in a DO CASE group. 
5.  If ELSE is not specified and the evaluation of the DO CASE does not result 
    in a match with any CASE statement, control will be transferred to the 
    corresponding END statement. 
6.  It is an error to have multiple specifications of the same constant or 
    ELSE.  That is, each list of const(s) in a CASE statement must be mutually 
    exclusive with the other such lists in the group, and with the yconst(s) 
    and zconst(s) in the CASE/ELSE statement, if present. 
00001
00002
    The following changes have been made for E02 PL6: 
    o  Fixed CALL Statement format. 
    o  Fixed MATERIALIZE Clause rule #2. 
    o  Created a new PL-6 HELP topic 'SYSTEM_FILE'. 
Description: 
The CHAR attribute declares a variable to be of the character-string data 
type. 
Format: 
DCL id CHAR {(lengthconst)}; 
            {(lengthref  )} 
Parameters: 
id    any valid identifier. 
lengthconst    a decimal integer between 0 and 16384, inclusive, indicating 
the length, in characters, of the string. 
lengthref    a possibly structure-qualified reference. 
Rules: 
1.  If the declaration of a variable contains the attribute CHAR(0), then the 
    declaration must also contain the INIT attribute, specifying a 
    character-string constant as an initial value.  The variable so declared 
    will be assigned a length equal to the length of its INIT value.  If the 
    item is arrayed, the variable will be assigned a length equal to the 
    length of the longest item in the INIT list. 
2.  If the declaration of a variable contains the reference form of the CHAR 
    attribute, then the length of the variable will be determined dynamically 
    each time the variable is referenced, and the value of the length will be 
    the current value of the length-defining reference.  Such a CHAR variable 
    is said to be adjustable.  The run-time value of the length-defining 
    reference may be from 0 to (2**18)-1, inclusive.  An adjustable CHAR 
    variable must be either a BASED, SYMREF, DCB or PARAM scalar, or the last 
    element in a BASED, SYMREF, DCB or PARAM structure. 
3.  The length-defining reference in the declaration of an adjustable CHAR 
    variable must be of the arithmetic data type.  The length reference may 
    not be BASED or DCB, except in the case that the adjustable CHAR variable 
    is an element of a structure and the length reference is an element of the 
    same structure. 
4.  The length-defining reference in the declaration of an adjustable CHAR 
    variable must not be an array reference. 
Example: 
    DCL  C1 CHAR(1); 
    DCL  C2 CHAR(451); 
    DCL LEN UBIN; 
    DCL ADJUSTABLE CHAR(LEN) BASED; 
    DCL 1 W BASED, 
          2 T CHAR(1), 
          2 BILL UBIN, 
          2 N CHAR(W.BILL); 
00003
00001
00002
Description: 
The CHARBIN built-in subroutine converts an unsigned digit character string to 
a positive binary integer. 
Format: 
CALL CHARBIN (ref, str); 
Parameters: 
ref    a possibly pointer-qualified, possibly structure-qualified, possibly 
subscripted reference. 
str    any character expression. 
Rules: 
1.  ref must be SBIN WORD, SBIN(36), UBIN WORD, or UBIN(36), and word aligned. 
    The value of str will be placed in ref as a positive integer. 
2.  str represents the digit character string to be converted and must be of 
    data type CHAR.  Any sign character is illegal, and if one is found the 
    result will be undefined.  The length of str must be within the range 
    defined as: 
        1 <= LENGTHC (str) <= 63 
    or results will be undefined. 
3.  If the binary value will not fit in the resultant word, then truncation or 
    an overflow fault will result. 
4.  If nondigit characters are used or if string length is out of range the 
    results are undefined. 
00001
00002
Description: 
The CHARBIN preprocessor function converts a numeric character string to an 
SBIN value. 
Format: 
CHARBIN (exp) 
Parameters: 
exp    is an unsigned decimal character string expression. 
Rules: 
1.  The argument character string must not contain a leading sign.  If signed 
    data is to be converted, XCHARBIN should be used. 
2.  The argument character string must not contain non-numeric characters. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = CHARBIN ('234599'); 
    DCL A SBIN; 
    A = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = 234599; 
    DCL A SBIN; 
            A = 234599; 
    END DEMO; 
00003
00001
00002
Description: 
The CHARTEXT preprocessor function converts a character string expression into 
a text expression.  Essentially, this function removes the delimiting 
apostrophes from a character string. 
Format: 
CHARTEXT (exp) 
Parameters: 
exp    is a character string expression. 
Rules: 
1.  It is recommended that this function be used only for the creation of 
    unique PL-6 identifiers. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %SET VARNUM = 1; 
    DCL %(CHARTEXT (CONCAT ('VAR', BINCHAR (VARNUM,2))))  UBIN; 
    %SET VARNUM = VARNUM + 1; 
    DCL %(CHARTEXT (CONCAT('VAR', BINCHAR (VARNUM,2)))) UBIN; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %SET VARNUM = 1; 
    DCL VAR01  UBIN; 
    %SET VARNUM = 2; 
    DCL VAR02 UBIN; 
    END DEMO; 
00003
00001
00002
Description: 
The CONCAT built-in subroutine allows the concatenation of up to six strings. 
Format: 
CALL CONCAT (tostr, str1 [, str2] ... [, str6]) 
    [ALTRET (label)                                 ]; 
    [[WHENRETURN DO group ] [WHENALTRETURN DO group]] 
Parameters: 
tostr    character location reference. 
str1,...,str6    any character expression. 
label    any valid label. 
Rules: 
1.  tostr is the character location reference which specifies the destination 
    of the concatenated strings. 
2.  The source character strings will be concatenated in the order str1, 
    str2,... str6. 
3.  If the length of the concatenated source strings is less than the length 
    of tostr, then blank-fill on the right will occur. 
4.  If the length of the concatenated string is greater than the length of 
    tostr then the concatenated string will be truncated to the length of 
    tostr. 
5.  If truncation of the concatenated string occurs the CONCAT operation will 
    ALTRETURN. 
6.  If tostr overlaps any of the source strings, the result is undefined. 
00001
00002
Description: 
The CONCAT preprocessor function returns a string which is the concatenation 
of all of the argument strings specified. 
Format: 
CONCAT (exp [, exp] ... ) 
Parameters: 
exp    is either a bit string expression or a character string expression. 
Rules: 
1.  The argument expressions may be either bit strings or character strings. 
    The two types may not be mixed within one CONCAT. 
2.  For bit string arguments CONCAT returns a bit string composed of the 
    concatenated bit string arguments.  The length of the resultant bit string 
    must be less than or equal to 72. 
3.  For character string arguments CONCAT returns a character string composed 
    of the concatenated character string arguments.  The length of the 
    resultant character string must be less than or equal to 272. 
4.  The source strings are concatenated in the order in which they appear 
    (left to right) in the argument list. 
5.  A maximum of 48 arguments may be given to the CONCAT function. 
6.  For character arguments, LENGTHC (CONCAT (A, B)) = LENGTHC (A) + LENGTHC 
    (B). 
7.  For bit string arguments, LENGTHB (CONCAT (A, B)) = LENGTHB (A) + LENGTHB 
    (B). 
Example: 
The following example illustrates bit string concatenation: 
    DEMO:PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = CONCAT ('010'B,'0110'B,'1'B); 
    DCL FOR_LACK_OF_BETTER_WORDS BIT (36); 
    FOR_LACK_OF_BETTER_WORDS = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = '01001101'B; 
    DCL FOR_LACK_OF_BETTER_WORDS BIT (36); 
            FOR_LACK_OF_BETTER_WORDS = '01001101'B; 
    END DEMO; 
The following example illustrates character string concatenation: 
    BOUGHS_OF_HOLLE: PROC; 
    %SET LISTEXP = '1'B; 
    %SET TWENTY_FIVE = CONCAT ('ABCDE', 'FGHIJ', 'KMNOP', 'QRSTU', 'VWXYZ'); 
    DCL GREETINGS CHAR (25); 
    GREETINGS = %TWENTY_FIVE; 
    END BOUGHS_OF_HOLLE; 
The preceding source produces the following listing output: 
    BOUGHS_OF_HOLLE: PROC; 
    %SET LISTEXP = '1'B; 
    %SET TWENTY_FIVE = 'ABCDEFGHIJKMNOPQRSTUVWXYZ'; 
    DCL GREETINGS CHAR (25); 
            GREETINGS = 'ABCDEFGHIJKMNOPQRSTUVWXYZ'; 
    END BOUGHS_OF_HOLLE; 
00003
00001
00002
Description: 
The CONSTANT attribute declares an identifier as one whose value will never be 
changed. 
Format: 
DCL id a1 [a2] ... INIT (value) CONSTANT; 
Parameters: 
id    any valid identifier at level-1. 
a1,a2    any valid attributes. 
value    see description of INIT attribute. 
Rules: 
1.  A CONSTANT variable is statically allocated storage that is described as 
    read-only.  Accordingly, if a variable has the CONSTANT attribute 
    specified, it is illegal to use the variable as a target reference in an 
    assignment statement. 
Example: 
    DCL ONE UBIN(3) INIT(1) CONSTANT; 
Cross Reference: 
See the READONLY attribute. 
00004
00003
00001
00002
Description: 
The CONV attribute differentiates between calls to the operating system, PL-6 
procedures and the alternate-shared library. 
Format: 
DCL id ENTRY [(n)] CONV (type [, code1 [, code2]]); 
Parameters: 
id    any valid identifier. 
type } 
code1}    integers. 
code2} 
Rules: 
1.  A type field of zero (0) implies a standard calling sequence.  None of the 
    optional codes are allowed with CONV(0).  This clause will inform the 
    compiler to generate the descriptor information as part of the call.  The 
    default is not to generate this information. 
2.  A type field of one (1) indicates a call to the operating system.  code1 
    represents the number of vectors/parameters to be specified in the PMME 
    form of the CLIMB.  code2 represents the specific value identifying the 
    PMME.  It is not legal to take the ENTADDR of a CONV(1) ENTRY. 
    The CLIMB instruction will be generated as follows: 
    E = 0, P = 0, if code1 = 0 
    E = 1,  P = code1 - 1, if code1 > 0 
    address = code2; (high order bit = 1, 
    if ALTRET option is specified on the CALL) 
3.  A type field of two (2) indicates a CALL to the alternate-shared library. 
    code1 represents the number of vectors/parameters to be specified in the 
    CALL form of the CLIMB.  Code 2 is not allowed and must be left blank.  It 
    is not legal to take the ENTADDR of a CONV(3) ENTRY.  The ENTRY id for 
    CONV(2) is placed in the object unit as a SYMREF rather than an ENTREF. 
    The CLIMB instruction will be generated as follows: 
    E = 0, P = 0, if code1 = 0 
    E = 1, P = code1  - 1, if code1 > 0 
    address = SYMREF of DCL name 
4.  A type field of three (3) or four (4) is not allowed. 
5.  A type field of five (5) identifies a data only procedure. 
    An ENTREF will be generated which matches the ENTDEF which 
    PL6 generates for a non-callable data only procedure.  The 
    other CONV options, ALTRET, OPTIONAL, ASYNC or number of 
    parameters may not be specified with CONV(5). 
    A CONV(5) ENTRY may not be called or used in an ENTADDR 
    function. 
00001
00002
Description: 
The COUNT preprocessor function returns the number of elements in a list. 
Essentially, this returns the number of commas used as text delimiters + 1. 
Format: 
COUNT (item [, item] ... ) 
Parameters: 
item    is any text. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = COUNT (ONE, TWO, 5 + 34, (N)); 
    DCL A SBIN; 
    A = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = 4; 
    DCL A SBIN; 
            A = 4; 
    END DEMO; 
00002
00001
Description: 
The CPTR attribute declares an identifier as a pointer variable having a 
character offset. 
Format: 
DCL id CPTR 
Parameters: 
id    any valid identifier. 
Rules: 
1.  Character pointer variables are valid only in programs compiled with the 
    FEP option; in other programs they will be treated as pointer variables. 
2.  The identifier may be a scalar variable, an array name, or a structure 
    element.  It is declared as pointer-type data. 
3.  Character pointer variables may point to (or identify) based data. 
4.  A character pointer variable may be assigned only a pointer value or 
    character pointer value; that is, the value of another pointer variable, 
    or character pointer variable, or the value returned by a pointer valued 
    built-in function. 
5.  A character pointer variable may be null.  ADDR(NIL) represents this null 
    value and may be compared to or assigned. 
6.  A character pointer variable may be initialized only with the ADDR 
    built-in function. 
7.  No operations other than the comparison operations may be applied to 
    character pointer variables, and no conversions may be performed between 
    pointer data and other data types. 
Examples: 
DCL P$ CPTR; 
DCL POINTER_ARRAY$ (0:10) CPTR; 
Cross Reference: 
See the ADDR, DCBADDR, PINCRW, PINCRR, POFFU, POFFC built-in functions. 
00004
00003
00001
00002
ALIGNMENT
Description: 
The DBASE built-in function allows access to the base address of the segment 
described by the referenced descriptor. 
Format: 
DBASE(desc-ref) 
Parameters: 
desc-ref    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted descriptor reference. 
Rules: 
1.  DBASE represents a UBIN WORD value. 
2.  The compiler will never generate an LDD or STD instruction to access the 
    referenced descriptor for this function.  Therefore, the descriptor must 
    be accessible to the program via non-NSA instructions. 
3.  The DBASE built-in function may be used as a target pseudo-variable on the 
    left hand side of an assignment statement.  The evaluated expression must 
    be an arithmetic expression. 
00001
00002
00003
Description: 
The DBOUND built-in function allows access to the bound field of the 
referenced descriptor. 
Format: 
DBOUND(desc-ref) 
Parameters: 
desc-ref    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted descriptor reference. 
Rules: 
1.  DBOUND represents a UBIN(20) value. 
2.  The compiler will never generate an LDD or STD instruction to access the 
    referenced descriptor for this function.  Therefore, the descriptor must 
    be accessible to the program via non-NSA instructions. 
3.  The DBOUND built-in function may be used as a target pseudo-variable on 
    the left hand side of an assignment statement.  The evaluated expression 
    must be an arithmetic expression. 
00001
00002
00003
Description: 
The DCB attribute specifies the variable as a Data Control Block. 
Format: 
DCL id DCB; 
Parameters: 
id    any valid identifier. 
Rules: 
1.  A Data Control Block will be allocated with the name 'id'. 
2.  All references to a DCB variable must be pointer qualified.  To obtain a 
    pointer to a Data Control Block, the DCBADDR built-in function must be 
    used. 
3.  A structure declared with the DCB attribute may have the INIT attribute. 
4.  A variable declared with the DCB attribute must be pointer-qualified in 
    order to be passed as an argument in a procedure reference. 
00001
00002
Description: 
The DCBADDR built-in function builds a pointer to the DCB specified by a given 
DCB number. 
Format: 
DCBADDR (exp) 
Parameters: 
exp    any arithmetic expression. 
Rules: 
1.  The value of the expression will represent the DCB number to be used in 
    locating the correct pointer to the DCB. 
2.  DCBADDR returns a pointer locating the storage allocated for the DCB. 
3.  DCBADDR is not allowed in an INIT clause. 
Example: 
    DCL MY$DCB DCB; 
    DCL MY$DCB# UBIN STATIC INIT(DCBNUM(MY$DCB)); 
    DCL MY$DCB$ PTR; 
    MY$DCB$ = DCBADDR(MY$DCB#); 
Cross Reference: 
See the DCBNUM built-in function and the DCB attribute. 
00004
00003
00001
00002
Description: 
The DCBNUM built-in function returns the DCB number of the specified DCB. 
Format: 
DCBNUM (dcb) 
Parameters: 
dcb    any variable with the DCB attribute, or NIL. 
Rules: 
1.  The value returned is the DCB index of the specified DCB. 
2.  DCBNUM returns a UBIN WORD result. 
3.  DCBNUM (NIL) returns the DCB index of the null DCB. 
4.  DCBNUM is allowed within an INIT clause. 
Example: 
    DCL MY$DCB DCB; 
    OPENFPT.DCB = DCBNUM (MY$DCB); 
Cross Reference: 
See the DCBADDR built-in function and the DCB attribute. 
00004
00003
00001
00002
Description: 
The DCL statement defines a set of attributes (characteristics) for one or 
more identifiers. 
Format: 
DCL [lev1] id1 [attributelist1] [, levn idn [attributelistn]] ... ; 
Parameters: 
lev1,levn    level numbers, where n < 10. 
id1,idn    any valid identifier (or, if level number > 1, *). 
attributelist1    list of appropriate attributes. 
attributelistn    separated by blanks. 
Rules: 
1.  One scalar variable, array, or structure may appear in each DCL statement. 
    The statement may not have a label prefix. 
2.  The complete declaration of an identifier must be separated by a comma 
    from any other identifier in the declaration statement of a structure. 
3.  A level number, denoting a structure level, precedes each identifier in 
    the declaration of a structure.  It must be an unsigned non-zero decimal 
    integer constant.  The level number 1 must be specified for all major 
    structure names.  A non-structure variable has a default level number of 
    1. 
4.  DCL statements in a given procedure must be grouped such that all 
    declarations appear at the beginning of the procedure. 
5.  A given attribute must not be specified more than once for the same name. 
6.  At least one blank is required to separate a level number from the 
    identifier which follows it, and to separate attributes. 
7.  When an elementary data item is declared in a structure, the "filler" name 
    * may be assigned to that area of the structure rather than an actual 
    name.  This feature is useful for including areas for expansion in a 
    structure in such a manner that the expansion necessitates recompilation 
    of only those procedures that reference the new data items added in the 
    filler area.  Note that the variable * may not be explicitly referenced. 
Rules Concerning Order of Attributes 
1.  The ENTRY attribute must immediately follow the entry name. 
2.  The DIMENSION attribute must be the first attribute to follow an array 
    name in its declaration. 
3.  The REDEF attribute, if present, must immediately follow the name or 
    dimension attribute. 
4.  LENGTH attributes must immediately follow the data attributes to which 
    they apply (CHAR, UBIN, SBIN, and BIT). 
Cross Reference: 
See the discussion on Attributes 
Example: 
    DCL DNAME CHAR(5); 
    DCL CTR SBIN; 
    DCL 1 S BASED, 
          2 A$ PTR, 
          2 B (0:5), 
            3 C BIT(8), 
            3 D SBIN; 
Example of filler space: 
    DCL 1 BLOCK BASED, 
          2 FLAGS, 
            3 FLAG1 BIT(1), 
            3 FLAG2 BIT(1), 
            3 * BIT(34), 
          2 OTHER_STUFF$ PTR; 
may be changed to: 
    DCL 1 BLOCK BASED, 
          2 FLAGS, 
            3 FLAG1 BIT(1), 
            3 FLAG2 BIT(1), 
            3 FLAG3 BIT(1),     /* New flag                         */ 
            3 * BIT(33),        /* Filler decreased to make room    */ 
          2 OTHER_STUFF$ PTR; 
and all references to fields in the first version of BLOCK are still valid. 
00003
00004
00001
00002
Description: 
The DIMENSION attribute declares an identifier as an array name; specifies the 
subscript bound of the array. 
Format: 
DCL id (0:c1) a1 [a2] ... ; 
Parameters: 
id    any valid identifier. 
c1    upper subscript bound. 
a1,a2    any valid attributes. 
Rules: 
1.  c1 is a non-negative decimal constant. 
2.  The upper bound c1 is specifiable and is limited to (2**18)-1; the lower 
    bound must be zero. 
3.  An array has only one dimension. 
4.  If the dimension attribute appears, it must precede all other attributes 
    in the attribute list for that identifier. 
5.  Adjustable length CHAR or BIT strings may not be part of an array. 
6.  The maximum storage allocation for any data structure in PL6 is 256K 
    words. 
Example: 
    DCL ARRAY (0:8) SBIN; 
    DCL 1 BB (0:10) BASED, 
          2 AA BIT(7), 
          2 CC, 
            3 DD BIT(8), 
            3 EE CHAR(5); 
00003
00001
00002
Description: 
The DO statement, simple clause, delimits the start of a DO group, a group of 
statements which are performed as a unit. 
Format: 
[label:] DO; 
Rules: 
1.  The statements following the DO statement constitute a DO group.  This 
    group must be terminated by an END statement. 
2.  A DO group may appear in a compound (IF/THEN/ELSE) statement or any place 
    where a single statement is permitted. 
Example: 
    IF D < E THEN 
       I=0; 
    ELSE 
      DO; 
         I=I+1; 
         Z=Z*5; 
         END; 
00002
00001
DO_TO_DOWNTO_BY
Description: 
The DO statement, CASE clause, causes execution of one of several cases 
(sequences of statements), based on the value of an arithmetic expression. 
Format: 
[label:] DO CASE exp; 
Parameters: 
exp    any arithmetic expression or variable. 
Rules: 
1.  The statements following the DO CASE statement must be a series of cases; 
    i.e., statement sequences beginning with a CASE statement.  These cases 
    constitute a DO group, which must be terminated by an END statement. 
2.  The CASE group with a constant list that contains an arithmetic constant 
    matching the value of exp is executed; then, control passes to the 
    statement following the entire DO group. 
3.  If the value of the exp does not match a CASE group and a CASE (ELSE) 
    group is present, control will be transferred to the CASE (ELSE) group; 
    otherwise, control passes to the statement following the entire DO group. 
4.  If control is transferred to a labeled statement within a CASE group (by a 
    GOTO statement), the statement is executed.  Execution continues through 
    the DO CASE group until the CASE/END statement is encountered.  At that 
    point, control passes to the statement following the entire DO group. 
5.  The difference between maximum and minimum case values within one DO CASE 
    construct must not exceed 1024. 
Cross Reference: 
See the description of the CASE statement. 
Example: 
    DCL GTP UBIN; 
          DO CASE(GTP); 
           CASE(0); 
             K=K+1; 
           CASE(1,3,5); 
             K=K-1; 
             J=J-1; 
           CASE(2,4,ELSE); 
             K=99; 
           END; 
00003
00004
00001
00002
DO_TO_DOWNTO_BY
Description: 
The DO statement, INHIBIT clause, delimits the start of a DO group that 
contains inhibited code. 
Format: 
[label:] DO INHIBIT; 
Rules: 
1.  All instructions in the DO group will have the inhibit bit (bit 28 of the 
    instruction word) set to a 1. 
2.  Code reached dynamically as a result of a CALL or a branch from within a 
    DO INHIBIT group to outside a DO INHIBIT group is not guaranteed to be 
    inhibited. 
3.  The statements following the DO statement constitute a DO group.  This 
    group must be terminated by an END statement. 
4.  Care should be taken not to inhibit large blocks of code as the operating 
    system will fault the program after a time threshold has been exceeded. 
00001
Description: 
The DO statement, SELECT clause, causes execution of one of several sequences 
of statements based on the value of a UBIN, SBIN, BIT, or CHAR variable or 
expression. 
Format: 
[label:] DO SELECT exp; 
Parameters: 
exp    any UBIN, SBIN, BIT, or CHAR variable or expression. 
Rules: 
1.  The statements following the DO SELECT statement must be SELECT 
    statements.  This sequence, starting with the first SELECT statement, 
    constitutes a DO group which must be terminated by an END statement. 
2.  The SELECT group with a constant list that contains a UBIN, SBIN, BIT, or 
    CHAR constant matching the value of exp is executed; then, control passes 
    to the statement following the entire DO group. 
3.  If the value of the exp does not match a SELECT group and a SELECT (ELSE) 
    group is present, control will be transferred to the SELECT (ELSE) group; 
    otherwise, control passes to the statement following the entire DO group. 
4.  If control is transferred to a labeled statement within a SELECT group (by 
    a GOTO statement), the statement is executed.  Execution then proceeds 
    exactly as it would have if entered through the SELECT statement. 
Example: 
    MUCH_STRANGENESS: PROC ALTRET; 
    DCL STRING CHAR (20); 
    DCL BITSTR BIT (3); 
    DCL T1 UBIN; 
    DCL T2 UBIN; 
       DO SELECT (STRING); 
        SELECT ('Zeke Brenner', 'Raoul Duke');        T1=0; 
        SELECT ('Zonker Harris', 'Lacey Davenport'); T1=1; 
        SELECT ('B.D.',ELSE);                       T1=2; 
        END; 
       DO SELECT (BITSTR); 
        SELECT ('001'B); T2=0; 
        SELECT ('010'B); T2=1; 
        SELECT (ELSE);   T2=2; 
        SELECT ('100'B); T2=3; 
       END; 
       IF T1 > T2 
         THEN RETURN; 
         ELSE ALTRETURN; 
    END MUCH_STRANGENESS; 
Cross Reference: 
See the description of the SELECT statement. 
00004
00003
00001
00002
DO
Description: 
The DO statement, TO/DOWNTO/BY clause, delimits the start of a DO group; 
causes the statements of the DO group to be repeatedly executed based on the 
value of a control variable. 
Format: 
[label:] DO arithvar = exp1 {TO    } exp2 [BY exp3]; 
                            {DOWNTO} 
Parameters: 
arithvar    non-based, non-subscripted arithmetic scalar variable. 
exp1    initial value expression. 
exp2    limit value expression. 
exp3    increment value expression. 
Rules: 
1.  The statements following the DO statement constitute a DO group.  This 
    group must be terminated by an END statement. 
2.  The statements of the group will be executed 0 or more times, with a 
    different value of the control variable, arithvar, for each iteration. 
    The initial value will be exp1. 
3.  The limit test made before each loop execution depends on whether TO or 
    DOWNTO was specified.  Note that exp2 will be re-evaluated for each loop 
    limit test. 
    Statement         Condition           Control goes to 
    ---------         ---------           --------------- 
    DO...TO           arithvar<=exp2      first statement of the group 
                      arithvar> exp2      exit - to END of group 
    DO...DOWNTO       arithvar>=exp2      first statement of the group 
                      arithvar< exp2      exit - to END of group 
4.  The increment value, exp3, will also be re-evaluated for each loop 
    iteration, and will be added to arithvar before the second and any 
    subsequent executions of the group.  If omitted, the default value of exp3 
    depends on whether TO or DOWNTO was specified. 
    Statement         Default              Restriction 
    ---------         -------              ----------- 
    DO...TO           BY +1;               exp3 > 0 
    DO...DOWNTO       BY -1;               exp3 < 0 
5.  The value of arith-var is not defined after normal termination of the 
    group (by rule 3 above). 
6.  When control is transferred from inside the DO group to a statement 
    outside the DO group, the value of arithvar is the value that was attained 
    when the GOTO was encountered. 
7.  A transfer of control (GOTO) to a statement within a DO/TO/BY or 
    DO/DOWNTO/BY group from outside that group is not valid, and causes 
    unpredictable results. 
Example: 
    DO I=0 TO 10 BY 2; 
        . 
        . 
        . 
       END; 
    DO J=10 DOWNTO -5 BY -2; 
        . 
        . 
        . 
       END; 
    DO K=M TO N; 
        . 
        . 
        . 
        END; 
00003
00001
00002
Description: 
The DO statement, UNINHIBIT clause, delimits the start of a DO group that 
contains code to be executed with interrupts permitted. 
Format: 
[label:] DO UNINHIBIT; 
Rules: 
1.  The statements following the DO statement constitute a DO group.  This 
    group must be terminated by an END statement. 
2.  All instructions within the DO group will allow normal interrupt 
    processing.  (They will have the inhibit bit set to 0.)  The UNINHIBIT has 
    no effect outside of the scope of a DO INHIBIT group. 
Example: 
    DO INHIBIT; 
       DO WHILE(EXP);     /* Loop condition test is inhibited        */ 
          DO UNINHIBIT; 
              . 
              . 
              .          /*Code may be interrupted here              */ 
             END; 
          END; 
       END; 
00002
00001
Description: 
The DO statement, UNTIL clause, delimits the start of a DO group; indicates 
that the DO group is to be executed repeatedly until the conditional 
expression becomes true. 
Format: 
[label:] DO UNTIL exp; 
Parameters: 
exp    any bit-string or truth-value expression. 
Rules: 
1.  The statements following the DO statement constitute a DO group.  This 
    group must be terminated by an END statement. 
2.  Execution of a DO UNTIL group proceeds as follows: 
    a.  The statements following the DO UNTIL statement are executed. 
    b.  When control reaches the END statement, the value of the UNTIL 
        expression is computed.  If the value of the expression is true, then 
        control passes to the first statement after the group's END statement. 
        Otherwise, control returns to the first statement after the DO UNTIL 
        statement. 
3.  The differences between DO UNTIL and DO WHILE are as follows: 
    DO UNTIL                        DO WHILE 
    --------                        -------- 
    The statements in the loop      The statements in the loop might not 
    will be executed at least       be executed at all. 
    once. 
    The true condition causes       The true condition causes the 
    exit from the loop.             statements in the loop to be 
                                    executed. 
    At loop termination, the        At loop termination, the WHILE 
    UNTIL condition is true.        condition is false. 
           ***** Graphic CE44G_09_01.:MANUALS to be placed here. ***** 
     4.  Because the body of a DO UNTIL loop is always executed at least 
                              once, the statement DO 
      UNTIL (exp); is not the same as DO WHILE (NOT (exp));.  Also note that 
            DO WHILE (exp); is not the same as DO UNTIL (NOT (exp));. 
                            ~*B* CROSS_REFERENCE: 
Cross Reference: 
See the description of the DO Statement, WHILE clause. 
00001
00002
Description: 
The DO statement, WHILE clause, delimits the start of a DO group; indicates 
that the DO group is to be executed repeatedly, as long as the WHILE 
expression remains true. 
Format: 
[label:] DO WHILE exp; 
Parameters: 
exp    any bit-string or truth-value expression. 
Rules: 
1.  The statements following the DO statement constitute a DO group.  This 
    group must be terminated by an END statement. 
2.  Execution of a DO WHILE group proceeds as follows: 
    a.  When control is passed to the DO WHILE statement, the value of the 
        WHILE expression is computed.  If the value of the expression is 
        false, then control passes to the first statement after the group's 
        END statement.  Otherwise, control passes to the first statement after 
        the DO WHILE statement. 
    b.  When control reaches the END statement, control is passed to the DO 
        WHILE statement. 
3.  A GOTO statement can transfer control to a labeled statement within a DO 
    WHILE group from outside of that group.  If and when the END of the DO 
    WHILE group is encountered, control returns to the DO WHILE statement. 
    However, this is not good programming practice and it is discouraged. 
Example: 
    DO WHILE ((3*X-5)<9); 
       I=I+1; 
       CALL FACT (X, I); 
       END; 
The procedure FACT changes the value of X.  When (3*X - 5) is not less than 9, 
execution of the DO group will be terminated. 
Cross Reference: 
See the description of the DO Statement, UNTIL clause. 
00004
00003
00001
00002
Description: 
Declares an identifier as a descriptor variable. 
Format: 
DCL id DSCR a1 [a2]... ; 
Parameters: 
id    any valid identifier. 
a1,a2...    any valid attribute. 
Rules: 
1.  The identifier may be a scalar variable, an array name, or a structure 
    element.  It is declared as descriptor-type data.  The value of a 
    descriptor variable uniquely identifies a storage location (if it is not 
    null). 
2.  Descriptor-type data may be used only to qualify a reference to based data 
    or as the source or target of an assignment statement.  No implicit 
    conversions may be performed between descriptor data and numeric, 
    character, or pointer data types. 
3.  DSCR assignment will be done via LDD/STD instructions.  This means that 
    the data being assigned must be valid descriptor data and that the user 
    must have the proper access to the data to avoid faults. 
4.  DSCR data may be assigned to a BIT (72) DALIGNED item. 
5.  The PTRDSCR and VECTDSCR functions may be used to get special descriptor 
    information. 
6.  A descriptor variable may not be initialized with the INIT attribute. 
7.  DSCR variables are always DALIGNED and always require 72 bits. 
Cross Reference: 
See the BASED attribute and the PTRDSCR, VECTDSCR, DBASE, DBOUND and DTYPE 
builtin functions. 
00004
00001
00002
00003
Description: 
The DTYPE built-in function allows access to the type field of the referenced 
descriptor. 
Format: 
DTYPE(desc-ref) 
Parameters: 
desc-ref    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted descriptor reference. 
Rules: 
1.  DTYPE represents a UBIN(4) value. 
2.  The compiler will never generate an LDD or STD instruction to access the 
    referenced descriptor for this function.  Therefore, the descriptor must 
    be accessible to the program via non-NSA instructions. 
3.  The DTYPE built-in function may be used as a target pseudo-variable on the 
    left hand side of an assignment statement.  The evaluated expression must 
    be an arithmetic expression. 
00001
00002
00003
Description: 
The EDITCHAR built-in subroutine moves an unsigned digit character string, 
under control of a micro-operation sequence, to a target string. 
Format: 
CALL EDITCHAR (tostr, [start], [len], mopstr, fromstr); 
Parameters: 
tostr    any character location reference. 
fromstr    any character expression. 
mopstr    any character or bit expression. 
start, len    any arithmetic expression. 
Rules: 
1.  tostr represents the destination string and must be of data type CHAR. 
2.  The starting position and length defined by start and len are used to 
    define the field of tostr to receive the edited data.  Legal values for 
    start are defined as follows: 
        0 <= start < LENGTHC (tostr) 
    Legal values for len are defined as: 
        1 <= len <= LENGTHC (tostr) - start <= 63 
3.  mopstr represents the micro-operation sequence string and must be of CHAR 
    or BIT data type.  The length of mopstr must be within the range defined 
    as: 
        1 <= LENGTHC (mopstr) <= 63 
4.  fromstr represents the source string and must be of data type CHAR.  The 
    length of fromstr must be within the range defined as: 
        1 <= LENGTHC (fromstr) <= 63 
    fromstr can only contain digit characters or the results are undefined. 
5.  For a detailed definition of the micro-operation sequence, see the GMAP6 
    assembly instructions manual (DH03) section on Micro Operations for Edit 
    Instructions. 
6.  Arguments start and len are optional.  If start is omitted, a default of 0 
    is used.  If len is omitted, a default value of (LENGTHC(tostr)-start) is 
    used. 
00001
00002
Description: 
The EDITSTR built-in subroutine moves a character string under control of a 
micro-operation sequence to a target string. 
Format: 
CALL EDITSTR (tostr, [start], [len], mopstr, fromstr); 
Parameters: 
tostr    any character location reference. 
fromstr    any character expression. 
mopstr    any character or bit expression. 
start, len    any arithmetic expression. 
Rules: 
1.  tostr represents the destination string and must be of data type CHAR. 
2.  The starting position and length are used to define the field of tostr to 
    receive the edited data.  Legal values for start are defined as follows: 
        0 <= start < LENGTHC (tostr) 
    Legal values for len are defined as follows: 
        1 <= len <= LENGTHC (tostr) - start <= 63 
3.  mopstr represents the micro-operation sequence string and must be of CHAR 
    or BIT data type.  The length of mopstr must be within the range defined 
    as: 
        1 <= LENGTHC (mopstr) <= 63 
4.  fromstr represents the source string and must be of data type CHAR.  The 
    length of fromstr must be within the range defined as: 
        1 <= LENGTHC (fromstr) <= 63 
5.  For a detailed definition of the micro-operation sequence see the GMAP6 
    assembly instructions (DH03) manual section on Micro Operations for Edit 
    Instructions. 
6.  Arguments start and len are optional.  If start is omitted, a value of 0 
    is used.  If len is omitted, a value of (LENGTHC(tostr)-start) is used. 
00001
00002
Description: 
The EDITXCHAR built-in subroutine moves a signed digit character string under 
control of a micro-operation sequence to a target string. 
Format: 
CALL EDITXCHAR (tostr, [start], [len], mopstr, fromstr); 
Parameters: 
tostr    any character location reference. 
fromstr    any character expression. 
mopstr    any character or bit expression. 
start, len    any arithmetic expression. 
Rules: 
1.  tostr is the character location reference which specifies the destination 
    of the string, and must be of data type CHAR. 
2.  The starting position and length are used to define the field of tostr to 
    receive the edited data.  Legal values for start are defined as follows: 
        0 <= start < LENGTHC (tostr) 
    Legal values for len are defined as: 
        1 <= len <= LENGTHC (tostr) - start <= 63 
3.  mopstr represents the micro-operation sequence string and must be of CHAR 
    or BIT data type.  The length of mopstr must be within the range defined 
    as: 
        1 <= LENGTHC (mopstr) <= 63 
4.  fromstr represents the source string and must be of data type CHAR.  The 
    length of fromstr must be within the range defined as: 
        2 <= LENGTHC (fromstr) <= 63 
    fromstr must start with either a '+' or '-' character followed by digit 
    characters or the result is undefined. 
5.  For a detailed definition of the micro-operation sequence, see the GMAP6 
    assembly instructions manual (DH03) section on Micro Operations for Edit 
    Instructions. 
6.  Arguments start and len are optional.  If start is omitted, a value of 0 
    is used.  If len is omitted, a value of (LENGTHC(tostr)-start) is used. 
00001
00002
Description: 
%EJECT causes a page eject in the listing output. 
Format: 
%EJECT; 
Rules: 
1.  The %EJECT directive must be on a single line. 
2.  The %EJECT will not be honored if the listing is currently disabled by one 
    of the lisiting directives. 
00001
IF
IF_PREPROC
Description: 
The END statement delimits the end of a procedure or a DO group. 
Format: 
[label:] END [id]; 
Parameters: 
id    the label prefix that appears on the corresponding DO statement or PROC 
statement. 
Rules: 
1.  An END statement terminates the most recent previous DO group or procedure 
    for which a corresponding END statement has not been encountered. 
2.  The execution of an END statement delimiting a procedure has the same 
    effect as execution of a RETURN statement. 
Example: 
    AA:     PROC; 
    AA1:       PROC; 
    LAB:       DO; 
                  END LAB; 
               END; 
    END AA; 
00003
00001
00002
IF_PREPROC
Description: 
The ENTADDR built-in function generates a value representing the entry point 
of an external procedure.  The ENTADDR value may be assigned to an EPTR 
variable. 
Format: 
ENTADDR(id) 
Parameters: 
id    the name of an external procedure entry point or NIL. 
Rules: 
1.  The only valid contexts for ENTADDR are: 
    a.  On the right-hand side of an assignment statement whose left-hand side 
        is an EPTR variable. 
    b.  In the INIT attribute of an EPTR variable. 
    c.  In a relational expression whose operator is either = or ~=, and whose 
        other operand is either another reference to ENTADDR, or is an EPTR 
        variable. 
2.  ENTADDR (NIL) evaluates to the null entry value. 
00001
00002
Description: 
The ENTRY statement names and defines a secondary entry point in a procedure; 
specifies the parameters to be received, if any. 
Format: 
entryname:  ENTRY [ASYNC                            ] [ALTRET]; 
                  [(parameterlist                  )] 
Parameters: 
parameterlist    a list of identifiers separated by commas. 
Rules: 
1.  The ENTRY statement must be immediately contained in the procedure for 
    which it defines a secondary entry point.  It must not be mixed with DCL 
    statements or nested within any control constructs such as IF or DO. 
2.  Every parameter appearing in a secondary entry point parameter list must 
    also appear in the PROC statement parameter list.  The parameters in both 
    lists must be in the same order, and both lists must be identical up to 
    and including the last parameter in the secondary entry point parameter 
    list.  In other words, the parameter list at the secondary entry point 
    must be the same as, or a "left subset" of, the parameter list at the main 
    entry point. 
3.  A procedure must not have a flow of control such that reference is made to 
    a parameter which was not included in the parameter list of the ENTRY 
    statement through which the procedure was entered. 
4.  The specification of ALTRET on the ENTRY statement must match that of the 
    corresponding PROC statement. 
5.  When an ENTRY statement is encountered by control, it is skipped, and 
    control passes to the following statement. 
6.  The specification of ASYNC on the ENTRY statement must match that of the 
    corresponding PROC statement. 
7.  An ENTRY statement is illegal in an external procedure that specifies 
    MAIN.  It is legal in internal procedures within a MAIN procedure. 
Example: 
    X:      PROC (A, B) ALTRET; 
      DCL A CHAR(1); 
      DCL B CHAR(2); 
    Y:      ENTRY (A, B) ALTRET; 
    Z:      ENTRY (A); 
    XIT:   RETURN; 
    ABNORMAL: ALTRETURN; 
    END X; 
00003
00001
00002
Description: 
The ENTRY attribute declares an identifier as an entry name constant. 
Format: 
DCL id ENTRY [(n)]; 
Parameters: 
id    any valid identifier. 
n    number of parameters expected. 
Rules: 
1.  The appearance of an identifier as an entry name constant prefix to a PROC 
    or ENTRY statement of a procedure constitutes an implicit declaration of 
    that identifier as having the ENTRY attribute.  The identifier is known 
    within that procedure and its contained procedures. 
2.  An identifier that is used in a given block to refer to an entry point for 
    an external procedure must be declared with the ENTRY attribute, 
    implicitly or explicitly, in that block or in a containing block. 
3.  The constant n gives the maximum number of parameters which may be passed 
    in a CALL. The default is zero. 
4.  The declaration of the ENTRY attribute in explicit form is required to 
    declare an entry point of an external procedure in other external 
    procedures which are to invoke it.  The PROC or ENTRY statement 
    declaration and all DCL statement declarations of the same name are linked 
    and establish the scope and the attributes of the entry name. 
5.  If BASED is specified along with entry, the id is defined as a dummy for 
    use as the target of a CALL statement using the THRU option. 
Example: 
    DCL BB ENTRY(1); 
    DCL E ENTRY (3) ALTRET; 
          CALL BB (99); 
          CALL E (1, 2) ALTRET(ERR); 
Cross Reference: 
See the OPTIONAL, CONV, ALTRET and ASYNC attributes. 
00004
00003
00001
00002
Description: 
%EOD indicates the end of an external procedure in a batch compile. 
Format: 
%EOD; 
Rules: 
1.  When the %EOD directive is encountered, the preprocessor state is 
    discarded, and the default state is restored.  Any %SUBs, %SETs, and 
    %MACROs needed for a subsequent external procedure must be defined again 
    in that procedure. 
2.  The %EOD directive must be on a single line. 
Example: 
    FIRST_ONE: PROC; 
    %SET LISTEXP = '1'B; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %SUB SUB_ID = ODD_NUMBER; 
    %SET SET_ID = 123; 
    %MACRO MACRO_ID; 
    DCL 1 STRUCTURE, 
          2 POSITION UBIN, 
          2 CONTENTS CHAR (20), 
          2 NEXT$ PTR; 
    %MEND; 
    %MACRO_ID; 
    DCL SUB_ID UBIN; 
    SUB_ID = %SET_ID; 
    STRUCTURE.POSITION = 1; 
    STRUCTURE.CONTENTS = 'STUFF'; 
    STRUCTURE.NEXT$ = ADDR(NIL); 
    END FIRST_ONE; 
    %EOD; /* Discard preprocessor state created by this external procedure. */ 
    SECOND_ONE: PROC; 
    /* Listing directives are reset because the %EOD has discarded the 
       effects of the listing directives of previous external procedure. */ 
    %SET LISTEXP = '1'B; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %SUB SUB_ID = EVEN_NUMBER; /* Compare to %SUB SUB_ID in FIRST_ONE. */ 
    %SET SET_ID = 124; /* Compare this to %SET SET_ID in FIRST_ONE. */ 
    %MACRO MACRO_ID; 
    DCL 1 TREE, 
          2 DEPTH UBIN, 
          2 CONTENTS CHAR (20), 
          2 RIGHT$ PTR, 
          2 LEFT$ PTR; 
    %MEND; 
    %MACRO_ID; 
    DCL SUB_ID UBIN; 
    SUB_ID = %SET_ID; 
    TREE.DEPTH = 1; 
    TREE.CONTENTS = 'CHERRIES'; 
    TREE.RIGHT$ = ADDR(NIL); 
    TREE.LEFT$ = ADDR(NIL); 
    END SECOND_ONE; 
The preceding source produces the following listing output: 
    FIRST_ONE: PROC; 
    %SET LISTEXP = '1'B; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %SUB SUB_ID = ODD_NUMBER; 
    %SET SET_ID = 123; 
    %MACRO MACRO_ID; 
    DCL 1 STRUCTURE, 
          2 POSITION UBIN, 
          2 CONTENTS CHAR (20), 
          2 NEXT$ PTR; 
    %MEND; 
    %MACRO_ID; 
    DCL 1 STRUCTURE, 
          2 POSITION UBIN, 
          2 CONTENTS CHAR (20), 
          2 NEXT$ PTR; 
    DCL ODD_NUMBER UBIN; 
            ODD_NUMBER = 123; 
            STRUCTURE.POSITION = 1; 
            STRUCTURE.CONTENTS = 'STUFF'; 
            STRUCTURE.NEXT$ = ADDR(NIL); 
    END FIRST_ONE; 
    %EOD;     /* Discard preprocessor state created by this external 
                 procedure.   */ 
    SECOND_ONE: PROC; 
    /* Listing directives are reset because the %EOD has discarded 
       the effects of the listing directives of the previous 
       external procedure. */ 
    %SET LISTEXP = '1'B; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %SUB SUB_ID = EVEN_NUMBER; /* Compare to %SUB SUB_ID in FIRST_ONE. */ 
    %SET SET_ID = 124; /* Compare this to %SET SET_ID in FIRST_ONE. */ 
    %MACRO MACRO_ID; 
    DCL 1 TREE, 
          2 DEPTH UBIN, 
          2 CONTENTS CHAR (20), 
          2 RIGHT$ PTR, 
          2 LEFT$ PTR; 
    %MEND; 
    %MACRO_ID; 
    DCL 1 TREE, 
          2 DEPTH UBIN, 
          2 CONTENTS CHAR (20), 
          2 RIGHT$ PTR, 
          2 LEFT$ PTR; 
    DCL EVEN_NUMBER UBIN; 
            EVEN_NUMBER = 124; 
            TREE.DEPTH = 1; 
            TREE.CONTENTS = 'CHERRIES'; 
            TREE.RIGHT$ = ADDR(NIL); 
            TREE.LEFT$ = ADDR(NIL); 
    END SECOND_ONE; 
00002
00001
Description: 
The EPTR attribute specifies that the variable so declared is used as an entry 
variable.  It is then dynamically assigned the values of the entry points of 
external procedures. 
Format: 
DCL id [a1 [a2] ... ] EPTR; 
Parameters: 
id    any identifier. 
a1,a2    any valid attributes. 
Rules: 
1.  An EPTR variable may be a scalar, an array, or a member of a structure. 
2.  An EPTR variable may have (or be a member of a structure having) any 
    storage class. 
3.  An EPTR variable may only assume the values of entry points of external 
    procedures. 
4.  An EPTR variable occupies 36 bits, and is word-aligned by default. 
Example: 
    DCL E EPTR; 
          IF E ~= ENTADDR(NIL) THEN 
             CALL E; 
Cross Reference: 
See the ENTADDR built-in function. 
00004
00003
00001
00002
SET_EQU_LSET
Description: 
%ERROR allows the user to create diagnostic messages. 
Format 
%ERROR ([exp1, ] exp2 [, exp3]); 
Parameters: 
exp1     is a preprocessor bit string expression. 
exp2     is a preprocessor character string expression. 
exp3     is a preprocessor SBIN expression. 
Rules: 
1.  If the bit string expression is included, it is evaluated.  If the bit 
    string expression is all 0 bits, %ERROR processing is stopped at this 
    point.  Note that, if the bit string expression is omitted, it is not 
    correct to denote its absence by a comma.  The preprocessor will determine 
    whether the first expression specified is bit or character, by evaluating 
    the expression and determining the data type of the result. 
2.  The character string expression is evaluated, and the value is used for 
    the text of a diagnostic message that is output to the source listing. 
    The length of the character string, which results from the character 
    string expression, must be less than or equal to 92 characters.  The 
    message is also output to the diagnostic file (if different from the 
    listing). 
3.  The default severity level of the diagnostic is that of a preprocessor 
    warning (severity 2).  If the optional SBIN expression is specified, the 
    legal values are 0-4.  These values correspond to the severity level that 
    is displayed in the error message.  A severity level of 4 will cause the 
    compiler to terminate the compilation after the preprocessor phase. 
4.  The following table maps the %ERROR severity level to the severity level 
    in the object unit, if one is being produced: 
        SEVERITY                          OU_SEVERITY 
        0(NWARN specified)                     0 
        0(WARN specified)                      2 
        1(non-suppressible warning)            4 
        2(minor error)                         7 
        3(serious error)                      11 
        4(fatal error)                        15 
5.  The %ERROR directive is usually used within a macro to verify the validity 
    of parameters which are being passed at the time of a macro invocation. 
Example: 
    ERRARE_HUMANUM_EST: PROC; 
    %LIST; 
    DCL RESULT SBIN; 
    DCL NUMBER SBIN; 
    DCL FACTOR UBIN; 
    NUMBER = 127; 
    %MACRO MULTIPLY (FACTOR = 1); 
    %ERROR (FACTOR < 1, 'FACTOR MUST BE GREATER THAN 0.', 2); 
    RESULT = NUMBER * FACTOR; 
    %MEND; 
    %MULTIPLY (FACTOR = -1); 
    %MULTIPLY (FACTOR = 10); 
    END ERRARE_HUMANUM_EST; 
The preceding source produces the following listing output: 
    ERRARE_HUMANUM_EST: PROC; 
    %LIST; 
    DCL RESULT SBIN; 
    DCL NUMBER SBIN; 
    DCL FACTOR UBIN; 
    NUMBER = 127; 
    %MACRO MULTIPLY (FACTOR = 1); 
    %ERROR (FACTOR < 1, 'FACTOR MUST BE GREATER THAN 0.', 2); 
    RESULT = NUMBER * FACTOR; 
    %MEND; 
    %MULTIPLY (FACTOR = -1); 
    %ERROR (FACTOR < 1, 'FACTOR MUST BE GREATER THAN 0.', 2); 
     ** ZQC-00041-2        FACTOR MUST BE GREATER THAN 0. 
    RESULT = NUMBER * FACTOR; 
    %MULTIPLY (FACTOR = 10); 
    %ERROR (FACTOR < 1,, 'FACTOR MUST BE GREATER THAN 0.', 2); 
    RESULT = NUMBER * FACTOR; 
    END ERRARE_HUMANUM_EST; 
00003
00001
00002
Description: 
The EXIT statement provides a structured way for exiting from within a DO 
block. 
Format: 
EXIT [label] ; 
Rules: 
1.  When the EXIT statement is used without a label, control is returned to 
    the statement immediately following the end of the innermost DO block 
    currently in control. 
2.  When the EXIT statement is used with the label clause, control will be 
    transferred to the statement immediately following the end of the DO block 
    headed by a DO statement with the specified label.  This statement cannot 
    be used at a point which is not within the scope of a DO block with the 
    specified label. 
3.  The EXIT statement can only be executed within the execution scope of a 
    DO. 
4.  An EXIT statement cannot be used to EXIT from an internal or external 
    procedure.  Instead, use the RETURN statement. 
Example: 
    SELECTOR:   PROC (STR1, STR2); 
    DCL STR1 CHAR (80); 
    DCL STR2 CHAR (80); 
    DBK:  DO SELECT (STR1); 
             SELECT ('NOP', 'NIL', 'ZERCH', 'ZZZZ'); 
                STR2 = STR1; 
             SELECT ('BLOT', 'SMEAR'); 
                SUBSTR (STR2, 3, 2) = '<>'; 
                IF SUBSTR (STR2, 5, 1) = '?' 
                  THEN EXIT DBK; 
                STR1 = 'XXX'; 
             SELECT (ELSE); 
                STR2 = ' '; 
          END DBK; 
       RETURN; 
    END SELECTOR; 
00002
00001
EXT_EXTROOT
Description: 
The EXT/EXTROOT attribute specifies that an identifier may be referenced 
outside its declaring procedure. 
Format: 
DCL id a1 [a2] ... {EXT    }; 
                   {EXTROOT} 
Parameters: 
id    any valid identifier. 
a1,a2    any valid attributes. 
Rules: 
1.  EXT or EXTROOT may be used when it is desired to have the same name 
    (declared identifier) known in two or more disjoint procedures. 
2.  A name declared as EXT or EXTROOT is known in all procedures in which the 
    same name is declared with the EXT or EXTROOT attribute and in all 
    contained procedures, except those procedures in which the name is 
    declared without the EXT or EXTROOT attribute. 
3.  In all the EXT or EXTROOT declarations for the same identifier, all 
    attributes declared must be consistent, since all the declarations refer 
    to the same storage location. 
4.  EXT or EXTROOT may be specified only for level 1 names. 
5.  When a major structure is declared as EXT or EXTROOT in more than one 
    procedure: 
    a.  Attributes of structure members must be the same in each case although 
        the corresponding names of members do not have to be identical. 
    b.  Members of structures have the internal attribute and are not declared 
        with any scope attribute.  However, a reference to a member of an EXT 
        or EXTROOT structure, using the name known to the procedure containing 
        the reference to that member, is a reference to the corresponding 
        member in all procedures having the EXT or EXTROOT structure 
        declaration, whether or not the corresponding member names are 
        identical. 
6.  Entry names of external procedures always have the implied attribute of 
    EXT. 
7.  The EXT or EXTROOT attribute causes identifiers of the same name in two or 
    more external procedures to refer to the same data after linking, and that 
    data is allocated for the entire execution of the program. 
8.  EXT and EXTROOT are equivalent with the following exception:  when a 
    program is organized into overlays, an identifier having at least one DCL 
    using EXTROOT will have its storage located in the program root, 
    regardless of where the DCLs are encountered within the overlay structure. 
    Thus, the value of a variable that is declared EXTROOT is guaranteed to be 
    retained between PROC invocations, regardless of possible intervening 
    overlay operations. 
9.  Multiple occurrences of an EXT/EXTROOT variable may be initialized.  The 
    resulting value is indeterminate. 
10. If all DCLs for an identifier specify EXT (and not EXTROOT), then the 
    location of that identifier need not be in the root of an overlay 
    structure.  (The storage may be allocated in the root, however, depending 
    on where the DCLs are encountered within the overlay structure.)  When an 
    overlay operation occurs, an EXT variable may have its value restored to 
    the program-load INIT value. 
11. If care is exercised, EXT/EXTROOT can allow the user to access FORTRAN 
    common blocks. 
00001
00002
BUILT_IN
Description 
The GOTO statement controls the normal sequence of statement execution by 
specifying the next statement to be executed. 
Format 
[label:] GOTO id; 
Parameters: 
id    a label. 
Rules: 
1.  The GOTO label must be immediately contained in the same procedure as the 
    GOTO statement. 
2.  When the GOTO statement is executed, control is transferred to the 
    statement with the label prefix that is referenced. 
Example: 
    GOTO ABORT_LABEL; 
    GOTO RESTART; 
00003
00001
00002
Description: 
The HALF attribute is used with SBIN or UBIN to specify that a binary integer 
occupies 18 bits. 
Format: 
DCL id {UBIN} HALF; 
       {SBIN} 
Parameters: 
id    any valid identifier. 
Rules: 
1.  SBIN HALF defines id to be a binary integer with a precision of 17 bits 
    plus a sign bit. 
2.  UBIN HALF defines id to be a binary integer with a precision of 18 bits. 
Cross Reference: 
See SBIN and UBIN Attributes. 
00003
00001
00002
ALIGNMENT
The PL6 HELP facility provides on-line documentation of PL6.  HELP issues 
messages in response to the user's request for information.  The PL6 HELP 
contains the description, format, parameters and rules of the PL6 statements, 
attributes, built-in functions and subroutines as well as the PL6 preprocessor 
facility.  In some cases, examples are also given.  Information on the format 
facility, system format facility as well as compiler options and invocation of 
the PL6 compiler is also available. 
When requesting information, the first word of a statement or clause is 
usually sufficient to identify it; the second word is also necessary in cases 
where more than one topic begins with the same word.  When in doubt, use the 
most complete form.  Always separate words with an underscore (_) when 
requesting topics with more than one word. 
To obtain more HELP information: 
HELP (PL6) TOPICS       prints a list of all available HELP messages 
HELP (PL6) statement    prints the syntax of a statement 
HELP (PL6) STATEMENT    explains the use of statements in PL6 programs 
HELP (PL6) ATTRIBUTES   explains the use of attributes in PL6 programs 
HELP (PL6) PREPROCESSOR explains the use of preprocessor directives 
                        in PL6 programs 
HELP (PL6) BUILT_IN     explains the use of built-in subroutines 
                        and function in PL6 programs 
?                       means give the next level of HELP message 
??                      means give all levels of the current message 
A 
  ADDR built-in function - 
      HELP INIT RULES: 
      HELP VECTOR_ATTRIB RULES: 
      HELP ADDR 
  ALIGNED attribute - 
      HELP ALIGNMENT 
      HELP ALIGNMENT RULES: 
  Alignment attributes - 
      HELP ALIGNMENT 
  ALIGNMENT Attributes:  ALIGNED, UNAL, Et Al. - 
      HELP ALIGNMENT 
  ALTRET - 
      HELP CALL RULES: 
  ALTRET attribute - 
      HELP ENTRY RULES: 
      HELP ALTRET 
      HELP ALTRET CROSS_REFERENCE: 
  ALTRET clause - 
      HELP INDEX1R RULES: 
      HELP SEARCH RULES: 
      HELP SEARCHR RULES: 
  ALTRET option - 
      HELP ALTRET CROSS_REFERENCE: 
      HELP CONV RULES: 
  ALTRETURN statement - 
      HELP PROC RULES: 
      HELP RETURN_ALTRETURN RULES: 
  ALTSHARELIB option - 
      HELP OPTIONS ALTSHARELIB 
  AREADEF Attribute - 
      HELP AREADEF 
  AREAREF Attribute - 
      HELP ALIGNMENT RULES: 
      HELP AREAREF 
      HELP READONLY RULES: 
      HELP KEYWORDS 
  AREAREF storage type - 
      HELP PROC_MATERIALIZE PARAMETERS: 
  array - 
      HELP DCL RULES: 
      HELP INIT RULES: 
  array declarations - 
      HELP AREAREF RULES: 
  array name - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  array table - 
      HELP STORAGE_LAYOUT_FOR_ARRAYS 
  ASCBIN Built-In Function - 
      HELP ASCBIN 
  ASCBIN Preprocessor Function - 
      HELP ASCBIN_PREPROC 
  ASCBIT Built-In Function - 
      HELP ASCBIT 
  ASCBIT Preprocessor Function - 
      HELP ASCBIT_PREPROC 
  ASCII character - 
      HELP BINASC DESCRIPTION: 
  ASCII codes - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  Assignment Statement - 
      HELP ASSIGNMENT 
  ASYNC attribute - 
      HELP ENTRY RULES: 
      HELP PROC RULES: 
      HELP PROC RULES: 
      HELP ASYNC 
  ASYNC procedure - 
      HELP PROC RULES: 
      HELP RETURN_ALTRETURN RULES: 
      HELP UNWIND RULES: 
      HELP KEYWORDS 
  attribute keyword - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  attributes - 
      HELP DCL RULES: 
      HELP UNWIND RULES: 
      HELP UNWIND RULES: 
      HELP ATTRIBUTES 
      HELP KEYWORDS 
      HELP KEYWORDS 
  AUTO Attribute - 
      HELP ALIGNMENT RULES: 
      HELP AUTO 
      HELP AUTO RULES: 
      HELP BASED RULES: 
      HELP KEYWORDS 
  AUTO storage type - 
      HELP PROC_MATERIALIZE PARAMETERS: 
  AUTO variable - 
      HELP AUTO RULES: 
  automatic storage - 
      HELP AUTO RULES: 
  AUTOTEMP option - 
      HELP OPTIONS AUTOTEMP 
  AVOID clause - 
      HELP PROC PARAMETERS: 
      HELP PROC_AVOID 
B 
  BASED attribute - 
      HELP ALIGNMENT RULES: 
      HELP AUTO RULES: 
      HELP BASED 
      HELP BIT RULES: 
      HELP KEYWORDS 
  BASED data - 
      HELP LENGTHB RULES: 
      HELP SIZEB RULES: 
      HELP SIZEC RULES: 
  BC list option - 
      HELP OPTIONS BC 
  binary integer - 
      HELP WORD RULES: 
      HELP BINBIT DESCRIPTION: 
      HELP CHARBIN DESCRIPTION: 
  BINASC Built-In Function - 
      HELP BINASC 
  BINASC Preprocessor Function - 
      HELP BINASC_PREPROC 
  BINBIT Built-In Function - 
      HELP BINBIT 
  BINBIT Preprocessor Function - 
      HELP BINBIT_PREPROC 
  BINCHAR Built-In Subroutine - 
      HELP BINCHAR 
  BINCHAR Preprocessor Function - 
      HELP BINCHAR_PREPROC 
  BINXCHAR Built-In Subroutine - 
      HELP BINXCHAR 
  BINXCHAR Preprocessor Function - 
      HELP BINXCHAR_PREPROC 
  BIT - 
      HELP INIT RULES: 
  BIT arguments - 
      HELP MINIMUM RULES: 
  BIT Attribute - 
      HELP BIT 
  BIT datum - 
      HELP BITVECT DESCRIPTION: 
  Bit String Preprocessor Expressions - 
      HELP IF_PREPROC PARAMETERS: 
  bit strings - 
      HELP BINBIT DESCRIPTION: 
  BITASC Built-In Function - 
      HELP BITASC 
  BITASC Preprocessor Function - 
      HELP BITASC_PREPROC 
  BITBIN Built-In Function - 
      HELP BITBIN 
  BITBIN Preprocessor Function - 
      HELP BITBIN_PREPROC 
  BITVECT Built-In Function - 
      HELP BITVECT 
  built-in function rules - 
      HELP BUILT_IN 
  built-in functions - 
      HELP INIT PARAMETERS: 
      HELP WORD CROSS_REFERENCE: 
      HELP WORD CROSS_REFERENCE: 
      HELP BUILT_IN 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  Built-in Subroutine - 
      HELP WORD CROSS_REFERENCE: 
  built-in subroutine rules - 
      HELP BUILT_IN 
  BY Clause - 
      HELP DO_TO_DOWNTO_BY DESCRIPTION: 
  BYTE Attribute - 
      HELP BYTE 
C 
  CALIGNED attribute - 
      HELP ALIGNMENT 
      HELP ALIGNMENT RULES: 
  CALL Statement - 
      HELP CALL 
  CASE Clause - 
      HELP DO_CASE DESCRIPTION: 
  CASE group - 
      HELP DO_CASE RULES: 
  CASE Statement - 
      HELP CASE 
      HELP DO_CASE RULES: 
  CASE/ELSE statement - 
      HELP CASE RULES: 
  Changes from the Previous Manual - 
      HELP CHANGES 
  CHAR Attribute - 
      HELP CHAR 
  CHAR string - 
      HELP INIT RULES: 
  CHAR variable - 
      HELP CHAR RULES: 
  character codes - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  characters, special - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  CHARBIN Built-In Subroutine - 
      HELP CHARBIN 
  CHARBIN Preprocessor Function - 
      HELP CHARBIN_PREPROC 
  CHARTEXT Preprocessor Function - 
      HELP CHARTEXT_PREPROC 
  Clause keyword - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  CLIMB instruction - 
      HELP CONV RULES: 
  collating sequence - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  Compiler Invocation - 
      HELP KEYWORDS 
      HELP KEYWORDS 
  Compiler Options - 
      HELP KEYWORDS 
  CONCAT Built-In Subroutine - 
      HELP CONCAT 
  CONCAT Preprocessor Function - 
      HELP CONCAT_PREPROC 
  CONSTANT Attribute - 
      HELP ALIGNMENT RULES: 
      HELP BASED RULES: 
      HELP CONSTANT 
      HELP KEYWORDS 
  CONSTANT variable - 
      HELP CONSTANT RULES: 
  CONV Attribute - 
      HELP CONV 
  COUNT Preprocessor Function - 
      HELP COUNT_PREPROC 
  CP6 option - 
      HELP OPTIONS CP6 
  CPTR Attribute - 
      HELP CPTR 
  CSYS option - 
      HELP OPTIONS CSYS 
D 
  DALIGNED attribute - 
      HELP ALIGNMENT 
      HELP ALIGNMENT RULES: 
  DALIGNED variable - 
      HELP STORAGE_LAYOUT_FOR_ARRAYS 
  data types - 
      HELP INIT RULES: 
  DBASE Built-in Function - 
      HELP DBASE_BUILT_IN_FUNCTION 
  DBOUND Built-in Function - 
      HELP DBOUND_BUILT_IN_FUNCTION 
  DCB - 
      HELP ALIGNMENT RULES: 
      HELP BIT RULES: 
      HELP DCB RULES: 
  DCB attribute - 
      HELP BASED RULES: 
      HELP DCB 
      HELP KEYWORDS 
  DCB data - 
      HELP LENGTHB RULES: 
      HELP SIZEB RULES: 
      HELP SIZEC RULES: 
  DCBADDR Built-In Function - 
      HELP DCBADDR 
  DCBNUM Built-In Function - 
      HELP DCBNUM 
  DCL Statement - 
      HELP DCL 
      HELP DCL RULES: 
      HELP PROC RULES: 
      HELP EXT_EXTROOT RULES: 
      HELP BINBIT RULES: 
  declare statement - 
      HELP ATTRIBUTES 
  default identifier - 
      HELP MACRO_INVOCATION RULES: 
  DIMENSION attribute - 
      HELP DCL RULES: 
      HELP DIMENSION 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  directives, preprocessor - 
      HELP XLATE_9_TO_6 RULES: 
  DMAP option - 
      HELP OPTIONS DMAP 
  DO block - 
      HELP EXIT DESCRIPTION: 
  DO CASE expression - 
      HELP CASE RULES: 
  DO CASE statement - 
      HELP CASE RULES: 
  DO group - 
      HELP DO RULES: 
      HELP DO_SELECT RULES: 
  DO SELECT group - 
      HELP DO_SELECT RULES: 
      HELP SELECT RULES: 
  DO Statement/CASE Clause - 
      HELP DO_CASE 
  DO Statement/INHIBIT Clause - 
      HELP DO_INHIBIT 
  DO Statement/SELECT Clause - 
      HELP DO_SELECT 
  DO Statement/Simple - 
      HELP DO 
  DO Statement/TO/DOWNTO/BY Clause - 
      HELP DO_TO_DOWNTO_BY 
  DO Statement/UNINHIBIT Clause - 
      HELP DO_UNINHIBIT 
  DO Statement/UNTIL Clause - 
      HELP DO_UNTIL 
  DO Statement/WHILE Clause - 
      HELP DO_WHILE 
  DO UNTIL - 
      HELP DO_UNTIL RULES: 
  DO WHILE - 
      HELP DO_UNTIL RULES: 
  DOWNTO Clause - 
      HELP DO_TO_DOWNTO_BY DESCRIPTION: 
  DSCR Attribute - 
      HELP DSCR_ATTRIBUTE 
  DTYPE Built-in Function - 
      HELP DTYPE_BUILT_IN_FUNCTION 
E 
  EDITCHAR Built-In Subroutine - 
      HELP EDITCHAR 
  EDITSTR Built-In Subroutine - 
      HELP EDITSTR 
  EDITXCHAR Built-In Subroutine - 
      HELP EDITXCHAR 
  EJECT Preprocessor Directive - 
      HELP EJECT_PREPROC 
  ELSE Clause - 
      HELP CASE RULES: 
      HELP IF 
  ELSE preprocessor directive - 
      HELP XLATE_9_TO_6 RULES: 
      HELP IF_PREPROC 
  ELSEIF preprocessor directive - 
      HELP XLATE_9_TO_6 RULES: 
      HELP IF_PREPROC 
  END Statement - 
      HELP END 
  ENDIF preprocessor directive - 
      HELP XLATE_9_TO_6 RULES: 
      HELP IF_PREPROC 
  ENTADDR built-in function - 
      HELP ASSIGNMENT RULES: 
      HELP ENTADDR 
  ENTADDR function - 
      HELP ASYNC RULES: 
  ENTRY attribute - 
      HELP DCL RULES: 
      HELP BASED RULES: 
      HELP ENTRY_ATTRIB 
  entry name - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  ENTRY Statement - 
      HELP ENTRY 
      HELP ENTRY RULES: 
      HELP ENTRY RULES: 
  EOD preprocessor directive - 
      HELP XLATE_9_TO_6 RULES: 
      HELP EOD_PREPROC 
  EPTR Attribute - 
      HELP ASYNC RULES: 
      HELP EPTR 
      HELP INIT RULES: 
  EPTR variable - 
      HELP EPTR RULES: 
      HELP ENTADDR RULES: 
  EPTR, entry variable - 
      HELP ASSIGNMENT RULES: 
  EQU Preprocessor Directive - 
      HELP SET_EQU_LSET 
  ERROR preprocessor directive - 
      HELP XLATE_9_TO_6 RULES: 
      HELP ERROR_PREPROC 
  EXIT Statement - 
      HELP EXIT 
  EXT Attribute - 
      HELP ALIGNMENT RULES: 
      HELP EXT_EXTROOT RULES: 
      HELP KEYWORDS 
  EXT storage type - 
      HELP PROC_MATERIALIZE PARAMETERS: 
  EXT/EXTROOT Attribute - 
      HELP EXT_EXTROOT 
  External Proc Subroutine - 
      HELP KEYWORDS 
  External subroutine - 
      HELP KEYWORDS 
  EXTROOT Attribute - 
      HELP ALIGNMENT RULES: 
      HELP EXT_EXTROOT RULES: 
      HELP KEYWORDS 
  EXTROOT storage type - 
      HELP PROC_MATERIALIZE PARAMETERS: 
F 
  FEP option - 
      HELP OPTIONS FEP 
  FORMAT option - 
      HELP OPTIONS FORMAT 
G 
  GCOS option - 
      HELP OPTIONS GCOS 
  GOTO Label - 
      HELP GOTO RULES: 
  GOTO Statement - 
      HELP GOTO 
H 
  HALF Attribute - 
      HELP HALF 
  HALIGNED attribute - 
      HELP ALIGNMENT 
      HELP ALIGNMENT RULES: 
I 
  identifier, default - 
      HELP MACRO_INVOCATION RULES: 
  identifier, keyword - 
      HELP MACRO_INVOCATION RULES: 
  identifiers - 
      HELP XLATE_9_TO_6 RULES: 
  IF preprocessor directive - 
      HELP XLATE_9_TO_6 RULES: 
  IF Statement - 
      HELP IF 
  IF/ELSE/ELSEIF/ENDIF Preprocessor Directives - 
      HELP IF_PREPROC 
  IF/THEN/ELSE statement - 
      HELP DO RULES: 
      HELP IF RULES: 
  INCLUDE Preprocessor Directive - 
      HELP INCLUDE_PREPROC 
  INDEX Built-In Subroutine - 
      HELP INDEX 
  INDEX1R/INDEX2R Built-In Subroutines - 
      HELP INDEX1R 
  INHIBIT Clause - 
      HELP DO_INHIBIT DESCRIPTION: 
  INIT attribute - 
      HELP BASED RULES: 
      HELP BIT RULES: 
      HELP CHAR RULES: 
      HELP INIT 
      HELP INIT RULES: 
      HELP ENTADDR RULES: 
  INIT clause - 
      HELP REDEF RULES: 
      HELP BINBIT RULES: 
  INIT value - 
      HELP BIT RULES: 
      HELP INIT RULES: 
      HELP LENGTHB RULES: 
      HELP LENGTHC RULES: 
  INSERT Built-In Subroutine - 
      HELP INSERT 
  Internal/External Procedures - 
      HELP KEYWORDS 
  Introduction to PL6 - 
      HELP PROCESSOR 
K 
  keyword identifier - 
      HELP MACRO_INVOCATION RULES: 
  keywords - 
      HELP KEYWORDS 
  keywords, for future use - 
      HELP KEYWORDS 
L 
  legal values - 
      HELP INIT RULES: 
  Length attribute - 
      HELP DCL RULES: 
  LENGTHB Built-In Function - 
      HELP LENGTHB 
      HELP LENGTHB RULES: 
  LENGTHB Preprocessor Function - 
      HELP LENGTHB_PREPROC 
  LENGTHC Built-In Function - 
      HELP LENGTHC 
  LENGTHC Preprocessor Function - 
      HELP LENGTHC_PREPROC 
  LENGTHV Built-In Function - 
      HELP LENGTHV 
  LENGTHW Built-In Function - 
      HELP LENGTHW 
  LEVEL option - 
      HELP OPTIONS LEVEL 
  LIST Preprocessor Directive - 
      HELP LIST_PREPROC 
      HELP LISTING_PREPROC RULES: 
  LISTCOM preprocessor directive - 
      HELP LISTING_PREPROC FORMAT: 
  LISTCON preprocessor directive - 
      HELP LISTING_PREPROC FORMAT: 
  LISTDIR preprocessor directive - 
      HELP LISTING_PREPROC FORMAT: 
  LISTEXP preprocessor directive - 
      HELP LISTING_PREPROC FORMAT: 
  LISTINC preprocessor directive - 
      HELP LISTING_PREPROC FORMAT: 
  LISTING Preprocessor Directives - 
      HELP LISTING_PREPROC 
  LISTMAC preprocessor directive - 
      HELP LISTING_PREPROC FORMAT: 
  LISTSUB preprocessor directive - 
      HELP LISTING_PREPROC FORMAT: 
  LO option - 
      HELP OPTIONS LO 
  LPS option - 
      HELP OPTIONS LPS 
  LS option - 
      HELP OPTIONS LS 
  LSET Preprocessor Directive - 
      HELP SET_EQU_LSET 
  LU option - 
      HELP OPTIONS LU 
M 
  MACRO Definition - 
      HELP MACRO_DEFINITION 
      HELP MACRO_INVOCATION DESCRIPTION: 
      HELP MACRO_INVOCATION RULES: 
  macro expansion text - 
      HELP PLIST_PREPROC DESCRIPTION: 
  MACRO Invocation - 
      HELP MACRO_INVOCATION 
      HELP MACRO_INVOCATION RULES: 
  macros - 
      HELP XLATE_9_TO_6 RULES: 
  MAIN attribute - 
      HELP PROC RULES: 
  MAIN procedure - 
      HELP RETURN_ALTRETURN RULES: 
      HELP KEYWORDS 
  MATERIALIZE clause - 
      HELP PROC PARAMETERS: 
      HELP PROC_MATERIALIZE 
  MAX Preprocessor Function - 
      HELP MAX_PREPROC 
  MAXIMUM Built-In Function - 
      HELP MAXIMUM 
  MDMAP option - 
      HELP OPTIONS MDMAP 
  MIN Preprocessor Function - 
      HELP MIN_PREPROC 
  MINIMUM Built-In Function - 
      HELP MINIMUM 
  MOD Built-In Function - 
      HELP MOD 
  MOD Preprocessor Function - 
      HELP MOD_PREPROC 
  MPMAP option - 
      HELP OPTIONS MPMAP 
  MSCHEMA option - 
      HELP OPTIONS MSCHEMA 
  MUREF option - 
      HELP OPTIONS MUREF 
  MXREF option - 
      HELP OPTIONS MXREF 
N 
  NDMAP option - 
      HELP OPTIONS NDMAP 
  NFORMAT option - 
      HELP OPTIONS NFORMAT 
  NLEVEL option - 
      HELP OPTIONS NLEVEL 
  NLIST Preprocessor Directive - 
      HELP NLIST_PREPROC 
      HELP LISTING_PREPROC RULES: 
  NLO option - 
      HELP OPTIONS NLO 
  NLPS option - 
      HELP OPTIONS NLPS 
  NLS option - 
      HELP OPTIONS NLS 
  NLU option - 
      HELP OPTIONS NLU 
  NMDMAP option - 
      HELP OPTIONS NMDMAP 
  NOAUTO option - 
      HELP PROC RULES: 
  NOSHARELIB option - 
      HELP OPTIONS NOSHARELIB 
  NOU option - 
      HELP OPTIONS NOU 
  NPMAP option - 
      HELP OPTIONS NPMAP 
  NSCHEMA option - 
      HELP OPTIONS NSCHEMA 
  NSO option - 
      HELP OPTIONS NSO 
  NSYS option - 
      HELP OPTIONS NSYS 
  NUI option - 
      HELP OPTIONS NUI 
  Null Statement - 
      HELP NULL 
  NUREF option - 
      HELP OPTIONS NUREF 
  NWARN option - 
      HELP OPTIONS NWARN 
  NXREF option - 
      HELP OPTIONS NXREF 
O 
  operators - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  OPTIONAL Attribute - 
      HELP OPTIONAL 
  OPTUI option - 
      HELP OPTIONS OPTUI 
  OU option - 
      HELP OPTIONS OU 
P 
  page eject - 
      HELP EJECT_PREPROC DESCRIPTION: 
  PALIGND Built-In Function - 
      HELP PALIGND 
  PALIGNW Built-In Function - 
      HELP PALIGNW 
  PARAM Attribute - 
      HELP PARAMETER 
  Parameter - 
      HELP ALIGNMENT RULES: 
  PARAMETER attribute - 
      HELP KEYWORDS 
  parameter structure - 
      HELP BIT RULES: 
  PINCRB Built-In Function - 
      HELP PINCRB 
  PINCRC Built-In Function - 
      HELP PINCRC 
  PINCRW Built-In Function - 
      HELP PINCRW 
  PL-6 Attributes - 
      HELP UNWIND RULES: 
  PL-6 Built-in Functions - 
      HELP WORD CROSS_REFERENCE: 
  PL-6 Built-in Subroutines - 
      HELP WORD CROSS_REFERENCE: 
  PL-6 operators - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  PL-6 reserved words - 
      HELP KEYWORDS 
  PL-6 Statement Syntax - 
      HELP STATEMENTS 
  PL-6 Statements - 
      HELP HELP 
  PL6 Compiler Invocation - 
      HELP KEYWORDS 
  PL6 HELP Facility - 
      HELP HELP 
  PL6 Overview - 
      HELP PROCESSOR 
  PLIST Preprocessor Directive - 
      HELP PLIST_PREPROC 
      HELP LISTING_PREPROC RULES: 
  PMAP option - 
      HELP OPTIONS PMAP 
  POFFC Built-In Function - 
      HELP POFFC 
  POFFW Built-In Function - 
      HELP POFFW 
  pointer - 
      HELP PROC_AVOID RULES: 
  pointer value - 
      HELP PROC_MATERIALIZE DESCRIPTION: 
  pointer variable - 
      HELP PTR RULES: 
  Preprocessor Concepts - 
      HELP PREPROCESSOR 
  preprocessor directives - 
      HELP XLATE_9_TO_6 RULES: 
      HELP MACRO_INVOCATION RULES: 
  Preprocessor Expression and Function Facilities - 
      HELP PREP_EXPRESSION 
  preprocessor expressions - 
      HELP PREPROCESSOR 
  preprocessor-variable identifier - 
      HELP SET_EQU_LSET DESCRIPTION: 
  PROC ASYNC - 
      HELP KEYWORDS 
  PROC External - 
      HELP KEYWORDS 
  PROC MAIN - 
      HELP KEYWORDS 
  PROC statement - 
      HELP ENTRY RULES: 
      HELP PROC 
      HELP PARAMETER RULES: 
  PROC Statement/AVOID Clause - 
      HELP PROC_AVOID 
  PROC Statement/MATERIALIZE Clause - 
      HELP PROC_MATERIALIZE 
  procedure rules - 
      HELP KEYWORDS 
  program listing operation - 
      HELP XLATE_9_TO_6 RULES: 
  PTR - 
      HELP INIT RULES: 
  PTR Attribute - 
      HELP PTR 
  PTR variable - 
      HELP BASED PARAMETERS: 
  PTRDSCR Built-in Function - 
      HELP PTRDSCR_BUILT_IN_FUNCTION 
Q 
  qualifiers - 
      HELP BASED RULES: 
R 
  READONLY Attribute - 
      HELP READONLY 
  REDEF attribute - 
      HELP DCL RULES: 
      HELP BASED RULES: 
      HELP REDEF 
  Reference Tables - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  REMEMBER Attribute - 
      HELP REMEMBER_ATTRIB 
  REMEMBER Statement - 
      HELP REMEMBER 
      HELP REMEMBER RULES: 
      HELP REMEMBER_ATTRIB DESCRIPTION: 
  REMEMBER variable - 
      HELP REMEMBER RULES: 
      HELP UNWIND RULES: 
  reserved words - 
      HELP KEYWORDS 
  reserved words, for future use - 
      HELP KEYWORDS 
  RESUB Preprocessor Directive - 
      HELP SUB_RESUB_PREPROC 
  RETURN - 
      HELP RETURN_ALTRETURN RULES: 
  RETURN statement - 
      HELP END RULES: 
      HELP EXIT RULES: 
  RETURN/ALTRETURN Statement - 
      HELP RETURN_ALTRETURN 
S 
  SBIN - 
      HELP BYTE DESCRIPTION: 
      HELP HALF DESCRIPTION: 
      HELP BINBIT RULES: 
      HELP MAXIMUM RULES: 
  SBIN Attribute - 
      HELP SBIN 
      HELP WORD CROSS_REFERENCE: 
  scalar declaration - 
      HELP AREAREF RULES: 
  scalar name - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  scalar quantity - 
      HELP INIT RULES: 
  scalar variable - 
      HELP DCL RULES: 
      HELP STORAGE_LAYOUT_FOR_SCALARS 
  SCHEMA option - 
      HELP OPTIONS SCHEMA 
  SEARCH Built-In Subroutine - 
      HELP SEARCH 
  SEARCHR Built-In Subroutine - 
      HELP SEARCHR 
  SELECT Clause - 
      HELP DO_SELECT DESCRIPTION: 
  SELECT group - 
      HELP SELECT RULES: 
  SELECT Statement - 
      HELP SELECT 
  SELECT/ELSE group - 
      HELP SELECT RULES: 
  semicolon - 
      HELP ATTRIBUTES 
  SET directive - 
      HELP LISTING_PREPROC FORMAT: 
  SET/EQU/LSET Preprocessor Directives - 
      HELP SET_EQU_LSET 
  SEVERITY option - 
      HELP OPTIONS SEVERITY 
  SIZEB Built-In Function - 
      HELP SIZEB 
  SIZEC Built-In Function - 
      HELP SIZEC 
  SIZEV Built-In Function - 
      HELP SIZEV 
  SIZEW Built-In Function - 
      HELP SIZEW 
  SO option - 
      HELP OPTIONS SO 
  SPACE Preprocessor Directive - 
      HELP SPACE_PREPROC 
  special characters - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  Specification of Attributes - 
      HELP ATTRIBUTES 
  SRCH (list) option - 
      HELP OPTIONS SRCH 
  START option - 
      HELP OPTIONS START 
  statement identifier keyword - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  statement label - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  Statement Syntax - 
      HELP STATEMENTS 
  STATIC AREADEF storage type - 
      HELP PROC_MATERIALIZE PARAMETERS: 
  STATIC Attribute - 
      HELP ALIGNMENT RULES: 
      HELP BASED RULES: 
      HELP STATIC 
      HELP KEYWORDS 
  STATIC storage type - 
      HELP PROC_MATERIALIZE PARAMETERS: 
  storage class attribute - 
      HELP AREAREF RULES: 
  storage class attributes - 
      HELP KEYWORDS 
  Storage Classes - 
      HELP ALIGNMENT RULES: 
      HELP STATIC DESCRIPTION: 
  structure declarations - 
      HELP AREAREF RULES: 
  structure name - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  structures - 
      HELP DCL RULES: 
      HELP AUTO RULES: 
  SUB/RESUB Preprocessor Directives - 
      HELP SUB_RESUB_PREPROC 
  SUBBIT Preprocessor Function - 
      HELP SUBBIT_PREPROC 
  subroutine name keyword - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  Subroutine, External - 
      HELP KEYWORDS 
  Subroutine, Internal - 
      HELP KEYWORDS 
  SUBSTR built-in function - 
      HELP ASSIGNMENT RULES: 
      HELP SUBSTR 
  SUBSTR Preprocessor Function - 
      HELP SUBSTR_PREPROC 
  SYMDEF Attribute - 
      HELP SYMDEF 
  SYMREF - 
      HELP ALIGNMENT RULES: 
      HELP READONLY RULES: 
  SYMREF attribute - 
      HELP BASED RULES: 
      HELP SYMREF 
      HELP KEYWORDS 
  SYMREF storage type - 
      HELP PROC_MATERIALIZE PARAMETERS: 
  SYN option - 
      HELP OPTIONS SYN 
  SYS option - 
      HELP OPTIONS SYS 
  system file - 
      HELP SYSTEM_FILE 
T 
  Tables, list of included - 
      HELP XCHARBIN_PREPROC EXAMPLE: 
  TEXTCHAR Preprocessor Function - 
      HELP TEXTCHAR_PREPROC 
  THEN Clause - 
      HELP IF 
  TO Clause - 
      HELP DO_TO_DOWNTO_BY DESCRIPTION: 
U 
  UBIN - 
      HELP BYTE DESCRIPTION: 
      HELP HALF DESCRIPTION: 
      HELP BINBIT RULES: 
      HELP MAXIMUM RULES: 
  UBIN Attribute - 
      HELP UBIN 
      HELP WORD CROSS_REFERENCE: 
  UBIN values - 
      HELP SELECT RULES: 
  UBIN/SBIN - 
      HELP INIT RULES: 
  UI option - 
      HELP OPTIONS UI 
  UNAL attribute - 
      HELP ALIGNMENT 
      HELP ALIGNMENT RULES: 
  UNINHIBIT Clause - 
      HELP DO_UNINHIBIT 
  UNTIL Clause - 
      HELP DO_UNTIL DESCRIPTION: 
  UNWIND procedure - 
      HELP UNWIND RULES: 
  UNWIND statement - 
      HELP REMEMBER DESCRIPTION: 
      HELP UNWIND 
      HELP REMEMBER_ATTRIB DESCRIPTION: 
  UNWIND TO - 
      HELP REMEMBER RULES: 
  UREF option - 
      HELP OPTIONS UREF 
V 
  VBASE Built-In Function - 
      HELP VBASE 
  VBOUND Built-In Function - 
      HELP VBOUND 
  VECTDSCR Built-in Function - 
      HELP VECTDSCR_BUILT_IN_FUNCTION 
  VECTOR - 
      HELP INIT RULES: 
      HELP VTYPE DESCRIPTION: 
  VECTOR Attribute - 
      HELP VECTOR_ATTRIB 
  VECTOR Built-In Function - 
      HELP VECTOR 
  VECTOR function - 
      HELP INIT RULES: 
      HELP VECTOR_ATTRIB RULES: 
  VECTOR type - 
      HELP BITVECT DESCRIPTION: 
  VECTOR type field - 
      HELP VTYPE DESCRIPTION: 
  vertical format character - 
      HELP SPACE_PREPROC DESCRIPTION: 
      HELP SPACE_PREPROC DESCRIPTION: 
  VFLAGS Built-In Function - 
      HELP VFLAGS 
  VTYPE Built-In Function - 
      HELP VTYPE 
W 
  WALIGNED attribute - 
      HELP ALIGNMENT 
  WALIGNED attributes - 
      HELP ALIGNMENT RULES: 
  WARN option - 
      HELP OPTIONS WARN 
  WHENALTRETURN - 
      HELP CALL RULES: 
      HELP CALL RULES: 
  WHENRETURN - 
      HELP CALL RULES: 
      HELP CALL RULES: 
  WHILE Clause - 
      HELP DO_WHILE DESCRIPTION: 
  WORD - 
      HELP SBIN RULES: 
  WORD Attribute - 
      HELP WORD 
X 
  XCHARBIN Built-In Subroutine - 
      HELP XCHARBIN 
  XCHARBIN Preprocessor Function - 
      HELP XCHARBIN_PREPROC 
  XLATE Built-In Subroutine - 
      HELP XLATE 
  XLATE_6_TO_9 Built-In Subroutine - 
      HELP XLATE_6_TO_9 
  XLATE_9_TO_6 Built-In Subroutine - 
      HELP XLATE_9_TO_6 
  XREF option - 
      HELP OPTIONS XREF 
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
Description: 
The IF statement permits a choice as to which of two sets of statements is to 
be executed.  The decision is based on the value of an expression. 
Format: 
[label1:] IF exp THEN [label2:] stmt1; [ELSE [label3:] stmt2;] 
Parameters: 
exp    a bit-string or truth-value expression. 
stmt1 - stmt2    any single PL-6 statement (except a CASE, DCL, END, ENTRY, 
PROC or SELECT statement), or a DO group. 
Rules: 
1.  The IF statement is not terminated by a semicolon; however, stmt1 and 
    stmt2 must have terminal semicolons. 
2.  Both stmt1 and stmt2 may be any valid PL-6 statements, including the null 
    statement or another IF statement, with the following exceptions:  CASE, 
    DCL, END, ENTRY, PROC and SELECT. 
3.  In the case where IF statements are nested, each ELSE clause is always 
    associated with the nearest preceding unmatched IF statement. 
4.  If an inner IF statement does not logically need an ELSE clause, an ELSE 
    with a null statement may be required in order to maintain the desired 
    relationship between the IF statements and their ELSE clauses. 
5.  Execution proceeds as follows.  The expression is evaluated.  If the 
    result is true, the THEN clause is executed and control leaves the IF 
    statement.  If the result is false, the THEN clause is skipped, the ELSE 
    clause is executed if present, and control leaves the IF statement.  Each 
    THEN or ELSE clause may contain statements that specify a transfer of 
    control (e.g., GOTO); hence, the normal sequence of the IF statement may 
    be overridden. 
6.  If control is transferred to a labeled THEN or ELSE statement by a GOTO, 
    the statement is executed and control leaves the IF/THEN/ELSE statement. 
    If control is transferred to a labeled statement within a simple DO or 
    DO/WHILE group that is the THEN or ELSE statement, execution continues at 
    that statement.  When execution of the DO group is complete, control 
    leaves the IF/THEN/ELSE statement. 
Example: 
    IF AA=17 OR BB=18 THEN 
       GOTO LBLA; 
    IF BB+C>0 THEN 
      DO X=1 TO 13 BY 2; 
         Y=X+1; 
         END; 
    IF X=0 THEN 
       IF Y=1 THEN 
          X=1; 
       ELSE; 
    ELSE 
       GOTO NEXT; 
    A=B+C; 
As the example is written, if X = 0 and Y = 1, then X is set to 1 and A = B + 
C is executed.  If X = 0 and Y is not equal to 1, then A = B + C is executed. 
If X is not equal to 0, GOTO NEXT is executed. 
    IF X=0 THEN 
       IF Y=1 THEN 
          X=1; 
       ELSE 
          GOTO NEXT; 
    A=B+C; 
In this example the ELSE clause (line 4 above) is omitted.  If X = 0 and Y = 
1, then X is set to 1 and A = B + C is executed.  If X = 0 and Y is not equal 
to 1, then GOTO NEXT is executed.  If X is not equal to 0, then A = B + C is 
executed. 
00003
00001
00002
Description: 
%IF provides conditional inclusion, or exclusion of a number of source records 
or preprocessor directives. 
Format: 
%IF  exp ; 
    any code or directives except %EOD 
    [%ELSEIF exp ;  ...                                 ] 
    [   any code or directives except %EOD              ] 
    [%ELSE ;                                            ] 
    [   any code or directives except: %EOD, %ELSEIF or ] 
    [   %ELSE which is not preceded by an %IF directive ] 
    %ENDIF; 
Parameters: 
exp   is a preprocessor bit string expression containing one or more of the 
following elements: 
1.  bit-string constants, e.g., '0'B (0 <= LENGTHB(bit-string) <= 72). 
2.  preprocessor relational expressions 
3.  previously-SET bit-string preprocessor variables. 
4.  bit-string preprocessor functions. 
Bit-string preprocessor expressions can be: 
1.  optionally enclosed in parentheses. 
2.  optionally preceded by a bit-string ~ or a truth-value NOT. 
3.  optionally combined with the operators: 
    &    (bit-string 'and' operator) 
    |    (bit-string 'or' operator) 
    AND  (truth-value 'and' operator) 
    OR   (truth-value 'or' operator) 
Rules: 
1.  When an %IF directive is encountered, the preprocessor bit-string 
    expression is evaluated. 
2.  If the expression of an %IF or %ELSEIF directive evaluates to all 0 bits, 
    all text and directives are skipped (including %IF...%ENDIF blocks) until: 
    a.  an %ELSEIF directive causes another expression to be evaluated. 
    b.  an %ELSE directive causes text and directives to be processed through 
        the matching %ENDIF directive. 
    c.  an %ENDIF directive resumes either normal processing or processing of 
        the containing conditional (%IF or %ELSEIF) block. 
3.  If the expression of an %IF or %ELSEIF directive evaluates to other than 
    all 0 bits, the following text and directives are processed (including %IF 
    blocks) until: 
    a.  an %ELSEIF or %ELSE directive causes succeeding text and directives 
        (including %IF...%ENDIF blocks) to be skipped until the matching 
        %ENDIF directive is found. 
    b.  an %ENDIF directive resumes either normal processing or processing of 
        the containing conditional block. 
4.  %IF...%ENDIF blocks can be nested.  Each %IF directive must correspond to 
    one and only one %ENDIF directive.  Each %IF directive can correspond to 
    any number of %ELSEIF directives and at most one %ELSE directive. 
5.  %EOD directives cannot be nested in conditional code. 
Example: 
    MOTHER_GOOSE: PROC; 
    DCL FAIRY_TALE CHAR (20); 
    DCL WOLF CHAR (20); 
    DCL PORRIDGE CHAR (20); 
    DCL COLLECT_INSURANCE BIT (1); 
    %EQU PAPA_BEAR = '1'B; 
    %EQU MAMA_BEAR = '0'B; 
    %EQU BABY_BEAR = '0'B; 
    %EQU STRAW = '0'B; 
    %EQU STICKS = '0'B; 
    %EQU BRICKS = '1'B; 
    %EQU FAIRY_TALE = 'THREE LITTLE PIGS'; 
    %IF FAIRY_TALE = 'GOLDY LOCKS'; 
        %IF PAPA_BEAR; 
            PORRIDGE = 'TOO HOT'; 
        %ELSEIF MAMA_BEAR; 
            PORRIDGE = 'TOO COLD'; 
        %ELSEIF BABY_BEAR; 
            PORRIDGE = 'JUST RIGHT'; 
        %ENDIF; 
    %ELSEIF FAIRY_TALE = 'THREE LITTLE PIGS'; 
        %IF STRAW; 
            COLLECT_INSURANCE = '1'B; 
        %ELSEIF STICKS; 
            COLLECT_INSURANCE = '1'B; 
        %ELSEIF BRICKS; 
            WOLF = 'HYPER-VENTILATED'; 
        %ENDIF; 
    %ENDIF; 
    END MOTHER_GOOSE; 
The preceding source produces the following listing output: 
    MOTHER_GOOSE: PROC; 
    DCL FAIRY_TALE CHAR (20); 
    DCL WOLF CHAR (20); 
    DCL PORRIDGE CHAR (20); 
    DCL COLLECT_INSURANCE BIT (1); 
    %EQU PAPA_BEAR = '1'B; 
    %EQU MAMA_BEAR = '0'B; 
    %EQU BABY_BEAR = '0'B; 
    %EQU STRAW = '0'B; 
    %EQU STICKS = '0'B; 
    %EQU BRICKS = '1'B; 
    %EQU FAIRY_TALE = 'THREE LITTLE PIGS'; 
    %IF FAIRY_TALE = 'GOLDY LOCKS'; 
    %ELSEIF FAIRY_TALE = 'THREE LITTLE PIGS'; 
        %IF STRAW; 
        %ELSEIF STICKS; 
        %ELSEIF BRICKS; 
            WOLF = 'HYPER-VENTILATED'; 
        %ENDIF; 
    %ENDIF; 
    END MOTHER_GOOSE; 
Cross Reference: 
Please consult the rules concerning bit-string preprocessor functions for 
additional information regarding bit strings. 
00004
00003
00001
00002
Description: 
%INCLUDE allows inclusion of source records from files other than the current 
source input file. 
Format: 
%INCLUDE fid; 
Parameters: 
fid    is any valid CP-6 file identifier. 
Rules: 
1.  %INCLUDE files can contain PL-6 source code and PL-6 preprocessor 
    directives. 
2.  When the %INCLUDE directive is encountered, the current input source is 
    suspended and the named source file is input.  Specified text is 
    incorporated into the source program immediately following the %INCLUDE 
    directive.  When the end-of-file is reached on the INCLUDE file, input is 
    resumed from the suspended file. 
3.  %INCLUDE files can be nested to 9 levels, giving a total of 10 levels of 
    include files. 
4.  %INCLUDE directives within macro definitions are expanded at definition 
    time, not at invocation time. 
5.  The %INCLUDE directive must be on a single line. 
6.  The include fid may specify file name, or both file name and account, e.g. 
    %INCLUDE DCL_FILE; or %INCLUDE DCL_FILE.ACCTNO;.  If the fid specifies 
    file name only, a search of relevant accounts will be made, in accordance 
    with the CP-6 search rules, and the first instance of the file found will 
    be used.  The order of the search is: 
    a.  Accounts specified in the SRCH option of the compiler invocation 
        command, in the order specified in the SRCH option list, if this 
        option was used. 
    b.  The user's running account. 
    c.  The :LIBRARY account. 
Example: 
Consider the include file, DCL_FILE, which has the following records: 
    DCL 1 PERSONAL_INFO, 
          2 NAME, 
            3 FIRST CHAR (20), 
            3 MIDDLE CHAR (20), 
            3 LAST CHAR (20), 
          2 ADDRESS, 
            3 NUMBER CHAR (7), 
            3 STREET CHAR (30), 
            3 CITY CHAR (30), 
            3 STATE CHAR (2), 
            3 ZIP UBIN (9), 
          2 PHONE, 
            3 AREA_CODE UBIN (3), 
            3 NUMBER UBIN (7), 
          2 OCCUPATION CHAR (25); 
The following procedure includes the above file. 
    DEMO: PROC; 
    %LIST; 
    %INCLUDE DCL_FILE; 
    PERSONAL_INFO.OCCUPATION = 'UNDERWATER BASKETWEAVER'; 
    END DEMO; 
The preceding source produces the following listing output: 
     
    DEMO: PROC; 
    %LIST; 
    %INCLUDE DCL_FILE; 
    DCL 1 PERSONAL_INFO, 
          2 NAME, 
            3 FIRST CHAR (20), 
            3 MIDDLE CHAR (20), 
            3 LAST CHAR (20), 
          2 ADDRESS, 
            3 NUMBER CHAR (7), 
            3 STREET CHAR (30), 
            3 CITY CHAR (30), 
            3 STATE CHAR (2), 
            3 ZIP UBIN (9), 
          2 PHONE, 
            3 AREA_CODE UBIN (3), 
            3 NUMBER UBIN (7), 
          2 OCCUPATION CHAR (25); 
    PERSONAL_INFO.OCCUPATION = 'UNDERWATER BASKETWEAVER'; 
    END DEMO; 
00003
00001
00002
Description: 
The INDEX built-in subroutine locates the first occurrence of a string within 
another string with a left to right scan. 
Format: 
CALL INDEX (index, pattern, string [ , [start] [, mask]]) 
    [ALTRET (label)                                 ]; 
    [[WHENRETURN DO group ] [WHENALTRETURN DO group]] 
Parameters: 
index    any arithmetic location reference. 
pattern,string    any character string or character location reference. 
start    any arithmetic expression. 
mask    a bit, octal or hexadecimal literal. 
label    any valid label. 
Rules: 
1.  Index is the result destination, and is set by the routine to the leftmost 
    character position in string (after start) where the leftmost character of 
    pattern was found. It must be defined as either SBIN WORD or UBIN WORD and 
    must be word aligned. 
    If pattern is not found in string, index will be set to LENGTHC(string) 
    Legal values  for index (if pattern is found) are defined as: 
        0 <= start <= index < LENGTHC(string) 
2.  pattern specifies the character string to be searched for in string. 
3.  string specifies the character string to be searched. The search is made 
    left to right for the first occurrence of pattern. 
4.  start represents an optional integer value which determines the character 
    position in string at which the search is to begin. Legal values for start 
    are defined as: 
        0 <= start <= LENGTHC(string) 
    If start is not specified, the default is zero. 
5.  mask optionally specifies which bit positions within each character are to 
    be compared during a one character indexing operation. This field is not 
    legal if the LENGTHC(pattern) is not equal to one, or is variable. 
    The mask parameter must be a bit or octal literal such that the 
    LENGTHB(mask) is equal to nine. A 0 bit value in the mask means the 
    corresponding bit is to be involved in the comparison. A 1 bit value means 
    the corresponding bit in each character is not involved in the comparison. 
    If mask is not specified, and is legal, a value of '000'O will be used. 
6.  If pattern is not found in string, the INDEX operation will ALTRETURN. 
00001
00002
INDEX
Description: 
The INDEX1R/INDEX2R built-in subroutines will locate the first occurrence of a 
string within another string with a right to left scan. 
Format: 
CALL { INDEX1R } (index, pattern, string [ , [start] [,mask]]) 
     { INDEX2R } 
    [ALTRET (label)                                 ]; 
    [[WHENRETURN DO group ] [WHENALTRETURN DO group]] 
Parameters: 
index    any arithmetic location reference. 
pattern,string    any character string or character location reference. 
start    any arithmetic expression. 
mask    a bit, octal or hexadecimal literal. 
label    any valid label. 
Rules: 
1.  Index is the result destination, and is set by the routine to the 
    rightmost character position in string (after start) where the rightmost 
    character of pattern was found. It must be defined as either SBIN WORD or 
    UBIN WORD and must be word aligned. 
    If pattern is not found in string, index will be set as follows: 
        LENGTHC(string)  if start is not specified 
        start            if start is specified 
    Legal values  for index (if pattern is found) are defined as: 
        0 <= index < start <= LENGTHC(string) 
2.  pattern specifies the character string to be searched for in string.  For 
    INDEX1R the LENGTHC(pattern) must equal one. For INDEX2R the 
    LENGTHC(pattern) must equal two. 
3.  string specifies the character string to be searched. The search is made 
    right to left for the first occurrence of pattern. 
4.  start represents an optional integer value which determines the character 
    position in string at which the search is to begin. The first character 
    tested is start-1. Legal values for start are defined as: 
        1 <= start <= LENGTHC(string) 
    If start is not specified, the default is LENGTHC(string). 
5.  mask optionally specifies which bit positions within each character are to 
    be compared during a one character indexing operation. This field is not 
    legal if the LENGTHC(pattern) is not equal to one, or is variable. 
    The mask parameter must be a bit or octal literal such that the 
    LENGTHB(mask) is equal to nine. A 0 bit value in the mask means the 
    corresponding bit is to be involved in the comparison. A 1 bit value means 
    the corresponding bit in each character is not involved in the comparison. 
    If mask is not specified, and is legal, a value of '000'O will be used. 
6.  If pattern is not found in string, the INDEX operation will ALTRETURN. 
00001
00002
INDEX
INDEX1R
Description: 
The INIT attribute specifies the value (or set of values) to which the storage 
corresponding to the specified identifier is to be initialized at compile 
time.  If this attribute is not specified, the storage is not initialized. 
Format: 
DCL id a1 [a2] ... INIT (value1); 
DCL id (0:n) a1 [a2] ... INIT (value1 [*m1], value2 [*m2] ... ); 
Parameters: 
id    any valid identifier. 
a1,a2    any valid attributes. 
n    any valid numeric integer. 
m1,m2    any valid numeric integers. 
value1,value2    one of the following: 
    char-strg    any valid character-string constant. 
    bit-strg    any valid bit-string constant. 
    dec-val    any decimal integer value, signed or unsigned. 
    ref    a reference to any of the following built-in functions: 
        ADDR        ENTADDR      SIZEV 
        ASCBIN      LENGTHB      SIZEW 
        ASCBIT      LENGTHC      VECTOR 
        BINASC      LENGTHV 
        BINBIT      LENGTHW 
        BITASC      SIZEB 
        BITBIN      SIZEC 
        DCBNUM 
Rules: 
1.  If the identifier being declared represents a scalar quantity, only one 
    initial value may be given.  If the identifier represents an array, as 
    indicated by the (0:n) dimension attribute, up to n+1 values may be given. 
    In a structure, elementary data items are initialized separately. 
2.  For an array, the values are assigned left to right, beginning at the 
    lower bound.  The *m construct indicates that the value specified is to be 
    repeated for each array element the number of times specified by m.  If 
    too many values are specified, the excess ones are ignored.  If too few 
    are specified, the remainder of the array is not initialized.  If m is 
    zero on the last specification in the INIT list, the specified value will 
    be repeated for each remaining array element, if any.  If m is zero (*0), 
    on other than the last specification in the INIT list, the specified value 
    will be repeated sufficient times to ensure that the array is completely 
    initialized.  There may be only one *0 item per init list.  In the 
    following example the *0 item will be repeated 3 times. 
    DCL DAN(0:4) UBIN STATIC INIT(1,2*0,3); 
    For a scalar variable, 
    INIT('A'*0) or INIT('A'*1) 
    will initialize the scalar to 'A'. 
3.  The INIT attribute is legal only on the STATIC, CONSTANT, EXT, EXTROOT and 
    DCB variables.  It may only appear on an elementary item. 
4.  The value specified must be of the same data type as the variable being 
    initialized.  The following list shows data type and legal values: 
    BIT          bit-string, ASCBIT, BINBIT, VECTOR 
    PTR          ADDR 
    VECTOR       VECTOR 
    CHAR         char-string, BITASC, BINASC 
    UBIN/SBIN    dec-value, ASCBIN, BITBIN, LENGTHB, LENGTHC, 
                 LENGTHV, LENGTHW, SIZEB, SIZEC, SIZEV, SIZEW, DCBNUM 
    EPTR         ENTADDR 
5.  If the ADDR or VECTOR function appears as a value, then the argument of 
    the function must be described as STATIC, SYMREF, EXT, EXTROOT, AREAREF, 
    or CONSTANT. 
6.  If the LENGTHB, LENGTHC, LENGTHV, LENGTHW, SIZEB, SIZEC, SIZEV, or SIZEW 
    function appears as a value, then the argument of the function must not 
    contain an adjustable string. 
7.  The rules for assigning an INIT value to the declaring variable are 
    exactly the same as the rules applying to an assignment statement with the 
    variable on the left-hand side and the value on the right. 
Example: 
    DCL X CHAR(2) STATIC INIT('A'); 
    DCL Y$ PTR CONSTANT INIT(ADDR(X)); 
    DCL 1 A (0:3) AREADEF, 
          2 B UBIN BYTE CALIGNED INIT(1,2,3,4), 
          2 C BIT(9) INIT(ASCBIT('A')*4); 
00003
00001
00002
Description: 
The INSERT built-in subroutine allows the concatenation of up to six strings 
and inserts the result into a subset of a character string.  INSERT is a 
character move and concatenation operation. 
Format: 
CALL INSERT (tostr, [start], [len], str1 [,str2]...[,str6]) 
    [ALTRET (label)                                 ]; 
    [[WHENRETURN DO group ] [WHENALTRETURN DO group]] 
Parameters: 
tostr    character location reference. 
str1,...,str6    character expression. 
start, len    any arithmetic expression. 
label    any valid label. 
Rules: 
1.  The resultant string to be inserted is the concatenation of str1, str2,... 
    str6 in that order. 
2.  tostr as modified by start and len represents the destination string.  If 
    the length of the concatenated strings is less than len, then blank-fill 
    will occur.  If the length is greater than len, then truncation will 
    occur. 
3.  Legal values for start and len are defined as follows: 
        0 <= start < LENGTHC (tostr) 
        0 <= len <= LENGTHC (tostr) 
    such that 
        0 <= start + len <= LENGTHC (tostr) 
4.  If truncation of the concatenated string occurs the INSERT operation will 
    ALTRETURN. 
5.  If the start argument is omitted, 0 is assumed.  If the len argument is 
    omitted, (LENGTHC (tostr) - start) is assumed. 
6.  If tostr overlaps any of the source strings, results are undefined. 
00001
00002
ADDR ALIGNED ALTRET ALTRETURN AND AREADEF AREAREF ASCBIN ASCBIT ASYNC AUTO 
AVOID BASED BINASC BINBIT BINCHAR BINXCHAR BIT BITASC BITBIN BITVECT BY BYTE 
CALIGNED CALL CASE CHAR CHARBIN CONCAT CONSTANT CONV CPTR DALIGNED DBASE DCB 
DCBADDR DCBNUM DBOUND DCL DO DOMAIN * DOWNTO DSCR DTYPE EDITCHAR EDITSTR 
EDITXCHAR ELSE END ENTADDR ENTRY EPTR ERASE EXIT EXT EXTROOT GOTO HALF 
HALIGNED IF IN INDEX INDEX1 * INDEX1R INDEX2 * INDEX2R INHIBIT INIT INSERT 
LENGTHB LENGTHC LENGTHV LENGTHW MAIN MATERIALIZE MAXIMUM MINIMUM MOD NIL 
NOAUTO NOT OPTIONAL OR PALIGND PALIGNW PARAM PINCRB PINCRC PINCRW POFFC POFFW 
PROC PTR PTRDSCR READONLY REDEF REMEMBER RETURN SBIN SEARCH SEARCHR SELECT 
SIZEB SIZEC SIZEV SIZEW STATIC SUBSTR SYMDEF SYMREF THEN THRU * TO UBIN UNAL 
UNINHIBIT UNTIL UNWIND VBASE VBOUND VECTDSCR VECTOR VFLAGS VTYPE WALIGNED 
WHENALTRETURN WHENRETURN WHILE WORD XCHARBIN XLATE XLATE_6_TO_9 XLATE_9_TO_6 
$PRO $PR1 $PR2 $PR3 $PR4 $PR5 $PR6 $PR7 $X5 $X6 $X7 
* These keywords cannot be used in CP6 PL6. 
Description: 
The LENGTHB built-in function returns the number of bits required for the 
logical storage of a constant or reference.  This is the number of bits 
specified by DCLs for a reference, and does not include supplementary bits 
that may be implied by alignment requirements. 
Format: 
        {(reference     )} 
LENGTHB {(stringconstant)} 
        {(NIL           )} 
        {(ERASE         )} 
Parameters: 
reference    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted reference. 
stringconstant    a bit-string or character-string constant. 
Rules: 
1.  LENGTHB returns a UBIN WORD value. 
2.  LENGTHB is defined as follows: 
        LENGTHB (x) = number of bits required for storage of x 
    where x is a reference or a string constant. 
    NOTE:  The LENGTHB function is evaluated before the required alignment has 
    been performed.  Therefore, the function represents the logical size as 
    opposed to the physical size of the reference. 
3.  By definition 
        LENGTHB (NIL) = 0 
    and 
        LENGTHB (ERASE) = 1 
4.  If the argument of LENGTHB is a reference, then the reference may have any 
    storage class, and any data type except ENTRY. 
5.  If the LENGTHB function appears as the INIT value in a declaration of a 
    variable and the argument is a reference, the argument may not indicate an 
    adjustable bit/character string or a structure containing one.  In 
    addition, a BASED reference must not be pointer qualified. 
6.  BASED and DCB data can be referenced without pointer-qualification in the 
    LENGTHB function.  The only time pointer-qualification is required with 
    LENGTHB is when the reference is to an adjustable bit/character string (or 
    a structure containing one) and the adjustable size variable is contained 
    within the referenced structure.  In all other cases, 
    pointer-qualification for BASED or DCB data is not needed for LENGTHB. 
Example: 
    DCL A BIT(5); 
    DCL B BIT(5) ALIGNED; 
    DCL 1 C, 
          2 D ALIGNED, 
            3 E BIT(5), 
            3 F BIT(5) ALIGNED, 
            3 G BIT(1), 
          2 H BIT(1) DALIGNED; 
From the above definitions, the results of the LENGTHB function would be as 
follows: 
    LENGTHB(A)     = 5 
    LENGTHB(B)     = 5 
    LENGTHB(C)     = 216 
    LENGTHB(C.D)   = 73 
    LENGTHB(C.D.E) = 5 
    LENGTHB(C.D.F) = 5 
    LENGTHB(C.D.G) = 1 
    LENGTHB(C.H)   = 1 
00003
00001
00002
Description: 
The LENGTHB preprocessor function returns the number of bits which result from 
a bit string expression. 
Format: 
LENGTHB (exp) 
Parameters: 
exp    is a bit string expression. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = LENGTHB ( '00101'B); 
    DCL A SBIN; 
    A = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = 5; 
    DCL A SBIN; 
            A = 5; 
    END DEMO; 
00002
00001
Description: 
The LENGTHC built-in function returns the number of characters required for 
the logical storage of a constant or reference.  This is the number of 
characters specified by DCLs for a reference, and does not include 
supplementary storage that might be implied by alignment requirements. 
Format: 
        {(reference     )} 
LENGTHC {(stringconstant)} 
        {(NIL           )} 
        {(ERASE         )} 
Parameters: 
reference    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted reference. 
stringconstant    a bit-string or character-string constant. 
Rules: 
1.  LENGTHC returns a UBIN WORD value. 
2.  LENGTHC is defined as follows: 
        LENGTHC(x) = integer part of (LENGTHB(x) + 8)/9 
    where x is a reference or a string constant. 
    NOTE:  The LENGTHC function is evaluated before the required alignment has 
    been performed.  Therefore, the function represents the logical size as 
    opposed to the physical size of the reference. 
3.  By definition 
        LENGTHC (NIL) = 0 
    and 
        LENGTHC (ERASE) = 1 
4.  If the argument of LENGTHC is a reference, then the reference may have any 
    storage class, and any data type except ENTRY. 
5.  If the LENGTHC function appears as the INIT value in a declaration of a 
    variable, and the argument is a reference, the argument may not indicate 
    an adjustable bit/character string or a structure containing one.  In 
    addition, a based reference must not be pointer qualified. 
6.  BASED and DCB data can be referenced without pointer-qualification in the 
    LENGTHC function.  The only time pointer-qualification is required with 
    LENGTHC is when the reference is to an adjustable bit/character string (or 
    a structure containing one) and the adjustable size variable is contained 
    within the referenced structure.  In all other cases, 
    pointer-qualification for BASED or DCB data is not needed for LENGTHC. 
Example: 
    DCL A CHAR(1); 
    DCL B CHAR(1) ALIGNED; 
    DCL 1 C DALIGNED, 
          2 D ALIGNED, 
            3 E BIT(1), 
            3 F CHAR(2), 
          2 G CHAR(1); 
From the above definitions, the results of the LENGTHC function would be as 
follows: 
    LENGTHC (A)      = 1 
    LENGTHC (B)      = 1 
    LENGTHC (C)      = 5 
    LENGTHC (C.D)    = 3 
    LENGTHC (C.D.E)  = 1 
    LENGTHC (C.D.F)  = 2 
    LENGTHC (C.G)    = 1 
00003
00001
00002
Description: 
The LENGTHC preprocessor function returns the number of characters which 
result from a character string expression. 
Format: 
LENGTHC (exp) 
Parameters: 
exp    is a character string expression. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = LENGTHC ( 'FOUR'); 
    DCL A SBIN; 
    A = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = 4; 
    DCL A SBIN; 
            A = 4; 
    END DEMO; 
00002
00001
Description: 
The LENGTHV built-in function returns the number of characters, less one, 
required for the logical storage of a constant or the count is based only on 
the number of characters required to represent the variable, not including 
character positions required by alignment considerations. 
Format: 
        {(reference     )} 
LENGTHV {(stringconstant)} 
        {(NIL           )} 
        {(ERASE         )} 
Parameters: 
reference    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted reference. 
stringconstant    a bit-string or character-string constant. 
Rules: 
1.  LENGTHV returns a UBIN WORD value. 
2.  LENGTHV is defined as follows: 
        LENGTHV(x) = integer part of (LENGTHB(x) + 8)/9) - 1 
    where x is a reference or a string constant. 
    NOTE:  The LENGTHV function is evaluated before the required alignment has 
    been performed.  Therefore, the function represents the logical size as 
    opposed to the physical size of the reference. 
3.  By definition 
        LENGTHV (NIL) = 0 
    and 
        LENGTHV (ERASE) = 1 
4.  If the argument of LENGTHV is a reference, then the reference may have any 
    storage class, and any data type except ENTRY. 
5.  If the LENGTHV function appears as the INIT value in the declaration of a 
    variable, and the argument is a reference, the argument may not indicate 
    an adjustable bit/character string or a structure containing one.  In 
    addition, a based reference must not be pointer qualified. 
6.  BASED and DCB data can be referenced without pointer-qualification in the 
    LENGTHV function.  The only time pointer-qualification is required with 
    LENGTHV is when the reference is to an adjustable bit/character string (or 
    a structure containing one) and the adjustable size variable is contained 
    within the referenced structure.  In all other cases, 
    pointer-qualification for BASED or DCB data is not needed for LENGTHV. 
Example: 
    DCL A CHAR(1); 
    DCL B CHAR(1) ALIGNED; 
    DCL 1 C DALIGNED, 
          2 D ALIGNED, 
            3 E BIT(1), 
            3 F CHAR(2), 
          2 G CHAR(1); 
From the above definitions, the results of the LENGTHV function would be as 
follows: 
    LENGTHV (A)     = 0 
    LENGTHV (B)     = 0 
    LENGTHV (C)     = 4 
    LENGTHV (C.D)   = 2 
    LENGTHV (C.D.E) = 0 
    LENGTHV (C.D.F) = 1 
    LENGTHV (C.G)   = 0 
00003
00001
00002
Description: 
The LENGTHW built-in function returns the number of words required for the 
logical storage of a constant or reference.  This is the number of words 
described by DCLs for a reference, and does not include supplementary storage 
that might be implied by alignment requirements. 
Format: 
        {(reference     )} 
LENGTHW {(stringconstant)} 
        {(NIL           )} 
        {(ERASE         )} 
Parameters: 
reference    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted reference. 
stringconstant    a bit-string or character-string constant. 
Rules: 
1.  LENGTHW returns a UBIN WORD value. 
2.  LENGTHW is defined as follows: 
        LENGTHW(x) = integer part of (LENGTHB(x) + 35)/36 
    where x is a reference or a string constant. 
    NOTE:  The LENGTHW function is evaluated before the required alignment has 
    been performed.  Therefore, the function represents the logical size as 
    opposed to the physical size of the reference. 
3.  By definition 
        LENGTHW (NIL) = 0 
    and 
        LENGTHW (ERASE) = 1 
4.  If the argument of LENGTHW is a reference, then the reference may have any 
    storage class and any data type except ENTRY. 
5.  If the LENGTHW function appears as the INIT value in the declaration of a 
    variable, and the argument is a reference, the argument may not indicate 
    an adjustable bit/character string or a structure containing one.  In 
    addition, a based reference must not be pointer qualified. 
6.  BASED and DCB data can be referenced without pointer-qualification in the 
    LENGTHW function.  The only time pointer-qualification is required with 
    LENGTHW is when the reference is to an adjustable bit/character string (or 
    a structure containing one) and the adjustable size variable is contained 
    within the referenced structure.  In all other cases, 
    pointer-qualification for BASED or DCB data is not needed for LENGTHW. 
Example: 
    DCL A CHAR(1); 
    DCL B CHAR(1) DALIGNED; 
    DCL 1 C, 
          2 D DALIGNED, 
            3 E BIT(1), 
            3 F SBIN ALIGNED, 
            3 G BIT(1), 
          2 H CHAR(1); 
From the above definitions, the results of the LENGTHW function would be as 
follows: 
    LENGTHW (A)     = 1 
    LENGTHW (B)     = 1 
    LENGTHW (C)     = 5 
    LENGTHW (C.D)   = 3 
    LENGTHW (C.D.E) = 1 
    LENGTHW (C.D.F) = 1 
    LENGTHW (C.D.G) = 1 
    LENGTHW (C.H)   = 1 
00003
00001
00002
LIST_PREPROC
LISTING_PREPROC
LISTING_PREPROC
LISTING_PREPROC
LISTING_PREPROC
LISTING_PREPROC
Description: 
In addition to %LIST and %PLIST, seven predefined preprocessor variables are 
provided to set and modify the listing facilities of the preprocessor. 
Format: 
         {LISTCON} 
         {LISTDIR} 
         {LISTEXP} 
%SET     {LISTINC}   = exp ; 
         {LISTMAC} 
         {LISTSUB} 
         {LISTCOM} 
Parameters: 
exp    is a bit string preprocessor expression. 
Rules: 
1.  %SET LISTCON='1'B; 
    Causes the listing output to include all lines which are within the 
    conditional %IF, %ELSEIF, %ELSE, and %ENDIF directives, as opposed to 
    listing only those lines which are associated with the %IF, %ELSEIF, or 
    %ELSE statements which evaluate to true ('1'B). 
2.  %SET LISTCON='0'B; 
    Causes the listing output to include only those lines which are associated 
    with the %IF, %ELSEIF, or %ELSE statements which evaluate to true ('1'B). 
3.  %SET LISTDIR='1'B;: 
    Causes listing output to include preprocessor directives. 
4.  %SET LISTDIR ='0'B; 
    Causes preprocessor directives to be excluded from the output listing. 
5.  %SET LISTEXP='1'B; 
    Causes listing output to include the results of all preprocessor 
    expressions instead of the original preprocessor expression itself. 
6.  %SET LISTEXP='0'B; 
    Causes listing output to include the text prior to evaluation of 
    preprocessor expressions instead of the resultant text. 
7.  %SET LISTINC='1'B; 
    Causes the listing output to include include-file text, subject to the 
    effects of other preprocessor listing directives contained in the 
    include-file text. 
8.  %SET LISTINC='0'B; 
    Causes listing output to skip all include file text. 
9.  %SET LISTMAC='1'B; 
    Causes macro expansions to be shown in the listing output. 
10. %SET LISTMAC='0'B; 
    Causes listing output to exclude expansions of macro invocations. 
11. %SET LISTSUB='1'B; 
    Causes listing output to include all substituted strings rather than the 
    original %SUB identifier. 
12. %SET LISTSUB='0'B; 
    Causes listing output to include only the original %SUB identifier and not 
    the substituted prepstring. 
13. %SET LISTCOM='1'B; 
    Causes listing output to include comments. 
14. %SET LISTCOM='0'B; 
    Causes listing output to exclude comments. 
15. The default settings for the listing variables are: 
    %SET LISTCON = '0'B; 
    %SET LISTDIR = '1'B; 
    %SET LISTEXP = '0'B; 
    %SET LISTINC = '0'B; 
    %SET LISTMAC = '0'B; 
    %SET LISTSUB = '0'B; 
    %SET LISTCOM = '1'B; 
16. Listing variables are used in the same manner that other preprocessor 
    bit-string variables are used. 
17. While these preprocessor variables are presented by using the %SET 
    directives, the %LSET directive can also be used to modify listing 
    variables, keeping in mind that the %LSET directive is restricted to use 
    within macros. 
18. The following table illustrates the interrelationship of %LIST, %PLIST, 
    %NLIST, LISTINC, and LISTMAC. 
    Directives Preceded By:   %LIST            %PLIST          %NLIST 
    -----------------------   -----            ------          ------ 
    %SET LISTINC = '1'B;      no effect        include files   no effect 
                                               are listed 
    %SET LISTMAC = '1'B;      no effect        macros are      no effect 
                                               listed 
    %LIST;                                     include files   listing resumes 
                                               and macros      according to 
                                               are listed      %LIST effect 
    %PLIST;                   include files                    listing resumes 
                              and macros                       according to 
                              are not listed                   %PLIST effect 
    %NLIST;                   all listing      all listing 
                              is suppressed    is suppressed 
Example: 
The following example illustrates %SET LISTCON = '1'B;: 
    OF_THE_ROAD: PROC; 
    %SET LISTCON = '1'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    DCL BASE UBIN CONSTANT INIT (2); 
    %ELSEIF NUM = 2; 
    DCL BASE UBIN CONSTANT INIT (8); 
    %ELSEIF NUM = 3; 
    DCL BASE UBIN CONSTANT INIT (10); 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    DCL BASE UBIN CONSTANT INIT (0); 
    %ENDIF; 
    END OF_THE_ROAD; 
The preceding source produces the following listing output: 
    OF_THE_ROAD: PROC; 
    %SET LISTCON = '1'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    DCL BASE UBIN CONSTANT INIT (2); 
    %ELSEIF NUM = 2; 
    DCL BASE UBIN CONSTANT INIT (8); 
    %ELSEIF NUM = 3; 
    DCL BASE UBIN CONSTANT INIT (10); 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    DCL BASE UBIN CONSTANT INIT (0); 
    %ENDIF; 
    END OF_THE_ROAD; 
The following example illustrates %SET LISTCON = '0'B;: 
    OF_THE_ROAD: PROC; 
    %SET LISTCON = '0'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    DCL BASE UBIN CONSTANT INIT (2); 
    %ELSEIF NUM = 2; 
    DCL BASE UBIN CONSTANT INIT (8); 
    %ELSEIF NUM = 3; 
    DCL BASE UBIN CONSTANT INIT (10); 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    DCL BASE UBIN CONSTANT INIT (0); 
    %ENDIF; 
    END OF_THE_ROAD; 
The preceding source produces the following listing output: 
    OF_THE_ROAD: PROC; 
    %SET LISTCON = '0'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    %ELSEIF NUM = 2; 
    %ELSEIF NUM = 3; 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    %ENDIF; 
    END OF_THE_ROAD; 
The following example illustrates %SET LISTDIR = '1'B;: 
    OF_THE_ROAD: PROC; 
    %SET LISTDIR = '1'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    DCL BASE UBIN CONSTANT INIT (2); 
    %ELSEIF NUM = 2; 
    DCL BASE UBIN CONSTANT INIT (8); 
    %ELSEIF NUM = 3; 
    DCL BASE UBIN CONSTANT INIT (10); 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    DCL BASE UBIN CONSTANT INIT (0); 
    %ENDIF; 
    END OF_THE_ROAD; 
The preceding source produces the following listing output: 
    OF_THE_ROAD: PROC; 
    %SET LISTDIR = '1'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    %ELSEIF NUM = 2; 
    %ELSEIF NUM = 3; 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    %ENDIF; 
    END OF_THE_ROAD; 
The following example illustrates %SET LISTDIR = '0'B;: 
    OF_THE_ROAD: PROC; 
    %SET LISTDIR = '0'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    DCL BASE UBIN CONSTANT INIT (2); 
    %ELSEIF NUM = 2; 
    DCL BASE UBIN CONSTANT INIT (8); 
    %ELSEIF NUM = 3; 
    DCL BASE UBIN CONSTANT INIT (10); 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    DCL BASE UBIN CONSTANT INIT (0); 
    %ENDIF; 
    END OF_THE_ROAD; 
The preceding source produces the following listing output: 
    OF_THE_ROAD: PROC; 
    %SET LISTDIR = '0'B; 
    DCL BASE UBIN CONSTANT INIT (16); 
    END OF_THE_ROAD; 
The following example illustrates %SET LISTEXP = '1'B;: 
    OF_THE_ROAD: PROC; 
    %SET LISTEXP = '1'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    DCL BASE UBIN CONSTANT INIT (2); 
    %ELSEIF NUM = 2; 
    DCL BASE UBIN CONSTANT INIT (8); 
    %ELSEIF NUM = 3; 
    DCL BASE UBIN CONSTANT INIT (10); 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    DCL BASE UBIN CONSTANT INIT (0); 
    %ENDIF; 
    END OF_THE_ROAD; 
The preceding source produces the following listing output: 
    OF_THE_ROAD: PROC; 
    %SET LISTEXP = '1'B; 
    %SET NUM = 4; 
    %IF '0'B; 
    %ELSEIF '0'B; 
    %ELSEIF '0'B; 
    %ELSEIF '1'B; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    %ENDIF; 
    END OF_THE_ROAD; 
The following example illustrates %SET LISTEXP = '0'B;: 
    OF_THE_ROAD: PROC; 
    %SET LISTEXP = '0'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    DCL BASE UBIN CONSTANT INIT (2); 
    %ELSEIF NUM = 2; 
    DCL BASE UBIN CONSTANT INIT (8); 
    %ELSEIF NUM = 3; 
    DCL BASE UBIN CONSTANT INIT (10); 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    DCL BASE UBIN CONSTANT INIT (0); 
    %ENDIF; 
    END OF_THE_ROAD; 
The preceding source produces the following listing output: 
    OF_THE_ROAD: PROC; 
    %SET LISTEXP = '0'B; 
    %SET NUM = 4; 
    %IF NUM = 1; 
    %ELSEIF NUM = 2; 
    %ELSEIF NUM = 3; 
    %ELSEIF NUM = 4; 
    DCL BASE UBIN CONSTANT INIT (16); 
    %ELSE; 
    %ENDIF; 
    END OF_THE_ROAD; 
The following example illustrates %SET LISTINC = '1'B;: 
The following include file is used in this example: 
    DCL 1 TIME_TRAVELERS, 
          2 SHERMAN CHAR (10), 
          2 MR_PEABODY CHAR (10), 
          2 WAYBACK_MACHINE$ PTR, 
          2 YEAR UBIN; 
    OF_THE_ROAD: PROC; 
    %SET LISTINC = '1'B; 
    %INCLUDE SAMPLE_INCLUDE_FILE; 
    TIME_TRAVELERS.YEAR = 1066; 
    END OF_THE_ROAD; 
The preceding source produces the following listing output: 
    OF_THE_ROAD: PROC; 
    %SET LISTINC = '1'B; 
    %INCLUDE SAMPLE_INCLUDE_FILE; 
    DCL 1 TIME_TRAVELERS, 
          2 SHERMAN CHAR (10), 
          2 MR_PEABODY CHAR (10), 
          2 WAYBACK_MACHINE$ PTR, 
          2 YEAR UBIN; 
            TIME_TRAVELERS.YEAR = 1066; 
    END OF_THE_ROAD; 
The following example illustrates %SET LISTINC = '0'B;: 
This example uses the previously listed include file, SAMPLE_INCLUDE_FILE. 
    OF_THE_ROAD: PROC; 
    %SET LISTINC = '0'B; 
    %INCLUDE SAMPLE_INCLUDE_FILE; 
    TIME_TRAVELERS.YEAR = 1066; 
    END OF_THE_ROAD; 
The preceding source produces the following listing output: 
    OF_THE_ROAD: PROC; 
    %SET LISTINC = '0'B; 
    %INCLUDE SAMPLE_INCLUDE_FILE; 
            TIME_TRAVELERS.YEAR = 1066; 
    END OF_THE_ROAD; 
The following example illustrates %SET LISTMAC = '1'B;: 
    ANONYMOUS: PROC; 
    %SET LISTMAC = '1'B; 
    %MACRO COSM; 
    DCL 1 UNIVERSE, 
          2 STARS UBIN, 
          2 PLANETS UBIN, 
          2 OTHER_STUFF BIT (1); 
    %MEND; 
    %COSM; 
    END ANONYMOUS; 
The preceding source produces the following listing output: 
    ANONYMOUS: PROC; 
    %SET LISTMAC = '1'B; 
    %MACRO COSM; 
    DCL 1 UNIVERSE, 
          2 STARS UBIN, 
          2 PLANETS UBIN, 
          2 OTHER_STUFF BIT (1); 
    %MEND; 
    %COSM; 
    DCL 1 UNIVERSE, 
          2 STARS UBIN, 
          2 PLANETS UBIN, 
          2 OTHER_STUFF BIT (1); 
    END ANONYMOUS; 
The following example illustrates %SET LISTMAC = '0'B;: 
    ANONYMOUS: PROC; 
    %SET LISTMAC = '0'B; 
    %MACRO COSM; 
    DCL 1 UNIVERSE, 
          2 STARS UBIN, 
          2 PLANETS UBIN, 
          2 OTHER_STUFF BIT (1); 
    %MEND; 
    %COSM; 
    END ANONYMOUS; 
The preceding source produces the following listing output: 
    ANONYMOUS: PROC; 
    %SET LISTMAC = '0'B; 
    %MACRO COSM; 
    DCL 1 UNIVERSE, 
          2 STARS UBIN, 
          2 PLANETS UBIN, 
          2 OTHER_STUFF BIT (1); 
    %MEND; 
    %COSM; 
    END ANONYMOUS; 
The following example illustrates %SET LISTSUB = '1'B;: 
    U_BOAT: PROC; 
    %SET LISTSUB = '1'B; 
    %SUB STRUCTURE = LINK_LIST; 
    %SUB CONTENTS = NAME; 
    %SUB LEN = 20; 
    DCL 1 STRUCTURE, 
          2 FLINK$ PTR, 
          2 BLINK$ PTR, 
          2 CONTENTS CHAR (LEN); 
    STRUCTURE.CONTENTS = 'ZIGVELT B. SCHNOOK'; 
    END U_BOAT; 
The preceding source produces the following listing output: 
    U_BOAT: PROC; 
    %SET LISTSUB = '1'B; 
    %SUB STRUCTURE = LINK_LIST; 
    %SUB CONTENTS = NAME; 
    %SUB LEN = 20; 
    DCL 1 LINK_LIST, 
          2 FLINK$ PTR, 
          2 BLINK$ PTR, 
          2 NAME CHAR (20); 
            LINK_LIST.NAME = 'ZIGVELT B. SCHNOOK'; 
    END U_BOAT; 
The following example illustrates %SET LISTSUB = '0'B;: 
    U_BOAT: PROC; 
    %SET LISTSUB = '0'B; 
    %SUB STRUCTURE = LINK_LIST; 
    %SUB CONTENTS = NAME; 
    %SUB LEN = 20; 
    DCL 1 STRUCTURE, 
          2 FLINK$ PTR, 
          2 BLINK$ PTR, 
          2 CONTENTS CHAR (LEN); 
    STRUCTURE.CONTENTS = 'ZIGVELT B. SCHNOOK'; 
    END U_BOAT; 
The preceding source produces the following listing output: 
    U_BOAT: PROC; 
    %SET LISTSUB = '0'B; 
    %SUB STRUCTURE = LINK_LIST; 
    %SUB CONTENTS = NAME; 
    %SUB LEN = 20; 
    DCL 1 STRUCTURE, 
          2 FLINK$ PTR, 
          2 BLINK$ PTR, 
          2 CONTENTS CHAR (LEN); 
            STRUCTURE.CONTENTS = 'ZIGVELT B. SCHNOOK'; 
    END U_BOAT; 
The following example illustrates %SET LISTCOM = '1'B;: 
    REMARK: PROC; 
    %SET LISTCOM = '1'B; 
    /* This comment will not appear in the listing output if 
       LISTCOM = '0'B. */ 
    END REMARK; 
The preceding source produces the following listing output: 
    REMARK: PROC; 
    %SET LISTCOM = '1'B; 
    /* This comment will not appear in the listing output if 
       LISTCOM = '0'B. */ 
    END REMARK; 
The following example illustrates %SET LISTCOM = '0'B;: 
    REMARK: PROC; 
    %SET LISTCOM = '0'B; 
    /* This comment will not appear in the listing output if 
       LISTCOM = '0'B. */ 
    END REMARK; 
The preceding source produces the following listing output: 
    REMARK: PROC; 
    %SET LISTCOM = '0'B; 
    END REMARK; 
Cross Reference: 
Please consult Preprocessor Expression and Function Facilities for information 
concerning bit string preprocessor expressions. 
00004
00003
00001
00002
LISTING_PREPROC
LISTING_PREPROC
Description: 
%LIST causes the expanded text of %MACRO invocations, and %INCLUDE files to be 
printed on the source listing output. 
Format: 
%LIST; 
Rules: 
1.  %LIST can be specified at any time and takes effect immediately. 
2.  %LIST directives must be on a single line. 
3.  %LIST and %PLIST have complimentary effects with respect to macros and 
    include files. 
4.  %LIST nullifies the effect of %NLIST and %PLIST. 
Example: 
    DEMO: PROC; 
    %LIST; 
    /* The following include file contains a macro, 
       and a data structure. */ 
    %INCLUDE SAMPLE_FILE; 
    %TOPO (PTR$ = TOPO$); 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO: PROC; 
    %LIST; 
    /* The following include file contains a macro, 
       and a data structure. */ 
    %INCLUDE SAMPLE_FILE; 
    %MACRO TOPO (PTR$ = PTR$); 
    DCL 1  TOPOGRAPHIC_INFO BASED (PTR$), 
           2  LOCATION_NAME CHAR (30), 
           2  LATITUDE, 
              3  DEGREES UBIN (8) UNAL, 
              3  MINUTES UBIN (6) UNAL, 
              3  SECONDS UBIN (6) UNAL, 
           2  LONGITUDE, 
              3  DEGREES UBIN (8) UNAL, 
              3  MINUTES UBIN (6) UNAL, 
              3  SECONDS UBIN (6) UNAL, 
           2 ALTITUDE UBIN (32) UNAL; 
    DCL PTR$ PTR; 
    %MEND; 
    DCL 1 ROUTE, 
           2 MILEAGE UBIN, 
           2 KILOMETERS UBIN, 
           2 TIME, 
             3 HOURS UBIN, 
             3 MINUTES UBIN, 
             3 SECONDS UBIN; 
    %TOPO (PTR$ = TOPO$); 
    DCL 1  TOPOGRAPHIC_INFO BASED (PTR$), 
           2  LOCATION_NAME CHAR (30), 
           2  LATITUDE, 
              3  DEGREES UBIN (8) UNAL, 
              3  MINUTES UBIN (6) UNAL, 
              3  SECONDS UBIN (6) UNAL, 
           2  LONGITUDE, 
              3  DEGREES UBIN (8) UNAL, 
              3  MINUTES UBIN (6) UNAL, 
              3  SECONDS UBIN (6) UNAL, 
           2 ALTITUDE UBIN (32) UNAL; 
    DCL PTR$ PTR; 
    END DEMO; 
The following source is the same as the source in the first example, however, 
it does not use the %LIST directive. 
    DEMO: PROC; 
    /* The following include file contains a macro, 
       and a data structure. */ 
    %INCLUDE SAMPLE_FILE; 
    %TOPO (PTR$ = TOPO$); 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO: PROC; 
    /* The following include file contains a macro, 
       and a data structure. */ 
    %INCLUDE SAMPLE_FILE; 
    %TOPO (PTR$ = TOPO$); 
    END DEMO; 
00002
00001
SET_EQU_LSET
Description: 
A macro is defined by using the %MACRO and %MEND directives.  The %MACRO 
directive alerts the preprocessor that a macro is being defined.  The 
preprocessor then processes the macro name, and the possible default 
identifier list (with an optional key identifier list), which follows the 
macro name, and then saves all of the macro text contained between the macro 
definition line and the %MEND directive for future invocations. 
Format: 
%MACRO  id [(default_id [, default_id] ... )]; 
    your choice of text 
%MEND; 
Parameters: 
id    is any valid preprocessor identifier. 
default_id    has the following two forms: 
1.  preprocessor identifier = prepstring 
        prepstring has the following two forms: 
    a.  any characters, (except a comma, right parenthesis, or a semicolon) 
        which are between the equal sign and one of the following delimiters: 
        a comma, a right parenthesis, or a semicolon. 
    b.  any characters (except a quotation mark (")) which are enclosed within 
        quotation marks. 
2.  identifier ( keyword_id = prepstring [, keyword_id = prepstring] ... [, 
    ANY]) = prepstring; 
        keyword_id has the same form as preprocessor identifier defined above, 
        and prepstring has the same form as defined above. 
        keyword_id limits the prepstrings, which can be used as substitutions 
        for identifiers in the default list, to those which are declared in 
        the keyword_id list.  When a keyword_id list is associated with a 
        default identifier only those keyword_ids which appear in the 
        keyword_id list may be used as substitutions in future macro 
        invocations.  An exception to this rule is the use of the ANY feature 
        in the keyword_id list.  When ANY follows the last keyword_id entry in 
        the keyword_id list, the user may substitute any prepstring for the 
        default_id when invoking the macro. 
Rules: 
1.  A macro can be defined at any place in a file, but its definition must 
    precede its first invocation. 
2.  Macros can contain any PL-6 text (data declarations, procedures, comments, 
    or any combinations). 
3.  Macros can contain any preprocessor text except the %EOD directive.  All 
    preprocessor expressions and directives except the %INCLUDE directive are 
    processed at invocation time, not at definition time. 
4.  The keyword identifier (keyword_id) associates its string with the 
    specified default identifier (default_id) when used in an invocation.  The 
    scope of a keyword identifier is limited to one particular default 
    identifier.  If the keyword ANY is specified, any valid prepstring may be 
    substituted for the default identifier at macro invocation time. 
5.  A default identifier list may extend over several lines.  Each line must 
    not end in the middle of a string. 
Example: 
    %MACRO ORCA_M (STCLASS = STATIC SYMDEF); 
    %LSET STR = CONCAT (TEXTCHAR (STCLASS), '      '); 
    %IF (SUBSTR (STR, 0, 6) = 'STATIC') 
     OR (SUBSTR (STR, 0, 8) = 'CONSTANT') 
     OR (SUBSTR (STR, 0, 3) = 'EXT'); 
        %LSET INIT = CHARTEXT ('INIT'); 
        %LSET INIT_END = CHARTEXT (' '); 
    %ELSE; 
        %LSET INIT = CHARTEXT ('/*'); 
        %LSET INIT_END = CHARTEXT ('*/'); 
    %ENDIF; 
    DCL 1 PALINDROMES STCLASS, 
        2 HIS CHAR (50) %INIT ('MADAM I''M ADAM') %INIT_END, 
        2 HERS CHAR (50) %INIT ('EVE') %INIT_END, 
        2 TEDDYS CHAR (50) %INIT ('A MAN, A PLAN, 
                   A CANAL - PANAMA') %INIT_END, 
        2 TOMS CHAR (50) %INIT ('GATE MAN SEES NAME, 
                   GARAGE MAN SEES NAME TAG') %INIT_END; 
    %MEND; 
00003
00001
00002
Description: 
Once a macro has been defined it may then be invoked.  Depending upon the 
definition of the macro, the user may invoke the macro in several different 
ways.  If the macro definition has no default identifier list the only manner 
of invoking the macro is: %identifier, where identifier is the same name used 
to define the macro.  If the macro has a default identifier list, the user may 
choose to invoke the macro substituting strings for any of the identifiers 
which are in the default identifier list of the macro definition, or the user 
may choose to leave the default identifiers unchanged. 
Format: 
%id [(reference_sub [,reference_sub] ... )]; 
Parameters: 
id    is any valid preprocessor identifier. 
reference_sub    has the following three forms: 
1.  reference_id = prepstring 
    where reference_id is any valid preprocessor identifier and prepstring has 
    the same form as defined in HELP (PL6) MACRO_DEFINITION. 
2.  reference_id = keyword_id 
    where keyword_id is any valid preprocessor identifier. 
3.  reference_id1 = reference_id2 
    where reference_id2 on the right side of the equal sign is a reference_id 
    from the reference_id parameter list of a containing macro.  This form of 
    a reference_sub is used only in nested macro invocations. 
Rules: 
1.  Macro invocation can occur anywhere within source text, with the following 
    restrictions: 
    a.  Macro invocation must be after macro definition. 
    b.  When a macro is invoked within the definition of a containing macro, 
        the expansion of the invoked macro does not take place within the 
        definition.  The macro, which is invoked within a containing macro 
        definition, is expanded only when the containing macro is invoked. 
    c.  Macro invocations must not be nested more than 256 levels deep. 
2.  The macro invocation must be on a line by itself, (i.e. no other PL-6 text 
    on the same line), but the text of a macro invocation can extend over 
    several lines.  However, a line must not end in the middle of a string. 
3.  A reference_id parameter must correspond to a default_id found in the 
    default_id list in the macro definition.  (See parameter replacement, rule 
    5 below.) 
4.  When a macro is invoked, the expanded macro text replaces the entire macro 
    reference, from the percent sign through the semicolon.  In addition, all 
    preprocessor directives are processed as they are encountered during 
    expansion of the macro text. 
5.  Parameter replacement occurs at macro invocation according to the 
    following rules: 
    a.  When a reference_id parameter corresponds to a default_id parameter 
        which has a keyword_id list, the keyword_id of the reference_id 
        parameter must match a keyword_id in the list; the string associated 
        with the keyword_id in the list then replaces the reference_id 
        parameter in the expanded macro text. 
        If a macro is invoked within another macro, the default_id list of the 
        containing macro is searched for a match to the reference_id parameter 
        in the immediately contained macro.  If found, the 'reference_id = 
        string' of the containing macro is placed in the macro invocation 
        reference_id list in place of the original reference_sub. 
        Default identifiers are added to the end of the reference identifier 
        list.  If an identifier is otherwise unreferenced, its default string 
        is substituted. 
    b.  Each line of text in the macro definition is processed in order of 
        appearance. 
    c.  Preprocessor directives are recognized and processed as they occur 
        within the macro. 
    d.  Each identifier in the macro text is checked for a match against a 
        reference_id in the reference_id list of the macro invocation.  If a 
        match exists, the identifier in the macro text is replaced with the 
        prepstring associated with the reference_id found in the reference_id 
        list. 
    e.  The line is rescanned and each identifier that matches a %SUB 
        identifier is replaced by the prepstring associated with the %SUB 
        identifier. 
    f.  The line is rescanned once more and each preprocessor expression is 
        evaluated and replaced with its external representation.  Please 
        consult the Preprocessor Expression and Function Facilities section 
        for a detailed explanation. 
6.  If ANY is listed as the last element of a keyword identifier list, the 
    user may substitute any prepstring for the default identifier which is 
    associated with that keyword identifier list. 
7.  If a default identifier in the default identifier list has a keyword list 
    associated with it, the user may invoke the macro using one of the keyword 
    identifiers associated with a particular default identifier, thereby 
    substituting the string, which is associated with the keyword identifier, 
    for all occurences of the default identifier in the macro text. 
Example: 
The following example shows the definition and invocation of a macro with no 
default_id list. 
    T:PROC; 
    %LIST; 
    %MACRO SIMPLE; 
    DCL PTR$ PTR; 
    DCL 1 TREE_STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 RIGHT_BRANCH$ PTR, 
          2 LEFT_BRANCH$ PTR; 
    %MEND; 
    %SIMPLE; 
    END T; 
The above source produces the following listing output: 
    T:PROC; 
    %LIST; 
    %MACRO SIMPLE; 
    DCL PTR$ PTR; 
    DCL 1 TREE_STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 RIGHT_BRANCH$ PTR, 
          2 LEFT_BRANCH$ PTR; 
    %MEND; 
    %SIMPLE; 
    DCL PTR$ PTR; 
    DCL 1 TREE_STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 RIGHT_BRANCH$ PTR, 
          2 LEFT_BRANCH$ PTR; 
    END T; 
The following example shows the definition and invocation of a macro which has 
a simple default_id list. In this example no substitution is made for the 
default_id when the macro is invoked. 
    T:PROC; 
    %LIST; 
    %MACRO SIMPLE (PTR$ = PTR$); 
    DCL PTR$ PTR; 
    DCL 1 TREE_STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 RIGHT_BRANCH$ PTR, 
          2 LEFT_BRANCH$ PTR; 
    %MEND; 
    %SIMPLE; 
    END T; 
The preceding source produces the following listing output: 
    T:PROC; 
    %LIST; 
    %MACRO SIMPLE (PTR$ = PTR$); 
    DCL PTR$ PTR; 
    DCL 1 TREE_STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 RIGHT_BRANCH$ PTR, 
          2 LEFT_BRANCH$ PTR; 
    %MEND; 
    %SIMPLE; 
    DCL PTR$ PTR; 
    DCL 1 TREE_STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 RIGHT_BRANCH$ PTR, 
          2 LEFT_BRANCH$ PTR; 
    END T; 
In the following example the macro is defined and invoked, and a substitution 
is made for the default_id when the macro is invoked. 
    T:PROC; 
    %LIST; 
    %SET LISTSUB = '1'B; 
    %MACRO SIMPLE (PTR$ = PTR$); 
    DCL PTR$ PTR; 
    DCL 1 TREE_STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 RIGHT_BRANCH$ PTR, 
          2 LEFT_BRANCH$ PTR; 
    %MEND; 
    %SIMPLE (PTR$ = TREE_PTR$); 
    END T; 
The preceding source produces the following listing output: 
    T:PROC; 
    %LIST; 
    %SET LISTSUB = '1'B; 
    %MACRO SIMPLE (PTR$ = PTR$); 
    DCL PTR$ PTR; 
    DCL 1 TREE_STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 RIGHT_BRANCH$ PTR, 
          2 LEFT_BRANCH$ PTR; 
    %MEND; 
    %SIMPLE (PTR$ = TREE_PTR$); 
    DCL TREE_PTR$ PTR; 
    DCL 1 TREE_STRUCTURE BASED (TREE_PTR$), 
          2 LEAF CHAR (10), 
          2 RIGHT_BRANCH$ PTR, 
          2 LEFT_BRANCH$ PTR; 
    END T; 
The following example shows a macro definition which has numerous 
default_id's.  The invocations make substitutions for some of the 
default_id's, enabling the user to change some of the identifiers, and even 
the structure of the data structure. 
    JOYCE_KILMER:PROC; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %MACRO ARBORETUM (PTR$ = PTR$, STRUCTURE = STRUCTURE, LEAF = LEAF, 
                     NEXT = NEXT$ PTR); 
    DCL PTR$ PTR; 
    DCL 1 STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 NEXT; 
    %MEND; 
    /* Make a binary tree structure. */ 
    %ARBORETUM (PTR$ = BIN_TREE_PTR$, STRUCTURE = BIN_TREE_STRUCTURE, 
                LEAF = BIN_TREE_CONTENTS, 
                NEXT = "LEFT_BRANCH$ PTR, 2 RIGHT_BRANCH$ PTR"); 
    /*Make a ternary tree. */ 
    %ARBORETUM (PTR$ = TRI_TREE_PTR$, STRUCTURE = TRI_TREE_STRUCTURE, 
                LEAF = TRI_TREE_CONTENTS, 
                NEXT = "LEFT_BRANCH$ PTR, 2 MIDDLE_BRANCH$ PTR, 
                        2 RIGHT_BRANCH$ PTR"); 
    END JOYCE_KILMER; 
The preceding source produces the following listing output: 
    JOYCE_KILMER:PROC; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %MACRO ARBORETUM (PTR$ = PTR$, STRUCTURE = STRUCTURE, 
                      LEAF = LEAF, 
                      NEXT = NEXT$ PTR); 
    DCL PTR$ PTR; 
    DCL 1 STRUCTURE BASED (PTR$), 
          2 LEAF CHAR (10), 
          2 NEXT; 
    %MEND; 
    /* Make a binary tree structure. */ 
    %ARBORETUM (PTR$ = BIN_TREE_PTR$, STRUCTURE = 
                BIN_TREE_STRUCTURE, 
                LEAF = BIN_TREE_CONTENTS, 
                NEXT = 
                "LEFT_BRANCH$ PTR, 2 RIGHT_BRANCH$ PTR" 
                ); 
    DCL BIN_TREE_PTR$ PTR; 
    DCL 1 BIN_TREE_STRUCTURE BASED (BIN_TREE_PTR$), 
          2 BIN_TREE_CONTENTS CHAR (10), 
          2 LEFT_BRANCH$ PTR, 2 RIGHT_BRANCH$ PTR; 
    /*Make a ternary tree. */ 
    %ARBORETUM (PTR$ = TRI_TREE_PTR$, STRUCTURE = 
                TRI_TREE_STRUCTURE, 
                LEAF = TRI_TREE_CONTENTS, 
                NEXT = "LEFT_BRANCH$ PTR, 2 MIDDLE_BRANCH$ 
                PTR, 2 RIGHT_BRANCH$ PTR"); 
    DCL TRI_TREE_PTR$ PTR; 
    DCL 1 TRI_TREE_STRUCTURE BASED (TRI_TREE_PTR$), 
          2 TRI_TREE_CONTENTS CHAR (10), 
          2 LEFT_BRANCH$ PTR, 2 MIDDLE_BRANCH$ PTR, 
          2 RIGHT_BRANCH$ PTR; 
    END JOYCE_KILMER; 
The following example uses the keyword_id option. 
    DR_GEORGE: PROC; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %MACRO WEATHER (FORCAST (LA = 'SMOG', SANFRAN = 'FOG') = 'SUNNY'); 
    DCL TODAYS_WEATHER CHAR (0) STATIC INIT (FORCAST); 
    %MEND; 
    %WEATHER (FORCAST = LA); 
    END DR_GEORGE; 
The preceding source produces the following listing output: 
    DR_GEORGE: PROC; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %MACRO WEATHER (FORCAST (LA = 'SMOG', SANFRAN = 'FOG') 
        = 'SUNNY'); 
    DCL TODAYS_WEATHER CHAR (0) STATIC INIT (FORCAST); 
    %MEND; 
    %WEATHER (FORCAST = LA); 
    DCL TODAYS_WEATHER CHAR (0) STATIC INIT ('SMOG'); 
    END DR_GEORGE; 
The following example uses a keyword_id list which has ANY specified as the 
last element of the list. 
    DR_GEORGE: PROC; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %MACRO WEATHER (FORCAST (LA = 'SMOG', SANFRAN = 'FOG', ANY) = 'SUNNY'); 
    DCL TODAYS_WEATHER CHAR (0) STATIC INIT (FORCAST); 
    %MEND; 
    %WEATHER (FORCAST = 'BLIZZARD'); 
    END DR_GEORGE; 
The preceding source produces the following listing output: 
    DR_GEORGE: PROC; 
    %SET LISTSUB = '1'B; 
    %LIST; 
    %MACRO WEATHER (FORCAST (LA = 'SMOG', SANFRAN = 'FOG', 
                    ANY) = 'SUNNY'); 
    DCL TODAYS_WEATHER CHAR (0) STATIC INIT (FORCAST); 
    %MEND; 
    %WEATHER (FORCAST = 'BLIZZARD'); 
    DCL TODAYS_WEATHER CHAR (0) STATIC INIT ('BLIZZARD'); 
    END DR_GEORGE; 
The following example illustrates three invocations of the same macro.  The 
first two invocations use the keyword_id option.  The last invocation relies 
on the default value of the default_id. 
    PIGS: PROC; 
    %SET LISTSUB= '1'B; 
    %LIST; 
    %MACRO FIVE_TOES (WHICH_PIGGY 
                      (PIGGY1 = 'WENT TO MARKET', PIGGY2 = 'STAYED HOME', 
                       PIGGY3 = 'HAD ROAST BEEF', PIGGY4 = 'HAD NONE', 
                       PIGGY5 = 'WENT WEE WEE WEE ALL THE WAY HOME', 
                       MISS_PIGGY = 'WENT WILD ON KERMIE') 
                       = 'WAS MAKIN'' BACON'); 
    AND_THIS_LITTLE_PIGGY = WHICH_PIGGY; 
    %MEND; 
    DCL AND_THIS_LITTLE_PIGGY CHAR (30); 
    %FIVE_TOES (WHICH_PIGGY = PIGGY1); 
    %FIVE_TOES (WHICH_PIGGY = MISS_PIGGY); 
    %FIVE_TOES; 
    END PIGS; 
The preceding source produces the following listing output: 
    PIGS:   PROC; 
    %SET LISTSUB= '1'B; 
    %LIST; 
    %MACRO FIVE_TOES (WHICH_PIGGY 
                      (PIGGY1 = 'WENT TO MARKET', PIGGY2 = 
                          'STAYED HOME', 
                       PIGGY3 = 'HAD ROAST BEEF', PIGGY4 = 
                           'HAD NONE', 
                       PIGGY5 = 
                       'WENT WEE WEE WEE ALL THE WAY HOME' 
                           , 
                       MISS_PIGGY = 'WENT WILD ON KERMIE') 
                           = 'WAS MAKIN'' BACON'); 
            AND_THIS_LITTLE_PIGGY = WHICH_PIGGY; 
    %MEND; 
    DCL AND_THIS_LITTLE_PIGGY CHAR (30); 
            %FIVE_TOES (WHICH_PIGGY = PIGGY1); 
            AND_THIS_LITTLE_PIGGY = 'WENT TO MARKET'; 
            %FIVE_TOES (WHICH_PIGGY = MISS_PIGGY); 
            AND_THIS_LITTLE_PIGGY = 'WENT WILD ON KERMIE'; 
            %FIVE_TOES; 
            AND_THIS_LITTLE_PIGGY = 'WAS MAKIN'' BACON'; 
    END PIGS; 
The following example contains macro invocations which are nested.  The string 
'THE BALL' is passed from the top level macro to an invoked macro.  In turn, 
the invoked macro passes 'THE BALL' to the macro which it invokes.  This legal 
procedure continues until the bottom level macro receives 'THE BALL', at which 
time the pass is complete. 
    FOOTBALL: PROC; 
    %SET LISTSUB = '1'B; 
    %SET LISTMAC = '1'B; 
    %LIST; 
    DCL INSTANT_REPLAY CHAR (20); 
    DCL THE_RECEIVER_HAS CHAR (20); 
    /* Watch the ball get passed from macro to macro. */ 
    %MACRO SECOND_DOWN (CENTER_HAS = 'THE BALL'); 
      INSTANT_REPLAY = CENTER_HAS; 
      %HIKE (QUARTERBACK_HAS = CENTER_HAS); 
    %MEND; 
    %MACRO HIKE (QUARTERBACK_HAS = 'BEEN TACKLED'); 
      INSTANT_REPLAY = QUARTERBACK_HAS; 
      %PASS (WHO_HAS = QUARTERBACK_HAS); 
    %MEND; 
    %MACRO PASS (WHO_HAS = 'WHO KNOWS?'); 
      INSTANT_REPLAY = WHO_HAS; 
      %CATCH (RECEIVER_HAS = WHO_HAS); 
    %MEND; 
    %MACRO CATCH (RECEIVER_HAS = 'DROPPED THE BALL'); 
      THE_RECEIVER_HAS = RECEIVER_HAS; 
    %MEND; 
    %SECOND_DOWN; 
    END FOOTBALL; 
The preceding source produces the following listing output: 
    FOOTBALL: PROC; 
    %SET LISTSUB = '1'B; 
    %SET LISTMAC = '1'B; 
    %LIST; 
    DCL INSTANT_REPLAY CHAR (20); 
    DCL THE_RECEIVER_HAS CHAR (20); 
    /* Watch the ball get passed from macro to macro. */ 
    %MACRO SECOND_DOWN (CENTER_HAS = 'THE BALL'); 
            INSTANT_REPLAY = CENTER_HAS; 
            %HIKE (QUARTERBACK_HAS = CENTER_HAS); 
    %MEND; 
    %MACRO HIKE (QUARTERBACK_HAS = 'BEEN TACKLED'); 
            INSTANT_REPLAY = QUARTERBACK_HAS; 
            %PASS (WHO_HAS = QUARTERBACK_HAS); 
    %MEND; 
    %MACRO PASS (WHO_HAS = 'WHO KNOWS?'); 
            INSTANT_REPLAY = WHO_HAS; 
            %CATCH (RECEIVER_HAS = WHO_HAS); 
    %MEND; 
    %MACRO CATCH (RECEIVER_HAS = 'DROPPED THE BALL'); 
            THE_RECEIVER_HAS = RECEIVER_HAS; 
    %MEND; 
            %SECOND_DOWN; 
            INSTANT_REPLAY = 'THE BALL'; 
            %HIKE (QUARTERBACK_HAS = CENTER_HAS); 
            INSTANT_REPLAY = 'THE BALL'; 
            %PASS (WHO_HAS = QUARTERBACK_HAS); 
            INSTANT_REPLAY = 'THE BALL'; 
            %CATCH (RECEIVER_HAS = WHO_HAS); 
            THE_RECEIVER_HAS = 'THE BALL'; 
    END FOOTBALL; 
00003
00001
00002
PROC_MATERIALIZE
Description: 
The MAXIMUM built-in function examines a list of arguments, and returns the 
value of the largest of the arguments. 
Format: 
MAXIMUM (arg1 [ , arg2] ... ) 
Parameters: 
arg1, arg2 ...    arguments to be compared. 
Rules: 
1.  All arguments in a MAXIMUM call must be of the same type so that 
    comparison is valid.  The single exception to this is:  UBIN and SBIN may 
    be mixed in the argument list. 
2.  The result of the MAXIMUM call will be of the same type as the arguments 
    of the call.  The exception to this is:  If UBIN and SBIN are mixed, the 
    result will be of type SBIN.  (Note that this may return undefined results 
    if the UBIN values exceed the precision of the SBIN storage.) 
3.  If BIT arguments differ in length, the shorter ones will be extended on 
    the right with 'O'B. 
4.  If CHAR arguments differ in length, the shorter ones will be extended on 
    the right with ASCII blanks. 
5.  Comparisons between PTR values which are offsets into different segments 
    are not guaranteed to be meaningful. 
6.  A maximum of 63 arguments may be specified in the argument list. 
00001
00002
Description: 
The MAX preprocessor function returns the maximum value in a list of sbin 
expressions. 
Format: 
MAX (exp [, exp] ... ) 
Parameters: 
exp    is an sbin expression. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = MAX (-123, 45 / 9, 67 + 48, 178 - 36); 
    DCL A SBIN; 
    A = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = 142; 
    DCL A SBIN; 
            A = 142; 
    END DEMO; 
00002
00001
Description: 
The MINIMUM built-in function examines a list of arguments, and returns the 
value of the smallest of the arguments. 
Format: 
MINIMUM (arg1 [ , arg2] ... ) 
Parameters: 
arg1, arg2 ...    arguments to be compared. 
Rules: 
1.  All arguments in a MINIMUM call must be of the same type so that 
    comparison is valid.  The single exception to this is:  UBIN and SBIN may 
    be mixed in the argument list. 
2.  The result of the MINIMUM call will be of the same type as the arguments 
    of the call.  The exception to this is:  If UBIN and SBIN are mixed, the 
    result will be of type SBIN.  (Note that this may return undefined results 
    if the UBIN values exceed the precision of the SBIN storage.) 
3.  If BIT arguments differ in length, the shorter ones will be extended on 
    the right with '0'B. 
4.  If CHAR arguments differ in length, the shorter ones will be extended on 
    the right with ASCII blanks. 
5.  Comparisons between PTR values which are offsets into different segments 
    are not guaranteed to be meaningful. 
6.  A maximum of 63 arguments may be specified in the argument list. 
00001
00002
Description: 
The MIN preprocessor function returns the minimum value in a list of sbin 
expressions. 
Format: 
MIN (exp [, exp] ... ) 
Parameters: 
exp    is an sbin expression. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = MIN (-123, 45 / 9, 67 + 48, 178 - 36); 
    DCL A SBIN; 
    A = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = -123; 
    DCL A SBIN; 
            A = -123; 
    END DEMO; 
00002
00001
Description: 
The MOD built-in function returns the remainder resulting from the division of 
one expression by another. 
Format: 
MOD (dvnd, dvsr) 
Parameters: 
dvnd    any arithmetic expression (the dividend). 
dvsr    any arithmetic expression (the divisor). 
Rules: 
1.  MOD returns an SBIN WORD result unless both of its arguments are UBIN in 
    which case it returns a UBIN WORD result. 
2.  MOD (dvnd, dvsr) = dvnd - (dvnd/dvsr)*dvsr. 
3.  The sign of the result is the same as the sign of the dividend. 
4.  The absolute value of the result is less than the absolute value of the 
    divisor.  Note that this definition may not be compatible with MOD 
    functions in other languages or on other machines. 
5.  If the divisor is zero, the result is undefined. 
6.  If the dividend is greater than (2**35)-1 then the result is undefined. 
Example: 
    MOD(4,3) =   1 
    MOD(4,-3) =  1 
    MOD(-4,3) = -1 
    MOD(-4,-3)   = -1 
    MOD(3*N+2,3) = (2 IF N>=0, or -1 if N<0) 
00003
00001
00002
Description: 
The MOD preprocessor function returns the remainder resulting from the 
division of one expression by another. 
Format: 
MOD (dvnd, dvsr) 
Parameters: 
dvnd, dvsr    are sbin expressions. 
Rules: 
1.  The result of the MOD function is an SBIN number. 
2.  MOD(dvnd, dvsr) = dvnd - (dvnd/dvsr) * dvsr 
3.  The sign of the result is the same as the sign of the dividend. 
4.  The absolute value of the result is less than the absolute value of the 
    divisor.  Note that this definition may not be compatible with the MOD 
    functions in other languages or on other machines. 
5.  The divisor must not be zero. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULTA = MOD (16, 5); 
    %EQU RESULTB = MOD(-16, 5); 
    DCL A SBIN; 
    DCL B SBIN; 
    A = %RESULTA; 
    A = %RESULTB; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULTA = 1; 
    %EQU RESULTB = -1; 
    DCL A SBIN; 
    DCL B SBIN; 
            A = 1; 
            B = -1; 
    END DEMO; 
00003
00001
00002
Description: 
%NLIST cause the suppression of the source listing output. 
Format: 
%NLIST; 
Rules: 
1.  The effect of %NLIST can be reversed by specifying the %LIST or %PLIST 
    directive. 
2.  %NLIST can be specified at any time.  It takes effect immediately. 
3.  %NLIST directives must be on a single line. 
Example: 
The following two examples include the file: SUM_DATA which contains: 
    DCL SUM SBIN; 
    DCL NUM SBIN; 
    DCL I UBIN; 
The following source uses the %NLIST directive. 
    DEMONSTRATE_NLIST : PROC; 
    %NLIST; 
    %INCLUDE SUM_DATA; 
    %MACRO SUM_10_CONSEC_NUMBERS; 
    SUM = 0; 
    DO I = NUM TO NUM + 9; 
    SUM = SUM + NUM; 
    END; 
    %MEND; 
    NUM = 0; 
    %SUM_10_CONSEC_NUMBERS; 
    NUM = 100; 
    %SUM_10_CONSEC_NUMBERS; 
    NUM = 1000; 
    %SUM_10_CONSEC_NUMBERS; 
    END DEMONSTRATE_NLIST ; 
The preceding source produces the following listing output: 
    DEMONSTRATE_NLIST : PROC; 
Note: The single line which appears above is the entire source listing output. 
The following source uses the %NLIST directive, which is then nullified by the 
%LIST directive. 
    DEMONSTRATE_NLIST : PROC; 
    %NLIST; 
    %INCLUDE SUM_DATA; 
    %MACRO SUM_10_CONSEC_NUMBERS; 
    SUM = 0; 
    DO I = NUM TO NUM + 9; 
    SUM = SUM + NUM; 
    END; 
    %MEND; 
    NUM = 0; 
    %SUM_10_CONSEC_NUMBERS; 
    NUM = 100; 
    %SUM_10_CONSEC_NUMBERS; 
    %LIST; 
    NUM = 1000; 
    %SUM_10_CONSEC_NUMBERS; 
    END DEMONSTRATE_NLIST ; 
The preceding source produces the following listing output: 
    DEMONSTRATE_NLIST : PROC; 
    %LIST; 
    NUM = 1000; 
    %SUM_10_CONSEC_NUMBERS; 
    SUM = 0; 
    DO I = NUM TO NUM + 9; 
       SUM = SUM + NUM; 
       END; 
    END DEMONSTRATE_NLIST ; 
00002
00001
The following table gives notation conventions used in this manual to describe 
commands, statements, directives, and other language elements.  The 
information can be accessed by either typing a ? or ??, or by typing: 
HELP (PL6) NOTATION_CONVENTIONS convention 
where LOWER_CASE, CAPITAL_LETTERS, 
SPECIAL_CHARACTERS, NUMERALS, BRACKETS, BRACES, OR_BAR, 
ELLIPSIS, VERTICAL_ELLIPSIS, and EXPONENTIATION are the 
available conventions. 
Example: HELP (PL6) NOTATION BRACES 
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
                An element inside brackets is optional.  If elements are 
                stacked vertically within brackets, the elements may be 
                omitted or one of them may be entered.  The brackets may be 
                elongated to contain the stack of elements, or may be 
                represented by vertically-stacked printed brackets.  For 
                example, the notation 
                    [DISK] 
                    [TAPE] 
                means that the user may omit this entry, or may enter DISK, or 
                may enter TAPE.  When used to enclose portions of keywords, 
                brackets signify that the bracketed portion may be omitted, or 
                truncated at any point.  For example, the notation K[EY] means 
                that the user may enter K, KE, or KEY. 
  Braces 
                Elements stacked inside a pair of braces identify a required 
                choice.  The braces may be elongated to contain the possible 
                choices, or may be represented by vertically-stacked printed 
                braces. 
                    {id }   means that either a value for id or the word ALL 
                    {ALL}   must be entered. 
                Alternatively, the vertical OR bar is used to separate the 
                choices, thus:  {id|ALL} 
  OR Bar 
                The OR bar separates elements in a list from which one element 
                may be, or must be, chosen. 
                    {A|id}    means that either the letter A or the value 
                              of id must be entered. 
  Horizontal Ellipsis 
                The horizontal ellipsis indicates that a previous bracketed 
                element may be repeated, or that elements have been omitted. 
                    name [, name] ...  means that one or more name values 
                             or        may be entered, with commas inserted 
                    name1[, name2] ... between the name values. 
  Vertical Ellipsis 
                The vertical ellipsis indicates that zero or more commands or 
                instructions have been omitted. 
                    DCL A SBIN WORD; 
                         .              means that there are zero or more 
                         .              statements omitted between the 
                         .              two DCL statements. 
                    DCL E SBIN WORD; 
  ** 
                ** represents exponentation.  It is not a PL6 operator, rather 
                it is used for documentation purposes. 
                    1000 = 10**3 
00010
00006
00005
00002
00002
00008
00010
00008
00008
00001
00004
00007
00003
00009
00009
NOTATION
Description: 
The null statement places a label at a particular point in a program; permits 
the use of a statement that causes no action and that does not alter 
sequential program execution. 
Format: 
[label:]; 
Parameters: 
label    any valid identifier. 
Rules: 
1.  When the statement is executed, no action occurs, and control passes to 
    the next sequential statement.  It is used primarily as a convenient way 
    of writing an ELSE clause that takes no action. 
2.  A null statement can appear anywhere in a PL-6 procedure. 
Example: 
    GAR: ; 
    ELSE; 
In the second example, the ELSE statement clause consists of a null statement. 
00003
00001
00002
OPTIONS
Description: 
The OPTIONAL attribute applies to the declaration of an entry point.  It 
directs the Linker not to issue an error message if it finds that no procedure 
enterable by this name is present in the object unit to be LINKed. 
Format: 
Form 1: 
DCL id ENTRY ASYNC OPTIONAL; 
Form 2: 
DCL id ENTRY [(n)] OPTIONAL; 
Rules: 
1.  The absence of the declared entry constant will not cause a severe error 
    during linking. 
2.  If referenced, the entry constant must have been declared as the PROC name 
    or secondary entry point of an external-level PROC or PROC ASYNC. 
3.  The presence or absence of a routine can be determined at run time by 
    comparing the ENTADDR of the routine to ENTADDR (NIL), i.e.: 
    IF ENTADDR(ROUTINE) = ENTADDR(NIL) THEN 
             . 
             . 
             . 
4.  An attempt to CALL an undefined (absent) entry constant will result in a 
    fault. 
Cross Reference: 
See the ENTADDR built-in function. 
00003
00001
00002
To obtain HELP messages for a particular Compiler Option, enter 
HELP (PL6) OPTIONS option 
For example, HELP (PL6) OPTIONS NWARN 
To obtain HELP messages for calling the PL6 compiler, type:  HELP (PL6) The 
compiler assumes LS, OU, MSCHEMA, NWARN and BC(ALL) unless specified 
otherwise.  Following is a complete list of the PL6 compiler options. 
ALT[SHARELIB]          MXR[EF]                NXR[EF] 
AUTOTEMP               NDM[AP]                OPTUI 
BC                     NFO[RMAT]              OU 
CP6                    NLEV[EL]               PM[AP] 
CSYS                   NLO                    SC[HEMA] 
DM[AP]                 NLPS                   SEV[ERITY] 
FEP                    NLS                    SH[ARELIB] 
FO[RMAT]               NLU                    SO 
GCOS                   NMDM[AP]               SR[CH] 
LEV[EL]                NOSH[ARELIB]           START 
LO                     NOU                    SYN[TAX] 
LPS                    NPM[AP]                SYS 
LS                     NSC[HEMA]              UI 
LU                     NSO                    UR[EF] 
MDM[AP]                NSYS                   WA[RN] 
MPM[AP]                NUI                    XR[EF] 
MSC[HEMA]              NUR[EF] 
MUR[EF]                NWA[RN] 
In the description of the compiler options, an "S" in the Note column 
indicates that the option is a standard compiler invocation option.  A "P" in 
this column indicates that the option is not a standard option.  An "X" in the 
Note column indicates that the option is not implemented; it is syntactically 
legal but is not supported.  Descriptions are in a tabular form with 3 columns 
as follows: 
  Option        Note    Explanation 
  ALT[SHARELIB] 
               P      Enables the user to specify in the object unit which 
                      default alternate shared library to use at link time. 
  AUTOTEMP(value) 
               P      This option is used only when the compiler issues a 
                      message specifically instructing the user to do so.  It 
                      is anticipated that circumstances requiring the use of 
                      this option will occur rarely, if at all. 
  BC[(list)] 
               S      Specifies that the batch compilation mode is to be used, 
                      that is, multiple procedures in the source file are to 
                      be compiled.  The list is a list of the sequence numbers 
                      of the procedures to be compiled, separated by commas, 
                      or is the word ALL.  The procedures in the source file 
                      are delimited by the preprocessor directive %EOD. The 
                      default is BC(ALL). 
  CP6 
               P      Specifies that object code for the CP-6 system is to be 
                      generated. The default is CP6. 
  CSYS 
               P      Produce a system file on the M$SYSTEM DCB from all 
                      MACRO, MAC, SET, EQU, and SUB preprocessor commands in 
                      the first compile unit.  Subsequent compile units in the 
                      same file will be processed with the newly built system 
                      file (see System File Facility).  This is off by 
                      default. 
  DM[AP][(suboptions)] 
               S      Generate data map.  The suboptions list is a list of 
                      storage classes, separated by commas.  Permitted storage 
                      classes are A[UTO], BA[SED], ST[ATIC], and SY[MREF]. The 
                      default is NDM.  The suboption default is all of the 
                      above. 
  FEP 
               P      Specifies that object code for the FEP system is to be 
                      generated. 
  FOR[MAT] 
               P      Format the source listing per the option list.  The 
                      default is NFORMAT. 
  GCOS 
               P      Specifies that object code for the GCOS system is to be 
                      generated. 
  LEV[EL] 
               P      Include nesting level information in listings. The 
                      default is LEVEL. 
  LO[(suboption)] 
               S      List object code.  The suboptions permit the option to 
                      be used to specify; list only procedure (CODE) or to 
                      specify list only (DATA). The default is NLO. The 
                      suboption default is both of the above. 
  LPS 
               P      List the output of the preprocessor.  The default is 
                      NLPS. 
  LS 
               S      List source program.  The default is LS. 
  LU 
               S      List the update file before listing the source.  The 
                      default is NLU. 
  MDM[AP][(suboptions)] 
               S      Generate mini data map.  The suboption list is a list of 
                      storage classes, separated by commas.  Permitted classes 
                      are A[UTO], BA[SED], ST[ATIC], and SY[MREF].  The 
                      default is NMDM. The suboption default is all of the 
                      above. 
  MPM[AP] 
               S      Generate mini procedure map.  The default is NMPM. 
  MSC[HEMA] 
               S      Generate mini schema.  The default is MSC. 
  MUR[EF] 
               S      Generate mini unreferenced variable listing.  The 
                      default is NUR. 
  MXR[EF] 
               S      Generate mini cross reference listing.  The default is 
                      NXR. 
  NDM[AP] 
               S      Do not generate data map.  The default is NDM. 
  NFOR[MAT] 
               S      Do not format source listing.  The default is NFOR. 
  NLEV[EL] 
               P      Do not include nesting level information in listing. 
                      The default is LEVEL. 
  NLO 
               S      Do not generate object code listing.  The default is 
                      NLO. 
  NLPS 
               P      Do not list preprocessor output. The default is NLPS. 
  NLS 
               S      Do not list source program.  The default is LS. 
  NLU 
               S      Do not list updates.  The default is NLU. 
  NMDM[AP] 
               S      Do not produce mini data map.  The default is NMDM. 
  NOSH[ARELIB] 
               P      Do not specify a default shared library for the linker 
                      in the object unit.  The default is NOSH. 
  NOU 
               S      Do not generate object unit.  The default is OU. 
  NPM[AP] 
               S      Do not generate procedure map.  The default is NPM. 
  NSC[HEMA] 
               S      Do not generate debug schema.  The default is MSC. 
  NSO 
               S      Do not produce updated source.  The default is NSO. 
  NSYS 
               P      Do not use any system file and do not search :LIBRARY 
                      for any include files.  The default is SYS. 
  NUI 
               S      Do not use update input.  The default is NUI. 
  NUR[EF] 
               S      Do not generate an unreferenced listing.  The default is 
                      NUR. 
  NWA[RN] 
               S      Do not generate warning messages.  The default is NWA. 
  NXR[EF] 
               S      Do not generate cross reference listing.  The default is 
                      NXR. 
  OPTUI 
               P      Optionally use Update Input, if any exists.  If not, 
                      proceed without erroring the compiler. 
  OU 
               S      Generate object unit.  The default is OU. 
  PM[AP] 
               S      Generate procedure map.  The default is NPM. 
  SC[HEMA] 
               S      Generate full debug schema.  The default is MSC. 
  SEV[ERITY](value) 
               P      Do not generate LO/DM/PM for compile unit if compile 
                      severity exceeds specified value. The default is 16. 
  SH[ARELIB] 
               P      Allows the user to specify the default shared library to 
                      be used at link time.  The default is NOSH. 
  SO 
               S      Produce updated source.  The default is NSO. 
  SR[CH] (list) 
               S      This option augments the specification of the accounts 
                      and packsets to be searched if the PL6 processor 
                      encounters an INCLUDE preprocessor directive which 
                      specifies a file only by file name. The list is a list 
                      of accounts, possibly qualified by packset,separated by 
                      commas.  Each account designation must have a leading 
                      period.  A maximum of eight accounts may be specified. 
                      If the file is not found in any of these accounts, the 
                      :LIBRARY account and the user's running account will 
                      then be searched.  Password designations are allowed 
                      also.  That is, .[account].password.  A second period 
                      specifies that a password is to be used in the search. 
  START 
               PX     Specifies that entry points and start of loops are to 
                      start on the boundary specified by value.  Legal values 
                      that may be specified are 1, 2, 4, and 8. 
  SYN 
               P      Do syntax checking only on the program. 
  SYS 
               P      Use a system file, if present, using the M$SYSTEM DCB. 
                      The default is SYS. 
  UI 
               S      Use update input.  The default is NUI unless UI fid is 
                      specified on invocation. 
  UR[EF] 
               S      Generate full unreferenced variable listing.  The 
                      default is NUR. 
  WA[RN] 
               S      List warning messages.  The default is NWA. 
  XR[EF] 
               S      Generate full cross reference listing.  The default is 
                      NXR. 
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
Description: 
The PALIGND built-in function, from a given pointer value, returns a pointer 
value that is double-word bounded, stepping to the next higher double word if 
necessary. 
Format: 
PALIGND (ptrexp) 
Parameters: 
ptrexp    a pointer-valued expression 
Rules: 
1.  ptrexp is any pointer-valued expression which may point to a word, 
    character, or bit location. 
2.  The result of the PALIGND is a pointer-value which points to a double-word 
    boundary, either equal to ptrexp or pointing to the next higher 
    double-word address.  The character and bit offsets will be zero in the 
    returned pointer value. 
3.  Note that address space wrap-around may occur at the addressing limit of 
    the pointer. 
00001
00002
Description: 
The PALIGNW built-in function, from a given pointer value, returns a pointer 
value that is word bounded, stepping to the next higher word if necessary. 
Format: 
PALIGNW (ptrexp) 
Parameters: 
ptrexp    a pointer-valued expression. 
Rules: 
1.  ptrexp is any pointer-valued expression which may point to a word, 
    character, or a bit location. 
2.  The result of PALIGNW is a pointer value which points to a word boundary, 
    either equal to ptrexp or pointing to the next higher word address.  The 
    character and bit offsets will be zero in the returned pointer value. 
3.  Note that address space wrap-around may occur at the addressing limit of 
    the pointer. 
00001
00002
Description: 
The PARAM attribute specifies a variable as a parameter. 
Format: 
entryname:  PROC [(p1 [, p2] ... )]; 
            DCL p1 [PARAM] [attributes]; 
Parameters: 
attributes    any legal attributes for parameters. 
entryname    any valid entry name. 
p1,p2    any valid identifier. 
Rules: 
1.  The parameter attribute may be specified explicitly or implicitly.  PARAM 
    may be explicitly used as a storage class or variables may be assigned the 
    parameter attribute by appearing in the parameter list of a PROC 
    statement. 
2.  Parameters must be declared with attributes in DCL statements. 
    Declarations of parameters must be internal to the procedure. 
3.  Only level 1 names or scalar items may appear in a parameter list. 
4.  Parameters in the PROC parameter list are separated by commas.  The 
    parameter list must be enclosed in parentheses. 
5.  If any parameters appear, a relationship is established between the 
    parameters in the PROC statement and the arguments in CALL statements 
    invoking the procedure.  There must be a one-to-one correspondence between 
    arguments and parameters. 
6.  Parameters may not have ENTRY, STATIC, CONSTANT, SYMREF, EXT, EXTROOT, 
    AUTO, BASED, AREAREF, REDEF, INIT or DCB attributes. 
7.  A PARAM can be declared as an adjustable CHAR or BIT string.  Such a 
    declaration in a parameter structure can be given only for the last 
    element in the structure declaration.  The length of the adjustable string 
    is evaluated at each reference to the parameter variable. 
Cross Reference: 
See the discussions of the ENTRY attribute, the ENTRY statement and the PROC 
statement . 
00003
00001
00002
Description: 
The PINCRB built-in function increments a specified pointer value by a given 
number of bits. 
Format: 
PINCRB (ptrexp, nrbits) 
Parameters: 
ptrexp    a pointer-valued expression. 
nrbits    an arithmetic expression. 
Rules: 
1.  PINCRB returns a PTR value.  Let k be the value of nrbits, and suppose 
    that ptrexp identifies a storage location starting at some bit B.  Then 
    the value returned by PINCRB identifies a storage location starting at the 
    bit defined by the algebraic sum of B plus k. 
2.  The value of nrbits may be positive or negative. 
3.  Note that address space wrap-around may occur at the addressing limit of 
    the pointer. 
00001
00002
Description: 
The PINCRC built-in function increments a specified pointer value by a given 
number of characters. 
Format: 
PINCRC (ptrexp, nrchars) 
Parameters: 
ptrexp    a pointer-valued expression. 
nrchars    an arithmetic expression. 
Rules: 
1.  PINCRC returns a PTR value.  Let k be the value of nrchars, and suppose 
    that ptrexp identifies a storage location starting at the nth bit of some 
    character C.  Then the value returned by PINCRC identifies a storage 
    location starting at the nth bit of the character defined by the algebraic 
    sum of C plus k. 
2.  The value of nrchars may be positive or negative. 
3.  Note that address space wrap-around may occur at the addressing limit of 
    the pointer. 
00001
00002
Description: 
The PINCRW built-in function increments a specified pointer value by a given 
number of words. 
Format: 
PINCRW (ptrexp, nrwords) 
Parameters: 
ptrexp    a pointer-valued expression. 
nrwords    an arithmetic expression. 
Rules: 
1.  PINCRW returns a PTR value.  Let k be the value of nrwords, and suppose 
    that ptrexp identifies a storage location starting at the nth bit of some 
    word W.  Then the value returned by PINCRW identifies a storage location 
    starting at the nth bit of the word defined by the algebraic sum of W plus 
    k. 
2.  The value of nrwords may be positive or negative. 
3.  Note that address space wrap-around may occur at the addressing limit of 
    the pointer. 
00001
00002
Description: 
%PLIST excludes include-file text, and macro expansion text from the source 
listing output. 
Format: 
%PLIST; 
Rules: 
1.  %PLIST can be specified at any time and takes effect immediately. 
2.  The %PLIST directive must be on a single line. 
3.  %PLIST and %LIST have complimentary effects with respect to macros and 
    include files. 
Example: 
The following two examples include the file: SUM_DATA, which contains: 
    DCL SUM SBIN; 
    DCL NUM SBIN; 
    DCL I UBIN; 
The following source uses the %PLIST directive. 
    DEMONSTRATE_PLIST : PROC; 
    %PLIST; 
    %INCLUDE SUM_DATA; 
    %MACRO SUM_10_CONSEC_NUMBERS; 
    SUM = 0; 
    DO I = NUM TO NUM + 9; 
    SUM = SUM + NUM; 
    END; 
    %MEND; 
    NUM = 0; 
    %SUM_10_CONSEC_NUMBERS; 
    NUM = 100; 
    %SUM_10_CONSEC_NUMBERS; 
    NUM = 1000; 
    %SUM_10_CONSEC_NUMBERS; 
    END DEMONSTRATE_PLIST ; 
The preceding source produces the following listing output: 
    DEMONSTRATE_PLIST : PROC; 
    %PLIST; 
    %INCLUDE SUM_DATA; 
    %MACRO SUM_10_CONSEC_NUMBERS; 
            SUM = 0; 
            DO I = NUM TO NUM + 9; 
               SUM = SUM + NUM; 
               END; 
    %MEND; 
            NUM = 0; 
            %SUM_10_CONSEC_NUMBERS; 
            NUM = 100; 
            %SUM_10_CONSEC_NUMBERS; 
            NUM = 1000; 
            %SUM_10_CONSEC_NUMBERS; 
    END DEMONSTRATE_PLIST ; 
The following source uses the %PLIST directive, which is then nullified by 
using the %LIST directive. 
    DEMONSTRATE_PLIST : PROC; 
    %PLIST; 
    %INCLUDE SUM_DATA; 
    %MACRO SUM_10_CONSEC_NUMBERS; 
    SUM = 0; 
    DO I = NUM TO NUM + 9; 
    SUM = SUM + NUM; 
    END; 
    %MEND; 
    NUM = 0; 
    %SUM_10_CONSEC_NUMBERS; 
    NUM = 100; 
    %SUM_10_CONSEC_NUMBERS; 
    %LIST; 
    NUM = 1000; 
    %SUM_10_CONSEC_NUMBERS; 
    END DEMONSTRATE_PLIST ; 
The preceding source produces the following listing output: 
    DEMONSTRATE_PLIST : PROC; 
    %PLIST; 
    %INCLUDE SUM_DATA; 
    %MACRO SUM_10_CONSEC_NUMBERS; 
            SUM = 0; 
            DO I = NUM TO NUM + 9; 
               SUM = SUM + NUM; 
               END; 
    %MEND; 
            NUM = 0; 
            %SUM_10_CONSEC_NUMBERS; 
            NUM = 100; 
            %SUM_10_CONSEC_NUMBERS; 
    %LIST; 
            NUM = 1000; 
            %SUM_10_CONSEC_NUMBERS; 
            SUM = 0; 
            DO I = NUM TO NUM + 9; 
               SUM = SUM + NUM; 
               END; 
    END DEMONSTRATE_PLIST ; 
00002
00001
Description: 
The POFFC built-in function returns a signed value that represents the 
positional relationship in characters between two storage locations. 
Format: 
POFFC (ptrexp1, ptrexp2) 
Parameters: 
ptrexp1, ptrexp2    pointer-valued expression. 
Rules: 
1.  POFFC returns an SBIN WORD value that represents the result obtained when 
    the word/character offset of ptrexp2 is subtracted from the word/character 
    offset of ptrexp1. 
2.  The result is undefined in the following cases: 
    a.  The segment identifiers of the two ptrexp are not the same. 
    b.  The bit offsets of the two ptrexp are not the same. 
00001
00002
Description: 
The POFFW built-in function returns a signed value that represents the 
positional relationship in words between two storage locations. 
Format: 
POFFW (ptrexp1, ptrexp2) 
Parameters: 
ptrexp1, ptrexp2    pointer-valued expression. 
Rules: 
1.  POFFW returns an SBIN WORD value that represents the result obtained when 
    the word offset of ptrexp2 is subtracted from the word offset of ptrexp1. 
2.  The result is undefined in the following cases: 
    a.  The segment identifiers of the two ptrexp are not the same. 
    b.  The bit offsets of the two ptrexp are not the same. 
    c.  The character offsets of the two ptrexp are not the same. 
Example: 
    DCL R SBIN; 
    DCL P$ PTR; 
    DCL Q$ PTR; 
          R=POFFW(P$, Q$); 
00003
00001
00002
A preprocessor directive must conform to the following rules: 
1.  Preprocessor directive lines must be separate from PL-6 text lines. 
2.  A %directive may appear in the middle of a PL-6 statement; however, it 
    must be on a separate line, (or lines, such that each syntactic element of 
    the %directive is not split across lines). 
3.  %directives are not recognized within PL-6 comments or within PL-6 
    character string constants. 
4.  Preprocessor expressions may be contained within a PL-6 text line. 
5.  Comments may be placed anywhere after the %directive. 
Available topics for PL6 preprocessor directives are: 
ASCBIN, ASCBIT, BINASC, BINBIT, BINXCHAR, BITASC, BITBIN 
CHARBIN, CHARTEXT, CONCAT, COUNT, EJECT, EOD, ERROR 
IF/ELSE/ELSEIF/ENDIF, INCLUDE, LENGTHB, LENGTHC, LIST 
LISTCON, LISTDIR, LISTEXP, LISTINC, LISTMAC, LISTSUB 
MAX, MIN, MOD, NLIST, PLIST, SET/EQU/LSET, SPACE, SUB/RESUB 
SUBBIT, SUBSTR, TEXTCHAR 
For further HELP on preprocessors, type: 
HELP (PL6) preprocessor-directive  displays the format and a 
                        description of the specified directive. 
HELP (PL6) SET_P RULES  displays the rules pertaining to SET 
HELP (PL6) SET_P FORMAT displays the format of the SET directive. 
HELP (PL6) RESUB_P EXAM displays an example illustraing RESUB. 
HELP (PL6) RESUB_P PA   displays the parameters of the RESUB directive. 
?                       displays the next level of HELP message. 
??                      displays all levels of the current HELP message. 
Description: 
A preprocessor expression is one of the following:  a preprocessor-variable 
reference, an sbin expression, a bit or character string expression, or a text 
expression.  An expression may be used within certain preprocessor directives, 
to direct the actions of the preprocessor or to modify its internal state. 
When used outside of preprocessor directives, a preprocessor expression causes 
a text representation of the resultant value of the preprocessor expression to 
be placed in the user's source program which will then be passed to the PL-6 
compiler. 
Format: 
%(exp) 
Parameters: 
exp    is a valid preprocessor expression. 
Rules: 
1.  A preprocessor expression can be specified anywhere outside of a 
    preprocessor directive, and in specific places within some preprocessor 
    directives.  The results will be placed in the text stream, starting at 
    the position occupied by the %. 
2.  A preprocessor expression can be one of the following: 
    a.  sbin preprocessor expression, which can have signed or unsigned 
        integer values. 
    b.  bit string preprocessor expression.  The expression must evaluate to a 
        bit string, 0 to 72 bits in length. 
    c.  character string preprocessor expression.  The expression must 
        evaluate to a properly delimited character string constant, i.e. a 
        string which is delimited by apostrophes. 
    d.  text expression, which is a character string expression represented 
        without delimiters, i.e. a string which is not delimited by 
        apostrophes. 
00001
00002
Description: 
The PROC statement delimits the beginning of a procedure; indicates the name 
of the primary entry point to the procedure; specifies the procedure 
parameters and options, if any. 
Format: 
                 [MAIN           ] 
entryname:  PROC [ASYNC          ] [ALTRET] [NOAUTO] [otheroptions]; 
                 [(parameterlist)] 
Parameters: 
parameterlist    a sequence of identifiers, separated by commas, denoting the 
parameters which may be passed to the procedure when it is called. 
otheroptions    control clauses.  See the sub-descriptions following for the 
AVOID and MATERIALIZE clauses of the PROC statement. 
Rules: 
Entryname 
1.  The entryname is implicitly declared as an entry constant.  It must not be 
    within a DO group or IF statement. 
Parameters 
1.  The parameter storage class is implicitly given to all names in the 
    parenthesized list following the keyword PROC. 
2.  Each parameter must be declared in a DCL statement immediately contained 
    in the procedure. 
3.  Parameters must not be substructure or structure element names. 
4.  Parameters may not be of data type ENTRY. 
ALTRET Attribute 
1.  ALTRET must be specified if the ALTRETURN statement is used in the 
    procedure. 
2.  If ALTRET is given on the PROC line, ALTRET is implied for all of the 
    procedure's entry points. 
3.  ALTRET should be specified if the ALTRET, WHENRETURN or WHENALTRETURN 
    option is specified on any CALL statement invoking the procedure. 
MAIN Attribute 
1.  The MAIN attribute is used to indicate that this procedure is the one to 
    which control will first be transferred at execution time. 
2.  The MAIN attribute may be specified only on an external procedure. 
ASYNC Attribute 
1.  The presence of the ASYNC attribute implies that the procedure will be 
    entered by the operating system in response to a previous program request 
    for user control of an exceptional condition. 
2.  An ASYNC procedure may not be invoked by a CALL statement. 
3.  The ASYNC attribute may appear only on an external procedure. 
Correspondence of Parameters and Arguments 
1.  When a procedure is invoked, a relationship is established between each 
    argument in the invoking construct and the positionally corresponding 
    parameter in the PROC statement. 
2.  Arguments correspond to parameters by reference.  This fact is of no 
    significance if the argument is an expression.  However, if the argument 
    is a reference, this means that a modification made to the corresponding 
    parameter is actually made to the argument.  If the argument is a 
    constant, then the programmer must ensure that the corresponding parameter 
    is not modified by the invoked procedure. 
Allocation of Automatic Storage 
1.  The user can control the way automatic storage is to be allocated by the 
    NOAUTO keyword on the external procedure definition. 
2.  NOAUTO indicates that the compiler is to allocate all data that normally 
    resides in automatic storage as if the user had specified the STATIC 
    attribute.  Automatic space is not acquired upon entry to the procedure. 
    Thus, use of this option restricts the procedure to being non-recursive. 
3.  NOAUTO is not the default value.  If not specified, automatic storage is 
    allocated as usual. 
00001
00002
PL-6 is a system implementation language that has the capacity and flexibility 
required for efficient system programming.  The PL-6 language, which is 
intended for block-structured programming, provides a simple syntax and simple 
data types.  The language requires no special coding forms.  Each statement is 
written as a string of characters without column requirements.  The PL-6 data 
types and data structures allow program data to be organized in a clear and 
convenient way.  The program syntax and control statements allow programs to 
be written in a modular, easy-to-read style. 
PL-6 programs typically perform commonly needed data processing functions by 
CALLs to the appropriate monitor services.  All monitor services, as 
documented in the Monitor Services Reference Manual, are directly CALLable by 
PL-6 programs.  To obtain more HELP information: 
HELP (PL6) TOPICS       prints a list of all available HELP messages 
HELP (PL6) statement    prints the syntax of a statement 
HELP (PL6) STATEMENT    explains the use of statements in PL6 programs 
HELP (PL6) ATTRIBUTES   explains the use of attributes in PL6 programs 
HELP (PL6) PREPROCESSOR explains the use of preprocessor directives 
                        in PL6 programs 
HELP (PL6) BUILT_IN     explains the use of built-in subroutines 
                        and function in PL6 programs 
?                       means give the next level of HELP message 
??                      means give all levels of the current message 
Description: 
The PROC statement, AVOID clause, informs the compiler not to use a specific 
pointer or index register. 
Format: 
                 [MAIN           ] 
entryname:  PROC [ASYNC          ] [ALTRET] [NOAUTO] 
                 [(parameterlist)] 
    AVOID (reg1[, reg2] ... ); 
Parameters: 
entryname    } 
MAIN         } 
ASYNC        } same as PROC statement. 
parameterlist} 
ALTRET       } 
NOAUTO       } 
reg    can be $PR5, $PR6, $PR7, $X5, $X6, or $X7. 
Rules: 
1.  A specific register can be specified only once. 
2.  The compiler will not use the specified register under any circumstances. 
    It will not save the register upon entry or restore it upon exit. 
3.  It is possible that the compiler will be unable to compile a statement due 
    to the lack of an index or pointer register. If this happens, the compiler 
    will issue a diagnostic informing the user that more registers are 
    required. 
4.  A procedure which specifies AVOID may only call procedures which also 
    specify AVOID.  This restriction will be enforced by the linker. 
00001
00002
Description: 
The PROC statement, MATERIALIZE clause, causes a pointer value from one of the 
pointer registers to be stored into memory. 
Format: 
                 [MAIN           ] 
entryname:  PROC [ASYNC          ] [ALTRET] [NOAUTO] 
                 [(parameterlist)] 
    MATERIALIZE ($PRn1 IN id1 [, $PRn2 IN id2 [, $PRn3 IN id3]]); 
Parameters: 
entryname    } 
MAIN         } 
ASYNC        } same as PROC statement. 
parameterlist} 
ALTRET       } 
NOAUTO       } 
$PRn    can be $PR0, $PR1, $PR2, $PR3, $PR4, $PR5, $PR6, or $PR7. 
idn    reference to an automatic or static pointer variable; that is, the 
pointer variable must not be a structure or substructure element or an array, 
and must be of storage type AUTO, STATIC, EXT, EXTROOT, SYMREF, AREAREF, or 
STATIC AREADEF. 
Rules: 
1.  A specific pointer register can be specified only once in the MATERIALIZE 
    clause. 
2.  Upon entry to the external procedure, following procedure initialization, 
    the value of the specified pointer register is automatically stored into 
    the specified id.  There is no implicit restoring of the pointer register 
    upon exit from the procedure.  However, the same pointer register may be 
    specified in the AVOID clause if desired. 
00001
00002
Description: 
The PTR attribute declares an identifier as a pointer variable. 
Format: 
DCL id PTR; 
Parameters: 
id    any valid identifier. 
Rules: 
1.  The identifier may be a scalar variable, an array name, or a structure 
    element.  It is declared as pointer-type data. 
2.  Pointer variables may point to (or identify) based data. 
3.  A pointer variable may be assigned only a pointer value; that is, the 
    value of another pointer variable, or the value returned by a pointer 
    valued built-in function. 
4.  A pointer variable may be null.  ADDR(NIL) represents this null value and 
    may be compared to or assigned. 
5.  A pointer variable may be initialized only with the ADDR built-in 
    function. 
6.  Arithmetic operations are not allowed on pointer variables. 
Example: 
    DCL P$ PTR; 
    DCL POINTER_ARRAY$ (0:10) PTR; 
Cross Reference: 
See the ADDR, DCBADDR, PINCRB, PINCRC, POFFC and POFFW built-in functions. 
00004
00003
00001
00002
Description: 
The PTRDSCR built-in function allows the user to get the descriptor which 
underlies a pointer. 
Format: 
PTRDSCR (ptr-ref) 
Parameters: 
ptr-ref    a possibly pointer qualified, possibly structure qualified, 
possibly subscripted reference. 
Rules: 
1.  The PTRDSCR returns a DSCR value. 
2.  The code generated is: 
        LDPn    ptr-ref 
        STDn    DSCR-loc 
    thus returning the descriptor which underlies the referenced pointer. 
00001
00002
00003
Description: 
The READONLY attribute specifies that the declared variable is in read-only 
memory. 
Format: 
DCL id ... { SYMREF  } READONLY ... ; 
           { AREAREF } 
Rules: 
1.  The READONLY attribute must immediately follow the storage class keywords 
    SYMREF or AREAREF. 
2.  When READONLY is specified, the corresponding SYMDEF/AREADEF definition 
    must have the CONSTANT storage class. 
3.  Since the compiler is informed that the variable described cannot be 
    modified, the specification of READONLY may result in improved code 
    generation. 
00001
Description: 
The REDEF attribute allows the same storage location to be described by 
different data description entries. 
Format: 
DCL id2 [array] REDEF id1 [a1] ... ; 
Parameters: 
id1, id2    any valid identifiers. 
array    any valid array specification. 
a1    any valid data attribute. 
Rules: 
1.  The REDEF attribute must immediately follow id2 or the array specification 
    if present. 
2.  The level numbers of id1 and id2 must be identical.  If the level number 
    is one, a separate declaration statement (DCL) must be made. 
3.  The data attributes allowed for a1 are any legal scalar or structure 
    description. 
4.  The data description of id1 may contain an array specification.  In this 
    case, the redefinition of id1 represents the area allocated for the entire 
    array.  In addition, id1 may be subordinate to an item whose description 
    contains an array specification. 
5.  Either id1 or id2 may contain an item whose size is variable. 
    a.  If an adjustable length string is within a structure, it must be 
        declared last. 
    b.  For REDEF checking purposes, the physical size of an adjustable length 
        string is defined to be zero bits. 
    c.  Between two items, if the physical size of either one is zero bits, 
        then REDEF is legal. 
    d.  Between two items, both with non-zero size, REDEF is legal only if the 
        physical sizes match exactly. 
6.  No entry having a level-number numerically lower than the level-number of 
    id1 may occur between the description of id1 and id2.  If a level number 
    equal to the level number of id2 occurs between the description of id1 and 
    id2, then that description must also contain a REDEF of id1. 
7.  Redefinition starts at id2 and ends when a level number less than or equal 
    to id2 is encountered. 
8.  The alignment of id1 will be forced to the alignment of id2 if id2 
    requires a boundary alignment of greater resolution. 
9.  Multiple redefinitions of the same storage area are allowed.  All 
    redefinitions must use the identifier that originally defined the area. 
10. The INIT clause is not allowed on entries having the REDEF attribute or on 
    entries subordinate to redefined entries. 
11. Storage classification clauses (BASED, AUTO, STATIC, AREAREF, CONSTANT, 
    EXT, EXTROOT, SYMREF, DCB) are not legal on a redefinition.  All storage 
    class attributes of id1 apply to id2 including implied pointers if 
    specified. 
12. The SYMDEF/AREADEF clause is not allowed on a redefinition. 
Example: 
    DCL A BASED(P$) UBIN WORD; 
    DCL C REDEF A CHAR(4); 
    DCL B REDEF A SBIN WORD; 
    DCL 1 SYMDEF_ENTRY, 
          2 VALUE SBIN WORD, 
          2 SEC_TYPE REDEF VALUE, 
            3 LOADEFLAGS BIT(9), 
            3 SECT_NO UBIN BYTE UNAL, 
            3 OFFSET_VAL UBIN HALF UNAL, 
          2 NAME_POINTER UBIN HALF UNAL, 
          2 FLAG BIT(1), 
          2 * BIT(17); 
    DCL 1 J, 
          2 W (0:2), 
            3 L CHAR(4), 
            3 E REDEF L UBIN WORD, 
          2 JOHN CHAR(8), 
          2 G (0:7) REDEF JOHN UBIN BYTE UNAL; 
00003
00001
00002
Description: 
The REMEMBER statement causes information about the current state, or dynamic 
environment, to be stored such that a subsequent UNWIND statement causes this 
state to be restored. 
Format: 
[label:] REMEMBER id IN var; 
Parameters: 
id    label of the statement at which execution will continue following 
execution of the UNWIND statement. 
var    a variable of data type REMEMBER. 
Rules: 
1.  The programmer must ensure that the procedure that sets up a given 
    REMEMBER variable using the above statement is active (i.e., is a member 
    of the current dynamic environment) whenever an UNWIND TO that variable is 
    executed. 
2.  The programmer must ensure that a given REMEMBER variable is accessible to 
    any procedure which expects to UNWIND TO it. 
3.  The label in the REMEMBER statement must be immediately contained in the 
    same procedure as the REMEMBER statement. 
4.  A REMEMBER statement is legal only in an external procedure. 
5.  The REMEMBER statement can only reference data of type REMEMBER. 
00001
00002
Description: 
The REMEMBER attribute declares a data item which is to be used with the 
REMEMBER and UNWIND statements. 
Format: 
DCL id REMEMBER; 
Parameters: 
id    any valid identifier. 
Rules: 
1.  The identifier may be a scalar variable, an array name, or a structure 
    element.  It is declared as a REMEMBER variable. 
2.  REMEMBER data can only be used with the REMEMBER and UNWIND statements. 
3.  REMEMBER data type is defined internally as BIT(72) DALIGNED. 
4.  The value of a REMEMBER variable uniquely identifies a program environment 
    and point of continuation. 
Cross Reference: 
See the REMEMBER and UNWIND statements. 
00003
00001
00002
KEYWORDS
SUB_RESUB_PREPROC
Description: 
The RETURN/ALTRETURN statement terminates execution of a procedure and returns 
control to the invoking procedure. 
Format: 
[label:] {RETURN;   } 
         {ALTRETURN;} 
Rules: 
1.  When a RETURN/ALTRETURN statement is used in a procedure invoked by the 
    CALL statement, control is returned to the statement immediately following 
    the CALL statement if RETURN is specified; if ALTRETURN is specified, 
    control is returned to the label specified on the ALTRET option of the 
    CALL statement.  If an ALTRET label, WHENRETURN or WHENALTRETURN was not 
    specified on the CALL, then ALTRETURN functions like RETURN. 
2.  ALTRETURN cannot be executed in a procedure that does not have the ALTRET 
    attribute. 
3.  When RETURN is executed in an ASYNC procedure, execution will be resumed 
    at the point at which the exceptional condition that originally caused 
    entry to the ASYNC procedure occurred.  (This is accomplished by using the 
    M$TRTN monitor service.) 
4.  When ALTRETURN is executed in an ASYNC procedure, control will be given to 
    the operating system for standard processing of the exceptional condition. 
    (This is accomplished by using the M$MERCS monitor service.) 
5.  When RETURN is executed in a MAIN procedure, control will be returned to 
    the operating system by using the M$EXIT monitor service.  The program 
    terminates normally. 
6.  When ALTRETURN is executed in a MAIN procedure, control will be returned 
    to the operating system by using the M$ERR monitor service.  The program 
    terminates abnormally. 
Cross Reference: 
Descriptions of the M$TRTN, M$EXIT and M$ERR monitor services may be found in 
the Monitor Services Reference manual. 
Example: 
            CALL CALC (Z, 7) ALTRET(L1); 
    L1:     X=X*Z; 
    EGD:    PROC (A, B) ALTRET; 
            IF A>B THEN 
               ALTRETURN; 
            ELSE 
               RETURN; 
    END EGD; 
The procedure, CALC, is called as a subroutine, with the ALTRET option.  If A 
is greater than B, CALC executes an ALTRETURN; control returns to the 
statement labeled L1.  If A is not greater than B, control returns to the 
statement following the CALL. 
00002
00003
00001
Description: 
The SBIN attribute declares an identifier as representing data of the signed, 
fixed-point binary format. 
Format: 
            [HALF    ] 
DCL id SBIN [WORD    ] [a] ... ; 
            [BYTE    ] 
            [(length)] 
Parameters: 
id    any valid identifier representing a scalar variable, array name or 
structure element. 
length    number of bits in the integer -1. 
a    any other valid attribute. 
HALF    use 17-bit precision. 
WORD    use 35-bit precision. 
BYTE    use 8-bit precision. 
Rules: 
1.  WORD will be assumed if a length attribute is not specified; that is, 
    default is 36 bits. 
2.  Length indicates the amount of storage reserved for the value of id.  The 
    maximum length is 36 bits. 
3.  The length attribute must be a decimal integer constant, with a range of 1 
    to 36. 
4.  The length attribute must immediately follow the SBIN attribute, with or 
    without intervening spaces. 
5.  If an arithmetic overflow condition occurs, results are undefined. 
Cross Reference: 
See BYTE, HALF, and WORD Attributes. 
Example: 
    DCL SHORT SBIN BYTE; 
    DCL MEDIUM SBIN HALF; 
    DCL LONG SBIN WORD; 
    DCL XX SBIN(24); 
00003
00004
00001
00002
Description: 
The SEARCH built-in subroutine searches a character string from left to right 
looking for the first/next occurrence of any one character from a set 
specified by a 512 character table. 
Format: 
CALL SEARCH (index, tableval, table, string [,start]) 
    [ALTRET (label)                                 ]; 
    [[WHENRETURN DO group ] [WHENALTRETURN DO group]] 
Parameters: 
index, tableval, table    possibly pointer-qualified, possibly 
structure-qualified, possibly subscripted references. 
string    any character expression. 
start    any arithmetic expression. 
label    any valid label. 
Rules: 
1.  table is a word-aligned 512 character reference of BIT or CHAR data type 
    that will control the search.  The elements of the table must be CALIGNED, 
    and the table structure must start on a word boundary.  If C is a 
    character and J = ASCBIN (C), then table (J) is a BYTE field (i.e., 
    character-aligned) representing the table value for C. 
2.  string represents the character string to be searched, left to right, 
    character by character, for any character with a non-zero table value. 
3.  start represents an optional integer quantity which determines the 
    character position where the search is to begin.  Legal values for start 
    are defined as follows: 
        0 <= start < LENGTHC (string) 
    If start is not specified, the default value is 0. 
4.  index is a word aligned UBIN WORD value which is assigned the character 
    number of the leftmost character that stopped the search.  If the search 
    is unsuccessful, index will be assigned LENGTHC (string). 
5.  tableval is a word aligned UBIN WORD value which is assigned the table 
    entry corresponding to the character that stopped the search.  If the 
    search is unsuccessful, tableval will be assigned zero. 
6.  If the SEARCH is unsuccessful the SEARCH operation will ALTRETURN. 
7.  The nth table entry will only be accessed if a character within string has 
    a character-code of n.  If the programmer is confident that all characters 
    in the string have character-codes less than 128 (for example), then the 
    table need have only 128 entries, and no error or fault will occur. 
00001
00002
Description: 
The SEARCHR built-in subroutine searches a character string from right to left 
looking for the first/next occurrence of any one character from a set 
specified by a 512 character table. 
Format: 
CALL SEARCHR (index, tableval, table, string [,start]) 
    [ALTRET (label)                                 ]; 
    [[WHENRETURN DO group ] [WHENALTRETURN DO group]] 
Parameters: 
index, tableval, table    possibly pointer-qualified, possibly 
structure-qualified, possibly subscripted references. 
str1    any character expression. 
start    any arithmetic expression. 
label    any valid label. 
Rules: 
1.  table is a word-aligned 512 character reference of BIT or CHAR data type 
    that will control the search.  The elements of the table must be CALIGNED, 
    and the table structure must start on a word boundary.  If C is a 
    character and J = ASCBIN (C), then table (J) is a BYTE field (i.e., 
    character-aligned) representing the table value for C. 
2.  string represents the character string to be searched, right to left, 
    character by character, for any character with a non-zero table value. 
3.  start represents an optional integer quantity which determines the 
    character position where the search is to begin.  The first character 
    tested is start-1.  Legal values for start are defined as follows: 
        1 <= start <= LENGTHC (string) 
    If start is not specified, the default value is LENGTHC (string). 
4.  index is a word aligned UBIN WORD value which is assigned the character 
    number of the rightmost character that stopped the search.  If the search 
    is unsuccessful, index will be assigned start. 
5.  tableval is a word aligned UBIN WORD value which represents the table 
    entry corresponding to the character that stopped the search.  If the 
    search is unsuccessful, tableval will be assigned zero. 
6.  If the SEARCH is unsuccessful, the SEARCH operation will ALTRETURN. 
7.  The nth table entry will only be accessed if a character within string has 
    a character-code of n.  If the programmer is confident that all characters 
    in the string have character-code less that 128 (for example), then the 
    table need have only 128 entries, and no error or fault will occur. 
00001
00002
Description: 
The SELECT statement defines the start of a select to be executed when the 
expression in the DO SELECT group matches one of the arguments of the SELECT 
statement. 
Format: 
SELECT [(]const1[, const2] ... [)]; 
         or 
SELECT [(][yconst1, [yconst2,] ... ] ELSE [, zconst1[, zconst2] ... ][)]; 
Parameters: 
constn    any UBIN, SBIN, BIT or CHAR constant specifying a value of the DO 
SELECT expression for which this select is to be executed. 
yconst,zconst    see Rule 3. 
Rules: 
1.  SELECT statements are used between the DO SELECT statement and its 
    corresponding END statement.  The code between a given SELECT statement 
    and the next SELECT statement, or END statement matching the DO SELECT, 
    will be executed whenever that SELECT statement specifies a constant equal 
    to the value of the DO SELECT expression. 
2.  A label is not permitted on the SELECT statement. 
3.  If ELSE is specified, the code following the SELECT/ELSE statement will be 
    executed if the value of the DO SELECT exp does not match any of the 
    constants specified on any other SELECT statement associated with the DO 
    SELECT group. 
    The list of yconst(s) and zconst(s) does not affect the execution of the 
    statement.  Provision for these lists is made so that the programmer can 
    remind himself of certain possible values of the DO SELECT expression for 
    which he has not written an ELSE-less SELECT group and which, if they 
    occur, will cause execution of the SELECT/ELSE group.  Note that there can 
    be but one SELECT/ELSE statement in a DO SELECT group. 
4.  If ELSE is not specified, and the evaluation of the DO SELECT does not 
    result in a match with any SELECT statement, control will be transferred 
    to the corresponding END statement. 
5.  It is an error to have multiple specifications of the same constant or 
    ELSE.  That is, each list of const(s) in a SELECT statement must be 
    mutually exclusive with the other such lists in the group, and with the 
    yconst(s) and zconst(s) in the SELECT/ELSE statement. 
6.  DO SELECT should be used when dealing with a large, sparse range of CASE 
    values. However, DO CASE produces much faster code for most situations 
    involving UBIN values. 
Cross Reference: 
See the DO SELECT statement. 
00003
00001
00002
Description: 
The %SET, %EQU, and %LSET directives assign the value of a specified 
expression to a specified preprocessor-variable identifier.  The variable can 
then be referenced in preprocessing, and/or the value of the variable can be 
passed on to the compiler as a constant. 
Format: 
%SET id = exp ; 
%EQU id = exp ; 
%LSET id = exp ; 
Parameters: 
id    is any valid preprocessor identifier. 
exp    is one of the following preprocessor expressions: 
1.  an SBIN expression. 
2.  a bit string expression where the expression evaluates to a bit string 
    which is 0 to 72 bits in length. 
3.  a character string expression where the expression evaluates to a 
    character string, of no more than 272 characters. A character string 
    begins and ends with an apostrophe ('), e.g. 'STRING OF PEARLS'. 
4.  a text string expression, which is essentially a character string without 
    beginning and ending apostrophes (').  The text string expression is often 
    the result of the CHARTEXT function.  A text string may have a maximum of 
    272 characters. 
5.  a preprocessor identifier which has been previously defined. 
Rules: 
1.  %EQU provides an error if the value of the %EQU identifier is subsequently 
    changed, or an attempt is made to change an %EQU identifier to a %SET 
    identifier. 
2.  %LSET is valid only within macros.  %LSET provides a temporary value which 
    is valid only within a particular macro invocation.  Previous identifier 
    values are restored, or the identifier becomes undefined at the end of the 
    macro invocation which defined the %LSET identifier.  (Note:  %LSET is 
    particularly useful for temporarily modifying listing modes.)  A limit of 
    256 LSETs can be in effect at one time. 
3.  Preprocessor variables, defined by %EQU, %SET, or %LSET, may be used 
    within preprocessor directives, (e.g. %ERROR, %IF, %ELSEIF, and %SPACE), 
    and macros.  They may also be used as arguments to preprocessor functions, 
    as described in the subsection on "Preprocessor Expression and Function 
    Facilities". Or they may also be invoked directly, as follows: 
          %id 
    When the variable is invoked in this manner, its value is passed to the 
    compiler as a constant. 
4.  The preprocessor expressions used in these facilities are evaluated after 
    all string substitution has taken place. 
5.  Preprocessor-variable identifiers can be specified within macro 
    definitions, and they can also be used during macro invocations. 
    Evaluation of these preprocessor-variable identifiers will take place at 
    macro expansion time. 
6.  Substitutions specified by %SUB directives will not be applied to the 
    identifier which occurs on the left side of the equal sign in a %SET, 
    %EQU, or %LSET directive. 
Example: 
    SISYPHUS: PROC; 
    %SET LISTEXP = '1'B; 
    %SET FOREVER = CHARTEXT ('WHILE (''1''B)'); 
    %SET YES = '1'B; 
    %SET NO = '0'B; 
    DCL TOP_OF_HILL BIT (1) STATIC INIT (%NO); 
    DO %FOREVER; 
    IF TOP_OF_HILL  = %YES THEN 
       TOP_OF_HILL = %NO; 
    ELSE 
    TOP_OF_HILL = %YES; 
    END; 
    END SISYPHUS; 
The preceding source produces the following listing output: 
    SISYPHUS: PROC; 
    %SET LISTEXP = '1'B; 
    %SET FOREVER = WHILE ('1'B); 
    %SET YES = '1'B; 
    %SET NO = '0'B; 
    DCL TOP_OF_HILL BIT (1) STATIC INIT ('0'B); 
    DO WHILE ('1'B); 
    IF TOP_OF_HILL  = '1'B THEN 
       TOP_OF_HILL = '0'B; 
    ELSE 
    TOP_OF_HILL = '1'B; 
    END; 
    END SISYPHUS; 
The next example demonstrates the %EQU  directive. 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU PASSING = 70; 
    DCL NUM_FAILING UBIN STATIC INIT (0); 
    DCL NUM_PASSING UBIN STATIC INIT (0); 
    DCL TEST_SCORE UBIN; 
    IF TEST_SCORE < %PASSING THEN 
       NUM_FAILING = NUM_FAILING + 1; 
    ELSE 
       NUM_PASSING = NUM_PASSING + 1; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU PASSING = 70; 
    DCL NUM_FAILING UBIN STATIC INIT (0); 
    DCL NUM_PASSING UBIN STATIC INIT (0); 
    DCL TEST_SCORE UBIN; 
    IF TEST_SCORE < 70 THEN 
       NUM_FAILING = NUM_FAILING + 1; 
    ELSE 
       NUM_PASSING = NUM_PASSING + 1; 
    END DEMO; 
The next example demonstrates the %LSET directive. 
    OKTOBERFEST: PROC; 
    %SET LISTMAC = '1'B; 
    %SET LISTEXP = '1'B; 
    %MACRO ANOTHER_ROUND (BOTTLES_OF_BEER = 99); 
    %LSET PREVIOUS_ROUND = BOTTLES_OF_BEER - 1; 
    %IF BOTTLES_OF_BEER > 0; 
        %ANOTHER_ROUND (BOTTLES_OF_BEER = PREVIOUS_ROUND); 
    %ENDIF; 
    %MEND; 
    /* Let the fun begin; invoke the macro. */ 
    %ANOTHER_ROUND (BOTTLES_OF_BEER = 3); 
    END OKTOBERFEST; 
The preceding source produces the following listing output: 
    OKTOBERFEST: PROC; 
    %SET LISTMAC = '1'B; 
    %SET LISTEXP = '1'B; 
    %MACRO ANOTHER_ROUND (BOTTLES_OF_BEER = 99); 
    %LSET PREVIOUS_ROUND = BOTTLES_OF_BEER - 1; 
    %IF BOTTLES_OF_BEER > 0; 
        %ANOTHER_ROUND (BOTTLES_OF_BEER = PREVIOUS_ROUND); 
    %ENDIF; 
    %MEND; 
    /* Let the fun begin; invoke the macro. */ 
    %ANOTHER_ROUND (BOTTLES_OF_BEER = 3); 
    %LSET PREVIOUS_ROUND = 2; 
    %IF '1'B; 
        %ANOTHER_ROUND (BOTTLES_OF_BEER = PREVIOUS_ROUND); 
    %LSET PREVIOUS_ROUND = 1; 
    %IF '1'B; 
        %ANOTHER_ROUND (BOTTLES_OF_BEER = PREVIOUS_ROUND); 
    %LSET PREVIOUS_ROUND = 0; 
    %IF '0'B; 
    %ENDIF; 
    %ENDIF; 
    %ENDIF; 
    END OKTOBERFEST; 
Cross Reference: 
See the LISTING directives for more information on using %LSET. 
00004
00003
00001
00002
SET_EQU_LSET
Description: 
The SIZEB built-in function returns the number of bits required for the 
physical storage of a constant or reference, including possible supplementary 
bits implied by alignment requirements. 
Format: 
      {(reference     )} 
      {(stringconstant)} 
SIZEB {(NIL           )} 
      {(ERASE         )} 
Parameters: 
reference    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted reference. 
stringconstant    a bit-string or character-string constant. 
Rules: 
1.  SIZEB returns a UBIN WORD value. 
2.  SIZEB is defined as follows: 
        SIZEB (x) = number of required bits for storage of x. 
    where x is a reference or a string constant. 
    NOTE:  The SIZEB function is evaluated after the required alignment has 
    been performed.  Therefore, the function represents the physical size as 
    opposed to the logical size of the reference. 
3.  By definition 
        SIZEB (NIL) = 0 
    and 
        SIZEB (ERASE) = 1 
4.  If the argument of SIZEB is a reference, then the reference may have any 
    storage class, and any data type except ENTRY. 
5.  If the SIZEB function appears as the INIT value in a declaration of a 
    variable, and the argument is a reference, the argument may not indicate 
    an adjustable bit/character string or a structure containing one.  In 
    addition, a based reference must not be pointer qualified. 
6.  BASED and DCB data can be referenced without pointer-qualification in the 
    SIZEB function.  The only time pointer-qualification is required with 
    SIZEB is when the reference is to an adjustable bit/character string (or a 
    structure containing one) and the adjustable size variable is contained 
    within the referenced structure.  In all other cases, 
    pointer-qualification for BASED or DCB data is not needed for SIZEB. 
Example: 
    DCL A BIT(5); 
    DCL B BIT(5) ALIGNED; 
    DCL 1 C, 
          2 D ALIGNED, 
            3 E BIT(5), 
            3 F BIT(5) ALIGNED, 
            3 G BIT(1), 
          2 H BIT(1) DALIGNED; 
From the above definitions, the results of the SIZEB function would be as 
follows: 
    SIZEB (A)     = 5 
    SIZEB (B)     = 36 
    SIZEB (C)     = 216 
    SIZEB (C.D)   = 108 
    SIZEB (C.D.E) = 5 
    SIZEB (C.D.F) = 36 
    SIZEB (C.D.G) = 1 
    SIZEB (C.H)   = 72 
00003
00001
00002
Description: 
The SIZEC built-in function returns the number of characters required for the 
physical storage of a constant or reference, including possible supplementary 
bits implied by alignment requirements. 
Format: 
      {(reference     )} 
SIZEC {(stringconstant)} 
      {(NIL           )} 
      {(ERASE         )} 
Parameters: 
reference    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted reference. 
stringconstant    a bit-string or character-string constant. 
Rules: 
1.  SIZEC returns a UBIN WORD value. 
2.  SIZEC is defined as follows: 
        SIZEC (x) = integer part of (SIZEB (x) + 8)/9 
    where x is a reference or a string constant. 
    NOTE:  The SIZEC function is evaluated after the required alignment has 
    been performed.  Therefore, the function represents the physical size as 
    opposed to the logical size of the reference. 
3.  By definition 
        SIZEC (NIL) = 0 
    and 
        SIZEC (ERASE) = 1 
4.  If the argument of SIZEC is a reference, then the reference may have any 
    storage class, and any data type except ENTRY. 
5.  If the SIZEC function appears as the INIT value in a declaration of a 
    variable, and the argument is a reference, the argument may not indicate 
    an adjustable bit/character string or a structure containing one.  In 
    addition, a based reference must not be pointer qualified. 
6.  BASED and DCB data can be referenced without pointer-qualification in the 
    SIZEC function.  The only time pointer-qualification is required with 
    SIZEC is when the reference is to an adjustable bit/character string (or a 
    structure containing one), and the adjustable size variable is contained 
    within the referenced structure.  In all other cases, 
    pointer-qualification for BASED or DCB data is not needed for SIZEC. 
Example: 
    DCL A CHAR(1); 
    DCL B CHAR(1) ALIGNED; 
    DCL 1 C DALIGNED, 
          2 D ALIGNED, 
            3 E BIT(1), 
            3 F CHAR(2), 
          2 G CHAR(1); 
From the above definitions, the results of the SIZEC function would be as 
follows: 
    SIZEC (A)     = 1 
    SIZEC (B)     = 4 
    SIZEC (C)     = 8 
    SIZEC (C.D)   = 4 
    SIZEC (C.D.E) = 1 
    SIZEC (C.D.F) = 2 
    SIZEC (C.G)   = 1 
00003
00001
00002
Description: 
The SIZEV built-in function returns the number of characters, less one, 
required for the physical storage of a constant or reference. 
Format: 
      {(reference     )} 
SIZEV {(stringconstant)} 
      {(NIL           )} 
      {(ERASE         )} 
Parameters: 
reference    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted reference. 
stringconstant    a bit-string or character-string constant. 
Rules: 
1.  SIZEV returns a UBIN WORD value. 
2.  SIZEV is defined as follows: 
        SIZEV (x) = integer part of (SIZEB (x) + 8)/9 - 1 
    where x is a reference or a string constant. 
    NOTE:  The SIZEV function is evaluated after the required alignment has 
    been performed.  Therefore, the function represents the physical size as 
    opposed to the logical size of the reference. 
3.  By definition 
        SIZEV (NIL) = 0 
    and 
        SIZEV (ERASE) = 1 
4.  If the argument of SIZEV is a reference, then the reference may have any 
    storage class, and any data type except ENTRY. 
5.  If the SIZEV function appears as the INIT value in the declaration of a 
    variable, and the argument is a reference, the argument may not indicate 
    an adjustable bit/character string or a structure containing one.  In 
    addition, a based reference must not be pointer qualified. 
6.  BASED and DCB data can be referenced without pointer-qualification in the 
    SIZEV function.  The only time pointer-qualification is required with 
    SIZEV is when the reference is to an adjustable bit/character string (or a 
    structure containing one), and the adjustable size variable is contained 
    within the referenced structure.  In all other cases, 
    pointer-qualification for BASED or DCB data is not needed for SIZEV. 
Example: 
    DCL A CHAR(1); 
    DCL B CHAR(1) ALIGNED; 
    DCL 1 C DALIGNED, 
          2 D ALIGNED, 
            3 E BIT(1), 
            3 F CHAR(2), 
          2 G CHAR(1); 
From the above definitions, the results of the SIZEV function would be as 
follows: 
    SIZEV (A)     = 0 
    SIZEV (B)     = 3 
    SIZEV (C)     = 7 
    SIZEV (C.D)   = 3 
    SIZEV (C.D.E) = 0 
    SIZEV (C.D.F) = 1 
    SIZEV (C.G)   = 0 
00003
00001
00002
Description: 
The SIZEW built-in function returns the number of words required for the 
physical storage of a constant or reference, including possible supplementary 
bits implied by alignment requirements. 
Format: 
      {(reference     )} 
SIZEW {(stringconstant)} 
      {(NIL           )} 
      {(ERASE         )} 
Parameters: 
reference    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted reference. 
stringconstant    a bit-string or character-string constant. 
Rules: 
1.  SIZEW returns a UBIN WORD value. 
2.  SIZEW is defined as follows: 
        SIZEW (x) = integer part of (SIZEB (x) + 35)/36 
    where x is a reference or a string constant. 
    NOTE:  The SIZEW function is evaluated after the required alignment has 
    been performed.  Therefore, the function represents the physical size as 
    opposed to the logical size of the reference. 
3.  By definition 
        SIZEW (NIL) = 0 
    and 
        SIZEW (ERASE) = 1 
4.  If the argument of SIZEW is a reference, then the reference may have any 
    storage class, and any data type except ENTRY. 
5.  If the SIZEW function appears as the INIT value in a declaration of a 
    variable, and the argument is a reference, the argument may not indicate 
    an adjustable bit/character string or a structure containing one.  In 
    addition, a based reference must not be pointer qualified. 
6.  BASED and DCB data can be referenced without pointer-qualification in the 
    SIZEW function.  The only time pointer-qualification is required with 
    SIZEW is when the reference is to an adjustable bit/character string (or a 
    structure containing one), and the adjustable size variable is contained 
    within the referenced structure.  In all other cases, 
    pointer-qualification for BASED or DCB data is not needed for SIZEW. 
Example: 
    DCL A CHAR(1); 
    DCL B CHAR(1) DALIGNED; 
    DCL 1 C, 
          2 D DALIGNED, 
            3 E BIT(1), 
            3 F SBIN ALIGNED, 
            3 G BIT(1), 
          2 H CHAR(1); 
From the above definitions, the results of the SIZEW function would be as 
follows: 
    SIZEW (A)     = 1 
    SIZEW (B)     = 2 
    SIZEW (C)     = 6 
    SIZEW (C.D)   = 4 
    SIZEW (C.D.E) = 1 
    SIZEW (C.D.F) = 1 
    SIZEW (C.D.G) = 1 
    SIZEW (C.H)   = 1 
00003
00001
00002
Description: 
%SPACE causes a vertical format character, which corresponds to the number of 
lines to be spaced, to be placed in the source output listing print buffer. 
Consequently, 1 or more blank lines will appear in the source listing output 
following the %SPACE directive. 
Format: 
%SPACE [exp]; 
Parameters: 
exp    is an sbin expression. 
Rules: 
1.  %SPACE with no expression (%SPACE;) causes one blank line to be printed 
    immediately following the space directive. 
2.  %SPACE with an expression (%SPACE n;) causes n blank lines or a 
    top-of-page, whichever comes first, to be printed immediately following 
    the %SPACE n directive. 
Example: 
    NOTHING: PROC; 
    %SPACE; 
    END NOTHING; 
The preceding source produces the following listing output: 
    NOTHING: PROC; 
    %SPACE; 
    END NOTHING; 
    NOTHING: PROC; 
    %SPACE 3; 
    END NOTHING; 
The preceding source produces the following listing output: 
    NOTHING: PROC; 
    %SPACE 3; 
    END NOTHING; 
00003
00001
00002
There are few restrictions in the format of PL-6 statements.  A source record 
can be no longer than 140 characters.  Statements can be continued from one 
source record to the next.  String literals can be continued from one source 
record to the next.  Identifiers and keywords cannot be continued from one 
record to the next. 
A statement can begin in the position or column that immediately follows the 
preceding statement, or it can begin after any number of blanks.  Each source 
statement is terminated with a semicolon. 
Available topics for PL6 statements are: 
ASSIGNMENT      CALL          CASE         DCL 
DO_CASE         DO_INHIBIT    DO_SELECT    DO_SIMPLE 
DO_TO_DOWNTO_BY DO_UNINHIBIT  DO_UNTIL     DO_WHILE 
END             ENTRY         EXIT         GOTO 
ELSE            IF            NULL         PROC 
PROC_AVOID      PROC_MATERIALIZE           REMEMBER 
RETURN_ALTRETURN              SELECT       UNWIND 
For additional HELP topics type: 
HELP (PL6) statement  displays the format and a description of 
                      the specified statement 
HELP (PL6) CALL RULES displays any rules pertaining to CALL. 
HELP (PL6) END FORMAT displays the format of the END statement. 
HELP (PL6) NULL EXAMP displays an example illustrating the NULL statement. 
HELP (PL6) SELECT PA  displays the parameters of the SELECT statement. 
?                     displays the next level of HELP message. 
??                    displays all levels of the current HELP message. 
Description: 
The STATIC attribute assigns a class of storage, to a given data item, that 
specifies that a variable is to be allocated storage statically (before 
program execution). 
Format: 
DCL id a1 [a2] ... STATIC; 
Parameters: 
id    any valid identifier. 
a1,a2    any valid attributes. 
Rules: 
1.  STATIC specifies that storage is to be allocated before the program is 
    executed and is not to be released until program execution has been 
    completed. 
2.  For structures, only the major structure may be given a storage class 
    attribute; the elements automatically receive the same attribute. 
3.  STATIC variables have the same scoping rules as any other variable except 
    when used in conjunction with the SYMDEF or AREADEF attributes.  Use of 
    one of these attributes makes the variable globally visible to any 
    procedure. 
4.  The length or bound of a STATIC variable may be specified only with a 
    decimal integer constant.  (Variables declared to have adjustable string 
    lengths must be BASED or parameters.) 
00001
00002
Description: 
The SUBBIT preprocessor function returns a bit string of length exp3 bits 
starting at bit position exp2 + 1 from the start of exp1. 
Format: 
SUBBIT ( exp1, exp2 [, exp3 ]) 
Parameters: 
exp1    is a bit string expression. 
exp2 and exp3    are sbin expressions. 
Rules: 
1.  If exp3 is not specified, it is assumed to be LENGTHB (exp1) - exp2. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = SUBBIT ('0000011111'B,5,5); 
    DCL HOBBIT BIT (36); 
    HOBBIT = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = '11111'B; 
    DCL HOBBIT BIT (36); 
            HOBBIT = '11111'B; 
    END DEMO; 
00003
00001
00002
BUILT_IN
Description: 
The SUBSTR built-in function allows access to a sub-string of a character 
string. 
Format: 
SUBSTR (string, start [,len]) 
Parameters: 
string    a possibly pointer-qualified, possibly structure-qualified, or 
possibly subscripted character expression. 
start, len    any arithmetic expression. 
Rules: 
1.  start represents the number of the first character of string to be in the 
    resultant string.  The legal values for start are defined as follows: 
        0 <= start < LENGTHC (string) 
2.  len represents the length of the resulting sub-string.  The legal values 
    for len are defined as follows: 
        0 <= len <= LENGTHC (string) 
    such that 
        0 <= start + len <= LENGTHC (string) 
3.  If the length parameter is not specified, then the length is defined to be 
    as follows: 
        len = LENGTHC (string) - start 
4.  In addition to its normal use within an expression, SUBSTR may be used on 
    the left of an assignment statement.  When so used, it inserts the 
    specified part of the specified expression into the specified character 
    location reference.  The two following statements are equivalent: 
        SUBSTR (str,start,len)=exp; 
        CALL INSERT (str,start,len,exp); 
00001
00002
    The SUBSTR preprocessor function returns a portion of a character string 
    for use as a separate character string within the preprocessor. 
Format: 
SUBSTR (string1,start_minus_1[,len]) 
Parameters: 
string1    is a character string expression. 
start_minus_1,len    are sbin expressions. 
Rules: 
1.  Start_minus_1 represents the starting position minus 1 of string1 to be in 
    the resultant string.  In other words, the resultant string begins at the 
    character position start_minus_1 + 1 character from the start of string1. 
    The legal values here are: 
        0 <= start_minus_1 < LENGTHC (string1) 
2.  len represents the number of characters of string1 to be included in the 
    resultant string expression.  The legal values for len are: 
        0 <= len <= LENGTHC (string1) 
    such that 
        0 <= start-1 + len <= LENGTHC (string1) 
    If this is not true then the len parameter is ignored. 
3.  If the len parameter is not specified, it is assumed to be 
        LENGTHC(string1) - start_minus_1 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU DIRT = SUBSTR ('VEGITATIONSOILHUMUSCLAYROCK', 19, 4); 
    DCL SUBSTRATUM CHAR (4); 
    SUBSTRATUM = %DIRT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU DIRT = 'CLAY'; 
    DCL SUBSTRATUM CHAR (4); 
            SUBSTRATUM = 'CLAY'; 
    END DEMO; 
00004
00001
00002
00003
SUB_RESUB_PREPROC
Description: 
%SUB and %RESUB cause each occurrence of a specified identifier, in a PL-6 
source statement or in a preprocessor macro invocation parameter list, to be 
replaced by a specified substitution string. 
Format: 
%SUB id = prepstring; 
%RESUB id = prepstring; 
Parameters: 
id    is any valid preprocessor identifier. 
prepstring    has the following two forms: 
1.  all characters between the = and the ending delimiter (excluding leading 
    and trailing blank characters) which can be a comma ',', semicolon ';', or 
    right parenthesis ')'. 
2.  all characters delimited by quotation marks ("). 
Rules: 
1.  The %SUB directive defines an identifier for which a prepstring will be 
    substituted. 
2.  The %RESUB directive defines an identifier which may be redefined by 
    another %RESUB directive, using the same identifier, e.g.  %RESUB 
    CHAMELEON = 'DR JEKYLL'; %RESUB CHAMELEON = 'MR. HYDE'; 
3.  %SUB definitions are checked against every PL-6 identifier in the 
    procedure.  If a match is found, the identifier is replaced with the 
    defined string. 
4.  The entire identifier must match. 
5.  %SUB string replacement cannot be specified for: 
    o   an identifier which has been defined as the name of a macro, or has 
        been specified on either the default list or the macro reference list. 
    o   an identifier which has been defined as the name of a preprocessor 
        variable, by means of a %SET, %LSET, or %EQU directive. 
    o   an identifier appearing within a comment string. 
    o   an identifier appearing within a string constant. 
    o   an identifier appearing in a %SUB directive. 
6.  When string substitution takes place, the text line is reformatted, and 
    may become several text lines. 
7.  Inserted text is not rescanned for %SUB strings. 
8.  %SUB strings cannot contain partial (i.e., failing to contain both 
    delimiters) comment strings or partial string constants. 
9.  The string portion of the %SUB directive must be contained on a single 
    line. 
10. A preprocessor string specified delimited by the equal sign (=) and the 
    semicolon (;) must not contain the characters , ; or ) and must not start 
    with ". 
    The following example uses the %SUB directive to illustrate a preprocessor 
    string. 
        %SUB TOTAL = PRICE + TAX; 
    where PRICE + TAX is the valid preprocessor string delimited by the equal 
    sign (=) , and the semicolon (;). 
11. A preprocessor string delimited by the quotation mark characters (") may 
    not contain the quotation mark character.  The following example uses the 
    %SUB directive to illustrate the other form of a preprocessor string. 
        %SUB CUMULATIVE_TOTAL = "ITEM_COST (I) * NUM_OF_ITEMS"; 
    where ITEM_COST (I) * NUM_OF_ITEMS is the valid preprocessor string 
    delimited by the quotation mark character ("). 
12. There must be an even number of apostrophes (') in any preprocessor 
    string, in order for the preprocessor to process the string correctly. 
    Double apostrophes ('') must be used when the user wants a single 
    apostrophe to appear in the resultant text, e.g. %SUB LEXICON = 
    'WEBSTER''S DICTIONARY'; will result in 'WEBSTER''S DICTIONARY' being 
    substituted for occurrences of LEXICON in the source text. 
Example: 
    DEMO: PROC; 
    %SET LISTSUB = '1'B; 
    %SUB CUTANEOUS = 'UNDER MY SKIN'; 
    DCL SONG CHAR (50); 
    CALL CONCAT (SONG, 'I''VE GOT YOU ', CUTANEOUS); 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTSUB = '1'B; 
    %SUB CUTANEOUS = 'UNDER MY SKIN'; 
    DCL SONG CHAR (50); 
    CALL CONCAT (SONG, 'I''VE GOT YOU ', 
                       'UNDER MY SKIN'); 
    END DEMO; 
The next example illustrates use of the %RESUB directive. 
    ROBERT_LOUIS_STEVENSON: PROC; 
    %SET LISTSUB = '1'B; 
    DCL LON_CHANEY CHAR (10); /* Oh yes, what a character! */ 
    %RESUB PROTEUS = 'DR JEKYLL'; 
    LON_CHANEY = PROTEUS; 
    %RESUB PROTEUS = 'MR HYDE'; 
    LON_CHANEY = PROTEUS; 
    END ROBERT_LOUIS_STEVENSON; 
The preceding source produces the following listing output: 
    ROBERT_LOUIS_STEVENSON: PROC; 
    %SET LISTSUB = '1'B; 
    DCL LON_CHANEY CHAR (10); 
        /* Oh yes, what a character!          */ 
    %RESUB PROTEUS = 'DR JEKYLL'; 
            LON_CHANEY = 'DR JEKYLL'; 
    %RESUB PROTEUS = 'MR HYDE'; 
            LON_CHANEY = 'MR HYDE'; 
    END ROBERT_LOUIS_STEVENSON; 
00003
00001
00002
Description: 
The storage location of a variable with the SYMDEF attribute may be referenced 
from other PL-6 procedures by declaring, in another PROC, the same variable 
with the storage class attribute SYMREF. 
Format: 
DCL id ... {STATIC  } SYMDEF; 
           {CONSTANT} 
Parameters: 
id    any valid identifier. 
Rules: 
1.  The SYMDEF attribute may appear in the declaration of any scalar, array, 
    or structure with a storage attribute of STATIC or CONSTANT. 
2.  If a given structure is declared with the SYMDEF attribute in one PROC, 
    and with the SYMREF storage class in a second PROC, then the names of the 
    substructures and elements of the structure need not be identical, but the 
    programmer should ensure that the two declarations have identical relative 
    structuring.  For example, if the following declaration appears in PROC P 
    DCL 1 A STATIC SYMDEF, 
          2 B BIT(1), 
          2 C$ PTR; 
    and the following declaration appears in PROC Q 
    DCL 1 A SYMREF, 
          2 D BIT(1), 
          2 E$ PTR; 
    then a reference in P to A.B and a reference in Q to A.D access the same 
    storage location--namely, that belonging to A.B. 
3.  An INIT clause is allowed for STATIC SYMDEF and CONSTANT SYMDEF variables, 
    but is not allowed on the corresponding SYMREF declaration. 
4.  SYMDEF may not be used in conjunction with REDEF. 
Cross Reference: 
See the SYMREF attribute. 
00003
00001
00002
Description: 
The SYMREF attribute specifies that an identifier refers to the same storage 
location as the same identifier declared with the SYMDEF attribute in another 
procedure. 
Format: 
DCL id SYMREF; 
Rules: 
1.  SYMREF is a storage class attribute, and may appear in the declaration of 
    any scalar, array, or structure where no other storage class attribute 
    appears or is implied. 
2.  INIT clause is not allowed on SYMREF variables. 
3.  SYMREF may not be used in conjunction with REDEF. 
4.  A SYMREF can be declared as an adjustable CHAR or BIT string.  Such a 
    declaration in a parameter structure can be given only for the last 
    element in the structure declaration.  The length of the adjustable string 
    is evaluated at each reference to the parameter variable. 
Cross Reference: 
See the SYMDEF Attribute. 
00002
00001
A system file is a file which contains an internal representation of the 
preprocessor state when it encountered the first %EOD or the end of file. 
The system file contains the following: 
1.  All %MACRO definitions 
2.  All %SUB definitions 
3.  The definition of %SET or %EQU variables with their last value 
4.  A list of all %INCLUDE files. 
It does not contain %EJECT, %ERROR, %IF, %LSET, %SPACE, %preprocessor 
expressions, or PL6 statements unless they are contained in the definition of 
a %MACRO. 
Rules: 
1.  A system file is created by specifying the 'CSYS' option in the PL-6 
    invocation line.  PL6 will write a system file using the M$SYSTEM DCB.  If 
    the M$SYSTEM DCB is not assigned by the user, the default system file 
    (PL6SYSTEMFILE.:LIBRARY) will be used.  The new system file will be used 
    in subsequent compile units, if any. 
    When a system file is being created, any include files used should consist 
    only of preprocessor directives. 
2.  If the 'NSYS' option is specified, a system file will not be used even if 
    one is present.  In addition, the 'NSYS' option will prohibit the search 
    of the :LIBRARY account for include files unless specifically specified on 
    the 'SRCH' option. 
3.  If the 'SYS' option (default) is specified, the M$SYSTEM DCB will be 
    opened to read the system file.  If the file is not present, the 
    compilation will proceed normally.  If the file is present, it will be 
    used to define the preprocessor's initial state.  When the preprocessor 
    encounters an include file with the same name as one in the system file, 
    the preprocessor will assume that the include file has already been 
    included in the system file and will ignore the %INCLUDE directive. 
    If the M$SYSTEM DCB is not assigned by the user, the default system file 
    (PL6SYSTEMFILE.:LIBRARY) will be used. 
00001
Description: 
The TEXTCHAR preprocessor function converts a preprocessor identifier into a 
character string expression. 
Format: 
TEXTCHAR (exp) 
Parameters: 
exp    evaluates to a preprocessor identifier. 
Rules: 
1.  The effect of the TEXTCHAR function is to add delimiting apostrophes to 
    the text argument. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU TEXTUS_RECEPTUS = 'GREEK_NEW_TESTAMENT'; 
    %EQU CHARACTERS = TEXTCHAR (TEXTUS_RECEPTUS); 
    DCL GREEK_NEW_TESTAMENT CHAR (20); 
    GREEK_NEW_TESTAMENT = %CHARACTERS; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU TEXTUS_RECEPTUS = 'GREEK_NEW_TESTAMENT'; 
    %EQU CHARACTERS = 'TEXTUS_RECEPTUS'; 
    DCL GREEK_NEW_TESTAMENT CHAR (20); 
            GREEK_NEW_TESTAMENT = 'TEXTUS_RECEPTUS'; 
    END DEMO; 
00003
00001
00002
IF
Description: 
The UBIN attribute declares an identifier as an unsigned (non-negative) 
integer. 
Format: 
            [WORD    ] 
DCL id UBIN [HALF    ] [a] ... ; 
            [BYTE    ] 
            [(length)] 
Parameters: 
id    any valid identifier. 
length    number of bits in the integer. 
a    any other valid attribute. 
HALF    use 18-bit precision. 
WORD    use 36-bit precision. 
BYTE    use 9-bit precision. 
Rules: 
1.  length indicates the amount of storage reserved for the value of id.  The 
    maximum length is 36 bits. 
2.  The length attribute must be a decimal integer constant, with a range of 1 
    to 36. 
3.  The length attribute must immediately follow the UBIN attribute, with or 
    without intervening spaces. 
4.  Default is 36 bits. 
5.  Although a UBIN WORD may contain values up to (2**36)-1, some operations 
    will not be performed correctly on values greater than (2**35)-1.  These 
    operations include:  division, multiplication and MOD.  Use of values 
    greater than (2**35)-1 is not recommended. 
00001
00002
ALIGNMENT
Description: 
The UNWIND statement permits a procedure to restore the dynamic environment to 
a state specified by a given REMEMBER variable, and causes execution to 
continue at the statement specified by the REMEMBER variable (a statement in 
the procedure corresponding to the restored dynamic environment). 
Format: 
[label:] UNWIND TO var; 
Parameters: 
var    a REMEMBER variable which has previously been set up through the use of 
the REMEMBER statement. 
label    any valid label. 
Rules: 
1.  The programmer must ensure that the procedure that initialized the 
    REMEMBER variable is active whenever an UNWIND to that variable is 
    executed. 
2.  When UNWIND is executed in an ASYNC procedure control will be returned to 
    the REMEMBER variable.  Before control is transferred using the UNWIND 
    procedure, the user may want to issue a M$CLRSTK to delete the exceptional 
    conditional frame.  For additional information concerning this, refer to 
    the section on Exceptional Condition processing in the Monitor Services 
    Reference Manual. 
3.  The UNWIND statement can only reference data of type REMEMBER. 
00001
00002
Description: 
The VBASE built-in function allows access to the base address field of the 
referenced vector. 
Format: 
VBASE (vec-ref) 
Parameters: 
vec-ref    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted vector reference. 
Rules: 
1.  VBASE returns a PTR value. 
2.  VBASE may be used as the receiving operand of an assignment statement. 
    When VBASE is used in this manner, the base address field can be altered. 
00001
00002
Description: 
The VBOUND built-in function allows access to the bound field of the 
referenced vector. 
Format: 
VBOUND (vec-ref) 
Parameters: 
vec-ref    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted vector reference. 
Rules: 
1.  VBOUND returns a UBIN(20) value. 
2.  VBOUND may be used as the receiving operand of an assignment statement. 
    When VBOUND is used in this manner, the 20-bit bound field can be altered. 
00001
00002
Description: 
The VECTDSCR built-in function converts vector data to descriptor data. 
Format: 
VECTDSCR (vec-ref) 
Parameters: 
vec-ref    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted vector reference. 
Rules: 
1.  VECTDSCR applies the NSA shrink operation to the vector and returns a DSCR 
    value. 
2.  The vec-ref must explicitly specify the VECTOR attribute or must be an 
    occurrence of the use of the VECTOR built-in function. 
00001
00002
00003
Description: 
The VECTOR built-in function returns a vector describing the storage location 
of the argument. 
Format: 
VECTOR(reference) 
Parameters: 
reference    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted reference, or NIL, or ERASE. 
Rules: 
1.  The value returned by VECTOR is of data type VECTOR. 
2.  The argument of VECTOR must represent a storage location which is aligned 
    on at least a byte boundary and which contains an integral number of 
    bytes. 
3.  If the VECTOR function appears in the INIT attribute of a variable's 
    declaration, then the argument must be of storage class STATIC, CONSTANT, 
    SYMREF, EXT, AREAREF, or EXTROOT. 
4.  The argument of VECTOR may have any storage class, and any data type 
    except ENTRY. 
5.  VECTOR(NIL) returns a vector with a pointer part of ADDR(NIL), and a size 
    part of 0. 
6.  VECTOR(ERASE) returns a vector with a pointer part of ADDR(NIL), and size 
    part of 1. 
7.  The VECTOR function will use the SIZEV value of the reference in building 
    the hardware vector. 
Cross Reference: 
See the discussion of vectors in the GMAP6 manual (DH03). 
00003
00001
00002
Description: 
The VECTOR attribute declares a data item suitable for holding a PL6 vector 
value. 
Format: 
DCL id VECTOR; 
Parameters: 
id    any valid identifier. 
Rules: 
1.  The identifier may be a scalar variable, array name or a structure 
    element.  It is declared as vector-type data. 
2.  VECTOR data items may be assigned only values of the VECTOR type. 
3.  VECTOR variables may be used as explicit qualifiers for BASED data, but 
    not as implicit qualifiers. 
4.  A VECTOR variable can only be INITialized with the VECTOR built-in 
    function. 
5.  No operations other than the assignment or comparison operations may be 
    applied to vector variables.  No implicit conversions may be performed 
    between vector data and numeric, character or pointer data types. 
6.  Vector-qualified items may not be referenced by the ADDR or VECTOR 
    functions (e.g., "P$=ADDR(VEC->FIELD)" is not legal), and may not be 
    passed as parameters to a subroutine. 
Example: 
    DCL NEW_BUFFER_ VECTOR; 
    NEW_BUFFER_ = VECTOR(NIL); 
Cross Reference: 
See VECTOR, VECTDSCR, BITVECT, VBASE, VBOUND, VTYPE and VFLAGS built-in 
functions and the BASED attribute. 
00004
00003
00001
00002
Description: 
The VFLAGS built-in function allows access to the bit-string value of the flag 
field of the referenced vector. 
Format: 
VFLAGS (vec-ref) 
Parameters: 
vec-ref    a possibly pointer-qualified, possibly structure-qualified, 
possibly subscripted VECTOR reference. 
Rules: 
1.  VFLAGS returns a BIT (9) value. 
2.  VFLAGS may be used as the receiving operand of an assignment statement. 
    When VFLAGS is used in this manner, the 9-bit flags field of the vector 
    can be altered by the assignment. 
00001
00002
Description: 
The VTYPE built-in function allows access to the VECTOR type field of the 
referenced vector. 
Format: 
VTYPE (vec-ref) 
Parameters: 
vec-ref    a possibly pointer-qualified/structure-qualified/ or subscripted 
VECTOR reference. 
Rules: 
1.  VTYPE returns a UBIN (2) value. 
2.  VTYPE may be used as the receiving operand of an assignment statement. 
    When VTYPE is used in this manner, the 2-bit type field can be altered. 
00001
00002
ALIGNMENT
Description: 
The WORD attribute is used with SBIN or UBIN to specify that a binary integer 
occupies 36 bits (the default). 
Format: 
DCL id {UBIN} WORD; 
       {SBIN} 
Parameters: 
id    any valid identifier. 
Rules: 
1.  The WORD attribute defines id to be a binary integer with a precision of 
    35 bits plus a sign bit for SBIN; it defines id to be a binary integer 
    with a precision of 36 bits for UBIN. 
Cross Reference: 
See SBIN and UBIN Attributes. 
00003
00001
00002
Description: 
The XCHARBIN built-in subroutine converts a signed digit character string to a 
signed binary number. 
Format: 
CALL XCHARBIN (ref, str); 
Parameters: 
ref    a possibly pointer-qualified, possibly structure-qualified, possibly 
subscripted reference. 
str    any character expression. 
Rules: 
1.  ref must be either SBIN WORD or UBIN WORD and word aligned.  The value of 
    str will be placed in ref as a signed integer. 
2.  str represents the signed digit character string to be converted and must 
    be of data type CHAR.  The SUBSTR (str,0,1) must be either the character 
    '+' or '-'.  If the sign is not present, the results are undefined.  The 
    length of str must be within the range defined as: 
      2 <= LENGTHC (str) <= 63 
    or the results are undefined. 
3.  If non-digit characters are found within str, or if the binary value will 
    not fit in the resultant word, then the results are undefined. 
00001
00002
Description: 
The XCHARBIN preprocessor function converts a signed numeric character string 
to an SBIN value. 
Format: 
XCHARBIN (exp) 
Parameters: 
exp    is a signed or unsigned decimal character string. 
Rules: 
1.  The argument character string must not contain non-numeric characters 
    except for the leading sign character. 
Example: 
    DEMO: PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = XCHARBIN ('-234599'); 
    DCL A SBIN; 
    A = %RESULT; 
    END DEMO; 
The preceding source produces the following listing output: 
    DEMO:   PROC; 
    %SET LISTEXP = '1'B; 
    %EQU RESULT = -234599; 
    DCL A SBIN; 
            A = -234599; 
    END DEMO; 
00003
00001
00002
Description: 
The XLATE subroutine moves and translates a character string using a 512 
character translation table. 
Format: 
CALL XLATE (tostr, table, str) 
        [ALTRET (label)                                 ]; 
        [[WHENRETURN DO group ] [WHENALTRETURN DO group]] 
Parameters: 
tostr    any character location reference. 
str    any character expression. 
table    any reference of type character or bit. 
label    any valid label. 
Rules: 
1.  tostr is the character location reference specifying the destination of 
    the translated string. 
2.  str represents the source string.  Each character of tostr is set from an 
    entry in the table, using the corresponding character from str as an 
    index.  The table entry is accessed as follows: 
        SUBSTR(table, ASCBIN(char),1) 
3.  table must start on a word boundary, and should have a length of 512 
    characters.  Entry 511 will only be accessed if str contains a character 
    with a value of 511.  If the programmer is convinced that every 
    character-code in str is less than 128 (for example), then table may be 
    only 128 characters, and no error or fault will occur. 
4.  The subroutine sets each character of tostr from an entry in the table, 
    using the corresponding character from str as an index.  The subroutine 
    accesses each needed table entry as follows: 
        SUBSTR(table, ASCBIN(char),1) 
5.  If the length of str is less than the length of tostr, str is considered 
    to be padded with ASCII spaces ('040'O or 32 decimal).  Therefore, tostr 
    will be padded with the value defined as: 
        SUBSTR(table,32,1) 
6.  If the length of str is greater than the length of tostr, then truncation 
    occurs on the right and the XLATE operation will ALTRETURN. 
00001
00002
Description: 
The XLATE_6_TO_9 built-in subroutine moves and translates a string of 6 bit 
entities to a string of 9 bit entities, using a 64 character translation 
table. 
Format: 
CALL XLATE_6_TO_9 (tostr, table, str) 
        [ALTRET (label)                                 ]; 
        [[WHENRETURN DO group ] [WHENALTRETURN DO group]] 
Parameters: 
tostr    any character location reference. 
table    any bit or character location reference. 
str    any bit location reference. 
label    any valid label. 
Rules: 
1.  tostr is the character location reference specifying the destination of 
    the translated string. 
2.  str is the bit string location reference specifying the source bit string. 
    The source string is treated as entities 6 bits long aligned on a 6 bit 
    boundary.  From an entry in table using the corresponding 6 bit entity 
    from str as an index the subroutine accesses each needed table entry as 
    follows: 
        SUBSTR (table, BITBIN (6 bit entity), 1) 
3.  table must start on a word boundary and should have a length of 64 
    characters.  Entry 63 will be accessed only if str contains a 6 bit entity 
    with a value of 63.  If the programmer is convinced that every 6 bit code 
    in str is less than 32 (for example), then table may be only 32 
    characters, and no error or fault will occur. 
4.  If the length of str in terms of 6 bit entities is less than the length of 
    tostr, str is considered to be padded with '20'O.  Therefore, tostr will 
    be padded with the value defined as: 
        SUBSTR (table, 16, 1) 
5.  If the length of str in terms of 6 bit entities is greater than the length 
    of tostr, then truncation occurs on the right and the XLATE operation will 
    ALTRETURN. 
00001
00002
Description: 
The XLATE_9_TO_6 built-in function moves and translates a string of 9 bit 
character entities to a string of 6 bit entities, using a 512 character 
translation table. 
Format: 
CALL XLATE_9_TO_6 (tostr, table, str) 
        [ALTRET (label)                                 ]; 
        [[WHENRETURN DO group ] [WHENALTRETURN DO group]] 
Parameters: 
tostr    any bit string location reference. 
table    any character or bit location reference. 
str    any character location reference. 
label    any valid label. 
Rules: 
1.  tostr is the bit-string location reference specifying the destination 
    string. It must be aligned on a 6 bit boundary. 
2.  str is the character location reference specifying the source string. 
3.  table must start on a word boundary and should have a length of 512 
    characters.  Entry 511 will be accessed only if str contains a character 
    with the value 511.  If the programmer is convinced that every 
    character-code in str is less than 128 (for example), then table may be 
    only 128 characters, and no error or fault will occur. 
4.  The subroutine sets each character of tostr, using the 6 low order bits 
    from an entry in table using the corresponding character from str as an 
    index.  The subroutine accesses each needed table entry as follows: 
        SUBSTR (table, ASCBIN (char), 1) 
5.  If the length of str is less than the length of tostr treated as entities 
    6 bits long, str is considered to be padded with ASCII spaces.  Therefore, 
    tostr will be padded with the low order 6 bits of the value defined as: 
        SUBSTR (table, 32, 1) 
6.  If the length of str is greater than the length of tostr treated as 
    entities 6 bits long, then truncation occurs on the right and the XLATE 
    operation will ALTRETURN. 
00001
00002
