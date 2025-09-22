A HELP facility for FEP monitor services includes as topics all services and 
related structures.  This HELP facility is available through IBEX or any 
system processor.  For more information, enter: 
HELP (FEPMON) TOPICS             For a list of topics 
HELP (FEPMON) TOPICS keyword1    For a list of subtopics for a specific 
                                 service or structure 
HELP (FEPMON) keyword1           For a description of the specified 
                                 service or structure 
HELP (FEPMON) keyword1 keyword2  For a description of a specific 
                                 parameter or field (keyword2) for a 
                                 a specified service or structure (keyword1) 
For example, to display all subtopics for M$DCB, enter: 
HELP (FEPMON) M$DCB TOPICS 
Then to display a specific parameter of M$DCB, STRM, for example, enter: 
HELP (FEPMON) M$DCB STRM 
In addition, once a HELP information message is requested, entering 
?            displays the next level of HELP message 
??           displays all subsequent levels of the HELP message. 
Information on notation and conventions is contained in the topics NOTATION, 
PARAMETER_CONVENTIONS, and FIELD_CONVENTIONS. 
For complete information on the HELP command, enter: HELP HELP 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
Most of the following information is in GH_LCP6_M, but included here.  Figure 
H-1 is a DRAW of the AUTO structure.  The layout of automatic storage which is 
assumed by the calling/receiving sequences is as follows: 
1.  T controls all of Automatic Storage. 
2.  B7 locates the current external frame which may include several internal 
    frames. 
3.  Static (NOAUTO) frames have the same format as auto frames. 
4.  The external frame is defined by the G$FRAME macro; see "G$FRAME 
    Structure" later in this section. 
5.  The base of the automatic storage segment contains certain global 
    information about all of automatic storage.  It, for example, locates the 
    stack head and the bottom frame, and also defines the type of stack.  The 
    first fifteen words are described in the G$BASE macro, which is discussed 
    later in this section. 
6.  As AUTOmatic storage is used, additional frames are allocated within the 
    currently allocated portion of the AUTO segment to the extent possible. 
    When a new frame cannot be allocated, the AUTO segment is extended and the 
    AUTO head and BASE are updated.  The G$AUTO_HEAD macro is illustrative; 
    see "G$AUTO_HEAD Structure" later in this section. 
7.  Figure H-1 gives a picture of AUTO storage as a whole.  The 
    MONITOR_AUTO_LAYOUT and USER_AUTO_LAYOUT macros have no operational value, 
    but describe the layout of the entire automatic storage segment. 
                             MONITOR_AUTO_LAYOUT 
       01234567 01234567 
      +--------+--------+ DCL 
   .0 |        |        | 1 MONITOR_AUTO_LAYOUT BASED, 
   .0 |        |        |   2 FPTN, 
   .0 |pppppppp|pppppppp|     3 CUR_T_REG   PTR, 
   .1 |pppppppp|pppppppp| 
   .2 |        |        |     3 BOTTOM_FRAME$ 
   .2 |pppppppp|pppppppp|                   PTR, 
   .3 |pppppppp|pppppppp| 
   .4 |uuuuuuuu|uuuuuuuu|     3 AUTO_TYPE   UBIN, 
   .5 |pppppppp|pppppppp|     3 SPARE(0:4)  PTR, 
   .6 |pppppppp|pppppppp| 
      Z        Z        Z 
   .F |        |        |   2 AVAILABLE(0:63) 
   .F |uuuuuuuu|uuuuuuuu|                   UBIN, 
      Z        Z        Z 
  .4F |uuuuuuuu|uuuuuuuu|   2 FR_3_SIZE     UBIN, 
  .50 |        |        |   2 FPTN, 
  .50 |eeeeeeee|eeeeeeee|     3 RET_ADDR    EPTR, 
  .51 |eeeeeeee|eeeeeeee| 
  .52 |uuuuuuuu|uuuuuuuu|     3 TYPE        UBIN, 
  .53 |uuuuuuuu|uuuuuuuu|     3 PREV_FR_SIZ UBIN, 
  .54 |pppppppp|pppppppp|     3 PARAMS(0:0) PTR, 
  .55 |pppppppp|pppppppp| 
  .56 |        |        |     3 VAR_TEMP(0:24) 
  .56 |uuuuuuuu|uuuuuuuu|                   UBIN, 
      Z        Z        Z 
  .6F |uuuuuuuu|uuuuuuuu|   2 FR_2_SIZE     UBIN, 
  .70 |        |        |   2 FPTN, 
  .70 |eeeeeeee|eeeeeeee|     3 RET_ADDR    EPTR, 
  .71 |eeeeeeee|eeeeeeee| 
  .72 |uuuuuuuu|uuuuuuuu|     3 TYPE        UBIN, 
  .73 |uuuuuuuu|uuuuuuuu|     3 PREV_FR_SIZ UBIN, 
  .74 |pppppppp|pppppppp|     3 PARAMS(0:0) PTR, 
  .75 |pppppppp|pppppppp| 
  .76 |        |        |     3 VAR_TEMP(0:24) 
  .76 |uuuuuuuu|uuuuuuuu|                   UBIN, 
      Z        Z        Z 
  .8F |uuuuuuuu|uuuuuuuu|   2 FR_1_SIZE     UBIN, 
  .90 |        |        |   2 FPTN, 
  .90 |eeeeeeee|eeeeeeee|     3 RET_ADDR    EPTR, 
  .91 |eeeeeeee|eeeeeeee| 
  .92 |uuuuuuuu|uuuuuuuu|     3 TYPE        UBIN, 
  .93 |uuuuuuuu|uuuuuuuu|     3 PREV_FR_SIZ UBIN, 
  .94 |pppppppp|pppppppp|     3 PARAMS(0:0) PTR, 
  .95 |pppppppp|pppppppp| 
  .96 |        |        |     3 VAR_TEMP(0:24) 
  .96 |uuuuuuuu|uuuuuuuu|                   UBIN, 
      Z        Z        Z 
  .AF |        |        |   2 FPTN, 
  .AF |uuuuuuuu|uuuuuuuu|     3 CUR_USED    UBIN, 
  .B0 |uuuuuuuu|uuuuuuuu|     3 MAX_ALLOWED UBIN, 
  .B1 |        |        |     3 MUST_BE_NIL(0:1) 
  .B1 |pppppppp|pppppppp|                   PTR; 
  .B2 |pppppppp|pppppppp| 
      Z        Z        Z 
      +--------+--------+ 
       01234567 01234567   .B5-0-0 total length 
                               USER_AUTO_LAYOUT 
       01234567 01234567 
      +--------+--------+ DCL 
   .0 |        |        | 1 USER_AUTO_LAYOUT BASED, 
   .0 |        |        |   2 FPTN, 
   .0 |pppppppp|pppppppp|     3 CUR_T_REG   PTR, 
   .1 |pppppppp|pppppppp| 
   .2 |        |        |     3 BOTTOM_FRAME$ 
   .2 |pppppppp|pppppppp|                   PTR, 
   .3 |pppppppp|pppppppp| 
   .4 |uuuuuuuu|uuuuuuuu|     3 AUTO_TYPE   UBIN, 
   .5 |pppppppp|pppppppp|     3 SPARE(0:4)  PTR, 
   .6 |pppppppp|pppppppp| 
      Z        Z        Z 
   .F |uuuuuuuu|uuuuuuuu|   2 FR_1_SIZE     UBIN, 
  .10 |        |        |   2 FPTN, 
  .10 |eeeeeeee|eeeeeeee|     3 RET_ADDR    EPTR, 
  .11 |eeeeeeee|eeeeeeee| 
  .12 |uuuuuuuu|uuuuuuuu|     3 TYPE        UBIN, 
  .13 |uuuuuuuu|uuuuuuuu|     3 PREV_FR_SIZ UBIN, 
  .14 |pppppppp|pppppppp|     3 PARAMS(0:0) PTR, 
  .15 |pppppppp|pppppppp| 
  .16 |        |        |     3 VAR_TEMP(0:24) 
  .16 |uuuuuuuu|uuuuuuuu|                   UBIN, 
      Z        Z        Z 
  .2F |uuuuuuuu|uuuuuuuu|   2 FR_2_SIZE     UBIN, 
  .30 |        |        |   2 FPTN, 
  .30 |eeeeeeee|eeeeeeee|     3 RET_ADDR    EPTR, 
  .31 |eeeeeeee|eeeeeeee| 
  .32 |uuuuuuuu|uuuuuuuu|     3 TYPE        UBIN, 
  .33 |uuuuuuuu|uuuuuuuu|     3 PREV_FR_SIZ UBIN, 
  .34 |pppppppp|pppppppp|     3 PARAMS(0:0) PTR, 
  .35 |pppppppp|pppppppp| 
  .36 |        |        |     3 VAR_TEMP(0:24) 
  .36 |uuuuuuuu|uuuuuuuu|                   UBIN, 
      Z        Z        Z 
  .4F |uuuuuuuu|uuuuuuuu|   2 FR_3_SIZE     UBIN, 
  .50 |        |        |   2 FPTN, 
  .50 |eeeeeeee|eeeeeeee|     3 RET_ADDR    EPTR, 
  .51 |eeeeeeee|eeeeeeee| 
  .52 |uuuuuuuu|uuuuuuuu|     3 TYPE        UBIN, 
  .53 |uuuuuuuu|uuuuuuuu|     3 PREV_FR_SIZ UBIN, 
  .54 |pppppppp|pppppppp|     3 PARAMS(0:0) PTR, 
  .55 |pppppppp|pppppppp| 
  .56 |        |        |     3 VAR_TEMP(0:24) 
  .56 |uuuuuuuu|uuuuuuuu|                   UBIN, 
      Z        Z        Z 
  .6F |        |        |   2 AVAILABLE(0:63) 
  .6F |uuuuuuuu|uuuuuuuu|                   UBIN, 
      Z        Z        Z 
  .AF |        |        |   2 FPTN, 
  .AF |uuuuuuuu|uuuuuuuu|     3 CUR_USED    UBIN, 
  .B0 |uuuuuuuu|uuuuuuuu|     3 MAX_ALLOWED UBIN, 
  .B1 |        |        |     3 MUST_BE_NIL(0:1) 
  .B1 |pppppppp|pppppppp|                   PTR; 
  .B2 |pppppppp|pppppppp| 
      Z        Z        Z 
      +--------+--------+ 
       01234567 01234567   .B5-0-0 total length 
The B$TERMINAL_ID macro may be used to define a structure containing terminal 
identification information.  The subfields which may be specified are: 
    LEV = {1|2|3}.  Specifies whether TERM.SUBDEVICE and TERM.SUBSUBDEVICE are 
    meaningful. 
    1 - TERM.SUBDEVICE and TERM.SUBSUBDEVICE are not meaningful 
    2 - TERM.SUBDEVICE is meaningful; TERM.SUBSUBDEVICE 
        is not meaningful 
    3 - TERM.SUBDEVICE and TERM.SUBSUBDEVICE are meaningful 
    For HASP stations, LEV=2, i.e., TERM.SUBDEVICE is valid.  For IBM 
    3270-like devices, LEV=3; TERM.SUBDEVICE identifies the controller and 
    TERM.SUBSUBDEVICE identifies a specific 3270-like terminal device. 
    TERM.CHANNEL = VALUE-DEC(0-65535).  Specifies the port to which the 
    terminal is most directly connected. 
    TERM.SUBDEVICE = VALUE-DEC(0-65535).  Specifies the CP-6 subdevice or 
    controller number, assigned by SUPER when the device or controller was 
    defined. 
    TERM.SUBSUBDEVICE = VALUE-DEC(0-65535).  Specifies the device port through 
    which the terminal is connected to its controller. 
    TERM.TERM_NAME = VALUE-CHAR(8).  Specifies the terminal name specified to 
    SUPER by the system manager. 
    TERMID = VALUE-CHAR(14).  Is a REDEF of TERM and is used when TTYP is 
    KLTY_PROG#.  TERMID will contain the user name from G$JIT.UNAME, or when 
    the connection is being made by the LCP-6 monitor, will contain 'BABOON'. 
    TTYP = OPTION.  Specifies the terminal type.  EQUs for terminal types are 
    listed in the table. 
  Identifier                    Meaning 
KLTY_3270#                    3270 Line. 
KLTY_CONT#                    Controller for 3270. 
KLTY_FEP#                     FEP node. 
KLTY_HIP_CONT#                Controller for Polled VIP. 
KLTY_HIP_DEV#                 Device for Polled VIP. 
KLTY_HIP_LINE#                Communication Line for Polled VIP. 
KLTY_LINEDEV#                 Device for 3270. 
KLTY_LINK#                    X25 - Link Line. 
KLTY_LINKDEV#                 Communication Line Device for LINK. 
KLTY_PROG#                    FEP Program - No PROFILE. 
KLTY_SDEV#                    Terminal type SYNC device (SUB-DEV). 
KLTY_STRM#                    Terminal type SYNC terminal. 
KLTY_TTY#                     Terminal type TTY. 
KLTY_URP#                     FEP Unit Record Peripheral. 
KLTY_VIRCIR#                  Virtual Circuit Device. 
00001
00002
00003
00004
00005
00006
00007
All calls to external unknown routines must use the following formats.  Calls 
to routines for performing intrinsic functions or to internal (well known) 
subroutines may deviate as required.  PL-6 will use the described calling 
sequence for all external subroutine calls (except monitor calls). 
The basic form of the call is as follows: 
    Instruction             Comment 
    -----------             ------- 
    [LAB,B3    PTR_LIST]    list of pointers to actual 
                            arguments. 
     LAB,B4    DESC_LIST    descriptors of actual 
                            arguments. 
     LNJ,B6    routine 
     DC        altret,PREL  Contains 1 if no ALTRET 
where: 
PTR_LIST    is the list of PTRs and/or CPTRs to actual arguments being passed. 
This list of pointers is made up as necessary depending on the complexity of 
the call.  When all arguments being passed are in STATIC or CONSTANT storage, 
the list should be compiled as a block of literals in constant storage.  The 
list must be word aligned. 
DESC_LIST    defines the number of arguments being passed, and optionally 
describes them in terms of data type, size, etc.  The list must be word 
aligned.  The number of arguments must be specified.  The format of the 
description list at its present state of definition is as follows: 
                 ____________________________________ 
     DESC_LIST   _# of arguments | # of descriptions| 
                  0             7 8               15 
The following PL-6 data types are defined in PL-6 terms for conciseness of 
expression.  This does not imply that these field names will have any special 
significance or that the fields will be individually referenceable, although 
they will in some cases. 
 DCL 1 PTR,                     /*Pointer to ALIGNED item*/ 
       2 MBZ BIT(12),             /*Must be zero*/ 
       2 ADDRESS BIT(20);         /*Word Address*/ 
 DCL 1 CPTR,                    /*Pointer to CALIGNED item*/ 
       2 CHAR_OFFSET BIT(1),      /*Character Offset in Word*/ 
       2 MBZ BIT(11),             /*Must be zero*/ 
       2 ADDRESS BIT(20);         /*Word Address*/ 
 DCL 1 EPTR,                      /*Entry Pointer*/ 
       2 MBZ BIT(12),             /*Must be zero*/ 
       2 ADDRESS BIT(20);         /*Word Address of Procedure*/ 
 DCL 1 VECTOR ALIGNED,            /*Vector for framing storage 
                                    area.  Note word alignment 
                                    is minimum*/ 
       2 VBOUND UBIN,             /*PINCRC (VECTOR.VBASE, 
                                    VECTOR.VBOUND) yields 
                                    CPTR to last byte framed*/ 
       2 VBASE CPTR;              /*CPTR to first byte framed*/ 
 DCL 1 REMEMBER ALIGNED,          /*Variable to be used in 
                                    REMEMBER and UNWIND 
                                    statements*/ 
       2 AUTO PTR,                /*Auto pointer (B7) at the 
                                    time the REMEMBER statement 
                                    is executed*/ 
       2 STMT EPTR;               /*Address of the statement 
                                    remembered*/ 
Note also that ADDR(NIL), ENTADDR(NIL), and VECTOR(NIL) all have 0 values. 
VECTOR(ERASE) has VBOUND of 1 and VBASE of 0. 
Changes to FEP Monitor Services are listed below: 
IO Services 
  M$DCB - DISP:  new parameter.  ACTPOS field description now documented. 
  M$OPEN - DISP:  new parameter. 
  M$CLOSE - DISP:  default is DESTROY. 
  M$READ - KEYS:  sentence on FORM access added. 
    - READMLT:  new parameter. 
  M$WRITE - EOM:  new parameter. 
    - EOMCHAR:  new parameter. 
  VLP_CG - STATION:  corrected to read "STATION may be wildcarded.." 
Memory Management Services 
  Introduction:  correction - "big segments, allocated..." 
  M$GDS - PAGES:  range of value for PAGES corrected to 0 - n. 
  M$FDS - PAGES:  range of values for PAGES corrected to 0 - n. 
  VLP_SEGMENT:  BASE may also be initialized to a value. (D00) 
Program Management Services 
  M$LDTRC - DISP:  new parameter. 
Terminal Services 
  FORM Access Method - new discussion includes "Defining the Form and its 
      Fields", "Manipulating the Form", "Form Escape and Control Sequences". 
  M$PROMPT and M$GPROMPT - PROMPT:  maximum prompt length raised to 94 
      characters. 
  VLP_EOMTABLE - Introduction:  note added on use of "Special Characters" as 
      activation characters. 
  M$TRMPRG - CURSORHERE:  new parameter. 
  VLP_TRMCTL - ADJTOPLFT, PARKCURSOR - new fields. 
  VLP_LINEATTR - MICROFPL:  new field. 
  VLP_TRMATTR - CHARSETNAME:  new options EBCE, BIT, 3270EUR.  Options 
      previously available but undocumented:  EBC, HISI, HISO, HIS, XDS. 
    - FCNTBL:  new option, SE2, for read-only screen editing access mode. 
      CP5, CP5S1, SE1 include the numeric escapes C, D, H, M; CP5S1 includes 
      numeric escapes C, D (D00).  All function tables have new numeric 
      escape, . (dot).  FRM1 has several numeric escapes, including a new one, 
      I.  Various corrections were made to "Escape Characters" and "Special 
      Characters" for all the tables. 
    - New parameters:  FF_INCCR, MICROFPL. 
  M$DCLFLD - additions to introduction, for clarity. 
  M$MDFFLD - FLDATR:  field is required (document correction). 
    - KEY:  field is 18 bits and CALIGNED. 
    - KEYTYPE:  text added to description. 
  M$SLCFLD - additions to introduction. 
    - KEY:  field is 18 bits and CALIGNED. 
  M$RLSFLD - additions to introduction. 
    - KEY:  field is 18 bits and CALIGNED. 
  M$ERASE - KEY:  field is 18 bits and CALIGNED. 
Exceptional Condition Services 
  G$ECCB - new help topic added for G$ECCB; manual unchanged. 
  M$EVENT - Service description:  additional value for TRLR.SUBC is 
        %G_IO_CMP#     5      IO Complete 
User Context Data 
  G$ROS - AUTO_DS$, AUTO_T$:  new fields. 
  G$JIT - JUNK.KEEP, JUNK2, JUNK2.BYPASS_MFPL, JUNK2.MICROFPL:  new fields. 


The macros for VLRs and the user context structure do not provide for 
specification of initial values.  Descriptions of the fields within the 
structure generated by the macro are shown in the format 
"fieldname - data_type [(size)]" throughout this manual. 
If an ASYNC procedure must specify an FPT to exit, it can do so while allowing 
the AUTO stack to be properly cleaned up as follows: 
For M$INTRET,      CALL X6A_INTRET (FPT) 
For M$TRTN,        CALL X6A_TRTN (FPT) 
For M$MERCS,       CALL X6A_MERCS (FPT) 
The G$ASDT macro may be used to generate an array of uninitialized segment 
descriptors. 
The G$ASDT_USR macro may be used to generate a structure defining the user's 
Address Space Descriptor Table. 
This macro is used to describe the header portion of automatic storage. The T 
register will point to this header.  The meaning is different for the two 
formats. 
    CUR_USED - UBIN.  This field is the 'current used' field maintained by the 
    stack hardware.  Its meaning is dependent on the type of auto stack. For 
    both types, this field locates the current top frame. However, for the 
    fixed type of stack, this also indicates the amount of auto space 
    currently in use. But for the variable type of stack, this field minus 
    current frame size is the current amount available for allocation. 
    MAX_ALLOWED - UBIN.  This field contains the maximum amount of space 
    currently allocated for auto storage. This includes the space currently in 
    use. 
    MUST_BE_NIL - PTR Array.  These fields are reserved for future use and 
    must contain NIL pointers. 
00001
00002
00003
The G$BASE macro can be used to generate a description of the base of the 
automatic storage segment. 
    AUTO_TYPE - UBIN.  This field indicates which type of auto stack this is. 
    There are two types of auto stack because of interaction between the 
    memory management hardware and the stack hardware. This field takes on two 
    values. AUTO_TYPE = 0 indicates a 'fixed' type of auto stack which cannot 
    be expanded.  This type has the following characteristics: 
    1) It is managed by X6A$CSEQM. 
    2) It is used primarily by the monitor. 
    3) No further storage can be allocated for new demands. 
    4) Frames are added using ACQ. 
    5) Frames are removed using RLQ. 
    AUTO_TYPE = 1 indicates a 'variable' type of auto stack which can be 
    expanded (up to 64kw) as needed. This type has the following 
    characteristics: 
    1) It is managed by X6A$CSEQU. 
    2) It is used by user programs, handlers, etc. 
    3) Storage is allocated as needed. 
    4) Frames are added using RLQ. 
    5) Frames are removed using ACQ. 
    BOTTOM_FRAME$ - PTR.  This field always contains a pointer to the bottom 
    frame of the auto stack, which is usually a frame for a MAIN procedure. 
    CUR_T_REG - PTR.  This field always contains the pointer which is the 
    proper contents of the T (stack) register. 
00001
00002
00003
The G$COMIO macro may be used to generate a based structure of a frame placed 
on the TCB stack for a communications I/O event.  All the fields in the 
G$COMIO structure are identical to those in G$EXCFR. 
Of special interest here is G$COMIO.TRLR.EVID which will contain the event ID 
as was specified on the M$OPEN service request. 
The standard exceptional condition frame is then followed by: 
    ARS - UBIN contains the actual record size. This is the size of the record 
    available for a %G_DATA_AVL# event or the size of the read buffer for a 
    %G_DATA_RQS# event. 
00001
The G$DCBTABLE may be used to generate the DCB Table, which is simply an array 
of pointers that contains the addresses of each allocated DCB.  This table may 
be accessed via the pointer at G$ROS.DCBPTR$. 
The G$DEV macro may be used to generate a structure for the Device word that 
is stored in the Interrupt Save Area. 
The fields within DEV are: 
    CHN - UBIN(10) contains the interrupting channel.  The default is 0. 
    IL - UBIN(6) contains the Interrupting Level number.  The default is 0. 
00001
00002
The monitor maintains an Exceptional Condition Control Block (ECCB) for each 
domain in the user's Read Only Segment. The ECCB contains the entry points of 
the procedure to be entered when one of the Exceptional Condition occurs.  It 
also contains control flags used by the monitor when giving exceptional 
condition control to the user. 
The G$ECCB macro may be used to generate a structure of the ECCB.  The ECCB 
may be addressed by using the U_ECCB$ pointer which is within the user's Read 
Only Segment.  Please refer to the description of the G$ROS macro elsewhere in 
this manual for details on accessing data within the Read Only Segment. 
The subfields within G$ECCB have the following meaning: 
    EVENT$ - EPTR contains the address of the procedure to be entered on event 
    completion. 
    FLAGS is a bit field that contains the bit settings used by the monitor 
    for Exceptional Condition control as follows: 
    FLAGS.EXTD_LIM - BIT(1) is set when the maximum run time has been extended 
    for Class 2 or Class 3 exit control processing. 
    FLAGS.TCBFULL - BIT(1) is set when the exit control frame is in the ALTRET 
    frame of the TCB because the TCB was full at entry to exit control. 
    FLAGS.XCONP - BIT(1)  set when Exit Control is in progress. 
    FLTFLG - BIT(48) contains the bit settings to indicate which of the 
    hardware traps are under control of the user.  Refer to 
    VLP_TRAP_CONDITIONS for the names and meanings of the individual traps. 
    HAND$ - EPTR ARRAY may be used to reference EVENT$, INT$, XCON$ and TRAP$ 
    as an array of EPTRs indexed by the MCL codes for the corresponding 
    service request. 
    INT$ - EPTR contains the address of the procedure to be entered on break 
    key interrupt. 
    TRAP$ - EPTR contains the address of the procedure to be entered on 
    machine traps and on Monitor Service Request errors when ALTRET is not 
    specified on the service request call. 
    XCON$ - EPTR contains the address of the procedure to be entered for exit 
    control processing. 
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
The G$EXCFR macro may be used to generate a structure that defines the fixed 
portion of any environment in the Task Control Block, be it the ALTRET frame 
or a frame on the exceptional condition stack.  The value in G$EXCFR.ECC 
differentiates the frame types. 
The structure contains the hardware environment followed by monitor supplied 
error information. 
The subfields within G$EXCFR have the following meaning: 
    ALTEMPTY - SBIN contains a non-zero value when the ALTRET frame is empty. 
    The ALTRET frame is marked empty on initial entry to a run-unit and after 
    execution of an M$MERC, M$RETRY or M$SENV monitor service.  This field has 
    meaning only in an ALTRET frame and is redefined as PREVSZ in a TCB Stack 
    frame. 
    DCB# - UBIN for ALTRET frames contains the number of the DCB associated 
    with this monitor service request. 
    ECC - SBIN contains the Exceptional Condition Code. When the environment 
    is in a frame on the exceptional condition stack, the ECC will be set to 
    one of the following: 
     %G_EVENT#   0    Event Completion 
     %G_INT#     1    Time-sharing terminal INT keyin 
     %G_XCON#    2    Exit condition, normal or abnormal 
     %G_TRAP#    3    Program Trap 
    When the environment is in the ALTRET frame, the ECC will contain: 
     %G_ALT#     99   Monitor services error with ALTRET specified 
     %G_TCBFULL# 98   Insufficient space in TCB stack to 
                      allocate an Exceptional Condition frame 
    P$$ - EPTR contains the contents of the Program Counter at the time the 
    exceptional condition occurred.  This field is REDEFed as P$ PTR and as P 
    UBIN(32). 
    PREVSZ - SBIN contains the number of words in the previous Stack frame. If 
    this is the first frame on the Exceptional Condition Stack the value will 
    be zero.  This field is redefined as ALTEMPTY in an ALTRET frame. 
    REGS - is the contents of the hardware registers at the time of the 
    exceptional condition: 
    REGS.Bn$ - PTR (where n = 1-7) (where n = 1-7) contains the contents of 
    the base registers. 
    REGS.CI - BIT(8) are the Commercial Indicator Register bits that are set 
    and reset by the CIP: 
    REGS.CI.G - BIT(1) is the Greater-than Indicator that contains the results 
    of the last compare instruction executed by the computer. 
    REGS.CI.L - BIT(1) is the Less-than Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    REGS.CI.OV - BIT(1) if set, indicates that an overflow occurred during a 
    decimal instruction. 
    REGS.CI.QLT - BIT(1) indicates whether the CIP has successfully completed 
    its Quality Logic Test or not. 
         0 = QLT successfully completed. 
         1 = QLT either still running or failed 
    REGS.CI.SF - BIT(1) if set, indicates that a sign fault occurred (negative 
    operand is stored in unsigned field). 
    REGS.CI.TR - BIT(1) if set, indicates that the alphanumeric result was 
    truncated. 
    REGS.I - BIT(16) contains a copy of the Indicator Register and, if a trap 
    condition exists, the trap number.  is an 8 bit indicator register that 
    contains the overflow and program status indicators: 
    REGS.I.B - BIT(1) may be considered to be a one-bit register loaded by 
    load bit instructions. 
    REGS.I.C - BIT(1) is the carry indicator that is set when the "logical" 
    capacity of any of the seven general registers is exceeded. 
    REGS.I.G - BIT(1) is the Greater-than Indicator that contains the results 
    of the last compare instruction executed by the computer. 
    REGS.I.IO - BIT(1) is the Input/Output Indicator that is set if the last 
    I/O operation was successful. 
    REGS.I.L - BIT(1) is the Less-than Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    REGS.I.OV - BIT(1) is the overflow indicator that is set when any of the 
    seven general registers overflows its "arithmetic" capacity. 
    REGS.I.TRAP# - UBIN(8) contains the trap number associated with the trap. 
    The hardware stores the trap number as '40'X - Trap Vector#.  This number 
    is then converted to the Trap Vector# by the software.  The following EQUs 
    may be used to determine the type of trap: 
    %G_MCL#             MCL 
    %G_TRACE#           Trace Breakpoint Trap 
    %G_NO_SIP#          Uninstalled SIP Trap 
    %G_TROT#            Watch Dog Timer Runout 
    %G_UNIMPL#          Unimplemented Instruction Trap 
    %G_INT_REG_OV#      Integer Register Overflow Trap 
    %G_S_DBZ#           SIP Divide by Zero Trap 
    %G_S_EXP_OV#        SIP Exponent Overflow Trap 
    %G_STK_UF#          Stack Underflow Trap 
    %G_STK_OV#          Stack Overflow Trap 
    %G_REMOTE_DESC#     Remote Data Descriptor Trap 
    %G_PRIV#            Privilege Violation Trap 
    %G_MEM_PROT#        Memory Protection Trap 
    %G_INT_UR#          Internal Unavailable Resource Trap 
    %G_PROG_ERR#        Program Error Trap 
    %G_INT_MBE#         Internal Memory or Bus Error Trap 
    %G_S_EXP_UF#        SIP Exponent Underflow Trap 
    %G_S_PROG_ERR#      SIP Program Error Trap 
    %G_S_SIGNIF#        SIP Significance Error Trap 
    %G_S_PRECISION#     SIP Precision Error Trap 
    %G_EXT_UR#          External (CIP or SIP) Unavailable Resource 
    %G_EXT_MBE#         External (CIP or SIP) Memory or Bus 
    %G_C_DBZ#           CIP Divide by Zero Trap 
    %G_C_SPEC#          CIP Illegal Specification Trap 
    %G_C_CHAR#          CIP Illegal Character Trap 
    %G_C_TRUNC#         CIP Truncation Trap 
    %G_C_OV#            CIP Overflow Trap 
    %G_CIP_QLT#         CIP QLT Fault 
    %G_SIP_QLT#         SIP QLT Fault 
    %G_EXT_PROT#        CIP or SIP Memory Protect Trap 
    %G_S_ARG#           SIP Illegal Argument Trap 
    REGS.I.U - BIT(1) is the Unlike-sign Indicator that contains the results 
    of the last compare instruction executed by the computer. 
    REGS.M1 enables and disables the Trace Trap and the General Register 
    Overflow Trap: 
    REGS.M1.J - BIT(1) is the Trace Trap control bit; 0 = Trace Trap disabled, 
    1 = Trace Trap enabled. 
    REGS.M1.Rn_OV - BIT(1) (where n = 1-7) are the Overflow trap control bits 
    for the seven general registers; 0 = trap disabled, 1 = trap enabled. 
    REGS.M3 contains the control information for the Commercial Instruction 
    Processor(CIP): 
    REGS.M3.CIP_OV - BIT(1) is the CIP Overflow Trap Mask; 0 = trap disabled, 
    1 = trap enabled. 
    REGS.M3.CIP_TR - BIT(1) is the CIP Truncation Trap Mask; 0 = trap 
    disabled, 1 = trap enabled. 
    REGS.RDBR$ - PTR is the Remote Descriptor Base Register used by the CIP to 
    locate a remote descriptor array. 
    REGS.Rn - UBIN (where n = 1-7) are the seven 16 bit general registers 
    numbered R1 through R7.  The first three, R1 - R3, may be used as index 
    registers.  R6 and R7 may be used as a double word. 
    REGS.T$ - PTR contains the address of the first word of the stack header. 
    PL-6 programs use T$ to address the AUTO stack. 
    S - BIT(16) contains the contents of the Status Register at the time of 
    the exceptional condition: 
    S.ID - BIT(2) contains the processor ID which is hard-wired and cannot be 
    changed under program control.  These 2 bits are used as the least 
    significant bits of the 10-bit channel number for the processor itself, 
    where the 8 high order bits are always zero. 
    S.LEVEL - UBIN(6) contains the interrupt priority level on which the 
    processor is currently executing.  Level 0 is the highest priority level 
    and 63 is the lowest. 
    S.QLT - VALUE-BIT(1) indicates whether a unit in the system has 
    successfully completed its Quality Logic Test or not. 
         0 = QLT successfully completed. 
         1 = QLT either still running or failed 
    S.RING - BIT(2) contains the currently active Ring value.  Note that ring 
    values are always encoded as ones complement whenever they appear.  Thus 
    this field will contain one of the following: 
      %G_RING0#  11   Ring 0 - Monitor 
      %G_R_MON#  10   Ring 1 - Monitor/Handlers 
      %G_R_DB#   01   Ring 2 - Debugger 
      %G_R_USR#  00   Ring 3 - User 
    TRLR - is the trailer portion of an exceptional condition frame.  TRLR is 
    an area 5 words long that contains information about the condition 
    supplied by the software: 
    TRLR.BRKCNT - UBIN contains the number of terminal breaks received since 
    the last read.  This is for break condition only. 
    TRLR.DEV - BIT(16)  for Interrupt frames, contains the Device word: 
    TRLR.DEV.CHN - UBIN(10)   contains the interrupting channel number. 
    TRLR.DEV.IL - UBIN(6)   contains the interrupting level number. 
    TRLR.ERR - BIT(32) contains the error code. TRLR.ERR is in VLP_ERRCODE 
    format and contains the following subfields: 
    TRLR.ERR.ERR# - UBIN(13) (Range is 0 to 8191) contains the number that 
    identifies a particular error condition.  The file B_ERRORS_C.:LIBRARY 
    contains the values for the ERR#s reported by the monitor. 
    TRLR.ERR.FCG - BIT(10) contains the two special five bit characters that 
    identify the functional code group that is reporting the error. 
    TRLR.ERR.MID - BIT(5) contains the special five bit character that 
    identifies which module in the functional code group is reporting the 
    error. 
    TRLR.ERR.MON - BIT(1) is set if this error is reported by the monitor. 
    TRLR.ERR.SEV - UBIN(3) (Range is 0 to 7) serves a double purpose. Within 
    the monitor it is used to indicate the seriousness of an error.  When 
    passed by the user to M$ERRMSG it indicates the level of detail requested 
    in the error message. 
    TRLR.EVID - SBIN for event frames, contains the event ID. This value is 
    user supplied. 
    TRLR.MCL_CODE - SBIN for ALTRET frames, contains the Service Request Code: 
    TRLR.MCL_CODE.CODE - UBIN(10) contains the monitor service request code. A 
    list of monitor service codes may be found in Appendix E of this manual. 
    The system file, LCP_6, contains EQU statements for monitor service 
    request codes in the form 
        %EQU G_MCL_name# 
    where name is the name from M$name. 
    TRLR.MCL_CODE.V# - UBIN(6)  contains the number of vectors in the FPT. 
    TRLR.P# - SBIN contains the number of additional words on this stack 
    frame.  For ALTRET frame, this value is always zero. 
    The content of these additional words is dependent on the type of 
    condition that has occurred. 
    TRLR.RNST - BIT(16) for Exit Control frames, contains the Run Status. If 
    the program terminated via M$EXIT, TRLR.RNST will be set to '0000'X.  If 
    the program terminated for any other reason, TRLR.RNST will be set as 
    follows: 
    TRLR.RNST.ABRT - BIT(1) is set if termination was caused by a monitor 
    detected error condition.  This may be a program trap when the program has 
    no trap control or an errored monitor service request when there is no 
    ALTRET routine specified. 
    TRLR.RNST.DSC - BIT(1) is set if termination was because of path 
    disconnect. 
    TRLR.RNST.EKEY - BIT(1) is set if termination was because of a !E keyin by 
    the operator. 
    TRLR.RNST.ERR - BIT(1) is set if an M$ERR service request was issued. 
    TRLR.RNST.INTABRT - BIT(1) is set if termination occurred at an interrupt 
    level. 
    TRLR.RNST.LDTRC - BIT(1) is set if an M$LDTRC service request was issued. 
    TRLR.RNST.LIMX - BIT(1) is set if termination is because of a limit that 
    has been exceeded. 
    TRLR.RNST.OFF - BIT(1) is set if the monitor is terminating the session. 
    TRLR.RNST.SSP - BIT(1) is set if termination was initiated by a Special 
    Shared Processor; i.e., the Debugger. 
    TRLR.RNST.XKEY - BIT(1) is set if termination was because of a !X keyin by 
    the operator. 
    TRLR.RNST.XXX - BIT(1) is set if an M$XXX service request was issued. 
    TRLR.SUBC - SBIN contains the exceptional condition sub-code. The contents 
    of this field is dependent on the type of condition that has occurred. 
    This field is redefined by MCL_CODE, DEV, TRAP, and XCON. 
    TRLR.TRAP.IR - BIT(8) contains the contents of the Indicator register at 
    the time of the trap. 
    TRLR.TRAP.TRAP# - UBIN(8) for trap frames, contains the trap number 
    associated with the trap.  See REGS.I.TRAP#. 
    TRLR.XCON - BIT(16) for exit control frames, contains the following: 
    TRLR.XCON.FLAGS.XCONP - BIT(1) set if exit control was already in progress 
    on this entry to exit control. 
    TRLR.XCON.TRAP# - UBIN(8) contains the value from G$TSA.I.TRAP# at the 
    time of the exit condition.  See REGS.I.TRAP#. 
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
The G$FRAME macro can be used to describe the automatic storage frame header. 
    PARAMS = PTR Array.  This array contains the pointers to the parameters 
    passed to this procedure. 
    PREV_FR_SIZ - UBIN.  This field is only used and maintained for the 
    variable type of stack. It contains the size of the previous frame (not 
    including size word) and is used for procedure exit to remove a frame. 
    RET_ADDR - EPTR.  This field contains the return address for the call 
    which invoked the procedure to which this frame belongs. In the case of 
    Main or Async procedure, this field contains the address of the procedure 
    activation. 
    TYPE = UBIN.  This field contains a value which indicates the type of 
    frame.  The currently defined values are: 
    0 - Standard procedure invoked by CALL 
    -1 - Main procedure 
    -2 - Async procedure 
00001
00002
00003
00004
The G$INDICATOR_REG macro may be used to generate a structure that contains 
the Indicator Register. 
The fields of the Indicator Register are: 
    B = VALUE-BIT(1) may be considered to be a one-bit register loaded by load 
    bit instructions. 
    When generating a STATIC or CONSTANT structure, this field may be 
    initialized by specifying B={G_ON# | G_OFF#}.  Default = G_OFF#. 
    C = VALUE-BIT(1) is the carry indicator that is set when the "logical" 
    capacity of any of the seven general registers is exceeded. 
    When generating a STATIC or CONSTANT structure, this field may be 
    initialized by specifying C={G_ON# | G_OFF#}.  Default = G_OFF#. 
    G = VALUE-BIT(1) is the Greater-than Indicator that contains the results 
    of the last compare instruction executed by the computer. 
    When generating a STATIC or CONSTANT structure, this field may be 
    initialized by specifying G={G_ON# | G_OFF#}.  Default = G_OFF#. 
    IO = VALUE-BIT(1) is the Input/Output Indicator that is set if the last 
    I/O operation was successful. 
    When generating a STATIC or CONSTANT structure, this field may be 
    initialized by specifying IO={G_ON# | G_OFF#}.  Default = G_OFF#. 
    L = VALUE-BIT(1) is the Less-than Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    When generating a STATIC or CONSTANT structure, this field may be 
    initialized by specifying L={G_ON# | G_OFF#}.  Default = G_OFF#. 
    OV = VALUE-BIT(1) is the overflow indicator that is set when any of the 
    seven general registers overflows its "arithmetic" capacity. 
    When generating a STATIC or CONSTANT structure, this field may be 
    initialized by specifying OV={G_ON# | G_OFF#}.  Default = G_OFF#. 
    TRAP# = VALUE-UBIN(8) contains the trap number associated with the trap. 
    The hardware stores the trap number as '40'X - Trap Vector#.  This number 
    is then converted to the Trap Vector# by the software.  The following EQUs 
    may be used to determine the type of trap: 
    %G_MCL#             MCL 
    %G_TRACE#           Trace Breakpoint Trap 
    %G_NO_SIP#          Uninstalled SIP Trap 
    %G_TROT#            Watch Dog Timer Runout 
    %G_UNIMPL#          Unimplemented Instruction Trap 
    %G_INT_REG_OV#      Integer Register Overflow Trap 
    %G_S_DBZ#           SIP Divide by Zero Trap 
    %G_S_EXP_OV#        SIP Exponent Overflow Trap 
    %G_STK_UF#          Stack Underflow Trap 
    %G_STK_OV#          Stack Overflow Trap 
    %G_REMOTE_DESC#     Remote Data Descriptor Trap 
    %G_PRIV#            Privilege Violation Trap 
    %G_MEM_PROT#        Memory Protection Trap 
    %G_INT_UR#          Internal Unavailable Resource Trap 
    %G_PROG_ERR#        Program Error Trap 
    %G_INT_MBE#         Internal Memory or Bus Error Trap 
    %G_S_EXP_UF#        SIP Exponent Underflow Trap 
    %G_S_PROG_ERR#      SIP Program Error Trap 
    %G_S_SIGNIF#        SIP Significance Error Trap 
    %G_S_PRECISION#     SIP Precision Error Trap 
    %G_EXT_UR#          External (CIP or SIP) Unavailable Resource 
    %G_EXT_MBE#         External (CIP or SIP) Memory or Bus 
    %G_C_DBZ#           CIP Divide by Zero Trap 
    %G_C_SPEC#          CIP Illegal Specification Trap 
    %G_C_CHAR#          CIP Illegal Character Trap 
    %G_C_TRUNC#         CIP Truncation Trap 
    %G_C_OV#            CIP Overflow Trap 
    %G_CIP_QLT#         CIP QLT Fault 
    %G_SIP_QLT#         SIP QLT Fault 
    %G_EXT_PROT#        CIP or SIP Memory Protect Trap 
    %G_S_ARG#           SIP Illegal Argument Trap 
    This field is undefined in the Indicator Register as stored in the 
    Interrupt Save Area. 
    When generating a STATIC or CONSTANT structure, this field may be 
    initialized by specifying TRAP#=value.  Default = 0. 
    U = VALUE-BIT(1) is the Unlike-sign Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    When generating a STATIC or CONSTANT structure, this field may be 
    initialized by specifying U={G_ON# | G_OFF#}.  Default = G_OFF#. 
00001
00002
00003
00004
00005
00006
00007
00008
The G$ISA macro may be used to generate a structure that defines the entire 
Interrupt Save Area. 
    DEV - BIT(16) contains the contents of the Device word stored by the 
    hardware: 
    DEV.CHN - UBIN(10) contains the interrupting channel. 
    DEV.IL - UBIN(6) contains the Interrupting Level number. 
    ISM1 - BIT(16) contains the Interrupt Save Mask 1.  See G$ISM1 for the 
    names and meanings of the bits within this word. 
    ISM2 - BIT(16) contains the Interrupt Save Mask 2.  See G$ISM2 for the 
    names and meanings of the bits within this word. 
    P$$ - EPTR contains the contents of the Program Counter at the time of the 
    interrupt.  This field is REDEFed as P$ PTR. 
    REGS - contains the contents of the hardware registers at the time of the 
    interrupt.  Note that the bit settings within ISM1 and ISM2 determine the 
    the contents of REGS. 
    REGS.Bn$ - PTR (where n = 1-7) contains the contents of the base 
    registers. 
    REGS.CI - BIT(8) contains the Commercial Indicator register bits which are 
    set and reset by the CIP: 
    REGS.CI.G - BIT(1) is the Greater-than Indicator that contains the results 
    of the last compare instruction executed by the computer. 
    REGS.CI.L - BIT(1) is the Less-than Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    REGS.CI.OV - BIT(1) if set, indicates that an overflow occurred during a 
    decimal instruction. 
    REGS.CI.QLT - BIT(1) indicates whether the CIP has successfully completed 
    its Quality Logic Test or not: 
         0 = QLT successfully completed. 
         1 = QLT either still running or failed 
    REGS.CI.SF - BIT(1) if set, indicates that a sign fault occurred (negative 
    operand is stored in unsigned field). 
    REGS.CI.TR - BIT(1) if set, indicates that the alphanumeric result was 
    truncated. 
    REGS.I - BIT(16) is an 8 bit indicator register that contains the overflow 
    and program status indicators: 
    REGS.I.B - BIT(1) may be considered to be a one-bit register loaded by 
    load bit instructions. 
    REGS.I.C - BIT(1) is the carry indicator that is set when the "logical" 
    capacity of any of the seven general registers is exceeded. 
    REGS.I.G - BIT(1) is the Greater-than Indicator that contains the results 
    of the last compare instruction executed by the computer. 
    REGS.I.IO - BIT(1) is the Input/Output Indicator that is set if the last 
    I/O operation was successful. 
    REGS.I.L - BIT(1) is the Less-than Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    REGS.I.OV - BIT(1) is the overflow indicator that is set when any of the 
    seven general registers overflows its "arithmetic" capacity. 
    REGS.I.TRAP# - UBIN(8) contains the trap number associated with the trap. 
    The hardware stores the trap number as '40'X - Trap Vector#.  This number 
    is then converted to the Trap Vector# by the software.  The following EQUs 
    may be used to determine the type of trap: 
    %G_MCL#             MCL 
    %G_TRACE#           Trace Breakpoint Trap 
    %G_NO_SIP#          Uninstalled SIP Trap 
    %G_TROT#            Watch Dog Timer Runout 
    %G_UNIMPL#          Unimplemented Instruction Trap 
    %G_INT_REG_OV#      Integer Register Overflow Trap 
    %G_S_DBZ#           SIP Divide by Zero Trap 
    %G_S_EXP_OV#        SIP Exponent Overflow Trap 
    %G_STK_UF#          Stack Underflow Trap 
    %G_STK_OV#          Stack Overflow Trap 
    %G_REMOTE_DESC#     Remote Data Descriptor Trap 
    %G_PRIV#            Privilege Violation Trap 
    %G_MEM_PROT#        Memory Protection Trap 
    %G_INT_UR#          Internal Unavailable Resource Trap 
    %G_PROG_ERR#        Program Error Trap 
    %G_INT_MBE#         Internal Memory or Bus Error Trap 
    %G_S_EXP_UF#        SIP Exponent Underflow Trap 
    %G_S_PROG_ERR#      SIP Program Error Trap 
    %G_S_SIGNIF#        SIP Significance Error Trap 
    %G_S_PRECISION#     SIP Precision Error Trap 
    %G_EXT_UR#          External (CIP or SIP) Unavailable Resource 
    %G_EXT_MBE#         External (CIP or SIP) Memory or Bus 
    %G_C_DBZ#           CIP Divide by Zero Trap 
    %G_C_SPEC#          CIP Illegal Specification Trap 
    %G_C_CHAR#          CIP Illegal Character Trap 
    %G_C_TRUNC#         CIP Truncation Trap 
    %G_C_OV#            CIP Overflow Trap 
    %G_CIP_QLT#         CIP QLT Fault 
    %G_SIP_QLT#         SIP QLT Fault 
    %G_EXT_PROT#        CIP or SIP Memory Protect Trap 
    %G_S_ARG#           SIP Illegal Argument Trap 
    REGS.I.U - BIT(1) is the Unlike-sign Indicator that contains the results 
    of the last compare instruction executed by the computer. 
    REGS.M1 - The M1 register enables and disables the Trace Trap and the 
    General Register Overflow Trap: 
    REGS.M1.J - BIT(1) is the Trace Trap control bit; 0 = Trace Trap disabled, 
    1 = Trace Trap enabled. 
    REGS.M1.Rn_OV - BIT(1) (where n = 1-7) are the overflow trap control bits 
    for the seven general registers; 0 = trap disabled, 1 = trap enabled. 
    REGS.M3 - The M3 register contains the control information for the 
    Commercial Instruction Processor(CIP): 
    REGS.M3.CIP_OV - BIT(1) is the CIP Overflow Trap Mask; 0 = trap disabled, 
    1 = trap enabled. 
    REGS.M3.CIP_TR - BIT(1) is the CIP Truncation Trap Mask; 0 = trap 
    disabled, 1 = trap enabled. 
    REGS.RDBR$ - PTR specifies the Remote Descriptor Base register and is used 
    by the CIP to locate a remote descriptor array. 
    REGS.Rn - UBIN WORD (where n = 1-7) contains the contents of the 16 bit 
    general registers. 
    REGS.T$ - PTR is the Stack Address Register and contains the address of 
    the first word of the stack header. 
    S - BIT(16) contains the contents of the Status Register at the time of 
    the interrupt: 
    S.ID - BIT(2) is the processor identification which is hard-wired and 
    cannot be changed under program control.  These 2 bits are used as the 
    least significant bits of the 10-bit channel number for the processor 
    itself, where the 8 high order bits are always ZERO. 
    S.LEVEL - UBIN(6) contains the interrupt priority level on which the 
    processor is currently executing.  Level 0 is the highest priority level 
    and 63 is the lowest. 
    S.QLT - BIT(1) indicates whether a unit in the system has successfully 
    completed its Quality Logic Test or not. 
         0 = QLT successfully completed. 
         1 = QLT either still running or failed 
    S.RING - BIT(2) contains the currently active Ring value.  Note that ring 
    values are always encoded as ones complement whenever they appear.  Thus 
    this field will contain one of the following: 
          11 = Ring 0 - the most privileged; used by the Monitor 
          10 = Ring 1 - also privileged and used by the Monitor 
          01 = Ring 2 - Command Processor or Debugger 
          00 = Ring 3 - User 
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
The G$ISA_HDR macro may be used to generate a structure that contains the 
words in the Interrupt Save Area prior to the one pointed to by the interrupt 
save vector. 
The fields in the Interrupt Save Area header are: 
    ASV$ - PTR contains the Address Space Vector.  This pointer specifies the 
    base of an MMU image in memory.  The default is NIL. 
    TSAP$ - PTR contains the Trap Save Area Pointer.  This pointer is null 
    until a trap occurs, at which time the address of the Trap Save Area used 
    for the trap is stored here by the hardware.  The default is NIL. 
00001
00002
The G$ISA_MINI macro may be used to generate a structure that defines the 
Interrupt Save Area for a centrally connected interrupt handler. 
The mini ISA must reside in the monitor's HJIT so that it may be addressed 
from all interrupt levels. 
The G$ISA_HDR macro is invoked using the name specified via the FPTN parameter 
which will determine the name of the structure.  The header is followed by the 
following fields: 
    DEV - BIT(16) contains the contents of the Device word stored by the 
    hardware.  See G$DEV for details.  Only IL may be initialized. 
    ISM1 - BIT(16) contains the Interrupt Save Mask 1.  See G$ISM1 for the 
    names and meanings of the bits within this word.  In a mini ISA, all mask 
    bits are reset. 
    ISM2 - BIT(16) contains the Interrupt Save Mask 2.  See G$ISM2 for the 
    names and meanings of the bits within this word.  In a mini ISA, the MMU 
    bit is reset, the NATSAP_SEL value is set to %G_NATSAP_HND%, and all other 
    mask bits are reset. 
    P$$ - EPTR contains the contents of the Program Counter to be loaded at 
    the time of the interrupt.  This is to be the address of the Common 
    Interrupt Handler in the MON_ENTRY Segment.  This field is REDEFed as P$ 
    PTR.  The default is NIL. 
    S - BIT(16) contains an image of a Status Register which would be stored 
    if the ISA were ever interrupted.  Otherwise, only the RING field is used, 
    and thus only it can be initialized. 
    S.ID - BIT(2) is the processor identification which is hard-wired and 
    cannot be changed under program control.  These 2 bits are used as the 
    least significant bits of the 10-bit channel number for the processor 
    itself, where the 8 high order bits are always ZERO. 
    S.LEVEL - UBIN(6) contains the interrupt priority level on which the 
    processor is currently executing.  Level 0 is the highest priority level 
    and 63 is the lowest. 
    S.QLT - BIT(1) indicates whether a unit in the system has successfully 
    completed its Quality Logic Test or not. 
         0 = QLT successfully completed. 
         1 = QLT either still running or failed 
    S.RING - BIT(2) contains the currently active Ring value.  Note that ring 
    values are always encoded as ones complement whenever they appear.  Thus 
    this field will contain one of the following: 
          11 = Ring 0 - the most privileged; used by the Monitor 
          10 = Ring 1 - also privileged and used by the Monitor 
          01 = Ring 2 - Command Processor or Debugger 
          00 = Ring 3 - User 
00001
00002
00003
00004
00005
00006
00007
00008
00009
The G$ISM1 macro may be used to generate a structure that contains the 
Interrupt Save Mask 1.  When generating a CONSTANT or STATIC structure, each 
field within ISM1 may be set or reset by specifying field-name = {G_ON# | 
G_OFF#}.  The default in each case is G_ON#. 
The fields of ISM1 are: 
    Bn - BIT(1) indicates, if set, that the contents of the base register Bn 
    (where n = 1-7) is to be saved and restored.  The default is G_ON#. 
    I - BIT(1) indicates, if set, that the contents of the Indicator Register 
    is to be saved and restored.  The default is G_ON#. 
    M1 - BIT(1) indicates, if set, that the contents of Mode Control Register 
    M1 is to be saved and restored.  The default is G_ON#. 
    Rn - BIT(1) indicates, if set, that the contents of the general register 
    Rn (where n = 1-7) is to be saved and restored.  The default is G_ON#. 
00001
00002
00003
00004
The G$ISM2 macro may be used to generate a structure that contains the 
Interrupt Save Mask 2.  When generating a CONSTANT or STATIC structure, the 
fields that control the saving and restoring of the registers may be set or 
reset by specifying field-name = {G_ON# | G_OFF#}.  The default in each case 
is G_ON#. 
The fields of ISM2 are: 
    CIP - BIT(1) indicates, if set, that the CIP context is to be saved and 
    restored.  The default is G_ON#. 
    M2_M7 - BIT(1) indicates, if set, that the contents of Mode Control 
    Registers M1 to M7 is to be saved and restored.  The default is G_ON#. 
    MMU - BIT(1) indicates, if set, that the MMU context is to be loaded when 
    an interrupt level change takes place.  Note, however, that MMU context is 
    never stored.  The default is G_ON#. 
    NATSAP_SEL - UBIN(3) contains an index to the pool of Trap Save Areas to 
    be used when a trap occurs while this interrupt level is active.  The 
    default is 0. 
    T - BIT(1) indicates, if set, that the contents of the Stack Address 
    Register is to be saved and restored.  The default is G_ON#. 
00001
00002
00003
00004
00005
The Job Information Table (JIT) contains the various user identity, limit and 
accounting information. 
The G$JIT macro, which is contained in the G_JIT_M include file, may be used 
to generate a structure that defines the JIT.  Because the G$JIT macro 
requires some of the macros contained in the GU_LCP6_M include file, GU_LCP6_M 
(or LCP_6) must also be specified as an include file in a compile unit that 
requires the G$JIT structure. 
A user may reference the JIT through the FEPLINK defined pointer G$JIT$. 
A description of the fields in the JIT follows: 
    ACCN - CHAR(8).  Is the ACCouNt field containing the user's log on 
    account. 
    ACCTLOG.  The JIT contains all the information that is eventually written 
    to the :ACCTLG file.  The information is written directly from the JIT, 
    and therefore must begin with the control words for writing the the 
    message to the Host.  This includes: 
    ACCTLOG.FCN - UBIN.  Contains the function code that indicates that the 
    message is a syslog message.  This value is %IGA_SYSLOG (39) from the 
    KL_AFCN_C include file. 
    ACCTLOG.FILENUM - UBIN.  Contains the code to specify that the message is 
    to be written to :ACCTLG.  This is always 2. 
    BILL - CHAR(6).  Specifies the rate schedule that is to be used to 
    determine the LCP-6 user's charges.  See the FEBILLING user authorization 
    option of SUPER. 
    CALCNT - See MCLS. 
    CCBUF - CHAR(256).  Is the Control Command BUFfer.  It contains the text 
    that is passed from one run unit to another via M$LDTRC. 
    CLUKRINT - SBIN(32).  Contains the interval of time of the permanent wall 
    time clock, if set; otherwise it contains zero. 
    CLUKRLVL - UBIN BYTE.  Contains the level number of the interrupt to be 
    triggered after a specified real time has expired. 
    CLUKXINT - SBIN(32).  Contains the interval of time of the permanent 
    execution time clock, if set; otherwise it contains zero. 
    CLUKXLVL - UBIN BYTE.  Contains the level number of the interrupt to be 
    triggered after a specified execution time has expired. 
    CODE - UBIN.  Contains a value to define the type of :ACCTLG record.  See 
    file AZ_SUBS_C for the TYPE value EQUs.  This is always %AZ$LCP6 (7) for 
    an LCP-6 user accounting record. 
    CQPC - UBIN.  Is the Circular Queue Page Count.  It contains the number of 
    pages currently used by the circular queue on behalf of this user. 
    CURRLVLS - UBIN BYTE.  Contains the number of interrupt levels currently 
    allocated by this user. 
    CURSUDO - ARRAY(0:7) UBIN BYTE.  Is the CURrent pSeUDO field.  It contains 
    the current number of each pseudo resource defined which is currently 
    allocated to this user.  The order is as defined by GFR_PSUDO_NM. 
    CVM_REAL - ARRAY(0:31) BIT(1).  Contains bits that correspond to the 
    segments in the G$UHJIT.ASDT_USR.  If a bit is set, the corresponding 
    segment has been mapped with a physical page that may not belong to this 
    user and indicates that the pages mapped into the segment are not to be 
    released at rundown.  See M$CVM. 
    DB# - UBIN BYTE.  Contains the associated DeBugger number. 
    DB_ACCN - CHAR(8).  Is the DeBug ACCount field.  It contains the host user 
    account that is allowed to debug this LCP-6 user.  This account field may 
    be wild carded. 
    DB_WRTSEGS - ARRAY(0:14) BIT(1).  Contains bits that represent the user 
    segments 16 through 31.  If a bit is set, it indicates to the trap handler 
    that the debugger is to be given write access to the segment. 
    DLL - UBIN.  Contains the Data Lower Limit, which is the virtual page 
    number of the first data page of the run unit or standard shared processor 
    currently executing. 
    DUL - UBIN.  Contains the Data Upper Limit, which is the virtual page 
    number of the last data page of the run unit or standard shared processor 
    currently executing.  If the user is at job step, JIT.DUL will be set to 
    JIT.DLL -1. 
    ERR.  Contains the error code that reflects the exit condition of the user 
    program.  G$JIT.ERR is in VLP_ERRCODE format and contains the following 
    subfields: 
    ERR.ERR# - UBIN(13). Range is 0 to 8191.  contains the number that 
    identifies a particular error condition.  The file B_ERRORS_C.:LIBRARY 
    contains the values for the ERR#s reported by the monitor. 
    ERR.FCG - BIT(10).  contains the two special five bit characters that 
    identify the functional code group that is reporting the error. 
    ERR.MID - BIT(5).  contains the special five bit character that identifies 
    which module in the functional code group is reporting the error. 
    ERR.MON - BIT(1).  is set if this error is reported by the monitor. 
    ERR.SEV - UBIN(3). Range is 0 to 7.  serves a double purpose.  Within the 
    monitor it is used to indicate the seriousness of an error.  When passed 
    by the user to M$ERRMSG it indicates the level of detail requested in the 
    error message. 
    ERRLOG_LVL - ARRAY(0:7) BIT(1).  Contains bit settings that indicate the 
    severity of the errors that are to be reported via the error logging 
    mechanism.  This field is redefined as follows: 
    ERRLOG.SEVn BIT(1)   where n = 0 -> 7 
    FD_ALTERR - BIT(32).  Contains the monitor service error code for monitor 
    services requested by a debugger.  This field is valid only for debugger 
    monitor service ALTRET procedures.  FD_ALTERR is in VLP_ERRCODE format. 
    FD_P$ = PTR.  Contains the debugger's Program Counter at the time of the 
    debugger monitor service ALTRET. 
    FEP# - UBIN.  Contains the FEP node number. 
    FIRST_SEG - ARRAY(0:31) BIT(1).  Contains bits that correspond to the 
    segments in the G$UHJIT.ASDT_USR.  If a FIRST_SEG bit is set, the 
    corresponding segment is the first in a user-allocated extent or cannot be 
    allocated by the user.  If a FIRST_SEG bit is reset, either the 
    corresponding segment is not allocated, or, if the corresponding 
    G$ASDT.SEGDESC.V bit is set, the segment is an extension of a 
    user-allocated data extent. 
    FRS - BIT(16).  Is the Final Run Status field.  This field contains the 
    accumulated abort flags.  This is a logical OR of the following flags that 
    may appear in RNST as the job step is rundown through all the various 
    levels of exit control. 
    For example, if a user is aborted by the host program, G_RS_DSC# will 
    appear in RNST until it is put in the user's exit control frame.  At that 
    point the G_RS_DSC# flag is moved to FRS and RNST is set to zero.  Should 
    the user reach the maximum time in his exit control routine, G_RS_LIMX# 
    would temporarily appear in RNST, and both G_RS_DSC# and RS_LIMX# would be 
    set in FRS. 
    FRS.ABRT - BIT(1).  is set if termination was caused by a monitor detected 
    error condition.  This may be a program trap when the program has no trap 
    control or an errored monitor service request when there is no ALTRET 
    routine specified. 
    FRS.DSC - BIT(1).  is set if termination was because of path disconnect. 
    FRS.EKEY - BIT(1).  is set if termination was because of a !E keyin by the 
    operator. 
    FRS.INTABRT - BIT(1).  is set if termination occurred at an interrupt 
    level. 
    FRS.LIMX - BIT(1).  is set if termination is because of a limit that has 
    been exceeded. 
    FRS.OFF - BIT(1).  is set if the monitor is terminating the session. 
    FRS.SSP - BIT(1).  is set if termination was initiated by a Special Shared 
    Processor; i.e., the Debugger. 
    FRS.XKEY - BIT(1).  is set if termination was because of a !X keyin by the 
    operator. 
    GFR_ACCT - UBIN BYTE.  Contains an index into the monitor's account 
    resource table for this user's account. 
    IDELTAT - UBIN(32).  Contains the total quantum time allocated at the last 
    quantum end.  This will normally be the quantum specified by the system 
    manager for this mode, partition, user, etc. 
    JMCLS - UBIN.  Contains the number of monitor service requests executed 
    during this job. 
    JOBUNIT - ARRAY(0:3) UBIN.  Contains a set of four counters that are 
    maintained through an entire job.  See M$CHGUNIT and the RATES processor. 
    JPEAK_LVLS - UBIN.  Is the JPEAK LeVeLS field.  It contains the maximum 
    number of interrupt levels allocated at any given time during this job. 
    JPEAK_MEM - UBIN.  Is the JPEAK MEMory field.  It contains the maximum 
    number of pages allocated at any given time during the job. 
    JPEAK_SUDO - ARRAY(0:7) UBIN BYTE.  Is the JPEAK pSeUDO array.  It 
    contains the maximum number of each pseudo resource allocated at any given 
    time during this job. The order is as defined by GFR_PSUDO_NM. 
    JPROC_EXTIME - UBIN(32).  Is the Job PROCessor EXecution TIME field.  It 
    contains the user execution time used in the entire job.  This is 
    maintained in clock ticks. 
    JPROC_MEMTIME - UBIN(32).  Is the Job PROCessor MEMory TIME field.  It 
    contains the integral of ((JPROC_EXTIME + PROC_SVTIME) * current memory 
    allocation) over all quanta of the entire job.  This is maintained in 
    clock ticks * page units. 
    JPROC_SVTIME - UBIN(32).  Is the Job PROCessor SerVice TIME field.  It 
    contains the user service time used in the entire job.  This is maintained 
    in clock ticks. 
    JREADS_HOST - UBIN(32).  Is the Job READS_HOST field.  It contains a count 
    of the number of reads through a DCB where RES = 'HO' over the entire job. 
    JREADS_UC - UBIN(32).  Is the Job READS_UC field.  It contains a count of 
    the number of reads through a DCB where RES = 'UC' over the entire job. 
    JSTART - UBIN(32).  Contains the LCP-6 UTS at the time the user was 
    created. 
    JUNK - BIT(16).  Contains bits used by job step processing: 
    JUNK.ALIBFD - BIT(1).  Is set when a message has arrived for the front-end 
    debugger and the debugger does not have a read outstanding.  This flag is 
    reset by the GJU$GET_DB routine after associating or awakening the 
    debugger. 
    JUNK.BACKP$ - BIT(1).  Is set to indicate that control is to be returned 
    to the user with P$ in the TSA reset to the address of the outstanding 
    monitor service request. 
    JUNK.DB_TIMER - BIT(1).  Is set in conjunction with JUNK.ALIBFD if the 
    Debugger is to be entered because the Debugger specified clock time has 
    expired.  This flag is used by FEPMON.  It is reset by the GJU$GET_DB 
    routine after associating or awakening the debugger. 
    JUNK.EXONLY - BIT(1).  Is set when an execute-only run unit is put into 
    execution.  When this flag is set, association of a debugger is not 
    allowed. 
    JUNK.HOST_STEP_ABRT - BIT(1).  Set if the host aborted the job step 
    process because of problems reading the fprg. 
    JUNK.KEEP - BIT(1).  Set if UC DCBs are to be closed with DISP=KEEP as 
    part of the M$LDTRC operation. 
    JUNK.MLDTRC - BIT(1).  Is set while processing an M$LDTRC monitor service 
    request.  This flag is reset when the run unit has been fetched or the 
    LDTRC process is aborted. 
    JUNK.PROCACCT - BIT(1).  Is set if the run unit from the :SYS account had 
    been linked with the PROCACC option. 
    JUNK.PROCSURCHG - BIT(1).  Is set if the run unit from the :SYS account 
    had been linked with the SURCHARGE option. 
    JUNK.RTNFID - BIT(1).  Is set when a host debugger has requested that a 
    message containing the FPRG fid be returned. 
    JUNK.SCCSET - BIT(1).  Is set when an M$EXIT, M$ERR or M$XXX monitor 
    service request is issued with the STEPCC option specified. 
    JUNK.STEP - BIT(1).  Is set when job step is in progress; the flag is 
    reset when entering the user program. 
    JUNK.STEPACCT - BIT(1).  Is set if job step accounting records are to be 
    written for this user as indicated by the FESTEPACCNT option in SUPER. 
    JUNK2 - BIT(8).  Contains more bits used by job step processing: 
    JUNK2.BYPASS_MFPL - BIT(1).  Set if TPFP has done an M$LDTRC with the 
    NO_MICROFPL bit set.  Reset when the standard FPRG has been associated 
    with the user. 
    JUNK2.MICROFPL - BIT(1).  Set if MICROFPL bit was set in the VLP_LINEATTR 
    for this user's terminal. 
    JUSER_EXTIME - UBIN(32).  Is the Job USER EXecution TIME field.  It 
    contains the user execution time used in the entire job.  This is 
    maintained in clock ticks. 
    JUSER_MEMTIME - UBIN(32).  Is the Job USER MEMory TIME field.  It contains 
    the integral of ((JUSER_EXTIME + USER_SVTIME) * current memory allocation) 
    over all quanta of the entire job.  This is maintained in clock ticks * 
    page units. 
    JUSER_SVTIME - UBIN(32).  Is the Job USER SerVice TIME field.  It contains 
    the user service time used in the entire job.  This is maintained in clock 
    ticks. 
    JWRITES_HOST - UBIN(32).  Is the Job WRITES_HOST field.  It contains a 
    count of the number of writes through a DCB where RES = 'HO' over the 
    entire job. 
    JWRITES_UC - UBIN(32).  Is the Job WRITES_UC field.  It contains a count 
    of the number of writes through a DCB where RES = 'UC' over the entire 
    job. 
    LANG - CHAR(1).  Is the LANGuage field containing a single character which 
    specifies the native language of the user.  This field is used to select 
    the correct error message file for this user. 
    LLL - UBIN.  Is the Library Lower Limit field.  It contains the virtual 
    page number of the first page of procedure of an associated run-time 
    library. 
    LUL - UBIN.  Is the Library Upper Limit field.  It contains the virtual 
    page number of the last page of procedure of an associated run-time 
    library. 
    MAXLVLS - UBIN BYTE.  Is the MAXimum interrupt LeVeLS field.  It contains 
    the number of interrupt levels this user may have allocated to him. 
    MAXMEM - UBIN.  Contains the maximum number of pages that may be allocated 
    by this user. 
    MAXSUDO - ARRAY(0:7) UBIN BYTE.  Is the MAXimum pSeuDO field.  It contains 
    the maximum number of each pseudo resource defined which may be allocated 
    by this user.  The order is as defined by GFR_PSUDO_NM. 
    MCLS - UBIN.  Contains the total number of monitor service requests 
    executed during this job or job step. 
    MMFLGS.  Contains a set of flags which describe the current state of this 
    user from a memory management standpoint. 
    MMFLGS.FREE_PPGS - BIT(1).  Is the FREE Procedure PaGeS field.  It 
    indicates whether or not the procedure pages in the currently executing 
    run unit are to be charged to this user.  A value of '1'B specifies that 
    the pages are not to be charged, regardless of whether the run-unit is 
    shared or not. 
    MODE - UBIN.  Specifies the type of user.  One of the following EQUed 
    values will be contained in this field: 
      G_M_USER#    1      USER Connected 
      G_M_CG#      2      Comgroup Station Connected 
      G_M_HANDLER# 3      Handler 
      G_M_GHOST#   4      Ghost 
    MRT - SBIN(32).  Is the Maximum Run Time field.  It contains the maximum 
    allowed execution plus service time as specified in the :HLP user record 
    when the user is created.  At any other time it contains the amount of 
    time remaining within the limit. This field is maintained in clocks ticks. 
    NSPC - UBIN.  Is the Non-Shufflable Page Count field.  It contains the 
    number of pages of Dynamic Data which were obtained by M$GDS with 
    IOBUF=YES specified. 
    PCC - UBIN.  Is the Page Count of Context field.  It contains the number 
    of pages the monitor has allocated for this user's context.  User context 
    includes HJIT, TSTACKU, and the fixed portion of the Read Only 
    Segment(ROS). 
    PCD - UBIN.  Is the Page Count of Data field.  It contains the number of 
    pages that have been allocated for program data in the instruction 
    segment. 
    PCDDS - UBIN.  Is the Page Count Debugger Data Segments field.  It 
    contains the total number of pages which a debugger has allocated on 
    behalf of this user. 
    PCDS - UBIN.  Is the Page Count Dynamic Segments field.  It contains the 
    number of pages of dynamic data which were obtained by M$GDS with IOBUF=NO 
    specified. 
    PCL - UBIN.  Is the Page Count of Library field.  It contains zero if no 
    run-time library is associated, or if a shared run-time library is 
    associated.  If the run-library becomes unshared, because of an M$UNSHARE 
    or UNSHARELIB command to DELTA, this field will contain the number of 
    pages that have been obtained for the run-time library procedure. 
    PCP - UBIN.  Is the Page Count of Procedure field.  It contains the number 
    of pages that have been allocated for procedure. 
    PCROS - UBIN.  Is the Page Count Read Only Segment field.  It contains the 
    additional number of pages in the Read Only Segment required for user 
    DCBs.  The fixed portion of this segment is counted in PCC. 
    PEAK_LVLS - UBIN.  Is the PEAK LeVeLS field.  It contains the maximum 
    number of interrupt levels allocated at any given time during this job or 
    job step. 
    PEAK_MEM - UBIN.  Is the PEAK MEMory field.  It contains the maximum 
    number of pages allocated at any given time during the job or job step. 
    PEAK_SUDO - ARRAY(0:7) UBIN BYTE.  Is the PEAK pSeUDO array.  It contains 
    the maximum number of each pseudo resource allocated at any given time 
    during this job or job step. 
    PLL - UBIN.  Contains the Procedure Lower Limit, which is the virtual page 
    number of the first procedure page of the run unit or standard shared 
    processor currently executing. 
    PRIV.  Consists of three double words defined in the JIT that are used to 
    verify a user's privilege prior to performing certain system functions for 
    this user.  A description of the contents of each of these words follows: 
    PRIV.ACTIVE - BIT(32).  Contains the privileges that are currently in 
    effect. 
    These privilege bits may be set and reset by the M$SPRIV monitor service 
    request.  Refer to the FEP Monitor Services Reference Manual for a 
    description of M$SPRIV. 
    The individual bits in PRIV.ACTIVE are as follows: 
    PRIV.ACTIVE.CQ - BIT(1).  allows the user to use the Circular Queue. 
    PRIV.ACTIVE.EXMM - BIT(1).  allows the user to utilize a set of EXtended 
    Memory Management services.  M$CVM (read/write access) is the only one 
    available to date. 
    PRIV.ACTIVE.EXPM - BIT(1).  allows the user to start and stop the monitor 
    performance monitor. 
    PRIV.ACTIVE.GPP - BIT(1).  allows a user to override the stealable page 
    limit and acquire physical memory pages. 
    PRIV.ACTIVE.INTCON - BIT(1).  allows the user to use the M$INTCON monitor 
    service. 
    PRIV.ACTIVE.MAXMEM - BIT(1).  allows the user to allocate memory beyond 
    his authorized limit. 
    PRIV.ACTIVE.MSYS - BIT(1).  allows the user to use the M$SYS monitor 
    service and to execute his interrupt processing routines in Ring 1. 
    PRIV.ACTIVE.SCREECH - BIT(1).  allows the user to use M$SCREECH to dump 
    and reboot the Front End. 
    PRIV.ACTIVE.SPCLMM - BIT(1).  allows the user to utilize a set of SPeCiaL 
    Memory Management services.  M$CVM (read only access) is the only one 
    available to date. 
    PRIV.ACTIVE.SYSLOG - BIT(1).  allows the user to use the M$WRSYSLOG 
    monitor service request. 
    PRIV.ACTIVE.TND - BIT(1).  allows the user to use the Test aNd Diagnostic 
    monitor services. 
    PRIV.AUTH - BIT(32).  Contains the user's privilege indicators as defined, 
    via SUPER, in the :USERS file. 
    Refer to the description of G$JIT.PRIV.ACTIVE for the names and the 
    meanings of the individual bits in this field. 
    PRIV.PRC - BIT(32).  Contains the processor privilege bits, as defined by 
    LINK options, from the :SYS processor's head record.  If the currently 
    executing run unit is not from :SYS, PRIV.PRC is set to zero. 
    Refer to the description of G$JIT.PRIV.ACTIVE for the names and the 
    meanings of the individual bits in this field. 
    PROCNAME - TEXTC(31).  Contains the name of the FPRG from the :SYS account 
    for which a process accounting is to be generated. 
    PROFILE - Contains the profile name in TEXTC format: 
    PROFILE.CNT - UBIN BYTE.  Contains the length of PROFILE.TXT. 
    PROFILE.TXT - CHAR(11).  Contains the name of the profile. 
    PROG_ENTRY - UBIN.  Set to indicate how the run-unit was put into 
    execution as follows: 
       G_PE_BF#        0    Started by BIGFOOT 
       G_PE_HOST#      1    Started via Host program 
       G_PE_LDTRC#     2    Started via M$LDTRC. 
    PSEUDOPGS - UBIN.  Contains the total number of pages which the user is 
    charged for but which are not reflected in his ASDT; i.e. the HHJIT pages. 
    PUL - UBIN.  Contains the Procedure Upper Limit, which is the virtual page 
    number of the last procedure page of the run unit or standard shared 
    processor currently executing.  If the user is at job step, JIT.PUL will 
    be set to JIT.PLL -1. 
    READS_HOST - UBIN(32).  Contains a count of the number of reads through a 
    DCB where RES = 'HO' for this job or job step. 
    READS_UC - UBIN(32).  Contains a count of the number of reads through a 
    DCB where RES = 'UC' for this job or job step. 
    RNST - BIT(16).  Is the Program RuN STatus field.  This field contains bit 
    settings that indicate the reason for program termination.  This field may 
    have more than one bit set on to indicate multiple exit conditions. 
    The RNST field in the JIT always contains the "current" run status 
    reported on this user.  This field will be moved to the exit control frame 
    on the Task Control Block.  JIT.RNST is subject to change during exit 
    control processing and should therefore never be referenced by the user 
    program. 
    RNST.ABRT - BIT(1).  is set if termination was caused by a monitor 
    detected error condition.  This may be a program trap when the program has 
    no trap control or an errored monitor service request when there is no 
    ALTRET routine specified. 
    RNST.DSC - BIT(1).  is set if termination was because of path disconnect. 
    RNST.EKEY - BIT(1).  is set if termination was because of a !E keyin by 
    the operator. 
    RNST.ERR - BIT(1).  is set if an M$ERR service request was issued. 
    RNST.INTABRT - BIT(1).  is set if termination occurred at an interrupt 
    level. 
    RNST.LDTRC - BIT(1).  is set if an M$LDTRC service request was issued. 
    RNST.LIMX - BIT(1).  is set if termination is because of a limit that has 
    been exceeded. 
    RNST.OFF - BIT(1).  is set if the monitor is terminating the session. 
    RNST.SSP - BIT(1).  is set if termination was initiated by a Special 
    Shared Processor; i.e., the Debugger. 
    RNST.XKEY - BIT(1).  is set if termination was because of a !X keyin by 
    the operator. 
    RNST.XXX - BIT(1).  is set if an M$XXX service request was issued. 
    RUNFLAGS - BIT(8).  Indicates the currently executing process as follows: 
      G_RUN_MON#    '01'X   Monitor or Command Processor 
      G_RUN_PROC#   '02'X   Processor in :SYS linked with PROCACC 
      G_RUN_USER#   '04'X   User program or processor not linked 
                            with the PROCACC option 
    SCHTIME - UBIN(32).  Is the SCHedule TIME field.  It contains the sum of 
    XTIME and STIME as they existed the last time this user was scheduled for 
    execution. 
    SLIB# - UBIN BYTE.  Contains the associated Shared LIBrary number. 
    SPROC# - UBIN BYTE.  Contains the associated Shared PROCessor number. 
    START - UBIN(32).  Contains the LCP-6 UTS at the time the user or job step 
    was initiated. 
    STEP - UBIN.  Contains the number of job steps that have been executed. 
    STEPCC - UBIN BYTE.  Contains the Step Condition Code.  This field is set 
    from the SEV field of the error code at the time of the exit condition 
    from the user program: 
       G_EXIT#   0    M$EXIT 
       G_ERR#    4    Job step has been errored. 
       G_XXX#    6    Job step has been aborted. 
    STEPUNIT - ARRAY(0:3) UBIN.  Contains a set of four counters that are 
    maintained through a job step and reset to zero at the beginning of each 
    job step.  See M$CHGUNIT and the RATES processor. 
    STIME - UBIN(32).  Is the Service TIME field.  It contains the number of 
    clock ticks of service time used this quantum. 
    STOP - UBIN(32).  Contains the LCP-6 UTS at the time the user or job step 
    was terminated. 
    SYSID - UBIN.  Contains the unique SYStem IDentification number that has 
    been assigned to this user by the system.  All operator communication and 
    external or printed form of user identification is by SYSID. 
    TIMERS - ARRAY(0:2) UBIN(32).  Contains the time, in clock ticks, 
    remaining before expiration of the timer established via M$CLOCK.  The 
    array is indexed by LCP-6 domain.  A value of zero means there is no timer 
    currently established. 
    TUEXT - UBIN(32).  Is the Total User EXecution Time field.  It contains 
    the user execution time used in this job step prior to the current 
    quantum.  This is maintained in clock ticks. 
    TUSVT - UBIN(32).  Is the Total User SerVice Time field.  It contains the 
    user service time used in this job step prior to the current quantum. 
    This is maintained in clock ticks. 
    TYPE - UBIN.  Contains the type of LCP-6 user accounting record.  This 
    field will contain one of the following EQUed values from the AZ_SUBS_C 
    include file: 
        AZ$JOBEND      2 
        AZ$STEP        4 
        AZ$PROC        5 
    UMEMTIM - UBIN(32).  Is the User MEMory TIMe field.  It contains the 
    integral of ((TUEXT + TUSVT) * current memory allocation) over all quanta 
    of the entire job step.  This is maintained in clock ticks * page units. 
    UNAME - CHAR(12).  Is the User NAME field containing the user's log on 
    name. 
    USR# - UBIN.  Contains the User Number that has been assigned to this user 
    by the system.  This number is used internally as an index into the system 
    user tables and is not used for any external user identification. 
    WRITES_HOST - UBIN(32).  Contains a count of the number of writes through 
    a DCB where RES = 'HO' for this job or job step. 
    WRITES_UC - UBIN(32).  Contains a count of the number of writes through a 
    DCB where RES = 'UC' for this job or job step. 
    XLIMFLG - BIT(8).  Is a set of exceeded limit flags. 
    XLIMFLG.TIME - BIT(1).  Is set if the maximum run time has been exceeded. 
    XTIME - UBIN(32).  Is the eXecution TIME field.  It contains the number of 
    clock ticks of execution time used this quantum. 
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
00075
00076
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
00135
00136
00137
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
00156
00157
00158
The G$JIT_E macro, which is in the G_JIT_M INCLUDE file, generates the EQUs to 
be used when referencing the fields within the JIT. 
Refer to the descriptions of the various fields in the G$JIT structure for a 
description of the EQUs that are generated. 
The %G$NWIO macro may be used to generate a based structure of a frame placed 
on the TCB stack for a No-wait I/O event. 
All the fields in the G$NWIO structure are identical to those in G$EXCFR. 
Of special interest here is G$NWIO.TRLR.EVID which will contain the event ID 
as was specified on the M$OPEN service request. 
The standard exceptional condition frame is then followed by: 
    ARS - UBIN  contains the actual record size. 
    CGPARM is described under VLP_CG. 
    DVE.DVBYTE is returned on reads and contains information about the nature 
    of the item read.  See M$DCB.  This field contains the following 
    subfields: 
    DVE.DVBYTE.BIN - BIT(1).  Set if the record was read in binary mode.  This 
    means that data was read bit-by-bit from the medium into the buffer rather 
    than one character per 9 bit byte. 
    DVE.DVBYTE.TRANS - BIT(1).  Set if the record was read in transparent 
    mode.  This means that no translation was performed by the system and the 
    data is that which was read from the I/O medium. This bit is only set in 
    cases where the default read of the record would cause a translation to be 
    done, as with time-sharing terminals. 
    DVE.DVBYTE.VFC - BIT(1).  Set if the first character of the record read 
    should be interpreted as a VFC character. 
    DVE.EOMCHAR - CHAR(1)   contains the activation character of reads. 
    EVID - UBIN contains the event ID as was specified on the M$READ or 
    M$WRITE Service Request. 
    P# - UBIN   contains the number of words of parameters that follow. 
    TRLR.ERR is the 32 bit error code. 
    TRLR.SUBC - UBIN contains the event sub-code. For No-wait I/O completion 
    this field will be set to %G_IO_CMP#. 
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
The G$ROS macro generates a structure that defines the user's Read Only 
Segment. 
The Read Only Segment contains all the information to which the user has read, 
but not write, permission.  This includes: 
  1) the user's Job Information Table which contains various accounting, limit 
     and identity information. 
  2) Exceptional Condition Control Blocks - used to contain information 
     concerning conditions for which the user wishes to receive control. 
     There is a separate ECCB allocated in the Read Only Segment for the user 
     and debugger. 
  3) Task Control Block - used to contain the environment at the time of an 
     exceptional condition or error on a monitor service request. 
  4) The DCB Table which contains the address of each Data Control Block. 
  5) The following "canned" Data Control Blocks: 
       M$DEBUG 
       M$LM 
       M$ME 
       M$HOST 
       M$DO 
  6) An available space header. 
The Read Only Segment may be accessed by using the linker built pointer 
G$ROS$.  The first portion of the Read Only Segment contains pointers to those 
specific areas that follow.  A description of the fields in this portion of 
the Read Only Segment follows. 
    AUTO_DS$ - PTR.  Contains the address of the base of the user AUTO data 
    segment (which depends on the LAUTO option in FEPLINK). 
    AUTO_T$ - PTR.  Contains the address of the stack control words for user 
    AUTO (which depends on the LAUTO option in FEPLINK). 
    AVAIL$ - PTR.  Contains the address of G$ROS.AVAIL_HDR. 
    DB_ECCB$ - PTR.  Contains the address of G$ROS.DB_ECCB which is the 
    Exceptional Condition Control Block for the debugger domain.  Refer to 
    G$ECCB. 
    DCBPTR$ - PTR.  Contains the address of G$ROS.DCBTABLE. 
    JIT$ - PTR.  Contains the address of G$ROS.JIT. 
    NUMDCBS - UBIN.  Contains the number of entries in the DCBTABLE. 
    PIA - ARRAY(0:31) BIT(16).  Is the Processor Information Area in the ROS. 
    PIA is available for use by the debugger. 
    PIA$ - PTR.  Contains the address of G$ROS.PIA. 
    TCB.ALT$ - PTR.  Contains the address of the ALTRET frame on the user's 
    TCB.  This pointer is built by Job Step. 
    TCB.AVSZ - SBIN WORD.  Contains the word size of the available TCB space. 
    TCB.CURRSZ - SBIN WORD.  Contains the word size of the top of stack frame. 
    TCB.STK$ - PTR.  Contains the address of the current top of stack frame on 
    the user's TCB.  This pointer is build by Job Step and maintained by the 
    Exceptional Condition processing routines. 
    U_ECCB$ - PTR.  Contains the address of G$ROS.U_ECCB which is the 
    Exceptional Condition Control Block for the user domain.  Refer to G$ECCB. 
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
The G$ROS_AVAIL_HDR macro may be used to generate the structure that defines 
that available Read Only Segment available space header.  This header may be 
accessed via the pointer at G$ROS.AVAIL$. 
This structure contains the following fields: 
    NEXT$ - PTR.  Contains the address of the next available space header if 
    all of the space in this section has been allocated. 
    NWORDS - UBIN WORD.  Contains the number of words available. 
00001
00002
The G$SEGDESC macro may be used to generate a single Address Space Descriptor. 
The fields within an Address Space Descriptor are: 
    BASE - UBIN(15) contains the starting address of the segment in real 
    memory, in units of 256 words.  The default is 0. 
    EP - BIT(2) contains the lowest privilege Ring number in which the 
    processor must be operating in order to execute within this segment.  Ring 
    number is encoded as ones complement; therefore: 
       Ring 0 (Monitor) - 11 
       Ring 1 (Monitor) - 10 
       Ring 2 (Debugger)- 01 
       Ring 3 (User)    - 00 
    This field may be initialized by specifying {G_RING0# | G_R_MON# | G_R_DB# 
    | G_R_USR#}.  The default is G_RING0#. 
    RP - BIT(2) contains the lowest privilege Ring number in which the 
    processor must be operating in order to read data within this segment. 
    Ring number is encoded as ones complement.  This field may be initialized 
    by specifying {G_RING0# | G_R_MON# | G_R_DB# | G_R_USR#}.  The default is 
    G_RING0#. 
    SIZE - UBIN(9) contains the size of the segment in units of 256 words. 
    The default is 0. 
    V - BIT(1) is the segment validity bit which is set if the segment is 
    valid; reset if the segment does not exist.  This field may be initialized 
    by specifying V={YES|NO}.  The default is YES. 
    WP - BIT(2) contains the lowest privilege Ring number in which the 
    processor must be operating in order to write data within this segment. 
    Ring number is encoded as ones complement.  This field may be initialized 
    by specifying {G_RING0# | G_R_MON# | G_R_DB# | G_R_USR#}.  The default is 
    G_RING0#. 
00001
00002
00003
00004
00005
00006
The G$STACK_HDR macro may be used to generate a structure for the header for 
the header of a stack that is to be managed by the hardware stack 
instructions. 
    CW - SBIN contains the current number of words in use for the stack. 
    MW - UBIN contains the maximum stack size in words. 
00001
00002
The G$STATUS_REG macro may be used to generate a structure that contains the 
Status Register. 
The fields of the Status Register are: 
    ID = VALUE-BIT(2) is the processor identification which is hard-wired and 
    cannot be changed under program control.  These 2 bits are used as the 
    least significant bits of the 10-bit channel number for the processor 
    itself, where the 8 high order bits are always ZERO.  The default is 
    '00'B. 
    LEVEL = VALUE-UBIN(6) contains the interrupt priority level on which the 
    processor is currently executing.  Level 0 is the highest priority level 
    and 63 is the lowest.  The default is 0. 
    QLT = VALUE-BIT(1) indicates whether a unit in the system has successfully 
    completed its Quality Logic Test or not. 
         0 = QLT successfully completed. 
         1 = QLT either still running or failed 
    Default = '0'B. 
    RING = VALUE-BIT(2) contains the currently active Ring value.  Note that 
    ring values are always encoded as ones complement whenever they appear. 
    Thus this field will contain one of the following: 
          11 = Ring 0 - the most privileged; used by the Monitor 
          10 = Ring 1 - also privileged and used by the Monitor 
          01 = Ring 2 - Command Processor or Debugger 
          00 = Ring 3 - User 
    This field may be initialized by specifying {G_RING0# | G_R_MON# | 
    G_R_CPDB# | G_R_USR#}.  The default is G_R_USR#. 
00001
00002
00003
00004
When an exceptional condition occurs over which the user requested control, 
the system saves the environment of the interrupted program.  This action 
enables the user to return to the point of interruption and resume normal 
processing, if the user determines that this is possible. 
When an exceptional condition processing procedure is entered, the environment 
of the interrupted program as well as information specific to the exceptional 
condition is stored in the program Task Control Block (TCB).  The TCB is in 
the Read Only Segment.  The TCB consists of three parts: 
   1.  The TCB header which contains control information and pointers to the 
       next two sections. 
   2.  A fixed area for the program environment when an ALTRET code sequence 
       is to be entered following a monitor service request. 
   3.  An Exceptional Condition Stack containing one or more frames.  A frame 
       is allocated, filled with the program environment from the TSA or ISA, 
       and pushed onto the top of the stack for each exceptional condition. 
       The stack is "popped" (that is, the top frame is released) by the user 
       after the exceptional condition is processed. 
The G$TCB macro may be used to generate a based structure for accessing data 
on the TCB. 
The TCB may be referenced through the linker built pointer, G$TCB$. 
The fields in the TCB header are as follows: 
    ALT$ - PTR   contains a pointer to the ALTRET frame in the TCB. 
    AVSZ - SBIN contains the number of unused words remaining in the TCB 
    Exceptional Condition Stack. 
    CURRSZ - SBIN contains the size of the top frame on the TCB Exceptional 
    Condition Stack. 
    STK$ - PTR contains a pointer to the top frame in the TCB Exceptional 
    Condition Stack. 
00001
00002
00003
00004
The G$TSA macro may be used to generate a structure that defines the entire 
Trap Save Area.  This includes the header where information is stored by the 
hardware, and the extension where the rest of the environment is stored by the 
LCP-6 trap handler. 
    A$ - PTR contains an address associated with the trap. 
    B3$ - PTR contains the contents of the B3 register at the time of the 
    trap. 
    I - BIT(16) contains the trap number and the contents of the Indicator 
    Register at the time of the trap: 
    I.B - BIT(1) may be considered to be a one-bit register loaded by load bit 
    instructions. 
    I.C - BIT(1) is the carry indicator that is set when the "logical" 
    capacity of any of the seven general registers is exceeded. 
    I.G - BIT(1) is the Greater-than Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    I.IO - BIT(1) is the Input/Output Indicator that is set if the last I/O 
    operation was successful. 
    I.L - BIT(1) is the Less-than Indicator that contains the results of the 
    last compare instruction executed by the computer. 
    I.OV - BIT(1) is the overflow indicator that is set when any of the seven 
    general registers overflows its "arithmetic" capacity. 
    I.TRAP# - UBIN(8) contains the trap number associated with the trap.  The 
    hardware stores the trap number as '40'X - Trap Vector#.  This number is 
    then converted to the Trap Vector# by the software.  The following EQUs 
    may be used to determine the type of trap: 
    %G_MCL#             MCL 
    %G_TRACE#           Trace Breakpoint Trap 
    %G_NO_SIP#          Uninstalled SIP Trap 
    %G_TROT#            Watch Dog Timer Runout 
    %G_UNIMPL#          Unimplemented Instruction Trap 
    %G_INT_REG_OV#      Integer Register Overflow Trap 
    %G_S_DBZ#           SIP Divide by Zero Trap 
    %G_S_EXP_OV#        SIP Exponent Overflow Trap 
    %G_STK_UF#          Stack Underflow Trap 
    %G_STK_OV#          Stack Overflow Trap 
    %G_REMOTE_DESC#     Remote Data Descriptor Trap 
    %G_PRIV#            Privilege Violation Trap 
    %G_MEM_PROT#        Memory Protection Trap 
    %G_INT_UR#          Internal Unavailable Resource Trap 
    %G_PROG_ERR#        Program Error Trap 
    %G_INT_MBE#         Internal Memory or Bus Error Trap 
    %G_S_EXP_UF#        SIP Exponent Underflow Trap 
    %G_S_PROG_ERR#      SIP Program Error Trap 
    %G_S_SIGNIF#        SIP Significance Error Trap 
    %G_S_PRECISION#     SIP Precision Error Trap 
    %G_EXT_UR#          External (CIP or SIP) Unavailable Resource 
    %G_EXT_MBE#         External (CIP or SIP) Memory or Bus 
    %G_C_DBZ#           CIP Divide by Zero Trap 
    %G_C_SPEC#          CIP Illegal Specification Trap 
    %G_C_CHAR#          CIP Illegal Character Trap 
    %G_C_TRUNC#         CIP Truncation Trap 
    %G_C_OV#            CIP Overflow Trap 
    %G_CIP_QLT#         CIP QLT Fault 
    %G_SIP_QLT#         SIP QLT Fault 
    %G_EXT_PROT#        CIP or SIP Memory Protect Trap 
    %G_S_ARG#           SIP Illegal Argument Trap 
    I.U - BIT(1) is the Unlike-sign Indicator that contains the results of the 
    last compare instruction executed by the computer. 
    INST - UBIN WORD contains the first word of the current instruction. 
    ISA contains the contents of the hardware environment as stored by a level 
    change within the trap handler.  See G$ISA for the names and meanings of 
    the individual fields within ISA. 
    P$$ - EPTR contains the Program Counter at the time of the trap. 
    R3 - UBIN WORD contains the contents of R3 register at the time of the 
    trap. 
    S - BIT(16) contains the contents of the Status Register at the time of 
    the trap: 
    S.ID - BIT(2) is the processor identification which is hard-wired and 
    cannot be changed under program control.  These 2 bits are used as the 
    least significant bits of the 10-bit channel number for the processor 
    itself, where the 8 high order bits are always ZERO. 
    S.LEVEL - UBIN(6) contains the interrupt priority level on which the 
    processor is currently executing.  Level 0 is the highest priority level 
    and 63 is the lowest. 
    S.QLT - BIT(1) indicates whether a unit in the system has successfully 
    completed its Quality Logic Test or not. 
         0 = QLT successfully completed. 
         1 = QLT either still running or failed 
    S.RING - BIT(2) contains the currently active Ring value.  Note that ring 
    values are always encoded as ones complement whenever they appear.  Thus 
    this field will contain one of the following: 
          11 = Ring 0 - the most privileged; used by the Monitor 
          10 = Ring 1 - also privileged and used by the Monitor 
          01 = Ring 2 - Command Processor or Debugger 
          00 = Ring 3 - User 
    TSAL$ - PTR contains the Trap Save Area Link.  When the TSA is in use, 
    this pointer will be null if this is the only or last trap save area 
    connected to the ISA, or it will point to the next TSA connected to the 
    ISA. 
    Z - BIT(16) contains miscellaneous information relative to the trap as 
    follows: 
    Z.BI - BIT(4) has the following meaning when indexing is specified in the 
    AS: 
         For bit instructions:  4 low order bits of the selected 
                                index register. 
         For byte instructions: 1st bit contains low order bit 
                                of the selected index register. 
    Z.IS - UBIN(4) contains the trapping Instruction Size. 
    Z.R - BIT(2) contains the saved ring number from the System Status 
    Register of the trapped procedure. 
    Z.REG - BIT(1) indicates, if set, that address A is meaningless (e.g. 
    Register address form). 
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
The G$TSA_HDR macro may be used to generate a structure that contains the 
environment as saved by the hardware when a trap occurs. 
After saving the following words, the hardware will set B3 to point to 
G$TSA_HDR.A$: 
    A$ - PTR contains an address associated with the trap. 
    B3$ - PTR contains the contents of the B3 register at the time of the 
    trap. 
    I - BIT(16) contains the trap number and the contents of the Indicator 
    Register at the time of the trap: 
    I.B - BIT(1) may be considered to be a one-bit register loaded by load bit 
    instructions. 
    I.C - BIT(1) is the carry indicator that is set when the "logical" 
    capacity of any of the seven general registers is exceeded. 
    I.G - BIT(1) is the Greater-than Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    I.IO - BIT(1) is the Input/Output Indicator that is set if the last I/O 
    operation was successful. 
    I.L - BIT(1) is the Less-than Indicator that contains the results of the 
    last compare instruction executed by the computer. 
    I.OV - BIT(1) is the overflow indicator that is set when any of the seven 
    general registers overflows its "arithmetic" capacity. 
    I.TRAP# - UBIN(8) contains the trap number associated with the trap.  The 
    hardware stores the trap number as '40'X - Trap Vector#.  This number is 
    then converted to the Trap Vector# by the software.  The following EQUs 
    may be used to determine the type of trap: 
    %G_MCL#             MCL 
    %G_TRACE#           Trace Breakpoint Trap 
    %G_NO_SIP#          Uninstalled SIP Trap 
    %G_TROT#            Watch Dog Timer Runout 
    %G_UNIMPL#          Unimplemented Instruction Trap 
    %G_INT_REG_OV#      Integer Register Overflow Trap 
    %G_S_DBZ#           SIP Divide by Zero Trap 
    %G_S_EXP_OV#        SIP Exponent Overflow Trap 
    %G_STK_UF#          Stack Underflow Trap 
    %G_STK_OV#          Stack Overflow Trap 
    %G_REMOTE_DESC#     Remote Data Descriptor Trap 
    %G_PRIV#            Privilege Violation Trap 
    %G_MEM_PROT#        Memory Protection Trap 
    %G_INT_UR#          Internal Unavailable Resource Trap 
    %G_PROG_ERR#        Program Error Trap 
    %G_INT_MBE#         Internal Memory or Bus Error Trap 
    %G_S_EXP_UF#        SIP Exponent Underflow Trap 
    %G_S_PROG_ERR#      SIP Program Error Trap 
    %G_S_SIGNIF#        SIP Significance Error Trap 
    %G_S_PRECISION#     SIP Precision Error Trap 
    %G_EXT_UR#          External (CIP or SIP) Unavailable Resource 
    %G_EXT_MBE#         External (CIP or SIP) Memory or Bus 
    %G_C_DBZ#           CIP Divide by Zero Trap 
    %G_C_SPEC#          CIP Illegal Specification Trap 
    %G_C_CHAR#          CIP Illegal Character Trap 
    %G_C_TRUNC#         CIP Truncation Trap 
    %G_C_OV#            CIP Overflow Trap 
    %G_CIP_QLT#         CIP QLT Fault 
    %G_SIP_QLT#         SIP QLT Fault 
    %G_EXT_PROT#        CIP or SIP Memory Protect Trap 
    %G_S_ARG#           SIP Illegal Argument Trap 
    I.U - BIT(1) is the Unlike-sign Indicator that contains the results of the 
    last compare instruction executed by the computer. 
    INST - UBIN WORD contains the first word of the current instruction. 
    P$$ - EPTR contains the Program Counter at the time of the trap. 
    R3 - UBIN WORD contains the contents of R3 register at the time of the 
    trap. 
    TSAL$ - PTR contains the Trap Save Area Link.  When the TSA is in use, 
    this pointer will be null if this is the only or last trap save area 
    connected to the ISA, or it will point to the next TSA connected to the 
    ISA.  The default is NIL. 
    Z - BIT(16) contains miscellaneous information relative to the trap as 
    follows: 
    Z.BI - BIT(4) has the following meaning when indexing is specified in the 
    AS: 
         For bit instructions:  4 low order bits of the selected 
                                index register. 
         For byte instructions: 1st bit contains low order bit 
                                of the selected index register. 
    Z.IS - UBIN(4) contains the trapping Instruction Size. 
    Z.R - BIT(2) contains the saved ring number from the System Status 
    Register of the trapped procedure. 
    Z.REG - BIT(1) indicates, if set, that address A is meaningless (e.g. 
    Register address form). 
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
The User Housekeeping Job Information Table (UHJIT) contains the data required 
by the hardware and the LCP-6 Scheduler for running a user. 
The G$UHJIT macro, which is contained in the G_HJIT_M include file, may be 
used to generate a structure defining the UHJIT.  Because the G$UHJIT macro 
requires some of the macros contained in the GH_LCP6_M include file, GH_LCP6_M 
(or LCP_6) must also be specified as an include file in a compile unit that 
requires the G$UHJIT structure. 
A user may reference the UHJIT through the pointer G$UHJIT$.  This pointer is 
defined in the G_UPTRS_D object unit file. 
The fields within the UHJIT of particular interest to the system programmer 
are: 
    ASDT_MCL - The MCL Address Space Descriptor Table contains the segment 
    descriptors that are loaded into the Memory Management Unit while 
    processing a user's monitor service request. 
    ASDT_USR - The User Address Space Descriptor Table contains the segment 
    descriptors that are loaded into the Memory Management Unit for user 
    program execution. 
    ISA_USR - The User Interrupt Save Area is accessed by the hardware on the 
    occurrence of the user's interrupt level.  Refer to the description of 
    G$ISA. 
    TSA_USR - The User Trap Save Area is used by the hardware and the LCP-6 
    system to store the environment at the time of a user trap.  Refer to the 
    description of G$TSA. 
    UHJIT.DMN.ID - UBIN contains the DoMaiN IDentification which indicates 
    which process is running; Monitor, Debugger, User, user Interrupt Level, 
    or monitor service.  The value will be one of the following EQUated values 
    from the G_LCP6_E (or LCP_6) include file: 
    %G_DMN_MON_SVC  0       %G_DMN_MON  4 
    %G_DMN_DB_SVC   1       %G_DMN_DB   5 
    %G_DMN_INT_SVC  2       %G_DMN_INT  6 
    %G_DMN_USR_SVC  3       %G_DMN_USR  7 
00001
00002
00003
00004
00005
The G$VECTOR macro generates a structure that defines the LCP-6 vector. 
There are no provisions for specification of initial values.  The default for 
STCLASS is BASED. 
The fields within this structure are as follows: 
    BASE$ - PTR contains the base address of the data framed by this vector. 
    This field is REDEFed as CPTR$ and CBASE. 
    BND - UBIN  contains the bound (size-1) of the area framed by this vector. 
    CBASE.ADDRS - VALUE-UBIN(20) contains a UBIN value for the base address of 
    the data framed by this vector. 
    CBASE.C - BIT(1) indicates, if set, that the pointer is a character 
    pointer. 
    CPTR$ - CPTR redefines BASE$. 
00001
00002
00003
00004
00005
Returns from function subroutines should be done by a transfer to X6A_FARET if 
the function subroutine uses AUTO storage. 
A 
  A$ -   
    G$TSA - 
      HELP G$TSA A$ 
    G$TSA_HDR - 
      HELP G$TSA_HDR A$ 
  Abort Program - 
      HELP M$XXX 
  ABORTREAD -   
    M$TRMPRG - 
      HELP M$TRMPRG ABORTREAD 
  ABSGRPRND -   
    VLP_FLDATR - 
      HELP VLP_FLDATR ABSGRPRND 
  ACCN -   
    G$JIT - 
      HELP G$JIT ACCN 
  ACCT -   
    M$LDTRC - 
      HELP M$LDTRC ACCT 
  ACCTLOG -   
    G$JIT - 
      HELP G$JIT ACCTLOG 
  ACCTLOG.FCN -   
    G$JIT - 
      HELP G$JIT ACCTLOG.FCN 
  ACCTLOG.FILENUM -   
    G$JIT - 
      HELP G$JIT ACCTLOG.FILENUM 
  ACPALL -   
    VLP_FLDATR - 
      HELP VLP_FLDATR ACPALL 
  ACPALP -   
    VLP_FLDATR - 
      HELP VLP_FLDATR ACPALP 
  ACPGRP -   
    VLP_FLDATR - 
      HELP VLP_FLDATR ACPGRP 
  ACPNMR -   
    VLP_FLDATR - 
      HELP VLP_FLDATR ACPNMR 
  ACTONTRN -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL ACTONTRN 
  ACTPOS -   
    M$DCB - 
      HELP M$DCB ACTPOS 
  Address Space Descriptor Table (ASDT) - 
      HELP SAMPLE_FEP_PROGRAMS 
  ADJTOPLFT -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL ADJTOPLFT 
  ALT$ -   
    G$TCB - 
      HELP G$TCB ALT$ 
  ALTCODE -   
    M$ERRMSG - 
      HELP M$ERRMSG ALTCODE 
  ALTEMPTY -   
    G$EXCFR - 
      HELP G$EXCFR ALTEMPTY 
  ALTMSG -   
    VLR_ERRMSG - 
      HELP VLR_ERRMSG ALTMSG 
  APL -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR APL 
  APLLCNRM -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL APLLCNRM 
  ARS -   
    G$COMIO - 
      HELP G$COMIO ARS 
    G$NWIO - 
      HELP G$NWIO ARS 
    M$DCB - 
      HELP M$DCB ARS 
  ASDT - 
      HELP SAMPLE_FEP_PROGRAMS 
  ASDT_MCL -   
    G$UHJIT - 
      HELP G$UHJIT ASDT_MCL 
  ASDT_USR -   
    G$UHJIT - 
      HELP G$UHJIT ASDT_USR 
  ASV$ -   
    G$ISA_HDR - 
      HELP G$ISA_HDR ASV$ 
  ATRSCRNPOS -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR ATRSCRNPOS 
  ATTR -   
    M$GCHAN - 
      HELP M$GCHAN ATTR 
  AUTH -   
    M$SPRIV - 
      HELP M$SPRIV AUTH 
  AUTHORIZED -   
    VLR_GDDL - 
      HELP VLR_GDDL AUTHORIZED 
  AUTOCURSOR -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL AUTOCURSOR 
  Automatic Storage Layout - 
      HELP AUTOMATIC_STORAGE_LAYOUT 
  AUTONL -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR AUTONL 
  AUTOTABCLM -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL AUTOTABCLM 
  AUTO_DS$ -   
    G$ROS - 
      HELP G$ROS AUTO_DS$ 
  AUTO_T$ -   
    G$ROS - 
      HELP G$ROS AUTO_T$ 
  AUTO_TYPE -   
    G$BASE - 
      HELP G$BASE AUTO_TYPE 
  AVAIL$ -   
    G$ROS - 
      HELP G$ROS AVAIL$ 
  AVSZ -   
    G$TCB - 
      HELP G$TCB AVSZ 
B 
  B -   
    G$INDICATOR_REG - 
      HELP G$INDICATOR_REG B 
  B$TERMINAL_ID - Structure Defining a Terminal ID - 
      HELP B$TERMINAL_ID 
  B3$ -   
    G$TSA - 
      HELP G$TSA B3$ 
    G$TSA_HDR - 
      HELP G$TSA_HDR B3$ 
    M$RETRY - 
      HELP M$RETRY B3$ 
  BASE -   
    G$SEGDESC - 
      HELP G$SEGDESC BASE 
    VLP_SEGMENT - 
      HELP VLP_SEGMENT BASE 
  BASE$ -   
    G$VECTOR - 
      HELP G$VECTOR BASE$ 
  BAUTO_DS Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  BILL -   
    G$JIT - 
      HELP G$JIT BILL 
  BIN -   
    M$PROMPT - 
      HELP M$PROMPT BIN 
    VLP_TRMATTR - 
      HELP VLP_TRMATTR BIN 
  BLANKERASES -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR BLANKERASES 
  Bn -   
    G$ISM1 - 
      HELP G$ISM1 Bn 
  Bn$ -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS Bn$ 
  BND -   
    G$VECTOR - 
      HELP G$VECTOR BND 
  BOTTOM_FRAME$ -   
    G$BASE - 
      HELP G$BASE BOTTOM_FRAME$ 
  BP -   
    M$WRITE - 
      HELP M$WRITE BP 
  BREAKCOUNT -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL BREAKCOUNT 
  BRKABLE -   
    M$READ - 
      HELP M$READ BRKABLE 
  BTMBRDR -   
    VLP_WINDOW - 
      HELP VLP_WINDOW BTMBRDR 
  BUF -   
    M$DCLFLD - 
      HELP M$DCLFLD BUF 
    M$ERRMSG - 
      HELP M$ERRMSG BUF 
    M$MDFFLD - 
      HELP M$MDFFLD BUF 
    M$READ - 
      HELP M$READ BUF 
    M$SINPUT - 
      HELP M$SINPUT BUF 
    M$WRITE - 
      HELP M$WRITE BUF 
    M$WRSYSLOG - 
      HELP M$WRSYSLOG BUF 
    M$WRTMLT - 
      HELP M$WRTMLT BUF 
  Build Data Control Block - 
      HELP M$GETDCB 
C 
  C -   
    G$INDICATOR_REG - 
      HELP G$INDICATOR_REG C 
  CALCNT -   
    G$JIT - 
      HELP G$JIT CALCNT 
  calling sequences - 
      HELP SAMPLE_FEP_PROGRAMS 
  Calls to Unknown Routines - 
      HELP CALLS_TO_UNKNOWN_ROUTINES 
  CANCEL -   
    M$CLOCK - 
      HELP M$CLOCK CANCEL 
  CBASE.ADDRS -   
    G$VECTOR - 
      HELP G$VECTOR CBASE.ADDRS 
  CBASE.C -   
    G$VECTOR - 
      HELP G$VECTOR CBASE.C 
  CCBUF -   
    G$JIT - 
      HELP G$JIT CCBUF 
  Certain PL-6 Data Types - 
      HELP CERTAIN_PL_6_DATA_TYPES 
  CG -   
    M$READ - 
      HELP M$READ CG 
    M$WRITE - 
      HELP M$WRITE CG 
  CGPARM -   
    G$NWIO - 
      HELP G$NWIO CGPARM 
  Change Device Attributes - 
      HELP M$DEVICE 
  Change Virtual Map - 
      HELP M$CVM 
  Changes since Previous Manual - 
      HELP CHANGES 
  CHANNEL -   
    M$GCHAN - 
      HELP M$GCHAN CHANNEL 
    M$RCHAN - 
      HELP M$RCHAN CHANNEL 
    VLR_GCHAN - 
      HELP VLR_GCHAN CHANNEL 
  CHARSETNAME -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR CHARSETNAME 
  CHN -   
    G$DEV - 
      HELP G$DEV CHN 
  CI -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS CI 
  CI.G -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS CI.G 
  CI.L -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS CI.L 
  CI.OV -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS CI.OV 
  CI.QLT -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS CI.QLT 
  CI.SF -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS CI.SF 
  CI.TR -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS CI.TR 
  CIP -   
    G$ISM2 - 
      HELP G$ISM2 CIP 
  CIP_OV -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS CIP_OV 
  CIP_QLT -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS CIP_QLT 
  CIP_TR -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS CIP_TR 
  circular queues - 
      HELP SAMPLE_FEP_PROGRAMS 
  Clear the TCB Stack Frame - 
      HELP M$CLRSTK 
  CLM -   
    M$DCLFLD - 
      HELP M$DCLFLD CLM 
  CLOCK -   
    M$CLOCK - 
      HELP M$CLOCK CLOCK 
  Close DCB - 
      HELP M$CLOSE 
  CLUKRINT -   
    G$JIT - 
      HELP G$JIT CLUKRINT 
  CLUKRLVL -   
    G$JIT - 
      HELP G$JIT CLUKRLVL 
  CLUKXINT -   
    G$JIT - 
      HELP G$JIT CLUKXINT 
  CLUKXLVL -   
    G$JIT - 
      HELP G$JIT CLUKXLVL 
  CMD -   
    M$LDTRC - 
      HELP M$LDTRC CMD 
  CNS -   
    M$ERASE - 
      HELP M$ERASE CNS 
    VLP_FLDATR - 
      HELP VLP_FLDATR CNS 
  CODE -   
    G$JIT - 
      HELP G$JIT CODE 
    M$ERRMSG - 
      HELP M$ERRMSG CODE 
  Comgroup Message Parameter - 
      HELP VLP_CG 
  Communications IO Event Frame - 
      HELP G$COMIO 
  Connect to Interrupt - 
      HELP M$INTCON 
  Control Of System Privileges - 
      HELP M$SPRIV 
  CONTROLLER -   
    M$GCHAN - 
      HELP M$GCHAN CONTROLLER 
    M$RCHAN - 
      HELP M$RCHAN CONTROLLER 
    VLP_LINEATTR - 
      HELP VLP_LINEATTR CONTROLLER 
  COUNT -   
    VLP_HDR - 
      HELP VLP_HDR COUNT 
  CPTR$ -   
    G$VECTOR - 
      HELP G$VECTOR CPTR$ 
  CP_DS Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  CP_PROC Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  CQ -   
    VLP_PRIV - 
      HELP VLP_PRIV CQ 
  CQPC -   
    G$JIT - 
      HELP G$JIT CQPC 
  CRISNL -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR CRISNL 
  CTXSIZE -   
    VLP_HMI - 
      HELP VLP_HMI CTXSIZE 
  CURRLVLS -   
    G$JIT - 
      HELP G$JIT CURRLVLS 
  CURRSZ -   
    G$TCB - 
      HELP G$TCB CURRSZ 
  CURSORHERE -   
    M$TRMPRG - 
      HELP M$TRMPRG CURSORHERE 
  CURSORREAD -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL CURSORREAD 
  CURSORUP -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR CURSORUP 
  CURSUDO -   
    G$JIT - 
      HELP G$JIT CURSUDO 
  CUR_T_REG -   
    G$BASE - 
      HELP G$BASE CUR_T_REG 
  CUR_USED -   
    G$AUTO_HEAD - 
      HELP G$AUTO_HEAD CUR_USED 
  CVM_REAL -   
    G$JIT - 
      HELP G$JIT CVM_REAL 
  CW -   
    G$STACK_HDR - 
      HELP G$STACK_HDR CW 
  C_CHAR -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS C_CHAR 
  C_DBZ -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS C_DBZ 
  C_OV -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS C_OV 
  C_SPEC -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS C_SPEC 
  C_TRUNC -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS C_TRUNC 
D 
  Data Control Block - 
      HELP M$DCB 
  Data Control Block (DCB) - 
      HELP SAMPLE_FEP_PROGRAMS 
  DATE -   
    M$TIME - 
      HELP M$TIME DATE 
  DAY -   
    M$TIME - 
      HELP M$TIME DAY 
  DB# -   
    G$JIT - 
      HELP G$JIT DB# 
  DB_ACCN -   
    G$JIT - 
      HELP G$JIT DB_ACCN 
  DB_DS Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  DB_ECCB$ -   
    G$ROS - 
      HELP G$ROS DB_ECCB$ 
  DB_PROC Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  DB_WRTSEGS -   
    G$JIT - 
      HELP G$JIT DB_WRTSEGS 
  DCB -   
    M$CLOSE - 
      HELP M$CLOSE DCB 
    M$DCB - 
      HELP M$DCB DCB 
    M$DCLFLD - 
      HELP M$DCLFLD DCB 
    M$DEVICE - 
      HELP M$DEVICE DCB 
    M$EOM - 
      HELP M$EOM DCB 
    M$ERASE - 
      HELP M$ERASE DCB 
    M$GLINEATTR - 
      HELP M$GLINEATTR DCB 
    M$GTRMCTL - 
      HELP M$GTRMCTL DCB 
    M$GTRMTAB - 
      HELP M$GTRMTAB DCB 
    M$MDFFLD - 
      HELP M$MDFFLD DCB 
    M$OPEN - 
      HELP M$OPEN DCB 
    M$PLATEN - 
      HELP M$PLATEN DCB 
    M$PROMPT - 
      HELP M$PROMPT DCB 
    M$READ - 
      HELP M$READ DCB 
    M$RELDCB - 
      HELP M$RELDCB DCB 
    M$RLSFLD - 
      HELP M$RLSFLD DCB 
    M$SINPUT - 
      HELP M$SINPUT DCB 
    M$SLCFLD - 
      HELP M$SLCFLD DCB 
    M$STRMATTR - 
      HELP M$STRMATTR DCB 
    M$TRMPRG - 
      HELP M$TRMPRG DCB 
    M$WRITE - 
      HELP M$WRITE DCB 
    M$WRTMLT - 
      HELP M$WRTMLT DCB 
  DCB# -   
    G$EXCFR - 
      HELP G$EXCFR DCB# 
    M$DCB - 
      HELP M$DCB DCB# 
  DCB - 
      HELP NOTATION 
      HELP SAMPLE_FEP_PROGRAMS 
  DCBNAME -   
    M$DCB - 
      HELP M$DCB DCBNAME 
    M$GETDCB - 
      HELP M$GETDCB DCBNAME 
  DCBNAME.L -   
    M$DCB - 
      HELP M$DCB DCBNAME.L 
  DCBNAME.NAME -   
    M$DCB - 
      HELP M$DCB DCBNAME.NAME 
  DCBNUM -   
    M$GETDCB - 
      HELP M$GETDCB DCBNUM 
  DCBPTR$ -   
    G$ROS - 
      HELP G$ROS DCBPTR$ 
  DCHMOVFLD -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR DCHMOVFLD 
  DCRINT -   
    VLP_FLDATR - 
      HELP VLP_FLDATR DCRINT 
  Declare a Field. - 
      HELP M$DCLFLD 
  DEST -   
    M$TIME - 
      HELP M$TIME DEST 
  DEV -   
    G$ISA - 
      HELP G$ISA DEV 
    G$ISA_MINI - 
      HELP G$ISA_MINI DEV 
  DEV.CHN -   
    G$ISA - 
      HELP G$ISA DEV.CHN 
  DEV.IL -   
    G$ISA - 
      HELP G$ISA DEV.IL 
  DEVICE -   
    VLP_LINEATTR - 
      HELP VLP_LINEATTR DEVICE 
  DEVICEBS -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR DEVICEBS 
  DEVICECR -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR DEVICECR 
  DEVICELF -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR DEVICELF 
  DEVPOSOPTS -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR DEVPOSOPTS 
  DEVSCROLL -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR DEVSCROLL 
  DIAG -   
    M$GCHAN - 
      HELP M$GCHAN DIAG 
  DISP -   
    M$CLOSE - 
      HELP M$CLOSE DISP 
    M$DCB - 
      HELP M$DCB DISP 
    M$LDTRC - 
      HELP M$LDTRC DISP 
    M$OPEN - 
      HELP M$OPEN DISP 
  DISPINPUT -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL DISPINPUT 
  DLL -   
    G$JIT - 
      HELP G$JIT DLL 
  DSPHEIGHT -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR DSPHEIGHT 
  DUL -   
    G$JIT - 
      HELP G$JIT DUL 
  DVBYTE -   
    M$DCB - 
      HELP M$DCB DVBYTE 
  DVBYTE.BIN -   
    M$DCB - 
      HELP M$DCB DVBYTE.BIN 
  DVBYTE.BP -   
    M$DCB - 
      HELP M$DCB DVBYTE.BP 
  DVBYTE.TRANS -   
    M$DCB - 
      HELP M$DCB DVBYTE.TRANS 
  DVBYTE.VFC -   
    M$DCB - 
      HELP M$DCB DVBYTE.VFC 
  DVCATTR -   
    VLR_GCHAN - 
      HELP VLR_GCHAN DVCATTR 
  DVCFLWCTRALG -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR DVCFLWCTRALG 
  DVCID -   
    VLR_GCHAN - 
      HELP VLR_GCHAN DVCID 
  DVCRES -   
    VLR_GCHAN - 
      HELP VLR_GCHAN DVCRES 
  DVE.DVBYTE -   
    G$NWIO - 
      HELP G$NWIO DVE.DVBYTE 
  DVE.DVBYTE.BIN -   
    G$NWIO - 
      HELP G$NWIO DVE.DVBYTE.BIN 
  DVE.DVBYTE.TRANS -   
    G$NWIO - 
      HELP G$NWIO DVE.DVBYTE.TRANS 
  DVE.DVBYTE.VFC -   
    G$NWIO - 
      HELP G$NWIO DVE.DVBYTE.VFC 
  DVE.EOMCHAR -   
    G$NWIO - 
      HELP G$NWIO DVE.EOMCHAR 
  DVFC -   
    M$DCB - 
      HELP M$DCB DVFC 
    M$DEVICE - 
      HELP M$DEVICE DVFC 
    M$OPEN - 
      HELP M$OPEN DVFC 
E 
  ECC -   
    G$EXCFR - 
      HELP G$EXCFR ECC 
  ECCB (also see G$ECCB) - 
      HELP SAMPLE_FEP_PROGRAMS 
  EDITOVR -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL EDITOVR 
  ENB -   
    M$GCHAN - 
      HELP M$GCHAN ENB 
  ENBENTEXTSRDCHR -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL ENBENTEXTSRDCHR 
  Enter Privileged Mode - 
      HELP M$SYS 
  ENTRY - 
      HELP NOTATION 
  EOM -   
    M$WRITE - 
      HELP M$WRITE EOM 
  EOMCHAR -   
    M$DCB - 
      HELP M$DCB EOMCHAR 
    M$WRITE - 
      HELP M$WRITE EOMCHAR 
  EOMTABLE -   
    M$EOM - 
      HELP M$EOM EOMTABLE 
  EP -   
    G$SEGDESC - 
      HELP G$SEGDESC EP 
  Erase Fields or Records - 
      HELP M$ERASE 
  ERR -   
    G$JIT - 
      HELP G$JIT ERR 
  ERR# -   
    VLP_ERRCODE - 
      HELP VLP_ERRCODE ERR# 
    VLP_SCODE - 
      HELP VLP_SCODE ERR# 
  ERR.ERR# -   
    G$JIT - 
      HELP G$JIT ERR.ERR# 
  ERR.FCG -   
    G$JIT - 
      HELP G$JIT ERR.FCG 
  ERR.MID -   
    G$JIT - 
      HELP G$JIT ERR.MID 
  ERR.MON -   
    G$JIT - 
      HELP G$JIT ERR.MON 
  ERR.SEV -   
    G$JIT - 
      HELP G$JIT ERR.SEV 
  ERRCODE -   
    M$ERR - 
      HELP M$ERR ERRCODE 
    M$EXIT - 
      HELP M$EXIT ERRCODE 
    M$MERC - 
      HELP M$MERC ERRCODE 
    M$XXX - 
      HELP M$XXX ERRCODE 
  ERRLOG_LVL -   
    G$JIT - 
      HELP G$JIT ERRLOG_LVL 
  Error Program - 
      HELP M$ERR 
  EVENT -   
    M$DCB - 
      HELP M$DCB EVENT 
    M$INTRET - 
      HELP M$INTRET EVENT 
    M$OPEN - 
      HELP M$OPEN EVENT 
    M$READ - 
      HELP M$READ EVENT 
    M$WRITE - 
      HELP M$WRITE EVENT 
  EVENT$ -   
    G$ECCB - 
      HELP G$ECCB EVENT$ 
    M$EVENT - 
      HELP M$EVENT EVENT$ 
  EVID -   
    G$NWIO - 
      HELP G$NWIO EVID 
  Exceptional Condition Control Blocks (ECCB) - 
      HELP SAMPLE_FEP_PROGRAMS 
  Exceptional Condition Frame - 
      HELP G$EXCFR 
  Exit Program - 
      HELP M$EXIT 
  EXMM -   
    VLP_PRIV - 
      HELP VLP_PRIV EXMM 
  EXPM -   
    VLP_PRIV - 
      HELP VLP_PRIV EXPM 
  EXTDVCID -   
    VLR_GCHAN - 
      HELP VLR_GCHAN EXTDVCID 
  EXTWID -   
    VLP_PLATEN - 
      HELP VLP_PLATEN EXTWID 
    VLP_TRMATTR - 
      HELP VLP_TRMATTR EXTWID 
  EXT_MBE -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS EXT_MBE 
  EXT_PROT -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS EXT_PROT 
  EXT_UR -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS EXT_UR 
F 
  FCD -   
    M$DCB - 
      HELP M$DCB FCD 
  FCG -   
    M$WRSYSLOG - 
      HELP M$WRSYSLOG FCG 
    VLP_ERRCODE - 
      HELP VLP_ERRCODE FCG 
    VLP_SCODE - 
      HELP VLP_SCODE FCG 
  FCI -   
    M$DCB - 
      HELP M$DCB FCI 
  FCNTBL -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR FCNTBL 
  FD_ALTERR -   
    G$JIT - 
      HELP G$JIT FD_ALTERR 
  FD_P$ -   
    G$JIT - 
      HELP G$JIT FD_P$ 
  FEP# -   
    G$JIT - 
      HELP G$JIT FEP# 
  FEP Monitor Services HELP Facility - 
      HELP FEP_MONITOR SERVICES_HELP FACILITY 
  FFLG -   
    M$DCB - 
      HELP M$DCB FFLG 
  FFLG.READ -   
    M$DCB - 
      HELP M$DCB FFLG.READ 
  FFLG.WRITE -   
    M$DCB - 
      HELP M$DCB FFLG.WRITE 
  FF_FLUSH -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR FF_FLUSH 
  FF_INCCR -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR FF_INCCR 
  FILEACCT -   
    M$ERRMSG - 
      HELP M$ERRMSG FILEACCT 
  FILENAME -   
    M$ERRMSG - 
      HELP M$ERRMSG FILENAME 
  FILENUM -   
    M$WRSYSLOG - 
      HELP M$WRSYSLOG FILENUM 
  FILEPASS -   
    M$ERRMSG - 
      HELP M$ERRMSG FILEPASS 
  FIRSTLINE -   
    VLP_PLATEN - 
      HELP VLP_PLATEN FIRSTLINE 
  FIRST_SEG -   
    G$JIT - 
      HELP G$JIT FIRST_SEG 
  FLAGLEV -   
    M$ERRMSG - 
      HELP M$ERRMSG FLAGLEV 
  FLAGS -   
    G$ECCB - 
      HELP G$ECCB FLAGS 
  FLAGS.EXTD_LIM -   
    G$ECCB - 
      HELP G$ECCB FLAGS.EXTD_LIM 
  FLAGS.TCBFULL -   
    G$ECCB - 
      HELP G$ECCB FLAGS.TCBFULL 
  FLAGS.XCONP -   
    G$ECCB - 
      HELP G$ECCB FLAGS.XCONP 
  FLDATR -   
    M$DCLFLD - 
      HELP M$DCLFLD FLDATR 
    M$MDFFLD - 
      HELP M$MDFFLD FLDATR 
  FLDID -   
    M$DCB - 
      HELP M$DCB FLDID 
  FLTFLG -   
    G$ECCB - 
      HELP G$ECCB FLTFLG 
  FOREIGN -   
    VLP_LINEATTR - 
      HELP VLP_LINEATTR FOREIGN 
  FRAMES -   
    M$CLRSTK - 
      HELP M$CLRSTK FRAMES 
  FREE -   
    M$GAUTO - 
      HELP M$GAUTO FREE 
    M$GDS - 
      HELP M$GDS FREE 
  Free / Diminish Auto Segment - 
      HELP M$FAUTO 
  Free / Diminish Data Segment - 
      HELP M$FDS 
  FROMSEG -   
    M$CVM - 
      HELP M$CVM FROMSEG 
  FRS -   
    G$JIT - 
      HELP G$JIT FRS 
  FRS.ABRT -   
    G$JIT - 
      HELP G$JIT FRS.ABRT 
  FRS.DSC -   
    G$JIT - 
      HELP G$JIT FRS.DSC 
  FRS.EKEY -   
    G$JIT - 
      HELP G$JIT FRS.EKEY 
  FRS.INTABRT -   
    G$JIT - 
      HELP G$JIT FRS.INTABRT 
  FRS.LIMX -   
    G$JIT - 
      HELP G$JIT FRS.LIMX 
  FRS.OFF -   
    G$JIT - 
      HELP G$JIT FRS.OFF 
  FRS.SSP -   
    G$JIT - 
      HELP G$JIT FRS.SSP 
  FRS.XKEY -   
    G$JIT - 
      HELP G$JIT FRS.XKEY 
  FSTBLN -   
    VLP_FLDATR - 
      HELP VLP_FLDATR FSTBLN 
  FULLDUXPAPERTAPE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL FULLDUXPAPERTAPE 
  FWINDOW -   
    VLP_WINDOW - 
      HELP VLP_WINDOW FWINDOW 
G 
  G -   
    G$INDICATOR_REG - 
      HELP G$INDICATOR_REG G 
  G$ASDT - 
      HELP G$ASDT 
  G$ASDT_USR - 
      HELP G$ASDT_USR 
  G$AUTO_HEAD Structure - 
      HELP G$AUTO_HEAD 
  G$BASE Structure - 
      HELP G$BASE 
  G$COMIO - Communications IO Event Frame - 
      HELP G$COMIO 
  G$DCBTABLE - 
      HELP G$DCBTABLE 
  G$DEV - 
      HELP G$DEV 
  G$ECCB - Exception Condition Control Block - 
      HELP G$ECCB 
  G$EXCFR - Exceptional Condition Frame - 
      HELP G$EXCFR 
  G$FRAME Structure - 
      HELP G$FRAME 
  G$INDICATOR_REG - 
      HELP G$INDICATOR_REG 
  G$ISA - 
      HELP G$ISA 
  G$ISA_HDR - 
      HELP G$ISA_HDR 
  G$ISA_MINI - 
      HELP G$ISA_MINI 
  G$ISM1 - 
      HELP G$ISM1 
  G$ISM2 - 
      HELP G$ISM2 
  G$JIT - 
      HELP G$JIT 
  G$JIT_E - 
      HELP G$JIT_E 
  G$NWIO - No-Wait IO Event Frame - 
      HELP G$NWIO 
  G$ROS - 
      HELP G$ROS 
  G$ROS_AVAIL_HDR - 
      HELP G$ROS_AVAIL_HDR 
  G$SEGDESC - 
      HELP G$SEGDESC 
  G$STACK_HDR - 
      HELP G$STACK_HDR 
  G$STATUS_REG - 
      HELP G$STATUS_REG 
  G$TCB  - Saving the User Environment - 
      HELP G$TCB 
  G$TSA - 
      HELP G$TSA 
  G$TSA_HDR - 
      HELP G$TSA_HDR 
  G$UHJIT - 
      HELP G$UHJIT 
  G$VECTOR - 
      HELP G$VECTOR 
  GCHAN -   
    M$GCHAN - 
      HELP M$GCHAN GCHAN 
  General Function Calling Sequences - 
      HELP GENERAL_CALLING_SEQUENCES 
  Get / Enlarge Auto Segment - 
      HELP M$GAUTO 
  Get / Enlarge Data Segment - 
      HELP M$GDS 
  Get a Channel. - 
      HELP M$GCHAN 
  Get Dynamic Data Limits - 
      HELP M$GDDL 
  Get Line Attributes - 
      HELP M$GLINEATTR 
  GFR_ACCT -   
    G$JIT - 
      HELP G$JIT GFR_ACCT 
  GPP -   
    VLP_PRIV - 
      HELP VLP_PRIV GPP 
H 
  HALFDUXPAPERTAPE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL HALFDUXPAPERTAPE 
  HAND$ -   
    G$ECCB - 
      HELP G$ECCB HAND$ 
  Handler/Monitor Interface Parameter - 
      HELP VLP_HMI 
  HAND_Q Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  HARDWIRE -   
    VLP_LINEATTR - 
      HELP VLP_LINEATTR HARDWIRE 
  HBRDRCHR -   
    VLP_WINDOW - 
      HELP VLP_WINDOW HBRDRCHR 
  HBRDRSIZ -   
    VLP_WINDOW - 
      HELP VLP_WINDOW HBRDRSIZ 
  HDN -   
    VLP_FLDATR - 
      HELP VLP_FLDATR HDN 
  HDR -   
    M$DEVICE - 
      HELP M$DEVICE HDR 
    M$OPEN - 
      HELP M$OPEN HDR 
  Header Parameter - 
      HELP VLP_HDR 
  HEADERHEIGHT -   
    VLP_HDR - 
      HELP VLP_HDR HEADERHEIGHT 
  HEIGHT -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR HEIGHT 
  HELP - 
      HELP FEP_MONITOR SERVICES_HELP FACILITY 
  HIGHCHAN -   
    VLR_GCHAN - 
      HELP VLR_GCHAN HIGHCHAN 
  HIGHLOW -   
    M$GCHAN - 
      HELP M$GCHAN HIGHLOW 
  HMI -   
    M$OPEN - 
      HELP M$OPEN HMI 
  HMI$ -   
    M$DCB - 
      HELP M$DCB HMI$ 
  HSCROLL -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL HSCROLL 
  HSMARGIN -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL HSMARGIN 
  HSSHIFT -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL HSSHIFT 
I 
  I -   
    G$ISM1 - 
      HELP G$ISM1 I 
    G$TSA - 
      HELP G$TSA I 
    G$TSA_HDR - 
      HELP G$TSA_HDR I 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS I 
  I.B -   
    G$TSA - 
      HELP G$TSA I.B 
    G$TSA_HDR - 
      HELP G$TSA_HDR I.B 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS I.B 
  I.C -   
    G$TSA - 
      HELP G$TSA I.C 
    G$TSA_HDR - 
      HELP G$TSA_HDR I.C 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS I.C 
  I.G -   
    G$TSA - 
      HELP G$TSA I.G 
    G$TSA_HDR - 
      HELP G$TSA_HDR I.G 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS I.G 
  I.IO -   
    G$TSA - 
      HELP G$TSA I.IO 
    G$TSA_HDR - 
      HELP G$TSA_HDR I.IO 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS I.IO 
  I.L -   
    G$TSA - 
      HELP G$TSA I.L 
    G$TSA_HDR - 
      HELP G$TSA_HDR I.L 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS I.L 
  I.OV -   
    G$TSA - 
      HELP G$TSA I.OV 
    G$TSA_HDR - 
      HELP G$TSA_HDR I.OV 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS I.OV 
  I.TRAP# -   
    G$TSA - 
      HELP G$TSA I.TRAP# 
    G$TSA_HDR - 
      HELP G$TSA_HDR I.TRAP# 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS I.TRAP# 
  I.U -   
    G$TSA - 
      HELP G$TSA I.U 
    G$TSA_HDR - 
      HELP G$TSA_HDR I.U 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS I.U 
  ID -   
    G$STATUS_REG - 
      HELP G$STATUS_REG ID 
    M$DCLFLD - 
      HELP M$DCLFLD ID 
  IDELTAT -   
    G$JIT - 
      HELP G$JIT IDELTAT 
  IENTRY -   
    M$INTCON - 
      HELP M$INTCON IENTRY 
  IGN_IO -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS IGN_IO 
  IL -   
    G$DEV - 
      HELP G$DEV IL 
  INCINT -   
    VLP_FLDATR - 
      HELP VLP_FLDATR INCINT 
  INCLCODE -   
    M$ERRMSG - 
      HELP M$ERRMSG INCLCODE 
  Increment Unit Counter. - 
      HELP M$CHGUNIT 
  INDENT -   
    VLP_HDR - 
      HELP VLP_HDR INDENT 
  INERR -   
    VLR_ERRMSG - 
      HELP VLR_ERRMSG INERR 
  Initialization Parameters - 
      HELP NOTATION 
  Initializing Automatic Storage - 
      HELP Initializing 
  Initiate Recovery - 
      HELP M$SCREECH 
  INPUT -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR INPUT 
  INSERTMODE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL INSERTMODE 
  INST -   
    G$TSA - 
      HELP G$TSA INST 
    G$TSA_HDR - 
      HELP G$TSA_HDR INST 
  INT$ -   
    G$ECCB - 
      HELP G$ECCB INT$ 
    M$INT - 
      HELP M$INT INT$ 
  INTCON -   
    VLP_PRIV - 
      HELP VLP_PRIV INTCON 
  INT_MBE -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS INT_MBE 
  INT_REG_OV -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS INT_REG_OV 
  INT_UR -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS INT_UR 
  Invoking FEP Handlers - 
      HELP INVOKING_HOST_AND_FEP_PROGS 
  Invoking FPRGs - 
      HELP INVOKING_HOST_AND_FEP_PROGS 
  Invoking the Host and FEP Programs - 
      HELP INVOKING_HOST_AND_FEP_PROGS 
  IO -   
    G$INDICATOR_REG - 
      HELP G$INDICATOR_REG IO 
    VLP_HMI - 
      HELP VLP_HMI IO 
  IOBUF -   
    M$GDS - 
      HELP M$GDS IOBUF 
  ISA -   
    G$TSA - 
      HELP G$TSA ISA 
  ISA_USR -   
    G$UHJIT - 
      HELP G$UHJIT ISA_USR 
  ISM1 -   
    G$ISA - 
      HELP G$ISA ISM1 
    G$ISA_MINI - 
      HELP G$ISA_MINI ISM1 
  ISM2 -   
    G$ISA - 
      HELP G$ISA ISM2 
    G$ISA_MINI - 
      HELP G$ISA_MINI ISM2 
  ISR1 - ISR7 Segments - 
      HELP SAMPLE_FEP_PROGRAMS 
J 
  J -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS J 
  JIT - 
      HELP G$JIT 
      HELP SAMPLE_FEP_PROGRAMS 
  JIT$ -   
    G$ROS - 
      HELP G$ROS JIT$ 
  JMCLS -   
    G$JIT - 
      HELP G$JIT JMCLS 
  Job Information Table (JIT) - 
      HELP G$JIT 
      HELP SAMPLE_FEP_PROGRAMS 
  JOBUNIT -   
    G$JIT - 
      HELP G$JIT JOBUNIT 
  JPEAK_LVLS -   
    G$JIT - 
      HELP G$JIT JPEAK_LVLS 
  JPEAK_MEM -   
    G$JIT - 
      HELP G$JIT JPEAK_MEM 
  JPEAK_SUDO -   
    G$JIT - 
      HELP G$JIT JPEAK_SUDO 
  JPROC_EXTIME -   
    G$JIT - 
      HELP G$JIT JPROC_EXTIME 
  JPROC_MEMTIME -   
    G$JIT - 
      HELP G$JIT JPROC_MEMTIME 
  JPROC_SVTIME -   
    G$JIT - 
      HELP G$JIT JPROC_SVTIME 
  JREADS_HOST -   
    G$JIT - 
      HELP G$JIT JREADS_HOST 
  JREADS_UC -   
    G$JIT - 
      HELP G$JIT JREADS_UC 
  JSTART -   
    G$JIT - 
      HELP G$JIT JSTART 
  JUNK -   
    G$JIT - 
      HELP G$JIT JUNK 
  JUNK.ALIBFD -   
    G$JIT - 
      HELP G$JIT JUNK.ALIBFD 
  JUNK.BACKP$ -   
    G$JIT - 
      HELP G$JIT JUNK.BACKP$ 
  JUNK.DB_TIMER -   
    G$JIT - 
      HELP G$JIT JUNK.DB_TIMER 
  JUNK.EXONLY -   
    G$JIT - 
      HELP G$JIT JUNK.EXONLY 
  JUNK.HOST_STEP_ABRT -   
    G$JIT - 
      HELP G$JIT JUNK.HOST_STEP_ABRT 
  JUNK.KEEP -   
    G$JIT - 
      HELP G$JIT JUNK.KEEP 
  JUNK.MLDTRC -   
    G$JIT - 
      HELP G$JIT JUNK.MLDTRC 
  JUNK.PROCACCT -   
    G$JIT - 
      HELP G$JIT JUNK.PROCACCT 
  JUNK.PROCSURCHG -   
    G$JIT - 
      HELP G$JIT JUNK.PROCSURCHG 
  JUNK.RTNFID -   
    G$JIT - 
      HELP G$JIT JUNK.RTNFID 
  JUNK.SCCSET -   
    G$JIT - 
      HELP G$JIT JUNK.SCCSET 
  JUNK.STEP -   
    G$JIT - 
      HELP G$JIT JUNK.STEP 
  JUNK.STEPACCT -   
    G$JIT - 
      HELP G$JIT JUNK.STEPACCT 
  JUNK2 -   
    G$JIT - 
      HELP G$JIT JUNK2 
  JUNK2.BYPASS_MFPL -   
    G$JIT - 
      HELP G$JIT JUNK2.BYPASS_MFPL 
  JUNK2.MICROFPL -   
    G$JIT - 
      HELP G$JIT JUNK2.MICROFPL 
  JUSER_EXTIME -   
    G$JIT - 
      HELP G$JIT JUSER_EXTIME 
  JUSER_MEMTIME -   
    G$JIT - 
      HELP G$JIT JUSER_MEMTIME 
  JUSER_SVTIME -   
    G$JIT - 
      HELP G$JIT JUSER_SVTIME 
  JWRITES_HOST -   
    G$JIT - 
      HELP G$JIT JWRITES_HOST 
  JWRITES_UC -   
    G$JIT - 
      HELP G$JIT JWRITES_UC 
K 
  KEEPTYPAHD -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL KEEPTYPAHD 
  KEY -   
    M$ERASE - 
      HELP M$ERASE KEY 
    M$MDFFLD - 
      HELP M$MDFFLD KEY 
    M$READ - 
      HELP M$READ KEY 
    M$RLSFLD - 
      HELP M$RLSFLD KEY 
    M$SLCFLD - 
      HELP M$SLCFLD KEY 
    M$WRITE - 
      HELP M$WRITE KEY 
  KEYR -   
    M$READ - 
      HELP M$READ KEYR 
  KEYS -   
    M$READ - 
      HELP M$READ KEYS 
  KEYTYPE -   
    M$DCB - 
      HELP M$DCB KEYTYPE 
    M$ERASE - 
      HELP M$ERASE KEYTYPE 
    M$MDFFLD - 
      HELP M$MDFFLD KEYTYPE 
    M$OPEN - 
      HELP M$OPEN KEYTYPE 
    M$READ - 
      HELP M$READ KEYTYPE 
    M$RLSFLD - 
      HELP M$RLSFLD KEYTYPE 
    M$SLCFLD - 
      HELP M$SLCFLD KEYTYPE 
    M$WRITE - 
      HELP M$WRITE KEYTYPE 
L 
  L -   
    G$INDICATOR_REG - 
      HELP G$INDICATOR_REG L 
    VLP_TEXTC - 
      HELP VLP_TEXTC L 
  LANG -   
    G$JIT - 
      HELP G$JIT LANG 
    M$ERRMSG - 
      HELP M$ERRMSG LANG 
  LDCTX -   
    M$DCB - 
      HELP M$DCB LDCTX 
  LEN -   
    VLP_TEXTC - 
      HELP VLP_TEXTC LEN 
  LENGTH -   
    VLP_PLATEN - 
      HELP VLP_PLATEN LENGTH 
    VLP_WINDOW - 
      HELP VLP_WINDOW LENGTH 
  LEV -   
    B$TERMINAL_ID - 
      HELP B$TERMINAL_ID LEV 
  LEVEL -   
    G$STATUS_REG - 
      HELP G$STATUS_REG LEVEL 
    M$CLOCK - 
      HELP M$CLOCK LEVEL 
    M$INTCON - 
      HELP M$INTCON LEVEL 
    M$INTREL - 
      HELP M$INTREL LEVEL 
  LFISNL -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR LFISNL 
  LFTBRDR -   
    VLP_WINDOW - 
      HELP VLP_WINDOW LFTBRDR 
  LIMBO -   
    VLP_PLATEN - 
      HELP VLP_PLATEN LIMBO 
  LIMBOCLM -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR LIMBOCLM 
  LIN -   
    M$DCLFLD - 
      HELP M$DCLFLD LIN 
  LINEATTR -   
    M$GLINEATTR - 
      HELP M$GLINEATTR LINEATTR 
  LINES -   
    M$DCB - 
      HELP M$DCB LINES 
    M$DEVICE - 
      HELP M$DEVICE LINES 
    M$OPEN - 
      HELP M$OPEN LINES 
  LINESPEED -   
    VLP_LINEATTR - 
      HELP VLP_LINEATTR LINESPEED 
  LLL -   
    G$JIT - 
      HELP G$JIT LLL 
  Load and Transfer to Program - 
      HELP M$LDTRC 
  LOCALECHO -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR LOCALECHO 
  LOGON -   
    M$OPEN - 
      HELP M$OPEN LOGON 
  LOWCHAN -   
    VLR_GCHAN - 
      HELP VLR_GCHAN LOWCHAN 
  LOWERCASE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL LOWERCASE 
  LOWERCASEPRINTS -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR LOWERCASEPRINTS 
  LPI -   
    VLP_PLATEN - 
      HELP VLP_PLATEN LPI 
  LUL -   
    G$JIT - 
      HELP G$JIT LUL 
M 
  M$CHGUNIT - Increment Unit Counter - 
      HELP M$CHGUNIT 
  M$CLOCK - Request Clock Service - 
      HELP M$CLOCK 
  M$CLOSE - Close DCB - 
      HELP M$CLOSE 
  M$CLRSTK - Clear the TCB Stack Frame - 
      HELP M$CLRSTK 
  M$CVM - Change Virtual Map - 
      HELP M$CVM 
  M$DCB - Data Control Block - 
      HELP M$DCB 
  M$DCLFLD - Declare a Field - 
      HELP M$DCLFLD 
  M$DEVICE - Change Device Attributes - 
      HELP M$DEVICE 
  M$EOM - Set EOM Characters/Timeout - 
      HELP M$EOM 
  M$ERASE - Erase Fields or Records - 
      HELP M$ERASE 
  M$ERR - Error Program - 
      HELP M$ERR 
  M$ERRMSG - Return Text for Error Code - 
      HELP M$ERRMSG 
  M$EVENT - Set Event Control - 
      HELP M$EVENT 
  M$EXIT - Exit Program - 
      HELP M$EXIT 
  M$FAUTO - Free / Diminish Auto Segment - 
      HELP M$FAUTO 
  M$FDS - Free / Diminish Data Segment - 
      HELP M$FDS 
  M$GAUTO - Get / Enlarge Auto Segment - 
      HELP M$GAUTO 
  M$GCHAN - Get a Channel - 
      HELP M$GCHAN 
  M$GDDL - Get Dynamic Data Limits - 
      HELP M$GDDL 
  M$GDS - Get / Enlarge Data Segment - 
      HELP M$GDS 
  M$GETDCB - Build Data Control Block - 
      HELP M$GETDCB 
  M$GLINEATTR - Get Line Attributes - 
      HELP M$GLINEATTR 
  M$GPLATEN - Set and Get Page Format - 
      HELP M$PLATEN 
  M$GPROMPT - Prompt Control - 
      HELP M$PROMPT 
  M$GTRMATTR - Attributes - 
      HELP M$STRMATTR 
  M$GTRMCTL and M$STRMCTL - Terminal Control/Attribute Manipulation - 
      HELP M$GTRMCTL 
  M$GTRMTAB and M$STRMTAB - Tab Settings - 
      HELP M$GTRMTAB 
  M$INT - Set Break Control - 
      HELP M$INT 
  M$INTCON - Connect to Interrupt - 
      HELP M$INTCON 
  M$INTREL - Release Interrupt Control - 
      HELP M$INTREL 
  M$INTRET - Return from Interrupt - 
      HELP M$INTRET 
  M$LDTRC - Load and Transfer to Program - 
      HELP M$LDTRC 
  M$MDFFLD - Modify a Field - 
      HELP M$MDFFLD 
  M$MERC - Monitor Error Control - 
      HELP M$MERC 
  M$OPEN - Open DCB - 
      HELP M$OPEN 
  M$PDS - Protect Data Segments - 
      HELP M$PDS 
  M$PLATEN and M$GPLATEN - Set and Get Page Format - 
      HELP M$PLATEN 
  M$PROMPT and M$GPROMPT - Prompt Control - 
      HELP M$PROMPT 
  M$RCHAN - Release a Channel - 
      HELP M$RCHAN 
  M$READ - Read Data - 
      HELP M$READ 
  M$RELDCB - Release Data Control Block - 
      HELP M$RELDCB 
  M$RENV - Save/Restore ALTRET Environment - 
      HELP M$SENV 
  M$RETRY - Retry Monitor Service - 
      HELP M$RETRY 
  M$RLSFLD - Release a Field - 
      HELP M$RLSFLD 
  M$SCREECH - Initiate Recovery - 
      HELP M$SCREECH 
  M$SENV and M$RENV - Save/Restore ALTRET Environment - 
      HELP M$SENV 
  M$SINPUT - Set to Last Input - 
      HELP M$SINPUT 
  M$SLCFLD - Select a Field for Modification - 
      HELP M$SLCFLD 
  M$SPRIV - Control Of System Privileges - 
      HELP M$SPRIV 
  M$STRMATTR and M$GTRMATTR - Attributes - 
      HELP M$STRMATTR 
  M$STRMCTL - 
      HELP M$GTRMCTL 
  M$STRMCTL - Terminal Control - 
      HELP M$GTRMCTL 
  M$STRMTAB - 
      HELP M$GTRMTAB 
  M$STRMTAB - Tab Settings - 
      HELP M$GTRMTAB 
  M$SYS - Enter Privileged Mode - 
      HELP M$SYS 
  M$TIME - Return Time and Date - 
      HELP M$TIME 
  M$TRAP - Set Trap Control - 
      HELP M$TRAP 
  M$TRMPRG - Purge Terminal Buffers - 
      HELP M$TRMPRG 
  M$TRTN - TCB Return - 
      HELP M$TRTN 
  M$UNSHARE - Unshare Library or Program - 
      HELP M$UNSHARE 
  M$WAIT - Suspend Program - 
      HELP M$WAIT 
  M$WRITE - Write Data - 
      HELP M$WRITE 
  M$WRSYSLOG - Write to System Log - 
      HELP M$WRSYSLOG 
  M$WRTMLT - Write Multiple - 
      HELP M$WRTMLT 
  M$XCON - Set Exit Control - 
      HELP M$XCON 
  M$XXX - Abort Program - 
      HELP M$XXX 
  M1 -   
    G$ISM1 - 
      HELP G$ISM1 M1 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS M1 
  M1.J -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS M1.J 
  M1.Rn_OV -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS M1.Rn_OV 
  M2_M7 -   
    G$ISM2 - 
      HELP G$ISM2 M2_M7 
  M3 -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS M3 
  M3.CIP_OV -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS M3.CIP_OV 
  M3.CIP_TR -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS M3.CIP_TR 
  MARGIN -   
    VLP_TAB - 
      HELP VLP_TAB MARGIN 
  MAXATRS -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR MAXATRS 
  MAXLVLS -   
    G$JIT - 
      HELP G$JIT MAXLVLS 
  MAXMEM -   
    G$JIT - 
      HELP G$JIT MAXMEM 
    VLP_PRIV - 
      HELP VLP_PRIV MAXMEM 
  MAXSUDO -   
    G$JIT - 
      HELP G$JIT MAXSUDO 
  MAX_ALLOWED -   
    G$AUTO_HEAD - 
      HELP G$AUTO_HEAD MAX_ALLOWED 
  MCL -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS MCL 
  MCLS -   
    G$JIT - 
      HELP G$JIT MCLS 
  Memory Management Unit (MMU) - 
      HELP SAMPLE_FEP_PROGRAMS 
  MEM_PROT -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS MEM_PROT 
  MHJIT Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  MICROFPL -   
    VLP_LINEATTR - 
      HELP VLP_LINEATTR MICROFPL 
    VLP_TRMATTR - 
      HELP VLP_TRMATTR MICROFPL 
  MID -   
    VLP_ERRCODE - 
      HELP VLP_ERRCODE MID 
    VLP_SCODE - 
      HELP VLP_SCODE MID 
  MINLENGTH -   
    VLP_WINDOW - 
      HELP VLP_WINDOW MINLENGTH 
  MINREC -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR MINREC 
  MINWIDTH -   
    VLP_WINDOW - 
      HELP VLP_WINDOW MINWIDTH 
  MMFLGS -   
    G$JIT - 
      HELP G$JIT MMFLGS 
  MMFLGS.FREE_PPGS -   
    G$JIT - 
      HELP G$JIT MMFLGS.FREE_PPGS 
  MMU -   
    G$ISM2 - 
      HELP G$ISM2 MMU 
  MMU - 
      HELP SAMPLE_FEP_PROGRAMS 
  MODE -   
    G$JIT - 
      HELP G$JIT MODE 
    M$CLOCK - 
      HELP M$CLOCK MODE 
    M$WAIT - 
      HELP M$WAIT MODE 
  Modify a Field. - 
      HELP M$MDFFLD 
  MON -   
    VLP_ERRCODE - 
      HELP VLP_ERRCODE MON 
    VLP_SCODE - 
      HELP VLP_SCODE MON 
  Monitor Calling Sequences - 
      HELP MONITOR_CALLING_SEQUENCES 
  Monitor Error Control - 
      HELP M$MERC 
  MONITOR_AUTO_LAYOUT - 
      HELP AUTOMATIC_STORAGE_LAYOUT 
  MON_ENTRY Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  MON_ENTRY_DATA Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  MRT -   
    G$JIT - 
      HELP G$JIT MRT 
  MSGCOMP -   
    VLR_ERRMSG - 
      HELP VLR_ERRMSG MSGCOMP 
  MSGHALT -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL MSGHALT 
  MSGID -   
    VLP_CG - 
      HELP VLP_CG MSGID 
  MSGLINE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL MSGLINE 
  MSGTYP -   
    VLP_CG - 
      HELP VLP_CG MSGTYP 
  MSTENT -   
    VLP_FLDATR - 
      HELP VLP_FLDATR MSTENT 
  MSYS -   
    VLP_PRIV - 
      HELP VLP_PRIV MSYS 
  MULTIDEVICE -   
    VLP_LINEATTR - 
      HELP VLP_LINEATTR MULTIDEVICE 
  MUST_BE_NIL -   
    G$AUTO_HEAD - 
      HELP G$AUTO_HEAD MUST_BE_NIL 
  MW -   
    G$STACK_HDR - 
      HELP G$STACK_HDR MW 
  MY_LANG -   
    M$ERRMSG - 
      HELP M$ERRMSG MY_LANG 
N 
  NAME -   
    M$LDTRC - 
      HELP M$LDTRC NAME 
  NATSAP_SEL -   
    G$ISM2 - 
      HELP G$ISM2 NATSAP_SEL 
  NEVENT -   
    M$EVENT - 
      HELP M$EVENT NEVENT 
  NEXT -   
    M$CVM - 
      HELP M$CVM NEXT 
    M$GDS - 
      HELP M$GDS NEXT 
  NEXT$ -   
    G$ROS_AVAIL_HDR - 
      HELP G$ROS_AVAIL_HDR NEXT$ 
  NEXT_BIG -   
    VLR_GDDL - 
      HELP VLR_GDDL NEXT_BIG 
  NEXT_LITTLE -   
    VLR_GDDL - 
      HELP VLR_GDDL NEXT_LITTLE 
  NINT -   
    M$INT - 
      HELP M$INT NINT 
  NNATIVE -   
    VLR_ERRMSG - 
      HELP VLR_ERRMSG NNATIVE 
  No-Wait IO Event Frame - 
      HELP G$NWIO 
  NODAT -   
    M$READ - 
      HELP M$READ NODAT 
    M$WRITE - 
      HELP M$WRITE NODAT 
  NODE -   
    VLP_LINEATTR - 
      HELP VLP_LINEATTR NODE 
  NOFILE -   
    VLR_ERRMSG - 
      HELP VLR_ERRMSG NOFILE 
  NOMSG -   
    VLR_ERRMSG - 
      HELP VLR_ERRMSG NOMSG 
  NOOPTMIZ -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL NOOPTMIZ 
  NO_FLDTRM -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR NO_FLDTRM 
  NO_MICROFPL -   
    M$LDTRC - 
      HELP M$LDTRC NO_MICROFPL 
  NO_SIP -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS NO_SIP 
  NSPC -   
    G$JIT - 
      HELP G$JIT NSPC 
  NTC -   
    M$TRAP - 
      HELP M$TRAP NTC 
  NULL Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  NUMDCBS -   
    G$ROS - 
      HELP G$ROS NUMDCBS 
  NUM_BIG -   
    VLR_GDDL - 
      HELP VLR_GDDL NUM_BIG 
  NUM_LITTLE -   
    VLR_GDDL - 
      HELP VLR_GDDL NUM_LITTLE 
  NWORDS -   
    G$ROS_AVAIL_HDR - 
      HELP G$ROS_AVAIL_HDR NWORDS 
  NXCON -   
    M$XCON - 
      HELP M$XCON NXCON 
O 
  OPDTAB -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR OPDTAB 
  Open DCB - 
      HELP M$OPEN 
  OPTION - 
      HELP NOTATION 
  ORG -   
    M$DCB - 
      HELP M$DCB ORG 
    M$OPEN - 
      HELP M$OPEN ORG 
  ORG_PST -   
    VLP_WINDOW - 
      HELP VLP_WINDOW ORG_PST 
  Other PL-6 Library Routines - 
      HELP OTHER_PL_6_LIBRARY_ROUTINES 
  OUTPUT -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR OUTPUT 
  OUTPUTDISCARD -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL OUTPUTDISCARD 
  OV -   
    G$INDICATOR_REG - 
      HELP G$INDICATOR_REG OV 
P 
  P# -   
    G$NWIO - 
      HELP G$NWIO P# 
  P$$ -   
    G$EXCFR - 
      HELP G$EXCFR P$$ 
    G$ISA - 
      HELP G$ISA P$$ 
    G$ISA_MINI - 
      HELP G$ISA_MINI P$$ 
    G$TSA - 
      HELP G$TSA P$$ 
    G$TSA_HDR - 
      HELP G$TSA_HDR P$$ 
    M$TRTN - 
      HELP M$TRTN P$$ 
  PAGE -   
    M$DEVICE - 
      HELP M$DEVICE PAGE 
  PAGEHALT -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL PAGEHALT 
  PAGES -   
    M$CVM - 
      HELP M$CVM PAGES 
    M$FAUTO - 
      HELP M$FAUTO PAGES 
    M$FDS - 
      HELP M$FDS PAGES 
    M$GAUTO - 
      HELP M$GAUTO PAGES 
    M$GDS - 
      HELP M$GDS PAGES 
    VLP_SEGMENT - 
      HELP VLP_SEGMENT PAGES 
  Parameter Conventions - 
      HELP FIELD_CONVENTIONS 
  PARAMS -   
    G$FRAME - 
      HELP G$FRAME PARAMS 
  PARITY -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR PARITY 
  PARITYCHECK -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL PARITYCHECK 
  PARKCURSOR -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL PARKCURSOR 
  PASS -   
    M$LDTRC - 
      HELP M$LDTRC PASS 
  PCC -   
    G$JIT - 
      HELP G$JIT PCC 
  PCD -   
    G$JIT - 
      HELP G$JIT PCD 
  PCDDS -   
    G$JIT - 
      HELP G$JIT PCDDS 
  PCDS -   
    G$JIT - 
      HELP G$JIT PCDS 
  PCL -   
    G$JIT - 
      HELP G$JIT PCL 
  PCP -   
    G$JIT - 
      HELP G$JIT PCP 
  PCROS -   
    G$JIT - 
      HELP G$JIT PCROS 
  PEAK_LVLS -   
    G$JIT - 
      HELP G$JIT PEAK_LVLS 
  PEAK_MEM -   
    G$JIT - 
      HELP G$JIT PEAK_MEM 
  PEAK_SUDO -   
    G$JIT - 
      HELP G$JIT PEAK_SUDO 
  PERM -   
    M$CLOCK - 
      HELP M$CLOCK PERM 
  PEVENT -   
    M$EVENT - 
      HELP M$EVENT PEVENT 
  PIA -   
    G$ROS - 
      HELP G$ROS PIA 
  PIA$ -   
    G$ROS - 
      HELP G$ROS PIA$ 
  PINT -   
    M$INT - 
      HELP M$INT PINT 
  PLATEN -   
    M$PLATEN - 
      HELP M$PLATEN PLATEN 
  PLL -   
    G$JIT - 
      HELP G$JIT PLL 
  PORT -   
    VLP_LINEATTR - 
      HELP VLP_LINEATTR PORT 
  POSITION -   
    M$SINPUT - 
      HELP M$SINPUT POSITION 
    VLP_WINDOW - 
      HELP VLP_WINDOW POSITION 
  PPCHK -   
    M$SPRIV - 
      HELP M$SPRIV PPCHK 
  PPRIV -   
    M$SPRIV - 
      HELP M$SPRIV PPRIV 
  PRC -   
    M$SPRIV - 
      HELP M$SPRIV PRC 
  PREVSZ -   
    G$EXCFR - 
      HELP G$EXCFR PREVSZ 
  PREV_FR_SIZ -   
    G$FRAME - 
      HELP G$FRAME PREV_FR_SIZ 
  PRINTHALT -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL PRINTHALT 
  PRINTTYPE -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR PRINTTYPE 
  PRIV -   
    G$JIT - 
      HELP G$JIT PRIV 
    M$SPRIV - 
      HELP M$SPRIV PRIV 
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS PRIV 
  PRIV.ACTIVE -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE 
  PRIV.ACTIVE.CQ -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.CQ 
  PRIV.ACTIVE.EXMM -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.EXMM 
  PRIV.ACTIVE.EXPM -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.EXPM 
  PRIV.ACTIVE.GPP -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.GPP 
  PRIV.ACTIVE.INTCON -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.INTCON 
  PRIV.ACTIVE.MAXMEM -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.MAXMEM 
  PRIV.ACTIVE.MSYS -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.MSYS 
  PRIV.ACTIVE.SCREECH -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.SCREECH 
  PRIV.ACTIVE.SPCLMM -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.SPCLMM 
  PRIV.ACTIVE.SYSLOG -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.SYSLOG 
  PRIV.ACTIVE.TND -   
    G$JIT - 
      HELP G$JIT PRIV.ACTIVE.TND 
  PRIV.AUTH -   
    G$JIT - 
      HELP G$JIT PRIV.AUTH 
  PRIV.PRC -   
    G$JIT - 
      HELP G$JIT PRIV.PRC 
  PRIVILEGED -   
    M$INTCON - 
      HELP M$INTCON PRIVILEGED 
  Procedure Entry Routines - 
      HELP RECEIVING_SEQUENCES 
  Procedure Return Routines - 
      HELP RETURN_SEQUENCES 
  processor -   
    VLP_PPRIV - 
      HELP VLP_PPRIV processor 
  PROCNAME -   
    G$JIT - 
      HELP G$JIT PROCNAME 
  PROFILE -   
    G$JIT - 
      HELP G$JIT PROFILE 
    VLP_LINEATTR - 
      HELP VLP_LINEATTR PROFILE 
  PROFILE.CNT -   
    G$JIT - 
      HELP G$JIT PROFILE.CNT 
  PROFILE.TXT -   
    G$JIT - 
      HELP G$JIT PROFILE.TXT 
  PROG -   
    M$UNSHARE - 
      HELP M$UNSHARE PROG 
  PROGDTAB -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR PROGDTAB 
  PROG_ENTRY -   
    G$JIT - 
      HELP G$JIT PROG_ENTRY 
  PROG_ERR -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS PROG_ERR 
  PROMPT -   
    M$PROMPT - 
      HELP M$PROMPT PROMPT 
  Protect Data Segments - 
      HELP M$PDS 
  PROTXTC -   
    VLP_LINEATTR - 
      HELP VLP_LINEATTR PROTXTC 
  PRT -   
    M$ERASE - 
      HELP M$ERASE PRT 
    VLP_FLDATR - 
      HELP VLP_FLDATR PRT 
  PRTGRD -   
    VLP_FLDATR - 
      HELP VLP_FLDATR PRTGRD 
  PSEUDOPGS -   
    G$JIT - 
      HELP G$JIT PSEUDOPGS 
  PSN -   
    M$LDTRC - 
      HELP M$LDTRC PSN 
  PTC -   
    M$TRAP - 
      HELP M$TRAP PTC 
  PTR - 
      HELP NOTATION 
  PUL -   
    G$JIT - 
      HELP G$JIT PUL 
  Purge Terminal Buffers - 
      HELP M$TRMPRG 
  PURGEINPUT -   
    M$TRMPRG - 
      HELP M$TRMPRG PURGEINPUT 
  PURGEOUTPUT -   
    M$TRMPRG - 
      HELP M$TRMPRG PURGEOUTPUT 
  PXCON -   
    M$XCON - 
      HELP M$XCON PXCON 
Q 
  QLT -   
    G$STATUS_REG - 
      HELP G$STATUS_REG QLT 
R 
  R3 -   
    G$TSA - 
      HELP G$TSA R3 
    G$TSA_HDR - 
      HELP G$TSA_HDR R3 
    M$RETRY - 
      HELP M$RETRY R3 
  RCQSIZE -   
    VLP_HMI - 
      HELP VLP_HMI RCQSIZE 
  RDBR$ -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS RDBR$ 
  READ -   
    M$PDS - 
      HELP M$PDS READ 
  Read Data - 
      HELP M$READ 
  Read Only Segment (ROS) - 
      HELP SAMPLE_FEP_PROGRAMS 
  READMLT -   
    M$READ - 
      HELP M$READ READMLT 
  READS_HOST -   
    G$JIT - 
      HELP G$JIT READS_HOST 
  READS_UC -   
    G$JIT - 
      HELP G$JIT READS_UC 
  Receiving Sequences - 
      HELP RECEIVING_SEQUENCES 
  RECL -   
    M$DCB - 
      HELP M$DCB RECL 
    M$OPEN - 
      HELP M$OPEN RECL 
  Register Conventions - 
      HELP REGISTER_CONVENTIONS 
  Registers Used - 
      HELP REGISTERS_USED 
  REGS -   
    G$EXCFR - 
      HELP G$EXCFR REGS 
    G$ISA - 
      HELP G$ISA REGS 
    M$TRTN - 
      HELP M$TRTN REGS 
  REGS.Bn$ -   
    G$EXCFR - 
      HELP G$EXCFR REGS.Bn$ 
    G$ISA - 
      HELP G$ISA REGS.Bn$ 
  REGS.CI -   
    G$EXCFR - 
      HELP G$EXCFR REGS.CI 
    G$ISA - 
      HELP G$ISA REGS.CI 
  REGS.CI.G -   
    G$EXCFR - 
      HELP G$EXCFR REGS.CI.G 
    G$ISA - 
      HELP G$ISA REGS.CI.G 
  REGS.CI.L -   
    G$EXCFR - 
      HELP G$EXCFR REGS.CI.L 
    G$ISA - 
      HELP G$ISA REGS.CI.L 
  REGS.CI.OV -   
    G$EXCFR - 
      HELP G$EXCFR REGS.CI.OV 
    G$ISA - 
      HELP G$ISA REGS.CI.OV 
  REGS.CI.QLT -   
    G$EXCFR - 
      HELP G$EXCFR REGS.CI.QLT 
    G$ISA - 
      HELP G$ISA REGS.CI.QLT 
  REGS.CI.SF -   
    G$EXCFR - 
      HELP G$EXCFR REGS.CI.SF 
    G$ISA - 
      HELP G$ISA REGS.CI.SF 
  REGS.CI.TR -   
    G$EXCFR - 
      HELP G$EXCFR REGS.CI.TR 
    G$ISA - 
      HELP G$ISA REGS.CI.TR 
  REGS.I -   
    G$EXCFR - 
      HELP G$EXCFR REGS.I 
    G$ISA - 
      HELP G$ISA REGS.I 
  REGS.I.B -   
    G$EXCFR - 
      HELP G$EXCFR REGS.I.B 
    G$ISA - 
      HELP G$ISA REGS.I.B 
  REGS.I.C -   
    G$EXCFR - 
      HELP G$EXCFR REGS.I.C 
    G$ISA - 
      HELP G$ISA REGS.I.C 
  REGS.I.G -   
    G$EXCFR - 
      HELP G$EXCFR REGS.I.G 
    G$ISA - 
      HELP G$ISA REGS.I.G 
  REGS.I.IO -   
    G$EXCFR - 
      HELP G$EXCFR REGS.I.IO 
    G$ISA - 
      HELP G$ISA REGS.I.IO 
  REGS.I.L -   
    G$EXCFR - 
      HELP G$EXCFR REGS.I.L 
    G$ISA - 
      HELP G$ISA REGS.I.L 
  REGS.I.OV -   
    G$EXCFR - 
      HELP G$EXCFR REGS.I.OV 
    G$ISA - 
      HELP G$ISA REGS.I.OV 
  REGS.I.TRAP# -   
    G$EXCFR - 
      HELP G$EXCFR REGS.I.TRAP# 
    G$ISA - 
      HELP G$ISA REGS.I.TRAP# 
  REGS.I.U -   
    G$EXCFR - 
      HELP G$EXCFR REGS.I.U 
    G$ISA - 
      HELP G$ISA REGS.I.U 
  REGS.M1 -   
    G$EXCFR - 
      HELP G$EXCFR REGS.M1 
    G$ISA - 
      HELP G$ISA REGS.M1 
  REGS.M1.J -   
    G$EXCFR - 
      HELP G$EXCFR REGS.M1.J 
    G$ISA - 
      HELP G$ISA REGS.M1.J 
  REGS.M1.Rn_OV -   
    G$EXCFR - 
      HELP G$EXCFR REGS.M1.Rn_OV 
    G$ISA - 
      HELP G$ISA REGS.M1.Rn_OV 
  REGS.M3 -   
    G$EXCFR - 
      HELP G$EXCFR REGS.M3 
    G$ISA - 
      HELP G$ISA REGS.M3 
  REGS.M3.CIP_OV -   
    G$EXCFR - 
      HELP G$EXCFR REGS.M3.CIP_OV 
    G$ISA - 
      HELP G$ISA REGS.M3.CIP_OV 
  REGS.M3.CIP_TR -   
    G$EXCFR - 
      HELP G$EXCFR REGS.M3.CIP_TR 
    G$ISA - 
      HELP G$ISA REGS.M3.CIP_TR 
  REGS.RDBR$ -   
    G$EXCFR - 
      HELP G$EXCFR REGS.RDBR$ 
    G$ISA - 
      HELP G$ISA REGS.RDBR$ 
  REGS.Rn -   
    G$EXCFR - 
      HELP G$EXCFR REGS.Rn 
    G$ISA - 
      HELP G$ISA REGS.Rn 
  REGS.T$ -   
    G$EXCFR - 
      HELP G$EXCFR REGS.T$ 
    G$ISA - 
      HELP G$ISA REGS.T$ 
  Release a Channel. - 
      HELP M$RCHAN 
  Release a Field. - 
      HELP M$RLSFLD 
  Release Data Control Block - 
      HELP M$RELDCB 
  Release Interrupt Control. - 
      HELP M$INTREL 
  RELPAGE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL RELPAGE 
  REMAINING -   
    VLR_GDDL - 
      HELP VLR_GDDL REMAINING 
  REMOTE_DESC -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS REMOTE_DESC 
  REMOVABLE -   
    VLP_WINDOW - 
      HELP VLP_WINDOW REMOVABLE 
  Request Clock Service - 
      HELP M$CLOCK 
  REREAD -   
    M$READ - 
      HELP M$READ REREAD 
  REREADPOS -   
    M$SINPUT - 
      HELP M$SINPUT REREADPOS 
  RES -   
    M$DCB - 
      HELP M$DCB RES 
    M$GCHAN - 
      HELP M$GCHAN RES 
    M$OPEN - 
      HELP M$OPEN RES 
  RESETBREAK -   
    M$TRMPRG - 
      HELP M$TRMPRG RESETBREAK 
  RESETPAGE -   
    VLP_HDR - 
      HELP VLP_HDR RESETPAGE 
  RESULTS -   
    M$ERRMSG - 
      HELP M$ERRMSG RESULTS 
    M$FAUTO - 
      HELP M$FAUTO RESULTS 
    M$FDS - 
      HELP M$FDS RESULTS 
    M$GAUTO - 
      HELP M$GAUTO RESULTS 
    M$GDDL - 
      HELP M$GDDL RESULTS 
    M$GDS - 
      HELP M$GDS RESULTS 
  Retry Monitor Service - 
      HELP M$RETRY 
  Return from Interrupt - 
      HELP M$INTRET 
  Return Sequences - 
      HELP RETURN_SEQUENCES 
  Return Text for Error Code - 
      HELP M$ERRMSG 
  Return Time and Date - 
      HELP M$TIME 
  RETYPOVR -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL RETYPOVR 
  RET_ADDR -   
    G$FRAME - 
      HELP G$FRAME RET_ADDR 
  RHTBRDR -   
    VLP_WINDOW - 
      HELP VLP_WINDOW RHTBRDR 
  RING -   
    G$STATUS_REG - 
      HELP G$STATUS_REG RING 
  RLCID.GENERATION -   
    M$DCB - 
      HELP M$DCB RLCID.GENERATION 
  RLCID.LDCTX -   
    M$DCB - 
      HELP M$DCB RLCID.LDCTX 
  RLCID.NODE -   
    M$DCB - 
      HELP M$DCB RLCID.NODE 
  Rn -   
    G$ISM1 - 
      HELP G$ISM1 Rn 
    VLP_REGISTERS - 
      HELP VLP_REGISTERS Rn 
  RNST -   
    G$JIT - 
      HELP G$JIT RNST 
  RNST.ABRT -   
    G$JIT - 
      HELP G$JIT RNST.ABRT 
  RNST.DSC -   
    G$JIT - 
      HELP G$JIT RNST.DSC 
  RNST.EKEY -   
    G$JIT - 
      HELP G$JIT RNST.EKEY 
  RNST.ERR -   
    G$JIT - 
      HELP G$JIT RNST.ERR 
  RNST.INTABRT -   
    G$JIT - 
      HELP G$JIT RNST.INTABRT 
  RNST.LDTRC -   
    G$JIT - 
      HELP G$JIT RNST.LDTRC 
  RNST.LIMX -   
    G$JIT - 
      HELP G$JIT RNST.LIMX 
  RNST.OFF -   
    G$JIT - 
      HELP G$JIT RNST.OFF 
  RNST.SSP -   
    G$JIT - 
      HELP G$JIT RNST.SSP 
  RNST.XKEY -   
    G$JIT - 
      HELP G$JIT RNST.XKEY 
  RNST.XXX -   
    G$JIT - 
      HELP G$JIT RNST.XXX 
  Rn_OV -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS Rn_OV 
  ROS - 
      HELP SAMPLE_FEP_PROGRAMS 
  Routines for Exit from ASYNC Procedures Specifying FPT - 
      HELP FPT_EXITS_FOR_ASYNC_PROCS 
  RP -   
    G$SEGDESC - 
      HELP G$SEGDESC RP 
  RRR -   
    M$DCLFLD - 
      HELP M$DCLFLD RRR 
    M$ERASE - 
      HELP M$ERASE RRR 
    M$MDFFLD - 
      HELP M$MDFFLD RRR 
    M$READ - 
      HELP M$READ RRR 
    M$RLSFLD - 
      HELP M$RLSFLD RRR 
    M$SLCFLD - 
      HELP M$SLCFLD RRR 
    M$WRITE - 
      HELP M$WRITE RRR 
  RUNFLAGS -   
    G$JIT - 
      HELP G$JIT RUNFLAGS 
  RUNLEVEL -   
    M$INTCON - 
      HELP M$INTCON RUNLEVEL 
  RVRVID -   
    VLP_FLDATR - 
      HELP VLP_FLDATR RVRVID 
S 
  S -   
    G$EXCFR - 
      HELP G$EXCFR S 
    G$ISA - 
      HELP G$ISA S 
    G$ISA_MINI - 
      HELP G$ISA_MINI S 
    G$TSA - 
      HELP G$TSA S 
  S.ID -   
    G$EXCFR - 
      HELP G$EXCFR S.ID 
    G$ISA - 
      HELP G$ISA S.ID 
    G$ISA_MINI - 
      HELP G$ISA_MINI S.ID 
    G$TSA - 
      HELP G$TSA S.ID 
  S.LEVEL -   
    G$EXCFR - 
      HELP G$EXCFR S.LEVEL 
    G$ISA - 
      HELP G$ISA S.LEVEL 
    G$ISA_MINI - 
      HELP G$ISA_MINI S.LEVEL 
    G$TSA - 
      HELP G$TSA S.LEVEL 
  S.QLT -   
    G$EXCFR - 
      HELP G$EXCFR S.QLT 
    G$ISA - 
      HELP G$ISA S.QLT 
    G$ISA_MINI - 
      HELP G$ISA_MINI S.QLT 
    G$TSA - 
      HELP G$TSA S.QLT 
  S.RING -   
    G$EXCFR - 
      HELP G$EXCFR S.RING 
    G$ISA - 
      HELP G$ISA S.RING 
    G$ISA_MINI - 
      HELP G$ISA_MINI S.RING 
    G$TSA - 
      HELP G$TSA S.RING 
  Sample Front End Processor Program (FPRG) - 
      HELP SAMPLE_FEP_PROGRAMS 
  Sample Host Program - 
      HELP SAMPLE_HOST_PROGRAM 
  Saving the User Environment - 
      HELP G$TCB 
  SCHTIME -   
    G$JIT - 
      HELP G$JIT SCHTIME 
  Scope of the Sample Programs - 
      HELP SAMPLE_PROGRAM_SCOPE 
  SCQSIZE -   
    VLP_HMI - 
      HELP VLP_HMI SCQSIZE 
  SCREECH -   
    VLP_PRIV - 
      HELP VLP_PRIV SCREECH 
  SCROLL -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL SCROLL 
  SEGMENT -   
    M$PDS - 
      HELP M$PDS SEGMENT 
  Select a Field for Modification - 
      HELP M$SLCFLD 
  SENDBKSPACE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL SENDBKSPACE 
  Service Codes - 
      HELP G$JIT_E 
  Set Break Control - 
      HELP M$INT 
  Set EOM Characters/Timeout - 
      HELP M$EOM 
  Set Event Control - 
      HELP M$EVENT 
  Set Exit Control - 
      HELP M$XCON 
  Set to Last Input. - 
      HELP M$SINPUT 
  Set Trap Control - 
      HELP M$TRAP 
  SETGRPRND -   
    M$MDFFLD - 
      HELP M$MDFFLD SETGRPRND 
  SETQLF -   
    M$MDFFLD - 
      HELP M$MDFFLD SETQLF 
  SEV -   
    VLP_ERRCODE - 
      HELP VLP_ERRCODE SEV 
    VLP_SCODE - 
      HELP VLP_SCODE SEV 
  SIMPERF -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL SIMPERF 
  SINPUTSZ -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL SINPUTSZ 
  SIZE -   
    G$SEGDESC - 
      HELP G$SEGDESC SIZE 
  SLIB -   
    M$UNSHARE - 
      HELP M$UNSHARE SLIB 
  SLIB# -   
    G$JIT - 
      HELP G$JIT SLIB# 
  SLWBLN -   
    VLP_FLDATR - 
      HELP VLP_FLDATR SLWBLN 
  SOURCE -   
    M$ERRMSG - 
      HELP M$ERRMSG SOURCE 
    M$TIME - 
      HELP M$TIME SOURCE 
  SPACEINSERT -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL SPACEINSERT 
  SPCBFRPRT -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR SPCBFRPRT 
  SPCLMM -   
    VLP_PRIV - 
      HELP VLP_PRIV SPCLMM 
  SPEED -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR SPEED 
  SPROC# -   
    G$JIT - 
      HELP G$JIT SPROC# 
  SSN$ -   
    M$DCB - 
      HELP M$DCB SSN$ 
  START -   
    G$JIT - 
      HELP G$JIT START 
  STATION -   
    VLP_CG - 
      HELP VLP_CG STATION 
  STEP -   
    G$JIT - 
      HELP G$JIT STEP 
    M$CHGUNIT - 
      HELP M$CHGUNIT STEP 
  STEPCC -   
    G$JIT - 
      HELP G$JIT STEPCC 
    M$ERR - 
      HELP M$ERR STEPCC 
    M$EXIT - 
      HELP M$EXIT STEPCC 
    M$XXX - 
      HELP M$XXX STEPCC 
  STEPUNIT -   
    G$JIT - 
      HELP G$JIT STEPUNIT 
  STIME -   
    G$JIT - 
      HELP G$JIT STIME 
  STK$ -   
    G$TCB - 
      HELP G$TCB STK$ 
  STK_OV -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS STK_OV 
  STK_UF -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS STK_UF 
  STOP -   
    G$JIT - 
      HELP G$JIT STOP 
  Storage - 
      HELP Initializing 
  Structure Defining a Terminal ID - 
      HELP B$TERMINAL_ID 
  SUBFILE -   
    M$ERRMSG - 
      HELP M$ERRMSG SUBFILE 
  SUBLANG -   
    M$ERRMSG - 
      HELP M$ERRMSG SUBLANG 
  SUBMESS -   
    M$ERRMSG - 
      HELP M$ERRMSG SUBMESS 
  SUPPHALT -   
    M$EOM - 
      HELP M$EOM SUPPHALT 
  Suspend Program - 
      HELP M$WAIT 
  SYSID -   
    G$JIT - 
      HELP G$JIT SYSID 
  SYSLOG -   
    VLP_PRIV - 
      HELP VLP_PRIV SYSLOG 
T 
  T -   
    G$ISM2 - 
      HELP G$ISM2 T 
  T$ -   
    VLP_REGISTERS - 
      HELP VLP_REGISTERS T$ 
  TAB -   
    M$DEVICE - 
      HELP M$DEVICE TAB 
    M$GTRMTAB - 
      HELP M$GTRMTAB TAB 
    M$OPEN - 
      HELP M$OPEN TAB 
  TABRELATIVE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL TABRELATIVE 
  TABS -   
    VLP_TAB - 
      HELP VLP_TAB TABS 
  TABSIM -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL TABSIM 
  Tabulation Parameter - 
      HELP VLP_TAB 
  Task Control Block (TCB) - 
      HELP SAMPLE_FEP_PROGRAMS 
  TCB - 
      HELP SAMPLE_FEP_PROGRAMS 
  TCB Return - 
      HELP M$TRTN 
  TCB.ALT$ -   
    G$ROS - 
      HELP G$ROS TCB.ALT$ 
  TCB.AVSZ -   
    G$ROS - 
      HELP G$ROS TCB.AVSZ 
  TCB.CURRSZ -   
    G$ROS - 
      HELP G$ROS TCB.CURRSZ 
  TCB.STK$ -   
    G$ROS - 
      HELP G$ROS TCB.STK$ 
  TERM.CHANNEL -   
    B$TERMINAL_ID - 
      HELP B$TERMINAL_ID TERM.CHANNEL 
  TERM.SUBDEVICE -   
    B$TERMINAL_ID - 
      HELP B$TERMINAL_ID TERM.SUBDEVICE 
  TERM.SUBSUBDEVICE -   
    B$TERMINAL_ID - 
      HELP B$TERMINAL_ID TERM.SUBSUBDEVICE 
  TERM.TERM_NAME -   
    B$TERMINAL_ID - 
      HELP B$TERMINAL_ID TERM.TERM_NAME 
  TERMID -   
    B$TERMINAL_ID - 
      HELP B$TERMINAL_ID TERMID 
  TERMINAL_ID -   
    M$WRSYSLOG - 
      HELP M$WRSYSLOG TERMINAL_ID 
  TEXT -   
    VLP_TEXTC - 
      HELP VLP_TEXTC TEXT 
  TIME -   
    M$TIME - 
      HELP M$TIME TIME 
  TIMEOUT -   
    M$EOM - 
      HELP M$EOM TIMEOUT 
  TIMERS -   
    G$JIT - 
      HELP G$JIT TIMERS 
  TITLE -   
    VLP_HDR - 
      HELP VLP_HDR TITLE 
  TND -   
    VLP_PRIV - 
      HELP VLP_PRIV TND 
  TOPBRDR -   
    VLP_WINDOW - 
      HELP VLP_WINDOW TOPBRDR 
  TRACE -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS TRACE 
  TRANS -   
    M$PROMPT - 
      HELP M$PROMPT TRANS 
    M$READ - 
      HELP M$READ TRANS 
    M$WRITE - 
      HELP M$WRITE TRANS 
  TRAP# -   
    G$INDICATOR_REG - 
      HELP G$INDICATOR_REG TRAP# 
  TRAP$ -   
    G$ECCB - 
      HELP G$ECCB TRAP$ 
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS TRAP$ 
  TRLR -   
    G$EXCFR - 
      HELP G$EXCFR TRLR 
  TRLR.BRKCNT -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.BRKCNT 
  TRLR.DEV -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.DEV 
  TRLR.DEV.CHN -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.DEV.CHN 
  TRLR.DEV.IL -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.DEV.IL 
  TRLR.ERR -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.ERR 
    G$NWIO - 
      HELP G$NWIO TRLR.ERR 
  TRLR.ERR.ERR# -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.ERR.ERR# 
  TRLR.ERR.FCG -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.ERR.FCG 
  TRLR.ERR.MID -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.ERR.MID 
  TRLR.ERR.MON -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.ERR.MON 
  TRLR.ERR.SEV -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.ERR.SEV 
  TRLR.EVID -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.EVID 
  TRLR.MCL_CODE -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.MCL_CODE 
  TRLR.MCL_CODE.CODE -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.MCL_CODE.CODE 
  TRLR.MCL_CODE.V# -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.MCL_CODE.V# 
  TRLR.P# -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.P# 
  TRLR.RNST -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST 
  TRLR.RNST.ABRT -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.ABRT 
  TRLR.RNST.DSC -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.DSC 
  TRLR.RNST.EKEY -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.EKEY 
  TRLR.RNST.ERR -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.ERR 
  TRLR.RNST.INTABRT -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.INTABRT 
  TRLR.RNST.LDTRC -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.LDTRC 
  TRLR.RNST.LIMX -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.LIMX 
  TRLR.RNST.OFF -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.OFF 
  TRLR.RNST.SSP -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.SSP 
  TRLR.RNST.XKEY -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.XKEY 
  TRLR.RNST.XXX -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.RNST.XXX 
  TRLR.SUBC -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.SUBC 
    G$NWIO - 
      HELP G$NWIO TRLR.SUBC 
  TRLR.TRAP.IR -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.TRAP.IR 
  TRLR.TRAP.TRAP# -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.TRAP.TRAP# 
  TRLR.XCON -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.XCON 
  TRLR.XCON.FLAGS.XCONP -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.XCON.FLAGS.XCONP 
  TRLR.XCON.TRAP# -   
    G$EXCFR - 
      HELP G$EXCFR TRLR.XCON.TRAP# 
  TRMATTR -   
    M$STRMATTR - 
      HELP M$STRMATTR TRMATTR 
  TRMCTL -   
    M$GTRMCTL - 
      HELP M$GTRMCTL TRMCTL 
  TRUNCATE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL TRUNCATE 
  TRUOVRPRT -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR TRUOVRPRT 
  TSAL$ -   
    G$TSA - 
      HELP G$TSA TSAL$ 
    G$TSA_HDR - 
      HELP G$TSA_HDR TSAL$ 
  TSAP$ -   
    G$ISA_HDR - 
      HELP G$ISA_HDR TSAP$ 
  TSA_USR -   
    G$UHJIT - 
      HELP G$UHJIT TSA_USR 
  TSTACKU Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  TSTAMP -   
    M$TIME - 
      HELP M$TIME TSTAMP 
  TTYP -   
    B$TERMINAL_ID - 
      HELP B$TERMINAL_ID TTYP 
  TTYTYPE -   
    VLP_TRMATTR - 
      HELP VLP_TRMATTR TTYTYPE 
  TUEXT -   
    G$JIT - 
      HELP G$JIT TUEXT 
  TUSVT -   
    G$JIT - 
      HELP G$JIT TUSVT 
  TYC -   
    M$DCB - 
      HELP M$DCB TYC 
  TYC.LD# -   
    M$DCB - 
      HELP M$DCB TYC.LD# 
  TYPE -   
    G$FRAME - 
      HELP G$FRAME TYPE 
    G$JIT - 
      HELP G$JIT TYPE 
    M$CVM - 
      HELP M$CVM TYPE 
U 
  U -   
    G$INDICATOR_REG - 
      HELP G$INDICATOR_REG U 
  UETIME -   
    M$WAIT - 
      HELP M$WAIT UETIME 
  UHJIT Segment - 
      HELP SAMPLE_FEP_PROGRAMS 
  UHJIT.DMN.ID -   
    G$UHJIT - 
      HELP G$UHJIT UHJIT.DMN.ID 
  UMEMTIM -   
    G$JIT - 
      HELP G$JIT UMEMTIM 
  UNAME -   
    G$JIT - 
      HELP G$JIT UNAME 
  UNDSCR -   
    VLP_FLDATR - 
      HELP VLP_FLDATR UNDSCR 
  UNIMPL -   
    VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS UNIMPL 
  UNIT0 -   
    M$CHGUNIT - 
      HELP M$CHGUNIT UNIT0 
  UNIT1 -   
    M$CHGUNIT - 
      HELP M$CHGUNIT UNIT1 
  UNIT2 -   
    M$CHGUNIT - 
      HELP M$CHGUNIT UNIT2 
  UNIT3 -   
    M$CHGUNIT - 
      HELP M$CHGUNIT UNIT3 
  UNITS -   
    M$CLOCK - 
      HELP M$CLOCK UNITS 
    M$WAIT - 
      HELP M$WAIT UNITS 
  Unshare Library or Program - 
      HELP M$UNSHARE 
  Unwind Routines - 
      HELP UNWIND_ROUTINES 
  UPPERCASE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL UPPERCASE 
  Usage of Parameters - 
      HELP USAGE_OF_PARAMETERS 
  User Virtual Memory - 
      HELP SAMPLE_FEP_PROGRAMS 
  USERID -   
    M$CVM - 
      HELP M$CVM USERID 
  USERSEG -   
    M$CVM - 
      HELP M$CVM USERSEG 
  USER_AUTO_LAYOUT - 
      HELP AUTOMATIC_STORAGE_LAYOUT 
  USER_DS1 - USER_DS4 Segments - 
      HELP SAMPLE_FEP_PROGRAMS 
  USR# -   
    G$JIT - 
      HELP G$JIT USR# 
  UTYPE -   
    M$CLOCK - 
      HELP M$CLOCK UTYPE 
    M$EOM - 
      HELP M$EOM UTYPE 
    M$WAIT - 
      HELP M$WAIT UTYPE 
  U_ECCB$ -   
    G$ROS - 
      HELP G$ROS U_ECCB$ 
V 
  V -   
    G$SEGDESC - 
      HELP G$SEGDESC V 
  VALUE-BIT(n) - 
      HELP NOTATION 
  VALUE-CHAR(n) - 
      HELP NOTATION 
  VALUE-DEC(range) - 
      HELP NOTATION 
  VALUES -   
    M$WRSYSLOG - 
      HELP M$WRSYSLOG VALUES 
    VLP_EOMTABLE - 
      HELP VLP_EOMTABLE VALUES 
  VARIABLE - 
      HELP NOTATION 
  VBRDRCHR -   
    VLP_WINDOW - 
      HELP VLP_WINDOW VBRDRCHR 
  VBRDRSIZ -   
    VLP_WINDOW - 
      HELP VLP_WINDOW VBRDRSIZ 
  VFC -   
    M$PROMPT - 
      HELP M$PROMPT VFC 
    M$WRITE - 
      HELP M$WRITE VFC 
  virtual segments - 
      HELP SAMPLE_FEP_PROGRAMS 
  VLPTYPE -   
    M$GTRMCTL - 
      HELP M$GTRMCTL VLPTYPE 
  VLP_CG - Comgroup Message Parameter - 
      HELP VLP_CG 
  VLP_EOMTABLE - 
      HELP VLP_EOMTABLE 
  VLP_ERRCODE - 
      HELP VLP_ERRCODE 
  VLP_FLDATR - 
      HELP VLP_FLDATR 
  VLP_HDR - Header Parameter - 
      HELP VLP_HDR 
  VLP_HMI - Handler/Monitor Interface Parameter - 
      HELP VLP_HMI 
  VLP_LINEATTR - 
      HELP VLP_LINEATTR 
  VLP_PLATEN - 
      HELP VLP_PLATEN 
  VLP_PPRIV - 
      HELP VLP_PPRIV 
  VLP_PRIV - 
      HELP VLP_PRIV 
  VLP_REGISTERS - 
      HELP VLP_REGISTERS 
  VLP_SCODE - 
      HELP VLP_SCODE 
  VLP_SEGMENT - 
      HELP VLP_SEGMENT 
  VLP_TAB - Tabulation Parameter - 
      HELP VLP_TAB 
  VLP_TEXTC - 
      HELP VLP_TEXTC 
  VLP_TRAP_CONDITIONS - 
      HELP VLP_TRAP_CONDITIONS 
  VLP_TRMATTR - 
      HELP VLP_TRMATTR 
  VLP_TRMCTL - 
      HELP VLP_TRMCTL 
  VLP_WINDOW - 
      HELP VLP_WINDOW 
  VLR_ERRMSG - 
      HELP VLR_ERRMSG 
  VLR_GCHAN - 
      HELP VLR_GCHAN 
  VLR_GDDL - 
      HELP VLR_GDDL 
W 
  WAIT -   
    M$READ - 
      HELP M$READ WAIT 
  WAKEME -   
    M$INTRET - 
      HELP M$INTRET WAKEME 
  WDT -   
    M$DCLFLD - 
      HELP M$DCLFLD WDT 
  WIDTH -   
    M$DCB - 
      HELP M$DCB WIDTH 
    VLP_PLATEN - 
      HELP VLP_PLATEN WIDTH 
    VLP_TRMATTR - 
      HELP VLP_TRMATTR WIDTH 
    VLP_WINDOW - 
      HELP VLP_WINDOW WIDTH 
  WINDOW -   
    M$OPEN - 
      HELP M$OPEN WINDOW 
  WORDWRAPCLM -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL WORDWRAPCLM 
  WP -   
    G$SEGDESC - 
      HELP G$SEGDESC WP 
  WRAPPAGE -   
    VLP_TRMCTL - 
      HELP VLP_TRMCTL WRAPPAGE 
  WRITE -   
    M$PDS - 
      HELP M$PDS WRITE 
  Write Data - 
      HELP M$WRITE 
  Write Multiple - 
      HELP M$WRTMLT 
  Write to System Log - 
      HELP M$WRSYSLOG 
  WRITES_HOST -   
    G$JIT - 
      HELP G$JIT WRITES_HOST 
  WRITES_UC -   
    G$JIT - 
      HELP G$JIT WRITES_UC 
X 
  X6A$CSEQM - 
      HELP G$BASE AUTO_TYPE 
  X6A$CSEQU - 
      HELP G$BASE AUTO_TYPE 
  X6A_MARET - 
      HELP RETURN_SEQUENCES 
  X6A_MAUNWIND - 
      HELP UNWIND_ROUTINES 
  X6A_MAUTO - 
      HELP RECEIVING_SEQUENCES 
  X6A_MSRET - 
      HELP RETURN_SEQUENCES 
  X6A_MSTATIC - 
      HELP RECEIVING_SEQUENCES 
  X6A_MSUNWIND - 
      HELP UNWIND_ROUTINES 
  XCON$ -   
    G$ECCB - 
      HELP G$ECCB XCON$ 
    M$XCON - 
      HELP M$XCON XCON$ 
  XLIMFLG -   
    G$JIT - 
      HELP G$JIT XLIMFLG 
  XLIMFLG.TIME -   
    G$JIT - 
      HELP G$JIT XLIMFLG.TIME 
  XTIME -   
    G$JIT - 
      HELP G$JIT XTIME 
Z 
  Z -   
    G$TSA - 
      HELP G$TSA Z 
    G$TSA_HDR - 
      HELP G$TSA_HDR Z 
  Z.BI -   
    G$TSA - 
      HELP G$TSA Z.BI 
    G$TSA_HDR - 
      HELP G$TSA_HDR Z.BI 
  Z.IS -   
    G$TSA - 
      HELP G$TSA Z.IS 
    G$TSA_HDR - 
      HELP G$TSA_HDR Z.IS 
  Z.R -   
    G$TSA - 
      HELP G$TSA Z.R 
    G$TSA_HDR - 
      HELP G$TSA_HDR Z.R 
  Z.REG -   
    G$TSA - 
      HELP G$TSA Z.REG 
    G$TSA_HDR - 
      HELP G$TSA_HDR Z.REG 
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
HELP_INDEX
NOTATION
To execute the host and FEP programs, the user's account must be authorized 
for FE access.  As a result of invoking the host run unit, the FPRG is started 
(in this case via execution of the M$OPEN monitor service in the host 
program). 
Note:  FEP handlers are started as a result of parameters specified via 
NETCON's SET BOOTINFO command.  For an example, see the System Manager 
Handbook (CE60). 
All PL-6 programs with the attribute MAIN will automatically call the routine 
X6A_MAUTO or X6A_MSTATIC to initialize automatic storage.  Other main programs 
must include a call to X6A_MAUTO or X6A_MSTATIC to insure proper operation if 
PL-6 subroutines are to be called. 
The M$CHGUNIT service permits the user to increment any of eight counters, 
four 16-bit counters in G$JIT.JOBUNIT and four 16-bit counters in 
G$JIT.STEPUNIT. 
If a counter overflows, it is set to the maximum value; the alternate return 
is then taken with the severity code set to 0. 
If any STEPUNIT counter is incremented during the course of a job step, an 
LCP-6 step accounting record will be written to the :ACCTLG.:SYS file when the 
job step is terminated.  The values of the JOBUNIT counters will be reflected 
in the LCP-6 job end accounting record in the :ACCTLG file. 
The form of the call for this service is: 
CALL M$CHGUNIT (FPT_CHGUNIT) [ALTRET (label)]; 
The parameters for the M$CHGUNIT service are as follows: 
    STEP = {YES|NO} specifies, if yes, that the step counter(s) are to be 
    incremented. NO specifies that the job counter(s) are not to be 
    incremented.  Default=YES. 
    UNIT0 = VALUE-DEC(0 to 2**16-1) specifies the value by which to increment 
    the first 16-bit counter.  Default=0. 
    UNIT1 = VALUE-DEC(0 to 2**16-1) specifies the value by which to increment 
    the second 16-bit counter. Default=0. 
    UNIT2 = VALUE-DEC(0 to 2**16-1) specifies the value by which to increment 
    the third 16-bit counter. Default=0. 
    UNIT3 = VALUE-DEC(0 to 2**16-1) specifies the value by which to increment 
    the fourth 16-bit counter. Default=0. 
00001
00002
00003
00004
00005
The M$CLOCK service provides the facility for requesting notification when a 
specified period of time has expired, obtaining the currently unexpired time 
and canceling an outstanding request.  Either Wall time or Execution time may 
be specified in minutes, seconds or UTS units.  Both Wall and Execution timers 
may be in effect at the same time. 
Notification of timer expiration may be by entry to the user's Event 
asynchronous procedure or by activation of a specified interrupt level. 
Both execution and wall timers may be made permanent.  In this mode they are 
reset to their original increment each time they expire. 
This service is only available to the User domain at the User Interrupt Level 
or a Handler Interrupt Level, and cannot be used by the Debugger. 
The form of the call for this service is: 
CALL M$CLOCK (FPT_CLOCK) [ALTRET(label)]; 
The parameters for this service are as follows: 
    CANCEL = {YES|NO} specifies, if YES, that the clock is to be canceled.  No 
    entry is made to the Event procedure or interrupt level scheduled. 
    The default is NO. 
    CLOCK = OPTION specifies which clock is to be used. 
    WALL specifies that the real time wall clock is to be used. 
    EXECUTION specifies that user execution time, including time spent 
    performing monitor services, is to be used. 
    The default is WALL. 
    LEVEL = VALUE-DEC(0-61) specifies an Interrupt Level that is to be 
    scheduled (triggered) when the requested clock interval expires. 
    A value of zero (0) indicates that no interrupt level is to be scheduled 
    but that the users EVENT asynchronous entry procedure is to be entered 
    instead.  When the event handler is entered, G$EXCFR.SUBC will be set to 
    %G_RTTMRSC# if the CLOCK option specified WALL.  G$EXCFR.SUBC will be set 
    to %G_XTMRSC# if CLOCK=EXECUTION was specified. 
    The default is zero (0). 
    MODE = OPTION specifies the operation to be performed.  Valid options are: 
    SET specifies that the clock is to be set.  Setting a clock that is 
    already running is permitted and begins a new interval. 
    TEST specifies that the current unelapsed time in the specified clock is 
    to be returned in UNITS. 
    The default is SET. 
    PERM = {YES|NO} specifies, if yes, that the clock is to be permanent and 
    is to be reset with the original time interval each time it expires. 
    The default is NO. 
    UNITS = VARIABLE locates a 1-word area. If MODE=SET is specified this area 
    contains the number of units of time which are to elapse before the user 
    is notified by entry to his Event procedure. 
    If MODE=TEST is specified, this area will be set to the number of units of 
    time remaining before the specified clock will expire. 
    The default is NIL. 
    UTYPE = OPTION specifies the kind of time that UNITS is expressed in. 
    Valid options are: 
         TICS  FEP UTS units (.133 seconds) 
         SEC   seconds 
         MIN   minutes 
    The default is TICS. 
00001
00002
00003
00004
00005
00006
00007
The M$CLOSE monitor service terminates and inhibits communication through a 
specified DCB until the DCB is again opened.  Once closed, no more messages 
may be sent on the path that was established when the DCB was opened. 
The form of the call for this service is: 
CALL M$CLOSE (FPT_CLOSE) [ALTRET (label)]; 
Parameters for the M$CLOSE service are as follows: 
    DCB = DCBNAME specifies the name of the DCB.  This parameter is required. 
    DISP = {DESTROY|KEEP} determines for DCBs open to UC streams only, whether 
    the stream itself is to be released when the DCB is closed. 
    If KEEP is not specified, the stream is released if no other DCBs are 
    still open to it.  If KEEP is specified, the stream (and any associated 
    window) will remain until a DCB is closed without KEEP, or until the FPRG 
    terminates. 
    Using DISP=KEEP corresponds roughly to using M$LDEV to create the stream 
    in Host programs. 
00001
00002
The M$CLRSTK service deletes one or more frames from the Exceptional Condition 
Stack.  Following this call, execution continues in-line.  If there is no 
environment in the Exceptional Condition Stack, the alternate return is taken. 
Note that on removing an exit control frame from the Exceptional Condition 
Stack, if that frame does not indicate a nested exit control entry, the 
program is removed from the "exit" status. 
To clear the top frame in the stack, the form of the call to this service is 
as follows: 
CALL M$CLRSTK [ALTRET (label)]; 
To clear more that one frame, the form of the call for this service is as 
follows: 
CALL M$CLRSTK (FPT_CLRSTK) [ALTRET (label)]; 
In this case, the parameter for the service is as follows: 
    FRAMES = VALUE-DEC(1-n) specifies the number of frames to remove from the 
    Exceptional Condition Stack.  If the value specified is equal to or 
    greater than the number of frames currently on the stack, all frames are 
    removed and the stack is marked empty.  Default = 1. 
00001
The M$CVM service provides for mapping a memory segment that does not belong 
to a user into the user's virtual data segment space.  Access to the segment 
is set to read-only for a user with the Special MM Privilege, and to full 
read/write access for a user with the Extended MM Privilege. 
M$CVM may be used to change the segment previously mapped via M$CVM without 
first freeing the virtual segment. 
The form of the call for this service is: 
CALL M$CVM (FPT_CVM) [ALTRET (label)]; 
The parameters for this service are as follows: 
    FROMSEG = VARIABLE specifies the location of the area of memory which 
    identifies the segment to be mapped onto.  The VLP_SEGMENT macro is used 
    to generate this area. 
    When the TYPE parameter is specified as MON or USER, the VLP_SEGMENT.BASE 
    field should contain the address of the monitor or user's segment; 
    VLP_SEGMENT.PAGES will be ignored. 
    Specifying TYPE=PHYSICAL assumes the contents of VLP_SEGMENT.PAGES to be 
    interpreted as a real physical page number; VLP_SEGMENT.BASE will be 
    ignored. 
    The default is NIL. 
    NEXT = {EITHER|LITTLE|BIG} specifies which data segment is to be obtained 
    when the BASE field in the VLP_SEGMENT area framed by the USERSEG 
    parameter is equal to the ADDR (NIL) or to zero, or when the USERSEG 
    parameter is not specified.  The NEXT parameter is ignored if 
    VLP_SEGMENT.BASE is used to indicate where memory is to be mapped. 
    Specifying LITTLE or BIG causes the next available data segment with the 
    specified virtual size attribute to be selected by memory management.  The 
    default (NEXT=EITHER) is used in conjunction with the PAGES parameter to 
    select the next available data segment with preference given to little 
    data segments. 
    PAGES = VALUE-DEC(0-256) specifies the number of pages to map onto.  A 
    value of 0 is considered to be a request to unmap a previously mapped 
    segment.  The default is 0. 
    TYPE = {MON|USER|PHYSICAL} specifies the type of segment that is to be 
    mapped onto. The default (TYPE=MON) causes the segment to come from the 
    monitor's map.  The specific monitor segment is identified by the value of 
    VLP_SEGMENT.BASE as located via the FROMSEG parameter. 
    Specifying (TYPE=USER) causes the segment to come from the map of the user 
    whose user number is specified by the USERID parameter.  The specific user 
    segment is identified by the value of VLP_SEGMENT.BASE as located via the 
    FROMSEG parameter. 
    Specifying (TYPE=PHYSICAL) causes the segment to come from real physical 
    memory.  The specific page to map onto is identified by the value of 
    VLP_SEGMENT.PAGES as located via the FROMSEG parameter. 
    USERID = VALUE-DEC specifies, when TYPE=USER the user number of the user 
    to be mapped onto.  This parameter is ignored if TYPE is not USER.  The 
    default is 0. 
    USERSEG = VARIABLE specifies the location of the area of memory which 
    contains a pointer to the segment to be mapped into.  The VLP_SEGMENT 
    macro is used to generate this area. 
    The value in VLP_SEGMENT.BASE is used to identify the segment to map into. 
    If the BASE field is equal to the ADDR (NIL) or to zero, or if the USERSEG 
    parameter is not specified, then the NEXT parameter is used to identify 
    the data segment to map into.  The segment located by the USERSEG 
    parameter must be currently unallocated or mapped by a prior use of M$CVM. 
    The default is NIL. 
00001
00002
00003
00004
00005
00006
A Data Control Block (DCB) is a context area, readable by the user and 
maintained by the monitor, which contains information pertaining to I/O 
operations to or from some entity.  This entity may be a cooperating host 
program, a communications device, or the circular queue. 
The M$DCB macro may be used to generate a DCB or a BASED structure for a DCB. 
The name of the DCB is to be specified using the DCBN=dcbname option. 
The STCLASS specification determines if storage is to be generated. 
Specification of STCLASS=DCB will cause a DCB to be generated for inclusion in 
the Read Only Segment.  STCLASS=BASED will generate a BASED structure that may 
be used to inspect any DCB within the Read Only Segment. 
When STCLASS=DCB is specified, certain of the fields within the DCB may be 
initialized.  The options for initialization are listed with the description 
of the field.  Other fields within the DCB are set by the monitor to reflect 
the results of an I/O operation through the DCB; no initialization parameters 
are provided. 
Fields within a DCB that may be initialized are as follows: 
    DCB = DCBNAME specifies the name of the DCB.  This parameter is required. 
    DISP = {KEEP|DESTROY} determines for DCBs open to UC streams only, whether 
    the stream itself is to be released when the DCB is closed. 
    If KEEP is not specified, the stream is released if no other DCBs are 
    still open to it.  If KEEP is specified, the stream (and any associated 
    window) will remain until a DCB is closed without KEEP, or until the FPRG 
    terminates. 
    The default is DESTROY. 
    DVFC = VALUE-CHAR(1) specifies the default format control character for 
    records which have no format control specified on the M$WRITE request. 
    The default causes this parameter to be ignored. 
    EVENT - SBIN contains the event to be reported when there is a COMIO event 
    to pass to the user. 
    KEYTYPE = {COORD|FLDID|MSGID} specifies the key type: 
    FLDID - The key refers to a field identifier (i.e., FPT_DCLFLD.ID, a 
    byte-aligned, 2-byte value).  See M$DCLFLD for details. 
    COORD - The key refers to the coordinates of a field (i.e., a 
    byte-aligned, 2-byte structure consisting of the line and column of the 
    field's location). 
    MSGID - This feature is not currently implemented. 
    The default causes this parameter to be ignored. 
    LINES = VALUE-DEC(0-32768) specifies the number of printable lines per 
    page.  The default causes this parameter to be ignored. 
    ORG = {CONSEC|CQ|FORM|TERMINAL|SE|UR|X364} specifies data organization. 
    This parameter describes how the data to be transmitted will be organized. 
    CONSEC   - The I/O will be in a consecutive, record-by-record manner. 
    CQ       - The I/O will be to/from a circular queue. 
    FORM     - The I/O will be to a FORMS type virtual device. 
    SE       - Not yet implemented in the FEP. 
    TERMINAL - The I/O will be to a TERMINAL type virtual device. 
    UR       - The I/O will be to a UNIT RECORD type virtual device. 
    X364     - The I/O will be to an X364 type virtual device. 
    The default causes this parameter to be ignored. 
    RECL = VALUE-DEC(0-32768) specifies the maximum data record length in 
    bytes.  This option is meaningful only for fixed record length formats. 
    Default = 0.  This word is REDEFed as FLDID for DCBs open ORG=FORM. 
    RES = VALUE-CHAR(4) specifies a device ('ddnn').  dd is the 2-character 
    device mnemonic which determines the direction the I/O may take.  At 
    present, this may be any of: 
    'HO' - for communication to a host 
    'UC' - for communication to a device 
    'LG' - for logging on a device 
    'NA' - for connecting to NODEADMN 
    The 'nn' field is a stream identifier, and determines which stream the I/O 
    will be on. 
    The default causes this parameter to be ignored. 
A listing of additional fields in the DCB follows.  These fields are not set 
via parameters for M$DCB but are available for access by users. 
    ACTPOS - VALUE-DEC(0-32767) indicates the position in the input record at 
    which activation occurred.  The first character of the record is at 
    position one.  A value of zero means that activation occurred at the the 
    end of the record. 
    ARS - UBIN   contains the actual record size read (in bytes). 
    DCB# - UBIN BYTE   contains the number of this DCB. 
    DCBNAME   contains the name of the DCB in TEXTC format: 
    DCBNAME.L - contains the length of DCBNAME.NAME 
    DCBNAME.NAME - contains the text and is initialized with 'dcbname' from 
    the DCBN option. 
    DVBYTE.  DVBYTE is set in the DCB following reads and informs the user 
    about the nature of the record read. 
    DVBYTE.BIN - BIT(1) specifies that the data is present as a string of bits 
    rather than one character per byte. 
    DVBYTE.BP - BIT(1) specifies blank preservation. If set trailing blanks 
    were not removed.  Reset specifies that blank stripping was performed. 
    DVBYTE.TRANS - BIT(1) specifies that the data was placed in the user 
    buffer without translation. 
    DVBYTE.VFC - BIT(1) set if the first character of the record should be 
    interpreted as a VFC character. 
    EOMCHAR - CHAR(2) when a read is done to a terminal, EOMCHAR is filled in 
    with the activation character or the VFC character if DVBYTE.VFC is set. 
    If there is no activating character or the read is not to a terminal and 
    doesn't have VFC, EOMCHAR is set to G_EOM_EOR# ('A@'). 
    FCD - BIT(1)   set if the DCB is currently open. 
    FCI - BIT(1)   set if the DCB was ever successfully opened. 
    FFLG contains a collection of access control flags set when the DCB is 
    opened.  These flags control the I/O  that may be performed via this DCB. 
    FFLG.READ - BIT(1)  if set, records may be read. 
    FFLG.WRITE - BIT(1)  if set, records may be written. 
    FLDID - UBIN contains the field ID reported by the most recent operation 
    for an ORG=FORM DCB.  It is the same as that returned in KEY if 
    KEYTYPE=FLDID, but is always returned here.  This is particularly useful 
    for operations like M$DCLFLD that that ALTRET but have no provision for 
    returning a key.  This word is a REDEF of RECL. 
    HMI$ - PTR points to an area containing header information in a handler's 
    circular queue.  The information is provided by the HMI option of M$OPEN. 
    LDCTX - VALUE-DEC(0-?)  contains an index into the LDCT table for the LDCT 
    associated with this connection. 
    RLCID.GENERATION - VALUE-DEC(8) contains the generation of the remote 
    connection. 
    RLCID.LDCTX - VALUE-DEC(16)   contains the LDCT number on the remote node. 
    RLCID.NODE - VALUE-DEC(8) contains the node number of the remote 
    connection. 
    SSN$ - is a pointer to the session context with which this DCB is 
    communicating. 
    TYC.  The Type Completion field is set upon completion of an I/O operation 
    through the DCB: 
    TYC.LD# - BIT(1)  set if Lost Data on an M$READ. 
    WIDTH - UBIN set to the number of columns on a printable line or card. The 
    value is zero if WIDTH is meaningless for this device. 
00010
00011
00001
00012
00013
00014
00015
00002
00016
00017
00018
00019
00020
00003
00021
00004
00022
00023
00024
00025
00026
00027
00028
00005
00029
00006
00007
00008
00009
00030
00031
00032
00033
00034
00035
00036
The M$DCLFLD service is used to declare a field on a given virtual device. 
The user specifies the location of the field, initializing text if there is 
any, and field attributes. 
A field is one or more contiguous positions on a line.  Field declarations 
must not overlap one another. 
The form of the call is as follows: 
CALL M$DCLFLD (FPT_DCLFLD) [ALTRET (label)]; 
Parameters for the M$DCLFLD service are as follows: 
    BUF = VARIABLE locates a buffer which may contain initializing text for 
    the field.  The default is NIL. 
    CLM = VALUE-DEC(1-254) specifies the column that the field begins in, 
    within the given virtual device. 
    DCB = DCBNAME specifies the name of the DCB associated with the device. 
    The DCB must have ORG=FORM and be assigned to a timesharing terminal 
    device. 
    DCB must be specified. 
    FLDATR = VARIABLE Locates a VLP_FLDATR area, which specifies the 
    attributes of the field being defined. 
    ID = VALUE-DEC(0-65535) specifies a field identifier to be used when 
    referencing this field. 
    LIN = VALUE-DEC(1-254) specifies the line within the virtual device that 
    the field is to be placed on. 
    RRR = {YES|NO} YES specifies Return Receipt Request.  This option 
    specifies that the function is not complete until it reaches its 
    destination correctly.  Functions to a user terminal are normally 
    considered complete when the data leaves the user buffer.  There is no way 
    to know if the data reached the terminal correctly or if any errors 
    occurred performing the function.  If RRR is set, the function is not 
    considered complete until the data reaches the terminal and any error 
    status has been returned. 
    RRR=YES should be used only for debugging, as it greatly reduces 
    processing speed since a response is required whether an error occurs or 
    not.  Without RRR, any field-oriented error is reported on the next M$READ 
    or other service request with RRR specified.  Only M$READ is capable of 
    returning an error code by ALTRETurning unless the RRR option is used. 
    WDT = VALUE-DEC(1-254) specifies the width (number of columns) that the 
    field will occupy within the virtual device. 
00001
00002
00003
00004
00005
00006
00007
00008
The M$DEVICE service allows modification of formatting attributes while output 
is being created.  A number of the options available on M$DEVICE override 
options which can be specified by M$DCB or M$OPEN. 
The M$DEVICE service is appropriate for unit record data; the DCB may be 
associated with a resource device or a logical device. 
The service call is of the form: 
CALL M$DEVICE (FPT_DEVICE) [ALTRET (label)]; 
The parameters for the call are as follows: 
    DCB = DCBNAME specifies the name of the DCB.  This parameter is required. 
    DVFC = VALUE-CHAR(1) specifies the default format control character for 
    records which have no format control specified on the M$WRITE request. 
    The default causes this parameter to be ignored. 
    HDR = VARIABLE locates an area containing the page header definition. 
    This area may be generated by invoking the VLP_HDR macro.  Page headings 
    may be discontinued by specifying the VLP_HDR macro parameter HDR=ERASE. 
    The default is NIL. 
    LINES = VALUE-DEC(1-32768) specifies the number of printable lines per 
    page.  The default causes this parameter to be ignored. 
    PAGE = {YES|NO} specifies, if YES, that the rest of the current page is to 
    be left blank.  The default is NO. 
    TAB = VARIABLE locates an area that contains the settings for horizontal 
    tabulation.  This area may be generated by invoking the VLP_TAB macro. 
    Tabulation may be discontinued by specifying the VLP_TAB macro parameter 
    TAB=ERASE. 
    The default is NIL. 
00001
00002
00003
00004
00005
00006
This service is used to specify the activation character set and the read 
time-out for the terminal.  The activation character set includes all 
characters to be interpreted as end-of-message characters.  The default 
activation character set is: 
EOT, LF, FF, CR, SUB, FS, GS, RS, US. 
The form of the call for this service is as follows: 
CALL M$EOM (FPT_EOM) [ALTRET (label)]; 
The parameters for this service are as follows: 
    DCB = DCBNAME specifies the DCB assigned to a timesharing terminal device. 
    The default is M$UC which is assigned to the user's timesharing terminal. 
    EOMTABLE = VARIABLE locates a table. The structure of the table is 
    generated by the VLP_EOMTABLE macro which is described next in this 
    section. 
    The activation set is unchanged if the parameter is NIL.  The default is 
    NIL. 
    SUPPHALT = {YES|NO} YES specifies that output on the terminal may not be 
    halted by actions of its operator (ESC-H, etc.).  NO allows halting.  The 
    default is NO. 
    TIMEOUT = VALUE-DEC(1-255) specifies a time-out period to be used on 
    subsequent M$READs to the terminal.  If a M$READ is not completed within 
    this time period, it is terminated with a timed-out completion type.  For 
    delayed-read devices, namely comgroup terminal stations, this time-out 
    period will only begin counting once the first character has been sent 
    from the device.  In other words, a "silent" delayed-read device will not 
    time out. 
    The units for TIMEOUT are specified by the UTYPE parameter.  The default 
    is 0 which indicates no time-out. 
    UTYPE = OPTION specifies the units of TIMEOUT.  Options are: 
    MIL10     10 milliseconds 
    SEC       seconds 
    MIN       minutes 
    The default is SEC. 
00001
00002
00003
00004
00005
For a DCB opened with ORG = FORM, the M$ERASE service is used to erase the 
selected field(s).  If no key is specified, all selected fields will be 
erased, subject to the PRT and CNS options. 
For a DCB opened with ORG = SE, the M$ERASE service is used to remove all 
records from the FEP cache. 
The form of the call is as follows: 
CALL M$ERASE (FPT_ERASE) [ALTRET (label)]; 
Parameters for the M$ERASE service are as follows: 
    CNS = {YES|NO} specifies whether or not constant fields are to be erased. 
    Erasing unprotected fields is implicit. 
    DCB = DCBNAME associated with the device.  The DCB must have ORG=FORM and 
    be assigned to a timesharing terminal device. 
    DCB must be specified. 
    KEY = VARIABLE locates an optional area containing a key to identify which 
    field is to be erased.  If no key is specified, all selected fields are 
    erased. 
    KEYTYPE = {COORD|FLDID|NONE} specifies the keytype to be used on this 
    function.  Specifies the keytype to be used on this function. 
    FLDID refers to a field identifier (i.e., FPT_DCLFLD.V.ID, a byte-aligned 
    2-byte value). 
    COORD refers to the coordinates of a field (i.e., a byte-aligned, 2-byte 
    structure consisting of the line and column of the field's location). 
    PRT = {YES|NO} specifies whether or not protected fields are to be erased. 
    Erasing unprotected fields is implicit. 
    RRR = {YES|NO} YES specifies Return Receipt Request.  This option 
    specifies that the function is not complete until it reaches its 
    destination correctly.  Functions to a user terminal are normally 
    considered complete when the data leaves the user buffer.  There is no way 
    to know if the data reached the terminal correctly or if any errors 
    occurred performing the function.  If RRR is set, the function is not 
    considered complete until the data reaches the terminal and any error 
    status has been returned. 
    RRR=YES should be used only for debugging, as it greatly reduces 
    processing speed since a response is required whether an error occurs or 
    not.  Without RRR, any field-oriented error is reported on the next M$READ 
    or other service request with RRR specified.  Only M$READ is capable of 
    returning an error code by ALTRETurning unless the RRR option is used. 
00001
00002
00003
00004
00005
00006
The M$ERR service provides for error termination of the current program. 
No FPT is required by M$ERR but one may be specified to provide for an 
explicit setting of the Step Condition Code or error code if desired.  If no 
FPT is specified, the Step Condition Code is set to 4 and the error code is 
set to %E$ERRPMME. 
The form of the call for this service is: 
CALL M$ERR; 
or 
CALL M$ERR (FPT_ERR) [ALTRET (label)]; 
When the FPT is specified, the parameters are as follows: 
    ERRCODE = VARIABLE specifies the 2 word memory location containing the 
    error code to be returned to the process that had initiated the program. 
    The VLP_ERRCODE macro should be used to generate a structure for the error 
    code.  The default is NIL. 
    STEPCC = {G_EXIT#|G_ERR#|G_ABORT#|VALUE-DEC(0-255)} specifies how the Step 
    Condition Code is to be set:  G_EXIT#=0, G_ERR#=4, or G_ABORT#=6.  The 
    parameter may also be specified as a decimal value (0-255).  The default 
    is G_ERR#. 
00001
00002
The M$ERRMSG service obtains an error message based on the error code supplied 
as a parameter, and stores the message in the user buffer.  M$ERRMSG allows 
phrase and message substitution.  The output of the M$ERRMSG service is a TEXT 
string placed in a user-passed area.  Status about the call is returned in a 
RESULTS area. 
The form of the call for this service is as follows: 
CALL M$ERRMSG (FPT_ERRMSG) [ALTRET(label)]; 
The required parameters for the service are CODE and BUF. 
    ALTCODE = VARIABLE specifies the area in memory containing the error code 
    identifying the alternate message to be read from the file. It is used to 
    form the key to read the file if no message can be found for CODE.  This 
    area is to be in standard VLP_ERRCODE format.  The default is NIL. 
    BUF = VARIABLE specifies the buffer where the TEXT form of the error 
    message is to be placed.  The default is NIL. 
    CODE = VARIABLE specifies the area in memory containing the error code 
    identifying the message to be read from the file.  This area is to be in 
    standard VLP_ERRCODE format.  The default is NIL. 
    FILEACCT = VARIABLE specifies the area containing a TEXT string consisting 
    of eight characters, word aligned, designating the account of the error 
    message file.  The default is NIL. 
    FILENAME = VARIABLE specifies the area containing the TEXTC name of a file 
    to be read for the error message.  The VLP_TEXTC macro may be invoked to 
    generate this area. If the named file cannot be opened or if no error 
    message or default message can be found in the file, this condition is 
    treated as if no FILENAME were specified.  The default is NIL. 
    FILEPASS = VARIABLE specifies the area containing a TEXT string consisting 
    of eight characters, word aligned, designating the password of the error 
    message file.  The default is NIL. 
    FLAGLEV = VALUE-DEC(0-4) specifies the number asterisks (*), from 0-4, 
    that precede the error message.  The number is an indication of the 
    seriousness of the error message.  The default is 0. 
    INCLCODE = {YES|NO} indicates whether or not the error code should be 
    output before the error message.  The default is YES. 
    LANG = VALUE-CHAR(1) is an encoded character that determines the native 
    language to be used for the message.  The default is a blank (for 
    English). 
    MY_LANG = {YES|NO} specifies, if YES, that the default native language key 
    is that of the user making the M$ERRMSG request.  NO specifies that the 
    character specified via the LANG option is to be used in selecting the 
    error message file.  The default is YES. 
    RESULTS = VARIABLE specifies an area in the user's data where any status 
    information about a call to M$ERRMSG is returned to the caller.  The 
    information returned consists of bits indicating unusual conditions 
    encountered in the processing of the CALL.  The VLR_ERRMSG macro described 
    later in this section can be invoked to generate this area.  The default 
    is NIL. 
    SOURCE = {PASS|TRAP|ALTRET} specifies where M$ERRMSG should look for the 
    error code to report on.  PASS, the default, indicates that the error code 
    will be passed in CODE.  TRAP indicates that M$ERRMSG should look in the 
    top frame of the exceptional condition stack for the error code (G$TCB$ -> 
    G$TCB.STK$ -> G$EXCFR.TRLR.ERR).  ALTRET indicates that M$ERRMSG should 
    look in the monitor services ALTRET frame for the error code (G$TCB$ -> 
    G$TCB.ALT$ -> G$EXCFR.TRLR.ERR). 
    SUBFILE = {YES|NO} specifies, if YES, to use the default system error 
    message file if the file passed by the user does not contain a message for 
    the code passed in this call.  The default is YES. 
    SUBLANG = {YES|NO} specifies, if YES, that a message will be in the 
    default language if the user's native language is not available.  The 
    default is YES. 
    SUBMESS = {YES|NO} specifies, if YES, to use a substitute message, (i.e., 
    one with less severity) or the default message, if the error message file 
    contains no message corresponding to the error code specified.  The 
    default is YES.  If no substitute message is available, the text of the 
    error code is used. 
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
The M$EVENT service is used to establish the entry address of the users event 
processing procedure that is to receive control upon completion of an 
asynchronous operation, such as no-wait read or real time clock expiration. 
This service may also be used to determine the address of any previously set 
event control procedure and to reset the request for event control.  If an 
event completion occurs when event control has been reset, the program is 
aborted. 
Entry to the event procedure occurs following a monitor service request or at 
the completion of a time slice.  If a program has been suspended by the M$WAIT 
service when an event completion occurs, the suspension is terminated and the 
event completion is reported. 
The user may request as many concurrent no-wait operations as desired.  The 
order in which events are processed is not necessarily the order in which they 
were requested.  The event procedure processes events in the order of event 
completion. 
The event frame on the TCB contains the environment as described by the 
G$EXCFR structure.  The user may access the event frame through the STK$ 
pointer in the TCB; i.e. 
    G$TCB$ -> G$TCB.STK$ -> G$EXCFR 
G$EXCFR.ECC in the event frame will be set to %G_EVENT#. 
G$EXCFR.TRLR.SUBC in the event frame will be set to one of the following: 
  %G_XTMRSC#      0    M$CLOCK execution timer expiration 
  %G_RTTMRSC#     1    M$CLOCK real-time timer expiration 
  %G_DATA_RQS#    3    Remote end-point has issued a read 
  %G_DATA_AVL#    4    Remote end-point has issued a write 
  %G_IO_CMP#      5    IO Complete 
G$EXCFR.TRLR.EVID contains the user supplied event identification. 
G$EXCFR.TRLR.ERR will contain the error code (if any). 
The form of the call for this service is: 
CALL M$EVENT (FPT_EVENT) [ALTRET(label)]; 
The parameter for this service is as follows: 
    EVENT$ = {ENTRY|NIL} specifies the event procedure entry address. An 
    address of NIL resets a previous request and specifies that event 
    completion is not to be reported to the user.  Default = NIL. 
    If both NEVENT and EVENT$ are specified, the EVENT$ parameter is ignored. 
    NEVENT = VARIABLE locates a 2-word area that contains an EPTR to the 
    procedure that is to be entered when event completion occurs.  If the EPTR 
    contained in NEVENT is ENTADDR(NIL) the request for event control is 
    reset.  Default = NIL. 
    PEVENT = VARIABLE locates a 2-word area where an EPTR to the previously 
    set event procedure is to be returned.  Default = NIL. 
00001
00002
00003
The M$EXIT service provides for normal termination of the current program. 
No FPT is required by M$EXIT but one may be specified to provide for an 
explicit setting of the Step Condition Code or error code if desired.  If no 
FPT is specified, the Step Condition Code and the error code are both set to 
zero. 
The form of the call for this service is: 
CALL M$EXIT; 
or 
CALL M$EXIT (FPT_EXIT) [ALTRET (label)]; 
When the FPT is specified, the parameters are as follows: 
    ERRCODE = VARIABLE specifies the 2 word memory location containing the 
    error code to be returned to the process that had initiated the program. 
    The VLP_ERRCODE macro should be used to generate a structure for the error 
    code.  The default is NIL. 
    STEPCC = {G_EXIT#|G_ERR#|G_ABORT#|VALUE-DEC(0-255)} specifies how the Step 
    Condition Code is to be set:  G_EXIT#=0, G_ERR#=4, or G_ABORT#=6.  The 
    parameter may also be specified as a decimal value (0-255).  The default 
    is G_EXIT#. 
00001
00002
The M$FAUTO service provides for deallocation of memory from the AUTO data 
segment area of the user's virtual memory. 
The form of the call for this service is: 
CALL M$FAUTO (FPT_FAUTO) [ALTRET (label)]; 
The parameters for this service are as follows: 
    PAGES = VALUE-DEC(0-256) specifies the number of pages to release.  A 
    value of 0 is considered to be a status request, thus no memory will be 
    released.  The default is 0. 
    RESULTS = VARIABLE specifies the location of the area of memory where the 
    monitor will return a pointer to the first page of dynamic memory 
    remaining as well as the number of pages that remain allocated.  The 
    VLP_SEGMENT macro is used to generate this area.  The default is NIL. 
00001
00002
The M$FDS service provides for deallocation of memory from an allocated memory 
extent in the user's virtual memory. 
The number of pages to released is specified via the PAGES parameter.  The 
area of memory to be released is specified in the VLP_SEGMENT.BASE field of 
the RESULTS parameter. 
The form of the call for this service is: 
CALL M$FDS (FPT_FDS) [ALTRET (label)]; 
The parameters for this service are as follows: 
    PAGES = VALUE-DEC(0-n) specifies the number of pages to release.  A value 
    of 0 is considered to be a status request, thus no memory will be 
    released; information reflecting the current allocation of the specified 
    memory extent will be returned in the area specified via the RESULTS 
    parameter.  Default is 0. 
    RESULTS = VARIABLE specifies the location of the area of memory which is 
    used both as an input parameter and an output results area.  The 
    VLP_SEGMENT macro is used to generate this area. 
    On input, the BASE field in this area (VLP_SEGMENT.BASE) is used to 
    identify the memory extent to free or diminish.  On return from this 
    monitor service request the VLP_SEGMENT.BASE field will contain a pointer 
    to the first page of memory remaining in the extent.  The 
    VLP_SEGMENT.PAGES field will contain the number of pages that remain 
    allocated in the memory extent. 
    The default is NIL. 
00001
00002
The M$GAUTO service provides for allocation of memory from the AUTO data 
segment area of the user's virtual memory. 
The AUTO data segment area consists of a unique data segment in the user's 
virtual memory.  Memory can be allocated or deallocated from the AUTO segment 
only by use of the M$GAUTO and M$FAUTO services. 
The form of the call for this service is: 
CALL M$GAUTO (FPT_GAUTO) [ALTRET (label)]; 
The parameters for this service are as follows: 
    FREE = {YES|NO} specifies, if YES, that if the requested memory is not 
    available (user or installation memory limit reached), then no memory at 
    all is to be allocated.  The default (FREE=NO) causes as much memory as 
    possible to be allocated before returning an error code indicating that 
    the entire requested amount was unavailable. 
    PAGES = VALUE-DEC(0-256) specifies the number of pages to obtain.  A value 
    of 0 is considered to be a status request, thus no memory will be 
    allocated.  The default is 0. 
    RESULTS = VARIABLE specifies the location of the area of memory where the 
    monitor will return a pointer to the first page of memory allocated as 
    well as the number of pages that have been allocated.  The VLP_SEGMENT 
    macro is used to generate this area.  The default is NIL. 
00001
00002
00003
The M$GCHAN monitor service allows the user (with TND privilege) to acquire an 
available channel, with specific resource type and attributes, to be used for 
I/O.  Additionally, the user may request the channel for diagnostic purposes 
(T&Ds) and/or request the entire controller (in the case of NMLC or MLCP 
devices).  If a device of the appropriate characteristics cannot be acquired, 
an appropriate error is returned. 
The form of the call is as follows: 
CALL M$GCHAN (FPT_GCHAN) [ALTRET(label)]; 
Parameters for the M$GCHAN service are as follows: 
    ATTR = VALUE-BIT(16) specifies a bit string indicating the software 
    attributes of the channel to be acquired.  For details, see the CP-6 
    System Support Reference (HA20), NETCON, ATTR option in the table 
    'CONFIG/DEFAULT Command Line Options' and the discussion in and before the 
    table 'RESOURCE Attribute Defaults'.  The default is 0. 
    CHANNEL = VALUE-DEC(0-?) specifies a particular channel.  This field is 
    only valid if DIAG=YES.  The default is 0. 
    CONTROLLER = {YES|NO} if set, the entire controller is to be acquired. 
    CONTROLLER is only honored if DIAG is set.  Which controller to acquire is 
    determined by the value specified for CHANNEL.  If no value is specified, 
    an error is reported.  The default is NO. 
    DIAG = {YES|NO} if set, this channel is being acquired for diagnostic 
    purposes.  The default is NO. 
    ENB = {YES|NO} specifies whether or not the acquired channel is to come up 
    enabled.  The default is NO. 
    GCHAN = VARIABLE locates an area defined by the VLR_GCHAN macro, which 
    contains information passed back about the channel acquired.  The default 
    is NIL. 
    HIGHLOW = {YES|NO} specifies whether or not the HIGHCHAN and LOWCHAN 
    fields are to be returned in the VLR_GCHAN macro.  The default is YES. 
    RES = VALUE-CHAR(2) is the software resource type of the channel to be 
    acquired.  The resource types are as follows: 
    CL    Communication Line 
    DK    Diskette 
    HL    Host Link 
    UR    Unit Record 
    The default is blank. 
00001
00002
00003
00004
00005
00006
00007
00008
The M$GDDL service provides information about the current state of the user's 
memory allocation.  Information is returned in the area of memory that is 
generated by the VLR_GDDL macro. 
The form of the call for this service is: 
CALL M$GDDL (FPT_GDDL) [ALTRET (label)]; 
The parameters for this service are as follows: 
    RESULTS = VARIABLE specifies the location of the area of memory into which 
    the informational data provided by the M$GDDL service is returned to the 
    user.  The VLR_GDDL macro is used to generate this area.  The default is 
    NIL. 
00001
The M$GDS service provides for allocation of memory from an unallocated memory 
extent in the user's virtual memory.  This service may be used for the initial 
allocation of a memory extent, or to enlarge the current allocation of an 
extent. 
The number of pages to allocate is always specified via the PAGES parameter. 
The area of memory to be allocated may be specified in either the 
VLP_SEGMENT.BASE field of the RESULTS parameter or by using the NEXT 
parameter. 
The form of the call for this service is: 
CALL M$GDS (FPT_GDS) [ALTRET (label)]; 
The parameters for this service are as follows: 
    FREE = {YES|NO} specifies, if YES, that if the requested memory is not 
    available (user or installation memory limit reached), then no memory at 
    all is to be allocated. 
    The default (FREE=NO) causes as much memory as possible to be allocated 
    before taking the alternate return with an error code indicating that the 
    entire requested amount was unavailable.  The VLP_SEGMENT area, as 
    specified via the RESULTS parameter, may be inspected to determine how 
    many pages were actually allocated. 
    IOBUF = {YES|NO} specifies, if YES, that the physical memory obtained is 
    to come from the the area of system memory reserved for I/O buffers.  The 
    default (IOBUF=NO) causes the physical memory to be obtained from the 
    system area reserved for ordinary, i.e., non-I/O buffer, system memory. 
    NEXT = {EITHER|LITTLE|BIG} specifies which data area is to be obtained 
    when the BASE field in the VLP_SEGMENT area framed by the RESULTS 
    parameter is equal to the ADDR (NIL) or to zero, or when the RESULTS 
    parameter is not specified.  The NEXT parameter is ignored if 
    VLP_SEGMENT.BASE is used to indicate where memory is to be allocated. 
    Specifying LITTLE or BIG causes the next available data extent with the 
    specified virtual size attribute to be selected by memory management.  The 
    default (NEXT=EITHER) is used in conjunction with the PAGES parameter to 
    select the next available data extent with preference given to little data 
    segments. 
    PAGES = VALUE-DEC(0-n) specifies the number of pages to obtain.  A value 
    of 0 is considered to be a status request, thus no memory will be 
    allocated; information reflecting the current allocation of the specified 
    memory extent will be returned in the area specified via the RESULTS 
    parameter.  Default is 0. 
    RESULTS = VARIABLE specifies the location of the area of memory which is 
    used both as an input parameter and an output results area.  The 
    VLP_SEGMENT macro is used to generate this area. 
    On input, the BASE field in this area (VLP_SEGMENT.BASE) is used to 
    identify the memory extent to obtain or enlarge.  If the BASE field is 
    equal to the ADDR (NIL) or to zero, then the NEXT parameter will be used 
    to determine where memory is to be allocated.  Note that this is an 
    optional parameter; if not specified, the NEXT parameter must be used. 
    On normal return from this monitor service request the VLP_SEGMENT.BASE 
    field will contain a pointer to the first page of the allocated extent. 
    The VLP_SEGMENT.PAGES field will contain the number of pages currently 
    allocated in the memory extent. 
    Normally, the VLP_SEGMENT area will not be modified upon return when the 
    alternate return is taken.  See the description of the FREE parameter for 
    the exception. 
    The default is NIL. 
00001
00002
00003
00004
00005
The M$GETDCB service allocates a DCB.  The M$GETDCB service returns the DCB 
number for the DCB which is built. If a DCB of the name specified already 
exists, its DCB number is returned as if it had been built. 
The M$GETDCB service call is of the form: 
CALL M$GETDCB (FPT_GETDCB) [ALTRET (label)]; 
The parameters for this service are as follows: 
    DCBNAME = VARIABLE locates a VLP_NAME area containing the name of the DCB 
    to be obtained.  The default is NIL. 
    DCBNUM = VARIABLE locates a 1-word area into which the M$GETDCB service 
    returns the number of the DCB allocated, or if the DCB already exists, the 
    number corresponding to DCBNAME.  The default is NIL. 
00001
00002
The GLINEATTR service provides the user with information concerning the 
physical connection of the terminal to the system. 
The form of the call is as follows: 
CALL M$GLINEATTR (FPT_GLINEATTR) [ALTRET (label)]; 
Parameters for the M$GLINEATTR service are as follows: 
    DCB = DCBNAME specifies the DCB assigned to a timesharing terminal device. 
    The default is M$UC which is assigned to the user's timesharing terminal. 
    LINEATTR = VARIABLE locates a buffer that contains the physical line 
    information.  The structure of the buffer is generated by the VLP_LINEATTR 
    macro described next in this section. 
    The default is NIL. 
00001
00002
M$PLATEN
M$PROMPT
M$STRMATTR
The services described in this section allow the user to manipulate the 
terminal attributes and to specify special control of the terminal. 
The M$GTRMCTL service provides the user with the current terminal control 
information.  Terminal control information includes terminal control flags set 
by PROFILE, escape-character sequences, or M$STRMCTL. 
The form of the call for this service is as follows: 
CALL M$GTRMCTL (FPT_TRMCTL) [ALTRET (label)]; 
The M$STRMCTL service is used to programmatically set flags that control 
various characteristics of the terminal.  Many of these flags can also be set 
by the terminal user through the use of escape character sequences or via a 
profile. 
The form of the call for this service is as follows: 
CALL M$STRMCTL (FPT_TRMCTL) [ALTRET (label)]; 
Parameters for FPT_TRMCTL are as follows: 
    DCB = DCBNAME specifies the DCB assigned to a timesharing terminal device. 
    The default is M$UC which is assigned to the user's timesharing terminal. 
    TRMCTL = VARIABLE locates a buffer that contains or receives the terminal 
    control information.  The structure of the buffer is generated by the 
    VLP_vlptype macros described next in this section (see the VLPTYPE 
    option).  The default is NIL. 
    VLPTYPE = OPTION specifies which of a number of terminal control 
    structures is to be used to set or receive the control attributes.  The 
    name of the macro describing the TRMCTL variable may be constructed by 
    preceding the VLPTYPE option with a prefix of VLP_, e.g. VLP_TRMCTL.  The 
    options are TRMCTL, WINDOW, and EDTCTL.  Preprocessor equates for the 
    values used for this option are constructed by following the option name 
    with a #, and preceding the option name with G_TRMCTL_, e.g. 
    G_TRMCTL_TRMCTL#. 
    The default is TRMCTL. 
00001
00002
00003
The M$GTRMTAB service to obtain the device tab setting of the terminal. 
Device tabs are the physical tabs of the terminal.  The system uses device 
tabs to optimize carriage movement.  Device tabs are only used by the system 
and do not affect logical tabs or tab characters, with the following 
exceptions.  When an M$WRITE is issued to the terminal with a DCB that 
specifies ORG=TERMINAL and TRANS=YES or when tab simulation is not used (in 
VLP_TRMCTL TABSIM=NO), a tab character causes the terminal to move to the next 
device tab. 
NOTE:  To set normal horizontal tabulation at a terminal in order to align 
text, use the M$DEVICE not the M$STRMTAB service.  Refer to Section 3 for a 
discussion of M$DEVICE. 
The form of the call for this service is as follows: 
CALL M$GTRMTAB (FPT_TRMTAB) [ALTRET (label)]; 
The M$STRMTAB service is used to set the device tab setting of the terminal. 
The form of the call for this service is as follows: 
CALL M$STRMTAB (FPT_TRMTAB) [ALTRET (label)]; 
Parameters for FPT_TRMTAB are as follows: 
    DCB = DCBNAME specifies the DCB assigned to a timesharing terminal device. 
    The default is M$UC which is assigned to the user's timesharing terminal. 
    TAB = VARIABLE specifies a buffer from which the tab settings are moved. 
    The structure of the buffer is generated by the VLP_TAB macro.  When 
    specifying device tabs via VLP_TAB, MARGIN sets the first device tab and 
    TAB specifies the remainder of the tabs.  (VLP_TAB is defined in Section 
    3.)  If the terminal has no device tabs or if the device tabs are unknown, 
    0 is returned for all tab positions. 
    The default is NIL. 
00001
00002
The M$INT service permits the caller to specify a procedure to be entered in 
the event the BREAK key or YC (Control Y) is depressed.  The specified 
procedure is entered with the environment of the interrupted process on the 
TCB. 
The event frame on the TCB contains the environment as described by the 
G$EXCFR structure.  The user may access the event frame through the STK$ 
pointer in the TCB; i.e. 
    G$TCB$ -> G$TCB.STK$ -> G$EXCFR 
G$EXCFR.ECC in the event frame will be set to %G_BRK#. 
G$EXCFR.TRLR.SUBC in the event frame will be set to one of the following: 
  %G_YCSC#      0      YC (Control Y) was typed. 
  %G_BRKSC#     1      BREAK was typed. 
G$EXCFR.TRLR.ERR will contain the JIT error code. 
The form of the call for this service is: 
CALL M$INT (FPT_INT) [ALTRET (label)]; 
Parameters for the M$INT service are as follows: 
    INT$ = {ENTRY|NIL} specifies the procedure that is to be entered when the 
    terminal break key is depressed.  An address of NIL resets any previous 
    request for break control.  Default = NIL. 
    If both NINT and INT$ are specified, the INT$ parameter is ignored. 
    NINT = VARIABLE locates a 2-word area that contains an EPTR to the 
    procedure that is to be entered upon when the terminal break key is 
    depressed.  If the EPTR is ENTADDR(NIL) the request for break control is 
    reset.  Default = NIL. 
    PINT = VARIABLE locates a 2-word area where an EPTR to the previously set 
    break control address is to be returned.  Default = NIL. 
00001
00002
00003
The M$INTCON service allows a user to specify the entry address of an 
interrupt processing routine that receives control when an interrupt of the 
specified level occurs on the user's CPU. 
The INTCON privilege is required to use this service. 
The form of the call for this service is: 
CALL M$INTCON (FPT_INTCON) [ALTRET (label)]; 
The parameters for this service are as follows: 
    IENTRY = ENTRY specifies the interrupt procedure entry address.  A NIL 
    specification relinquishes control of the interrupt level(s) otherwise 
    specified in this FPT.  The default is NIL. 
    LEVEL = VALUE-DEC(12-59) specifies the interrupt level for which control 
    is requested.  A value of zero (the default) indicates that this service 
    request means only to allocate a RUNLEVEL.  The default is 0. 
    PRIVILEGED = {YES|NO} specifies, if yes, that IENTRY is to be entered in 
    RING-1 instead of RING-3. YES requires that the user be allowed to enter 
    master mode (MSYS privilege).  The default is YES. 
    RUNLEVEL = VALUE-DEC(12-59) specifies the level at which IENTRY is to be 
    entered as a result of an interrupt at LEVEL.  The default value of zero 
    implies RUNLEVEL=LEVEL. 
    This facility is NOT the same as a disable to RUNLEVEL, in that an enable 
    instruction (LEV '803F'X,IMO) is equivalent to M$INTRET, not a return to 
    execution at LEVEL. 
    If RUNLEVEL is specified but LEVEL is not, then RUNLEVEL is simply 
    reserved for this user as a disable level, to avoid conflicts with other 
    users.  The default is 0. 
00001
00002
00003
00004
The M$INTREL service is the complement of M$INTCON, providing a mechanism to 
release control of an interrupt level. 
The form of the call for this service is: 
CALL M$INTREL (FPT_INTREL) [ALTRET (label)]; 
The parameters for this service are as follows: 
    LEVEL = VALUE-DEC(12-59) specifies the level whose control is to be 
    relinquished.  The user must own the level to avoid an ALTRET.  The 
    default is 0. 
00001
The M$INTRET service should be used by a user interrupt processing routine to 
relinquish the CPU and wait for the next interrupt. It provides options to 
inform the main user program, if desired. 
The form of the call for this service is: 
CALL M$INTRET (FPT_INTRET) [ALTRET (label)]; 
The parameters for this service are as follows: 
    EVENT = VALUE-DEC(1-n) specifies the event to be reported to the user main 
    program to indicate the occurrence of the interrupt. 
    EVENT and WAKEME are mutually exclusive options.  If both are specified, 
    EVENT is honored and WAKEME is ignored.  The default is 0. 
    WAKEME = {YES|NO} specifies, if yes, that the user main program is to be 
    awakened (if asleep) without reporting an event (see the EVENT option). 
    The default is NO. 
00001
00002
The monitor LDTRC routine releases the memory used by the calling program, 
loads a specified run unit and transfers control to the starting address of 
the called run unit. Any communication from the calling program to the called 
program must be accomplished through user Dynamic Data Segment 4 and/or the 
Control Command Buffer.  All allocated data segments with the exception of 
user Dynamic Data Segment 4, are released by an M$LDTRC operation. 
If Exit Control has been established in the calling program, the issuing of an 
M$LDTRC causes control to be passed to the effective Exit Control procedure. 
The M$LDTRC occurs on exit from the Exit Control procedure, via M$EXIT or 
M$TRTN. 
The called program may determine that it has been entered via M$LDTRC as the 
value of G$JIT.PROG_ENTRY will have been set to %G_PE_LDTRC#. 
If a debugger is associated with the user, the debugger remains associated. 
If the called run unit is not found or the user's memory allocation limits 
would be exceeded by loading the run-unit, the alternate return will be taken. 
If an I/O error occurs when reading the run-unit, the job is aborted. 
The form of the call for this service is: 
CALL M$LDTRC (FPT_LDTRC) [ALTRET (label)]; 
The parameters for this service are as follows: 
    ACCT = VARIABLE specifies an area containing a TEXT string consisting of 
    eight characters, designating the account from which the run unit is to be 
    obtained.  The default is NIL. 
    CMD = VARIABLE locates an area containing a TEXT string of up to 256 
    characters that is passed in the Control Command Buffer to the called 
    program.  The default is NIL. 
    DISP = {KEEP|DESTROY} allows the user to specify the action the monitor is 
    to take when closing any open DCBs prior to loading the target run unit. 
    This option determines for DCBs open to UC streams only, whether the 
    stream itself is to be released when the DCB is closed. 
    If KEEP is not specified, the stream is released if no other DCBs are 
    still open to it.  If KEEP is specified, the stream (and any associated 
    window) will remain until a DCB is closed without KEEP, or until the FPRG 
    terminates. 
    The default is DESTROY. 
    NAME = VARIABLE specifies an area containing a TEXTC string consisting of 
    up to 31 characters, designating the run unit to which control is to be 
    transferred.  The area may be generated by invoking the VLP_TEXTC macro. 
    The default is NIL. 
    NO_MICROFPL = {YES|NO} allows TPFP to specify that the FPRG specified is 
    to be put into execution and that no attempt is to be made to associate 
    TPFP.:SYS for microFPL loading. 
    PASS = VARIABLE specifies the location of a string consisting of eight 
    characters, designating the password associated with the run unit.  The 
    default is NIL. 
    PSN = VARIABLE specifies the location of a 6 character string designating 
    the identification of the pack set on which the run unit is located.  The 
    default is NIL. 
00001
00002
00003
00004
00005
00006
00007
The M$MDFFLD service is used to modify a field on a given virtual device. The 
user specifies a key defining the location of the field, initializing text if 
there is any, and field attributes(optionally).  If no key is specified, all 
fields selected by the M$SLCFLD service are modified. 
The form of the call is as follows: 
CALL M$MDFFLD (FPT_MDFFLD) [ALTRET (label)]; 
Parameters for the M$MDFFLD service are as follows: 
    BUF = VARIABLE locates a buffer which may contain initializing text for 
    the field.  The default is NIL. 
    DCB = DCBNAME associated with the device.  The DCB must have ORG=FORM and 
    be assigned to a timesharing terminal device. 
    DCB must be specified. 
    FLDATR = VARIABLE locates a VLP_FLDATR area, which specifies the 
    attributes of the field being defined.  The FLDATR parameter is required. 
    KEY = VARIABLE locates an optional area containing a key to identify which 
    field is to be modified.  If no key is specified, all selected fields are 
    modified. 
    KEYTYPE = {COORD|FLDID|NONE} Specifies the keytype to be used on this 
    function. 
    FLDID refers to a field identifier (i.e., FPT_DCLFLD.V.ID, a byte-aligned 
    2-byte value). 
    COORD refers to the coordinates of a field (i.e., a byte-aligned, 2-byte 
    structure consisting of the line and column of the field's location). 
    RRR = {YES|NO} YES specifies Return Receipt Request.  This option 
    specifies that the function is not complete until it reaches its 
    destination correctly.  Functions to a user terminal are normally 
    considered complete when the data leaves the user buffer.  There is no way 
    to know if the data reached the terminal correctly or if any errors 
    occurred performing the function.  If RRR is set, the function is not 
    considered complete until the data reaches the terminal and any error 
    status has been returned. 
    RRR=YES should be used only for debugging, as it greatly reduces 
    processing speed since a response is required whether an error occurs or 
    not.  Without RRR, any field-oriented error is reported on the next M$READ 
    or other service request with RRR specified.  Only M$READ is capable of 
    returning an error code by ALTRETurning unless the RRR option is used. 
    SETGRPRND = {YES|NO} specifies whether or not the field's graphic 
    rendition is to be changed. 
    SETQLF = {YES|NO} specifies whether or not the field's qualification 
    attributes are to change. 
00001
00002
00003
00004
00005
00006
00007
00008
The M$MERC service returns control from the user ALTRET code sequence to the 
monitor.  This service is provided in case the ALTRET procedure cannot process 
all possible error codes.  The original environment from the error on a 
monitor service call is assumed to be in the ALTRET frame of the TCB at the 
call to the M$MERC service. 
The monitor responds by taking appropriate action based on the severity of the 
error: 
Severity Level   Monitor Action 
0               Ignore the error.  Return to the statement 
              following the monitor service call, with the 
              Trap Save Area reflecting the original 
              environment.  If the MERC is from exit control 
              the monitor performs M$EXIT. 
1-4              Abort the program. (The monitor performs M$ERR.) 
> 4              Abort the program.  (The monitor performs M$XXX.) 
The STEPCC will be set to the value of the severity of the error code.  The 
M$MERC service takes the alternate return if there is no environment in the 
ALTRET frame of the TCB.  No FPT is required by M$MERC but one may be 
specified to provide for explicit setting of the severity of the error. 
The form of the call for this service is: 
CALL M$MERC [ALTRET(label)]; 
or 
CALL M$MERC(FPT_MERC) [ALTRET(label)]; 
The M$MERCS service performs the same function as the M$MERC service, except 
that the environment is assumed to be in the top frame of the Exceptional 
Condition Stack.  (The M$MERCS service releases this top frame.)  Thus this 
service is appropriate for use in an ALTRET code sequence that previously 
executed M$SENV, in the M$TRAP procedure when G$EXCFR.TRLR.TRAP.TRAP# contains 
%G_MCL#, and in an exit control procedure that receives control because the 
program provides no ALTRET procedure or M$TRAP procedure. 
The M$MERCS service takes the alternate return if the Exceptional Condition 
Stack frame is empty.  No FPT is required by M$MERCS but one may be specified 
to provide for explicit setting of the severity of the error. 
The form of the call for this service is: 
CALL M$MERCS [ALTRET(label)]; 
or 
CALL M$MERCS(FPT_MERC) [ALTRET(label)]; 
Note that FPT_MERC is used for both the M$MERC and M$MERCS services. The 
parameter is: 
    ERRCODE = VARIABLE locates the double word that is to be used to replace 
    the error code.  The VLP_ERRCODE macro should be used to generate the 
    error code.  When specified the value of the Severity will be used by the 
    monitor to determine how to proceed.  The default is NIL. 
00001
The M$OPEN service allows the user to establish a path (SESSION) with the 
named device or program.  This path can then be used for communication between 
the two entities.  Once a path is open, services such as M$READ and M$WRITE 
may be used to send and receive messages on that path. 
The form of the call for this service is: 
CALL M$OPEN (FPT_OPEN) [ALTRET (label)]; 
Parameters for the M$OPEN service are as follows: 
    DCB = DCBNAME specifies the name of the DCB.  This parameter is required. 
    DISP = {KEEP|DESTROY} determines for DCBs open to UC streams only, whether 
    the stream itself is to be released when the DCB is closed. 
    If KEEP is not specified, the stream is released if no other DCBs are 
    still open to it.  If KEEP is specified, the stream (and any associated 
    window) will remain until a DCB is closed without KEEP, or until the FPRG 
    terminates. 
    The default is DESTROY. 
    DVFC = VALUE-CHAR(1) specifies the default format control character for 
    records which have no format control specified on the M$WRITE request. 
    The default causes this parameter to be ignored. 
    EVENT = VALUE-DEC(-32768-32767) is the event number returned on all events 
    associated with this DCB.  The default is 0. 
    HDR = VARIABLE locates an area containing a printer page header 
    definition. The area may be generated by invoking the VLP_HDR macro which 
    is described later in this section.  The default is NIL. 
    HMI = VARIABLE is meaningful for opens to DCBs where ORG is CQ.  This 
    vector frames an area generated by VLP_HMI, which contains information 
    used to allocate send and receive circular queues.  The default causes 
    this parameter to be ignored. 
    KEYTYPE = {COORD|FLDID|MSGID} specifies the key type: 
    FLDID - The key refers to a field identifier (i.e., FPT_DCLFLD.ID, a 
    byte-aligned, 2-byte value).  See M$DCLFLD for details. 
    COORD - The key refers to the coordinates of a field (i.e., a 
    byte-aligned, 2-byte structure consisting of the line and column of the 
    field's location). 
    MSGID - This feature is not currently implemented. 
    The default causes this parameter to be ignored. 
    LINES = VALUE-DEC(1-32768) specifies the number of printable lines per 
    page.  The default causes this parameter to be ignored. 
    LOGON = VARIABLE is used when RES equals 'LG' to specify a logon string. 
    The default causes this parameter to be ignored. 
    ORG = OPTION specifies data organization. This parameter describes how the 
    data to be transmitted will be organized. 
    CONSEC   - The I/O will be in a consecutive, record-by-record manner. 
    CQ       - The I/O will be to/from a circular queue. 
    FORM     - The I/O will be to a FORMS type virtual device. 
    SE       - Not yet implemented in the FEP. 
    TERMINAL - The I/O will be to a TERMINAL type virtual device. 
    UR       - The I/O will be to a UNIT RECORD type virtual device. 
    X364     - The I/O will be to an X364 type virtual device. 
    The default causes this parameter to be ignored. 
    RECL = VALUE-DEC(1-32768) specifies the maximum data record length in 
    bytes.  This option is meaningful only for fixed record length formats. 
    Default = 0. 
    RES = VALUE-CHAR(4) specifies a device ('ddnn').  dd is the 2-character 
    device mnemonic which determines the direction the I/O may take.  At 
    present, this may be any of: 
    'HO' - for communication to a host 
    'UC' - for communication to a device 
    'LG' - for logging on a device 
    'NA' - for connecting to NODEADMN 
    The 'nn' field is a stream identifier, and determines which stream the I/O 
    will be on. 
    The default causes this parameter to be ignored. 
    TAB = VARIABLE locates an area containing a horizontal tabulation 
    definition.  This area may be generated via the VLP_TAB macro which is 
    described later in this section.  The default is NIL. 
    WINDOW = VARIABLE specifies a VLP_WINDOW to be used to establish a stream. 
    The default is NIL. 
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
The M$PDS service provides the capability to change the memory access 
protection of a data extent. 
The form of the call for this service is: 
CALL M$PDS (FPT_PDS) [ALTRET (label)]; 
The parameters for this service are as follows: 
    READ = {YES|NO} specifies whether read access is to be permitted or 
    denied.  The default (READ=YES) causes read access to the specified data 
    segment to be permitted. 
    SEGMENT = VARIABLE specifies the location of the area of memory which 
    contains a pointer to the data extent for which the memory access 
    protection is to be set.  The VLP_SEGMENT macro is used to generate this 
    area.  The default is NIL. 
    WRITE = {YES|NO} specifies whether write access is to be permitted or 
    denied.  The default (WRITE=NO) causes write access to the specified data 
    segment to be denied. 
00001
00002
00003
The M$PLATEN service is used to describe the page format on a terminal.  The 
M$GPLATEN service retrieves the current page format. The user can specify or 
retrieve the following: 
o   The maximum number of characters to be written per line on the terminal. 
o   The number of lines to be printed following each automatic heading. 
o   The number of lines to be skipped between the last print line on the page 
    and the top of the next page. 
o   The number of lines to be skipped between the top of a page and the 
    heading line on the page. 
o   The paper width in columns, height in lines, the part of that height that 
    is not to be printed in, and the location of page boundary within the 
    non-printing area may be described. 
The parameters of M$PLATEN are shown in relation to the printer page layout in 
the following diagram. 
-<----- WIDTH ------>- 
|---------------   - - - - - - - - - -   (PERFORATION) 
|     ^           *                    *             | 
|     |           *                    *             | 
|FIRSTLINE        *                    *             | 
|     |           *                    *             | 
|     V                                              | 
|---------------  *TITLE AREA . . . .  *             | 
|     ^           *PRINT LINE . . . .  *             | 
|     |           *PRINT LINE . . . .  *             | 
|     |           *         .          *             | 
|   LENGTH        *         .          *             | 
|     |           *         .          *             | 
|     |           *         .          *             | 
|     V           *PRINT LINE . . . .  *             | 
|---------------                                     | 
|     ^           *                    *             | 
|     |           *                    *             | 
|   LIMBO         *                    *             | 
|     |           *                    *             | 
|     V           *                    *             | 
|---------------   - - - - - - - - - -  (PERFORATION)| 
The form of the calls are as follows: 
CALL M$PLATEN (FPT_PLATEN) [ALTRET (label)]; 
CALL M$GPLATEN (FPT_PLATEN) [ALTRET (label)]; 
Parameters for these services are as follows: 
    DCB = DCBNAME specifies the DCB assigned to a timesharing terminal device. 
    The default is M$UC which is assigned to the user's timesharing terminal. 
    PLATEN = VARIABLE specifies a buffer that contains the platen information. 
    The structure of the buffer is generated by the VLP_PLATEN macro described 
    next in this section. 
    The default is NIL. 
00001
00002
The M$PROMPT service changes the character string that is used to prompt for 
input on the terminal.  The default prompt characters are: 
!    for the command processor domain 
>    for the debugger domain 
*    for USER PROGRAMS 
M$PROMPT changes the prompt for a given stream interfacing with the terminal 
device. 
The form of the call for this service is as follows: 
CALL M$PROMPT (FPT_PROMPT) [ALTRET (label)]; 
The M$GPROMPT service retrieves the character string that is the current 
prompt for input on the terminal. The size of the prompt string is returned in 
the actual record size in the DCB.  The form of the call for this service is 
as follows: 
CALL M$GPROMPT (FPT_PROMPT) [ALTRET (label)]; 
Parameters for the M$PROMPT and M$GPROMPT service are as follows: 
    BIN = {YES|NO} is currently unused. 
    DCB = DCBNAME specifies the DCB assigned to a timesharing terminal device. 
    The default is M$UC which is assigned to the user's timesharing terminal. 
    PROMPT = VARIABLE specifies the character string to be used as the prompt 
    on the terminal.  Subsequent M$READs by this user cause the specified 
    prompt to be displayed on the terminal.  The maximum prompt length is 94 
    characters; this does not include VFC. 
    If PROMPT = NIL, the default prompt is used.  The default is NIL. 
    TRANS = {YES|NO} specifies transparency. If YES is specified, the prompt 
    string is sent literally to the terminal; that is, no translation or 
    interpretation is done.  If NO is specified, the prompt is processed 
    normally as it is sent to the terminal.  The default is NO.  This feature 
    is not currently implemented. 
    VFC = {YES|NO} specifies whether the first character of the prompt string 
    is the VFC. If NO is specified, the VFC default is used.  The VFC default 
    is '@' or extend, which causes the prompt to start in the current 
    character position and the cursor/carriage is positioned to the column 
    immediately following the last character of the prompt.  Refer to the CP-6 
    Programmer Reference Manual for a complete list of VFC codes.  The default 
    is NO. 
00001
00002
00003
00004
00005
The M$RCHAN monitor service allows the user to release an previously acquired 
channel.  If the user does not own the channel, an appropriate error code is 
returned.  If the CONTROLLER bit is set, the user must own each channel on the 
controller; otherwise an error is returned. 
The form of the call is as follows: 
CALL M$RCHAN (FPT_RCHAN) [ALTRET(label)]; 
Parameters for the M$RCHAN service are as follows: 
    CHANNEL = VALUE-DEC(0-?) is the channel to be released.  The default is 0. 
    CONTROLLER = {YES|NO} if set, the entire controller, indicated by CHANNEL, 
    is to be released.  The user must own the entire controller; otherwise an 
    error is returned. 
00001
00002
The M$READ service causes a specified data record to be read into a user 
buffer in memory.  The read operation will obtain data either from a circular 
queue (if the ORG of the DCB is CQ) or from the entity on the other end of the 
path (this could be a device, another LCP-6 user or a host user). 
The user normally provides a buffer that is large enough to contain the 
maximum length record.  If a record exceeds the buffer size, the record is 
truncated and this condition is reported as an error.  If a record is smaller 
than the buffer size, the remainder of the buffer is unchanged from its 
previous contents. 
The service call is of the form: 
CALL M$READ (FPT_READ) [ALTRET(label)]; 
The parameters for the service are as follows: 
    BRKABLE = {YES|NO} specifies that a read is able to take the ALTRETurn 
    when a user event is reported.  This is only effective when the monitor 
    does an internal read.  The default is NO. 
    BUF = VARIABLE locates the buffer into which the users data is to be read. 
    The default is NIL. 
    CG = VARIABLE locates the VLP_CG structure for this read.  The default is 
    NIL. 
    DCB = DCBNAME specifies the name of the DCB.  This parameter is required. 
    EVENT = VALUE-DEC(-32768-32767) specifies, if non-zero, an event number to 
    be reported to this user when this operation completes.  If zero is 
    specified, no event is reported. 
    If EVENT is non-zero, the event procedure established by M$EVENT is given 
    control at completion of the read operation whether an error occurred or 
    not.  If an event control procedure is not established at the time the I/O 
    completes, the user is aborted. 
    The default is 0. 
    KEY = VARIABLE locates an optional area containing one of the following: 
    The field-id of a field 
    The coordinates of a field 
    The message-id of a message 
    The default is NIL. 
    KEYR = {YES|NO} specifies, if YES, that the key of the record read is to 
    be returned to the user in the buffer described by KEY. The default is NO. 
    KEYS = {YES|NO} specifies, if YES, that the user has specified in KEY the 
    key of the field or message that is to be read.  If NO is specified, the 
    next sequential record is read.  For FORM access, specifying the key on 
    M$READ with KEYS=YES indicates the field at which to initially position 
    the cursor.  The default is NO. 
    KEYTYPE = {COORD|FLDID|MSGID} specifies the key type: 
    FLDID - The key refers to a field identifier (i.e., FPT_DCLFLD.ID, a 
    byte-aligned, 2-byte value).  See M$DCLFLD for details. 
    COORD - The key refers to the coordinates of a field (i.e., a 
    byte-aligned, 2-byte structure consisting of the line and column of the 
    field's location). 
    MSGID - This feature is not currently implemented. 
    The default causes this parameter to be ignored. 
    NODAT = {YES|NO} specifies the action the monitor is to take if there is 
    no data available.  If NO, the monitor should wait until data is 
    available; if YES, the monitor should return immediately to the user.  The 
    NODAT option can be used to prevent being suspended waiting for I/O.  The 
    default is NO. 
    READMLT = {YES|NO} specifies, if YES, that the CP-6 virtual-device 
    application protocol data is to be returned directly to the user's buffer 
    without decoding.  This facility is provided to streamline the acceptance 
    of multiple fields through a DCB opened with ORG=FORM.  The user program 
    must be capable of decoding the protocol itself, of course.  Only ARS in 
    DCB is meaningful after M$READ with READMLT=YES, and indicates the total 
    number of bytes of protocol returned.  Only complete fields (DAT VDOs) are 
    returned, so the program should continue to issue M$READs until the last 
    VDO indicates the completion error-code.  The minimum buffer size is 128 
    bytes if READMLT=YES. 
    REREAD = {YES|NO} applies to input originating from a time-sharing 
    terminal.  REREAD=YES specifies that the last input line is to be echoed 
    and set to be the current input line.  The line to be echoed is either the 
    last line typed by a time-sharing user or the line referenced via a call 
    to the M$SINPUT monitor service.  The FPT field name for this parameter is 
    FPT_READ.V.DVBYTE.REREAD.  The default is NO. 
    RRR = {YES|NO} specifies, if YES, that after the data associated with this 
    request has been transmitted, an acknowledgement should be sent.  The 
    default is NO. 
    TRANS = {YES|NO} specifies transparency, if YES, i.e., that data is to be 
    placed in the user buffer without translation.  This option is useful 
    primarily for devices which normally perform translation (for instance, 
    time-sharing terminals). The FPT field name for this parameter is 
    FPT_READ.V.DVBYTE.TRANS. The default is NO. 
    WAIT = {YES|NO} specifies, if NO, that the user program should not wait 
    for I/O completion before continuing execution.  The default is YES. 
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
This service releases a DCB's Read Only Segment space and deletes the DCB from 
the DCB pointer table. Any user DCB may be released, regardless of how it was 
obtained. However, a DCB must be closed before M$RELDCB is called. Once 
released, the DCB and its DCB number are invalid for monitor service calls. 
The service call is of the form: 
CALL M$RELDCB (FPT_RELDCB) [ALTRET (label)]; 
The parameter for the service is as follows: 
    DCB = VALUE-DEC(5-?) specifies the number of the DCB to be released. 
    System DCBs (1-4) may not be released.  Only special processors may 
    release special DCBs (5-9).  Others may be released as desired.  A DCB 
    need not have been defined via a GETDCB in order to be released.  The DCB 
    must be closed in order for it to be released. 
    This parameter is required. 
00001
M$SENV
The M$RETRY service returns control from the user ALTRET code sequence to the 
original monitor service call and retries the service call.  The environment 
for the original monitor service request is assumed to be in the ALTRET frame 
of the TCB.  The M$RETRY service takes the alternate return if there is no 
environment in the ALTRET frame. 
The contents of registers R3 and B3 may be altered via options on the FPT.  If 
no changes are to be made to the environment, the form of the call for this 
service is as follows: 
CALL M$RETRY [ALTRET (label)]; 
If changes are to be made to the environment, the form of the call is as 
follows: 
CALL M$RETRY (FPT_RETRY) [ALTRET (label)]; 
The M$RETRYS service retries a monitor service call.  Its function is the same 
as the M$RETRY service except that the environment of the original monitor 
service call is assumed to be in the top frame of the Exceptional Condition 
Stack.  The M$RETRYS service removes this frame from the stack and restores it 
to the Trap Save Area.  The M$RETRYS service takes the alternate return if the 
Exceptional Condition Stack is empty or if the top frame does not contain the 
environment of a monitor service request. 
If no changes are to be made to the environment prior to retrying the original 
monitor service call, the form of the call for this service is as follows: 
CALL M$RETRYS [ALTRET (label)]; 
If changes are to be made to the environment, the form of the call is as 
follows: 
CALL M$RETRYS (FPT_RETRY) [ALTRET (label)]; 
Note that FPT_RETRY is used for both the M$RETRY and M$RETRYS services.  The 
parameters are as follows: 
    B3$ = PTR specifies the value for base register B3. This is the value that 
    will be used as the address of the FPT.  The default is NIL. 
    R3 = VALUE(0-65535) specifies the value for general register R3. This is 
    the value that will be used for the monitor service request code.  The 
    default is 0. 
00001
00002
The M$RLSFLD service is used to delete a previously defined field within a 
given form.  If no key is specified, all selected fields are released. 
The form of the call is as follows: 
CALL M$RLSFLD (FPT_RLSFLD) [ALTRET (label)]; 
Parameters for the M$RLSFLD service are as follows: 
    DCB = DCBNAME associated with the device.  The DCB must have ORG=FORM and 
    be assigned to a timesharing terminal device. 
    DCB must be specified. 
    KEY = VARIABLE locates an optional area containing a key to identify which 
    field is to be released.  If no key is specified, all selected fields are 
    released. 
    KEYTYPE = {COORD|FLDID|NONE} specifies the keytype to be used on this 
    function.  Specifies the keytype to be used on this function. 
    FLDID refers to a field identifier (i.e., FPT_DCLFLD.V.ID, a byte-aligned 
    2-byte value). 
    COORD refers to the coordinates of a field (i.e., a byte-aligned, 2-byte 
    structure consisting of the line and column of the field's location). 
    RRR = {YES|NO} YES specifies Return Receipt Request.  This option 
    specifies that the function is not complete until it reaches its 
    destination correctly.  Functions to a user terminal are normally 
    considered complete when the data leaves the user buffer.  There is no way 
    to know if the data reached the terminal correctly or if any errors 
    occurred performing the function.  If RRR is set, the function is not 
    considered complete until the data reaches the terminal and any error 
    status has been returned. 
    RRR=YES should be used only for debugging, as it greatly reduces 
    processing speed since a response is required whether an error occurs or 
    not.  Without RRR, any field-oriented error is reported on the next M$READ 
    or other service request with RRR specified.  Only M$READ is capable of 
    returning an error code by ALTRETurning unless the RRR option is used. 
00001
00002
00003
00004
The M$SCREECH service provides an entry to the system recovery procedure for 
user programs.  The SNAP privilege is required to initiate a snapshot dump 
using M$SCREECH.  The SCREECH privilege is required to initiate a full 
recovery. 
The M$SCREECH services does not pass parameters via an FPT.  The single 
parameter passed on a call to M$SCREECH is the screech code which should be 
generated using the VLP_SCODE macro. 
The services to save and restore the environment are typically used in 
conjunction with an ALTRET code sequence.  Using M$SENV/M$RENV allows 
recursion into the ALTRET code sequence and can protect the ALTRET environment 
of the main procedure of a program if any ASYNC procedure also issues monitor 
service requests.  In addition, using the M$SENV service ensures the integrity 
of the ALTRET environment in case of an "insufficient space in TCB stack" 
condition which can occur if an exceptional condition is detected while the 
ALTRET code sequence has control. 
M$SENV 
The M$SENV service allocates a frame in the Exceptional Condition Stack and 
moves the environment to the frame from the TCB ALTRET frame. 
The M$SENV service takes the alternate return if there is no environment in 
the ALTRET frame or if there is insufficient space to store the environment in 
the Exceptional Condition Stack. 
The form of the call for this service is: 
CALL M$SENV [ALTRET (label)]; 
Because no parameters are associated with the monitor service call, there is 
no FPT. 
M$RENV 
The M$RENV service removes the top frame of the exceptional condition stack 
and restores the environment to the ALTRET frame in the TCB. 
The M$RENV service takes the alternate return if the exceptional condition 
stack is empty or if the top frame of the stack is not an ALTRET frame. 
The form of the call for this service is: 
CALL M$RENV [ALTRET (label)]; 
Because no parameters are associated with the monitor service call, there is 
no FPT. 
The M$SINPUT service is used to define a record that is to be processed as if 
it were the last input line entered by the user.  This record is used for any 
editing functions on the next M$READ to the terminal.  If the next M$READ 
specifies REREAD, this line is printed after the prompt is issued.  This 
service allows the user to process a record in a file in the same manner as a 
record entered from the terminal.  See also SINPUTSIZE in M$READ. 
For DCBs open with ORG=SE, this service is used to position the cursor on the 
screen, and supplies the key of the record instead of the data, since the data 
is already known. 
The form of the call is as follows: 
CALL M$SINPUT (FPT_SINPUT) [ALTRET (label)]; 
Parameters for the M$SINPUT service are as follows: 
    BUF = VARIABLE locates a buffer that contains the record to be processed 
    as the last input line. If POSITION=YES was specified, the first character 
    of the buffer specifies where to position the carriage within this line if 
    an M$READ with REREAD is performed.  The value is a character number 
    (1-255).  If zero is specified here, the carriage is positioned at the end 
    of the input. 
    For DCBs open with ORG=SE, the buffer contains the key of the record that 
    is to be edited next, and must be KEYL bytes long.  (KEYL is specified on 
    a call to M$OPEN.)  In addition, the REREADPOS option must be used instead 
    of POSITION. 
    The default is NIL. 
    DCB = DCBNAME specifies the DCB assigned to a timesharing terminal device. 
    The default is M$UC which is assigned to the user's timesharing terminal. 
    POSITION = {YES|NO} YES specifies that the first character of BUF provides 
    carriage positioning (see BUF).  NO specifies that the buffer is entirely 
    text and the carriage is to be positioned after it on a REREAD. 
    The default is NO. 
    REREADPOS = VALUE-DEC(0-?)  specifies where to position the carriage or 
    cursor within the text if an M$READ with REREAD is performed.  The value 
    is a character number in the text.  If zero is specified here, the 
    carriage is positioned at the end of the text.  The POSITION option 
    overrides this one, but provides only positioning in the first 255 bytes 
    of the input text. 
    The default is zero. 
00001
00002
00003
00004
The M$SLCFLD service is used to select a field for future modification by 
other field related services.  All fields on a form can be selected by 
omitting the key on M$SLCFLD.  Or a series of fields can be selected by 
issuing successive calls to M$SLCFLD specifying the key for each field. 
M$SLCFLD adds to the set of currently selected fields, if the previous 
operation was M$SLCFLD.  (If the previous operation was not M$SLCFLD, the 
current M$SLCFLD replaces any previously selected fields with the field(s) 
indicated on this call.) 
Note:  The specification of a key for any of the services for which selected 
fields are required (M$READ, M$WRITE, M$ERASE, M$MDFFLD, M$RLSFLD) is 
considered to be an implicit M$SLCFLD operation, thereby adding to the fields 
selected by any immediately preceding M$SLCFLD operations. 
In the case of M$READ and M$ERASE, only those fields that are both selected 
and otherwise valid for the operation are actually affected.  In the previous 
sentence, "valid" depends on the setting of CNS, PRT, and PRTGRD for the field 
(see VLP_FLDATR) and the setting of CNS and PRT for M$ERASE. 
The form of the call is as follows: 
CALL M$SLCFLD (FPT_SCLFLD) [ALTRET (label)]; 
Parameters for the M$SLCFLD service are as follows: 
    DCB = DCBNAME associated with the device.  The DCB must have ORG=FORM and 
    be assigned to a timesharing terminal device. 
    DCB must be specified. 
    KEY = VARIABLE locates an optional area containing a key to identify which 
    field is to be selected.  If no key is specified, all fields in the given 
    virtual device will become selected. 
    KEYTYPE = {COORD|FLDID|NONE} specifies the keytype to be used on this 
    function.  Specifies the keytype to be used on this function. 
    FLDID refers to a field identifier (i.e., FPT_DCLFLD.V.ID, a byte-aligned 
    2-byte value). 
    COORD refers to the coordinates of a field (i.e., a byte-aligned, 2-byte 
    structure consisting of the line and column of the field's location). 
    RRR = {YES|NO} YES specifies Return Receipt Request.  This option 
    specifies that the function is not complete until it reaches its 
    destination correctly.  Functions to a user terminal are normally 
    considered complete when the data leaves the user buffer.  There is no way 
    to know if the data reached the terminal correctly or if any errors 
    occurred performing the function.  If RRR is set, the function is not 
    considered complete until the data reaches the terminal and any error 
    status has been returned. 
    RRR=YES should be used only for debugging, as it greatly reduces 
    processing speed since a response is required whether an error occurs or 
    not.  Without RRR, any field-oriented error is reported on the next M$READ 
    or other service request with RRR specified.  Only M$READ is capable of 
    returning an error code by ALTRETurning unless the RRR option is used. 
00001
00002
00003
00004
The Job Information Table contains three double words that are used to verify 
a user's privileges prior to performing certain system functions on behalf of 
the user: G$JIT.PRIV.AUTH, G$JIT.PRIV.PRC, and G$JIT.PRIV.ACTIVE. 
The privileges allowed a user program are authorized by SUPER and stored in 
the user authorization record.  At program initiation these privilege bits are 
set in G$JIT.PRIV.AUTH. 
Processors in the :SYS account may have certain of these user privileges 
associated with the processor itself.  These privileges, specified by an 
option of FEPLINK, are stored in the head record of the run unit.  At 
initiation of a processor fetched from the :SYS account, these bits are copied 
to G$JIT.PRIV.PRC. If the run unit is not from :SYS, G$JIT.PRIV.PRC is set to 
zero. 
The privileges effective for the currently running user program or processor 
are set in G$JIT.PRIV.ACTIVE.  When a program is initiated, all privilege bits 
in G$JIT.PRIV.ACTIVE are turned off. 
A user program or system processor may use M$SPRIV to activate the privileges 
for which the user is authorized. 
The privilege bits specified on the PRIV parameter of M$SPRIV are turned on 
only if the corresponding bits are set in G$JIT.PRIV.AUTH or G$JIT.PRIV.PRC. 
The AUTH and PRC options may be used to qualify the operation. 
Only those privileges required by the current process should be specified to 
avoid inadvertent use of unneeded privileges. 
A separate word in the Job Information Table is used to control the access to 
restricted LCP-6 processors and the specific functions performed by these 
processors.  User authorization is established by SUPER and stored in the user 
authorization record.  When a user is initiated these processor function bits 
are set in G$JIT.PPRIV.  When a system processor is put into execution it may 
inspect the privilege bit settings in G$JIT.PPRIV to determine if the user has 
the required system processor privilege prior to performing a specific 
function.  The processor privilege bits in G$JIT.PPRIV may also be used to 
qualify the privileges to be made active. 
All bits specified and allowed are set in G$JIT.PRIV.ACTIVE.  All bits not 
specified are reset.  If not all specified bits are allowed, the bits 
representing privileges granted are set and the alternate return is then taken 
with the error severity code set to 0. 
The form of the call for this service is: 
CALL M$SPRIV (FPT_SPRIV)[ALTRET (label)]; 
The parameters for the M$SPRIV are as follows: 
    AUTH = {YES|NO} specifies, if YES, that the AUTH field from G$JIT.PRIV is 
    used to verify the operation.  Default is YES. 
    PPCHK = {ALL|ANY} specifies, if ALL, that the PRC field from G$JIT.PRIV is 
    to be used to verify the operation only if all the privileges specified 
    via the PPRIV option are contained in G$JIT.PPRIV.  If ANY is specified, 
    then the PRC privileges will be used to verify the operation if any of the 
    privileges specified via PPRIV are contained in G$JIT.PPRIV. 
    Default = ANY.  This option is ignored if the PRC option is NO, or if the 
    PPRIV option is not specified. 
    PPRIV = VARIABLE locates a two word memory location that contains the 
    privilege bits that are to be compared with G$JIT.PPRIV prior to granting 
    the privilege request.  The PPCHK option may be used to specify if all 
    bits in G$JIT.PPRIV must be set, or if a any one set is sufficient to 
    grant the request.  The VLP_PPRIV macro may be used to generate this area. 
    Default=NIL.  If this parameter is not specified, there is no test against 
    G$JIT.PPRIV. 
    PRC = {YES|NO} specifies, if YES, that the PRC field from G$JIT.PRIV is 
    used to verify the operation.  If YES, and the PPRIV option is also 
    specified, then the PRC privileges will be used to verify the operation 
    only if the PPRIV check succeeds. 
    Default is NO. 
    PRIV = VARIABLE locates a two word memory location that contains the 
    privilege bits that are to be set in G$JIT.ACTIVE.  The VLP_PRIV macro may 
    be used to generate this area. 
    Default=NIL. 
00001
00002
00003
00004
00005
The M$STRMATTR service is used to describe physical attributes of the terminal 
in the rare cases that M$PROFILE is inappropriate for this purpose.  The 
procedure call is of the form: 
CALL M$STRMATTR (FPT_TRMATTR) [ALTRET (label)]; 
The monitor M$GTRMATTR service is used to obtain certain physical attributes 
of the terminal.  The procedure call is of the form: 
CALL M$GTRMATTR (FPT_TRMATTR) [ALTRET (label)]; 
The parameters for these services are as follows: 
    DCB = DCBNAME specifies the DCB assigned to a timesharing terminal device. 
    The default is M$UC which is assigned to the user's timesharing terminal. 
    TRMATTR = VARIABLE locates a buffer that contains the terminal attributes. 
    The structure of the buffer is generated by the VLP_TRMATTR macro 
    described in this section. 
    The default is NIL. 
00001
00002
M$GTRMCTL
M$GTRMTAB
The M$SYS service provides a sufficiently privileged user the ability to enter 
privileged mode (in ring 1). 
The MSYS privilege is required to use this service. 
There is no FPT for M$SYS. 
The form of the call for this service is: 
CALL M$SYS [ALTRET (label)]; 
The M$TIME service returns date and time information, obtained from one of 
several possible sources, in several optional formats. The source of the date 
and time may be an input from the calling program or the current system 
elapsed time clock. The output format options include three character string 
formats and two binary formats. 
One of the possible source and output formats is the LCP6 Universal Time Stamp 
(UTS), which is a 32 bit value indicating the elapsed time since a base date 
and time, in units of .133 second.  UTS data is used throughout the LCP6 
system as the standard notation for time. 
The M$TIME service takes the alternate return if the source date is prior to 
January 1, 1978. (Dates prior to that time can occur when processing data from 
other systems and cannot be converted to UTS).  The form of the call for this 
service is as follows: 
CALL M$TIME (FPT_TIME) [ALTRET (label)]; 
The parameters for M$TIME are: 
    DATE = VARIABLE specifies a character string buffer to contain the month, 
    day and year. The size must be that shown in the table for the selected 
    DEST format and must correctly describe the input character string when 
    used with the SOURCE=LOCAL or SOURCE=ANS option.  The default is NIL. 
    DAY = VARIABLE specifies a character string buffer for the day of the week 
    for LOCAL or EXT format or the Julian date for ANS format outputs. The 
    size must be that shown in the table for the selected format. The default 
    is NIL. 
    DEST = OPTION specifies the format of the results of the M$TIME service. 
    The table below illustrates the formats and gives the size, in characters, 
    of the buffer. Results are not returned if a buffer is not specified. If 
    TSTAMP is present, a UTS will be returned in the specified double word 
    buffer if the LOCAL or EXT option is specified.  If the ANS option is 
    specified, a day of week value will be returned in a one word buffer 
    specified by TSTAMP.  The default for DEST is EXT. 
    EXT, ANS, LOCAL   are described in the following table. 
    OPTION  BUFFER  SIZE  FORMAT         EXAMPLE 
    EXT     DATE     10   'MON DD ''YY'  DEC 31 '77 
            TIME     11   'HH:MM:SS.SS'  23:59:59.99 
            DAY       3   'DAY'          SUN 
    LOCAL   DATE      8   'MM/DD/YY'     12/31/77 
            TIME     11   'HH:MM:SS.SS'  23:59:59.99 
            DAY       3   'DAY'          SUN 
    ANS     DATE      6   'YYMMDD'       771231 
            TIME      8   'HHMMSSSS'     23595999 
            DAY       5   'YYDDD'        80366 
    UTS specifies that a UTS is to be computed from the specified input and 
    returned in the TSTAMP buffer. 
    TUN specifies that the timer since midnight, in milliseconds, is to be 
    computed from the specified input and returned in the TSTAMP buffer. 
    SOURCE = OPTION indicates the source of the date and time. The options are 
    as follows: 
    CLOCK    specifies that the current date and time, obtained from the 
             system elapsed time clock, are to be returned. 
    UTS      specifies that the date and time are to be calculated from an 
             input UTS value found in the TSTAMP buffer. 
    LOCAL    specifies that the date and time are to be calculated from input 
             character string data found in the DATE and TIME buffers. Input 
             data must be in the LOCAL format described in the table above. 
             (Note that leading zeros may be omitted from any field and the 
             seconds or hundredths of seconds fields may be omitted, in which 
             case zero is assumed).  The exact length of the string must be 
             reflected in TIME_.BOUND.  Output data will be stored into the 
             DATE and TIME buffers if the EXT, ANS, or LOCAL options are 
             specified for DEST. 
    ANS      specifies that the date and time are to be calculated from input 
             character string data found in the DATE and TIME buffers. Input 
             data must be in the ANS format described in the table above 
             except that TIME is optional and defaults to zero.  Output data 
             will be stored into the DATE and TIME buffers if the EXT, ANS, or 
             LOCAL options are specified for DEST. 
    TUN      specifies that the input for time is a binary value of 
             milliseconds since midnight to be found in the TSTAMP buffer. 
             Date is to be the current date. 
    The default is CLOCK. 
    TIME = VARIABLE specifies a character string buffer to contain the time of 
    day.  The size must be that shown in the table for the selected DEST 
    format and must correctly describe the input character string when used 
    with the SOURCE=LOCAL or SOURCE=ANS option.  The default is NIL. 
    TSTAMP = VARIABLE specifies a two word buffer to contain either a UTS or 
    milliseconds since midnight when LOCAL, EXT, UTS or TUN is specified for 
    DEST.  TSTAMP specifies a one word variable to contain the number of the 
    day of the week when ANS is specified for DEST.  The days of the week are 
    numbered beginning with Monday=1, Tuesday=2, ... Sunday=7. 
00001
00002
00003
00004
00005
00006
The M$TRAP service identifies particular hardware detected traps at which the 
user wants control and provides for the enabling or disabling of the Trace, 
Overflow and Truncation traps. 
A call to M$TRAP specifies the desired trap settings through the New Trap 
Conditions (NTC) parameter.  The call may also request that the settings of 
the Prior Trap Conditions (PTC) be returned to the user. 
The trap condition settings include the trap handler entry address and the 
state of each of the hardware faults (TRAP or ABORT).  The structure of the 
NTC and PTC areas should be generated using the VLP_TRAP_CONDITIONS macro. 
The user may change trap control and specify different trap procedures during 
program execution.  The M$TRAP FPT may specify that both the PTC be returned 
to the user and that the active trap conditions be replaced with those 
specified in the NTC.  The active trap conditions may later be reset to their 
previous values by calling M$TRAP specifying the PTC area that was returned on 
the original call as the NTC parameter.  This allows any procedure within a 
program to handle its own trap conditions and to restore the trap conditions 
to their original states before returning. 
Entry to the trap procedure follows the occurrence of a hardware trap or a 
monitor service request error when no ALTRET is specified. 
The trap frame on the TCB contains the environment as described by the G$EXCFR 
structure.  The user may access the trap frame through the STK$ pointer in the 
TCB; i.e. 
    G$TCB$ -> G$TCB.STK$ -> G$EXCFR 
G$EXCFR.ECC in the trap frame will be set to %G_TRAP#. 
G$EXCFR.TRLR.SUBC in the trap frame will contain the contents of the Indicator 
Register at the time of the trap. 
The form of the call for this service is: 
CALL M$TRAP (FPT_TRAP) [ALTRET (label)]; 
Parameters for the M$TRAP service are as follows: 
    NTC = VARIABLE specifies the area that contains the settings for the 
    desired trap condition settings.  This area should be generated using the 
    VLP_TRAP_CONDITIONS macro.  The default is NIL. 
    PTC = VARIABLE specifies the area where the prior trap conditions are to 
    be returned to the user.  This area should also be generated by the 
    VLP_TRAP_CONDITIONS macro.  The default is NIL. 
00001
00002
This service allows the user to release current unprocessed terminal I/O. 
Input buffers waiting to be read, output buffers waiting to be sent, and 
consecutive BREAKs can be purged. 
The form of the call is as follows: 
CALL M$TRMPRG (FPT_TRMPRG) [ALTRET (label)]; 
Parameters for the M$TRMPRG service are as follows: 
    ABORTREAD = {YES|NO} specifies whether any pending no-wait read is to be 
    terminated with the error code set to E$OPER.  Partially entered input 
    data for such a read is moved into the read buffer. 
    The default is NO. 
    CURSORHERE = {YES|NO} specifies whether the cursor is to be moved to the 
    session issuing this M$TRMPRG request. 
    The default is NO. 
    DCB = DCBNAME specifies the DCB assigned to a timesharing terminal device. 
    The default is M$UC which is assigned to the user's timesharing terminal. 
    PURGEINPUT = {YES|NO} specifies whether type-ahead data accumulated in the 
    input buffers is to be purged. 
    The default is NO. 
    PURGEOUTPUT = {YES|NO} specifies whether data remaining in the output 
    buffers is to be purged. 
    The default is NO. 
    RESETBREAK = {YES|NO} specifies whether the current terminal break count 
    is to be reset.  RESETBREAK=YES can be used to reset the break count to 
    avoid having a CONTROL Y simulated because of four consecutive breaks. 
    The default is NO. 
00001
00002
00003
00004
00005
00006
The M$TRTN service returns control to the program from an exceptional 
condition procedure. The service removes the top frame of the Exceptional 
Condition Stack and restores that environment to the Trap Save Area.  The user 
may specify changes to be made to the environment, including the registers and 
the Program Counter.  The M$TRTN service transfers control to the user program 
at the statement following the point of interruption or to the location 
specified by the P$$ option. 
Note that if the M$TRTN service request is issued when the top frame on the 
Exceptional Condition Stack is an exit control frame, and that frame does not 
indicate a nested exit control entry, the program is removed from the "exit" 
status. 
The M$TRTN service takes the alternate return if there is no environment in 
the Exceptional Condition Stack. 
If there are no changes to the environment, the form of the call for the 
M$TRTN service is as follows: 
CALL M$TRTN [ALTRET (label)]; 
If there are changes to be made to the environment, the form of the call for 
this service is as follows: 
CALL M$TRTN (FPT_TRTN) [ALTRET (label)]; 
In this case, the parameters for the M$TRTN service are as follows: 
    P$$ = EPTR specifies the procedure to be entered following the call to 
    M$TRTN.  A value of NIL indicates that the Program Counter is not to be 
    changed.  Default = NIL. 
    REGS = VARIABLE locates a 34-word area that contains the values to be used 
    to replace the base registers, the general registers, the mode control 
    registers, etc.  The structure of this area should be generated using the 
    VLP_REGISTERS macro.  Default = NIL. 
00001
00002
The M$UNSHARE service provides a means for the user to obtain an unshared copy 
of the currently executing run unit and/or run time library. 
The form of the call for this service is: 
CALL M$UNSHARE(FPT_UNSHARE) [ALTRET(label)]; 
The parameters for this service are as follows: 
    PROG = {YES|NO} specifies, if YES, that the currently running program is 
    to be made unshared.  Default is NO. 
    SLIB = {YES|NO} specifies, if YES, that the currently associated run time 
    library is to be made unshared.  Default is NO. 
00001
00002
The M$WAIT service causes suspension of background program execution for a 
specified period of real time.  Program execution is resumed at the next 
statement following the M$WAIT request.  Optionally, the suspension period of 
a suspended program may be adjusted by an interrupt level program associated 
with the suspended program.  A suspended program is resumed before its 
suspension time has expired if an asynchronous event is reported (see 
M$EVENT). The amount of unexpired time may be returned to the user. 
The form of the call for this service is: 
CALL M$WAIT (FPT_WAIT) [ALTRET(label)]; 
The parameters for this service are as follows: 
    MODE = OPTION specifies if the calling program is to be suspended, 
    MODE=SUSP, or if the suspension time of the currently suspended background 
    level program of this user is to be adjusted, MODE=ADJUST.  The M$WAIT 
    service will return immediately if OPTION is incorrect for the mode of the 
    calling program. 
    The default is SUSP. 
    UETIME = VARIABLE locates a UBIN(16) area into which the unexpired time is 
    to be stored if the suspension is terminated prematurely.  If UETIME is 
    NIL, the time is not returned. If the suspension is not terminated 
    prematurely, the unexpired time will be zero.  When MODE=ADJUST, the 
    unexpired time will be zero unless the user is not suspended, in which 
    case it will be the requested adjust interval. 
    The value returned in UETIME is in UTS units, regardless of UTYPE.  If UTS 
    was specified, UETIME is the interval from the current time to the 
    specified UTS time. 
    The default is NIL. 
    UNITS = VARIABLE locates an area containing the number of units of time 
    the program is to be suspended or the suspension time is to be adjusted. 
    VARIABLE is UBIN(16) if UTYPE=SEC or UTYPE=TICS and UBIN(32) if UTYPE=UTS. 
    The default is NIL. 
    UTYPE = OPTION specifies the kind of time in which UNITS is expressed. 
    Valid options are: 
           TICS   FEP UTS units (.133 seconds) 
           SEC    Seconds. 
           UTS    A specific wakeup date and time in 
                  LCP-6 UTS units. 
    When TICS or SEC is specified, UNITS is treated modulo 24 hours.  When UTS 
    is specified, UNITS gives the date and time the user is to be awakened to 
    the nearest .133 second.  The default is SEC. 
00001
00002
00003
00004
The M$WRITE service causes a data record stored in a buffer in memory to be 
written. The M$WRITE service is used for all types of devices for which output 
is appropriate, as well as to send messages between communicating entities 
such as two LCP-6 users or an LCP-6 user and a host user. 
M$WRITE provides options comparable to the options available on the M$READ 
service. In addition, M$WRITE can accommodate format options particular to 
output: 
 o The system normally removes trailing blanks from unit record and TERMINAL 
   record output.  BP allows the user to retain trailing blanks in such 
   output. 
 o VFC specifies where the vertical format control information is to be 
   obtained for this write:  in the first byte of the buffer or from the DCB. 
If M$WRITE specifies a closed DCB, the monitor attempts the M$OPEN service. If 
the open procedure is successful, the write is then performed. 
If an error occurs, the alternate return is taken with an error code reported. 
The error code reflects the first bit set in the DCB TYC field, if the write 
operation was actually started. The user may perform further tests on the DCB 
TYC field in the alternate return code sequence.  The user may also specify 
EVENT to cause a procedure to be called when the I/O completes. 
The service call is of the form: 
CALL M$WRITE (FPT_WRITE) [ALTRET (label)]; 
The parameters for the services are as follows: 
    BP = {YES|NO} specifies blank preservation.  YES specifies that trailing 
    blanks are not to be removed.  NO specifies that blank stripping is to be 
    performed.  The default is NO. 
    BUF = VARIABLE locates the buffer from which the data is to be written. 
    The default is NIL. 
    CG = VARIABLE locates the VLP_CG structure for this write.  The default is 
    NIL. 
    DCB = DCBNAME specifies the name of the DCB.  This parameter is required. 
    EOM = {YES|NO} specifies, if YES, that EOMCHAR contains the activation 
    character to be reported with the data being transmitted with this 
    M$WRITE.  EOM is ignored for DCBs open to the terminal (RES=UCnn).  EOM 
    overrides VFC if both are specified, but the first buffer character is 
    then ignored. 
    The default is NO. 
    EOMCHAR = VALUE-CHAR(1) specifies, if EOM is YES, and the DCB is open with 
    RES other than UCnn, the character to be reported as EOM_CHAR along with 
    the data for this M$WRITE.  If EOM is NO, %EOM_EOR is reported instead. 
    The default is blank. 
    EVENT = VALUE-DEC(-32768-32767) specifies, if non-zero, that an event 
    number to be reported to this user when this operation completes.  If zero 
    is specified, no event is reported. 
    If EVENT is non-zero, the event procedure established by M$EVENT is given 
    control at completion of this operation whether an error occurred or not. 
    If an event control procedure is not established at the time the I/O 
    completes, the user is aborted. 
    The default is 0. 
    KEY = VARIABLE locates an optional area containing one of the following: 
    The field-id of a field 
    The coordinates of a field 
    The message-id of a message 
    The default is NIL. 
    KEYTYPE = {COORD|FLDID|MSGID} specifies the key type: 
    FLDID - The key refers to a field identifier (i.e., FPT_DCLFLD.ID, a 
    byte-aligned, 2-byte value).  See M$DCLFLD for details. 
    COORD - The key refers to the coordinates of a field (i.e., a 
    byte-aligned, 2-byte structure consisting of the line and column of the 
    field's location). 
    MSGID - This feature is not currently implemented. 
    The default causes this parameter to be ignored. 
    NODAT = {YES|NO} if YES, specifies that the alternate return is to be 
    taken if the distant end point has not done a read.  The default is NO. 
    RRR = {YES|NO} specifies, if YES, that after the data associated with this 
    request has been transmitted, an acknowledgement should be sent.  The 
    default is NO. 
    TRANS = {YES|NO} specifies transparency, if YES, i.e., that data is to be 
    written without translation.  This option is useful primarily for devices 
    which normally perform translation (for instance, time-sharing terminals). 
    The FPT field name for this parameter is FPT_WRITE.V.DVBYTE.TRANS. The 
    default is NO. 
    VFC = {YES|NO} specifies, if YES, that the first character of the record 
    is to be interpreted as a vertical format character.  Refer to the CP-6 
    Programmer Reference Manual for a list of VFC codes in the appendix 
    'Device Format Control Characters'.  The default is NO. 
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
The M$WRSYSLOG service provides the LCP6 user with the ability to place an 
entry in one of the system logs.  SYSLOG privilege is needed to use this 
service. 
The form of the call for this service is: 
CALL M$WRSYSLOG (FPT_WRSYSLOG) [ALTRET(label)] 
Parameters for this service are as follows: 
    BUF = VARIABLE locates a buffer containing additional information which is 
    to accompany the system log entry. 
    FCG, MID, MON, SEV, and ERR - specifies parameters for a VLP_ERRCODE which 
    is contained in the FPT, and is used for entries in the ERRLOG file to 
    associate a message from :ERRMSG.:SYS with the entry. 
    FILENUM = OPTION specifies the file to which the entry is to be written. 
    Either ERRLOG or ACCOUNTING may be specified.  Other files have the name 
    ELFnn, where nn is the file number and the nn value should be specified 
    for FILENUM. 
    The default is ERRLOG. 
    TERMINAL_ID identifies any device that should be associated with the entry 
    that is being logged.  This area in the FPT is a B$TERMINAL_ID structure 
    that can be supplied only at runtime. 
    VALUES = ARRAY(0:3) UBIN specifies four data words which may be used with 
    or instead of BUF for small amounts of data.  This data can be supplied 
    only at runtime. 
00001
00002
00003
00004
00005
The M$WRTMLT service is used for two purposes:  to write blocks of data to the 
terminal if ORG=FORM, or to scan the handler circular queue if ORG=CQ.  This 
service is currently reserved for use by the system only. 
The format of the call for this service is: 
CALL M$WRTMLT (FPT_WRTMLT) [ALTRET(label)]; 
Parameters for the M$WRTMLT service are as follows: 
    BUF = VARIABLE locates the buffer from which the data is to be written. 
    The default is NIL. 
    DCB = DCBNAME specifies the name of the DCB.  This parameter is required. 
00001
00002
EXIT CONDITIONS 
Conditions causing a program exit are listed below.  The conditions are 
classified by severity of impact as follows: 
  Class    Condition 
___________________________________________________________ 
     1     Normal exit at M$EXIT 
     1     Abnormal exit at M$ERR or M$XXX 
     1     Transfer of control to another load module (M$LDTRC) 
     1     Machine trap and no user trap control requested 
     1     Monitor service error not processed by ALTRET code 
           sequence or M$TRAP (MCL) procedure 
     1     Exceptional condition occurs but procedure cannot 
           be entered because the stack is full 
     1     Operator errored the user 
     2     Resources limit exceeded 
     3     Operator aborted the user 
     3     Line disconnect 
--------------------------------------------------------------- 
The M$XCON service is used to establish the entry address of the users 
procedure that is to receive control should any of these conditions occur. 
When the exit procedure takes control, the program is in "exit" status; a flag 
in the ECCB is set to reflect "exit control in progress".  Executing the 
M$XCON service within an exit procedure removes the program from "exit" 
status. 
The exit control frame on the TCB contains the environment as described by the 
G$EXCFR structure.  The user may access the exit control frame through the 
STK$ pointer in the TCB; i.e. 
    G$TCB$ -> G$TCB.STK$ -> G$EXCFR 
G$EXCFR.ECC in the exit control frame will be set to %G_XCON#. 
G$EXCFR.TRLR.RNST in the exit control frame will contain the value of 
G$JIT.RNST as it existed at the time of the exit condition. 
G$EXCFR.TRLR.ERR will contain the error code. 
A time limit is imposed if a class 2 or class 3 exit condition exists. 
If there is insufficient room on the Exceptional Condition stack for the 
exceptional condition environment, as indicated by the the FLAGS.TCBFULL bit 
set in the ECCB, the exit control environment will be in the ALTRET frame with 
the ECC set to indicate that the TCB is full (%G_TCBFULL#).  The format of the 
frame is the same as the exit control frame that is placed on the stack with 
the exception of the value of the ECC.  The user should always inspect the 
ECCB upon entry to the exit control procedure to determine if this condition 
exists. When this condition occurs, the exit control information must be 
accessed via the ALTRET frame pointer in the TCB. For example, on entry to an 
exit control procedure: 
     IF G$ECCB$->G$ECCB.FLAGS.TCBFULL 
     THEN MYPTR$ = G$TCB$->G$TCB.ALT$; 
     ELSE MYPTR$ = G$TCB$->G$TCB.STK$; 
The M$XCON service may also be used to determine the address of any previously 
set exit control procedure.  This previously set procedure address may then 
then be used on a subsequent call to M$XCON to restore the exit control 
procedure address to its former value. 
Using the M$XCON service with the exit control procedure address set NIL 
causes the request for exit control to be reset.  If an exit condition occurs 
when exit control has been reset, the program is aborted. 
To resume normal execution of a program after receiving exit control, the user 
can call the M$TRTN service.  This service removes the exit control frame from 
the TCB stack and removes the program from the "exit" status. 
Please note that a program is removed from the "exit" status any time an exit 
control frame is removed from the Exceptional Condition Stack and the frame 
does not indicate a nested exit control entry; when G$EXCFR.TRLR.XCON.XCONP is 
reset.  This may be as a result of an M$CLRSTK service request or an M$TRTN 
service request. 
The user can also issue the M$XCON service within the exit procedure to remove 
the program from the "exit" status.  The user may call this service with a 
previously acquired PXCON parameter specified as the exit control entry 
address to reestablish a previous exit control entry.  If this is followed by 
an M$EXIT, M$ERR or M$XXX, that exit control entry will then be entered. 
To unconditionally exit the current program, the user can call the M$EXIT, 
M$ERR, or M$XXX service. 
The form of the call for this service is: 
CALL M$XCON (FPT_XCON) [ALTRET (label)]; 
Parameters for the M$XCON service are as follows: 
    NXCON = VARIABLE locates a 2-word area that contains an EPTR to the exit 
    procedure that is to be entered upon exit of the current program whether 
    normal or abnormal.  If the EPTR is ENTADDR(NIL) the request for exit 
    control is reset.  Default = NIL. 
    PXCON = VARIABLE locates a 2-word area where an EPTR to the previously set 
    exit procedure address is to be returned.  Default = NIL. 
    XCON$ = {ENTRY|NIL} specifies the procedure that is to be entered upon 
    exit of the current program whether normal or abnormal.  Specifying NIL 
    will cause the request for exit control to be reset.  Default = NIL. 
    If both NXCON and XCON$ are specified, the XCON$ parameter is ignored. 
00001
00002
00003
The M$XXX service provides for abnormal termination of the current program. 
No FPT is required by M$XXX but one may be specified to provide for an 
explicit setting of the Step Condition Code or error code if desired.  If no 
FPT is specified, the Step Condition Code is set to 6 and the error code is 
set to %E$XXXPMME. 
The form of the call for this service is: 
CALL M$XXX; 
or 
CALL M$XXX (FPT_XXX) [ALTRET (label)]; 
When the FPT is specified, the parameters are as follows: 
    ERRCODE = VARIABLE specifies the 2 word area in memory containing the 
    error code to be returned to the process that had initiated the program. 
    The VLP_ERRCODE macro should be used to generate a structure for the error 
    code.  The default is NIL. 
    STEPCC = {G_EXIT#|G_ERR#|G_ABORT#|VALUE-DEC(0-255)} specifies how the Step 
    Condition Code is to be set:  G_EXIT#=0, G_ERR#=4, or G_ABORT#=6.  The 
    parameter may also be specified as a decimal value (0-255).  The default 
    is G_ABORT#. 
00001
00002
Monitor calls will take the following form: 
     LDR,3 = NVECTORS*1024+MCL_CODE 
    [LDB,3   FPT_PTR]       Need not be present 
    [LAB,3   FPT]           if NVECTORS=0. 
     MCL 
     DC      altret,PREL    Contains 0 if no ALTRET 
where: 
NVECTORS    specifies the number of contiguous vectors in the FPT, The first 
vector will, in general, locate the V (value) area of the FPT. 
MCL_CODE    specifies which monitor service is being invoked. 
FPT_PTR    locates the first vector. 
MCL    is the LCP-6 monitor call instruction. 
DC altret,PREL    is the offset from the MCL itself to the altret label. 
Initialization parameters are specified in the format "keyword = type" at 
macro invocation. 
where "type" is as follows: 
VARIABLE is always framed by a vector in the FPT.  A variable can be created 
    by invoking a macro in the system macro library or can be declared by the 
    user. 
    VARIABLE may also specify the word NIL or ERASE.  NIL implies that no 
    value is being specified, nothing is to be done, and any previously 
    specified value to remain unchanged.  ERASE implies that any current or 
    previous value is to be erased, and generally implies that the default is 
    to be reinstated. 
    The default for VARIABLE is NIL, unless otherwise stated. 
PTR locates an area in user memory. NIL may be specified to indicate no value 
    is being supplied.  The default for PTR is NIL unless otherwise specified. 
ENTRY is a procedure name, usually designated as an ASYNC procedure, to which 
    control may be transferred.  ENTRY is always defined as a PL-6 entry 
    point. 
    The default for ENTRY is NIL, unless otherwise stated. 
DCB is the name of a PL-6 variable with the storage class attribute DCB.  It 
    can be created by invoking the M$DCB macro or by declaring the DCB storage 
    class attribute. 
    When the DCB parameter is listed for a service it is a required parameter 
    unless otherwise stated. 
OPTION represents one of several possible or parameter assignments and are 
    listed in braces separated by the | symbol.  For example: 
    option_name = {YES|NO} 
VALUE-DEC(range) assigns a decimal value within the specified range.  Zero is 
    often defined as the default. 
VALUE-CHAR(n) assigns a character value of the length n characters.  Blank is 
    often defined as the default. 
VALUE-BIT(n) assigns a hexadecimal value which is n bits in length.  Zero is 
    often defined as the default. 
There are other library routines contained in the module X6A$CSEQ which deal 
with certain complex operations involving bits, characters, and double word 
arithmetic.  All are invoked by LNJ,B5 and return via B6 for exception 
condition (if any). 
1.  Double Word Operations. 
     X6D_CID - Compare R67 to double word located by 
               B1.  Set G,L,U indicators so signed or 
               unsigned tests can follow. 
     X6D_DID - Divides R67 by double word located by 
               B1.  Quotient returned in R67. 
     X6D_MID - Multiplies R67 by double word located by 
               B1.  Product returned in R67. 
2.  Byte String Operations Too Long For CIP. 
    The following operations assume the operands are specified as 
    follows: 
     First Operand  - Source for move and translate, left operand 
                      for compare, string being searched for search. 
                B2  - base address 
                R2  - byte offset from B1 
                R6  - length in bytes 
     Second Operand - Destination for move and translate, right operand 
                      for compare, string being searched for search. 
                B3  - base address 
                R3  - byte offset 
                R7  - length 
     Third Operand  - Translate table for translate, 6 word temporary area 
                      for search. 
                B1  - base address 
                R1  - byte offset 
           X6C_ACM  - Compare with blank fill.  Set 
                      CPU G&L indicators so CPU 
                      unsigned branches may follow. 
          X6C_ACMZ  - same except zero fill. 
           X6C_ALR  - move with blank fill. 
          X6C_ALRZ  - move with zero fill. 
           X6C_MAT  - move and translate. Exception if source 
                      string is longer than destination. 
          X6C_SRCH  - search string for another. Exception if string 
                      not found. If found, index returned in R6. 
3.  Bit String Operations 
    The following operations assume the same operand specification 
    as for character strings except that offsets and lengths are 
    in bits. 
          X6B_BCM     Compare with '0'B fill. 
          X6B_BLR     Move with '0'B fill. 
Monitor service parameters are shown in the format "keyword = type".  For each 
monitor service, keywords are listed in alphabetical order, unless there is a 
special reason to present them in a functional sequence. 
FPTN and STCLASS are not repeated for each FPT, VLP, VLR and user context 
structure, but these keywords may be used. 
The following list describes, in order of precedence, the source of parameters 
passed to a monitor service in the FPT: 
1.  Default parameters from FPT or VLP macro definitions. 
2.  Initialization parameters supplied by the user via FPT or VLP macro 
    invocation. 
3.  Run time modification performed between monitor service calls. 
The receiving sequence for all PL-6 subroutines will be one of the following 
forms depending upon the form of storage used and the type of procedure. 
Note that the receiving sequences documented here are those that will be used 
by PL-6 programs.  Other languages, while using the same basic calling 
sequence, may alter the receiving sequences as required by the language. 
  Procedure Type      Using AUTO     Using STATIC (NOAUTO) 
MAIN                X6A_MAUTO      X6A_MSTATIC 
ASYNC               X6A_AAUTO      X6A_ASTATIC 
Callable -          X6A_AUTO_0     X6A_STATIC_0 
0 Args Expected 
Callable -          X6A_AUTO_1     X6A_STATIC_1 
1 Arg Expected 
Callable -          X6A_AUTO_2     X6A_STATIC_2 
2 Args Expected 
Callable -          X6A_AUTO_3     X6A_STATIC_3 
3 Args Expected 
Callable -          X6A_AUTO_N     X6A_STATIC_N 
N Args Expected 
Each of the AUTO procedure entry routines listed above is entered upon 
procedure activation with the following sequence: 
     LNJ,B5   X6A_xxx 
     DC       Frameinfo 
     DC       Numargs 
The following is the format for the setup for a NOAUTO procedure, except those 
requiring X6A_STATIC_N: 
     LNJ,B5   X6A_xxx 
     doubleword Frameinfo 
The following is the format for the setup using X6A_STATIC_N: 
     LNJ,B5   X6A_STATIC_N 
     doubleword Frameinfo 
     X   B    X+2,SPREL 
     DC       Numargs 
where: 
Frameinfo    defines the procedure activation frame.  If the routine is an 
AUTO routine, Frameinfo is the required size of the AUTO frame and is a 1 word 
value.  If the routine is a NOAUTO routine, Frameinfo is the address in the 
instruction segment where return address and parameters are to be stored and 
is a doubleword (PTR). 
Numargs    is the number of arguments expected by the routine. 
If fewer arguments than expected are passed, ADDR(NIL) will be supplied for 
the unspecified arguments. 
All of the routines assume that Base Register 7 locates the current external 
automatic frame and the the T register controls all of auto storage.  Thus all 
programs should leave B7 undisturbed. 
    The following register usages will be adhered to in LCP-6: 
   Register   Usage                        Saved on Calls 
 B7         Automatic Storage Pointer    Updated as necessary. 
                                         Saved on Monitor 
                                         calls.  Never modified 
                                         elsewhere. 
 B6*        Link register to             Never 
            subroutines 
 B5*        Link to intimate operators   Never 
            (e.g., allocate AUTO,etc.) 
 B4         Locates descriptor list      Never 
            described below.  Also 
            used as link register for 
            transfers to ALTRET code. 
 B3         Locates pointer list         Saved on Monitor 
            described below.  Also       Calls. 
            locates FPT (vector list) 
            for Monitor Calls. 
 B2,B1      Available                    Never 
 R7-R4      Available                    Never 
 R3         Monitor Service Code         Saved on Monitor 
                                         Calls. 
 R2,R1      Available                    Never 
 T          Used to control allocation   Never modified 
            of automatic storage.        except by auto 
                                         management 
                                         routines. 
Note that both LNJ,B6 and LNJ,B5 instructions are expected to be 
followed by non-executable data words in all cases.  In the case of 
LNJ,B6, the P-relative altret address or a value of 1 follows (one 
word).  In the case of LNJ,B5, the contents depend on the function 
but two words always follow. 
The following table defines the exit sequences from various types of 
procedures: 
  Procedure Type     Using AUTO           Using STATIC (NOAUTO) 
MAIN               LNJ,B4 X6A_MARET     LNJ,B4 X6A_MSRET 
RETURN 
ASYNC              LNJ,B4 X6A_AARET     LNJ,B4 X6A_ASRET 
RETURN 
Callable           LNJ,B4 X6A_ARET      LDB,B6 frame 
RETURN                                  LNJ,B4 1,B6 
Function           LNJ,B4 X6A_FARET     LDB,B6 frame 
RETURN                                  LNJ,B4 1,B6 
MAIN               LNJ,B4 X6A_MAALT     LNJ,B4 X6A_MSALT 
ALTRETURN 
ASYNC              LNJ,B4 X6A_AAALT     LNJ,B4 X6A_ASALT 
ALTRETURN 
Callable           LNJ,B4 X6A_AALT      LDB,B6 frame 
ALTRETURN                               LDR,R1 ,B6 
                                        LNJ,B4 ,B6,R1 
                        /*Declares the FPRG program name and declares 
                          the program as a main program. 
                        */ 
FPRG_TEST:   PROC MAIN; 
                        /*Includes the CP-6 FEP system macro library. 
                        */ 
%INCLUDE  LCP_6; 
                        /*Includes the FEP system macros that access 
                          the user Job Information Table maintained 
                          in the FEP. 
                        */ 
%INCLUDE  G_JIT_M; 
                        /*Creates the READ structure for reading 
                          from the host program, and specifies the 
                          buffer space to be used for the reads.  (The 
                          memory for the buffer is defined via a DCL.) 
                        */ 
%FPT_READ (FPTN=READ_HOST,BUF=HOST_NUMBER,DCB=M$LM); 
                        /*Creates the WRITE structure for writing to a 
                          buffer to be read by the host.  Note that the 
                          same buffer space and DCB are used in the 
                          READ and WRITE FPTs. 
                        */ 
%FPT_WRITE (FPTN=WRITE_HOST,BUF=HOST_NUMBER,DCB=M$LM); 
                        /*Creates a structure for writing directly to 
                          the window defined for the UC02 stream.  This 
                          structure will write to the second window (the 
                          first 11 lines) on the terminal screen. 
                        */ 
%FPT_WRITE (FPTN=WRITE_TERMINAL,DCB=M$ME,BUF=TERMINAL_BUFFER); 
                        /*Since the default FEP DCB (M$LM) and the 
                          default host DCB (M$ME) are the only DCBs 
                          used in this FEP program, no OPEN FPT is 
                          necessary. 
                        */ 
DCL  M$LM DCB; 
DCL  M$ME DCB; 
                        /*Invokes the macros that access the FEP user 
                          Job Information Table. 
                        */ 
%G$JIT; 
                        /*Specifies that the FEP system pointer available 
                          through the INCLUDE G_JIT_M is to be used. 
                        */ 
DCL  G$JIT$  PTR  SYMREF; 
                        /*Declares the buffer to be used to receive 
                          data from the host.  (The ninth bit of data 
                          is dropped coming across the line.)  Using 
                          STATIC in these buffer declarations eliminates 
                          the need for assignments in the FPTs. 
                        */ 
DCL  HOST_NUMBER UBIN(32) STATIC; 
                        /*Declares the buffer for receiving data that 
                          is to be sent to the UC02 window on the 
                          terminal. 
                        */ 
DCL  1 TERMINAL_BUFFER   STATIC, 
                        /*Defines the characters to be displayed in 
                          the UC02 window, and defines two variables 
                          that will receive translated (from binary to 
                          ASCII) values for two numbers: the user's 
                          host system id and the FPRG sysid. 
                        */ 
       2 * CHAR (11) INIT ('FROM HOST "'), 
       2 HOST_CHAR CHAR(10), 
       2 * CHAR(19) INIT('"     G$JIT.SYSID ='), 
       2 FEP_CHAR CHAR(10); 
                        /*Receives the system id from the host.  This 
                          read is synchronized with the M$WRITE to 
                          UC02_WRITE in the host program and places 
                          the data in HOST_NUMBER. 
                       */ 
CALL  M$READ (READ_HOST) ALTRET (ERR); 
                        /*Converts the host system id from a BINary 
                          integer to a CHARacter string of all digit 
                          characters and places the results in 
                          TERMINAL_BUFFER.HOST_CHAR. 
                        */ 
CALL BINCHAR (TERMINAL_BUFFER.HOST_CHAR,HOST_NUMBER); 
                        /*Retrieves the FEP user system id from the 
                          G$JIT, converts it to a CHARacter string, and 
                          places it in TERMINAL BUFFER.FEP_CHAR. 
                          */ 
CALL BINCHAR (TERMINAL_BUFFER.FEP_CHAR, G$JIT$->G$JIT.SYSID); 
                        /*Sends the data in the buffer to the terminal 
                          by performing a write to the M$ME DCB. 
                        */ 
CALL  M$WRITE (WRITE_TERMINAL) ALTRET (ERR); 
                        /*Assigns the FPRG system id to HOST_NUMBER. 
                        */ 
HOST_NUMBER = G$JIT$->G$JIT.SYSID; 
                        /*Sends the FPRG system id back to the host, 
                          using the same buffer the host used to send 
                          down the host system id.  This write is 
                          synchronized with the M$READ in the host 
                          program. 
                        */ 
CALL  M$WRITE (WRITE_HOST) ALTRET (ERR); 
                        /*Terminates normal execution. 
                        */ 
RETURN; 
                        /*Specifies the monitor service to use for 
                          error conditions occurring when monitor 
                          service calls are executed. 
                        */ 
ERR: 
   CALL M$XXX; 
                        /*Terminates the program. 
                        */ 
END  FPRG_TEST; 
The source FPRG is compiled and linked with the following commands: 
  !PL6 FPRG_SI6 OVER *FPRG_OU,FPRG_LS(SC,FEP,LO) 
  !FEPLINK *FPRG_OU OVER FPRG_TEST 
                        /*Declares the program name and declares 
                          the program as a main program. 
                        */ 
HOST_TEST:  PROC MAIN; 
                        /*Includes the CP-6 system macro library. 
                        */ 
%INCLUDE CP_6; 
                        /*Includes the system macros that access 
                          the user Job Information Table. 
                        */ 
%INCLUDE B$JIT; 
                        /*Creates an FPT structure that will be 
                          used when the M$LDEV monitor service 
                          is called.  The following structure 
                          parameters are specified: 
                            o  the name by which the LDEV FPT will 
                               be accessed. 
                            o  the name of the stream that will be 
                               assigned to the second window on the 
                               host terminal. 
                            o  the name of the VLP structure that 
                               defines the second window on the host 
                               terminal. 
                        */ 
%FPT_LDEV(FPTN=LDEV_UC02,STREAMNAME='UC02',WINDOW=OUR_WINDOW); 
                        /*Defines the second window on the host 
                          terminal screen.  The second window will 
                          occupy the first 11 lines of the host 
                          terminal screen. 
                        */ 
%VLP_WINDOW (FPTN=OUR_WINDOW,LENGTH=11); 
                        /*Creates an OPEN FPT structure that creates 
                          the communication link between the host 
                          program and the FPRG.  The structure specifies: 
                            o  the name of the structure; 
                            o  the name of the DCB; 
                            o  the communication path: specifying ORG=FPRG 
                               and RES='UC02' establishes that the 
                               named DCB will communicate with an FPRG 
                               through stream UC02. 
                            o  FUN=CREATE is currently required. 
                            o  names the VLP structure containing 
                               the name of the FPRG run unit that 
                               is to be placed in the window stream. 
                        */ 
%FPT_OPEN (FPTN=UC02_OPEN,DCB=F$UC02,ORG=FPRG,RES='UC02', 
           FUN=CREATE,FPRG=FPRG_TEST); 
                        /*Names the structure and specifies the name 
                          of the file that contains the FPRG run unit. 
                        */ 
%VLP_FPRG (FPTN=FPRG_TEST,NAME='FPRG_TEST'); 
                        /*Creates the WRITE structure for writing to 
                          the FPRG via stream UC02 using the same DCB 
                          specified in the OPEN FPT, and specifies 
                          the buffer space to be used for the writes. 
                          (The memory for the buffer is declared via 
                          a DCL.) 
                        */ 
%FPT_WRITE  (FPTN=UC02_WRITE,DCB=F$UC02,BUF=UC02_BUF2); 
                        /*Creates the READ structure for reading from 
                          the FPRG through stream UC02.  Note that the 
                          READ and WRITE structures use the same 
                          buffer.  Note, too, that the DCBs specified 
                          in both the READ and WRITE FPTs must be the 
                          same DCB specified in the associated OPEN 
                          FPT. 
                        */ 
%FPT_READ (FPTN=UC02_READ,DCB=F$UC02,BUF=UC02_BUF2); 
                        /*Creates the WRITE structure for writing 
                          directly to the terminal in the M$UC 
                          (i.e., the original or first) window, and 
                          specifies the buffer space to be used for 
                          the writes.  (The memory for the buffer 
                          is defined via a DCL.) 
                        */ 
%FPT_WRITE (FPTN=UC_WRITE,DCB=M$UC,BUF=UC_BUFFER); 
                        /*Specifies that the system pointer (available 
                          through the INCLUDE B$JIT) is to be used. 
                        */ 
DCL B$JIT$  PTR  SYMREF; 
                        /*Declares the buffer for writing to the original 
                          (M$UC) window on the terminal.  Using 
                          STATIC in these buffer declarations eliminates 
                          the need for assignments in the FPTs. 
                        */ 
DCL  1 UC_BUFFER   STATIC, 
                        /*Defines the characters to be displayed in 
                          the M$UC window, and defines two variables 
                          that will receive translated (from binary 
                          to ASCII) values for two numbers:  (the 
                          user's host system id and the FPRG sysid. 
                        */ 
       2 *  CHAR (10) INIT ('FROM FEP "'), 
       2 FEP_ID  CHAR(10), 
       2 *  CHAR (15) INIT ('" B$JIT.SYSID ='), 
       2 HOST_ID CHAR(10); 
                        /*Declares a buffer for reading and writing 
                          to the FPRG.  The buffer is an array of four 
                          9-bit elements.  The first bit of each 
                          element is ignored. (A byte in the FEP is 
                          eight bits). 
                        */ 
DCL  1 UC02_BUF2 (0:3)  STATIC, 
       2 * BIT(1), 
       2 FEP_BYTE  BIT(8); 
                        /*Declares a DCB for reading and writing 
                          (referenced in the OPEN FPTs). 
                        */ 
DCL  F$UC02 DCB; 
                        /*Declares a substructure used to help decode 
                          the value returned from the FPRG.  (This 
                          buffer is used to repack the value after the 
                          ninth bit is inserted in an upload from the 
                          FEP to the host.  The structure is one 
                          36-bit word.) 
                        */ 
DCL  1 FEP_SYSID, 
       2 * BIT(4), 
       2 ONE_BYTE (0:3)  BIT(8); 
                        /*Enables access to the FEP_SYSID buffer as a 
                          single word. 
                        */ 
DCL  FEP_REAL REDEF FEP_SYSID UBIN; 
                        /*Declares a temporary variable used to control 
                          translation loops (one loop for each word 
                          passed between the host and FEP). 
                        */ 
DCL   CNT   UBIN; 
                        /*Defines the stream to the second window.  All 
                          monitor service calls use the same alternate 
                          return for error processing (a call to 
                          M$ERRMSG, specified at the end of the program). 
                        */ 
CALL  M$LDEV (LDEV_UC02) ALTRET (ERR); 
                        /*Opens the DCB (F$UCO2) and places the FPRG in 
                          the path between the host program and the 
                          streamed UC02 window. 
                        */ 
CALL  M$OPEN (UC02_OPEN); 
                        /*Assigns the user's host system id (contained 
                          in the user JIT) to the (redefined) buffer that 
                          will be used to send data to and receive 
                          data from the FPRG. 
                        */ 
FEP_REAL = B$JIT$->B$JIT.SYSID; 
                        /*Loops four times, each time assigning 
                          successive 8-bit structures from the user's 
                          host system id to one 8-bit byte in the 
                          buffer to be sent to the FPRG. 
                        */ 
DO  CNT=0 TO 3; 
  UC02_BUF2.FEP_BYTE(CNT) = FEP_SYSID.ONE_BYTE(CNT); 
  END; 
                        /*Sends the data in the buffer to the FPRG by 
                          performing a write to the UC02 stream.  At 
                          this point the FPRG must perform a read to 
                          receive the host system id.  Note that reads 
                          and writes between the host and the FPRG must 
                          be synchronized. 
                        */ 
CALL M$WRITE (UC02_WRITE) ALTRET (ERR); 
                        /*Receives the system id of the FPRG by 
                          performing a read from the UC02 stream.  The 
                          data is read into the same buffer from which 
                          the host system id was written. 
                        */ 
CALL  M$READ (UC02_READ) ALTRET (ERR); 
                        /*Loops four times, each time assigning eight 
                          bits sent by the FPRG to 8-bits in a host 
                          word such that the four 8-bit bytes are 
                          concatenated. 
                        */ 
DO  CNT=0 TO 3; 
  FEP_SYSID.ONE_BYTE(CNT) = UC02_BUF2.FEP_BYTE(CNT); 
  END; 
                        /*Converts the FPRG system id from a BINary 
                          integer to a CHARacter string of all digit 
                          characters and places the results in 
                          UC_BUFFER.FEPID. 
                        */ 
  CALL BINCHAR (UC_BUFFER.FEP_ID,FEP_REAL); 
                        /*Converts the host system id from a BINary 
                          integer into a CHARacter string of all digits 
                          and places the result in UC_BUFFER.HOST_ID. 
                        */ 
  CALL BINCHAR (UC_BUFFER.HOST_ID,B$JIT$->B$JIT.SYSID); 
                        /*Writes the contents of the buffer to the M$UC 
                          window (the bottom portion of the host 
                          terminal screen). 
                        */ 
CALL  M$WRITE (UC_WRITE) ALTRET (ERR); 
                        /*Terminates normal execution. 
                        */ 
RETURN; 
                        /*Specifies the monitor service to use for 
                          reporting monitor service error conditions. 
                        */ 
ERR: 
  CALL M$ERRMSG; 
                        /*Terminates the program. 
                        */ 
END  HOST_TEST; 
The host source program is compiled and linked with the following commands: 
  !PL6 HOST_SI6 OVER *HOST_OU,HOST_LS(SC,LS) 
  !LINK *HOST_OU OVER HOST 
This example contains two PL6 programs, one that runs in the host and a FEP 
program (or FPRG) that exchanges data with the host program.  In these 
programs, the same data is displayed in two windows on the terminal screen. 
The FPRG: 
o   Reads the user's host system id (B$JIT.SYSID) as a UBIN(32) number from 
    the host. 
o   Converts the user's host system id to a CHAR string and writes it and the 
    user's FEP system id (G$JIT.SYSID) to an FPRG window on the terminal 
    screen. 
o   Sends the FEP system id to the host as a 32 bit number. 
The host program: 
o   Creates a stream for sending FPRG data to a window on the terminal. 
o   Creates the FPRG window. 
o   Writes the user's host system id to the FPRG. 
o   Reads back the user's FPRG system id as a 32-bit number and converts it 
    and the user's host system id to a CHAR string. 
o   Writes the strings to the M$UC (i.e., the original or host) window on the 
    terminal screen. 
Note that packing and unpacking of data is required:  the host expects 9 bits 
per byte, and the FEP expects 8 bits per byte. 

NOTATION
The following table defines the routine names to be entered for the execution 
of an UNWIND statement for various cases.  In all cases B3 locates a REMEMBER 
variable and the routines are entered via LNJ,B4. 
  Procedure Type      AUTO             NOAUTO 
MAIN                X6A_MAUNWIND     X6A_MSUNWIND 
ASYNC               X6A_AAUNWIND     X6A_ASUNWIND 
Parameters behave very much like implicitly based variables.  A Base Register 
must be loaded before the actual parameter can be accessed.  When a parameter 
to one routine is passed as an argument to another routine, the pointer which 
represents the parameter is simply copied. 
The VLP_CG macro generates an area used at reads and writes to comgroups (in 
the host) to describe a message being read or written. 
    MSGID = VALUE-DEC(1-?) is the system generated ID of a message. 
    MSGTYP = VALUE-CHAR(8) specifies the message type being processed.  MSGTYP 
    may be wild carded as in STATION. 
    On M$READ, MSGTYP specifies the legal message type(s) that may be read. 
    Specifying '?' only or blanks means that any type is legal. 
    On M$WRITE, MSGTYP sets the message type of the message being written. 
    The default is blanks. 
    STATION = VALUE-CHAR(8) specifies the name of the station being addressed. 
    STATION may be wild carded by using '?' as the last non-blank character. 
    In this case, any station with the matching first 'n' characters up to the 
    '?' is valid. 
    On M$READ, exactly '?' or blanks means any station is valid. 
    On M$WRITE, specifies the station to which the message is to be delivered. 
    Note that when STATION is wild carded, only stations currently extant in 
    the comgroup may be addressed; new stations are never created by this type 
    of write operation. 
    The default is blanks. 
00001
00002
00003
VLP_EOMTABLE generates a table that specifies the activation character set for 
a terminal. 
Note:  A character defined as an activation character must not also be used as 
a system function table "Special Character".  See VLP_TRMATTR, FCNTBL for 
lists of the "Special Characters" available. 
The contents of VLP_EOMTABLE are specified as follows: 
    VALUES = OPTION can be set to any one of the following options: 
       STD    Specifies the following standard 
              end-of-message character set: 
              EOT LF FF CR SUB FS GS RS US 
       DELTA  Specifies the following DELTA 
              end-of-message character set: 
              EOT LF FF CR SUB FS GS RS US HT 
              [  ]  ^  {  }  =  / 
       ALFNUM  Specifies the following 
              non-alphanumeric end-of-message 
              character set: 
              SOH STX ETX EOT ENQ ACK BEL BS 
              LF  VT  FF  CR  SO  SI  DLE DC2 DC4 
              NAK SYN ETB SUB FS  GS  RS  US 
              ! " # $ % & ' ( ) * + , - . / : 
              ; < = > ? @ [ \ ] ^ _ ` { | } ~ 
       NGRAF  Specifies the following non-ASCII graphic 
              end-of-character set: 
              SOH STX ETX EOT ENQ ACK BEL BS 
              LF  VT  FF  CR  SO  SI  DLE  DC2 DC4 
              NAK SYN ETB SUB FS  GS  RS  US 
       VALUE-DEC(0-255) [,VALUE-DEC(0-255)...]  specifies 
              up to 16 values for the 32 bytes in the 
              EOMTABLE, as explained below. 
    The EOMTABLE contains 32 bytes.  The first 16 bytes of EOMTABLE represent 
    the ASCII characters with the parity bit set to zero; the second 16 bytes 
    of EOMTABLE represent the ASCII characters with the parity bit set to one. 
    Each byte in EOMTABLE represents an 8-character column of the ASCII code 
    chart.  Each bit set on represents an activation character.  The bit whose 
    value is 128 corresponds to the top character in the column; 1 corresponds 
    to the last character in the column.  Thus the first value in the VALUE 
    parameter and the first byte in EOMTABLE represent NUL (128) through BEL 
    (1).  The second value and second byte of EOMTABLE represent characters BS 
    through SI.  The third value and third byte of EOMTABLE represent 
    characters DLE through ETB, and so forth.  Figure 5-1 shows the ASCII code 
    chart with decimal values used to calculate the VALUE parameter. 
    The values for the standard activation character set provide an example: 
    VALUE= 8, 44, 0, 47, 0*12.  The values correspond to the ASCII code set as 
    follows: 
    Decimal 8 or binary 00001000 sets EOT as an activation character in column 
    1. 
    Decimal  44 or binary 00101100 sets LF, FF, and CR in column 2. 
    Decimal  47 or binary 00101111 sets SUB, FS, GS, RS, and US in column 4. 
    0 indicates that there are no activation characters in column 3 and 5 - 
    16. 
                     EVEN BYTES OF EOMTABLE 
 HEX                                           HEX DIGIT 
 DIGIT--->|  0 |  1 |  2 |  3 |  4 |  5|  6|  7| | 
          |____|____|____|____|____|___|___|____ v    ___ 
          |NUL |DLE |SP  | 0  | @  | P | ` | P | 0   |128| 
          |_______________________________________   |___| 
          |SOH |DC1 | !  | 1  | A  | Q | a | q | 1   | 64| 
          |_______________________________________   |___| 
          |STX |DC2 | =  | 2  | B  | R | b | r | 2   | 32| 
          |_______________________________________   |___| 
          |ETX |DC3 | #  | 3  | C  | S | c | s | 3   | 16| 
          |_______________________________________   |___| 
          |EOT |DC4 | $  | 4  | D  | T | d | t | 4   |  8| 
          |_______________________________________   |___| 
          |ENQ |NAK | %  | 5  | E  | U | e | U | 5   |  4| 
          |_______________________________________   |___| 
          |ACK |SYN | &  | 6  | F  | V | f | v | 6   |  2| 
          |_______________________________________   |___| 
          |BEL |ETB | '  | 7  | G  | W | g | w | 7   |  1| 
          |_______________________________________   |___| 
                     ODD BYTES OF EOMTABLE 
           _____________________________________      ___ 
          | BS |CAN | (  | 8  | H  | X | h | x  | 8  |128| 
          |________________________________________  |___| 
          | HT | EM | )  | 9  | I  | Y | i | y  | 9  | 64| 
          |________________________________________  |___| 
          | LF |SUB | *  | :  | J  | Z | j | z  | A  | 32| 
          |________________________________________  |___| 
          | VT |ESC | +  | ;  | K  | [ | k | [  | B  | 16| 
          |________________________________________  |___| 
          | FF | FS | ,  | <  | L  | \ | l | |  | C  |  8| 
          |________________________________________  |___| 
          | CR | GS | -  | =  | M  | ] | m | }  | D  |  4| 
          |________________________________________  |___| 
          | SO | RS | .  | >  | N  | ~ | n | -  | E  |  2| 
          |________________________________________  |___| 
          | SI | US | /  | ?  | O  | _ | o |DEL | F  |  1| 
          |________________________________________  |___| 
                                                       ^ 
   For calculation of VALUE parameter of VLP_EOMTABLE _| 
00001
The VLP_ERRCODE macro may be used to generate a structure that contains the 
standard 2 word error code used internally in LCP-6.  This is the format of 
the error code as it is maintained in the JIT, the exceptional condition 
frames, and in various messages sent to cooperating processes in CP-6.  It is 
also the error code that is passed to M$ERRMSG by that cooperating host 
process. 
    ERR# = VALUE-DEC(0-8191) contains the number that identifies a particular 
    error condition.  The file B_ERRORS_C.:LIBRARY contains the values for the 
    ERR#s reported by the monitor. 
    FCG = VALUE-BIT(10) contains the two special five bit characters that 
    identify the functional code group that is reporting the error.  For 
    convenience, it may be specified as text or as a quote string (e.g., 
    FCG=GM or FCG='GM').  Each character is composed of the low-order 5 bits 
    of the ASCII code; only the characters A through Z may be represented 
    within any 5 bit field. 
    MID = VALUE-BIT(5) contains the special five bit character that identifies 
    which module in the functional code group is reporting the error.  For 
    convenience, it may be specified as text or as a quote string (e.g., MID=M 
    or MID='M').  Only the characters A through Z should be specified. 
    MON = VALUE-BIT(1) is set if this error is reported by the monitor. 
    SEV = VALUE-DEC(0-7) serves a double purpose.  Within the monitor it is 
    used to indicate the seriousness of an error.  When passed by the user to 
    M$ERRMSG it indicates the level of detail requested in the error message. 
    One of the following may be specified to indicate the action the monitor 
    is to take when the user has not specified an ALTRET address on the 
    monitor service request that has caused the error: 
      G_SEV_CONT#   - Ignore the error; continue the user. 
      G_SEV_ERROR#  - Error the program. 
      G_SEV_ABORT#  - Abort the program. 
00001
00002
00003
00004
00005
The VLP_FLDATR macro describes the graphic rendition and input qualification 
attributes of a field in a virtual device. 
At compile time, the graphic rendition for the field may be initialized 
abstractly by specifying ABSGRPRND (e.g., ABSGRPRND = EMPHASIS), or directly 
by specifying ABSGRPRND = NONE (the default) and specifying individual graphic 
rendition items (e.g., UNDSCR = YES, SLWBLN = YES). 
At run time, the graphic rendition may be manipulated abstractly by setting 
VLP_FLDATR.ABSGRPRND to the proper abstract graphic rendition value.  Or it 
may be manipulated directly by setting and resetting the items subordinate to 
VLP_FLDATR.GRPRND (e.g., VLP_FLDATR.GRPRND.UNDSCR = '1'B).  Or all the graphic 
renditions may be manipulated directly and simultaneously by assigning the 
proper bit string to VLP_FLDATR.GRPRND (e.g., VLP_FLDATR.GRPRND = 
%G#GRPRND_UNDSCR | %G#GRPRND_SLWBLN).  The G#GRPRND_... items are defined by 
the G#GRPRND_E macro. 
The input qualification items may be initialized at compile or run time.  At 
run time, individual qualifications may be manipulated by setting and 
resetting the items subordinate to VLP_FLDATR.QLF (e.g., VLP_FLDATR.QLF.ACPNMR 
= '1'B), or all qualifications may be manipulated simultaneously by assigning 
the proper bit string to VLP_FLDATR.QLF (e.g., VLP_FLDATR.QLF = %G#QLF_ACPNMR 
| %G#QLF_ACPALP).  The G#QLF_... items are defined by the G#QLF_E macro. 
Parameters are as described below. 
    ABSGRPRND = {NONE | NULL | HIDDEN | EMPHASIS | INPUT | OUTPUT | ERROR | 
    WARNING} specifies the abstract graphic rendition to be applied to this 
    field.  The corresponding graphic rendition set is determined by the 
    device's profile.  NONE (the default) indicates the graphic rendition is 
    not specified abstractly, but by the GRPRND item and its subordinate 
    definitions. 
    ACPALL = {YES|NO} specifies whether or not to allow the input of all 
    characters into this field. 
    ACPALP = {YES|NO} specifies whether or not to allow the input of 
    alphabetic characters into this field. 
    ACPGRP = {YES|NO} specifies whether or not to allow the input of graphic 
    characters into this field. 
    ACPNMR = {YES|NO} specifies whether or not to allow the input of numeric 
    characters into this field. 
    CNS = {YES|NO} specifies whether this field is constant.  YES means don't 
    erase this field unless the erase function explicitly declares that 
    constant fields are to be erased.  (See the CNS option of M$ERASE.) 
    Constant fields are implicitly protected, to a greater extent than fields 
    that are only 'protected'. 
    DCRINT = {YES|NO} specifies whether or not the field is to be displayed 
    with decreased intensity. 
    FSTBLN = {YES|NO} specifies whether or not the field is to be displayed 
    with fast blinking. 
    HDN = {YES|NO} specifies whether or not the field is to be hidden (not 
    displayed). 
    INCINT = {YES|NO} specifies whether or not the field is to be displayed 
    with increased intensity. 
    MSTENT = {YES|NO} specifies whether or not data must be input into this 
    field. 
    PRT = {YES|NO} specifies whether or not to protect this field.  Data 
    cannot be input into a field that is protected.  (Also see the PRT option 
    of M$ERASE.) 
    PRTGRD = {YES|NO} specifies whether or not to protect and guard this 
    field.  (The "guard" feature is not currently implemented.)  Data cannot 
    be input into a field that is protected. 
    RVRVID = {YES|NO} specifies whether or not the field is to be displayed 
    with reverse video. 
    SLWBLN = {YES|NO} specifies whether or not the field is to be displayed 
    with slow blinking. 
    UNDSCR = {YES|NO} specifies whether or not the field is to be displayed 
    with underscoring. 
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
The VLP_HDR macro generates the header area referred to in FPT_OPEN.  This 
area contains information on how the header is to be positioned on a given 
page. 
    COUNT = VALUE-DEC(1-255) specifies that the page number is to be printed 
    on the TITLE line, with its lefthand digit in the specified column.  The 
    default is 0 (i.e., no page numbering). 
    HEADERHEIGHT = VALUE-DEC(0-15) specifies the height of the page header 
    area.  The default is 1 (i.e., single space after printing title line). 
    The default is 1. 
    INDENT = VALUE-DEC(1-255) specifies the column in which TITLE text is to 
    start (see TITLE).  Lefthand column is column 1, and is the default. 
    RESETPAGE = {YES|NO} specifies, if YES, that page numbering is to be 
    restarted at page 1. NO specifies that no change is to be made.  The 
    default is NO. 
    TITLE = VALUE-CHAR(1-255) specifies the text which is to be printed as a 
    title on the top of every page of output for the line printer.  This field 
    is TEXTC.  The default is blank. 
00001
00002
00003
00004
00005
The VLP_HMI macro may be used to generate the area framed by the HMI vector in 
FPT_OPEN.  The structure generated by this macro contains information which 
allows the monitor to create the send and receive circular queues used by the 
Handler Monitor Interface (HMI). 
The send and receive circular queues are allocated in the user's HANDQ data 
segment.  Options on the VLP_HMI macro allow specification of word sizes for 
the send circular queue, the receive circular queue and a user context 
segment.  The total size must fit into the 64K data segment.  The total size 
will be rounded up to a page (256 word) boundary and any extra words will be 
allocated equally to the send and receive circular queues. 
    CTXSIZE = VALUE-DEC(0-n) specifies the number of words to allocate for 
    context used by the handler associated with these queues.  The default is 
    0. 
    IO = {YES|NO} specifies whether or not actual I/O operations will be done 
    from these queues, and thus whether or not the pages in the circular queue 
    segment are to be allocated from the I/O memory pool.  The default is NO. 
    RCQSIZE = VALUE-DEC(0-n) specifies the number of words to allocate for the 
    receive circular queue.  The default is 0. 
    SCQSIZE = VALUE-DEC(0-n) specifies the number of words to allocate for the 
    send circular queue.  The default is 0. 
00001
00002
00003
00004
The VLP_LINEATTR describes the physical connection of the terminal to the 
system.  The information in this VLP is never set by the user; the user can 
only look at the information.  Parameters for the VLP are as follows: 
    CONTROLLER = VALUE-CHAR(4) identifies to which of perhaps several 
    controllers on the same port that the terminal is connected.  Only 
    meaningful if MULTIDEVICE=YES, but set to blanks if not. 
    DEVICE = VALUE-CHAR(4) identifies to which of perhaps several device ports 
    on the same controller that the terminal is connected.  Only meaningful if 
    MULTIDEVICE=YES, but set to blanks if not. 
    FOREIGN = {YES|NO} indicates whether the terminal is connected directly to 
    a CP-6 node (NO) or via another network (YES).  If FOREIGN=YES, the other 
    information in the buffer refers only to the physical connection of the 
    foreign network to the CP-6 system. 
    HARDWIRE = {YES|NO} indicates whether the terminal is hardwired (YES) or 
    dial-up (NO). 
    LINESPEED = VALUE-DEC(0-15) indicates the line speed of the terminal.  The 
    values are: 
    0 =     50 BITS-PER-SECOND 
    1 =     75 
    2 =    110  (10 CPS) 
    3 =    134 
    4 =    150  (15 CPS) 
    5 =    200 
    6 =    300  (30 CPS) 
    7 =    600 
    8 =   1050 
    9 =   1200  (120 CPS) 
    10 =  1800 
    11 =  2000 
    12 =  2400 
    13 =  4800 
    14 =  9600 
    15 = 19200 
    Values 0,1,3,8,10 and 11 are not currently supported. 
    MICROFPL = {YES|NO} indicates whether this terminal is a PC that is 
    configured to use microFPL programs. 
    MULTIDEVICE = {YES|NO} indicates whether this terminal is the only device 
    on the line (NO) or is a member of a cluster (for example, IRBT, 
    multi-drop line, foreign network). 
    NODE = VALUE-CHAR(4) this is the identifier of the CP-6 node to which the 
    terminal is most directly connected. 
    PORT = VALUE-CHAR(4) identifies the port (see CP-6 System Support 
    Reference Manual) to which the terminal is most directly connected. 
    PROFILE = VALUE-CHAR(12) specifies the current terminal profile.  This is 
    a TEXTC string in which the first byte contains the character count. 
    Profile names are a maximum of eleven characters. 
    PROTXTC - the value returned for profile name on M$GLINEATTR is actually 
    in TEXTC format.  PROTXTC redefines PROFILE and includes PROTXTC.CNT and 
    PROTXTC.TXT. 
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
The VLP_PLATEN macro describes the page format of a terminal.  Parameters for 
the macro are as follows: 
    EXTWID = {YES|NO} specifies whether the value of WIDTH is the number of 
    columns by which the carriage width exceeds 254.  When WIDTH = 255, this 
    parameter is ignored. 
    The default is NO. 
    FIRSTLINE = VALUE-DEC(0-254) specifies the height of the area which is to 
    be left blank between the beginning of the page or screen and the first 
    legal print line. 
    The default is 255, which causes this parameter to be ignored. 
    LENGTH = VALUE-DEC(0-254) specifies the number of printable lines on the 
    page.  A value of zero specifies that the form is to be treated as one 
    continuous page.  There are FIRSTLINE+LENGTH+LIMBO total lines on one page 
    or screen. 
    The default is 255, which causes this parameter to be ignored. 
    LIMBO = VALUE-DEC(0-254) specifies the number of lines to be left blank 
    between the last legal print line and the bottom of the page or screen. 
    The default is 255, which causes this parameter to be ignored. 
    LPI = VALUE-DEC(0-254)  is currently unused. 
    WIDTH = VALUE-DEC(0-254) specifies the maximum number of characters to be 
    written per line on the terminals. 
    The default is 255, which causes this parameter to be ignored. 
00001
00002
00003
00004
00005
00006
The VLP_PPRIV macro may be used to generate the area specified by the PPRIV 
option of FPT_SPRIV. 
Privileges in the VLP_PPRIV area may be set on or off by specifying the 
processor privilege={ON|OFF}.  A description of the processor privileges and 
the meaning of each privilege follows: 
    processor privilege = {ON|OFF}.  There are currently no LCP-6 processor 
    privileges defined. 
00001
The VLP_PRIV macro may be used to generate the area specified by the PRIV 
option of FPT_SPRIV. 
Privileges in the VLP_PRIV area may be set on or off by specifying the 
privilege name={ON|OFF}.  A description of the privilege names and the meaning 
of each privilege follows: 
    CQ = {ON|OFF} allows the user to use the Circular Queue. 
    EXMM = {ON|OFF} allows the user to utilize a set of EXtended Memory 
    Management services.  M$CVM (read/write access) is the only one available 
    to date. 
    EXPM = {ON|OFF} allows the user to start and stop the monitor performance 
    monitor. 
    GPP = {ON|OFF} allows a user to override the stealable page limit and 
    acquire physical memory pages. 
    INTCON = {ON|OFF} allows the user to use the M$INTCON monitor service. 
    MAXMEM = {ON|OFF} allows the user to allocate memory beyond his authorized 
    limit. 
    MSYS = {ON|OFF} allows the user to use the M$SYS monitor service and to 
    execute his interrupt processing routines in Ring 1. 
    SCREECH = {ON|OFF} allows the user to use M$SCREECH to dump and reboot the 
    Front End. 
    SPCLMM = {ON|OFF} allows the user to utilize a set of SPeCiaL Memory 
    Management services.  M$CVM (read only access) is the only one available 
    to date. 
    SYSLOG = {ON|OFF} allows the user to use the M$WRSYSLOG monitor service 
    request. 
    TND = {ON|OFF} allows the user to use the Test aNd Diagnostic monitor 
    services. 
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
The M$TRTN monitor service allows the user to specify that the values of the 
base registers, the general registers, the mode control registers, etc. are to 
be replaced with values supplied by the user. 
The VLP_REGISTERS macro may be used to define the area to contain these 
values.  No initial values are provided for in this macro as the values must 
always be supplied at run time.  Generally, the data area defined by the 
VLP_REGISTERS macro will be initialized from the TCB frame (G$EXCFR.REGS) and 
selected values replaced.  The monitor service FPT can then be modified to 
point to this area (or can be initialized at compile time to point to this 
area). 
For example, the following PL-6 statements would cause the contents of general 
register 7 to be set to zero and the overflow trap for general register 7 to 
be disabled on returning to the point of interruption: 
%INCLUDE LCP_6; 
%G$TCB; 
%G$EXCFR; 
%VLP_REGISTERS; 
%FPT_TRTN; 
DCL G$TCB$ PTR SYMREF; 
VLP_REGISTERS = G$TCB$->G$TCB.STK$->G$EXCFR.REGS; 
VLP_REGISTERS.R7 = 0; 
VLP_REGISTERS.M1.R7_OV = '0'B; 
FPT_TRTN.REGS_ = VECTOR(VLP_REGISTERS); 
CALL M$TRTN(FPT_TRTN); 
The fields within the VLP_REGISTERS structure are as follows: 
    Bn$ - PTR (where n = 1-7) contains the contents of the base registers. 
    CI - BIT(8) contains the Commercial Indicator register bits which are set 
    and reset by the CIP: 
    CI.G - BIT(1) is the Greater-than Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    CI.L - BIT(1) is the Less-than Indicator that contains the results of the 
    last compare instruction executed by the computer. 
    CI.OV - BIT(1) if set, indicates that an overflow occurred during a 
    decimal instruction. 
    CI.QLT - BIT(1) indicates whether the CIP has successfully completed its 
    Quality Logic Test or not: 
         0 = QLT successfully completed. 
         1 = QLT either still running or failed 
    CI.SF - BIT(1) if set, indicates that a sign fault occurred (negative 
    operand is stored in unsigned field). 
    CI.TR - BIT(1) if set, indicates that the alphanumeric result was 
    truncated. 
    I - BIT(16) is an 8 bit indicator register that contains the overflow and 
    program status indicators: 
    I.B - BIT(1) may be considered to be a one-bit register loaded by load bit 
    instructions. 
    I.C - BIT(1) is the carry indicator that is set when the "logical" 
    capacity of any of the seven general registers is exceeded. 
    I.G - BIT(1) is the Greater-than Indicator that contains the results of 
    the last compare instruction executed by the computer. 
    I.IO - BIT(1) is the Input/Output Indicator that is set if the last I/O 
    operation was successful. 
    I.L - BIT(1) is the Less-than Indicator that contains the results of the 
    last compare instruction executed by the computer. 
    I.OV - BIT(1) is the overflow indicator that is set when any of the seven 
    general registers overflows its "arithmetic" capacity. 
    I.TRAP# - UBIN(8) contains the trap number associated with the trap.  The 
    hardware stores the trap number as '40'X - Trap Vector#.  This number is 
    then converted to the Trap Vector# by the software.  The following EQUs 
    may be used to determine the type of trap: 
    %G_MCL#             MCL 
    %G_TRACE#           Trace Breakpoint Trap 
    %G_NO_SIP#          Uninstalled SIP Trap 
    %G_TROT#            Watch Dog Timer Runout 
    %G_UNIMPL#          Unimplemented Instruction Trap 
    %G_INT_REG_OV#      Integer Register Overflow Trap 
    %G_S_DBZ#           SIP Divide by Zero Trap 
    %G_S_EXP_OV#        SIP Exponent Overflow Trap 
    %G_STK_UF#          Stack Underflow Trap 
    %G_STK_OV#          Stack Overflow Trap 
    %G_REMOTE_DESC#     Remote Data Descriptor Trap 
    %G_PRIV#            Privilege Violation Trap 
    %G_MEM_PROT#        Memory Protection Trap 
    %G_INT_UR#          Internal Unavailable Resource Trap 
    %G_PROG_ERR#        Program Error Trap 
    %G_INT_MBE#         Internal Memory or Bus Error Trap 
    %G_S_EXP_UF#        SIP Exponent Underflow Trap 
    %G_S_PROG_ERR#      SIP Program Error Trap 
    %G_S_SIGNIF#        SIP Significance Error Trap 
    %G_S_PRECISION#     SIP Precision Error Trap 
    %G_EXT_UR#          External (CIP or SIP) Unavailable Resource 
    %G_EXT_MBE#         External (CIP or SIP) Memory or Bus 
    %G_C_DBZ#           CIP Divide by Zero Trap 
    %G_C_SPEC#          CIP Illegal Specification Trap 
    %G_C_CHAR#          CIP Illegal Character Trap 
    %G_C_TRUNC#         CIP Truncation Trap 
    %G_C_OV#            CIP Overflow Trap 
    %G_CIP_QLT#         CIP QLT Fault 
    %G_SIP_QLT#         SIP QLT Fault 
    %G_EXT_PROT#        CIP or SIP Memory Protect Trap 
    %G_S_ARG#           SIP Illegal Argument Trap 
    I.U - BIT(1) is the Unlike-sign Indicator that contains the results of the 
    last compare instruction executed by the computer. 
    M1 - The M1 register enables and disables the Trace Trap and the General 
    Register Overflow Trap: 
    M1.J - BIT(1) is the Trace Trap control bit; 0 = Trace Trap disabled, 1 = 
    Trace Trap enabled. 
    M1.Rn_OV - BIT(1) (where n = 1-7) are the overflow trap control bits for 
    the seven general registers; 0 = trap disabled, 1 = trap enabled. 
    M3 - The M3 register contains the control information for the Commercial 
    Instruction Processor(CIP): 
    M3.CIP_OV - BIT(1) is the CIP Overflow Trap Mask; 0 = trap disabled, 1 = 
    trap enabled. 
    M3.CIP_TR - BIT(1) is the CIP Truncation Trap Mask; 0 = trap disabled, 1 = 
    trap enabled. 
    RDBR$ - PTR specifies the Remote Descriptor Base register and is used by 
    the CIP to locate a remote descriptor array. 
    Rn - UBIN WORD (where n = 1-7) contains the contents of the 16 bit general 
    registers.  R1 - R3 may be used as index registers.  R6 and R7 may be used 
    as a double word. 
    T$ - PTR is the Stack Address Register and contains the address of the 
    first word of the stack header. 
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
The VLP_SCODE macro generates the structure describing a standard LCP-6 
recovery code.  This is the code passed to the monitor on a call to M$SCREECH. 
    ERR# = VALUE-DEC(0-8191) contains the number that identifies a particular 
    recovery condition.  The file B_SCODE_C contains the values for the 
    recoveries initiated by the monitor. 
    FCG = VALUE-BIT(10) contains the two special five bit characters that 
    identify the functional code group that is initiating the recovery.  For 
    convenience, it may be specified as text or as a quote string (e.g., 
    FCG=GM or FCG='GM').  Each character is composed of the low-order 5 bits 
    of the ASCII code; only the characters A through Z may be represented 
    within any 5 bit field. 
    MID = VALUE-BIT(5) contains the special five bit character that identifies 
    which module in the functional code group is initiating the recovery.  For 
    convenience, it may be specified as text or as a quote string (e.g., MID=M 
    or MID='M').  Only the characters A through Z should be specified. 
    MON = {YES|NO} specifies that Recovery was called by the Monitor if set to 
    1 or by a Ghost or Special Shared Processor if set to 0.  The default is 
    YES. 
    SEV = VALUE-DEC(0-7) specifies the severity of the Recovery code: 
         G_SEV_SNAP# - Snapshot Dump 
         G_SEV_SUA# - Single User Abort 
         G_SEV_SCREECH# - Full FEP Recovery 
    The default is G_SEV_SNAP#. 
00001
00002
00003
00004
00005
The VLP_SEGMENT macro creates a structure that frames an area of memory by 
specifying the address of the first word of memory and the size in pages, of 
the area of memory.  This structure is used to specify an area of memory in 
the form required by the various memory management services.  Note that this 
structure is not a vector. 
    BASE = {VARIABLE|VALUE-DEC(0-n)} specifies the virtual address of the 
    first word of the memory extent.  The field name for this parameter is 
    VLP_SEGMENT.BASE$ or VLP_SEGMENT.BASE.  The default is NIL. 
    PAGES = VALUE-DEC(0-n) specifies the size of the memory extent in pages. 
    The default is 0. 
00001
00002
The VLP_TAB macro generates an area containing the horizontal tabulation 
definition.  Tabulation is only applicable on output to devices. 
    MARGIN = VALUE-DEC(1-255) specifies the lefthand margin by column number. 
    The leftmost column is considered to be column 1.  A record from the 
    user's M$WRITE request will have blanks inserted so the user's text starts 
    in the specified column.  The default is no indentation. 
    TABS = VALUE-DEC(0-255) [,VALUE-DEC(0-255)...] specifies horizontal 
    tabulation columns.  There is a maximum of 31 tabulation columns, which 
    must be in ascending numeric order and separated by commas.  Records from 
    user M$WRITE requests which have HT (Horizontal Tab) characters in the 
    record will be processed as if each HT were replaced by a string of blanks 
    up to the next higher horizontal tabulation column. 
    If MARGIN is also specified, tabulation is displaced so that the MARGIN 
    column on the output medium is TABS column 1.  The default is no 
    tabulation.  (Each HT character in an output record is replaced by a 
    single blank.) 
00001
00002
The VLP_TEXTC macro may be used to generate storage for any monitor service 
parameter or results area that is in TEXTC format.  It generates a length byte 
and a character string of fixed length. 
If the VLP_TEXTC macro is used to generate a BASED structure, the length of 
the character string is that of the value currently in the length byte. 
    L = VALUE-DEC(0-n) specifies the number of significant characters in the 
    text string.  It defaults to the length of TEXT, or to 31 if TEXT is not 
    specified. 
    LEN = VALUE-DEC(0-n) specifies the number of bytes to be provided for the 
    name. 
    TEXT = VALUE-CHAR(n) specifies a character string. The length of the CHAR 
    field generated is the length of TEXT (31 if TEXT is not specified).  The 
    LEN parameter can be specified to override the length (e.g. LEN=5).  If a 
    non-initializing STCLASS is used, the default for LEN causes generation of 
    a variable-length character string whose length is in the length byte 
    (VLP_TEXT.L). 
    If STCLASS=AUTO is used, LEN must be specified. 
00001
00002
00003
The VLP_TRAP_CONDITIONS macro generates a structure that contains the program 
trap condition settings.  This includes the trap handler entry address, the 
contents of the Mode Control Registers, and, for each of the hardware traps, 
the action to be taken when the trap occurs. 
This structure is used with the M$TRAP monitor service. 
The TRAP$ parameter allows specification of the user trap handler address. 
The trap_name = {ABORT | ENT_TRAP} parameters allow specification of the trap 
state of each of the traps.  If set to TRAP, the user trap handler, as 
specified by the TRAP$ parameter, will be entered.  If set to ABORT, the 
program will be aborted.  The default in all cases is ABORT. 
The mask_name = {ENABLE | DISABLE} parameters allow specification of the trap 
mask for those traps that may be masked.  The default in each case is DISABLE. 
The IGN_IO parameter allows specification of special processing of the 
Internal Unavailable Resource trap. 
Options available with the VLP_TRAP_CONDITIONS macro are: 
    CIP_OV = {ENABLE | DISABLE} specifies the setting for the CIP Overflow 
    Trap mask in the M3 Register. Default = DISABLE. 
    CIP_QLT = {ABORT|ENT_TRAP} specifies the action to be taken in the event 
    on a CIP QLT Error Trap.  This trap is signaled by the CIP whenever it 
    detects a malfunction while executing the QLT.  Only users with Test and 
    Diagnostic authorization may request control of this trap. 
    CIP_TR = {ENABLE | DISABLE} specifies the setting for the CIP Truncation 
    Trap mask in the M3 Register. Default = DISABLE. 
    C_CHAR = {ABORT|ENT_TRAP} specifies the action to take in the event of a 
    CIP Illegal Character trap.  This trap is generated by the CIP under any 
    of the following conditions: 
      - illegal decimal digit is detected 
      - illegal sign digit is detected 
      - illegal overpunch digit is detected 
    C_DBZ = {ABORT|ENT_TRAP} specifies the action to take whenever the CIP 
    attempts to execute a decimal divide instruction and the divisor is equal 
    to zero.  Note that the OV bit in the CIP Indicator Register is set by 
    this trap. 
    C_OV = {ABORT|ENT_TRAP} specifies the action to be taken in the event of a 
    CIP Overflow Trap.  This trap is generated by the CIP whenever: 
      - the receiving field of a decimal instruction 
        cannot contain all significant digits of the 
        result 
      - a nonzero digit is shifted out during a shift 
        left instruction 
    This trap is enabled only when the OV bit in the M3 Register is set.  The 
    user may cause the CIP Overflow trap to be enabled or disabled via the 
    CIP_OV option. 
    If the trap occurs (M3.OV='1'B) then the instruction is aborted and the 
    original operands will remain unmodified.  Note that the OV bit in the CIP 
    Indicator Register will be set as a result of this trap. 
    If no trap occurs (M3.OV='0'B), the receiving field will be altered (it 
    will contain the least significant part of the result). 
    C_SPEC = {ABORT|ENT_TRAP} specifies the action to take in the event of a 
    CIP Illegal Specification trap.  This trap is generated by the CIP 
    whenever any of the following conditions are detected: 
      - undefined CIP op code is detected 
      - a descriptor of an alphanumeric instruction is 
        a packed decimal descriptor 
      - a decimal operand has a zero length 
      - an operand in an EDIT, VRF or SHR instruction 
        has a zero length 
      - a separate signed decimal operand consists 
        of only a sign ATOM 
      - in a Move and Edit instruction, the receiving 
        field length has been exhausted but either 
        there are no more micro-ops or the sending 
        field length is exhausted 
      - a DD2 specifies an IOM except for DCM and 
        ACM instructions 
      - in a DSH, DD1 specifies an IMO 
      - a DD3 specifies an IMO 
      - in an SRH instruction SLL < SAL or OL < OEL 
      - in an VRF instruction VLL < VAL or OL < OEL 
    C_TRUNC = {ABORT|ENT_TRAP} specifies the action to take in the event of a 
    CIP Truncation Trap.  This trap is generated by the CIP whenever the 
    receiving field of an alphanumeric instruction cannot contain all 
    characters of the result.  Note that the TR bit in the CIP Indicator 
    register will be set as a result of this trap. 
    This trap is enabled only when the CIP_TR bit in the M3 Register is set. 
    The user may cause the CIP Truncation trap to be enabled or disabled via 
    the CIP_TR option. 
    EXT_MBE = {ABORT|ENT_TRAP} specifies the action to take when an external 
    (CIP) Memory or Bus error (parity or noncorrectable EDAC) is detected. 
    Only users with Test and Diagnostic authorization may request control of 
    this trap. 
    EXT_PROT = {ABORT|ENT_TRAP} specifies the action to be taken in the event 
    of an External Memory Protection Trap. 
    EXT_UR = {ABORT|ENT_TRAP} specifies the action to take on an external 
    (CIP) reference to an unavailable resource. 
    IGN_IO = {YES|NO} specifies that if an internal unavailable resource trap 
    occurs on an IO instruction, the trap is to be ignored and control 
    returned to the user program. 
    INT_MBE = {ABORT|ENT_TRAP} specifies the action to take when an internal 
    Memory or Bus error (parity or noncorrectable EDAC) is detected.  Only 
    users with Test and Diagnostic authorization may request control of this 
    trap. 
    INT_REG_OV = {ABORT|ENT_TRAP} specifies the action to take on an Integer 
    Register Overflow trap.  This trap will occur when the overflow bit in the 
    Indicator Register is set to 1 as a result of an operation on an 
    R-register while the overflow trap for that register is enabled. 
    This trap is enabled or disabled for each R-register via bit settings in 
    the M1 Register.  The user may cause the Integer Register traps to be 
    enabled or disabled via the Rn_OV option (where n= 0->7). 
    INT_UR = {ABORT|ENT_TRAP} specifies the action to take on an internal 
    Unavailable Resource trap.  This trap is caused by any of the following: 
      - a reference to non-existent memory. 
      - a reference to a segment whose validity bit in 
        the address space descriptor is zero. 
      - access out of bounds; a reference to an address 
        beyond the size established by the address space 
        descriptor. 
      - improper channel number in an I/O instruction. 
      - a Watchdog Timer On or Off instruction when the 
        watchdog timer is not installed. 
    J = {ENABLE | DISABLE} specifies the setting for the Trace Trap control 
    bit in the M1 Register.  Default = DISABLE. 
    This option is ignored when executing under control of a debugger. 
    MCL = {ABORT|ENT_TRAP} specifies the action to take on a monitor service 
    error when ALTRET was not specified on the request. 
    MEM_PROT = {ABORT|ENT_TRAP} specifies the action to take on a Memory 
    Protection Trap.  This trap will occur whenever an attempt is made to 
    perform a type of memory access not permitted by the appropriate 
    permission field (read, write or execute) in the address space descriptor. 
    NO_SIP = {ABORT|ENT_TRAP} specifies the action to take whenever a 
    scientific instruction is encountered and the Scientific Instruction 
    Processor option has not been installed. 
    PRIV = {ABORT|ENT_TRAP} specifies the action to take when the central 
    processor attempts to execute a privileged instruction while running in 
    the unprivileged mode (RNG value in the Status Register > Ring 1).  The 
    following instructions are privileged: 
      HLT       Halt 
      RTCN/F    Real-time Clock On/Off 
      WDTN/F    Watchdog Timer On/Off 
      IO(H)     Input/Output Word/Halfword 
      IOLD      Input/Output Load 
      LEV       Level Change 
      ASD       Activate Segment Descriptor 
    PROG_ERR = {ABORT|ENT_TRAP}   specifies the action to take whenever: 
      - the central processor attempts to execute an RTT 
        instruction and a trap save area cannot be found. 
      - the central processor attempts to execute an 
        instruction that illegally contains a register 
        address syllable. 
      - the central processor attempts to execute an RLQ 
        (Relinquish Stack Space) instruction and the 
        CW (current word length) is already zero, of if 
        the RLQ would cause the CW to go negative. 
    REMOTE_DESC = {ABORT|ENT_TRAP} specifies the action to take on a trap 
    caused by Recursive Remote Descriptor usage. 
    Rn_OV = {ENABLE | DISABLE} specifies the setting for the Overflow Trap 
    control bits in the M1 Register, where n = 1 -> 7.  Default = DISABLE. 
    STK_OV = {ABORT|ENT_TRAP} specifies the action to take on a Stack Overflow 
    Trap.  This trap is generated when a ACQ (Acquire Stack Space) instruction 
    would cause the MW (maximum word length) to be exceeded. 
    STK_UF = {ABORT|ENT_TRAP} specifies the action to take on a Stack 
    Underflow Trap.  This trap is generated when a RLQ (Relinquish Stack 
    Space) instruction would cause the CW (current word length) to be reduced 
    to zero. 
    TRACE = {ABORT|ENT_TRAP} specifies the action to take whenever trace trap 
    control has been enabled and: (1) a BRK (Breakpoint) instruction is 
    executed or (2) a branch or jump instruction is executed. 
    This trap is enabled only when the J bit in the M1 Register is set.  The 
    user may cause the trace trap to be enabled or disabled via the J option. 
    TRAP$ = {ENTRY|NIL} specifies an entry address to which control is to be 
    transferred if any of the traps that have been set to the TRAP state 
    should occur.  This is also the entry address to which control is to be 
    transferred at an error on a monitor service call without ALTRET if the 
    MCL parameter has been specified as TRAP.  Default = NIL. 
    UNIMPL = {ABORT|ENT_TRAP} specifies the action to take whenever the 
    central processor attempts to execute an instruction and the contents of 
    the Instruction Register are not recognized as an instruction. 
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
The VLP_TRMATTR macro describes the physical attributes of the terminal. 
Parameters for the VLP are described below.  If a parameter is not specified 
the value is not changed. 
    APL = {YES|NO} YES indicates that the APL character set is present, or is 
    being simulated, on the terminal.  When YES is specified, input and output 
    characters are processed as the APL character set.  NO specifies that 
    normal translation is used. 
    This parameter is ignored for M$STRMATTR. 
    ATRSCRNPOS = {YES|NO} specifies whether a field attribute definition 
    occupies a printable column on the terminal, such that a character cannot 
    also be displayed there. 
    The default causes this parameter to be ignored. 
    AUTONL = {YES|NO} YES specifies that the terminal will itself perform a 
    new line function (CR+LF) immediately after printing in (or spacing 
    through) the right margin column.  NO means that the cursor will move to 
    the right of the right margin column to a column that cannot be printed 
    in. 
    The default causes this parameter to be ignored. 
    BIN = {YES|NO} indicates whether binary output to this device is legal. 
    This option does not apply to timesharing terminals. 
    The default causes this parameter to be ignored. 
    BLANKERASES = {YES|NO} YES means that a blank (Space) character displayed 
    on the terminal in a position occupied by another character erases the 
    previous character.  NO means that the previous character is unchanged. 
    The default causes this parameter to be ignored. 
    CHARSETNAME = VALUE-CHAR(8) specifies the name of the terminal character 
    set; that is, how the characters sent to and received from the terminal 
    are translated into ASCII.  Current defined values are: 
    APLBF    APL bit-paired translation.  Lowercase ASCII characters are 
    printed as underscored uppercase characters. 
    Device: ASYNC 
    APLBP    APL bit-paired translation.  Lowercase ASCII characters are 
    printed as uppercase characters on output. 
    Device: ASYNC 
    APLTF    APL typewriter-paired translation.  Lowercase ASCII characters 
    are printed as underscored uppercase characters on output. 
    Device: ASYNC 
    APLTP    APL typewriter-paired translation.  Lowercase ASCII characters 
    are printed as uppercase characters on output. 
    Device: ASYNC 
    ASC8    8-bit ASCII.  Like ASCII-95, but it passes 8-bit characters (X'00' 
    through X'FF') through on input rather than stripping the parity bit. 
    Device: ASYNC 
    ASC64    ASCII-64 translation (the default for ASYNC devices). 
    Device: ASYNC URP 
    ASC64B    ASCII-64 variant translation for Teletype Model 35.  This table 
    interprets Altmode (X'7E', tilde) as escape on input. 
    Device: ASYNC 
    ASC64C    ASCII-64 variant translation for Teletype Model 33, Xerox 7015, 
    Hazeltine 2000, etc.  This table exchanges NOT (tilde) and OR (vertical 
    line) in CP-6 system with right bracket and left bracket at the terminal. 
    It also interprets Altmode (X'7E', tilde) as escape on input. 
    Device: ASYNC 
    ASC95    ASCII-95 translation (the default for RBTD and URP). 
    Device: ASYNC RBTD URP 
    ASC95M    ASCII-95 variant translation for CDI1203 Miniterms operating in 
    STD mode.  Converts the character generated by the ESC key (without CTRL) 
    to an ESC. 
    Device: ASYNC 
    BIT    EBC variant translation for BITNET.  The differences are: 
         EBCDIC               ASCII 
         Hex AD          <--> left-bracket 
         Hex BD          <--> right-bracket 
         solid-bar       <--> broken-bar 
         broken-bar       --> broken-bar 
         Hex FA           --> broken-bar 
         Hex BF           --> hyphen 
         Hex 8B           --> left-brace 
         Hex 9B           --> right-brace 
         Hex 8F           --> semi-colon 
    Device:  RBTD 
    EBC[{I}|{O}]    EBCDIC to CP-6 ASCII and ASCII to EBCDIC input/output 
    translation.  See Host Monitor Services Reference, Vol. II (CE75), Table 
    E-2. 
    Device:  RBTD 
    EBCE    EBC variant for RBTD European sites.  The differences are: 
         EBCDIC               ASCII 
         cent-sign       <--> dollar sign 
         solid-bar       <--> pound sign 
         backslash       <--> ampersand 
         ampersand       <--> backslash 
         pound-sign      <--> left-bracket 
         dollar-sign     <--> exclamation point 
         exclamation pt. <--> left-bracket 
    Device:  RBTD 
    HIS[{I}|{O}]    Honeywell Bull (e.g., GCOS MOD400) EBCDIC to CP-6 ASCII 
    and ASCII to EBCDIC input/output translation. 
    Device:  RBTD 
    NONE    No translation to or from CP-6 ASCII will be performed. 
    Device:  RBTD 
    SDS7012    CP-6 ASCII operator console output is translated to an 
    uppercase EBCDIC subset; this should be specified for Xerox model 7012 
    operator consoles. 
    Device:  RBTD 
    XDS[{I}|{O}]    Xerox-extended EBCDIC to CP-6 ASCII and ASCII to EBCDIC 
    input/output translation. 
    Device:  RBTD 
    3276STD    Standard EBCDIC-ASCII translation with all characters that can 
    be displayed by the 3276 type devices.  The following translation is used 
    for those characters not in both sets: 
        EBCDIC                ASCII 
        not-sign         <--> vertical-arrow 
        cent-sign        <--> left-bracket 
        solid-vert-line  <--> right-bracket 
        field-mark       <--> escape 
    Device: 3270 
    3276LIM    Same as 3276STD except useful for data-entry keyboards that do 
    not have all keys, or for others that prefer a more obvious EBCDIC-ASCII 
    translation at the expense of not being able to enter or display square 
    brackets: 
        EBCDIC                ASCII 
        not-sign         <--> tilde 
        solid-vert-line  <--> broken-vert-line 
        cent-sign        <--> vert arrow 
        left-paren       <--  left-bracket 
        right-paren      <--  right-bracket 
        broken-vert-line  --> broken-vert-line 
    Note:  Not all translations hold for both input and output.  The arrows 
    indicate the direction of translation. 
    Device: 3270 
    3270    For pre-IBM 3276 type device (limited character set).  Same as 
    3276LIM with the following differences: 
        EBCDIC                ASCII 
        right-paren      <--  right-brace 
        left-paren       <--  left-brace 
        pound-sign       <--  accent-grave 
        pound-sign       <--  backslash 
    Device: 3270 (The default for 3270 devices.) 
    3270EUR    Same as 3276STD except for the following differences needed by 
    European sites: 
         EBCDIC               ASCII 
         cent-sign       <--> dollar sign 
         solid-bar       <--> pound sign 
         backslash       <--> ampersand 
         ampersand       <--> backslash 
         pound-sign      <--> left-bracket 
         dollar-sign     <--> exclamation point 
         exclamation pt. <--> left-bracket 
    Device:  3270 
    The default is blank. 
    CRISNL = {YES|NO} YES specifies that when a carriage return character is 
    sent to the terminal a new line function (CR+LF) is performed.  NO 
    specifies that CR has some other function (see DEVICECR). If CRISNL=YES is 
    specified, DEVICECR=YES must not be specified. 
    The default causes this parameter to be ignored. 
    CURSORUP = {YES|NO} YES specifies that the terminal is capable of moving 
    its cursor upward (in the opposite direction of line feed).  NO specifies 
    this feature is not present. 
    This parameter is ignored for M$STRMATTR. 
    DCHMOVFLD = {YES|NO} YES specifies that the local character-editing 
    functions (insert-character and delete-character) cause fields to the 
    right of their invocation to slide along with the data contained in them. 
    No specifies that such fields remain stationary on the screen.  YES causes 
    the use of such functions to be disabled if a field begins or ends to the 
    right of the editing position. 
    The default causes this parameter to be ignored. 
    DEVICEBS = {YES|NO} YES indicates that a BS character sent to the terminal 
    causes a backspace.  NO specifies that a BS character be processed 
    normally, which may or may not cause a backspace. 
    The default causes this parameter to be ignored. 
    DEVICECR = {YES|NO} YES specifies that a carriage return character sent to 
    the terminal causes exactly a carriage return (moves the cursor to left 
    margin of the same line).  NO means that CR has some other (or no) effect. 
    The default causes this parameter to be ignored. 
    DEVICELF = {YES|NO} YES specifies that a line feed character sent to the 
    terminal causes exactly a line feed (moves the cursor down one line 
    without horizontal movement.)  NO means that LF has some other (or no) 
    effect. 
    The default causes this parameter to be ignored. 
    DEVPOSOPTS = {YES|NO} indicates whether the terminal combines contiguous 
    horizontal positioning requests into a single internal operation (device 
    positioning optimization).  YES implies that if a tab to column 10 
    followed by a backspace were sent to the terminal, the carriage would go 
    directly to column 9. 
    The default causes this parameter to be ignored. 
    DEVSCROLL = {YES|NO} YES specifies that the terminal is self-scrolling. 
    This means it prints on a continuous form or rolls old lines off its 
    screen as new ones are added at the bottom.  NO means that lines are 
    overwritten when the screen is filled or the device is not a CRT. 
    The default causes this parameter to be ignored. 
    DSPHEIGHT = VALUE-DEC(0-254) specifies the number of displayable lines on 
    the screen for a screen-type terminal.  It should be specified only if it 
    is smaller than HEIGHT.  It causes the default scrolling operation of the 
    terminal to use the bottom DSPHEIGHT lines of the addressable memory so 
    that the rest functions as a capture buffer, and so that direct cursor 
    positioning can be used. 
    The default is 255, which means that DSPHEIGHT is not altered.  A value of 
    zero should be used to indicate that DSPHEIGHT = HEIGHT. 
    DVCFLWCTRALG = OPTION specifies the flow control algorithm used by a 
    buffered device to prevent overfilling its buffer. 
    NONE specifies that no algorithm is used. 
    ENQACK or ETXACK specifies that CP-6 is to send an ENQ or ETX and wait for 
    the device to respond with ACK whenever enough characters have been sent 
    to fill the buffer.  The size of the buffer is specified in the profile 
    for the device. 
    DC1DC3 specifies that the device sends DC3 to halt the flow of characters, 
    and DC1 to resume it.  This algorithm is also commonly known as XON/XOFF. 
    The default causes this parameter to be ignored. 
    EXTWID = {YES|NO} YES indicates that WIDTH is the number of columns by 
    which the terminal width exceeds 254.  NO indicates that WIDTH specifies 
    the number of columns in the terminal line. 
    The default is NO. 
    FCNTBL = {'CP5'|'CP5S1'|'CP5S2'|'FRM1'|'NO'|'SE1'|'SE2'} is the name of a 
    table which tells the terminal handler how to interpret control functions. 
    If a name unknown to the system is specified, the current table is not 
    changed. CP5 identifies the full input function table and is the default. 
    CP5S1 and CP5S2 identify subset tables.  FRM1 identifies forms functions. 
    NO is a table containing only necessary line-control functions (e.g., 
    disconnect).  SE1 identifies Read-Write screen editing functions; SE2 
    identifies Read-Only screen editing functions. 
    Table    Escape        Special       Control        Numeric 
    Name     Characters    Characters    Strings        Escapes 
    NO       None          None          DISCONNECT     None 
    Table    Escape        Special       Control        Numeric 
    Name     Characters    Characters    Strings        Escapes 
    CP5      SOH    $      BS     DC2    BREAK          HT   M 
             STX    *      HT     DC3    DISCONNECT     C    R-T 
             EOT    '      LF     NAK    OVERRUN        D    . 
             HT     (      FF     ETB    PARITY CHECK   H    ^ (caret) 
             LF     )      CR     CAN                   I 
             VT     -      DEL    EM 
             CR     .      DC1 
             DEL    : 
             DC2    < 
             DC4    > 
             ETB    A-Y 
             ESC    ^ (caret) 
    Table    Escape        Special       Control        Numeric 
    Name     Characters    Characters    Strings        Escapes 
    CP5S1    SOH    $      BS     DEL    BREAK          HT    M 
             STX    *      HT     DC2    DISCONNECT     C     R-T 
             EOT    '      LF     ETB    OVERRUN        D     . 
             HT     -      FF     CAN    PARITY CHECK   H     ^ (caret) 
             LF     .      CR     EM                    I 
             VT     : 
             CR     < 
             DEL    > 
             DC2    A-B 
             DC4    D-O 
             ETB    Q-R 
             ESC    U-Y 
                    ^ (caret) 
    Table    Escape        Special       Control        Numeric 
    Name     Characters    Characters    Strings        Escapes 
    CP5S2    EOT    :      BS     DEL    BREAK          HT   R-T 
             HT     <      HT     DC2    DISCONNECT     C    . 
             LF     >      LF     ETB    OVERRUN        D    ^ (caret) 
             VT     D      FF     CAN    PARITY CHECK   I 
             CR     F      CR 
             DEL    G 
             DC2    I-K 
             DC4    N 
             ETB    Q 
             '      R 
             *      V 
             .      X 
                    ^ (caret) 
    Table    Escape        Special       Control        Numeric 
    Name     Characters    Characters    Strings        Escapes 
    FRM1     STX    :      BS     DC2    BREAK          I 
             EOT    <      HT     NAK    DISCONNECT     R-T 
             LF     >      LF     ETB    OVERRUN        . 
             VT     A      CR     CAN    PARITY CHECK 
             CR     B      DEL    EM 
             DEL    D 
             DC2    G-K 
             ETB    M-O 
             ESC    Q 
             *      R 
             '      U 
             (      V 
             )      X 
             -      Y 
             .      i 
    Table    Escape        Special       Control        Numeric 
    Name     Characters    Characters    Strings        Escapes 
    SE1      STX    *      BS     DC2    BREAK          HT   M 
             EOT    -      HT     ETB    DISCONNECT     LF   P 
             BS     .      LF     CAN    OVERRUN        A-E  R-T 
             HT     :      CR     EM     PARITY CHECK   H-I  . 
             VT     <      DEL                               ^ (caret) 
             FF     > 
             CR     A-D 
             DEL    G-K 
             DC2    M-R 
             ESC    U 
             '      V 
             (      X 
             )      Y 
                    ^ (caret) 
    Table    Escape        Special       Control        Numeric 
    Name     Characters    Characters    Strings        Escapes 
    SE2      STX    >      None          BREAK          HT   M 
             HT     A-D                  DISCONNECT     A-E  R-T 
             CR     G-J                  OVERRUN        H    . 
             DC2    N                    PARITY CHECK   I    ^ (caret) 
             ESC    Q 
             *      R 
             -      V 
             .      Y 
             <      ^ (caret) 
    FF_FLUSH = {YES|NO} YES specifies that the device (usually a plotter) 
    needs to have a form-feed operation performed to complete the display of 
    any data still buffered in the device.  NO specifies that a new-line 
    operation is sufficient. 
    The default causes this parameter to be ignored. 
    FF_INCCR = {YES|NO} YES specifies that the form-feed function for this 
    terminal also positions to the left margin.  NO specifies that it 
    positions only vertically. 
    The default causes this parameter to be ignored. 
    HEIGHT = VALUE-DEC(0-254) indicates the number of addressable lines on the 
    screen of a screen-type terminal.  See also DSPHEIGHT.  HEIGHT=0(zero) for 
    non-screen-type terminals. 
    The default is 255, which means that the height is not altered. 
    INPUT = {YES|NO} YES specifies that the terminal is capable of receiving 
    input. 
    The default causes this parameter to be ignored. 
    LFISNL = {YES|NO} YES specifies that when a line feed character is sent to 
    the terminal a new line function (CR+LF) is performed.  NO specifies that 
    LF has some other function (see DEVICELF). If LFISNL=YES is specified, 
    then DEVICELF=YES must not be specified. 
    The default causes this parameter to be ignored. 
    LIMBOCLM = {YES|NO} YES indicates that a backspace operation, immediately 
    after displaying a character in the rightmost column of the terminal, has 
    the same effect as for any other column.  NO specifies that the cursor 
    remains in the rightmost column after a character is displayed there. 
    Applicable only if AUTONL=NO. 
    The default causes this parameter to be ignored. 
    LOCALECHO = {YES|NO} YES indicates that any characters received from the 
    terminal have already been displayed on the terminal.  This option is 
    especially useful for very slow connections where the normal CP-6 echo 
    mechanism becomes distracting.  NO specifies normal processing. 
    The default causes this parameter to be ignored. 
    LOWERCASEPRINTS = {YES|NO} YES indicates that the terminal is capable of 
    printing (displaying) lower-case letters.  NO indicates that the terminal 
    is not capable of printing lower-case letters. 
    The default causes this parameter to be ignored. 
    MAXATRS = VALUE-DEC(0-254) specifies the number of field definition 
    positions permitted on any line of the device. 
    The default causes this parameter to be ignored. 
    MICROFPL = {YES|NO} specifies whether this terminal is a PC that is 
    configured to use microFPL programs. 
    The default causes this parameter to be ignored. 
    MINREC = VALUE-DEC(0-254) specifies the minimum length of a record to be 
    sent to the terminal.  This option does not apply to timesharing 
    terminals.  If a record of less than MINREC is output, it is padded with 
    spaces or zeros (depending on BIN in the M$WRITE) out to MINREC.  Zero 
    specifies that there is no minimum. 
    The default is 255, which means that MINREC is not altered. 
    NO_FLDTRM = {YES|NO} specifies whether an otherwise unterminated field 
    definition extends to the end of the device.  NO specifies that such a 
    field extends only to the end of the line. 
    The default causes this parameter to be ignored. 
    OPDTAB = {YES|NO} YES specifies that the terminal has device tabs which 
    can be set by the operator.  NO specifies that they are programmatic 
    (PROGDTAB) or nonexistent. 
    The default causes this parameter to be ignored. 
    OUTPUT = {YES|NO} specifies whether the terminal is capable of receiving 
    output. 
    The default causes this parameter to be ignored. 
    PARITY = OPTION specifies the type of character parity at the terminal. 
    Possible options are: 
     Option  Parity 
     ------  ------ 
     NONE    On input the parity bit is ignored. 
             On output the parity bit of 
             translated characters is zero and 
             the parity bit of transparent 
             characters is unchanged. 
     ZERO    Parity is 0. 
     ODD     Parity is odd. 
     EVEN    Parity is even. 
     ONE     Parity bit is 1. 
     DC      Do not change parity. 
    The default causes this parameter to be ignored. 
    PRINTTYPE = {YES|NO} YES specifies that the terminal prints on a form or 
    screen such that vertical positioning is sensible.  NO specifies that the 
    terminal produces records only (like a card punch) and vertical 
    positioning is meaningless. 
    The default causes this parameter to be ignored. 
    PROGDTAB = {YES|NO} YES indicates that the terminal device tabs are 
    programmatic.  NO indicates that the terminal device tabs are manual. 
    The default causes this parameter to be ignored. 
    SPCBFRPRT = {YES|NO} if SPCBFRPRT=NO then any VFC will be translated such 
    that all paper motion will follow print (e.g., space 4 and print VFCs will 
    be translated into write a blank line and space 4 followed by write the 
    read data and don't space).  If SPCBFRPRT=YES, no special VFC translation 
    is done. 
    The default causes this parameter to be ignored. 
    SPEED = VALUE-DEC(0-15) specifies the line speed of the terminal. The 
    values are: 
    0 =     50 BITS-PER-SECOND 
    1 =     75 
    2 =    110  (10 CPS) 
    3 =    134 
    4 =    150  (15 CPS) 
    5 =    200 
    6 =    300  (30 CPS) 
    7 =    600 
    8 =   1050 
    9 =   1200  (120 CPS) 
    10 =  1800 
    11 =  2000 
    12 =  2400 
    13 =  4800 
    14 =  9600 
    15 = 19200 
    Values 0,1,3,8,10 and 11 are not currently supported.  The default, which 
    is a value of 255, requests that the current speed not be changed. 
    WARNING:  CHANGING THE SPEED OF YOUR TERMINAL TO ONE IT DOES NOT SUPPORT 
    MAY PREVENT YOU FROM RETURNING IT TO A USABLE SPEED. 
    TRUOVRPRT = {YES|NO} YES specifies that the terminal performs 
    overprinting.  NO specifies that the terminal is not capable of 
    overprinting (that is, upspace cannot be inhibited or multiple characters 
    cannot be displayed in one position).  NO specifies that the terminal is 
    not capable of over printing. 
    The default causes this parameter to be ignored.  Not currently 
    implemented. 
    TTYTYPE = {YES|NO} YES specifies that the terminal is capable of 
    displaying what it sends.  YES is typically specified for a device such as 
    a keyboard printer or CRT.  NO specifies that input is not displayed. 
    The default causes this parameter to be ignored. 
    WIDTH = VALUE-DEC(0-254) specifies the number of printable columns on the 
    terminal.  This number can be increased by specifying the EXTWID 
    parameter.  (If the WIDTH parameter specified by VLP_PLATEN is greater 
    than the VLP_TRMATTR WIDTH, the line is continued on an additional line on 
    the terminal.) 
    The default is 255, which means that width is not altered. 
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
The VLP_TRMCTL macro defines terminal control information.  Parameters for the 
VLP are as follows: 
    ACTONTRN = {YES|NO} YES specifies that the activation (EOM) characters are 
    to apply to transparent reads to the terminal.  NO specifies that only 
    activation on byte count will be performed.  BREAK functions normally 
    independently of this option. 
    The default causes this parameter to be ignored. 
    NOTE:  The default activation character set assumes that a normal read, 
    not a transparent read is performed.  For example, the CR character 
    received as '215'O is only recognized as EOM character '015'O, i.e., the 
    value of CR after a normal read strips off the parity bit.  When 
    performing transparent reads, the user may want to call M$EOM supplying an 
    activation character set that includes EOM characters in both odd and even 
    parity. 
    ADJTOPLFT = {YES|NO} indicates the default direction for window size 
    change requests.  YES specifies that a window size change request for this 
    window that does not specify the FWINDOW parameter will prefer to move the 
    top or left boundary of the window.  NO specifies that such a request will 
    prefer to move the bottom or right boundary.  The ADJTOPLFT window 
    attribute is initialized for a new window based on the boundary of the new 
    window that was moved to create it.  Windows created with POSITION=TOP or 
    POSITION=LEFT will have ADJTOPLFT initially set to NO, and ones created 
    with POSITION=BOTTOM or POSITION=RIGHT will have it set to YES.  (See 
    VLP_WINDOW for additional information). 
    The default causes this parameter to be ignored. 
    APLLCNRM = {YES|NO} YES specifies that if lower case characters are sent 
    to the terminal while it is in APL mode, they are simply printed as 
    upper-case.  NO specifies that they are to be upper-case and underscored. 
    The default causes this parameter to be ignored. 
    AUTOCURSOR = {YES|NO} YES specifies that the cursor is to move 
    automatically from a non-reading session when a read starts and is not 
    completed by type-ahead.  The cursor is moved to the newly reading 
    session.  NO specifies that the cursor is to be moved only via the 
    keyboard or M$TRMPRG with CURSORHERE=YES. 
    The default causes this parameter to be ignored. 
    AUTOTABCLM = VALUE-DEC(0-254) specifies the initial cursor position to be 
    used when a read with DVBYTE.REREAD=NO (a new record request) occurs.  Any 
    characters saved by the wordwrap facility or in type-ahead will, of 
    course, be displayed beginning at AUTOTABCLM as well.  A value of zero or 
    one specifies that the input data is to begin immediately after the 
    prompt. 
    The default causes this parameter to be ignored. 
    BREAKCOUNT = VALUE-DEC(0-3) specifies the current break count. A current 
    break count of three causes the next BREAK to be interpreted as control-Y. 
    The specification of any value greater than three for M$STRMCTL is 
    ignored. 
    The default causes this parameter to be ignored. 
    CURSORREAD = {YES|NO} YES specifies that the "change sessions" input 
    function (usually <ESC> <.>) is to access only sessions for which a read 
    is pending.  If NO is specified, or if there are no reading sessions, all 
    sessions are accessible. 
    The default causes this parameter to be ignored. 
    DISPINPUT = {YES|NO} YES specifies that the system is to display input 
    characters on the terminal (ECHOPLEX).  NO specifies that input display is 
    to be inhibited. 
    The default causes this parameter to be ignored. 
    EDITOVR = {YES|NO} YES specifies that for CRT devices that visual fidelity 
    is to be maintained while using input editing to insert or delete 
    characters.  Visual fidelity means the image on the screen matches the 
    input record.  NO specifies that upspacing and backslashes will be 
    displayed to indicate character insertions and deletions.  For ASYNC 
    devices, do not specify YES unless all of the following is true: 
    BLANKERASES = YES 
    CUU_CHR or CUP_ALG was specified in the profile 
    CUB_CHR or CUP_ALG or DEVICEBS was specified in the profile 
    CUF_CHR or CUP_ALG was specified in the profile 
    CUD_CHR or CUP_ALG  or DEVICELF was specified in the profile 
    For hardcopy devices, YES specifies that character-delete input operations 
    (e.g., depressing the DEL key) should overstrike the deleted character 
    with a \ (backslash).  NO specifies that the \ should simply be displayed. 
    ENBENTEXTSRDCHR = {YES|NO} YES specifies that when entering or exiting the 
    Subordinate Real Device(s) (SRDs) affected by this monitor service, a 
    character string should be sent transparently to the device.  When 
    entering, the character string specified on the last M$WRITE's KEY with 
    KEYTYPE = ENTSRDCHR is sent.  When exiting, the character string specified 
    on the EXTSRD_CHR option in the device's profile is sent.  This feature is 
    used for preserving the status of graphics devices. 
    The default causes this parameter to be ignored. 
    FULLDUXPAPERTAPE = {YES|NO} YES specifies that terminal input is handled 
    using the following paper tape conventions: 
       1.  DC3 (X-OFF) and DC1 (X-ON) characters are sent to the terminal so 
           that the input does not overflow available buffering space. 
       2.  A DEL character on input is ignored. 
       3.  A LF character received as the first character of an input message 
           is ignored when M$READ is using a default input function table 
           (CP5, CP5S1, CP5S2). 
    NO specifies normal processing of terminal input. 
    The default causes this parameter to be ignored. 
    HALFDUXPAPERTAPE = {YES|NO} YES specifies that the FULLDUXPAPERTAPE 
    conventions are to be followed and that absolutely no characters are to be 
    sent to the terminal for either output or echoing.  NO specifies normal 
    processing of terminal input. 
    The default causes this parameter to be ignored. 
    HSCROLL = {YES|NO} specifies, if YES and if RETYPOVR and EDITOVR are also 
    true, that input editing is to occupy only one line, even if the input 
    record is longer than the space remaining on the line after the prompt. 
    The HSMARGIN and HSSHIFT parameters may be used to control the display 
    characteristics of this mode. 
    The default causes this parameter to be ignored. 
    HSMARGIN = VALUE-DEC(0-254) specifies, if HSCROLL=YES, the closest the 
    cursor is to be allowed to approach the edge of an input area without 
    shifting a partially displayed record to reveal more of it.  Values less 
    than %G_SCROLL_PERCENT# (128) specify the distance in columns.  Higher 
    values specify a percentage of the width of the window as 
    %G_SCROLL_PERCENT#+percent. 
    The default causes this parameter to be ignored. 
    HSSHIFT = VALUE-DEC(0-254) specifies, if HSCROLL=YES, the number of 
    columns that an input image is to be shifted when the user attempts to 
    move the cursor closer than HSMARGIN to an incompletely displayed end of 
    the record.  The keyword CENTER may be specified to request that the 
    character under the cursor be positioned as closely as possible to the 
    center of the displayed portion of the record when a shift occurs. 
    Otherwise, the value is specified in columns or as a percentage of the 
    width of the input area.  The preprocessor equates %G_SCROLL_PERCENT# and 
    %G_SCROLL_CENTER# may be used to set the value at run-time. 
    The default causes this parameter to be ignored. 
    INSERTMODE = {YES|NO} specifies, if YES, that when the cursor is 
    positioned over an input character, any new characters entered are 
    inserted to the left of the cursor, and that the DEL character deletes 
    only the character (if any) under the cursor.  NO specifies that the 
    behavior in these situations depends on SENDBKSPACE and the position 
    relative to the insertion window (see Programmer Reference Manual (CE40)). 
    The default causes this parameter to be ignored. 
    KEEPTYPAHD = {YES|NO} YES specifies that a session change as a result of 
    the AUTOCURSOR parameter is to move any type-ahead from the old session to 
    the new one for use as input to the new session.  NO specifies that the 
    type-ahead is to remain with the previous session. 
    The default causes this parameter to be ignored. 
    LOWERCASE = {YES|NO} YES specifies that any uppercase alphabetic 
    characters input from the terminal are to be sent to the user program as 
    lowercase letters.  In addition, the following five characters are 
    translated: 
    Character   Translation 
    @           ` 
    [           { 
    \           | 
    ]           } 
    ^           ~ 
    NO specifies normal processing of terminal input.  This feature is 
    provided to enable terminals that are upper-case only to input lower-case 
    characters. 
    The default causes this parameter to be ignored. 
    MSGHALT = {YES|NO} specifies, if YES, that output to the terminal is to be 
    halted after an operator message until the user enters the customary 
    output continuation character. 
    The default causes this parameter to be ignored. 
    MSGLINE = {YES|NO} specifies, if YES and the profile indicates that the 
    terminal has such a facility, that the message line of the terminal is to 
    be used to display all operator messages. 
    The default causes this parameter to be ignored. 
    NOOPTMIZ = {YES|NO} YES specifies that carriage positioning optimization 
    is not to be done.  This is useful for writing to mini-computers and paper 
    tape punches.  NO specifies that data is to be written as efficiently as 
    possible. 
    The default causes this parameter to be ignored. 
    OUTPUTDISCARD = {YES|NO} YES specifies that output is not sent to the 
    terminal.  M$WRITE requests appear to work to the user program but no 
    characters are sent to the terminal.  An M$READ that can be immediately 
    satisfied by typed-ahead input is processed normally.  An M$READ that 
    cannot be satisfied by typed-ahead input turns off output-discard mode. 
    NO specifies normal processing of output. 
    The default causes this parameter to be ignored. 
    PAGEHALT = {YES|NO} YES specifies that when the end of a page is reached, 
    output is halted until the user types a carriage return.  NO specifies 
    that output continues in this situation.  YES is often used to prevent a 
    high speed CRT from printing faster than its operator can read. 
    For 3270, it is recommended that this option be used for timesharing.  It 
    is difficult to type any input (PA or PF) when data is being sent to the 
    device; PAGEHALT provides convenient breakpoints.  Use of this option 
    together with PRINTHALT is especially helpful when using the pagewrap 
    scrolling technique since the screen is never cleared and a new attribute 
    character is never inserted. 
    The default causes this parameter to be ignored. 
    PARITYCHECK = {YES|NO} YES specifies that characters input from the 
    terminal are to be checked for proper parity (see VLP_TRMATTR).  A 
    character with bad parity is echoed as a pound sign (#) and transmitted to 
    the program as a SUB character; a parity error completion type is reported 
    on the M$READ.  NO specifies that parity is not to be checked. 
    The default causes this parameter to be ignored. 
    PARKCURSOR = {YES|NO} YES specifies, for video display terminals, that the 
    cursor is to be moved to the window's home position when activation occurs 
    in forms or screen-editing mode.  NO specifies that the cursor is not 
    moved in those situations. 
    The default causes this parameter to be ignored. 
    PRINTHALT = {YES|NO} YES specifies that if the terminal is being halted at 
    the end of each page of output that the message (CR TO GO) is to be 
    printed to prompt the user to continue the output.  NO specifies that no 
    prompt be issued in this situation. 
    The default causes this parameter to be ignored. 
    For 3270, it is recommended that this option be used for timesharing.  It 
    is difficult to type any input (PA or PF) when data is being sent to the 
    device.  PRINTHALT is useful because it is desirable to maintain a 
    protected attribute character on the screen at all times.  PRINTHALT 
    effectively pre-empts the last line to provide a place for the attribute 
    character.  Use of this option together with PAGEHALT is especially 
    helpful when using the pagewrap scrolling technique since the screen is 
    never cleared and a new attribute character is never inserted. 
    RELPAGE = {YES|NO} YES specifies that if the terminal is being halted at 
    the end of each page of output, that the page boundary will be relative to 
    the last read which halted the terminal (was not satisfied by type-ahead). 
    Thus the terminal would halt when the last input line had just scrolled 
    off the top of the screen.  NO specifies that the halts occur every screen 
    size of lines independent of whether they are inputs. 
    The default causes this parameter to be ignored. 
    RETYPOVR = {YES|NO} YES specifies that retypes (ESC-R) are to overprint 
    the line being retyped.  NO specifies that they are to be printed on the 
    next line.  YES should always be specified for 3270 keyboard display 
    devices. 
    The default causes this parameter to be ignored. 
    SCROLL = {YES|NO} YES specifies that the terminal is to be scrolled, that 
    is, treated as though the media is a continuous form.  NO specifies that 
    when a page has been filled, a screen erase is sent and a new page 
    started.  NO should always be specified for IBM 3270 type display devices. 
    The default causes this parameter to be ignored. 
    SENDBKSPACE = {YES|NO} YES specifies that when the cursor is positioned 
    over a character (A), not at the right edge of the insertion window, and 
    with INSERTMODE=NO, if the user enters another character (B), then the 
    original character, a backspace, and the overstriking character are 
    returned to the reading program (A - BS - B).  NO specifies that in this 
    situation only the overstriking character is sent (B).  Note that no 
    backspaces may be involved in the above operation, ESC-CR (e.g.) might be 
    used. 
    The default causes this parameter to be ignored. 
    SIMPERF = {YES|NO} YES specifies that underscores will be printed where 
    the perforation would normally appear on the terminal form.  This gives 
    the appearance of perforated forms on terminals with continuous form 
    paper.  NO inhibits this printing. 
    The default causes this parameter to be ignored. 
    SINPUTSZ = VALUE-DEC(0-254) specifies the minimum length of lines typed 
    which are to be remembered by the system to be re-used (ESC-D). A value of 
    zero specifies that all lines are saved. 
    The default causes this parameter to be ignored. 
    SPACEINSERT = {YES|NO} YES specifies that horizontal tab (HT) characters 
    input from the terminal are to be replaced by an appropriate number of 
    blanks based on user tabstop settings prior to being placed in the M$READ 
    buffer.  NO specifies that HT characters are to be placed in the buffer 
    unchanged.  (This can result in a significant space saving in large 
    files.) 
    The default causes this parameter to be ignored. 
    TABRELATIVE = {YES|NO} YES specifies that on input and input echoing user 
    tabstops are relative to the column where input was prompted.  NO 
    specifies that user tabstops are relative to column 1. 
    The default causes this parameter to be ignored. 
    TABSIM = {YES|NO} YES specifies that when an HT character is sent to the 
    terminal, the cursor is positioned to the next logical tab stop.  If no 
    tabstops are set, each tab character is replaced by a single blank.  NO 
    specifies that HT characters are sent to the terminal unchanged.  (This 
    can result in the cursor being positioned one space or several spaces 
    depending on the device tabs of the terminal.) 
    The default causes this parameter to be ignored. 
    TRUNCATE = {YES|NO} YES specifies that output lines which exceed the 
    platen width will be truncated to fit on one line.  NO specifies that such 
    lines will wrap to the next line. 
    The default causes this parameter to be ignored. 
    UPPERCASE = {YES|NO} YES specifies that any lowercase alphabetic 
    characters input from the terminal are to be sent to the user program as 
    uppercase letters.  NO specifies normal processing of terminal characters. 
    For 3270, UPPERCASE is turned on in all supplied profiles.  IBM 3270-type 
    devices have no caps lock key, only a shift lock.  For timesharing, it is 
    convenient to have all lowercase characters shifted to uppercase.  ESC-U 
    may be used to toggle this. 
    The default causes this parameter to be ignored. 
    WORDWRAPCLM = VALUE-DEC(0-254) specifies the maximum length of lines 
    containing blanks that will be returned to the reading program.  If a 
    longer line is entered, the characters past the space before WORDWRAPCLM 
    will be saved for use in the next read operation.  A value of zero 
    disables this facility. 
    The default causes this parameter to be ignored. 
    WRAPPAGE = {YES|NO} YES specifies for CRTs with SCROLL=NO that the screen 
    is to be erased one line at a time, such that the line below the cursor is 
    always blank.  NO specifies that the entire screen is to be erased after 
    using the bottom line. 
    The default causes this parameter to be ignored. 
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
The VLP_WINDOW macro defines terminal control information.  Parameters for the 
VLP are as follows: 
    BTMBRDR = {YES|NO} specifies whether space is to be reserved at the bottom 
    to separate this window from the one below it.  The default causes this 
    parameter to be ignored, or is NO for a new window. 
    FWINDOW = VALUE-CHAR(4) specifies the name of the window from which a new 
    window is to be created, or whose space is to be used to change the size 
    of an existing one.  The name is of the form 'UCnn'. 
    The default causes this parameter to be ignored. 
    HBRDRCHR = VALUE-CHAR(1) specifies the single ASCII character to be used 
    to mark the horizontal border space(s).  It will fill every character 
    position of the farthest line of the border space.  The default causes 
    this parameter to be ignored. 
    HBRDRSIZ = VALUE-DEC(0-15) specifies the size in lines of the horizontal 
    border space(s) (TOPBRDR and BTMBRDR).  The default is zero, which causes 
    this parameter to be ignored.  Note that the border presence parameters 
    must be used to remove a border - HBRDRSIZ=0 won't work. 
    LENGTH = VALUE specifies the size of the window, in absolute or 
    incremental lines or as a percentage of the full screen (or of the current 
    size for an existing window).  The absolute option is indicated at MACRO 
    invocation time by the absence of + or - as the first character of the 
    substitution expression, and at run-time or in a preprocessor expression 
    as %WINDOW_ABSVAL#+lines.  The percentage option may be spelled at MACRO 
    invocation as a decimal fraction (e.g., .85), or at run-time or in a 
    preprocessor expression as %WINDOW_PERCENT#+value.  This option is ignored 
    for a new window if POSITION=LEFT or RIGHT.  The default is +0, which 
    doesn't change an existing window, but is specially interpreted for a new 
    one as .99. 
    LFTBRDR = {YES|NO} specifies whether space is to be reserved at the left 
    to separate this window from the one to the left.  The default causes this 
    parameter to be ignored, or is NO for a new window. 
    MINLENGTH = VALUE-DEC(0-254) specifies the minimum length for this window 
    in lines.  The default is 255, which causes this parameter to be ignored 
    unless this is a new window, in which case it means the length is to be 
    fixed.  See REMOVABLE also. 
    MINWIDTH = VALUE-DEC(0-254) specifies the minimum width for this window in 
    columns.  The default is 255, which causes this parameter to be ignored 
    unless this is a new window, in which case it means the width is to be 
    fixed.  See REMOVABLE also. 
    ORG_PST - for M$GTRMCTL only, returns the absolute position of the 
    top-left corner of the window.  The field names are LINE (UBIN BYTE) and 
    COLUMN (UBIN 2 Bytes). 
    POSITION = OPTION specifies the portion of FWINDOW that this (new) window 
    is to occupy.  The options are TOP, BOTTOM, LEFT, and RIGHT.  This 
    parameter is ignored if the window already exists. 
    REMOVABLE = {YES|NO} specifies whether the window size is permitted to 
    drop below MINWIDTH or MINLENGTH.  If so, the window will be removed from 
    the screen when it is too small, but its context will be maintained.  The 
    default causes this parameter to be ignored, or is NO for a new window. 
    RHTBRDR = {YES|NO} specifies whether space is to be reserved at the right 
    to separate this window from the one to the right.  The default causes 
    this parameter to be ignored, or is NO for a new window. 
    TOPBRDR = {YES|NO} specifies whether space is to be reserved at the top to 
    separate this window from the one above it.  The default causes this 
    parameter to be ignored, or is NO for a new window. 
    VBRDRCHR = VALUE-CHAR(1) specifies the single ASCII character to be used 
    to mark the vertical border space(s).  It will fill every character 
    position of the farthest column of the border space.  The default causes 
    this parameter to be ignored. 
    VBRDRSIZ = VALUE-DEC(0-15) specifies the size in columns of the vertical 
    border space(s) (LFTBRDR and RHTBRDR).  The default is zero, which causes 
    this parameter to be ignored.  Note that the border presence parameters 
    must be used to remove a border - HVBRDRSIZ=0 won't work. 
    WIDTH = VALUE specifies the size of the window, in absolute or incremental 
    columns or as a percentage of the full screen (or of the current size for 
    an existing window).  The absolute option is indicated at MACRO invocation 
    time by the absence of + or - as the first character of the substitution 
    expression, and at run-time or in a preprocessor expression as 
    %WINDOW_ABSVAL#+columns.  The percentage option may be spelled at MACRO 
    invocation as a decimal fraction (e.g., .85), or at run-time or in a 
    preprocessor expression as %WINDOW_PERCENT#+value.  This option is ignored 
    for a new window if POSITION=TOP or BOTTOM.  The default is +0, which 
    doesn't change an existing window, but is specially interpreted for a new 
    one as .50. 
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
The VLR_ERRMSG macro generates an area which receives the results of the 
M$ERRMSG service. The area contains these fields: 
    ALTMSG - BIT(1) if set specifies that M$ERRMSG stored a substitute message 
    in the user buffer. 
    INERR - BIT(1)   if set specifies error on reading the message. 
    MSGCOMP - BIT(1) if set specifies that the entire message is stored in the 
    user buffer. 
    NNATIVE - BIT(1) if set specifies that the returned message is not in the 
    user's native language. 
    NOFILE - BIT(1) if set specifies that M$ERRMSG was unable to open the 
    message file. 
    NOMSG - BIT(1) if set specifies that M$ERRMSG was unable to find any 
    message for the error code. 
00001
00002
00003
00004
00005
00006
The VLR_GCHAN macro is used to define an area which will contain the results 
of the M$GCHAN monitor service.  It contains complete information about the 
channel that was obtained by the M$GCHAN service.  Parameters for the macro 
are as follows: 
    CHANNEL = VALUE-DEC(0-n) contains the number of the returned channel. 
    DVCATTR = VALUE-BIT(16) contains the hardware device attributes of 
    CHANNEL.  For details, see the System Support Reference (HA20), NETCON, 
    Device IDs in the table 'RESOURCE Attribute Defaults'. 
    DVCID = VALUE-DEC(0-n) contains the device I.D. of CHANNEL. 
    DVCRES = VALUE-CHAR(2) contains the hardware device resource type of 
    CHANNEL. 
    EXTDVCID = VALUE-DEC(0-n) contains the extended device I.D. of CHANNEL. 
    HIGHCHAN = VALUE-DEC(0-n) contains the number of the highest channel in a 
    range of channels which satisfied the RES and ATTR requirements specified 
    in FPT_GCHAN.  Only returned if FPT_GCHAN.V.FLAGS.HIGHLOW was set. 
    LOWCHAN = VALUE-DEC(0-n) contains the number of the lowest channel in a 
    range of channels which satisfied the RES and ATTR requirements specified 
    in FPT_GCHAN.  Only returned if FPT_GCHAN.V.FLAGS.HIGHLOW was set. 
00001
00002
00003
00004
00005
00006
00007
The VLR_GDDL macro may be used to generate the value area that comprises the 
informational data provided by the M$GDDL service. 
Information that is not applicable to the domain making the service request 
will be returned with a value of 0. 
    AUTHORIZED = VALUE-DEC(0-n) contains the maximum number of physical pages 
    that the user is authorized to obtain. 
    NEXT_BIG = VALUE-DEC(0-n) contains the logical number of the next big data 
    segment that the user may obtain. 
    NEXT_LITTLE = VALUE-DEC(0-n) contains the logical number of the next 
    little data segment that the user may obtain. 
    NUM_BIG = VALUE-DEC(0-n) contains the number of big data segments that 
    remain to be allocated. 
    NUM_LITTLE = VALUE-DEC(0-n) contains the number of little data segments 
    that remain to be allocated. 
    REMAINING = VALUE-DEC(0-n) contains the number of physical pages remaining 
    that the user may obtain. 
00001
00002
00003
00004
00005
00006
