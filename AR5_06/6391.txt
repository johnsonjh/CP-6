The COBOL compiler is invoked by using the standard CP-6 processor invocation
line.
Format:
                           [{ON  }                    ]
!COBOL85 [source[, update]] [{OVER} [object][, listout]] [(optionlist)]
                           [{INTO}                    ]
Format Rules:
source    specifies the fid that contains COBOL source code.
update    specifies the fid that contains COBOL source code updates.
ON    specifies that if an object or listout file already exists, the existing
file is not to be overwritten and the command is to be aborted.
OVER    specifies that if an object or listout file already exists, the
existing file is to be overwritten.  If either of these files does not exist,
it is created.
INTO    specifies that if an object or listout file already exists, new output
is to be added to the existing file.  If either of these files does not exist,
it is created.
object    specifies the fid to contain the COBOL object units.  If
unspecified, an object file of *G is automatically assumed.
listout    specifies the fid of the listing output destination.  If a listing
file is not specified, the listing will be returned to the terminal if entered
from time sharing or to the printer if the job is entered as a batch job.
optionlist    specifies one or more of the compiler options in the format
(option[,option]...).
For a list of Standard Compiler Options, enter
HELP (COBOL85) COMP_OPT_STD
For a list of Non-standard Compiler Options, enter
HELP (COBOL85) COMP_OPT_NONSTD
For DCB default conventions
enter HELP (COBOL85) DCB_DEFAULT
For an overview of HELP, see HELP (COBOL85) HELP
  **************************************************************
  *   Copyright, (c) Bull HN Information Systems Inc., 1998
  **************************************************************
Format
CALL ".CDAT4" USING id1
 or
CALL ".CDAY4" USING id2
Syntax Rules
1.  id1 must be exactly 8 ASCII characters in length.
2.  id2 must be exactly 7 ASCII characters in length.
3.  id1/id2 must be USAGE IS DISPLAY.
4.  id1/id2 must be a Level 01 or 77 item.
General Rules
1.  A call to ".CDAT4" is equivalent to ACCEPT FROM DATE except that the
    returned date is formatted as YYYYmmDD instead of YYmmDD.
2.  A call to ".CDAY4" is equivalent to ACCEPT FROM DAY except that the
    returned date is formatted as YYYYddd instead of YYddd.
Examples
Example 1:
     01  The_Date PIC 9(8) USAGE IS BINARY.
     01  temp1    PIC 9(8).
      ...
         CALL ".CDAT4" USING temp1.
         MOVE temp1 TO The_Date.
Example 2:
     01  yyyyddd PIC X(7).
         ...
         CALL ".CDAY4" USING yyyyddd.
00003
00002
00001
.CDAT4
Function
The ACCEPT statement makes available low volume data to the specified data
item.
General Format
Format 1:
                        {mnemonic-name-1}
ACCEPT identifier [FROM {SYSIN          }]
                        {CONSOLE        }
Format 2:
                         {DATE       }
ACCEPT identifier-2 FROM {DAY        }
                         {DAY-OF-WEEK}
                         {TIME       }
Syntax Rule
1.  Mnemonic-name-1 in format 1 must also be specified in the SPECIAL-NAMES
    paragraph of the Environment Division and must be associated with either
    SYSIN or CONSOLE.
Note on Year 2000
For help on obtaining dates with 4-digit years via the routines .CDAT4 and
.CDAY4, type the following:
    HELP (COBOL85) Y2K
00001
ACCESS_MODE_SEQUENTIAL
Function
The ACCESS MODE clause specifies the order in which records are to be accessed
in the file.
General Format
               {SEQUENTIAL}
ACCESS MODE IS {RANDOM    }
               {DYNAMIC   }
Syntax Rule
1.  The ACCESS MODE IS RANDOM clause must not be specified for file-names
    specified in the USING or GIVING phrase of a SORT or MERGE statement.
00001
Function
The ACCESS MODE clause specifies the order in which records are to be accessed
in the file.
General Format
               {SEQUENTIAL} [RECORD KEY IS data-name-1]}
ACCESS MODE IS {          }                            }
               {{RANDOM   } RECORD KEY IS data-name-1  }
               {{DYNAMIC  }                            }
Syntax Rules
1.  Data-name-1 may be qualified.
2.  Data-name-1 must be defined as an alphanumeric data item and must be
    contained in a data record of the associated file or may be a data item
    external to the data records of the associated file.
3.  The ACCESS MODE IS RANDOM clause must not be specified for file-names
    specified in the USING or GIVING phrase of a SORT or MERGE statement.
00001
Function
The ACCESS MODE clause specifies the order in which records are to be accessed
in the file.
General Format
               {SEQUENTIAL [RELATIVE KEY IS data-name-1]}
ACCESS MODE IS {                                        }
               {{RANDOM } RELATIVE KEY IS data-name-1   }
               {{DYNAMIC}                               }
Syntax Rules
1.  Data-name-1 may be qualified.
2.  Data-name-1 must reference an unsigned integer data item whose description
    does not contain the PICTURE symbol 'P'.
3.  Data-name-1 must not be defined in a record description entry associated
    with that file-name.
4.  The ACCESS MODE IS RANDOM clause must not be specified for file-names
    specified in the USING or GIVING phrase of a SORT or MERGE statement.
5.  If a relative file is referenced by a START statement, the RELATIVE KEY
    phrase within the ACCESS MODE clause must be specified for that file.
00001
Function
The ACCESS MODE clause specifies the order in which records are to be accessed
in the file.
General Format
ACCESS MODE IS SEQUENTIAL
General Rules
1.  If the ACCESS MODE clause is not specified, sequential access is assumed.
2.  Records in the file are accessed in the sequence dictated by the file
    organization.  For sequential files this sequence is specified by
    predecessor-successor record relationships established by the execution of
    WRITE statements when the file is created or extended.
3.  If the associated file connector is an external file connector, every file
    control entry in the run unit which is associated with that file connector
    must specify the same access mode.
00001
    ADDRESS OF identifier-1
identifier-1 may name any item of any level except 66 or 88 within the
    program's own WORKING STORAGE, FILE SECTION or LINKAGE SECTION.
Function
The ADD statement causes two or more numeric operands to be summed and the
result to be stored.
General Format
Format 1:
ADD {identifier-1} ... TO {identifier-2 [ROUNDED]} ...
    {literal-1   }
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-ADD]
Format 2:
ADD {identifier-1} ... TO {identifier-2}
    {literal-1   }        {literal-2   }
  GIVING {identifier-3 [ROUNDED]} ...
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-ADD]
Format 3:
ADD {CORRESPONDING} identifier-1 TO identifier-2 [ROUNDED]
    {CORR         }
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-ADD]
Syntax Rules
1.  In formats 1 and 2, each identifier must refer to an elementary numeric
    item, except that in format 2 each identifier following the word GIVING
    must refer to either an elementary numeric item or an elementary numeric
    edited item.  In format 3, each identifier must refer to a group item.
2.  Each literal must be a numeric literal.
3.  The composite of operands must not contain more than 18 digits.
    a.  In format 1 the composite of operands is determined by using all of
        the operands in a given statement.
    b.  In format 2 the composite of operands is determined by using all of
        the operands in a given statement excluding the data items that follow
        the word GIVING.
    c.  In format 3 the composite of operands is determined separately for
        each pair of corresponding data items.
4.  CORR is an abbreviation for CORRESPONDING.
00001
ALTER_STATEMENT
Function
The ALTERNATE RECORD KEY clause specifies an alternate record key access path
to the records in an indexed file.
General Format
ALTERNATE RECORD KEY IS data-name-1 [WITH DUPLICATES]
Syntax Rules
1.  Data-name-1 may be qualified.
2.  Data-name-1 must be defined as a data item of the category alphanumeric
    within a record description entry associated with the file-name to which
    the ALTERNATE RECORD KEY clause is subordinate.
3.  Data-name-1 must not reference a group item that contains a variable
    occurrence data item.
4.  Data-name-1 must not reference an item whose leftmost character position
    corresponds to the leftmost character position of the prime record key or
    of any other alternate record key associated with this file.
5.  If the indexed file contains variable length records, each alternate
    record key must be contained within the first x character positions of the
    record, where x equals the minimum record size specified for the file.
00001
Function
The ALTER statement modifies a predetermined sequence of operations.
General Format
ALTER {procedure-name-1 TO [PROCEED TO] procedure-name-2} ...
Syntax Rules
1.  Procedure-name-1 is the name of a paragraph that contains a single
    sentence consisting of a GO TO statement without the DEPENDING phrase.
2.  Procedure-name-2 is the name of a paragraph or section in the Procedure
    Division.
00001
SELECT_SEQUENTIAL
SELECT_INDEXED
SELECT_KEYED
SELECT_RELATIVE
SELECT_SEQUENTIAL
    The AUTHOR paragraph is used to supply the name of or otherwise identify
    the author of the program.
General Format
[AUTHOR. [literal] [comment-entry] ... ]
Syntax Rules
1.  The literal must be a nonnumeric literal and, if present, must precede the
    comment-entry.
2.  The comment-entry can be one or more sentences, including any combination
    of characters.  The comment-entry or literal has no effect on the
    operation of a COBOL program.
Function
The BLANK WHEN ZERO clause permits the blanking of an item when its value is
zero.
General Format
BLANK WHEN ZERO
Syntax Rules
1.  The BLANK WHEN ZERO clause can be specified only for an elementary item
    whose PICTURE is specified as numeric or numeric edited.
2.  The numeric or numeric edited data description entry to which the BLANK
    WHEN ZERO clause applies must be described, either implicitly or
    explicitly, as USAGE IS DISPLAY.
00001
Function
The BLOCK CONTAINS clause specifies the size of a physical record.
General Format
BLOCK CONTAINS [integer-1 TO] integer-2 {RECORDS   }
                                        {CHARACTERS}
General Rules
1.  This clause is required except when one or more of the following
    conditions exists:
    a.  A physical record contains one and only one complete logical record.
    b.  The hardware device assigned to the file has one and only one physical
        record size.
    c.  The number of records contained in a block is specified in the
        operating environment.
2.  The size of a physical record may be stated in terms of records unless one
    or more of the following situations exists, in which case the RECORDS
    phrase must not be used:
    a.  In mass storage files, where logical records may extend across
        physical records.
    b.  The physical record contains padding (area not contained in a logical
        record).
    c.  Logical records are grouped in such a manner that an inaccurate
        physical record size would be implied.
3.  If the CHARACTERS phrase is specified, the physical record size is
    specified in terms of the number of character positions required to store
    the physical record, regardless of the types of characters used to
    represent the items within the physical record.
4.  If integer-1 is not specified, integer-2 represents the exact size of the
    physical record.  If integer-1 and integer-2 are both specified, they
    refer to the minimum and maximum size of the physical record,
    respectively.
5.  If the associated file connector is an external file connector, all BLOCK
    CONTAINS clauses in the run unit which are associated with that file
    connector must have the same value for integer-1 and integer-2.
00001
PROCEDURE_DIV_BODY
Function
The CALL statement causes control to be transferred from one object program to
another, within the run unit.
General Format
Format 1:
CALL {identifier-1} [USING {[BY REFERENCE] {argument-1} ...} ...]
     {literal-1   } [      {BY CONTENT {argument-1} ...    }    ]
  [ON OVERFLOW imperative-statement-1]
  [END-CALL]
Format 2:
CALL {identifier-1} [USING {BY REFERENCE] {argument-1} ...} ...]
     {literal-1   } [      {BY CONTENT {argument-1} ...   }    ]
  [ON EXCEPTION imperative-statement-1]
  [NOT ON EXCEPTION imperative-statement-2]
  [END-CALL]
Syntax Rules
1.  Literal-1 must be a nonnumeric literal.
2.  Identifier-1 must be defined as an alphanumeric data item such that its
    value can be a program-name.
3.  Argument-1 may be a REMEMBER variable (a paragraph or section name).  If
    this is the case, then the called program must be written in PL-6 or
    assembly language.
4.  Each of the operands in the USING phrase must have been defined as a data
    item in the File Section, Working-Storage Section, or Linkage Section in
    the calling program and each must have a level-number of 01 through 49 or
    77.  Each of the operands in the USING phrase of the Procedure Division
    header must be defined as a data item in the Linkage Section of the called
    program, and each operand must have a level-number of 01 or 77.
5.  Argument-1 may be an ADDRESS OF special register, or a LENGTH OF special
    register.  "BY CONTENT" is assumed for a LENGTH OF special register.
6.  Argument-1 may be an alphanumeric constant or a numeric constant, but, it
    cannot be a figurative constant.  A constant can only be passed with the
    BY CONTENT phrase.
00001
Function
The CANCEL statement ensures that the next time the referenced program is
called it will be in its initial state.
General Format
CANCEL {identifier-1} ...
       {literal-1   }
Syntax Rules
1.  Literal-1 must be a nonnumeric literal.
2.  Identifier-1 must reference an alphanumeric data item.
00001
The following features are new for this release of COBOL-85.
o   USAGE EBCDIC has been added as a new form of data representation.
o   Any identifier that is USAGE BINARY with a picture string with at least
    one fractional digit will be treated as COMP-11 or COMP-12, depending on
    the number of digits in the picture string.
o   New COBOL-specific Compiler Options have been added:  HIGH, INITIAL, LOW,
    N6UPD, OBS, RPW, SEG1, SEG2, and WRN73.
o   The COBOL-specific Compiler Option IBM has now been documented.
CLOSE_SEQUENTIAL
Function
The CLOSE statement terminates the processing of files with optional lock.
General Format
CLOSE {file-name-1 [WITH LOCK]} ...
Syntax Rule
1.  The files referenced in the CLOSE statement need not all have the same
    organization or access.
00001
Function
The CLOSE statement terminate the processing of files with optional lock.
General Format
CLOSE {file-name-1 [WITH LOCK]} ...
Syntax Rule
1.  The files referenced in the CLOSE statement need not all have the same
    organization or access.
00001
Function
The CLOSE statement terminate the processing of files with optional lock.
General Format
CLOSE {file-name-1 [WITH LOCK]} ...
Syntax Rule
1.  The files referenced in the CLOSE statement need not all have the same
    organization or access.
00001
Function
The CLOSE statement terminates the processing of reel/units and files with
optional rewind and/or lock or removal where applicable.
General Format
      {            [{REEL} [FOR REMOVAL]]}
      {            [{UNIT}              ]}
CLOSE {file-name-1 [                    ]}
      {            [WITH {NO REWIND}    ]}
      {            [     {LOCK     }    ]}
Syntax Rule
1.  The files referenced in the CLOSE statement need not all have the same
    organization or access.
00001
Function
The CLOSE statement terminates the processing of reels/units and files with
optional rewind and/or lock or removal, where applicable.
General Format
      {            [{REEL} [FOR REMOVAL]]}
      {            [{UNIT}              ]}
CLOSE {file-name-1 [                    ]}
      {            [WITH {NO REWIND}    ]}
      {            [     {LOCK     }    ]}
Syntax Rule
1.  The files referenced in the CLOSE statement need not all have the same
    organization or access.
00001
PROCESSOR
There can be five divisions in a COBOL program:  the Control Division, the
Identification Division, the Environment Division, the Data Division, and the
Procedure Division.  For more HELP information, see the following topics:
CONTROL_DIVISION, IDENTIFICATION_DIVISION, ENVIRONMENT_DIVISION,
DATA_DIVISION, and PROCEDURE_DIVISION.
CODE_CLAUSE
CODE_SET_CLAUSE
Function
The CODE clause specifies a two-character literal that identifies each print
line as belonging to a specific report.
General Format
CODE literal-1
Syntax Rules
1.  Literal-1 must be a two-character nonnumeric literal.
2.  If the CODE clause is specified for any report in a file, it must be
    specified for all reports in that file.
00001
Function
The CODE-SET clause specifies the character code convention used to represent
data on the external media.
General Format
CODE-SET IS alphabet-name-1
Syntax Rules
1.  If the CODE-SET clause is specified for a file, all data in that file must
    be described as USAGE IS DISPLAY and any signed numeric data must be
    described with the SIGN IS SEPARATE clause.
2.  The alphabet-name clause referenced by the CODE-SET clause must not
    specify the literal phrase.
00001
Function
The COLUMN NUMBER clause identifies a printable item and specifies the
position of the item on a print line.
General Format
COLUMN NUMBER IS integer-1
Syntax Rules
1.  The COLUMN NUMBER clause can be specified only at the elementary level
    within the report group.  The COLUMN NUMBER clause, if present, must
    appear in or be subordinate to an entry that contains a LINE NUMBER
    clause.
2.  Within a given print line, the printable items must be defined in
    ascending column number order such that each printable item defined
    occupies a unique sequence of contiguous character positions.
00001
COMP_4_SIGN_CLAUSE
For information on invoking the compiler,
enter HELP (COBOL85)
For additional compiler information, enter
HELP (COBOL85) COMP_OPT_STD
HELP (COBOL85) COMP_OPT_NONSTD
HELP (COBOL85) DCB_DEFAULT
HELP (COBOL85) SAMPLE_PROGRAM
For a HELP overview, enter HELP (COBOL85) OVERVIEW
Non-standard Compiler options are:
ANSI, CLIST, COBOL74, CONTINUE, DSE, ERRLIM,
FORMAT, HIGH, IBM, IDSLIST, INITIAL, INT, LOW, LSTOU,
N6UPD, OPTZ, PARAM, RPW, RUNTIME_CHECK SBCHK, SEG1,
SEG2, SUB, SV, TP, VIRTUAL, and WRN73.
For specific information, enter:
HELP (COBOL85) COMP_OPT_NONSTD option
For information on all non-standard options, enter: ??.
  Option     Description
  ANSI
             Specifies that non-ANSI COBOL-85 features used in the program are
             to be flagged through the M$LO DCB.
  [N]CLIST
             Specifies that the program is to create a copy listing through
             M$LO.
  COBOL74
             When conflicts between COBOL-85 and COBOL-74 definitions arise,
             use the COBOL-74 meaning.
  CONT[INUE]
             Specifies that when a runtime error occurs, the runtime support
             is to attempt to continue program execution at a point directly
             after where the error occurred.
  DSE
             Specifies that non-DSE COBOL features used in the program are to
             be flagged through the M$LO DCB (DSE is the Honeywell Bull
             standard COBOL).
  ERRLIM=n
             Specifies a limit to the number of error diagnostics reported.
             The default for n is 25.
  FORM[AT]
             Specifies that the source program is free format.
  HIGH
             Specifies that non-high-level ANSI COBOL-85 features are to be
             flagged through the M$L0 DCB.
  IBM
             Specifies that IBM syntax and semantics should be used. This
             includes initializing all elementary data items in the
             WORKING-STORAGE SECTION to ZEROS if they are numeric, NULL if
             they are USAGE POINTER or, otherwise, SPACES.
  IDSLIST
             Specifies the creation of an IDS sub-schema list.
  INITIAL
             Specifies that any elementary data items in the WORKING-STORAGE
             SECTION, that do not have VALUE IS clauses, should be initialized
             to LOW_VALUES.
  INT[ERMEDIATE]
             Specifies that non-intermediate level ANSI COBOL-85 features are
             to be flagged through the M$LO DCB.
  LOW
             Specifies that non-low-level ANSI COBOL-85 features are to be
             flagged through the M$LO DCB.
  [N]LSTOU[(CODE)|(DATA)]
             Specifies that a symbolic object listing (more mnemonic than LO)
             is to be written through the M$LO DCB.
  N6UPD
             Specifies that the IDS/II subschema is not to be updated, so that
             only read access to the subschema is needed.
  OBS
             Specifies that all COBOL-85 language features that are considered
             obsolete are to be flagged through the M$LO DCB.
  OPTZ
             Requests that the compiler optimize for runtime performance.
  PARAM
             Check the number, type, and size of the parameters with those of
             the calling program.
  RPW
             Specifies that all Report Writer features are to be flagged
             through the M$LO DCB.
  RUNTIME[_CHECK] SBCHK
             Check subscript, index, and reference modification references at
             runtime; if out of range, flag an error.
  SEG1
             Specifies that all Segmentation features are to be flagged
             through the M$LO DCB.
  SEG2
             Specifies that all non-level-1 ANSI COBOL-85 Segmentation
             features are to be flagged through the M$LO DCB.
  SUB
             Specifies that the source program being compiled is a subprogram
             rather than a main program.
  SVn
             Report errors of severity "n" or higher where "n" ranges from 1
             to 5 (SV1- Informational, SV2- Warning, SV3- Flagging SV4- Fatal,
             SV5- Terminal).  The default is 2.
  TP
             Specifies that the program being compiled is a TPR.
  VIRTUAL
             Requests that virtual memory be used to compile this program.
  WRN73
             Specifies that the program be checked for data in character
             positions 73-80 of the input record. If any data is found in
             positions 73-80, print one message at the end of the program.
             Check the number, type, and size of the parameters with those of
             the calling program.
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
00002
00014
00016
00017
00018
00019
00020
00020
00021
00022
00023
00024
00024
00024
00024
00024
00025
00026
00027
Standard Compiler options are:
DMAP, LO, LS, OPTUI, OU, PMAP, SCHEMA, SO, SRCH,
UI, UREF, WARN, and XREF.
For specific information, enter:
HELP (COBOL85) COMP_OPT_STD option
For information on all standard options, enter: ??.
  Option     Description
  [{M|N}]DM[AP] [(option[,option]...)]
             Requests a data map listing of the compilation object unit be
             written through the M$LO DCB.  Option may consist of the
             following data types:  AU[TO], BA[SED], ST[ATIC], SY[MREF].  The
             prefix M requests a mini-map that consists of the first level of
             a structure only.
  [N]LO
             Specifies that the symbolic object listing is to be written
             through the M$LO DCB.
  [N]LS
             Specifies that all source lines are to be listed through the M$LO
             DCB.  If LS is not specified, only source lines with errors are
             listed.
  OPTUI
             Specifies that the update source code is optional.
  [N]OU
             Specifies that the object unit is to be generated through the
             M$OU DCB.
  [{M|N}]PM[AP]
             Requests a procedure map indicating the relative locations of
             external entry points, local subroutines, and labels be written
             through the M$LO DCB.  The prefix M requests that the statement
             locations be omitted from the map.
  [{M|N}]SC[HEMA]
             Specifies that debugging schema records are to be written through
             the M$OU DCB.  The prefix M causes schema records to be written
             only for referenced external, or SYMDEFed items.
  [N]SO
             Requests that a new source file with updates merged is to be
             written through the M$SO DCB.
  SR[CH] (.account[,.account]...)
             Specifies one to eight accounts or packsets to be searched, in
             order, for missing COPY/INCLUDE files.  If there is more than one
             such file, the first file encountered is selected.  Note that the
             leading period is required for an account specification.
  [N]UI
             Specifies that update source code is to be read from the M$UI
             DCB.
  [N]UR[EF]
             Requests that a list of unused data references be written through
             the M$LO DCB.
  [N]WA[RN]
             Requests that all warning messages generated by the compiler be
             written through the M$DO DCB.
  [{M|N}]XR[EF]
             Requests a cross reference listing of the compiled object units
             to be written through the M$LO DCB.  This listing contains a
             dictionary of symbol definitions including all occurrences of all
             references to the definition.  The prefix M generates a cross
             reference for used references only.
00001
00002
00003
00001
00006
00007
00013
00001
00002
00003
00005
00006
00007
00008
00010
00011
00012
00013
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
The COMPUTATIONAL clause allows the user to specify a default format for
storing elementary data items in memory if the USAGE clause is omitted from
the data description entry.
General Format
[                                 {DISPLAY        }]
[                                 {COMP-5         }]
[                                 {COMPUTATIONAL-5}]
[              {COMP         }    {COMP-6         }]
[[DEFAULT FOR] {COMPUTATIONAL} IS {COMPUTATIONAL-6}]
[                                 {COMP-7         }]
[                                 {COMPUTATIONAL-7}]
[                                 {COMP-8         }]
[                                 {COMPUTATIONAL-8}]
[[DEFAULT FOR] {NUMERIC__IMIT IS integer-1}]
Syntax Rule
1.  The value of integer-1 may range from 18 to 60.
00001
Function
The COMPUTE statement assigns the value of an arithmetic expression to one or
more data items.
General Format
COMPUTE {identifier-1 [ROUNDED]} ... = arithmetic-expression-1
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-COMPUTE]
Syntax Rule
1.  Identifier-1 must reference either an elementary numeric item or an
    elementary numeric edited item.
00001
Function
The COMP-4 SIGN clause in the Default Section specifies the position of the
sign on each COMP-4 data item without requiring an explicit SIGN clause to be
used.
General Format
[                             {LEADING }]
[COMP-4 OPERATIONAL [SIGN IS] {TRAILING}]
Syntax Rules
1.  This clause applies to COMP-4 entries whose PICTURE contains an 'S'.
2.  This clause is not applicable to COMP-4 entries that have a SIGN clause
    associated with them.
00001
COMPILER_OPTIONS_NONSTANDARD
COMPILER_OPTIONS_STANDARD
    The Configuration Section is located in the Environment Division of a
    source program.  The Configuration Section deals with the characteristics
    of the source computer and the object computer.  This section also
    provides a means for specifying the currency sign, choosing the decimal
    point, specifying symbolic characters, relating specific-names to
    user-specified mnemonic-names, relating alphabet-names to character sets
    or collating sequences, and relating class-names to sets of characters.
    The Configuration Section is optional in the Environment Division of a
    COBOL source program.
General Format
CONFIGURATION SECTION.
[SOURCE-COMPUTER. [source-computer-entry]]
[OBJECT-COMPUTER. [object-computer-entry]]
[SPECIAL-NAMES. [special-names-entry]]
The Configuration Section must not be stated in a program which is contained
directly or indirectly within another program.
The entries explicitly or implicitly stated in the Configuration Section of a
program which contains other programs apply to each contained program.
Function
The CONTINUE statement is a no-operation statement.  It indicates that no
executable statement is present.
General Format
CONTINUE
Syntax Rule
1.  The CONTINUE statement may be used anywhere a conditional statement or an
    imperative-statement may be used.
00001
Function
The CONTROL clause establishes the levels of the control hierarchy for the
report.
General Format
{CONTROL IS  } {{data-name-1} ...      }
{CONTROLS ARE} {FINAL [data-name-1] ...}
Syntax Rules
1.  Data-name-1 must not be defined in the Report Section.  Data-name-1 may be
    qualified.
2.  Each recurrence of data-name-1 must identify a different data item.
3.  Data-name-1 must not have subordinate to it a variable occurrence data
    item.
00001
The Control Division is optional and consists of the Substitution Section and
the Default Section.  When it is included in the source program, the Control
Division must be the first division in the program, preceding the first
Identification Division.
The Control Division allows the specification of certain defaults other than
the standard compiler defaults.  The general format of the sections and
clauses in the Control Division and their order of presentation in the source
program is given below.
General Format
[CONTROL DIVISION.
[SUBSTITUTION SECTION. [replace statements] ... .]
[DEFAULT SECTION. [default clauses] ... .]]
The Substitution Section is provided for COBOL-74 compatibility only.  If
present, the Substitution Section must appear immediately following the
CONTROL DIVISION header.  REPLACE statements allow COBOL text to be replaced
within a source program.  REPLACE statements are not limited to the
Substitution Section.  The Default Section is optional and is included only if
the standard compiler defaults require changing.  See the following related
topics: DISPLAY_SIGN, COMP_4_SIGN, COMPUTATIONAL, GENERATE_DESCRIPTOR,
SOURCE_TEXT_MANIPULATION, and REPLACE.
Function
The COPY statement incorporates text into a COBOL source program.
General Format
COPY text-name-1 [{OF} library-name-1]
                 [{IN}               ]
  [          {{==pseudo-text-1==}    {==pseudo-text-2==}}    ]
  [REPLACING {{identifier-1     } BY {identifier-2     }} ...]
  [          {{literal-1        }    {literal-2        }}    ]
  [          {{word-1           }    {word-2           }}    ]
Syntax Rules
1.  If more than one COBOL library is available during compilation,
    text-name-1 must be qualified by library-name-1 identifying the COBOL
    library in which the text associated with text-name-1 resides.
    Within one COBOL library, each text-name must be unique.
2.  The COPY statement must be preceded by a space and terminated by the
    separator period.
3.  Pseudo-text-1 must contain one or more text words.
4.  Pseudo-text-2 must contain zero, one, or more text words.
5.  Character-strings within pseudo-text-1 and pseudo-text-2 may be continued.
6.  Word-1 or word-2 may be any single COBOL word except 'COPY' or 'BY'.
7.  A COPY statement may be specified in the source program anywhere a
    character-string or a separator, other than the closing quotation mark,
    may occur except that a COPY statement must not occur within a COPY
    statement.
8.  A length from 1 through 322 characters is allowed for a text word within
    pseudo-text and within library text.
9.  Pseudo-text-1 must not consist entirely of a separator comma or a
    separator semicolon.
10. If the word COPY appears in a comment-entry or in the place where a
    comment-entry may appear, it is considered part of the comment-entry.
00001
Function
A data description entry specifies the characteristics of a particular item of
data.
General Format
Format 1:
level-number [data-name-1]
             [FILLER     ]
  [REDEFINES data-name-2]
  [{PICTURE} IS character-string]
  [{PIC    }                    ]
  [           {BINARY          }]
  [           {COMPUTATIONAL   }]
  [           {COMP            }]
  [           {COMPUTATIONAL-1 }]
  [           {COMP-1          }]
  [           {COMPUTATIONAL-2 }]
  [           {COMP-2          }]
  [           {COMPUTATIONAL-3 }]
  [           {COMP-3          }]
  [           {COMPUTATIONAL-4 }]
  [           {COMP-4          }]
  [           {COMPUTATIONAL-5 }]
  [[USAGE IS] {COMP-5          }]
  [           {COMPUTATIONAL-6 }]
  [           {COMP-6          }]
  [           {COMPUTATIONAL-7 }]
  [           {COMP-7          }]
  [           {COMPUTATIONAL-8 }]
  [           {COMP-8          }]
  [           {COMPUTATIONAL-11}]
  [           {COMP-11         }]
  [           {COMPUTATIONAL-12}]
  [           {COMP-12         }]
  [           {DISPLAY         }]
  [           {EBCDIC          }]
  [           {INDEX           }]
  [           {PACKED-DECIMAL  }]
  [[SIGN IS] {LEADING } [SEPARATE CHARACTER]]
  [          {TRAILING}                     ]
  [OCCURS integer-2 TIMES                                       ]
  [                                                             ]
  [   [{ASCENDING } KEY IS {data-name-3} ... ] ...              ]
  [   [{DESCENDING}                          ]                  ]
  [                                                             ]
  [    [INDEXED BY {index-name-1} ... ]                         ]
  [                                                             ]
  [OCCURS integer-1 TO integer-2 TIMES DEPENDING ON data-name-4 ]
  [                                                             ]
  [   [{ASCENDING } KEY IS {data-name-3} ... ] ...              ]
  [   [{DESCENDING}                          ]                  ]
  [                                                             ]
  [    [INDEXED BY {index-name-1} ... ]                         ]
  [{SYNCHRONIZED} [LEFT ]]
  [{SYNC        } [RIGHT]]
  [{JUSTIFIED} RIGHT]
  [{JUST     }      ]
  [BLANK WHEN ZERO]
  [VALUE IS literal-1].
Format 2:
66 data-name-1 RENAMES data-name-2 [{THROUGH} data-name-3].
                                   [{THRU   }            ]
Format 3:
88 condition-name-1 {VALUE IS  } {literal-1 [{THROUGH} literal-2]} ... .
                    {VALUES ARE} {          [{THRU   }          ]}
Syntax Rules
1.  Level-number in format 1 may be any number from 01 through 49 or 77.
2.  In format 1, the data-name-1 or FILLER clause, if specified, must
    immediately follow the level-number.  The REDEFINES clause, if specified,
    must immediately follow the data-name-1 or FILLER clause if either is
    specified; otherwise, it must immediately follow the level-number.  The
    remaining clauses may be written in any order.
3.  The PICTURE clause must be specified for every elementary item except an
    index data item and the subject of the RENAMES clause, in which case use
    of this clause is prohibited.
4.  The words THRU and THROUGH are equivalent.
00001
Function
Within the Inter-Program Communication module, a level 01 data description
entry within the Working-Storage Section or File Section determines whether
the data record and its subordinate data items have local names or global
names.
Within the Inter-Program Communication module, a level 01 data description
entry in the Working-Storage Section determines the internal or external
attributes of the data record and its subordinate data items.
General Format
01 [data-name-1]
   [FILLER     ]
   [REDEFINES data-name-2]
   [IS EXTERNAL]
   [IS GLOBAL]
   [{PICTURE} IS character-string]
   [{PIC    }                    ]
   [           {BINARY        }]
   [           {COMPUTATIONAL }]
   [[USAGE IS] {COMP          }]
   [           {DISPLAY       }]
   [           {EBCDIC        }]
   [           {INDEX         }]
   [           {PACKED-DECIMAL}]
   [           {POINTER       }]
   [SIGN IS] {LEADING } [SEPARATE CHARACTERS]]
   [         {TRAILING}                      ]
   [OCCURS integer-2 TIMES                                      ]
   [                                                            ]
   [    [{ASCENDING } KEY IS {data-name-3} ...] ...             ]
   [    [{DESCENDING}                         ]                 ]
   [                                                            ]
   [     [INDEXED BY {index-name-1} ...]                        ]
   [                                                            ]
   [OCCURS integer-1 TO integer-2 TIMES DEPENDING ON data-name-4]
   [                                                            ]
   [    [{ASCENDING } KEY IS {data-name-3} ... ] ...            ]
   [    [{DESCENDING}                          ]                ]
   [                                                            ]
   [     [INDEXED BY {index-name-1} ...]                        ]
   [{SYNCHRONIZED} [LEFT ]]
   [{SYNC        } [RIGHT]]
   [{JUSTIFIED} RIGHT]
   [{JUST     }      ]
   [BLANK WHEN ZERO]
   [VALUE IS literal-1].
Syntax Rules
1.  The EXTERNAL clause may be specified only in data description entries in
    the Working-Storage Section whose level-number is 01.
2.  The EXTERNAL clause and the REDEFINES clause must not be specified in the
    same data description entry.
3.  The GLOBAL clause may be specified only in data description entries whose
    level-number is 01.
4.  Data-name-1 must be specified for any entry containing the GLOBAL or
    EXTERNAL clause, or for record descriptions associated with a file
    description entry which contains the EXTERNAL or GLOBAL clause.
00001
The Data Division describes the data that the object program is to accept as
input, to manipulate, to create, or to produce as output.
The Data Division is subdivided into sections: the File, Working-Storage,
Linkage, Report and Sub-Schema Sections.
The File Section defines the structure of data files. Each file is defined by
a file description entry and one or more record description entries, or by a
file description entry and one or more report description entries.  Record
description entries are written immediately following the file description
entry.  When the file description entry specifies a file to be used as a
report writer output file, no record description entries are permitted for
that file.  Report description entries appear in a separate section of the
Data Division, the Report Section.
The Working-Storage Section describes records and subordinate data items which
are not part of external data files but are developed and processed
internally.  It also describes data items whose values are assigned in the
source program and do not change during the execution of the object program.
The Linkage Section appears in the called program and describes data items
that are to be referred to by the calling program and the called program.  Its
structure is the same as the Working-Storage Section.
The Report Section describes the content and format of reports that are to be
generated.
The Sub-Schema section describes the schema and subschema for the I-D-S/II
interface.
General Format
DATA DIVISION.
[FILE SECTION.
[file-description-entry [record-description-entry] ...      ] ...]
[sort-merge-description-entry {record-description-entry} ...] ...]
[WORKING-STORAGE SECTION.
[77-level-description-entry] ...]
[record-description-entry  ] ...]
[LINKAGE SECTION.
[77-level-description-entry] ... ]
[record-description-entry  ] ... ]
[REPORT SECTION.
[report-description-entry {report-group-description-entry} ...] ...]
[SUB-SCHEMA SECTION.
[sub-schema-description-entry]]
00001
FILLER_CLAUSE
Function
A data-name specifies the name of the data item being described.
General Format
data-name-1
Syntax Rule
1.  In the Report Section, data-name-1 need not appear in a data description
    entry.
00001
Function
The DATA RECORDS clause serves only as documentation for the names of data
records within their associated file.
General Format
DATA {RECORD IS  } {data-name-1} ...
     {RECORDS ARE}
Syntax Rule
1.  Data-name-1 is the name of a data record and must have an 01 level-number
    record description, with the same name, associated with it.
00001
    The DATE-COMPILED paragraph provides the compilation date in the
    Identification Division source program listing.
General Format
DATE-COMPILED. [comment-entry]
Syntax Rule
1.  The comment-entry may be any combination of the characters from the
    computer's character set.  The continuation of the comment-entry by using
    a hyphen in the indicator area is not permitted; however, the
    comment-entry may be contained on one or more lines.
    The DATE-WRITTEN paragraph is used to supply the date on which the program
    was written.
General Format
[DATE-WRITTEN. [comment-entry]]
Syntax Rule
1.  The comment-entry can be one or more sentences, including any combination
    of characters.  The comment-entry has no effect on the operation of a
    COBOL program.
The CP-6 operating system makes the following default associations between
Data Control Blocks (DCBs) and fids of the compiler-invoking command.
  fid       Default DCB    I/O File Identified
1.        M$SI           Base source code; this is the input DCB
                         through which source code is read.
2.        M$UI           Source code updates.
3.        M$OU           Object unit(s).
4.        M$LO           Listing output; this is the output DCB through
                         which listings are written.
Declarative sections must be grouped at the beginning of the Procedure
Division preceded by the key word DECLARATIVES and followed by the key words
END DECLARATIVES.
DELETE_RELATIVE
Function
The DELETE statement logically removes a record from a mass storage file.
General Format
DELETE file-name-1 RECORD
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-DELETE]
Syntax Rules
1.  The INVALID KEY and the NOT INVALID KEY phrases must not be specified for
    a DELETE statement which references a file which is in sequential access
    mode.
2.  The INVALID KEY phrase must be specified for a DELETE statement which
    references a file which is not in sequential access mode and for which an
    applicable USE AFTER STANDARD EXCEPTION procedure is not specified.
00001
Function
The DELETE statement logically removes a record from a mass storage file.
General Format
DELETE file-name-1 RECORD
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-DELETE]
Syntax Rules
1.  The INVALID KEY and the NOT INVALID KEY phrases must not be specified for
    a DELETE statement which references a file in sequential access mode.
2.  The INVALID KEY phrase must be specified for a DELETE statement which
    references a file not in sequential access mode and for which an
    applicable USE AFTER STANDARD EXCEPTION procedure is not specified.
00001
Function
The DELETE statement logically removes a record from a mass storage file.
General Format
DELETE file-name-1 RECORD
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-DELETE]
Syntax Rules
1.  The INVALID KEY and the NOT INVALID KEY phrases must not be specified for
    a DELETE statement which references a file in sequential access mode.
2.  The INVALID KEY phrase must be specified for a DELETE statement which
    references a file not in sequential access mode and for which an
    applicable USE AFTER STANDARD EXCEPTION procedure is not specified.
00001
DISPLAY_STATEMENT
Function
The DISPLAY SIGN clause in the Default Section specifies the representation
and position of the sign on each DISPLAY data item without requiring an
explicit SIGN clause to be used.
General Format
[                            {LEADING }                     ]
[DISPLAY OPERATIONAL SIGN IS {TRAILING} [SEPARATE CHARACTER]] .
Syntax Rules
1.  The DISPLAY SIGN clause applies only to numeric data description entries
    whose PICTURE contains an 'S' and whose usage is DISPLAY, explicitly or
    implicitly.
2.  The DISPLAY SIGN clause is not applicable to a numeric data description
    entry that has an implicit (at the group entry) or explicit SIGN clause
    associated with it.
00001
Function
The DISPLAY statement causes low volume data to be transferred to an
appropriate hardware device.
General Format
                           [     {mnemonic-name-1}]
DISPLAY {identifier-1} ... [UPON {SYSOUT         }] [WITH NO ADVANCING]
                           [     {CONSOLE        }]
        {literal-1   }
Syntax Rules
1.  Mnemonic-name-1 is associated with SYSOUT or CONSOLE in the SPECIAL-NAMES
    paragraph in the Environment Division.
2.  If literal-1 is numeric,  it must be an unsigned integer.
00001
Function
The DIVIDE statement divides one numeric data item into others and sets the
values of data items equal to the quotient and remainder.
General Format
Format 1:
DIVIDE {identifier-1} INTO {identifier-2 [ROUNDED]} ...
       {literal-1   }
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-DIVIDE]
Format 2:
DIVIDE {identifier-1} INTO {identifier-2}
       {literal-1   }      {literal-2   }
  GIVING {identifier-3 [ROUNDED]} ...
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-DIVIDE]
Format 3:
DIVIDE {identifier-1} BY {identifier-2}
       {literal-1   }    {literal-2   }
  GIVING {identifier-3 [ROUNDED]} ...
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-DIVIDE]
Format 4:
DIVIDE {identifier-1} INTO {identifier-2} GIVING identifier-3 [ROUNDED]
       {literal-1   }      {literal-2   }
  REMAINDER identifier-4
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-DIVIDE]
Format 5:
DIVIDE {identifier-1} BY {identifier-2} GIVING identifier-3 [ROUNDED]
       {literal-1   }    {literal-2   }
  REMAINDER identifier-4
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-DIVIDE]
Syntax Rules
1.  Each identifier must refer to an elementary numeric item, except that any
    identifier associated with the GIVING or REMAINDER phrase must refer to
    either an elementary numeric item or an elementary numeric edited item.
2.  Each literal must be a numeric literal.
3.  The composite of operands, which is the hypothetical data item resulting
    from the superimposition of all receiving data items (except the REMAINDER
    data item) of a given statement aligned on their decimal points, must not
    contain more than 18 digits.
00001
COBOL_DIVISIONS
Function
The end program header indicates the end of the named COBOL source program.
General Format
END PROGRAM program-name.
Syntax Rules
1.  The program-name must conform to the rules for forming a user-defined
    word.
2.  The program-name must be identical to a program-name declared in a
    preceding PROGRAM-ID paragraph.
General Rules
1.  The end program header indicates the end of the specified COBOL source
    program.
2.  If the next source statement after the program terminated by the end
    program header is a COBOL statement, it must be the Identification
    Division header of a program to be compiled separately from that program
    terminated by the end program header.
00002
00001
Function
The end program header indicates the end of the named COBOL source program.
General Format
END PROGRAM program-name.
Syntax Rules
1.  The program-name must conform to the rules for forming a user-defined
    word.
2.  The program-name must be identical to a program-name declared in a
    preceding PROGRAM-ID paragraph.
3.  If a PROGRAM-ID paragraph declaring a specific program-name is stated
    between the PROGRAM-ID paragraph and the end program header declaring and
    referencing, respectively, another program-name, the end program header
    referencing the former program-name must precede that referencing the
    latter program-name.
00001
The Environment Division specifies a standard method of expressing those
aspects of a data processing problem that are dependent upon the physical
characteristics of a specific computer.  This division allows specification of
the configuration of the compiling computer and the object computer.  In
addition, information relative to input-output control, special hardware
characteristics, and control techniques can be given.
Two sections make up the Environment Division:  the Configuration Section and
the Input-Output Section.
The Configuration Section deals with the characteristics of the source
computer and the object computer.  This section is divided into three
paragraphs:  the SOURCE-COMPUTER paragraph, which describes the computer
configuration on which the source program is compiled; the OBJECT-COMPUTER
paragraph, which describes the computer configuration on which the object
program produced by the compiler is to be run; and the SPECIAL-NAMES
paragraph, which provides a means for specifying the currency sign, choosing
the decimal point, specifying symbolic characters, relating system-names to
user-specified mnemonic-names, relating alphabet-names to character sets or
collating sequences, and relating class-names to sets of characters.
The Input-Output Section deals with the information needed to control
transmission and handling of data between external media and the object
program.  This section is divided into two paragraphs:  the FILE-CONTROL
paragraph which names and associates the files with external media; and the
I-O-CONTROL paragraph which defines special control techniques to be used in
the object program.
General Format
ENVIRONMENT DIVISION.
[CONFIGURATION SECTION.
[SOURCE-COMPUTER. [source-computer-entry]]
[OBJECT-COMPUTER. [object-computer-entry]]
[SPECIAL-NAMES. [special-names-entry]]]
[INPUT-OUTPUT SECTION.
 FILE-CONTROL. {file-control-entry} ...
[I-O-CONTROL. [input-output-control-entry]]]
00001
Function
The EVALUATE statement describes a multi-branch, multi-join structure.  It can
cause multiple conditions to be evaluated.  The subsequent action of the
object program depends on the results of these evaluations.
General Format
         {identifier-1} [     {identifier-2}]
         {literal-1   } [     {literal-2   }]
EVALUATE {expression-1} [ALSO {expression-2}] ...
         {TRUE        } [     {TRUE        }]
         {FALSE       } [     {FALSE       }]
  {{WHEN
    {ANY                                                                    }
    {condition-1                                                            }
    {TRUE                                                                   }
    {FALSE                                                                  }
    {      {{identifier-3           } [{THROUGH} {identifier-4           }]}}
    {[NOT] {{literal-3              } [{THRU   } {literal-4              }]}}
    {      {{arithmetic-expression-1} [          {arithmetic-expression-2}]}}
  [ALSO
    {ANY
    {condition-2
    {TRUE
    {FALSE
    {      {{identifier-5           }
    {[NOT] {{literal-5              }
    {      {{arithmetic-expression-3}
                                             }]     }
                                             }]     }
                                             }]     }
                                             }]     }
       [{THROUGH} {identifier-6           }]}}] ... } ...
       [{THRU   } {literal-6              }]}}]     }
       [          {arithmetic-expression-4}]}}]     }
  imperative-statement-1} ...
  [WHEN OTHER imperative-statement-2]
  [END-EVALUATE]
Syntax Rules
1.  The operands or the words TRUE and FALSE which appear before the first
    WHEN phrase of the EVALUATE statement are referred to individually as
    selection subjects and collectively, for all those specified, as the set
    of selection subjects.
2.  The operands or the words TRUE, FALSE, and ANY which appear in a WHEN
    phrase of an EVALUATE statement are referred to individually as selection
    objects and collectively, for all those specified in a single WHEN phrase,
    as the set of selection objects.
3.  The words THROUGH and THRU are equivalent.
4.  Two operands connected by a THROUGH phrase must be of the same class.  The
    two operands thus connected constitute a single selection object.
5.  The number of selection objects within each set of selection objects must
    be equal to the number of selection subjects.
6.  Each selection object within a set of selection objects must correspond to
    the selection subject having the same ordinal position within the set of
    selection subjects according to the following rules:
    a.  Identifiers, literals, or arithmetic expressions appearing within a
        selection object must be valid operands for comparison to the
        corresponding operand in the set of selection subjects.
    b.  Condition-1, condition-2, or the words TRUE or FALSE appearing as a
        selection object must correspond to a conditional expression or the
        words TRUE or FALSE in the set of selection subjects.
    c.  The word ANY may correspond to a selection subject of any type.
00001
Function
The EXAMINE statement is used to count and/or replace occurrences of a given
character in a data item.
General Format 1
                             { UNTIL FIRST }
 EXAMINE identifier TALLYING { ALL } literal-1
                             { LEADING     }
       [ REPLACING BY literal-2]
General Format 2
                              { ALL           }
 EXAMINE identifier REPLACING { LEADING } literal-3
                              { UNTIL FIRST   }
       BY literal-4
Syntax Rules
1.  The identifier must be described, explicitly or implicitly, with USAGE
     DISPLAY.
2.  Each literal must consist of a single character belonging to a class
    consistent with that of 'identifier'. In addition, each literal may be any
    figurative constant except ALL.
3.  If the identifier is numeric, each literal must be an unsigned integer or
    the figurative constant ZERO, (ZEROES, ZEROS).
00001
SAMPLE_PROGRAM
Execution begins with the first statement of the Procedure Division, excluding
declaratives.  Statements are then executed in the order in which they are
presented for compilation, except where the rules indicate some other order.
EXIT_STATEMENT
Function
The EXIT PROGRAM statement marks the logical end of a called program.
General Format
EXIT PROGRAM
Syntax Rules
1.  If an EXIT PROGRAM statement appears in a consecutive sequence of
    imperative statements within a sentence, it must appear as the last
    statement in that sequence.
2.  The EXIT PROGRAM statement must not appear in a declarative procedure in
    which the GLOBAL phrase is specified.
00001
Function
The EXIT statement provides a common endpoint for a series of procedures.
General Format
EXIT.
Syntax Rule
1.  The EXIT statement must appear only in a sentence by itself and
    constitutes the only sentence in the paragraph.
00001
Function
The EXTERNAL clause specifies that a data item or a file connector is
external.  The constituent data item and group data items of an external data
record are available to every program in the run unit which describes that
record.
General Format
IS EXTERNAL
Syntax Rules
1.  The EXTERNAL clause may be specified only in file description entries or
    in record description entries in the Working-Storage Section.
2.  In the same program, the data-name specified as the subject of the entry
    whose level-number is 01 that includes the EXTERNAL clause must not be the
    same data-name specified for any other data description entry which
    includes the EXTERNAL clause.
3.  The VALUE clause must not be used in any data description entry which
    includes, or is subordinate to, an entry which includes the EXTERNAL
    clause.  The VALUE clause may be specified for condition-name entries
    associated with such data description entries.
00001
FD_SEQUENTIAL
Function
The file description entry furnishes information concerning the physical
structure, identification, and record-names pertaining to an indexed file.
General Format
FD file-name-1
  [BLOCK CONTAINS [integer-1 TO] integer-2 {RECORDS   }]
  [                                        {CHARACTERS}]
  [       {CONTAINS integer-3 CHARACTERS                                  }]
  [       {                                                               }]
  [       {IS VARYING IN SIZE [[FROM integer-4] [TO integer-5] CHARACTERS]}]
  [RECORD {                                                               }]
  [       {  [DEPENDING ON data-name-1]                                   }]
  [       {                                                               }]
  [       {CONTAINS integer-6 TO integer-7 CHARACTERS                     }]
  [LABEL {RECORD IS  } {STANDARD}]
  [      {RECORDS ARE} {OMITTED }]
  [         {FILE-ID  }    {data-name-2}    ]
  [VALUE OF {RETENTION} IS {literal-1  } ...]
  [         {FILE-NAME}                     ]
  [DATA {RECORD IS  } {data-name-3} ...] .
  [     {RECORDS ARE}                  ]
Syntax Rules
1.  The level indicator FD identifies the beginning of a file description
    entry and must precede file-name-1.
2.  The clauses which follow file-name-1 may appear in any order.
3.  One or more record description entries must follow the file description
    entry.
00001
Function
Within the Inter-Program Communication module, the file description entry in
the File Section determines the internal or external attributes of a file
connector, the associated data records, and the associated data items.  The
file description entry also determines whether a file-name is a local name or
a global name.
General Format
Format 1:
FD file-name-1
  [IS EXTERNAL]
  [IS GLOBAL]
  [BLOCK CONTAINS [integer-1 TO] integer-2 {RECORDS   }]                  }]
  [                                        {CHARACTERS}]                  }]
  [       {CONTAINS integer-3 CHARACTERS                                  }]
  [       {                                                               }]
  [       {IS VARYING IN SIZE [[FROM integer-4] [TO integer-5] CHARACTERS]}]
  [RECORD {                                                               }]
  [       {  [DEPENDING ON data-name-1]                                   }]
  [       {                                                               }]
  [       {CONTAINS integer-6 TO integer-7 CHARACTERS                     }]
  [LABEL {RECORD IS  } {STANDARD}]
  [      {RECORDS ARE} {OMITTED }]
  [VALUE OF {FILE-ID IS {data-name-2}} ...]
  [         {           {literal-1  }}    ]
  [DATA {RECORD IS  } {data-name-3} ...]
  [     {RECORDS ARE}                  ]
  [LINAGE IS {data-name-4} LINES [WITH FOOTING AT {data-name-5}]
  [          {integer-8  }       [                {integer-9  }]
    [LINES AT TOP {data-name-6}] [LINES AT BOTTOM {data-name-7}]]
    [             {integer-10 }] [                {integer-11 }]]
  [CODE-SET IS alphabet-name-1].
Format 2:
FD file-name-1
  [IS EXTERNAL]
  [IS GLOBAL]
  [BLOCK CONTAINS [integer-1 TO] integer-2 {RECORDS   }]
  [                                        {CHARACTERS}]
  [       {CONTAINS integer-3 CHARACTERS                                  }]
  [       {                                                               }]
  [       {IS VARYING IN SIZE [[FROM integer-4] [TO integer-5] CHARACTERS]}]
  [RECORD {                                                               }]
  [       {  [DEPENDING ON data-name-1]                                   }]
  [       {                                                               }]
  [       {CONTAINS integer-6 TO integer-7 CHARACTERS                     }]
  [LABEL {RECORD IS  } {STANDARD}]
  [      {RECORDS ARE} {OMITTED }]
  [VALUE OF {FILE-ID IS {data-name-2}} ...]
  [         {           {literal-1  }}    ]
  [DATA {RECORD IS  } {data-name-3} ...] .
  [     {RECORDS ARE}                  ]
Format 3:
FD file-name-1
  [IS EXTERNAL]
  [IS GLOBAL]
  [BLOCK CONTAINS [integer-1 TO] integer-2 {RECORDS   }]
  [                                        {CHARACTERS}]
  [       {CONTAINS integer-3 CHARACTERS                                  }]
  [       {                                                               }]
  [       {IS VARYING IN SIZE [[FROM integer-4] [TO integer-5] CHARACTERS]}]
  [RECORD {                                                               }]
  [       {  [DEPENDING ON data-name-1]                                   }]
  [       {                                                               }]
  [       [CONTAINS integer-6 TO integer-7 CHARACTERS                     }]
  [LABEL {RECORD IS  } {STANDARD}]
  [      {RECORDS ARE} {OMITTED }]
  [VALUE OF {FILE-ID IS {data-name-2}} ...]
  [         {           {literal-1  }}    ]
  [CODE-SET IS alphabet-name-1]
  {REPORT IS  } {report-name-1} ... .
  {REPORTS ARE}
 Syntax Rules
1.  Format 1 is the file description entry for a sequential file.
2.  Format 2 is the file description entry for a relative file or an indexed
    file or a keyed file.
3.  Format 3 is the file description entry for a report file.
00001
Function
The file description entry furnishes information concerning the physical
structure, identification, and record-names pertaining to a keyed file.
General Format
FD file-name-1
  [BLOCK CONTAINS [integer-1 TO] integer-2 {RECORDS   }]
  [                                        {CHARACTERS}]
  [       {CONTAINS integer-3 CHARACTERS                                  }]
  [       {                                                               }]
  [       {IS VARYING IN SIZE [[FROM integer-4] [TO integer-5] CHARACTERS]}]
  [RECORD {                                                               }]
  [       {  [DEPENDING ON  data-name-1]                                  }]
  [       {                                                               }]
  [       {CONTAINS integer-6 TO integer-7 CHARACTERS                     }]
  [LABEL {RECORD IS  } {STANDARD}]
  [      {RECORDS ARE} {OMITTED }]
  [         {FILE-ID  }    {data-name-2}    ]
  [VALUE OF {RETENTION} IS {literal-1  } ...]
  [         {FILE-NAME}                     ]
  [DATA {RECORD IS  } {data-name-3} ...] .
  [     {RECORDS ARE}                  ]
Syntax Rules
1.  The level indicator FD identifies the beginning of a file description
    entry and must precede file-name-1.
2.  The clause which follows file-name-1 may appear in any order.
3.  One or more record description entries must follow the file description
    entry.
00001
Function
The file description entry furnishes information concerning the physical
structure, identification, and record-names pertaining to a relative file.
General Format
FD file-name-1
  [BLOCK CONTAINS [integer-1 TO] integer-2 {RECORDS   }]
  [                                        {CHARACTERS}]
  [       {CONTAINS integer-3 CHARACTERS                                  }]
  [       {                                                               }]
  [       {IS VARYING IN SIZE [[FROM integer-4] [TO integer-5] CHARACTERS]}]
  [RECORD {                                                               }]
  [       {  [DEPENDING ON  data-name-1]                                  }]
  [       {                                                               }]
  [       {CONTAINS integer-6 TO integer-7 CHARACTERS                     }]
  [LABEL {RECORD IS  } {STANDARD}]
  [      {RECORDS ARE} {OMITTED }]
  [         {FILE-ID  }    {data-name-2}    ]
  [VALUE OF {RETENTION} IS {literal-1  } ...]
  [         {FILE-NAME}                     ]
  [DATA {RECORD IS  } {data-name-3} ...] .
  [     {RECORDS ARE}                  ]
Syntax Rules
1.  The level indicator FD identifies the beginning of a file description
    entry and must precede file-name-1.
2.  The clause which follows file-name-1 may appear in any order.
3.  One or more record description entries must follow the file description
    entry.
00001
Function
The file description entry furnishes information concerning the physical
structure, identification, and report-names pertaining to a report file.
General Format
FD file-name-1
  [BLOCK CONTAINS [integer-1 TO] integer-2 {RECORDS   }]
  [                                        {CHARACTERS}]
  [       {CONTAINS integer-3 CHARACTERS              }]
  [       {                                           }]
  [RECORD {    [DEPENDING ON data-name-1]             }]
  [       {                                           }]
  [       {CONTAINS integer-6 TO integer-7 CHARACTERS }]
  [LABEL {RECORD IS  } {STANDARD}]
  [      {RECORDS ARE} {OMITTED }]
  [         {FILE-ID  }    {data-name-2}    ]
  [VALUE OF {RETENTION} IS {literal-1  } ...]
  [         {FILE-NAME}                     ]
  [CODE-SET IS alphabet-name-1]
  {REPORT IS  } {report-name-1} ... .
  {REPORTS ARE}
Syntax Rules
1.  The level indicator FD indicates the beginning of the file description
    entry for a report file and must precede the file-name of the report file.
2.  The clauses which follow file-name-1 may appear in any order.
3.  File-name-1 may reference only a sequential file.
4.  No record description entries may follow the file description entry for a
    report file.
5.  The subject of a file description entry that specifies a REPORT clause may
    be referenced in the Procedure Division only by the USE statement, the
    CLOSE statement, or the OPEN statement with the OUTPUT or EXTEND phrase.
00001
Function
The file description entry furnishes information concerning the physical
structure, identification, and record-names pertaining to a sequential file.
General Format
FD file-name-1
  [BLOCK CONTAINS [integer-1 TO] integer-2 {RECORDS   }]
  [                                        {CHARACTERS}]
  [       {CONTAINS integer-3 CHARACTERS                                 ]}]
  [       {                                                               }]
  [       {IS VARYING IN SIZE [[FROM integer-4] [TO integer-5] CHARACTERS]}]
  [RECORD {                                                               }]
  [       {     [DEPENDING ON data-name-1]                                }]
  [       {                                                               }]
  [       {CONTAINS integer-6 TO integer-7 CHARACTERS                     }]
  [LABEL {RECORD IS  } {STANDARD}]
  [      {RECORDS ARE} {OMITTED }]
  [         {FILE-ID  }    {data-name-2}    ]
  [VALUE OF {RETENTION} IS {literal-1  } ...]
  [         {FILE-NAME}                     ]
  [DATA {RECORD IS  } {data-name-3} ...]
  [     {RECORDS ARE}                  ]
  [LINAGE IS {data-name-4} LINES [WITH FOOTING AT {data-name-5}]
  [          {integer-8  }       [                {integer-9  }]
    [LINES AT TOP {data-name-6}] [LINES AT BOTTOM {data-name-7}]]
    [             {integer-10 }] [                {integer-11 }]]
  [CODE-SET IS alphabet-name-1].
Syntax Rules
1.  The level indicator FD identifies the beginning of a file description
    entry and must precede file-name-1.
2.  The clauses which follow file-name-1 may appear in any order.
3.  One or more record description entries must follow the file description
    entry.
00001
Function
The FILE-CONTROL paragraph allows specification of file-related information.
General Format
FILE-CONTROL. {file-control-entry} ...
FD_SEQUENTIAL
FD_INDEXED
FD_KEYED
FD_RELATIVE
    The File Section is located in the Data Division of a source program.  The
    File Section defines the structure of data files.  Each file is defined by
    a file description entry and one or more record description entries.
    Record description entries are written immediately following the file
    description entry.
General Format
FILE SECTION.
[file-description-entry
{record-description-entry} ... ] ...
    The File Section is located in the Data Division of a source program.  The
    File Section defines the structure of report files.  Each report file is
    defined by a file description entry having a REPORT clause.  A file
    description entry for a report file is not followed by record description
    entries.
General Format
FILE SECTION.
[file-description-entry] ...
In a COBOL program, the file description entry (FD entry) represents the
highest level of organization in the File Section.  The File Section header is
followed by a file description entry consisting of a level indicator (FD), a
file-name, and a series of independent clauses.  For a report file, the file
description entry must contain the REPORT clause specifying the names of the
reports to be written onto the report file.  No record description entries may
follow the file description entry for a report file.
        The File Section is located in the Data Division of a source program.
        The File Section defines the structure of sort files and merge files.
        Each sort file or merge file is defined by a sort-merge file
        description entry and one or more record description entries.  Record
        description entries are written immediately following the sort-merge
        file description entry.
General Format
FILE SECTION.
[sort-merge-file-description-entry
{record-description-entry} ...] ...
00001
Function
The FILE STATUS clause specifies a data item which contains the status of an
input-output operation.
General Format
FILE STATUS IS data-name-1
Syntax Rules
1.  Data-name-1 may be qualified.
2.  Data-name-1 must be defined in the Data Division as a two-character data
    item of the category alphanumeric and must not be defined in the File
    Section or the Report Section.
00001
Function
A data-name specifies the name of the data item being described.  The keyword
FILLER may be used to specify a data item which is not referenced explicitly.
General Format
[data-name-1]
[FILLER     ]
Syntax Rule
1.  In the File, Working-Storage, and Linkage Sections, data-name-1 or the
    keyword FILLER, if either is specified, must be the first word following
    the level-number in each data description entry.
00001
GENERATE_STATEMENT
The GENERATE DESCRIPTOR clause allows the user to specify if descriptors are
needed, and, if so, what type, for arguments in the using list for CALL
statements.
This feature is needed when a more detailed description of the argument list
is required by the called procedures.  These called procedures are generally
GMAP procedures that interface with, or support, the COBOL procedure (caller).
General Format
[         {NO       }            ]
[GENERATE {AGGREGATE} DESCRIPTORS]
[         {SCALAR   }            ]
Syntax Rule
1.  The GENERATE DESCRIPTOR clause applies to the generation of descriptors
    for each argument specified on a CALL statement.
General Rules:
1.  The GENERATE NO DESCRIPTORS clause results in the production of no
    descriptors for the argument list within the object code.
2.  If the GENERATE AGGREGATE DESCRIPTORS clause is specified, descriptors are
    generated for each argument, according to the rules described in the
    User's Guide.
3.  If no GENERATE DESCRIPTOR clause was specified or the GENERATE SCALAR
    DESCRIPTORS clause is specified, descriptors are generated for each
    argument.  However, if an argument is a group item, then that argument is
    treated as a character string type descriptor.
00002
00001
Function
The GENERATE statement directs the report writer control system (RWCS) to
produce a report in accordance with the report description specified in the
Report Section of the Data Division.
General Format
GENERATE {data-name-1  }
         {report-name-1}
Syntax Rules
1.  Data-name-1 must name a TYPE DETAIL report group and may be qualified by a
    report-name.
2.  Report-name-1 may be used only if the referenced report description
    contains:
    a.  A CONTROL clause, and
    b.  Not more than one DETAIL report group, and
    c.  At least one body group.
00001
Function
The GLOBAL clause specifies that a data-name, a file-name, or a report-name is
a global name.  A global name is available to every program contained within
the program which declares it.
General Format
IS GLOBAL
Syntax Rules
1.  The GLOBAL clause may be specified only in data description entries whose
    level-number is 01 in the File Section or the Working-Storage Section,
    file description entries, or report description entries.
2.  In the same Data Division, the data description entries for any two data
    items for which the same data-name is specified must not include the
    GLOBAL clause.
3.  If the SAME RECORD AREA clause is specified for several files, the record
    description entries or the file description entries for these files must
    not include the GLOBAL clause.
00001
GO_TO_STATEMENT
Function
The GO TO statement causes control to be transferred from one part of the
Procedure Division to another.
General Format
Format 1:
GO TO [procedure-name-1]
Format 2:
GO TO {procedure-name-1} ... DEPENDING ON identifier-1
Syntax Rules
1.  Identifier-1 must reference a numeric elementary data item which is an
    integer.
2.  When a paragraph is referenced by an ALTER statement, that paragraph can
    consist only of a paragraph header followed by a format 1 GO TO statement.
3.  A format 1 GO TO statement, without procedure-name-1, can only appear in a
    single statement paragraph.
4.  If a GO TO statement represented by format 1 appears in a consecutive
    sequence of imperative statements within a sentence, it must appear as the
    last statement in that sequence.
00001
Function
The GROUP INDICATE clause specifies that the associated printable item is
presented only on the first occurrence of its report group after a control
break or page advance.
General Format
GROUP INDICATE
Syntax Rule
1.  The GROUP INDICATE clause must be specified only in a DETAIL report group
    entry that defines a printable item.
00001
PROCEDURE_DIV_HEADER
HELP_OVERVIEW
A
  ACCEPT Statement -
      HELP ACCEPT_STATEMENT
  ACCESS MODE -
      HELP SELECT_SEQUENTIAL GENERAL_FORMAT
  ACCESS MODE Clause -
      HELP ACCESS_MODE_SEQUENTIAL
      HELP ACCESS_MODE_RELATIVE
      HELP ACCESS_MODE_INDEXED
      HELP ACCESS_MODE_KEYED
  ADD Statement -
      HELP ADD_STATEMENT
  ADVANCING -
      HELP DISPLAY_STATEMENT GENERAL_FORMAT
  AFTER -
      HELP INSPECT_STATEMENT GENERAL_FORMAT
      HELP PERFORM_STATEMENT GENERAL_FORMAT
      HELP USE_SEQUENTIAL GENERAL_FORMAT
  AFTER ADVANCING -
      HELP WRITE_SEQUENTIAL GENERAL_FORMAT
  AGGREGATE -
      HELP GENERATE_DESCRIPTOR_CLAUSE GENERAL_FORMAT
  ALL -
      HELP INSPECT_STATEMENT GENERAL_FORMAT
      HELP SEARCH_STATEMENT GENERAL_FORMAT
  ALPHABETIC -
      HELP INITIALIZE_STATEMENT GENERAL_FORMAT
  ALPHANUMERIC -
      HELP INITIALIZE_STATEMENT GENERAL_FORMAT
  ALSO -
      HELP EVALUATE_STATEMENT GENERAL_FORMAT
  ALTER Statement -
      HELP ALTER_STATEMENT
  ALTERNATE RECORD KEY Clause -
      HELP ALTERNATE_RECORD_KEY_CLAUSE
  ANY -
      HELP EVALUATE_STATEMENT GENERAL_FORMAT
  AREA -
      HELP SELECT_SEQUENTIAL GENERAL_FORMAT
  ASCENDING -
      HELP MERGE_STATEMENT GENERAL_FORMAT
      HELP SORT_STATEMENT GENERAL_FORMAT
  ASCENDING KEY IS -
      HELP OCCURS_CLAUSE GENERAL_FORMAT
  ASCII -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  ASSIGN, Indexed Files -
      HELP SELECT_INDEXED GENERAL_FORMAT
  ASSIGN, Keyed Files -
      HELP SELECT_KEYED GENERAL_FORMAT
  ASSIGN, Relative Files -
      HELP SELECT_RELATIVE GENERAL_FORMAT
  ASSIGN, Sequential Files -
      HELP SELECT_SEQUENTIAL FUNCTION
  AT END -
      HELP SEARCH_STATEMENT GENERAL_FORMAT
      HELP READ_SEQUENTIAL GENERAL_FORMAT
      HELP READ_RELATIVE GENERAL_FORMAT
      HELP READ_KEYED GENERAL_FORMAT
  AUTHOR Paragraph -
      HELP AUTHOR_PARAGRAPH
B
  BEFORE -
      HELP INSPECT_STATEMENT GENERAL_FORMAT
      HELP PERFORM_STATEMENT GENERAL_FORMAT
  BEFORE ADVANCING -
      HELP WRITE_SEQUENTIAL GENERAL_FORMAT
  BINARY -
      HELP USAGE_CLAUSE GENERAL_FORMAT
  BLANK WHEN ZERO Clause -
      HELP BLANK_WHEN_ZERO_CLAUSE
  BLOCK CONTAINS Clause -
      HELP BLOCK_CONTAINS_CLAUSE
  BOTTOM -
      HELP LINAGE_CLAUSE GENERAL_FORMAT
  BY -
      HELP INITIALIZE_STATEMENT GENERAL_FORMAT
      HELP INSPECT_STATEMENT GENERAL_FORMAT
      HELP MULTIPLY_STATEMENT GENERAL_FORMAT
C
  CALL Statement -
      HELP CALL_STATEMENT
  CANCEL Statement -
      HELP CANCEL_STATEMENT
  .CDAT4 and .CDAY4 Year 2000 Subroutines -
      HELP .CDAT4
  CF -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  CH -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  Changes for A05 -
      HELP CHANGES
  CHARACTER -
      HELP SIGN_CLAUSE GENERAL_FORMAT
  CHARACTERS -
      HELP OBJECT_COMPUTER_PARAGRAPH GENERAL_RULES
      HELP INSPECT_STATEMENT GENERAL_FORMAT
  CLASS -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  CLOSE Statement -
      HELP CLOSE_SEQUENTIAL
      HELP CLOSE_RELATIVE
      HELP CLOSE_INDEXED
      HELP CLOSE_KEYED
      HELP CLOSE_REPORT_WRITER
  COBOL Divisions -
      HELP COBOL_DIVISIONS
  COBOL Source Program -
      HELP SOURCE_PROGRAM
  CODE Clause -
      HELP CODE_CLAUSE
  CODE-SET Clause -
      HELP CODE_SET_CLAUSE
  COLLATING SEQUENCE -
      HELP MERGE_STATEMENT GENERAL_FORMAT
      HELP SORT_STATEMENT GENERAL_FORMAT
  COLUMN NUMBER Clause -
      HELP COLUMN_NUMBER_CLAUSE
  COMMA -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  COMMON -
      HELP PROGRAM_ID_INTER_PROGRAM GENERAL_FORMAT
  Communication, Inter-Program -
      HELP INTER_PROGRAM_COMMUNICATION
  COMP-4 SIGN Clause -
      HELP COMP_4_SIGN_CLAUSE
  COMPUTATIONAL -
      HELP USAGE_CLAUSE GENERAL_FORMAT
  COMPUTATIONAL Clause -
      HELP COMPUTATIONAL_CLAUSE
  COMPUTE Statement -
      HELP COMPUTE_STATEMENT
  Condition-Name conventions -
      HELP SCOPE_OF_NAMES
  Configuration Section -
      HELP CONFIGURATION_SECTION
  CONSOLE -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
      HELP ACCEPT_STATEMENT GENERAL_FORMAT
      HELP DISPLAY_STATEMENT GENERAL_FORMAT
  CONTENT -
      HELP CALL_STATEMENT GENERAL_FORMAT
  CONTINUE Statement -
      HELP CONTINUE_STATEMENT
  CONTROL Clause -
      HELP CONTROL_CLAUSE
  Control Division -
      HELP CONTROL_DIVISION
  CONTROL FOOTING -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  CONTROL HEADING -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  CONVERTING -
      HELP INSPECT_STATEMENT GENERAL_FORMAT
  COPY Statement -
      HELP COPY_STATEMENT
  CORRESPONDING -
      HELP SUBTRACT_STATEMENT GENERAL_FORMAT
  COUNT IN -
      HELP UNSTRING_STATEMENT GENERAL_FORMAT
  CURRENCY SIGN -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
D
  Data Description Entry -
      HELP DATA_DESCRIPTION_ENTRY
  Data Description Entry, Inter-Program Communication -
      HELP DATA_DESCRIPTION_INTER_PROGRAM
  Data Division -
      HELP DATA_DIVISION
  DATA RECORDS Clause -
      HELP DATA_RECORDS_CLAUSE
  Data-Name Clause -
      HELP DATA_NAME_REPORT_WRITER
  DATA-NAME or FILLER Clause -
      HELP FILLER_CLAUSE
  DATE -
      HELP ACCEPT_STATEMENT GENERAL_FORMAT
  DATE-COMPILED Paragraph -
      HELP DATE_COMPILED_PARAGRAPH
  DATE-WRITTEN Paragraph -
      HELP DATE_WRITTEN_PARAGRAPH
  DAY -
      HELP ACCEPT_STATEMENT GENERAL_FORMAT
  DAY-OF-WEEK -
      HELP ACCEPT_STATEMENT GENERAL_FORMAT
  DCB Default Conventions -
      HELP DCB_DEFAULT
  DEBUGGING MODE -
      HELP SOURCE_COMPUTER_PARAGRAPH GENERAL_RULES
  DECIMAL-POINT IS COMMA -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  Declaratives -
      HELP DECLARATIVES
  DEFAULT -
      HELP COMPUTATIONAL_CLAUSE GENERAL_FORMAT
  DELETE Statement -
      HELP DELETE_RELATIVE
      HELP DELETE_INDEXED
      HELP DELETE_KEYED
  DELIMITED BY -
      HELP STRING_STATEMENT GENERAL_FORMAT
      HELP UNSTRING_STATEMENT GENERAL_FORMAT
  DELIMITER -
      HELP SELECT_SEQUENTIAL GENERAL_FORMAT
  DELIMITER IN -
      HELP UNSTRING_STATEMENT GENERAL_FORMAT
  DEPENDING ON -
      HELP OCCURS_CLAUSE GENERAL_FORMAT
      HELP GO_TO_STATEMENT GENERAL_FORMAT
      HELP RECORD_CLAUSE GENERAL_FORMAT
  DESCENDING -
      HELP MERGE_STATEMENT GENERAL_FORMAT
      HELP SORT_STATEMENT GENERAL_FORMAT
  DESCENDING KEY IS -
      HELP OCCURS_CLAUSE GENERAL_FORMAT
  DESCRIPTORS -
      HELP GENERATE_DESCRIPTOR_CLAUSE GENERAL_FORMAT
  DETAIL -
      HELP PAGE_CLAUSE GENERAL_FORMAT
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  DISPLAY -
      HELP USAGE_CLAUSE GENERAL_FORMAT
      HELP USAGE_CLAUSE_REPORT_WRITER GENERAL_FORMAT
  DISPLAY SIGN Clause -
      HELP DISPLAY_SIGN_CLAUSE
  DISPLAY Statement -
      HELP DISPLAY_STATEMENT
  DIVIDE Statement -
      HELP DIVIDE_STATEMENT
  DOWN BY -
      HELP SET_STATEMENT GENERAL_FORMAT
  DUPLICATES -
      HELP ALTERNATE_RECORD_KEY_CLAUSE GENERAL_FORMAT
      HELP SORT_STATEMENT GENERAL_FORMAT
  DYNAMIC -
      HELP ACCESS_MODE_RELATIVE GENERAL_FORMAT
      HELP ACCESS_MODE_INDEXED GENERAL_FORMAT
      HELP ACCESS_MODE_KEYED GENERAL_FORMAT
E
  EBCDIC -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  EDITED -
      HELP INITIALIZE_STATEMENT GENERAL_FORMAT
  ELSE -
      HELP IF_STATEMENT GENERAL_FORMAT
  End Program Header -
      HELP END_PROGRAM_HEADER
      HELP END_PROGRAM_HEADER_INTER_PROG
  END-OF-PAGE -
      HELP WRITE_SEQUENTIAL GENERAL_FORMAT
  ENTRY -
      HELP PROCEDURE_DIV_INTER_PROGRAM
  Environment Division -
      HELP ENVIRONMENT_DIVISION
  EOP -
      HELP WRITE_SEQUENTIAL GENERAL_FORMAT
  EQUAL -
      HELP START_RELATIVE GENERAL_FORMAT
      HELP START_KEYED GENERAL_FORMAT
  EQUAL TO -
      HELP SEARCH_STATEMENT GENERAL_FORMAT
  ERROR -
      HELP USE_SEQUENTIAL GENERAL_FORMAT
      HELP USE_RELATIVE GENERAL_FORMAT
      HELP USE_INDEXED GENERAL_FORMAT
      HELP USE_KEYED GENERAL_FORMAT
      HELP USE_INTER_PROGRAM GENERAL_FORMAT
  EVALUATE Statement -
      HELP EVALUATE_STATEMENT
  EXAMINE Statement -
      HELP EXAMINE_STATEMENT
  EXCEPTION -
      HELP USE_SEQUENTIAL GENERAL_FORMAT
      HELP USE_RELATIVE GENERAL_FORMAT
      HELP USE_INDEXED GENERAL_FORMAT
      HELP USE_KEYED GENERAL_FORMAT
      HELP USE_INTER_PROGRAM GENERAL_FORMAT
  Execution -
      HELP EXECUTION
  EXIT PROGRAM Statement -
      HELP EXIT_PROGRAM_STATEMENT
  EXIT Statement -
      HELP EXIT_STATEMENT
  EXTEND -
      HELP OPEN_SEQUENTIAL GENERAL_FORMAT
      HELP OPEN_RELATIVE GENERAL_FORMAT
      HELP OPEN_INDEXED GENERAL_FORMAT
      HELP USE_INDEXED GENERAL_FORMAT
      HELP OPEN_KEYED GENERAL_FORMAT
      HELP USE_KEYED GENERAL_FORMAT
      HELP USE_INTER_PROGRAM GENERAL_FORMAT
  EXTERNAL Clause -
      HELP EXTERNAL_CLAUSE
F
  FALSE -
      HELP EVALUATE_STATEMENT GENERAL_FORMAT
  FD, Indexed Files -
      HELP FD_INDEXED GENERAL_FORMAT
  FD, Inter-Program Communication -
      HELP FD_INTER_PROGRAM GENERAL_FORMAT
  FD, Keyed Files -
      HELP FD_KEYED GENERAL_FORMAT
  FD, Relative Files -
      HELP FD_RELATIVE FUNCTION
  FD, Report Writer -
      HELP FD_REPORT_WRITER GENERAL_FORMAT
  FD, Sequential Files -
      HELP FD_SEQUENTIAL FUNCTION
  File Control Entry -
      HELP SELECT_SEQUENTIAL
      HELP SELECT_RELATIVE
      HELP SELECT_INDEXED
      HELP SELECT_KEYED
      HELP SELECT_SORT_MERGE
      HELP SELECT_REPORT_WRITER
  File Description Entry -
      HELP FD_SEQUENTIAL
      HELP FD_RELATIVE
      HELP FD_INDEXED
      HELP FD_KEYED
      HELP FD_REPORT_WRITER
  File Description Entry, Inter-Program Communication -
      HELP FD_INTER_PROGRAM
  File Section -
      HELP FILE_SECTION
      HELP FILE_SECTION_SORT_MERGE
      HELP FILE_SECTION_REPORT_WRITER
  FILE STATUS -
      HELP SELECT_SEQUENTIAL GENERAL_FORMAT
  FILE STATUS Clause -
      HELP FILE_STATUS_CLAUSE
  FILE-CONTROL Paragraph -
      HELP FILE_CONTROL_PARAGRAPH
  FILLER Clause -
      HELP FILLER_CLAUSE FUNCTION
  FINAL -
      HELP CONTROL_CLAUSE GENERAL_FORMAT
      HELP SUM_CLAUSE GENERAL_FORMAT
  FIRST -
      HELP INSPECT_STATEMENT GENERAL_FORMAT
  FIRST DETAIL -
      HELP PAGE_CLAUSE GENERAL_FORMAT
  FOOTING -
      HELP LINAGE_CLAUSE GENERAL_FORMAT
      HELP PAGE_CLAUSE GENERAL_FORMAT
  FOR -
      HELP INSPECT_STATEMENT GENERAL_FORMAT
  FROM -
      HELP ACCEPT_STATEMENT GENERAL_FORMAT
G
  GENERATE DESCRIPTOR Clause -
      HELP GENERATE_DESCRIPTOR_CLAUSE
  GENERATE Statement -
      HELP GENERATE_STATEMENT
  GIVING -
      HELP DIVIDE_STATEMENT GENERAL_FORMAT
      HELP MULTIPLY_STATEMENT GENERAL_FORMAT
  GLOBAL Clause -
      HELP GLOBAL_CLAUSE
  GO TO Statement -
      HELP GO_TO_STATEMENT
  GREATER -
      HELP START_RELATIVE GENERAL_FORMAT
      HELP START_KEYED GENERAL_FORMAT
  GROUP INDICATE Clause -
      HELP GROUP_INDICATE_CLAUSE
H
  HEADING -
      HELP PAGE_CLAUSE GENERAL_FORMAT
I
  I-O -
      HELP OPEN_SEQUENTIAL GENERAL_FORMAT
      HELP OPEN_RELATIVE GENERAL_FORMAT
      HELP OPEN_INDEXED GENERAL_FORMAT
      HELP USE_INDEXED GENERAL_FORMAT
      HELP OPEN_KEYED GENERAL_FORMAT
      HELP USE_KEYED GENERAL_FORMAT
      HELP USE_INTER_PROGRAM GENERAL_FORMAT
  I-O-CONTROL Paragraph -
      HELP IO_CONTROL_PARAGRAPH
      HELP IO_CONTROL_SORT_MERGE
      HELP IO_CONTROL_REPORT_WRITER
  Identification Division -
      HELP IDENTIFICATION_DIVISION
  IF Statement -
      HELP IF_STATEMENT
  IN -
      HELP COPY_STATEMENT GENERAL_FORMAT
  INDEX -
      HELP USAGE_CLAUSE GENERAL_FORMAT
  Index-Name conventions -
      HELP SCOPE_OF_NAMES
  INDEXED BY -
      HELP OCCURS_CLAUSE GENERAL_FORMAT
  INITIAL -
      HELP PROGRAM_ID_INTER_PROGRAM GENERAL_FORMAT
  INITIALIZE Statement -
      HELP INITIALIZE_STATEMENT
  INITIATE Statement -
      HELP INITIATE_STATEMENT
  INPUT -
      HELP OPEN_SEQUENTIAL GENERAL_FORMAT
      HELP OPEN_RELATIVE GENERAL_FORMAT
      HELP OPEN_INDEXED GENERAL_FORMAT
      HELP USE_INDEXED GENERAL_FORMAT
      HELP OPEN_KEYED GENERAL_FORMAT
      HELP USE_KEYED GENERAL_FORMAT
      HELP USE_INTER_PROGRAM GENERAL_FORMAT
  INPUT PROCEDURE -
      HELP SORT_STATEMENT GENERAL_FORMAT
  Input-Output Section -
      HELP INPUT_OUTPUT_SECTION
  INSPECT Statement -
      HELP INSPECT_STATEMENT
  INSTALLATION Paragraph -
      HELP INSTALLATION_PARAGRAPH
  Inter-Program Communication -
      HELP INTER_PROGRAM_COMMUNICATION
  INTO -
      HELP DIVIDE_STATEMENT GENERAL_FORMAT
      HELP STRING_STATEMENT GENERAL_FORMAT
  Introduction to Indexed I-O -
      HELP INDEXED_IO
  Introduction to Inter-Program Communication -
      HELP INTER_PROGRAM_COMMUNICATION
  Introduction to Keyed I-O -
      HELP KEYED_IO
  Introduction to Relative I-O -
      HELP RELATIVE_IO
  Introduction to Segmentation -
      HELP SEGMENTATION
  Introduction to Sequential I-O -
      HELP SEQUENTIAL_IO
  Introduction to Sort-Merge -
      HELP SORT_MERGE
  Introduction to Source Text Manipulation -
      HELP SOURCE_TEXT_MANIPULATION
  Introduction to the Report Writer -
      HELP REPORT_WRITER
  INVALID KEY -
      HELP DELETE_RELATIVE GENERAL_FORMAT
      HELP READ_RELATIVE GENERAL_FORMAT
      HELP REWRITE_RELATIVE GENERAL_FORMAT
      HELP START_RELATIVE GENERAL_FORMAT
      HELP WRITE_RELATIVE GENERAL_FORMAT
      HELP DELETE_INDEXED GENERAL_FORMAT
      HELP READ_INDEXED GENERAL_FORMAT
      HELP REWRITE_INDEXED GENERAL_FORMAT
      HELP WRITE_INDEXED GENERAL_FORMAT
      HELP DELETE_KEYED GENERAL_FORMAT
      HELP READ_KEYED GENERAL_FORMAT
      HELP REWRITE_KEYED GENERAL_FORMAT
      HELP START_KEYED GENERAL_FORMAT
      HELP WRITE_KEYED GENERAL_FORMAT
  Invoking the Compiler -
      HELP INVOKING_THE_COMPILER
J
  JUSTIFIED Clause -
      HELP JUSTIFIED_CLAUSE
K
  KEY -
      HELP START_RELATIVE GENERAL_FORMAT
      HELP START_KEYED GENERAL_FORMAT
  KEY IS -
      HELP OCCURS_CLAUSE GENERAL_FORMAT
L
  LABEL RECORDS Clause -
      HELP LABEL_RECORDS_CLAUSE
  LAST DETAIL -
      HELP PAGE_CLAUSE GENERAL_FORMAT
  LEADING -
      HELP SIGN_CLAUSE GENERAL_FORMAT
      HELP INSPECT_STATEMENT GENERAL_FORMAT
  LEFT -
      HELP SYNCHRONIZED_CLAUSE GENERAL_FORMAT
  LESS -
      HELP START_RELATIVE GENERAL_FORMAT
      HELP START_KEYED GENERAL_FORMAT
  LEVEL-66-ASCII -
      HELP SOURCE_COMPUTER_PARAGRAPH GENERAL_RULES
  Level-Number -
      HELP LEVEL_NUMBER
      HELP LEVEL_NUMBER_REPORT_WRITER
  LIMIT -
      HELP PAGE_CLAUSE GENERAL_FORMAT
  LINAGE Clause -
      HELP LINAGE_CLAUSE
  LINE -
      HELP WRITE_SEQUENTIAL GENERAL_FORMAT
      HELP PAGE_CLAUSE GENERAL_FORMAT
  LINE NUMBER Clause -
      HELP LINE_NUMBER_CLAUSE
  LINES -
      HELP LINAGE_CLAUSE GENERAL_FORMAT
  Linkage Section -
      HELP LINKAGE_SECTION
  LOCK -
      HELP CLOSE_SEQUENTIAL GENERAL_FORMAT
      HELP CLOSE_RELATIVE GENERAL_FORMAT
      HELP CLOSE_INDEXED GENERAL_FORMAT
      HELP CLOSE_KEYED GENERAL_FORMAT
M
  MEMORY SIZE -
      HELP OBJECT_COMPUTER_PARAGRAPH GENERAL_RULES
  MERGE Statement -
      HELP MERGE_STATEMENT
  MODULES -
      HELP OBJECT_COMPUTER_PARAGRAPH GENERAL_RULES
  MOVE Statement -
      HELP MOVE_STATEMENT
  MULTIPLE FILE TAPE -
      HELP IO_CONTROL_PARAGRAPH GENERAL_FORMAT
  MULTIPLE FILE TAPE Clause -
      HELP MULTIPLE_FILE_TAPE_CLAUSE
  MULTIPLY Statement -
      HELP MULTIPLY_STATEMENT
N
  NATIVE -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  Nested Source Program -
      HELP PROGRAM_ID_INTER_PROGRAM GENERAL_FORMAT
  NEXT GROUP Clause -
      HELP NEXT_GROUP_CLAUSE
  NEXT RECORD -
      HELP READ_SEQUENTIAL GENERAL_FORMAT
      HELP READ_RELATIVE GENERAL_FORMAT
      HELP READ_INDEXED GENERAL_FORMAT
      HELP READ_KEYED GENERAL_FORMAT
  NEXT SENTENCE -
      HELP IF_STATEMENT GENERAL_FORMAT
      HELP SEARCH_STATEMENT GENERAL_FORMAT
  NUMERIC -
      HELP INITIALIZE_STATEMENT GENERAL_FORMAT
  NUMERIC LIMIT -
      HELP COMPUTATIONAL_CLAUSE GENERAL_FORMAT
O
  OBJECT-COMPUTER Paragraph -
      HELP OBJECT_COMPUTER_PARAGRAPH
      HELP OBJECT_COMPUTER_SEGMENTATION
  OCCURS Clause -
      HELP OCCURS_CLAUSE
  OF -
      HELP COPY_STATEMENT GENERAL_FORMAT
  OFF -
      HELP SET_STATEMENT GENERAL_FORMAT
      HELP REPLACE_STATEMENT GENERAL_FORMAT
  OFF STATUS -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  OMITTED -
      HELP LABEL_RECORDS_CLAUSE GENERAL_FORMAT
  ON -
      HELP SET_STATEMENT GENERAL_FORMAT
  ON OVERFLOW -
      HELP STRING_STATEMENT GENERAL_FORMAT
  ON STATUS -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  OPEN Statement -
      HELP OPEN_SEQUENTIAL
      HELP OPEN_RELATIVE
      HELP OPEN_INDEXED
      HELP OPEN_KEYED
      HELP OPEN_REPORT_WRITER
  ORGANIZATION IS INDEXED Clause -
      HELP ORGANIZATION_IS_INDEXED
  ORGANIZATION IS KEYED Clause -
      HELP ORGANIZATION_IS_KEYED
  ORGANIZATION IS RELATIVE Clause -
      HELP ORGANIZATION_IS_RELATIVE
  ORGANIZATION IS SEQUENTIAL Clause -
      HELP ORGANIZATION_IS_SEQUENTIAL
  OTHER -
      HELP EVALUATE_STATEMENT GENERAL_FORMAT
  OUTPUT -
      HELP OPEN_SEQUENTIAL GENERAL_FORMAT
      HELP OPEN_RELATIVE GENERAL_FORMAT
      HELP OPEN_INDEXED GENERAL_FORMAT
      HELP USE_INDEXED GENERAL_FORMAT
      HELP OPEN_KEYED GENERAL_FORMAT
      HELP USE_KEYED GENERAL_FORMAT
      HELP USE_INTER_PROGRAM GENERAL_FORMAT
  OUTPUT PROCEDURE -
      HELP MERGE_STATEMENT GENERAL_FORMAT
      HELP SORT_STATEMENT GENERAL_FORMAT
  OVERFLOW -
      HELP STRING_STATEMENT GENERAL_FORMAT
  Overview -
      HELP PROCESSOR
P
  PADDING CHARACTER -
      HELP SELECT_SEQUENTIAL GENERAL_FORMAT
  PADDING CHARACTER Clause -
      HELP PADDING_CHARACTER_CLAUSE
  PAGE -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
      HELP WRITE_SEQUENTIAL GENERAL_FORMAT
  PAGE Clause -
      HELP PAGE_CLAUSE
  PAGE FOOTING -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  PAGE HEADING -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  PERFORM Statement -
      HELP PERFORM_STATEMENT
  PF -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  PH -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  PICTURE Clause -
      HELP PICTURE_CLAUSE
  POINTER -
      HELP STRING_STATEMENT GENERAL_FORMAT
      HELP UNSTRING_STATEMENT GENERAL_FORMAT
  POSITION -
      HELP IO_CONTROL_PARAGRAPH GENERAL_FORMAT
  PRINTING -
      HELP SUPPRESS_STATEMENT GENERAL_FORMAT
  Procedure Division Body -
      HELP PROCEDURE_DIV_BODY
  Procedure Division Header -
      HELP PROCEDURE_DIV_HEADER
      HELP PROCEDURE_DIV_INTER_PROGRAM
  Procedure Division, Report Writer -
      HELP PROCEDURE_DIV_REPORT_WRITER
  Procedure Division, Segmentation -
      HELP PROCEDURE_DIV_SEGMENTATION
  Procedures -
      HELP PROCEDURE_DIVISION
  PROCEED TO -
      HELP ALTER_STATEMENT GENERAL_FORMAT
  PROGRAM COLLATING SEQUENCE -
      HELP OBJECT_COMPUTER_PARAGRAPH GENERAL_RULES
  PROGRAM-ID Paragraph -
      HELP PROGRAM_ID_PARAGRAPH
  PROGRAM-ID Paragraph and Nested Source Programs -
      HELP PROGRAM_ID_INTER_PROGRAM
  Program-Names -
      HELP SCOPE_OF_NAMES
R
  RANDOM -
      HELP ACCESS_MODE_RELATIVE GENERAL_FORMAT
      HELP ACCESS_MODE_INDEXED GENERAL_FORMAT
      HELP ACCESS_MODE_KEYED GENERAL_FORMAT
  RD, Inter-Program Communication -
      HELP RD_INTER_PROGRAM GENERAL_FORMAT
  RD, Report Writer -
      HELP RD_REPORT_WRITER GENERAL_FORMAT
  READ Statement -
      HELP READ_SEQUENTIAL
      HELP READ_RELATIVE
      HELP READ_INDEXED
      HELP READ_KEYED
  RECORD Clause -
      HELP RECORD_CLAUSE
  RECORD DELIMITER -
      HELP SELECT_SEQUENTIAL GENERAL_FORMAT
  RECORD DELIMITER Clause -
      HELP RECORD_DELIMITER_CLAUSE
  RECORD KEY -
      HELP ACCESS_MODE_KEYED GENERAL_FORMAT
  RECORD KEY Clause -
      HELP RECORD_KEY_CLAUSE
  REDEFINES Clause -
      HELP REDEFINES_CLAUSE
  REEL -
      HELP CLOSE_SEQUENTIAL GENERAL_FORMAT
  REFERENCE -
      HELP CALL_STATEMENT GENERAL_FORMAT
  RELATIVE KEY -
      HELP ACCESS_MODE_RELATIVE GENERAL_FORMAT
  RELEASE Statement -
      HELP RELEASE_STATEMENT
  REMAINDER -
      HELP DIVIDE_STATEMENT GENERAL_FORMAT
  REMOVAL -
      HELP CLOSE_SEQUENTIAL GENERAL_FORMAT
  RENAMES Clause -
      HELP RENAMES_CLAUSE
  REPLACE Statement -
      HELP REPLACE_STATEMENT
  REPLACING -
      HELP INITIALIZE_STATEMENT GENERAL_FORMAT
      HELP INSPECT_STATEMENT GENERAL_FORMAT
      HELP COPY_STATEMENT GENERAL_FORMAT
  REPORT Clause -
      HELP REPORT_CLAUSE
  Report Description Entry -
      HELP RD_REPORT_WRITER
  Report Description Entry, Inter-Program Communication -
      HELP RD_INTER_PROGRAM
  REPORT FOOTING -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
  Report Group Description Entry -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY
  REPORT HEADING -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  Report Section -
      HELP REPORT_SECTION
  Report Writer -
      HELP REPORT_WRITER
  RESERVE -
      HELP SELECT_SEQUENTIAL GENERAL_FORMAT
  RESERVE Clause -
      HELP RESERVE_CLAUSE
  RESET -
      HELP SUM_CLAUSE GENERAL_FORMAT
  RETENTION -
      HELP VALUE_OF_CLAUSE GENERAL_FORMAT
  RETURN Statement -
      HELP RETURN_STATEMENT
  REWIND -
      HELP CLOSE_SEQUENTIAL GENERAL_FORMAT
      HELP OPEN_SEQUENTIAL GENERAL_FORMAT
  REWRITE Statement -
      HELP REWRITE_SEQUENTIAL
      HELP REWRITE_RELATIVE
      HELP REWRITE_INDEXED
      HELP REWRITE_KEYED
  RF -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
  RH -
      HELP REPORT_GROUP_DESCRIPTION_ENTRY GENERAL_FORMAT
      HELP TYPE_CLAUSE GENERAL_FORMAT
  RIGHT -
      HELP SYNCHRONIZED_CLAUSE GENERAL_FORMAT
  RUN -
      HELP STOP_STATEMENT GENERAL_FORMAT
S
  SAME Clause -
      HELP SAME_CLAUSE
  SAME RECORD AREA -
      HELP IO_CONTROL_PARAGRAPH GENERAL_FORMAT
  SAME RECORD/SORT/SORT-MERGE AREA Clause -
      HELP SAME_SORT_MERGE
  Sample Program -
      HELP SAMPLE_PROGRAM
  SCALAR -
      HELP GENERATE_DESCRIPTOR_CLAUSE GENERAL_FORMAT
  SD, Sort-Merge -
      HELP SD_SORT_MERGE GENERAL_FORMAT
  SEARCH Statement -
      HELP SEARCH_STATEMENT
  SECTION -
      HELP SEGMENT_NUMBERS GENERAL_FORMAT
  SECURITY Paragraph -
      HELP SECURITY_PARAGRAPH
  SEGMENT-LIMIT Clause -
      HELP SEGMENT_LIMIT_CLAUSE
  Segment-Numbers -
      HELP SEGMENT_NUMBERS
  Segmentation -
      HELP SEGMENTATION
  SELECT, Indexed Files -
      HELP SELECT_INDEXED GENERAL_FORMAT
  SELECT, Keyed Files -
      HELP SELECT_KEYED GENERAL_FORMAT
  SELECT, Relative Files -
      HELP SELECT_RELATIVE GENERAL_FORMAT
  SELECT, Report Writer -
      HELP SELECT_REPORT_WRITER GENERAL_FORMAT
  SELECT, Sequential Files -
      HELP SELECT_SEQUENTIAL FUNCTION
  SEPARATE CHARACTER -
      HELP SIGN_CLAUSE GENERAL_FORMAT
  SEQUENCE -
      HELP OBJECT_COMPUTER_PARAGRAPH GENERAL_RULES
      HELP MERGE_STATEMENT GENERAL_FORMAT
      HELP SORT_STATEMENT GENERAL_FORMAT
  SET Statement -
      HELP SET_STATEMENT
  SIGN -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  SIGN Clause -
      HELP SIGN_CLAUSE
      HELP SIGN_CLAUSE_REPORT_WRITER
  SIZE -
      HELP STRING_STATEMENT GENERAL_FORMAT
  SORT Statement -
      HELP SORT_STATEMENT
  Sort-Merge File Description Entry -
      HELP SD_SORT_MERGE
  SOURCE Clause -
      HELP SOURCE_CLAUSE
  Source Program -
      HELP SOURCE_PROGRAM
  Source Text Manipulation -
      HELP SOURCE_TEXT_MANIPULATION
  SOURCE-COMPUTER Paragraph -
      HELP SOURCE_COMPUTER_PARAGRAPH
  SPECIAL-NAMES Paragraph -
      HELP SPECIAL_NAMES_PARAGRAPH
  STANDARD -
      HELP LABEL_RECORDS_CLAUSE GENERAL_FORMAT
      HELP USE_RELATIVE GENERAL_FORMAT
      HELP USE_KEYED GENERAL_FORMAT
      HELP USE_INTER_PROGRAM GENERAL_FORMAT
  STANDARD-1 -
      HELP SELECT_SEQUENTIAL GENERAL_FORMAT
  STANDARD-1, STANDARD-2 -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  START Statement -
      HELP START_RELATIVE
      HELP START_INDEXED
      HELP START_KEYED
  STOP Statement -
      HELP STOP_STATEMENT
  STRING Statement -
      HELP STRING_STATEMENT
  SUBTRACT Statement -
      HELP SUBTRACT_STATEMENT
  SUM Clause -
      HELP SUM_CLAUSE
  SUPPRESS Statement -
      HELP SUPPRESS_STATEMENT
  SWITCH-n -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  SYMBOLIC CHARACTERS -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
  SYNCHRONIZED Clause -
      HELP SYNCHRONIZED_CLAUSE
  syntax notations -
      HELP NOTATION_CONVENTIONS
  SYSIN -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
      HELP ACCEPT_STATEMENT GENERAL_FORMAT
  SYSOUT -
      HELP SPECIAL_NAMES_PARAGRAPH GENERAL_FORMAT
      HELP DISPLAY_STATEMENT GENERAL_FORMAT
T
  TALLYING -
      HELP INSPECT_STATEMENT GENERAL_FORMAT
      HELP UNSTRING_STATEMENT GENERAL_FORMAT
  TERMINATE Statement -
      HELP TERMINATE_STATEMENT
  TEST -
      HELP PERFORM_STATEMENT GENERAL_FORMAT
  TIME -
      HELP ACCEPT_STATEMENT GENERAL_FORMAT
  TIMES -
      HELP PERFORM_STATEMENT GENERAL_FORMAT
  TO -
      HELP ALTER_STATEMENT GENERAL_FORMAT
  TOP -
      HELP LINAGE_CLAUSE GENERAL_FORMAT
  TRAILING -
      HELP SIGN_CLAUSE GENERAL_FORMAT
  TRUE -
      HELP EVALUATE_STATEMENT GENERAL_FORMAT
      HELP SET_STATEMENT GENERAL_FORMAT
  TYPE Clause -
      HELP TYPE_CLAUSE
U
  UNIT -
      HELP CLOSE_SEQUENTIAL GENERAL_FORMAT
  UNSTRING Statement -
      HELP UNSTRING_STATEMENT
  UNTIL -
      HELP PERFORM_STATEMENT GENERAL_FORMAT
  UP BY -
      HELP SET_STATEMENT GENERAL_FORMAT
  UPON -
      HELP DISPLAY_STATEMENT GENERAL_FORMAT
  USAGE Clause -
      HELP USAGE_CLAUSE
      HELP USAGE_CLAUSE_REPORT_WRITER
  USE AFTER STANDARD EXCEPTION PROCEDURE Statement -
      HELP USE_REPORT_WRITER
  USE BEFORE REPORTING Statement -
      HELP USE_BEFORE_REPORTING_INTER_PR
      HELP USE_BEFORE_REPORTING_REPORT_W
  USE Statement -
      HELP USE_SEQUENTIAL
      HELP USE_RELATIVE
      HELP USE_INDEXED
      HELP USE_KEYED
      HELP USE_INTER_PROGRAM
  USING -
      HELP PROCEDURE_DIV_INTER_PROGRAM
      HELP CALL_STATEMENT GENERAL_FORMAT
V
  VALUE Clause -
      HELP VALUE_CLAUSE
      HELP VALUE_CLAUSE_REPORT_WRITER
  VALUE OF Clause -
      HELP VALUE_OF_CLAUSE
  VARYING -
      HELP PERFORM_STATEMENT GENERAL_FORMAT
      HELP SEARCH_STATEMENT GENERAL_FORMAT
      HELP RECORD_CLAUSE GENERAL_FORMAT
W
  WHEN -
      HELP EVALUATE_STATEMENT GENERAL_FORMAT
      HELP SEARCH_STATEMENT GENERAL_FORMAT
  WHEN OTHER -
      HELP EVALUATE_STATEMENT GENERAL_FORMAT
  WITH DEBUGGING MODE -
      HELP SOURCE_COMPUTER_PARAGRAPH GENERAL_RULES
  WORDS -
      HELP OBJECT_COMPUTER_PARAGRAPH GENERAL_RULES
  Working-Storage Section -
      HELP WORKING_STORAGE_SECTION
  WRITE Statement -
      HELP WRITE_SEQUENTIAL
      HELP WRITE_RELATIVE
      HELP WRITE_INDEXED
      HELP WRITE_KEYED
X
  X9MA$ALLOCATE Subroutine -
      HELP X9MA$ALLOCATE_SUBROUTINE
  X9MA$FREE Subroutine -
      HELP X9MA$FREE_SUBROUTINE
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
The following list gives an overview of the
major groups of topics provided by the COBOL85
HELP facility:
NUCLEUS, SEQUENTIAL_IO, RELATIVE_IO, INDEXED_IO,
KEYED_IO, INTER_PROGRAM_COMMUNICATION, SORT_MERGE,
SOURCE_TEXT_MANIPULATION, REPORT_WRITER,
SEGMENTATION, COMPILER and COBOL_DIVISIONS.
Each of the above topics, when requested provides
general information and pointers to related topics.
For a complete list of topics, enter:
HELP (COBOL85) TOPICS
HELP_INDEX
The Identification Division identifies the program.  In addition, the user may
include the date the program is written, the date the compilation of the
source program is accomplished, and other information as desired under the
paragraphs in the general format shown below.
Paragraph headers identify the type of information contained in the paragraph.
The name of the program must be given in the first paragraph, which is the
PROGRAM-ID paragraph.  The other paragraphs are optional and may be included
in this division at the user's choice, in order of presentation shown by the
format below.
General Format
IDENTIFICATION  DIVISION.
PROGRAM-ID.  program-name
[AUTHOR. [comment-entry] ... ]
[INSTALLATION. [comment-entry] ... ]
DATE-WRITTEN. [comment-entry] ... ]
[DATE-COMPILED. [comment-entry] ... ]
[SECURITY. [comment-entry] ... ]
00001
Function
The IF statement causes a condition to be evaluated.  The subsequent action of
the object program depends on whether the value of the condition is true or
false.
General Format
                    {                 } {ELSE {statement-2} ...[END-IF]}
IF condition-1 THEN {{statement-1} ...} {ELSE NEXT SENTENCE            }
                    {NEXT SENTENCE    } {[END-IF]                      }
Syntax Rules
1.  Statement-1 and statement-2 represent either an imperative statement or a
    conditional statement optionally preceded by an imperative statement.
2.  The ELSE NEXT SENTENCE phrase may be omitted if it immediately precedes
    the terminal period of the sentence.
3.  If the END-IF phrase is specified, the NEXT SENTENCE phrase must not be
    specified.
00001
    Indexed I-O allows records of a mass storage file to be accessed in either
    a random or sequential manner.  Each record in an indexed file is uniquely
    identified by an alphanumeric value of one or more keys within that
    record.
    A file with indexed organization is a mass storage file from which any
    record may be accessed by giving the value of a specified key in that
    record.  For each key data item defined for the records of a file, an
    index is maintained.  Each such index represents the set of values from
    the corresponding key data item in each record.  Each index, therefore, is
    a mechanism which can provide access to any record in the file.
    See the following related topics:
    INPUT_OUTPUT, FILE_CONTROL, SELECT_INDEXED,
    ACCESS_MODE_INDEXED, ALTERNATE_RECORD_KEY,
    ORGANIZATION_IS_INDEXED, RECORD_KEY, IO_CONTROL,
    FILE_SECTION, FD_INDEXED, CLOSE_INDEXED, DELETE,
    OPEN_INDEXED, READ_INDEXED, REWRITE_INDEXED, START_INDEXED,
    USE, and WRITE_INDEXED.
Function
The INITIALIZE statement provides the ability to set selected types of data
fields to predetermined values (e.g., numeric data to zeros or alphanumeric
data to spaces).
General Format
INITIALIZE {identifier-1} ...
  [          {{ALPHABETIC         }                       }    ]
  [          {{ALPHANUMERIC       }                       }    ]
  [REPLACING {{NUMERIC            } DATA BY {identifier-2}} ...]
  [          {{ALPHANUMERIC-EDITED}         {literal-1   }}    ]
  [          {{NUMERIC-EDITED     }                       }    ]
Syntax Rules
1.  Literal-1 and the data item referenced by identifier-2 represent the
    sending area; the data item referenced by identifier-1 represents the
    receiving area.
2.  Each category stated in the REPLACING phrase must be a permissible
    category as a receiving operand in a MOVE statement where the
    corresponding data item referenced by identifier-2 or literal-1 is used as
    the sending operand.
3.  The same category cannot be repeated in a REPLACING phrase.
4.  The description of the data item referenced by identifier-1 or any items
    subordinate to identifier-1 may not contain the DEPENDING phrase of the
    OCCURS clause.
5.  An index data item may not appear as an operand of an INITIALIZE
    statement.
6.  The data description entry for the data item referenced by identifier-1
    must not contain a RENAMES clause.
00001
Function
The INITIATE statement causes the report writer control system (RWCS) to begin
the processing of a report.
General Format
INITIATE {report-name-1} ...
Syntax Rule
1.  Report-name-1 must be defined by a report description entry in the Report
    Section of the Data Division.
00001
    The Input-Output Section is located in the Environment Division of a
    source program.  The Input-Output Section deals with the information
    needed to control transmission and handling of data between external media
    and the object program.  The Input-Output Section is optional in the
    Environment Division of a COBOL source program.
General Format
INPUT-OUTPUT SECTION.
FILE-CONTROL. {file-control-entry} ...
[I-O-CONTROL.  [input-output-control-entry]]
Function
The INSPECT statement provides the ability to tally or replace occurrences of
single characters or groups of characters in a data item.
General Format
Format 1:
INSPECT identifier-1 TALLYING
{                 {CHARACTERS [{BEFORE} INITIAL {identifier-4}] ...
{                 {           [{AFTER }         {literal-2   }]
{identifier-2 FOR {
{                 {{ALL    } {{identifier-3} [{BEFORE} INITIAL
{                 {{LEADING} {{literal-1   } [{AFTER }
                                                               }    }
                                                               }    }
                                                          }    } ...} ...
                                       {identifier-4}] ...} ...}    }
                                       {literal-2   }]    }    }    }
Format 2:
INSPECT identifier-1 REPLACING
{CHARACTERS BY {identifier-5} [{BEFORE} INITIAL {identifier-4}] ...
{              {literal-3   } [{AFTER }         {literal-2   }]
{
{{ALL    } {{identifier-3}    {identifier-5} [{BEFORE}
{{LEADING} {{literal-1   } BY {literal-3   } [{AFTER } INITIAL
{{FIRST  } {
                                                                  }
                                                                  }
                                                                  } ...
                                          {identifier-4}]    }    }
                                          {literal-2   }] ...} ...}
Format 3:
INSPECT identifier-1 TALLYING
{                 {CHARACTERS [{BEFORE} INITIAL {identifier-4}] ...
{                 {           [{AFTER }         {literal-2   }]
{identifier-2 FOR {
{                 {{ALL    } {{identifier-3} [{BEFORE} INITIAL
{                 {{LEADING} {{literal-1   } [{AFTER }
                                                             }    }
                                                             }    }
                                                        }    } ...} ...
                                     {identifier-4}] ...} ...}    }
                                     {literal-2   }]    }    }    }
REPLACING
  { CHARACTERS BY {identifier-5} [{BEFORE} INITIAL {identifier-4}] ...
  {               {literal-3   } [{AFTER }         {literal-2   }]
  {
  {{ALL    } {{identifier-3}    {identifier-5} [{BEFORE}
  {{LEADING} {{literal-1   } BY {literal-3   } [{AFTER } INITIAL
  {{FIRST  } {
                                                                  }
                                                                  }
                                                                  } ...
                                          {identifier-4}]    }    }
                                          {literal-2   }] ...} ...}
                                                             }    }
Format 4:
INSPECT identifier-1 CONVERTING {identifier-6} TO {identifier-7}
                                {literal-4   }    {literal-5   }
  [{BEFORE} INITIAL {identifier-4}] ...
  [{AFTER }         {literal-2   }]
Syntax Rules
ALL FORMATS:
1.  Identifier-1 must reference either a group item or any category of
    elementary item described, implicitly or explicitly, as USAGE IS DISPLAY.
2.  Identifier-3, ... , identifier-n must reference an elementary item
    described, implicitly or explicitly, as USAGE IS DISPLAY.
3.  Each literal must be a nonnumeric literal and must not be a figurative
    constant that begins with the word ALL.  If literal-1, literal-2, or
    literal-4 is a figurative constant, it refers to an implicit one character
    data item.
4.  No more than one BEFORE phrase and one AFTER phrase can be specified for
    any one ALL, LEADING, CHARACTERS, FIRST, or CONVERTING phrase.
FORMATS 1 AND 3:
5.  Identifier-2 must reference an elementary numeric data item.
FORMATS 2 AND 3:
6.  The size of literal-3 or the data item referenced by identifier-5 must be
    equal to the size of literal-1 or the data item referenced by
    identifier-3.  When a figurative constant is used as literal-3, the size
    of the figurative constant is equal to the size of literal-1 or the size
    of the data item referenced by identifier-3.
7.  When the CHARACTERS phrase is used, literal-2, literal-3, or the size of
    the data item referenced by identifier-4, identifier-5 must be one
    character in length.
FORMAT 4:
8.  The size of literal-5 or the data item referenced by identifier-7 must be
    equal to the size of literal-4 or the data item referenced by
    identifier-6.  When a figurative constant is used as literal-5, the size
    of the figurative constant is equal to the size of literal-4 or the size
    of the data item referenced by identifier-6.
9.  The same character must not appear more than once either in literal-4 or
    in the data item referenced by identifier-6.
00001
    The INSTALLATION paragraph is used to supply the name of or otherwise
    identify the installation at which the source program was written.
General Format
[INSTALLATION. [literal] [comment-entry]]
Syntax Rules
1.  The literal must be a nonnumeric literal and, if present, must precede the
    comment-entry.
2.  The comment-entry can be one or more sentences, including any combination
    of characters.  The comment-entry has no effect on the operation of a
    COBOL program.
    Inter-Program Communication allows a program to communicate with one or
    more programs.  This communication is provided by:  (a) the ability to
    transfer control from one program to another within a run unit and, (b)
    the ability to pass parameters between programs to make certain data value
    available to a called program.  The Inter-Program Communication module
    also permits communication between two programs by the sharing of data and
    the sharing of files.    See the following related topics:
    END_PROGRAM_HEADER_INTER_PROG, PROGRAM_ID_INTER_PROG,
    LINKAGE, FD_INTER_PROG, DATA_DESCRIPTION_INTER_PROG,
    RD_INTER_PROG, EXTERNAL, GLOBAL, PROCEDURE_DIV_INTER_PROG,
    CALL, CANCEL, EXIT_PROGRAM, USE_INTER_PROG, and
    USE_BEFORE_REPORTING_INTER_PR.

Function
The I-O-CONTROL paragraph specifies the memory area which is to be shared by
different files and the location of files on a multiple file reel.
General Format
I-0-CONTROL.
  [[SAME [RECORD] AREA FOR file-name-1 {file-name-2} ...] ...
    [MULTIPLE FILE TAPE CONTAINS
      {file-name-3 [POSITION integer-1]} ...] ... .]
Syntax Rule
1.  The clauses may appear in any order.
00001
Function
The I-O-CONTROL paragraph specifies the memory area which is to be shared by
different files and the location of files on a multiple file reel.
General Format
I-O-CONTROL.
  [[SAME AREA FOR file-name-1 {file-name-2} ...] ...
  [MULTIPLE FILE TAPE CONTAINS
    {file-name-3 [POSITION integer-1]} ...] ... .]
Syntax Rules
1.  The clauses may appear in any order.
2.  A file-name that represents a report file can appear in a MULTIPLE FILE
    TAPE clause or in a SAME clause for which the RECORD phrase is not
    specified.
00001
Function
The I-O-CONTROL paragraph specifies the memory area which is to be shared by
different files including sort or merge files.
General Format
I-O-CONTROL.
    [[     {RECORD    }
    [[SAME {SORT      } AREA FOR file-name-1 {file-name-2} ...] ... .]
    [[     {SORT-MERGE}
    See HELP (COBOL85) SAME_SORT_MERGE
00001
INPUT_OUTPUT_SECTION
IO_CONTROL_PARAGRAPH
IO_CONTROL_REPORT_WRITER
IO_CONTROL_SORT_MERGE
Function
The JUSTIFIED clause permits alternate positioning of data within a receiving
data item.
General Format
{JUSTIFIED} RIGHT
{JUST     }
Syntax Rules
1.  The JUSTIFIED clause can be specified only at the elementary item level.
2.  JUST is an abbreviation for JUSTIFIED.
3.  The JUSTIFIED clause cannot be specified for any data item described as
    numeric or for which editing is specified.
4.  The JUSTIFIED clause must not be specified for an index data item.
00001
    Keyed I-O provides a capability to access records of a mass storage file
    in either a random or sequential manner.  Each record in a keyed file is
    uniquely identified by the value of a key that is not required to be
    contained in each individual record.
    See the following related topics:
    INPUT_OUTPUT, FILE_CONTROL, SELECT_KEYED, ACCESS_MODE_KEYED,
    ORGANIZATION_IS_KEYED, IO_CONTROL, FILE_SECTION, FD_KEYED,
    CLOSE_KEYED, DELETE, OPEN_KEYED, READ_KEYED,
    REWRITE_KEYED, START_KEYED, USE, and WRITE_KEYED.
Function
The LABEL RECORDS clause specifies whether or not labels are present.
General Format
LABEL {RECORD IS  } {STANDARD}
      {RECORDS ARE} {OMITTED }
General Rules
1.  OMITTED specifies that no explicit labels exist for the file or the device
    to which the file is assigned.
2.  STANDARD specifies that labels exist for the file or the device to which
    the file is assigned and the labels conform to the label specifications.
3.  If the LABEL RECORDS clause is not specified for a file, label records for
    that file must conform to the label specifications.
4.  If the file connector associated with this file description entry is an
    external file connector all LABEL RECORDS clauses in the run unit which
    are associated with this file connector must be the same.
00001
    LENGTH OF identifier-1
1.  Identifier-1 may name any item of any level except 66 or 88 within the
    program's own WORKING STORAGE, FILE SECTION or LINKAGE SECTION.
2.  When LENGTH OF identifier-1 is used in a CALL statement, it must be
    specified in the USING ... BY CONTENT clause.
Function
The level-number indicates the position of a data item within the hierarchical
structure of a logical record.  In addition, it is used to identify entries
for working storage items, linkage items, condition-names, and the RENAMES
clause.
General Format
level-number
Syntax Rules
1.  A level-number is required as the first element in each data description
    entry.
2.  Data description entries subordinate to a FD or SD entry must have
    level-numbers with the values 01 through 49, 66, or 88.
3.  Data description entries in the Working-Storage Section and Linkage
    Section must have level-numbers 01 through 49, 66, 77, or 88.
00001
Function
The level-number indicates the position of a data item within the hierarchical
structure of a report group.
General Format
level-number
Syntax Rules
1.  A level-number is required as the first element in each data description
    entry.
2.  Data description entries subordinate to an RD entry must have
    level-numbers 01 through 49 only.
00001
Function
The LINAGE clause allows specification of the depth of a logical page in terms
of number of lines.  It also allows specification of the size of the top and
bottom margins on the logical page, and the line number, within the page body,
at which the footing area begins.
General Format
LINAGE IS {data-name-1} LINES [WITH FOOTING AT {data-name-2}]
          {integer-1  }       [                {integer-2  }]
  [LINES AT TOP {data-name-3}] [LINES AT BOTTOM {data-name-4}]
  [             {integer-3  }] [                {integer-4  }]
Syntax Rules
1.  Data-name-1, data-name-2, data-name-3, data-name-4 must reference
    elementary unsigned numeric integer data items.
2.  Data-name-1, data-name-2, data-name-3, data-name-4 may be qualified.
3.  Integer-2 must not be greater than integer-1.
4.  Integer-2, integer-4 may be zero.
00001
Function
The LINE NUMBER clause specifies vertical positioning information for its
report group.
General Format
LINE NUMBER IS {integer-1 [ON NEXT PAGE]}
               {PLUS integer-2          }
Syntax Rules
1.  Integer-1 and integer-2 must not exceed three significant digits in
    length.
    Neither integer-1 nor integer-2 may be specified in such a way as to cause
    any line of a report group to be presented outside the vertical
    subdivision of the page designated for that report group type, as defined
    by the PAGE clause.
    Integer-2 may be zero.
2.  Within a given report group description entry, an entry that contains a
    LINE NUMBER clause must not contain a subordinate entry that also contains
    a LINE NUMBER clause.
3.  Within a given report group description entry, all absolute LINE NUMBER
    clauses must precede all relative LINE NUMBER clauses.
4.  Within a given report group description entry, successive absolute LINE
    NUMBER clauses must specify integers that are in ascending order.  The
    integers need not be consecutive.
5.  If the PAGE clause is omitted from a given report description entry, only
    relative LINE NUMBER clauses may be specified in any report group
    description entry within that report.
6.  Within a given report group description entry, a NEXT PAGE phrase may
    appear only once and, if present, must be in the first LINE NUMBER clause
    in that report group description entry.
7.  A LINE NUMBER clause with the NEXT PAGE phrase may appear only in the
    description of body groups and in a REPORT FOOTING report group.
8.  Every entry that defines a printable item (see COLUMN NUMBER Clause) must
    either contain a LINE NUMBER clause, or be subordinate to an entry that
    contains a LINE NUMBER clause.
9.  The first LINE NUMBER clause specified within a PAGE FOOTING report group
    must be an absolute LINE NUMBER clause.
00001
    The Linkage Section is located in the Data Division of a source program.
    The Linkage Section appears in the called program and describes data items
    that are to be referred to by the calling program and the called program.
General Format
LINKAGE SECTION.
[77-level-description-entry] ...
[record description-entry  ]
If a data item in the Linkage Section is accessed in a program which is not a
called program, the effect is undefined, unless the address of the data item
has been established by a Format 5 SET statement.
Function
The MERGE statement combines two or more identically sequenced files on a set
of specified keys, and during the process makes records available, in merged
order, to an output procedure or to an output file.
General Format
MERGE file-name-1 {ON {ASCENDING } KEY {data-name-1} ...} ...
                  {   {DESCENDING}                      }
    [COLLATING SEQUENCE IS alphabet-name-1]
    USING file-name-2 {file-name-3} ...
    {OUTPUT PROCEDURE IS procedure-name-1 [{THROUGH} procedure-name-2]}
    {                                     [{THRU   }                 ]}
    {GIVING {file-name-4} ...                                         }
Syntax Rules
1.  A MERGE statement may appear anywhere in the Procedure Division except in
    the declarative portion.
2.  File-name-1 must be described in a sort-merge file description entry in
    the Data Division.
3.  If the file referenced by file-name-1 contains variable length records,
    the size of the records contained in the files referenced by file-name-2
    and file-name-3 must not be less than the smallest record nor greater than
    the largest record described for file-name-1.  If the file referenced by
    file-name-1 contains fixed length records, the size of the records
    contained in the file referenced by file-name-2 and file-name-3 must not
    be greater than the largest record described for file-name-1.
4.  Data-name-1 is a key data-name.  Key data-names are subject to the
    following rules:
    a.  The data items identified by key data-names must be described in
        records associated with file-name-1.
    b.  Key data-names may be qualified.
    c.  The data items identified by key data-names must not be group items
        that contain variable occurrence data items.
    d.  If file-name-1 has more than one record description, the data items
        identified by key data-names need to be described in only one of the
        record descriptions.  The same character positions referenced by a key
        data-name in one record description entry are taken as the key in all
        records of the file.
    e.  None of the data items identified by key data-names can be described
        by an entry that either contains an OCCURS clause or is subordinate to
        an entry that contains an OCCURS clause.
    f.  If the file referenced by file-name-1 contains variable length
        records, all the data items identified by key data-names must be
        contained within the first x character positions of the record, where
        x equals the minimum record size specified for the file referenced by
        file-name-1.
    g.  None of the data items identified by key data-names can be described
        as USAGE IS EBCDIC.
5.  File-name-2, file-name-3, and file-name-4 must be described in a file
    description entry, not in a sort-merge file description entry, in the Data
    Division.
6.  No two files specified in any one MERGE statement may reside on the same
    multiple file reel.
7.  File-names must not be repeated within the MERGE statement.
8.  No pair of file-names in a MERGE statement may be specified in the same
    SAME AREA, SAME SORT AREA, or SAME SORT-MERGE AREA clause.  The only
    file-names in a MERGE statement that can be specified in the same SAME
    RECORD AREA clause are those associated with the GIVING phrase.
9.  The words THRU and THROUGH are equivalent.
10. If file-name-4 references an indexed file, the first specification of
    data-name-1 must be associated with an ASCENDING phrase and the data item
    referenced by that data-name-1 must occupy the same character positions in
    its record as the data item associated with the prime record key for that
    file.
11. If the GIVING phrase is specified and the file referenced by file-name-4
    contains variable length records, the size of the records contained in the
    file referenced by file-name-1 must not be less than the smallest record
    nor greater than the largest record described for file-name-4.  If the
    file referenced by file-name-4 contains fixed length records, the size of
    the records contained in the file referenced by file-name-1 must not be
    greater than the largest record described for file-name-4.
00001
Function
The MOVE statement transfers data, in accordance with the rules of editing, to
one or more data areas.
General Format
Format 1:
MOVE {identifier-1} TO {identifier-2} ...
     {literal-1   }
Format 2:
MOVE {CORRESPONDING} identifier-1 TO identifier-2
     {CORR         }
Syntax Rules
1.  Literal-1 or the data item referenced by identifier-1 represents the
    sending area.  The data item referenced by identifier-2 represents the
    receiving area.
2.  CORR is an abbreviation for CORRESPONDING.
3.  When the CORRESPONDING phrase is used, all identifiers must be group
    items.
4.  An index data item must not appear as an operand of a MOVE statement.
00001
Function
The MULTIPLE FILE TAPE clause specifies the location of files on a multiple
file reel.
General Format
MULTIPLE FILE TAPE CONTAINS {file-name-1 [POSITION integer-1]} ...
Syntax Rules
1.  Each file-name specified in a MULTIPLE FILE TAPE clause must be specified
    in the FILE-CONTROL paragraph of the same program.
2.  File-name-1 may not reference an external file connector.
3.  Each file-name specified in a MULTIPLE FILE TAPE clause must have an
    associated file description entry.
4.  The same file-name must not be specified more than once in a MULTIPLE FILE
    TAPE clause.  The same file-name must not be specified in more than one
    MULTIPLE FILE TAPE clause.
00001
Function
The MULTIPLY statement causes numeric data items to be multiplied and sets the
values of data items equal to the results.
General Format
Format 1:
MULTIPLY {identifier-1} BY {identifier-2 [ROUNDED]} ...
         {literal-1   }
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-MULTIPLY]
Format 2:
MULTIPLY {identifier-1} BY {identifier-2}
         {literal-1   }    {literal-2   }
  GIVING {identifier-3 [ROUNDED]} ...
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-MULTIPLY]
Syntax Rules
1.  Each identifier must refer to a numeric elementary item, except that in
    format 2 each identifier following the word GIVING must refer to either an
    elementary numeric item or an elementary numeric edited item.
2.  Each literal must be a numeric literal.
3.  The composite of operands, which is that hypothetical data item resulting
    from the superimposition of all receiving data items of a given statement
    aligned on their decimal points, must not contain more than 18 digits.
00001
Function
The NEXT GROUP clause specifies information for vertical positioning of a page
following the presentation of the last line of a report group.
General Format
              {integer-1     }
NEXT GROUP IS {PLUS integer-2}
              {NEXT PAGE     }
Syntax Rules
1.  A report group entry must not contain a NEXT GROUP clause unless the
    description of that report group contains at least one LINE NUMBER clause.
2.  Integer-1 and integer-2 must not exceed three significant digits in
    length.
3.  If the PAGE clause is omitted from the report description entry only a
    relative NEXT GROUP clause may be specified in any report group
    description entry within that report.
4.  The NEXT PAGE phrase of the NEXT GROUP clause must not be specified in a
    PAGE FOOTING report group.
5.  The NEXT GROUP clause must not be specified in a REPORT FOOTING report
    group or in a PAGE HEADING report group.
00001
Notation conventions are:
WORDS, LEVEL_NUMBERS, BRACKETS, BRACES, ELLIPSIS, PUNCTUATION,
SPECIAL_CHARACTERS, FORMATS, SYNTAX_RULES, and GENERAL_RULES.
For specific information, enter:
HELP (COBOL85) NOTATION_CONVENTIONS notation
For information on all the conventions, enter: ??.
  Notation     Description
  Words
               All underlined uppercase words are called keywords and are
               required when the functions of which they are a part are used.
               Uppercase words which are not underlined are optional and may
               be included in the source program at the discretion of the
               user.  Uppercase words, whether underlined or not, must be
               spelled correctly.
               In a general format, lowercase words are generic terms used to
               represent COBOL words, literals, PICTURE character-strings,
               comment-entries, or a complete syntactical entry that must be
               supplied by the user.  If such generic terms are repeated in a
               general format, a number or letter appendage to the term serves
               to identify that term in a subsequent explanation or
               discussion.
  Level-Numbers
               When specific level-numbers appear in data description entry
               formats, they are required when such entries are used in a
               COBOL program.  In this manual, the convention 01, 02, ..., 09
               is used to indicate level-numbers 1 through 9.
  Brackets and Braces
               When a portion of a general format is enclosed in brackets [ ],
               that portion may be included or omitted at the user's choice.
               When a portion of a general format is enclosed in braces { },
               one of the options contained within the braces must be
               selected.  In both cases, the possible choices are stacked
               vertically in the format.  Stacked choices are delimited by
               vertical bars (e.g., {| |} to indicate that more than one
               choice may be selected.  When brackets or braces enclose a
               portion of a format but only one possibility is shown, the
               function of the brackets or braces is to delimit that portion
               of the format to which a following ellipsis applies (see
               below).  If an option within braces contains only reserved
               words that are not keywords, then the option is a default
               option (implicitly selected unless one of the other options is
               explicitly indicated).
  Ellipsis
               The ellipsis (...) may show the omission of a portion of a
               source program.  The meaning becomes apparent in context.
               In the general formats, the ellipsis represents the position at
               which repetition may occur at the user's option.  The portion
               of the format that may be repeated is determined as follows.
               In a clause or statement format in which the ellipsis appears,
               scan from right to left to determine the ] or } delimiter
               immediately to the left of the ...; continue scanning from
               right to left and determine the logically matching [ or {
               delimiter; the ellipsis applies to the words between the
               determined pair of delimiters.
  Punctuation
               The punctuation characters comma and semicolon are shown in
               some formats.  Where shown, they are optional and may be
               included or omitted in the coding.  In the source program,
               these two punctuation characters are interchangeable and either
               one may be used when one is desired.
               A comma or semicolon may be used anywhere, as long as a space
               follows it.
               Paragraphs within the Identification Division and Procedure
               Division, and the entries within the Environment Division and
               Data Division, must be terminated by the separator period.
  Special Characters
               When the characters '+', '-', '<', '>', and '=' appear in
               formats, they are required when such formats are used, even
               though they are not underlined.
  Formats
               A general format is the specific arrangement of the elements of
               a clause or a statement.  A clause or a statement consists of
               elements which are the uppercase words, lowercase words,
               level-numbers, brackets, braces, connectives, and special
               characters depicted in the appropriate sections of this manual.
               In this manual, a format is shown adjacent to information which
               defines the clause or statement.  If more than one specific
               arrangement is permitted, the general format is separated into
               numbered formats.  Clauses must be written in the sequence
               given in the general formats.  (If used, clauses that are
               optional must appear in the sequence shown.) In certain cases,
               however, stated explicitly in the rules associated with a given
               format, clauses may appear in sequences other than those shown.
               Applications, requirements, or restrictions are shown as rules.
  Syntax Rules
               A syntax rule is a rule that defines or clarifies the order in
               which words or elements are arranged to form larger elements
               such as phrases, clauses, or statements.  Syntax rules also
               impose restrictions on individual words or elements.
               Syntax rules are used to define or clarify the exact manner in
               which the statement must be written (i.e., the order of the
               elements of the statement and the restrictions on what each
               element may represent).
  General Rules
               A general rule is a rule that defines or clarifies the meaning
               or relationship of meanings of an element or set of elements.
               It is used to define or clarify the semantics of the statement
               and the effect that it has on either compilation or execution.
00003
00003
00004
00007
00009
00002
00005
00006
00008
00001
The Nucleus provides a language capability for the internal processing of data
within the structure of the four divisions of a program.  See the following
related topics:
SOURCE_PROGRAM, END_PROGRAM_HEADER, PROGRAM_ID, AUTHOR,
INSTALLATION, DATE_WRITTEN, DATE_COMPILED, SECURITY,
CONFIGURATION_SECTION, SOURCE_COMPUTER,
OBJECT_COMPUTER, SPECIAL_NAMES, WORKING_STORAGE,
DATA_DESCRIPTION, BLANK_WHEN_ZERO, FILLER, JUSTIFIED,
LEVEL_NUMBER, OCCURS, PICTURE, REDEFINES, RENAMES, SIGN,
SYNCHRONIZED, USAGE, VALUE, ACCEPT, ADD, ALTER, COMPUTE,
CONTINUE, DISPLAY, DIVIDE, EVALUATE, EXIT, GO_TO, IF,
INITIALIZE, INSPECT, MOVE, MULTIPLY, PERFORM, SEARCH, SET,
STOP, STRING, SUBTRACT, and UNSTRING.
Function
The OBJECT-COMPUTER paragraph provides a means of describing the computer on
which the program is to be executed.
General Format
OBJECT-COMPUTER. [[HIS-SERIES-60] LEVEL-66-ASCII
  [                      {WORDS     }]
  [MEMORY SIZE integer-1 {CHARACTERS}]
  [                      {MODULES   }]
  [PROGRAM COLLATING SEQUENCE IS alphabet-name-1].]
General Rules
1.  The computer-name may provide a means for identifying equipment
    configuration, in which case the computer-name and its implied
    configuration are specified.  The configuration definition contains
    specific information concerning the memory size.
2.  All clauses of the OBJECT-COMPUTER paragraph apply to the program in which
    they are explicitly or implicitly specified and to any program contained
    within that program.
3.  When the OBJECT-COMPUTER paragraph is not specified and the program is not
    contained within a program including an OBJECT-COMPUTER paragraph, the
    object computer is assumed to be the same computer on which the program is
    compiled.
4.  When the OBJECT-COMPUTER paragraph is specified, but the
    object-computer-entry is not specified, the object computer is assumed to
    be the same computer on which the program is compiled.
5.  If the PROGRAM COLLATING SEQUENCE clause is specified, the program
    collating sequence is the collating sequence associated with
    alphabet-name-1 specified in that clause.
6.  If the PROGRAM COLLATING SEQUENCE clause is not specified, the program
    collating sequence is the native collating sequence.
7.  The program collating sequence established in the OBJECT-COMPUTER
    paragraph is used to determine the truth value of any nonnumeric
    comparisons that are:
    a.  Explicitly specified in relation conditions
    b.  Explicitly specified in condition-name conditions
    c.  Implicitly specified by the presence of a CONTROL clause in a report
        description entry
8.  The program collating sequence established in the OBJECT-COMPUTER
    paragraph is applied to any nonnumeric merge or sort keys unless the
    COLLATING SEQUENCE phrase is specified in the respective SORT or MERGE
    statement
00001
Function
The OBJECT-COMPUTER paragraph provides a means of describing the computer on
which the program is to be executed.
General Format
OBJECT-COMPUTER. [computer-name
    [                      {WORDS     }]
    [MEMORY SIZE integer-1 {CHARACTERS}]
    [                      {MODULES   }]
    [PROGRAM COLLATING SEQUENCE IS alphabet-name-1]
    [SEGMENT-LIMIT IS segment-number].]
Syntax Rule
1.  Computer-name is a system-name.
00001
Function
The OCCURS clause eliminates the need for separate entries for repeated data
items and supplies information required for the application of subscripts.
General Format
Format 1:
OCCURS integer-2 TIMES
  [{ASCENDING } KEY IS {data-name-2} ... ] ...
  [{DESCENDING}                          ]
  [INDEXED BY {index-name-1} ...]
Format 2:
OCCURS integer-1 TO integer-2 TIMES DEPENDING ON data-name-1
  [{ASCENDING } KEY IS {data-name-2} ... ] ...
  [{DESCENDING}                          ]
    [INDEXED BY {index-name-1} ...]
Syntax Rules
1.  The OCCURS clause must not be specified in a data description entry that:
    a.  Has a level-number of 01, 66, 77, or 88, or
    b.  Has a variable occurrence data item subordinate to it
2.  Data-name-1 and data-name-2 may be qualified.
3.  The first specification of data-name-2 must be the name of either the
    entry containing the OCCURS clause or an entry subordinate to the entry
    containing the OCCURS clause.  Subsequent specification of data-name-2
    must be subordinate to the entry containing the OCCURS clause.
4.  Data-name-2 must be specified without the subscripting normally required.
5.  Where both integer-1 and integer-2 are used, integer-1 must be greater
    than or equal to zero and integer-2 must be greater than integer-1.
6.  Data-name-1 must describe an integer.
7.  In format 2, the data item defined by data-name-1 must not occupy a
    character position within the range of the first character position
    defined by the data description entry containing the OCCURS clause and the
    last character position defined by the record description entry containing
    that OCCURS clause.
8.  If the OCCURS clause is specified in a data description entry included in
    a record description entry containing the EXTERNAL clause, data-name-1, if
    specified, must reference a data item possessing the external attribute
    which is described in the same Data Division.
9.  If the OCCURS clause is specified in a data description entry subordinate
    to one containing the GLOBAL clause, data-name-1, if specified, must be a
    global name and must reference a data item which is described in the same
    Data Division.
10. A data description entry that contains format 2 of the OCCURS clause may
    only be followed, within that record description, by data description
    entries which are subordinate to it.
11. The data item identified by data-name-2 must not contain an OCCURS clause
    except when data-name-2 is the subject of the entry.
12. There must be no entry that contains an OCCURS clause between the
    descriptions of the data items identified by the data-names in the KEY IS
    phrase and the subject of the entry.
13. An INDEXED BY phrase is required if the subject of this entry, or an entry
    subordinate to this entry, is to be referenced by indexing.  The
    index-name identified by this phrase is not defined elsewhere since its
    allocation and format are dependent on the hardware and, not being data,
    cannot be associated with any data hierarchy.
14. Index-name-1 must be a unique word within the program.
00001
OPEN_SEQUENTIAL
Function
The OPEN statement initiates the processing of files.
General Format
     {INPUT {file-name-1} ...  }
OPEN {OUTPUT {file-name-2} ... } ...
     {I-O {file-name-3} ...    }
     {EXTEND {file-name-4} ... }
Syntax Rules
1.  The EXTEND phrase must only be used for files in the sequential access
    mode.
2.  The files referenced in the OPEN statement need not all have the same
    organization or access.
00001
Function
The OPEN statement initiates the processing of files.
General Format
     {INPUT {file-name-1} ... }
OPEN {OUTPUT {file-name-2} ...} ...
     {I-O {file-name-3} ...   }
     {EXTEND {file-name-4} ...}
Syntax Rules
1.  The EXTEND phrase must only be used for files in the sequential access
    mode.
2.  The files referenced in the OPEN statement need not all have the same
    organization or access.
00001
Function
The OPEN statement initiates the processing of files.
General Format
     {INPUT {file-name-1} ... }
OPEN {OUTPUT {file-name-2} ...} ...
     {I-O {file-name-3} ...   }
     {EXTEND {file-name-4} ...}
Syntax Rules
1.  The EXTEND phrase must only be used for files in the sequential access
    mode.
2.  The files referenced in the OPEN statement need not all have the same
    organization or access.
00001
Function
The OPEN statement initiates the processing of report files.
General Format
OPEN {OUTPUT {file-name-1 [WITH NO REWIND]} ...} ...
     {EXTEND {file-name-2} ...                 }
Syntax Rule
1.  The OPEN statement for a report file must contain only the OUTPUT phrase
    or the EXTEND phrase.
00001
Function
The OPEN statement initiates the processing of files.
General Format
     {INPUT {file-name-1 [WITH NO REWIND]} ... }
OPEN {OUTPUT {file-name-2 [WITH NO REWIND]} ...} ...
     {I-O {file-name-3} ...                    }
     {EXTEND {file-name-4} ...                 }
Syntax Rules
1.  The EXTEND phrase must not be specified for a multiple file reel.
2.  The EXTEND phrase must be used only for files for which the LINAGE clause
    has not been specified.
3.  The files referenced in the OPEN statement need not all have the same
    organization or access.
00001
Function
The ORGANIZATION IS INDEXED clause specifies the indexed organization as the
logical structure of a file.
General Format
[ORGANIZATION IS] INDEXED
General Rules
1.  The ORGANIZATION IS INDEXED clause specifies indexed organization as the
    logical structure of a file.  The file organization is established at the
    time a file is created and cannot subsequently be changed.
2.  Indexed organization is a permanent logical file structure in which each
    record is identified by the value of one or more keys within that record.
00001
Function
The ORGANIZATION IS KEYED clause specifies keyed organization as the logical
structure of a file.
General Format
[ORGANIZATION IS] KEYED
General Rules
1.  The ORGANIZATION IS KEYED clause specifies keyed organization as the
    logical structure of a file.  The file organization is established at the
    time a file is created and cannot subsequently be changed.
2.  Keyed organization is a permanent logical file structure in which each
    record is uniquely identified by its record key.
00001
Function
The ORGANIZATION IS RELATIVE clause specifies relative organization as the
logical structure of a file.
General Format
[ORGANIZATION IS] RELATIVE
General Rules
1.  The ORGANIZATION IS RELATIVE clause specifies relative organization as the
    logical structure of a file.  The file organization is established at the
    time a file is created and cannot subsequently be changed.
2.  Relative organization is a permanent logical file structure in which each
    record is uniquely identified by an integer value greater than zero, which
    specifies the record's logical ordinal position in the file.
00001
Function
The ORGANIZATION IS SEQUENTIAL clause specifies sequential organization as the
logical structure of a file.
General Format
[ORGANIZATION IS] SEQUENTIAL
General Rules
1.  The ORGANIZATION IS SEQUENTIAL clause specifies sequential organization as
    the logical structure of a file.  The file organization is established at
    the time a file is created and cannot subsequently be changed.
2.  Sequential organization is a permanent logical file structure in which a
    record is identified by a predecessor-successor relationship established
    when the record is placed into the file.
3.  When the ORGANIZATION clause is not specified, sequential organization is
    implied.
00001
HELP_OVERVIEW
Function
The PADDING CHARACTER clause specifies the character to be used for block
padding on sequential files.
General Format
PADDING CHARACTER IS {data-name-1}
                     {literal-1  }
Syntax Rules
1.  Literal-1 must be a one-character nonnumeric literal.
2.  Data-name-1 may be qualified.
3.  Data-name-1 must be defined in the Data Division as a one-character data
    item of the category alphanumeric and must not be defined in the
    Communication Section, the File Section, or the Report Section.
00001
Function
The PAGE clause defines the length of a page and the vertical subdivisions
within which report groups are presented.
General Format
PAGE [LIMIT IS  ] integer-1 [LINE ] [HEADING integer-2]
     [LIMITS ARE]           [LINES]
  [FIRST DETAIL integer-3] [LAST DETAIL integer-4]
  [FOOTING integer-5]
Syntax Rules
1.  The HEADING, FIRST DETAIL, LAST DETAIL, and FOOTING phrases may be written
    in any order.
2.  Integer-1 must not exceed three significant digits in length.
3.  Integer-2 must be greater than or equal to 1.
4.  Integer-3 must be greater than or equal to integer-2.
5.  Integer-4 must be greater than or equal to integer-3.
6.  Integer-5 must be greater than or equal to integer-4.
7.  Integer-1 must be greater than or equal to integer-5.
8.  The following rules indicate the vertical subdivision of the page in which
    each type of report group may appear when the PAGE clause is specified.
    a.  A report heading report group that is to be presented on a page by
        itself, if defined, must be defined such that it can be presented in
        the vertical subdivision of the page that extends from the line number
        specified by integer-2 to the line number specified by integer-1,
        inclusive.
        A report heading report group that is not to be presented on a page by
        itself, if defined, must be defined such that it can be presented in
        the vertical subdivision of the page that extends from the line number
        specified by integer-2 to the line number specified by integer-3 minus
        1, inclusive.
    b.  A page heading report group, if defined, must be defined such that it
        can be presented in the vertical subdivision of the page that extends
        from the line number specified by integer-2 to the line number
        specified by integer-3 minus 1, inclusive.
    c.  A control heading or detail report group, if defined, must be defined
        such that it can be presented in the vertical subdivision of the page
        that extends from the line number specified by integer-3 to the line
        number specified by integer-4, inclusive.
    d.  A control footing report group, if defined, must be defined such that
        it can be presented in the vertical subdivision of the page that
        extends from the line number specified by integer-3 to the line number
        specified by integer-5, inclusive.
    e.  A page footing report group, if defined, must be defined such that it
        can be presented in the vertical subdivision of the page that extends
        from the line number specified by integer-5 plus 1 to the line number
        specified by integer-1, inclusive.
    f.  A report footing report group, if defined, must be defined such that
        it can be presented in the vertical subdivision of the page that
        extends from the line number specified by integer-2 to the line number
        specified by integer-1, inclusive.
        A report footing report group that is not to be presented on a page by
        itself, if defined, must be defined such that it can be presented in
        the vertical subdivision of the page that extends from the line number
        specified by integer-5 plus 1 to the line number specified by
        integer-1, inclusive.
9.  All report groups must be described such that they can be presented on one
    page.  The report writer control system (RWCS) never splits a multi-line
    report group across page boundaries.
00001
Function
The PERFORM statement is used to transfer control explicitly to one or more
procedures and to return control implicitly whenever execution of the
specified procedure is complete.  The PERFORM statement is also used to
control execution of one or more imperative statements which are within the
scope of that PERFORM statement.
General Format
Format 1:
PERFORM [procedure-name-1 [{THROUGH} procedure-name-2]]
        [                 [{THRU   }                 ]]
  [imperative-statement-1 END-PERFORM]
Format 2:
PERFORM [procedure-name-1 [{THROUGH} procedure-name-2]]
        [                 [{THRU   }                 ]]
  {identifier-1} TIMES [imperative-statement-1 END-PERFORM]
  {integer-1   }
Format 3:
PERFORM [procedure-name-1 [{THROUGH} procedure-name-2]]
        [                 [{THRU   }                 ]]
  [WITH TEST {BEFORE}] UNTIL condition-1
  [          {AFTER }]
  [imperative-statement-1 END-PERFORM]
Format 4:
PERFORM [procedure-name-1 [{THROUGH} procedure-name-2]]
        [                 [{THRU   }                 ]]
  [WITH TEST {BEFORE}]
  [          {AFTER }]
                              {identifier-3}
  VARYING {identifier-2} FROM {index-name-2}
          {index-name-1}      {literal-1   }
    BY {identifier-4} UNTIL condition-1
       {literal-2   }
  [                          {identifier-6}
  [AFTER {identifier-5} FROM {index-name-4}
  [      {index-name-3}      {literal-3   }
    BY {identifier-7} UNTIL condition-2     ] ...
       {literal-4   }                       ]
  [imperative-statement-1 END-PERFORM]
Syntax Rules
1.  If procedure-name-1 is omitted, imperative-statement-1 and the END-PERFORM
    phrase must be specified; if procedure-name-1 is specified,
    imperative-statement-1 and the END-PERFORM phrase must not be specified.
2.  In format 4, if procedure-name-1 is omitted, the AFTER phrase must not be
    specified.
3.  If neither the TEST BEFORE nor the TEST AFTER phrase is specified, the
    TEST BEFORE phrase is assumed.
4.  Each identifier represents a numeric elementary item described in the Data
    Division.  In format 2, identifier-1 must be described as a numeric
    integer.
5.  Each literal represents a numeric literal.
6.  The words THROUGH and THRU are equivalent.
7.  If an index-name is specified in the VARYING or AFTER phrase:
    a.  The identifier in the associated FROM and BY phrases must reference an
        integer data item.
    b.  The literal in the associated FROM phrase must be a positive integer.
    c.  The literal in the associated BY phrase must be a nonzero integer.
8.  If an index-name is specified in the FROM phrase:
    a.  The identifier in the associated VARYING or AFTER phrase must
        reference an integer data item.
    b.  The identifier in the associated BY phrase must reference an integer
        data item.
    c.  The literal in the associated BY phrase must be an integer.
9.  Literal in the BY phrase must not be zero.
10. Condition-1, condition-2, ... , may be any conditional expression.
11. Where procedure-name-1 and procedure-name-2 are both specified and either
    is the name of a procedure in the declaratives portion of the Procedure
    Division, both must be procedure-names in the same declarative section.
12. At least six AFTER phrases are permitted in format 4 of the PERFORM
    statement.
00001
Function
The PICTURE clause describes the general characteristics and editing
requirements of an elementary item.
General Format
{PICTURE} IS character-string
{PIC    }
Syntax Rules
1.  A PICTURE clause can be specified only at the elementary item level.
2.  A character-string consists of certain allowable combinations of
    characters in the COBOL character set used as symbols.  The allowable
    combinations determine the category of the elementary item.
3.  The lowercase letters corresponding to the uppercase letters representing
    the PICTURE symbols A, B, P, S, V, X, Z, CR and DB are equivalent to their
    uppercase representations in a PICTURE character-string.  All other
    lowercase letters are not equivalent to their corresponding uppercase
    representations.
4.  The maximum number of characters allowed in the character-string is 30.
5.  The PICTURE clause must be specified for every elementary item except an
    index data item or the subject of the RENAMES clause.  In these cases the
    use of this clause is prohibited.
6.  PIC is an abbreviation for PICTURE.
7.  The asterisk, when used as the zero suppression symbol, and the clause
    BLANK WHEN ZERO may not appear in the same entry.
00001
PROCEDURE_DIVISION
The Procedure Division may contain declarative and nondeclarative procedures.
A procedure is composed of a paragraph, or a group of successive paragraphs,
or a section, or a group of successive sections within the Procedure Division.
If one paragraph is in a section, all paragraphs must be in sections.  A
procedure-name is a word used to refer to a paragraph or section in the source
program in which it occurs.  It consists of a paragraph-name (which may be
qualified) or a section-name.
A section-name consists of a section header followed by zero, one, or more
successive paragraphs.  A section ends immediately before the next section or
at the end of the Procedure Division or, in the declaratives portion of the
Procedure Division, at the key words END DECLARATIVES.
A paragraph consists of a paragraph-name followed by a period and a space and
by zero, one, or more successive sentences.  A paragraph ends immediately
before the next paragraph-name or section-name or at the end of the Procedure
Division or, in the declaratives portion of the Procedure Division, at the key
words END DECLARATIVES.  A sentence consists of one or more statements and is
terminated by the separator period.
A statement is a syntactically valid combination of words, literals, and
separators beginning with a COBOL verb.
The term 'identifier' is defined as the word or words necessary to make unique
reference to a data item.      See the following related topics:
DECLARATIVES, EXECUTION, HEADER, BODY, PROCEDURE_DIV_INTER_PROGRAM,
PROCEDURE_DIV_REPORT_WRITER, and PROCEDURE_DIV_SEGMENTATION.
The body of the Procedure Division must conform to one of the formats that
follow.
Format 1:
[DECLARATIVES.
{section-name SECTION [segment-number].
    USE statement.
[paragraph-name. [sentence] ...] ...} ...
 END DECLARATIVES.]
{section-name SECTION [segment-number].
[paragraph-name. [sentence] ...] ...} ...
Format 2:
{paragraph-name. [sentence] ...} ...
The Procedure Division is identified by, and must begin with, the following
header:
PROCEDURE DIVISION [USING {data-name-1} ...].
    The Procedure Division is identified by, and must begin with, the
    following header:
    PROCEDURE DIVISION [USING {data-name-1} ...]
      [ENTRY section-name-1 [, section-name-2] ...].
    The USING phrase is necessary only if the object program is to be invoked
    by a CALL statement and that statement includes a USING phrase.
    The USING phrase of the Procedure Division header identifies the names
    used by the program for any parameters passed to it by a calling program.
    The parameters passed to a called program are identified in the USING
    phrase of the calling program's CALL statement.  The correspondence
    between the two lists of names is established on a positional basis.
    Data-name-1 must be defined as a level 01 entry or a level 77 entry in the
    Linkage Section.  A particular user-defined word may not appear more than
    once as data-name-1.  The data description entry for data-name-1 must not
    contain a REDEFINES clause.  Data-name-1 may, however, be the object of a
    REDEFINES clause elsewhere in the Linkage Section.
    The Procedure Division contains declarative procedures when the USE BEFORE
    REPORTING statement from the Report Writer module is present in a COBOL
    source program.  Shown below is the general format of the Procedure
    Division when the USE BEFORE REPORTING and/or USE AFTER STANDARD EXCEPTION
    PROCEDURE statements are present.
    PROCEDURE DIVISION.
    DECLARATIVES.
    {section-name SECTION.
      USE {AFTER STANDARD EXCEPTION PROCEDURE} statement.
          {BEFORE REPORTING                  }
    [paragraph-name.
      [sentence] ...] ...} ...
    END DECLARATIVES.
    {section-name SECTION.
    [paragraph-name.
      [sentence] ...] ...} ...
    The Procedure Division contains sections with segment-numbers when the
    Segmentation module is used in a COBOL source program.  Shown below is the
    general format of the Procedure Division when sections and segment-numbers
    are present.
    PROCEDURE DIVISION.
    [DECLARATIVES.
    {section-name SECTION [segment-number].
        USE statement.
    [paragraph-name.
        [sentence] ...] ...} ...
    END DECLARATIVES.]
    {section-name SECTION [segment-number].
    [paragraph-name.
        [sentence] ...] ...} ...
COBOL is a programming language used throughout the world for programming
business data processing applications.  The COBOL language was developed by a
group of computer users and manufacturers; the first documentation was
distributed in April 1960.  It has since undergone many changes and extensions
resulting from manufacturers' experiences with COBOL implementation and users'
experiences with COBOL programming on computers of varying sizes and
configurations.  The best of these improvements are embodied in this version
of the language termed COBOL-85.
As a programming language, COBOL provides reasonably swift programming
implementation, reduces program conversion costs, reduces programmer training
time, and guarantees a measure of standard documentation.
COBOL allows the user to instruct the computer in a language similar to
English.  The user writes English-like sentences and paragraphs, following the
conventions of a standard reference format, to describe the data to be
processed and to specify the required procedures.  The English-like language
program is called a COBOL 'source program'.
A source program is usually entered as an EDIT file.  Each line of data
occupies one EDIT record.  The file is submitted as input to the computer
under the control of a special program known as a compiler.  As output, the
compiler produces an object unit on disk storage.  The object program is the
actual sequence of machine instructions required to accomplish the functions
specified in the source program.  In addition, the compiler produces an edited
listing, which includes a printout of the source program in the reference
format.  Another important function of the compiler is to analyze the source
program for correct COBOL syntax, and to print error comments for any syntax
errors that are detected.  The computer's operation under control of the
compiler is called compilation.  For an overview of the HELP (COBOL85)
facility, enter HELP (COBOL85) HELP
PROGRAM_ID_PARAGRAPH
Function
The PROGRAM-ID paragraph specifies the name by which a program is identified
and assigns selected program attributes to that program.
General Format
PROGRAM-ID. program-name [IS {|COMMON |} PROGRAM].
                         [   {|INITIAL|}        ]
Syntax Rules
1.  The program-name must conform to the rules for formation of a user-defined
    word.
2.  A program contained within another program must not be assigned the same
    name as that of any other program contained within the separately compiled
    program which contains this program.
3.  The optional COMMON clause may be used only if the program is contained
    within another program.
00001
Function
The PROGRAM-ID paragraph specifies the name by which a program is identified.
General Format
PROGRAM-ID. program-name.
Syntax Rule
1.  The program-name must conform to the rules for formation of a user-defined
    word.
General Rule
1.  The program-name identifies the source program, the object program, and
    all listings pertaining to a particular program.
00002
00001
RD_REPORT_WRITER
Function
Within the Inter-Program Communication module, the report description entry in
the Report Section determines whether a report-name is a local name or a
global name.
General Format
RD report-name-1
  [IS GLOBAL]
  [CODE literal-1]
  [{CONTROL IS  } {data-name-1} ...       }]
  [{CONTROLS ARE} {FINAL [data-name-1] ...}]
  [PAGE [LIMIT IS  ] integer-1 [LINE ] [HEADING integer-2]
  [     [LIMITS ARE]           [LINES]
     [FIRST DETAIL integer-3] [LAST DETAIL integer-4]
     [FOOTING integer-5]] .
General Rules
1.  If the report description entry contains the GLOBAL clause, the special
    registers LINE-COUNTER and PAGE-COUNTER are global names.
Function
The report description entry names a report, specifies any identifying
characters to be prefixed to each print line in the report, and describes the
physical structure and organization of that report.
General Format
RD report-name-1
  [CODE literal-1]
  [{CONTROL IS  } {{data-name-1} ...      }]
  [{CONTROLS ARE} {FINAL [data-name-1] ...}]
  [PAGE [LIMIT IS  ] integer-1 [LINE ] [HEADING integer-2]
  [     [LIMITS ARE]           [LINES]
    [FIRST DETAIL integer-3 [LAST DETAIL integer-4]
    [FOOTING integer-5]] .
Syntax Rules
1.  Report-name-1 must appear in one and only one REPORT clause.
2.  The clauses following report-name-1 may appear in any order.
3.  Report-name-1 is the highest permissible qualifier that may be specified
    for LINE-COUNTER, PAGE-COUNTER, and all data-names defined within the
    Report Section.
00001
READ_SEQUENTIAL
Function
For sequential access, the READ statement makes available the next logical
record from a file.  For random access, the READ statement makes available a
specified record from a mass storage file.
General Format
Format 1:
READ file-name-1 [NEXT] RECORD [INTO identifier-1]
  [AT END imperative-statement-1]
  [NOT AT END imperative-statement-2]
  [END-READ]
Format 2:
READ file-name-1 RECORD [INTO identifier-1]
  [KEY IS data-name-1]
  [INVALID KEY imperative-statement-3]
  [NOT INVALID KEY imperative-statement-4]
  [END-READ]
Syntax Rules
1.  The storage area associated with identifier-1 and the record area
    associated with file-name-1 must not be the same storage area.
2.  Data-name-1 must be the name of a data item specified as a record key
    associated with file-name-1.
3.  Data-name-1 may be qualified.
4.  Format 1 must be used for all files in sequential access mode.
5.  The NEXT phrase must be specified for files in dynamic access mode, when
    records are to be retrieved sequentially.
6.  Format 2 is used for files in random access mode or for files in dynamic
    access mode when records are to be retrieved randomly.
7.  The INVALID KEY phrase or the AT END phrase must be specified if no
    applicable USE AFTER STANDARD EXCEPTION procedure is specified for
    file-name-1.
00001
Function
For sequential access, the READ statement makes available the next logical
record from a file.  For random access, the READ statement makes available a
specified record from a mass storage file.
General Format
Format 1:
READ file-name-1 [NEXT] RECORD [INTO identifier-1]
  [AT END imperative-statement-1]
  [NOT AT END imperative-statement-2]
  [END-READ]
Format 2:
READ file-name-1 RECORD [INTO identifier-1]
  [INVALID KEY imperative-statement-3]
  [NOT INVALID KEY imperative-statement-4]
  [END-READ]
Syntax Rules
1.  The storage area associated with identifier-1 and the record area
    associated with file-name-1 must not be the same storage area.
2.  Format 1 must be used for all files in sequential access mode.
3.  The NEXT phrase must be specified for files in dynamic access mode when
    records are to be retrieved sequentially.
4.  Format 2 is used for files in random access mode or for files in dynamic
    access mode when records are to be retrieved randomly.
5.  The INVALID KEY phrase or the AT END phrase must be specified if no
    applicable USE AFTER STANDARD EXCEPTION procedure is specified for
    file-name-1.
00001
Function
For sequential access, the READ statement makes available the next logical
record from a file.  For random access, the READ statement makes available a
specified record from a mass storage file.
General Format
Format 1:
READ file-name-1 [NEXT] RECORD [INTO identifier-1]
  [AT END imperative-statement-1]
  [NOT AT END imperative-statement-2]
  [END-READ]
Format 2:
READ file-name-1 RECORD [INTO identifier-1]
  [INVALID KEY imperative-statement-3]
  [NOT INVALID KEY imperative-statement-4]
  [END-READ]
Syntax Rules
1.  The storage area associated with identifier-1 and the record area
    associated with file-name-1 must not be the same storage area.
2.  Format 1 must be used for all files in sequential access mode.
3.  The NEXT phrase must be specified for files in dynamic access mode when
    records are to be retrieved sequentially.
4.  Format 2 is used for files in random access mode or for files in dynamic
    access mode when records are to be retrieved randomly.
5.  The INVALID KEY phrase or the AT END phrase must be specified if no
    applicable USE AFTER STANDARD EXCEPTION procedure is specified for
    file-name-1.
00001
Function
The READ statement makes available the next logical record from a file.
General Format
READ file-name-1 NEXT RECORD [INTO identifier-1]
  [AT END imperative-statement-1]
  [NOT AT END imperative-statement-2]
  [END-READ]
Syntax Rules
1.  The storage area associated with identifier-1 and the record area
    associated with file-name-1 must not be the same storage area.
2.  The AT END phrase must be specified if no applicable USE AFTER STANDARD
    EXCEPTION procedure is specified for file-name-1.
00001
Function
The RECORD clause specifies the number of character positions in a fixed
length record, or the range of character positions in a variable length
record.  If the number of character positions does vary, the clause specifies
the minimum and maximum number of character positions.
General Format
Format 1:
RECORD CONTAINS integer-1 CHARACTERS
Format 2:
RECORD IS VARYING IN SIZE [[FROM integer-2] [TO integer-3] CHARACTERS]
  [DEPENDING ON data-name-1]
Format 3:
RECORD CONTAINS integer-4 TO integer-5 CHARACTERS
Syntax Rules
FORMAT 1:
1.  No record description entry for the file may specify a number of character
    positions greater than integer-1.
FORMAT 2:
2.  Record descriptions for the file must not describe records which contain a
    lesser number of character positions than that specified by integer-2 nor
    records which contain a greater number of character positions than that
    specified by integer-3.
3.  Integer-3 must be greater than integer-2.
4.  Data-name-1 must describe an elementary unsigned integer in the
    Working-Storage or Linkage Section.
00001
Function
The RECORD DELIMITER clause indicates the method of determining the length of
a variable length record on the external medium.
General Format
RECORD DELIMITER IS {STANDARD-1}
Syntax Rules
1.  The RECORD DELIMITER clause may be specified only for variable length
    records.
2.  If the STANDARD-1 phrase is specified, the external medium must be a
    magnetic tape file.
00001
Function
The RECORD KEY clause specifies the prime record key access path to the
records in an indexed file.
General Format
RECORD KEY IS data-name-1
Syntax Rules
1.  Data-name-1 may be qualified.
2.  Data-name-1 must reference a data item of the category alphanumeric within
    a record description entry associated with the file-name to which the
    RECORD KEY clause is subordinate.
3.  Data-name-1 must not reference a group item that contains a variable
    occurrence data item.
4.  If the indexed file contains variable length records, the prime record key
    must be contained within the first x character positions of the record,
    where x equals the minimum record size specified for the file.
00001
Function
The REDEFINES clause allows the same computer storage area to be described by
different data description entries.
General Format
level-number [data-name-1] REDEFINES data-name-2
             [FILLER     ]
NOTE:  Level-number, data-name-1, and FILLER are shown in the above
       format to improve clarity.  Level-number, data-name-1, and
       FILLER are not part of the REDEFINES clause.
Syntax Rules
1.  The REDEFINES clause, when specified, must immediately follow the subject
    of the entry.
2.  The level-numbers of data-name-2 and the subject of the entry must be
    identical, but must not be 66 or 88.
3.  This clause must not be used in level 01 entries in the File Section.
4.  The data description entry for data-name-2 cannot contain an OCCURS
    clause.  However, data-name-2 may be subordinate to an item whose data
    description entry contains an OCCURS clause.  In this case, the reference
    to data-name-2 in the REDEFINES clause may not be subscripted.  Neither
    the original definition nor the redefinition can include a variable
    occurrence data item.
5.  If the data item referenced by data-name-2 is either declared to be an
    external data record or is specified with a level-number other than 01,
    the number of character positions it contains must be greater than or
    equal to the number of character positions in the data item referenced by
    the subject of this entry.  If the data-name referenced by data-name-2 is
    specified with a level-number of 01 and is not declared to be an external
    data record, there is no such constraint.
6.  Data-name-2 must not be qualified even if it is not unique since no
    ambiguity of reference exists in this case because of the required
    placement of the REDEFINES clause within the source program.
7.  Multiple redefinitions of the same character positions are permitted but
    must all use the data-name of the entry that originally defined the area.
8.  The entries giving the new description of the character positions must not
    contain any VALUE clauses, except in condition-name entries.
9.  No entry having a level-number numerically lower than the level-number of
    data-name-2 and the subject of the entry may occur between the data
    description entries of data-name-2 and the subject of the entry.
10. The entries giving the new descriptions of the character positions must
    follow the entries defining the area of data-name-2, without intervening
    entries that define new character positions.
11. In level 1, data-name-2 cannot be subordinate to an entry which contains a
    REDEFINES clause.  In level 2, data-name-2 may be subordinate to an entry
    which contains a REDEFINES clause.
00001
    Relative I-O provides a capability to access records of a mass storage
    file in either a random or sequential manner.  Each record in a relative
    file is uniquely identified by an integer value greater than zero which
    specifies the record's logical ordinal position in the file.
    A file with relative organization is a mass storage file from which any
    record may be stored or retrieved by providing the value of its relative
    record number.
    See the following related topics:
    INPUT_OUTPUT, FILE_CONTROL, SELECT_RELATIVE,
    ACCESS_MODE_RELATIVE, ORGANIZATION_IS_RELATIVE, IO_CONTROL,
    FILE_SECTION, FD_RELATIVE, CLOSE_RELATIVE, DELETE,
    OPEN_RELATIVE, READ_RELATIVE, REWRITE_RELATIVE, START,
    USE and WRITE_RELATIVE.
Function
The RELEASE statement transfers records to the initial phase of a sort
operation.
General Format
RELEASE record-name-1 [FROM identifier-1]
Syntax Rules
1.  Record-name-1 must be the name of a logical record in a sort-merge file
    description entry and it may be qualified.
2.  A RELEASE statement may be used only within the range of an input
    procedure associated with a SORT statement for the file-name whose
    sort-merge file description entry contains record-name-1.
3.  Record-name-1 and identifier-1 must not refer to the same storage area.
00001
Function
The RENAMES clause permits alternative, possibly overlapping, groupings of
elementary items.
General Format
66 data-name-1 RENAMES data-name-2 [{THROUGH} data-name-3] .
                                   [{THRU   }            ]
NOTE:  Level-number 66 and data-name-1 are shown in the above
       format to improve clarity.  Level-number and data-name-1
       are not part of the RENAMES clause.
Syntax Rules
1.  Any number of RENAMES entries may be written for a logical record.
2.  All RENAMES entries referring to data items within a given logical record
    must immediately follow the last data description entry of the associated
    record description entry.
3.  Data-name-1 cannot be used as a qualifier, and can only be qualified by
    the names of the associated level 01, FD, or SD entries.  Neither
    data-name-2 nor data-name-3 may have an OCCURS clause in its data
    description entry nor be subordinate to an item that has an OCCURS clause
    in its data description entry.
4.  Data-name-2 and data-name-3 must be names of elementary items or groups of
    elementary items in the same logical record, and cannot be the same
    data-name.  A 66 level entry cannot rename another 66 level entry nor can
    it rename a 77, 88, or 01 level entry.
5.  Data-name-2 and data-name-3 may be qualified.
6.  None of the items within the range, including data-name-2 and data-name-3,
    if specified, can be variable occurrence data items.
7.  The words THROUGH and THRU are equivalent.
8.  The beginning of the area described by data-name-3 must not be to the left
    of the beginning of the area described by data-name-2.  The end of the
    area described by data-name-3 must be to the right of the end of the area
    described by data-name-2.  Data-name-3, therefore, cannot be subordinate
    to data-name-2.
00001
Function
The REPLACE statement is used to replace source program text.
General Format
Format 1:
        {{==pseudo-text-1==}    {==pseudo-text-2}}
REPLACE {{identifier-1     } BY {identifier-2   }} ...
        {{literal-1        }    {literal-2      }}
        {{word-1           }    {word-2         }}
Format 2:
REPLACE OFF
Syntax Rules
1.  A REPLACE statement may occur anywhere in the source program where a
    character-string may occur.  It must be preceded by a separator period
    except when it is the first statement in a separately compiled program.
2.  A REPLACE statement must be terminated by a separator period.
3.  Pseudo-text-1 must contain one or more text words.
4.  Pseudo-text-2 may contain zero, one, or more text words.
5.  Character-strings within pseudo-text-1 and pseudo-text-2 may be continued.
6.  A length from 1 through 322 characters is allowed for a text word within
    pseudo-text.
7.  Pseudo-text-1 must not consist entirely of a separator comma or a
    separator semicolon.
8.  If the word REPLACE appears in a comment-entry or in the place where a
    comment-entry may appear, it is considered part of the comment-entry.
9.  Word-1 or word-2 may be any single COBOL word except 'COPY' or 'BY'.
00001
Function
The REPORT clause specifies the names of reports that constitute a report
file.
General Format
{REPORT IS  } {report-name-1} ...
{REPORTS ARE}
Syntax Rules
1.  Each report-name specified in a REPORT clause must be the subject of a
    report description entry in the Report Section of the same program.  The
    report-names may appear in any order.
2.  A report-name must appear in only one REPORT clause.
3.  The subject of a file description entry that specifies a REPORT clause may
    be referenced in the Procedure Division only by the USE statement, the
    CLOSE statement, or the OPEN statement with the OUTPUT or EXTEND phrase.
00001
Function
The report group description entry specifies the characteristics of a report
group and of the individual items within a report group.
General Format
Format 1:
01 [data-name-1]
   [LINE NUMBER IS {integer-1 [ON NEXT PAGE]}]
   [               {PLUS INTEGER-2          }]
   [              {integer-3     }]
   [NEXT GROUP IS {PLUS integer-4}]
   [              {NEXT PAGE     }]
           {{REPORT HEADING}               }
           {{RH            }               }
           {                               }
           {{PAGE HEADING}                 }
           {{PH          }                 }
           {                               }
           {{CONTROL HEADING} {data-name-2}}
           {{CH             } {FINAL      }}
           {                               }
   TYPE IS {{DETAIL}                       }
           {{DE    }                       }
           {
           {{CONTROL FOOTING} {data-name-3}}
           {{CF             } {FINAL      }}
           {                               }
           {{PAGE FOOTING}                 }
           {{PF          }                 }
           {                               }
           {{REPORT FOOTING}               }
           {{RF            }               }
  [[USAGE IS] DISPLAY].
Format 2:
level-number [data-name-1]
  [LINE NUMBER IS {integer-1 [ON NEXT PAGE]}}
  [               {PLUS integer-2          }]
  [[USAGE IS] DISPLAY].
Format 3:
level-number [data-name-1]
  {PICTURE} IS character-string
  {PIC    }
  [[USAGE IS] DISPLAY]
  [[SIGN IS] {LEADING } SEPARATE CHARACTER]
  [          {TRAILING}                   ]
  [{JUSTIFIED} RIGHT]
  [{JUST     }      ]
  [BLANK WHEN ZERO]
  [LINE NUMBER IS {integer-1 [ON NEXT PAGE]}]
  [               {PLUS integer-2          }]
  [COLUMN NUMBER IS integer-3]
  {SOURCE IS identifier-1                               }
  {                                                     }
  {VALUE IS literal-1                                   }
  {                                                     }
  {{SUM {identifier-2} ... [UPON {data-name-2} ...]} ...}
  {                                                     }
  {   [RESET ON {data-name-3}]                          }
  {   [         {FINAL      }]                          }
  [GROUP INDICATE].
Syntax Rules
1.  The report group description entry can appear only in the Report Section.
2.  Except for the data-name clause, which when present must immediately
    follow the level-number, the clauses may be written in any sequence.
3.  In format 2 the level-number may be an integer from 02 to 48 inclusive.
    In format 3 the level-number may be any integer from 02 to 49.
4.  A description of a report group may consist of one, two, or three
    hierarchic levels:
    a.  The first entry that describes a report group must be a format 1
        entry.
    b.  Both format 2 and format 3 entries may be immediately subordinate to a
        format 1 entry.
    c.  At least one format 3 entry must be immediately subordinate to a
        format 2 entry.
    d.  Format 3 entries must define elementary data items.
5.  In a format 1 entry, data-name-1 is required only when:
    a.  A detail report group is referenced by a GENERATE statement.
    b.  A detail report group is referenced by the UPON phrase of a SUM
        clause.
    c.  A report group is referenced in a USE BEFORE REPORTING sentence.
    d.  The name of a control footing report group is used to qualify a
        reference to a sum counter.
    If specified, data-name-1 may be referenced only by a GENERATE statement,
    the UPON phrase of a SUM clause, a USE BEFORE REPORTING sentence, or as a
    sum counter qualifier.
6.  A format 2 entry must contain at least one optional clause.
7.  In a format 2 entry, data-name-1 is optional.  If present it may be used
    only to qualify a sum counter reference.
8.  In the Report Section, the USAGE clause is used only to declare the usage
    of printable items.
    a.  If the USAGE clause appears in a format 3 entry, that entry must
        define a printable item.
    b.  If the USAGE clause appears in a format 1 or format 2 entry, at least
        one subordinate entry must define a printable item.
9.  An entry that contains a LINE NUMBER clause must not have a subordinate
    entry that also contains a LINE NUMBER clause.
10. In format 3:
    a.  A GROUP INDICATE clause may appear only in a type detail report group.
    b.  A SUM clause may appear only in a type control footing report group.
    c.  An entry that contains a COLUMN NUMBER clause but no LINE NUMBER
        clause must be subordinate to an entry that contains a LINE NUMBER
        clause.
    d.  Data-name-1 is optional but may be specified in any entry.
        Data-name-1 may be referenced only if the entry defines a sum counter.
    e.  An entry that contains a VALUE clause must also have a COLUMN NUMBER
        clause.
00001
    The Report Section is located in the Data Division of a source program.
    The Report Section describes the reports to be written onto report files.
    The description of each report must begin with a report description entry
    (RD entry) and be followed by one or more report group description
    entries.
General Format
REPORT SECTION.
[report-description-entry {report-group-description-entry} ...] ...
    The Report Writer provides a facility for producing reports by specifying
    the physical appearance of a report rather than requiring specification of
    the detailed procedure necessary to produce that report.
    A hierarchy of levels is used in defining the logical organization of a
    report.  Each report is divided into report groups, which in turn are
    divided into sequences of items.  Such a hierarchical structure permits
    explicit reference to a report group with implicit reference to other
    levels in the hierarchy.  A report group contains one or more items to be
    presented on zero, one, or more lines.    See the following topics:
    SELECT_REPORT_WRITER, IO_CONTROL_REPORT_WRITER,
    FILE_SECTION_REPORT_WRITER, REPORT, REPORT_SECTION,
    REPORT_GROUP_DESCRIPTION_ENTRY, RD_REPORT_WRITER, CODE,
    CONTROL, PAGE, REPORT_GROUP_DESCRIPTION, COLUMN_NUMBER,
    DATA_NAME_REPORT_WRITER, GROUP_INDICATE,
    LEVEL_NUMBER_REPORT_WRITER, LINE_NUMBER, NEXT_GROUP,
    SIGN_REPORT_WRITER, TYPE, USAGE_REPORT_WRITER,
    VALUE_REPORT_WRITER, PROCEDURE_DIV_REPORT_WRITER,
    CLOSE_REPORT_WRITER, GENERATE, INITIATE, OPEN_REPORT_WRITER,
    SUPPRESS, TERMINATE, USE_REPORT_WRITER USAGE_REPORT_WRITER
    USE_BEFORE_REPORTING_REPORT_W.
RESERVE_CLAUSE
Reserved words are terms that may be used in COBOL source program but must not
appear in the programs as user-defined words.  They may only be used as
indicated in the general formats.  The seven types of reserved words are:
1.  Keywords - A word(s) whose presence is required when the format in which
    the word(s) appears is used in a source program
2.  Optional Words - Within each format, uppercase words that are not
    underlined and may be specified at the discretion of the user
3.  Connectives - Qualifier connectives (OF, IN); series connectives
    (separator comma or separator semicolon); and logical connectives (AND,
    OR)
4.  Special Registers - Certain reserved words used to name and reference
    special registers (are used to store data produced in conjunction with
    specific COBOL features)
5.  Figurative Constants - Certain reserved words used to name and reference
    specific constant values
6.  Special-Character Words - Arithmetic operators and relation characters
7.  System-Names - Names that refer to specific features of the
    hardware/software environment
For a complete list of reserved words, enter ??
ACCEPT                    C10
ACCESS                    CHANNEL-11                DATA
ACTUAL                    C11                       DATE
ADD                       CHANNEL-12                DATE-COMPILED
ADDITIONAL                C12                       DATE-WRITTEN
ADVANCING                 CHANNEL-13                DAY
AFTER                     C13                       DAY-OF-WEEK
AGGREGATE                 CHANNEL-14                DB
ALL                       C14                       DB-EXCEPTION
ALPHABET                  CHANNEL-15                DB-KEY
ALPHABETIC                C15                       DE
ALPHABETIC-LOWER          CHARACTER                 DEBUGGING
ALPHABETIC-UPPER          CHARACTERS                DECIMAL-POINT
ALPHANUMERIC              CHECKPOINT-FILE           DECLARATIVES
ALPHANUMERIC-EDITED       CLASS                     DEFAULT
ALSO                      CLOCK-UNITS               DELETE
ALTER                     CLOSE                     DELIMITED
ALTERNATE                 COBOL                     DELIMITER
AND                       CODE                      DENSITY
ANSI                      CODE-SET                  DEPENDING
ANY                       COLLATING                 DESCENDING
APPLY                     COLUMN                    DESCRIPTORS
ARE                       COMMA                     DESTINATION
AREA                      COMMON                    DETACH
AREAS                     COMMUNICATION             DETAIL
ASCENDING                 COMP                      DEVICE
ASCII                     COMPUTATIONAL             DISABLE
ASSIGN                    COMP-1                    DISCONNECT
AT                        COMPUTATIONAL-1           DISPLAY
ATTACH-OPTIONS            COMP-2                    DISPLAY-1
AUTHOR                    COMPUTATIONAL-2           DISPLAY-2
                          COMP-3                    DIVIDE
BEFORE                    COMPUTATIONAL-3           DIVISION
BEGINNING                 COMP-4                    DOWN
BINARY                    COMPUTATIONAL-4           DSP-8
BIT                       COMP-5                    DUPLICATE
BITS                      COMPUTATIONAL-5           DUPLICATES
BLANK                     COMP-6                    DYNAMIC
BLOCK                     COMPUTATIONAL-6
BLOCK-COUNT               COMP-7                    EBCDIC
BOTTOM                    COMPUTATIONAL-7           EGI
BSN                       COMP-8                    ELSE
BY                        COMPUTATIONAL-8           EMI
                          COMP-11                   EMPTY
C-6000                    COMPUTATIONAL-11          ENABLE
CALL                      COMP-12                   END
CANCEL                    COMPUTATIONAL-12          END-ADD
CATALOG-NAME              COMP-13                   END-CALL
CATALOG-NAMES             COMPUTATIONAL-13          END-COMPUTE
CD                        COMP-14                   END-DELETE
CF                        COMPUTATIONAL-14          END-DIVIDE
CH                        COMPUTE                   END-EVALUATE
CHANNEL-01                CONFIGURATION             END-IF
C01                       CONNECT                   END-MULTIPLY
CHANNEL-02                CONSOLE                   END-OF-FILE
C02                       CONSTANT                  END-OF-PAGE
CHANNEL-03                CONTAINS                  END-OF-TAPE
C03                       CONTENT                   END-PERFORM
CHANNEL-04                CONTINUE                  END-READ
C04                       CONTROL                   END-RECEIVE
CHANNEL-05                CONTROLS                  END-RETURN
C05                       CONVERSION                END-REWRITE
CHANNEL-06                CONVERTING                END-SEARCH
C06                       COPY                      END-START
CHANNEL-07                CORR                      END-STRING
C07                       CORRESPONDING             END-SUBTRACT
CHANNEL-08                COUNT                     END-UNSTRING
C08                       CP-6                      END-WRITE
CHANNEL-09                CSP                       ENDING
C09                       CURRENCY                  ENTER
CHANNEL-10                CURRENT                   ENTRY
ENVIRONMENT               LEVEL-68                  REALM
EOP                       LEVEL-68-ASCII            REALM-NAME
EQUAL                     LIMIT                     REALMS
EQUALS                    LIMITS                    RECEIVE
ERASE                     LINAGE                    RECORD
ERROR                     LINAGE-COUNTER            RECORD-NAME
ESI                       LINE                      RECORDS
EVALUATE                  LINE-COUNTER              REDEFINES
EVERY                     LINES                     REEL
EXAMINE                   LINKAGE                   REEL-NUMBER
EXCEEDS                   LOAD                      REEL-SERIAL-NUMBER
EXCEPTION                 LOCALLY                   REFERENCE
EXIT                      LOCK                      REFERENCES
EXTEND                    LOW-VALUE                 RELATIVE
EXTERNAL                  LOW-VALUES                RELEASE
                                                    REMAINDER
FALSE                     MAXIMUM                   REMOVAL
FD                        MEMBER                    RENAMES
FILE                      MEMBERS                   REPLACEMENT
FILE-CONTROL              MEMBERSHIP                REPLACING
FILE-ID                   MEMORY                    REPORT
FILE-SERIAL-NUMBER        MERGE                     REPORTING
FILLER                    MESSAGE                   REPORTS
FINAL                     MODE                      RERUN
FIND                      MODIFICATION              RESERVE
FINISH                    MODIFY                    RESET
FIRST                     MODULES                   RETAIN
FLR                       MOVE                      RETAINING
FOOTING                   MULTICS                   RETENTION
FOR                       MULTIPLE                  RETENTION-PERIOD
FORCE                     MULTIPLY                  RETRIEVAL
FROM                                                RETURN
GBCD                      NATIVE                    REVERSED
GCOS                      NEGATIVE                  REWIND
GENERATE                  NEXT                      REWRITE
GENERATION                NO                        RF
GET                       NOMINAL                   RH
GFRC                      NOT                       RIGHT
GIVING                    NULL                      ROLLBACK
GLOBAL                    NUMBER                    ROUNDED
GO                        NUMERIC                   RUN
GREATER                   NUMERIC-EDITED
GROUP                                               SAME
                          OBJECT                    SCALAR
H-2000                    OBJECT-COMPUTER           SD
H-2400                    OCCURS                    SEARCH
HBCD                      OF                        SECTION
HEADING                   OFF                       SECURITY
HIGH-VALUE                OMITTED                   SEGMENT
HIGH-VALUES               ON                        SEGMENT-LIMIT
HIS-SERIES-60             ONLY                      SELECT
                          OPEN                      SEND
I-O                       OPERATIONAL               SENTENCE
I-O-CONTROL               OPTIONAL                  SEPARATE
IBM-DOS                   OR                        SEQUENCE
IBM-OS                    ORDER                     SEQUENTIAL
IDENTIFICATION            ORGANIZATION              SET
IDS-II                    OTHER                     SETS
IF                        OTHERWISE                 SIGN
IN                        OUTPUT                    SIZE
INCLUDING                 OUTPUT-MODE               SORT
INDEX                     OVERFLOW                  SORT-MERGE
INDEXED                   OWNER                     SOURCE
INDICATE                                            SOURCE-COMPUTER
INITIAL                   PACKED-DECIMAL            SPACE
INITIALIZE                PADDING                   SPACES
INITIATE                  PAGE                      SPANNED
INPUT                     PAGE-COUNTER              SPECIAL-NAMES
INPUT-OUTPUT              PERFORM                   SSF
INSPECT                   PERMANENT                 STANDARD
INSTALLATION              PF                        STANDARD-1
INTERCHANGE               PH                        STANDARD-2
INTO                      PIC                       START
INVALID                   PICTURE                   STATUS
IS                        PLUS                      STOP
ISP                       POINTER                   STORE
                          POSITION                  STREAM
JIS                       POSITIONING               STRING
JUST                      POSITIVE                  SUB-QUEUE-1
JUSTIFIED                 PRINTING                  SUB-QUEUE-2
                          PRIOR                     SUB-QUEUE-3
KEY                       PRIVACY                   SUB-SCHEMA
KEYED                     PROCEDURE                 SUBSTITUTION
                          PROCEDURES                SUBTRACT
LABEL                     PROCEED                   SUM
LABEL-DAY                 PROCESS-AREA              SUPPRESS
LABEL-IDENTIFIER          PROGRAM                   SWITCH-0
LABEL-YEAR                PROGRAM-ID                SWITCH-1
LAST                      PROTECT                   SWITCH-10
LEADING                   PURGE                     SWITCH-11
LEFT                                                SWITCH-12
LENGTH                    QUEUE                     SWITCH-13
LESS                      QUOTE                     SWITCH-14
LEVEL-6                   QUOTES                    SWITCH-15
LEVEL-62                                            SWITCH-16
LEVEL-64                  RANDOM                    SWITCH-17
LEVEL-66                  RD                        SWITCH-18
LEVEL-66-ASCII            READ                      SWITCH-19
LEVEL-66-EBCDIC           READY                     SWITCH-2
SWITCH-20                 TAPE                      USE
SWITCH-21                 TAPE-OPTIONS              USER
SWITCH-22                 TEMPORARY                 USING
SWITCH-23                 TENANT
SWITCH-24                 TERMINAL                  VALUE
SWITCH-25                 TERMINATE                 VALUES
SWITCH-26                 TEST                      VARYING
SWITCH-27                 TEXT                      VFC
SWITCH-28                 THAN                      VLR
SWITCH-29                 THEN
SWITCH-3                  THROUGH                   WHEN
SWITCH-30                 THRU                      WITH
SWITCH-31                 TIME                      WITHIN
SWITCH-32                 TIMES                     WORDS
SWITCH-33                 TO                        WORKING-STORAGE
SWITCH-34                 TOP                       WRITE
SWITCH-35                 TRAILING
SWITCH-4                  TRANSFORM                 ZERO
SWITCH-5                  TRUE                      ZEROES
SWITCH-6                  TYPE                      ZEROS
SWITCH-7
SWITCH-8                  UFAS                      +
SWITCH-9                  UFF                       -
SYMBOLIC                  UNBANNERED                *
SYNC                      UNEQUAL                   /
SYNCHRONIZED              UNIT                      **
SYSIN                     UNSTRING                  >
SYSIPT                    UNTIL                     <
SYSLST                    UP                        =
SYSOUT                    UPDATE                    >=
                          UPON                      <=
TABLE                     USAGE
TALLYING                  USAGE-MODE
00001
Function
The RESERVE clause allows the user to specify the number of input-output areas
allocated.
General Format
RESERVE integer-1 [AREA ]
                  [AREAS]
General Rule
1.  The RESERVE clause allows the user to specify the number of input-output
    areas allocated.  If the RESERVE clause is specified, the number of
    input-output areas allocated is equal to the value of integer-1.  If the
    RESERVE clause is not specified, the number of input-output areas
    allocated will default to one.
00001
Function
The RETURN statement obtains either sorted records from the final phase of a
sort operation or merged records during a merge operation.
General Format
RETURN file-name-1 RECORD [INTO identifier-1]
  AT END imperative-statement-1
  [NOT AT END imperative-statement-2]
  [END-RETURN]
Syntax Rules
1.  The storage area associated with identifier-1 and the record area
    associated with file-name-1 must not be the same storage area.
2.  File-name-1 must be described by a sort-merge file description entry in
    the Data Division.
3.  A RETURN statement may only be used within the range of an output
    procedure associated with a SORT or MERGE statement for file-name-1.
00001
00002
REWRITE_SEQUENTIAL
Function
The REWRITE statement logically replaces a record existing in a mass storage
file.
General Format
REWRITE record-name-1 [FROM identifier-1]
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-REWRITE]
Syntax Rules
1.  Record-name-1 and identifier-1 must not refer to the same storage area.
2.  Record-name-1 is the name of a logical record in the File Section of the
    Data Division and may be qualified.
3.  The INVALID KEY and the NOT INVALID KEY phrases must be specified if an
    applicable USE AFTER STANDARD EXCEPTION procedure is not specified for the
    associated file-name.
00001
Function
The REWRITE statement logically replaces a record existing in a mass storage
file.
General Format
REWRITE record-name-1 [FROM identifier-1]
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-REWRITE]
Syntax Rules
1.  Record-name-1 and identifier-1 must not refer to the same storage area.
2.  Record-name-1 is the name of a logical record in the File Section of the
    Data Division and may be qualified.
3.  The INVALID KEY and the NOT INVALID KEY phrases must not be specified in
    the REWRITE statement which references a keyed file in sequential access
    mode.
4.  The INVALID KEY phrase must be specified in the REWRITE statement for
    keyed files in the random or dynamic access mode, and for which an
    appropriate USE AFTER STANDARD EXCEPTION procedure is not specified.
00001
Function
The REWRITE statement logically replaces a record existing in a mass storage
file.
General Format
REWRITE record-name-1 [FROM identifier-1]
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-REWRITE]
Syntax Rules
1.  Record-name-1 and identifier-1 must not refer to the same storage area.
2.  Record-name-1 is the name of a logical record in the File Section of the
    Data Division and may be qualified.
3.  The INVALID KEY and the NOT INVALID KEY phrases must not be specified for
    a REWRITE statement which references a relative file in sequential access
    mode.
4.  The INVALID KEY phrase must be specified in the REWRITE statement for
    relative files in the random or dynamic access mode, and for which an
    appropriate USE AFTER STANDARD EXCEPTION procedure is not specified.
00001
Function
The REWRITE statement logically replaces a record existing in a mass storage
file.
General Format
REWRITE record-name-1 [FROM identifier-1] [END-REWRITE]
Syntax Rules
1.  Record-name-1 and identifier-1 must not refer to the same storage area.
2.  Record-name-1 is the name of a logical record in the File Section of the
    Data Division and may be qualified.
00001
Function
The SAME clause specifies the memory area which is to be shared by different
files.
General Format
SAME [RECORD] AREA FOR file-name-1 {file-name-2} ...
Syntax Rules
1.  File-name-1 and file-name-2 must be specified in the FILE-CONTROL
    paragraph of the same program.
2.  File-name-1 and file-name-2 may not reference an external file connector.
3.  More than one SAME clause may be included in the program, subject to the
    following restrictions:
    a.  A file-name must not appear in more than one SAME AREA clause.
    b.  A file-name must not appear in more than one SAME RECORD AREA clause.
    c.  If one or more file-names of a SAME AREA clause appear in a SAME
        RECORD AREA clause, all of the file-names in that SAME AREA clause
        must appear in the SAME RECORD AREA clause.  However, additional
        file-names not appearing in the SAME AREA clause may also appear in
        that SAME RECORD AREA clause.  The rule that only one of the files
        mentioned in a SAME AREA clause can be open at any time takes
        precedence over the rule that all files mentioned in a SAME RECORD
        AREA clause can be open at any given time.
4.  The files referenced in the SAME AREA or SAME RECORD AREA clause need not
    all have the same organization or access.
00001
Function
The SAME RECORD/SORT/SORT-MERGE AREA clause specifies the memory area which is
to be shared by different files at least one of which is a sort or merge file.
General Format
     {RECORD    }
SAME {SORT      } AREA FOR file-name-1 {file-name-2} ...
     {SORT-MERGE}
Syntax Rules
1.  Each file-name specified in the SAME RECORD/SORT/SORT-MERGE AREA clause
    must be specified in the FILE-CONTROL paragraph of the same program.
2.  File-name-1 and file-name-2 may not reference an external file connector.
3.  SORT and SORT-MERGE are equivalent.
4.  A file-name that represents a sort or merge file must not appear in the
    SAME clause unless the SORT, SORT-MERGE, or RECORD phrase is used.
5.  More than one SAME clause may be included in the program, subject to the
    following restrictions:
    a.  A file-name must not appear in more than one SAME RECORD AREA clause.
    b.  A file-name that represents a sort or merge file must not appear in
        more than one SAME SORT AREA or SAME SORT-MERGE AREA clause.
    c.  If a file-name that does not represent a sort or merge file appears in
        a SAME clause and one or more SAME SORT AREA or SAME SORT-MERGE AREA
        clauses, all of the files named in that SAME clause must be named in
        that SAME SORT AREA or SAME SORT-MERGE AREA clause(s).
6.  The files referenced in the SAME RECORD/SORT/SORT-MERGE AREA clause need
    not all have the same organization or access.
7.  The SAME clause is documentary in nature.
00001
00002
The following example is a simulated COBOL programming session on the CP-6
system.  A carriage return is required at the end of each line of user input.
  ***CP-6 AT YOUR SERVICE, LADC L66A
LOGON PLEASE:  account,name,password
  *** SYSID# 23196 ON LADC L66S AT 10:58:32.52 MON JAN 21 '86.
The system identifies itself and requests that the user logon.  The user types
the account, name and password; this information is not normally echoed by the
system.  The system confirms logon, stating the exact time and date that logon
took place.
!DISPLAY
   USERS = 62
   ETMF = 3
   90% RESPONSE < 250 MSECS
   JAN 21 '86  10:59
                      The user requests information about the current state of
                      the system.
!TABS 8,12,16,20,24,28,32,36,40
                      The user sets tab stops for COBOL programming.
!EDIT
EDIT HERE
*BUILD COBOL-EXAMPLE
     1.000          IDENTIFICATION DIVISION.
     2.000          PROGRAM-ID.    COBOL-EXAMPLE.
     3.000          AUTHOR.        CFL III.
     4.000          ENVIRONMENT DIVISION.
     5.000          CONFIGURATION SECTION.
     6.000          SOURCE-COMPUTER.
     7.000              DPS-8000.
     8.000          OBJECT-COMPUTER.
     9.000              DPS-8000.
    10.000          INPUT-OUTPUT SECTION.
    11.000          FILE-CONTROL.
    12.000          SELECT RELATIVE-FILE
    13.000                 ASSIGN TO DISK
    14.000                 ORGANIZATION IS RELATIVE
    15.000                 ACCESS IS SEQUENTIAL.
    16.000          SELECT ASCII-FILE
    17.000                 ASSIGN TO DISK
    18.000                 ORGANIZATION IS SEQUENTIAL.
    19.000          DATA DIVISION.
    20.000          FILE SECTION.
    21.000          FD ASCII-FILE.
    22.000              01  ascii-record   PIC X(80).
    23.000          FD RELATIVE-FILE.
    24.000              01  relative-record   PIC X(80).
    25.000          WORKING-STORAGE SECTION.
    26.000          77  data-indicator     PIC X  VALUE SPACE.
    27.000              88  data-present          VALUE SPACE.
    28.000              88  no-more-data          VALUE HIGH-VALUES.
    29.000          PROCEDURE DIVISION.
    30.000          Required-label.
    31.000              OPEN INPUT  ASCII-FILE
    32.000                   OUTPUT RELATIVE-FILE
    33.000              PERFORM UNTIL no-more-data
    34.000                READ ASCII-FILE
    35.000                  AT END
    36.000                    MOVE HIGH-VALUES TO data-indicator
    37.000                    DISPLAY 'End of input'
    38.000                END-READ
    39.000
    40.000                IF data-present THEN
    41.000                  WRITE relative-record FROM ascii-record
    42.000                    INVALID KEY
    43.000                      DISPLAY "Invalid key on relative file"
    44.000                  END WRITE
    45.000                END-IF
    46.000              END-PERFORM
    47.000
    48.000              CLOSE ASCII-FILE RELATIVE-FILE
    49.000              STOP RUN.
*END
!COBOL85 COBOL-EXAMPLE OVER COBOL-OBJECT-UNIT(NLS)
                      The user compiles the source program, using the standard
                      compiler options.
!LINK COBOL-OBJECT-UNIT OVER COBOL-RUN-UNIT
                      The user loads the object program.
!SET ASCII-FILE OLD-FILE
                      The user sets the input DCB.
!SET RELATIVE-FILE NEW-FILE,NRECS=30
                      The user sets the output DCB.
!COBOL-RUN-UNIT.
                      The user calls the run unit into execution.
!L
COBOL-EXAMPLE  COBOL-OBJECT-UNIT  COBOL-RUN-UNIT  NEW-FILE  OLD-FILE
 ..5 FILES LISTED
                      The user lists the files in the account.
!L(A) NEW-FILE
13:27 JAN 21 '86  DP/.COBRAM
ORG TY  GRAN NGAV     REC   LAST MODIFIED   NAME
REL        2    0      40 13:26 JAN 21 '86  NEW-FILE
                      The user requests a listing of NEW-FILE with attributes,
                      note that the organization (ORG) is relative (REL).
!DELETE COBOL-OBJECT-UNIT
COBOL-OBJECT-UNIT
1 FILE     2 GRANULES DELETED
                      The user deletes the object unit from the account.
!OFF
                      The user leaves the system.
Function
The sort-merge file description entry furnishes information concerning the
physical structure and record-names pertaining to a sort or merge file.
General Format
SD file-name-1
  [       {CONTAINS integer-1 CHARACTERS                                  }]
  [       {                                                               }]
  [       {IS VARYING IN SIZE [[FROM integer-2] [TO integer-3] CHARACTERS]}]
  [RECORD {                                                               }]
  [       {   [DEPENDING ON data-name-1]                                  }]
  [       {                                                               }]
  [       {CONTAINS integer-4 TO integer-5 CHARACTERS                     }]
  [DATA {RECORD IS  } {data-name-2} ...] .
  [     {RECORDS ARE}                  ]
Syntax Rules
1.  The level indicator SD identifies the beginning of the sort-merge file
    description entry and must precede file-name-1.
2.  The clauses which follow file-name-1 are optional, and their order of
    appearance is immaterial.
3.  One or more record description entries must follow the sort-merge file
    description entry; however, no input-output statements may be executed for
    this sort or merge file.
00001
Function
The SEARCH statement is used to search a table for a table element that
satisfies the specified condition and to adjust the value of the associated
index to indicate that table element.
General Format
Format 1:
SEARCH identifier-1 [VARYING {identifier-2}]
                    [        {index-name-1}]
  [AT END imperative-statement-1]
  {WHEN condition-1 {imperative-statement-2}} ...
  {                 {NEXT SENTENCE         }}
  [END-SEARCH]
Format 2:
SEARCH ALL identifier-1 [AT END imperative-statement-1]
       {            {IS EQUAL TO} {identifier-3           }}
       {data-name-1 {IS =       } {literal-1              }}
  WHEN {                          {arithmetic-expression-1}}
       {condition-name-1                                   }
    [     {            {IS EQUAL TO} {identifier-4           }}]
    [     {data-name-2 {IS =       } {literal-2              }}]
    [ AND {                          {arithmetic-expression-2}}] ...
    [     {condition-name-2                                   }]
    {imperative-statement-2}
    {NEXT SENTENCE         }
  [END-SEARCH]
Syntax Rules
1.  In both formats 1 and 2, identifier-1 must not be subscripted or reference
    modified, but its description must contain an OCCURS clause including an
    INDEXED BY phrase.  The description of identifier-1 in format 2 must also
    contain the KEY IS phrase in its OCCURS clause.
2.  Identifier-2 must reference a data item described as USAGE IS INDEX or as
    a numeric elementary data item without any positions to the right of the
    assumed decimal point.  Identifier-2 may not be subscripted by the first
    (or only) index-name specified in the INDEXED BY phrase in the OCCURS
    clause associated with identifier-1.
3.  In format 1, condition-1 may be any conditional expression.
4.  In format 2, all referenced condition-names must be defined as having only
    a single value.  The data-name associated with a condition-name must
    appear in the KEY IS phrase in the OCCURS clause referenced by
    identifier-1.  Each data-name-1, data-name-2 may be qualified.  Each
    data-name-1, data-name-2 must be subscripted by the first index-name
    associated with identifier-1 along with other subscripts as required, and
    must be referenced in the KEY IS phrase in the OCCURS clause referenced by
    identifier-1.  Identifier-3, identifier-4, or identifiers specified in
    arithmetic-expression-1, arithmetic-expression-2 must not be referenced in
    the KEY IS phrase in the OCCURS clause referenced by identifier-1 or be
    subscripted by the first index-name associated with identifer-1.
    In format 2, when a data-name in the KEY IS phrase in the OCCURS clause
    referenced by identifier-1 is referenced, or when a condition-name
    associated with a data-name in the KEY IS phrase in the OCCURS clause
    referenced by identifier-1 is referenced, all preceding data-names in the
    KEY IS phrase in the OCCURS clause referenced by identifier-1 or their
    associated condition-names must also be referenced.
5.  If the END-SEARCH phrase is specified, the NEXT SENTENCE phrase must not
    be specified.
00001
    The SECURITY paragraph is used to supply the level of security attached to
    the program by the installation or user.
General Format
SECURITY. [comment-entry]
Syntax Rule
1.  The comment-entry can be one or more sentences, including any combination
    of characters.  The comment-entry has no effect on the operation of a
    COBOL program.
    Segmentation provides a means by which the user may communicate with the
    compiler to specify object program overlay requirements.
    COBOL segmentation deals only with segmentation of procedures.  As such,
    only the Procedure Division and the Environment Division are considered in
    determining segmentation requirements for an object program.    See the
    following related topics:
    OBJECT_COMPUTER_SEGMENTATION, SEGMENT_LIMIT,
    PROCEDURE_DIV_SEGMENTATION, and SEGMENT_NUMBERS.
Function
Ideally, all program segments having segment-numbers ranging from 0 through 49
should be specified as permanent segments.  However, when insufficient memory
is available to contain all permanent segments plus the largest overlayable
segment, it becomes necessary to decrease the number of permanent segments.
The SEGMENT-LIMIT feature provides the user with a means of reducing the
number of permanent segments in this program, while still retaining the
logical properties of fixed portion segments (segment-numbers 0 through 49).
General Format
SEGMENT-LIMIT IS segment-number
Syntax Rule
1.  Segment-number must be an integer ranging in value from 1 through 49.
00001
Function
Section classification is accomplished by means of a system of
segment-numbers.  The segment-number is included in the section header within
the Procedure Division.
General Format
section-name SECTION [segment-number].
Syntax Rules
1.  The segment-number must be an integer ranging in value from 0 through 99.
2.  If the segment-number is omitted from the section header, the
    segment-number is assumed to be 0.
3.  Sections in the declaratives must contain segment-numbers less than 50.
00001
SELECT_SEQUENTIAL
Function
The file control entry declares the relevant physical attributes of an indexed
file.
General Format
SELECT [OPTIONAL] file-name-1
  ASSIGN TO DISK
  [RESERVE integer-1 [AREA ]]
  [                  [AREAS]]
  [ORGANIZATION IS] INDEXED
  [               {SEQUENTIAL}]
  [ACCESS MODE IS {RANDOM    }]
  [               {DYNAMIC   }]
  RECORD KEY IS data-name-1
  [ALTERNATE RECORD KEY IS data-name-2 [WITH DUPLICATES]] ...
  [FILE STATUS IS data-name-3].
Syntax Rules
1.  The SELECT clause must be specified first in the file control entry.  The
    clauses which follow the SELECT clause may appear in any order.
2.  Each file-name in the Data Division must be specified only once in the
    FILE-CONTROL paragraph.  Each file-name specified in the SELECT clause
    must have a file description entry in the Data Division of the same
    program.
00001
Function
The file control entry declares the relevant physical attributes of a keyed
file.
General Format
SELECT [OPTIONAL] file-name-1
  ASSIGN TO DISK
  [RESERVE integer-1 [AREA ]]
  [                  [AREAS]]
  [ORGANIZATION IS] KEYED
  [               {SEQUENTIAL [RECORD KEY IS data-name-1] }]
  [ACCESS MODE IS {                                       }]
  [               {{RANDOM    } RECORD KEY IS data-name-1 }]
  [               {{DYNAMIC   }                           }]
  [FILE STATUS IS data-name-2].
Syntax Rules
1.  The SELECT clause must be specified first in the file control entry.  The
    clauses which follow the SELECT clause may appear in any order.
2.  Each file-name in the Data Division must be specified only once in the
    FILE-CONTROL paragraph.  Each file-name specified in the SELECT clause
    must have a file description entry in the Data Division of the same
    program.
00001
Function
The file control entry declares the relevant physical attributes of a relative
file.
General Format
SELECT [OPTIONAL] file-name-1
  ASSIGN TO DISK
  [RESERVE integer-1 [AREA ]]
  [                  [AREAS]]
  [ORGANIZATION IS] RELATIVE
  [               {SEQUENTIAL [RELATIVE KEY IS data-name-1]}]
  [ACCESS MODE IS {                                        }]
  [               {{RANDOM } RELATIVE KEY IS data-name-1   }]
  [               {{DYNAMIC}                               }]
  [FILE STATUS IS data-name-2].
Syntax Rules
1.  The SELECT clause must be specified first in the file control entry.  The
    clauses which follow the SELECT clause may appear in any order.
2.  Each file-name in the Data Division must be specified only once in the
    FILE-CONTROL paragraph.  Each file-name specified in the SELECT clause
    must have a file description entry in the Data Division of the same
    program.
00001
Function
The file control entry declares the relevant physical attributes of a report
file.
General Format
SELECT [OPTIONAL] file-name-1
  ASSIGN TO {external-device-name-1} ...
  [RESERVE integer-1 [AREA ]]
  [                  [AREAS]]
  [[ORGANIZATION IS] SEQUENTIAL
  [PADDING CHARACTER IS {data-name-1}]
  [                     {literal-1  }]
  [RECORD DELIMITER IS {STANDARD-1}]
  [ACCESS MODE IS SEQUENTIAL]
  [FILE STATUS IS data-name-2].
Syntax Rules
1.  The SELECT clause must be specified first in the file control entry.  The
    clauses which follow the SELECT clause may appear in any order.
2.  Each report file described in the Data Division must be specified only
    once in the FILE-CONTROL paragraph.  Each report file specified in the
    SELECT clause must have a file description entry containing a REPORT
    clause in the Data Division of the same program.
3.  External-device-name-1 must be one the following:  PRINTER, SYSOUT, or
    DISK.
00001
Function
The file control entry declares the relevant physical attributes of a
sequential file.
General Format
SELECT [OPTIONAL] file-name-1
  ASSIGN TO {external-device-name-1} ...
  [RESERVE integer-1 [AREA ]]
  [                  [AREAS]]
  [[ORGANIZATION IS] SEQUENTIAL]
  [PADDING CHARACTER IS {data-name-1}]
  [                     {literal-1  }]
  [RECORD DELIMITER IS {STANDARD-1}]
  [ACCESS MODE IS SEQUENTIAL]
  [FILE STATUS IS data-name-2].
Syntax Rules
1.  The SELECT clause must be specified first in the file control entry.  The
    clauses which follow the SELECT clause may appear in any order.
2.  Each file-name in the Data Division must be specified only once in the
    FILE-CONTROL paragraph.  Each file-name specified in the SELECT clause
    must have a file description entry in the Data Division of the same
    program.
3.  External-device-name-1 must be selected from the following:  PRINTER,
    PRINTER-F, CARD-READER, SYSIN, SYSOUT, CARD-PUNCH, MAGNETIC-TAPE, or DISK.
00001
Function
The file control entry declares the relevant physical attributes of a sort or
merge file.
General Format
SELECT file-name-1 ASSIGN TO {MAGNETIC-TAPE} ... .
                             {DISK         }
Syntax Rules
1.  Each sort or merge file described in the Data-Division must be specified
    only once in the FILE-CONTROL paragraph.  Each sort or merge file
    specified in the SELECT clause must have a sort-merge file description
    entry in the Data Division of the same program.
2.  Since file-name-1 represents a sort or merge file, only the ASSIGN clause
    is permitted to follow file-name-1 in the FILE-CONTROL paragraph.
00001
00002
    Sequential I-O provides a capability to access records of a file in an
    established sequence.  The sequence is established as a result of writing
    the records to the file.
    Sequential files are organized so that each record, except the last, has a
    unique successor record; each record, except the first, has a unique
    predecessor record.  The successor relationships are established by the
    order of execution of WRITE statements when the file is created.  Once
    established, successor relationships do not change except where records
    are added to the end of a file.
    A sequentially organized mass storage file has the same logical structure
    as a file on any sequential medium; however, a sequential mass storage
    file may be updated in place.  When this technique is used, new records
    cannot be added to the file and each replaced record must be the same size
    as the original record.  See the following related topics:
    INPUT_OUTPUT, FILE_CONTROL, SELECT, ACCESS_MODE, FILE_STATUS,
    ORGANIZATION, PADDING_CHARACTER, RECORD_DELIMITER, RESERVE,
    IO_CONTROL, MULTIPLE_FILE_TAPE, SAME, FILE_SECTION,
    FD, BLOCK_CONTAINS, CODE_SET, DATA_RECORDS, LABEL_RECORDS,
    LINAGE, RECORD, VALUE_OF, CLOSE, OPEN, READ, REWRITE, USE,
    and WRITE.
Function
The SET statement establishes reference points for table handling operations
by setting indices associated with table elements.  It also alters the status
of external switches, and alters the value of conditional variables and
pointer variables.
General Format
Format 1:
                          {index-name-2}
SET {index-name-1} ... TO {identifier-2}
    {identifier-1}        {integer-1   }
Format 2:
SET {index-name-3} ... {UP BY  } {identifier-3}
                       {DOWN BY} {integer-2   }
Format 3:
    {                          {ON              }}
SET {{SWITCH-integer-1} ... TO {OFF             }} ...
    {                          {SWITCH-integer-2}}
    {                          {mnemonic-name-2 }}
    {                          {ON              }}
SET {{mnemonic-name-1}  ... TO {OFF             }} ...
    {                          {SWITCH-integer-2}}
    {                          {mnemonic-name-2 }}
Format 4:
SET {condition-name-1} ... TO TRUE
Format 5:
    {identifier-4           }
SET {ADDRESS OF identifier-5} ...
    {identifier-6           }
TO  {NULL                   }
    {ADDRESS OF identifier-7}
Syntax Rules
1.  All references to index-name-1, identifier-1, and index-name-3 apply
    equally to all recursions thereof.
2.  Identifier-1 and identifier-2 must each reference an index data item or an
    elementary item described as an integer.
3.  Identifier-3 must reference an elementary numeric integer.
4.  Integer-1 and integer-2 may be signed.  Integer-1 must be positive.
5.  Switch-name-n is an external switch where  n is 0 to 35.
6.  Condition-name-1 must be associated with a conditional variable.
7.  For compatibility with COBOL-74, in SET format 3, the TO is optional when
    the sending field is ON or OFF, and the receiving field consists of one
    SWITCH or one mnemonic-name (for example, SET SWITCH-17 ON).
8.  Identifier-4 and identifier-6 must be described as USAGE IS POINTER.
9.  Identifier-5 must be a level 01 or 77 item defined in the LINKAGE SECTION.
00001
Function
The SIGN clause specifies the position and the mode of representation of the
operational sign when it is necessary to describe these properties explicitly.
General Format
[SIGN IS] {LEADING } [SEPARATE CHARACTER]
          {TRAILING}
Syntax Rules
1.  The SIGN clause may be specified only for a numeric data description entry
    whose PICTURE contains the character 'S', or a group item containing at
    least one such numeric data description entry.
2.  The numeric data description entries to which the SIGN clause applies must
    be described, implicitly or explicitly, as USAGE IS DISPLAY, COMP, COMP-3,
    COMP-4, COMP-5, COMP-8.
3.  If the CODE-SET clause is specified in a file description entry, any
    signed numeric data description entries associated with that file
    description entry must be described with the SIGN IS SEPARATE clause.
00001
Function
The SIGN clause specifies the position and the mode of representation of the
operational sign when it is necessary to describe these properties explicitly.
General Format
[SIGN IS] {LEADING } SEPARATE CHARACTER
          {TRAILING}
Syntax Rules
1.  The SIGN clause may be specified only for a numeric data description entry
    whose PICTURE contains the character 'S'.
2.  The numeric data description entries to which the SIGN clause applies must
    be described, implicitly or explicitly, as USAGE IS DISPLAY.
3.  When the SIGN clause is included in a report group description entry, the
    SEPARATE CHARACTER phrase must be specified.
00001
SIGN_CLAUSE_REPORT_WRITER
SORT_STATEMENT
        Sort-Merge provides the capability to order one or more files of
        records, or to combine two or more identically ordered files of
        records, according to a set of user-specified keys contained within
        each record.  Optionally, a user may apply some special processing to
        each of the individual records by input or output procedures.  This
        special processing may be applied before and/or after the records are
        ordered by the SORT or after the records have been combined by the
        MERGE.    See the following related topics:    IO_CONTROL_SORT_MERGE,
        SELECT_SORT_MERGE, SAME_SORT_MERGE, FILE_SECTION_SORT_MERGE, SD,
        MERGE, RELEASE, RETURN and SORT.
Function
The SORT statement creates a sort file by executing an input procedure or by
transferring records from another file, sorts the records in the sort file or
a set of specified keys; and, in the final phase of the sort operation, makes
available each record from the sort file, in sorted order, to an input
procedure or to an output file.
General Format
SORT file-name-1 {ON {ASCENDING } KEY {data-name-1} ...} ...
                 {   {DESCENDING}                      }
  [WITH DUPLICATES IN ORDER]
  [COLLATING SEQUENCE IS alphabet-name-1]
  {INPUT PROCEDURE IS procedure-name-1 [{THROUGH} procedure-name-2]}
  {                                    [{THRU   }                 ]}
  {USING {file-name-2} ...                                         }
  {OUTPUT PROCEDURE IS procedure-name-3 [{THROUGH} procedure-name-4]}
  {                                     [{THRU   }                 ]}
  {GIVING {file-name-3} ...                                         }
Syntax Rules
1.  A SORT statement may appear anywhere in the Procedure Division except in
    the declarative portion.
2.  File-name-1 must be described in a sort-merge file description entry in
    the Data Division.
3.  If the USING phrase is specified and the file referenced by file-name-1
    contains variable length records, the size of the records contained in the
    file referenced by file-name-2 must not be less than the smallest record
    nor larger than the largest record described for file-name-1.  If the file
    referenced by file-name-1 contains fixed length records, the size of the
    records contained in the file referenced by file-name-2 must not be larger
    than the largest record described for the file referenced by file-name-1.
4.  Data-name-1 is a key data-name.  Key data-names are subject to the
    following rules:
    a.  The data item identified by key data-names must be described in
        records associated with file-name-1.
    b.  Key data-names may be qualified.
    c.  The data items identified by key data-names must not be group items
        that contain variable occurrence data items.
    d.  If file-name-1 has more than one record description, the data items
        identified by key data-names need be described in only one of the
        record descriptions.  The same character positions which are
        referenced by a key data-name in one record description entry are
        taken as the key in all records of the file.
    e.  None of the data items identified by key data-names can be described
        by an entry which either contains an OCCURS clause or is subordinate
        to an entry which contains an OCCURS clause.
    f.  If the file referenced by file-name-1 contains variable length
        records, all the data items identified by key data-names must be
        contained within the first x character positions of the record, where
        x equals the minimum record size specified for the file referenced by
        file-name-1.
    g.  None of the data items identified by key data-names can be described
        as USAGE IS EBCDIC.
5.  The words THRU and THROUGH are equivalent.
6.  File-name-2 and file-name-3 must be described in a file description entry,
    not in a sort-merge file description entry, in the Data Division.
7.  The file referenced by file-name-2 and file-name-3 may reside on the same
    multiple file reel.
8.  If file-name-3 references an indexed file, the first specification of
    data-name-1 must be associated with an ASCENDING phrase and the data item
    referenced by that data-name-1 must occupy the same character positions in
    its record as the data item associated with the prime record key for that
    file.
9.  No pair of file-names in the same SORT statement may be specified in the
    same SAME SORT AREA or SAME SORT-MERGE AREA clause.  File-names associated
    with the GIVING phrase may not be specified in the SAME clause.
10. If the GIVING phrase is specified and the file referenced by file-name-3
    contains variable length records, the size of the records contained in the
    file referenced by file-name-1 must not be less than the smallest record
    nor larger than the largest record described for file-name-3.  If the file
    referenced by file-name-3 contains fixed length records, the size of the
    records contained in the file referenced by file-name-1 must not be larger
    than the largest record described for the file referenced by file-name-3.
00001
Function
The SOURCE clause identifies the sending data item that is moved to an
associated printable item defined within a report group description entry.
General Format
SOURCE IS identifier-1
Syntax Rules
1.  Identifier-1 may be defined in any section of the Data Division.  If
    identifier-1 is a Report Section item it must be a:
    a.  PAGE-COUNTER, or
    b.  LINE-COUNTER, or
    c.  Sum counter that is part of the report within which the SOURCE clause
        appears.
2.  Identifier-1 specifies the sending data item of the implicit MOVE
    statement that the report writer control system (RWCS) executes to move
    the content of the data item referenced by identifier-1 to the printable
    item.  Identifier-1 must be defined such that it conforms to the rules for
    sending items in the MOVE statement.
00001
Function
The SOURCE-COMPUTER paragraph provides a means of describing the computer upon
which the program is to be compiled.
General Format
SOURCE-COMPUTER. [HIS-SERIES-60] LEVEL-66-ASCII [WITH DEBUGGING MODE].]
General Rules
1.  All clauses of the SOURCE-COMPUTER paragraph apply to the program in which
    they are explicitly or implicitly specified and to any program contained
    within that program.
2.  When the SOURCE-COMPUTER paragraph is not specified and the program is not
    contained within a program including a SOURCE-COMPUTER paragraph, the
    computer on which the source program is being compiled is the source
    computer.
3.  When the SOURCE-COMPUTER paragraph is specified, but the
    source-computer-entry is not specified, the computer upon which the source
    program is being compiled is the source computer.
4.  If the WITH DEBUGGING MODE clause is specified in a program, all debugging
    lines are compiled as specified in this presentation of the Nucleus
    module.
5.  If the WITH DEBUGGING MODE clause is not specified in a program and the
    program is not contained within a program including a WITH DEGUGGING MODE
    clause, any debugging lines are compiled as if they were comment lines.
00001
A COBOL source program is a syntactically correct set of COBOL statements.
With the exception of COPY and REPLACE statements and the end program header,
the statements, entries, paragraphs, and sections of a COBOL source program
are grouped into five divisions which are sequenced in the following order:
    1.  The Control Division
    2.  The Identification Division
    3.  The Environment Division
    4.  The Data Division
    5.  The Procedure Division
The end of a COBOL source program is indicated by either the end program
header, if specified, or the absence of additional source program lines.
The following gives the general format and order of presentation of the
entries and statements which constitute a COBOL source program.
General Format
[control-division]
identification-division
[environment-division]
[data-division]
[procedure-division]
[end-program-header]
Syntax Rule
1.  The generic terms control-division, identification-division,
    environment-division, data-division, procedure-division, and
    end-program-header represent a COBOL Control Division, a COBOL
    Identification Division, a COBOL Environment Division, a COBOL Data
    Division, a COBOL Procedure Division, and a COBOL end program header,
    respectively.
General Rules
1.  The beginning of a division in a program is indicated by the appropriate
    division header.  The end of a division is indicated by one of the
    following:
    a.  The division header of a succeeding division in that program
    b.  The end program header
    c.  That physical position after which no more source program lines occur
2.  All separately compiled source programs in a sequence of programs must be
    terminated by an end program header except for the last program in the
    sequence.
00002
00001
            Source Text Manipulation contains the COPY statement and the
            REPLACE statement.  Each of these statements can function either
            independently or in conjunction with the other to provide an
            extensive capability to insert and replace source program text as
            part of the compilation of the source program.
              See the following related topics:  COPY and REPLACE.
Function
The SPECIAL-NAMES paragraph provides a means for specifying the currency sign,
choosing the decimal point, specifying symbolic characters, relating
specific-names to user-specified mnemonic-names, relating alphabet-names to
character sets or collating sequences, and relating class-names to sets of
characters.
General Format
               [[{SWITCH-n}
               [[{SYSIN   }
SPECIAL-NAMES. [[{SYSOUT  }
               [[{CONSOLE }
               [[{PAGE    }
  {IS mnemonic-name-1 [ON STATUS IS condition-name-1 [OFF STATUS IS
  {IS mnemonic-name-2 [OFF STATUS IS condition-name-2 [ON STATUS IS
  {ON STATUS IS condition-name-1 [OFF STATUS IS condition-name-2]
  {OFF STATUS IS condition-name-2 [ON STATUS IS condition-name-1]
      condition-name-2]]}]
      condition-name-1]]}]
                        }] ...
                        }]
  [ALPHABET alphabet-name-1 IS
    {STANDARD-1                            }]
    {STANDARD-2                            }]
    {NATIVE                                }]
    {ASCII                                 }]
    {EBCDIC                                }]
    {{          [{THROUGH}          ]}     }] ...
    {{literal-1 [{THRU   } literal-2]} ... }]
    {{          [{ALSO literal-3}   ]}     }]
  [SYMBOLIC CHARACTERS {{{symbolic-character-1} ... {IS } {integer-1} ...} ...
  [                    {{                           {ARE}                }
    [IN alphabet-name-2]}] ...
  [CLASS class-name IS {literal-4 [{THROUGH} literal-5]} ...] ...
  [                    {          [{THRU   }          ]}    ]
  [CURRENCY SIGN IS literal-6]
  [DECIMAL-POINT IS COMMA].]
Syntax Rules
1.  If SWITCH-n is specified, n must be 0 through 35.  The associated
    mnemonic-name may be specified only in the SET statement.
2.  If CONSOLE, SYSIN, or PAGE is specified, the associated mnemonic-name may
    be specified only in the ACCEPT, DISPLAY, or WRITE statements.  A
    condition-name cannot be associated with such a system-name.
3.  If the literal phrase of the ALPHABET clause is specified, a given
    character must not be specified more than once in that clause.
4.  The literals specified in the literal phrase of the ALPHABET clause:
    a.  If numeric, must be unsigned integers and must have a value within the
        range of one through the maximum number of characters in the native
        character set.
    b.  If nonnumeric and associated with a THROUGH or ALSO phrase, must each
        be one character in length.
5.  Literal-1, literal-2, literal-3, literal-4 and literal-5 must not specify
    a symbolic-character figurative constant.
6.  The words THRU and THROUGH are equivalent.
7.  The same symbolic-character-1 must appear only once in a SYMBOLIC
    CHARACTERS clause.
8.  The relationship between each symbolic-character-1 and the corresponding
    integer-1 is by position in the SYMBOLIC-CHARACTERS clause.  The first
    symbolic-character-1 is paired with the first integer-1; the second
    symbolic-character-1 is paired with the second integer-1, and so on.
9.  There must be a one-to-one correspondence between occurrences of
    symbolic-character-1 and occurrences of integer-1.
10. The ordinal position specified by integer-1 must exist in the native
    character set.  If the IN phrase is specified, the ordinal position must
    exist in the character set named by alphabet-name-2.
11. The literals specified in the literal-4 phrase:
    a.  If numeric, must be unsigned integers and must have a value within the
        range of one through the maximum number of characters in the native
        character set.
    b.  If nonnumeric and associated with a THROUGH phrase, must each be one
        character in length.
12. Literal-6 must not be a figurative constant.
00001
START_RELATIVE
Function
The START statement provides a basis for logical positioning within an indexed
file, for subsequent sequential retrieval of records.
General Format
                  [    {IS EQUAL TO                }            ]
                  [    {IS =                       }            ]
                  [    {IS GREATER THAN            }            ]
START file-name-1 [KEY {IS >                       } data-name-1]
                  [    {IS NOT LESS THAN           }            ]
                  [    {IS NOT <                   }            ]
                  [    {IS GREATER THAN OR EQUAL TO}            ]
                  [    {IS >=                      }            ]
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-START]
Syntax Rules
1.  File-name-1 must be the name of a file with sequential or dynamic access.
2.  Data-name-1 may be qualified.
3.  The INVALID KEY phrase must be specified if no applicable USE AFTER
    STANDARD EXCEPTION procedure is specified for file-name-1.
4.  If the KEY phrase is specified, data-name-1 must reference either:
    a.  A data item specified as a record key associated with file-name-1 or
    b.  Any data item of category alphanumeric whose leftmost character
        position within a record of the file corresponds to the leftmost
        character position of a record key associated with file-name-1 and
        whose length is not greater than the length of that record key
00001
Function
The START statement provides a basis for logical positioning within a keyed
file, for subsequent sequential retrieval of records.
General Format
                  [    {IS EQUAL TO                }            ]
                  [    {IS =                       }            ]
                  [    {IS GREATER THAN            }            ]
                  [    {IS >                       }            ]
START file-name-1 [KEY {IS NOT LESS THAN           } data-name-1]
                  [    {IS NOT <                   }            ]
                  [    {IS GREATER THAN OR EQUAL TO}            ]
                  [    {IS >=                      }            ]
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-START]
Syntax Rules
1.  File-name-1 must be the name of the file with sequential or dynamic
    access.
2.  Data-name-1 may be qualified.
3.  The INVALID KEY phrase must be specified if no applicable USE AFTER
    STANDARD EXCEPTION procedure is specified for file-name-1.
4.  Data-name-1, if specified, must be the data item specified in the RECORD
    KEY phrase in the ACCESS MODE clause of the associated file control entry.
00001
Function
The START statement provides a basis for logical positioning within a relative
file, for subsequent sequential retrieval of records.
General Format
                  [    {IS EQUAL TO                }            ]
                  [    {IS =                       }            ]
                  [    {IS GREATER THAN            }            ]
                  [    {IS >                       }            ]
START file-name-1 [KEY {IS NOT LESS THAN           } data-name-1]
                  [    {IS NOT <                   }            ]
                  [    {IS GREATER THAN OR EQUAL TO}            ]
                  [    {IS >=                      }            ]
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-START]
Syntax Rules
1.  File-name-1 must be the name of the file with sequential or dynamic
    access.
2.  Data-name-1 may be qualified.
3.  The INVALID KEY phrase must be specified if no applicable USE AFTER
    STANDARD EXCEPTION procedure is specified for file-name-1.
4.  Data-name-1, if specified, must be the data item specified in the RELATIVE
    KEY phrase in the ACCESS MODE clause of the associated file control entry.
00001
Function
The STOP statement causes a permanent or temporary suspension of the execution
of the run unit.
General Format
STOP {RUN      }
     {literal-1}
Syntax Rules
1.  Literal-1 must not be a figurative constant that begins with the word ALL.
2.  If a STOP RUN statement appears in a consecutive sequence of imperative
    statements within a sentence, it must appear as the last statement in that
    sequence.
3.  If literal-1 is numeric,  it must be an unsigned integer.
00001
Function
The STRING statement provides juxtaposition of the partial or complete
contents of one or more data items into a single data item.
General Format
                                        {identifier-2}}
STRING {{identifier-1} ... DELIMITED BY {literal-2   }} ...
       {{literal-1   }                  {SIZE        }}
  INTO identifier-3
  [WITH POINTER identifier-4]
  [ON OVERFLOW imperative-statement-1]
  [NOT ON OVERFLOW imperative-statement-2]
  [END-STRING]
Syntax Rules
1.  Literal-1 or literal-2 must not be a figurative constant that begins with
    the word ALL.
2.  All literals must be described as nonnumeric literals, and all
    identifiers, except identifier-4, must be described implicitly or
    explicitly as USAGE IS DISPLAY.
3.  Identifier-3 must not be reference modified.
4.  Identifier-3 must not represent an edited data item and must not be
    described with the JUSTIFIED clause.
5.  Identifier-4 must be described as an elementary numeric integer data item
    of sufficient size to contain a value equal to 1 plus the size of the data
    item referenced by identifier-3.  The symbol 'P' may not be used in the
    PICTURE character-string of identifier-4
6.  Where identifier-1 or identifier-2 is an elementary numeric data item, it
    must be described as an integer without the symbol 'P' in its PICTURE
    character-string.
00001
Function
The SUBTRACT statement is used to subtract one, or the sum of two or more,
numeric data items from one or more items, and set the value of one or more
items equal to the results.
General Format
Format 1:
SUBTRACT {identifier-1} ... FROM {identifier-2 [ROUNDED]} ...
         {literal-1   }
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-SUBTRACT]
Format 2:
SUBTRACT {identifier-1} ... FROM {identifier-2}
         {literal-1   }          {literal-2   }
  GIVING {identifier-3 [ROUNDED]} ...
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-SUBTRACT]
Format 3:
SUBTRACT {CORRESPONDING} identifier-1 FROM identifier-2 [ROUNDED]
         {CORR         }
  [ON SIZE ERROR imperative-statement-1]
  [NOT ON SIZE ERROR imperative-statement-2]
  [END-SUBTRACT]
Syntax Rules
1.  Each identifier must refer to a numeric elementary item except that:
    a.  In format 2, each identifier following the word GIVING must refer to
        either an elementary numeric item or an elementary numeric edited
        item.
    b.  In format 3, each identifier must refer to a group item.
2.  Each literal must be a numeric literal.
3.  The composite of operands must not contain more than 18 digits.
    a.  In format 1, the composite of operands is determined by using all of
        the operands in a given statement.
    b.  In format 2, the composite of operands is determined by using all of
        the operands in a given statement excluding the data items that follow
        the word GIVING.
    c.  In format 3, the composite of operands is determined separately for
        each pair of corresponding data items.
4.  CORR is an abbreviation for CORRESPONDING.
00001
Function
The SUM clause establishes a sum counter and names the data items to be
summed.
General Format
{SUM {identifier-1} ... [UPON {data-name-1} ...]} ...
  [RESET ON {data-name-2}]
  [         {FINAL      }]
Syntax Rules
1.  The data item that is the subject of the report group description entry in
    which the SUM clause appears must not be defined as alphabetic.  If
    identifier-1 is defined in the Report Section, identifier-1 must reference
    a sum counter.
    If the UPON phrase is omitted, any identifiers in the associated SUM
    clause which are themselves sum counters must be defined either in the
    same report group that contains this SUM clause or in a report group which
    is at a lower level in the control hierarchy of this report.
    If the UPON phrase is specified, any identifiers in the associated SUM
    clause must not be sum counters.
2.  Data-name-1 must be the name of a DETAIL report group described in the
    same report as the CONTROL FOOTING report group in which the SUM clause
    appears.  Data-name-1 may be qualified by a report-name.
3.  A SUM clause can appear only in the description of a CONTROL FOOTING
    report clause.
4.  Data-name-2 must be one of the data-names specified in the CONTROL clause
    for this report.  Data-name-2 must not be a lower level control than the
    associated control for the report group in which the RESET phrase appears.
    FINAL, if specified in the RESET phrase, must also appear in the CONTROL
    clause for this report.
5.  The highest permissible qualifier of a sum counter is the report-name.
00001
Function
The SUPPRESS statement causes the report writer control system (RWCS) to
inhibit the presentation of a report group.
General Format
SUPPRESS PRINTING
Syntax Rule
1.  The SUPPRESS statement may only appear in a USE BEFORE REPORTING
    procedure.
00001
Function
The SYNCHRONIZED clause specifies the alignment of an elementary item on the
natural boundaries of the computer memory.
General Format
{SYNCHRONIZED} [LEFT ]
{SYNC        } [RIGHT]
Syntax Rules
1.  This clause may appear only with an elementary item.
2.  SYNC is an abbreviation for SYNCHRONIZED.
00001
Function
The TERMINATE statement causes the report writer control system (RWCS) to
complete the processing of the specified reports.
General Format
TERMINATE {report-name-1} ...
Syntax Rule
1.  Report-name-1 must be defined by a report description entry in the Report
    Section of the Data Division.
00001
Function
The TYPE clause specifies the particular type of report group that is
described by this entry and indicates the time at which the report group is to
be processed by the report writer control system (RWCS).
General Format
        {{REPORT HEADING}               }
        {{RH            }               }
        {                               }
        {{PAGE HEADING}                 }
        {{PH          }                 }
        {                               }
        {{CONTROL HEADING} {data-name-1}}
        {{CH             } {FINAL      }}
        {                               }
TYPE IS {{DETAIL}                       }
        {{DE    }                       }
        {                               }
        {{CONTROL FOOTING} {data-name-2}}
        {{CF             } {FINAL      }}
        {                               }
        {{PAGE FOOTING}                 }
        {{PF          }                 }
        {                               }
        {{REPORT FOOTING}               }
        {{RF            }               }
Syntax Rules
1.  RH is an abbreviation for REPORT HEADING.
    PH is an abbreviation for PAGE HEADING.
    CH is an abbreviation for CONTROL HEADING.
    DE is an abbreviation for DETAIL.
    CF is an abbreviation for CONTROL FOOTING.
    PF is an abbreviation for PAGE FOOTING.
    RF is an abbreviation for REPORT FOOTING.
2.  Report groups specified by REPORT HEADING, PAGE HEADING, CONTROL HEADING
    FINAL, CONTROL FOOTING FINAL, PAGE FOOTING, and REPORT FOOTING report
    groups may each appear.
3.  PAGE HEADING and PAGE FOOTING report groups may be specified only if a
    PAGE clause is specified in the corresponding report description entry.
4.  Data-name-1, data-name-2, and FINAL, if present, must be specified in the
    CONTROL clause of the corresponding report description entry.  At most,
    one CONTROL HEADING report group and one CONTROL FOOTING report group can
    be specified for each data-name or FINAL in the CONTROL clause of the
    report description entry.  However, neither a CONTROL HEADING report group
    nor a CONTROL FOOTING report group is required for a data-name or FINAL
    specified in the CONTROL clause of the report description entry.
5.  In CONTROL FOOTING, PAGE HEADING, PAGE FOOTING, and REPORT FOOTING report
    groups, SOURCE clauses and associated USE statements must not reference
    any of the following:
    a.  Group data items containing a control data item.
    b.  Data items subordinate to a control data item.
    c.  A redefinition or renaming of any part of a control data item.
    In PAGE HEADING and PAGE FOOTING report groups, SOURCE clauses and USE
    statements must not reference control data-names.
6.  When a GENERATE report-name statement is specified in the Procedure
    Division, the corresponding report description entry must include no more
    than one DETAIL report group.  If no GENERATE data-name statements are
    specified for such a report, a DETAIL report group is not required.
7.  The description of a report must include at least one body group.
00001
Function
The UNSTRING statement causes contiguous data in a sending field to be
separated and placed into multiple receiving fields.
General Format
UNSTRING identifier-1
  [DELIMITED BY [ALL] {identifier-2} [OR [ALL] {identifier-3}] ...]
  [                   {literal-1   } [         {literal-2   }]    ]
  INTO {identifier-4 [DELIMITER IN identifier-5] [COUNT IN identifier-6]} ...
  [WITH POINTER identifier-7]
  [TALLYING IN identifier-8]
  [ON OVERFLOW imperative-statement-1]
  [NOT ON OVERFLOW imperative-statement-2]
  [END-UNSTRING]
Syntax Rules
1.  Literal-1 and literal-2 must be nonnumeric literals and neither can be a
    figurative constant that begins with the word ALL.
2.  Identifier-1, identifier-2, identifier-3, and identifier-5 must reference
    data items described, implicitly or explicitly, as category alphanumeric.
3.  Identifier-4 may be described as either the category alphabetic,
    alphanumeric, or numeric (except that the symbol 'P' may not be used in
    the PICTURE character-string), and must be described implicitly or
    explicitly, as USAGE IS DISPLAY.
4.  Identifier-6 and identifier-8 must reference integer data items (except
    that the symbol 'P' may not be used in the PICTURE character-string).
5.  Identifier-7 must be described as an elementary numeric integer data item
    of sufficient size to contain a value equal to 1 plus the size of the data
    item referenced by identifier-1.  The symbol 'P' may not be used in the
    PICTURE character-string of identifier-7.
6.  The DELIMITER IN phrase and the COUNT IN phrase may be specified only if
    the DELIMITED BY phrase is specified.
7.  Identifier-1 must not be reference-modified.
00001
Function
The USAGE clause specifies the format of a data item in the computer storage.
General Format
           {BINARY           }
           {COMPUTATIONAL    }
           {COMP             }
           {COMPUTATIONAL-1  }
           {COMP-1           }
           {COMPUTATIONAL-2  }
           {COMP-2           }
           {COMPUTATIONAL-3  }
           {COMP-3           }
           {COMPUTATIONAL-4  }
           {COMP-4           }
           {COMPUTATIONAL-5  }
[USAGE IS] {COMP-5           }
           {COMPUTATIONAL-6  }
           {COMP-6           }
           {COMPUTATIONAL-7  }
           {COMP-7           }
           {COMPUTATIONAL-8  }
           {COMP-8           }
           {COMPUTATIONAL-11 }
           {COMP-11          }
           {COMPUTATIONAL-12 }
           {COMP-12          }
           {DISPLAY          }
           {EBCDIC           }
           {INDEX            }
           {PACKED-DECIMAL   }
           {POINTER          }
Syntax Rules
1.  The USAGE clause may be written in any data description entry with a
    level-number other than 66 or 88.
2.  If the USAGE clause is written in the data description entry for a group
    item, it may also be written in the data description entry for any
    subordinate elementary item or group item, but the same usage must be
    specified in both entries.
3.  An elementary data item whose declaration contains, or an elementary data
    item subordinate to a group item whose declaration contains, a USAGE
    clause specifying COMPUTATIONAL must be declared with a PICTURE
    character-string that describes a numeric item, i.e., a PICTURE
    character-string that contains only the symbols 'P', 'S', 'V', and '9'.
4.  COMP is an abbreviation for COMPUTATIONAL.  COMP-n is an abbreviation for
    COMPUTATIONAL-n.
5.  An index data item can be referenced explicitly only in a SEARCH or SET
    statement, a relation condition, the USING phrase of a PROCEDURE Division
    header, or the USING phrase of a CALL statement.
6.  The BLANK WHEN ZERO, JUSTIFIED, PICTURE, SYNCHRONIZED, and VALUE clauses
    must be not be specified for data items whose usage is INDEX.
7.  An elementary data item described with a USAGE IS INDEX clause must not be
    a conditional variable.
8.  The BLANK WHEN ZERO, JUSTIFIED, and PICTURE clauses must not be specified
    for data items whose usage is POINTER.
9.  A data item described as USAGE IS POINTER may be the subject or object of
    a REDEFINES clause.
10. A data item described as USAGE IS POINTER cannot be a conditional
    variable.
00001
Function
The USAGE clause specifies the format of a data item in the computer storage.
General Format
[USAGE IS] DISPLAY
Syntax Rules
1.  The USAGE clause may be written in any data description entry.
2.  If the USAGE clause is written in the data description entry for a group
    item, it may also be written in the data description entry for a
    subordinate elementary item or group item.
3.  The USAGE clause for a report group item can specify only USAGE IS
    DISPLAY.
00001
USAGE_CLAUSE_REPORT_WRITER
USE_SEQUENTIAL
Function
Within the Inter-Program Communication module, the USE BEFORE REPORTING
statement determines whether the associated declarative procedures are invoked
during the execution of any program contained within the program which
includes the USE BEFORE REPORTING statement.
General Format
USE [GLOBAL] BEFORE REPORTING identifier-1
General Rule
1.  Special precedence rules are followed when programs are contained within
    other programs.  In applying these rules, only the first qualifying
    declarative will be selected for execution.  The declarative which is
    selected for execution must satisfy the rules for execution of that
    declarative.  The order of precedence for selecting a declarative is:
    a.  The declarative within the program that contains the statement which
        caused the qualifying condition.
    b.  The declarative in which the GLOBAL phrase is specified and which is
        within the program directly containing the program which was last
        examined for a qualifying declarative.
    c.  Any declarative selected by applying rule 1b to each more-inclusive
        containing program until rule 1b is applied to the outermost program.
        If no qualifying declarative is found, none is executed.
00001
Function
The USE BEFORE REPORTING statement specifies Procedure Division statements
that are executed just before a report group named in the Report Section of
the Data Division is presented.
General Format
USE BEFORE REPORTING identifier-1
Syntax Rules
1.  A USE BEFORE REPORTING statement, when present, must immediately follow a
    section header in the declaratives portion of the Procedure Division and
    must appear in a sentence by itself.  The remainder of the section must
    consist of zero, one, or more procedural paragraphs that define the
    procedures to be used.
2.  Identifier-1 must reference a report group.  Identifier-1 must not appear
    in more than one USE BEFORE REPORTING statement.
3.  The GENERATE, INITIATE, or TERMINATE statements must not appear in a
    paragraph within a USE BEFORE REPORTING procedure.  A PERFORM statement in
    a USE BEFORE REPORTING procedure must not have GENERATE, INITIATE, or
    TERMINATE statements in its range.
4.  A USE BEFORE REPORTING procedure must not alter the value of any control
    data item.
5.  The USE BEFORE REPORTING statement itself is never executed; it merely
    defines the conditions calling for the execution of the USE procedures.
00001
Function
The USE statement specifies procedures for input-output error handling that
are in addition to the standard procedures provided by the input-output
control system.
General Format
                                            {{file-name-1} ...}
                                            {INPUT            }
USE AFTER STANDARD {EXCEPTION} PROCEDURE ON {OUTPUT           }
                   {ERROR    }              {I-O              }
                                            {EXTEND           }
Syntax Rules
1.  A USE statement, when present, must immediately follow a section header in
    the declaratives portion of the Procedure Division and must appear in a
    sentence by itself.  The remainder to the section must consist of zero,
    one, or more procedural paragraphs that define the procedures to be used.
2.  The USE statement is never executed; it merely defines the conditions
    calling for the execution of the USE procedures.
3.  Appearance of file-name-1 in a USE statement must not cause the
    simultaneous request for execution of more than one USE procedure.
4.  The words ERROR and EXCEPTION are synonymous and may be used
    interchangeably.
5.  The files implicitly or explicitly referenced in the USE statement need
    not all have the same organization or access.
6.  The INPUT, OUTPUT, I-O, and EXTEND phrases may each be specified only once
    in the declaratives portion of a given Procedure Division.
00001
Function
Within the Inter-Program Communication module, the USE statement determines
whether the associated declarative procedures are invoked during the execution
of any program contained within the program which includes the USE statement.
General Format
                                                     {{file-name-1} ...}
                                                     {INPUT            }
USE [GLOBAL] AFTER STANDARD {EXCEPTION} PROCEDURE ON {OUTPUT           }
                            {ERROR    }              {I-O              }
                                                     {EXTEND           }
General Rule
1.  Special precedence rules are followed when programs are contained within
    other programs.  In applying these rules, only the first qualifying
    declarative will be selected for execution.  The declarative which is
    selected for execution must satisfy the rules for execution of that
    declarative.  The order of precedence for selecting a declarative is:
    a.  The declarative within the program that contains the statement which
        caused the qualifying condition.
    b.  The declarative in which the GLOBAL phrase is specified and which is
        within the program directly containing the program which was last
        examined for a qualifying declarative.
    c.  Any declarative selected by applying rule 1b to each more-inclusive
        containing program until rule 1b is applied to the outermost program.
        If no qualifying declarative is found, none is executed.
00001
Function
The USE statement specifies procedures for input-output error handling that
are in addition to the standard procedures provided by the input-output
control system.
General Format
                                            {file-name-1 ...}
                                            {INPUT          }
USE AFTER STANDARD {EXCEPTION} PROCEDURE ON {OUTPUT         }
                   {ERROR    }              {I-O            }
                                            {EXTEND         }
Syntax Rules
1.  A USE statement, when present, must immediately follow a section header in
    the declaratives portion of the Procedure Division and must appear in a
    sentence by itself.  The remainder of the section must consist of zero,
    one, or more procedural paragraphs that define the procedures to be used.
2.  The USE statement is never executed; it merely defines the conditions
    calling for the execution of the USE procedures.
3.  Appearance of file-name-1 in a USE statement must not cause the
    simultaneous request for execution of more than one USE procedure.
4.  The words ERROR and EXCEPTION are synonymous and may be used
    interchangeably.
5.  The files implicitly or explicitly referenced in the USE statement need
    not all have the same organization or access.
6.  The INPUT, OUTPUT, I-O, and EXTEND phrases may each be specified only once
    in the declaratives portion of a given Procedure Division.
00001
Function
The USE statement specifies procedures for input-output error handling that
are in addition to the standard procedures provided by the input-output
control system.
General Format
                                            {file-name-1 ...}
                                            {INPUT          }
USE AFTER STANDARD {EXCEPTION} PROCEDURE ON {OUTPUT         }
                   {ERROR    }              {I-O            }
                                            {EXTEND         }
Syntax Rules
1.  A USE statement, when present, must immediately follow a section header in
    the declaratives portion of the Procedure Division and must appear in a
    sentence by itself.  The remainder of the section must consist of zero,
    one, or more procedural paragraphs that define the procedures to be used.
2.  The USE statement is never executed; it merely defines the conditions
    calling for the execution of the USE procedures.
3.  Appearance of file-name-1 in a USE statement must not cause the
    simultaneous request for execution of more than one USE procedure.
4.  The words ERROR and EXCEPTION are synonymous and may be used
    interchangeably.
5.  The files implicitly or explicitly referenced in the USE statement need
    not all have the same organization or access.
6.  The INPUT, OUTPUT, I-O, and EXTEND phrases may each be specified only once
    in the declaratives portion of a given Procedure Division.
00001
Function
The USE AFTER STANDARD EXCEPTION PROCEDURE statement specifies procedures for
input-output error handling that are in addition to the standard procedures
provided by the input-output control system.
General Format
                                            {{file-name-1} ...}
USE AFTER STANDARD {EXCEPTION} PROCEDURE ON {OUTPUT           }
                   {ERROR    }              {EXTEND           }
Syntax Rules
1.  A USE statement, when present, must immediately follow a section header in
    the declaratives portion of the Procedure Division and must appear in a
    sentence by itself.  The remainder of the section must consist of zero,
    one, or more procedural paragraphs that define the procedure to be used.
2.  The USE statement is never executed; it merely defines the conditions
    calling for the execution of the USE procedures.
3.  Appearance of file-name-1 in a USE statement must not cause the
    simultaneous request for execution of more than one USE procedure.
4.  The words ERROR and EXCEPTION are synonymous and may be used
    interchangeably.
5.  The files implicitly or explicitly referenced in the USE statement need
    not all have the same organization or access.
6.  The OUTPUT and EXTEND phrases may each be specified only once in the
    declaratives portion of a given Procedure Division.
00001
Function
The USE statement specifies procedures for input-output error handling that
are in addition to the standard procedures provided by the input-output
control system.
General Format
                                            {{file-name-1} ...}
                                            {INPUT            }
USE AFTER STANDARD {EXCEPTION} PROCEDURE ON {OUTPUT           }
                   {ERROR    }              {I-O              }
                                            {EXTEND           }
Syntax Rules
1.  A USE statement, when present, must immediately follow a section header in
    the declarative portion of the Procedure Division and must appear in a
    sentence by itself.  The remainder of the section must consist of zero,
    one, or more procedural paragraphs that define the procedures to be used.
2.  The USE statement is never executed; it merely defines the conditions
    calling for the execution of the USE procedures.
3.  Appearance of file-name-1 in a USE statement must not cause the
    simultaneous request for execution of more than one USE procedure.
4.  The words ERROR and EXCEPTION are synonymous and may be used
    interchangeably.
5.  The files implicitly or explicitly referenced in the USE statement need
    not all have the same organization or access.
6.  The INPUT, OUTPUT, I-O, and EXTEND phrases may each be specified only once
    in the declaratives portion of a given Procedure Division.
00001
Function
The VALUE clause defines the initial value of Working-Storage Section and File
Section data items, and the values associated with condition-names.
General Format
Format 1:
VALUE IS literal-1
Format 2:
{VALUE IS  } {literal-2 [{THROUGH} literal-3]} ...
{VALUES ARE} {          [{THRU   }          ]}
Format 3:
VALUE IS NULL
Syntax Rules
1.  The words THROUGH and THRU are equivalent.
2.  A signed numeric literal must have associated with it a signed numeric
    PICTURE character-string.
3.  All numeric literals in a VALUE clause of an item must have a value which
    is within the range of values indicated by the PICTURE clause, and must
    not have a value which would require truncation of nonzero digits.
    Nonnumeric literals in a VALUE clause of an item must not exceed the size
    indicated by the PICTURE clause.
4.  The VALUE clause must not be specified in any entry which is part of the
    description or redefinition of an external data record.  The VALUE clause
    may be specified for condition-name entries associated with such data
    description entries.
5.  A pointer data item may be initialized to contain a NULL pointer with a
    VALUE IS NULL clause in its data definition.
00001
Function
The VALUE clause defines the value of Report Section printable items.
General Format
VALUE IS literal-1
Syntax Rules
1.  A signed numeric literal must have associated with it a signed numeric
    PICTURE character-string.
2.  A numeric literal in a VALUE clause of an item must have a value which is
    within the range of values indicated by the PICTURE clause, and must not
    have a value which would require truncation of nonzero digits.  A
    nonnumeric literal in a VALUE clause of an item must not exceed the size
    indicated by the PICTURE clause.
00001
Function
The VALUE OF clause in the FD entry specifies the expected or desired contents
of the file identification and/or retention fields of the file labels.
General Format
         {RETENTION}    {data-name-1}
VALUE OF {FILE-ID  } IS {literal-1  }
         {FILE-NAME}
Syntax Rules
1.  Data-name-1, etc., should be qualified when necessary, but cannot be
    subscripted or indexed, nor can they be items described with the USAGE IS
    INDEX clause.
2.  Data-name-1, etc., must be specified in the Working-Storage Section.
3.  If a data-name is specified for the RETENTION phrase, it must be described
    as an unsigned numeric DISPLAY with a maximum size of three digits.
4.  If a literal is specified for the RETENTION phrase, it must be described
    as an unsigned numeric with a maximum value of 999.
5.  If a data-name is specified for the VALUE phrase, it must be described as
    an alphanumeric string with a maximum length of 31 characters.
6.  If a literal is specified for the VALUE phrase, it must be described as an
    alphanumeric string with a maximum length of 31 characters.
00001
VALUE_CLAUSE_REPORT_WRITER
    The Working-Storage Section is located in the Data Division of a source
    program.  The Working-Storage Section describes records and subordinate
    data items which are not part of data files.
    The Working-Storage Section is composed of the section header, followed by
    record description entries and/or data description entries for
    noncontiguous data items.
General Format
 WORKING-STORAGE SECTION.
[77-level-description-entry] ...
[record-description-entry  ]
WRITE_SEQUENTIAL
Function
The WRITE statement releases a logical record for an output or input-output
file.
General Format
WRITE record-name-1 [FROM identifier-1]
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-WRITE]
Syntax Rules
1.  Record-name-1 and identifier-1 must not refer to the same storage area.
2.  Record-name-1 is the name of a logical record in the File Section of the
    Data Division and may be qualified.
3.  The INVALID KEY phrase must be specified if an applicable USE AFTER
    STANDARD EXCEPTION procedure is not specified for the associated
    file-name.
00001
Function
The WRITE statement releases a logical record for an output or input-output
file.
General Format
WRITE record-name-1 [FROM identifier-1]
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-WRITE]
Syntax Rules
1.  Record-name-1 and identifier-1 must not refer to the same storage area.
2.  Record-name-1 is the name of a logical record in the File Section of the
    Data Division and may be qualified.
3.  The INVALID KEY phrase must be specified if an applicable USE AFTER
    STANDARD EXCEPTION procedure is not specified for the associated
    file-name.
00001
Function
The WRITE statement releases a logical record for an output or input-output
file.
General Format
WRITE record-name-1 [FROM identifier-1]
  [INVALID KEY imperative-statement-1]
  [NOT INVALID KEY imperative-statement-2]
  [END-WRITE]
Syntax Rules
1.  Record-name-1 and identifier-1 must not refer to the same storage area.
2.  Record-name-1 is the name of a logical record in the File Section of the
    Data Division and may be qualified.
3.  The INVALID KEY phrase must be specified if an applicable USE AFTER
    STANDARD EXCEPTION procedure is not specified for the associated
    file-name.
00001
Function
The WRITE statement releases a logical record for an output file.  It can also
be used for vertical positioning of lines within a logical page.
General Format
WRITE record-name-1 [FROM identifier-1]
  [                   {{identifier-2} [LINE ]}]
  [                   {{integer-1   } [LINES]}]
  [{BEFORE} ADVANCING {                      }]
  [{AFTER }           {{mnemonic-name-1}     }]
  [                   {{PAGE           }     }]
  [AT {END-OF-PAGE} imperative-statement-1]
  [   {EOP        }                       ]
  [NOT AT {END-OF-PAGE} imperative-statement-2]
  [       {EOP        }                       ]
  [END-WRITE]
Syntax Rules
1.  Record-name-1 is the name of a logical record in the File Section of the
    Data Division and may be qualified.
2.  The ADVANCING mnemonic-name-1 phrase cannot be specified when writing a
    record to a file which is associated with a file description entry
    containing a LINAGE clause.
3.  Identifier-2 must reference an integer data item.
4.  Integer-1 may be positive or zero, but must not be negative.
5.  When mnemonic-name-1 is specified, the name must be associated with a
    single character non-numeric literal which is defined in the SPECIAL-NAMES
    paragraph of the Environment Division.  This is the VFC character to be
    used to format the printed output.  VFC characters are found in the guide.
6.  The phrases ADVANCING PAGE and END-OF-PAGE must not both be specified in a
    single WRITE statement.
7.  If the END-OF-PAGE or NOT END-OF-PAGE phrase is specified, the LINAGE
    clause must be specified in the file description entry for the associated
    file.
8.  The words END-OF-PAGE and EOP are equivalent.
00001
Format
CALL "X9MA$ALLOCATE" USING
                  {identifier-1           }
   [BY REFERENCE] {                       }
                  {ADDRESS OF identifier-2}
    {BY CONTENT LENGTH OF identifier-3}
    {                                 }
    {[BY CONTENT] identifier-4        }
General Rules
1.  X9MA$ALLOCATE is an entry point of the run time heap management support
    routine.  With this call, the heap management routine allocates a piece of
    free heap space from the heap storage.  The length of the heap space to be
    allocated is described in the second argument.  The address of the
    allocated heap space is then stored in the first argument.
2.  The first argument of the call to X9MA$ALLOCATE must be a pointer data
    item and passed by reference implicitly or explicitly.  The second
    argument must be a comp-6 data item which contains a value range from 1 to
    1020K.  The value denotes the length in number of bytes.  1020K bytes is
    the maximum length of a level 01 or 77 based variable.
3.  Identifier-1 must be an elementary data item which is described as USAGE
    IS POINTER.
4.  Identifier-2 must be a level 01 or 77 item in the LINKAGE SECTION.  In
    this case, the address base register of identifier-2 is passed as the
    first argument.
5.  Identifier-4 must be an elementary data item which is described as USAGE
    IS COMP-6.
6.  The total heap storage that may be allocated by one process is 16
    megabytes.
00001
Format
CALL "X9MA$FREE" USING
                   {identifier-1           }
    [BY REFERENCE] {                       }
                   {ADDRESS OF identifier-2}
General Rules
1.  X9MA$FREE is an entry point of the run time heap management routine.  With
    this call, the heap manager returns the heap space, which is pointed to by
    the argument, to the heap.  Once the heap space is returned, it may be
    reused again.
2.  For this CALL statement, the argument must describe a pointer data item
    which points to a piece of heap space to be returned to the heap.
3.  Identifier-1 must be an elementary data item which is described as USAGE
    IS POINTER.
4.  Identifier-2 must be a level 01 or 77 item in the LINKAGE SECTION.  In
    this case, the address base register of identifier-2 is passed as the
    argument.
5.  The argument is reset to the NULL address by the heap manager after the
    heap space is returned.
6.  Only those heap spaces allocated through the call to X9MA$ALLOCATE may be
    returned through the call to X9MA$FREE.
00001
.CDAT4
