The KEYIN ghost provides operator control of devices (such as disk, tape, and 
unit record equipment), batch and on-line users, front-end processors, and 
central processing units (CPU).  Although a wide range of keyins are 
available, their use is restricted by the attributes of the console that the 
keyins are issued from.  In addition, the information that can be displayed at 
a console is limited by the console's attributes. 
To obtain a list of available operator keyins, enter: 
    HELP OPERATOR_KEYINS 
To obtain a list of operator keyin groups, enter: 
    HELP GROUPS 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
KEYIN_1_QUESTIONMARK
KEYIN_2_QUESTIONMARKS
Syntax: 
@mastername textstring 
Description: 
Sends the specified text-string to the corresponding master terminal when the 
CP-6 system is acting as a slave IRBT to another computer system. 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
Syntax: 
ABOR[T] devicename [[ IF ] sysid] 
Description: 
Aborts the current output on the specified symbiont device.  If the optional 
sysid is specified, the ABORT occurs only if the specified sysid is currently 
outputting. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
ACCT[LG] filename 
Description: 
Causes the :ACCTLG.:SYS file to be renamed to the specified filename in the 
:SYS account so that it can be accessed by billing and statistical programs. 
The filename must be less than 32 characters long.  The resultant file has the 
same access controls as :ACCTLG.:SYS. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
ALIG[N] devicename 
Description: 
The ALIGN keyin initiates an alignment sequence for the specified symbiont 
device, and may be issued when the device is busy or idle. 
For a busy device, the alignment sequence begins by automatically suspending 
the device.  Then the VFU image, chain image, and alignment image are sent to 
the device.  If the form on the device contains no alignment image, the file 
automatically resumes printing at completion of the alignment sequence.  If 
the form contains an alignment image, the operator uses the CONTINUE keyin 
after aligning the paper to cause the file to resume output.  For LP devices, 
the resumption point is the top of the form immediately preceding the point of 
interruption.  For CP devices, it is the card immediately preceding the point 
of interruption.  For all other device types, output resumes at the point of 
interruption. 
For an idle device, when the ALIGN keyin is issued the device is locked, and 
the alignment information follows.  The device remains locked until the 
operator restarts it by use of the START keyin.  This enables the operator to 
print several alignment images, if necessary, to get the paper aligned 
properly without being interrupted by a new file. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
ANSS[CRATCH] devicename [ [ WITH ] #serialnumber ] [ FOR ] sysid 
Description: 
Authorizes the user with the specified sysid to use the tape on the specified 
device as an ANS scratch tape.  If the serialnumber is specified, the scratch 
tape is given that serialnumber. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
AUTO S[CHEDULING] {ON|OFF} 
Description: 
When ON, initiates the automatic scheduling of keyins, ghost jobs, and 
messages by the GOOSE ghost job.  When OFF, the automatic scheduling does not 
take place. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
AUTO S[CHEDULING] M[ESSAGE] {ON|OFF} 
Description: 
When ON, warning messages are sent by the GOOSE ghost when it schedules a 
keyin or a ghost job.  When OFF, the warning messages are disabled. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
AUTO S[CHEDULING] U[PDATE] 
Description: 
Notifies the GOOSE ghost that the GOOSE_EGG file has been changed. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
B: 
Description: 
Simulates a "BREAK" or "ESCAPE-B" to the console ghost associated with this 
console. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
BATC[H] 
Description: 
Allows a SYSTEM or ADMINISTRATIVE (PADMIN, UADMIN) console to display the 
status of batch jobs in the system.  The following items are shown: 
    BATCH          if new jobs can be entered, then BATCH is ON, otherwise, 
                   BATCH is off. 
    N in queue     is the total number of jobs in the input queue. 
    N allowed      is the total number of batch jobs allowed to run (see ON BA 
                   keyin). 
    N running      is the number of currently running batch job. 
Console Attribute Required: 
ADMINISTRATIVE OUTPUT 
00002
00002
00001
BATCH_ON_OFF
Syntax: 
BATC[H] { ON | OFF } 
Description: 
Allows an operator at a SYSTEM console to control the entry of jobs into the 
input queue.  If ON is specified, then jobs may be !BATCHed from IBEX and 
entered from remote and local input symbiont devices.  If OFF is specified, 
then jobs cannot be !BATCHed or entered from input symbiont devices. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
BATCH_ON_OFF
Syntax: 
BOOT FEP {fepnumber|fepname} 
Description: 
Reboots either the specified FEP, which may be local or remote (if the remote 
FEP is currently active), or an optical disk controller. 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
Syntax: 
BROA[DCAST] [textstring] 
Description: 
Sends the specified text to all online users and logged-on consoles that are 
FEP connected.  Additionally, the textstring becomes the "administrative 
message" placed in the log-on salutation.  If no textstring is present, a 
blank field becomes the administrative message. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
BYE 
Description: 
Logs the operator's console off.  If this keyin is performed on the SCC, it 
ceases to function until a REQuest/EOM sequence is typed in, which logs it 
back on.  If this keyin is performed on the LCC, it ceases to function until a 
RETURN/RETURN sequence is typed in, which logs it back on. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
CANR[EAD] 
Description: 
Cancels the current 'READ' file for the console. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
CANT MOUN[T] devicename 
Description: 
Aborts a requested tape or disk mount because the operator can't or won't 
mount the reel or pack that is being requested on the specified device. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
CANT OVER devicename 
Description: 
Aborts a tape mount which has requested an OVER keyin.  The user receives an 
error indicating the operator denied a rewrite of an unexpired ANS tape. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
CANT RING devicename 
Description: 
Aborts a request for a RING keyin for the reel on the specified tape drive. 
The user receives an error indicating the operator deemed it unsafe to mount 
this reel with a write ring. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
COMGROUP_PROCESSING_KEYINS
COMGROUP_PROCESSING_KEYINS
The following keyins apply to comgroups: 
RESTRICT     Restricts usage of symbiont devices. 
ROUTE FROM   Routes (or inhibits) processing of a workstation by 
             an output symbiont device or class of devices at a 
             terminal name. 
ROUTE INTO   Routes processing of a workstation to an output 
             symbiont device or class of devices. 
SYMB INPUT   Displays status of symbiont input device. 
UNROUTE      Removes ROUTE FROM restrictions and ROUTE INTO 
             additions on devices. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
The following keyins apply to communications consoles: 
@mastername    Sends a textstring to a master terminal or another 
               CP-6 system. 
BOOT FEP       Reboots specified front-end processor. 
CRASH FEP      Disables specified FEP after requesting an online dump, 
               then automatically restarts the FEP. 
DISABLE LINES  Removes available lines from FEP. 
DISCONNECT     Disconnects specified FEP channel or channels. 
DISCONNECT     Disconnects terminal associated with a console. 
  TERMINAL 
DUMP FEP       Disables and requests dump of FEP. 
E FEP          Errors the current job step for the specified FEP user. 
ENABLE         Makes lines available for logon and use. 
FEPS           Displays status of all front-end processors. 
HEADER         Defines logon header message. 
HOSTS          Displays status of host or all hosts. 
KILL           Immediately disconnects and disables a line or lines. 
LINKS          Displays status of local FEP connected to this host. 
MASTERS        Displays master terminals connected to CP-6 slave system. 
NETWORK ROUTE  Displays network routing information for node or nodes. 
NODES          Displays status of specified node or all nodes. 
STATION        Displays all devices associated with a console. 
START FEP      Allows specified FEP to operate normally. 
START FEPS     Performs START FEP for all FEPs. 
STOP FEP       Shuts down but does not crash specified FEP. 
STOP FEPS      Performs STOP FEP for all FEPs. 
TELL           Sends string to specified console. 
TELLALL        Sends string to all consoles. 
TERMINAL       Displays terminals that are currently connected. 
TERMINALS      Displays all communications-connected terminals and 
               devices. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
CONS[OLES] 
Description: 
Displays currently logged-on consoles.  (Useful when using the TELL and X 
CONSOLE Keyins.)  Information displayed includes console device name, 
associated terminal, associated workstation, and input and output attributes 
for each console.  If a console is a FEP connected console that did not log on 
as part of a terminal, its logon string is also displayed. 
Console Attribute Required: 
ANY 
00002
00002
00001
The following keyins apply to console ghosts: 
B:            Issues a "BREAK" to the console ghost. 
F:            Performs an "END-OF-FILE" to a pending read for a console ghost. 
G:            Provides input to a console ghost. 
GHOST         Initiates a console ghost. 
PENDING       Displays the outstanding M$KEYIN reads requiring a 
              response from this console. 
Y:            Sends a <CNTL-Y> to the console ghost. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
CONS[OLE] STAT[US] 
Description: 
Displays the following information: 
1.  The devicename of the console, the associated terminal, and the 
    workstation of the console this keyin was submitted from. 
2.  If a console ghost is active, the current console ghost prompt. 
3.  The attributes and maximum priority for PRIO keyins. 
4.  The status of the UC (uppercase) flag, the current profile, the status of 
    the TIME messages (whether or not they are being printed) and the natural 
    language of the console. 
5.  The turnover of the accounting log and the history file. 
6.  The current accounts for READ keyins, and the line printer workstation 
    name. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
CONT[INUE] devicename 
Description: 
Allows suspended output to be resumed at the point of interruption.  See the 
SUSPEND keyin.  Devicename must specify an output symbiont device. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
CPU portnumber 
Description: 
Allows a SYSTEM or ADMINISTRATIVE console to display the status of the CPU 
specified by its decimal portnumber. 
Console Attribute Required: 
ADMINISTRATIVE OUTPUT 
00002
00002
00001
Syntax: 
CPUS 
Description: 
Allows a console to display the status of all known CPUs in the system. 
Console Attribute Required: 
ADMINISTRATIVE OUTPUT 
00002
00002
00001
Syntax: 
CRASH FEP {fepnumber|fepname} 
Description: 
Disables the specified FEP after requesting an upline dump of its contents, 
then automatically restarts the FEP after it has been dumped.  FEP specified 
may be local or remote (if the remote FEP is active). 
Also used to disable and restart an optical disk controller, but no upline 
dump is produced. 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
Syntax: 
DATE mm/dd/yy 
Description: 
Sets the current date for the CP-6 system.  Often used in conjunction with the 
TIME keyin. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
DELE[TE] I[NPUT] sysid 
Description: 
Deletes the specified sysid from the batch input queue. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
DELE[TE] I[NPUT] ALL [ .account ] [ @wsnname ] 
Description: 
If no options are given, all waiting jobs for this workstation will be deleted 
(if keyed in at a console with the ADMINISTRATIVE INPUT attribute), or all 
waiting jobs in the system will be deleted (if keyed in at a INPUT console 
with the SYSTEM INPUT attribute). 
If the optional @wsnname is specified from a SYSTEM console, only waiting jobs 
at the specified workstation will be deleted. If the optional account is 
given, only waiting jobs from that account will be deleted. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If .account or @wsnname is specified, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
DELE[TE] O[UTPUT] sysid [-identifier] 
Description: 
Deletes the output for the specified sysid.  If the optional identifier is 
omitted, all output for that sysid is deleted.  If the identifier is a valid 
identifier for an output symbiont sub-file, only that sysid's sub-file is 
deleted. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
DELE[TE] O[UTPUT] ALL [[NOT] .account] [[NOT] @wsnname] 
Description: 
Deletes all output symbiont files created by the specified account.  If the 
keyin is performed at a unit record console (such as an IRBT console) only 
output destined for the terminal is deleted.  If the keyin is performed from a 
SYSTEM console, and the optional wsnname is specified, then only output for 
that account at that workstation is deleted. 
If wsnname is not specified, and if the console is a system console, all 
output in the system is deleted; otherwise all output for the issuing 
console's terminal is deleted.  If wsnname is specified (allowed at SYSTEM 
consoles only), all output for the specified workstation is deleted. 
The NOT allows the specification of all accounts or workstations that are not 
named specifically. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If @wsnname is used, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
DELE[TE] O[UTPUT] ALL [NOT] FORM=formname [[NOT] @wsnname] 
Description: 
Deletes all output symbiont files created for and waiting to output on the 
specified form.  If the keyin is performed at a unit record console (such as 
an IRBT console) only output destined for that terminal is deleted.  If the 
keyin is performed from a SYSTEM console, and the optional wsnname is 
specified, only output for that form name at that workstation is deleted.  If 
the optional wsnname is not specified, all output for that form name at all 
terminals is deleted.  The NOT allows the specification of all formnames or 
workstations that are not named specifically. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If @wsnname is used, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
DELTA 
Description: 
Transfers control of the system to the executive debugger if retained in 
memory during the last tape or disk boot.  Note that if the keyin is used from 
a system console that is not IOM connected, i.e., not an LCC or SCC, the 
system will stop in DELTA and will not accept DELTA commands from the console 
that issued the keyin.  DELTA will only accept commands from an LCC or SCC. 
Same as the XDELTA keyin. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
DEVI[CES] 
Description: 
Displays the devices that currently have an error condition.  These devices 
may need a RETRY, ERROR, or PROCEED keyin, or may require manual intervention 
in order to clear the error condition. 
Console Attribute Required: 
DEVICE OUTPUT 
00002
00002
00001
Syntax: 
DIAG sysid 
Description: 
Authorizes the specified user for diagnostic access. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
The following keyins can only be issued from a SYSTEM console, and apply to 
diagnostic access: 
DIAG    Authorizes a user for diagnostic access. 
ERSEND  Places a textstring in the system error logging file. 
NODIAG  Denies a user diagnostic access. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
DIE! 
Description: 
Initiates an OPERATOR RECOVERY.  The exclamation point (!) is required. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
DISA[BLE] [LINE[S]] {fepnumber|fepname} - startingline [ -> endingline ] 
Description: 
Removes availability of the specified line(s) in the specified FEP.  If 
endingline is specified, all lines from startingline through endingline in the 
specified FEP will be disabled.  If only startingline is specified, then only 
the single line identified by startingline will be disabled. 
If the DISABLE keyin refers to line(s) currently supporting a logged on 
terminal or timesharing user, the line will become unavailable after the 
lines' user(s) log off.  If there are no current users, the lines will be 
disabled immediately.  Once disabled no new logons will be allowed until a 
subsequent ENABLE keyin is performed. 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
Syntax: 
DISC[ONNECT] {fepnumber | fepname} - startingline [-> endingline] 
Description: 
Disconnects the specified FEP channel or channels.  If only startingline is 
specified, only that single line will be disconnected.  If endingline is 
specified, then all lines from startingline through endingline will be 
disconnected. 
Console Attribute Required: 
COMM, SYSTEMP 
00002
00002
00001
Syntax: 
DISC[ONNECT] TERM[INAL] [ @terminalname ] 
Description: 
Disconnects the terminal associated with this console if performed at an 
ADMINISTRATIVE INPUT console, or any specified terminal if performed at a 
SYSTEM console.  A SYSTEM console must specify the terminal name. 
Console Attribute Required: 
COMMUNICATION INPUT 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
DISK [devicename] 
Description: 
Displays the status of the requested disk drive and its mounted packset, if 
any.  If devicename is not specified, displays the status of all disk drives 
controlled by this console that have physically mounted packsets on them. 
Console Attribute Required: 
DEVICE OUTPUT 
00002
00002
00001
The following keyins apply to disk drives: 
DISK        Displays status of disk drives. 
DISMOUNT    Requests dismount of unused packset. 
EXCLMOUNT   Specifies that a packset is to be used exclusively. 
PUBLIC      Mounts a public packset. 
REQUEST     Removes a packset from further access. 
SET         Displays status of a specified packset. 
SETS        Displays status of all currently mounted packsets. 
SHARE       Mounts a shared packset. 
VOLUMES     Displays the volume mounted on a specified disk drive. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
DISM[OUNT] packsetname [{FAST|NOW}] 
Description: 
Requests the dismount of the specified packset when all users who are now 
associated with it cease to be associated with it.  Note, however, that a 
still-spinning pack (as in a 501) is still subject to user accessing.  To 
prevent this, use the EXCLMOUNT keyin specifying this packset. 
If FAST is specified, the dismount is delayed until all batch users have 
completed and when associated online users reach jobstep (barring them further 
access).  If NOW is specified, the dismount takes place immediately and 
associated users will be aborted. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
DISP[LAY] ALL [[NOT].account] [{F[ORCE]|ON LP|S[HORT]}] 
Parameters: 
NOT    allows the specification of all accountnames that are not named 
specifically. 
FORCE    forces the display; otherwise very long displays are inhibited and a 
notifying message is substituted. 
ON LP    sends the display to be printed to the local line printer using the 
standard form. 
SHORT    generates a shortened version of the display. 
Description: 
Performs a DISP JOB, DISP INPUT, and DISP OUTPUT combined, thus showing all 
jobs that could possibly be displayed. 
Console Attribute Required: 
DEVICE OUTPUT 
00003
00003
00002
00001
Syntax: 
DISP[LAY] DEFE[R] [[NOT].account] [[NOT]@wsnname] [{F[ORCE]|ON LP}] 
Parameters: 
NOT    allows the specification of all accountnames or workstations that are 
not named specifically. 
FORCE    forces the display; otherwise very long displays are inhibited and a 
notifying message is substituted. 
ON LP    sends the display to be printed to the local line printer using the 
standard form. 
Description: 
If no deferred jobs are found, the following message appears: 
"Sorry, you have no deferred jobs" 
Otherwise, the following message appears for each deferred job: 
"sysid <sysid> (<jobname>.<accn>) deferred to <time>" 
where <time> is the date and time at which the job is to be scheduled. 
Console Attribute Required: 
ADMINISTRATIVE OUTPUT 
If @wsnname is specified, SYSTEM OUTPUT is required. 
00003
00003
00002
00001
Syntax: 
DISP[LAY] I[NPUT] [[NOT].account] [[NOT]@wsnname] [{F[ORCE]|ON LP|S[HORT]}] 
Parameters: 
NOT    allows the specification of all accountnames or workstations that are 
not named specifically. 
FORCE    forces the display; otherwise very long displays are inhibited and a 
notifying message is substituted. 
ON LP    sends the display to be printed to the local line printer using the 
standard form. 
SHORT    generates a shortened version of the display. 
Description: 
Displays the entire input queue.  If there is none (for the issuing console), 
the following message appears: 
"Sorry, you have no waiting jobs" 
Otherwise, a list of the input queue appears.  Jobs that are waiting to run 
are listed first (from priority 15 to priority 0); for each of these, a 
message as shown under DISP PRIO n appears.  Next, the NORUN jobs (if any) are 
listed, with the message for each as shown under DISP NORUN.  Then the 
deferred jobs (if any) are listed, with the message for each as shown under 
DISP DEFER. 
Console Attribute Required: 
ADMINISTRATIVE OUTPUT 
If @wsnname is specified, SYSTEM OUTPUT is required. 
00003
00003
00002
00001
Syntax: 
DISP[LAY] NORU[N] [[NOT].account] [[NOT]@wsnname] [{F[ORCE]|ON LP}] 
Parameters: 
NOT    allows the specification of all account names or workstations that are 
not named specifically. 
FORCE    forces the display; otherwise very long displays are inhibited and a 
notifying message is substituted. 
ON LP    sends the display to be printed to the local line printer using the 
standard form. 
Description: 
Displays all waiting jobs which cannot run with the current partition 
definition and resource configuration.  If no such jobs are found, the 
following message appears: 
"Sorry, you have no norun jobs" 
Otherwise, the following message appears for each such job: 
"Sysid <sysid> (<accn>) requires TIM=mm:ss MEM=k [<psl>] [<dvl>] [<sul>]" 
where: 
psl    appears if the job requires packsets, and is a packset list of the 
form: 
    #name(pa),#name(pa),... 
    where pa = PB (public), PR (private), EX (exclusive) 
<dvl>    appears if the job requires resource devices, and is a device list of 
the form: 
    LLD (<atl>),LLD (<atl>),... 
    where <atl> is an attribute list of the form: 
        <atr>,<atr>,...  with each <atr> one of the following: 
            LC, BIN, APL, OVR, 100MB, 200MB, 500MB, 600MB, 800BPI, 1600BPI, 
            6250BPI 
<sul>    appears if the job requires pseudo resources, and is a 
pseudo-resource list of the form: 
    name1=n,name2=m,... 
Console Attribute Required: 
ADMINISTRATIVE OUTPUT 
If @wsnname is specified, SYSTEM OUTPUT is required. 
00003
00003
00002
00001
Syntax: 
DISP[LAY] NSFO[RM] [[NOT].account] [[NOT]@wsnname] [{F[ORCE]|ON LP}] 
Parameters: 
NOT    allows the specification of all accounts or workstations that are not 
named specifically. 
FORCE    forces the display; otherwise very long displays are inhibited and a 
notifying message is substituted. 
ON LP    sends the display to be printed to the local line printer using the 
standard form. 
Description: 
Displays output files with nonstandard forms.  A nonstandard form is defined 
as any formname not beginning with the letters "STD" (STDLP is standard, 
CPUNCH is not).  If there are none, the following message appears: 
"Sorry, you have no symbiont output for nonstandard form" 
Otherwise, each such file is listed with the same message as for DISP OUTPUT: 
"output <sysid>-<num>(<accn>): <dt> [@<wsn>] form<form>" 
where: 
<dt>    is the device type (e.g., LP) 
<form>    is the formname 
Console Attribute Required: 
DEVICE OUTPUT 
If @wsnname is specified, SYSTEM OUTPUT is required. 
00003
00003
00002
00001
Syntax: 
DISP[LAY] O[UTPUT] [[NOT] FORM=[formname] [[NOT] .account] [FOR devicetype] 
[[NOT]@wsnname] [{F[ORCE]|ON LP|S[HORT]}] 
Parameters: 
NOT    allows the specification of all formnames, accountnames, or 
workstations that are not named specifically. 
FORCE    forces the display; otherwise very long displays are inhibited and a 
notifying message is substituted. 
ON LP    sends the display to be printed to the local line printer using the 
standard form. 
SHORT    generates a shortened version of the display. 
Description: 
If devicetype is not specified, this keyin displays the entire queue of output 
symbiont files associated with the issuing console, and if none exist, the 
following message appears: 
"Sorry, you have no symbiont output" 
If the optional workstation name is specified (legal only from SYSTEM 
consoles), only that workstation's output is displayed.  If the terminalname 
is not specified from SYSTEM console, ALL output in the host system is 
displayed. 
If devicetype is specified, it is a device type (e.g., LP, CP, etc.), and then 
only those files destined for the given type are displayed; if none exists, 
the following message appears: 
"Sorry, you have no symbiont output for devicetype" 
Otherwise, the appropriate files are listed.  When an operator displays output 
symbiont file information interactively, a combination of the following 
message appears in the response: 
"Output <sysid>-<num> (<accn>): <dt>[@<term>] [<form>] nn [xc] grans prio 
<p>[(C)] [on<dt> nn | being spilled]" 
In non-interactive responses (i.e., those directed to LP), messages are listed 
in column format with the following headings: 
SYSID, NUM, MODE, JOBNAME, ACCOUNT, DESTINATION, GRANS, COPIES, PRIO, SAP, 
COM, *FORM*, ATTR, *CREATED AT*, *NODEV* 
where 
    sysid    is the system id. 
    num    is the output sub-file identifier for the sysid. 
    (accn):    is the account from which the output is generated. 
    dt    is the device type (e.g., LP) 
    [@term]    is the destination TERMINAL which appears only on system 
    consoles and in non-interactive responses. 
    [form]    specifies the formname enclosed in brackets ([]), which is 
    printed only if it is neither STDLP nor STD**.  In non-interactive 
    responses, the form always appears and is not enclosed in brackets. 
    nn grans    is the size of the file in granules. 
    [xc]    is the number of copies to print (displayed only in interactive 
    responses). 
    prio p    is the assigned priority of the file from 0 to 15 or one one of 
    the following: 
        SPLD    specifies spilled. 
        CMFW    specifies a concurrent multi-file wait (i.e., incomplete 
        chunked file). 
        HOLD    specifies that output is being held after printing the number 
        of copies specified in the SAPCOPIES field in the FIT. 
    (C)    appears only if the file is built in commode chunks and is eligible 
    to print (i.e., prio not W).  If OUTSYM has received the last commode 
    chunk of a file, or the file is not chunked the commode field contains 
    "N".  If a commode file is still being built, the commode field contains 
    the highest chunk number that has currently been built. 
    dtnn    is the device that the file is being output on if it is currently 
    being output.  For both interactive and non-interactive responses, when a 
    device is available for output, the field is left blank; otherwise it 
    contains the message "*NODEV*" for non-interactive responses and "NODEV" 
    for interactive responses. 
    MODE    specifies the mode of the output creator (i.e., BAtch, GHost, Time 
    Sharing (TS) or Transaction Processing (TP)) and is listed only in 
    non-interactive responses. 
    SAP    is a flag (displayed only in non-interactive responses) which 
    informs OUTSYM to save a file after printing because more copies are to be 
    printed.  If "copies" or "hold copies" was specified on the LDEV command, 
    then SAP (Save After Print) and SAPCOPIES (Save After Print COPIES) are 
    set in the output file's FIT.  SAPCOPIES contains the number specified in 
    "hold copies" and tells OUTSYM to halt after printing the number of copies 
    specified.  If only one copy is to be printed, the field contains "N".  If 
    multiple copies are to be printed, the field contains "SAPCOPIES". 
    ATTR    specifies the file output attributes (displayed only in 
    non-interactive responses).  The following is a list of attributes: 
        O    true overprint. 
        L    lower case. 
        B    binary. 
        A    APL. 
    CREATED AT    is the creation time of the output. 
Console Attribute Required: 
DEVICE OUTPUT 
If @wsnname is specified, SYSTEM OUTPUT is required. 
00003
00003
00002
00001
Syntax: 
DISP[LAY] PRIO [[NOT].account] n [TO m] [[NOT]@wsnname] [{F[ORCE]|ON LP}] 
Parameters: 
NOT    allows the specification of all accountnames or workstations that are 
not named specifically. 
FORCE    forces the display; otherwise very long displays are inhibited and a 
notifying message is substituted. 
ON LP    sends the display to be printed to the local line printer using the 
standard form. 
Description: 
Displays the input queue of jobs at priority n, or, if "TO m" is specified, 
priority n thru m (m > n). 
If no such jobs are found, the message 
"Sorry, you have no jobs waiting at the specified priority" 
appears on the issuing console. 
Otherwise, for each waiting job, the following message appears: 
"Sysid <sysid> (<accn>) <pos>, prio n" 
where 
    <pos> is the position (e.g., 1st, 33rd, etc). 
Console Attribute Required: 
DEVICE OUTPUT 
If @wsnname is specified, SYSTEM OUTPUT is required. 
00003
00003
00002
00001
Syntax: 
DISP[LAY] R[UNNING] [[NOT].account] [[NOT]@wsnname] [{F[ORCE]|ON LP}] 
Parameters: 
NOT    allows the specification of all accountnames or workstations that are 
not named specifically. 
FORCE    forces the display; otherwise very long displays are inhibited and a 
notifying message is substituted. 
ON LP    sends the display to be printed to the local line printer using the 
standard form. 
Description: 
Displays the currently running jobs.  If no running jobs are found, the 
message 
"Sorry, you have no running job" 
appears on the issuing console, even if ON LP was requested. 
Otherwise, the following message appears for each job found: 
"Job <sysid> (<jobname>.<accn>) on since <hh:mm>, in part <part>#" 
Console Attribute Required: 
ADMINISTRATIVE OUTPUT 
If @wsnname is used, SYSTEM OUTPUT is required. 
00003
00003
00002
00001
Syntax: 
DISP[LAY] sysid [FULL] [{F[ORCE]|ON LP|S[HORT]}] 
Parameters: 
FULL    requests a full display (see Description below). 
FORCE    forces the display; otherwise very long displays are inhibited and a 
notifying message is substituted. 
ON LP    sends the display to be printed to the local line printer using the 
standard form. 
SHORT    generates a shortened version of the display. 
Description: 
If FULL is not requested, displays the current status of the given sysid as a 
batch job or as symbiont output.  That is, if no symbiont output exists for 
the sysid, and if it is not a running or waiting job, the following message 
appears: 
"Sorry, you have nothing to display for sysid <sysid>" 
Otherwise, appropriate messages appear.  Specifically, if the sysid is a job 
waiting to run, the message shown under DISP PRIO or DISP DEFER or DISP NORUN 
(as determined by the job's status) appears.  If the sysid is a running job, 
the message shown under DISP RUN appears.  In addition, if any symbiont output 
for the sysid exists, each such file results in a message of the type shown 
under DISP OUTPUT. 
Requesting FULL causes the display to be different only in that if the sysid 
is a job waiting to run, or running, then the following message is displayed 
regardless of its status: 
"Sysid <sysid> (<jobname>.<accn>) [(<oan>)] [(<org>)] <gpos> <rql> [(<fol>)]" 
where 
    <oan>    appears only if the job specified is at least one of ORDER, 
    ACCOUNT, NRERUN, and is one of "O", "A", "N", "OA", "ON", "AN", "OAN" 
    depending on which combination was specified. 
    <org>    describes the WSN from which the job originated (W1) and the WSN 
    under which the job will run (W2); it appears only if at least one of W1, 
    W2 does not match the console's WSN, and has the form 
        W1 
    if W1=W2, and otherwise has the form 
        W1 -> W2 
    <gpos>    is "deferred to <time>" if the job is deferred, 
        "NORUN"    if the job is norun, 
        <pos>    if the job is waiting to run.  (See <pos> 
                 under DISP PRIO n). 
    <rql>    is resource requirement list as defined under "DISP NORUN". 
    <fol>    appears only if the job follows some other job(s), and is: 
        "follows <sysid1>,<sysid2>,..." 
Console Attribute Required: 
ADMINISTRATIVE OUTPUT 
00003
00003
00002
00001
Syntax: 
DUMP FEP {fepnumber|fepname} 
Description: 
Disables the specified FEP after requesting an upline dump of its contents.  A 
BOOT FEP keyin must be issued to restart the FEP after it has been DUMPed. 
May be used with local fepnumber or fepname, or with remote FEP if connected. 
Also used to disable an optical disk controller, but no upline dump is 
produced. 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
Syntax: 
E sysid 
Description: 
Errors the current job step for the specified user. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
ENAB[LE] {fepnumber|fepname} - startingline [-> endingline] [ONCE] 
Description: 
Makes the specified line or lines available for logon and use (if DISABLEd or 
KILLed). 
If only startingline is specified, only that single line will be enabled.  If 
endingline is specified, then all lines from startingline through endingline 
will be enabled.  If ONCE is specified, the line or lines are to allow only 
one logon, and then be automatically disabled when the line's user logs off 
(see DISABLE keyin). 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
Syntax: 
ERRO[R] devicename 
Description: 
If the specified device has an error condition, this keyin causes the current 
I/O activity on the specified device to be aborted, and returns an error code 
to the device's user. 
Using the ERROR keyin for disk devices may result in destroyed files or file 
directories; use only as a last resort in this case. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
ERSE[ND] textstring 
Description: 
Causes the specified textstring to be placed in the system error logging file. 
Console Attribute Required: 
ADMINISTRATIVE INPUT, DEVICE INPUT 
00002
00002
00001
Syntax: 
EXCL[MOUNT] packsetname 
Description: 
Specifies that the next time the specified packset is mounted, it will be 
mounted for exclusive access only.  Must follow a DISMOUNT keyin if the 
operator wants to prevent user access to a still-spinning pack. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
E FEP n-sysid 
Parameters: 
n    is a fepnumber or fepname. 
Description: 
Errors the current job step for the specified FEP user. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00003
00003
00002
00001
Syntax: 
F: 
Description: 
Performs an "END-OF-FILE" on the read currently outstanding for the console 
ghost associated with this console. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
FEPS|FEP {fepnumber|fepname} 
Description: 
Displays the status of the specified FEP.  If no FEP number or name is given, 
the status of all FEPs will be displayed. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
FIRM[LOAD] mpcname 
Parameters: 
mpcname    may be TCnn, UCnn, or DCnn where nn is 01, 02, etc., as defined in 
the system TIGR deck. 
Description: 
Requests a firmware download to the specified MPC.  Firmware can only be 
loaded using the first non-partitioned channel found.  Switches on MPCs must 
be set correctly to allow firmware loading using that channel.  If all 
channels to a controller are partitioned or if the switches are not properly 
set on an MPC, the firmware load will fail. 
For the DPS 90, the FIRMLOAD keyin does not actually load firmware into a 
controller.  That is accomplished by using the MSOS LOAD command.  However, if 
CP-6 reports (on the system console) that an MPC is stopped on a DPS 90, the 
way to start it again is to issue a FIRMLOAD keyin. 
For the DPS 8000, FIRMLOAD keyins to IPC-type controllers (FIPS tape, FIPS 
disk, UR channels) may require up to one minute or more to complete.  IPC 
firmware is loaded via the MCA. 
Console Attribute Required: 
DEVICE INPUT 
00003
00003
00002
00001
Syntax: 
FLUSH devicename 
Description: 
Causes the specified input symbiont to discard the current job or NCTL file 
being built, and to flush the input stream up to the end of the current 
job/file. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
FORM ON keyin 
Syntax: 
FORM [ON]  devicename  [IS]  formname 
Description: 
Causes the specified form to be mounted on the specified output device.  If 
the FORM keyin is issued to a symbiont output device, then the device MUST BE 
IDLE.  If the FORM keyin is issued to a resource (non-symbiont) output device, 
then the device MUST NOT BE IN USE (idle or requesting a form mount). 
After this keyin is issued to a symbiont device, the device is considered to 
be "unaligned".  This means that the first time a file starts output on the 
device, an alignment sequence is initiated.  However, if the device is not 
symbiont, no further action is taken by the CP-6 system; thus the program 
owning the resource output device must perform its own alignment sequence. 
For symbiont devices, if the form was defined by SUPER to have no alignment 
image, then an 'alignment sequence' simply consists of loading the VFU image, 
whereupon the message "VFU image loaded" appears, and the file starts to 
output.  Otherwise (i.e., if there really is an alignment image), the 
alignment image is output; when this finishes, the device automatically 
suspends (to permit the operator to verify the alignment).  If realignment is 
desired, the ALIGN keyin may be used to cause the alignment image to be output 
again (followed by automatic suspend). 
When the operator is satisfied with the alignment, the CONTINUE keyin causes 
the file to start output.  After the alignment has been completed 
successfully, the device is considered to be aligned.  Note that if the 
alignment sequence aborts due to a device error, then the CONTINUE keyin is 
rejected (because the device is unaligned); the operator must complete the 
alignment sequence before continuing.  Note also that while the alignment 
sequence is in progress, none of the usual keyins (REPRINT, SUSPEND, etc) can 
be issued to the device. 
Console Attribute Required: 
DEVICE INPUT 
00003
00003
00002
00001
Syntax: 
G: [textstring] 
Description: 
Causes the specified text to satisfy the read of the console ghost associated 
with this console. 
Console Attribute Required: 
ANY 
00002
00002
00001
    The following keyins provide general console functions: 
    ?                Obtains additional levels of HELP. 
    ??               Obtains all additional levels of HELP. 
    BYE              Logs the console off the system. 
    CONSOLES         Displays information about all consoles. 
    CONSOLE STATUS   Displays information about the issuing console. 
    HELP             Prints information about valid CP-6 keyins. 
    HISTORY          Enables or disables console activity logging. 
    INFO             Prints ETMF, TIME, DATE, and 90% RESPONSE TIME. 
    MSG              Sends a message to all system consoles. 
    MYREAD           Sets the account for READ keyins. 
    NATLANG          Sets the active language for the console. 
    OCHIST           Closes current history file and opens a new one. 
    OFF              Logs the console off the system. 
    PENDING          Displays outstanding M$KEYIN request. 
    PROFILE          Sets the terminal profile for an FEP Connected Console. 
    READ             Executes a file of keyins. 
    READ$            Begins each READ file. 
    READACCT         Changes default account for READ keyins. 
    TIME             Requests the time if activity has occurred in the 
                     last minute. 
    TURNOVER         Closes current history or accounting file and opens a 
                     new file at the specified time. 
    UC               Requests or suppresses the increase to Upper-Case 
                     translation. 
    X CONSOLE        Allows a system console to remove other consoles 
                     from the system. 
    To obtain more information about a keyin, enter: 
        HELP keyin 
    To obtain the console attribute for a specific 
    keyin, enter: 
        HELP keyin ATTR 
The following keyins apply to all devices: 
DEVICES     Displays devices currently in an error condition. 
ERROR       Suspends activity on a specified device. 
FIRMLOAD    Requests a firmware download to an MPC. 
PROCEED     Overrides I/O error condition and return to normal. 
QUIET       Suppresses repetitive error reporting at the console. 
RETRY       Retries current erroring I/O. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
GHOST account, username [ ,password ] 
Description: 
Initializes a console ghost for this console if the specified account number, 
username and password are a legal logon ID.  Note that the account must be 
authorized for ONLINE usage by SUPER. 
Console Attribute Required: 
ANY 
00002
00002
00001
KEYIN_GROUPS
Syntax: 
HEAD[ER] [textstring] 
Description: 
Defines the administrative message seen in the logon header to be the 
specified textstring.  This keyin, unlike the BROADCAST keyin, does not send 
the text to all online users.  If the textstring is not specified, the 
administrative message is reset to blanks. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
HELP [(KEYIN)] [TOPICS] [keyword1] [keyword2] 
Description: 
Prints information about the valid CP-6 keyins.  (Only KEYIN HELP is available 
from a console.  In addition, ranges of HELP are prohibited from a console). 
The following examples illustrate the use of the HELP keyin: 
    Keyin            Description 
    HELP             prints an overview of KEYIN. 
    HELP TOPICS      prints a list of valid keywords. 
    HELP SEND        prints the first level message for the SEND 
                     keyin.  Entering a question mark (?) prints 
                     the next deeper level of the message. 
                     Entering a double question mark (??) prints 
                     all levels. 
    HELP SEND ATT    prints the minimum attribute required for the 
                     SEND keyin. 
    HELP DISK DES    prints a description of the DISK keyin. 
Console Attribute Required: 
ANY 
00002
00002
00001
A 
  ABORT Keyin - 
      HELP ABORT 
  ACCTLG Keyin - 
      HELP ACCTLG 
  ALIGN Keyin - 
      HELP ALIGN 
  ANSSCRATCH Keyin - 
      HELP ANSSCRATCH 
  AUTO SCHEDULING Keyin - 
      HELP AUTO_SCHEDULING 
  AUTO SCHEDULING MESSAGE Keyin - 
      HELP AUTO_SCHEDULING_MESSAGE 
  AUTO SCHEDULING UPDATE Keyin - 
      HELP AUTO_SCHEDULING_UPDATE 
B 
  B: Keyin - 
      HELP B: 
  BATCH Keyin - 
      HELP BATCH 
  BATCH ON/OFF Keyin - 
      HELP BATCH_ON_OFF 
  BOOT FEP Keyin - 
      HELP BOOT_FEP 
  BROADCAST Keyin - 
      HELP BROADCAST 
  BYE Keyin - 
      HELP BYE 
C 
  CANREAD Keyin - 
      HELP CANREAD 
  CANT MOUNT Keyin - 
      HELP CANT_MOUNT 
  CANT OVER Keyin - 
      HELP CANT_OVER 
  CANT RING Keyin - 
      HELP CANT_RING 
  Comgroup Processing Keyins - 
      HELP COMGROUP_PROCESSING_KEYINS 
  Communications Keyins - 
      HELP COMMUNICATIONS_KEYINS 
  Console Ghost Keyins - 
      HELP CONSOLE_GHOST_KEYINS 
  CONSOLE STATUS Keyin - 
      HELP CONSOLE_STATUS 
  CONSOLES Keyin - 
      HELP CONSOLES 
  CONTINUE Keyin - 
      HELP CONTINUE 
  CP-6 Operator Keyins - 
      HELP OPERATOR_KEYINS 
  CPU Keyin - 
      HELP CPU 
  CPUS Keyin - 
      HELP CPUS 
  CRASH FEP Keyin - 
      HELP CRASH_FEP 
D 
  DATE Keyin - 
      HELP DATE 
  DELETE INPUT ALL Keyin - 
      HELP DELETE_INPUT_ALL 
  DELETE INPUT Keyin - 
      HELP DELETE_INPUT 
  DELETE OUTPUT ALL FORM Keyin - 
      HELP DELETE_OUTPUT_ALL_FORM 
  DELETE OUTPUT ALL Keyin - 
      HELP DELETE_OUTPUT_ALL 
  DELETE OUTPUT Keyin - 
      HELP DELETE_OUTPUT 
  DELTA Keyin - 
      HELP DELTA 
  DEVICES Keyin - 
      HELP DEVICES 
  DIAG Keyin - 
      HELP DIAG 
  Diagnostic Keyins - 
      HELP DIAGNOSTIC_KEYINS 
  DIE! Keyin - 
      HELP 'DIE!' 
  DISABLE LINES Keyin - 
      HELP DISABLE_LINES 
  DISCONNECT Keyin - 
      HELP DISCONNECT 
  DISCONNECT TERMINAL Keyin - 
      HELP DISCONNECT_TERMINAL 
  Disk Drive Keyins - 
      HELP DISK_DRIVE_KEYINS 
  DISK Keyin - 
      HELP DISK 
  DISMOUNT Keyin - 
      HELP DISMOUNT 
  DISPLAY ALL Keyin - 
      HELP DISPLAY_ALL 
  DISPLAY DEFER Keyin - 
      HELP DISPLAY_DEFER 
  DISPLAY INPUT Keyin - 
      HELP DISPLAY_INPUT 
  DISPLAY NORUN Keyin - 
      HELP DISPLAY_NORUN 
  DISPLAY NSFORM Keyin - 
      HELP DISPLAY_NSFORM 
  DISPLAY OUTPUT Keyin - 
      HELP DISPLAY_OUTPUT 
  DISPLAY PRIO Keyin - 
      HELP DISPLAY_PRIO 
  DISPLAY RUNNING Keyin - 
      HELP DISPLAY_RUNNING 
  DISPLAY sysid Keyin - 
      HELP DISPLAY_SYSID 
  DPS 90 - 
      HELP FIRMLOAD DESCRIPTION: 
  DUMP FEP Keyin - 
      HELP DUMP_FEP 
E 
  E FEP Keyin - 
      HELP E_FEP 
  E Keyin - 
      HELP E 
  ENABLE Keyin - 
      HELP ENABLE 
  ERROR Keyin - 
      HELP ERROR 
  ERSEND Keyin - 
      HELP ERSEND 
  EXCLMOUNT Keyin - 
      HELP EXCLMOUNT 
F 
  F: Keyin - 
      HELP F: 
  FEPS Keyin - 
      HELP FEPS 
  FIPS -   
    LOAD Keyin - 
      HELP LOAD DESCRIPTION: 
    REQUEST Keyin - 
      HELP REQUEST DESCRIPTION: 
  FIRMLOAD Keyin - 
      HELP FIRMLOAD 
  FLUSH Keyin - 
      HELP FLUSH 
  FORM ON Keyin - 
      HELP FORM_ON 
G 
  G: Keyin - 
      HELP G: 
  General Console Keyins - 
      HELP GENERAL_CONSOLE_KEYINS 
  General Device Keyins - 
      HELP GENERAL_DEVICE_KEYINS 
  GHOST Keyin - 
      HELP GHOST 
H 
  HEADER Keyin - 
      HELP HEADER 
  HELP Keyin - 
      HELP HELP 
  HISTORY Keyin - 
      HELP HISTORY 
  HOSTS Keyin - 
      HELP HOSTS 
I 
  INFO Keyin - 
      HELP INFO 
  Informational Keyins - 
      HELP INFORMATIONAL_KEYINS 
  Introduction - 
      HELP INTRODUCTION 
J 
  Job Display Keyins - 
      HELP JOB_DISPLAY_KEYINS 
K 
  ? Keyin - 
      HELP KEYIN_1_QUESTIONMARK 
  ?? Keyin - 
      HELP KEYIN_2_QUESTIONMARKS 
  KEYIN Groups - 
      HELP KEYIN_GROUPS 
  KEYIN Parameters - 
      HELP KEYIN_PARAMETERS 
  KILL Keyin - 
      HELP KILL 
L 
  LINKS Keyin - 
      HELP LINKS 
  LOAD Keyin - 
      HELP LOAD 
  LOCK Keyin - 
      HELP LOCK 
  LPWSN Keyin - 
      HELP LPWSN 
M 
  MAKE CPU Keyin - 
      HELP MAKE_CPU 
  MAKE RESOURCE Keyin - 
      HELP MAKE_RESOURCE 
  MAKE SYMBIONT Keyin - 
      HELP MAKE_SYMBIONT 
  @mastername Keyin - 
      HELP @MASTERNAME 
  MASTERS Keyin - 
      HELP MASTERS 
  Message Sending Keyins - 
      HELP MESSAGE_SENDING_KEYINS 
  MOUNT Keyin - 
      HELP MOUNT 
  MSG Keyin - 
      HELP MSG 
  MYREADACCT Keyin - 
      HELP MYREADACCT 
N 
  NATLANG Keyin - 
      HELP NATLANG 
  NCTL Keyin - 
      HELP NCTL 
  NETWORK ROUTE Keyin - 
      HELP NETWORK_ROUTE 
  NODES Keyin - 
      HELP NODES 
  NODIAG Keyin - 
      HELP NODIAG 
  NOUSERS! Keyin - 
      HELP 'NOUSERS!' 
O 
  OCHIST - 
      HELP HISTORY DESCRIPTION: 
      HELP OCHIST DESCRIPTION: 
      HELP TURNOVER DESCRIPTION: 
  OCHIST Keyin - 
      HELP OCHIST 
  ODUNLOAD Keyin - 
      HELP ODUNLOAD_KEYIN 
  ODVOLINIT Keyin - 
      HELP ODVOLINIT_KEYIN 
  OFF Keyin - 
      HELP OFF 
  ON BA Keyin - 
      HELP ON_BA 
  ON GH Keyin - 
      HELP ON_GH 
  ON Keyin - 
      HELP ON 
  ON TP Keyin - 
      HELP ON_TP 
  ON TS Keyin - 
      HELP ON_TS 
  Optical Disk Keyins - 
      HELP OPTICAL_DISK_KEYINS 
  OVER Keyin - 
      HELP OVER 
P 
  PENDING Keyin - 
      HELP PENDING 
  PRIO INPUT ALL Keyin - 
      HELP PRIO_INPUT_ALL 
  PRIO INPUT Keyin - 
      HELP PRIO_INPUT 
  PRIO OUTPUT .account Keyin - 
      HELP PRIO_OUTPUT_.ACCOUNT 
  PRIO OUTPUT ALL Keyin - 
      HELP PRIO_OUTPUT_ALL 
  PRIO OUTPUT sysid Keyin - 
      HELP PRIO_OUTPUT_SYSID 
  PROCEED Keyin - 
      HELP PROCEED 
  PROFILE Keyin - 
      HELP PROFILE 
  PUBLIC Keyin - 
      HELP PUBLIC 
  PWIDTH Keyin - 
      HELP PWIDTH 
Q 
  Queue Control Keyins - 
      HELP QUEUE_CONTROL_KEYINS 
  QUIET Keyin - 
      HELP QUIET 
R 
  READ Keyin - 
      HELP READ 
  READ$ Keyin - 
      HELP READ$ 
  READACCT Keyin - 
      HELP READACCT 
  REPRINT Keyin - 
      HELP REPRINT 
  REQUEST Keyin - 
      HELP REQUEST 
  RERUN ALL Keyin - 
      HELP RERUN_ALL 
  RERUN Keyin - 
      HELP RERUN 
  RESERVE Keyin - 
      HELP RESERVE 
  RESTRICT Keyin - 
      HELP RESTRICT 
  RETRY Keyin - 
      HELP RETRY 
  RING Keyin - 
      HELP RING 
  ROUTE FROM Keyin - 
      HELP ROUTE_FROM_KEYIN 
  ROUTE INTO Keyin - 
      HELP ROUTE_INTO_KEYIN 
S 
  S Keyin - 
      HELP S 
  SAVE Keyin - 
      HELP SAVE 
  SCRATCH Keyin - 
      HELP SCRATCH 
  SEND Keyin - 
      HELP SEND 
  SENDALL Keyin - 
      HELP SENDALL 
  SENDFEP Keyin - 
      HELP SENDFEP 
  SET Keyin - 
      HELP SET 
  SETS Keyin - 
      HELP SETS 
  SETUP Keyin - 
      HELP SETUP 
  SHARE Keyin - 
      HELP SHARE 
  SPACE Keyin - 
      HELP SPACE 
  Special System Keyins - 
      HELP SPECIAL_SYSTEM_KEYINS 
  START CPU Keyin - 
      HELP START_CPU 
  START FEP Keyin - 
      HELP START_FEP 
  START FEPS Keyin - 
      HELP START_FEPS 
  START Keyin - 
      HELP START 
  START TP Keyin - 
      HELP START_TP 
  STARTUP!! Keyin - 
      HELP 'STARTUP!!' 
  STATION Keyin - 
      HELP STATION 
  STOP CPU Keyin - 
      HELP STOP_CPU 
  STOP FEP Keyin - 
      HELP STOP_FEP 
  STOP FEPS Keyin - 
      HELP STOP_FEPS 
  SUSPEND Keyin - 
      HELP SUSPEND 
  SWITCH OUTPUT .account Keyin - 
      HELP SWITCH_OUTPUT_.ACCOUNT 
  SWITCH OUTPUT ALL Keyin - 
      HELP SWITCH_OUTPUT_ALL 
  SWITCH OUTPUT FORM Keyin - 
      HELP SWITCH_OUTPUT_FORM 
  SWITCH OUTPUT Keyin - 
      HELP SWITCH_OUTPUT 
  SWITCH OUTPUT sysid Keyin - 
      HELP SWITCH_OUTPUT_SYSID 
  SYMB INPUT Keyin - 
      HELP SYMB_INPUT 
  SYMB OUTPUT Keyin - 
      HELP SYMB_OUTPUT 
  sysid: Keyin - 
      HELP SYSID: 
  System Control Keyins - 
      HELP SYSTEM_CONTROL_KEYINS 
T 
  Tape Drive Keyins - 
      HELP TAPE_DRIVE_KEYINS 
  TAPES Keyin - 
      HELP TAPES 
  TELL Keyin - 
      HELP TELL 
  TELLALL Keyin - 
      HELP TELLALL 
  TERMINAL Keyin - 
      HELP TERMINAL 
  TERMINAL ON Keyin - 
      HELP TERMINAL_ON 
  TERMINALS Keyin - 
      HELP TERMINALS 
  TIME Keyin - 
      HELP TIME 
  TIME ON/OFF Keyin - 
      HELP TIME_ON_OFF 
  TP/ Keyin - 
      HELP TP 
  TPHEADER Keyin - 
      HELP TPHEADER 
  Transaction Processing Keyins - 
      HELP TRANSACTION_PROCESSING_KEYINS 
  TURNOVER Keyin - 
      HELP TURNOVER 
U 
  UC Keyin - 
      HELP UC 
  Unit Record Device Keyins - 
      HELP UNIT_RECORD_DEVICE_KEYINS 
  UNRESERVE Keyin - 
      HELP UNRESERVE 
  UNRESTRICT Keyin - 
      HELP UNRESTRICT 
  UNROUTE Keyin - 
      HELP UNROUTE_KEYIN 
  User Control Keyins - 
      HELP USER_CONTROL_KEYINS 
  USERS Keyin - 
      HELP USERS 
V 
  VOLUMES Keyin - 
      HELP VOLUMES 
X 
  X CONSOLE Keyin - 
      HELP X_CONSOLE 
  X FEP Keyin - 
      HELP X_FEP 
  X Keyin - 
      HELP X_KEYIN 
  XDELTA  Keyin - 
      HELP XDELTA 
Y 
  Y: Keyin - 
      HELP Y: 
Z 
  ZAP!! Keyin - 
      HELP 'ZAP!!' 
  ZAP!  Keyin - 
      HELP 'ZAP!' 
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
Syntax: 
HIST[ORY] { ON | OFF } 
Description: 
Specifies whether logging of operator console activity is to be enabled (ON) 
or disabled (OFF).  When the system is booted, HISTORY is ON.  The status is 
remembered across crashes.  History logging is recommended to aid Bull support 
personnel diagnose problems remotely. 
NOTE:  :OCHIST.:SYSTAC should not be deleted, because doing so makes it 
impossible for KEYIN to correctly restart the console history logging process, 
and also makes it impossible to REPLAY properly. 
If :OCHIST.:SYSTAC is accidentally deleted, it will be necessary to boot the 
system to get history logging started properly. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
HOSTS|HOST {hostnumber|hostname} 
Description: 
Displays the status of the specified host.  If no host number or name is 
given, the status of all hosts will be displayed. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
INFO 
Description: 
Prints ETMF, TIME, DATE, and 90% RESPONSE TIME, similar to the IBEX !DI 
command. 
Console Attribute Required: 
ANY 
00002
00002
00001
The following keyins provide information: 
?               Requests additional HELP. 
??              Requests all additional HELP. 
NETWORK ROUTE   Displays network routing data for node or all nodes. 
BATCH           Displays batch job status. 
CONSOLES        Displays currently logged on consoles. 
CONSOLE STATUS  Displays the attributes of the current console. 
DEVICES         Displays currently erroring devices. 
DISK            Displays status of disk drives. 
DISPLAY         Displays information about batch queues. 
FEPS            Displays front-end processor status. 
HELP            Describes keyins and gives keyin syntax. 
HOSTS           Displays status of host or all hosts. 
INFO            Displays ETMF, TIME, DATE, and 90% RESPONSE TIME. 
LINKS           Displays status of local FEP connected to this host. 
MASTERS         Displays master terminals. 
NODES           Displays status of node or nodes. 
PENDING         Displays outstanding M$KEYIN requests. 
SETS            Displays packset status. 
SETUP           Displays information about a form. 
STARTUP!!       Displays the progress of a system boot. 
STATION         Displays all devices associated with a console. 
SYMB            Displays symbiont information. 
TAPES           Displays tape drive usage. 
TERMINALS       Displays communications-connected terminals. 
USERS           Displays maximum users permitted. 
VOLUMES         Displays tape usage. 
ZAP!!           Displays the current progress of the ZAP! procedure. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 

The following keyins display information about the jobs currently on the 
system.  Because the output of these keyins could be (under certain 
circumstances) very long, a message notifying the operator of a long list is 
sent, and the list is not printed.  The operator can override this restriction 
by adding "FORCE" to the DISPLAY keyin (which forces the list to print) or by 
adding "ON LP" to the DISPLAY keyin, which prints the list on to the line 
printer.  Some forms of DISPLAY also allow "SHORT" to be added, which 
generates a shortened version of the DISPLAY output. 
DISPLAY ALL      Combines a DISPLAY RUNNING, DISPLAY INPUT and 
                 DISPLAY OUTPUT. 
DISPLAY DEFER    Displays deferred jobs. 
DISPLAY INPUT    Displays input queue. 
DISPLAY NORUN    Displays waiting jobs. 
DISPLAY NSFORM   Displays output queue entries requiring nonstandard 
                 forms. 
DISPLAY OUTPUT   Displays the output queue. 
DISPLAY PRIO     Displays input jobs of specified priority. 
DISPLAY RUNNING  Displays currently running jobs. 
DISPLAY sysid    Displays current job status. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
OPERATOR_KEYINS
Syntax: 
? 
Description: 
This keyin is used to obtain additional levels of help.  It should only be 
entered following a HELP keyin. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
?? 
Description: 
This keyin is used to obtain all additional levels of HELP.  It should only be 
issued following a HELP or a ? keyin. 
Console Attribute Required: 
ANY 
00002
00002
00001
The keyins for operator consoles on the CP-6 system can be organized (with 
some overlap) into the following groups: 
    General Console Keyins 
    System Control Keyins 
    Special System Keyins 
    User Control Keyins 
    General Device Keyins 
    Tape Drive Keyins 
    Disk Drive Keyins 
    Optical Disk Keyins 
    Unit Record Keyins 
    Queue Control Keyins 
    Job Display Keyins 
    Communications Keyins 
    Diagnostic Keyins 
    Console Ghost Keyins 
    Informational Keyins 
    Message Sending Keyins 
    Transaction Processing Keyins 
    Comgroup Processing Keyins 
    To obtain a listing of keyins within all 
    keyin groups, enter: 
        HELP OPERATOR_KEYINS 
    To obtain a list of keyins with brief descriptions 
    within a specific keyin group, enter: 
        HELP GENERAL_CONSOLE_KEYINS 
        HELP SYSTEM_CONTROL_KEYINS 
        HELP SPECIAL_SYSTEM_KEYINS 
        HELP USER_CONTROL_KEYINS 
        HELP GENERAL_DEVICE_KEYINS 
        HELP TAPE_DRIVE_KEYINS 
        HELP DISK_DRIVE_KEYINS 
        HELP OPTICAL_DISK_KEYINS 
        HELP UNIT_RECORD_KEYINS 
        HELP QUEUE_CONTROL_KEYINS 
        HELP JOB_DISPLAY_KEYINS 
        HELP COMMUNICATIONS_KEYINS 
        HELP DIAGNOSTIC_KEYINS 
        HELP CONSOLE_GHOST_KEYINS 
        HELP INFORMATIONAL_KEYINS 
        HELP MESSAGE_SENDING_KEYINS 
        HELP TRANSACTION_PROCESSING_KEYINS 
        HELP COMGROUP_PROCESSING_KEYINS 
The following commonly used keyin parameters are defined once, here.  Less 
frequently used parameters are defined in the keyin descriptions where they 
occur. 
1.  A fepnumber is a decimal value between 0 and n.  A unique number is 
    assigned to each FEP by the System Manager (via the NETCON processor). 
    The upper limit is site dependent. 
2.  A fepname is a 1-8 character alphanumeric value assigned to a FEP by the 
    System Manager (via the NETCON processor). 
3.  A filename is a CP-6 file id. 
4.  A devicename is of the form MT01 or mt01. 
5.  A wsnname is of the form @wsnname (1 to 8 characters). 
6.  A terminalname is of the form @terminalname (1 to 8 characters). 
7.  A stationname is of the form @stationname (1 to 8 characters). 
8.  A packsetname is of the form #packsetname (1 to 6 characters). 
9.  A serialnumber is of the form #serialnumber (1 to 6 characters). 
10. A formname is an alphanumeric of 1 to 6 characters. 
Syntax: 
KILL [LINE[S]] {fepnumber|fepname} - startingline [ -> endingline ] 
Description: 
Immediately disconnects and disables the specified line(s) in the specified 
FEP (see DISABLE keyin).  If only startingline is specified, only that single 
line will be killed.  If endingline is specified, all lines from startingline 
through endingline will be killed.  Any connected users or terminals will be 
disconnected (and autosaved if possible).  Any KILLed lines must be enabled 
(see ENABLE keyin) before they can be used again. 
Console Attribute Required: 
COMMUNICATION INPUT 
00002
00002
00001
Syntax: 
LINK[S][fepnumber] 
Description: 
Displays the status of the local FEP or optical disk controller connected to 
this host.  If no number is specified, all nodes connected to the host are 
displayed. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
LOAD devicename 
Description: 
Requests that an automatic start sequence be performed on the specified tape 
drive, i.e., acts as if the START button on the tape drive has been pressed. 
NOTE: Unless the tape is already positioned at BOT, the LOAD keyin is not 
effective with FIPS magnetic tape devices.  In such a case, an error message 
is returned. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
LOCK devicename 
Description: 
Keeps the specified symbiont device from outputting after the current file is 
finished outputting. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
LPWS[N] [=]@workstation_name 
Description: 
Allows an operator with a wild-carded workstation name to select the 
workstation to which the results of DISPLAY ... ON LP are directed.  This 
field must contain a non-blank or non-wildcarded value to successfully perform 
DISPLAY ... ON LP keyins. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
MAKE CPU portnumber [MAST[ER]] 
Description: 
If the CPU on the specified port number is usable as a slave CPU, it will 
become the master CPU.  The currently running master CPU will become a slave 
CPU, and will be automatically stopped (see STOP CPU keyin).  If the operator 
desires to continue using the old master CPU as a slave CPU, he must issue a 
START CPU keyin on the old master CPU's port number. 
This keyin will be rejected and an appropriate error message will be printed 
if either CPU is running in diagnostic mode. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
MAKE devicename RESO[URCE] 
Description: 
Causes the specified symbiont devicename to become a resource device rather 
than a symbiont device. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
MAKE devicename SYMB[IONT] 
Description: 
Causes the specified resource device to become a symbiont device. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
MAST[ERS] 
Description: 
Allows SYSTEM and COMMUNICATION consoles to display the master terminals 
connected to this CP-6 slave system. 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
The following keyins send messages to various destinations: 
@mastername  Sends a message to a master control terminal. 
BROADCAST    Sends a message to all on-line users and makes it a 
             a logon header. 
ERSEND       Sends a textstring to the system error logging file. 
HEADER       Performs a logon header message change. 
MSG          Sends a message to all SYSTEM consoles. 
SEND         Sends a message to a user terminal. 
SENDALL      Sends a message to all user terminals. 
SENDFEP      Sends a message to all stations connected to the specified FEP. 
sysid:       Replies to an M$KEYIN request. 
TELL         Sends a message to another console. 
TELLALL      Sends a message to all consoles. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
MOUN[T] devicename [WITH] serialnumber [[FOR] sysid] 
Description: 
Allows the operator to specify or change the serial number of the tape mounted 
on the specified device.  FOR sysid, specifies that only that sysid can use 
the drive. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
MSG textstring 
Description: 
Causes the textstring to be sent to all SYSTEM consoles in the CP-6 system. 
(See also the TELL and TELLALL keyins.) 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
MYRE[ADACCT] {.account|R[ESET]} 
Description: 
Sets the default account from which READ files will be read for the issuing 
console.  The "default" read account is as follows:  if an operator READs a 
file, and does not specify an account, the default READ account set via this 
keyin will be used.  If no default account is set, the default account will be 
the current system default read account.  Otherwise use the KEYIN global READ 
account.  RESET specifies use the KEYIN global READ default account. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
NATL[ANG] [languagecharacter] 
Description: 
Sets the native language in which the console receives messages. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
NCTL devicename textstring  [ ONCE ] 
Description: 
Changes the default NCTL FID for the specified input symbiont device to the 
specified string.  This is the FID used by such devices as paper tape readers 
(i.e., those for which it is awkward or impossible to transmit a !NCTL 
record), or when a record containing simply '!NCTL' is encountered.  The FID 
must be not more than 25 characters in length. 
If ONCE is specified, then the FID will only be used the next time a default 
is required, after which the default reverts to its value before the keyin was 
issued. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
NETW[ORK] ROUT[E] [nodenumber] 
Description: 
Displays network routing information for specified node, or, if node number is 
not specified, for all nodes. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
NODES|NODE nodenumber 
Description: 
Displays the status of the specified node.  If no node number is given, the 
status of all nodes will be displayed. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
NODI[AG] sysid 
Description: 
Denies the DIAG keyin request for the specified sysid. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
NOTATION_CONVENTIONS
Notation conventions used in command specifications and examples are listed in 
the Notation Conventions table below.  The information can be accessed by 
either entering a ? or ?? immediately following this message, or by entering: 
HELP NOTATION_CONVENTIONS convention 
Available notation conventions are: 
CAPITAL_LETTERS, LOWERCASE_LETTERS, SPECIAL_CHARACTERS, 
BRACKETS, BRACES_AND_OR_BARS, ELLIPSIS, CARATED_LETTERS, 
KEYWORDS, DOUBLE_QUOTES, APOSTROPHE. 
Example:  HELP NOTATION_CONVENTIONS ELLIPSIS 
Descriptions are in tabular form as follows: 
  Notation       Description 
  CAPITAL LETTERS 
                 Capital letters must be entered as shown for input, and will 
                 be printed as shown in output. 
  lowercase letters 
                 Lowercase letters identify an element that must be replaced 
                 with a user-selected value. 
                 AP i could be entered as AP 2. 
  Special Characters 
                 Numbers that appear on the line (i.e., not subscripts), 
                 special symbols, and underlines appear as shown in output 
                 messages and must be entered as shown when input. 
                 #xxx could be entered as #011. 
  Brackets 
                 An element inside brackets is optional.  Several elements 
                 separated by an "or" bar inside a pair of brackets means that 
                 the user may select any one or none of those elements. 
                 [key]   -   means a key value may be entered. 
                 When enclosing keywords, brackets signify that all or part of 
                 the bracketed portion may be entered. 
                 K[EY] can appear as K, KE, or KEY. 
  Braces and Or Bar 
                 Elements placed inside a pair of braces identify a required 
                 choice.  These are always used with the Or bar (|).  The Or 
                 bar separates the elements in a required choice. 
                 {A|id}   -   means that either the letter A or the value of 
                 id must be entered. 
  Ellipsis 
                 The horizontal ellipsis indicates that a previous bracketed 
                 element may be repeated, or that elements have been omitted. 
                 option[,option]...   -   means that one or more options may 
                 be entered, with a comma inserted between each variable. 
  Carated Letters 
                 Letters inside carats indicate the keys on a physical 
                 terminal device. 
                 <ESC> <BS>   -   means press the escape key and then the 
                 backspace key. 
                 Note that the control key (shown as <CNTL>) is similar to the 
                 shift key:  it does nothing on its own, but changes the 
                 meaning of the keys that are hit while it is depressed. 
                 <CNTL-Y>   -   means press the control key AND the Y key at 
                 the same time. 
  Keywords 
                 Keywords can be typed in uppercase or lowercase or a 
                 combination of both.  In this manual, keywords are always 
                 shown in uppercase. 
  Double Quotes 
                 Comments within command streams are denoted by being enclosed 
                 in double quotes marks ("). 
  Apostrophe 
                 Strings that contain delimiters must be enclosed by 
                 apostrophes ('); if an apostrophe is part of a string, it is 
                 denoted by adjacent apostrophes (''). 
00010
00005
00004
00001
00007
00009
00006
00008
00002
00005
00009
00003
Syntax: 
NOUS[ERS!] 
Description: 
Prevents unnecessary users from accessing the system.  This keyin can only be 
used prior to SLUG completing the five-phased system startup process. 
The NOUSERS! keyin has the same effect as answering 'N' to the AARDVARK prompt 
'DO YOU WANT USERS (Y/N).' Otherwise, the operator is informed that it is too 
late to prevent unnecessary users from system access.  This keyin is 
counteracted by submitting any "ON" type keyin. 
If this keyin is entered before the message 'LOGGING OF CONSOLE ACTIVITY 
INITIATED' is output, the keyin cannot be abbreviated and the full form 
NOUSERS! must be used. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
OCHI[ST] filename 
Description: 
Causes the :OCHIST.:SYSTAC file (KEYIN console activity file) to be closed and 
renamed to the specified file name in the :SYSTAC account.  :OCHIST will then 
be rebuilt, depending on whether HISTORY is ON or OFF. 
NOTE:  :OCHIST.:SYSTAC should not be deleted, because doing so makes it 
impossible for KEYIN to correctly restart the console history logging process, 
and also makes it impossible to REPLAY properly. 
If :OCHIST.:SYSTAC is accidentally deleted, it will be necessary to boot the 
system to get history logging started properly. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
ODUN[LOAD] FEP {fepnumber|fepname} [{serialnumber|nnnnn}] 
Description: 
Causes the specified cartridge to be moved into the OSAR input/output door so 
that it may be removed from the optical disk cabinet.  The cartridge may be 
identified by its serial number or by its cartridge identifier number.  If 
neither a cartridge serial number or identifier is specified, the system 
assumes that the cartridge is the currently blank cartridge. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
ODVOL[INIT] FEP {fepnumber|fepname} nnnnn 
Description: 
Allows the operator to write a cartridge identifier on both surfaces (A and B) 
of the currently inserted blank optical disk cartridge in the optical disk 
controller specified by fepnumber or fepname.  The cartridge identifier is a 
1-5 digit number.  The system adds to the number an A or B side suffix, as 
appropriate. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
OFF 
Description: 
Logs the operator's console off.  If this keyin is performed on the LCC, it 
ceases to function until a RETURN/RETURN sequence is typed in, which logs it 
back on.  If this keyin is performed on the SCC, it ceases to function until a 
REQUEST/EOM sequence is typed in, which logs it back on. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
ON numberofusers 
Description: 
Specifies the maximum number of users permitted to use the system.  Note that 
this number need not be the sum of the ON TS, ON GH, and ON BA numbers.  Note 
that this number cannot be set less than 13, the number of required system 
ghosts. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
ON BA numberofusers 
Description: 
Specifies the maximum number of batch users permitted to run simultaneously. 
NOTE:  The CONTROL partition parameters may prevent the maximum number of 
batch users from running.  For example, if ON BA 16 is done, and there are 
only 8 partitions open, and if PJMAX=1 for each partition, only 8 batch jobs 
will run rather than 16. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
ON GH numberofusers 
Description: 
Specifies the maximum number of ghost users permitted to run simultaneously. 
Note that this number cannot be set less than 13, the number of required 
system ghosts. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
ON TP numberofusers 
Description: 
Specifies the maximum number of transaction processing users permitted to run 
simultaneously. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
ON TS numberofusers 
Description: 
Specifies the maximum number of online (timesharing and console ghost) users 
permitted to run simultaneously. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
    Available CP-6 keyins are: 
GENERAL_CONSOLE:         ?, ??, BYE, CONSOLES, CONSOLE_STATUS, HELP, HISTORY, 
                         INFO, MSG, MYREAD, NATLANG, OCHIST, OFF, PENDING, 
                         PROFILE, READ, READ$, READACCT, TIME, TURNOVER, UC, 
                         X_CONSOLE. 
SYSTEM_CONTROL:          ACCTLG, AUTO_SCHEDULING, BATCH, CPU, CPUS, DATE, 
                         DELTA, DIE!, E, FLUSH, MAKE_CPU, NOUSERS!, ON, ON_BA, 
                         ON_GH, ON_TP, ON_TS, START_CPU, STARTUP!!, STATION, 
                         STOP_CPU, TIME, USERS, X, XDELTA, ZAP!, ZAP!!. 
SPECIAL_SYSTEM:          DELTA, DIE!, ERROR, FIRMLOAD, NOUSER!, PROCEED, 
                         RETRY. 
USER_CONTROL:            sysid:, BROADCAST, CANREAD, E, HEADER, PENDING, 
                         RERUN, SEND, SENDALL, SENDFEP, X, X_FEP. 
GENERAL_DEVICE:          DEVICES, ERROR, FIRMLOAD, PROCEED, QUIET, RETRY. 
TAPE_DRIVES:             ANSSCRATCH, CANT_MOUNT, CANT_OVER, CANT_RING, 
                         DISMOUNT, LOAD, MOUNT, OVER, REQUEST, RESERVE, RING, 
                         SCRATCH, TAPE, TAPES, UNRESERVE, VOLUME, VOLUMES. 
DISK_DRIVES:             DISK, DISMOUNT, EXCLMOUNT, PUBLIC, REQUEST, SET, 
                         SETS, SHARE, VOLUMES. 
OPTICAL_DISKS:           BOOT_FEP, CRASH_FEP, DUMP_FEP, ODUNLOAD, ODVOLINIT. 
UNIT_RECORD_DEVICES:     ABORT, ALIGN, CONTINUE, FLUSH, FORM, LOCK, MAKE, 
                         NCTL, REPRINT, SAVE, SETUP, SPACE, START, SUSPEND, 
                         SYMB_INPUT, SYMB_OUTPUT. 
QUEUE_CONTROL:           DELETE_INPUT, DELETE_INPUT_ALL, DELETE_OUTPUT, 
                         DELETE_OUTPUT_ALL, DELETE_OUTPUT_ALL_FORM, DISPLAY, 
                         PRIO_INPUT, PRIO_INPUT_ALL, PRIO_OUTPUT, RERUN, 
                         RERUN_ALL, RESTRICT, S, SWITCH_OUTPUT, UNRESTRICT. 
Insert ? for additional keyins. 
JOB_DISPLAY:             DISPLAY_ALL, DISPLAY_DEFER, DISPLAY_INPUT, 
                         DISPLAY_NORUN, DISPLAY_NSFORM, DISPLAY_OUTPUT, 
                         DISPLAY_PRIO, DISPLAY_RUNNING, DISPLAY_sysid. 
COMMUNICATIONS:          @mastername, BOOT_FEP, CRASH_FEP, DISABLE_LINES, 
                         DISCONNECT, DISCONNECT_TERMINAL, DUMP_FEP, E_FEP, 
                         ENABLE, FEPS, HEADER, HOSTS, KILL, LINKS, MASTERS, 
                         NETWORK_ROUTE, NODES, START_FEP, START_FEPS, STATION, 
                         STOP_FEP, STOP_FEPS, TELL, TELLALL, TERMINAL, 
                         TERMINALS, X_FEP. 
DIAGNOSTIC:              DIAG, ERSEND, NODIAG. 
CONSOLE_GHOST:           B:, F:, G:, GHOST, PENDING, Y:. 
INFORMATIONAL:           ?, ??, BATCH, CONSOLES, CONSOLE_STATUS, DEVICES, 
                         DISK, DISPLAY, FEPS, HELP, HOSTS, INFO, LINKS, 
                         MASTERS, NETWORK_ROUTE, NODES, PENDING, SETS, SETUP, 
                         STARTUP!!, STATION, SYMB_INPUT, SYMB_OUTPUT, TAPES, 
                         TERMINALS, USERS, VOLUMES, ZAP!!. 
MESSAGE_SENDING:         @mastername, BROADCAST, ERSEND, HEADER, MSG, SEND, 
                         SENDALL, sysid:, TELL, TELLALL. 
TRANSACTION_PROCESSING:  START_TP, TP/, ON_TP. 
COMGROUPS:               RESTRICT, ROUTE_FROM, ROUTE_INTO, SYMB_INPUT, 
                         UNROUTE. 
To obtain a brief description of keyins in a particular 
keyin group, enter: 
    HELP keyin_group 
To obtain information about a specific keyin, enter: 
    HELP keyin 
To obtain information about the console attribute 
of a specific keyin, enter: 
    HELP keyin ATTR 
To obtain the description of a specific keyin, enter: 
    HELP keyin DESC 
The following standard CP-6 keyins are used to control the operation of the 
optical disk controller Direct Interface Board (DIB):  BOOT FEP, CRASH FEP and 
DUMP FEP.  In addition, the following optical disk specific keyins are used: 
ODUNLOAD FEP    Moves an optical disk cartridge to the OSAR input/output door 
                for removing the cartridge from the optical disk cabinet. 
ODVOLINIT FEP   Allows the operator to write cartridge identifiers on optical 
                disk cartridges. 
The BOOT FEP keyin is used to reinitialize the interface between the host and 
the optical disk controller.  This keyin causes any outstanding host IO 
requests for optical disk files to be aborted, with an irrecoverable IO error 
code returned.  Open optical disk files will be closed and their volumes 
dismounted.  Note that some data may be lost from unwritten monitor buffers 
when this occurs.  No program procedure will be reloaded as a result of the 
BOOT FEP keyin. 
The CRASH FEP keyin reinitializes an optical disk controller interface and 
restarts it.  An upline dump of its contents will not be created. 
The DUMP FEP keyin disables an optical disk controller interface.  An upline 
dump of its contents will not be created. 
Syntax: 
OVER devicename 
Description: 
Permits the user associated with the unexpired ANS tape on the specified 
device to write over it. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
PEND[ING] [READ[S]] 
Description: 
Displays the outstanding M$KEYIN reads requiring a response from this console. 
This keyin will display the console ghost read size and prompt, if such read 
is active. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
PRIO I[NPUT] sysid [ TO ] priority 
Description: 
Allows the operator to change the input batch queue scheduling priority on the 
specified sysid to the specified priority.  The system manager (using SUPER) 
sets the maximum priority value allowed for an individual console. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
PRIO I[NPUT] ALL [[AT] oldpriority] [.account] [@wsnname] [TO] newpriority 
Description: 
Specifies that all waiting batch jobs that meet all of the given criteria be 
given the new priority.  If no criteria are specified, then all waiting jobs 
are to be given the new priority.  @wsnname, when specified, may only be 
specified from a SYSTEM console. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If .account and @wsnname are specified, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
PRIO O[UTPUT] .account [ @wsnname ] [ TO ] priority 
Description: 
Changes the output symbiont scheduling priority for all output files created 
by the specified account.  If the keyin is performed from a SYSTEM console, 
and the optional @wsnname is not specified, then ALL output for the selected 
account at ALL terminals is affected.  If the optional @wsnname is specified 
from a SYSTEM console, then only output at the selected terminal is affected. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If @wsnname is specified, SYSTEM INPUT. 
00002
00002
00001
Syntax: 
PRIO O[UTPUT] [ALL] [@wsnname] [TO] priority 
Description: 
Allows the operator to change the output symbiont scheduling priority for ALL 
output files at the workstation in which the issuing console resides.  If the 
issuing console is a SYSTEM console, ALL output files in the system will 
change priority.  If @wsnname is specified, the keyin allows the operator to 
change the output symbiont scheduling priority for all output files at a 
particular workstation. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If @wsnname is specified, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
PRIO O[UTPUT] sysid [-identifier] [ TO ] priority 
Description: 
Changes the output symbiont scheduling priority for the specified sysid's 
output files to the specified priority.  If the optional identifier is not 
given, all files for the specified sysid have their priority changed.  If the 
optional identifier is given, and it is a valid output symbiont sub-file 
identifier, only the specified sub-file is affected. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
PROC[EED] devicename 
Description: 
Causes the current I/O error condition on the specified device to be ignored 
and normal status to be returned to the user, in spite of the actual error. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
PROF[ILE] profilename 
Description: 
Sets the terminal profile for an FEP-connected console.  This keyin is not 
legal from IOM-connected consoles. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
PUBL[IC] packsetname 
Description: 
Mounts the specified packset as a shared packset and merges its account 
directory into the master account directory (MAD).  (See SHARE keyin). 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
PWID[TH] [=]width 
Description: 
Sets the number of printable characters per line on an IOM-connected console 
to a value in the range 72-132.  This value only applies to IOM-connected 
consoles, as FEP-connected consoles rely on the FEP for terminal handling 
(e.g., wraparound).  The system default is 132 when the system is booted, or 
comes up during recovery. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
The following keyins apply to queue control: 
DELETE INPUT            Deletes input from batch queue. 
DELETE INPUT ALL        Deletes all input from batch queue. 
DELETE OUTPUT           Deletes the output for specified sysid. 
DELETE OUTPUT ALL       Deletes all output symbiont files. 
DELETE OUTPUT ALL FORM  Deletes all output symbiont files for forms. 
DISPLAY                 Displays information about batch queues. 
PRIO INPUT              Changes input batch queue priority. 
PRIO INPUT ALL          Changes all input batch queue priorities. 
PRIO OUTPUT             Changes output batch queue priority. 
RERUN                   Aborts a specified job and reruns it. 
RERUN ALL               Performs a RERUN for all running jobs. 
RESTRICT                Restricts usage of symbiont devices. 
S                       Forces the multi-batch scheduler to schedule. 
SWITCH OUTPUT           Changes output destination for symbiont file. 
UNRESTRICT              Cancels RESTRICT keyin. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
QUIE[T] devicename 
Description: 
Requests that the error message that is printing for the specified device stop 
printing.  Note that this does not correct the error condition.  It does stop 
the message from printing once a minute.  The CP-6 system will remind the 
operator at one hour intervals that the error still exists, or the operator 
may use the DEVICES keyin to get a display of which devices are in an errored 
state. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
READ fid 
Description: 
Performs keyins from the specified file as if the operator has keyed them in 
manually.  Any syntax error terminates the entire READ.  Non-legal keyin 
attempts from a READ file will also halt the READ.  Note that the file must be 
read-accessible to KEYIN.:SYS.  Note also that the first "keyin" in the input 
file must be a READ$ keyin.  (See READ$). 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
READ$ [{LOGO[N]=console_logon_name|DEVI[CE]= [console_devnm]@station}] 
Description: 
Each READ file must begin with this keyin. 
This guarantees security on READ files.  In the case where a logon name is 
specified, the file will be restricted and can only be READ from the console 
with that logon.  When console_devnm@station is specified, the file will be 
restricted and can only be READ from that console.  If just @station is 
specified, then any console at that station may READ the file.  If just READ$ 
is specified, any console may READ that file. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
READA[CCT] {.account|RESET} 
Description: 
Changes the default global account for READ file from :SYS to the specified 
account.  The default will be changed for all consoles.  The RESET option 
changes the default read account to :SYS. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
REPR[INT] devicename [[IF] sysid] 
Description: 
Causes the specified symbiont device to print from the beginning of the output 
symbiont file.  The optional sysid, if specified, indicates that the action is 
to be taken only if the specified sysid is currently outputting. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
REQU[EST] devicename 
Description: 
This keyin is used to: 
o   physically dismount tapes 
o   physically dismount disks on MSU0451 disk drives 
o   logically dismount MSU0501 disk drives 
o   logically dismount FIPS (MSU3380 and MSU3382) disk drives 
If the requested device is a 451 disk drive, and the packset has been 
dismounted (see DISMOUNT keyin) the pack will be spun down.  If the specified 
device is a tape drive, and no user is using the tape mounted on the tape 
drive, the tape will be unloaded.  REQUEST keyins can only be performed for 
devices that have packsets or tapes physically mounted on them.  Note that a 
DISMOUNT keyin should be entered prior to a REQUEST keyin. 
This keyin is used when partitioning multi-packset 501 or FIPS drives, as 
shown in the following example: 
    DISMOUNT                      (all packsets on 501 or FIPS drives) 
    REQU DP05 
    !SYSCON 
    SYSCON E02 Here 
    >PARTITION DP05 
      Unable to partition device DP050000. 
      Device in use.  Will be partitioned when released. 
    >DI DP05 
    Component     Part   TDOK   Checkwrite 
    DP050000      Yes    No     No 
    >END 
The "Device in use" error occurs when partitioning a multi-packset 501 or FIPS 
disk device because PIG has access to the disk, but upon the partition 
request, the disk is released by PIG and then partitioned via the normal 
delayed partitioning mechanism. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
RERU[N] sysid 
Description: 
Requests that the specified job be aborted and, if RERUN was requested for 
that sysid, that the job be reinserted in the input queue.  The job is 
reinserted at a priority one unit greater than the priority it had when 
started. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
RERU[N] ALL 
Description: 
Performs a RERUN for all running batch jobs.  Jobs that cannot be rerun will 
be reported as such, and must have X keyins performed on them if they are to 
be aborted immediately. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
RESE[RVE] devicename [FOR] sysid 
Description: 
Allows the operator to make any tape mounted (currently or subsequently) on 
the specified tape drive available only to the specified sysid. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
REST[RICT] devicename [TO] {.account|@wsnname} 
Description: 
Restricts the use of the specified output symbiont device to a single account 
or workstation. 
When used with account, first, the specified device is prevented from 
processing files from any account other than the one specified.  Second, the 
specified account is prevented from being processed by any other unrestricted 
device.  This, however is more complex than it might appear at first.  It only 
applies to files from the specified account which are destined for devices of 
the same type as the one specified, and at the same TERMINAL as the one 
specified. 
When used with wsnname, a device can be restricted to a workstation.  However, 
account restrictions take precedence over workstation restrictions. 
Examples: 
The following example illustrates the use of RESTRICT with account: 
Suppose the operator @SEATTLE issues the keyin: 
    RESTRICT CP01 TO .BLOTTO 
This would not prevent files from account BLOTTO which are destined for 
LP@SEATTLE from printing, since CP and LP are different device types.  Neither 
would it prevent files from account BLOTTO which are destined for CP@BOSTON 
from punching on the punch @BOSTON. 
Furthermore, the second restriction does not apply to files which could not 
print on the specified device.  Thus, for example, if @SEATTLE has two 
printers, LP01 and LP02, where LP01 has APL character set and LP02 does not, 
then the keyin: 
    RESTRICT LP02 TO .BLOTTO 
will not prevent a file from account BLOTTO which requires APL from printing 
on LP01. 
Note that the account specification may be wild-carded.  That is, it may 
contain a leading or trailing '?'.  Specifying 'ABC?' means any account 
beginning in ABC; specifying '?ABC' means any account ending with 'ABC'. 
Devices may be identically restricted if this is desirable.  For example, if 
there is a large backlog of output from account BLOTTO, the operator may wish 
to dedicate two or more devices to that account by restricting both to 
.BLOTTO. 
The following example illustrates how account restrictions take precedence 
over workstation restrictions: 
If LP01 processes WSN @REDONDO and is restricted to .WINTON, and LP02 is 
restricted to @REDONDO, ALL output from .WINTON to an LP@REDONDO will print on 
LP01.  Conversely, if LP01 does not process WSN @HERMOSA and LP02 does, ALL 
output from .WINTON to an LP@HERMOSA will print on LP02. 
Usage Notes: 
1.  The use of this keyin does not preclude the use of other device types by 
    output from this account. 
2.  A symbiont device cannot be restricted to an account and workstation 
    simultaneously. 
3.  A symbiont device cannot be restricted to multiple workstations (see ROUTE 
    keyin). 
Console Attribute Required: 
DEVICE INPUT 
00004
00004
00001
00002
00003
Syntax: 
RETR[Y] devicename 
Description: 
Retries the currently erroring I/O for the specified device. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
RING devicename 
Description: 
Requests that the tape on the specified drive be dismounted so that the 
operator can put a write ring in it. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
ROUT[E] [NOT] [@wsnname] FROM devicetype [devicenumber[@terminalname]] 
Parameters: 
wsnname    is the name of the workstation to route from the device(s). 
devicetype    is a 2 character device type 
devicenumber    is a 2 character (numeric) device identifier 
Description: 
Routes (or inhibits) processing of a workstation by a output symbiont device 
or class of devices at a terminal name.  If no terminalname is specified, the 
terminal name of the issuing console is assumed.  If no terminal name is 
specified and the issuing console is a SYSTEM console, 'LOCAL' is assumed.  On 
a device class route, all symbiont devices known to the output symbiont 
manager (connected or not) are subject to the route provided they match the 
specified criteria.  In other words, recovery information is updated with each 
route.  Note that routing the only instance of a wsn from a device type will 
result in a *NODEV* status on all files destined for that device type and wsn. 
Console Attribute Required: 
DEVICE INPUT 
If @terminalname is specified, SYSTEM INPUT is required. 
00003
00003
00002
00001
Syntax: 
ROUT[E] @wsnname INTO devicetype [devicenumber[@terminalname]] 
Description: 
Routes (in this case adds) processing of a workstation to an output symbiont 
device or class of devices at a terminalname.  If no terminalname is 
specified, 'LOCAL' is assumed. 
Recovery information is updated for both connected and disconnected devices. 
Finally, adding the only instance of a wsn to a device type will affect the 
*NODEV* status on all files destined for that device type and workstation. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
S 
Description: 
Allows an operator at a SYSTEM console to force the multi-batch scheduler 
(MBS) to schedule.  This is useful if a batch partition definition has just 
been modified by the use of the CONTROL processor. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
SAVE devicename [[IF] sysid] [CHEC[KPOINT]] 
Description: 
Locks the device, and returns the currently outputting file to the queue for 
outputting later.  If the optional sysid is specified, that action only occurs 
if the specified sysid is outputting.  If CHECKPOINT is requested, the file 
begins outputting at the point of interruption (to the nearest page or card) 
when it next becomes eligible to output.  Note that once a file has been 
CHECKPOINTed this way, it can still be printed from the beginning by the 
REPRINT keyin. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
SCRA[TCH] devicename [FOR] sysid 
Description: 
Allows the specified user to use the tape on the specified drives as an 
unmanaged (free-form) scratch tape. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
SEND sysid [textstring] 
Description: 
Sends the specified text to the specified user's terminal. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
SENDALL [textstring] 
Description: 
Sends the textstring to ALL user's terminals and logged on consoles.  This 
keyin is legal only from a SYSTEM console.  This keyin, unlike the BROADCAST 
keyin, does not affect the "administrative message" seen in logon salutations. 
If no textstring is specified, a blank line is sent. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
SENDALL FEP {fepnumber|fepname} textstring 
Description: 
Sends a textstring to all timesharing terminals and consoles connected to the 
specified FEP. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
SET packsetname 
Description: 
Requests a status display of the specified packset. 
Console Attribute Required: 
DEVICE OUTPUT 
00002
00002
00001
Syntax: 
SETS 
Description: 
Requests a display of all currently mounted packsets. 
Console Attribute Required: 
DEVICE OUTPUT 
00002
00002
00001
Syntax: 
SETU[P] formname 
Description: 
Requests a display of how to mount the specified formname. 
Console Attribute Required: 
DEVICE OUTPUT 
00002
00002
00001
Syntax: 
SHAR[E] packsetname 
Description: 
Mounts the specified packset as a shared packset, but does not merge its 
account directory into the master account directory (MAD).  (See PUBLIC 
keyin.)  Note that if the packset has already been mounted PUBLIC (and a PIG 
MADDELETE has not been performed), that the packset's account directory will 
still exist in the MAD. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
SPAC[E] devicename spacecount [FROM {BOF|EOF|HERE}] [[IF] sysid ] [CONT[INUE]] 
Description: 
Requests that the SPACE function count output units from the beginning (BOF) 
or the end-of-file (EOF) of the output file instead of the current point in 
the output file. 
If HERE is specified (assumed if neither FROM BOF or FROM EOF is specified), 
the default requests that the output on the specified device be 
forward-skipped a certain number of output units (if the number is positive) 
or backward-skipped a certain number of output units (if the number is 
negative) from the current point in outputting.  Output units are pages on 
line printers and individual records for other devices. 
The optional sysid, if specified, indicates that the action is only taken if 
the specified sysid is currently outputting.  If CONTINUE is specified, 
automatic suspension of the device when the output file reaches EOF will not 
occur. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
    A set of special system keyins are available before the KEYIN ghost is 
    started (at boot time), or if the system is in an unknown state or the 
    system packset is in trouble.  (See Appendix E of the Operations Reference 
    Manual (CE34) for additional information.) 
    NOTE:  These keyins: 
o   Are available only on an IOM-connected console 
o   Must be input in their full form, as there are no abbreviations 
o   Must be preceded by a <CNTL-Y> character if the system has come up and 
    KEYIN is running (or has run) and the standard set of keyins is 
    unavailable. 
o   May need to be entered several times. 
The special keyins are: 
DELTA        Transfer to XDELTA, the executive debugger. 
DIE!         Crash the system. 
ERROR        Error a device's I/O. 
FIRMLOAD     Causes a firmware download. 
NOUSERS!     Prevents startup of users and remote devices. 
PROCEED      Ignore a device's I/O error. 
RETRY        Retry a device's I/O. 
An alternative way of transferring to XDELTA is to type (on the LCC) <CNTL-Y> 
<CNTL-Y> <RETURN> or (on the SCC) <ESC> <ESC> <EOM>. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
STAR[T] devicename 
Description: 
Unlocks a locked symbiont output device, and attempts to begin output if the 
device has any output queued for it.  The CONTINUE keyin can be used to 
restart SUSPENDed output. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
STARTUP!! 
Description: 
Displays the progress of a system boot. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
STAR[T] CPU portnumber 
Description: 
Instructs the CP-6 system to begin using the CPU connected to the specified 
portnumber as a secondary processor. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
STAR[T] FEP {fepnumber|fepname} 
Description: 
Allows the specified FEP to operate normally.  If the FEP was STOPped, it will 
resume running.  If it has crashed, or it is down, the FEP is rebooted.  May 
only be used with local fepnumber or fepname. 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
Syntax: 
STAR[T] FEPS 
Description: 
Performs the START FEP function for all FEPs in the system. 
Console Attribute Required: 
COMMUNICATION INPUT 
00002
00002
00001
Syntax: 
STAR[T] TP/account,tpname[,password] 
Description: 
Begins a TP instance in the specified account.  Only one instance may run in 
any account at any given time.  The first command is the one specified for 
this ghost via SUPER. 
Console Attribute Required: 
TP INPUT 
00002
00002
00001
Syntax: 
STAT[ION] 
Description: 
Allows any console to display all devices associated with its own terminal. 
This keyin is not legal from SYSTEM INPUT consoles. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
STOP CPU portnumber 
Description: 
Instructs the CP-6 system to stop using the CPU at the specified portnumber as 
a secondary processor.  This keyin will be rejected if the CPU is running in 
diagnostic mode. 
If the CPU is experiencing hardware problems, attempting to stop the CPU may 
result in an HFA-129-7 screech.  This screech is caused by the operating 
system attempting to connect to the failing CPU during the stop sequence.  The 
STOP CPU keyin may fail if the CPU is hung in such a way that it cannot 
respond to the master.  In this case, CP-6 will report that the CPU is still 
running. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
STOP FEP {fepnumber|fepname} [ textstring ] 
Description: 
Allows the operator to shut down, but not crash the specified FEP.  If the 
optional textstring is specified, it is sent to all users who are on or 
subsequently attempt to log on through that FEP.  Note that all users or IRBTs 
that are connected via the selected FEP will disconnect as if a line hangup 
has occurred.  May be used with local fepnumber or fepname, only. 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
Syntax: 
STOP FEPS [textstring] 
Description: 
Performs the STOP FEP function for all FEPs in the system. 
Console Attribute Required: 
COMMUNICATIONS INPUT 
00002
00002
00001
Syntax: 
SUSP[END] devicename [[IF] sysid ] 
Description: 
Causes the specified output symbiont device to cease output after the current 
granule is exhausted.  The current file remains 'on' the device (unlike SAVE, 
which pulls the file off the device).  Output may be continued from the point 
of suspension by use of the CONTINUE keyin.  If the optional sysid is 
specified, it indicates that suspension is only to occur if the specified 
sysid is currently outputting. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
SWIT[CH] O[UTPUT] ALL [NOT]@wsnname1 [TO] @wsnname2 
Description: 
Requests that all output symbiont files at wsnname1 be made to output at 
wsnname2. 
The NOT allows the specification of all workstations that are not named 
specifically. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If @wsnname1 is specified, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
SWIT[CH] O[UTPUT] [NOT].account [[NOT]@wsnname1] [[TO] @wsnname2 ] 
Description: 
If entered at a SYSTEM console, this keyin requests that ALL output for the 
specified account is to be switched to be output at wsnname2. 
If wsnname1 is not specified, ALL output for that account at all terminals is 
switched to wsnname2.  If wsnname1 is specified, then only output for the 
specified account at the specified wsnname1 is switched to wsnname2. 
If any output that the DEVICE INPUT console controls is for the specified 
account, then it is switched to LOCAL. 
The NOT allows the specification of all accountnames and WSNs that are not 
named specifically. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If @wsnname1 is specified, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
SWIT[CH] O[UTPUT] ALL 
Description: 
Requests that all existing output designated for devices controlled by this 
console be switched to LOCAL. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
SWIT[CH] O[UTPUT] [NOT] FORM=formname [[NOT] @wsnname1] [[TO] @wsnname2] 
Description: 
If entered at a SYSTEM console, this keyin requests that all output for the 
specified form is to be switched to be output at wsnname2. 
If @wsnname1 is not specified, all output for that account at all workstations 
is switched to wsnname2.  If @wsnname1 is specified, only output for the 
specified account at the specified wsnname1 is switched to wsnname2. 
If any output that the DEVICE INPUT console controls is for the specified 
formname, then it will be switched to LOCAL.  The NOT allows the specification 
of all formnames or workstations that are not named specifically. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If @wsnname1 or @wsnname2 is specified, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
SWIT[CH] O[UTPUT] sysid [-identifier] [[TO] @wsnname] 
Description: 
Allows the operator to change the workstation receiving an output symbiont 
file.  If the optional identifier is not given, all output for the specified 
sysid is switched.  If the identifier is specified, and it is a valid output 
symbiont sub-file identifier, only the sub-file is switched. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
If @wsnname is specified, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
SYMB I[NPUT] [devicename] [@terminalname] 
Description: 
Displays the status of the specified input symbiont device.  If the devicename 
is not given at a DEVICE console, all input symbiont device relating to this 
console are displayed.  If @terminalname is specified, then the appropriate 
devices at the specified terminal will be displayed. 
Console Attribute Required: 
DEVICE OUTPUT 
If @terminalname is specified, SYSTEM OUTPUT is required. 
00002
00002
00001
Syntax: 
SYMB O[UTPUT] [devicename] [@terminalname] [WSN|THROTTLE] 
Description: 
Displays the status of the specified output symbiont device.  If the 
devicename is not given, all output symbiont devices relating to this console 
are displayed.  If @terminalname is specified, the appropriate device(s) at 
the specified terminal are displayed.  If the WSN option is specified, a list 
of workstation names currently associated with the device(s) is also 
displayed.  If the THROTTLE option is specified, the number of times and the 
amount of time the symbiont output line has been throttled is displayed. 
Console Attribute Required: 
DEVICE OUTPUT 
If @terminal name is specified, SYSTEM OUTPUT is required. 
00002
00002
00001
NOTATION_CONVENTIONS
Syntax: 
sysid: [textstring] 
Description: 
Replies to a solicited request for operator response, via the M$KEYIN service. 
The sysid must match the sysid of the user requesting the response. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
    The following are system control keyins: 
    ACCTLG           Renames accounting log file. 
    AUTO SCHEDULING  Sets automatic scheduling by GOOSE. 
    BATCH            Controls entry to batch queue, or display batch job 
                     status. 
    CPU              Displays status of CPU by portnumber. 
    CPUS             Displays status of all processor CPUs in the system. 
    DATE             Gives the CP-6 system the current date. 
    DELTA            Associates XDELTA with the system. 
    DIE!             Initiates recovery sequence. 
    E                Errors job step for specified users. 
    FLUSH            Flushes the input stream. 
    MAKE CPU         Turns a slave CPU into a master CPU. 
    NOUSERS!         Prevents startup of users and remote devices. 
    ON               Specifies maximum number of users. 
    ON BA            Specifies maximum number of batch users. 
    ON GH            Specifies maximum number of ghost users. 
    ON TP            Specifies maximum number of TP users. 
    ON TS            Specifies maximum number of on-line (time-sharing) users. 
    START CPU        Begins usage of secondary labeled central processing 
                     unit. 
    STARTUP!!        Displays the progress of a system boot. 
    STATION          Displays all devices associated with a console. 
    STOP CPU         Ends usage of secondary labeled central processing unit. 
    TIME             Gives the CP-6 system the current time. 
    USERS            Displays maximum allowed number of users. 
    X                Aborts specified user. 
    X FEP            Aborts a specified sysid within a named FEP. 
    XDELTA           Transfers control to the executive debugger. 
    ZAP!             Causes orderly system shutdown. 
    ZAP!!            Displays the current progress of the ZAP! procedure. 
    To obtain more information about a keyin, enter: 
        HELP keyin 
    To obtain the console attribute for a specific 
    keyin, enter: 
        HELP keyin ATTR 
Syntax: 
TAPE|TAPES devicename 
Description: 
Displays the usage of all tape drives controlled by this console.  If 
devicename is specified, then only the usage of the specified drive will be 
displayed. 
Console Attribute Required: 
DEVICE OUTPUT 
00002
00002
00001
The following keyins apply to tape drives: 
ANSSCRATCH  Authorizes use of an ANS scratch tape. 
CANT MOUNT  Aborts a requested tape mount. 
CANT OVER   Aborts a requested tape mount that requested an OVER keyin. 
CANT RING   Aborts a requested tape mount with RING. 
LOAD        Requests an automatic start sequence. 
MOUNT       Specifies or changes serial numbered mounted tape. 
OVER        Permits a unexpired ANS tape to be overwritten. 
REQUEST     Dismounts a tape if no user is associated. 
RESERVE     Reserves a tape to be used by a specified sysid. 
RING        Dismounts tape so that a write ring can be inserted. 
SCRATCH     Allows use of an unmanaged tape. 
TAPE        Displays usage of a tape drive. 
TAPES       Displays usage of all tape devices. 
UNRESERVE   Cancels a RESERVE keyin. 
VOLUME      Displays usage of mounted tape volume. 
VOLUMES     Displays usage of all mounted tape volumes. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
TELL {OCnn|SCnn} [@terminalname] textstring 
Description: 
Sends the specified textstring to the specified operator's console.  The OCnn 
and terminal name may be obtained from the CONS[OLES] keyin.  If terminalname 
is not specified, the terminal name of the originating console will be used. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
TELLALL textstring 
Description: 
Sends the specified textstring to all active operator's consoles.  The keyin 
is legal only from a SYSTEM console. 
Console Attribute Required: 
SYSTEM 
00002
00002
00001
Syntax: 
TERM[INAL] @stationname [F[ULL]] 
Description: 
Allows a SYSTEM or COMMUNICATION console to display devices which were 
connected at the same time as the specified station.  If FULL is specified, 
any device associated with the station is displayed. 
Console Attribute Required: 
COMMUNICATIONS OUTPUT 
00002
00002
00001
Syntax: 
TERM[INALS] 
Description: 
Allows a SYSTEM or COMMUNICATION console to display all 
communications-connected terminals and devices. 
Console Attribute Required: 
COMMUNICATIONS OUTPUT 
00002
00002
00001
Syntax: 
TERM[INALS] ON comgroup_fid 
Description: 
Requests a display of all the devices connected to the specified comgroup. 
Console Attribute Required: 
COMMUNICATIONS OUTPUT 
00002
00002
00001
Syntax: 
TIME hh:mm 
Description: 
Allows an operator at a SYSTEM console to input the current time to the CP-6 
system.  Often used in conjunction with the DATE keyin. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
TIME {ON|OFF} 
Description: 
If ON is specified, this keyin requests that the time be printed on this 
console if any activity has occurred in the last minute, and on the hour 
regardless of the activity.  If OFF is specified, requests that time printing 
activity be suppressed.  This can be useful if the console is a master console 
for a computer which prints the time itself.  The default is to print the 
time.  This keyin only affects time printing on the issuing console. 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
TP/tpinstance command 
Description: 
Sends a valid TP command to the specified instance of TP.  If the specified 
instance is not running, a message will display indicating the fact. 
Console Attribute Required: 
TP INPUT 
00002
00002
00001
Syntax: 
TPHE[ADER] [TP]/instance_name [ message ] 
Description: 
Changes the message sent when a user logs on to the specified instance of TP. 
If the specified instance is not currently defined (via CONTROL), a message is 
displayed indicating that fact.  If no message specified, the current message 
is deleted.  The maximum length of the message is 80 characters. 
Console Attribute Required: 
TP INPUT 
00002
00002
00001
The following keyins apply to transaction processing: 
ON TP     Specifies the maximum number of TP users. 
START TP  Invokes an instance of TP. 
TP/       Sends a valid TP command to the specified TP instance. 
TPHEADER  Specifies a message to be sent to a user at logon to a TP 
          instance. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific keyin, enter: 
    HELP keyin ATTR 
Syntax: 
[DONT] TURN[OVER] {ACCTLG|OCHIST|ALL} 
Description: 
Closes the current account logging file (:ACCTLG) or the current console 
history file (:OCHIST) or both (ALL) and opens a new file (or files) at 23:59 
each day.  The account logging files will be named :ACCTLGyymmdd, where yymmdd 
is the current date.  The history file will be named :OCHISTyymmdd.  If DONT 
is specified, the corresponding file(s) will not be closed at midnight, as is 
the default. 
NOTE:  :OCHIST.:SYSTAC should not be deleted, because doing so makes it 
impossible for KEYIN to correctly restart the console history logging process, 
and also makes it impossible to REPLAY properly. 
If :OCHIST.:SYSTAC is accidentally deleted, it will be necessary to boot the 
system to get history logging started properly. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
UC {ON|OFF} 
Description: 
Requests that all lower case characters input at this console be interpreted 
as upper case.  This command also activates a "backspace edit mode" that is 
especially useful on the IOM connected console.  This is the default on system 
start-ups for IOM-connected consoles.  If OFF is specified, requests that 
upper case interpretation and backspace edit mode be discontinued for this 
console.  UC OFF is the default for FEP-connected consoles. 
Console Attribute Required: 
ANY 
00002
00002
00001
The following keyins apply to unit record equipment: 
ABORT       Aborts current output. 
ALIGN       Initiates alignment sequence. 
CONTINUE    Resumes suspended output. 
FLUSH       Flushes the input stream. 
FORM        Mounts a logical form. 
LOCK        Suspends output after current output is finished. 
MAKE        Logically makes a device a resource. 
NCTL        Changes default NCTL fid for an input device. 
REPRINT     Reprints the current output from the keyin. 
SAVE        Locks device and returns current output. 
SETUP       Requests information about a formname. 
SPACE       Causes forward or backward skipping. 
START       Removes LOCK and resumes output. 
SUSPEND     Suspends output after current granule. 
SYMB INPUT  Displays status of symbiont input device. 
SYMB OUTPUT Displays status of symbiont output device. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
UNRE[SERVE] devicename 
Description: 
Cancels the previous RESERVE keyin for this device. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
UNREST[RICT] devicename 
Description: 
Cancels the effect of the RESTRICT keyin, freeing the specified device from 
being limited to use by a single account or workstation. 
Console Attribute Required: 
DEVICE INPUT 
00002
00002
00001
Syntax: 
UNRO[UTE] [NOT] [@wsnname] FROM devicetype [devicenumber[@terminalname]] 
Description: 
Removes route wsn restrictions (ROUTE FROMs) and route wsn additions (ROUTE 
INTOs) on devices.  If no terminal name is specified, the issuing consoles 
terminalname is assumed.  If no terminalname is specified and the issuing 
console is a system console, 'LOCAL' is assumed. 
Recovery information is updated for both connected and disconnected devices. 
Finally, note that issuance of an UNROUTE keyin can send files into the 
*NODEV* state if there is no longer a type-wsn combination available that 
matches certain file destinations. 
Console Attribute Required: 
DEVICE INPUT 
If @terminalname is specified, SYSTEM INPUT is required. 
00002
00002
00001
Syntax: 
USER[S] 
Description: 
Displays the allowed number of users in all modes and the current number of 
users in all modes.  The allowed figures may be modified by use of the ON 
keyin. 
Console Attribute Required: 
ADMINISTRATIVE OUTPUT 
00002
00002
00001
The following are user control keyins: 
sysid:      Replies to M$KEYIN. 
BROADCAST   Sends a message to user terminals and assigns a 
            logon header. 
CANREAD     Cancels current 'READ' file for the console. 
E           Errors a job step for a specified user. 
HEADER      Sets a message to be printed with the logon banner. 
PENDING     Displays the outstanding M$KEYIN reads requiring a 
            response from this console. 
RERUN       Requests a specified job be aborted and that this job be 
            reinstated in the input queue. 
SEND        Sends a message to an individual user terminal. 
SENDALL     Like BROADCAST, but does not change logon message. 
SENDFEP     Sends a message to all active stations on the specified FEP. 
X           Aborts a user. 
To obtain more information about a keyin, enter: 
    HELP keyin 
To obtain the console attribute for a specific 
keyin, enter: 
    HELP keyin ATTR 
Syntax: 
VOLU[MES]|VOLU[ME] devicename 
Description: 
Displays the mounted tape volumes for all tape drives controlled by this 
console.  If devicename is specified, the mounted volume for the specified 
tape or disk drive will be displayed. 
Console Attribute Required: 
DEVICE OUTPUT 
00002
00002
00001
X_KEYIN
Syntax: 
XDELTA 
Description: 
Transfers control of the system to the executive debugger.  Same as the DELTA 
keyin. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
X CONS[OLE] OCnn [@terminalname] 
Description: 
Allows a SYSTEM console to abort any other non-SYSTEM console.  SYSTEM 
consoles may only be aborted from the IOM-connected console.  No console is 
allowed to abort the IOM-connected console.  If @terminalname is not 
specified, the terminal name of the originating console will be used. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
X FEP n-sysid 
Parameters: 
n    is a fepnumber or fepname. 
Description: 
Aborts the specified sysid with the named FEP. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00003
00003
00002
00001
Syntax: 
X sysid 
Description: 
Aborts the user with the specified sysid. 
Console Attribute Required: 
ADMINISTRATIVE INPUT 
00002
00002
00001
Syntax: 
Y: 
Description: 
Performs the "CONTROL-Y" function on the console ghost associated with this 
console (if any). 
Console Attribute Required: 
ANY 
00002
00002
00001
Syntax: 
ZAP! [textstring] 
Description: 
Initiates an orderly shutdown of a CP-6 system.  This process may take as much 
as five minutes if many users need to be aborted.  The optional textstring, 
when specified, is used like the textstring in the STOP FEPS keyin.  After 
this keyin is performed, all batch, online, and non-system ghosts will be 
aborted, the packsets will be dismounted, and the FEPs will be stopped.  A 
tape or disk boot will be required to restore the CP-6 system to life. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
Syntax: 
ZAP!! 
Description: 
Displays the current progress of the ZAP procedure (initiated via ZAP!).  A 
system ZAP is divided into the following phases: 
1.  Execute a RERUNALL operation, "X" the users and stop the FEPs. 
2.  Dismount all but the SYS packset. 
3.  "X" remaining users (those who specified NRERUN, or those who are 
    autosaved). 
4.  Send messages to OUTSYM, INSYM, DOG, and PRESCAN informing them to close 
    all files. 
5.  Close the ERRLOG (ELF). 
6.  Close the ACCTLG (SLUG). 
7.  Screech. 
Console Attribute Required: 
SYSTEM INPUT 
00002
00002
00001
