The Job Information Table (JIT) contains system related information about an 
individual CP-6 user.  From logon to logoff time, the JIT is used to 
accumulate and retain facts about the user's session. 
The B$JIT file in :LIBRARY contains a BASED structure for the JIT.  This 
structure my be addressed using the Linker built pointer "B$JIT$". 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1992 
  ************************************************************** 
The following fields are contained in the JIT: 
    ACCEPT_FLAGS.  The ACCEPT_FLAGS field contains the items set either by 
    M$TRMISC or the ACCEPT, DONT ACCEPT IBEX commands. 
    ACCEPT_FLAGS.ANNOUNCE - BIT(1).  The ANNOUNCE field is a flag which, if 
    set, specifies the user will accept tape and disk mount announcements. 
    ACCEPT_FLAGS.BROADCAST - BIT(1).  The BROADCAST field is a flag which, if 
    set, specifies the user will accept operator messages sent via the 
    BROADCAST and SENDALL keyins. 
    ACCEPT_FLAGS.SEND - BIT(1).  The SEND field is a flag which, if set, 
    specifies the user will accept operator messages sent via the SEND keyin. 
    ACCESS.  The ACCESS field contains counts of various kinds of physical 
    accesses to devices. 
    ACCESS.FORMS - SBIN.  The FORMS field counts the number of physical 
    accesses to resource devices other than disk or tape (e.g. resource Line 
    Printer). 
    ACCESS.PACKS - SBIN.  The PACKS field counts the number of physical 
    accesses to files during this job or session. Also included are requested 
    physical accesses which were satisfied by the I/O cache. 
    ACCESS.TAPES - SBIN.  The TAPES field counts the number of physical 
    accesses to tapes during this job or session. 
    ACCN - CHAR(8).  The ACCouNt field contains the user's log on account. 
    APATTR - BIT(18).  The APATTR field contains the attributes to be 
    requested when a floating point array processor is opened.  This field is 
    set via the !RES or !ORES command in IBEX. 
    ARECX - UBIN(16).  The Accounting RECord indeX field contains the key to 
    be used in the next resource accounting record to be written to *S. This 
    field is incremented each time a resource accounting record is written. 
    B$JIT0_ES_MODES.  This macro specifies equates used for security logging. 
    This is to accommodate additional attribute types known at logon which are 
    never found in the JIT but may be interesting for security purposes. 
    BILL - CHAR(6).  The BILL field is used to locate the user's charge rate 
    record. 
    BLINDACCTNG - BIT(1).  The BLIND ACCounTiNG field is a flag which, if set, 
    specifies that this user is only to see resources used, and not charge 
    rates or actual monetary units. 
    BUDLIM - SBIN.  The BUDget LIMit field contains the amount of charges 
    which this job or session is allowed to incur. This field is recorded in 
    hundredths of pennies. 
    CALCNT - SBIN.  The CALCNT field contains the total number of monitor 
    services (PMMEs) executed during this job or session. 
    CCARS - SBIN HALF.  The Control Command Actual Record Size field contains 
    the size of the last run unit invocation command. 
    CCBUF - CHAR(256).  The Control Command BUFfer contains the the text of 
    the first record of the last run unit invocation. 
    CCDISP - SBIN HALF.  The Control Command DISPlacement field contains the 
    position within the last run unit invocation at which the beginning of 
    options may be found. 
    CHECK_CFU - BIT (1).  This flag is set if a CFU is still associated with 
    an ALTKEY file that has gone through run down. 
    CLRES - ARRAY(0:2) BIT(1).  The Communication Line RESource field contains 
    permission bits which allow users to use CL resources without reserving 
    them via !ORES.  Since !ORES CL is not valid, the last entry 
    B$JIT.CLRES(2) indicates that the user is allowed unlimited access to CL 
    devices. 
    CPFLAGS1 - BIT(36).  CPFLAGS1 is used by the monitor to communicate with 
    the command processor and is also available for use by the command 
    processor as a word where he may remember user directives. 
    Bits 0 -> 8 are used by the monitor to communicate job step information to 
    the command processor. These bits are not to be set or reset by the 
    command processor. The meanings of these bit settings are: 
        CP_LOGOFF#     When set indicates that the system has 
     '400000000000'O   detected a line hang-up of a time-sharing 
                       terminal or an operator abort of a user 
                       and indicates to the command processor that 
                       no more job steps are allowed.  This bit may 
                       be set in conjunction with any of the other 
                       CPFLAGS1 bits that are owned by the monitor. 
        CP_JSTEP#      Indicates that the user is at Job Step. 
     '200000000000'O   Unless the user is at Job Step, another 
                       run unit may not be started. 
        CP_RUND#       Indicates that all levels of exit control 
     '100000000000'O   processing are completed and the user is 
                       about to be rundown.  The program image is 
                       intact; a debugger may be associated or 
                       the program image may be SAVEd. 
        CP_YC#         Indicates that the command processor is 
     '040000000000'O   being entered because the time-sharing 
                       user has typed the Control-Y sequence. 
                       The user program image is intact; a debugger 
                       may be associated or the program image may 
                       be SAVEd. 
        CP_YCPMME#     Indicates that the command processor is 
     '020000000000'O   being entered because of an M$YC monitor 
                       service request. 
        CP_SSTART#     Used only by the monitor.  Indicates that 
     '010000000000'O   a Start Step Accounting record has been 
                       written.  This bit is reset when the Stop 
                       Step Accounting record is written. 
        CP_LNKPMME#    Indicates that the command processor is 
     '004000000000'O   being entered because of an M$LINK or M$LDTRC 
                       monitor service request specifying a command 
                       to be parsed by the command processor.  CP_JSTEP# 
                       will also be set if the request were M$LDTRC.  In 
                       either case, the user program will have been 
                       rundown. 
    The following bits are also used for monitor / command processor or LOGON 
    / command processor communication: 
        CP_YCGET# Set in conjunction with CP_YC# after a successful M$CPEXIT 
     '001000000000'O   with GET specified.  The command processor should reset 
                       this flag after using it. 
        CP_STARSACC#   Set by LOGON if the '*S_ACCOUNTING' option 
     '000020000000'O   of SUPER was specified for this user.  When 
                       this bit is set, :ACCTLG records will be 
                       written to the user's *S file as well. 
      CP_LASTCPEXISTS# Set by LOGON if the 'LAST CPROC' option 
     '000010000000'O   of SUPER has been specified for this user. 
                       Indicates that the default Command Processor is 
                       to make its final M$CPEXIT to this user's logoff 
                       command processor as specified in the :USERS 
                       file (AS$USERS.LASTCPROC.NAME, which is 
                       indexed by mode) and not use the delete user 
                       form of M$CPEXIT. 
        CP_LASTCP#     To be set by the command processor when issuing 
     '000004000000'O   an M$CPEXIT to the logoff command processor. 
                       This allows one final job step after the monitor 
                       has set CP_LOGOFF#. 
        CP_FIRSTCP#    LOGON sets this bit when exiting to the user's 
     '000002000000'O   command processor.  The command processor 
                       finds this bit set should reset it. 
        CP_STARPROC#   Set by the monitor whenever a proprietary 
     '000001000000'O   accounting record is written to the *S file. 
                       Refer to M$ACCT in the Host Monitor Services 
                       Reference Manual. 
        CP_DRIBBLE#    To be set and reset by the command processor 
     '000000100000'O   to indicate to the monitor if interactive 
                       terminal transactions are to be recorded on 
                       the file or device assigned to the M$DRIBBLE 
                       DCB. 
        CP_EXIT#       Set by the monitor to indicate that the error 
     '000000020000'O   in JIT.USRERR is not to be reported to the user. 
                       The command processor should, however, use the 
                       value of JIT.USRERR.SEV as the severity level 
                       of the error message last reported to the user. 
        CP_KEEPDS#     This bit may be set by the command processor 
     '000000010000'O   to indicate that the monitor is not to release 
                       the command processor dynamic data segments. 
        CP_PROCACCT#   Set by the monitor whenever a run unit from the 
     '000000001000'O   :SYS account that has been LINKed with the 
                       SURCHARGE option is put into execution.  When 
                       this bit is set, the monitor will cause 
                       proprietary start and stop records to be 
                       written to the *S file. 
        CP_STEPACCT#   Set by LOGON if the 'STEPACCNT' option of 
     '000000000400'O   SUPER was specified for this user.  When set, 
                       the monitor will cause job step start and stop 
                       records to be written to the *S file. 
    The remainder of the bits in CPFLAGS1 may be used as seen fit by the 
    command processor.  IBEX has predefined the bits for a specific use as 
    follows: 
        CP_WHEN_INPUT# This flag is set by IBEX to indicate that the user 
     '000400000000'O   has input a WHEN command and that a WHEN control 
                       record has been written to the *S file. 
        CP_ECHO_LINK#  This flag is set by the monitor for M$LINK with 
     '000200000000'O   both CP_CMD and ECHO set; reset if CP_CMD specified 
                       and ECHO not specified. 
        CP_DONTRFEXT3# This flag tells IBEX not to RESET FEXT bit for #3 
     '000100000000'O   because the file name was *G.  This is for when 
                       IBEX is at JOBSTEP. 
        CP_SOMENOTIFY# There is something to NOTIFY user. 
     '000040000000'O 
        CP_SKIPABORT#  Don't abort user at this time 
     '000000040000'O 
        CP_TRMNATE#    Logoff this user after rundown 
     '000000004000'O 
        CP_NOTIFY#     NOTIFY user of changes in BATCH jobs 
     '000000002000'O 
        CP_STEPLMT#    Step limits in effect 
     '000000000200'O 
        CP_PROTECT#    Don't prompt !quit 
     '000000000100'O 
        CP_BUFFULL#    Command in B$JIT.CCBUF 
     '000000000040'O 
        CP_CFREAD#     Read from XEQ file 
     '000000000020'O 
        CP_ECHO#       Echo commands from XEQ 
     '000000000010'O 
        CP_BRK#        Break received 
     '000000000004'O 
        CP_SCREECH#    Prevent multiple snaps when IBEX aborts 
     '000000000002'O 
        CP_DELTA#      !U command found 
     '000000000001'O 
    CSLEV - UBIN(9).  This field holds the Command Stream LEVel.  If file A is 
    being XEQed the command stream level would be 1.  If A XEQs a file B, the 
    command stream level for B would be 2.  If CSLEV is 0, then the last 
    command was not read from an XEQ file, i.e., a command input by an on-line 
    user.  (See mode to tell what type of user.)  This field is maintained by 
    File Management. 
    CTIME - SBIN.  The Compensatory TIME field contains the number of 
    microseconds by which this quantum will be shortened due to I/O 
    operations.  This value is the number of physical I/O operations done this 
    quantum times the I/O Time Allowance (IOTA) for the user's mode. 
    CURPNUM - SBIN HALF.  The CURPNUM field is incremented every time a run 
    unit that is the target of an M$LINK or M$LDTRC request is put into 
    execution.  This field is decremented when that run unit exits.  CURPNUM 
    and HIGHPNUM are used when processor accounting is in effect. 
    CURRCORE - UBIN HALF.  The CURRent CORE field contains the current number 
    of memory pages chargeable to this user. This value is the result of the 
    following calculation. CURRCORE = PCD + PCDD + PCDS + PCDDS + PCADS + PCL 
    + PCV + PCROS - 1. PCP is also added unless MMFLGS.FREE_PPGS is set. 
    CURSUDO - ARRAY(0:7) UBIN BYTE.  The CURrent pSeUDO field contains the 
    current number of each pseudo resource defined which is currently 
    allocated to this job or session. The order is as defined by TIGR. 
    CURTMPDP - SBIN.  The CURrent TeMP Disk Pack field contains the current 
    number of granules of temporary disk space allocated. 
    DCB$ - PTR.  Contains a pointer to the DCB that was specified on the 
    current monitor service request.  If the service request doesn't have a 
    DCB associated with it, this value will be nil.  As with JIT.DCBNO, 
    JIT.DCB$ should not be referenced by the user program. 
    DCBNO - UBIN(9).  Contains the number of the DCB that was specified on the 
    current monitor service request.  If the service request doesn't have a 
    DCB associated with it, this value will be zero.  If an ALTRETURN is made 
    to the user request, this field will be placed in the ALTRET frame along 
    with the value from JIT.ERR.  As with JIT.ERR, JIT.DCBNO should not be 
    referenced by the user program. 
    DDLL - UBIN HALF.  The Dynamic Data Lower Limit field contains the virtual 
    page number of the first page in the Instruction Segment that may be used 
    for dynamic data. 
    DDUL - UBIN HALF.  The Dynamic Data Upper Limit field contains the virtual 
    page number of the last page in the Instruction Segment that may be used 
    for dynamic data. 
    DEFEXP - SBIN HALF.  The DEFault EXPire field contains the default value 
    for the duration that a file created by this user will be unexpired. This 
    value is used if no expiration date is specified when a file is created. 
    DEFPRI - UBIN BYTE.  The DEFault PRIority field contains the default batch 
    priority to assign to jobs batched by this job or session. 
    DLL - UBIN HALF.  This field contains the Data Lower Limit, which is the 
    virtual page number of the first data page of the run unit or standard 
    shared processor currently executing. 
    DO$ - PTR.  The DO$ field contains a pointer to an active do-list entry 
    used during several file management operations. 
    DUL - UBIN HALF.  This field contains the Data Upper Limit, which is the 
    virtual page number of the last data page of the run unit or standard 
    shared processor currently executing.  If the user is at job step, JIT.DUL 
    will be set to JIT.DLL -1. 
    ENQS - UBIN(18).  The ENQS field contains the current number of ENQue 
    resources owned by this job or session. 
    ERR.  The ERR field in the JIT always contains the "current" error code 
    reported on this user.  This field will be moved to the ALTRET or Stack 
    Frame on the Task Control Block of the domain (user, alternate shared 
    library, debugger or command processor) in control at the time of the 
    error.  If this is the error to be reported to the user following all 
    levels of exit control processing, this field will be moved to JIT.USRERR. 
    In any event JIT.ERR is subject to change on any change of domain and 
    should therefore never be referenced by the user program.  JIT.ERR is in 
    VLP_ERRCODE format and contains the following subfields: 
    ERR.CODE - UBIN(14).  This field contains the number (0-16383) that 
    identifies a particular error condition.  The file B_ERRORS_C contains a 
    list of the error codes reported by the monitor. 
    ERR.FCG - BIT(12).  This field contains the two special six bit characters 
    that identify the functional code group that is reporting the error.  Each 
    character is composed of the low-order 6 bits of the ASCII code. 
    ERR.MID - BIT(6).  This field contains the special six bit character that 
    identifies which module in the functional code group is reporting the 
    error.  This character is composed of the low-order 6 bits of the ASCII 
    code. 
    ERR.MON - BIT(1).  This bit is set if this error is reported by the 
    monitor; reset if reported by a processor. 
    ERR.SEV - UBIN(3).  This field serves a double purpose.  Within the 
    monitor it is used to indicate the seriousness of an error.  When passed 
    by the user to M$ERRMSG it indicates the level of detail requested in the 
    error message.  SEV can range from 0 - 7. 
    EUP - UBIN HALF.  The End User Page field contains the highest virtual 
    page number in the instruction segment which is available for user 
    allocation. 
    EXTUS - UBIN.  The EXecution Time microseconds field contains the number 
    of microseconds (0-9999) of execution time which were not able to be 
    reflected in TPEXT or TUEXT at the end of the previous quantum. 
    FACCN - CHAR(8).  The File ACCouNt field contains the users default file 
    account.  This field is used as the account for any file reference made 
    when an account is not explicitly specified. This field may be freely be 
    changed by the user, and is not used to determine accessibility of files. 
    See M$SETFMA, !DIRECTORY. 
    FACNACS - BIT(18).  The File ACcouNt ACceSs field contains the account 
    permissions for this user vis-a-vis his current file account (FACCN). 
    FACNCM - UBIN(9).  The File ACcouNt Character Match field contains the 
    number of characters of FACCN which matched on a wild compare. 
    FBUC - UBIN HALF.  The File Buffer Use Count field contains the total 
    number of file buffers (FPOOLs) currently in use by this user. 
    FBUL - UBIN HALF.  The File Buffer Upper Limit field contains the maximum 
    number of file buffers which file management will use on this user's 
    behalf.  See !LIMIT FPOOL=n. 
    FEXT - ARRAY(0:35) BIT(1).  The File EXTension field contains bits which 
    specify whether ('1'B) or not automatic file extension is currently active 
    on the four command line DCBs as well as a number of DCBs of the form 
    M$xx, where xx is any of a set of CP-6 special names. 
    FPSN - CHAR(6).  The File PackSet Name field contains the packset name 
    which is to be used in conjunction with FACCN for default file references. 
    FRS - BIT(9).  The Final Run Status field contains the accumulated abort 
    flags.  This is a logical OR of all the flags that may appear in bits 0 
    through 4 of RNST as the job step is rundown through all the various 
    levels of exit control.  Refer to RNST for the EQUated values and the 
    meanings of the bit settings in this field. 
    For example, if a user is aborted by the operator, RS_XKEY will appear in 
    RNST until it is put in either the user's exit control frame or USRRNST. 
    At that point the RS_XKEY flag is moved to FRS and RNST is set to zero. 
    Should the user exceed MRT in the exit control routine, RS_LIMX would 
    temporarily appear in RNST, and both RS_XKEY and RS_LIMX would be set in 
    FRS. 
    GAC - ARRAY(0:2) UBIN.  The Granule ACcounting field contains accounting 
    information for files deleted during this job or session which had been 
    created by this user. Each entry contains a floating point number which is 
    the integral of granules times time. The three entries are for the three 
    charging classes of file granules: 
       AZ$GACBACKUP    0         Granules of files 
                                 eligible for backup. 
       AZ$GACNOBACKUP  1         Granules of files 
                                 not eligible for backup. 
       AZ$GACSTOWACT   2         Granules of stowed 
                                 active files. 
    HIGHPNUM - SBIN HALF.  The HIGHPNUM field is incremented every time a run 
    unit that is the target of an M$LINK or M$LDTRC is put into execution and 
    is reset only on job step termination; thus, this is a count of the number 
    of "fetches" per job step. 
    HPSN - CHAR(6).  The Home Pack Set Name field contains the name of the 
    home pack set for this user. The principal use of this field is to 
    determine the pack set on which to create the user's account if it does 
    not already exist. 
    IDELTAT - SBIN.  The IDELTAT field contains the total quantum time 
    allocated at the last quantum end. This will normally be the quantum 
    specified by the system manager for this mode, partition, user, etc. 
    INSTWORD - ARRAY(0:3) UBIN(18).  The INSTallation WORD field is a set of 
    four values available for installation use. See M$USRFIELD. 
    INTER - SBIN HALF.  The INTERactions field contains the number of terminal 
    interactions which have occurred during this time sharing session. 
    INTTIME - SBIN.  The INTeraction compute TIME field contains the time in 
    microseconds expended until the time of the last terminal read. This is 
    used in the calculation of compute time used per interaction. This field 
    is used for time sharing only. See also STATS HISTOGRAM. 
    JOBNAME - CHAR(31).  The JOB NAME field contains the job name as specified 
    by !JOB NAME=x.  Regardless of mode, this job name will be carried with 
    any output symbiont files generated. It may be subsequently used by a user 
    in interrogating the status of output. It will also be displayed on 
    operator displays. 
    JOBUNIT - ARRAY(0:3) UBIN(18).  The JOB UNIT field is a set of four 
    counters which are maintained through an entire job and may be used for 
    'transaction charging'.  See M$CHGUNIT and RATES processor. 
    JPEAK - UBIN HALF.  The Job PEAK field contains the maximum value of 
    CURRCORE attained during the job or session. 
    JRESPEAK - UBIN HALF.  The Job RESource PEAK field contains the value 
    which must be specified on a !RESOURCE or !ORES command to assure the job 
    of successful execution. This value may differ from JPEAK due to overlay 
    path considerations. 
    JSLEV - UBIN(3).  The Job Statistics LEVel field specifies the type of 
    accounting summary which is to be displayed at the end of job or session. 
    See !OFF.  The field can contain the following values: 
       AZ_ALL#         1         Full Accounting Display 
       AZ_SUMMARY#     2         One line Accounting Summary 
       AZ_NONE#        3         No Accounting Display 
    JTMPDPPK - SBIN.  The Job TeMP Disk Pack PeaK field contains the maximum 
    amount of temporary disk storage allocated during this job or session. 
    JUNK - BIT(18).  Bits in JIT.JUNK are used by job step processing and help 
    us keep track of what we are doing: 
      JJ_MLINKIP#   Set while processing an M$LINK or M$LDTRC. 
       '000001'O    Reset when run-unit has been fetched or the 
                    LINK/LDTRC process is aborted. 
      JJ_LNKRETIP#  Set while the M$LINKing program is being restored. 
       '000002'O 
      JJ_RTNXIT#    Set while an M$LINKed to run-unit is in execution. 
       '000100'O 
      JJ_MONLINK#   Set while an M$LINK by the monitor is in progress. 
       '000020'O 
      JJ_ASYNCLINK# Set in conjunction with JJ_MONLINK if the M$LINK by 
       '000004'O    the monitor was initiated at quantum end instead of 
                    during monitor service processing. 
                    Also set in conjunction with JJ2_CP_LINK in JUNK2 if 
                    the command processor issuing the M$CPEXIT with the 
                    LINK option had been entered after the time sharing 
                    user had typed the Control-Y sequence. 
      JJ_SAVING#    Set while a program is being saved for M$SAVE or 
       '010000'O    the SAVE command via IBEX. 
      JJ_GETTING#   Set while a SAVEd image is being restored. 
       '020000'O 
      JJ_NOSAVE#    Set when an M$SCON service request has been issued 
       '040000'O    with SAVEFLG = NO specified.  When set, all requests 
                    to SAVE the program are ignored.  Once set, this 
                    bit may only be reset when the job step terminates. 
      JJ_SCON#      Set when an M$SCON service request has been issued 
       '100000'O    with XCON = YES specified.  When set, the user's 
                    exit control routine (if any) is entered prior to 
                    writing the save image.  Reset only on job step 
                    termination. 
      JJ_SCCSET#    Set when an M$EXIT, M$ERR or M$XXX service request 
       '000040'O    with the STEPCC option is specified (from any 
                    domain).  Reset when the trickle down for exit 
                    control reaches the user level, thus allowing the 
                    user to reset his STEPCC settings via his final 
                    exit from exit control processing. 
      JJ_LOGOFF#    Set on M$CPEXIT when CP_LASTCP# is set in CPFLAGS1 
       '000200'O    and the user is at job step.  Used to allow entry to 
                    a Logoff Command Processor, and to prevent multiple 
                    entries to same. 
      JJ_BYPASSD#   Set on M$DRTN when the Debugger indicates that the 
       '000400'O    user exit control routine is to be entered.  Reset 
                    when entering the user exit control routine. 
      JJ_EVENT#     Set on M$DRTN with EVENT = YES specified.  Causes 
       '400000'O    the Scheduler to defer events for this user until 
                    after the user program has been re-entered.  Reset 
                    by the scheduler. 
      JJ_UDELTA#    Set when a run-unit is started under control of a 
       '200000'O    debugger and not set when a debugger is associated 
                    via M$ALIB.  Control goes to the debugger on all 
                    user exceptional conditions (break, traps, etc.) 
                    when this bit is set. 
      JJ_BAKIC#     Set by various monitor service processing routines 
       '001000'O    to indicate that control is to be returned to the 
                    user with the IC in Safe-Store reset to the address 
                    of the outstanding service request.  Used to back 
                    out of reads when a break is received, for example. 
      JJ_RUNXCON#   Set by the exit control logic when the user exit 
       '002000'O    control processing is complete and giving exit 
                    control logic for the special shared processors 
                    is to be entered.  Causes the subcode in the exit 
                    control frame for the special shared processor to 
                    be set to one. 
      JJ_DLIB#      Set when a debugger or ASL is disassociated because 
       '004000'O    of an M$DLIB request.  Causes the exit control logic 
                    to be entered (run-up) for the processor being 
                    disassociated and indicates that the user program is 
                    to be resumed following exit from the processor's 
                    exit control routine. 
      JJ_EXONLY#    Set when an execute-only run-unit is put into 
       '000010'O    execution.  Causes association of a debugger to 
                    be disallowed. 
    JUNK2 - BIT(18).  JUNK2 is the overflow of JIT.JUNK.  Bits in this word 
    are used as follows: 
      JJ2_DBRK#     Set on M$DRTN when the DBRK = YES option is 
       '000001'O    specified.  Write access to data pages with the 
                    SCDRRK bit set in the user's page table will be 
                    disabled.  This bit will be reset and the write 
                    access allowed on those pages when the debugger is 
                    next entered. 
      JJ2_PACCESS#  Set prior to transfer of control to the debugger if 
       '000002'O    the user page table has been modified to allow the 
                    debugger to modify user procedure.  Will not be set 
                    if ALIB.  Reset on M$DRTN when write access to 
                    procedure is reset. 
      JJ2_DFRBRK#  Set by the scheduler to defer break control to the 
       '000004'O   user when the break is received during M$YC PMME 
                   processing.  This bit is reset when the command 
                   processor issues the M$CPEXIT, at which time control 
                   will be given to the user's break control routine. 
      JJ2_CP_LINK# Set if the LINK option was specified on the M$CPEXIT 
       '000010'O   request.  If the Command Processor had been entered 
                   because the time-sharing user had typed the 
                   Control-Y sequence the JJ_ASYNCLINK bit in JUNK will 
                   also be set.  If the Command Processor had been 
                   entered for M$YC processing, JJ_ASYNCLINK will be 
                   reset. 
      JJ2_ASAVE_LNK# Set in the ASAVE logic prior to calling the M$LINK 
       '000020'O   handler to write the program image and free the 
                   memory of a user whose timesharing line has failed. 
      JJ2_NOSAVE_CP# Set when an M$SCON request has been issued by a CP 
       '000040'O   with SAVEFLG = NO specified.  When set, all requests 
                   to SAVE the program are ignored.  Once set, this 
                   bit may only be reset by the CP. 
      JJ2_MEM_ERR# Set if restoring an M$LINK image causes the user's 
       '000100'O   dynamic data segment space to be over allocated. 
    LANG - CHAR(1).  The LANGuage field is a single character which specifies 
    the native language of the user. This field is used to select the correct 
    error message and help files for this user. 
    LBJID - UBIN HALF.  The Last Batch Job ID field contains the sysid of the 
    last batch job submitted by this job or session. 
    LLL - UBIN HALF.  The Library Lower Limit field contains the virtual page 
    number of the first page of procedure of an associated run-time library. 
    LNKCNT - UBIN(9).  Contains the current number of nested M$LINK service 
    requests.  This field is incremented on every M$LINK request and 
    decremented each time the linking program is restored. 
    LOCK - ARRAY(0:71) BIT(1).  The LOCK is really a "KEY".  This double word 
    contains bit settings that allow users to access restricted processors. 
    The LOCK is initialized from the :USERS record when the user enters the 
    system.  Refer to the description of the KEY option of SUPER in the System 
    Support Reference Manual and to the description of the SLOCK and WLOCK 
    options of LINK in the Programmer Reference Manual. 
    LOGONTIME - UBIN.  The LOGON TIME field contains the time, in UTS units, 
    when this job or session was initiated. 
    LUL - UBIN HALF.  The Library Upper Limit field contains the virtual page 
    number of the last page of procedure of an associated run-time library. 
    MAXCORE - UBIN HALF.  The MAXimum CORE field contains the maximum value 
    which CURRCORE will be allowed to reach. The word CORE is retained for 
    nostalgia.  See !RESOURCE, !ORES, !LIMIT. 
    MAXENQ - UBIN(18).  Defines the maximum number of ENQ/DEQ packets for this 
    user. 
    MAXEXP - SBIN HALF.  The MAXimum EXPiration field contains the maximum 
    expiration time that this user may specify. 
    MAXPRI - UBIN BYTE.  The MAXimum PRIority field contains the maximum batch 
    priority which this job or session may assign to a submitted batch job. 
    MAXTMPDP - SBIN.  The MAXimum TeMP Disk Pack field contains the maximum 
    number of granules of temporary disk space which this job or session is 
    allowed to use. 
    MMFLGS.  The Memory Management FLaGS field contains a set of flags which 
    describe the current state of this user from a memory management 
    standpoint. 
    MMFLGS.FREE_PPGS - BIT(1).  The FREE Procedure PaGeS field indicates 
    whether or not the procedure pages in the currently executing run unit are 
    to be charged to this user. A value of '1'B specifies that the pages are 
    not to be charged. 
    MODE - UBIN(4).  Specifies the type of user.  One of the following equated 
    values will be contained in this field: 
      M_BATCH#   1      Batch User 
      M_GHOST#   2      Ghost User 
      M_INT#     3      Interactive User 
      M_TP#      4      Transaction Processing User 
    MOUNTS - ARRAY(0:2) SBIN HALF.  The MOUNTS field contains the number of 
    operator mounts required for various resource devices. The entries are 
    used as follows: 
    disk=0, tape=1, other=2. 
    MRT - SBIN.  The Maximum Run Time field contains the maximum allowed 
    execution plus service time at the beginning of a job and when a !LIMIT 
    command is processed. At any other time it contains the amount of time 
    remaining within the limit. This field is maintained in csec units. 
    MSGID.  The MeSsaGe IDentification field contains the message id of the 
    last comgroup read done by this job or session. This is used primarily for 
    Transaction Processing. 
    MSGID.PRIMARY - UBIN.  The PRIMARY subfield contains the primary 
    identification of the transaction. This value is the same for all spawned 
    transactions and identifies the parent transaction. 
    MSGID.XT - UBIN.  The eXTension field provides a unique identifier for 
    spawned transactions. 
    NEXTCC - UBIN(9).  The NEXT Control Command field specifies where the next 
    command will be obtained. The possible values are: 
       CC_FROMNO#      0         There are no more 
                                 (end of batch job). 
       CC_FROMJOB#     1         Batch job not in XEQ file. 
       CC_FROMXEQ#     2         Execute file. 
       CC_FROMUC#      3         Time sharing terminal. 
    NODOEVER - BIT (1).  This bit is set during logon.  If the user's MAXDO 
    for this mode, as defined in the user's record, is 0 then this bit is a 1. 
    The effect of this bit being on is to inhibit any type of DO output. 
    NOLOEVER - BIT (1).  This bit is set during logon.  If the user's MAXLO 
    for this mode, as defined in the user's record, is 0 then this bit is a 1. 
    The effect of this bit being on is to inhibit any type of LO output. 
    NOPOEVER - BIT (1).  This bit is set during logon.  If the user's MAXPO 
    for this mode, as defined in the user's record, is 0 then this bit is a 1. 
    The effect of this bit being on is to inhibit any type of PO output. 
    NUTS - BIT(1).  The NUTS field is no longer used. 
    OLTA - ARRAY(0:1) BIT(1).  The On Line TApe field contains permission bits 
    which allow time sharing users to use 0-2 tape drives without reserving 
    them via !ORES. 
    ORIGINATOR_MODE - UBIN(4).  Specifies the mode of the originator of the 
    job stream to which this job belongs.  One of the following EQUs will be 
    contained in this field: 
      M_BATCH#   Originator was a card reader: 
                 B$JIT.ORIGINATOR_PORT.FROM_CR contains the 
                 device name and TNAME of the originator. 
      M_GHOST#   Originator was a ghost user: 
                 B$JIT.ORIGINATOR_PORT.FROM_GHOST contains the 
                 SYSID of the originator. 
      M_INT#     Originator was an interactive user: 
                 B$JIT.ORIGINATOR_PORT.FROM_INT contains the 
                 TSLINE of the originator. 
    See B$JIT.MODE, B$JIT.ORIGINATOR_PORT. 
    ORIGINATOR_PORT.  The ORIGINATOR_PORT field contains information 
    concerning the originator of the job stream to which this job belongs. 
    This field is a REDEF of the TSLINE field. 
    ORIGINATOR_PORT.FROM_CR.  The ORIGINATOR_PORT.FROM_CR field contains 
    information concerning the originator of the job stream to which this job 
    belongs, if B$JIT.ORIGINATOR_MODE is M_BATCH#. 
    ORIGINATOR_PORT.FROM_CR.DEVICE - CHAR(4).  Contains the device name of the 
    card reader of origin. 
    ORIGINATOR_PORT.FROM_CR.TNAME - CHAR(8).  Contains the TNAME of the card 
    reader of origin. 
    ORIGINATOR_PORT.FROM_GHOST.  The ORIGINATOR_PORT.FROM_GHOST field contains 
    information concerning the originator of the job stream to which this job 
    belongs, if B$JIT.ORIGINATOR_MODE is M_GHOST#.  This field is a REDEF of 
    the ORIGINATOR_PORT.FROM_CR field. 
    ORIGINATOR_PORT.FROM_GHOST.SYSID - UBIN HALF.  Contains the SYSID of the 
    originating ghost user. 
    ORIGINATOR_PORT.FROM_INT.  The ORIGINATOR_PORT.FROM_INT field contains 
    information concerning the originator of the job stream to which this job 
    belongs, if B$JIT.ORIGINATOR_MODE is M_INT#.  This field is a REDEF of the 
    ORIGINATOR_PORT.FROM_CR field. 
    ORIGINATOR_PORT.FROM_INT.SYSID.  The ORIGINATOR_PORT.FROM_INT.SYSID field 
    REDEFs a portion of the TSLINE field, and contains the SYSID of the 
    originating time-sharing user. 
    ORIGINATOR_PORT.FROM_INT.TSLINE.  The ORIGINATOR_PORT.FROM_INT.TSLINE 
    field is a REDEF of the TSLINE field. 
    OUTPRIO - UBIN(9).  The OUTput PRIOrity field contains the priority value 
    to be assigned to output symbiont files generated by this job or session. 
    PCADS - UBIN HALF.  The Page Count ASL Data Segments field contains the 
    total number of pages which an ASL has allocated on behalf of this user. 
    PCC - UBIN HALF.  The Page Count of Context field contains the number of 
    pages the monitor has allocated for this user's context.  User context 
    includes HJIT, Page Table, Tstack, JIT, the first page of the Read Only 
    Segment(ROS), and the Command Processor Dynamic Data Segment pages. 
    PCD - UBIN HALF.  The Page Count of Data field contains the number of 
    pages that have been allocated for program data in the instruction 
    segment. 
    PCDD - UBIN HALF.  The Page Count Dynamic Data field contains the number 
    of pages which have been allocated dynamically in the Instruction Segment. 
    See M$GDP, M$GVP. 
    PCDDS - UBIN HALF.  The Page Count Debugger Data Segments field contains 
    the total number of pages which a debugger has allocated on behalf of this 
    user. 
    PCDS - UBIN HALF.  The Page Count Dynamic Segments field contains the 
    number of pages that the user has allocated in dynamic data segments.  See 
    M$GDS. 
    PCL - UBIN HALF.  The Page Count of Library field contains zero if no 
    run-time library is associated, or if a shared run-time library is 
    associated.  If the run-library becomes unshared, because of an M$DLIB or 
    UNSHARELIB command to DELTA, this field will contain the number of pages 
    that have been obtained for the run-time library procedure. 
    PCP - UBIN HALF.  The Page Count of Procedure field contains the number of 
    pages that have been allocated for procedure.  If a shared processor is in 
    execution, this number will not be included in the PPC field. 
    PCROS - UBIN HALF.  The Page Count Read Only Segment is the total number 
    of pages in the Read Only Segment. This segment contains the TCB and DCBs. 
    The first page of this segment is also counted in PCC. 
    PCV - UBIN HALF.  The Page Count Virtual field contains the total number 
    of real pages allocated in the three virtual segments, as well as the page 
    tables and context necessary to support them. 
    PLL - UBIN HALF.  This field contains the Procedure Lower Limit, which is 
    the virtual page number of the first procedure page of the run unit or 
    standard shared processor currently executing. 
    PMEMTIM - SBIN.  The Processor MEMory TIMe field contains the integral of 
    (B$JIT.TPEXT + B$JIT.TPSVT) * B$JIT.CURRCORE over all quanta of the entire 
    job or session.  This is maintained in csec * page units. 
    PMME_COUNT - SBIN.  The PMME_COUNT and PMME_DATA field are used in 
    conjunction to gather data on PMMEs executed when the MoUsE (Monitor Usage 
    Evaluator) feature of STATS is in use. The PMME_COUNT field contains the 
    current nesting level of a PMME, e.g. an M$ERRMSG PMME must invoke an 
    M$OPEN PMME to open the appropriate error message file. 
    PMME_DATA - ARRAY(0:2).  The PMME_DATA field contains various information 
    about starting a PMME for this user. When the PMME completes, the 
    resultant information is recorded in the system MOUSE tables. This field 
    is indexed by PMME_COUNT. 
    PMME_DATA.CPU - UBIN.  The CPU field contains the service time used by 
    this job or session up to the start of this PMME. 
    PMME_DATA.I_O - UBIN.  The I_O field contains the sum of the three ACCESS 
    fields at the start of this PMME. 
    PMME_DATA.MISC1 - SBIN.  The MISCellaneous1 and MISC2 fields contain 
    various information about the PMME in progress, e.g. for file management 
    operations, the ASN field of the DCB. 
    PMME_DATA.MISC2 - SBIN.  See MISC1. 
    PNR - UBIN(9).  The Partition NumbeR field contains, if batch, the batch 
    partition in which this user is running. 
    PPC - UBIN HALF.  The Physical Page Count field contains the number of 
    real memory pages which are only recorded in the page table of this user. 
    The value in this field may or may not be equal to CURRCORE depending on a 
    variety of factors, such as shared procedure, shared data segments, free 
    procedure, etc. 
    PPRIV - BIT(36).  Contains bit settings indicating which privileged 
    processors may be put into execution by this user.  Refer to the 
    description of the PPRIVILEGE option of SUPER in the System Support 
    Reference Manual for a description of the various processor privileges 
    that may be set.  Each of the processor privileges have an EQU defined 
    here in the JIT that may be used to test the bit setting in JIT.PPRIV. 
    These are of the form: 
       %EQU PPR_pprivname# = value; 
    where pprivname is the same as that of the option. 
    PRDPRM - SBIN.  The PeRmanent Disk Pack ReMaining field contains the 
    number of granules of permanent space which this job or session is still 
    allowed to allocate. Note that this is not the same as file account 
    limits. 
    PRFLAGS.  The PRocessor FLAGS field contains a set of flags which are set 
    by the command processor based on the run unit invocation line and other 
    commands. 
    PRFLAGS.COMMENT - BIT(1).  The COMMENT field is a flag which is set unless 
    a !DONT COMMENT command was entered immediately prior to this job step. 
    PRFLAGS.CONTINUED - BIT(1).  The CONTINUED field is a flag which is set if 
    a run unit invocation command is continued. The continuation records may 
    be found in the file *CONTINUATION_COMMANDS. 
    PRFLAGS.EXPOUND - BIT(1).  The EXPOUND field is a flag which is set unless 
    a !DONT EXPOUND command was entered.  It is queried by XUG$GETCMD to 
    determine whether syntax error messages should be followed by "Type a ? 
    for details". 
    PRFLAGS.LIST - BIT(1).  The LIST field is a flag which is set unless a 
    !DONT LIST command was entered immediately prior to this job step. 
    PRFLAGS.LS - BIT(1).  The List Source field is a flag which is set if a 
    fid was specified in the fid4 position of the run unit invocation. 
    PRFLAGS.NOSCAN - BIT(1).  The NOSCAN field is a flag that is set when the 
    contents of CCBUF have not been scanned by the Command Processor.  When 
    this bit is set the contents of PRFLAGS.NSYSNTAX has no meaning. 
    PRFLAGS.NSSYNTAX - BIT(1).  The Non-Standard SYNTAX field is a flag that 
    is set by the command processor if a run unit invocation did not conform 
    to the standard syntax.  When a program issues an M$LINK or M$LDTRC 
    monitor service request with a CP_CMD command, the NSSYNTAX flag will be 
    set or cleared based on the command passed to the command processor.  When 
    a program issues an M$LINK or M$LDTRC request without using the CP_CMD 
    option, the NSSYNTAX bit will always be set. 
    PRFLAGS.OU - BIT(1).  The Object Unit field is a flag which is set if a 
    fid was specified in the fid3 position of the run unit invocation. 
    PRFLAGS.OUTPUT - BIT(1).  This field is not currently used. 
    PRFLAGS.POINT - BIT(1).  The POINT field is a flag which is reset until a 
    !POINT command is entered.  It is queried by XUG$GETCMD and related 
    routines to control the method used to point out errors in command lines. 
    PRFLAGS.POSITION - BIT(1).  This flag, which is normally set, can be reset 
    via the IBEX command !DONT POSITION.  If this flag is set, the XUG$GETCMD 
    package will attempt to reload the user's reread (escape-D) buffer so that 
    if the user types escape-D, the terminal's cursor will be positioned at 
    the point of the first error reported via XUG$ERRPTR. 
    PRFLAGS.SI - BIT(1).  The Source Input field is a flag which is set if a 
    fid was specified in the fid1 position of the run unit invocation. 
    PRFLAGS.UI - BIT(1).  The Update Input field is a flag which is set if a 
    fid was specified in the fid2 position of the run unit invocation. 
    PRFLAGS.WHEN - BIT(1).  This flag indicates that an IBEX WHEN command is 
    in effect for this command stream level, B$JIT.CSLEV.  This flag can be 
    reset via the IBEX command !DONT WHEN. 
    PRIINC - REDEF PNR UBIN(9).  The PRIority INCrement field contains the 
    execution priority increment to be given to this system ghost over that 
    established for ghosts as a default. 
    PRIOB - SBIN(9).  The PRIOrity Base field contains a signed offset that is 
    combined with the system default PRIOB value.  The result is the value to 
    use for this user's scheduling priority. 
    PRIOCORE - UBIN HALF.  The PRIOr CORE field contains the previous value of 
    CURRCORE when a run-unit is brought into execution via a monitor M$LINK. 
    PRIOR_CP - UBIN(9).  Contains the processor number of the previous command 
    processor.  When one command processor issues an M$CPEXIT service request 
    to associated a different command processor, the processor number of the 
    command processor making the request is put here. 
    PRIV.  There are five words that are defined in the JIT that are used to 
    verify a user's privilege prior to performing certain system functions for 
    this user.  A description of the contents of each of these words follows. 
    Within each of the words, the bit settings will correspond to a value for 
    which an EQU statement is included in B$JIT_C.  These are of the form: 
       %EQU PR_privname# = value; 
    where privname is the same as that of the sub-option available on the 
    PRIVILEGE option of SUPER.  Please refer to the System Support Reference 
    Manual for the names and meaning of these sub-options. 
    PRIV.ACTIVE - BIT(36).  Contains the privileges that are currently in 
    effect.  These active privileges are the combination of PRIV.JOB and 
    PRIV.PRC.  These privilege bits may also be set and reset by the M$SPRIV 
    and M$RPRIV monitor service request.  Refer to the Monitor Services 
    Reference Manual for a description of these requests. 
    PRIV.AUTH - BIT(36).  Contains the user's privilege indicators as defined, 
    via SUPER, in the :USERS file. 
    PRIV.JOB - BIT(36).  Contains the privileges that have been requested via 
    the !PRIV command of IBEX.  The privilege must appear in JIT.AUTH before 
    IBEX will set it in JIT.JOB. 
    PRIV.PRC - BIT(36).  Contains the processor privilege bits, as defined by 
    LINK options, from the :SYS processor's head record.  If the currently 
    executing run unit is not from :SYS, PRIV.PRC is set to zero. 
    PRIV.SAVED - BIT(36).  Contains the value from PRIV.ACTIVE while the 
    associated Command Processor is in control.  This value is then restored 
    to PRIV.ACTIVE when the command processor returns control to the user. 
    PROG_ENTRY - BIT(9).  Set to indicate how the currently executing run-unit 
    was put into execution as follows: 
       PE_CP#     '000'O    Started via M$CPEXIT; 
       PE_MLINK#  '030'O    Started via JLU$MLINK. 
       PE_LINK#   '020'O    Started via M$LINK. 
       PE_LDTRC#  '010'O    Started via M$LDTRC. 
    PSEUDOPGS - UBIN HALF.  The PSEUDO PaGeS field contains the total number 
    of pages which the user is charged for but which are not reflected in PPC. 
    PSEUDO_COUNT - UBIN BYTE.  Contains the number of pseudo resources of the 
    name specified by PSEUDO_TEXT, which were acquired for this user by Job 
    Step. 
    PSEUDO_TEXT - CHAR(8).  Contains the pseudo resource name of the resource 
    acquired for this user by Job Step.  These pseudo resources are released 
    when the currently executing program is terminated. 
    PSLEV - UBIN(3).  The Processor Statistics LEVel field specifies the type 
    of accounting summary which is to be displayed when proprietary processor 
    charging is in effect. See JSLEV for possible values.  Also see RATES, 
    CONTROL. 
    PTSIZ - UBIN HALF.  The Page Table Size field contains the total number of 
    words of Page Table that currently exist for this user.  This will usually 
    be 1023, but will expand to 2047 if required. 
    PUL - UBIN HALF.  This field contains the Procedure Upper Limit, which is 
    the virtual page number of the last procedure page of the run unit or 
    standard shared processor currently executing.  If the user is at job 
    step, JIT.PUL will be set to JIT.PLL -1. 
    QUAN - SBIN(18).  The QUANtum field contains a signed offset, in 
    microseconds, that is combined with the system default QUAN value.  The 
    result is the number of microseconds to give this user each quantum. 
    REMCPO - SBIN.  This field contains the number of punched cards allowed 
    remaining for this job. 
    REMDO - SBIN.  This field contains the number of pages of DO output 
    remaining for this job. 
    REMLO - SBIN.  This field contains the number of pages of LO output 
    remaining for this job. 
    RERUN - BIT(1).  The RERUN field specifies, if set, that this batch job is 
    being rerun as a result of some precipitate termination on a previous run. 
    RESCORE - UBIN WORD.  The RESource CORE field contains the current amount 
    of resource memory allocated (not necessarily physically allocated). The 
    MAXCORE field is always less than or equal to RESCORE.  See !RESOURCE, 
    !ORES. 
    RESPEAK - REDEF JRESPEAK UBIN HALF.  See JRESPEAK. 
    RNST - BIT(9).  This field contains one of the following equated values: 
       RS_EXIT#   '000'O   M$EXIT was issued. 
       RS_ERR#    '001'O   M$ERR was issued. 
       RS_XXX#    '002'O   M$XXX was issued. 
       RS_SSP#    '004'O   Aborted by Special Shared Processor. 
       RS_ABRT#   '010'O   Job step aborted by the monitor.  This 
                           may be because of program trap and no 
                           trap control or an errored monitor service 
                           request and no ALTRET. 
       RS_EKEY#   '020'O   Aborted because of operator !E keyin 
                           or because on user Control-Y QUIT. 
       RS_CAN#    '021'O   Batch job has been canceled. 
       RS_OFF#    '040'O   Logoff by the command processor. 
       RS_LIMX#   '100'O   Abort because some limit has been exceeded. 
                           See description of XLIMFLG. 
       RS_DROP#   '200'O   Interactive user's line has disconnected. 
       RS_XKEY#   '400'O   Abort because of !X keyin by the operator. 
    Note that this field may have more than one bit set on to indicate 
    multiple exit conditions. 
    The RNST field in the JIT always contains the "current" run status 
    reported on this user.  This field will be moved to the exit control frame 
    on the Task Control Block of the domain (user, alternate shared library, 
    debugger or command processor) in control at the time of the exit 
    condition.  If this is the status to be reported to the user following all 
    levels of exit control processing, this field will be moved to 
    JIT.USRRNST.  JIT.RNST is subject to change on any change of domain and 
    should therefore never be referenced by the user program. 
    RUNFLAGS - BIT(9).  Indicates the currently executing process as follows: 
      RUN_MON#    '001'O   Monitor or Command Processor 
      RUN_PROC#   '002'O   Processor in :SYS linked with PROCACC 
      RUN_USER#   '004'O   User program or processor not linked 
                           with the PROCACC option 
    SAVEDCB$ - PTR.  This saves the value of B$JIT.DCB$ when linking to 
    ALTKEY_MON from within the monitor. 
    SCHTIME - SBIN.  The SCHedule TIME field contains the sum of XTIME, STIME, 
    and CTIME as they existed the last time this user was scheduled for 
    execution. 
    SINPUTSZ - UBIN BYTE.  This field contains (at least for time-sharing 
    users) the most recently specified value for the VLP_TRMCTL.SINPUTSZ 
    option. 
    SPEAK - UBIN HALF.  The Step PEAK field contains the maximum value of 
    CURRCORE attained during the current job step. 
    SRESPEAK - UBIN HALF.  The Step RESource PEAK field is the same as 
    JRESPEAK for a job step. 
    SSLEV - UBIN(3).  The Step Statistics LEVel field specifies the type of 
    accounting summary which is to be displayed at each job step. See JSLEV 
    for possible values. Also see !REPORT. 
    STAR - ARRAY(0:7).  The STAR field contains information about several 
    commonly used star files. The entries are in the order: 
    *T,*G,*L,*A,*S,*N,*X,*I. 
    STAR.DA - UBIN.  The Disk Address field contains the disk address of the 
    file information field for each of the abovementioned star files. 
    STDLOPGS - SBIN WORD.  The STanDard LO PaGeS field contains the number of 
    printed pages of output which have been generated using the form STDLP. 
    STEPCC - UBIN(9).  Contains the Step Condition Code.  This field is set 
    from the SEV field of the error code at the time of the exit condition 
    from the user program: 
       CC_EXIT#   0    M$EXIT 
       CC_ERR#    4    Job step has been errored. 
       CC_XXX#    6    Job step has been aborted. 
    STEPS - SBIN HALF.  Contains the number of job steps that have been 
    executed since this user logged on. 
    STEPUNIT - ARRAY(0:3) UBIN(18).  The STEP UNIT field is a set of four 
    counters which are maintained through a job step and reset to zero at the 
    beginning of each job step. These may be used for 'transaction charging'. 
    See M$CHGUNIT and RATES processor. 
    STIME - SBIN.  The Service TIME field contains the number of microseconds 
    of service time used this quantum. 
    STMPDPPK - SBIN.  The Step TeMP Disk Pack PeaK field contains the maximum 
    amount of temporary disk storage allocated during this job step. 
    SVLDTF - BIT(9).  The SVLDT field contains bit settings to keep track of 
    various functions (exit control processing and association of DELTA) in 
    the course of M$LINK, M$LDTRC, SAVE and GET processing: 
       SVL_DIC#    '200'O   DELTA was in control at the time of the SAVE. 
       SVL_EXIT#   '100'O   M$EXIT from exit control for SAVE - Saved 
                            program is now to be run down. 
       SVL_TRTN#   '040'O   M$TRTN from exit control for SAVE - Saved 
                            program is to continue execution. 
       SVL_LINK#   '020'O   M$LINK in progress. 
       SVL_LDTRC#  '010'O   M$LDTRC in progress. 
       SVL_MSAVE#  '004'O   M$SAVE in progress. 
       SVL_YCSAVE# '002'O   Control-Y SAVE in progress. 
       SVL_GET#    '001'O   GET in progress. 
    SVTUS - UBIN.  The SerVice Time microseconds field contains the number of 
    microseconds (0-9999) of service time which were not able to be reflected 
    in TPSVT or TUSVT at the end of the previous quantum. 
    SWITCH - ARRAY(0:35) BIT(1).  The SWITCH field contains a set of 36 pseudo 
    sense switches which may be set/reset by !SWITCH and set/reset by 
    M$SSWITCH/M$RSWITCH. 
    SYSID - UBIN HALF.  Specifies the unique System Identification number that 
    has been assigned to this user by the system.  This number is reset only 
    on a cold boot or wrap around.  All operator communication and external or 
    printed form of user identification will use SYSID. 
    TDP - UBIN HALF.  The Top Dynamic Page field contains the virtual page 
    number of the highest dynamic page currently allocated. 
    TMPGAC.  The TeMPorary Granule ACcounting field contains accounting 
    information for temporary files used in this job or session. 
    TMPGAC.N - UBIN.  The TMPGAC.N field contains the integral of temporary 
    granules times time up to the time recorded in TMPGAC.TIME in floating 
    point. This is updated each time a temporary granule is allocated or 
    deallocated. 
    TMPGAC.TIME - UBIN.  The TMPGAC.TIME field contains the time in UTS units 
    of the last update of TMPGAC.N. 
    TPEXT - SBIN.  The Total Processor EXecution Time field contains the 
    processor execution time used in this job or session prior to the current 
    quantum. This is maintained in csec units. 
    TPSVT - SBIN.  The Total Processor SerVice Time field contains the 
    processor service time used in this job or session prior to the current 
    quantum. This is maintained in csec units. 
    TSLINE.  The Time Sharing LINE field contains several attributes of a time 
    sharing users terminal connection. 
    TSLINE.FEX - UBIN(9).  The Front End indeX field contains the FEP number 
    of the FEP to which this user's terminal is connected. 
    TSLINE.LEV - UBIN (9).  The LEV defines what level of the line is valid. 
    Values: 
     1 - Only the PORT is valid. 
     2 - The PORT-SUBDEVICE is valid. 
     3 - The PORT-SUBDEVICE-SUBSUBDEVICE is valid. 
    TSLINE.PORT - UBIN(18).  The PORT field identifies the port or MLCP 
    address on the FEP to which this user's terminal is connected. 
    TSLINE.SPEED - UBIN(9).  The SPEED field contains a number signifying the 
    line speed of this user's terminal. The current values are: 
     SPEED   baud      SPEED     baud      SPEED     baud 
      0        50       1          75       2         110 
      3       134       4         150       5         200 
      6       300       7         600       8        1050 
      9      1200      10        1800      11        2000 
     12      2400      13        4800      14        9600 
     15     19200 
     Values 0, 1, 3, 8, 10, 11 are not currently supported. 
    TSLINE.SUBDEVICE - UBIN(18).  The SUBDEVICE field identifies the subdevice 
    for a given channel to which this user's terminal is connected. 
    TSLINE.SUBSUBDEVICE - UBIN(18).  The SUBSUBDEVICE field identifies the 
    subsubdevice for a given channel to which this user's terminal is 
    connected. 
    TSLINE.TTYP - UBIN(9).  The TTYP field defines what type of device the 
    connection is to. 
    TUEXT - SBIN.  The Total User EXecution Time field contains the user 
    execution time used in this job or session prior to the current quantum. 
    This is maintained in csec units. 
    TUSVT - SBIN.  The Total User SerVice Time field contains the user service 
    time used in this job or session prior to the current quantum. This is 
    maintained in csec units. 
    UMEMTIM - SBIN.  The User MEMory TIMe field contains the integral of 
    (B$JIT.TUEXT + B$JIT.TUSVT) * B$JIT.CURRCORE over all quanta of the entire 
    job or session.  This is maintained in csec * page units. 
    UNAME - CHAR(12).  The User NAME field contains the user's log on name. 
    USER - UBIN(9).  Specifies the User Number that has been assigned to this 
    user by the system.  This number is used internally as an index into the 
    system user tables (B$USER) and is not used for any external user 
    identification. 
    USERWORD - ARRAY(0:3) UBIN(18).  The USER WORD field is a set of four 
    values available for user use.  See M$USRFIELD. 
    USRDCB - UBIN(9).  Contains the value from DCBNO at the time of the exit 
    condition from the user program.  Thus, if there is a DCB# associated with 
    the error code in JIT.USRERR it will be here. 
    USRERR.  Contains the error code that reflects the exit condition of the 
    user program.  JIT.USRERR is in VLP_ERRCODE format; refer to ERR for an 
    explanation of the FCG, MID, MON, CODE and SEV subfields.  USRERR only 
    reflects the exit condition of the user domain. 
    USRIC - UBIN(18).  Contains the Instruction Counter at he time of the exit 
    condition from the user program. 
    USRRNST - BIT(9).  Contains the run status to reflect the exit condition 
    of the user program.  Refer to RNST for an explanation of the bit settings 
    in this field.  Note that USRRNST only applies to the exit condition of 
    the user domain.  For example, if the job step is terminated because a 
    special shared processor aborts, RS_ABRT# would have been set JIT.RNST for 
    that special shared processor's error processing, but JIT.USRRNST would 
    have RS_ABORT# reset and RS_SSP# would be set instead. 
    UTIMER - UBIN.  The User TIMER field contains the time, in microseconds, 
    remaining before expiration of the timer which the user established with 
    M$STIMER. A value of zero means there is no timer currently established. 
    VIRTUAL.  The VIRTUAL field is a structure defining currently open virtual 
    data segment files. 
    VIRTUAL.DCB# - ARRAY(0:2) UBIN(9).  The DCB# field contains the DCB number 
    of the DCB open to the file which defines each of the virtual data 
    segments. 
    WOO - CHAR(8).  The Workstation Of Origin field contains the name of the 
    workstation from which this batch job originated. If the WSN option is 
    specified on a !JOB record, that becomes the WOO for the job. Timesharing, 
    ghost, and Transaction Processing jobs get their default WOO from the 
    authorization file.  Regardless of the source of WOO, it is used as the 
    default workstation for all unit record output if WSN is not specified. It 
    can also be used for banners. 
    XCONF - BIT(9).  Bits 6 through 8 of the XCONF field are used by the 
    monitor to keep track of the exit control activity as control passes from 
    one domain to another: 
       XC_URND     '004'O    Set when user level exit control processing 
                             is completed, or if the user has no request 
                             for exit control. 
       XC_ASL#     '002'O    Set when ASL exit control processing 
                             is complete. 
       XC_QUIT     '001'O    Set on a QUIT command to DELTA or IBEX. 
    Bits 0 through 7 are used to record the prior RNST for multiple entries to 
    exit control within any domain.  Refer to RNST for the EQUated values and 
    meanings of these bits. 
    XLIMFLG - BIT(9).  When RS_LIMX# is set in RNST, one of the following bits 
    will be set in XLIMFLG to indicate what limit has been exceeded: 
       XL_PO#     '400'O    Cards Punched 
       XL_MEM#    '200'O    Memory -only causes abort if restoring a 
                                    an M$LINK or SAVE program image. 
       XL_LO#     '100'O    M$LO pages 
       XL_DO#     '040'O    M$DO pages 
       XL_STACK#  '002'O    Safe-store Stack or Argument Stack 
       XL_TIME#   '001'O    Maximum Run Time exceeded 
    XTIME - SBIN.  The eXecution TIME field contains the number of 
    microseconds of execution time used this quantum. 
    YC0SZ - UBIN(18).  Contains the bound of the M$YC monitor service request 
    CMD parameter.  This field has meaning only when the CP_YCPMME# bit is set 
    in CPFLAGS1. 
    YC2SZ - UBIN(18).  Contains the bound of the M$YC monitor service request 
    REPLY parameter.  This field has meaning only when the CP_YCPMME# bit is 
    set in CPFLAGS1. 
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
00159
00160
00161
00162
00163
00164
00165
00166
00167
00168
00169
00170
00171
00172
00173
00174
00175
00176
00177
00178
00179
00180
00181
00182
00183
00184
00185
00186
00187
00188
00189
00190
00191
00192
00193
00194
00195
00196
00197
00198
00199
00200
00201
00202
00203
00204
00205
00206
00207
00208
00209
00210
00211
00212
00213
00214
00215
00216
00217
00218
00219
00220
A 
  ACCEPT_FLAGS -   
    B$JIT - 
      HELP B$JIT ACCEPT_FLAGS 
  ACCEPT_FLAGS.ANNOUNCE -   
    B$JIT - 
      HELP B$JIT ACCEPT_FLAGS.ANNOUNCE 
  ACCEPT_FLAGS.BROADCAST -   
    B$JIT - 
      HELP B$JIT ACCEPT_FLAGS.BROADCAST 
  ACCEPT_FLAGS.SEND -   
    B$JIT - 
      HELP B$JIT ACCEPT_FLAGS.SEND 
  ACCESS -   
    B$JIT - 
      HELP B$JIT ACCESS 
  ACCESS.FORMS -   
    B$JIT - 
      HELP B$JIT ACCESS.FORMS 
  ACCESS.PACKS -   
    B$JIT - 
      HELP B$JIT ACCESS.PACKS 
  ACCESS.TAPES -   
    B$JIT - 
      HELP B$JIT ACCESS.TAPES 
  ACCN -   
    B$JIT - 
      HELP B$JIT ACCN 
  APATTR -   
    B$JIT - 
      HELP B$JIT APATTR 
  ARECX -   
    B$JIT - 
      HELP B$JIT ARECX 
B 
  B$JIT Description - 
      HELP B$JIT 
  B$JIT0_ES_MODES -   
    B$JIT - 
      HELP B$JIT B$JIT0_ES_MODES 
  BILL -   
    B$JIT - 
      HELP B$JIT BILL 
  BLINDACCTNG -   
    B$JIT - 
      HELP B$JIT BLINDACCTNG 
  BUDLIM -   
    B$JIT - 
      HELP B$JIT BUDLIM 
C 
  CALCNT -   
    B$JIT - 
      HELP B$JIT CALCNT 
  CCARS -   
    B$JIT - 
      HELP B$JIT CCARS 
  CCBUF -   
    B$JIT - 
      HELP B$JIT CCBUF 
  CCDISP -   
    B$JIT - 
      HELP B$JIT CCDISP 
  CHECK_CFU -   
    B$JIT - 
      HELP B$JIT CHECK_CFU 
  CLRES -   
    B$JIT - 
      HELP B$JIT CLRES 
  CPFLAGS1 -   
    B$JIT - 
      HELP B$JIT CPFLAGS1 
  CSLEV -   
    B$JIT - 
      HELP B$JIT CSLEV 
  CTIME -   
    B$JIT - 
      HELP B$JIT CTIME 
  CURPNUM -   
    B$JIT - 
      HELP B$JIT CURPNUM 
  CURRCORE -   
    B$JIT - 
      HELP B$JIT CURRCORE 
  CURSUDO -   
    B$JIT - 
      HELP B$JIT CURSUDO 
  CURTMPDP -   
    B$JIT - 
      HELP B$JIT CURTMPDP 
D 
  DCB$ -   
    B$JIT - 
      HELP B$JIT DCB$ 
  DCBNO -   
    B$JIT - 
      HELP B$JIT DCBNO 
  DDLL -   
    B$JIT - 
      HELP B$JIT DDLL 
  DDUL -   
    B$JIT - 
      HELP B$JIT DDUL 
  DEFEXP -   
    B$JIT - 
      HELP B$JIT DEFEXP 
  DEFPRI -   
    B$JIT - 
      HELP B$JIT DEFPRI 
  DLL -   
    B$JIT - 
      HELP B$JIT DLL 
  DO$ -   
    B$JIT - 
      HELP B$JIT DO$ 
  DUL -   
    B$JIT - 
      HELP B$JIT DUL 
E 
  ENQS -   
    B$JIT - 
      HELP B$JIT ENQS 
  ERR -   
    B$JIT - 
      HELP B$JIT ERR 
  ERR.CODE -   
    B$JIT - 
      HELP B$JIT ERR.CODE 
  ERR.FCG -   
    B$JIT - 
      HELP B$JIT ERR.FCG 
  ERR.MID -   
    B$JIT - 
      HELP B$JIT ERR.MID 
  ERR.MON -   
    B$JIT - 
      HELP B$JIT ERR.MON 
  ERR.SEV -   
    B$JIT - 
      HELP B$JIT ERR.SEV 
  EUP -   
    B$JIT - 
      HELP B$JIT EUP 
  EXTUS -   
    B$JIT - 
      HELP B$JIT EXTUS 
F 
  FACCN -   
    B$JIT - 
      HELP B$JIT FACCN 
  FACNACS -   
    B$JIT - 
      HELP B$JIT FACNACS 
  FACNCM -   
    B$JIT - 
      HELP B$JIT FACNCM 
  FBUC -   
    B$JIT - 
      HELP B$JIT FBUC 
  FBUL -   
    B$JIT - 
      HELP B$JIT FBUL 
  FEXT -   
    B$JIT - 
      HELP B$JIT FEXT 
  FPSN -   
    B$JIT - 
      HELP B$JIT FPSN 
  FRS -   
    B$JIT - 
      HELP B$JIT FRS 
G 
  GAC -   
    B$JIT - 
      HELP B$JIT GAC 
H 
  HIGHPNUM -   
    B$JIT - 
      HELP B$JIT HIGHPNUM 
  HPSN -   
    B$JIT - 
      HELP B$JIT HPSN 
I 
  IDELTAT -   
    B$JIT - 
      HELP B$JIT IDELTAT 
  INSTWORD -   
    B$JIT - 
      HELP B$JIT INSTWORD 
  INTER -   
    B$JIT - 
      HELP B$JIT INTER 
  INTTIME -   
    B$JIT - 
      HELP B$JIT INTTIME 
J 
  JOBNAME -   
    B$JIT - 
      HELP B$JIT JOBNAME 
  JOBUNIT -   
    B$JIT - 
      HELP B$JIT JOBUNIT 
  JPEAK -   
    B$JIT - 
      HELP B$JIT JPEAK 
  JRESPEAK -   
    B$JIT - 
      HELP B$JIT JRESPEAK 
  JSLEV -   
    B$JIT - 
      HELP B$JIT JSLEV 
  JTMPDPPK -   
    B$JIT - 
      HELP B$JIT JTMPDPPK 
  JUNK -   
    B$JIT - 
      HELP B$JIT JUNK 
  JUNK2 -   
    B$JIT - 
      HELP B$JIT JUNK2 
L 
  LANG -   
    B$JIT - 
      HELP B$JIT LANG 
  LBJID -   
    B$JIT - 
      HELP B$JIT LBJID 
  LLL -   
    B$JIT - 
      HELP B$JIT LLL 
  LNKCNT -   
    B$JIT - 
      HELP B$JIT LNKCNT 
  LOCK -   
    B$JIT - 
      HELP B$JIT LOCK 
  LOGONTIME -   
    B$JIT - 
      HELP B$JIT LOGONTIME 
  LUL -   
    B$JIT - 
      HELP B$JIT LUL 
M 
  MAXCORE -   
    B$JIT - 
      HELP B$JIT MAXCORE 
  MAXENQ -   
    B$JIT - 
      HELP B$JIT MAXENQ 
  MAXEXP -   
    B$JIT - 
      HELP B$JIT MAXEXP 
  MAXPRI -   
    B$JIT - 
      HELP B$JIT MAXPRI 
  MAXTMPDP -   
    B$JIT - 
      HELP B$JIT MAXTMPDP 
  MMFLGS -   
    B$JIT - 
      HELP B$JIT MMFLGS 
  MMFLGS.FREE_PPGS -   
    B$JIT - 
      HELP B$JIT MMFLGS.FREE_PPGS 
  MODE -   
    B$JIT - 
      HELP B$JIT MODE 
  MOUNTS -   
    B$JIT - 
      HELP B$JIT MOUNTS 
  MRT -   
    B$JIT - 
      HELP B$JIT MRT 
  MSGID -   
    B$JIT - 
      HELP B$JIT MSGID 
  MSGID.PRIMARY -   
    B$JIT - 
      HELP B$JIT MSGID.PRIMARY 
  MSGID.XT -   
    B$JIT - 
      HELP B$JIT MSGID.XT 
N 
  NEXTCC -   
    B$JIT - 
      HELP B$JIT NEXTCC 
  NODOEVER -   
    B$JIT - 
      HELP B$JIT NODOEVER 
  NOLOEVER -   
    B$JIT - 
      HELP B$JIT NOLOEVER 
  NOPOEVER -   
    B$JIT - 
      HELP B$JIT NOPOEVER 
O 
  OLTA -   
    B$JIT - 
      HELP B$JIT OLTA 
  ORIGINATOR_MODE -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_MODE 
  ORIGINATOR_PORT -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_PORT 
  ORIGINATOR_PORT.FROM_CR -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_PORT.FROM_CR 
  ORIGINATOR_PORT.FROM_CR.DEVIC -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_PORT.FROM_CR.DEVIC 
  ORIGINATOR_PORT.FROM_CR.TNAME -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_PORT.FROM_CR.TNAME 
  ORIGINATOR_PORT.FROM_GHOST -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_PORT.FROM_GHOST 
  ORIGINATOR_PORT.FROM_GHOST.SY -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_PORT.FROM_GHOST.SY 
  ORIGINATOR_PORT.FROM_INT -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_PORT.FROM_INT 
  ORIGINATOR_PORT.FROM_INT.SYSI -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_PORT.FROM_INT.SYSI 
  ORIGINATOR_PORT.FROM_INT.TSLI -   
    B$JIT - 
      HELP B$JIT ORIGINATOR_PORT.FROM_INT.TSLI 
  OUTPRIO -   
    B$JIT - 
      HELP B$JIT OUTPRIO 
P 
  PCADS -   
    B$JIT - 
      HELP B$JIT PCADS 
  PCC -   
    B$JIT - 
      HELP B$JIT PCC 
  PCD -   
    B$JIT - 
      HELP B$JIT PCD 
  PCDD -   
    B$JIT - 
      HELP B$JIT PCDD 
  PCDDS -   
    B$JIT - 
      HELP B$JIT PCDDS 
  PCDS -   
    B$JIT - 
      HELP B$JIT PCDS 
  PCL -   
    B$JIT - 
      HELP B$JIT PCL 
  PCP -   
    B$JIT - 
      HELP B$JIT PCP 
  PCROS -   
    B$JIT - 
      HELP B$JIT PCROS 
  PCV -   
    B$JIT - 
      HELP B$JIT PCV 
  PLL -   
    B$JIT - 
      HELP B$JIT PLL 
  PMEMTIM -   
    B$JIT - 
      HELP B$JIT PMEMTIM 
  PMME_COUNT -   
    B$JIT - 
      HELP B$JIT PMME_COUNT 
  PMME_DATA -   
    B$JIT - 
      HELP B$JIT PMME_DATA 
  PMME_DATA.CPU -   
    B$JIT - 
      HELP B$JIT PMME_DATA.CPU 
  PMME_DATA.I_O -   
    B$JIT - 
      HELP B$JIT PMME_DATA.I_O 
  PMME_DATA.MISC1 -   
    B$JIT - 
      HELP B$JIT PMME_DATA.MISC1 
  PMME_DATA.MISC2 -   
    B$JIT - 
      HELP B$JIT PMME_DATA.MISC2 
  PNR -   
    B$JIT - 
      HELP B$JIT PNR 
  PPC -   
    B$JIT - 
      HELP B$JIT PPC 
  PPRIV -   
    B$JIT - 
      HELP B$JIT PPRIV 
  PRDPRM -   
    B$JIT - 
      HELP B$JIT PRDPRM 
  PRFLAGS -   
    B$JIT - 
      HELP B$JIT PRFLAGS 
  PRFLAGS.COMMENT -   
    B$JIT - 
      HELP B$JIT PRFLAGS.COMMENT 
  PRFLAGS.CONTINUED -   
    B$JIT - 
      HELP B$JIT PRFLAGS.CONTINUED 
  PRFLAGS.EXPOUND -   
    B$JIT - 
      HELP B$JIT PRFLAGS.EXPOUND 
  PRFLAGS.LIST -   
    B$JIT - 
      HELP B$JIT PRFLAGS.LIST 
  PRFLAGS.LS -   
    B$JIT - 
      HELP B$JIT PRFLAGS.LS 
  PRFLAGS.NOSCAN -   
    B$JIT - 
      HELP B$JIT PRFLAGS.NOSCAN 
  PRFLAGS.NSSYNTAX -   
    B$JIT - 
      HELP B$JIT PRFLAGS.NSSYNTAX 
  PRFLAGS.OU -   
    B$JIT - 
      HELP B$JIT PRFLAGS.OU 
  PRFLAGS.OUTPUT -   
    B$JIT - 
      HELP B$JIT PRFLAGS.OUTPUT 
  PRFLAGS.POINT -   
    B$JIT - 
      HELP B$JIT PRFLAGS.POINT 
  PRFLAGS.POSITION -   
    B$JIT - 
      HELP B$JIT PRFLAGS.POSITION 
  PRFLAGS.SI -   
    B$JIT - 
      HELP B$JIT PRFLAGS.SI 
  PRFLAGS.UI -   
    B$JIT - 
      HELP B$JIT PRFLAGS.UI 
  PRFLAGS.WHEN -   
    B$JIT - 
      HELP B$JIT PRFLAGS.WHEN 
  PRIINC -   
    B$JIT - 
      HELP B$JIT PRIINC 
  PRIOB -   
    B$JIT - 
      HELP B$JIT PRIOB 
  PRIOCORE -   
    B$JIT - 
      HELP B$JIT PRIOCORE 
  PRIOR_CP -   
    B$JIT - 
      HELP B$JIT PRIOR_CP 
  PRIV -   
    B$JIT - 
      HELP B$JIT PRIV 
  PRIV.ACTIVE -   
    B$JIT - 
      HELP B$JIT PRIV.ACTIVE 
  PRIV.AUTH -   
    B$JIT - 
      HELP B$JIT PRIV.AUTH 
  PRIV.JOB -   
    B$JIT - 
      HELP B$JIT PRIV.JOB 
  PRIV.PRC -   
    B$JIT - 
      HELP B$JIT PRIV.PRC 
  PRIV.SAVED -   
    B$JIT - 
      HELP B$JIT PRIV.SAVED 
  PROG_ENTRY -   
    B$JIT - 
      HELP B$JIT PROG_ENTRY 
  PSEUDOPGS -   
    B$JIT - 
      HELP B$JIT PSEUDOPGS 
  PSEUDO_COUNT -   
    B$JIT - 
      HELP B$JIT PSEUDO_COUNT 
  PSEUDO_TEXT -   
    B$JIT - 
      HELP B$JIT PSEUDO_TEXT 
  PSLEV -   
    B$JIT - 
      HELP B$JIT PSLEV 
  PTSIZ -   
    B$JIT - 
      HELP B$JIT PTSIZ 
  PUL -   
    B$JIT - 
      HELP B$JIT PUL 
Q 
  QUAN -   
    B$JIT - 
      HELP B$JIT QUAN 
R 
  REMCPO -   
    B$JIT - 
      HELP B$JIT REMCPO 
  REMDO -   
    B$JIT - 
      HELP B$JIT REMDO 
  REMLO -   
    B$JIT - 
      HELP B$JIT REMLO 
  RERUN -   
    B$JIT - 
      HELP B$JIT RERUN 
  RESCORE -   
    B$JIT - 
      HELP B$JIT RESCORE 
  RESPEAK -   
    B$JIT - 
      HELP B$JIT RESPEAK 
  RNST -   
    B$JIT - 
      HELP B$JIT RNST 
  RUNFLAGS -   
    B$JIT - 
      HELP B$JIT RUNFLAGS 
S 
  SAVEDCB$ -   
    B$JIT - 
      HELP B$JIT SAVEDCB$ 
  SCHTIME -   
    B$JIT - 
      HELP B$JIT SCHTIME 
  SINPUTSZ -   
    B$JIT - 
      HELP B$JIT SINPUTSZ 
  SPEAK -   
    B$JIT - 
      HELP B$JIT SPEAK 
  SRESPEAK -   
    B$JIT - 
      HELP B$JIT SRESPEAK 
  SSLEV -   
    B$JIT - 
      HELP B$JIT SSLEV 
  STAR -   
    B$JIT - 
      HELP B$JIT STAR 
  STAR.DA -   
    B$JIT - 
      HELP B$JIT STAR.DA 
  STDLOPGS -   
    B$JIT - 
      HELP B$JIT STDLOPGS 
  STEPCC -   
    B$JIT - 
      HELP B$JIT STEPCC 
  STEPS -   
    B$JIT - 
      HELP B$JIT STEPS 
  STEPUNIT -   
    B$JIT - 
      HELP B$JIT STEPUNIT 
  STIME -   
    B$JIT - 
      HELP B$JIT STIME 
  STMPDPPK -   
    B$JIT - 
      HELP B$JIT STMPDPPK 
  SVLDTF -   
    B$JIT - 
      HELP B$JIT SVLDTF 
  SVTUS -   
    B$JIT - 
      HELP B$JIT SVTUS 
  SWITCH -   
    B$JIT - 
      HELP B$JIT SWITCH 
  SYSID -   
    B$JIT - 
      HELP B$JIT SYSID 
T 
  TDP -   
    B$JIT - 
      HELP B$JIT TDP 
  TMPGAC -   
    B$JIT - 
      HELP B$JIT TMPGAC 
  TMPGAC.N -   
    B$JIT - 
      HELP B$JIT TMPGAC.N 
  TMPGAC.TIME -   
    B$JIT - 
      HELP B$JIT TMPGAC.TIME 
  TPEXT -   
    B$JIT - 
      HELP B$JIT TPEXT 
  TPSVT -   
    B$JIT - 
      HELP B$JIT TPSVT 
  TSLINE -   
    B$JIT - 
      HELP B$JIT TSLINE 
  TSLINE.FEX -   
    B$JIT - 
      HELP B$JIT TSLINE.FEX 
  TSLINE.LEV -   
    B$JIT - 
      HELP B$JIT TSLINE.LEV 
  TSLINE.PORT -   
    B$JIT - 
      HELP B$JIT TSLINE.PORT 
  TSLINE.SPEED -   
    B$JIT - 
      HELP B$JIT TSLINE.SPEED 
  TSLINE.SUBDEVICE -   
    B$JIT - 
      HELP B$JIT TSLINE.SUBDEVICE 
  TSLINE.SUBSUBDEVICE -   
    B$JIT - 
      HELP B$JIT TSLINE.SUBSUBDEVICE 
  TSLINE.TTYP -   
    B$JIT - 
      HELP B$JIT TSLINE.TTYP 
  TUEXT -   
    B$JIT - 
      HELP B$JIT TUEXT 
  TUSVT -   
    B$JIT - 
      HELP B$JIT TUSVT 
U 
  UMEMTIM -   
    B$JIT - 
      HELP B$JIT UMEMTIM 
  UNAME -   
    B$JIT - 
      HELP B$JIT UNAME 
  USER -   
    B$JIT - 
      HELP B$JIT USER 
  USERWORD -   
    B$JIT - 
      HELP B$JIT USERWORD 
  USRDCB -   
    B$JIT - 
      HELP B$JIT USRDCB 
  USRERR -   
    B$JIT - 
      HELP B$JIT USRERR 
  USRIC -   
    B$JIT - 
      HELP B$JIT USRIC 
  USRRNST -   
    B$JIT - 
      HELP B$JIT USRRNST 
  UTIMER -   
    B$JIT - 
      HELP B$JIT UTIMER 
V 
  VIRTUAL -   
    B$JIT - 
      HELP B$JIT VIRTUAL 
  VIRTUAL.DCB# -   
    B$JIT - 
      HELP B$JIT VIRTUAL.DCB# 
W 
  WOO -   
    B$JIT - 
      HELP B$JIT WOO 
X 
  XCONF -   
    B$JIT - 
      HELP B$JIT XCONF 
  XLIMFLG -   
    B$JIT - 
      HELP B$JIT XLIMFLG 
  XTIME -   
    B$JIT - 
      HELP B$JIT XTIME 
Y 
  YC0SZ -   
    B$JIT - 
      HELP B$JIT YC0SZ 
  YC2SZ -   
    B$JIT - 
      HELP B$JIT YC2SZ 
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
