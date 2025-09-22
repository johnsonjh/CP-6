The ELAN processor is used to examine the contents of the system error log 
files, as well as generating reports on the performance of various system 
components. 
For more information, type: 
HELP (ELAN) COMMANDS      For a list of ELAN command names. 
HELP (ELAN) COMMAND_SUMM  For summary description of ELAN 
                          commands. 
HELP (ELAN) TOPICS        For a list of ELAN HELP topics 
HELP (ELAN) command       For a command format.  Then type ? 
                          or ?? for more information. 
HELP (ELAN) command PARA  For parameters for a specific 
                          command. 
HELP (ELAN) command DESC  For description of a specific 
                          command. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
An error type 310 is logged whenever the TPA fails to initialize.  The record 
is displayed in octal.  See the CP-6 TP Administrator Guide (CE50) for more 
information. 
An ANLZ entry is logged any time ANLZ/DELTA is used to modify the running 
Monitor.  The following is a list of headers displayed to identify items from 
an ANLZ entry. 
Header          Meaning 
------          ------- 
COMMAND         Text of the command that was entered. 
USER#,          Identification of the user who modified the Monitor. 
USER NAME, 
ACCOUNT, 
SYSID 
CGERR entries are recoverable errors that are logged by the comgroup facility. 
Header          Meaning 
------          ------- 
CODE            Gives one of ten possible error codes: 
                 1 = Illegal state noted during fetch of data block 
                 2 = Time stamp error noted during fetch of data block 
                 3 = Unable to un-delete a previously deleted data block 
                 4 = Illegal state noted during deletion of data block 
                 8 = Granule has bad time stamp 
                 9 = Error encountered during fetch of data block for 
                     a read or get 
                10 = Continued write data block fetch error 
                11 = Inconsistency noted in an MLH containing super MBLKs 
                12 = Inconsistency noted during comgroup garbage 
                     collection 
                13 = Bad link discovered in super MBLK 
CTX             Word display of CTX block pointer. 
NAME            Name of user. 
INFO            Octal dump of record. 
A CHANTRAN entry is logged when a channel changes state such as from normal to 
suspended.  The CP-6 host is informed of this by a special interrupt being 
issued on channel 6.  This interrupt represents a transition from one allowed 
channel state to another. 
Header          Meaning 
------          ------- 
IOP             IOP this special interrupt came from. 
CHAN            The channel requiring service. 
STATUS          Gives one of four possible state transitions: 
                    Normal to suspended   =  1 
                    Suspended to normal   =  2 
                    Suspended to stopped  =  8 
                    Stopped to normal     = 16 
SPECIAL STATUS  Octal dump of the 1 word and 1 byte record. 
WORD 
A CHNGAARD entry is logged whenever a component needed by AARDVARK for disk 
boots, recovery or XDELTA is partitioned by a user.  AARDVARK's components are 
the path to the system disk, the system console, the unit-record controller, 
and unit record devices.  When a component is partitioned, the system will, if 
possible, assign an alternate component and rewrite AARDVARK's data in the 
DP#CP-6'S area of the system disk.  If no alternate component can be assigned, 
DP#CP-6'S is not rewritten and AARDVARK will use the original component.  If 
this component has not been RETURNed to the system, via SYSCON, difficulties 
may occur when performing a disk boot, recovery, or when running XDELTA. 
Header               Meaning 
------               ------- 
OLD I-CCC            This is the component that AARDVARK required for a 
                     disk boot or recovery and which is now partitioned. 
NEW I-CCC            If present, this is the new component that the system 
                     has designated for AARDVARK's use. 
ACCOUNT,             Identification of the user who performed the 
USER NAME,           partition. 
SYSID 
MESSAGE              If present, an entry under this header reports an 
                     error when AARDVARK's data was being rewritten to 
                     the DP#CP-6'S area of the system disk. 
A CMPSTRT entry is logged when a CPU changes state such as startup or stopped. 
Header           Meaning 
------           ------- 
COMPONENT        Component number 
LAST STATE       UTS at previous state change 
CHANGE 
NEW STATE        Processor state after state change which may be 
                 stopped, running, or hung up. 
ELAN commands are divided into the following categories: 
o   Miscellaneous commands:  DATE, END, EXIT, FILE, HELP, PROMPT, QUIT, 
    STATUS, THRESH, TIME. 
o   Report command: The REPORT command requests report generation and 
    specifies report type. 
o   Selection commands:  ERROR, EXCLUDE, MATCH, OCTAL, RESET, SELECT, and 
    SPAN.  These commands specify what information from the error log files or 
    :DEVHIST file is to be included. 
For more information on a specific command, type: 
HELP (ELAN) command 
For a brief description of a specific command, type: 
HELP (ELAN) COMMAND_SUM command 
For a summary of all commands, type ??.  For the summary description of a 
specific command, type 
HELP (ELAN) COMMAND_SUM command 
Valid command names are DATE, END, ERROR, EXCLUDE, EXIT, FILE, HELP, MATCH, 
OCTAL, PROMPT, REPORT, RESET, SELECT, SPAN, STATUS, THRESH, TIME. 
  Command        Description 
  {DATE|TIME} 
                 Displays the current date and time. 
  {END|EXIT|QUIT} 
                 Terminates ELAN. 
  ERROR 
                 Causes only error log records of the specified type(s) to be 
                 included in reports.  ERROR and SELECT are synonyms. 
  EXCLUDE 
                 Specifies the items in error log file IOERR or FEPERR records 
                 that are to be excluded from reports. 
  FILE 
                 Allows the user to redirect error log input to a specified 
                 fid, instead of defaulting to the standard :ERRLOG file. 
  HELP 
                 Provides information about operation of the ELAN processor 
                 and other processors. 
  MATCH 
                 Specifies the items in error log file IOERR or FEPERR records 
                 that are to be reported. 
  OCTAL 
                 Specifies an octal dump with ASCII translation for RAW and 
                 DETAIL reports. 
  PROMPT 
                 Changes ELAN's prompt. 
  REPORT 
                 Selects the type of report to be generated and initiates 
                 report generation. 
  RESET 
                 Resets report selection criteria. 
  SELECT 
                 Causes only error log records of the specified type(s) to be 
                 included in reports.  SELECT and ERROR are synonyms. 
  SPAN 
                 Specifies the time span for which information is to be 
                 reported. 
  STATUS 
                 Displays report selection criteria. 
  THRESH 
                 Establishes and displays the ATTEN and ALERT thresholds. 
Redirects ELAN to the specified account for :ERRLOG files. 
00001
00002
00003
00004
00005
00006
00007
00008
00009
00002
00010
00011
00012
00013
00014
00015
00001
00002
A CP6SAYS entry is logged when the CP-6 host responds to an MSOS request. 
This entry will give the response and the reason for the response. 
Header          Meaning 
------          ------- 
IOP             The IOP in which this response is given/coming from. 
CP6 RESPONSE    CP-6 host's response to MSOS's request. 
TO MSOS 
REASON          Reason for the response. 
COMMAND BLOCK   The octal 4 words and 1 byte of the logged record. 
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
    mmm dd 'yy hh:mm (month)(day)(year)(hours)(minutes) 
Examples: 
elan:DATE 
requests a display of the current data and time.  A sample display is: 
    MAR 02  '86  11:03 
00001
00002
A DEVSTAT entry is a statistical entry gathered from counters in certain 
device controllers.  The firmware in these controllers maintains statistical 
information in counters pertaining to the devices connected to it.  The 
controllers are polled and a DEVSTAT entry is logged every 30 minutes.  The 
counters are reset at the time of the poll and whenever the firmware is 
rebooted.  This information is provided for tapes on MPC-type and TPUR-type 
controllers and disks on MPC-type, DAU-type and MDS-type controllers. 
Note:  Report headers explained below for DEVSTAT entries refer to various 
controller types for which corresponding models are listed below. 
    Controller Type             Models 
    ---------------             ------ 
    MPC-type Tape Controllers   MTP0601, MTP8021, MTP8022, MTP8023 
                                MTP0610, MTP0611 
    TPUR-type Tape Controllers  MFP8000T, MFP8001T, MTPTPUR, MTP8000, 
                                MTP8001 
    MPC-type Disk Controllers   MSP0191, MSP0450, MSP0600, MSP0611, 
                                MSP0612, MSP8000, MSP8001 
    DAU-type Disk Controllers   MSP8021, MSP8022, MSP8023 
    MDS-type Disk Controllers   MSS8080, MSS8090 
Report Headers for tapes on MPC-type and TPUR-type controllers: 
Header               Meaning 
------               ------- 
DEV                  Device name. 
MPC                  Name of controller polled for statistical information. 
RECS READ            Number of physical records that have been read by 
                     the controller during the execution of read-type 
                     commands. 
RECS WRITTEN         Number of physical records that have been written 
                     by the controller during the execution of 
                     write-type commands. 
WRITE ERRS           Number of physical records that were detected to have 
                     an error during the writing process. 
READ ERRS            Number of physical records that were detected to have 
                     an error during the reading process. 
TRANSFER TIM ERRS    Number of transfer timing errors detected while 
                     transferring information during either a read or 
                     write. 
MARG RECS            Number of read, write, and forward space operations 
                     for which the handler indicated that a marginal 
                     condition occurred. 
RECS W/SNG TRK CORR  Number of PE records that were successfully read 
                     after single track correction was performed. 
MTC RD CNT           Number of times the controller issued a read 
                     command while attempting a retry. 
Raw Report Headers for disks: 
Header               Meaning 
------               ------- 
DEV                  Device name. 
MPC                  Name of controller polled for statistical information. 
#OF SEEKS            Number of seek commands.  For MDS-type controllers, 
                     this is the total of seek-reads and seek-writes. 
SECTORS READ         Number of sectors read from the device. 
SECTORS WRITTEN      Number of sectors written to the device. 
SEEK ERRORS          Number of seek errors detected by the controller for 
                     the device.  For MPC-type controllers, this is the 
                     total of header verification errors and incomplete 
                     seeks. 
RETRIES              Number of data retries to the device. 
CORR EDAC ERS        Number of correctable EDAC errors. 
UNCORR EDAC ERS      Number of uncorrectable EDAC errors on the device. 
OTHER ERRS           Total of other types of errors reported on the device. 
                     Use the Extended Report for more information. 
Extended Report Headers for disks on MPC-type and DAU-type controllers: 
Header               Meaning 
------               ------- 
# OF SEEKS           Number of actuator movements of the device. 
SECTORS WRITTEN      Total number of sectors written on the device. 
SECTORS READ         Total number of sectors transferred from the device 
                     to the host. 
# DATA TR CMDS       Total number of data transfer commands issued to the 
                     device (i.e., read or write). 
INCOMP SEEKS         Number of incomplete seeks the controller received 
                     from the device. 
HDR VER ERRS         Number of positioning errors (i.e., the CYL/HEAD 
                     information in the count field did not agree with the 
                     CYL/HEAD of the seek address). 
TRANS TIM ERRS       Number of transfer timing errors (i.e., the 
                     controller was unable to keep up with the data 
                     transfer to or from the device). 
DATA CHK ALERTS      Number of EDAC errors in the data field. 
CNT CHK ALERTS       Number of ECC or EDAC errors in the count field. 
DLI PAR ERRS         Number of parity errors detected by the controller on 
                     data from the PSIA or the device. 
ALT TRKS ACCESSED    Number of times, if alternate tracks are assigned, 
                     the controller went to the alternate track to continue 
                     the data transfer. 
CORR EDAC ERS        Number of data fields that were corrected using the 
                     EDAC syndrome. 
UNCORR EDAC ERS      Number of data fields that could not be corrected 
                     using EDAC. 
LATENCY RETRIES      Number of extra disk revolutions wasted because the 
                     PSIA was not fast enough to empty/fill data buffers 
                     in time to continue the I/O transaction. 
DATA RETRIES         Number of times a data field was reread in an attempt 
                     to correct data. 
SYNC FAILURES        Number of times the sync byte on the disk pack did 
                     not agree with what it should be. 
Extended Report Headers for disks on MDS-type controllers: 
Header               Meaning 
------               ------- 
BYTES READ(1024K)    Counter in CM subsystem indicating number of bytes 
                     read.  Number is a multiple of 1024K. 
BYTES WRT(1024K)     Counter in CM subsystem indicating number of bytes 
                     written.  Number is a multiple of 1024K. 
# OF SEEKS(1K)       Counter in CM subsystem indicating number of seeks 
                     performed.  Number is a multiple of 1K. 
# OF SEEK ERRS       Counter in CM subsystem indicating number of seek 
                     errors. 
DATA CHKS CORRECTED  Counter in CM subsystem indicating number of data 
                     checks corrected. 
DATA CHKS UNCORR     Counter in CM subsystem indicating number of data 
                     checks uncorrected. 
# OF SEEKS           Counter in IPC controller indicating number of seek 
                     commands. 
# OF SEEK/READS      Counter in IPC controller indicating number of 
                     seek/read commands. 
SECTORS READ         Counter in IPC controller indicating number of sectors 
                     read. 
# OF SEEK/WRTS       Counter in IPC controller indicating number of 
                     seek/write commands issued. 
SECTORS WRITTEN      Counter in IPC controller indicating number of sectors 
                     written. 
# OF RETRIES         Counter in IPC controller indicating number of 
                     retries. 
LATENCIES LOST       Counter in IPC controller indicating number of 
                     latencies lost. 
NOTE: The reason lost latencies occur on MDS disks is because (1) MDS 
disks are flawed on a sector by sector basis; (2) CP-6 does disk IO by 
the granule; (3) one granule is two sectors on MDS disks; and (4) if 
the first sector of a granule is flawed and assigned to an alternate 
sector that is "after" the second granule, the MDS disk firmware will 
record a Lost Latency every time that granule is read or written. 
Therefore, if your MDS HDA has flawed sectors, it is likely that you 
will see Lost Latencies reported in the DEVICE STATISTICS.  Unless 
there are a very large number of them (tens or hundreds of thousands), 
there is no cause to be alarmed. Each Lost Latency costs the system 
1/3600 of a second in extra IO wait time. They can come in bursts if 
there is a file that is on one or more flawed sectors and that is 
accessed only occasionally. 
A DIAG entry is logged whenever a diagnostic test is issued on a device. 
Header           Meaning 
------           ------- 
ACCOUNT          Users account 
USER NAME        Users name who requested the test 
SYSID            Users sysid 
DEV              Device opened 
TEST             May be one of the following test types: 
                     POLTS, MDR, ITR, MTAR, FEP, MPC, or MCA 
These entries are logged to report the mounting/dismounting of I/O devices. 
Header           Meaning 
------           ------- 
VOLUME           Volume serial number 
PSN              Packset name if disk 
DEVNM            Device name 
REQT             Request time in Universal Time Stamp (UTS) 
                 MOUNT/DISMOUNT - one of these is displayed 
                                  specifying whether a mount or 
                                  dismount occurred. 
END
An EDAC entry is logged when an EDAC syndrome register becomes non-zero and 
it's the first error of this type since the last disk boot. 
Header           Meaning 
------           ------- 
ADDRESS          Real address of Store unit in octal 
SCU MODE         System Controller Unit Mode in octal 
STORE UNIT MODE  Store Unit Mode register in octal 
PORT             SCU port to which master CPU is connected 
STORE UNIT       Store unit on the System Controller 
SLOT             Board select address 
CHIP             Chip select address 
COUNT            Number of errors on this unit with the same syndrome 
                 number 
ELAN has several report formats that allow specification of various types of 
information to be reported.  Some of these reports are higher-level, giving 
information on the entire system, while others are low-level, device specific 
reports. 
To display a brief description of each report, type ? or ??.  To display the 
description of a specific report, type 
HELP (ELAN) ELAN_R rtype 
Valid rtypes are AMS, CONFIG, DETAIL, EXTENDED, HWE, RAW, SUM, SYS, UPR.  For 
explanation of column headings in reports, type HELP (ELAN) err_type, where 
valid err_types are ANLZ, CGERR, CHANTRAN, CHNGAARD, CMPSTRT, CP6SAYS, 
DEVSTAT, DIAG, DSMT, EDAC, FEPDUMP, FEPERR, FEPEVENT, FEPFLT, FI, GABRT, 
IOERR, LOST, MPCSTAT, MSOSSAYS, OPER, OSFI, PROCERR, RECOV, SCREECH, SNAP, 
SPURINT, SUA, SYSCON, SYSID, TIMESTAMP, ZAP, 310 
Information on reports is displayed under these headings: 
  Type     Description 
  Anticipatory Maintenance Summary (AMS) 
           This report is intended for use by the Bull Customer Service 
           Engineer in identifying those components that are below current 
           system thresholds (which are discussed below under the heading 
           Performance Values).  All components that have performance values 
           below a current threshold will be reported. 
  Configuration Report (CONFIG) 
           This report shows the current system configuration.  I-O 
           Multiplexers (IOMs), Micro-Programmed Controllers (MPCs), and their 
           devices, along with the channel connections are displayed. 
  Detail Report (DETAIL) 
           This report is identical to the EXTENDED report, except that EDAC, 
           IOERR and FEPERR records are sorted by sub-items within each record 
           and printed in summarized formats.  All other types are identical 
           to the EXTENDED report formats. 
  Extended Report (EXTENDED) 
           This report is identical to the RAW report, except that all 
           information contained in the error log records is included.  Not 
           all information contained in the IOERR, FI, FEPERR, DEVSTAT, 
           MPCSTAT, and CGERR records is included in the RAW report.  This 
           report also includes interpretation of major, minor, and extended 
           status codes for IOERR entries; and interpretation of fault code 
           and fault register for PROCERR entries. 
  Hardware Error Report (HWE) 
           This report provides information concerning the I/O errors that 
           have occurred on a given system component.  This report contains a 
           detailed look at the information in the IOERR records, along with 
           the major and minor status codes and their translations.  This 
           report is aimed at assisting the Customer Service Engineer who is 
           attempting to fix a particular system component. 
  RAW Report (RAW) 
           This report allows the user to examine the contents of daily error 
           log files.  It provides a formatted display of these records. 
  Summary Report (SUM) 
           This report is a summary list of the error records in an error log 
           file.  The report lists the number of records of each type that are 
           in the error log.  In addition, under the PERIPHERAL DEVICE ERRORS, 
           the number of connects, errors, and mounts are reported. 
  System Summary Report (SYS) 
           This report is the highest level report produced by ELAN.  It 
           provides the system manager with an overall view of the performance 
           of the system.  This report will show performance values on 
           peripherals, flagging any that are below current thresholds.  A 
           summary of MOS memory errors, processor errors, front-end processor 
           crashes, and system crashes is also included. 
  Unit Performance Report (UPR) 
           This report allows the Customer Service Engineer to examine the 
           performance of a system component over the past 30 days.  This 
           report produces a graph showing performance value versus time in 
           days from the present date. 
00001
00002
00003
00004
00005
00006
00007
00008
00009
Format: 
E[ND]|[E]X[IT]|Q[UIT] 
Description: 
The END command, and its synonyms EXIT and QUIT, cause ELAN to do a normal 
exit and return control to IBEX. 
00001
END
Format: 
{ER[ROR]|SE[LECT]} [ +] typelist 
Parameters: 
 +    specifies that the error type(s) input are to be added to the current 
error type selection criteria.  Otherwise, the type(s) input replace any 
previous error type selection criteria. 
typelist    specifies one or more of the following error types separated by 
commas: 
    Type         Description 
    ----         ----------- 
    ANLZ         ANLZ text 
    CGERR        Comgroup error 
    CHANTRAN     Channel transition 
    CHNGAARD     Aardvark component partitioned. 
    CMPSTRT      Component startup 
    CP6SAYS      CP-6 response 
    DEVSTAT      Device statistics 
    DIAG         Diagnostic open 
    DSMT/MOUNT   Volume dismount/mount 
    EDAC         MOS memory errors 
    FEPDUMP      Front-end processor dump 
    FEPERR       Front-end processor errors 
    FEPEVENT     Front-end processor event 
    FEPFLT       Front-end processor fault 
    FI           File inconsistency 
    FWLOAD       Firmware load 
    GABRT        Ghost abort 
    IOERR        I/O error 
    LOST         Lost entries 
    MIRROR       Mirrored Disk entries 
    MPCSTAT      MPC statistics 
    MSOSSAYS     MSOS request 
    OPER         Operator input 
    OSFI         Output symbiont file inconsistency 
    PROCERR      Processor errors 
    RECOV        Combines SUA, SNAP, and SCREECH 
    REX          Resource exhausted 
    SCREECH      System recovery 
    SNAP         Snap 
    SPURINT      Spurious interrupt 
    SUA          Single User Abort 
    SYSCON       Partition or return device 
    SYSID        Contents of B_SITEINFO 
    TIMESTAMP    Timestamp 
    ZAP          ZAP! operator keyin 
    310          TPA initialization error 
Description: 
This command causes only error log records of the specified type(s) to be 
selected for inclusion in reports.  ERROR and SELECT are synonyms. 
00002
00001
Format: 
EXC[LUDE] [AD[D]|DE[LETE]] {ioerr_optlist|feperr_optlist|fi_optlist} 
Parameters: 
ADD|DELETE    specifies options to add/delete from existing EXCLUDE options. 
If neither ADD nor DELETE is specified, the options listed replace any 
previous options as those to be ignored; options not specified are included. 
ioerr_optlist    specifies one or more of the following options separated by 
commas: 
    Option                      Description 
    ------                      ----------- 
    MAJ=ooo                     IOERR records containing the specified 
                                octal major field. 
    SUB=ooo                     IOERR records containing the specified 
                                octal sub-field. 
    MED=id                      IOERR records containing the specified 
                                media identifier. 
    BYTE n[,BIT n] = bbbbbbbb   IOERR records containing byte n 
                                (and bit n) equal to the specified 
                                binary value. 
feperr_optlist    specifies one or more of the following options separated by 
a comma: 
    Option     Description 
    ------     ----------- 
    FCG=fcg    FEPERR records containing the 2- to 3-character FEP 
               functional code group specified. 
    CHAN=hhhh  FEPERR records containing the hexadecimal channel number 
               specified. 
fi_optlist   specifies one or  more of the following options separated 
by a comma: 
    Option       Description 
    ------       ----------- 
    COD[E]=dd    FI records containing the specified decimal file 
                 management error CODE for the file inconsistency. 
    REA[SON]=dd  FI records containing the specified decimal REASON for 
                 the file inconsistency. 
    ACT[ION]=d   FI records containing the specified ACTION taken by file 
                 management in response to the file inconsistency. 
Description: 
This command determines which error records to exclude in a subsequent report. 
If ADD or DELETE is specified, the listed options are added or removed from 
the previously excluded options. 
Examples: 
elan:EXCLUDE MAJ=43 
elan:EXCLUDE MAJ=42, SUB=01 
elan:EXCLUDE MAJ=42, SUB=02, MED=1046 
elan:EXCLUDE BYTE 3, BIT 1 = 0 
elan:EXCLUDE BYTE 3 = 11110101 
elan:EXCLUDE FCG=GNS, CHAN=2380 
elan:EXCLUDE ACT=0 
elan:EXCLUDE COD=38,REA=72 
00002
00003
00001
MIRROR
FILE
A FEPDUMP entry is logged after an initial FEP crash is issued and a dump file 
is produced. 
Header           Meaning 
------           ------- 
FEP#             FEP number 
DUMP FILE NAME   Dump file name 
REASON           Reason for the crash 
SCREECH          SCREECH description 
An FEPERR entry is logged when the FEP detects an error condition.  This 
information is sent to the host for entry into the error log.  The following 
is a list of headers displayed to identify items from an FEPERR entry. 
Raw and Detail Report Headers: 
Header          Meaning 
------          ------- 
CHAN            Hexadecimal channel number. 
DATA            YES indicates the existence of dynamic data in the 
                Detail report. 
E/CNT           Summarized count of the occurrences of this 
                FEPERR operation. 
ERROR CODE      Error code being reported.  See Appendix H for a 
                list of the error codes and their meaning. 
ERROR MESSAGE   Explanatory error message. 
FEP#            FEP reporting the error. 
Additional Detail Report Headers: 
Header          Meaning 
------          ------- 
BASE REGS/      Contents of several of the registers in the FEP 
GEN REGS        when the error condition occurred. 
CODE            Unique code in addition to ERROR CODE that 
                further identifies this error condition. 
DYNAMIC DATA    When an FEPERR is logged, up to 100 bytes of 
                dynamic data may also be part of the entry.  In 
                the Raw Report, this entry identifies how much 
                dynamic data is present.  In the Detail Report, 
                the dynamic data is dumped in octal. 
L6 TIME         Number of ticks (8.333 ms.) since the FEP was 
                booted. 
UTS             Universal Time Stamp (UTS) sent to the FEP by the 
                Host at FEP boot time. 
An FEPEVENT entry is logged whenever a FEP interface event occurs.  The 
following is a list of the headers displayed to identify items from a FEPEVENT 
entry. 
Header          Meaning 
------          ------- 
I-CCC           IOM/Channel connection of the FEP to the Host. 
NAME            Name of the FEP that crashed. 
PROBLEM         Reason for the crash. 
REMOTE          Number of connected paths (CNCT) to the remote FEP 
                at the time of the crash. 
SEQ             Crash number for this FEP. 
STATE           State of the FEP when it crashed. 
A FEPFLT entry is logged when a SCREECH occurs while the FEP is booting, or 
during a normal operation. 
Header           Meaning 
------           ------- 
I-CCC            IOM channel 
FEP#             FEP number 
FAULT WORD       Fault word in octal 
An FI entry is logged whenever a file inconsistency is detected.  The 
following is a list of headers displayed to identify items from an FI entry. 
Raw and Detail Report Headers: 
Header          Meaning 
------          ------- 
ACT             Action being logged. 
COD             Error code. 
DEV             Device name. 
FID             CP-6 file identifier. 
FRDA            File-relative disk address. 
REA             Reason for error. 
REQID           Request ID from IOQ packet. 
SRDA            Set-relative disk address. 
Additional Detail Report Headers: 
Header          Meaning 
------          ------- 
AC              Contents of DCB.ACS. 
BFRn/BFRnX      3 words from buffer (and their displacement). 
CYL-HD-SE       Cylinder, head, sector numbers. 
D               Contents of DCB.DISP. 
F               Contents of DCB.FUNC. 
G               Contents of DCB.GTYP. 
L               Contents of DCB.LVL. 
MISC            Miscellaneous word for internal use. 
ORG             Contents of DCB.ORG. 
PLUGH           Program List Used to Get Here. 
S               Contents of DCB.SHARE. 
SEEKADDR        Seek address. 
STATUS          Status from the IOQ packet. 
SYSID           Sysid of user. 
TYC             TYC from the IOQ packet. 
Format: 
FI[LE] fid 
Parameters: 
fid    specifies a valid CP-6 file identifier. 
Description: 
This command allows the user to redirect ELAN to the specified file containing 
error log records.  The file must be compatible with the standard :ERRLOG 
files with respect to the format of the records and the order of the records 
within the file.  ELAN will determine the time span of the records within the 
file to establish the time constraints for all subsequent reports and 
selection criteria.  A RESET command can be used to reset ELAN's default file 
assignments.  The FILE command provides an easy way to look at BEAMed (or 
otherwise saved on CP-6) error log files. 
00002
00001
A GABRT entry is logged whenever a Ghost user aborts.  The following is a list 
of the headers displayed to identify items from a GABRT entry. 
Header          Meaning 
------          ------- 
CC              Contents of B$JIT.STEPCC. 
ERRCODE         Contents of B$JIT.ERR. 
FRS             Contents of B$JIT.FRS. 
IC              Contents of Instruction Counter at the Abort. 
RNS             Contents of B$JIT.RNST. 
SYSID,          Identification of the Ghost that aborted. 
USER NAME 
USER ERRCODE    Contents of B$JIT.USRERR. 
XFL             Contents of B$JIT.XLIMFLG. 
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
  ANLZ -   
    USE Command - 
      HELP USE FORMAT: 
  ANLZ Entries - 
      HELP ANLZ 
C 
  CGERR Entries - 
      HELP CGERR 
  CHANTRAN Entries - 
      HELP CHANTRAN 
  CHNGAARD Entries - 
      HELP CHNGAARD 
  CMPSTRT Entries - 
      HELP CMPSTRT 
  CP6SAYS Entries - 
      HELP CP6SAYS 
D 
  DATE Command - 
      HELP DATE 
  :DEVHIST file (ELAN) - 
      HELP RELATED_FILES 
  DEVSTAT Entries - 
      HELP DEVSTAT 
  DIAG Entries - 
      HELP DIAG 
  DSMT/MOUNT Entries - 
      HELP DSMT 
E 
  EDAC Entries - 
      HELP EDAC 
  ELAN -   
    ERROR Command - 
      HELP ERROR FORMAT: 
    EXCLUDE Command - 
      HELP EXCLUDE FORMAT: 
    FILE Command - 
      HELP FILE FORMAT: 
    MATCH Command - 
      HELP MATCH FORMAT: 
    OCTAL Command - 
      HELP OCTAL FORMAT: 
    PROMPT Commands - 
      HELP PROMPT FORMAT: 
    REPORT Command - 
      HELP REPORT FORMAT: 
    RESET Command - 
      HELP RESET FORMAT: 
    SPAN Command - 
      HELP SPAN FORMAT: 
    STATUS Command - 
      HELP STATUS FORMAT: 
    THRESH Command - 
      HELP THRESH FORMAT: 
  ELAN Command Summary - 
      HELP COMMANDS 
  ELAN Report Formats - 
      HELP ELAN_REPORTS 
  END Command - 
      HELP END 
  :ERRLOGyymmdd file - 
      HELP RELATED_FILES 
  Error log - 
      HELP REPORT_ENTRIES 
      HELP RELATED_FILES 
  ERROR/SELECT Command - 
      HELP ERROR 
  EXCLUDE Command - 
      HELP EXCLUDE 
F 
  FEPDUMP Entries - 
      HELP FEPDUMP 
  FEPERR Entries - 
      HELP FEPERR 
  FEPEVENT Entries - 
      HELP FEPEVENT 
  FEPFLT Entries - 
      HELP FEPFLT 
  FI Entries - 
      HELP FI 
  FILE Command - 
      HELP FILE 
  Files Examined/Maintained by ELAN - 
      HELP RELATED_FILES 
G 
  GABRT Entries - 
      HELP GABRT 
H 
  HELP Command - 
      HELP HELP 
I 
  Invoking ELAN - 
      HELP INVOKING_ELAN 
  IOERR Entries - 
      HELP IOERR 
L 
  latencies lost - 
      HELP DEVSTAT 
  LOST Entries - 
      HELP LOST 
  lost latencies - 
      HELP DEVSTAT 
M 
  MATCH Command - 
      HELP MATCH 
  MIRROR Entries - 
      HELP MIRROR Entries 
  MPCSTAT Entries - 
      HELP MPCSTAT 
  MSOSSAYS Entries - 
      HELP MSOSSAYS 
O 
  OCTAL Command - 
      HELP OCTAL 
  OPER Entries - 
      HELP OPER 
  OSFI Entries - 
      HELP OSFI 
P 
  Performance Values for ELAN - 
      HELP PERFORMANCE_VALUES 
  Privileges for Use of ELAN - 
      HELP PRIVILEGES 
  PROCERR Entries - 
      HELP PROCERR 
  PROMPT Command - 
      HELP PROMPT 
R 
  RECOV Entries - 
      HELP RECOV 
  REPORT Command - 
      HELP REPORT 
  REPORT Command (ELAN) - 
      HELP REPORT FORMAT: 
  RESET Command - 
      HELP RESET 
  RESET Command (ELAN) - 
      HELP RESET FORMAT: 
S 
  SCREECH/SNAP/SUA Entries - 
      HELP SCREECH 
  SPAN Command - 
      HELP SPAN 
  SPURINT Entries - 
      HELP SPURINT 
  STATUS Command - 
      HELP STATUS 
  STATUS Command (ELAN) - 
      HELP STATUS FORMAT: 
  SYSCON Entries - 
      HELP SYSCON 
  SYSID Entries - 
      HELP SYSID 
T 
  THRESH Command - 
      HELP THRESH 
  TIMESTAMP Entries - 
      HELP TIMESTAMP 
  Total On-line Testing System (TOLTS) - 
      HELP REPORT_ENTRIES 
  310 (TP Initialization) Error Entries - 
      HELP 310_ERROR 
U 
  USE Command - 
      HELP USE 
Z 
  ZAP Entries - 
      HELP ZAP 
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
HELP_INDEX
ELAN may be run as a batch, ghost or on-line job. 
ELAN is invoked by: 
    !ELAN 
to request information that is contained in :DEVHIST and the daily error logs 
that currently exist. 
When run as an on-line job, ELAN solicits commands with the prompt elan:. The 
prompt can be changed through the PROMPT command (described below). 
The user may terminate execution of any of the report commands by means of the 
break key.  ELAN will print out the word BREAK and prompt for another ELAN 
command. 
In ghost mode, ELAN is invoked by: 
    !ELAN ME 
The DCBs used by ELAN are: 
o   M$SI for input 
o   M$LO for output 
An IOERR entry is logged whenever an I/O error occurs.  The following is a 
list of headers displayed to identify items from an IOERR entry. 
Raw and Detail Report Headers: 
Header          Meaning 
------          ------- 
CNCT            Connect count since the last error on the 
                component. 
COMPONENT       Device name. 
DEV             Device on which the error occurred. 
E/CNT           Summarized count of the occurrences of this 
                I/O operation. 
ER-CT           ER is the number of times this I/O operation was 
                retried.  CT is the count of repeats of this 
                error. 
ERROR TYPE      Interpretation of major and minor status codes 
                plus their octal representation. 
I-CCC-DD        IOM-Channel-Device number of the component. 
ICCCDD          Same as I-CCC-DD. 
IDCW            6-bit device command from the IDCW on which the 
                error occurred. 
ISTAT/FSTAT     Initial and final MAJOR-MINOR-IOM hardware 
                status. 
REQ             An asterisk (*) entry indicates that this error 
                has the same REQID as the one preceding it in the 
                report. 
SECTOR          Seek address. 
SN              Serial number of the media mounted on the device. 
Additional Detail Report Headers: 
Header          Meaning 
------          ------- 
CNCT            Connect count since the last error on the 
                component. 
CYL-HD-SE       Cylinder, head, and sector numbers. 
DCW             Full DCW for which the error occurred. 
DEV             Device name. 
ER-CT           ER is the number of times this I/O operation was 
                retried.  CT is the count of repeats of this 
                error. 
Extended status 26 8-bit bytes of extended status returned by the 
                hardware and output in hexadecimal. 
FIL             For a tape error, FIL is the current 
                file count on that tape. 
FINAL STATUS    Full Final status doubleword. 
I-CCC-DD        IOM-Channel-Device number of the component. 
IDCW            Full IDCW for which the error occurred. 
INITIAL STATUS  Full Initial status doubleword. 
MEM ADDRESS     Last memory address referenced. 
RECCNT          For a tape error, RECCNT is the current 
                record count within a file (FIL) on the 
                tape. 
REQID           Request ID for this I/O request. 
SEEKADDR        Seek address. 
SN              Serial number of the media mounted on the device. 
STATUS          Octal major and minor status codes. 
STATUS CODES    Interpretation of major and minor status codes. 
Lost entries are logged when lost error records are detected.  ELAN displays 
one sentence specifying how many records are lost during a spanned time. 
Format: 
MA[TCH] [AD[D]|DE[LETE] {ioerr_optlist|feperr_optlist|fi_optlist} 
Parameters: 
ADD|DELETE    specifies options to add/delete from existing MATCH options.  If 
neither ADD nor DELETE is specified, the options listed replace any previous 
set options. 
ioerr_optlist    specifies one or more of the following options separated by 
commas. 
    Option                      Description 
    ------                      ----------- 
    MAJ=ooo                     IOERR records containing the specified 
                                octal major field. 
    SUB=ooo                     IOERR records containing the specified 
                                octal sub-field. 
    MED=id                      IOERR records containing the specified 
                                media identifier. 
    BYTE n[,BIT n] = bbbbbbbb   IOERR records containing byte n 
                                (and bit n) equal to the specified 
                                binary value. 
feperr_optlist    specifies one or more of the following options separated by 
a comma: 
    Option     Description 
    ------     ----------- 
    FCG=fcg    FEPERR records containing the 2- to 3-character FEP 
               functional code group specified. 
    CHAN=hhhh  FEPERR records containing the hexadecimal channel number 
               specified. 
fi_optlist   specifies one or more of the following options separated 
by a comma: 
    Option       Description 
    ------       ----------- 
    COD[E]=dd    FI records containing the specified decimal file 
                 management error CODE for the file inconsistency. 
    REA[SON]=dd  FI records containing the specified decimal REASON for 
                 the file inconsistency. 
    ACT[ION]=d   FI records containing the specified ACTION taken by file 
                 management in response to the file inconsistency. 
Description: 
This command sets parameters that determine which error records to include in 
a subsequent report.  Specifying ADD or DELETE, adds or removes previously set 
options. 
Examples: 
elan:MATCH MAJ=43 
elan:MATCH MAJ=42, SUB=01 
elan:MATCH MAJ=42, SUB=02, MED=1046 
elan:MATCH BYTE 3, BIT 1 = 0 
elan:MATCH BYTE 3 = 11110101 
elan:MATCH FCG=GNS, CHAN=2380 
elan:MATCH CHAN=4C00 
elan:MATCH ACT=8 
elan:MATCH COD=39,REA=5 
00002
00003
00001
           PRI/  NEW    TIME OF 
TIME  DEV  SEC  STATE STATE CHANGE  VSN  MIRROR   ACCT     UNAME    SYSID 
____  ____ ____ _____ ____________  ___  ______  ______   ________  _____ 
08:06 DP05  P   OPR    8:06:20.91   167   DP06   MAJHOST  102JONES  30339 
08:06 DP06  S   OPER   8:06:20.91     0   DP05   MAJHOST  102JONES  30339 
A MIRROR entry is logged whenever a Mirrored Disk is created, 
terminated, or changes the state of its Mirrored Disk operation. 
MIRROR Entry Headers: 
Header                       Meaning 
------                       ------- 
TIME                         Time this entry was logged. 
DEV                          Device name. 
PRI/SEC                      Primary or secondary Mirrored Disk device. 
NEW STATE                    New Mirrored Disk state for this device. 
TIME OF STATE CHANGE         Time the state change took place. 
VSN                          VSN of this device 
MIRROR                       Device which is mirror to the device 
                             listed under DEV. 
ACCT                         Account of user making this change. If 
                             no user was associated with this change, 
                             then this will be blank. 
UNAME                        User name of user making this change. If 
                             no user was associated with this change, 
                             then this will be blank. 
SYSID                        Sysid of the user making this change. If 
                             no user was associated with this change, 
                             then this will be 0. 
DSMT
An MPCSTAT entry is a statistical entry gathered from counters in the EURC and 
IPC unit-record controllers.  The firmware in these controllers maintains 
statistical counters pertaining to the activity on all its ports.  The 
controllers are polled and an MPCSTAT entry is logged in the error log every 
30 minutes.  The counters are reset at the time of the poll and whenever the 
firmware is rebooted. 
Raw Report Headers: 
Header                       Meaning 
------                       ------- 
MPC NAME                     Name of unit-record controller. 
FW NAME                      Name of firmware currently installed in 
                             controller. 
CARDS READ                   Total number of cards read (on all ports). 
CARDS PUNCHED                Total number of cards punched (on all ports). 
LINES PRINTED                Total number of lines printed (on all ports). 
PAGES PRINTED                Total number of pages printed (on all ports). 
IOM WD TRANS                 Total number of word transfers on IOM 
                             interface (for all ports). 
LOST INTS                    Lost interrupt count. 
UNSOL FRAMES                 Number of unsolicited frames. 
TR/REC ERRORS                Total number of PDSI transmitter and receiver 
                             errors (on all ports). 
Extended Report Headers: 
Header                       Meaning 
------                       ------- 
FW                           Firmware name. 
PDSI RECEIVER ERRORS         Number of transmission errors across the PDSI 
                             link (detected by the controller when 
                             receiving data). 
PDSI TRANSMITTER ERRORS      Number of transmission errors across the PSDI 
                             link (detected by the controller when 
                             transmitting data). 
CARDS PUNCHED                Number of cards punched. 
CARDS READ                   Number of cards read. 
FRAMES RECEIVED OVER PDSI    Number of frames of data received by the 
                             controller over the PDSI link. 
FRAMES TRANSMITTED OVER PDSI Number of frames of data transmitted by the 
                             controller over the PDSI link. 
CONNECT PCWS                 Number of connects issued to the controller by 
                             the IOM. 
PCWS ON IOM INTERFACE        Number of PCW commands (other than connects) 
                             issued to the controller by the IOM. 
IOM INTERFACE TRANSACTIONS   Number of transactions across the IOM 
                             interface. 
IOM INTERFACE WD TRANSFERS   Number of words transferred across the IOM 
                             interface. 
LINES PRINTED                Number of lines printed. 
RETRANSMISSIONS OVER PDSI    Number of retransmissions across the PDSI 
                             interface. 
PAGES PRINTED                Number of pages printed. 
ELAPSED TIME                 Time in minutes since last firmware boot. 
LOST INTERRUPTS              Number of interrupts issued to a device for 
                             which there was no response. 
UNSOLICITED FRAMES           Number of unsolicited frames transmitted 
                             across PDSI link. 
PROM xx                      Revision of firmware in read-only memory. 
CONFIG                       PROM configuration byte.  Indicates which type 
                             of firmware is present in the application 
                             PROMs. 
A MSOSSAYS entry is logged where MSOS initiates a dialogue with the CP-6 host 
in order to coordinate resource management between them. 
Header          Meaning 
------          ------- 
IOP             The IOP in which this dialogue is initiated. 
MSOS REQUEST    The type of request that is given by MSOS. 
TO CP6 
COMMAND BLOCK   The octal 4 words and 1 byte of the logged record. 
Format: 
OC[TAL] 
Description: 
The OCTAL command causes selected information to be dumped in octal with ASCII 
translation.  This option is only meaningful with the REPORT RAW and REPORT 
DETAIL commands. 
The default is OCTAL not set. 
00001
An OPER entry is logged when an operator keyin is issued at a console to 
control devices.  The time of the message is displayed with the keyin message 
following.  An example of an OPER entry: 
    <<<< OPERATOR INPUT >>>> 
   07:45: CRASH FEP 1 TO TRY TO CLEAR SYNC LINES... 
An OSFI entry is logged whenever an output symbiont file inconsistency is 
detected.  The following is a list of headers displayed to identify items from 
an OSFI entry. 
Header          Meaning 
------          ------- 
AVAIL           Number of words left in the current output 
                symbiont granule. 
EXPSTAMP        Expected stamp if stamp error; otherwise NAVX. 
FRDAD           File Relative Disk ADdress. 
SUBC            Subcode: 1 = bad granule stamp 
                         2 = bad format: NAVX + AVAIL > 1024 
STAMP           Stamp from granule. 
SYSID           File sysid; 0=banner file. 
Several ELAN reports make references to performance values for system 
components.  This value is calculated by the formula: 
    1 - (error/connects) 
Every system component has two thresholds associated with it: the ALERT and 
the ATTEN thresholds.  These threshold values are used for comparison with the 
performance values of components being reported.  A component having the 
current performance value below either of its thresholds will be flagged as 
such in certain ELAN reports.  The ATTEN threshold indicates degraded 
performance, but nothing too serious.  The ALERT threshold indicates a 
condition requiring immediate correction by the Customer Service Engineer. 
    Use of ELAN requires the SPCLMM privilege or the EL processor privilege. 
Two types of errors cause a processor error log entry to be created.  The more 
serious error, an unexpected fault, is a fault that does not appear to be 
caused by software.  This type of error (e.g., parity faults, 
operation-not-complete faults) is indicated by a non-zero fault code entry. 
For this type of error, the Detail Report also contains the corresponding 
safe-store frame and processor history registers. 
The second and less serious error is a correctable CPU error condition.  This 
type of error (e.g., correctable ECS error on DPS 8/44, cache directory write 
notification buffer overflow on DPS 8/70) is indicated by a zero fault code. 
The following is a list of headers displayed to identify items from PROCERR 
entries. 
Header          Meaning 
------          ------- 
FAULT CODE      If non-zero, this entry is the 5-bit fault code 
                from bits 12-16 of safe-store word 5.  The most 
                common hardware faults are: 
                9 (decimal)    Parity fault 
                11 (decimal)   Operation-not-complete fault 
                If the fault code is zero, this is a report of a 
                correctable CPU error and the only other 
                meaningful fields are PORT# and FAULT REGISTER 
                CONTENTS. 
FAULT CODE:     Interpretation of FAULT CODE. 
FAULT           For unexpected faults, the contents of the memory 
INSTRUCTION     location specified by IC at the time of the fault. 
FAULT REGISTER  Contents of the processor fault register after either 
                the unexpected fault occurred or the correctable CPU 
                error condition was detected.  Usually, the first 
                word is meaningful only for unexpected faults and 
                the second word is meaningful only for 
                correctable CPU error conditions. 
FAULT REGISTER 
INTERPRETATION: Interpretation of FAULT REGISTER. 
IC              For unexpected faults, Instruction Counter at the 
                time of the fault from bits 0-17 of safe-store 
                word 4. 
ISR WSR         For unexpected faults, this field is the ISR 
                working space register type field from bits 29-31 
                of safe-store word 10.  This identifies the 
                running domain at the time of the fault.  Common 
                values are: 
                Value  Meaning 
                0      Monitor running 
                7      Slave user program running. 
PORT#           Port number of the CPU on which the unexpected 
                fault or correctable CPU error condition 
                occurred. 
PROC TYPE       CPU type on which the error occurred. 
                Value  Meaning 
                0      Level 66 type CPU 
                1      DPSE (8/50, 8/52, 8/62, 8/70) type CPU 
                2      ELSI (8/20, 8/44, 8/47, 8/49) type CPU 
                3      DPS 88 type CPU 
                4      DPS 90 EPU not in XA mode 
                5      DPS 90 EPU in XA mode 
                6      DPS 8000 CPU 
SYSID           For unexpected faults, this field is the sysid of 
                the current user on the faulting CPU at the time 
                of the fault. 
Format: 
PROM[PT] 'char_string' 
Parameters: 
'char_string'    is 1-28 ASCII graphics characters enclosed in single quotes. 
Description: 
The PROMPT command allows the user to change ELAN's prompt string from elan: 
to another string of characters or a single prompt character. 
Examples: 
elan:PROMPT 'Command?' 
Command?PROMPT '>' 
> 
00002
00003
00001
END
A RECOV entry is either a SCREECH, SNAP, or SUA entry. See SCREECH/SNAP/SUA 
Entries for descriptions. 
    CP-6 maintains information about system activity in a daily error log 
    file.  The name of this file is :ERRLOGyyyymmdd, where the 'yyyymmdd' is 
    the ANS format for date.  These daily files are maintained in the :SYSTAC 
    account.  The length of time that these files are saved is at the 
    discretion of the system manager; a minimum of 30 days is recommended. 
    The system maintains another file in :SYSTAC to keep track of the 
    performance of system components.  This file, called :DEVHIST, maintains a 
    history of error counts and connect counts for the entire system for the 
    past 30 days.  It also contains all the information about the 
    configuration of the system.  The information in this file is used to 
    generate the SYS and AMS reports.  :DEVHIST contains one record per 
    component per day.  These records are created by combining the :CONFIG 
    file with the IOERR records for each system component from the day's error 
    log.  ELAN updates the :DEVHIST file after all tape boots to represent the 
    current configuration.  To build a new :DEVHIST file, first delete or 
    rename the original :DEVHIST file, then invoke ELAN specifying the REBUILD 
    option as follows: 
        !ELAN (REBUILD) 
    Note that, if the REBUILD option is specified and the original :DEVHIST 
    file exists, the file will be sized down to 30 days of information.  If 
    information prior to that time is important, the original file should be 
    saved under a different name. 
Format: 
                [    {device}] [{TO  }    ] 
RE[PORT] repopt [FOR {model }] [{ON  } fid] 
                [    {class }] [{OVER}    ] 
                [    {ALL   }] [{INTO}    ] 
Parameters: 
repopt    specifies which report format is desired, as follows: 
    AMS        Anticipatory Maintenance Summary 
    CONFIG     Configuration Report 
    DETAIL     Detailed error log listing 
    EXTENDED   Extended detail error log listing 
    HWE        Hardware Error Report 
    RAW        Raw error log listing 
    SUM        Error log summary 
    SYS        System summary 
    UPR        Unit Performance Report 
{device|model|class|ALL}    specifies the device(s) to be included in the 
report.  To specify a device, the particular model or device is entered, e.g., 
MTU0610 or MT01.  To specify a class, the appropriate class designator is 
entered, e.g., MT, DP, etc.  The legal class designators are listed below. 
The default is FOR ALL. 
Class     Description 
-----     ----------- 
AC        Array Processor Controllers 
AP        Array Processors 
ALL       All system components 
CONSOLE   System consoles 
CP        Card punches 
CR        Card readers 
DC        Disk controllers 
DP        Disk drives 
FEP       Front-end Processors 
IOM       All IOMs 
LP        Line printers 
MC        Maintenance Channel interface 
MEM       Memory 
MP        All MPCs 
MT        Magnetic tape (9 track) 
OD        Optical disks 
OPTC      Optical disk controllers 
SC        System consoles 
TC        Tape controllers 
UC        Unit record controllers 
{TO|ON|OVER|INTO}    directs ELAN output to the specified file identifier. 
The default is ON ME. 
Description: 
This command determines the type of report to be produced and initiates 
production of the report. 
00002
00001
The entries that appear in ELAN reports correspond to an error type that may 
be included in reports via the ERROR command.  See the HELP topic HELP (ELAN) 
ERROR and the report entry HELP topics HELP (ELAN) ANLZ, FEPCRASH, FEPERR, FI, 
GABRT, IOERR, PROCERR, SCREECH, SNAP, SPURINT, SUA, SYSCON, SYSID, and ZAP. 
Format: 
RES[ET] [criterialist] 
Parameters: 
criterialist    is any of ERROR/SELECT, SPAN, MATCH, EXCLUDE, OCTAL, or USE. 
No criteria list means reset all criteria to their defaults. 
Description: 
The RESET command causes all or specified criteria to be reset to their 
default values. 
00002
00001
One of these entries is logged any time a Screech, SNAP, or SUA occurs.  The 
following is a list of the headers displayed to identify items from a 
Screech/SNAP/SUA entry. 
Header          Meaning 
------          ------- 
DUMP FILE       Dump file name. 
DUMP FLAGS      Dump flags indicating to RCVR2 what portions of 
                memory are to be written to the dump file. 
None            If RCVR2 trapped while performing the recovery, 
                'TRAPPED' appears on the entry line. 
SCREECH CODE    SCREECH code. 
SNAPU#          User number of the snapped user, when other than 
                the current user is requested via an option of 
                the SNAP command. 
ERROR
SCREECH
Format: 
SP[AN] {start [-stop]} 
       {-stop        } 
Parameters: 
start and stop    specify any of the following: 
    hh:mm 
    mm/dd/yy 
    hh:mm,mm/dd/yy 
    hh:mm mm/dd/yy 
    mm/dd/yy,hh:mm 
    mm/dd/yy hh:mm 
The default for start is 00:00 of the present day; the default for stop is 
23:59 of the present day. 
Description: 
The SPAN command allows specification of a time constraint.  Only information 
occurring in the time span specified will be reported. 
00002
00001
A SPURINT entry is logged whenever a spurious interrupt is received by the I/O 
system.  The following is a list of headers displayed to identify items from 
the SPURINT entry. 
Header          Meaning 
------          ------- 
I-CCC           IOM-Channel reporting the interrupt. 
INTLVL          Interrupt level. 
STATE           Scheduling state of the channel. 
STATUS WORDS    Contents of two status words. 
T & D           Current T & D function. 
Format: 
ST[ATUS] 
Description: 
The status command allows the user to see any of his selection criteria that 
have been set.  This command will display the current time constraint at all 
times.  Current MATCH/EXCLUDE options, error types, or octal display will only 
be displayed if any criteria have been established. 
00001
SCREECH
A SYSCON entry is logged any time the SYSCON processor is used to partition, 
return, or set flags for a device.  The following is a list of headers 
displayed to identify items from a SYSCON entry. 
Header          Meaning 
------          ------- 
ACCOUNT,        Identification of the user who performed the 
USER NAME,      SYSCON activity. 
SYSID 
COMP            Type of component that was affected:  DVC=device, 
                CHAN=channel, FEP=front-end processor, 
                MPC=micro-programmed controller, IOM=input/output 
                multiplexor, CPU=central processing unit, SCU=system 
                control unit 
DEVNAME         If COMP=MPC or DVC, this entry gives the device 
                name of the component affected, e.g., DP01, DC01. 
                If COMP=IOM, this entry gives the relative IOM#, e.g., 
                IOM1.  If COMP=SCU or CPU, this entry indicates the 
                port number, e.g., CPU7. 
FUNCTION        Specifies the function performed:  PARTITION, 
                RETURN, SETFLAG, DISPLAY, or RELEASE. 
I-CCC           If COMP=CHAN, I-CC is the IOM-Channel number of 
                the channel affected.  If COMP=FEP, this entry 
                identifies the FEP affected. 
A SYSID entry is logged on every system start-up, e.g., tape boot, disk boot, 
or recovery.  The following is a list of headers displayed to identify items 
from the SYSID entry. 
Header          Meaning 
------          ------- 
ANSPROT         Level of ANS tape protection in the system. 
                0 = unprotected system 
                1 = semi-protected system 
                2 = fully-protected system. 
SITE ID         Unique site ID assigned by Bull Marketing. 
SITE NAME       Site name. 
TIMESTAMP       Universal Time Stamp (UTS) for the creation of 
                the Monitor. 
VERSION         System version, of the form vvvb, where vvv is 
                the version of the CP-6 system and b is 
                represents the 'new files' boot level; b is 
                initially set to 'A' and is incremented (A-Z, 
                a-z, 0-9) for each 'boot under files'. 
Format: 
         [    {device}] 
TH[RESH] [FOR {model }] [atten-alert = nn[.nn] [,atten-alert = nn[.nn]]] 
         [    {class }] 
         [    {ALL   }] 
Parameters: 
{device|model|class|ALL}    specifies that this threshold is to be set for all 
or for specific devices.  See description in the REPORT command.  The default 
is ALL. 
atten-alert    specifies either one or both of the following options.  If both 
are specified, they must be separated by a comma.  (The order of 
specifications is not meaningful).  atten-alert options are: 
    ATTEN    is the threshold for conditions causing degraded performance. 
    ALERT    is the threshold for conditions requiring immediate correction. 
nn[.nn]    specifies the threshold value as a percentage.  If .nn is not 
specified, .00 is assumed.  Type HELP (ELAN) PERFORMANCE_VALUES for additional 
explanation.  If atten and alert are omitted, the current thresholds for the 
specified components are displayed. 
Description: 
The THRESH command allows the user to establish and display the ATTEN and 
ALERT thresholds that will be used by ELAN when reporting on the performance 
of system components. 
00002
00001
DATE
A TIMESTAMP entry is made every hour on the hour, and consists of the word 
"TIMESTAMP" followed by the current time (hh:mm, using a 24-hour clock). 
Format: 
USE .acct 
Parameters: 
 .acct    specifies the account containing :ERRLOG files. 
Description: 
The USE command allows the user to redirect ELAN to the specified account 
where :ERRLOG files are to be found.  These files must have names of the form 
:ERRLOGyyyymmdd.  This command must be followed by a SPAN command to supply a 
time span for subsequent reports. 
00002
00001
END
A ZAP entry is logged any time a ZAP! keyin is entered from a system console. 
The following is a list of headers displayed to identify items in a ZAP entry. 
Header          Meaning 
------          ------- 
OPERATOR TEXT   Optional text entered with the ZAP! keyin. 
STATION         Console from which the ZAP! keyin was entered. 
