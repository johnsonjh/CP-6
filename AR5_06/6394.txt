DELTA can be invoked by entry of any of the following commands: 
    !S[TART] fid U[NDER] DELTA 
        to start a program with DELTA associated. 
    !!DELTA 
        to associate DELTA with a running program at any time, or after 
        a program aborts. 
    !DELTA 
        to use DELTA in calculator mode (i.e., no program associated). 
    !PMD 
        to perform post-mortem dumps. 
To obtain more HELP information: 
HELP (DELTA) TOPICS     gives a list of all available HELP messages. 
HELP (DELTA) command    gives the syntax of a command. 
HELP (DELTA) COMMANDS   gives a list of commands in categories. 
HELP (DELTA) RUM        gives the syntax of the RUM command. 
HELP (DELTA) CONCEPTS   explains more on invocation. 
?                       means give the next level of HELP message. 
??                      means give all levels of the current. 
HELP (DELTA) RUM DES    gives a description of the RUM command. 
Note: It is not necessary to specify (DELTA) while in DELTA. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
AT
Format: 
{AC[TIVE]  }  id [-id  ] 
{IN[ACTIVE]}     [TO id] 
Description: 
These commands set stored commands to either an active or inactive status.  An 
active breakpoint is one which is still in effect.  An inactive breakpoint is 
one which is no longer in effect.  An inactive breakpoint is remembered by 
DELTA, however, and will still maintain its identification number. 
Example: 
     Command                   Explanation 
     ACTIVE 10-15              Set the specified range of inactive 
                               breakpoints to an active status. 
     INACTIVE 10-15            Set the specified range of active 
                               breakpoints to an inactive status. 
Usage Notes: 
1.  INACTIVE may also be specified as part of the AT command in the following 
    manner: 
        [id] ATI ROUTINE10[;attachment] ... 
    Attachments to an inactive breakpoint will not function until the 
    breakpoint is activated again, since an inactive breakpoint is never hit. 
00001
00002
00003
00003
AT
Format: 
ALI[B] {R[ETURN]   } [, K[EEP]] 
       {A[LTRETURN]} 
Parameters: 
RETURN    causes a RETURN to the M$ALIB call. 
ALTRETURN    causes an ALTRETURN to the M$ALIB call. 
KEEP    overrides the DLIB option on the M$ALIB call, forcing DLIB=NO and 
directs DELTA to detect faults, etc. 
Description: 
The ALIB command causes a RETURN, or an ALTRETURN if DELTA is entered from the 
M$ALIB monitor service call.  The GO command may also be used, except if DELTA 
has been placed in the ANLZ or RUM mode. 
Usage Notes: 
1.  The KEEP option is not legal when M$ALIB is issued from the ASL domain. 
2.  If the RETURN=YES option is used, an ALIB RETURN is performed by DELTA 
    after the command specified by the CMD option is performed. 
3.  If the M$ALIB call does not specify ALTRET, ALIB ALTRETURN is equivalent 
    to ALIB RETURN. 
4.  The ALIB command is not allowed for FEP programs. 
5.  If entry to DELTA was via M$ALIB, the KEEP option must be used instead of 
    GO to have DELTA field user faults, breakpoints, etc. 
00002
00003
00001
00003
Format: 
A[LTERNATE] V[ARIABLES] position 
Parameters: 
position    may be expressed as either a primary or secondary entry name. 
Description: 
This command is used to specify an alternate schema to be searched by DELTA 
whenever a search for a location (variable) reference is not satisfied within 
the current schema. 
The command can be used to great benefit during debugging sessions whose 
target run units are composed of two or more ECU's.  Through use of this 
command, references to both global and based variables may be made without ECU 
qualification. 
Example: 
    Command                        Explanation 
    ALTERNATE VARIABLES ENTRYNAME  Search the schema associated with 
                                   ENTRYNAME whenever a search 
                                   within the current schema has failed. 
Usage Notes: 
1.  The ALTERNATE VARIABLES schema is always searched as a last resort when 
    DELTA tries to satisfy a variable reference (MODIFY, LET, DISPLAY, FIND, 
    STORE, DUMP commands). 
2.  For COBOL and FORTRAN programs, the initial default for position is the 
    ECU that contains the run unit's start address.  For all other programs, 
    the initial default position is the entry name B_DELTA_D. 
Cross Reference: 
See the SCHEMA command (position option). 
00005
00002
00003
00004
00001
00004
Format: 
       [@                   ] 
AN[LZ] [RUNNING [,schemafid]] 
       [dumpfid             ] 
Parameters: 
@    specifies the running program. 
RUNNING    specifies the running monitor. 
dumpfid    is the identification of the dumpfile.  If this parameter is 
omitted, the running monitor is used. 
schemafid    is the identification of the schema file.  If omitted, M:MON.:SYS 
is assumed. 
Description: 
The ANLZ command causes DELTA to access the running monitor or a dump or 
schema file instead of memory.  The command selects the dump file that is to 
be processed and a file from which to take the schema. 
00002
00001
AT
Format: 
[id] A[T][I][S] position [#n] [condition] [;attachment] ... 
Parameters: 
id    is a decimal number from 1 to 99 which identifies the AT command. 
I    indicates that the breakpoint is to be inactive (see the INACTIVE 
command). 
S    indicates that the breakpoint is to be silent (see the SILENT command). 
#n    specifies the number of times to BYPASS the breakpoint with a true 
CONDITION before allowing it to be executed. 
condition    is an IF attachment. 
Description: 
The AT command conditionally or unconditionally interrupts execution at a 
specific position in the logical flow of a run unit. 
Example: 
    Command                         Explanation 
    AT P:100                        Sets a breakpoint at statement number 
                                    100 in ECU P. 
    AT P:100;DISPLAY X;GO           At P:100 the value of X is printed and 
                                    execution is resumed. 
    10 AT P:100 IF X EQ 0;DISPLAY Y The AT command has an id of 10. At 
                                    P:100 if X equals 0, the value of Y is 
                                    printed and DELTA reads its next 
                                    command. If X is not equal to 0, 
                                    execution resumes without 
                                    interruption. 
    AT :7 #6; LET A 1; GO           Conditional execution is specified 
                                    by using a bypass count (#6). The 
                                    breakpoint will be bypassed six 
                                    times, then reported and executed 
                                    on the seventh time. 
    AT :10 IF A GT 20;              Multiple levels of conditionality are 
                                    specified using the IF conditional. 
                                    Both the reporting of this breakpoint 
       LET B 0 IF C > 10;           and the execution of its attachments 
                                    are dependent upon the truth of the 
       LET B 1 IF C LE 10;          first IF conditional. 
                                    When the first condition is true, the 
       GO THERE IF B EQ 1; GO       breakpoint is reported and the 
                                    attachments are examined.  The 
                                    The attachments are executed only when 
                                    their associated IF condition is true. 
The previous example translates to the following pseudo code: 
         10:   IF A > 20 
         11:   THEN DO; 
         12:      IF C > 10 THEN B = 0; 
         13:      IF C <= 10 THEN B = 1; 
         14:      IF B = 1 THEN GOTO THERE; 
         15:      END; 
Usage Notes: 
1.  When both BYPASS and IF are specified, the bypass count is decremented 
    only when the IF condition is true.  The breakpoint will be reported on 
    occurrence n+1 of the true condition. 
2.  When the INACTIVE or SILENT options are specified, no space character is 
    allowed between the AT and the option (e.g., ATS or AS means AT, SILENT). 
3.  All executable statements and static data are located in the Instruction 
    Segment of a run unit.  The AT command should always specify the address 
    of an executable instruction.  Because of the way that position may be 
    specified (symbols, octal addresses, decimal addresses, expressions), 
    DELTA cannot guarantee that this requirement is met.  DELTA places a 
    breakpoint at the position to which the expression is resolved.  Should 
    this position not be an executable instruction, then the breakpoint will 
    not occur and it is possible that the placement of the breakpoint may 
    alter a word of data within the run unit.  Should this happen, the results 
    will be unpredictable.  Special care should be exercised to avoid setting 
    a breakpoint in the arguments of a calling sequence which are often 
    intermingled with the executable instructions.  Specification of a 
    breakpoint using a program statement number or label will always perform 
    correctly. 
4.  To continue execution from the point of interruption, use the GO command 
    with no position specified.  If you use GO position where position is the 
    current IC, i.e., where the breakpoint occurred, the breakpoint will 
    immediately re-occur.  Any other execution resuming command can be used 
    (that is, STEP, GOSTEP, XCON, BREAK, or GO position where position is not 
    the current IC). 
5.  The same position may not be used in two different ATs at the same time; 
    i.e., 
        3 AT 10;DISPLAY A;GO 
        4 AT 10;DISPLAY B;GO 
    is not valid. 
00002
00003
00004
00001
00004
AT
AT
General Syntax 
A stored command and its attachments are issued in the form: 
    [id] [stored command][;attachment][;attachment] ... <CR> 
The command line ends with a carriage return or end-of-record. 
Commands can be continued onto a new line if the previous line ends with a 
semicolon and the new line begins with an attachment. 
Example: 
    10 AT READ-MASTER;DISPLAY NETPAY,GROSSPAY,DEDUCTIONS  <RET> 
The example includes the following elements: 
1.  The stored command AT READ-MASTER was assigned an id of 10 by the user. 
    If a stored command with the same id already exists, it will be replaced. 
2.  The single DISPLAY attachment will display three items (variables) within 
    the user's run unit: NETPAY, GROSSPAY, and DEDUCTIONS. 
3.  The semicolon (;) is used to separate attachments. 
In the above example, the programmer directs DELTA to set a breakpoint at the 
location "READ-MASTER" in the run unit.  When the Instruction Counter reaches 
this location, DELTA will report the breakpoint at the user's terminal and 
then display the requested variables.  If the programmer does not wish to 
interact with DELTA following the display, the command should be written: 
    10 AT READ-MASTER;DISPLAY NETPAY,GROSSPAY,DEDUCTIONS;GO 
With the command written in this form, DELTA will not stop after performing 
the display but will cause the run unit to resume execution as though the 
breakpoint had not occurred. 
00001
ALTERNATE_VARIABLES
ALTERNATE_VARIABLES
Format: 
B[REAK] 
Description: 
The BREAK command causes control to be given to the break handler (declared in 
an M$INT monitor service call).  A BREAK frame is placed on the user Task 
Control Block (TCB) before giving control to the break handler. 
Usage Notes: 
1.  The BREAK command should not be confused with the break key.  Depressing 
    the break key at any time during a debugging session gives control to 
    DELTA unless the user has specified TRAP BREAK.  If TRAP BREAK has been 
    specified, DELTA gives control to the break handler without reporting the 
    break.  To direct a break to DELTA even though TRAP BREAK has been 
    specified, the user enters <CNTL-Y>, then DELTA. This will simulate a 
    break that DELTA will not pass to the break handler. 
00001
00002
00002
Format: 
BY[PASS] 
Description: 
This command is used to specify that DELTA is to skip step reporting while 
stepping assembly language program units.  This is useful for PL-6 ECU's which 
call assembly language routines.  When BYPASS is specified, all subsequent 
STEPs will not stop in assembly language modules, but will stop at the first 
instruction/statement after exiting from the bypassed module.  BYPASS/KILL 
BYPASS also controls entry into routines having no schema (as well as BMAP). 
BYPASS is the default unless the start address is in an assembly language 
routine; then the default is KILL BYPASS. 
Usage Notes: 
1.  BYPASS is a toggle.  It is reset with the BYPASS option of the KILL 
    command. 
00001
00002
00002
COPY
    There have been no significant changes to DELTA since its last release. 
    The DELTA HELP file has changed slightly in that the list of acceptable 
    TOPIC synonyms has been reduced. 
Listings of commands by categories appear at the next levels of this HELP 
message.  Type ? or ?? to see each of these categories\ or for a specific 
category type, HELP (DELTA) COMMANDS category where category is one of the 
following:  HOUSEKEEPING, EXECUTION_CONTROL, EXECUTION_TRACING, 
MEMORY_DISPLAY, MODE_CONTROL, MISCELLANEOUS HELP (DELTA) command gives the 
syntax of a command.  HELP (DELTA) category command gives a brief description 
of the specified command. 
  Housekeeping 
       Input/Output Control: 
           COPY 
           ECHO 
           EOM 
           OUTPUT 
           PROMPT 
           READ 
           REPORT 
           SYNTAX 
       Fault and TRAP Control: 
           IGNORE 
           KEEP 
           ON ABORT 
           ON EXIT 
           TRAP 
       Addressing and Symbol Control: 
           ALTERNATE VAR 
           BYPASS 
           DEFINE 
           FORMAT 
           RANGE 
           SCHEMA 
           USE NODE 
       Stored Command Management: 
           ACTIVE/INACTIVE 
           DO 
           KILL 
           SAVE 
           SHOW 
           SILENT/UNSILENT 
           UPDATE 
       For a summary description of an housekeeping command, type 
       HELP (DELTA) HOUSEKEEPING housekeeping_command 
       For instance, HELP (DELTA) HOUSEKEEPING COPY.  For a full description 
       of the command, type HELP (DELTA) command. 
  Execution Control 
       Procedure Breakpoint: 
           AT 
           ON CALL(S) 
           ON NODE(S) 
       Data Breakpoint: 
           WHEN 
       Transfer of Control: 
           ALIB 
           BREAK 
           EXIT 
           GO 
           GO TRAP 
           UNSHARE 
           XCON 
       Procedure Stepping: 
           GO STEP 
           GO TRAP STEP 
           STEP 
       For a summary description of an execution control command, type 
       HELP (DELTA) EXECUTION_CONTROL execution_control_command 
       For instance, HELP (DELTA) EXECUTION_CONTROL ON_CALL.  For a full 
       description of the command, type HELP (DELTA) command. 
  Execution Tracing 
           HISTORY 
           PLUGH 
           TRACE 
       For a summary description of an execution tracing command, type 
       HELP (DELTA) EXECUTION_TRACING execution_tracing_command 
       For instance, HELP (DELTA) EXECUTION_TRACING HISTORY.  For a full 
       description of the command, type HELP (DELTA) command. 
  Memory Display and Modification 
       Variable Oriented Commands: 
           DISPLAY 
           LET 
       Word Oriented Commands: 
           DUMP 
           EVALUATE 
           FIND 
           MODIFY 
           STORE 
           TSA 
       Post Mortem Dump: 
           PMD 
       For a summary description of an memory display and modification 
       command, type 
       HELP (DELTA) MEMORY_DISPLAY memory_display_command 
       For instance, HELP (DELTA) MEMORY_DISPLAY LET.  For a full description 
       of the command, type HELP (DELTA) command. 
  Mode Control 
           ANLZ 
           RUM 
       For a summary description of an mode control command, type 
       HELP (DELTA) MODE_CONTROL mode_control_command 
       For instance, HELP (DELTA) MODE_CONTROL RUM.  For a full description of 
       the command, type HELP (DELTA) command. 
  Miscellaneous 
           END 
           ERRFID 
           HELP 
           LIST 
           PROTECT 
           QUIT 
           SAD 
           UNFID 
           XEQ 
       For a summary description of an miscellaneous command, type 
       HELP (DELTA) MISC miscellaneous_command 
       For instance, HELP (DELTA) MISC HELP.  For a full description of the 
       command, type HELP (DELTA) command. 
00002
00003
00001
00004
00006
00005
DELTA may be entered at three times during the life of a program: as it starts 
execution, during execution and after a program aborts.  DELTA may also be 
called in stand-alone mode, and at run-time by a user program via the M$ALIB 
monitor service.  The methods of invocation and uses are discussed below. 
Enter ? to see each of the following subtopics on 
  Start Program with DELTA 
  Post Association of DELTA 
  No Run Unit Associated 
  Programmed Association 
  Communications with DELTA 
Initiating A Program with DELTA Associated 
Most debugging sessions are begun by starting the program to be debugged under 
DELTA.  This is accomplished in two ways, both are commands in IBEX. 
    !S[TART] fid U[NDER] [DELTA] 
This command brings a run unit named fid into memory and prepares it for 
execution.  DELTA is entered with the user program ready to run.  DELTA prints 
the current value of the instruction counter, the program start address.  For 
example: 
    !START COBOLRU UNDER DELTA 
    DELTA E03 HERE IC = PROG:0 [ENTRY] 
This method can be used online and in batch.  The user may now use any of the 
DELTA commands, or just say GO to begin execution.  IC is the instruction 
counter and indicates the address that is about to be executed. 
If the user's program reads the invocation line from B$JIT.CCBUF or depends on 
IBEX to implicitly set DCBs, the start command should not be used.  Instead 
the IBEX command U may be used.  The U implies the words UNDER DELTA on the 
next command line.  For example: 
    !U 
    !MYCOMP.ME ON OUFILE,LP (LS,OU) 
    DELTA E03 HERE IC = MAIN:0 [ENTRY] 
In this case, the invocation line that is placed in B$JIT.CCBUF will be the 
same as if DELTA were not associated. 
Post Association of DELTA 
DELTA may be associated with a running program at any time.  This is useful 
when a program appears to be looping or is in a bad or unexpected state, and 
the user wants to interrupt execution and see what the IC value is, or look at 
program variables.  To associate DELTA after the program has started, the user 
types <CNTL-Y>.  IBEX prompts with a double bang (!!).  The user types DELTA 
to associate DELTA with the interrupted program.  When DELTA is associated, if 
the program is autoshared, the user should use the UNSHARE command if any 
modification of procedure (including breakpoints) is to be done.  For example: 
    !MYPROG. 
The program does not prompt as expected; a loop is suspected.  The user enters 
<CNTL-Y>. 
    !!DELTA 
    DELTA E03 HERE IC = INITVALS:54,,.3 [ASSIGNMENT] 
This method is only available online. 
When a user program aborts, IBEX holds the image of the run unit in memory. 
The user can associate DELTA with the image by typing DELTA immediately after 
the abort message.  For example: 
    !MYPROG. 
          memory fault  (IBEX reports program abort due to 
                                  memory fault) 
    !DELTA 
    DELTA E03 HERE IC = SUBPRO6:73,,.5 [INPUT/OUTPUT] 
DELTA reports the IC value at the time of the fault.  Any DELTA command can be 
issued, and the program can be continued by the GO command. 
No Run Unit Associated 
DELTA can be entered alone, i.e., with no program associated.  This is 
sometimes referred to as calculator mode.  DELTA is usually used to evaluate 
expressions when entered in stand-alone mode, although small programs in GMAP6 
instruction format may be entered.  For example: 
    !DELTA 
    >DELTA E03 HERE - NO RU ASSOCIATED 
    >EV 250 +.13\U 
    = 261 
    >.101\C 
    ='A   ' 
    >M .30 LDQ 43,DL 
    >M .31 0 
    >GO .30 
       IPR fault @ .31/0 
    >D $Q\U 
     $Q=43 
The procedure space available to the user when DELTA is in the stand-alone 
mode extends from location .20 to location .2000; locations .0 to .17 are 
reserved for use by DELTA.  KILL EOM is the default in stand-alone mode.  To 
enable it, the user can use the EOM command. 
Programmed Association of DELTA 
DELTA may also be associated by a running program via the M$ALIB monitor 
service call.  Using this service a command may be passed to DELTA for 
execution.  This is useful to an exceptional condition handling routine in a 
production program.  If, for example, the program has entered the XCON routine 
due to bad data in an input buffer, a DUMP command may be passed to DELTA to 
print the offending buffer. 
Communications with DELTA 
DELTA uses the prompt character '>' when it is waiting for the user to enter a 
command at the terminal.  All commands should be ended with the <RETURN> key 
on the keyboard. 
All commands, except for the open form of the MODIFY command, will error if 
ended with <LINEFEED>.  When <LINEFEED> is used with the open form of the 
MODIFY command, the next memory cell will be opened for modification. 
By default, DELTA uses a special End-of-Message (EOM) character set.  These 
are characters which terminate the mode and activate DELTA.  The complete list 
of DELTA EOM characters includes T, <LINEFEED>, <TAB>, <RETURN>, [, {, ], }, 
/, and =.  Most of the special EOM characters are used only when debugging at 
the assembly or machine language level.  However, ] and }, which have the same 
effect, are a shorthand for the STEP command and are very convenient for 
stepping through a program.  In order to enter any of these characters without 
activation to DELTA, for instance in a character string constant for the LET 
command, DELTA's special activation set must be turned off.  This is done with 
KILL EOM command.  The EOM command turns the special activation set back on. 
KILL EOM is the default for stand-alone mode. 
If a symbol name is used that matches one of DELTA's special names, contains a 
period and is not a PL-6 structure name, contains a colon, or begins with an 
*, the symbol name must be specified by enclosing it in quotes followed by an 
"S".  For example: 
    '$JIT'S 
    '.LABEL'S 
If DELTA is already associated, depressing the break key will cause the 
running program to be interrupted.  DELTA will report the current IC position 
and prompt for input. 
00005
00003
00002
00004
00001
IF_ATTACHMENT
Format: 
C[OPY] 
Description: 
DELTA's output is normally routed to the interactive terminal during an 
on-line session.  The interactive user who has routed DELTA output to some 
other destination (e.g., a fid so that a copy of the session is maintained) 
may also wish to use the COPY command to see DELTA's output at the interactive 
terminal.  By using COPY in conjunction with OUTPUT, the user directs DELTA's 
output to two places. 
Example: 
These examples of input/output control commands assume an on-line session. 
    Command                Explanation 
    OUTPUT ON LP           Direct DELTA's output to the line printer. 
    ECHO                   Write any input not received from the 
                           default command stream to the M$DO DCB (in 
                           this example, to the line printer). 
    READ MYFILE            Read the next commands from the file 
                           called MYFILE.  (Commands will be 
                           echoed on the line printer). 
    COPY                   Direct DELTA's output to two places. 
    READ MYOTHERFILE       Read the next commands from the file 
                           called MYOTHERFILE.  (These commands 
                           will now be written both to the line 
                           printer and the interactive terminal). 
Usage Notes: 
1.  COPY is a toggle command.  It is reset by the command: 
        KILL COPY 
2.  KILL COPY is the initial default. 
00001
00002
00003
00003
DISPLAY
DEFINE
DEBUG_FPRGS
Information on debugging DCB-connected FPRGs is given below.  For information 
on debugging a specified SYSID on a specified FEP, enter 
HELP DEBUG_FPRG BY_SYSID 
DCB-connected FEP programs are started via an M$SETFP monitor service call 
done in a program running on the Host.  In order to debug DCB-connected FEP 
programs, the user just starts the Host program under DELTA. 
    !U 
    !HOSTRU. 
    or 
    !START HOSTRU UNDER DELTA 
This associates DELTA with the Host program and with any FEP programs started 
via an M$SETFP monitor service call by the Host program.  DELTA identifies 
which program the user is dealing with by preceding the prompt ('>') with the 
value the user specified for RES on the M$OPEN of the FEP program. 
    Example                                     Explanation 
     !U 
     !HOSTRU. 
     DELTA E03 HERE IC=TEST:1 [PROC] 
     >G                                         User does GO to host 
                                                program so M$SETFP can 
                                                happen. 
     HOST PROGRAM STOPPED IC=TEST:4956 [MONITOR CALL] 
     (UC05) IC=A:1 [PROC] 
     FPGR STARTED VIA M$SETFP 
     UC05>                                      User gets control when 
                                                FEP program (UC05) gets 
                                                started - user can enter 
                                                DELTA commands for this 
                                                FEP program, i.e., set 
                                                breakpoints, GO, etc. 
For more information, enter ? . 
Post Association of DELTA 
To associate DELTA with a Host program and the FEP programs started by the 
Host program via an M$SETFP monitor service call, the user types <ESC> <.> 
<CNTL-Y>.  IBEX prompts with a double bang (!!).  The user types DELTA to 
associate DELTA with the interrupted Host program and the FEP programs 
associated with the Host program.  Any FEP programs which have been started by 
the Host program will be reported to the user.  When DELTA is associated, if 
the host program or any FEP program is autoshared, the user should use the 
UNSHARE command if any modification of procedure (including breakpoints) is to 
be done. 
   Examples                     Explanation 
    !HOSTRU.                    Program does not prompt as expected; 
                                a loop is suspected.  The user enters 
                                <ESC> <.> <CNTL-Y>. 
    !!DELTA 
    DELTA E03 HERE IC=TEST:5053,,.3 [ASSIGNMENT] 
    (UC05) IC=A:10 [ASSIGNMENT] 
    > 
DELTA may be associated with a FEP program (FPRG) by specifying the sysid and 
fepname of the program on the DEBUG command. 
DEBUG Command (FEP Program) 
Format: 
DEB[UG] sysid {AT} fepname 
              {ON} 
Parameters: 
sysid    is the decimal sysid of the desired FEP program to debug. 
fepname    is a character string of eight characters or less that identifies 
the FEP in which the program to debug is running. 
Description: 
This command associates DELTA with the FEP program identified by its sysid and 
the FEP in which it is running.  The user can then enter DELTA commands, 
including GO to start execution of the FEP program. 
Example: 
At a timesharing terminal the user enters 
    !DELTA 
    DELTA E03 HERE - NO RU ASSOCIATED 
    >DEBUG 21 AT FEP12 
DELTA is associated with the FEP program in FEP12 that is sysid 21. 
Usage Notes: 
1.  If a second DEBUG command is entered before the user QUITs or ENDs the 
    first program being debugged, DELTA will do a KILL DELTA on the first 
    program before setting up for debugging the second specified program. 
00002
00001
    The DELTA DEBUG command is used to debug a handler running in a debug FEP. 
    In order to do this, the user needs to do the following: 
1.  Get an ASYNC line between the debug FEP (FEP 2) and a local FEP (FEP 1). 
    This is referred to as the debug link. 
2.  Use the SUPER processor to define the profile for the debug link and to 
    define the debug link.  For example: 
     !SUPER 
     REM PRO $DEBUGPRO 
     CR PRO $DEBUGPRO FROM DFLCRT  "Define the debug link profile 
     DEVICECR=NO 
     DEVICELF=NO 
     DEVICEBS=NO 
     PRINTTYPE=NO 
     END 
     END 
     !SUPER 
     REM DEVICE DEBUG2 
     CR DEVICE DEBUG2 FOR STATION LOCAL  "Define the debug link from FEP1 
     USE=CG                              "to FEP 2 
     COMG=CG/FECG.:SYS 
     PASS=NONE 
     PRO=$DEBUGPRO 
     END 
     END 
3.  Set up the debug link in the local FEP (FEP 1) by configuring 
    the line in NETCON as follows: 
     !NETCON 
     SEL NODE=1                 "Select FEP1 
     CONFIG .1000 SPEED=9600,;  "The debug link is at port '1000'X in FEP 1 
                  HARD=YES,; 
                  LOGON='DEBUG2',; 
                  SAL=NO,; 
                  DROPDTR=YES,; 
                  BUF=128,; 
                  PRO='$DEBUGPRO',; 
                  READTIMEOUT=0 
     END 
4.  Set up a copy of the LCP-6 monitor rununit to be used in the debug FEP 
    (FEP 2) as follows: 
    a. 
         !C M:FEP.:SYS OVER M:FEP_TEST.:SYS (READ=?) 
         !RUM M:FEP_TEST.:SYS,NUTS 
         M GD_CHN\X .1000      "Sets the port of the debug link in FEP2. 
         M GD_LINSPD\X .E      "Sets the line speed of the debug link 
                               "(Refer to the discussion of 
                               "VLP_ATTR in the publication CP-6 
                               "Host Monitor Services Reference 
                               "V.1 (Descriptions)(CE74), for 
                               "a listing of the speed codes that 
                               "can be placed in GD_LINSPD.) 
    b.  Establish control of traps: 
        G_KEEP_USER is a bit array corresponding to the trap number in the 
        LCP-6 system.  EQU's for the trap numbers can be found in 
        G_LCP6_E.:LIBRARY.  The user can set the bits in G_KEEP_USER 
        corresponding to the traps for which he would like to get control in 
        DELTA.  The following example will get control of all trap number 10 
        (stack overflow) and all trap number 14 (memory protection): 
          !RUM M:FEP_TEST.:SYS,test 
          M G_KEEP_USER .0044      "Get control of traps 10 and 14. 
          Q 
        When the user is in DELTA debugging and a trap occurs corresponding to 
        one for which control has been requested, DELTA will report the trap 
        to the user and prompt for commands. 
    c.  If the following words are set to -1 they allow the user to get 
        control early on in the boot process. 
        o   M GD_DBG_INIT -1 will allow the user to associate DELTA before any 
            handlers have been read in. 
        o   M GD_DBG_MONINIT -1 will allow the user to associate DELTA before 
            any users have run. 
        If the user needs control for either of these two cases, M:FEP_TEST 
        should be RUMmed and the appropriate location modified to be -1 as 
        follows: 
         !RUM M:FEP_TEST.:SYS,NUTS 
         M GD_DBG_INIT -1      "Get control before any handlers run. 
         Q 
5.  Set up the boot information for the debug FEP (FEP 2) to include the 
    handler by using NETCON as follows: 
     !NETCON 
     SEL NODE=2            "Select the debug FEP (FEP 2) 
     SET BOOTINFO          "Set the boot information 
     M:FEP_TEST.:SYS       "Set the monitor fid 
     3                     "Set the number of handlers 
     NODEADMN              "First handler name 
     NODEADMN.:SYS         "First handler fid 
     COUPLER               "Second handler name 
     COUPLER.:SYS          "Second handler fid 
     yourhandlername       "Third handler name 
     yourhandlername.acct  "Third handler fid 
     :SYS                  "Library account 
     END 
6.  Boot the FEP and associate DELTA for debugging: 
     !NETCON 
     BOOT N=2,NOTIME     "Specify NOTIME so the FEP 
     END                 "does not time out while debugging 
     !DELTA 
     DEBUG @DEBUG2 U M:FEP_TEST.:SYS  "Associate DELTA with the debug 
                                      "FEP (FEP 2) 
When debugging a forms program, two terminals are required.  One terminal is 
logged on as a station that runs the FPL program; the other is a timesharing 
terminal that runs DELTA. 
DELTA may be invoked prior to or during Forms Program execution.  All 
debugging sessions begin by starting the Forms at a TP station.  Then DELTA is 
invoked from a separate timesharing terminal.  As soon as DELTA is activated, 
it takes control of Forms Program execution.  For more information, enter ?? . 
Associating DELTA at Program Invocation 
Associating DELTA at program invocation requires entry of special commands at 
the TP station and the timesharing terminal.  For additional information, 
enter ?? or enter 
HELP (DELTA) DEBUG_TP_FORMS DEBUG_FORMS 
HELP (DELTA) DEBUG_TP_FORMS DEBUG_TP_STATION 
HELP (DELTA) DEBUG_TP_FORMS POST_ASSOCIATION_OF_DELTA 
DEBUG Command (TP Forms Program) 
Format: 
DEBUG name 
Parameters: 
name    is the Forms Program name (as entered in the BEGIN command). 
Description: 
The DEBUG command, instead of the BEGIN command, is entered at the TP station 
to invoke the Forms Program for debugging.  As a result of this command, the 
Forms Program is loaded, but does not begin execution. 
At a separate timesharing terminal, the user invokes DELTA and DELTA responds 
with a prompt.  The user then enters the DEBUG command to associate DELTA with 
the station and comgroup that invoked the Forms Program for debugging. 
DEBUG Command (TP Station) 
Format: 
DEB[UG] station {AT} {comgroupfid} 
                {ON} {TP/tpacct  } 
Parameters: 
station    is a character string of eight characters or less that defines the 
station name of the terminal running the Forms Program to be debugged.  If 
station is all numeric, it must be entered in quote strings. 
comgroupfid    is a comgroup fid of the form CG[#psn]/name.acct or of the form 
CG[#psn] name.acct.  'name' identifies the comgroup through which the FPL 
program is communicating. 
tpacct    is a character string of eight characters or less that names the 
account in which the particular instance of TP is being run. 
Description: 
This command associates DELTA with the TP station.  The user can then enter 
DELTA commands, including GO, to start execution of the Forms Program. 
Example: 
At STATION1 on the instance of TP called PAYROLL, the user enters: 
    DEBUG PAY 
At the timesharing terminal the user enters: 
    !DELTA 
    DELTA E03 HERE - NO RU ASSOCIATED 
    >DEBUG STATION1 AT TP/PAYROLL 
In this example, the Forms Program called PAY is loaded and halts.  Then DELTA 
is invoked to debug the Forms Program operating on behalf of STATION1 on the 
PAYROLL instance of TP (i.e., PAY). 
Post Association of DELTA 
After a Forms Program has been invoked via the BEGIN command, the user can 
associate DELTA.  At a timesharing terminal, the user invokes DELTA and enters 
the DEBUG command as shown above.  DELTA assumes control over the execution of 
the Forms Program, the user may then enter DELTA commands. 
Usage Notes: 
1.  If a second DEBUG command is entered before the user QUITS or ENDS the 
    first program being debugged, DELTA will do a KILL DELTA on the first 
    program and then set up for debugging the second specified program. 
2.  If a user post-associates DELTA and the FPL program is sitting on a READ 
    from the terminal, the user must satisfy the READ to get control with 
    DELTA. 
3.  If a "LOAD fid BY NAME" is done in an FPL program, the user gets control 
    with a "GHB-MO1350-0 FPRG requesting M$LDTRC" message.  At this point, the 
    user must enter GOTRAP to cause the new program to start. 
00002
00003
00001
00004
Format: 
DE[FINE] symbol expression 
Parameters: 
symbol    is a symbol name up to 30 characters in length. 
expression    is any address expression which results in a value.  Overflow is 
ignored, and only the least significant 36 bits of the value are saved. 
Description: 
The DEFINE command associates a symbolic name with a value, allowing the 
symbol to be used whenever the associated value is desired.  This is 
particularly useful for defining addresses in programs that do not have debug 
schema. 
Example: 
     DEFINE HEP .14136 
     DEFINE HEPMORE HEP+.201 
Usage Notes: 
1.  A DEFINED symbol may be removed with the DEF option of the KILL command. 
2.  DEFINE cannot be used to define replacement names for ENTDEFs.  An ENTDEF 
    (primary entry definition, secondary entry definition, ECU name) is a 
    special entity which has schema associated.  A symbol name defined with 
    DEFINE has no associated schema.  Therefore, while: 
        MODIFY VERYLONGENTRYNAME:23 
                   and 
        DEF VLEN VERYLONGENTRYNAME 
    are meaningful, MODIFY VLEN:23 is not. 
00002
00003
00004
00001
00004
    All descriptors which are visible to a run unit may also be used to 
    qualify memory references.  Each of these descriptors is known to DELTA by 
    a distinguished name and may be used as a pointer in much the same manner 
    as a pointer variable or constant.  All of the distinguished names known 
    to DELTA are described in the topic DISTINGUISHED_NAMES, and the topic 
    FEP_DEBUG_TIPS, the DISTINGUISHED_NAMES subtopic.  The more common ones 
    are listed below. 
    Distinguished 
    Descriptor 
    Name                    Refers To: 
    $LS0 or $ISR            Instruction Segment 
    $LS1 or $JIT            Job Information Table (JIT) 
    $LS3                    Read Only Segment 
    $LS4 or $DS1            Automatic Segment 
    $LS5 or $DS2            Common Segment 
    $LS6 or $DS3            Dynamic Data Segment 3 
    $LS7 or $DS4            Dynamic Data Segment 4 
    $LS8 or $DS5            Dynamic Data Segment 5 
    $LS9 or $DS6            Dynamic Data Segment 6 
    $LS10 or $DS7           Dynamic Data Segment 7 
    $LS11 or $DS8           Dynamic Data Segment 8 
    $LS12                   Null Segment 
    Whenever descriptor qualification is used, the distinguished name of the 
    descriptor must be the leftmost qualifier in the memory reference.  For 
    examples, enter ? . 
Example: 
Command                                     Meaning 
DISPLAY $LS5->ARRAY1(3)                     Display the third element 
                                            of ARRAY1.  The base address 
                                            of the common segment is also 
                                            the base address of ARRAY1. 
DISPLAY $LS5->4->ARRAY1(3)                  Display the third element of 
                                            ARRAY1.  Use word 4 in the 
                                            common segment to determine 
                                            the address of ARRAY1. 
DISPLAY $LS2->0->NEXT->MS.SS.ITEM           Use word zero of the segment 
                                            described by Linkage Segment 
                                            Descriptor #2 to determine the 
                                            address of the based pointer 
                                            called NEXT.  Use NEXT to 
                                            determine the address of the 
                                            Major Structure called MS. 
                                            Display the elementary item 
                                            called ITEM contained within 
                                            the Subordinate Structure SS. 
00001
COMMANDS
Format: 
D[ISPLAY] item[\f][,item[\f] ... ] 
Parameters: 
item    may be: 
o   A scalar variable 
o   A structure 
o   A qualified subordinate structure 
o   A qualified elementary item 
o   An array 
o   A subscripted element of an array 
o   A subscripted range of an array 
o   Any general location reference (address expression) 
o   Any general position reference 
o   A DELTA distinguished name 
f    is one of the format specifiers (see the FORMAT command).  In general, 
specification of a format for variables is not necessary since each variable 
is described in the debug schema allowing DELTA to display it in the correct 
form.  General address expression items are displayed in octal by default, 
while general position references are displayed in instruction format.  The 
default display mode for any item may be overridden by use of the desired 
format specifier. 
Description: 
The DISPLAY command is used to display an area of memory or a program visible 
register. 
The DISPLAY command displays program variables by name.  The user need have no 
knowledge of their location or internal representation.  DISPLAY handles 
simple variables, structured variables, arrays and all of the storage 
classifications used by the supported languages.  These are static, automatic, 
parameters (both in automatic stack frames and in static storage) and based 
for PL-6; File Section, Linkage Section and Working Storage Section in COBOL; 
and all FORTRAN variables including subroutine parameters.  The allowable 
forms of reference are as varied as the different data types.  The PL-6 
pointer variables in a pointer qualified reference may be part of a structure 
and may be subscripted.  Subscripts themselves may be pointer qualified and/or 
subscripted. 
Example: 
    Command                                   Explanation 
    DISPLAY HAROLD                            Simple elementary variable. 
    DISPLAY JOHN(2)                           Subscripted variable, using 
                                              literal subscript. 
    DISPLAY JEFF(HAROLD)                      Subscripted variable using 
                                              elementary variable for the 
                                              subscripted value.  Note:  A 
                                              variable used for a subscript 
                                              must be a signed or unsigned 
                                              integer (PL-6, FORTRAN, COBOL) 
                                              or a packed or unpacked decimal 
                                              number which represents an 
                                              integer value (COBOL). 
    DISPLAY PVAR->BASEDITEM                   Pointer qualified variable. 
    DISPLAY SPVAR(3)->BASEDITEM               Pointer qualified variable using 
                                              subscripted pointer variable. 
    DISPLAY SPVAR(PVAR->BASEDITEM)->          General pointer qualified 
    OTHERBASE(PVAR->NEWVAL)->MYBASEDVAL       subscripted reference. 
    DISPLAY ALPHA.BETA.GAMMA                  Structure qualified item.  Note: 
                                              All levels of a structure must 
                                              be specified. 
A subset of an array may be displayed by specifying a range of subscripts for 
one of its dimensions.  A range is specified by two subscript values separated 
by a colon (:).  If a subscript or subscript range is not specified for an 
array item, the entire array will be displayed.  For example: 
    DISPLAY VECTOR(FIRST:LAST) 
    DISPLAY MATRIX(3:LASTITEM,THISROW) 
    DISPLAY VECTOR 
Usage Notes: 
1.  PL-6 based variables declared with implicit pointers may be displayed 
    without specifying the implied pointer, or explicit pointer qualification 
    may be given to override the default implication. 
2.  While a variable to be displayed may have a range of subscripts specified, 
    a subscripted pointer used in a pointer qualified reference may not.  That 
    is: 
        DISPLAY PTR(2)->VAR.X      is allowed 
        DISPLAY PTR(2:5)->VAR.X    is not allowed. 
3.  To DISPLAY a variable not described (referenced) in the current program 
    unit requires procedure qualification in order to indicate to DELTA where 
    the schema describing the item may be found.  Procedure qualification is 
    specified by giving the external program unit name of the EPU containing 
    the variable followed by a colon (:).  For example: 
        DISPLAY SUBPROGRAM1:XVAR 
        DISPLAY MAIN:LOOPCOUNT 
    In PL-6, which has internally nested procedures (IPU), a variable which is 
    local to an IPU must be qualified by the EPU and all levels of IPU to that 
    containing the variable. 
    Assume an external PL-6 procedure called EXPROC with internal procedure 
    LOCPROC which, in turn, contains the procedure for ALPHA.  To display a 
    variable DATES which is local to ALPHA when the program counter is not 
    currently within ALPHA, the reference is: 
        DISPLAY EXPROC:LOCPROC:ALPHA:DATE 
4.  Only one procedure qualification specification is allowed for each item to 
    be displayed.  This means that all pointers and subscript variables in a 
    general variable reference must be in the same procedure.  For exceptions 
    to this rule see the discussion of the ALTERNATE VARIABLES command. 
5.  The DISPLAY command also allows the display of addressed locations of 
    memory and the program-visible registers.  In pointer qualified references 
    it is allowable to use general address expressions for specifying the 
    pointer location together with a based variable name for the item to be 
    displayed.  For example: 
        DISPLAY .400 
        DISPLAY .41235->GORGO.PUUDLY 
        DISPLAY $LS1->B$JIT.UNAME 
        DISPLAY $X1,$Q 
6.  When displaying multiple items from an ECU, it is not necessary to 
    propagate the ECU name.  For example: 
        DISPLAY EXPROC1:A,B,EXPROC2:C,D 
    is equivalent to 
        DISPLAY EXPROC1:A,EXPROC1:B,EXPROC2:C,EXPROC2:D 
00002
00003
00001
00004
Format: 
DO id 
Parameters: 
id    is the identifier of any stored command. 
Description: 
The DO command performs the attachments to any stored command.  This includes 
attachments saved with the SAVE command and the attachments to any breakpoint 
command whether active or inactive. 
Usage Notes: 
1.  The DO command is itself attachable, and allows an IF specification.  This 
    allows very complex, and possibly recursive, chains of attachments.  The 
    user must take care to avoid recursions which will never exit.  The BREAK 
    key can be used to stop an endless attachment loop. 
00002
00003
00001
00003
Format: 
                                       [ON      ] 
DU[MP][A][L] location[,word count][\f] [OVER fid] ['title'] 
                                       [INTO    ] 
Parameters: 
A    indicates that ASCII translation is desired. 
L    indicates nonsuppresion of duplicate lines is desired. 
location    may be any form of location or position reference. 
word count    defines the number of cells (beginning at location) to be 
dumped.  If word count is omitted, cells beginning from location to the end of 
the memory segment are dumped.  If missing pages are encountered, they are 
reported and the dump continues at the next page.  Word count may be an 
expression. 
f    designates octal 'O' or hexadecimal 'X' format for the dump.  f may also 
be 'C', in which case DUMP becomes the equivalent of DUMPA. 
fid    may be any valid CP-6 file identification. 
'title'    is any character string to be printed at the top of the dump. 
Description: 
The DUMP command dumps a range of memory.  The user may optionally specify 
that: 
o   Each cell be dumped in either octal or hexadecimal format. 
o   The dump output be directed to a destination other than the one currently 
    assigned for DELTA's output. 
o   A title line be printed at the top of the dump. 
o   The width of the dump output be divided in half such that: 
    -   the left half is printed in the specified format (octal or 
        hexadecimal) 
    -   the right half contains the interpretation of all printable characters 
        in ASCII. 
o   Duplicate lines not be suppressed. 
Usage Notes: 
1.  When fid is specified, the run unit must have a reserved DCB slot to be 
    used by DELTA for the duration of the DUMP command.  Absence of the fid 
    option specifies that DELTA will output the dump through the normal output 
    DCB M$DO.  ON will cause an error if the file referenced by fid already 
    exists, OVER will overwrite an existing file, INTO will extend an existing 
    file or create a new one if none exists. 
2.  If fid is LP@WSN, the CP-6 system will release the symbiont file to be 
    printed as soon as the dump is complete; a PRINT command to IBEX is then 
    not needed. 
3.  The form DUMP location\C is equivalent to DUMPA location.  With both forms 
    the dump is octal with ASCII translation. 
4.  To stop a lengthy DUMP printout, depress the break key. 
5.  If location is preceded by a ":", then a substatement and offset must be 
    specified before specifying a word count.  For example: 
        DUMP :100,1,.0, word count 
        DUMP :100,,.0,word count 
00002
00001
00003
EVALUATE
Format: 
EC[HO] 
Description: 
The user may specify that DELTA is to read its commands from some source other 
than the default stream (see the READ command).  The ECHO command allows the 
user to see these commands at the interactive terminal.  When ECHO is in 
effect, all input read by DELTA from other than the interactive terminal is 
written to the M$DO DCB. 
Usage Notes: 
1.  ECHO is a toggle command.  It is reset by the command: 
        KILL ECHO 
2.  ECHO is the initial default. 
00001
00002
00002
Format: 
{EN[D] } [fprg-res] 
{Q[UIT]} 
FEP Parameters: 
fprg-res    will cause the specified FEP program to be terminated. 
Description: 
The commands EN[D] and Q[UIT] cause the current DELTA session to be 
terminated, and returns the user to his command processor (IBEX). 
00001
Format: 
EO[M] 
Description: 
The EOM (end of message) command activates a special character set which 
signals end of message when using the MODIFY command and during program 
stepping.  See HELP (DELTA) EOM_CHARACTERS for a listing of the EOM set, which 
also shows sub-directives that may be used in place of the EOM characters. 
Cross Reference: 
See also the STEP and EVALUATE commands. 
Usage Notes: 
The EOM character set may be disabled with the KILL EOM command.  The default 
is EOM unless you are in stand-alone mode. 
00002
00001
00003
00003
        Several special EOM characters (in addition to /) apply to the open 
        form of the MODIFY command.  If the EOM activation character set has 
        been disabled with the KILL EOM command, a special set of sub-commands 
        is provided to indicate the same activity.  The EOM activation 
        characters along with their substitute sub-commands are shown in the 
        following table. 
        The table is in a three column tabular form as follows: 
  Character      Sub-Command    Action Indicated 
Linefeed       N[EXT]         Open next memory cell for modify.  Cell 
                              will be opened and displayed as if it has 
                              been addressed directly with a MODIFY 
                              command. 
Up Arrow       P[REV]         Open previous cell for modify. 
                              The cell preceding the current cell will 
                              be opened and displayed as if it has 
                              been addressed directly with a 
                              MODIFY command. 
Left Bracket   O[PEN]         Re-open and re-display the 
Left Brace                    last cell addressed by a MODIFY 
                              command.  DELTA remembers the address of 
                              the last cell (if any) referenced in a 
                              MODIFY command. 
Tab Character  Asterisk (*)   Indirect addressing. 
                              Display and open for modification the 
                              cell specified by the contents 
                              of the currently open cell. 
                              The interpretation of the 
                              address contained within the 
                              cell is dependent upon the format of 
                              the current display.  If the 
                              current display is in pointer 
                              format, then the "segid" portion 
                              of the pointer is used to determine 
                              the appropriate segment, 
                              and the word offset portion of 
                              the pointer determines the 
                              offset within the segment.  If the 
                              current display is in relative 
                              format, then the right half (the 
                              least significant eighteen bits) 
                              of the currently open cell is 
                              assumed to specify an address 
                              in the instruction segment.  If the 
                              current display is in other 
                              than pointer format, then the 
                              left half (the most significant 
                              eighteen bits) of the 
                              currently open cell is assumed 
                              to specify an address in the 
                              instruction segment. 
[\f]/          None           Same as * except do not open the cell for 
                              modification.  Optionally a format 
                              specifier may be used. 
None           *L[\f]         Treat left 18 bits as an address 
                              regardless of displayed format. 
                              Optionally a format specifier 
                              may be used. 
None           *R[\f]         Same as *L except that the right half (the 
                              least significant eighteen bits) of the 
                              currently open cell is assumed to 
                              specify an address in the instruction 
                              segment.  Optionally a format specifier 
                              may be used. 
None           *P[\f]         Treat contents of the currently 
                              open cell as a pointer regardless of the 
                              format in which it was displayed.  Take 
                              same action as for the tab EOM character 
                              or the * sub-command.  Optionally a 
                              format specifier may be used. 
FEP EOM 
Characters: 
None           *L[\f]         Invalid for FEP programs. 
None           *R[\f]         Invalid for FEP programs. 
None           *P[\f]         Treats the contents of the 
                              currently open cell (2 words) as a 
                              pointer.  Take the same action as 
                              for the tab EOM character or the 
                              * subcommand.  Optionally a 
                              format specifier may be used. 
None           *SP[\f]        Treats the contents of the 
                              currently open cell (1 word) as a 
                              16 bit address.  Take the same action 
                              as for the tab EOM character or the 
                              * subcommand.  Optionally a format 
                              specifier may be used. 
Tab Character  Asterisk (*)   Indirect Addressing. 
                              Display and open for modification 
                              the cell(s) starting at the 
                              address specified by the contents 
                              of the currently open cell(s).  The 
                              interpretation of the address 
                              contained within the cell(s) is 
                              dependent upon the format of the 
                              current display.  If the current 
                              display is in instruction format, 
                              pointer format or relative format, 
                              the least significant 20 bits of 
                              the currently open cell (2 words) 
                              is assumed to specify an address. 
                              If the current display is in octal, 
                              unsigned integer, signed integer, 
                              bit, or hex format, the contents of 
                              the currently open cell (1 word) 
                              is assumed to specify an address. 
                              Other formats will be errored. 
For more information, enter ? . 
Usage Notes: 
1.  When in the modify-active mode, the sub-command NEXT, PREV, OPEN, and any 
    of their abbreviations may be classified by program symbols with the same 
    spelling.  When in doubt about a possible conflict, the user can use the 
    activation character or leave the modify-active mode (return key) before 
    issuing any of these sub-commands. 
2.  All of the MODIFY sub-commands may be issued as major commands in which 
    case their action is based on the last MODIFY command issued. 
3.  New values for the open cell can be expressed as octal or decimal numbers, 
    simple expressions, address expressions, or instructions in mnemonic form. 
    When the new value is specified followed by a carriage return, the value 
    is stored in the currently open cell, and DELTA leaves the modify-active 
    mode.  For example: 
    >MODIFY CPA+.265\I 
    CPA+.265 / LDPO 3,,PR2 M>TRA CPA+.324 
    >MODIFY $DS1->.101 
    $LS4->.101 / .236 M>$L+.40000 
    If, however, the specifications of the new value is followed by one of the 
    characters N, <LF>, P, |, ^, O, *, or <TAB>, then the new value is stored 
    in the currently open cell and action is taken according to the 
    descriptions in Table 6-1. 
4.  These characters may optionally be preceded by a format specification 
    indicating the desired format to be used for the requested display.  These 
    characters, with the optional format specification, may be entered either 
    following or in lieu of the new value for the currently open cell.  When 
    specified in lieu of any new value, the currently open cell is not 
    modified.  For example: 
    Command                          Explanation 
    >MODIFY .1023                    Add .4000 to current cell 
    .1023 / .501 M>$L+.4000 [        and re-display it. 
    .1023 / .4501 M><LF>             Display the next cell. 
    .1024 / .777777777742 M>\S[      Re-display in signed binary 
    .1024 / -30 M>                   (decimal). 
    >MODIFY .2415 
    .2415 / .5006001 M> <TAB>        Display indirect through 
                                     current cell. 
    .5 / .0 M>.2415\P/               Try it again, this time as 
                                     a pointer. 
    .2415 / .5-0-0,$LS1 M> <TAB>     ...then go indirect. 
    $LS1->.5 / .120 M> 
    Although the addresses used in the above examples have been simply 
    expressed, the MODIFY command will accept any address specification that 
    can be resolved to a segment and word offset within that segment.  When an 
    address is specified by using variable names, all the qualification rules 
    that apply to the DISPLAY or LET command also apply to MODIFY.  However, 
    unlike DISPLAY or LET, only the word address portion of the variable 
    information is used.  For example, the MODIFY command will accept a PL-6 
    variable that is defined as an automatic variable in the current auto 
    frame of type BIT(1); but when displayed the whole word containing the 
    BIT(1) variable will be printed and the address will be printed as a word 
    offset in the segment containing the automatic stack for the current 
    process.  For example: 
        >DISPLAY BITVAR 
        BITVAR = '1'B 
        >MODIFY BITVAR 
        $LS4->.106 / .4000012623100 M> 
    When specifying addresses in the run unit's procedure (position reference) 
    when using the debug schema information (statement numbers, internal entry 
    names, and statement levels) it is necessary to precede the address 
    specification with a colon.  This causes the address to be interpreted 
    exactly as described for the AT and GO commands.  For example: 
        >MODIFY 258                         (treated as decimal word 
        .410 / .104213 M>                   offset in IS) 
        >MODIFY :258                        (treated as statement 258 
        FMN$OPNF+.32 :258 / LDP4 0,,PR0 M>  in the current external 
                                            procedure) 
00001
Format: 
ERR[FID] fid 
Description: 
The ERRFID command changes the default error message file for \J displays. 
Example: 
    !DELTA 
    DELTA E03 here (No RU associated) 
    >E .152520000010\J 
     = MUP-00001-0 
    >ERRFID MUPPET.X "MUPPET has it's error messages inside the ru file 
    >E .152520000010\J 
     = MUP-00001-0   There are currently no available fprg slots. 
    >END 
    ! 
00001
00002
Format: 
E[VALUATE] expression[\f] 
Parameters: 
expression    may be: 
o   A symbolic name (e.g., EVALUATE SYMBOL). 
o   A symbolic name plus offset (EVALUATE SYMBOL+.10). 
o   Simple octal or decimal addresses (EVALUATE 1329\O). 
o   Simple address expressions with plus (+), minus (-), multiply (*), divide 
    (%), logical AND (&), logical OR (|), shift left (<<), and shift right 
    (>>).  (EVALUATE .60630>>2+3). 
o   Simple pointer-qualified expressions using SYMDEFs or ENTDEFs even when 
    schema usage is disabled.  (EVALUATE B$JIT$->.12). 
o   All forms of pointer and descriptor qualified references 
        (EVALUATE $LS2->MYSTRUCT.NEXT->MS.SS.ITEM). 
o   Any expression that can be resolved and expressed within a 36-bit word. 
    This includes: 
        Binary values (signed or unsigned). 
        Bit strings up to 36 bits. 
        Character strings up to 4, 9-bit bytes. 
        GMAP6 assembler instructions. 
o   If a format is specified, it does not change the default format for the 
    MODIFY command.  f is one of the format specifiers from which can be 
    displayed via HELP (DELTA) FORMAT PARAM 
Description: 
This command is used to: 
o   Perform simple arithmetic. 
o   Reduce an address expression to its simplest form. 
o   Obtain an address expression for use in some word oriented command. 
o   Relate memory addresses to symbolic locations and positions within a run 
    unit. 
o   Convert between numbering systems. 
Example: 
    Command                             Explanation 
    EVALUATE 35+.13\U                   Do arithmetic with mixed 
    = 46                                numbering systems. 
    EVALUATE .40<<18                    Perform logical arithmetic. 
    = .40000000 
    EVALUATE $LS5->MYSTRUCT.NEXT->MS    Reduce this expression to 
      .3712                             its simplest form. 
    EVALUATE .2011\R                    To what part of my run unit 
    = PROG3+.5 :12(LOOP)                does word .2011 (of the IS) 
                                        relate? 
    EVALUATE PROG3                      Display the octal offset of 
    = .2004                             PROG3 within the IS. 
    EVALUATE J                          What expression may I use to 
    = $LS4->.7                          address the symbol J which is 
                                        not contained within the IS? 
    EVALUATE LDQ P3DEF+.12,X3,PR2       What is the octal representation 
    = .200422236113                     of this symbolic GMAP6 
                                        instruction? 
Usage Notes: 
1.  There is no operator precedence; operations are performed left to right. 
2.  Default format for output of EVALUATE is octal unless changed by the 
    FORMAT EVALUATE command. 
3.  Format specification is ignored if the resultant address is not in the 
    Instruction Segment (IS), that is, cannot be expressed as a value.  When 
    this occurs, the output is always segid->octal offset (e.g., $LS6->.1236). 
4.  The EOM (activation) character '=' can be used in place of EVALUATE.  The 
    format is: 
        expression[\f]= 
    For example: 
        35+.13\U=46  (The 46 is supplied by DELTA). 
Cross Reference: 
See the FORMAT command. 
00005
00002
00003
00001
00004
EXIT
Summary descriptions of execution control commands appear at the next levels 
of this HELP message.  Type ? or ?? for a listing of these descriptions or for 
a specific summary description, type 
HELP (DELTA) EXECUTION_CONTROL execution_control_command 
where execution_control_command is one of the following:  ALIB, AT, BREAK, 
EXIT, GO, GOSTEP, GOTRAP, GOTRAPSTEP, ON_CALL, ON_X_CALLS, ON_NODE, ON_NODES, 
UNSHARE, STEP, WHEN, XCON. 
For a categorized list of commands, type HELP (DELTA) COMMANDS. 
The command summaries are presented in tabular form as follows: 
  Command       Function 
  ALI[B] 
                Specifies return/altreturn from M$ALIB call to DELTA. 
  A[T] 
                Sets an instruction breakpoint. 
  B[REAK] 
                Passes control to user interrupt routine. 
  EX[IT] 
                Exits from a run unit invoked by M$LINK and returns to the 
                linking program, or continues an M$LDTRC or M$SAVE. 
  G[O] 
                Proceeds with program execution. 
  G[O] S[TEP] 
                Goes to a specified location and executes one step. 
  G[O] T[RAP] 
                Passes control to user's event handling routine when DELTA has 
                been entered for an exceptional or asynchronous event. 
  G[O] T[RAP] ST[EP] 
                Same as GOTRAP except that one step is executed. 
  O[N] C[ALL] 
                Sets breakpoints on a specific procedure call. 
  O[N] [X] C[ALLS] 
                Sets breakpoints on all procedure calls.  If X is specified, 
                sets breakpoints only on external procedure calls. 
  O[N] N[ODE] 
                Sets a breakpoint on a specific overlay. 
  O[N] N[ODES] 
                Sets breakpoints on all overlays. 
  S[TEP] 
                Steps by statement or instruction. 
  UNSH[ARE] 
                Unshares an autoshared program and/or library so the user can 
                have execution control. 
  W[HEN] 
                Sets a data breakpoint. 
  XC[ON] 
                Passes control to the user's exit control procedure simulating 
                an exit condition. 
00001
00002
00003
00004
00005
00006
00007
00008
00006
00007
00008
00009
00011
00012
00010
00009
00011
00012
00010
00013
00014
00015
00016
Summary descriptions of execution tracing commands appear at the next level of 
this HELP message.  Type ? or ?? for a listing of these descriptions or for a 
specific summary description, type 
HELP (DELTA) EXECUTION_TRACING execution_tracing_command 
where execution_tracing_command is one of the following:  HISTORY, PLUGH, 
TRACETRANSFERS, TRACEXCALLS. 
For a categorized list of commands, type HELP (DELTA) COMMANDS. 
The command summaries are presented in tabular form as follows: 
  Command       Function 
  H[ISTORY] 
                Displays contents of history buffer (filled by TRACE). 
  PL[UGH] 
                (Acronym for "Procedure List Used to Get Here").  Traces back 
                through the automatic stack and lists the return addresses 
                leading to the arrival at the current procedure point. 
  T[RACE] T[RANSFERS] 
                Traces all transfer instructions. 
  T[RACE] [X] C[ALLS] 
                Traces entry to all procedures.  If X is specified, trace 
                entry to external procedures only. 
00001
00002
00003
00004
00003
00004
Format: 
EX[IT] 
Description: 
DELTA checks to ensure that the user does not force an exit condition while 
the run unit is already in exit control, as this will cause the program to be 
run down, and control to return to IBEX.  This feature makes it difficult for 
a user to terminate a debug session unintentionally.  However, there are three 
conditions which require an exit from exit control to continue debugging: 
M$SAVE, M$LDTRC, and exit from an M$LINKed-to program.  The EXIT command is 
used to continue an M$SAVE or M$LDTRC after the final exit from exit control. 
In an M$LINKed-to program, EXIT is used within the exit control routine, or 
after the first exit if the program has no exit control routine. 
Usage Notes: 
1.  The EXIT command is not allowed for FEP programs. 
00001
00002
FIND
For information on how to start debugging programs that run in the FEP, see 
the topics:  DEBUG_TP_FORMS, DEBUG_FPRGS, DEBUG_HANDLERS. 
Tips for debugging in the FEP include the following subtopics:  FEP_DEFAULTS, 
COMMAND_OPTIONS_FOR_FEP, DISTINGUISHED_NAMES, SYSTEM_AREAS, 
COMMAND_WORK_AREAS, SPECIAL_NOTES.  Enter ? or ?? for tips, or request them by 
entering HELP (DELTA) FEP_DEBUG_TIPS subtopic . 
Defaults when Debugging FEP Programs 
o   A number preceded by a period is a hexadecimal number when debugging FEP 
    programs (it is an octal number when debugging Host programs). 
o   A maximum of 20 breakpoints are allowed for a single FEP program. 
    Command Options for FEP Debugging 
    Several DELTA commands have options which pertain to debugging FEP 
    programs.  Below is a list of the commands and a summary of the FEP and 
    Host options.  For more detail, see the desired command. 
    Command            New Options 
    GO                 fprg-res - GO a specific FEP program 
                       ALL      - GO ALL FEP programs 
                       HOST     - GO the host program 
    QUIT               fprg-res - QUIT a specific FEP program 
    KEEP/TRAP/IGNORE   fprg-res - identifies a specific FEP program 
                       ALL      - identifies ALL FEP programs 
                       HOST     - identifies the Host program 
    KILL               DELTA fprg-res - disassociates DELTA from the 
                                        specified FEP program 
    SHOW               FPRG's - shows state of all FPRGs - if 
                                stopped, shows current IC 
                       fprg-res - shows state of a specific FEP 
                                  program 
    MODIFY             M[ODIFY] D[OUBLE] [W[ORD] - Modify two 
                                                   words - specifically 
                                                   tells DELTA you want 
                                                   to modify two words. 
Distinguished Names 
DELTA recognizes many distinguished names related to FPRGs as syntactical 
components of DELTA's commands.  These names are listed below. 
Included are the machine registers visible to programming and usage and 
default formats for display.  D, L, M, and P indicate DISPLAY, LET, MODIFY, 
and POINTER usage respectively.  When one of these is used in a pointer 
qualified reference, it must be the leftmost name in the expression. 
                                                                 DEFAULT 
    NAME            REFERS TO:                          USAGE    FORMAT 
    $B1 to $B7      Corresponding 16-bit Base Register  P,D,L,M  Hex 
    $R1 to $R7      Corresponding 16-bit General          D,L,M  Hex 
                    Register 
    $M1 to $M7      Corresponding 8-bit Mode Control      D,L,M  Hex 
                    Register 
    $T              Stack address Register (16 bits)      D,L,M  Hex 
    $S              System Status Register (16 bits)      D,L,M  Hex 
    $               Address associated with a trap        D,L,M  Hex 
                    (20 bits) 
    $IV             Contents of $B3 at the time of a      D,L,M  Hex 
                    trap (16 bits) 
    $Z              Z-word-miscellaneous information      D      Hex 
                    relative to a trap (16 bits) 
    $ASV            Address Space Vector - the base       D      Hex 
                    of an MPU image in memory (20 
                    bits) 
    $CI             CIP Indicator Register (8 bits)       D,L,M  Hex 
    $IND            Indicator Register (8 bits)           D,L,M  Hex 
    $IC or $P       Instruction Counter (20 bits)         D,L,M  Relative 
    $ISR1 to $ISR7  Instruction Segment                   P,D    Descriptor 
    $AUTO           Auto Segment                          P,D    Pointer 
    $DS1 to $DS4    Corresponding LCP6 Data Segment       P,D    Descriptor 
                    descriptor 
Enter ?? for additional distinguished names. 
System Areas 
This group of distinguished names are used exclusively as pointers to various 
system areas. 
    NAME          REFERS TO: 
    $ROSEG        Read-Only-Segment 
    $RDBR         Remote descriptor array 
    $TSA          Trap Save Area 
    $DCBn         Refers to DCB #n 
Special Notes 
o   If the host program closes the DCB that is connected to the FEP program, 
    the user must say USE HOST and then KILL DELTA fprg-res in order to exit 
    the FEP program and end the host program normally. 
o   A user who has FMR privilege turned on will be allowed to debug anything. 
    Otherwise, the user must match the FEDBACCN in the SUPER authorization of 
    the user being debugged. 
00002
00001
00003
00005
00004
Format: 
F[IND][N[OT]] pattern1 [F[ROM] range] [U[NDER] mask1] 
    [S[UB] pattern2] [U[NDER] mask2] 
Parameters: 
NOT    specifies a search for cells whose contents are NOT equal to pattern1. 
pattern1,pattern2    may be specified in any form that can be resolved by 
DELTA into a 36-bit pattern.  This includes: 
o   Octal or decimal literals.  These are converted to their binary 
    equivalents (right-justified with zero-fill). 
o   Bit string literals.  These are left-justified with zero-fill when 
    necessary. 
o   Character string literals.  These are truncated to four characters, 
    blank-fill on the right if necessary. 
o   Octal string literal.  These are left-justified with zero-fill where 
    necessary.  Truncation to a 36-bit value is also performed when necessary. 
o   GMAP6 assembler instruction expression.  Single word instructions only. 
mask1,mask2    may be any of the above literal types, but may not be a GMAP6 
instruction. 
range    is expressed in the form: 
    location[,word count] 
    where location may be any valid position or location reference. 
    word count    defines the number of cells to be searched.  If omitted, all 
    cells from location to the end of the memory segment are searched. 
Description: 
The FIND command searches a specified range of cells for a specified 36-bit 
pattern, and reports the address of every cell within the range in which the 
pattern was found.  The user may optionally specify a secondary pattern with 
which DELTA is to replace every occurrence of the pattern being sought.  Both 
the search and the substitution may be conducted under mask.  If the search is 
conducted under mask, the contents of each cell in the range is logically 
ANDed with the search mask in a work cell to select those bits which are to be 
considered in the comparison.  The search pattern is also masked in the same 
way.  The work cell is then compared with the masked search pattern.  When the 
comparison proves equal, then: 
o   If substitution is indicated and a substitution mask is not present, DELTA 
    replaces the contents of the entire cell with the secondary pattern, and 
    reports the location/position. 
o   If substitution is indicated and a substitution mask is present, DELTA 
    selects those bits from the secondary pattern which have corresponding 
    bits set in the substitution mask, inserts them into the cell, and then 
    reports the location/position. 
o   If substitution is not specified the position/location is reported along 
    with the cell's contents. 
DELTA then continues the search until the end of the range is reached. 
Usage Notes: 
1.  To stop a lengthy FIND press the break key.  DELTA will print out the 
    address of the next cell to be compared, and stop.  There is no way to 
    continue the search without issuing another FIND command. 
2.  The FIND command is not allowed for FEP programs. 
Special Considerations: 
Two of the syntax components of the FIND command are associated with certain 
of DELTA's distinguished names.  These assume a default value when DELTA is 
invoked which can be changed in two different ways: 
o   Implicitly specified as a syntax component in the FIND command. 
o   When referenced by its distinguished name in a MODIFY or LET command. 
    SYNTAX         DISTINGUISHED 
    COMPONENT      NAME              DEFAULT VALUE 
    range          $FRANGE           Entire instruction segment (only 
                                     modifiable syntactically) 
    mask1          $FMASK            .777777777777 (-1) 
The SUB pattern and mask are not remembered by DELTA and must be specified 
each time you issue the FIND command and desire substitution to take place. 
For example: 
    PATTERN              EXPLANATION 
    FIND .7              FIND an octal literal (binary 7). 
    FIND 'ABCD'          FIND a character string literal. 
    FIND TRA :HERE       FIND a GMAP6 assembler instruction which is a 
                         transfer to the statement label HERE in the 
                         current compile unit. 
    FIND TSX1 HERB       FIND a GMAP6 assembler instruction which is a 
                         transfer and set index to the external entry 
                         name HERB. 
    FIND NOT 0           Find cells which do not contain zero. 
    RANGE                EXPLANATION 
    FROM HERE,50         50 words, beginning with the data cell named HERE. 
    FROM 0               Entire Instruction Segment (IS). 
    FROM $LS4->0         Entire Automatic Stack ($LS4, $DS1). 
    FROM $TCB->0,66      Top TCB frame (66 words long). 
    FROM MYPROG:20,.30   30 octal words from statement 20 in MYPROG. 
    FROM .50,.20         20 octal words beginning at location .50 in the 
                         Instruction Segment ($LS0). 
FIND under default mask and report only: 
    FIND -1 FROM TABLE,100 
FIND under mask and report only: 
    FIND TRA 0 FROM MAINLINE,1000 UNDER .777000 
    The command is to find all TRA instructions within the range. 
    Mask is:  .000000777000 
    TRA op code is: xxxxxx710xxx 
    The 0 in TRA is necessary even though it does not enter into the 
    comparison.  TRA is a GMAP6 instruction; TRA alone is a symbol name. 
FIND under default mask and substitute: 
    FIND TRA :HERE SUB TRA :THERE 
This command causes DELTA to replace all branches to HERE with branches to 
THERE within the default range. 
FIND under mask and substitute under mask: 
    FIND '4'O FROM WORD_TABLE,50 UNDER .700000000000 
    SUB '5'O UNDER .700000000000 
This command causes DELTA to find each word in the first 50 words of 
WORD_TABLE which contain a 4 in its high-order octal digit and replaces only 
that digit with a 5.  '4'O and '5'O are expressed as octal literals which are 
left-justified. 
00004
00002
00001
00004
00003
Format: 
FOR[MAT] {M[ODIFY]  } \f 
         {E[VALUATE]} 
Parameters: 
f    is one of the following specifiers: 
AR, BIT, CHAR, DESCR, EPTR, FLOAT, INSTR, JDE, OCTAL 
PTR, REL, SBIN, TIME, UBIN, VECTOR, X, ZERO 
This information can be accessed in several ways. 
By typing a ? or ?? after this message all specifiers will 
be displayed.  To specify a particular specifier, type: 
HELP (DELTA) FORMAT specifier 
Descriptions and an example are in a tabular form as follows: 
Specifier       Meaning                       Example 
A[R]            Display left 24 bits of a 
                word as word-char-bit.        .35-2-5 
B[IT]           Display in binary format.     '010110100'B 
C[HAR]          Character.                    'ABCD' 
D[ESCR]         Descriptor.                   .46000,BD=.75777-3, 
                                              FL=.643,WSR=7,TY=0 
EB[CDIC] 
                EBCDIC Character              '694E' 
E[PTR]          Displays left half of word 
                as ENTDEF+.offset[:stmnt#]    PROGB+.374 :27 
F[LOAT]         Floating point binary. 
                Single precision for 
                36-bit items, double 
                precision for 72-bit 
                items.                        5.789604E+76 
I[NSTR]         Assembly language 
                instruction.                  LDQ .1,DL 
J[DE]           JIT Dot ERR.  Displays 
                a one word value as a         FMN-M00113-0 
                standard CP-6 error           File does not exist 
                code and associated 
                message level if any. 
O[CTAL]         Octal digits with leading 
                zeroes suppressed.            .1024 
P[TR]           Pointer. word-char-bit, 
                segid.                        .35-2-7,$LS0 
R[EL]           Relative.  Primary ENTDEF+ 
                offset[,:stmnt#, substmnt, 
                offset] or SYMDEF + offset.   PROGA+.6 :12,,.1(LOOP) 
REM[EMBER]      Remember.                     TEST:6(LABEL)[ASSIGNMENT] 
                                              (+.4) 
S[BIN]          Signed binary (decimal).      -357 
T[IME]          Convert UTS to display 
                format.                       13:52:36.82 06/25/79 
U[BIN]          Unsigned binary (decimal).    357 
V[ECTOR]        Vector.                       .6245-0-0,$LS0,BD=.14-2, 
                                              FL=.777,TY=NORMAL SHRINK 
X               Hexadecimal.                  'F100CS40D'X 
X1              Pseudo-hexadecimal. 
                Leading bit of each byte 
                ignored.                      'F0F8F6F4'X 
Z[ERO]          Displays a word value in      .000000001024 
                Octal with leading zeroes. 
Description: 
The FORMAT command establishes the default display for the EVALUATE and MODIFY 
commands.  The normal display format for these commands is octal with leading 
zeros suppressed. 
00002
00001
Format: 
     [position           ] 
G[O] [AL[L]              ] 
     [H[OST] [position]  ] 
     [fprg-res [position]] 
Parameters: 
position    will cause execution to resume at the specified position.  If not 
specified, position is assumed to be the current value of $IC. 
FEP Parameters: 
ALL    causes program execution to resume at the current position for all 
programs - Host and FEP. 
HOST    causes program execution to resume either at the current position or 
at a specified position for the Host program. 
fprg-res    causes program execution to resume either at the current position 
or at a specified position for the specified FEP program. 
Description: 
This command is used to resume program execution either at the current 
position or at a specified position. 
Example: 
    Command                     Explanation 
    GO 100                      Resume execution at statement number 100 of 
                                the current ECU. 
    GO READ_REC                 Resume execution of the statement labeled 
                                READ_REC in the current ECU. 
    GO ECUB:100                 Resume execution at statement number 100 
                                of ECUB. 
    AT 100;DISPLAY X; GO        When control reaches statement 100 of the 
                                current ECU, display X and continue 
                                execution. 
    AT 100 IF A > B ;DISPLAY X; When control reaches statement number 100 
    GO 200 IF A EQ 40; GO       of the current ECU, if A is greater than B, 
                                then display X and continue execution at 
                                200 if A is equal to 40 or at 100 if A is 
                                not equal to 40. 
Usage Notes: 
1.  Users of higher level language processors are warned that some language 
    compilers generate optimized code.  This means that some statements are 
    combined by the compiler, and cannot be executed out of order if the 
    proper results are to be obtained.  For example: 
        19:   B = 6 
        20:   A = B+5+D 
        21:   C = B+5+E 
    The compiler might compute the value of B+5 in statement 20 and save it in 
    a temporary storage location.  For statement 21, the value of B+5 is 
    fetched from the saved cell, and used in the equation.  B+5 is not 
    recomputed.  This saves time and reduces the amount of code produced. 
    However, if a breakpoint is placed at 20, and a GO 21 is performed, 
    statement 20 is never executed.  The value B+5 is never computed and a 
    possible wrong answer will be produced by statement 21. 
    This example is simple, but shows that the GO [position] command should be 
    used with care in code produced by optimizing compilers.  In general, at 
    least for PL-6, FORTRAN and COBOL, it is safe to "GO label" (paragraph 
    name for COBOL).  The compiler is expecting multiple entry paths to that 
    statement, and will not generate code that relies on previous statements. 
00002
00003
00004
00001
00004
Format: 
           [position           ] 
G[O]S[TEP] [H[OST] [position]  ] 
           [fprg-res [position]] 
Parameters: 
position    will cause execution to resume at the specified position. 
FEP Parameters: 
HOST    will cause execution to resume at the current position or specified 
position in the Host program. 
fprg-res    will cause execution to resume at the current position or at the 
specified position in the specified FEP program. 
Description: 
This command performs the GO function but, at the same time, directs that a 
single step (instruction or statement) be performed. 
Usage Notes: 
1.  One step will be performed at position.  This command is equivalent to: 
        LET $IC position 
        STEP 
00002
00003
00001
00003
Format: 
           [position           ] 
G[O]T[RAP] [H[OST] [position]  ] 
           [fprg-res [position]] 
Parameters: 
position    will cause execution to resume at the specified position. 
FEP Parameters: 
HOST    causes control to be transferred to the Host program's exceptional 
condition routine for the condition that caused entry to DELTA. 
fprg-res    causes control to be transferred to the specified FEP program's 
exceptional condition routine for the condition that caused entry to DELTA. 
Description: 
This command transfers control to the exceptional condition routine for the 
condition that caused entry to DELTA.  (This command is used to enter the TRAP 
routine and the EVENT routine.) 
Usage Notes: 
1.  When the command is issued, the information about the exceptional 
    condition is moved into place in the TCB.  If position is specified, the 
    Instruction Counter (IC) value in the TCB is set to reflect that position. 
    Execution resumes at the handler for the exceptional condition that caused 
    entry to DELTA. 
2.  For FEP programs: 
    If position is specified, the Instruction Counter (IC) value in the TSA is 
    set to reflect that position.  Execution resumes at the specified handler 
    for the exceptional condition that caused the specified FEP program's 
    entry to DELTA. 
00002
00003
00001
00003
Format: 
                 [position           ] 
G[O]T[RAP]ST[EP] [H[OST] [position]  ] 
                 [fprg-res [position]] 
Parameters: 
position    will cause execution to resume at the specified position. 
FEP Parameters: 
HOST    will cause execution to resume at the current position or the 
specified position in the Host program. 
fprg-res    will cause execution to resume at the current position or the 
specified position in the specified FEP program. 
Description: 
This command performs the same function as the GOTRAP command except that the 
step level of operation is placed into effect. 
Usage Notes: 
1.  One step is performed from the beginning of the exceptional condition 
    handler for the condition which caused entry to DELTA.  If position is 
    specified, the IC value in the TCB frame for the exceptional condition is 
    set to reflect that position. 
2.  For FEP programs: 
    If position is specified, the IC value in the TSA frame for the 
    exceptional condition is set to reflect that position. 
00002
00003
00001
00003
GOSTEP
GOTRAP
GOTRAPSTEP
HISTORY
Format: 
{H|HELP} [(processor)][ TOPICS ][ keyword1 ][ - ][ keyword2] 
Parameters: 
processor    specifies a program or processor that has an associated helpfile 
in the form HELP:processor:[.[account][.password]].  The default is the 
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
Any standard HELP file (even those for other processors) can be accessed with 
the HELP command. 
Example: 
    HELP (DELTA) RUM 
Usage Notes: 
1.  The standard CP-6 HELP facility is used by DELTA so the user can get help 
    on any other CP-6 processor by entering: 
        HELP (processor) [TOPICS] [keyword1] [-] [keyword2] 
00002
00003
00004
00001
00004
A 
  ACTIVE/INACTIVE command - 
      HELP HOUSEKEEPING ACTIVE_INACTIVE 
      HELP ACTIVE_INACTIVE 
  addressing and symbol control commands - 
      HELP DESCRIPTOR_QUALIFIED_REFERENCES EXAMPLE: 
  ALIB command - 
      HELP EXECUTION_CONTROL ALIB 
      HELP ALIB 
  ALL keyword - 
      HELP KILL_SHOW PARAMETERS: 
  ALTERNATE VARIABLES command - 
      HELP HOUSEKEEPING ALTERNATE_VARIABLES 
      HELP ALTERNATE_VARIABLES 
  ALTERNATE VARIABLES keyword - 
      HELP KILL_SHOW PARAMETERS: 
  ANLZ command - 
      HELP MODE_CONTROL ANLZ 
      HELP ANLZ 
  ANLZ keyword - 
      HELP KILL_SHOW PARAMETERS: 
  AR specifier - 
      HELP FORMAT PARAMETERS: 
  Array - 
      HELP ARRAY 
  Associating DELTA at Program Invocation - 
      HELP DELTA_AT_PROGRAM_INVOCATION 
  Asterisk, EOM sub-command - 
      HELP EOM_CHARACTERS 
  AT command - 
      HELP EXECUTION_CONTROL AT 
      HELP AT 
  ATS keyword - 
      HELP KILL_SHOW PARAMETERS: 
  attachments - 
      HELP IF_ATTACHMENT EXAMPLE: 
B 
  BIT specifier - 
      HELP FORMAT PARAMETERS: 
  Braces - 
      HELP NOTATION_CONVENTIONS BRACES 
  Brackets - 
      HELP NOTATION_CONVENTIONS BRACKETS 
  BREAK command - 
      HELP EXECUTION_CONTROL BREAK 
      HELP BREAK 
  break key - 
      HELP COMMUNICATIONS_WITH_DELTA 
  BYPASS command - 
      HELP HOUSEKEEPING BYPASS 
      HELP BYPASS 
  BYPASS keyword - 
      HELP KILL_SHOW PARAMETERS: 
C 
  Capital Letters - 
      HELP NOTATION_CONVENTIONS CAPITAL_LETTERS 
  CHAR specifier - 
      HELP FORMAT PARAMETERS: 
  Characters, special - 
      HELP NOTATION_CONVENTIONS NUMBERS 
  Command Options for FEP Debugging - 
      HELP COMMAND_OPTIONS_FOR_FEP 
  command stream - 
      HELP READ PARAMETERS: 
  commands - 
      HELP PROCESSOR 
  Communications with DELTA - 
      HELP COMMUNICATIONS_WITH_DELTA 
  COPY command - 
      HELP HOUSEKEEPING COPY 
      HELP COPY 
  COPY keyword - 
      HELP KILL_SHOW PARAMETERS: 
D 
  data addresses - 
      HELP SYMBOLIC_ADDRESSING 
  data names - 
      HELP SYMBOLIC_ADDRESSING 
  DEBUG Command (FEP Program) - 
      HELP DEBUG_COMMAND_(FEP_PROGRAM) 
  DEBUG Command (TP Forms Program) - 
      HELP DEBUG_FORMS 
  DEBUG Command (TP Station) - 
      HELP DEBUG_TP_STATION 
  Debug mode - 
      HELP PATCHING 
  Debugging a Specified SYSID on a Specified FEP - 
      HELP BY_SYSID 
  Debugging DCB-Connected FEP Programs - 
      HELP DEBUG_FPRGS 
  Debugging Forms Programs - 
      HELP DEBUG_TP_FORMS 
  Debugging Handlers - 
      HELP DEBUG_HANDLERS 
  DEF keyword - 
      HELP KILL_SHOW PARAMETERS: 
      HELP KILL_SHOW PARAMETERS: 
  defaults - 
      HELP DESCRIPTOR_QUALIFIED_REFERENCES EXAMPLE: 
  Defaults when Debugging FEP Programs - 
      HELP DEBUG_FEP_DEFAULTS 
  DEFINE command - 
      HELP HOUSEKEEPING DEFINE 
      HELP SYMBOLIC_ADDRESSING 
      HELP DEFINE 
  DELTA invoking - 
      HELP INVOKING_DELTA 
  DELTA keyword - 
      HELP KILL_SHOW PARAMETERS: 
  DELTA Overview - 
      HELP PROCESSOR 
  DESCR specifier - 
      HELP FORMAT PARAMETERS: 
  Descriptor-Qualified References - 
      HELP DESCRIPTOR_QUALIFIED_REFERENCES 
  DISPLAY command - 
      HELP MEMORY_DISPLAY DISPLAY 
      HELP DISPLAY 
  distinguished names - 
      HELP DESCRIPTOR_QUALIFIED_REFERENCES 
      HELP DISTINGUISHED_NAMES 
  DO command - 
      HELP HOUSEKEEPING DO 
      HELP DO 
  DUMP command - 
      HELP MEMORY_DISPLAY DUMP 
      HELP DUMP 
  dumping - 
      HELP DUMP 
      HELP PMD USAGE_NOTES: 
E 
  ECHO command - 
      HELP HOUSEKEEPING ECHO 
      HELP ECHO 
  ECHO keyword - 
      HELP KILL_SHOW PARAMETERS: 
  ECU - 
      HELP EXTERNAL_COMPILE_UNIT 
  EDIT - 
      HELP READ EXAMPLE: 
  EDIT file - 
      HELP READ EXAMPLE: 
  Elementary Item - 
      HELP ELEMENTARY_ITEM 
  END command - 
      HELP MISC END 
  End-of-Message Characters (EOM) - 
      HELP EOM_CHARACTERS 
  END/QUIT command - 
      HELP ANLZ DESCRIPTION: 
  END/QUIT Commands - 
      HELP END_QUIT 
  Entry Name - 
      HELP ENTRY_NAME 
  EOM - 
      HELP COMMUNICATIONS_WITH_DELTA 
  EOM character - 
      HELP COMMUNICATIONS_WITH_DELTA 
  EOM characters - 
      HELP EOM CROSS_REFERENCE: 
      HELP EOM_CHARACTERS 
  EOM command - 
      HELP HOUSEKEEPING EOM 
      HELP EOM 
  EOM commands - 
      HELP EOM USAGE_NOTES 
  EOM keyword - 
      HELP KILL_SHOW PARAMETERS: 
  EPTR specifier - 
      HELP FORMAT PARAMETERS: 
  ERRFID - 
      HELP MISC ERRFID 
  ERRFID Command - 
      HELP ERRFID 
  EVALUATE command - 
      HELP MEMORY_DISPLAY EVALUATE 
      HELP EVALUATE 
  exceptional conditions - 
      HELP KILL_SHOW DESCRIPTION: 
  execution control - 
      HELP SAD USAGE_NOTES 
  execution control commands - 
      HELP SAD USAGE_NOTES 
  Execution tracing commands - 
      HELP UNSHARE DESCRIPTION: 
  EXIT command - 
      HELP EXECUTION_CONTROL EXIT 
      HELP EXIT 
  External Compile Unit - 
      HELP EXTERNAL_COMPILE_UNIT 
F 
  fids - 
      HELP READ PARAMETERS: 
  FIND command - 
      HELP MEMORY_DISPLAY FIND 
      HELP FIND 
  FLOAT specifier - 
      HELP FORMAT PARAMETERS: 
  FORMAT command - 
      HELP HOUSEKEEPING FORMAT 
      HELP FORMAT 
  Format For Position - 
      HELP FORMAT_FOR_POSITION 
  FORMAT keyword - 
      HELP KILL_SHOW PARAMETERS: 
  Format specifiers - 
      HELP FORMAT PARAMETERS: 
G 
  GMAP6 - 
      HELP PATCHING 
  GO command - 
      HELP EXECUTION_CONTROL GO 
      HELP GO 
  GO STEP command - 
      HELP EXECUTION_CONTROL GOSTEP 
  GO TRAP command - 
      HELP EXECUTION_CONTROL GOTRAP 
  GOSTEP Command - 
      HELP GOSTEP 
  GOTRAP Command - 
      HELP GOTRAP 
  GOTRAPSTEP command - 
      HELP EXECUTION_CONTROL GOTRAPSTEP 
      HELP GOTRAPSTEP 
H 
  HELP command - 
      HELP MISC HELP 
      HELP ANLZ DESCRIPTION: 
      HELP HELP 
  HISTORY command - 
      HELP EXECUTION_TRACING HISTORY 
      HELP HISTORY 
  Horizontal Ellipsis - 
      HELP NOTATION_CONVENTIONS HORIZONTAL_ELLIPSIS 
  Housekeeping Commands - 
      HELP DESCRIPTOR_QUALIFIED_REFERENCES EXAMPLE: 
I 
  IBEX commands - 
      HELP START_PROGRAM_WITH_DELTA 
  IGNORE command - 
      HELP HOUSEKEEPING KEEP_TRAP_IGNORE 
      HELP KEEP_TRAP_IGNORE 
  IGNORE keyword - 
      HELP KILL_SHOW PARAMETERS: 
  INACTIVE command - 
      HELP ACTIVE_INACTIVE 
  Initiating A Program with DELTA Associated - 
      HELP START_PROGRAM_WITH_DELTA 
  input stream - 
      HELP READ DESCRIPTION: 
  INSTR specifier - 
      HELP FORMAT PARAMETERS: 
  instructions, multiword - 
      HELP PATCHING 
  Internal Program Unit - 
      HELP INTERNAL_PROGRAM_UNIT 
  Invoking DELTA - 
      HELP INVOKING_DELTA 
  IPU - 
      HELP INTERNAL_PROGRAM_UNIT 
  items, elementary - 
      HELP ELEMENTARY_ITEM 
J 
  JDE specifier - 
      HELP FORMAT PARAMETERS: 
K 
  KEEP keyword - 
      HELP KILL_SHOW PARAMETERS: 
  KEEP/TRAP/IGNORE Command - 
      HELP KEEP_TRAP_IGNORE 
  KEEP/TRAP/IGNORE commands - 
      HELP HOUSEKEEPING KEEP_TRAP_IGNORE 
  keywords used with KILL/SHOW - 
      HELP KILL_SHOW PARAMETERS: 
  KILL command - 
      HELP HOUSEKEEPING KILL 
  KILL EOM command - 
      HELP COMMUNICATIONS_WITH_DELTA 
  KILL/SHOW Command - 
      HELP KILL_SHOW 
  KILL/SHOW keywords - 
      HELP KILL_SHOW PARAMETERS: 
L 
  Left bracket, EOM character - 
      HELP EOM_CHARACTERS 
  LET command - 
      HELP MEMORY_DISPLAY LET 
      HELP LET 
  Linefeed, EOM character - 
      HELP EOM_CHARACTERS 
  LIST command - 
      HELP MISC LIST 
      HELP ANLZ DESCRIPTION: 
      HELP LIST 
  location reference - 
      HELP RESOLVING_A_SYMBOLIC_REFERENCE 
  logical operator - 
      HELP IF_ATTACHMENT FORMAT: 
  lower case letters - 
      HELP NOTATION_CONVENTIONS LOWER_CASE 
M 
  M$ALIB - 
      HELP CONCEPTS 
  M$ERR - 
      HELP ON_EXIT_ON_ABORT DESCRIPTION: 
  M$EXIT - 
      HELP ON_EXIT_ON_ABORT DESCRIPTION: 
  M$LDTRC - 
      HELP ON_EXIT_ON_ABORT DESCRIPTION: 
  M$SAD - 
      HELP SAD DESCRIPTION: 
  M$SAVE - 
      HELP ON_EXIT_ON_ABORT DESCRIPTION: 
  M$XXX - 
      HELP ON_EXIT_ON_ABORT DESCRIPTION: 
  ME - 
      HELP READ EXAMPLE: 
  memory - 
      HELP PLUGH USAGE_NOTES 
  memory display and modification command - 
      HELP PLUGH USAGE_NOTES 
  Miscellaneous Commands - 
      HELP ANLZ DESCRIPTION: 
  Mode Control Commands - 
      HELP PMD USAGE_NOTES: 
  modification - 
      HELP LET DESCRIPTION: 
  MODIFY Closed Form Command - 
      HELP MODIFY_CLOSED 
  MODIFY command - 
      HELP MEMORY_DISPLAY MODIFY 
  MODIFY Open Form Command - 
      HELP MODIFY_OPEN 
  multiword instructions - 
      HELP PATCHING 
N 
  NEXT, sub-command - 
      HELP EOM_CHARACTERS 
  No Run Unit Associated - 
      HELP NO_RUN_UNIT_ASSOCIATED 
  Node - 
      HELP NODE 
  nodes - 
      HELP USE_NODE PARAMETERS: 
  Numbers - 
      HELP NOTATION_CONVENTIONS NUMBERS 
O 
  OCTAL specifier - 
      HELP FORMAT PARAMETERS: 
  Offset - 
      HELP OFFSET 
  ON ABORT - 
      HELP ON_EXIT_ON_ABORT USAGE_NOTES 
  ON ABORT command - 
      HELP HOUSEKEEPING ONABORT 
      HELP ON_EXIT_ON_ABORT 
  ON ABORT keyword - 
      HELP KILL_SHOW PARAMETERS: 
  ON CALL command - 
      HELP EXECUTION_CONTROL ON_CALL 
  ON CALL, ON CALLS Commands - 
      HELP ON_CALL 
  ON CALLS keyword - 
      HELP KILL_SHOW PARAMETERS: 
  ON EXIT - 
      HELP ON_EXIT_ON_ABORT USAGE_NOTES 
  ON EXIT command - 
      HELP HOUSEKEEPING ON_EXIT 
  ON EXIT keyword - 
      HELP KILL_SHOW PARAMETERS: 
  ON EXIT/ON ABORT Command - 
      HELP ON_EXIT_ON_ABORT 
  ON NODE command - 
      HELP EXECUTION_CONTROL ON_NODE 
  ON NODE, ON NODES Commands - 
      HELP ON_NODE 
  ON NODES command - 
      HELP EXECUTION_CONTROL ON_NODES 
  ON NODES keyword - 
      HELP KILL_SHOW PARAMETERS: 
  ON X CALLS command - 
      HELP EXECUTION_CONTROL ON_X_CALLS 
  OPEN, EOM sub-command - 
      HELP EOM_CHARACTERS 
  OUTPUT command - 
      HELP HOUSEKEEPING OUTPUT 
      HELP OUTPUT 
  output destinations - 
      HELP OUTPUT FORMAT: 
P 
  PARAGRAPHS, transfer type - 
      HELP TRACE PARAGRAPHS 
  Patching - 
      HELP PATCHING 
  PLUGH command - 
      HELP EXECUTION_TRACING PLUGH 
      HELP PLUGH 
  PMD command - 
      HELP MEMORY_DISPLAY PMD 
      HELP PMD 
  Pointer - 
      HELP POINTER 
      HELP POINTER_QUALIFIED_REFERENCES 
  Pointer-Qualified References - 
      HELP POINTER_QUALIFIED_REFERENCES 
  position reference - 
      HELP RESOLVING_A_SYMBOLIC_REFERENCE 
  Post Association of DELTA - 
      HELP POST_ASSOCIATION_OF_DELTA 
      HELP POST_ASSOCIATION_OF_DELTA 
      HELP POST_ASSOCIATION_OF_DELTA 
  PREV, EOM sub-command - 
      HELP EOM_CHARACTERS 
  procedure address - 
      HELP SYMBOLIC_ADDRESSING 
  Processor - 
      HELP PROCESSOR 
  Programmed Association of DELTA - 
      HELP PROGRAMMED_ASSOCIATION_OF_DELTA 
  prompt character - 
      HELP COMMUNICATIONS_WITH_DELTA 
      HELP PROMPT PARAMETERS: 
  PROMPT command - 
      HELP HOUSEKEEPING PROMPT 
      HELP PROMPT 
  PROTECT - 
      HELP MISC PROTECT 
  PROTECT Command - 
      HELP PROTECT 
  PROTECT keyword - 
      HELP KILL_SHOW PARAMETERS: 
  PTR specifier - 
      HELP FORMAT PARAMETERS: 
Q 
  QUIT command - 
      HELP MISC END 
      HELP ANLZ DESCRIPTION: 
      HELP END_QUIT 
R 
  RANGE command - 
      HELP HOUSEKEEPING RANGE 
      HELP RANGE 
  RANGE keyword - 
      HELP KILL_SHOW PARAMETERS: 
  READ command - 
      HELP HOUSEKEEPING READ 
      HELP READ 
  REL specifier - 
      HELP FORMAT PARAMETERS: 
  REPORT command - 
      HELP HOUSEKEEPING REPORT 
      HELP REPORT 
  REPORT keyword - 
      HELP KILL_SHOW PARAMETERS: 
  Resolving A Symbolic Reference - 
      HELP RESOLVING_A_SYMBOLIC_REFERENCE 
  RUM command - 
      HELP MODE_CONTROL RUM 
      HELP RUM 
  RUM keyword - 
      HELP KILL_SHOW PARAMETERS: 
  RUM mode - 
      HELP PATCHING 
S 
  SAD command - 
      HELP MISC SAD 
      HELP SAD 
  SAD keyword - 
      HELP KILL_SHOW PARAMETERS: 
  SAVE command - 
      HELP HOUSEKEEPING SAVE 
      HELP SAVE 
  SAVES keyword - 
      HELP KILL_SHOW PARAMETERS: 
  SBIN specifier - 
      HELP FORMAT PARAMETERS: 
  Scalars - 
      HELP SCALARS 
  SCHEMA command - 
      HELP HOUSEKEEPING SCHEMA 
      HELP SCHEMA 
  SCHEMA keyword - 
      HELP KILL_SHOW PARAMETERS: 
  schema, debug - 
      HELP SCHEMA DESCRIPTION: 
  SET - 
      HELP READ USAGE_NOTES 
  SET command (IBEX) - 
      HELP READ DESCRIPTION: 
  SHOW command - 
      HELP HOUSEKEEPING SHOW 
      HELP KILL_SHOW 
  SHOW keywords - 
      HELP KILL_SHOW PARAMETERS: 
  SILENT/UNSILENT Command - 
      HELP SILENT_UNSILENT 
  SILENT/UNSILENT commands - 
      HELP HOUSEKEEPING SILENT_UNSILENT 
  Special characters - 
      HELP NOTATION_CONVENTIONS NUMBERS 
  Special Notes - 
      HELP SPECIAL_NOTES 
  START - 
      HELP START_PROGRAM_WITH_DELTA 
  Statement Label - 
      HELP STATEMENT_LABEL 
  statement labels - 
      HELP SYMBOLIC_ADDRESSING 
  Statement Number - 
      HELP STATEMENT_NUMBER 
  statement numbers - 
      HELP SYMBOLIC_ADDRESSING 
  STATEMENTS, transfer type - 
      HELP TRACE STATEMENTS 
  STATUS Command - 
      HELP STATUS 
  STATUS keyword - 
      HELP KILL_SHOW PARAMETERS: 
  STEP BY Command - 
      HELP STEP_BY 
  STEP command - 
      HELP EXECUTION_CONTROL STEP 
      HELP STEP 
  STEP keyword - 
      HELP KILL_SHOW PARAMETERS: 
  step mode - 
      HELP STEP_BY DESCRIPTION: 
  STEP ONE CALL Command - 
      HELP STEP_ONE_CALL 
  STOP Command - 
      HELP STOP 
  STORE command - 
      HELP MEMORY_DISPLAY STORE 
      HELP STORE 
  Structures - 
      HELP STRUCTURES 
      HELP SYNTAX DESCRIPTION: 
  Substatement - 
      HELP SUBSTATEMENT 
  symbolic address qualification - 
      HELP SYMBOLIC_POSITION_NAMES 
      HELP SYMBOLIC_ADDRESS_QUALIFICATION 
  Symbolic Addressing - 
      HELP SYMBOLIC_ADDRESSING 
  Symbolic Location Names - 
      HELP SYMBOLIC_LOCATION_NAMES 
  symbolic names - 
      HELP SYMBOLIC_ADDRESSING 
  Symbolic Position Names - 
      HELP SYMBOLIC_POSITION_NAMES 
  symbolic reference - 
      HELP RESOLVING_A_SYMBOLIC_REFERENCE 
  SYNTAX command - 
      HELP HOUSEKEEPING SYNTAX 
      HELP SYNTAX 
  SYNTAX keyword - 
      HELP KILL_SHOW PARAMETERS: 
  System Areas - 
      HELP SYSTEM_AREAS 
T 
  Tab Character, EOM character - 
      HELP EOM_CHARACTERS 
  TIME specifier - 
      HELP FORMAT PARAMETERS: 
  toggle switches - 
      HELP DESCRIPTOR_QUALIFIED_REFERENCES EXAMPLE: 
  TRACE Command - 
      HELP TRACE 
  TRACE keyword - 
      HELP KILL_SHOW PARAMETERS: 
  TRACE TRANSFERS command - 
      HELP EXECUTION_TRACING TRACE_TRANSFERS 
  TRACE X CALLS command - 
      HELP EXECUTION_TRACING TRACE_X_CALLS 
  TRANSFERS, transfer type - 
      HELP TRACE TRANSFERS 
  TRAP command - 
      HELP HOUSEKEEPING KEEP_TRAP_IGNORE 
      HELP KEEP_TRAP_IGNORE 
  TRAP keyword - 
      HELP KILL_SHOW PARAMETERS: 
  TSA Command - 
      HELP MEMORY_DISPLAY TSA 
      HELP TSA 
U 
  U command - 
      HELP START_PROGRAM_WITH_DELTA 
  UBIN specifier - 
      HELP FORMAT PARAMETERS: 
  UNFID command - 
      HELP MISC UNFID 
      HELP ANLZ DESCRIPTION: 
      HELP UNFID 
  UNSHARE command - 
      HELP EXECUTION_CONTROL UNSHARE 
      HELP UNSHARE 
  UNSILENT command - 
      HELP HOUSEKEEPING SILENT_UNSILENT 
  Up Arrow, EOM character - 
      HELP EOM_CHARACTERS 
  UPDATE Closed Form Command - 
      HELP UPDATE_CLOSED 
  UPDATE command - 
      HELP HOUSEKEEPING UPDATE 
  UPDATE Open Form Command - 
      HELP UPDATE_OPEN 
  USE Command - 
      HELP USE 
  USE NODE command - 
      HELP HOUSEKEEPING USENODE 
      HELP USE_NODE 
V 
  Variable - 
      HELP VARIABLE 
      HELP POINTER_QUALIFIED_REFERENCES 
  VECTOR specifier - 
      HELP FORMAT PARAMETERS: 
W 
  WAIT Command - 
      HELP WAIT 
  WHEN command - 
      HELP EXECUTION_CONTROL WHEN 
      HELP WHEN 
  WHENS keyword - 
      HELP KILL_SHOW PARAMETERS: 
X 
  X specifier - 
      HELP FORMAT PARAMETERS: 
  XCON command - 
      HELP EXECUTION_CONTROL XCON 
      HELP XCON 
  XEQ command - 
      HELP MISC XEQ 
      HELP ANLZ DESCRIPTION: 
      HELP XEQ 
Z 
  ZERO specifier - 
      HELP FORMAT PARAMETERS: 
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
Format: 
H[ISTORY]  [n [M[ORE]]] 
           [C[LEAR]   ] 
Parameters: 
n    is a decimal integer which specifies the number of history entries to be 
displayed.  If n is not specified, all entries, or remaining entries, will be 
displayed. 
MORE    is a keyword which specifies that the display is to continue from the 
last entry displayed. 
CLEAR    removes all entries from the buffer. 
Description: 
When one of the TRACE modes is active, DELTA maintains a list of the trace 
reports in the history buffer.  The history buffer can hold 256 entries, and 
is circular, meaning the 257th entry will replace the first entry; the second 
is replaced by the 258th entry.  The buffer is also last-in, first-out, 
meaning that the latest (most recent) buffer entry is the first to be 
displayed.  Thus, HISTORY shows a backwards flow of control. 
Example: 
    Command              Explanation 
    HISTORY 3            Display three history buffer entries starting 
                         with the latest entry. 
    H3M                  Display the next three history buffer entries. 
Example of TRACE and HISTORY: 
    >TRACE CALLS 
    >G 
    A:3<CALLED> B:1 
    B:15<CALLED> C:1 
    C:120<CALLED> G:1 
    BREAK @ G:27   (User hits break) 
    >HISTORY 2 
    C:120<CALLED> G:1 
    B:15<CALLED> C:1 
    >HISTORY 5 MORE 
    A:3<CALLED> B:1 
    No more history 
    > 
Usage Notes: 
1.  The HISTORY command is used in conjunction with the TRACE command.  If the 
    command is issued before one of the TRACE commands has been entered, the 
    history buffer will contain no entries. 
2.  The history buffer is cleared (reset to null) whenever a KILL TRACE 
    command is issued. 
00002
00003
00004
00001
00004
Summary descriptions of housekeeping commands appear at the next levels of 
this HELP message.  Type ? or ?? for a listing of these descriptions or for a 
specific summary description type, 
HELP (DELTA) HOUSEKEEPING housekeeping_command 
where housekeeping_command is one of the following:  ACTIVE|INACTIVE, 
ALTERNATE_VARIABLES, BYPASS, COPY, DEFINE, DO, ECHO, EOM, FORMAT, 
KEEP_TRAP_IGNORE, KILL, ONABORT, ONEXIT, OUTPUT, PROMPT, RANGE, READ, REPORT, 
SAVE, SCHEMA, SHOW, SILENT_UNSILENT, SYNTAX, UPDATE, USENODE. 
For a categorized list of commands, type HELP (DELTA) COMMANDS.  The command 
summaries are presented in tabular form as follows: 
  Command       Function 
  AC[TIVE]|IN[ACTIVE] 
                Activates or deactivates a single or a range of stored 
                commands. 
  A[LTERNATE] V[ARIABLES] 
                Specifies alternate debug schema to be searched when an 
                unqualified variable reference is not satisfied by searching 
                the current schema. 
  BY[PASS] 
                Bypasses assembler program units during stepping. This command 
                sets a toggle within DELTA. 
  C[OPY] 
                Causes DELTA output to be copied on the user terminal when the 
                specified destination for output is other than the user 
                terminal. This command sets a toggle within DELTA. 
  DE[FINE] 
                Associates a value or location with a symbol. 
  DO 
                Executes the attachments to a stored command or a group of 
                commands identified by the SAVE command. 
  EC[HO] 
                Causes input to be echoed to an output device when DELTA input 
                is from a device other than an on-line terminal.  This command 
                sets a toggle within DELTA. 
  EO[M] 
                Set or reset special activation (end of message) character 
                set.  This command sets a toggle within DELTA. 
  FO[RMAT] 
                Specifies default format for MODIFY and EVALUATE display 
                output. 
  KE[EP]|TRAP|IG[NORE] 
                Direct DELTA's handling of asynchronous events and other 
                exceptional conditions. 
  K[ILL] 
                Deactivates a toggle or removes a stored command or a range of 
                stored commands. 
  O[N] A[BORT] 
                Specifies activities to occur upon abort. 
  O[N] E[XIT] 
                Specifies activities to occur upon normal exit. 
  OU[TPUT] 
                Specify destination for DELTA output. 
  PRO[MPT] 
                Sets the DELTA prompt character (default is >). 
  RA[NGE] 
                Specify range of offsets from defined symbol to be used for 
                position reporting. 
  R[EAD] 
                Causes DELTA to read other than the normal input stream. 
  REP[ORT] 
                Directs DELTA's formatting of position reporting. 
  SA[VE] 
                Stores and remembers a single or a range of stored commands. 
  SC[HEMA] 
                Activates or deactivates schema usage or sets "current" 
                schema. This command sets a toggle within DELTA. 
  SH[OW] 
                Displays the status of toggled options, keyword options or a 
                single or range of stored commands and attachments. 
  SI[LENT]|UN[SILENT] 
                Activates or deactivates the reporting of a single or a range 
                of stored commands. 
  SY[NTAX] 
                Allows specification of FORTRAN, COBOL, or PL-6 input syntax. 
  UP[DATE] 
                Updates stored commands or attachments of stored commands. 
  U[SE] N[ODE] 
                Activates schema(s) associated with a specific overlay node. 
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
00001
00010
00011
00012
00013
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
00010
00022
00024
00025
00025
Format: 
    IF var logical_operator cons 
Parameters: 
var    is any position or location reference.  Position and location 
references are described under the topics SYMBOLIC_POSITION_NAMES and 
SYMBOLIC_LOCATION_NAMES. 
logical_operator    is any of the following: 
    =      EQ          equal 
    >< <>  NE          not equal 
    <      LT          less than 
    >      GT          greater than 
    <=  =< LE          less than or equal 
    >=  => GE          greater than or equal 
cons    is any literal: octal, decimal, bit or character. 
Description: 
All stored commands may be formed to specify varying levels of conditional 
execution by using IF conditional.  The IF conditional must be used as part of 
another command. 
The value described by var is compared with the constant value.  If the 
logical relation is true, then the stored command is reported and its 
attachments executed (if the condition was on a stored command), or the 
attachment is executed (if the condition was on an attachment). 
Specification of an IF condition is allowed on almost all DELTA commands. 
Specific instances where the IF is not allowed are noted in the description of 
the commands. 
Taking into account the IF condition, the complete specification of stored 
commands is: 
    [id] stored_command [IF var logical_operator cons] 
      [;attachment [IF var logical_operator cons] 
        [;attachment [IF var logical_operator cons]] ... ] 
Rules: 
1.  The operators =, >=, <=, etc., cannot be entered from an online terminal 
    unless "KILL EOM" has been specified. 
Example: 
    20 AT ROUTINE10 IF NET_PAY EQ 0; DISPLAY DEDUCTIONS; 
    DUMP PAY_RECORD,20; GO 
In this example, IF specifies conditional execution.  When the ROUTINE10 
breakpoint is reached, NETPAY will be examined to determine if its value is 
zero.  If its value is not zero, DELTA will not report to the user that 
ROUTINE10 has been reached nor will any of the attachments be executed. 
00002
00004
00001
00003
IF_ATTACHMENT
KEEP_TRAP_IGNORE
ACTIVE_INACTIVE

KILL_SHOW
Format: 
           {AL[L]                           } 
           {N[ONE]                          } 
           {category[,category] ...         } 
           {type[,type] ...                 } 
KE[EP]     {H[OST]  AL[L]                   } 
TRAP       {H[OST] N[ONE]                   } 
IG[NORE]   {H[OST] type[,type] ...          } 
           {fprg-res AL[L]                  } 
           {fprg-res N[ONE]                 } 
           {fprg-res type[,type] ...        } 
Parameters: 
ALL    specifies all categories and types are to be added to this list. 
NONE    specifies all categories and types are to be removed from this list. 
category specifies a category to add to this list. (categories are in the 
following table.  All types in a category may be placed on a list by using the 
category name.) 
type    specifies a type to add to this list. 
FEP Parameters: 
Host    specifies the host program 
fprg-res specifies a particular FEP program. This is the value the user 
specified for the RES on the M$OPEN of the FEP program. 
                                                  APPLICABLE CATEGORY EC TYPE 
MONITOR SVC 
MO[NITOR]         T[IMER]                         M$STIMER 
                  EV[ENT]                         M$EVENT 
                  B[REAK]                         M$INT 
                  X[CON]                          M$XCON 
                  PM[ME] (Bad PMME, no ALTRET)    M$TRAP 
AR[ITHMETIC]      OV[ERFLOW]                      M$TRAP 
                  DI[VIDE_CHECK] (Divide check)   M$TRAP 
PR[OGRAMMED]      MM[E]                           M$TRAP 
                  DE[RAIL]                        M$TRAP 
                  F[AULT_TAG]                     M$TRAP 
ER[ROR]           ME[MORY]                        M$TRAP 
                  CO[MMAND]                       M$TRAP 
                  L[OCKUP]                        M$TRAP 
                  I[PR] (Illegal Procedure)       M$TRAP 
                  SEG (Missing Segment)           M$TRAP 
                  PA[GE] (Missing Page)           M$TRAP 
                  SEC_1 (Security 1)              M$TRAP 
                  SEC_2 (Security 2)              M$TRAP 
                                       APPLICABLE EC TYPE MONITOR SERVICE 
EV[ENT]                                M$EVENT 
B[REAK]                                M$INT 
X[CON]                                 M$XCON 
M[CL] (Bad MCL, no ALTRET)             M$TRAP 
T[RAP]                                 M$TRAP 
Description: 
KEEP/TRAP/IGNORE are used to build a list of EC types which will be handled in 
one of three ways. 
If an EC type is on the KEEP list when an EC of that type occurs, it is 
reported, along with the current position.  If an EC is on the TRAP list when 
an EC of that type occurs, it will be passed to the user program's handler for 
that EC type.  If an EC is on the IGNORE list when an EC of that type occurs, 
the program IC is adjusted to avoid re-occurrence of the EC and control 
returns to the program at the new position. 
To remove an EC type from one list, the user specifies that it is to be placed 
on some other list.  To remove all EC types from a list, the user specifies 
NONE for that list.  Any EC types that were on a NONEed list are placed on the 
KEEP list. 
Usage Notes: 
1.  Use of a category name implies all types in that category.  Types and 
    categories may be mixed freely on a line, e.g., TRAP MONITOR, DIVIDE. 
2.  If, at the time of an occurrence of an EC on the TRAP list, a program does 
    not have a valid handler for that EC, an error message will be issued. 
    DELTA will continue as if that EC had been on the KEEP list. 
3.  Precedence is given to ON EXIT/ON ABORT for the XCON EC. 
4.  When there are FEP programs associated, the commands have the following 
    meanings: 
        KEEP ALL    report everything on all programs - Host and FEP. 
        KEEP HOST ALL    report everything on the Host program. 
        KEEP fprg-res ALL    report everything on the specified FEP program. 
        KEEP HOST EVENT    report event exceptional conditions on the Host 
        program. 
        TRAP ALL    passes exceptional conditions on all programs to the 
        program's trap handler - this does not include the start of FEP 
        programs. 
        TRAP HOST ALL    passes exceptional conditions on the Host program to 
        the Host program's trap handler. 
        TRAP fprg-res ALL    passes exceptional conditions on the specified 
        FEP program to the specified FEP program's trap handler. 
        TRAP fprg-res MCL    only pass MCL exceptional conditions for the 
        specified FEP program to the specified FEP program's trap handler. 
        IGNORE ALL    reports no exceptional conditions on all programs. 
        IGNORE HOST ALL    reports no exceptional conditions on the Host 
        program. 
        IGNORE fprg-res ALL    reports no exceptional conditions on the 
        specified FEP program. 
        IGNORE HOST BREAK    reports no BREAK type exceptional conditions on 
        the Host program. 
00002
00003
00001
00003
Format: 
{K[ILL]}  {id[-id]   } 
{SH[OW]}  {id [TO id]} [ON      ] 
          {keyword   } [OVER fid] 
                       [INTO    ] 
                       [TO      ] 
Parameters: 
id    is the identification of a stored command. 
fid    specifies a file created by the SHOW command that allows the 
information to be output in a format that can be read back in via the READ 
command. 
keyword is one of the following keywords ALL, ALTERNATE_VARIABLES, ANLZ, ATS, 
BYPASS, COPY DEF, DEFS, DELTA, ECHO, EOM, FORMAT, FPRGS, IGNORE, KEEP 
ON_ABORT, ON_CALLS, ON_EXIT, ON_NODES, PROTECT RANGE, REPORT, RUM, SAD, SAVES, 
SCHEMA, STATUS, STEP, SYNTAX TRACE, TRAP, WHENS This information can be 
accessed in several ways.  By typing a ? or ?? after this message all keywords 
will be displayed.  To specify a particular keyword type: 
HELP (DELTA) {KILL|SHOW} keyword 
For example, HELP (DELTA) KILL ALL. 
Descriptions and an example are in tabular form as follows: 
  Keyword           Meaning with Kill          Meaning with Show 
AL[L]             Remove all stored          Display status of all 
                  commands.                  stored commands, toggle 
                                             options, and modes. 
A[LTERNATE]       Discontinue use of         Show status of toggle and 
V[ARIABLES]       alternate variables.       schema name, if any. 
AN[LZ]            Return to debug mode.      Show status of toggle. 
A[TS]             Remove all AT breakpoints  Display all AT breakpoints 
                  and their attachments.     and their attachments. 
B[YPASS]          Do not bypass step         Show status of toggle. 
                  reporting in assembler 
                  modules. 
C[OPY]            Discontinue COPYing.       Show status of toggle. 
D[EF]             Remove a specific named    Not applicable. 
                  DEFINED symbol. 
DEFS              Remove all DEFINED         Display all defined 
                  symbols.                   symbols. 
DEL[TA]           Causes DELTA to be         Not applicable. 
                  disassociated from the 
                  current run unit being 
                  debugged. 
EC[HO]            Discontinue ECHOing.       Show status of toggle. 
E[OM]             Deactivate the EOM         Show status of toggle. 
                  character set. 
F[ORMAT]          Set display formats for    Display current default 
                  MODIFY and EVAL back to    formats for MODIFY and 
                  initial defaults.          EVAL. 
I[GNORE]          Not applicable.            Display which exceptional 
                                             condition groups and/or 
                                             names are being ignored. 
K[EEP]            Not applicable.            Display which exceptional 
                                             conditions will be 
                                             intercepted and reported 
                                             by DELTA. 
O[N] A[BORT]      Remove ON ABORT            Display ON ABORT breakpoint 
                  breakpoint and its         and its attachments. 
                  attachments. 
O[N] C[ALLS]      Remove all ON CALL(S)      Display all ON CALL(S) 
                  commands and their         commands and their 
                  attachments.               attachments. 
O[N] E[XIT]       Remove ON EXIT breakpoint  Display ON EXIT breakpoint 
                  and its attachments.       and its attachments. 
O[N] N[ODES]      Remove all ON NODE(S)      Display all ON NODE(S) 
                  commands and their         commands and their 
                  attachments.               attachments. 
P[ROTECT]         Discontinue PROTECT mode.  Display PROTECT mode. 
R[ANGE]           Not applicable.            Display value of range 
                                             specification for relation 
                                             position reporting. 
RE[PORT]          Not applicable.            Display reporting mode 
                                             for position reporting. 
RU[M]             Return to debug mode.      Show status of toggle. 
SAD               Disables use of the        Display special access 
                  $SAD symbol.               descriptor number. 
SA[VES]           Remove all SAVE commands   Display all SAVE commands 
                  and their attachments.     and their attachments. 
SC[HEMA]          Discontinue schema usage.  Display the position which 
                                             defines the current schema, 
                                             as set by the instruction 
                                             counter or the SCHEMA 
                                             command. 
S[TEP]            Default to step by         Show status of STEP mode. 
                  statement. 
SY[NTAX]          Not applicable.            Display which input 
                                             syntax DELTA is currently 
                                             accepting. 
T[RACE]           Discontinue tracing.       Display all TRACE 
                                             commands. 
TRAP              Not applicable.            Display which exceptional 
                                             conditions will be passed 
                                             to the trap handler in the 
                                             target run unit. 
W[HENS]           Remove all WHEN            Display all WHEN 
                  breakpoints and            breakpoints and their 
                  their attachments.         attachments. 
FEP Keywords: 
DEL[TA] fprg-res  Causes DELTA to be         Not applicable. 
                  disassociated from the 
                  specified FEP program. 
FP[RGS]           Not Applicable.            Displays the state 
                                             of all existing FEP 
                                             programs being debugged. 
fprg-res          Not Applicable.            Display the state 
                                             of the specified FEP 
                                             program. 
STAT[US]          Discontinue status mode    Display status mode. 
                  which controls the 
                  printing of an FPL 
                  field's status. 
Description: 
The KILL command is used either to change the status of a toggle or to cancel 
a previously entered command. 
The SHOW command is used to display the status of a toggle, classes of 
commands and attachments, and the current disposition of exceptional 
conditions.  The SHOW command also has an optional fid that allows the output 
information to be output in a format that can be read back in for purposes 
such as breakpoints. 
00002
00001
Format: 
L[ET] item constant 
Parameters: 
item    may be as described under DISPLAY. 
constant    is any meaningful literal in the current syntax (as specified by 
the currently specified SYNTAX option.  See the SYNTAX command. 
Description: 
The LET command is used to modify the contents of an area of memory or a 
program visible register. 
Some literals are allowed and mean the same regardless of the current syntax. 
They are: 
o   bit string '0010101'B      up to 72 bits - left justified 
o   octal bit string '123'O    up to 24 octal digits - left justified 
o   octal value O'123'         up to 12 octal digits - right justified 
o   hex value X'AB29'          up to 9 hex digits - right justified 
o   character string 'ABC'     up to 63 characters - left justified 
    or 'ABC'C or C'ABC' 
o   a pointer literal of the form: 
        octal word offset [-char offset[-bit offset]],segid 
    where segid is of the form: 
        $LSn, $ASn, or $PSn (n is a decimal number) 
    For example: 
        .123,$LS0 
        .212-0-4,$LS4 
Usage Notes: 
1.  If the literal is a character string (e.g., 'ANDERSON'), then the variable 
    must be a character string, or any item whose length in bits is 0 modulo 9 
    (an integral number of bytes).  The character string constant can be up to 
    63 characters and is stored in the variable left-justified with truncation 
    or blank-fill on the right as necessary to match the defined size of the 
    variable. 
2.  If the literal is a pointer literal, the variable must be a pointer or any 
    item whose size is 36 bits. 
3.  If the constant is a bit string or octal bit string, it is stored without 
    regard to variable type, left-justified with truncation or zero-fill on 
    the right as necessary to match the defined size of the item. 
4.  If the literal is an octal or decimal value, it is treated as a 36-bit 
    constant and can be stored in any 36-bit variable or in any integer 
    variable regardless of size, right-justified with truncation or zero-fill 
    on the left as necessary to match the size of the variable. 
5.  When specifying item with an expression (e.g., simple octal addresses) or 
    any variable or SYMDEF name with an offset expression, the location to 
    which the expression resolves is treated as a 36-bit variable. 
Cross Reference: 
See the SYNTAX command. 
00004
00002
00001
00003
Format: 
LI[ST] [ n [- m ]] 
       [   [TO m]] 
Parameters: 
n - m    will display the nth through the mth RUM. 
Description: 
The LIST command will list all changes made to a run unit in RUM mode.  The 
LIST command may be issued while DELTA is in either RUM mode or debug mode. 
Usage Notes: 
1.  LIST 0 may be used to find out how many times a run unit has been 
    modified. 
00002
00001
00003
MODIFY_OPEN
Summary descriptions of memory display and modification commands appear at the 
next levels of this HELP message.  Type a ? or ?? for a listing of these 
descriptions or for a specific summary description, type 
HELP (DELTA) MEMORY_DISPLAY memory_display_command 
where memory_display_command is one of the following:  DISPLAY, DUMP, 
EVALUATE, FIND, LET, MODIFY, PMD, STORE, TSA. 
For a categorized list of commands, type HELP (DELTA) COMMANDS. 
The command summaries are presented in tabular form as follows: 
  Command       Function 
  D[ISPLAY] 
                Displays the value of a variable or the contents of an 
                address. 
  DU[MP] 
                Dumps a specified range of memory in octal or hexadecimal 
                format.  Optionally allows no suppression of duplicate lines. 
                Optionally provides ASCII translation. 
  E[VALUATE] 
                Evaluates an expression and reports its value in a specified 
                format.  Reports the address of a program entity by segment 
                and offset. 
  F[IND] 
                Searches memory under mask and optionally substitutes under 
                mask. 
  L[ET] 
                Changes the value of a variable or the contents of an address. 
  M[ODIFY] 
                Displays the contents of an address and optionally replaces it 
                with new contents. 
  PMD 
                Dumps specified portions of a program which terminates 
                abnormally. 
  STO[RE] 
                Modifies a range of memory.  Optionally performs the 
                modification under mask. 
  TSA 
                Formats a trap save area starting at a specified hexadecimal 
                location. 
00001
00002
00003
00004
00005
00006
00007
00008
00009
Summary descriptions of miscellaneous commands appear at the next levels of 
this HELP message.  Type a ? or ?? for a listing of these descriptions or for 
a specific summary description, type 
HELP (DELTA) MISC miscellaneous_command 
where miscellaneous_command is one of the following: 
END, ERRFID, HELP, LIST, PROTECT, QUIT, SAD, UNFID, XEQ. 
For a categorized list of commands, type HELP (DELTA) COMMANDS 
The command summaries are presented in tabular form as follows: 
  Command       Function 
  EN[D] or Q[UIT] 
                Unconditionally exits to the command processor. 
  ERRFID 
                Changes the default error message file for \J displays. 
  HELP 
                Provides HELP via the HELP facility. 
  LI[ST] 
                Lists changes made during Run Unit Modification. 
  PROT[ECT] 
                Sets Protect mode (disallows LET, MODIFY store). 
  SAD 
                Special Access Descriptor allows addressing through a Monitor 
                descriptor for privileged users. 
  UNF[ID] 
                Performs M$UNFID on specified DCB. 
  X[EQ] 
                Executes a GMAP6 assembler instruction. 
00001
00002
00003
00004
00005
00001
00006
00007
00008
MISC
MODIFY_OPEN
Summary descriptions of mode control commands appear at the next levels of 
this HELP message.  Type ? or ?? for a listing of these descriptions or for a 
specific summary description, type: 
HELP (DELTA) MODE_CONTROL mode_control_command 
where mode_control_command is one of the following:  ANLZ, RUM. 
For a categorized list of commands, type HELP (DELTA) COMMANDS. 
The command summaries are presented in tabular form as follows: 
  Command       Function 
  AN[LZ] 
                Associates the schemas for the CP-6 Monitor, or associates the 
                schema from the specified file, and sets DELTA's domain of 
                reference to that of the running monitor, a specified system 
                dump file, or the running program. 
  RU[M] 
                Invokes the Run Unit Modification mode, optionally specifying 
                the number of buffers to use for faster I/O (up to 10, default 
                is 5). 
00001
00002
MODIFY_OPEN
Format: 
M[ODIFY] location[\f] newcontents [(expected old contents)] 
Parameters: 
location and f    are the same as in the open form of MODIFY. 
newcontents    is an expression that can be evaluated or is a GMAP6 
instruction. 
expected old contents    must be enclosed in parentheses () and the left 
parenthesis must be preceded by a blank.  The value can be any expression that 
can be evaluated or a GMAP6 instruction. 
Description: 
The closed or patching form can be issued either directly or can be attached 
to a stored command.  The difference in this form is that both the address and 
the new value are specified and the modify-active mode is not entered. 
Optionally, a display format can be specified and the expected old value of 
the addressed location can be specified.  The format specifier is used to 
change the default format for the display of the modified cell.  The default 
format is octal unless the location is in the run unit's procedure space or 
the new value is specified in mnemonic instruction form, in which case both 
the previous contents and the new contents are displayed in instruction 
format.  When the specified expected value does not match the previous 
contents, DELTA treats the command as an interactive MODIFY, displaying the 
addressed location and prompting for a new value. 
Example: 
    >M MYLOC+.510 TRA CPA+.210                  The previous contents 
    MYLOC+.510 / TRA CPA+.210 (LDP0 0,,PR2)     are displayed in 
                                                parentheses. 
    >M MYLOC+.510 TRA CPA+.210 (LDP0,,PR3)      Bad expected value. 
    (LDP0,,PR3) EXPECTED VALUE NOT FOUND 
    MYLOC+.510 / LDP0 0,,PR2 M>                 DELTA prompts for a 
                                                new value. 
    >M MYLOC+.510\O TRA CPA+.510                Use of format 
                                                specifier. 
00002
00003
00001
Format: 
M[ODIFY] location[\f][/] 
Parameters: 
location may be: 
o   an octal or decimal literal 
o   an address expression (location reference or position reference). 
o   a symbolic name. 
f   may be any valid format specifier. 
/   is the activation form of MODIFY and is allowed if KILL EOM has 
    not been specified. 
Description: 
When the open form of MODIFY is used, DELTA first displays the address of the 
cell to be modified followed by its current contents and then prompts for the 
value to which the cell is to be modified.  The prompt character (>) is 
preceded by the letter M (M>) which indicates that DELTA is in the 
modify-active mode.  This means that: 
o   The indicated address is open for modification. 
o   DELTA expects either: 
    -   A new value to be placed in the open cell and the cell to be closed. 
    -   A new value to be placed in the open cell, the open cell to be closed 
        and another cell to be displayed and opened for modification as 
        specified by one of the EOM characters or MODIFY sub-commands.  Type 
        HELP (DELTA) EOM_CHARACTERS for more information. 
    -   The open cell to be closed without modification. 
00002
00001
MODIFY_CLOSED
    Notation conventions used in format specifications and examples throughout 
    this manual are listed below.  The information can be accessed by either 
    typing a ? or ??  immediately following this message, or by typing: 
    HELP (DELTA) NOTATION_CONVENTIONS convention 
    where the available conventions are: 
    LOWER_CASE, CAPITAL_LETTERS, BRACKETS, BRACES, ELLIPSIS, 
    SPECIAL_CHARACTERS 
    Example: HELP (DELTA) NOTATION_CONVENTIONS BRACES 
    Descriptions are in a tabular form with two columns like so: 
  Notation      Description 
  Lower-case Letters 
                Lower-case letters indicate that the element is a variable, to 
                be replaced with the desired value. 
  CAPITAL LETTERS 
                Capital letters indicate a literal, to be entered as shown. 
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
                may enter TAPE.  When used to enclose keywords, brackets 
                signify that the bracketed portion may be omitted, or 
                truncated at any point.  For example, the notation K[EY] means 
                that the user may enter K, KE, or KEY. 
  Braces 
                Elements stacked inside a pair of braces identify a required 
                choice. 
                    {id }   means that either a value for id or the 
                    {ALL}   word ALL must be entered. 
                Alternatively, the vertical OR bar is used to separate the 
                choices, thus:  {id|ALL} 
  Horizontal Ellipsis 
                The horizontal ellipsis indicates that a previous bracketed 
                element may be repeated, or that elements have been omitted. 
                    attachment[;attachment] ...    means that one or more 
                    attachments may be entered, with a semicolon inserted 
                    between each attachment. 
  Numbers/Special Characters 
                Numbers that are not part of a parameter name, special 
                symbols, and punctuation marks other than brackets, braces and 
                underlines appear as shown in output messages and must be 
                entered as shown when input. 
                   \f   means that a format specifier (f) must be 
                   preceded by a \ character. 
00004
00003
00002
00002
00006
00005
00005
00005
00001
00006
00006
ON_EXIT_ON_ABORT
ON_CALL
ON_EXIT_ON_ABORT
ON_EXIT_ON_ABORT
ON_CALL
ON_EXIT_ON_ABORT
ON_NODE
ON_CALL
ON_EXIT_ON_ABORT
Format: 
General Form: 
[id] O[N] [X] C[ALLS] [condition][;attachment] ... 
Specific Form: 
[id] O[N] C[ALL] name [condition][;attachment] ... 
Parameters: 
id    is a decimal number from 1 to 99. 
X    specifies breakpoints on external procedure calls only. 
condition    is an IF conditional which must be true before the breakpoint is 
to occur. 
name    is the name of a program unit. 
Description: 
The ON CALL command allows the user to conditionally interrupt execution prior 
to entry of a CALLed program unit. 
Usage Notes: 
1.  When the general and a specific form of the command are active, they are 
    mutually exclusive.  The specific form is not activated unless the named 
    program unit is CALLed.  The general form is not activated when any 
    program unit named in a specific form of the command is called. 
2.  Only one general form is permitted, but many specific forms may be active. 
3.  The breakpoint occurs before execution of the first instruction of the 
    called program unit.  The $IC points to the first instruction of the 
    called program unit. 
00002
00003
00001
00003
ON_CALL
Format: 
[id] O[N] A[BORT] [condition][;attachment] ... 
[id] O[N] E[XIT] [condition][;attachment] ... 
Description: 
These commands are primarily intended for use by the noninteractive user 
(batch mode or online !XEQ) who wishes to specify an action to be taken when 
his program aborts or exits unexpectedly.  ON EXIT specifies a list of 
attachments to execute when an EXIT condition is encountered, ON ABORT 
specifies a list of attachments to execute on an abort condition. 
An EXIT condition can be caused by M$EXIT, M$SAVE, and M$LDTRC.  An abort 
condition can be caused by M$ERR, M$XXX or a monitor abort for limit exceeded. 
Example: 
    ON ABORT;DU $TCB->0,64;Q 
When an abort occurs, dump the top TCB frame, and then exit DELTA. 
Usage Notes: 
1.  ON ABORT and ON EXIT are stored commands.  They can be displayed and 
    killed using SHOW id and KILL id. 
2.  ON ABORT and ON EXIT take precedence over KEEP/TRAP/IGNORE, i. e., even 
    though TRAP XCON was specified, the attachments for ON ABORT or ON EXIT 
    will be executed if an XCON EC (Exceptional Condition) occurs.  If the 
    user wishes to pass control to an XCON handler in his program after the 
    attachments are executed, he attaches a GOTRAP command. 
3.  ON ABORT is not allowed for FEP programs. 
00001
00002
00003
00003
Format: 
General Form: 
[id] O[N] N[ODES] [condition][; attachment] ... 
Specific Form: 
[id] O[N] N[ODE] name [condition][; attachment] ... 
Parameters: 
id    is a decimal number from 1 to 99. 
condition    is an IF conditional which must be true for the breakpoint to 
occur. 
name    is the name of an overlay node. 
Description: 
The ON NODE command conditionally interrupts execution when an overlay is 
loaded. 
Usage Notes: 
1.  When the general and a specific form of the command are active, they are 
    mutually exclusive.  The specific form is not activated unless the named 
    overlay is loaded.  The general form is not activated when any overlay 
    named in a specific form of the command is loaded. 
2.  Only one general form is permitted, but many specific forms may be active. 
3.  The breakpoint occurs on the M$OLAY monitor service and $IC points to the 
    instruction immediately after the CLIMB instruction. 
4.  The ON NODE(S) command is not allowed for FEP programs. 
00002
00003
00001
00003
ON_NODE
ON_CALL
Format: 
OU[TPUT] [[ON|TO|OVER|INTO] fid] 
Parameters: 
[ON|TO|OVER|INTO]    determines the disposition of an existing file of the 
same name as the fid. 
fid    is a valid file identifier. 
Description: 
DELTA'S output is always written through the M$DO DCB.  The default 
destination differs depending upon whether the session is conducted on-line or 
in batch.  The default destination for an on-line session is the user's 
terminal; for a batch session it is the line printer at the user's workstation 
of origin.  The OUTPUT command overrides these defaults. 
Example: 
    Command                      Explanation 
    OUTPUT ON MYFILENAME         Write DELTA output on a new file 
                                 called MYFILENAME. 
    OUTPUT OVER MYFILENAME       Overwrite the old file called MYFILENAME with 
                                 DELTA output. 
    OUTPUT INTO MYFILENAME       Extend the old file called MYFILENAME 
                                 with DELTA output. 
Usage Notes: 
1.  The ON or TO option will cause an error if the fid references a file which 
    already exists.  The OVER option will cause the file to be overwritten if 
    the fid references a file which already exists.  The INTO option will 
    cause the file to be extended if the fid references a file which already 
    exists.  In all cases, if the fid references a file and the file does not 
    exist, it will be created.  If none of ON/TO/OVER/INTO are specified, the 
    default is ON. 
2.  DELTA does not exercise complete control over the M$DO DCB.  The 
    connection of the DCB may be changed by: 
    o   Using the IBEX SET command. 
    o   Using the M$OPEN or M$CLOSE monitor service in the program 
        being debugged. 
3.  If the run unit being debugged also routes data through the M$DO DCB, 
    DELTA's output will be intermingled with it.  Should the run unit CLOSE 
    the DCB, it will be implicitly reopened by the next write from DELTA using 
    whatever parameters that remain. 
4.  If the run unit being debugged explicitly OPENs the M$DO DCB, it must be 
    able to handle the ALTRET condition "DCB is already open", since DELTA 
    will have opened the M$DO DCB to write its greeting message when DELTA is 
    first associated. 
00002
00003
00004
00001
00004
ON_CALL
ON_EXIT_ON_ABORT
ON_EXIT_ON_ABORT
    This set of Assembler Instruction Formats is used for patching in RUM or 
    DEBUG modes. 
    DELTA handles the standard GMAP6 instruction format for 1-word 
    instructions except for the following: 
o   The ZERO op code has the following format: 
    ZERO    any DELTA position or location reference, octal constant. 
    The ZERO op code specifies the contents of a word of memory.  The 
    evaluated position or location reference is placed in the left half of the 
    word and the octal constant is placed in the right half.  If the position 
    or location reference is preceded by a ":", a substatement and offset must 
    be specified before specifying the octal constant.  For example: 
        ZERO :100,1,.1,.1000 
        ZERO :100,,,.1000 
o   The PTR op code has the following format: 
        PTR    any DELTA position or location reference, octal constant. 
    The PTR op code specifies the contents of a word of memory in pointer 
    format.  The only segids which may be specified are .6000-.60FF.  The 
    octal constant specifies 00-FF of the segid.  The evaluated position or 
    location reference is placed in the left half of the word.  It is not 
    possible to specify a character or bit offset. 
o   A "!" after the op code causes DELTA to set the inhibit bit in the 
    generated instruction word.  For example: 
        LDA! .4010,DL 
Multiword instructions must be specified to DELTA in octal.  No mnemonic form 
is available for the instruction word or the descriptors.  When DELTA prints a 
multiword instruction, the octal value of the instruction word is preceded by 
the op code mnemonic. 
The following multiword instruction: 
    MLR FILL='040'0 
    ADSC9  2,QL,PR1 
    ADSC9  TEXT 
must be entered to DELTA as: 
    .40000100506 
    .100002000010 
    .1000010 
and will be printed out by DELTA as: 
    MLR  (AR,0,0,Q),(0,0,0),.40,0 
     .10000200010 
     .1000010 
Note:  The descriptor words may be printed in octal or some single instruction 
format.  The user must specify \O format to force printing of the descriptor 
in octal. 
For code that is the subject of XEC or XED, or that is generated dynamically, 
it is advantageous to keep DELTA away from it, i.e., do not use AT, STEP, XEQ, 
TRACE TRANSFER in such code, unless the user knows how DELTA will modify the 
code to do these commands. 
Format: 
PL[UGH] [location] 
Parameters: 
location may be: 
o   an octal or decimal literal 
o   an address expression (location reference or position reference) 
o   a symbolic name 
Description: 
The PLUGH (Procedure List Used to Get Here) command displays the chain of 
procedure calls which led to the arrival of the Instruction Counter at the 
current point.  The chain links are displayed on a last-in, first-out basis. 
DELTA's source for the procedure list is the user's automatic stack.  A line 
is displayed which identifies the CALL statement which caused the entry to 
each currently active procedure.  If location is specified, DELTA uses the 
location as the base of the automatic stack. 
Example: 
Assume   3 ECU's, which call each other in this order: 
             Y2 calls ROOM 
             ROOM calls WALL 
             WALL calls BUILDING 
             >GO 
             IPR FAULT @ BUILDING:15,,.1   (a program bug is hit.) 
             >PLUGH 
             WALL:93/TSX1 BUILDING:3       (PLUGH shows how the program 
                                           arrived at BUILDING from Y2.) 
             ROOM:70/TSX1 WALL:1 
             Y2:31/TSX1 ROOM:2 
Assume   Z calls X 
         X calls A 
             >REPORT O 
             >PLUGH 
             X+.262/TSX1 A(+.60) 
             Z+.360/TSX1 X(+.32) 
             Z/TSX0! X66_ARET+.1036 (X66_MAUTO)(+.4) 
             Bottom Frame 
Usage Notes: 
1.  The command is useful only in those run units with activation stack 
    frames. 
2.  If the REPORT command is issued with the OFFSET option before doing a 
    PLUGH, the PLUGH command will display the offset into the user's automatic 
    stack for each procedure.  If the offsets are not preceded by a "+", the 
    offsets are actual addresses of static parameter blocks. 
3.  A system call to an asynchronous entry will be indicated as a Bottom 
    Frame. 
00002
00003
00004
00001
00004
Format: 
PMD optionlist 
Parameters: 
optionlist    is any list of the following keywords: 
    AU[TO]            Auto segment (DS1) 
    CO[MMON]          Common segment (DS2) 
    DA[TA]            Data pages within Instruction Segment 
    DC[BS]            All DCBs 
    DS                All data segments 
    DS1 through DS8   Data segments 1 through 8 
    D[YNAMIC]D[ATA]   Dynamic data pages within Instruction Segment 
    IS                Entire Instruction Segment 
    JI[T]             User JIT 
    PL[UGH]           Causes same action as the PLUGH command. 
    PR[OCEDURE]       Procedure pages within Instruction Segment 
    RO[SEG]           Entire Read-only segment 
    TC[B]             Task control block (TCB stack) 
Description: 
The PMD command causes all or selected portions of a user's entire program 
image to be dumped.  Options allow for general selections of what areas to 
dump. 
Usage Notes: 
1.  The PMD command is not allowed for FEP programs. 
00002
00001
00003
A pointer-qualified reference has the form: 
    pointer -> variable 
where pointer is a memory word which contains the address (in pointer format) 
of an entity in memory. 
variable    is a based structure, array or scalar (based variable). 
If the based variable was declared with an implicit pointer, DELTA is aware of 
the relationship between the pointer and the based variable and will 
automatically use the implied pointer in resolving memory references.  The 
implied association may be overridden, however, by explicit pointer 
specification. 
Assume that ARRAY1 is an array of one dimension.  It is a based variable with 
an implied pointer called ARRAYPTR.  Then: 
Command                          Explanation 
DISPLAY ARRAY1(3)                Display the third element of the array 
                                 using ARRAYPTR to determine the address 
                                 of the array (implicit qualification). 
DISPLAY ARRAYPTR->ARRAY1(3)      Same.  Qualification was unnecessary. 
DISPLAY BASEPTR->ARRAY1(3)       Display the third element of the array. 
                                 Use "BASEPTR" to determine the address 
                                 of the array (explicit qualification). 
Multiple pointers may be used in a pointer-qualified reference. 
For examples, enter ? . 
Example: 
    DISPLAY BASEPTR1->BASEPTR2->ARRAYPTR->ARRAY (3) 
In this example: 
1.  BASEPTR1 contains the address of BASEPTR2. 
2.  BASEPTR2 contains the address of ARRAYPTR. 
3.  ARRAYPTR contains the address of ARRAY. 
For more information, enter ? . 
Notes: 
1.  Every pointer in a pointer-qualified reference must be in pointer format. 
00001
00002
PROMPT
DELTA is the Universal Debugger for CP-6 programs.  It is a special shared 
processor that, when invoked by a user, adds a system level dimension to the 
user's domain.  This dimension includes levels of logic with a precise 
understanding of the programming, object, and machine languages.  When invoked 
on behalf of a user, DELTA assumes both the user's identity and privilege 
levels. 
DELTA is driven by a set of English-like statements called commands.  These 
commands may be presented to DELTA directly through an interactive terminal or 
interspersed with IBEX commands in a batch job stream.  In either case, DELTA 
translates the commands into the language of that execution level which is 
capable of carrying them out.  Using DELTA, the user may: 
o   Conduct debugging sessions in the interactive or batch modes. 
o   Apply permanent patches to a run unit. 
o   Obtain current or post-mortem dumps of portions of a run unit. 
o   Examine the executing monitor. 
o   Examine any executing domain of the system.  To obtain more HELP 
    information: 
    HELP (DELTA) TOPICS     prints a list of all available HELP messages. 
    HELP (DELTA) command    prints the syntax of a command. 
    HELP (DELTA) COMMANDS   prints a list of commands in categories. 
    HELP (DELTA) RUM        prints the syntax of the RUM command. 
    ?                       means give the next level of HELP message. 
    ??                      means give all levels of the current message. 
    HELP (DELTA) RUM DES    prints a description of the RUM command. 
Format: 
PRO[MPT] char_string 
Parameters: 
char_string    is the desired prompt character string, from 1 to 28 
characters.  If all numeric characters or any non-alphanumeric are used, the 
entire string must be enclosed in quotes. 
Description: 
This command allows the user to change DELTA's prompt character (>) to another 
character or string of characters. 
00002
00001
Format: 
PROT[ECT] 
Description: 
This command is used to specify that DELTA is not to modify memory locations 
as specified by the MODIFY, LET, FIND, or STORE commands.  The command is most 
often used when the interactive form of the MODIFY command is used to examine 
a run unit image in RUM mode, or when the running monitor is being examined in 
ANLZ mode, and the user wishes to insure that a typing error will not cause a 
memory location to be changed inadvertently.  KILL PROTECT is the default. 
Usage Notes: 
1.  PROTECT is a toggle.  It is reset with the PROTECT option of the KILL 
    command. 
00001
00002
00002
END_QUIT
READ
Format: 
RA[NGE]  value 
Parameters: 
value    is any octal or decimal literal.  The default is .7777. 
Description: 
Sets the maximum range DELTA will use when determining whether to print a 
location as an octal location, or as the closest of a user DEF + offset or 
SYMDEF + offset. 
Example: 
    DEF A .30 
    RANGE .40 
When modifying location .70, DELTA will write A+.40, but modifying location 
.71 results in .71. 
00002
00003
00001
Format: 
R[EAD] [fid[,rec]] 
Parameters: 
fid    may be any valid CP-6 file identifier (fid).  See the discussion on 
fids in the Programmer Reference Manual (CE40).  Specifying the fid ME resets 
the input to the default command stream.  When fid is a CP-6 file, the 
specification of a starting record number is allowed. 
rec    can be either a record sequence number or, if the file is an EDIT 
compatible, keyed file, an EDIT line number.  Specification of an EDIT line 
number must always contain a decimal point with the exception of record number 
zero (0) which is assumed to be edit line number 0.000. 
Description: 
Unless directed otherwise, DELTA reads from the normal program command stream. 
This is the interactive terminal during on-line sessions, the input job 
command stream when in batch, or the file of command input specified by the 
IBEX XEQ command in either situation.  The DCB used by DELTA for reading its 
input is M$DELTA, one of the reserved system DCBs.  A user program cannot 
affect this DCB; however, a user can direct DELTA's input stream prior to 
entry to DELTA through the IBEX SET command.  Once DELTA is in control, 
DELTA's input stream may be re-directed by use of the READ command. 
Example: 
    Directive              Explanation 
    READ MYFILENAME        Read from the file MYFILENAME starting with 
                           the first record. 
    READ DP#JRC/JEFFILE,5  Read from the file JEFFILE contained on 
                           #JRC beginning with the fifth record. 
    READ EFILE,6.          Read from the EDIT compatible file EFILE 
                           beginning with line number 6.000. 
    READ ME                Read from the default command input stream. 
Usage Notes: 
1.  Upon reaching end-of-file or upon the occurrence of any unusual condition 
    while reading, DELTA resets its input to the default command stream. 
2.  Operationally, the READ command acts as a SET command on DELTA's input 
    DCB.  It does not cause the initiation of any read operations; it simply 
    alters the source of input for the next time that DELTA reads a command. 
3.  When an EDIT key is specified but is found not to exist, DELTA begins 
    reading at the following record. 
4.  If fid is not specified, DELTA defaults to READ UC. 
00002
00003
00004
00001
00004
Format: 
REP[ORT] [compiler]  [info] 
Parameters: 
compiler    is one of the following: 
    G[MAP] 
    P[L6] 
    F[ORTRAN] 
    FP[L] 
    C[OBOL] 
    PL1 
    R[PG] 
    CC 
If compiler is omitted, the info field applies to all compilers. 
info     is one of the following: 
    A[LL] 
    D[EFAULT] 
or any combination of O[FFSET, L[INE], or T[YPE], separated by commas.  If 
info is omitted, the info field is treated as DEFAULT. 
A complete position report consists of the following fields: 
Primary  +.offset :line# (label),substmnt#,.offset [TYPE] /GMAP6 instruction 
ENTDEF  \________/\_______________________________/\_____/\________________/ 
Field        1                2                       3            4 
Display of fields 1 and 4 is enabled by specifying OFFSET. 
Display of field 2 is enabled by specifying LINE. 
Display of field 3 is enabled by specifying TYPE. 
Field 4 is available only when the report is generated as the result of a STEP 
command. 
Description: 
The REPORT command controls the manner in which DELTA displays position 
references.  DELTA normally displays position reference information based upon 
what compiler produced the object unit from which the current position is 
being displayed. 
Example: 
    REPORT ALL 
    REPORT PL6 OFFSET, LINE 
    REPORT COBOL ALL 
Usage Notes: 
1.  Schema is required for the REPORT command to have any effect.  If schema 
    has been KILLed, or if the object unit that contains the position 
    reference being displayed by DELTA does not have any debug schema 
    associated with it, the REPORT will be identical to REPORT GMAP, i.e., 
    def +.offset (label) 
    where def is the closest primary ENTDEF; or if there are no ENTDEFs less 
    than or equal to the position, def is a user defined symbol (subject to 
    RANGE). 
    label   is an exact matching secondary ENTDEF or SYMDEF. 
2.  The initial defaults for REPORT as a function of compiler type may be 
    displayed by using the REPORT option of the SHOW command when DELTA is 
    first entered. 
00002
00003
00004
00001
00004
Format: 
          [  {NUTS     }] [  {C[OPY] }] 
RU[M] fid [, {UTS=value}] [, {I[NPUT]}] [B[UFFERS] = n] 
                          [  {T[EST] }] 
Parameters: 
fid    is the file identification of the run unit file. 
NUTS    overrides the requirement for creation UTS (Universal Time Stamps) to 
match.  If neither NUTS nor UTS=value is specified, NUTS is assumed.  If the 
run unit is in the system account :SYS, IN must be specified. 
UTS=value    specifies an octal digit string of the form mm/dd/yy hh:mm:ss.ss 
which must match the creation UTS as given to the run unit by the linker.  If 
neither NUTS nor UTS=value is specified, NUTS is assumed.  If the run unit is 
in the system account :SYS, IN must be specified. 
INPUT    specifies to DELTA that the run unit file is to be opened in the 
input mode; therefore, the run unit may only be examined.  (If a file is busy 
or the user does not have write permission to it, the file is opened in INPUT 
mode.)  If neither NUTS nor UTS=value is specified, NUTS is assumed.  If the 
run unit is in the system account :SYS, IN must be specified. 
COPY    creates a new copy of the run unit file with the same name.  This is 
handy if the file is already open and the user wishes to modify the run unit 
without affecting the user of the current generation of the run unit. 
TEST    specifies that patches made are not to be permanently applied to the 
run unit.  The run unit will be opened in the input mode. 
BUFFERS=n    specifies the number of buffers for DELTA to use.  This speeds up 
I/O.  Maximum is 10.  Default is 5. 
Description: 
RUM command causes DELTA to access a run unit file instead of memory for 
accesses made by the MODIFY, FIND, STORE, and DUMP commands.  In this manner 
the programmer can examine and change (apply permanent patches to) the run 
unit.  Patches made with the MODIFY, FIND, and STORE commands are recorded in 
the run unit file and may be displayed at any time with the LIST command.  The 
DISPLAY and LET commands cannot be used in this mode. 
While in RUM mode the patch symbols @, @@, #, and ## can be used (if patch 
space has been included in the run unit) and addresses for these symbols will 
be permanently updated in the run unit for future use.  Patch space may be 
defined in a run unit by including the file B_PATCH from the :LIBRARY account 
in the object file list or using IPATCH and DPATCH options on the !LINK 
command when linking the run unit.  The special symbols $SA and $PRIV may be 
modified to change the start address and privilege flags associated with the 
run unit.  The special pointer symbol $HEAD may be used to address any offset 
within the head record of the run unit. 
Usage Notes: 
1.  When EOM mode is in effect the = and / will activate.  Substitution of 
    blanks for the = and / in the UTS option is acceptable to DELTA. 
00002
00003
00001
00003
STEP
SAVE
Format: 
SAD n 
Parameters: 
n    is a decimal or octal number. 
Description: 
This command specifies which descriptor from the monitor's linkage segment is 
to be associated with the special symbol $SAD.  (See the HOSTMON HELP 
facility's M$SAD description for more information regarding special access 
descriptors.) 
Usage Notes: 
1.  The SAD option of the SHOW command is used to display the currently 
    associated descriptor number. 
2.  The SAD command is not allowed for FEP programs. 
3.  The SAD option of the KILL command disables use of the $SAD symbol. 
00002
00003
00001
00003
Format: 
[id] SA[VE];attachment[;attachment] ... 
Description: 
This command is a keystroke saver.  It saves attachable commands as though 
they were attached to a breakpoint.  The SAVEed attachments may then be 
executed by referring to their id in a DO command. 
00001
STEP_BY
Format: 
SC[HEMA] [position|fid] 
Parameters: 
position    may be any position reference.  If position is omitted, general 
schema usage is reactivated with the defaults in effect as described above. 
fid    is a valid file identifier. 
Description: 
This command is used: 
1.  To reactivate schema usage that has been deactivated by the SCHEMA option 
    of the KILL command. 
2.  To specify the current schema for all nonqualified position or location 
    references. 
There is always some default in effect regarding the current schema unless 
general schema usage has been deactivated by the SCHEMA option of the KILL 
command.  These are: 
1.  In the debug mode, the current schema is the one associated with the ECU 
    indicated by the contents of the Instruction Counter (IC). 
2.  In the RUM mode, the current schema is the one associated with the ECU 
    which contains the start address of the run unit. 
Example: 
    Directive                 Explanation 
    SCHEMA                    Reactivate general schema usage and default 
                              to the current schema as per IC. 
    SCHEMA PROBNAME:556       Consider the schema associated with PROBNAME:556 
                              the current schema. 
Cross Reference: 
See the ALTERNATE VARIABLES command. 
00004
00002
00003
00001
KILL_SHOW
Format: 
{SI[LENT]  }  id [-id   ] 
{UN[SILENT]}     [TO id ] 
Description: 
These commands control the reporting of active breakpoints.  They silence 
redundant reporting once the user determines that a breakpoint or a range of 
breakpoints is achieving the desired results. 
Example: 
     Command                   Explanation 
     SILENT 10-15              Silence the reporting of the 
                               breakpoints in the range 
                               specified. 
     UNSILENT 10-15            Resume reporting of the 
                               breakpoints in the specified 
                               range. 
     SILENT 7                  Silence stored command number 7. 
Usage Notes: 
1.  SILENT may also be specified as an option of the AT command in the 
    following manner: 
         [id] ATS ROUTINE10[;attachment] ... 
    All attachments to a silent breakpoint function normally except MODIFY. 
    The display of the old contents of the modified location is inhibited. 
00001
00002
00003
00003
STEP_ONE_CALL
Format: 
STAT[US] 
Description: 
The STATUS command controls whether or not status information is provided with 
FPL status variables (see STATUS keyword in Table 3-2, Keywords used with KILL 
and SHOW). 
00001
Format: 
S[TEP] [n] 
Parameters: 
n    is an octal or decimal constant specifying the number of steps to be 
taken.  If n is omitted, one step is taken.  The right bracket (]) may be used 
in place of STEP.  The STEP command format then becomes ] or n]. 
Description: 
The STEP command causes execution to proceed for a given number of steps. 
Example: 
    Command            Explanation 
    STEP 5             Take 5 steps (instructions or statements, depending 
                       on the context in which the command is used). 
00002
00003
00001
Format: 
S[TEP] B[Y] mode 
Parameters: 
mode is one of the following: 
    Mode                     Explanation 
    I[NSTRUCTION]            A machine level instruction. 
    SU[BSTATEMENT]           A substatement as defined by the compiler. 
                             A substatement is usually defined as a single 
                             statement in a multiple statement line; that 
                             is, a single source code line in which more 
                             than one statement appears. 
    ST[ATEMENT]              A source statement.  (The default step mode 
                             is STATEMENT.) 
    P[ARAGRAPH]              A COBOL PARAGRAPH, or the next source line 
                             containing a label in non-COBOL ECUs. 
Description: 
The STEP BY command sets a new step mode (unit size), and then steps once. 
Example: 
    Command                Explanation 
    SBI                    Step one instruction and set the step mode to 
                           INSTRUCTION. 
    SBST                   Step to the beginning of the next statement, 
                           and set the step mode to STATEMENT. 
Usage Notes: 
1.  Use SHOW STEP to display the current step mode. 
00002
00003
00004
00001
00004
Format: 
S[TEP] O[NE] C[ALL] 
Description: 
This command temporarily overrides the current step mode without setting a new 
one.  The STEP O[NE] C[ALL] is used only when the current user program 
statement is a CALL statement, PROC statement, or ENTRY statement.  Execution 
will next stop at the statement immediately following the CALL statement, or 
at the ALTRET statement, if the called routine ALTRETURNs.  The current mode 
is unchanged. 
Example: 
    Command                  Explanation 
    SOC                      DELTA will halt execution when the CALLed 
                             routine RETURNS or ALTRETURNs. 
00001
00002
STORE
Format: 
STOP {A[LL]   } 
     {fprg-res} 
Parameters: 
ALL    specifies all FEP programs. 
fprg-res    specifies a particular FEP program.  This is the value the user 
specified for RES on the M$OPEN of the FEP program. 
Description: 
The STOP command causes the specified FEP program(s) to be interrupted.  DELTA 
will report the location at which any FEP programs were interrupted to the 
user and prompt for commands. 
Example: 
    >STOP ALL 
    (UC05) IC=A:10,,.3 [ASSIGNMENT] 
    (UC10) IC=B:310,,.4 [CALL] 
    > 
User can now enter DELTA commands. 
00002
00003
00001
Format: 
STO[RE] pattern [F[ROM] range] [U[NDER] mask] 
Parameters: 
pattern    may be specified in any form that can be resolved into a 36-bit 
pattern.  This includes: 
o   Octal or decimal literals.  These are converted to their binary 
    equivalents (right-justified with zero-fill). 
o   Bit string literals.  These are left-justified with zero-fill when 
    necessary. 
o   Character string literals.  These may not exceed four characters.  They 
    are converted by DELTA into their binary equivalents (left-justified with 
    space-fill where necessary). 
o   Octal string literals.  These are left-justified with zero-fill where 
    necessary. 
o   Any GMAP6 assembler instruction expression (Single word instructions 
    only). 
range    is as described under the FIND command.  The default is the entire 
instruction segment. 
mask    may be any of the above literals, but may not be a GMAP6 instruction. 
If mask is specified, DELTA selects those bits from the pattern which have 
corresponding bits set in the mask and inserts them into the cell.  The 
default is .7777777777777 (-1). 
Description: 
The STORE command modifies every cell in a specified range of cells.  The 
contents of the cell may be completely replaced or replacement may be on a 
bit-by-bit basis under control of a mask. 
Usage Notes: 
1.  The range for STORE is remembered in the same location as the range for 
    FIND ($FRANGE). 
2.  The STORE command is not allowed for FEP programs. 
00002
00001
00003
SYNTAX
A data name, statement label, statement number or any symbolic name assigned 
by using the DEFINE command during a debugging session may be used as a 
symbolic memory reference.  When a symbolic memory reference is made, DELTA 
determines the actual memory addresses associated with the symbol.  The rules 
governing the formation of symbolic names differ among the various programming 
languages.  The symbolic name "X" could be an external procedure name in PL-6, 
a file name in COBOL or an element of an array in FORTRAN.  For this reason, 
language processors place symbols which refer to data addresses (data names) 
and those which refer to procedure addresses (statement labels, statement 
numbers) in different tables within the schema.  DELTA must therefore 
determine which of these tables is to be searched when resolving a symbolic 
reference into a memory address.  For more information, enter ? . 
Resolving A Symbolic Reference 
There are two classes of symbolic references: 
1.  A LOCATION REFERENCE refers to a memory address which contains data. 
2.  A POSITION REFERENCE refers to a memory address that contains an 
    executable instruction. 
DELTA does not require any special user effort to distinguish these 
references.  In some cases, however, it is necessary to override DELTA's 
assumptions about a particular symbolic reference.  This is explained in the 
commentary on those commands where it applies. 
00001
The following six levels of qualification may be required by DELTA to 
accurately resolve a memory reference: 
1.  Domain (XDELTA only) 
2.  Node name (overlaid program only) 
3.  External compile unit name (ECUNAME) 
4.  Internal program unit name (IPUNAME) 
5.  Major structure name (MS) 
6.  Subordinate structure name (SS) 
Most qualification levels are summarized below. 
---------------------------------------------------------------------- 
|Qualifier   |   How specified   |   Example        | Default to:   *| 
|                                                                    | 
|NODE NAME   |   Use Command     |   USE NODE ABLE  |   Current Node | 
|                                                                    | 
|ECU         |   Name of ECU     |   ECUNAME:       |   Current ECU  | 
|                                                                    | 
|IPU         |   Name of IPU     |   IPUNAME:       |   Current IPU  | 
|                                                                    | 
|MS        **|   Name of MS      |   MSNAME.        |   No Default   | 
|                                                                    | 
|SS          |   Name of SS      |   MSNAME.SSNAME  |   No Default   | 
---------------------------------------------------------------------- 
    * For convenience DELTA recognizes what are termed the current node, 
    current external compile unit, and current internal program unit.  They 
    are determined by the contents of the Instruction Counter at the time that 
    the symbolic reference is resolved.  Note that position references are 
    implied by a colon (:). 
  ** DELTA requires that all symbolic references to structures of a data 
    hierarchy be qualified with the name of each structure to which it is 
    subordinate (e.g., to qualify to the level of an elementary item within a 
    three-level structure:  MSNAME.SSNAME.VARIABLE). 
    Note that multiple levels of structure qualification are both allowed and 
    required to whatever level the elementary item is embedded: 
                 MSNAME.SSNAME.SSNAME.SSNAME.VARIABLE 
        LEVELS ->   1      2      3      4      5 
The following subtopics name and describe data entities as they are known to 
DELTA.  The subtopics are as follows:  SCALARS, STRUCTURES, ELEMENTARY_ITEMS, 
ARRAY, POINTER, VARIABLE.  Enter ?? or 
HELP (DELTA) SYMBOLIC_LOCATION_NAMES subtopic 
for more information. 
Scalars 
A scalar is a single item of data, an element. 
Structures 
A structure is a hierarchical set of names that refers to an aggregate of data 
items that may have different attributes.  The various members of the 
structure may be further identified through the assignment of member names. 
There are two kinds of structures: major and subordinate. 
A major structure exists at the highest level of the data hierarchy.  It is 
known as a Level 1 structure to DELTA and is not viewed as being dependent or 
related to any other data construct. 
A subordinate structure exists at some lower level of the data hierarchy 
(meaning some level number greater than 1) and is always contained within some 
structure with a level number less than its own. 
Elementary Item 
An elementary item exists at the lowest level of the data hierarchy. 
Array 
An array is a contiguous, named series of data constructs all of which have 
identical sizes and characteristics.  Because each data construct has the same 
name, they must be referred to by their position within the array for unique 
reference.  DELTA recognizes all forms of arrays exactly as they are declared 
by each of the CP-6 language processors.  The rules that govern subscripting 
and/or indexing in the language through which the array was declared are 
recognized and honored by DELTA in any symbolic location reference. 
Pointer 
A pointer is a location reference construct used to specify a particular 
address in memory.  There are several kinds of pointers.  They will be 
discussed in later paragraphs in the context to which they apply. 
Variable 
A variable is the name used in any general reference to all of the data 
entities named above.  Wherever a distinction in their treatment by DELTA is 
important, they will be referred to by their proper names. 
00004
00003
00005
00001
00002
00006
The following subtopics name and describe procedure entities whose names may 
be used in symbolic position references.  They also identify those whose names 
may be used to qualify both position and location references.  The subtopics 
are as follows:  NODE, EXTERNAL_COMPILE_UNIT, INTERNAL_COMPILE_UNIT, 
ENTRY_NAME, STATEMENT_LABEL, STATEMENT_NUMBER, SUBSTATEMENT, OFFSET, 
FORMAT_FOR_POSITION.  Enter ?? or 
HELP (DELTA) SYMBOLIC_POSITION_NAME subtopic 
for more information. 
Node 
A node is an element in an overlay structure.  A node name is the highest 
level qualifier that can be used in an address reference.  Node applies only 
to overlaid programs. 
External Compile Unit 
An external compile unit (ECU) is the unit of compilation or assembly -- the 
input to the LINK processor.  An ECU name may be used to qualify both position 
and location references.  Note that the ECU name is that name defined within 
the procedure code and not the name given to the object unit file in which it 
is stored. 
Internal Compile Unit 
An internal program unit (IPU) is a logical block within an external compile 
unit which limits the scope of both procedure names and data names.  An IPU 
name may be used to qualify both position and location references. 
Entry Name 
An entry name is an externally known procedure location within an external 
compile unit.  There are primary entry names and secondary entry names.  A 
primary entry name is one which names an external compile unit.  Both may be 
used to qualify position and location references. 
Statement Label 
A statement label names a position within an ECU or IPU that may be used as 
the target of a transfer of program flow. 
Statement Number 
A statement number is that number assigned by a language processor to each 
statement that it translates into object code.  DELTA recognizes statement 
numbers as valid, symbolic position references. 
Substatement 
A substatement is a division of a statement. 
Offset 
An offset is the octal or word offset from the specified 
statement/substatement.  When a substatement is not specified, an offset must 
be preceded by two commas. 
Format For Position 
Position is used in the AT, GO, and GOSTEP commands and sometimes in the 
MODIFY command.  The format for position can be one of the following: 
o   [ECU]:statement number,substatement,offset 
    For the AT, GO, and GOSTEP commands, if ECU is omitted, the colon is 
    optional.  For the MODIFY command, the colon is required.  The offset may 
    be specified in octal or decimal.  For example, 
    :10,1,.1 
o   ECU{:INTERNAL ENTRY, ... }:label, substatement, offset. 
    Label must be fully qualified by all INTERNAL ENTRIES necessary. 
Example: 
    PROGNAME:PROCA:PROCB:LABEL1 
o   ECU + offset 
    PROGX+.54 
o   octal address 
The octal address must be preceded by a period to be octal. 
    .2004 
Note: 
1.  2004 will be interpreted as: 
    a.  statement 2004 if used with an AT, GO, or GOSTEP command 
    b.  decimal location 2004 (octal location .3724) if used with any other 
        command. 
00004
00002
00009
00003
00001
00008
00005
00006
00007
Format: 
SY[NTAX]  [compiler] 
Parameters: 
compiler    is one of the following: 
    F[ORTRAN] 
    FP[L] 
    C[OBOL] 
    P[L6] 
    R[PG] 
    G[MAP] 
    PL1 
    CC 
Description: 
The SYNTAX command tells DELTA how symbols, expressions, and structure 
references are specified. 
The initial default of SYNTAX is the compiler that produced the main program 
of the run unit being debugged.  If compiler is omitted, the initial default 
compiler will be used.  As far as DELTA is concerned PL6, RPG, GMAP6 and PL1 
are identical and COBOL and FPL are identical; thus, three types of distinct 
SYNTAX can actually be specified: SYNTAX PL6, SYNTAX COBOL, and SYNTAX 
FORTRAN. 
The character set for symbols in each SYNTAX specification is identical to the 
character set allowed in the language definition.  The major difference 
between SYNTAX COBOL and SYNTAX PL6 is that the embedded dash or minus sign 
(-) is allowed in SYNTAX COBOL.  This difference gives rise to the difference 
in expressions in SYNTAX COBOL and SYNTAX PL6.  In SYNTAX PL6, the expression 
operators (-,+,*,%,>>,<<) must separate the expression elements (symbols, 
constants, etc.) with no separating blanks.  Conversely, in SYNTAX COBOL the 
expression operations must be separated from the expression elements by 
leading and trailing blanks. 
In SYNTAX PL6, structure items are separated by periods, in order of major 
level identifier followed by minor level identifiers.  A SYNTAX PL6 structure 
reference must be fully qualified. 
In SYNTAX COBOL, structure items are separated by the keywords IN or OF.  The 
major level structure item is specified last, as is natural in the COBOL 
language.  A COBOL structure reference may take one of three forms.  In the 
first type of reference, only one identifier is specified.  The reference will 
be satisfied by the first variable name that matches the given identifier, 
regardless of actual structure level.  In the second type of reference, two 
identifiers are specified.  The major structure name must be the second 
identifier specified.  In the third type of reference, any number of 
identifiers may be specified.  The reference must be fully qualified by 
specifying all low level references and the major structure name must be the 
last identifier specified. 
The SYNTAX command also tells DELTA how to interpret decimal constants for the 
LET command.  For SYNTAX PL6, .octal-digit-string is considered to be a right 
justified octal constant.  For SYNTAX FORTRAN, .decimal-digit-string is 
considered to be a floating point (real) constant.  For SYNTAX COBOL, 
.decimal-digit-string is considered to be a fixed point decimal constant. 
(See the LET command for more information about constants.) 
Example: 
    SYNTAX   COBOL 
    DISPLAY  D IN A 
    SYNTAX   PL6 
    DISPLAY  A.B.C.D 
    SYNTAX   FORTRAN 
    LET REAL 3E21 
Usage Notes: 
1.  When SYNTAX COBOL is in effect, it is possible to specify a non-fully 
    qualified reference that DELTA considers valid, but that the COBOL 
    compiler will consider ambiguous.  The ambiguous reference which DELTA 
    finds is undefined. 
2.  The SYNTAX command is likely to be useful only when a run unit consists of 
    object units produced by different compilers. 
3.  The SYNTAX option of the SHOW command displays the current setting of the 
    SYNTAX mode. 
00002
00003
00004
00001
00004
STEP_ONE_CALL
Format: 
T[RACE] {[X] C[ALLS][S]   [prefix]} 
        {transfer-type[S] [prefix]} 
        {O[N]                     } 
        {OF[F]                    } 
Parameters: 
X    specifies that only external calls are to be traced. 
prefix    specifies that calls to procedures whose name begins with the 
character string defined by prefix are to be traced for TRACE CALLS. 
Specifies that DELTA will only report transfers FROM object units with the 
specified prefix for TRACE TRANSFERS. 
OFF    turns current TRACE mode off. 
ON    turns current TRACE mode on. 
S    specifies tracing is to be silent, i.e., entries are to be made to the 
history buffer, but are not displayed.  They may be displayed later with the 
HISTORY command. 
Transfer type is one of the following: 
  Transfer Type       Description 
  T[RANSFERS] 
                      Traces all TSX instructions. 
  S[TATEMENTS] 
                      Traces branches to the first instruction of a statement. 
  P[ARAGRAPHS] 
                      Traces branches to the first instruction of a COBOL 
                      paragraph or to source lines containing labels in 
                      non-COBOL ECUs. 
Description: 
The TRACE command is used to invoke the maintenance of a history buffer by 
DELTA.  The contents of the buffer are dependent upon the type or types of 
trace specified by the various options of the commands. 
Example: 
    Command                          Explanation 
    TRACE X CALLS                    Trace calls to all external procedures. 
    TRACE CALLSS                     Trace all calls, silently. 
    TRACE CALLS S                    Trace all calls to procedures whose names 
                                     begin with S. 
    TRACE TRANSFERS                  Trace all TSX (transfer) instructions. 
    AT FMN$OPNF:100;TRACE CALLS;GO   When control is received at FMN$OPNF:100, 
                                     activate the TRACE CALL mode and proceed. 
Usage Notes: 
1.  SHOW TRACE displays the current TRACE mode, and KILL TRACE is used to 
    remove the current TRACE mode. 
00002
00003
00004
00001
00004
KEEP_TRAP_IGNORE
Format: 
TSA .hex 
Parameters: 
 .hex    is a four-digit hexadecimal address. 
Description 
The TSA command formats a trap save area starting at the specified hexadecimal 
address.  This is only useful for programs (user, handler) running in the FEP. 
00002
00001
USE
SILENT_UNSILENT
Format: 
        [{O}] [{dcb# [{ - dcb#}]}] 
UNF[ID] [{C}] [{     [{TO dcb#}]}] 
              [{dcbname         }] 
Parameters: 
O    specifies only open dcbs. 
C    specifies only closed dcbs. 
dcb#    is the number of the DCB as assigned by the linker specified as a 
decimal or an octal value.  (Examples:  10 and .12) 
dcbname    is a DCB name such as M$SI. 
Description: 
The UNFID command performs the M$UNFID monitor service on the specified DCB 
and prints the results.  If dcbname is given, rather than the range, the O or 
C specification is ignored.  If no range or dcbname is given, all DCBs 
(subject to the O or C specification) are UNFIDed. 
Example: 
    >UNF M$UC 
    DCB #3 M$UC UC# (OPEN, UPDATE, TERMINAL) 
00002
00003
00001
Format: 
        [A[LL] 
UNSHARE [P[ROGRAM]] 
        [L[IBRARY]] 
Parameters: 
ALL    specifies both the program and library.  PROGRAM is the default. 
Description: 
The UNSHARE command causes the program and/or library of an autoshared run 
unit to be unshared via the M$UNSHARE monitor service call. 
00002
00001
SILENT_UNSILENT
UPDATE_OPEN
Format: 
UP[DATE]  id[ ,m]  text 
Parameters: 
id    is the identification of a stored command. 
m    is the attachment number. 
text    is the text to replace attachment m of stored command id. 
Description: 
The UPDATE command replaces attachment m of the specified stored command with 
replacement text.  Attachment zero is the stored command.  If attachment m 
does not exist an error message is given.  If m is not specified, the 
replacement text is added as an attachment to the end of the specified stored 
command.  If attachment m is replaced with all blanks, attachment m is 
deleted. 
Example: 
    Command                  Explanation 
    UPDATE 1,2 DI ALPHA      Replace the second attachment of stored 
                             command 1 with the text 'DI ALPHA' 
    UPDATE 3 PLUGH           Add the text 'PLUGH' as an attachment to 
                             the end of stored command 3. 
    UPDATE 2,0  AT PROG:100  Replace stored command 2 with the text 
                             'AT PROG:100' 
00002
00003
00001
Format: 
UP[DATE][A]  id[-id] 
     or 
UP[DATE]     id,m 
Parameters: 
id    is the identification of a stored command. 
A    indicates that UPDATEing is to be done an attachment at a time. 
m    is the attachment number. 
Description: 
The first format displays stored commands id to id, stopping at the end of 
each to allow modification of the stored command.  If A is specified, for 
stored commands id to id, an attachment at a time will be printed, stopping at 
the end of each attachment to allow modification.  Entering linefeed causes 
the next attachment or stored command to be displayed stopping at the end to 
allow modification.  Entering an up-arrow causes the previous attachment or 
stored command to be displayed stopping at the end to allow modification.  A 
carriage return ends updating on the current stored command.  If a stored 
command is greater than 256 characters in length and A was not specified, a 
message will be given and the stored command will be updated one attachment at 
a time. 
The second format will print attachment m of stored command id, stopping at 
the end to allow modification of that attachment. 
Example: 
    Command                  Explanation 
    UPDATE 1-4               Prints the stored commands in the 
                             range specified stopping at the end of 
                             each to allow modification. 
    UPDATEA 5-10             The stored commands in the range 
                             specified are printed an attachment at 
                             a time stopping at the end of each 
                             attachment to allow modification. 
    UPDATE 3,2               Prints the second attachment of stored 
                             command 3 stopping at the end to allow 
                             modification of that attachment. 
00002
00003
00001
UPDATE_CLOSED
UPDATE_OPEN
Format: 
U[SE] {fprg-res} 
      {H[OST]  } 
Parameters: 
fprg-res    specifies a particular FEP program.  This is the value the user 
specified for RES on the M$OPEN of the FEP program. 
HOST    specifies the host program. 
Description: 
The USE command is used to specify a particular program the user wants to 
examine.  If the specified FEP program is running, it will be stopped for the 
user to examine it. 
    Example:                     Explanation: 
     >USE UC05                   This specifies the FEP program 
                                 identified by UC05. 
     >USE HOST                   This specifies the host program. 
Usage Notes: 
1.  When a USE command is done by the user, DELTA will remember the state of 
    the program being USEd and if another USE command is done without GOing 
    the first program, the first program will be returned to its original 
    state. 
00002
00001
00003
USE_NODE
Format: 
U[SE]   {N[ODE] nodename} 
        {[CURRENT]      } 
Parameters: 
nodename    specifies the name of an overlay node.  When CURRENT is specified 
the schemata for the overlay nodes currently in memory are re-established. 
Description: 
The USE command is used to specify the name of a program overlay when running 
in the debug or RUM mode of DELTA. 
When the command is issued, the schemata associated with the overlay node and 
its backward path are activated so that symbolic references may be made using 
symbols defined within the overlay schemata. 
Special Considerations: 
The USE NODE command sets breakpoints at procedure positions within overlay 
nodes that are not in memory.  This command prevents waiting for those 
operations until the overlay node is loaded into memory.  DELTA does not, 
however, prevent an attempt to modify a location by using a symbolic location 
reference in either the LET or MODIFY command.  If the overlay node named in 
the USE NODE command is not actually in memory, the contents of memory which 
that symbol would occupy if it were in memory will be changed and no warning 
would be issued by DELTA.  To modify a location in a overlay node not in 
memory, the ON NODE command is used to cause a breakpoint when the overlay 
node is loaded.  See the Usage Notes for more information. 
Example: 
Assume that the target run unit consists of five ECU's in the following tree 
structure: 
                       --------- 
                  |----|NDBAKER| -ECUB-ECUC 
                  |    --------- 
                  | 
                  | 
    --------      | 
    |NDABLE| -ECUA- 
    --------      | 
                  | 
                  |    ------- 
                  |----|NDDOG| -ECUD-ECUE 
                       ------- 
where 
NDABLE    is a node containing an external compile unit ECUA. 
NDBAKER    is a node containing ECUB and ECUC. 
NDDOG    is a node containing ECUD and ECUE. 
Upon initial entry to DELTA, the user wishes to establish breakpoints at 
statement number 50 in ECUB, statement number 100 in ECUE, and statement 
number 50 in ECUA. 
    Command                  Explanation 
    AT 50                    Having entered DELTA, the root node (NDABLE) 
                             is in memory and ECUA is implicit; therefore, 
                             no qualification was necessary. 
    USE NODE NDBAKER         NDBAKER is the node name for the set of ECU's 
                             ECUB and ECUC. 
    AT ECUB:50               Qualification is required to distinguish 
                             statement number 50 in ECUB from statement 
                             number 50 in ECUC and ECUA. 
    USE NODE NDDOG           This specifies the node containing ECUE. 
    AT ECUE:100              ECUE is used to qualify the desired statement 
                             number. 
Usage Notes: 
1.  When USE NODE is used in the RUM mode, the overlay is made to look as if 
    it is in memory, i. e., instructions and data are brought in as well as 
    schema.  Any modifications made while USE NODE is in effect will be made 
    to the location in the named overlay node, and not to the root node. 
2.  The USE NODE command is not allowed for FEP programs. 
00002
00004
00005
00001
00003
00005
USE_NODE
WHEN
Format: 
WA[IT] 
Description: 
The WAIT command causes DELTA to wait for the next event from an FEP program, 
i.e., hitting a breakpoint, trap, etc.  This command is especially useful 
after the user has done a GO to one or two FEP programs, does not want the 
Host program to continue execution, and wants to wait for the next breakpoint 
or trap in one of the executing FEP programs. 
00001
Format: 
[id] W[HEN] item [relation constant] [#n] 
    [condition][; attachment[; attachment] ... ] 
Parameters: 
id    is a decimal number from 1 to 99. 
item    is an elementary item, structure or substructure, or single element of 
an array.  A range of array subscripts may not be specified.  See HELP 
commands for more information. 
relation    any of the relations legal in the IF attachment ,e.g., =, >, <, 
GT, LE, etc. 
constant    any of the literal constants known to DELTA, e.g., 7, 'ABCD', 2.2, 
'0'B, .134, etc. 
#n    specifies the number of times to bypass the breakpoint with a true 
condition before allowing it to be executed. 
condition    an IF attachment. 
Description: 
This stored command causes data breakpoints to occur when the value of a named 
variable or structure changes. 
Example: 
In the examples in this subsection, assume the following program section is 
defined: 
    DCL 1 LEN_REC STATIC, 
          2 NAME, 
            3 LN CHAR(12), 
            3 FN CHAR(10), 
            3 MI CHAR(1), 
          2 SSN CHAR(9); 
Command                Explanation 
WHEN SSN               Halt execution when the value of SSN changes 
                       from the value it had when the command was 
                       first issued.  Both of the following statements 
                       could cause the example data breakpoint to be 
                       hit: 
                       SSN = ' '; 
                       LEN_REC = IN_REC; 
WHEN FN EQ '**'        Halt execution when the value of FN is changed 
                       to '**'.  Note that if FN is equal to '**' when 
                       the command is issued, the data breakpoint 
                       will not be hit until FN is changed to 
                       something other than '**', and then back to 
                       '**'. 
WHEN SSN='999999999';  This example shows that attachments can be made 
DISPLAY NAME;GO        to WHEN in the same manner as the AT command. 
                       The IF conditional may also be used. 
Usage Notes: 
1.  If more than one data breakpoint variable is changed at the same time, 
    only the breakpoint with the smallest ID is considered to be hit.  For 
    example, consider the following two breakpoints, using the structure 
    defined above: 
        4  WHEN NAME 
        5  WHEN SSN 
    The statement MOVE SPACE TO LEN_REC would cause only breakpoint 4 to be 
    hit, and not 5, even though the value of SSN may have changed.  If NAME 
    was already equal to space, but SSN was not, breakpoint 5 would be hit in 
    this example, since the value of NAME did not change. 
2.  While duplicate positions are not legal for multiple AT commands, 
    duplicate variables may be specified for WHEN, e.g., 
        WHEN A>10 
        WHEN A<4 
    can exist together.  If two or more data breakpoints are hit at the same 
    time (overlapping conditions or data), only the first (smallest id) will 
    be honored. 
3.  If a variable is used as a subscript for an array, the value of the 
    variable subscript is stored in the WHEN command, and not the variable. 
    For example, assume the value of A is 7.  WHEN ARRAY(A) is stored as WHEN 
    ARRAY(7) by DELTA. 
4.  Data breakpoints are very costly in terms of computer resources.  They 
    will greatly increase the execution time of the program, more so than any 
    other DELTA command.  DELTA works with the CP-6 monitor to watch the 
    variables in the program change in value.  The smallest area of memory 
    that can be watched is a page (that is 1,024 words) of memory.  This means 
    that if WHEN A is specified, DELTA is notified anytime anything on the 
    page or pages containing A is modified.  DELTA then checks to see if the 
    value of A has changed.  If all of the variables in the program are stored 
    in the same page of memory, DELTA is entered every time any variable is 
    modified, or just about every statement. 
    Always try to localize the area of the program that is to monitor a 
    variable.  For example, assume you, the user, are only interested in 
    changes made to A between statements 100 and 150.  The following method 
    can be used to reduce the amount of overhead used by DELTA. 
        >10 WHEN A                 Defines the breakpoint assigned with a 
                                   number of 10. 
        >INACTIVE 10               Turns it off. 
        >ATS 100; ACTIVE 10;GO     Silently turns it on at 100. 
        >ATS 150; INACTIVE 10;GO   Silently turns it off at 150. 
    AT is much less costly than having a data breakpoint in effect all the 
    time.  After the WHEN has served its purpose, KILL it. 
5.  The WHEN command is not allowed for FEP programs. 
00002
00003
00004
00001
00004
XEQ
Format: 
XC[ON] 
Description: 
This command simulates an exit control condition, that is, a condition which 
will cause entry to the routine specified in an M$XCON monitor service call. 
It is most useful in avoiding the one condition where having DELTA associated 
with a run unit will cause different results. 
Assume a run unit has an exit control (M$XCON), but not a trap control 
(M$TRAP) routine.  When the program runs without DELTA, any error or abort 
condition will cause direct entry to the exit control routine.  However, when 
the program runs under the control of DELTA, these conditions are caught and 
held by DELTA, and reported to the user.  In this case, the GOTRAP command 
will not work:  DELTA checks to ensure that the program has a trap routine for 
the error or abort condition.  The XCON command must be used to give control 
to the exit control routine. 
The XCON command may also be used to give control to an exit control routine 
for exit conditions such as M$EXIT, M$ERR, M$XXX, and M$SAVE or M$LDTRC.  In 
these cases, GOTRAP will work, since DELTA treats the exit control routine 
specified by M$XCON as a trap control routine for exit conditions.  The TRAP 
XCON command will also work for exit conditions, for the same reason. 
00001
Format: 
X[EQ]  instruction 
Parameters: 
instruction    must be specified as a GMAP6 instruction mnemonic.  X0 through 
X7 may be used in the tag field to denote indexing.  All tag mnemonics are 
recognized, and in addition the tag field may be specified as a decimal number 
(0-7 only) to indicate indexing with X0-X7, or the tag field may be given in 
octal in which case it will be used as given.  The PR field may be specified 
mnemonically with PR0 through PR7 or with the decimal numbers 0 through 7. 
Description: 
The XEQ command causes the immediate execution of a single word machine 
instruction.  XEQ is not allowed on certain types of instructions such as 
transfers. 
Usage Notes: 
1.  The XEQ command is not allowed for FEP programs. 
00002
00001
00003
