The ANLZ processor gives CP-6 support personnel access to formatted displays
and dumps of both user context and monitor context of a CP-6 system.  ANLZ may
be used to look at either a running CP-6 system or the dump file produced by a
screech, single user abort or system snapshot dump.
For further information, type:
HELP (ANLZ) HOST_COMMANDS  For a summary description of ANLZ
                           host commands.
HELP (ANLZ) FEP_COMMANDS   For a summary description of ANLZ
                           FEP commands.
HELP (ANLZ) GEN_COMMANDS   For a summary description of ANLZ
                           general commands.
HELP (ANLZ) COMMAND_SUM    For a complete list of ANLZ
                           commands by category.
HELP (ANLZ) TOPICS         For a list of ANLZ HELP topics
HELP (ANLZ) command        For a command format.  Then type
                           ? or ?? for more information.
HELP (ANLZ) command PARA   For information on parameters
                           for a command.
HELP (ANLZ) command DESC   For description of a command.
  **************************************************************
  *   Copyright, (c) Bull HN Information Systems Inc., 1998
  **************************************************************
DO
TEXT
TEXT
Format:
ACC[RES]
Description:
This command displays the contents of the user account resource table.
00001
Format:
ADD [display_opts]
Parameters:
display_opts    are one or more of the following channel context display
options separated by commas:
  Option      Display Requested
CHT         Display channel tables
ERD         Display extended real device
FLD         Display field tables (forms)
INP         Display input buffers
LCT         Display LCT bytes
MRD         Display master real device
MVD         Display master virtual device
OPT         Display output buffers
PST         Display position information
RCR         Display record buffers (SE)
SRD         Display subordinate real device
SSN         Display session context
STR         Display GV$STR
TRC         Display trace buffers
TYP         Display type-ahead buffers
USR         Display user (handler) context
VDI         Display GV$VDI
Description:
The ADD command specifies which portions of context for a channel are to be
displayed.  The ADD command turns a display flag on.  When ANLZ is invoked,
the CHT display flag is turned off, and all the remaining display flags (i.e.,
the LCT, OTP, PST, RCV, SSN, STR, TYP, and VDI flags (see HELP (ANLZ)
PARAMETERS)) are turned on.  The ADD command with no parameters is equivalent
to "ADD LCT,OTP,PST,RCU,SSN,STR,TYP,VDI".
Example:
nodename -ADD CHT
nodename -ADD LCT,OTP
nodename -ADD OTP
00002
00003
00001
The displays produced by ANLZ commands are all implemented using the X$FORMAT
HOST library services.  Some of them are implemented by using CRAWDAD.X to
create appropriate format string records in the ANLZ data file named
:FORMAT.:SYS.  Readers unfamiliar with the concept of format strings should
consult the CP-6 Host Library Services Reference Manual (CE71) section
concerning XUF services, and the Help for CRAWDAD.X before proceeding with
this appendix.
For those commands implemented via CRAWDAD.X, ANLZ searches for the required
format string first through the M$FMT DCB, which defaults to :FORMAT in the
directory account, and then through M$FMTSYS, which defaults to :FORMAT.:SYS.
As a result, even users without permission to modify :FORMAT.:SYS are able to
modify the displays produced by those commands.  More importantly, users can
add new commands to ANLZ simply by creating a format string with CRAWDAD.X, to
be invoked via the "backslash" command.
Format:
AN[LZ] [dumpfile[,symbolfile]]
Parameters:
dumpfile    is one of the following:
    fid    identifies the dump file to be examined.  The fid value may be the
    full name of a dump file, the three digit sequence number of a dump file
    in :SYSTAC, or the four character boot id and sequence number of a dump
    file in :SYSTAC.  If the three digit sequence number or the four character
    boot id is specified, and the dump does not exist in :SYSTAC, the :SYSTAC2
    account is searched.
    LAST    examines the last dump file created on the system.
    NEXT    examines the dump following the one currently open.
    PREV    examines the dump previous to the one currently open.
    RUNNING    examines the running system.  The default is RUNNING.
    @    continues examining in the same place when a new symbol file is
    selected (running system or dump file).
symbolfile    is the name of the run unit to use for ENTDEF/SYMDEF searches.
If no symbolfile is specified, ANLZ uses M:MON.:SYS if looking at the host,
and M:FEP.:SYS if looking at a FEP.  If symbolfile is specified, the named
file is used regardless of whether ANLZ is looking at the host or a FEP.
Description:
The ANLZ command is used to select a dump file or the running system, as well
as to invoke the processor (see INVOKING_ANLZ).  This command may be preceded
but not followed by other commands on the same line.
Examples:
nodename -ANLZ LAST
nodename -AN :DFE02A777.:SYSTAC
nodename -AN A777
nodename -ANLZ RUN
00002
00003
00001
Format:
ASR [location ]
    [*location]
Parameters:
location    sets ASR to frame from location to the end of the segment.
location is an address expression.
*location    sets ASR to the contents of location and location+1.  location is
an address expression.
If no parameter is given, the current ASR is displayed.
Description:
This command sets the Argument Stack Register to use during address resolution
when specifying a location as $ASn.
Examples:
nodename -ASR USERHJIT$->.1600
nodename -ASR
00002
00003
00001
Format:
AUT[O] location [{FOR  } {sysid   }[,domain]] [[WITH] A[SCII]] ['title']
                [{USING} {.usernum}         ]
Parameters:
location    is an address expression.
FOR    means use monitor linkage segment.
USING    means use user linkage segment.
sysid    is a decimal number.
 .usernum    is an octal number.
domain    is ASL, MON, ICP, IDB, or USR.  domain overrides FOR or USING.
WITH ASCII    includes the ASCII representation of the characters to the
right.
'title'    specifies the title text that is to be placed in the page header
and table of contents.
Description:
This command produces an octal dump of the specified segment of memory with
each auto frame separated out and addressed relative to zero.  In addition,
the history registers are formatted if a fault handler frame is encountered.
Examples:
nodename -AUTO $LS16 FOR CUN
00002
00003
00001
The format of the "backslash" command is:
    \ format_string_name [location [,location] ...
                                 [{F/OR|U/SING} userid [,domain]]]
where
format_string_name    is the name as specified to CRAWDAD.X when creating
format string.
location    is any address expression, usually used to specify the location of
the data to be formatted.  For example, in the \K$ICQ command described in
this section, the first "location" specifies the circular-queue segment
containing the messages to be formatted, and the second "location" is used to
specify the number of messages to display.
userid,domain    qualifies "location" as needed, as in the DUMP command.
The "backslash" command is valid in both Host and FEP modes.  Its effect is
entirely dependent on the contents of the referenced format string.
The simplest sort of "backslash" command would be one that asks ANLZ to access
some words at a location specified in the command, and displays those words in
some format available through X$FORMAT.  For example, a command called ARRAY
that displays eight words of memory as decimal numbers in eight columns each
could be created by compiling the following source file into :FORMAT with
CRAWDAD.X:
ARRAY                                     /* give the Format string a name */
     /8                       /* tell ANLZ how many words of memory to get */
     ='%8('                             /* tell X$FORMAT to repeat 8 times */
      '%8D'         /* tell X$FORMAT to display a word as 8-column decimal */
      '%)'                                          /* end of repeat group */
     ;                                  /* end of Format string definition */
Of course, the definition could easily have been represented on one line, if
the commentary were omitted, as:
    ARRAY/8='%8(%8D%)';
However, it turns out to be not quite that simple, because more complicated
commands need a more interesting environment than was assumed here.  It was
assumed here that X$FORMAT would be called with exactly eight words of memory
framed by a single data vector.  Instead, ANLZ calls X$FORMAT with three data
vectors, the second of which frames the expected eight words of memory.  The
CRAWDAD source that would work properly needs to position to the actual data,
and then quit after displaying eight values:
    ARRAY/8='%2P%8(%8D%)%IQ';
The maximum length of a format string that can be used in a "backslash"
command is 4096 characters.  This does not include commentary, blank space, or
pre-processor identifiers, which are removed by CRAWDAD.X.  If longer format
strings are required, they need to be chained together, using EDIT ROUTINE
Service (1) or Service (5).
Format:
BAN[NER]
Description:
This command writes the block print banner for crash dumps which contains the
dumpfile name, screech code, and time of the screech.
00001
Format:
BOB[CAT]
Description:
The BOBCAT command produces a formatted display of the base of the LCP6
monitor BOBCAT data segment.  The BOBCAT data contains LCP6 control parameters
and pointers.
00001
Format:
CFU[S] [optionlist]
Parameters:
optionlist    specifies one or more of the following options separated by
commas:
Option                 Description
DPnn                   Display volume CFUs for specified disk device.
DP#set                 Display packset CFUs.  May be wildcarded.
[DP#set].acct          Display account CFUs.
[DP#set/]fname[.acct]  Display CFUs for file.  Filename may be
                       wildcarded and may be followed by one of the
                       modifiers L[ONG] or F[DAS].  If LONG is specified,
                       multiple lines are displayed for each file CFU.
                       If FDAS is specified, both inactive and active
                       file CFUs are displayed.  If FDAS is omitted,
                       only active CFUs are displayed.
SERIAL#                Display all serial number CFUs.
UNALLOCATED            Display all unallocated CFUs.
Description:
This command produces formatted displays of current File Usage Tables.
Examples:
nodename -CFUS MYFILE.MYACCT
nodename -CFUS DP#PACK
nodename -CFUS FILE.ACCT LONG
00002
00003
00001
Format:
CG [cgid]
Parameters:
This command either requests comgroup displays or sets the current comgroup.
If cgid is not specified, this command produces the CGS, DATA CACHE, MMD,
GARB, and QUEUE displays for the current comgroup.
'cgid' is specified to set the current comgroup prior to entering other
commands.  This form of the command does not produce any display.  If a fid is
specified for cgid without an account, the account defaults to :SYS.
Examples:
nodename -CG .22726
nodename -CG
00002
00001
Format:
CGL[OG]
Description:
This command displays the comgroup history log.  If logging is not currently
enabled, nothing is displayed.
00001
Format:
CGMS[UMMARY]
Description:
This command displays the amount of memory that each open comgroup on the
system is using, is capable of using, and the amount of memory necessary for
the proper functioning of the comgroup.  Based on this information, the
administrator can determine if MON CGMAP in the TIGR deck needs to be
modified.
00001
CGSUMMARY
Format:
CGST[ATS] [FOR cgid]
Parameters:
cgid    specifies either a fid or an octal number that is the word offset of
the desired comgroup's context block from the beginning of the comgroup
context area (B$CGCTXT$).  This value appears in the CTXT @ column of the
CGSUMMARY display.
Description:
This command displays various statistics related to the specified comgroup,
including the number of words of memory reserved for the comgroup that are
free and in use.
If no comgroup identifier is specified, statistics for the current comgroup
are displayed.
00002
00001
Format:
CGS[UMMARY]
Description:
This command displays summary information for each open comgroup.
00001
Format:
CHANNELS [chan_select]
Parameters:
chan_select    is one of the following:
    Option             Description
    ALL                All channels
    ATTR=number        Channels with the specified attributes
    BUSY               Channels currently in use
    RES=dd             Channels with the specified resource type
    SYSID=number       Channels belonging to the specified handler
Description:
This command displays the channel id and channel type of each of the
configured channels on a FEP.  Channels subordinate to another channel are
indicated by indenting the display.
If chan_select is omitted, all channels are listed.
00002
00001
Format:
CHN[TBL] {.channelnum[-subnum[-subsubnum]]} [FULL]
         {@location [FOR userid]          }
Parameters:
 .channelnum    is a hexadecimal number that is the address of the physical
channel whose channel table is to be displayed.  The period preceding the
hexadecimal value is required.
-subnum    is a decimal number that represents the second level (i.e., the
first subordinate level).
-subsubnum    is a decimal number that represents the third level (i.e., the
second subordinate level.
FULL    specifies that all subordinate channel table entries are to be
displayed also.
@location    is an address expression that specifies a starting memory
location at which to begin formatting data for display as a channel table
entry.
userid    is either a hexadecimal user number preceded by a period, a decimal
sysid, or CUN.  CUN requests a memory dump of the current user at the time of
a screech.
Description:
The CHNTBL command produces a formatted display of one or more channel table
entries.  A channel table can be identified by its channel specification or
starting location.  If a channel is identified by its channel specification,
the keyword FULL can be appended to the command which will cause a display of
the specified channel table as well as subordinate channel table entries.
Examples:
nodename -CHN .4E00 FULL
nodename -CHN .5B00-1-3
nodename -CHN @.C0432
00002
00003
00001
COMMAND_SUMMARY
ANLZ commands are divided into three categories: host, FEP and general
commands.  For a brief description of commands by category, enter:
HELP (ANLZ) HOST_COMMANDS
HELP (ANLZ) FEP_COMMANDS
HELP (ANLZ) GENERAL_COMMANDS
For a list of all commands by category, enter: ?.
Command      Mode        Command      Mode        Command      Mode
{:|>} text   Host        EVBUF        Host        RAT          Host
ACCRES       FEP         EXIT         General     RCQ          FEP
ADD          FEP         FEI          Host        READ         General
ANLZ         General     FMT          FEP         RECOVERY     FEP
ASR          Host        \FO_DET      Host        RECOVERY     Host
AUTO         Host        GARB         Host        REPEAT       General
BANNER       Host        GATE         Host        ROS          FEP
BOBCAT       FEP         GODELTA      Host        RESOLVE      Host
CFUS         Host        HELP         General     ROUTE        FEP
CG           Host        HISTREG      Host        ROUTE        Host
CGLOG        Host        HMI          FEP         RUE          FEP
CGMSUMMARY   Host        INTCON       FEP         RUE          Host
CGSTATS      Host        IOCACHE      Host        RVBUFF       Host
CGSUMMARY    Host        IOP          FEP         SCHED        Host
CHANNELS     FEP         IOPCHECK     FEP         SCQ          FEP
CHNTBL       FEP         IOQ          Host        SCTX         Host
CONTENTS     General     ISA          FEP         SELECT       General
CPU          Host        JIT          FEP         SFILES       FEP
CPUS         Host        JIT          Host        SPROC        Host
DATACACHE    Host        \K$ICQ       Host        SPY          FEP
DATE         General     \K$OCQ       Host        SPY          Host
DCBS         FEP         \K$RCQ       FEP         SQH          Host
DCBS         Host        \K$SCQ       FEP         SSFRAME      Host
DCT          Host        \KN$TCTX     FEP         SSN          FEP
DDT          Host        LCT          FEP         SSNCHECK     FEP
DELETE       General     LDCT         FEP         STAR         General
DELTA        Host        LDCT         Host        STATUS       FEP
DFRBLKS      Host        LDCTCHECK    FEP         STREE        Host
DIRECTORY    General     LIST         General     SYMBOLS      General
DO           General     LLIST        FEP         TCB          FEP
DOMAIN       Host        LLIST        Host        TCB          Host
DQH          Host        MAP          FEP         TCTX         FEP
DROP         FEP         MEMORY       FEP         TCTX         Host
DTREE        Host        MLCP         FEP         TCTXCHECK    FEP
DUMP         FEP         MLH          Host        TIME         General
DUMP         Host        MMD          Host        TRAPFRAME    General
ECCB         FEP         MPDUMP       Host        \TREE        Host
ECHO         General     MSGLIST      Host        TSA          FEP
END          General     OUTPUT       General     TTREE        Host
ENTER        General     PLUGH        FEP         UNDELTA      Host
ENQALL       Host        PPUT         FEP         USRTABLES    FEP
ENQUEUE      Host        PRINT        General     USRTABLES    Host
ERASE        General     PSR          Host        WAIT         General
ERROR        General     QTREE        Host        WHO HAS      Host
EVALUATE     General     QUEUE        Host        XEQ          General
EVBUF        FEP         QUIT         General
00001
Format:
CON[TENTS]
Description:
This command displays the table of contents for all displays produced since
the ANLZ session began or since the last CONTENTS command.  The table of
contents is not maintained if output is to a UC device or a destination that
does not have page numbering.
00001
Format:
CPU number
Parameters:
number    specifies a logical CPU number.
Description:
This command selects which CPU is to be examined on a multi-processing system.
00002
00001
Format:
CPUS
Description:
This command displays the logical CPU number, port number, and state of each
CPU configured in the system.
00001
The buffers framed by the three data vectors passed to X$FORMAT consist of one
buffer containing control information and two buffers for accessing the data
used to create the display.  The first word of the control information buffer,
which can be positioned to in the format string via '%1P', contains the
pointer most recently used to access data for a data buffer, either in an
edit-routine service, or in the initial startup of the format string.  If the
size specified to CRAWDAD for the format string is zero, this pointer is not
actually used to access data at initial startup, but its value does reflect
the location specified in the "backslash" command, or provided in the LIFO
stack in a FMT command.
The second word of the control buffer ('%1.1P') indicates to the format string
whether ANLZ is performing a FMT command or a "backslash" command.  For a FMT
command, bit-zero is set, and the remaining 35 bits represent the channel
identification (e.g., E680-1-17).  Bits 1 through 9 contain the first nine
bits of the channel number (the other seven are always zero).  Bit 10 is set
if there is a sub-channel number in bits 11 through 22, and bit 23 is set if
there is a sub-sub-channel number in bits 24 through 35.  For a "backslash"
command, the second word of the control buffer contains the number of location
values that were specified in the command.
The third word of the control buffer ('%1.2P') contains a bitmap of FMT
command options when a FMT command is being performed.  This word controls the
operation of the edit routine service (5).  For a "backslash" command, all the
bits of this word are set.
The remaining words of the control buffer are significant only for a
"backslash" command, and contain all of the "location" pointers specified in
the command except the first one.  The n-th pointer is in word n+1 of the
buffer.
The first and second data buffers can be positioned to in a format string via
'%2P' and '%3P', respectively.  The current position of the format string in
the buffers determines which buffer is to be affected by the edit routine
services.  The first data buffer is affected if the position is in the control
buffer or the first data buffer, and the second one is affected if the
position is there.  The first buffer initially contains the data framed by the
location specified in a "backslash" command (or implicitly in a FMT command)
and the size specified in the definition of the Format string to CRAWDAD.X.
The second buffer initially contains the "base" (level one) channel table
entry in a FMT command, and is initially unused in a "backslash" command.  The
maximum data size that may be specified, either via CRAWDAD.X or via an edit
routine service, is 1024 words.  For the second buffer, the maximum size in a
FMT command is 32 words, and in FEP mode is 512 words.  In FEP mode, if the
second buffer is used, it occupies the second half of the 1024-word buffer
available for the first buffer, so using the second buffer limits the useful
size of either buffer to 512 words.  In Host mode, if the size is specified as
one word, ANLZ will try to frame the entire segment requested (e.g., the TIGR
data segment).
Format:
DATA [CACHE] [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays information about operation of and memory use by the
current comgroup's data cache.
00002
00001
Service (2) is usually used to adjust the amount of memory framed by the data
vector when the data itself defines its size.  The CNT(1) parameter specifies
the new size for the data, in words.  CNT(2), if non-zero, specifies a new
location for the data.
Service (3) is usually used to display a chain of similar items, and as such
can change the location of the data but not its size.  CNT(1) specifies the
new location.  CNT(2) specifies the SYSID, if greater than zero, or minus the
user number, if less than zero, of the user in which to find the data.  If
given, CNT(3) specifies a new domain from which to find data.  Domain EQUs can
be found in B_STRINGS_C.
Service (4) is the same as (3), except that the text parameter is used to
replace the current format string with the one named by the parameter.  If
CNT(1) is zero, the data framed by the data vectors is unchanged.  Otherwise,
if it is non-zero, the size specified in the new format string determines the
amount of memory to access at the new location.
Services (10),(11), and (12) are the same as (2),(3), and (4), respectively,
except that for the Host, the location parameter is always presumed to be a
pointer, even if its decimal value does not exceed 262143.  For services
(2),(3), and (4), a location parameter for the Host that does not exceed
262143 (a half-word) is presumed to be a new word-offset into the same segment
used for the previous data.
Format:
{DATE|TIME}
Description:
DATE (and its synonym TIME) displays the current date and time.  The format of
the display is:
mmm dd 'yy hh:mm   (month)(day)(year)(hours)(minutes)
Examples:
nodename -DATE
requests a display of the current date and time.  A sample display is:
AUG 02  '90  11:03
00001
00002
DATA_CACHE
Format:
DCB[S][,JIT][,TCB] [uselect_list]
Parameters:
uselect_list    specifies user selection criteria, separated by commas.  For a
list of options type HELP (ANLZ) USELECT.  The default is all users.
JIT    performs the JIT command for selected users.
TCB    performs the TCB command for selected users.
Description:
This command produces a formatted display of the selected users' Data Control
Blocks.
Examples:
nodename -DCBS NAME=SLUG
00002
00003
00001
Format:
DCB[S] [useridlist]
Parameters:
useridlist    is one or more userids separated by commas.  Each userid is
either a hexadecimal user number preceded by a period, a decimal sysid, or
CUN.  CUN requests the DCBs of the current user at the time of a screech.
Description:
This command produces a formatted display of the selected user(s) Data Control
Blocks.  If useridlist is omitted, all users DCBs are displayed.
00002
00001
DCBS
DCBS_FEP
Format:
DCT [optionlist]
Parameters:
optionlist    specifies any of the following options separated by commas:
  Option      Description
name        First four characters of device name (may be wildcarded).
number      DCT index.
Description:
This command produces a formatted display of selected device control tables.
If no DCT indices are specified, then the device control tables for all local
devices are displayed.
Device control table item headers are as follows:
  Header         Description
DCTADDR        Pointer to this DCT.
DCTX           DCT index.
DFLG           Device flags.
FL             DCT index of DCT pointed to by DCT.FL$.
I-CCC-DD       IOM, channel and device number of last connect
               on this device.
MSG            Whether operator message is outstanding on this device.
PART           Whether device is partitioned.
SQ             Word address portion of DCT.SQ$.
STATE          Current device state.
TDU            User number of current T & D user.
TND            Current T & D function.
Examples:
nodename -DCT DP01,MT?
nodename -DCT 7
00002
00003
00001
Format:
DDT
Description:
This command displays device dependent tables.  These are tables of
information that tape file management keeps regarding tape devices.
00001
Format:
DELETE
Description:
This command deletes the current dump file.
00001
Format:
DELT[A]
Description:
This command associates ANLZ DELTA.  ANLZ continues reading commands.  Any
command beginning with a : or > is to be passed to DELTA.  For further
information type HELP (DELTA).
00001
Format:
DFR[BLKS] [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays the current comgroup's defer blocks sorted by which
chain of defer blocks to which they are currently linked.
00002
00001
Format:
{DIR|DIRECTORY} [fid|R[ESET]]
Parameters:
fid    specifies the new default account fid, and may consist of an account or
a packset name and an account.
RESET    specifies that the default account is to be reset to the running
account.
Description:
This command changes the default account and packset.  The default account and
packset are the account and associated packset that are selected if an account
is not supplied as part of a disk file fid specification.  Initially, the
default account is the logon or running account and the packset name is nil.
When used without parameters, DIRECTORY displays the current directory
pointer.
Examples:
nodename -DIRECTORY .SYSLIB
This command directs that subsequent fids that do not include an account are
to default to the .SYSLIB account and the packset associated with that
account.
nodename -DIRECTORY DP#UTIL.Y
This command specifies that subsequent fids that do not include an account are
to default to the Y account on the packset named UTIL.
nodename -DIRECTORY RESET
This command re-establishes the running account and its associated packset as
the default.
00002
00003
00001
Format:
{DO|!} IBEX-command
Parameters:
IBEX-command    any legal IBEX command.  See the CP-6 Programmer Reference
Manual (CE40).
Description:
The DO command allows the user to execute an IBEX command without exiting the
current processor.
Note:  The ! (exclamation point) may be used instead of the word DO.  It
should be noted however that if the ! is used in an XEQ file, it will
terminate the current processor session unless preceded by at least one blank,
or by a double ! (!!).
Examples:
nodename -DO DI
means display the current system status
nodename -!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3
means set up a title and page number for a report destination
00002
00003
00001
Format:
DOM[AIN] domain
Parameters:
domain is one of the following:
    ASL      Alternate Shared Library
    ICP      Interactive Command Processor
    IDB      Interactive Debugger
    USR      User domain
Description:
This command selects which linkage segment to use on domain-dependent user
display commands.
Examples:
nodename -DOMAIN ASL
nodename -DOMAIN USR
00002
00003
00001
Format:
DQH [iom[-channel][,iom[-channel]] ...
Parameters:
iom    specifies an I/O Multiplexor number (0 through 3).
channel    specifies a channel number (0 through 127).  If channel is omitted,
the default is all channels on the IOM.
Description:
This command produces a formatted display of driver queue headers (channel
tables).
The driver queue header display items include:
  Header         Description
I-CCC          IOM and channel number of this channel.
IO$            Pointer to IOQ packet for last IO on this channel.
MPC            Name of MPC that channel is on.
MRC            Whether multi-record command is in progress.
PART           Whether channel is partitioned.
SQH$           Pointer to subsystem queue header for this channel.
STATE          Current channel state.
STP            Whether channel is to be stopped.
TI             Number of 5-second intervals remaining before timeout.
TND            Current T & D function on channel.
Examples:
nodename -DQH 1
nodename -DQH 0-16
00002
00003
00001
Format:
DROP [display_opts]
Parameters:
display_opts    are one or more of the following channel context display
options separated by commas:
  Option      Display Requested
CHT         Display channel tables
ERD         Display extended real device
FLD         Display field tables (forms)
INP         Display input buffers
LCT         Display LCT bytes
MRD         Display master real device
MVD         Display master virtual device
OTP         Display output buffers
PST         Display position information
RCR         Display record buffers (SE)
SRD         Display subordinate real device
SSN         Display session context
STR         Display GV$STR
TRC         Display trace buffers
TYP         Display type-ahead buffers
USR         Display user (handler) context
VDI         Display GV$VDI
Description:
The DROP command specifies which portions of context for a channel are to be
deleted from display.  The DROP command turns a display flag off.  When ANLZ
is invoked, the CHT display flag is turned off, and all the remaining display
flags (i.e., the LCT, OTP, PST, RCV, SSN, STR, TYP, and VDI flags (see HELP
(ANLZ) PARAMETERS)) are turned on.  The DROP command can be used initially to
turn off the LCT, OTP, PST, RCV, SSN, STR, TYP and/or the VDI flags, and
thereafter to remove the effects of turning on display flags via the ADD
command.
The command:
    DROP
turns off all display flags which causes the FMT command to display the
channel tree structure.
Example:
 nodename -DROP CHT
 nodename -DROP LCT,OTP
 nodename -DROP OTP
00002
00003
00001
Format:
DTR[EE] [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays the current comgroup's tree of data pages currently in
use by the data cache.  Each page is associated with a single file relative
disk granule.
00002
00001
Format:
DU[MP][format] location[,size] [{FOR  } {sysid   }[,domain]
                               [{USING} {.usernum}        ]
    [[WITH] A[SCII]] ['title']
Parameters:
format    is one of the following options which must be appended to DUMP (no
intervening blanks):
    A    includes the ASCII representation of the characters on the right.
    (This format option and the clause WITH ASCII request the same format.)
    L    requests a long dump, which inhibits compression of duplicate dump
    lines.
    X    requests a hexadecimal (8-of-9-bits) dump instead of octal.
location    is an address expression.
size    is a value expression that specifies the number of words to be dumped.
FOR    means use monitor linkage segment.
USING    means use user linkage segment.
sysid    is a decimal number.
 .usernum    is an octal number.
domain    is ASL, MON, ICP, IDB, or USR.  domain overrides FOR or USING.
WITH ASCII    includes the ASCII representation of the characters on the
right.
'title'    specifies the title text that is to be placed in the page header
and table of contents (see the CONTENTS command).
Description:
This command produces an octal dump of a specified area of memory.
Examples:
nodename -DUMP B$USRT$->0,15 WITH ASCII
nodename -DUMP B$JIT$->0,10 FOR .35
nodename -DUMP JIT$->0,30 FOR .37 ASCII
00002
00003
00001
Format:
DUMP location[,size] [FOR userid] [WITH {ASCII }] ['title']
                     [                  {EBCDIC}]
Parameters:
location    is an address expression for the starting location of the dump.
size    is a value expression that specifies the number of words to dump.
WITH ASCII    includes ASCII character representation on the right side of the
dump.
WITH EBCDIC    includes EBCDIC character representation on the right side of
the dump.
userid    is either a hexadecimal user number preceded by a period, a decimal
sysid, or CUN.  CUN requests a memory dump of the current user at the time of
a screech.
'title'    specifies the title text that is to be placed in the page header
and table of contents.  (See the CONTENTS Command.)
Description:
This command produces a hexadecimal dump of memory.
Examples:
nodename -DUMP G$JIT$->0,.20 FOR .3 ASCII
nodename -DUMP ROS$->.34 FOR .2 EBCDIC
00002
00003
00001
DUMP
DUMP_FEP
DUMP
END
Format:
ECCB [useridlist]
Parameters:
useridlist    is one of more userids separated by commas.  Each userid is
either a hexadecimal user number preceded by a period, a decimal sysid, or
CUN.  CUN requests an ECCB display for the current user at the time of a
screech.
Description:
This command produces a formatted display of the selected user(s) Exceptional
Condition Control Blocks.  If useridlist is omitted, all user ECCBs are
displayed.
00002
00001
Format:
     [ON  ]
ECHO [TO  ] fid
     [OVER]
     [INTO]
Parameters:
{ON|TO|OVER|INTO}    directs file output processing.  OVER causes an existing
file to be overwritten.  INTO causes file extension.  ON and TO are synonyms
used to create a new file.  If the file exists, an error will occur.  The
default is ON.
fid    identifies the file to receive echoed commands.
Description:
This command echoes subsequent command input to the specified file, but only
if the IBEX echo flag is set via the IBEX ECHO command.
Examples:
nodename -ECHO INTO ANLZEXAMPLE
00002
00003
00001
More complicated commands use the "edit routine" function of X$FORMAT('%E') to
request services of ANLZ that are unavailable from X$FORMAT.  The four "count"
values serve as parameters to the ANLZ edit routine.  The first one, CNT(0),
specifies which service is being requested.  For some services, a text
parameter is required, and is supplied by enclosing the parameter text in a
zero-count repeat-group immediately after the "E" code.  For example, the
format string fragment '%4.16E%(NEW_FMT%)' requests service number 4, with 16
as the CNT(1) parameter, and 'NEW_FMT' as the text parameter.
Format:
{E[ND]|[E]X[IT]|Q[UIT]}
Description:
This command terminates ANLZ.
00001
ENQUEUE
Format:
ENQA[LL] [uselect_list]
Parameters:
uselect_list    specifies user selection criteria separated by commas.  For a
list of options type HELP (ANLZ) USELECT.  The default is all users.
Description:
This command displays all information in the ENQ-DEQ tables for the selected
user(s).
Enqueue-Dequeue table display items include:
  Header         Description
D              Domain.
EVENT_ID       Event code to be reported to user upon allocation.
QENTRY         Word offset into LS6 for queue entry.
REQUEST        Current "sharability".
STATE          Current state of enqueue request.
UPGRADE        If non-blank, sharability required for state to become
               allocated.
USER           User number.
W              Wait flag.
Examples:
nodename -ENQALL
00002
00003
00001
Format:
ENQ[UEUE] [uselect_list]
Parameters:
uselect_list    specifies user selection criteria separated by commas.  For a
list of options type HELP (ANLZ) USELECT.  The default is all users.
Description:
This command displays active ENQ-DEQ tables for selected users.  See the
description of the ENQALL command for an explanation of items displayed.
Examples:
nodename -ENQ
nodename -ENQ AC=JTAHOST
00002
00003
00001
Format:
ENTER [script_fid] [,frame_name] [initial_input]
Parameters:
script_fid    is the file identifier for the script to be executed.
frame_name    is the first frame of the script to execute.
initial_input    supplies responses to the initial prompts for the dialog.
Description:
The ENTER command invokes a CP-6 ADAPT dialog that permits use of precompiled,
menu-driven user interfaces called compiled scripts.  script_fid identifies
the file containing the compiled script for the dialog.  See the CP-6 ADAPT
Reference Manual (HA12) for more information on using ADAPT dialogs.
00002
00001
Format:
ERASE [ALL|ldevlist]
Parameters:
ALL    specifies that the accumulated output for all logical devices is to be
deleted.  This is the default.
ldevlist    specifies that the accumulated output for the specified logical
device or devices is to be deleted.  The list is entered in the format
ldevname[,ldevname]...
ldevname is a logical device name established through the LDEV command.
Description:
ERASE deletes the accumulated output for logical devices.
Examples:
nodename -ERASE ALL
deletes all output accumulated for all logical devices defined for the session
or job.
00002
00003
00001
Format:
ERR[OR] number
Parameters:
number    number is the value to be displayed as the error code.  If entered
as a hexadecimal value, number is assumed to be a front end error code and is
converted to host format before display.
Description:
This command passes a number to M$ERRMSG to be displayed as an error code.  If
entered as a hexadecimal value, number is assumed to be a FEP error code and
is converted to a host error code prior to being passed to M$ERRMSG.
Example:
nodename -ERROR .302522000010
00002
00003
00001
Format:
EV[ALUATE] value_expression
Parameters:
value_expression    specifies a value expression to be evaluated.
Description:
The EVALUATE command evaluates an expression and displays the result as a
decimal, octal and hexadecimal value.  If appropriate, the value is displayed
as an ENTDEF+offset, also.
Example:
nodename -EV 37*4+.200
00002
00003
00001
Format:
EVB[UF]
Description:
This command produces a formatted display of event buffer and connect buffer
in reverse chronological order.  The header for the EVBUF display contains two
lines, each beginning with the character "E" or "C" for a scheduler event and
connect fault, respectively.  The top header line is for event entries and the
bottom header line is for connect entries.  Time difference and time stamp
applies to both event and connect entries.
The event buffer display items are:
  Item           Measuring
CODE           Identifies who made the entry
DIFFERENCE     Time difference in microseconds since previous entry
EVENT          Event reported
STAMP          Time stamp in octal
STATE          User's state at time event was reported
USR            Octal user number
The connect buffer display items are:
  Item           Measuring
DIFFERENCE     Time difference in microseconds since previous entry
IC             Instruction counter of connect fault
MLBX           Connect information
PORT           Port number of CPU
STAMP          Time stamp in octal
WSR            Domain in which connect fault occurred
00001
Format:
EVB[UF]
Description:
This command produces a formatted display of the Scheduler Event Buffer.
00001
EVBUF
EXIT
The following example illustrates how to use ANLZ to display comgroup
information.  In the example, the following ANLZ commands are used:
o   CGSUM is used to display all active comgroups.
o   CG is used to display general comgroup context for a selected comgroup.
o   STREE is used to display current and defined stations for the selected
    comgroup.
o   TTREE is used to display current and defined message types for the
    selected comgroup.
o   QTREE is used to display anonymous queue information.
o   DTREE is used to display data cache page mapping data.
o   MLH is used to display the message list headers.
o   MSGLIST is used to display message context information.
o   EVALUATE is used to convert an offset value that identifies the location
    of message data.
o   DUMPA is used to display the message data.
!ANLZ
ANLZ E02
SAMPNODE - (node 20) Selected
SAMPNODE -
SAMPNODE -"Display all active comgroups.
SAMPNODE -CGSUM
  CTXT @   DSB$    CFU$   AU STA    AUSTA$   TERMs DCBs FID:name.acct(packset)
 ------- ------- ------- -------- ---------- ----- ---- ----------------------
 .022152 .020240 .006460   none    ***NIL***     0    5 EXAMPLE_CG.:CGGN(DOVE)
 .022440 .020414 .004710 STARGHST .003272/00     2    1 STARCG.:SYS(SYS)
 .022726 .020570 .004740 TheGhost .003342/00     0    1 THINGCG.:SYS(SYS)
 .023214 .020656 .005020 AU       .003342/00     1    1 RINGCG.:SYS(SYS)
 .023512 .020744 .005210 MAILMAN  .003342/00     0    1 MAIL_CG.:MAIL(SYS)
 .016162 .021032 .000630 FROG     .003342/00     3    1 FECG.:SYS(SYS)
 .016450 .021120 .000610 INSYM    .003342/00     0    1 APLCG.:SYS(SYS)
 .016736 .021206 .001470 INSYM    .003342/00     2    1 ISCG.:SYS(SYS)
 .017224 .021274 .001430 OUTSYM   .003342/00     7    2 OSCG.:SYS(SYS)
 .017512 .021362 .002160 HLPADMIN .003342/00    11    3 HLPCG.:SYS(SYS)
 .014152 .007624 .002560 KEYIN    .003342/00     2    1 OCCG.:SYS(SYS)
 .005512 .007712 .003060 KEYIN    .002754/00     0   18 CSCG.:SYS(SYS)
SAMPNODE -
SAMPNODE -"Select the appropriate cg.
SAMPNODE -CG EXAMPLE_CG.:CGGN
SAMPNODE -
SAMPNODE -"Display general cg context.
SAMPNODE -CG
  CTXT @   DSB$    CFU$   AU STA    AUSTA$   TERMs DCBs FID:name.acct(packset)
 ------- ------- ------- -------- ---------- ----- ---- ----------------------
 .022152 .020240 .006460   none    ***NIL***     0    5 EXAMPLE_CG.:CGGN(DOVE)
DATA CACHE
NEEDPGHD$= ***NIL***  IOHD$= ***NIL***  GETHD$= ***NIL*** AVAIL.HD$=.004000/00
NEEDPGTL$= ***NIL***  IOTL$= ***NIL***  GETTL$= ***NIL*** AVAIL.TL$=.004000/00
NEEDPGCNT= 0          IOCNT= 0          GETFLG= 0
DATAFREE$= ***NIL*** IOQHD$= ***NIL*** DFRFRHD$=.003610/00 CURDATAPGS= 1
  ADDFREE= 0         IOQTL$= ***NIL*** NDFRBLKS= 20        MINDATAPGS= 1
   FREEDA=.1000001   UGRANS= 3           NGAVAL= 27        MAXDATAPGS= 5
MMD    GATE=(0,U=KQM$MM2+.4104,L=KQM$MM2+.3711)
 HEAD$=.002000/00  CURPG=2         MAXBPG=5        BASEREL$= ***NIL*** GIP=0
PHEAD$= ***NIL*** CURBPG=1         MINBPG=1          STAHD$= ***NIL*** FREECNT
 FREE$= ***NIL*** CURPPG=0        BAPLOCK=0         MBLKHD$= ***NIL*** | 0
GARB
     STA=0 MBLK$= ***NIL***    DELAY=0        NCSTAMP=.0
    DMIP=0 OMLH$= ***NIL***   ACTCNT=0          NCDDA=.0
 RECYCLE=0 SPHD$= ***NIL*** SPLITCNT=0        SCSTAMP=.0
   INSRT=0 SPTL$= ***NIL***     INDX=0          SCDDA=.0
  CONERR=0 SQHD$= ***NIL***   RELCNT=0        PCSTAMP=.0
    SQIP=0 DBLK$= ***NIL***  CCCOUNT=0        SPSTATE= 0
    DELJ=0 JNLD$= ***NIL***   TCOUNT=0           TYPE= 0
QUEUE
 WCRL$= ***NIL*** DELAY$= ***NIL***   BUSY=none  GACT=0   RQGC=0
 PLHD$=.003406/00   MLH$= ***NIL***  RUSR#=.0            RQMEM=0
SAMPNODE -
SAMPNODE -"Display the current and defined stations for the cg.
SAMPNODE -STREE
  ADDR @    STATION KQRS LOCKCNT IDSC   USR# MLH.COUNT  READS   WRITES S-TREE
---------- -------- ---- ------- | TERM ---- --------- -------  ------
STREE.GATE=(.34,0,U=KQR$READ+.5702,L=KQR$READ+.5747)
 .003144/00 $CON0000 PEND      0 0 0      34         0       4       4 >
 .002572/00 $CON0001 PEND      0 0 0      40         0       5       5 >
 .003474/00 *GORGO   none      0 0 0      40         0       0       0 >
 .003254/00 LARK_CTL PEND      0 0 0      36         0       9       9 >
 .002702/00 READER   none      0 0 0      34         5       0       0 >
 .002504/00 WRITER   none      0 0 0      40         0       0       5 >
 .003144/00 $CON0000 R=.003122/00 G=(.34,0,U=KQL$LIST+.6010,L=KQR$READ+.1457)
 .002572/00 $CON0001 R=.002550/00 G=(.40,0,U=KQL$LIST+.6010,L=KQR$READ+.1457)
 .003474/00 *GORGO   R= ***NIL*** G=(.40,0,U=MONECCB+.17752,L=MONECCB+.17740)
 .003254/00 LARK_CTL R=.003320/00 G=(.36,0,U=KQL$LIST+.6010,L=KQR$READ+.1457)
 .002702/00 READER   R= ***NIL*** G=(.40,0,U=KQW$WRITE+.4111,L=KQW$WRITE
 .002702/00 (cont.)                  +.3051)
 .002504/00 WRITER   R= ***NIL*** G=(.40,0,U=KCA$AU+.46,L=KCA$AU+.32)
SAMPNODE -
SAMPNODE -"NOTE:  The MLH.COUNT for station READER indicates that there are
SAMPNODE -"       5 directed messages waiting in the comgroup to be
SAMPNODE -"       delivered to station READER.
SAMPNODE -
SAMPNODE -"Display the current and defined message types for the selected cg.
SAMPNODE -TTREE
  ADDR @    MSGTYP  #WRITE JRNL        ADDR @    MSGTYP  #WRITE JRNL   T-TREE
---------- -------- ------ | MPRIO    --------- -------- ------- | MPRIO
TTREE.GATE=(.36,0,U=KQR$READ+.5702,L=KQR$READ+.5674)
 .003406/00              0 0 1     > .003034/00 CONTROL        0 0 1     >
 .002746/00              0 0 1     > .002356/00 STATSBLK       0 0 1     >
SAMPNODE -
SAMPNODE -"Display anonymous queue information (organized by message type in
SAMPNODE -"this case because QISS=NO).
SAMPNODE -QTREE
  ADDR @      KEY     CNACT    READS$   LOCKCNT MLH.COUNT   Q-TREE
---------- -------- -------- ---------- ------- ---------
 .003406/00                0  ***NIL***       0         0 >
 .003034/00 CONTROL        0  ***NIL***       0         0 >
 .002746/00 FUNCTBLK       0  ***NIL***       0         0 >
 .002356/00 STATSBLK       0  ***NIL***       0         0 >
SAMPNODE -
SAMPNODE -"Display pages currently mapped into the data cache (this is where
SAMPNODE -"the actual data of the messages is stored).
SAMPNODE -DTREE
  ADDR @       KEY        ADDR @       KEY        ADDR @       KEY      D-TREE
---------- ----------   ---------- ----------   ---------- ----------
DTREE.GATE=(0,U=KQD$DBLK+.7174,L=KQD$DBLK+.7215)
 .004000/00 .001000002 >
SAMPNODE -
SAMPNODE -"NOTE:  There is currently only one page mapped into the data cache:
SAMPNODE -"       .004000/00 is $AS0->.4000 - memory page
SAMPNODE -"       .001000002 is granule 2 - file relative disk address.
SAMPNODE -
SAMPNODE -"Display the message list headers.
SAMPNODE -MLH
   MLH @    STA/KEY  Q    HEAD$      TAIL$     DELAY$  SUPERCNT CNT BUSY RUSR
 ---------- -------- - ---------- ---------- --------- -------- --- ---- ----
 .003200/00 $CON0000 0  ***NIL***  ***NIL*** ***NIL***      0     0      .0
 .002626/00 $CON0001 0  ***NIL***  ***NIL*** ***NIL***      0     0      .0
 .003530/00 *GORGO   0  ***NIL***  ***NIL*** ***NIL***      0     0      .0
 .003310/00 LARK_CTL 0  ***NIL***  ***NIL*** ***NIL***      0     0      .0
 .002736/00 READER   0 .002662/00 .003234/00 ***NIL***      0     5      .0
 .002540/00 WRITER   0  ***NIL***  ***NIL*** ***NIL***      0     0      .0
 .003463/00          1  ***NIL***  ***NIL*** ***NIL***      0     0      .0
 .003111/00 CONTROL  1  ***NIL***  ***NIL*** ***NIL***      0     0      .0
 .003023/00 FUNCTBLK 1  ***NIL***  ***NIL*** ***NIL***      0     0      .0
 .002433/00 STATSBLK 1  ***NIL***  ***NIL*** ***NIL***      0     0      .0
SAMPNODE -
SAMPNODE -"NOTE:  Because the messages in this cg are sorted by message type
SAMPNODE -"       (QISS=NO), entries appear for each message type as well as
SAMPNODE -"       each station.
SAMPNODE -"
SAMPNODE -"       COUNT for READER is non-zero, indicating that messages
SAMPNODE -"       currently reside in the cg waiting to be delivered to this
SAMPNODE -"       station.
SAMPNODE -"
SAMPNODE -"       HEAD$ and TAIL$ point to the head and tail of a linked list
SAMPNODE -"       of MBLKs each containing the context information associated
SAMPNODE -"       with a particular message;  the MBLK does not contain the
SAMPNODE -"       actual data of the message.
SAMPNODE -
SAMPNODE -!PLATEN W=120
SAMPNODE -CG EXAMPLE_CG.:CGGN
SAMPNODE -
SAMPNODE -"Display the message list of context information for station READER.
SAMPNODE -"NOTE:  The HEAD$ of the linked list is used in this command.  In
SAMPNODE -"       this example, .002662/00 ($AS0->.2662) should be used.
SAMPNODE -MSGLIST $AS0->.2662
         MBLK @   S KEY1   KEY2     STAR  DVBYT MSGSIZ PRIO    EOM/VFC LNK DDA
           UTS          MID.PRIMARY  M
                 if a super-MBLK ->  KEY1A KEY2A COUNT          PRIOLO
                        UTSHI        I
       ---------- - ------ -------- ----- ----- ------ ------- ------- --- ---
     1 .002662/00          WRITER         .200    1024 .001001 .501(A)  >  .42
3001000001 .365017365522          13
     2 .002642/00          WRITER         .200    1024 .001001 .501(A)  >  .22
0001000001 .365017365522          14
     3 .003346/00          WRITER         .200    1024 .001001 .501(A)  >  .57
5001000002 .365017365522          15
     4 .003366/00          WRITER         .200    1024 .001001 .501(A)  >  .37
2001000002 .365017365523          16
     5 .003234/00          WRITER         .200    1024 .001001 .501(A) NIL .16
7001000002 .365017365523          17
SAMPNODE -
SAMPNODE -"NOTE:  The information displayed here is the message context, taken
SAMPNODE -"       from each MBLK.  The reference to the corresponding DBLK
SAMPNODE -"       where the data is stored is the DDA (Data Disk Address).
SAMPNODE -"       The DDA is stored as .oooggggggggg, where o represents a
SAMPNODE -"       double word offset into the granule and g represents the
SAMPNODE -"       file relative granule number.
SAMPNODE -"
SAMPNODE -"       Examining the DDAs of these five messages shows that the
SAMPNODE -"       message data is stored in two granules:  .001000001 and
SAMPNODE -"       .001000002
SAMPNODE -"
SAMPNODE -"       Only data cache granules that are currently mapped into
SAMPNODE -"       memory can be examined.  The DTREE display shows that only
SAMPNODE -"       .001000002 is currently mapped in.
SAMPNODE -
SAMPNODE -!PLATEN W=80
SAMPNODE -CG EXAMPLE_CG.:CGGN
SAMPNODE -
SAMPNODE -"Display the message associated with MBLK 3.
SAMPNODE -"NOTE:  The DDA of message 3 is .575001000002.  The DTREE display
SAMPNODE -"       indicates that this page is mapped into $AS0->.4000.  The
SAMPNODE -"       double word offset (.575) must be converted to a single word
SAMPNODE -"       offset and used as an offset into $AS0->.4000.  The MSGSIZE
SAMPNODE -"       is 1024 bytes, which is .400 words.
SAMPNODE -EV .575*2
          Dec: 762  Oct: 1372  Hex: 2FA  Entdef: S_RWPARM+.24
SAMPNODE -EV .4000+.1372
          Dec: 2810  Oct: 5372  Hex: AFA  Entdef: KI_NET+.7
SAMPNODE -DUA $AS0->.5372,.406
 .5372-0-0,$AS0,.406 ASCII
005370                            016732002000 000000000000          .Z......
005374  000000006014 000400000000 000406000000 555555555555  ............mmmm
005400  060060060060 060060060062 040040040040 040040040040  00000002
005404  040040040040 040040040040 040040040040 040040040040
005774* 040040040040 040040040040 040040040040 040040040052                 *
SAMPNODE -
SAMPNODE -"NOTE:  The first 6 words of the DBLK contains information to aid in
SAMPNODE -"       message processing.  The message data, in this case an
SAMPNODE -"       8 digit sequence number followed by blanks and concluded
SAMPNODE -"       with an "*", directly follows.
SAMPNODE -
SAMPNODE -"Display the message associated with MBLK 4.
SAMPNODE -EV .372*2
          Dec: 500  Oct: 764  Hex: 1F4  Entdef: S_PGTABLE+.32
SAMPNODE -DUA $AS0->.4764,.406
 .4764-0-0,$AS0,.406 ASCII
004764  005266002000 000000000000 000000006014 000400000000  .6..............
004770  000406000000 555555555555 060060060060 060060060063  ....mmmm00000003
004774  040040040040 040040040040 040040040040 040040040040
005370* 040040040040 040040040052                                   *
SAMPNODE -QUIT
Format:
[E]X[IT]
Description:
This command terminates ANLZ.
00001
Format:
FEI [fexlist]
Parameters:
fexlist    specifies one or more indexes into the local FEP tables separated
by commas.  Note that fex is not a node number.
Description:
This command displays information from the FEP/HOST interface tables.  If
fexlist is omitted, information for all local FEPs is displayed.
00002
00001
The FEP commands are: ACCRES, ADD, BOBCAT, CHANNELS, CHNTBL, DCBS(DCBS_FEP for
HELP), DROP, DUMP(DUMP_FEP for HELP), ECCB, EVBUF, FMT, HMI, INTCON, IOP,
IOPC[HECK], ISA, JIT(JIT_FEP for HELP), K$RCQ, K$SCQ, KN$TCTX, LCT, LDCT,
LDCTCHECK, LLIST, MAP, MEMORY, MLCP, PLUGH, PPUT, RCQ, RECOVERY(RECOVERY_FEP
for HELP), ROS, ROUTE(ROUTE_FEP for HELP), RUE, SCQ, SFILES, SPY(SPY_FEP for
HELP), SSN, SSNCHECK, STATUS, TCB(TCB_FEP for HELP), TCTX, TCTXCHECK, TSA, and
USRTABLES(USRTABLES_FEP for HELP).
For a one-line summary of these commands, enter: ?.
For complete HELP for each command, enter:
HELP (ANLZ) command.
  Command     Description
  ACC[RES]
              Displays the contents of the Account Resource Table.
  ADD
              Identifies portions of channel context to be displayed via the
              FMT command.
  BOB[CAT]
              Produces a formatted display of the base of the BOBCAT data
              segment.
  CHANNELS
              Displays channel ids and channel types.
  CHN[TBL]
              Produces a formatted display of a channel table entry.
  DCB[S]
              Displays DCBs for selected user(s).
  DROP
              Removes portions of channel context from display via the FMT
              command.
  DU[MP]
              Dumps specified areas of FEP memory in hexadecimal.
  ECCB
              Displays the ECCB for selected user(s).
  EVB[UF]
              Displays the contents of the Scheduler Event Buffer.
  FMT
              Produces a formatted display of context for a channel.
  HMI
              Displays the contents of a Host/Monitor Context Block.
  INT[CON]
              Displays the contents of the Interrupt Table.
  IOP
              Displays the contents of an I/O Packet.
  IOPC[HECK]
              Checks for inconsistencies in the I/O Packet Chain.
  ISA
              Formats an area of FEP memory as an Interrupt Save Area.
  JIT
              Displays selected items from the JIT for selected user(s).
              Displays the last messages removed from the Receive Circular
              Queue for a specified user.
              Displays the last messages removed from the Send Circular Queue
              for a specified user.
              Produces a detailed display of the Transport Context Block.
  LCT
              Dumps the Line Control table for a channel in hexadecimal.
  LDCT
              Displays the contents of the Logical Device Control Table.
  LDCTC[HECK]
              Checks for inconsistencies in the LDCT free chain.
  LLIST
              Dumps the nodes of a linked list.
  MAP
              Displays formatted contents of the Physical Page Table.
  MEM[ORY]
              Displays current memory allocation in the FEP.
  MLCP
              Dumps specified areas of MLCP memory in hexadecimal.
  PL[UGH]
              Displays a chain of procedure calls in the user's automatic
              stack.
  PPUT
              Checks for inconsistencies in the Physical Page Table.
  RCQ
              Displays the contents of the Receive Circular Queue.
  REC[OVERY]
              Displays formatted FEP recovery buffer.
  ROS
              Displays the Read-Only Segment header information.
  ROUTE
              Displays network routing information.
  RUE
              Reports a scheduler event for a user.
  SCQ
              Displays the contents of the Send Circular Queue.
  SFI[LES]
              Displays the contents of the Shared File Table.
  SPY
              Displays all currently logged on FEP users.
  SSN
              Displays the contents of Session Context Block(s).
  SSNC[HECK]
              Checks for inconsistencies in the Session Context chain.
  STAT[US]
              Displays memory usage for selected user(s).
  TCB
              Displays the Task Control Block for selected user(s).
  TCTX
              Produces a summary display of the Transport Context Table.
  TCTXC[HECK]
              Reports inconsistencies in the Transport Context Table chain.
  TSA
              Formats an area of FEP memory as a Trap Save Area.
  USR[TABLES]
              Displays the contents of the User Table.
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
  Name        Segment Start     Description
AUTO$       .A0000            User Auto
BIGFOOT$    .F0000            Bigfoot Procedure
CP_DS$      .0C000            Command Processor Data Segment
DB_DS$      .02000            Debugger Data Segment
DS1$        .0A000            User Data Segment 1
DS2$        .0B000            User Data Segment 2
DS3$        .B0000            User Data Segment 3
DS4$        .C0000            User Data Segment 4
ENT_DATA$   .08000            Monitor Entry Data
ENT_PROC$   .09000            Monitor Entry Procedure
HANDQ$      .D0000            Handler Circular Queue
ISR$        .10000            Instruction Segment
LOW_MEM$    .03000            Window to low 4K of real memory
MHJIT$      .06000            Monitor HJIT
ROS$        .01000            Read Only Segment
TSTACK$     .04000            Monitor Auto
UHJIT$      .05000            User HJIT
WINDOW$     .90000            Window Segment
Format:
FMT {[.channelnum[-subnum[subsubnum]]} [FULL] [display_opts]]
    {@location [FOR userid]          }
Parameters:
 .channelnum    is a hexadecimal number that is the address of the physical
channel whose context is to be displayed.  The period preceding the
hexadecimal value is required.
-subnum    is a decimal number that represents the second level (i.e., the
first subordinate level).
-subsubnum    is a decimal number that represents the third level (i.e., the
second subordinate level).
FULL    specifies that context for all subordinate levels is to be displayed
also.
display_opts    are one or more of the following channel context display
options separated by commas:
      Option      Display Requested
    CHT         Display channel tables
    ERD         Display extended real device
    FLD         Display field tables (forms)
    INP         Display input buffers
    LCT         Display LCT bytes
    MRD         Display master real device
    MVD         Display master virtual device
    OTP         Display output buffers
    PST         Display position information
    RCR         Display record buffers (SE)
    SRD         Display subordinate real device
    SSN         Display session context
    STR         Display GV$STR
    TRC         Display trace buffers
    TYP         Display type-ahead buffers
    USR         Display user (handler) context
    VDI         Display GV$VDI
@location    is an address expression that specifies a starting memory
location at which to begin formatting data for display as a channel table
entry.
userid    is either a hexadecimal user number preceded by a period, a decimal
sysid, or CUN.  CUN requests a memory dump of the current user at the time of
a screech.
Description:
The FMT command produces a formatted display of the context for one or more
channels.
If the keyword FULL is appended to the command, context for the specified
channel and all subordinate context will be displayed.
If display_opts is specified, only the requested context will be displayed.
Otherwise, the display options as set by ADD and DROP commands will be used.
The command:
FMT
displays a list of the currently set flags.
Examples:
nodename -FMT .4F80 FULL VDI,CHT,TYP
nodename -FMT .8200-3-2
00002
00003
00001
Service (1) helps to implement the formatting of multiple chains of different
pieces of context required for the ANLZ FEP command FMT.  This service adds an
entry to a last-in, first-out stack, each entry of which consists of the
location of some context to display, and the name of a format string to use to
display it.  CNT(1) specifies the location, and the text parameter specifies
the format string name.  If CNT(1) is zero or if the service is requested
other than while performing a FMT command, the request is ignored.
Service (5) helps to implement the FMT command options that select only
portions of the complete display.  CNT(1), CNT(2), and CNT(3) should be
computed by adding two to the EQUs of the form DA_CHNTBL_OPT_optionname in
DA_CMD_C.:LIBRARY.  If none of the indicated options are in effect for this
invocation of the FMT command, formatting for the current format string is
terminated.  For example:
    '%5.' %(DA_CHNTBL_OPT_INP+2).%(DA_CHNTBL_OPT_USR+2) E
is used to abort formatting unless at least one of the options INP or USR is
selected.  The service (5) request should follow any service (1) requests in
the format string; otherwise, the service (1) displays requested would also be
suppressed.
The following table lists the format strings released with ANLZ in
:FORMAT.:SYS, along with a short description of the function of each string.
They might be useful as examples of how to accomplish various effects,
although they are generally quite difficult to parse after CRAWDAD.X has
removed all the commentary, blank space, and pre-processor identifiers.
    Name             Description
    ---------------  --------------------------------------------------
    DBD$FMT          Implements the FMT command (nothing is displayed)
    G$ASDT           G$ASDT structure display
    G$ISA            G$ISA structure - used for the ISA command
    G$PLUGH          Auto frame display - used for PLUGH command
    G$TSA            G$TSA structure - used for the TSA command
    GJA$HAND_CTX     NODEADMN handler context at GJA_HAND_HEAD$->0
    GJA$USRLGN_CTX   NODEADMN logon context at GJA_USRLGN_HEAD$->0
    FO_DET           OUTSYM device/event trace at FO_DET
    K$CQM            Used by the \K$RCQ and \K$SCQ commands
    K$ICQ            HOST \K$ICQ command
    K$LCT            LCT display
    K$OCQ            HOST \K$OCQ command
    K$RCQ            \K$RCQ command
    K$SCQ            \K$SCQ command
    KA$INP           INP part of FMT display for an ASYNC line
    KA$OTP           OTP part of FMT display for an ASYNC line
    KH$CHN           CHN command and CHT part of FMT display
    KH$CHT           CHANNELS command
    KI$OSIROUTE      HOST OSI route table at KI_OSIROUTE$$->x->0
    KJF$CTX          COUPLER context at .D0018->0
    KN$TCTX          Another name for \TCTX command
    KNN$LINK         FEP LINK table at KNN_LINK$$->x->0
    KNN$NFRAG        OSI message network fragment header
    KNN$NHDR         OSI message network context data
    KNN$NPDU_FIXED   OSI message network header
    KNN$NPDU_SEGMENT OSI message network trailer
    KNN$OSIROUTE     FEP OSI route table at KNN_OSIROUTE$$->x->0
    KV$BPC           VDH buffer manager context display
    KV$ERD           Part of the FMT command display
    KV$ERDCHR        Used by KV$ERD
    KV$FLD           FLD part of the FMT command display
    KV$FLDLST        FLD part of the FMT command display
    KV$FNDMRD        Used by the FMT command (Nothing is displayed)
    KV$LIN           FLD part of the FMT command display
    KV$LINLST        FLD part of the FMT command display
    KV$MRD           MRD part of the FMT command display
    KV$MVD           MVD part of the FMT command display
    KV$PTR           Part of the FMT command display
    KV$RCR           RCR part of the FMT command display
    KV$RCRLST        RCR part of the FMT command display
    KV$RCVSSN        VDH context at KV$RCVSSN$->0
    KV$SRD           SRD part of the FMT command display
    KV$SSN           SSN part of the FMT command display
    KV$SSN2          Used by KV$SSN
    KV$SSN_          Used by the FMT command (nothing is displayed)
    KV$STR           STR part of the FMT command display
    KV$TRC           TRC part of the FMT command display
    KV$TYPAHD        TYP part of the FMT command display
    KV$USRPRM        VDH context at KV$VDI.USRPRM$->0
    KV$VDI           VDI part of the FMT command display
    KV$X364          Part of FMT display if KV$MVD.ORG is X364
    KX$L2            X25 context part of FMT display
    KX$L2S           Used by KX$L2
    KX$L2TRC         Used by KX$L2
    KX$L2_2          Used by KX$L2
    KX$L3            Virtual circuit part of FMT display
    KX$L3_2          Used by KX$L3
    KX$L3_3          Used by KX$L3
    KX$LINKDEV       X25 resource circuit control part of FMT display
    KX$SL            X25 RFEP circuit part of FMT display
    KX$VC            X25 resource circuit part of FMT display
    KX$X29           INP part of FMT display for an X29 circuit
    KX_X29O          OTP part of FMT display for an X29 circuit
    KY$CTX           URP context part of FMT display
    KZ$3270CTR       3270 controller part of FMT display
    KZ$3270DEV       3270 device part of FMT display
    KZ$FNDCTX        Used to locate HASP context for FMT command
    KZ$LINCTX        BISYNC line context part of FMT display
    KZ$LINCTX2       Used by KZ$LINCTX
    KZ$SDEV          HASP subdevice part of FMT display
    TCTX             Transport context display
    TCTX2            Used by TCTX
    TREE             Tree table in ROSEG by user number (or SYSID if negative)
\FO_DET
Format:
GAR[B] [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays garbage collection items for the currently selected
comgroup.
00002
00001
Format:
GAT[E] location [{FOR  } {sysid   }[,domain]] ['title']
                [{USING} {.usernum}         ]
Parameters:
location    is an address expression.
FOR    means use monitor linkage segment.
USING    means use user linkage segment.
 .usernum    is an octal number.
domain    is one of the following:
ASL    Alternate Shared Library
ICP    Interactive Command Processor
IDB    Interactive Debugger
MON    Monitor
USR    User
domain overrides FOR or USING phrase.
'title'    specifies the title text that is to be placed in the page header
and table of contents.
Description:
This command displays two words of memory formatted as a gate.
Examples:
nodename -GATE NI_MFGATE
00002
00003
00001
The general commands are: ANLZ, CONTENTS, DATE, DELETE, DIRECTORY, DO, ECHO,
END, ENTER, ERASE, ERROR, EVALUATE, EVBUF, EXIT, FEI, HELP, LIST, OUTPUT,
PRINT, QUIT, READ, REPEAT, SELECT, STAR, SYMBOLS, TIME, TRAPFRAME, WAIT and
XEQ.  For a one-line description of these commands, enter: ?.  For complete
HELP for each, enter: HELP (ANLZ) command.
  Command     Description
  AN[LZ]
              Selects a dump file or the running system for ANLZ processing.
  CON[TENTS]
              Displays table of contents and start a new one.
  {DATE|TIME}
              Displays the current date and time.
  DELETE
              Deletes the current dump file.
  {DIRECTORY|DIR}
              Changes the default account and packset.
  {DO|!}
              Executes an IBEX command from within ANLZ.
  ECHO
              Echoes subsequent commands to a fid.
  E[ND]
              Exits ANLZ.
  ENTER
              Invokes a CP-6 ADAPT dialog from within this processor.
  ERASE
              Deletes accumulated output for logical devices.
  ERR[OR]
              Supplies a value to be displayed by M$ERRMSG as an error code.
  EV[ALUATE]
              Evaluates an expression and displays the results.
  EVB[UF]
              Displays event buffer and connect fault data.
  [E]X[IT]
              Exits ANLZ.
  HELP
              Obtains processor information.
  LIST
              Lists dump files in :SYSTAC.
  OU[TPUT]
              Sends subsequent output to fid.
  PRINT
              Sends output accumulated for logical devices to the destination.
  Q[UIT]
              Exits ANLZ.
  READ
              Reads subsequent commands from fid.
  REP[EAT]
              Repeats all preceding commands entered on the same line.
  SEL[ECT]
              Specifies host or FEP mode, and selects the host or FEP to
              analyze.
  STAR
              Creates text for a STAR.
  SYM[BOLS]
              Selects a run unit to be used for SYMDEF/ENTDEF searches and
              displays.
  TIME
              Displays the current time and date.
  TRAPFRAME
              Displays safe store frame at ANLZ trap.
  WA[IT]
              Waits a specified number of seconds.
  XEQ
              Inserts all or part of an XEQ file into the command stream;
              initiates execution of the contents of the file.
00006
00001
00002
00003
00004
00005
00006
00008
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
GENERAL_COMMANDS
Format:
GOD[ELTA]
Description:
This command transfers control to ANLZ DELTA to read commands.  Return to the
ANLZ command level may be effected with the ALIBRET command to DELTA.
00001
Format:
HELP [(processor)] [TOPICS] [keyword1] [-] [keyword2]
Note:  The elements
    [(processor)]
    [TOPICS]
    [keyword1] [-] [keyword2]
can be entered in any sequence.
Parameters:
For IBEX HELP, type:  !HELP HELP PARAMETERS
Description:
For IBEX HELP, type:  !HELP HELP DESCRIPTION
Examples:
For IBEX HELP, type:  !HELP HELP EXAMPLES
00002
00003
00001
A
  ACCRES Command -
      HELP ACCRES
  ADD Command -
      HELP ADD
  ANLZ -
    : Command -
      HELP TEXT FORMAT:
    ACCRES Command -
      HELP ACCRES FORMAT:
    ANLZ command -
      HELP ANLZ DESCRIPTION:
    ASR Command -
      HELP ASR FORMAT:
    AUTO Command -
      HELP AUTO FORMAT:
    BANNER Command -
      HELP BANNER FORMAT:
    BOBCAT Command -
      HELP BOBCAT FORMAT:
    CFUS Command -
      HELP CFUS FORMAT:
    CG Command -
      HELP CG FORMAT:
    CGLOG Command -
      HELP CGLOG FORMAT:
    CGSUMMARY Command -
      HELP CGSUMMARY FORMAT:
    CHANNELS Command -
      HELP CHANNELS FORMAT:
    CONTENTS Command -
      HELP CONTENTS FORMAT:
    CPU Command -
      HELP CPU FORMAT:
    CPUS Command -
      HELP CPUS FORMAT:
    DATA CACHE Command -
      HELP DATA_CACHE FORMAT:
    DCBS Command -
      HELP DCBS FORMAT:
      HELP DCBS_FEP FORMAT:
    DCT Command -
      HELP DCT FORMAT:
    DDT Command -
      HELP DDT FORMAT:
    DELETE Command -
      HELP DELETE FORMAT:
    DELTA Command -
      HELP DELTA FORMAT:
    DFRBLKS Command -
      HELP DFRBLKS FORMAT:
    DOMAIN Command -
      HELP DOMAIN FORMAT:
    DQH Command -
      HELP DQH FORMAT:
    DTREE Command -
      HELP DTREE FORMAT:
    DUMP Command -
      HELP DUMP FORMAT:
      HELP DUMP_FEP FORMAT:
    ECCB Command -
      HELP ECCB FORMAT:
    ECHO Command -
      HELP ECHO FORMAT:
    ENQALL Command -
      HELP ENQALL FORMAT:
    ENQUEUE Command -
      HELP ENQUEUE FORMAT:
    ERROR Command -
      HELP ERROR FORMAT:
    EVALUATE Command -
      HELP EVALUATE FORMAT:
    EVBUF Command -
      HELP EVBUF FORMAT:
    FEI Command -
      HELP FEI PARAMETERS:
    FO_DET Command -
      HELP \FO_DET_COMMAND FORMAT:
    GARB Command -
      HELP GARB FORMAT:
    GATE Command -
      HELP GATE FORMAT:
    GODELTA Command -
      HELP GODELTA FORMAT:
    HISTREG Command -
      HELP HISTREG FORMAT:
    INTCON Command -
      HELP INTCON FORMAT:
    IOCACHE Command -
      HELP IOCACHE FORMAT:
    IOQ Command -
      HELP IOQ FORMAT:
    ISA Command -
      HELP ISA PARAMETERS:
    JIT Command -
      HELP JIT FORMAT:
      HELP JIT_FEP FORMAT:
    K$ICQ Command -
      HELP \K$ICQ_COMMAND FORMAT:
    K$OCQ Command -
      HELP \K$OCQ_COMMAND FORMAT:
    K$RCQ Command -
      HELP \K$RCQ_COMMAND FORMAT:
    K$SCQ Command -
      HELP \K$SCQ_COMMAND FORMAT:
    KN$TCTX Command -
      HELP \KN$TCTX_COMMAND FORMAT:
    LCT Command -
      HELP LCT FORMAT:
    LDCT Command -
      HELP LDCT FORMAT:
    LIST Command -
      HELP LIST DESCRIPTION:
    MDCT Command -
      HELP MDCT FORMAT:
    MEMORY Command -
      HELP MEMORY FORMAT:
    MLCP Command -
      HELP MLCP FORMAT:
    MLH Command -
      HELP MLH FORMAT:
    MMD Command -
      HELP MMD FORMAT:
    MPDUMP Command -
      HELP MPDUMP FORMAT:
    MSGLIST Command -
      HELP MSGLIST FORMAT:
    OUTPUT Command -
      HELP OUTPUT FORMAT:
    PLUGH Command -
      HELP PLUGH FORMAT:
    PSR Command -
      HELP PSR FORMAT:
    QTREE Command -
      HELP QTREE FORMAT:
    QUEUE Command -
      HELP QUEUE FORMAT:
    RAT Command -
      HELP RAT FORMAT:
    READ Command -
      HELP READ FORMAT:
    RECOVERY Command -
      HELP RECOVERY FORMAT:
      HELP RECOVERY_FEP FORMAT:
    REPEAT Command -
      HELP REPEAT FORMAT:
    RESOLVE Command -
      HELP RESOLVE FORMAT:
    ROUTE Command, FEP -
      HELP ROUTE_FEP FORMAT:
    ROUTE Command, Host -
      HELP ROUTE FORMAT:
    RVBUFF Command -
      HELP RVBUFF FORMAT:
    SCHED Command -
      HELP SCHED FORMAT:
    SELECT Command -
      HELP SELECT FORMAT:
      HELP SELECT EXAMPLES:
    SFILES Command -
      HELP SFILES FORMAT:
    SPROC Command -
      HELP SPROC FORMAT:
    SPY Command -
      HELP SPY FORMAT:
      HELP SPY_FEP FORMAT:
    SSFRAME Command -
      HELP SSFRAME FORMAT:
    STAR Command -
      HELP STAR FORMAT:
    STATUS Command -
      HELP STATUS FORMAT:
    STREE Command -
      HELP STREE FORMAT:
    SYMBOLS Command -
      HELP SYMBOLS FORMAT:
    TCB Command -
      HELP TCB FORMAT:
      HELP TCB_FEP FORMAT:
    TCTX Command -
      HELP TCTX FORMAT:
      HELP TCTX_FEP FORMAT:
    TCTXCHECK Command -
      HELP TCTXCHECK_FEP FORMAT:
    TRAPFRAME Command -
      HELP TRAPFRAME FORMAT:
    TREE Command -
      HELP \TREE_COMMAND FORMAT:
    TSA Command -
      HELP TSA PARAMETERS:
    TTREE Command -
      HELP TTREE FORMAT:
    UNDELTA Command -
      HELP UNDELTA FORMAT:
    USRTABLES Command -
      HELP USRTABLES FORMAT:
      HELP USRTABLES_FEP FORMAT:
    WAIT Command -
      HELP WAIT FORMAT:
    WHO HAS Command -
      HELP WHO_HAS FORMAT:
    XEQ Command -
      HELP XEQ FORMAT:
  ANLZ Command -
      HELP ANLZ
  Appendix:  Adding New Displays -
      HELP ADDING_NEW_DIPLAYS
  Argument Stack Register -
      HELP ASR EXAMPLES:
  ASR Command -
      HELP ASR
  AUTO Command -
      HELP AUTO
  AUTO Stack -
      HELP AUTO EXAMPLES:
B
  The Backslash Command -
      HELP BACKSLASH
  BANNER Command -
      HELP BANNER
  BOBCAT Command -
      HELP BOBCAT
C
  CFUS Command -
      HELP CFUS
  CG Command -
      HELP CG
  CGLOG Command -
      HELP CGLOG
  CGMSUMMARY Command -
      HELP CGMSUMMARY
  CGSTATS Command -
      HELP CGSTATS
  CGSUMMARY Command -
      HELP CGSUMMARY
  channel table -
      HELP DQH DESCRIPTION:
  CHANNELS Command -
      HELP CHANNELS
  CHNTBL Command -
      HELP CHNTBL
  comgroup -
      HELP CG EXAMPLES:
  {:|>} Command -
      HELP TEXT
  CONTENTS Command -
      HELP CONTENTS
  CPU Command -
      HELP CPU
  CPUS Command -
      HELP CPUS
  Creating Format Strings for the Backslash Command -
      HELP BACKSLASH_FORMAT_STRINGS
  Current File Usage Table -
      HELP CFUS EXAMPLES:
D
  Data Buffers -
      HELP DATA_BUFFERS
  DATA CACHE Command -
      HELP DATA_CACHE
  Data Fetch Services (2,3,4,10,11, and 12) -
      HELP DATA_FETCH_SERVICES
  DATE Command -
      HELP DATE
  DCBS Command -
      HELP DCBS
      HELP DCBS_FEP
  DCT Command -
      HELP DCT
  DDT Command -
      HELP DDT
  DELETE Command -
      HELP DELETE
  DELTA Command -
      HELP DELTA
  device control table -
      HELP DCT DESCRIPTION:
  DFRBLKS Command -
      HELP DFRBLKS
  DIRECTORY Command -
      HELP DIRECTORY
  DO Command -
      HELP DO
  DOMAIN Command -
      HELP DOMAIN
  DQH Command -
      HELP DQH
  driver queue header -
      HELP DQH DESCRIPTION:
  DROP Command -
      HELP DROP
  DTREE Command -
      HELP DTREE
  DUMP Command -
      HELP DUMP
      HELP DUMP_FEP
E
  ECCB Command -
      HELP ECCB
  ECHO Command -
      HELP ECHO
  EDIT ROUTINE Services -
      HELP EDIT_ROUTINE_SERVICES
  END Command -
      HELP END
  ENQALL Command -
      HELP ENQALL
  ENQUEUE Command -
      HELP ENQUEUE
  ENTER Command -
      HELP ENTER
  ERASE Command -
      HELP ERASE
  ERROR Command -
      HELP ERROR
  EVALUATE Command -
      HELP EVALUATE
  EVBUF Command -
      HELP EVBUF
      HELP EVBUF_FEP
  event buffer -
      HELP EVBUF DESCRIPTION:
  Examples -
      HELP EXAMPLES
  EXIT Command -
      HELP EXIT
F
  FEI Command -
      HELP FEI
  FMT Command -
      HELP FMT
  FMT Command Services (1 and 5) -
      HELP FMT_COMMAND_SERVICES
  Format Strings Included in :FORMAT.:SYS -
      HELP FORMAT_STRINGS_IN_:FORMAT.:SYS
  \FO_DET Command -
      HELP \FO_DET_COMMAND
G
  GARB Command -
      HELP GARB
  GATE Command -
      HELP GATE
  GODELTA Command -
      HELP GODELTA
H
  HELP Command -
      HELP HELP
  history registers -
      HELP HISTREG EXAMPLES:
  HISTREG Command -
      HELP HISTREG
  HMI Command -
      HELP HMI
I
  INTCON Command -
      HELP INTCON
  IOCACHE Command -
      HELP IOCACHE
  IOP Command -
      HELP IOP
  IOPCHECK Command -
      HELP IOPCHECK
  IOQ Command -
      HELP IOQ
  ISA Command -
      HELP ISA
J
  JIT Command -
      HELP JIT
      HELP JIT_FEP
  Job Information Table -
      HELP JIT EXAMPLES:
K
  \K$ICQ Command -
      HELP \K$ICQ_COMMAND
  \K$OCQ Command -
      HELP \K$OCQ_COMMAND
  \K$RCQ Command -
      HELP \K$RCQ_COMMAND
  \K$SCQ Command -
      HELP \K$SCQ_COMMAND
  \KN$TCTX Command -
      HELP \KN$TCTX_COMMAND
L
  LCT Command -
      HELP LCT
  LDCT Command -
      HELP LDCT
      HELP LDCT_FEP
  LDCTCHECK Command -
      HELP LDCTCHECK
  LIST Command -
      HELP LIST
  LLIST Command -
      HELP LLIST_HOST
      HELP LLIST_FEP
M
  MAP Command -
      HELP MAP
  MDCT Command -
      HELP MDCT
  MEMORY Command -
      HELP MEMORY
  mirrored device control table (MDCT) -
      HELP MDCT DESCRIPTION:
  Miscellaneous Services (0) -
      HELP MISC_SERVICES
  MLCP Command -
      HELP MLCP
  MLH Command -
      HELP MLH
  MMD Command -
      HELP MMD
  Modifying the FMT Command -
      HELP MODIFYING_FMT_COMMAND
  MPDUMP Command -
      HELP MPDUMP
  MSGLIST Command -
      HELP MSGLIST
N
  Number Parameters -
      HELP NUMBER_PARAMETER
O
  OUTPUT Command -
      HELP OUTPUT
P
  Parameter Stack Register -
      HELP PSR EXAMPLES:
  PLUGH Command -
      HELP PLUGH
  PPUT Command -
      HELP PPUT
  PRINT Command -
      HELP PRINT
  Privileges for Use of ANLZ -
      HELP PRIVILEGES
  PSR Command -
      HELP PSR
Q
  QTREE Command -
      HELP QTREE
  QUEUE Command -
      HELP QUEUE
R
  RAT Command -
      HELP RAT
  RCQ Command -
      HELP RCQ
  READ Command -
      HELP READ
  READ Command (ANLZ) -
      HELP READ FORMAT:
  recovery buffer -
      HELP RVBUFF DESCRIPTION:
  RECOVERY Command -
      HELP RECOVERY
      HELP RECOVERY_FEP
  REPEAT Command -
      HELP REPEAT
  RESOLVE Command -
      HELP RESOLVE
  Resource Allocation Table -
      HELP RAT DESCRIPTION:
  ROS Command -
      HELP ROS
  ROUTE Command -
      HELP ROUTE
      HELP ROUTE_FEP
  RUE Command -
      HELP RUE
      HELP RUE_FEP
  RVBUFF Command -
      HELP RVBUFF
S
  safe store frame -
      HELP SSFRAME EXAMPLES:
  SCHED Command -
      HELP SCHED
  scheduler state chain -
      HELP SCHED DESCRIPTION:
  scheduler states (ANLZ) -
      HELP SCHEDULER_STATES
  SCQ Command -
      HELP SCQ
  SCTX Command -
      HELP SCTX
  SELECT Command -
      HELP SELECT
  SFILES Command -
      HELP SFILES
  shared processor table -
      HELP SPROC DESCRIPTION:
  SPROC Command -
      HELP SPROC
  SPY Command -
      HELP SPY
      HELP SPY_FEP
  SQH Command -
      HELP SQH
  SSFRAME Command -
      HELP SSFRAME
  SSN Command -
      HELP SSN
  SSNCHECK Command -
      HELP SSNCHECK
  STAR Command -
      HELP STAR
  STATUS Command -
      HELP STATUS
  STREE Command -
      HELP STREE
  Symbol Lookup Services (6 and 7) -
      HELP SYMBOL_LOOKUP_SERVICES
  SYMBOLS Command -
      HELP SYMBOLS
T
  TCB Command -
      HELP TCB
      HELP TCB_FEP
  TCTX Command -
      HELP TCTX
      HELP TCTX_FEP
  TCTXCHECK Command -
      HELP TCTXCHECK_FEP
  TRAPFRAME Command -
      HELP TRAPFRAME
  \TREE Command -
      HELP \TREE_COMMAND
  TSA Command -
      HELP TSA
  TTREE Command -
      HELP TTREE
U
  UNDELTA Command -
      HELP UNDELTA
  user tables -
      HELP USRTABLES EXAMPLES:
  USRTABLES Command -
      HELP USRTABLES
      HELP USRTABLES_FEP
W
  WAIT Command -
      HELP WAIT
  WHO HAS Command -
      HELP WHO_HAS
X
  XEQ Command -
      HELP XEQ
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
Format:
HIS[TREG] location [{FOR  }{sysid   }[,domain]] ['title']
                   [{USING}{.usernum}        ]
Parameters:
location    is an address expression:
FOR    means use monitor linkage segment.
USING    means use user linkage segment.
sysid    is the decimal sysid for a user.
usernum    is an octal user number.
domain    is one of the following:
ASL    Alternate Shared Library
ICP    Interactive Command Processor
IDB    Interactive Debugger
MON    Monitor
USR    User
domain overrides FOR or USING phrase.
'title'    specifies the title text to be placed in the page header and table
of contents.
Description:
This command formats the history registers in the fault handler auto frame
starting at the specified location.
Examples:
nodename -HISTREG $LS16->.370 FOR 12345
00002
00003
00001
Format:
HMI [hmilist]
Parameters:
hmilist    is one or more userids separated by commas.  Each userid is either
a hexadecimal user number preceded by a period or a decimal sysid.
Description:
This command produces a formatted display of a Handler/Monitor Interface
Context Block.  If hmilist is omitted, all entries in the HMI table that are
in use are displayed.  If 0 is specified for hmilist, all used and unused
entries in the table are displayed.
00002
00001
The host commands are:  text, ASR, AUTO, BANNER, CFUS, CG, CGLOG, CGMSUMMARY,
CSSTATS, CGSUMMARY, CPU, CPUS, DATA_CACHE, DCBS, DCT, DDT, DELTA, DFRBLKS,
DOMAIN, DQH, DTREE, DUMP, ENQALL, ENQUEUE EVBUF, FEI, GARB, GATE, GODELTA,
HISTREG, IOCACHE, IOQ, JIT, K$ICQ, K$OCQ, LDCT LLIST, MLH, MMD, MPDUMP,
MSGLIST, PSR, QTREE, QUEUE, RAT, RECOVERY, RESOLVE, ROUTE, RUE, RVBUFF, SCHED,
SCTX, SPROC, SPY, SQH, SSFRAME, STREE, TCB, TCTX, TTREE, UNDELTA, USRTABLES,
and WHO_HAS.
For a one-line description of a particular command, enter:
HELP (ANLZ) HOST_COMMANDS command.
For a one-line description of all commands, enter: ??.
For complete HELP for each command, enter:
HELP (ANLZ) command.
  Command     Description
  {:|>}text
              Passes text to DELTA as a command; then returns to ANLZ.
  ASR
              Sets Argument Stack Register for mapping of $ASn locations.
  AUT[O]
              Produces octal dump of auto stack.
  BAN[NER]
              Writes a print block banner for a crash dump.
  CFU[S]
              Displays Current File Usage tables.
  CG
              Sets the current comgroup; or requests comgroup displays.
  CGL[OG]
              Displays comgroups history log.
  CGMS[UMMARY]
              Displays summary of memory usage and allocation for all open
              comgroups.
  CGST[ATS]
              Displays the number of words of memory that are free and in use
              for each open comgroup.
  CGS[UMMARY]
              Displays summary of open comgroups.
  CPU
              Selects CPU to be examined in multi-processing systems.
  CPUS
              Displays CPU number, port number, and state of each CPU in the
              system.
  DATA [CACHE]
              Displays data cache for current comgroup.
  DCB[S]
              Displays DCBs for selected user(s).
  DCT
              Displays device control tables.
  DDT
              Displays device dependent tables (tape).
  DELT[A]
              Associates ANLZ DELTA.
  DFR[BLKS]
              Displays defer blocks for comgroup.
  DOM[AIN]
              Sets default domain for TCB command.
  DQH
              Displays I/O channel tables.
  DTR[EE]
              Displays data cache tree for current comgroup.
  DU[MP]
              Dumps specified area of memory in octal.
  ENQA[LL]
              Displays ENQ-DEQ tables.
  ENQ[UEUE]
              Displays active ENQ-DEQ tables.
  EVB[UF]
              Displays event buffer and connect fault data.
  FEI
              Displays information from the FEP/HOST interface tables.
              Displays OUTSYM's device/event history buffer.
  GAR[B]
              Displays garbage collection data for current comgroup.
  GAT[E]
              Displays two words of memory formatted as a gate.
  GOD[ELTA]
              Transfers control to ANLZ DELTA to read commands.
  HIS[TREG]
              Displays history registers.
  IOC[ACHE]
              Displays I/O cache tables.
  IOQ
              Displays I/O request queues.
  JIT
              Displays selected items from the Job Information Table for
              selected user(s).
              Displays messages from the Input Circular Queue for a local FEP
              table.
              Displays messages from the Output Circular Queue for a local FEP
              table.
  LDCT
              Displays Logical Device Tables.
  LLIST
              Dumps the nodes of a linked list.
  MLH
              Displays message list headers for current comgroup.
  MMD
              Displays memory management data for current comgroup.
  MPD[UMP]
              Dumps private pages for CPUs other than current CPU.
  MSG[LIST]
              Displays list of MBLKs for current comgroup.
  PSR
              Sets Program Stack Register for mapping of $PSn location.
  QTR[EE]
              Displays anonymous queue tree for current comgroup.
  QUE[UE]
              Displays anonymous queue for current comgroup.
  RAT
              Displays resource allocation tables.
  REC[OVERY]
              Displays formatted host recovery buffer.
  RES[OLVE]
              Attempts to resolve an address expression to a virtual address
              and working space quarter number, and to a real memory address.
  ROUTE
              Displays network routing information.
  RUE
              Reports a scheduler event for a specified user.
  RVB[UFF]
              Dumps recovery buffer.
  SCH[ED]
              Displays scheduler state chains.
  SCTX
              Displays OSI Session Context Table entries.
  SPR[OC]
              Displays shared processor tables.
  SPY
              Displays selected host users.
  SQH
              Produces a formatted display of the Subsystem Queue Headers
              (SQHs) for the I/O system.
  SSF[RAME]
              Produces formatted display of safe store frame.
  STR[EE]
              Displays station tree for current comgroup.
  TCB
              Displays Task Control Block for selected user(s).
  TCTX
              Produces a summary display of the Transport Context Table.
              Displays the tree table in the Read-Only Segment.
  TTR[EE]
              Displays message type tree for current comgroup.
  UND[ELTA]
              Disassociates ANLZ DELTA.
  USR[TABLES]
              Displays user tables.
  WHO HAS
              Displays a list of users who have a specified file open.
00002
00003
00004
00005
00006
00007
00008
00010
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
00022
00024
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
00001
  Name         Segment ID      Description
$ASn         (4xxx)          Argument Stack descriptor "n".
$LSn         (6xxx)          Linkage Segment descriptor "n".
$PSn         (0xxx)          Parameter Stack descriptor "n".
AS$          (6053) $LS43    Monitor Argument Stack Descriptor
ASLLS$       (6033) $LS27    UUDR for ASL's LS
BUF$         (6002) $LS2     UUDR for File Mgmt Buffer Segment
CGCTXT$      (6164) $LS116   CG Context & Address Block Area
CGPT$        (6163) $LS115   Comgroup Page Table
CPGT1$       (6075) $LS61    Page Table for CWSQ No. 1
CPGT2$       (6076) $LS62    Page Table for CWSQ No. 2
CPGT3$       (6077) $LS63    Page Table for CWSQ No. 3
CPGT4$       (6100) $LS64    Page Table for CWSQ No. 4
CPGT5$       (6101) $LS65    Page Table for CWSQ No. 5
CPGT6$       (6102) $LS66    Page Table for CWSQ No. 6
CPGT7$       (6103) $LS67    Page Table for CWSQ No. 7
CPGT8$       (6104) $LS68    Page Table for CWSQ No. 8
CPGT9$       (6105) $LS69    Page Table for CWSQ No. 9
CPGT10$      (6106) $LS70    Page Table for CWSQ No. 10
CPGT11$      (6107) $LS71    Page Table for CWSQ No. 11
CPGT12$      (6110) $LS72    Page Table for CWSQ No. 12
CPGT13$      (6111) $LS73    Page Table for CWSQ No. 13
CPGT14$      (6112) $LS74    Page Table for CWSQ No. 14
CPGT15$      (6113) $LS75    Page Table for CWSQ No. 15
CPGT16$      (6114) $LS76    Page Table for CWSQ No. 16
CPLS$        (6034) $LS28    UUDR for CP's LSNo.
CWSQ1$       (6055) $LS45    Communications WSQ No. 1
CWSQ2$       (6056) $LS46    Communications WSQ No. 2
CWSQ3$       (6057) $LS47    Communications WSQ No. 3
CWSQ4$       (6060) $LS48    Communications WSQ No. 4
CWSQ5$       (6061) $LS49    Communications WSQ No. 5
CWSQ6$       (6062) $LS50    Communications WSQ No. 6
CWSQ7$       (6063) $LS51    Communications WSQ No. 7
CWSQ8$       (6064) $LS52    Communications WSQ No. 8
CWSQ9$       (6065) $LS53    Communications WSQ No. 9
CWSQ10$      (6066) $LS54    Communications WSQ No. 10
CWSQ11$      (6067) $LS55    Communications WSQ No. 11
CWSQ12$      (6070) $LS56    Communications WSQ No. 12
CWSQ13$      (6071) $LS57    Communications WSQ No. 13
CWSQ14$      (6072) $LS58    Communications WSQ No. 14
CWSQ15$      (6073) $LS59    Communications WSQ No. 15
CWSQ16$      (6074) $LS60    Last Communications WSQ No. 16
DBLS$        (6032) $LS26    UUDR for Debugger LS
DS1$         (6004) $LS4     Data Segment 1 (For a user, this is AUTO)
DS2$         (6005) $LS5     Data Segment 2 (For a user, this is COMMON)
DS3$         (6006) $LS6     Data Segment 3
DS4$         (6007) $LS7     Data Segment 4
DS5$         (6010) $LS8     Data Segment 5
DS6$         (6011) $LS9     Data Segment 6
DS7$         (6012) $LS10    Data Segment 7
DS8$         (6013) $LS11    Data Segment 8
ECCB$        (6016) $LS14    Descriptor of ECCB Area
FIRM$        (6157) $LS111   For MPC Firmware Loading
IS$          (6000) $LS0     Instruction Segment
JIT$         (6001) $LS1     UUDR for the JIT
JITPG$       (6115) $LS77    Entire JIT Page
LDCT$        (6013) $LS11    LDCT Data Segment (DS8)
LOWMEM$      (6121) $LS81    Low 256K of Real
LS$          (6035) $LS29    Linkage Segment
MAGICAS$     (6167) $LS119   MAGIC AS
MAGICECCB$   (6172) $LS122   MAGIC ECCB
MAGICLS$     (6166) $LS118   MAGIC LS
MAGICPS$     (6170) $LS120   MAGIC PS
MAGICSS$     (6165) $LS117   MAGIC SS
MAGICTCB$    (6171) $LS121   MAGIC TCB
MASTERHJIT$  (6145) $LS101   Master CPU HJIT
MASTERPT$    (6135) $LS93    Master CPU Page Table
MHJIT$       (6043) $LS35    Monitor HJIT
MJIT$        (6042) $LS34    Monitor JIT
MONSS$       (6044) $LS36    Type 0 Descriptor for Monitor SSS
MPT$         (6037) $LS31    Monitor Page Table
MTSTACK$     (6041) $LS33    UUDR for Monitor TSTACK in JIT
PPUT$        (6116) $LS78    M$PPUT - Physical Page Chain
REAL$        (6021) $LS17    Frames Real Pgs 0-7
RO$ or ROS$  (6003) $LS3     UUDR for Read-only Segment
SBUF1$       (6046) $LS38    UUDR for Special Buffer No. 1
SBUF2$       (6047) $LS39    UUDR for Special Buffer No. 2
SLV1HJIT$    (6146) $LS102   Slave No. 1 HJIT
SLV1PT$      (6136) $LS94    Slave No. 1 Page Table
SLV2HJIT$    (6147) $LS103   Slave No. 2 HJIT
SLV2PT$      (6137) $LS95    Slave No. 2 Page Table
SLV3HJIT$    (6150) $LS104   Slave No. 3 HJIT
SLV3PT$      (6140) $LS96    Slave No. 3 Page Table
SLV4HJIT$    (6151) $LS105   Slave No. 4 HJIT
SLV4PT$      (6141) $LS97    Slave No. 4 Page Table
SLV5HJIT$    (6152) $LS106   Slave No. 5 HJIT
SLV5PT$      (6142) $LS98    Slave No. 5 Page Table
SLV6HJIT$    (6153) $LS107   Slave No. 6 HJIT
SLV6PT$      (6143) $LS99    Slave No. 6 Page Table
SLV7HJIT$    (6154) $LS108   Slave No. 7 HJIT
SLV7PT$      (6144) $LS100   Slave No. 7 Page Table
TCB$         (6017) $LS15    Descriptor of TCB
TIGR$        (6123) $LS83    TIGR data
TSTACK$      (6020) $LS16    UUDR for TSTACK in JIT
UPT$         (6036) $LS30    User Page Table
USERHJIT$    (6045) $LS37    UUDR for User HJIT
USERIS$      (6040) $LS32    UUDR for Instruction Segment
USERLS$      (6031) $LS25    UUDR for User LS
USERSS$      (6022) $LS18    UUDR for Safe Store Stack Area
WINDOW$      (6052) $LS42    Window Area for Mapping Phy Pgs.
Format:
INT[CON] [intlist]
Parameters:
intlist    is one or more interrupt level numbers separated by commas.  An
interrupt level number can be specified as either a hexadecimal number
preceded by a period or a decimal number.
Description:
This command produces a formatted display of the Interrupt Control Table.  If
intlist is omitted, the entire Interrupt Control Table is displayed.
00002
00001
The ANLZ program is first invoked by entering:
ANLZ [dumpfile[,symbolfile]]
dumpfile    is one of the following:
    fid    identifies the dump file to be examined.  The fid value may be the
    full name of a dump file, the three digit sequence number of a dump file
    in :SYSTAC, or the four character boot id and sequence number of a dump
    file in :SYSTAC.
    @    continues examining in the same place when a new symbol file is
    selected (running system or dump file).
    LAST    examines the last dump file created on the system.
    NEXT    examines the dump file following the currently analyzed one.
    PREV    examines the dump file preceding the currently analyzed one.
    RUNNING    examines the running system.  The default is RUNNING.
symbolfile    is the name of the run unit to use for ENTDEF/SYMDEF searches.
If no symbolfile is specified, ANLZ uses M:MON.:SYS if looking at the host,
and M:FEP.:SYS if looking at a FEP.  If symbolfile is specified, the named
file is used regardless of whether ANLZ is looking at the host or a FEP.
ANLZ permits entry of multiple commands per line; commands must be separated
by the semi-colon.  However, the ANLZ and SELECT commands may be preceded but
not followed by one or more commands on the same line.  ANLZ also permits
commands to be entered on multiple lines; the semi-colon indicates
continuation.
Format:
IOC[ACHE] [entry_list] [STATISTICS]
Parameters:
entry_list    specifies a list of decimal or octal numbers identifying the I/O
cache entries.
STATISTICS    specifies that the accumulated statistics are to be displayed.
Description:
This command displays I/O cache table items.  This table reflects the granules
currently in the I/O cache.  If no entry_list is specified, all entries and
all statistics are displayed.
00002
00001
Format:
IOP [ioplist]
Parameters:
ioplist    is the address of one or more IOP's, separated by commas.
Description:
This command produces a formatted display of a Host/Monitor Interface Context
Block.  If ioplist is omitted, all entries in the IOP table that are in use
are displayed.  If the address specified in ioplist is 0, all used and unused
entries in the IOP table are displayed.
00002
00001
Format:
IOPC[HECK]
Description:
This command causes ANLZ to inspect the chain of free I/O Packets and report
any inconsistency.  Current use count, peak use count and maximum use count
are displayed.
00001
Format:
IOQ [[*]location|ALL]
Parameters:
*    specifies that the location is to be the head of a queue of I/O requests.
location    is the address of an I/O request packet.  If location is omitted,
the I/O requests queued on each device are displayed.
ALL    requests display of all IOQ packets.
Description:
This command produces a formatted display of all selected I/O request packets.
This command may be used to display all current I/O requests for each local
device, a particular I/O request packet or a particular queue of I/O request
packets.
If no options are specified, then I/O requests queued on each device are
displayed.  The IOQ packet display items are:
  Item           Meaning
DCTX           DCT index of requested device.
FC             Logical function code.
FL$            Pointer to next IOQ packet in chain.
IOF            IO flags.
IOS$           Pointer to associated IOS (NI$REQ) packet.
OPF            OP flags.
BDM            Mirrored Disk flags: (B) bypass mirrored
               disk processing; (D) do mirrored disk
               processing; (M) first mirrored disk
               processing has been done.
REQ$           Address of this IOQ packet.
STATUS         Status word 0 from last attempt at this IO.
Examples:
nodename -IOQ
nodename -IOQ *N$FQ$->2 "This displays free IOQ packets"
00002
00003
00001
Format:
ISA location [FOR userid] ['title']
Parameters:
location    is an address expression for the starting location of the area to
be formatted as an Interrupt Save Area (ISA).
userid    is either a hexadecimal user number preceded by a period, a decimal
sysid, or CUN.  CUN requests ISA formatting for the current user at the time
of a screech.
'title'    specifies the title text that is to be placed in the page header
and table of contents.  (See the CONTENTS Command.)
Description:
This command formats an area of memory as an Interrupt Save Area.
Examples:
nodename -ISA UHJIT$->0 FOR .2
00002
00003
00001
Format:
JIT[,DCBS][,TCB] [uselect_list]
Parameters:
DCBS    performs the DCBS command for selected users.
TCB    performs the TCB command for selected users.
uselect_list    specifies the user selection criteria separated by commas.
For a list of options type HELP (ANLZ) USELECT.  If uselect_list is omitted,
all currently logged on users are displayed.
Description:
This command produces a display of selected information from the user's Job
Information Table.
Examples:
nodename -JIT ME
00002
00003
00001
Format:
JIT [useridlist]
Parameters:
useridlist    is one or more userids separated by commas.  Each userid is
either a hexadecimal user number preceded by a period, a decimal sysid, or
CUN.  CUN requests a JIT display for the current user at the time of a
screech.
Description:
This command produces a formatted display of the selected user(s) Job
Information Table.  If useridlist is omitted, the JITs for all currently
logged on users are displayed.
00002
00001
\K$ICQ
\K$OCQ
\K$RCQ_FEP
\K$SCQ_FEP
\KN$TCTX_FEP
Format:
LCT channel [WITH {ASCII }] ['title']
            [     {EBCDIC}]
Parameters:
channel    is the number of any MLCP channel.
WITH ASCII    includes ASCII character representation on the right side of the
dump.
WITH EBCDIC    includes EBCDIC character representation on the right side of
the dump.
'title'    specifies the title text that is to be placed in the page header
and table of contents.  (See the CONTENTS Command.)
Description:
This command produces a hexadecimal dump of the Line Control Table for a
particular channel.
Examples:
nodename -LCT .1C00
00002
00003
00001
Format:
LDCT [optionlist]
Parameters:
optionlist    specifies one or more of the following separated by commas:
  Option         Description
name           Device name, which can be wildcarded.
number         DCT index.
The default is all LDCTs.
Description:
This command displays the specified Logical Device Control Tables.
Examples:
nodename -LDCT LP01,55,FT?
00002
00003
00001
Format:
LDCTC[HECK]
Description:
This command causes ANLZ to inspect the chain of LDCTs and report any
inconsistency.  Current use count, peak use count and maximum use count are
displayed.
00001
Format:
LDCT [ldctlist]
Parameters:
ldctlist    is the address or index for one or more LDCTs, separated by
commas.
Description:
This command produces a formatted display of the Logical Device Control Table.
If ldctlist is omitted, all entries in the LDCT table that are in use are
displayed.  If 0 is specified for ldctlist, all used and unused entries are
displayed.
00002
00001
LDCT
Format:
LIST [type]
Parameters:
type    is an alphanumeric 2-character value.
Description:
This command lists the dump files in the :SYSTAC and :SYSTAC2 accounts.  Only
those dump files whose names adhere to the dump file naming convention are
listed.  The listing for each file contains the dump file name and associated
screech code.
If type is specified, only those files whose type matches the specified type
are listed.
00002
00001
LLIST_HOST
Format:
LL[IST] location[,size] [{@ } lpx] [[WITH] A[SCII]] ['title']
                        [{AT}    ]
Parameters:
location    is the start of the first node to be dumped.
size    is the size of the node.
lpx    is the word position (origin 0) of the link pointer which contains the
node.  The default is 0.
WITH ASCII    includes the ASCII representation of the characters on the
right.
'title'    specifies the title text that is to be placed in the page header
and table of contents (see HELP (ANLZ) CONTENTS).
Description:
The LLIST command dumps the nodes of a linked list.  The nodes are considered
to be 'size' long with the first node starting at 'location'.  The doubleword
at word offset 'lpx' from the current node is considered to be a pointer to
the next node.
Example:
LLIST NK_FHD$->0,.30 @4
This command will dump all of the LDCTs on the free chain.
00002
00003
00001
Format:
LL[IST] location[,size] [{@ } lpx] [[WITH] A[SCII]] ['title']
                        [{AT}    ]
Parameters:
location    is the start of the first node to be dumped.
size    is the size of the node.
lpx    is the word position (origin 0) of the link pointer which contains the
node.  The default is 0.
WITH ASCII    includes the ASCII representation of the characters on the
right.
'title'    specifies the title text that is to be placed in the page header
and table of contents (see HELP (ANLZ) CONTENTS).
Description:
The LLIST command dumps the nodes of a linked list.  The nodes are considered
to be 'size' long with the first node starting at 'location'.  The word at
word offset 'lpx' from the current node is considered to be a pointer to the
next node.
Example:
LLIST NK_FHD$->0,.30 @4
This command will dump all of the LDCTs on the free chain.
00002
00003
00001
In host and FEP commands, the term 'location' describes an address expression
composed of operators and terms.  The following operators may be used:
                      Operator
Operation             Symbol
---------             --------
Addition                 +
Subtraction              -
Multiplication           *
Division                 /
Location identifier      ->
The four arithmetic operators will affect only the word offset portion of a
host address expression.
The terms that may be used are:
o   Numbers (decimal, hexadecimal or octal)
    See HELP (ANLZ) NUMBER
o   External symbol definitions (SYMDEFs or ENTDEFs)
In addition, the first term in an address expression may be a special segment
symbol.  See HELP (ANLZ) HOST_SEGMENT_NAMES for the special symbols that can
precede an address expressed to identify a segment in the host.  See HELP
(ANLZ) FEP_SEGMENT_NAMES for the special symbols that can be used in FEP
address expressions.
Format:
MAP
Description:
This command produces a formatted display of the Physical Page Table, along
with information to indicate where the pages are mapped; i.e., in a user's
ASDT, in the shared file tables or as an HHJIT page.  This command is intended
to be used with FEP dumps; use of this command on a running FEP will give
unpredictable results.
00001
Format:
MDCT [ ALL | DPxx [, DPyy, ...]]
Parameters:
ALL    specifies all disk devices on the system.
DPxx, DPyy, ...    specifices a list of disk devices to be displayed.
Description:
The MDCT command is used to display the Mirrored Disk information for
specified disk devices on the system.
Device control table item headers are as follows:
  Header         Description
DCTX           Device control table (DCT) index.
DEVNAME        Device name.
MIR            Mirrored Disk indicator. If not YES, then remainder of
               entries are not valid.
MDCTX          DCTX of mirror for this device.
STATE          Mirrored Disk state for this device.
UTS            Mirrored Disk creation time.
LOCK           Mirrored Disk lock indicator U# and LQ$ are valid only
               if LOCK is YES.
U#             User who locked this Mirrored Disk.
LQ$            Pointer to Mirrored Disk locked queue.
DRZERO         Minimum granule number actually mirrored on this device.
Examples:
nodename -MDCT DP01,DP1?
nodename -MDCT 7
00002
00003
00001
Format:
MEM[ORY]
Description:
This command displays the current memory allocation in the FEP.
00001
Service (0) precedes the non-blank portion of the last formatted output field
with a period.  This is used throughout ANLZ to distinguish octal numbers from
decimal ones.  For example, %4O%E would display the decimal value (12) in four
columns as " .14".
Format:
MLCP channel location[,size] [WITH {ASCII }] ['title']
                             [     {EBCDIC}]
Parameters:
channel    is the number of any channel on the MLCP.
location    is an address expression that specifies the starting address of
the dump.
size    is a value expression that specifies the number of words to dump.
WITH ASCII    include ASCII character representation on the right side of the
dump.
WITH EBCDIC    include EBCDIC character representation on the right side of
the dump.
'title'    specifies the title text that is to be placed in the page header
and table of contents.  (See the CONTENTS Command.)
Description:
This command produces a hexadecimal dump of an area of MCLP memory.
Examples:
nodename -MLCP .2480 .0,.20 EBCDIC
00002
00003
00001
Format:
MLH [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays all of the message list headers and information about
each one for the current comgroup.
00002
00001
Format:
MMD [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays memory management information for the current comgroup.
00002
00001
The FMT command operates by calling X$FORMAT with a format string called
DBD$FMT, passing the channel table for the desired device in the first data
buffer and the channel table for its base channel in the second data buffer.
DBD$FMT produces no display output, but instead looks at items in the channel
table like RES, ATTR, TERMID.TTYP and TERMID.LVL, and selects a format string
name to push into the LIFO stack along with the context address from the
channel table.  Adding displays for a new handler thus consists of building
format strings for the handler data with CRAWDAD.X, and modifying DBD$FMT to
select the new format string when appropriate.  The source for DBD$FMT is in
DBD$CHN.:LIBRARY.  Since the handler data usually contains the only link
between the channel table and any VDH context, it is the responsibility of the
format string(s) for the handler data to request an edit routine service (1)
for the KV$VDI Format string, providing as a location the address of the
KV$VDI context for the device.  For example, if KV$VDI is pointed to by a
pointer at word two of the context, the following string could be used:
    '%2..4P' /* position to the pointer (byte 4 = Fep word 2 = Host word 1) */
    '%1.@NE%(KV$VDI%)'        /* CNT(0)=1, CNT(1)=the Fep pointer at word 2 */
Format:
MPD[UMP]
Description:
This command dumps the private pages for CPUs other than the current CPU.  The
dump includes the monitor page table, monitor HJIT, monitor JIT, monitor
TSTACK, and processor page.  The purpose of this command is to facilitate
dumping of the CPUs other than the one on which the screech occurred.
00001
Format:
MSG[LIST] location[,n]
Parameters:
location    is an address expression.
n    is the number of messages to dump.  The default is all remaining
messages.
Description:
This command displays a list of messages (MBLKs) for a comgroup starting at
the specified location.
00002
00001
The term "number" can be entered in any of the following formats:
  Format    Value
ddd       Decimal
O'ooo'    Octal
X'xxx'    Hexadecimal
 .nnn     Octal/hexadecimal.  That is, a number
          entered in this format will be treated as octal
          when a host node is selected and hexadecimal when
          a FEP node is selected.
Format:
         [[ON  ] LP[@location]]
OU[TPUT] [[OVER] fid          ] [(option[,option]...[)]]
         [[INTO] ME           ]
         [[TO  ]              ]
Parameters:
{ON|TO|OVER|INTO}    directs file output processing.  OVER causes an existing
file to be overwritten.  INTO causes file extension.  ON and TO are synonyms
used to create a new file.  If the file exists, an error will occur.  The
default is ON.
fid    any valid CP-6 file identifier.
LP    directs output to the default line printer.  @location identifies a
specific line printer.
ME    redirects output to the user's terminal.
option    is one of the following:
    F[ORM]={formname|'formname'}    Applies to unit record files and unit
    record devices and specifies the name of a form to be mounted on a unit
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
Examples:
nodename -OUTPUT ON OUTPUTFILE
nodename -OUTPUT ON ME
00002
00003
00001
For information on the ANLZ parameters, see:
HELP (ANLZ) SIZE_PARAMETER
HELP (ANLZ) LOCATION_PARAMETER
HELP (ANLZ) USELECT_LIST_PARAMETER
HELP (ANLZ) NUMBER_PARAMETER
Format:
PL[UGH] address_expression [FOR userid]
Parameters:
address_expression    specifies the address of the base of the auto stack or
TSTACK.
userid    is either a hexadecimal user number preceded by a period, a decimal
sysid, or CUN.  CUN requests a PLUGH display for the current user at the time
of a screech.
Description:
The PLUGH (Procedure List Used to Get Here) command displays the chain of
procedure calls which led to the arrival of the Instruction Counter at the
current point.  The source for the procedure list is the user's automatic
stack.  The currently active frame is displayed first.  The call address and
offset into the stack segment are displayed for each frame.
Example:
!ANLZ
ANLZ E02
L66B (node 20) Selected
L66B     -ANLZ C098
 :DFE02C098.:SYSTAC for GHT-001314-3 at 13:30 APR 17 '90 on LADC L66B
 JP is to blame
 Nodes:      L66B      L6IX
L6IX (node 9) Selected
L6IX     -SPY
M Usr#  Identification           Sysid     CPU     M$LM
H . 1   :SYS,NODEADMN                1    0:02     NODEADMN.:SYS
H . 2   :SYS,COUPLER                 2    0:02     COUPLER.:SYS
H . 3   :SYS,ASYNC                   3    0:03     ASYNC.:SYS
H . 4   :SYS,BISYNC                  4    0:01     BISYNC.:SYS
H . 5   :SYS,HDLCX25                 5    0:01     HDLCX25.:SYS
H . 6   :SYS,MHDLCX25                6    0:01     MHDLCX25.:SYS
L6IX     -SYM BISYNC.:SYS
L6IX     -PLUGH .D000 F 4
Header at .D7FA, CW=.681, MW=.7ED
Stack displayed from bottom frame to top frame:
Frame @.D00F called from .24228 (KZI$INIT+.0)
Frame @.D020 called from .242DF (KZI$INIT+.B7)
Frame @.D179 called from .EC5FE (Y_SND_DAT.395)
L6IX     -Q
!
00002
00003
00001
Format:
PPUT [pputlist]
Parameters:
pputlist    is one or more physical page numbers, separated by commas.
Description:
This command causes ANLZ to inspect the Physical Page Table and report any
inconsistency when no pputlist options are specified.  If the pputlist option
is used, the Physical Page Table entries for the pages specified are
displayed.  If page 0 is specified in the pputlist, all entries in the
Physical Page Table are displayed.
00002
00001
Format:
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
Examples:
nodename -PRINT LP01,LP02
The above example causes the accumulated output associated with logical
devices LP01 and LP02 to be sent immediately to the associated destinations.
00002
00003
00001
Use of ANLZ requires that users be authorized for SPCLMM privilege.  If a FEP
is to be ANLZed, the user must be authorized for FEP SPCLMM privilege.
Format:
PSR [location ]
    [*location]
Parameters:
location    sets PSR to frame from location to the end of the segment.
location is an address expression.
*location    sets PSR to the contents of location and location+1.  location is
an address expression.
If no parameter is given, the current PSR is displayed.
Description:
This command sets the Parameter Stack Register to use during address
resolution when specifying a location as $PSn.
Examples:
nodename -PSR USERHJIT$->.1610
00002
00003
00001
Format:
QTR[EE] [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays the current comgroup's anonymous queue tree and some
information from each node.
00002
00001
Format:
QUE[UE] [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays information about the current comgroup's anonymous
queue.
00002
00001
Format:
    [DP   ]
RAT [MT   ]
    [NPOOL]
Parameters:
DP    is disk devices.
MT    is magnetic tapes.
NPOOL    is non-pooled resources.
Description:
This command produces a formatted display of resource allocation tables.  If
no option is present, all resource allocation tables are displayed.  If an
option is specified, then only entries on that resource chain are displayed.
Resource Allocation Table display items include:
  Header         Description
ACTX           Internal information (B$JIT.ARECX).
ASID           Additional sysid.
DEVNM          Device name of physical resource.
FLG            Flags.
M1             Attributes that resource has.
M2             Attributes that resource owner sees.
NU             Logical resource number if allocated.
RCOD           Resource type (DP, MP, or NPOOL).
RFL            Resource flags.
SER            Serial number (Form for NPOOL).
SOL            Solicit user number.
SSER           Solicit serial number.
SYSID          Sysid of owner if allocated
TY             Resource type.
Examples:
nodename -RAT DP
nodename -RAT
00002
00003
00001
Format:
RCQ [useridlist] [L[AST]]
Parameters:
useridlist    is one or more userids separated by commas.  Each userid is
either a hexadecimal user number preceded by a period, a decimal sysid, or
CUN.
LAST    may be specified to indicate that the contents of the message headers
for the last messages taken off the receive circular queue are to be
displayed.
Description:
This command produces a formatted display of the contents of a user's Receive
Circular Queue.  The circular queue header information is displayed, followed
by the formatted display of the message headers.  If useridlist is omitted,
the RCQ information for all users having a RCQ is displayed.
00002
00001
Format:
READ fid
Parameters:
fid    identifies the file to be read.
Description:
This command reads subsequent commands from the specified file.  (This command
does not affect the source for DELTA commands if the GODELTA command is used.)
Examples:
nodename -READ COMMANDFILE
00002
00003
00001
Format:
REC[OVERY]
Description:
This command displays formatted recovery buffer information.  The screech
code, screeching processor number, and current user number are displayed along
with a formatted display of the safe store frame that was laid down as a
result of the climb to recovery.
00001
Format:
REC[OVERY]
Description:
This command displays formatted FEP recovery buffer information.  The screech
code, current user number, TSA address and the TSA leading to the screech are
displayed.
00001
RECOVERY
RECOVERY_FEP
RECOVERY
Format:
REP[EAT] [number]
Parameters:
number    is the number of times the commands are to be repeated.  If number
is omitted, the repeat continues until terminated with a BREAK.
Description:
This command repeats all commands preceding the REPEAT command on the same
line.  Multiple commands on a line are separated with semi-colons.
Examples:
nodename -SPY B;WAIT 20;REPEAT 10
00002
00003
00001
Format:
RES[OLVE] location
Parameters:
location    is an address expression.
Description:
This command attempts to resolve an address expression to a virtual address
and working space quarter number, and to a real memory address.  It is not
always possible to complete the resolution to a real memory address.
00002
00001
Format:
ROS [useridlist]
Parameters:
useridlist    is one or more userids separated by commas.  Each userid is
either a hexadecimal user number preceded by a period, a decimal sysid, or
CUN.
Description:
This command produces a display of the Read-only Segment header information
for the selected user(s).  If the useridlist is omitted, the ROS header
information is displayed for all users.
00002
00001
Format:
ROUTE [nodelist]
Parameters:
nodelist    is one or more node numbers separated by commas.
Description:
This command displays the network routing information for the specified node
or nodes.  Node names cannot be used.  If no node number is specified, the
entire routing table is displayed.
00002
00001
Format:
ROUTE [nodelist]
Parameters:
nodelist    is one or more node numbers separated by commas.
Description:
This command displays the network routing information for the specified node
or nodes.  Node names cannot be used.  If no node number is specified, the
entire routing table is displayed.
00002
00001
ROUTE
Format:
RUE event [uselect_list]
Parameters:
event    one of the following events:
    ABRT    AP    APA    AU    CA    CAN    CBA    CBF    CBK    CBL
    CEC     CIC   CRD    CUB   CW    DISC   DISCP  DU     ERR    FC
    FPEVNT  FPLDTRC      IIP   IIPC  IIPCA  IOC    IOCU   MP     NAP
    NC      NQP   NQR    NQW   QA    QC     QE     QMF    QPA    SL
    SLPMME  UQA   UQC    WU
CAUTION:  This command is intended primarily for use by Bull personnel.
Misuse of this command can easily corrupt the operation of the CP-6 system,
causing either an immediate system recovery, or delayed and possibly difficult
to diagnose symptoms.
See Description before using these events.
uselect_list    specifies user selection criteria separated by commas.  For a
list of options, type: HELP (ANLZ) USELECT_LIST.  The default is all users.
Description:
This command reports the specified scheduler event on the selected users.  Use
of the RUE command requires the MSYS privilege.
There are two events that may safely be reported on any user, other than
system ghosts, at any time.  The ABRT event has the same effect as the
operator's X keyin:  the selected users will be logged off the system.  The
ERR event has the same effect as the operator's E keyin:  the selected users
current job step will be errored.
00002
00001
Format:
RUE event {sysid      }
          {user_number}
Parameters:
event    one of the following:
    ABRT    AP    APA    AU    CA    CAN    CBA    CBF    CBK    CBL
    CEC     CIC   CRD    CUB   CW    DISC   DISCP  DU     ERR    FC
    FPEVNT  FPLDTRC      IIP   IIPC  IIPCA  IOC    IOCU   MP     NAP
    NC      NQP   NQR    NQW   QA    QC     QE     QMF    QPA    SL
    SLPMME  UQA   UQC    WU
CAUTION:  This command is intended primarily for use by Bull personnel.
Misuse of the RUE command can easily corrupt the operation of the FEP
operating system, causing either an immediate system recovery, or delayed and
possibly difficult to diagnose symptoms.
See Description before using these events.
sysid    is a decimal sysid.
user-number    is a hexadecimal number preceded by a period.
Description:
This command reports the specified scheduler event on the selected user.  The
RUE command requires MSYS privilege.
There are two events that may safely be reported on any user, other than
system ghosts, at any time.  The ABRT event has the same effect as the
operator's X FEP keyin:  the selected user is removed from the system.  The
ERR event has the same effect as the operator's E FEP keyin:  the selected
user's current job step is errored.
00002
00001
RUE
Format:
RVB[UFF]
Description:
This command produces an octal dump of the recovery buffer.
00001
Format:
SCH[ED]
Description:
This command produces a display of scheduler state chains.  The name of the
state for each non-empty state chain is displayed, followed by a list of user
numbers in octal for each user in that state.
00001
  Mnemonic       Meaning
QRCQ           Queued for communications circular queue
QRIO           Queued for I/O packet
QRMM           Queued for memory pages
QRNQ           Queued for Enqueue/Dequeue resource
SCn            Compute 1 (SC1) through Compute 11 (SC11)
SCU            Current User
SCW            Communication Wait
SDSC           Disconnecting
SIOCACHE       I/O cache wait
SIOMF          Blocked for master function
SIOW           I/O wait
SIOWC          Communication I/O wait
SNULL          Null User
SQA            Queued for access
SQC            Queued for I/O CACHE
STI            Terminal Input
STOB           Terminal output blocked
SW             Wait
Format:
SCQ [useridlist] [L[AST]
Parameters:
useridlist    is one or more userids separated by commas.  Each userid is
either a hexadecimal user number preceded by a period, a decimal sysid, or
CUN.
LAST    may be specified to indicate that the contents of the message headers
for the last messages taken off the send circular queue are to be displayed.
Description:
This command produces a formatted display of the contents of a user's Send
Circular Queue.  The circular queue header information is displayed, followed
by the formatted display of the message headers.  If useridlist is omitted,
the SCQ information for all users having a SCQ are displayed.
00002
00001
Format:
SCTX [sctxlist]
Parameters:
sctxlist    is a comma-separated list of one or more SCTX entries.
Description:
This command produces a summary display of the OSI Session Context Table.  If
sctxlist is omitted, currently active entries in the SCTX table are displayed.
If sctxlist is specified as 0, all entries are displayed.  Otherwise, each
SCTX entry listed in sctxlist is displayed.
00002
00001
Format:
SEL[ECT] node
Parameters:
node    specifies whether the host or a FEP is to be analyzed.  The value
specified is a HOST or FEP number or name.
Description:
This command specifies that the host is to be examined, or specifies which FEP
to examine (in the current dump file or the running system).  When ANLZing the
running system the host is selected by default.  For dump files, the node that
initiated the screech is selected.
This command may be preceded but not followed by other commands on the same
line.
Examples:
nodename -SELECT HOST
nodename -SELECT 1
00002
00003
00001
Format:
SFI[LES] [filelist]
Parameters:
filelist    is one or more shared file identifiers separated by commas.  Each
shared file identifier is either a hexadecimal file number preceded by a
period or a decimal file number.
Description:
This command produces a formatted display of selected entries in the Shared
File Table.  If filelist is omitted, the entire Shared File Table is
displayed.
00002
00001
In host and FEP commands, the term 'size' defines a value expression composed
of operators and terms.  The following operators may be used:
                     Operator
Operation             Symbol
---------             --------
Addition                 +
Subtraction              -
Multiplication           *
Division                 /
Location identifier      ->
The pointer operator (represented by the composite symbol ->) specifies the
contents of the current location.  For host value expressions, the value of
the portion of the expression to the left of the pointer operator will be used
as an offset into the monitor instruction segment.  For FEP expressions, the
left operand of a pointer evaluation is an address in the monitor virtual
space.
The terms that may be used in value expressions are:
o   Numbers (decimal, hexadecimal or octal)
    See HELP (ANLZ) NUMBER
o   External symbol definitions (SYMDEFs or ENTDEFs)
Format:
SPR[OC] [optionlist]
Parameters:
optionlist    is a comma-separated list of one or more items from the
following table.
  Option         Description
 .acct         Display all processors in account .acct.
~.acct         Display all processors not in account .acct.
name           Name of processor (may be wildcarded).
number         A processor number.
Description:
This command displays information contained in the shared processor table for
selected processors.
Examples:
nodename -SPROC IBEX?
nodename -SPROC ANLZ
nodename -SPROC
00002
00003
00001
Format:
SPY [uselect_list]
Parameters:
uselect_list    specifies user selection criteria separated by commas.  For a
list of options type HELP (ANLZ) USELECT.  If uselect is omitted, all
currently logged on users are displayed.
Description:
This command produces a display of selected users.  The information displayed
is obtained by mapping to each selected user's job information table.
Examples:
nodename -SPY CCBUF=PL6?
nodename -SPY BOG
00002
00003
00001
Format:
SPY [useridlist]
Parameters:
useridlist    is one or more userids separated by commas.  Each userid is
either a hexadecimal user number preceded by a period, a decimal sysid, or
CUN.  CUN requests a SPY display for the current user at the time of a
screech.
Description:
This command produces a formatted display of users.  The information displayed
is obtained by mapping to each user's Job Information Table.  If useridlist is
omitted, all currently logged on users are displayed.
00002
00001
SPY
Format:
SQH
Description:
This command produces a formatted display of the Subsystem Queue Headers
(SQHs) for the I/O system.  If the display TYPE field is in uppercase, the SQH
gate is locked.  If the display TYPE field is in lowercase, the SQH gate is
unlocked.
00001
Format:
SSF[RAME] location [{FOR  } {sysid   }[,domain]] ['title']
                   [{USING} {.usernum}         ]
Parameters:
location    is an address expression.
FOR    means use monitor linkage segment.
USING    means use user linkage segment.
sysid    is a decimal number.
 .usernum    is an octal number.
domain    is one of the following:
ASL    Alternate Shared Library
ICP    Interactive Command Processor
IDB    Interactive Debugger
MON    Monitor
USR    User
domain overrides FOR or USING phrase.
'title'    specifies the title text that is to be placed in the page header
and table of contents.
Description:
This command displays 64 words beginning at the specified location as a safe
store frame.
Examples:
nodename -SSFRAME MHJIT$->.540
00002
00003
00001
Format:
SSN [ssnlist]
Parameters:
ssnlist    is the address of one or more Session Context Blocks, separated by
commas.
Description:
This command produces a formatted display of the Session Context Blocks.  If
ssnlist is omitted, all Session Context Blocks that are in use are displayed.
00002
00001
Format:
SSNC[HECK]
Description:
This command causes ANLZ to inspect the chain of free Session Context Blocks
and report any inconsistency.  Current use count, peak use count and maximum
use count are displayed.
00001
Format:
STAR
Description:
This command creates supporting documentation for a STAR for the currently
open dump file.  The CP-6 system is supplied with a file, ANLZ_STAR,
containing a list of commands from which ANLZ performs those commands
appropriate to the type of dump file.  The STAR command attempts to open the
file ANLZ_STAR in the current file management account or, if it does not exist
there, it will open that file in :SYS.
The command is structured so that the key of the report record will be an EDIT
key constructed from the screech code.  The key built for the report record
will vary depending on the screech code.  The key may be:
o   the binary value of the Functional Code Group (FCG) as the integer part
    and the binary value of the Module ID (MID) as the fractional part.
o   the binary value of the FCG as the integer part and zero as the fractional
    part.
o   the value 0.000, if a host node is currently selected or 1.000 if an FEP
    node is currently selected.
The procedure to create the text for the STAR and then create the STAR follows
(see the example below):
1.  Within ANLZ:
    o   Issue an ANLZ command to select the dump file.
    o   Issue a REC command to obtain the screech code and IC
    o   Direct output to a file
    o   Issue the ANLZ command again to put header information in the test
        case file.
    o   Issue the STAR command to obtain relevant information from the dump.
2.  Within STARLOG:
    o   Build a STAR
    o   Enter the screech code and IC from the REC command as the title of the
        STAR.
    o   Include in the description the name of the testcase containing the
        information obtained from the STAR command along with the name and
        location of the dump file.  Also include any relevant information
        concerning the circumstances surrounding the screech.
3.  Send the STAR command output to LADC, using BEAM.X.  The name of the
    testcase should be starnumber_ANLZ.
Example:
!ANLZ
ANLZ E02
L66B (node 20) Selected
L66B     -ANLZ C011
 :DFE02C011.:SYSTAC for UDE-M00501-7 at 15:09 APR 12 '90 on LADC L66B
 CW is to blame
 Nodes:      L66B
L66B (node 20) Selected
L66B     -REC
 SCREECH CODE:
 UDE-M00501-7   Memory fault
 CURRENT USER .26 ON LOGICAL PROCESSOR #0 AT 15:09:47 APR 12 '90
SAFE STORE FRAME:
 WORD 0        WORD 1        WORD 2        WORD 3        TIME STAMP
 ------------  ------------  ------------  ------------  -------------------
 000000000000  000000000000  775710777773  000552404375  011160 511520536163
 IC=MME$VMEM+.677   IR=.004210     MRT=NO    SSF=NO    FLTCODE=1
 CP=0    SCR=3   ISSID=.6000   DSAR=.000000   EWSQ=0   TRAP/AUTO=.577477
 ISR: .200000-0,BD=.777777-3,WSR=0,FL=.757,TY=0
 ASR: .33600-0,BD=.0-0,WSR=7,FL=.741,TY=1
 LSR: .32000-0,BD=.441-3,WSR=0,FL=.543,TY=1
 PSR: .0-0,BD=.0-0,WSR=7,FL=.101,TY=1
 PR0: .324703-0-0,$LS0    DR0: .200000-0,BD=.777777-3,WSR=0,FL=.757,TY=0
 PR1: .0-0-0,$LS78        DR1: .364000-0,BD=.13777-3,WSR=2,FL=.703,TY=0
 PR2: .132-0-0,$LS16      DR2: .26366-0,BD=.3411-3,WSR=7,FL=.743,TY=0
 PR3: .0-0-0,$LS1         DR3: .26000-0,BD=.365-3,WSR=7,FL=.743,TY=0
 PR4: .75412-0-0,$LS83    DR4: .1420000-0,BD=.377777-3,WSR=0,FL=.703,TY=0
 PR5: .404554-0-0,$LS0    DR5: .200000-0,BD=.777777-3,WSR=0,FL=.757,TY=0
 PR6: .3204-0-0,$LS17     DR6: .1200000-0,BD=.17777-3,WSR=0,FL=.703,TY=0
 PR7: .400-0-0,$LS16      DR7: .26366-0,BD=.3411-3,WSR=7,FL=.743,TY=0
 X0      X1      X2      X3      X4      X5      X6      X7
 ------  ------  ------  ------  ------  ------  ------  ------
 213477  324634  777645  000030  000004  003551  000001  707455
 X0: FOM$PMME+.1055
 X1: JSU$RELMEM+.26
 X2: MONECCB+.54732
 X3: S_WSPTD+.30
 X4: S_WSPTD+.4
 X5: F_CWUSER+.0
 X6: S_WSPTD+.1
 X7: XSA$MON+.11
 A: 000000000010    Q: 000005000000     E: 000    TIMER: 000177737000
MORE STUFF FROM THE RECOVERY BUFFER:
SSR: .32600-0,BD=.777-3,WSR=7,FL=.743,TY=1
PSR: .0-0,BD=.0-0,WSR=7,FL=.101,TY=1
ASR: .33600-0,BD=.0-0,WSR=7,FL=.741,TY=1
WSRs: .1,.1,.0,.14,.4,.5,.6,.10
CURRENT COMGROUP: .0-0-0,$PS0
L66B     -OUT ON *STARINFO                "Directs output to file
                                          "*STARINFO."
L66B     -ANLZ C011                       "Puts header information in"
                                          "the file."
L66B     -STAR                            "Obtain STAR information."
L66B     -END
  !STARLOG
   STARLOG C01 15:37:21 TUE APR 12 '90
  #BUILD STAR                               "Builds the STAR."
  Subject name: CENTRAL
  Subject version: E02
  Originator name: John L. Customer
  Severity: 4
  Title: Screech UDE-M00501-7 at MME$VEM+.677   "The screech code and"
  STAR number: 21511                            "IC are included in"
                                                "the STAR file."
  Description:                                  "The description identifies"
                                                "the test case and the"
                                                "location of the dump file."
  -This screech occurs whenever we try to boot FEP 257.  Star info is in
  -21511_ANLZ.ZZZTEST @LADC.  Dump is :DFE02C011.:SYSTAC.
  -
  #END
 !BEAM.X $STARINFO ON 21511_ANLZ.ZZZTEST @LADC  "The test case is"
 ..BEAMing $STARINFO                            "named starnum_ANLZ."
 Enter account,name to run under @L66A or CR    "The BEAM program"
 for JIT account,name.                          "in the X account"
 *ZZZCUST,900DUMMY                              "is used to make"
 Please enter your password @L66a (echo is off) "it available."
 *900DUMMY
 42 records in transmission; approximate time is 1.47
 Your SYSID (on this machine) is 26750-1.
00001
00002
STATUS
SCHEDULER_STATES
Format:
STAT[US] [useridlist]
Parameters:
useridlist    is one or more userids separated by commas.  Each userid is
either a hexadecimal user number preceded by a period, a decimal sysid, or
CUN.  CUN requests a STATUS display for the current user at the time of a
screech.
Description:
This command produces a formatted display of memory usage.  If useridlist is
omitted, memory usage for all users is displayed.
00002
00001
Format:
STR[EE] [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays the station tree (directed queue) and some information
from each node.
00002
00001
Format:
SYM[BOLS] [fid [,node]]
Parameters:
fid    specifies the run unit to be used for SYMDEF/ENTDEF searches and
displays.
node    specifies the overlay node number to use for additional symbols
instead of the shared library, if fid specifies an overlaid run unit.
Description:
This command selects a run unit to be set for SYMDEF/ENTDEF searches and
displays.  If no fid is specified, M:MON.:SYS is searched while looking at the
host, or M:FEP.:SYS is searched while looking at a FEP.  If fid is specified,
the named file is used regardless of whether ANLZ is looking at the host or a
FEP.
If the run unit that the symbol file refers to has a shared library associated
with it, the symbols in the shared library are available unless node is
specified.  Usually, even if the library appears to be of more immediate
interest, results will be more meaningful if the SYMBOL command sets the
symbols to the running program.  For example, PLUGH command results will be
more interesting if symbols are set to the running program than if they are
set to the associated library.
This command is similar to the symbolfile option of the ANLZ command.
00002
00001
Service (6) is used to display a location as "label+offset".  CNT(2) specifies
the location to look up in the symbol tables.  CNT(3) may be used to limit the
maximum acceptable offset value.  The largest PRIMARY ENTDEF or SYMDEF whose
value is less than CNT(2) is determined.  If such a DEF exists and its value
conforms to any CNT(3) specification, its name is inserted into the current
output line, and CNT(2) minus its value (the offset) replaces CNT(0).
Otherwise, CNT(0) is set to minus one to indicate failure to find a symbol.
Then, regardless of the outcome, ANLZ ALTRETURNs to X$FORMAT, so that the
Format string can make use of the new CNT(0) value, most conveniently to
assign its value to a variable.  For example, '%6.n.m#E=' would assign the
offset or minus one to variable-n, based on the look-up of the value in
variable-m.  Then:
    '%n#:1+[%m#.n=%?+%]%.nD'
can be used to display either the original value or "+offset", depending on
the success of the look-up operation.
Service (7) looks up the text parameter in the symbol tables (ENTDEF and then
SYMDEF) and returns the value as a pointer in FDS.USERDAT1.  If the symbol is
not found, the command is aborted with a message indicating the problem.
Format:
TCB[(domain)][,DCBS][,JIT] [uselect_list]
Parameters:
domain    specifies USR (user domain, WSR7), ICP (command processor, WSR4),
IDB (debugger, WSR5), or ASL (alternate shared library, WSR6).  The default is
USR, which may be changed by use of the DOMAIN command.
DCBS    performs the DCBS command for the selected users.
JIT    performs the JIT command for the selected users.
uselect_list    specifies user selection criteria separated by commas.  For a
list of options type HELP (ANLZ) USELECT.
Description:
This command displays the Task Control Block of a specified domain for a
selected user.  The ALTRET frame is formatted and words 64-67 are dumped in
octal.  Following that, the safe store frame from each active exceptional
condition frame is formatted and the remaining words in the exceptional
condition frame are dumped in octal.
Examples:
nodename -TCB(ICP) CUN
nodename -TCB .7
00002
00003
00001
Format:
TCB [useridlist]
Parameters:
useridlist    is one or more userids separated by commas.  Each userid is
either a hexadecimal user number preceded by a period, a decimal sysid, or
CUN.  CUN requests a TCB display for the current user at the time of a
screech.
Description:
This command produces a formatted display of user(s) Task Control Blocks.  If
useridlist is omitted, TCBs for all users are displayed.
00002
00001
TCB
Format:
TCTX [tctxlist]
Parameter:
tctxlist    is the index for one or more TCTXs, separated by commas.
Description:
This command produces a summary display of the Transport Context Table.  If
tctxlist is omitted, all in-use entries in the TCTX table are displayed.  If 0
is specified for tctxlist, all used and unused entries are displayed.
00002
00001
Format:
TCTXC[HECK]
Description:
This command causes ANLZ to inspect the chain of TCTXs and report any
inconsistency.  Current use count, peak use count and maximum use count are
displayed.
00001
TCTXCHECK_FEP
Format:
TCTX [tctxlist]
Parameters:
tctxlist    is the address or index for one or more TCTXs, separated by
commas.
Description:
This command produces a summary display of the Transport Context Table.  If
tctxlist is omitted, all in-use entries in the TCTX table are displayed.  If 0
is specified for tctxlist, all used and unused entries are displayed.
00002
00001
TCTX
Format:
{:}text
{>}
Description:
This command passes the specified text as a command to DELTA.
Examples:
nodename -:M B_SITEINFO+5
nodename -:D B$USRT$->B$USER.US(0:3)
00001
00002
DATE
Format:
TRAPFRAME
Description:
This command displays the safe store frame from the last time ANLZ trapped.
TRAPFRAME is intended as a debugging aid.  Most traps in ANLZ, and
particularly missing page faults, relate to the unavailability of memory
required to execute a command.
00001
\TREE
Format:
TSA location [FOR userid] ['title']
Parameters:
location    is an address expression for the starting location of the area to
be formatted as a Trap Save Area.
userid    is either a hexadecimal user number preceded by a period, a decimal
sysid, or CUN.  CUN requests a TSA display for the current user at the time of
a screech.
'title'    specifies the title text that is to be placed in the page header
and table of contents.  (See CONTENTS (general) Command.)
Description:
This command formats an area of memory as a Trap Save Area.
Examples:
nodename -TSA .4320
00002
00003
00001
Format:
TTR[EE] [F[OR] cgid]
Parameters:
cgid    specifies an octal number that is the word offset of the desired
comgroup's context block from the beginning of the comgroup context area
(B$CGCTXT$).  This value appears in the CTXT @ column of the CGSUMMARY
display.
Description:
This command displays the current comgroup's message type tree and some
information from each node.
00002
00001
Format:
UND[ELTA]
Description:
This command disassociates DELTA.
00001
To list all uselect options, type ??.  To display information on a specific
option, type:
HELP (ANLZ) USELECT option
Valid options are ACCOUNT, ALL, BATCH, CCBUF, FEP, LINE, NAME, STATE, and
usernum.
  Possible USELECT    Explanation
  AC[COUNT] {=acct1|(acct1[, acct2] ... )}
                      Select only users whose B$JIT.ACCN matches one of the
                      possibly wildcarded account names.
  [ALL]
                      Select all active users.  ALL is the default where no
                      other uselect is specified.
  {B[ATCH]|O[NLINE]|G[HOST]|T[P]}
                      Mode of user.  Any or all are permitted, e.g., BATCHTP.
  CC[BUF] {=cc1|(cc1[, cc2] ... )}
                      Select only users whose B$JIT.CCBUF matches one of the
                      possibly wildcard CC names.  If a CCBUF string is to
                      contain a '+' or ',', it must be enclosed in quotes.
  FE[P] {=number|(number1[, number2] ... )}
                      Select only users on the specified Front-end Processors
                      (FEPs).
  LI[NE] {=d-hhhh|(d-hhhh[, d-hhhh] ... )}
                      Select only users on the specified lines.  Number is a
                      combination of decimal FEP numbers (d) and hexadecimal
                      line numbers (hhhh).
  NA[ME] {=name1|(name1[, name2] ... )}
                      Select only users whose B$JIT.UNAME matches one of the
                      possibly wildcarded names.
  ST[ATE] {=state1|(state1[, state2] ... )}
                      Select only users in the specified scheduler states.
                      For a list of state options, type HELP (ANLZ) STATE.
  usernum
                      Either a decimal sysid, an .octal user number, or a
                      screech.
00002
00001
00002
00003
00004
00005
00003
00006
00007
00003
00008
00003
00009
Format:
USR[TABLES] [uselect_list]
Parameters:
uselect_list    specifies user selection criteria separated by commas.  For a
list of options type HELP (ANLZ) USELECT.  The default is all currently logged
on users.
Description:
This command displays user tables for specified users.
Examples:
nodename -USRT STATE=SNULL
nodename -USRT
00002
00003
00001
Format:
USR[TABLES] [userid]
Parameters:
userid    specifies the user portion of an entry in the User Table.  userid is
specified as either a hexadecimal user number preceded by a period, a decimal
sysid, or CUN.  CUN requests a User Table display for the current user at the
time of a screech.
Description:
This command produces a formatted display of entries in the User Table.
If userid is omitted, the entire User Table is displayed.
00002
00001
USRTABLES
USRTABLES_FEP
Format:
WA[IT] n
Parameters:
n    is the number of seconds to wait.
Description:
This command causes a wait of the specified number of seconds.
Examples:
nodename -WAIT 10
00002
00003
00001
Format:
WHO HAS {fid|CG/fid} [OPEN?]
Parameters:
fid    specifies a disk file or comgroup fid.  If a comgroup is specified, it
is specified as CG/fid.
Description:
This command searches the DCBs of all users for the specified fid.  It lists
the users with a DCB that contains the specified fid, or the users that have
the specified fid open if the OPEN option is included in the command.  If the
filename is omitted from the fid, all files with the specified PSN/account are
listed.  A blank account and/or PSN in the fid specification matches any value
in the DCB.  A blank PSN in the DCB matches any specified PSN.
00002
00001
EXIT
Format:
XEQ fid [(optionlist)][, fid(optionlist)] ... ]
Description:
This command inserts all or part of an XEQ file into the command stream and
initiates execution of the contents of the file.  XEQ only can be used if the
command processor is IBEX.  Type HELP (IBEX) XEQ for a description of XEQ.
Examples:
nodename -XEQ XEQFILE PARAM='A,B,C,D'
00001
00002
Format:
\FO_DET FO_DET U 3
Parameters:
FO_DET U 3    should be specified for any invocation of this command.
Description:
This command displays OUTSYM's device/event history buffer.
Examples:
nodename -SYM OUTSYM
nodename -\FO_DET FO_DET U 3
00002
00003
00001
Format:
\FO_DET FO_DET U 3
Parameters:
FO_DET U 3    should be specified for any invocation of this command.
Description:
This command displays OUTSYM's device/event history buffer.
Examples:
nodename -SYM OUTSYM
nodename -\FO_DET FO_DET U 3
00002
00003
00001
Format:
\K$ICQ $LSnn,size
Parameters:
nn    specifies the segment that contains the FEP table.  The value to use may
be determined by using the FEI command.
size    specifies the number of messages to be displayed.  If this parameter
is omitted, all messages in the queue are displayed.
Description:
This command displays messages from the Input Circular Queue for the specified
local FEP table.  The data is displayed in X1 format.
Example:
nodename -\K$ICQ $LS49,20
00002
00003
00001
Format:
\K$ICQ $LSnn,size
Parameters:
nn    specifies the segment that contains the FEP table.  The value to use may
be determined by using the FEI command.
size    specifies the number of messages to be displayed.  If this parameter
is omitted, all messages in the queue are displayed.
Description:
This command displays messages from the Input Circular Queue for the specified
local FEP table.  The data is displayed in X1 format.
Example:
nodename -\K$ICQ $LS49,20
00002
00003
00001
Format:
\K$OCQ $LSnn,size
Parameters:
nn    specifies the segment that contains the FEP table.  The value to use may
be determined by using the FEI command.
size    specifies the number of messages to be displayed.  If this parameter
is omitted, all messages in the queue are displayed.
Description:
This command displays messages from the Output Circular Queue for the
specified local FEP table.  The data is displayed in X1 format.
Example:
nodename -\K$OCQ $LS49,20
00002
00003
00001
Format:
\K$OCQ $LSnn,size
Parameters:
nn    specifies the segment that contains the FEP table.  The value to use may
be determined by using the FEI command.
size    specifies the number of messages to be displayed.  If this parameter
is omitted, all messages in the queue are displayed.
Description:
This command displays messages from the Output Circular Queue for the
specified local FEP table.  The data is displayed in X1 format.
Example:
nodename -\K$OCQ $LS49,20
00002
00003
00001
Format:
\K$RCQ user,size
Parameters:
user    specifies the user whose circular queue is to be displayed.  user is
specified as either a hexadecimal (user) number preceded by a period or a
decimal sysid.
size    specifies the number of messages to be displayed.  If this parameter
is omitted, all messages removed from the queue are displayed.
Description:
This command displays messages from the Receive Circular Queue for the
specified user.  The messages displayed are the last ones that have been
removed from the queue.
Example:
nodename -\K$RCQ .2,10
00002
00003
00001
Format:
\K$RCQ user,size
Parameters:
user    specifies the user whose circular queue is to be displayed.  user is
specified as either a hexadecimal (user) number preceded by a period or a
decimal sysid.
size    specifies the number of messages to be displayed.  If this parameter
is omitted, all messages removed from the queue are displayed.
Description:
This command displays messages from the Receive Circular Queue for the
specified user.  The messages displayed are the last ones that have been
removed from the queue.
Example:
nodename -\K$RCQ .2,10
00002
00003
00001
Format:
\K$SCQ user,size
Parameters:
user    specifies the user whose circular queue is to be displayed.  user is
specified as either a hexadecimal (user) number preceded by a period or a
decimal sysid.
size    specifies the number of messages from the Send Circular Queue for the
specified user.  The messages displayed are the last ones that have been
removed from the queue.
Description:
This command displays messages from the Send Circular Queue for the specified
user.  The messages displayed are the last ones that have been removed from
the queue.
Example:
nodename -\K$SCQ .2,10
00002
00003
00001
Format:
\K$SCQ user,size
Parameters:
user    specifies the user whose circular queue is to be displayed.  user is
specified as either a hexadecimal (user) number preceded by a period or a
decimal sysid.
size    specifies the number of messages from the Send Circular Queue for the
specified user.  The messages displayed are the last ones that have been
removed from the queue.
Description:
This command displays messages from the Send Circular Queue for the specified
user.  The messages displayed are the last ones that have been removed from
the queue.
Example:
nodename -\K$SCQ .2,10
00002
00003
00001
Format:
\KN$TCTX location
Parameter:
location    is an address expression.
Description:
This command produces a detailed display of the Transport Context Block
specified by location.
00002
00001
Format:
\KN$TCTX location
Parameter:
location    is an address expression.
Description:
This command produces a detailed display of the Transport Context Block
specified by location.
00002
00001
Format:
\TREE { usernum | - sysid }
Parameters:
usernum    specifies a positive user number.
sysid    specifies a sysid that must be negative.
Description:
This command displays the tree table in the Read-Only Segment (ROSEG).
00002
00001
Format:
\TREE { usernum | - sysid }
Parameters:
usernum    specifies a positive user number.
sysid    specifies a sysid that must be negative.
Description:
This command displays the tree table in the Read-Only Segment (ROSEG).
00002
00001
