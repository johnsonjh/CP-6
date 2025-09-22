The MIRROR processor is used to create, display, update, manipulate and 
terminate Mirrored Disk devices on CP-6. It reads commands from the user, and 
generates listings and diagnostics from the execution of those commands. 
For additional information about MIRROR, type any of the following: 
HELP (MIRROR) INVOKING         For information on how to 
                               invoke the MIRROR processor. 
HELP (MIRROR) COMMAND_SUMMARY  For a a brief description of 
                               each command. 
HELP (MIRROR) command          For the format of a specific 
                               command or option. Type ? or 
                               ?? for more information. 
HELP (MIRROR) command PARAM    For parameter information on a 
                               particular command or option. 
HELP (MIRROR) command DESC     For the description of a 
                               particular command or option. 
HELP (MIRROR) command USAGE    For usage information on a 
                               particular command or option. 
HELP (MIRROR) TOPICS           For a list of all MIRROR HELP 
                               topics. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
DO
COMMAND_SUMMARY
The following are commands accepted by MIRROR: 
  Command               Description 
COMPARE         Compare Mirrored Disk pair. 
COPY            Copy operational Mirrored Disk to another 
                Mirrored Disk. 
DATE|TIME       Display the current date and time. 
DISPLAY         Display Mirrored Disk device information. 
DIRECTORY       Change the default account and packset. 
DO              Execute an IBEX command from within MIRROR. 
DONT MIRROR     Terminate Mirrored Disk pair. 
END|QUIT|EXIT   Exit MIRROR. 
ENTER           Invoke a CP-6 ADAPT dialog from within this 
                processor. 
ERASE           Delete accumulated output for logical devices. 
FAIL            Change Mirrored Disk state to FAILed. 
HELP            Obtain processor information. 
LOCK            Lock Mirrored Disk device. 
MIRROR          Create Mirrored Disk device pair. 
OUTPUT          Send subsequent output to fid. 
PRINT           Send output accumulated for logical devices to 
                the destination. 
SWITCH          Switch primary Mirrored Disk device. 
UNLOCK          Unlock Mirrored Disk device. 
Enter: 'HELP (MIRROR) command' for information on a specific command. 
Format: 
COMPARE DPxx WITH DPyy [ ( options ) ] 
Parameters: 
DPxx  specifies the primary Mirrored Disk device that is to be compared. 
DPyy specifies the secondary Mirrored Disk device that is to be compared. DPyy 
    must be the secondary Mirrored Disk device for DPxx. 
options  are one or more of the following, separated by commas: 
        {GRANS|GRANULES} = nn 
        MXDIFF = nnnnnn 
        NREPORT 
        PAUSE = tttttt [ { SECONDS | MS } ] 
        REPORT [ = nn ] 
    For a description of an option type 'HELP (MIRROR) OPTIONS option_name'. 
Description: 
The COMPARE command is used to compare the contents of a Mirrored Disk pair. 
Both Mirrored Disk devices must be OPERational.  DPxx must be a primary 
Mirrored Mirrored Disk device.  DPyy must be a mirror of DPxx. 
Once these test have been successfully completed, MIRROR starts comparing the 
contents of the Mirrored Disk pair.  The comparison starts with granule 
DRZERO.  The comparison continues until either the maximum number of 
differences specified by the MXDIFF option are found or the entire device has 
been compared. 
If the comparison finds no differences, the STEPCC is set to zero (if no other 
errors are detected by MIRROR).  If the comparison does find differences, the 
STEPCC is set to five (5). 
Usage Notes: 
1.  DRZERO for each Mirrored Disk is established when the Mirrored Disk pair 
    is linked together.  Normally, DRZERO is 0 for all Mirrored Disk pairs. 
    However, if the first packset on the Mirrored Disk devices is DP#CP-6'S, 
    then DRZERO is set to the beginning of the second volume (usually DP#SYS). 
2.  The VID in granule 0 can be different for each Mirrored Disk device.  But 
    when both Mirrored Disks are OPERational, the VIDs of the devices should 
    be identical. 
00002
00001
00003
Format: 
COPY DPxx OVER DPyy [ ( options ) ] 
Parameters: 
DPxx specifies a Mirrored Disk device that is to be copied from. DPxx must be 
    an OPERational Mirrored Disk device. 
DPyy specifies a Mirrored Disk device that will be copied to. DPyy must be a 
    FAILed Mirrored Disk device. 
options  are one or more of the following separated by commas: 
        {GRANS|GRANULES} = nn 
        NREPORT 
        PAUSE = tttttt [ { SECONDS | MS } ] 
        REPORT [ = nn ] 
    For a description of an option type 'HELP (MIRROR) OPTIONS option_name'. 
Description: 
The COPY command is used to copy the contents of an OPERational Mirrored Disk 
device over a FAILed Mirrored Disk device.  The COPY command can be used only 
on an existing Mirrored Disk pair.  (The MIRROR command can be used to create 
a Mirrored Disk pair.) 
Once these tests have been successfully completed, MIRROR changes the state of 
DPyy to RESToring.  The VID of DPyy is not updated at this time. 
MIRROR then starts copying DPxx over DPyy.  The copy is done GRANS granules 
per read/write.  There is a pause of PAUSE seconds/milliseconds at the end of 
the read/write loop. 
When the copy successfully completes, MIRROR changes the state of DPyy to 
OPERational.  The VID of DPyy is updated at this time. 
MIRROR uses monitor services to copy device DPxx over device DPyy.  The 
copying starts with granule one (i.e., the first granule after the VID).  The 
copying always starts with granule one even if DRZERO is greater than one. 
This allows a Mirrored Disk device that contains DP#CP-6'S to be used after a 
reconfiguration (i.e., MXT) boot in case of a device failure.  Starting the 
copy at granule one copies DP#CP-6'S.  If DP#CP-6'S is not copied, the 
mirrored copy can not be booted to in case of a device failure. 
Usage Notes: 
1.  The COPY command can be used only after a FAIL command has been used to 
    change the state of a Mirrored Disk device to FAILed. 
2.  The COPY command cannot be used after a Mirrored Disk pair has been 
    terminated either through an irrecoverable I/O error or through the use of 
    the DONT MIRROR command.  In either of these cases, the MIRROR command 
    must be used to reestablished a Mirrored Disk pair. 
00002
00001
00003
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format 
for the display is: 
mmm dd 'yy hh:mm   (month)(day)(year)(hours)(minutes) 
Examples: 
*DATE 
requests a display of the current data and time.  A sample display is: 
AUG 10  '88  11:03 
00001
00002
The MIRROR processor uses the following DCBs: 
  DCB        Usage 
M$DO       Diagnostic output. 
M$EI       Read first Mirrored Disk device. 
M$EO       Read/write second Mirred Disk device. 
M$LO       Listed output (DCB4). 
M$ME       Output greeting. 
M$SI       Read commands (DCB1). 
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
DISPLAY [ ALL | DPxx [, DPyy, ... ] 
Parameters: 
ALL  specifies all disk devices on the system. 
DPxx, DPyy, ...  specifies a list of disk devices to be displayed. 
Description: 
The DISPLAY command is used to display the Mirrored Disk information for 
either all or specified disk devices on the system. 
00002
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
DONT MIRROR DPxx 
Parameter: 
DPxx specifies a Mirrored Disk device. DPxx must be in either the OPERational 
    or WAIT state. 
Description: 
The DONT MIRROR command is used to terminate Mirrored Disk operation for a 
Mirrored Disk device.  This command will be accepted only for Mirrored Disk 
devices in either the OPERational or WAIT states. 
If DPxx is a Mirrored Disk device that is OPERational, DPxx would continue to 
be used by the system as a nonmirrored disk device.  The mirror of DPxx would 
become a single volume scratch pack and would not be recognized by the system 
as a CP-6 pack. 
If DPxx is a Mirrored Disk device that is WAITing for its mirror device to be 
found, DPxx may or may not be used by the system.  If the VSN of the device is 
unique, DPxx will be used by the system as a nonmirrored disk device.  If the 
VSN of the device is not unique, DPxx will not be recognized by the system as 
a CP-6 pack. 
00002
00001
Format: 
{ END | QUIT | XIT } 
Description: 
The END command is used to terminate the MIRROR program. 
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
END
Format: 
FAIL DPxx 
Parameter: 
DPxx  specifies a Mirrored Disk device. 
Description: 
The FAIL command is used to change the state of a Mirrored Disk device to 
FAILed.  This command is accepted only for a Mirrored Disk device whose mirror 
is OPERational. 
Usage Note: 
The FAIL command is used to force a Mirrored Disk into the FAILed state.  This 
is usually done after the COMPARE command showed that the contents of the two 
Mirrored Disk devices were different.  The user selects one of the two 
Mirrored Disk devices to FAIL, and then uses the COPY command to restore both 
devices to normal Mirrored Disk operation. 
00002
00001
00003
Format: 
HELP [(processor)] [TOPICS] [keyword1] [-] [keyword2] 
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
For more detailed information, type: 
!HELP HELP PARAMETERS 
Description: 
HELP prints information. 
HELP messages have levels.  Once the initial level has been printed, typing a 
question mark prints the next level, usually containing greater detail. 
Typing two question marks prints the entire message. 
Any standard HELP file (even those for other processors) can be accessed with 
the HELP command. 
For more detailed information, type: 
!HELP HELP DESCRIPTION 
Examples: 
    HELP (MIRROR) COMPARE 
For more detailed information, type: 
!HELP HELP EXAMPLES 
Usage Notes: 
1.  The standard CP-6 HELP facility is used by MIRROR so the user can get help 
    on any other CP-6 processor by entering: 
        HELP (processor) [TOPICS] [keyword1] [-] [keyword2] 
    For more detailed information type:  !HELP HELP NOTES 
00002
00003
00004
00001
00004
A 
  ANLZ -   
    OUTPUT Command - 
      HELP OUTPUT FORMAT: 
C 
  COMPARE Command - 
      HELP COMPARE 
  COPY Command - 
      HELP COPY 
D 
  Data Control Blocks (DCBs) for MIRROR - 
      HELP DCBS 
  DATE Command - 
      HELP DATE 
  Defective Track Table - 
      HELP OVERVIEW_OF_MIRRORED_DISKS 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DISPLAY Command - 
      HELP DISPLAY 
  DO Command - 
      HELP DO 
  DONT MIRROR Command - 
      HELP DONT_MIRROR 
  DP#CP-6'S - 
      HELP OVERVIEW_OF_MIRRORED_DISKS 
  DTT - 
      HELP OVERVIEW_OF_MIRRORED_DISKS 
E 
  END Command - 
      HELP END 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
F 
  FAIL Command - 
      HELP FAIL 
G 
  GRANS Option - 
      HELP GRANS 
H 
  HELP Command - 
      HELP HELP 
I 
  Invoking MIRROR - 
      HELP INVOKING 
L 
  LOCK Command - 
      HELP LOCK 
M 
  MIRROR -   
    COMPARE Command - 
      HELP COMPARE FORMAT: 
    COPY Command - 
      HELP COPY FORMAT: 
    DCBs - 
      HELP DCBS 
    DISPLAY Command - 
      HELP DISPLAY FORMAT: 
    DONT MIRROR Command - 
      HELP DONT_MIRROR FORMAT: 
    END Command - 
      HELP END FORMAT: 
    FAIL Command - 
      HELP FAIL FORMAT: 
    GRANS Option - 
      HELP GRANS FORMAT: 
    invoking - 
      HELP INVOKING 
    LOCK Command - 
      HELP LOCK FORMAT: 
    MIRROR Command - 
      HELP MIRROR FORMAT: 
    modes - 
      HELP PRIVILEGES 
    MXDIFF Option - 
      HELP MXDIFF FORMAT: 
    NREPORT Option - 
      HELP NREPORT FORMAT: 
    PAUSE Option - 
      HELP PAUSE FORMAT: 
    privileges - 
      HELP PRIVILEGES 
    REPORT Option - 
      HELP NREPORT FORMAT: 
    SWITCH Command - 
      HELP SWITCH FORMAT: 
    UNLOCK Command - 
      HELP UNLOCK FORMAT: 
  MIRROR Command - 
      HELP MIRROR 
  MIRROR Command Summary - 
      HELP COMMAND_SUMMARY 
  MIRROR Commands - 
      HELP MIRROR_COMMANDS 
  MIRROR Options - 
      HELP OPTIONS 
  Mirrored Disks -   
    DTT - 
      HELP OVERVIEW_OF_MIRRORED_DISKS 
    overview - 
      HELP OVERVIEW_OF_MIRRORED_DISKS 
    VSN - 
      HELP OVERVIEW_OF_MIRRORED_DISKS 
  MXDIFF Option - 
      HELP MXDIFF 
N 
  NREPORT/REPORT Options - 
      HELP NREPORT 
O 
  OUTPUT Command - 
      HELP OUTPUT 
  Overview of Mirrored Disks - 
      HELP OVERVIEW_OF_MIRRORED_DISKS 
P 
  PAUSE Option - 
      HELP PAUSE 
  PRINT Command - 
      HELP PRINT 
  Privileges for Using MIRROR - 
      HELP PRIVILEGES 
S 
  SWITCH Command - 
      HELP SWITCH 
U 
  UNLOCK Command - 
      HELP UNLOCK 
V 
  Volume Serial Number - 
      HELP OVERVIEW_OF_MIRRORED_DISKS 
  VSN - 
      HELP OVERVIEW_OF_MIRRORED_DISKS 
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
HELP_INDEX
INVOKING
INVOKING
Syntax:          !MIRROR [fid1] [{ON|TO|OVER|INTO},fid2] 
Parameters: 
fid1             specifies an optional fid from which commands are 
read. The default is the command stream (CR#) or M$SI. 
fid2             specifies an optional fid into which listed output 
would be printed. The default is the listing output device or M$LO. 
Example: 
    !MIRROR 
    MIRROR E04 here 
    <Mirror> 
MIRROR uses XUG$GETCMD to read commands through M$SI (DCB#1).  Listed output 
is written through M$LO (DCB#4).  Diagnostic output is written through M$DO. 
The first Mirrored Disk device specified is read through M$EI.  The second 
Mirrored Disk device specified is read/written through M$EO. 
Format: 
LOCK DPxx 
Parameter: 
DPxx specifies a Mirrored Disk device. 
Description: 
The LOCK command is used to lock a Mirrored Disk device.  Only the user who 
locked a Mirrored Disk device can do I/O to that device.  All other users have 
their I/Os held by the system until the Mirrored Disk device is unlocked. 
Usage Note: 
This command should be used only in testing the MIRROR program or Mirrored 
Disk devices.  Locking a Mirrored Disk device prevents other users from doing 
I/O to the locked device.  Preventing users from doing I/O to a Mirrored Disk 
device can cause these users to appear to be hung SIOW. 
00002
00001
00003
Format: 
MIRROR DPxx OVER DPyy [ ( options ) ] 
Parameters: 
DPxx  specifies a nonmirrored disk device. 
DPyy  specifies a nonmirrored disk device. 
options  are one or more of the following separated by commas: 
        {GRANS|GRANULES} = nn 
        NREPORT 
        PAUSE = tttttt [ { SECONDS | MS } ] 
        REPORT [ = nn ] 
    For a description of an option type 'HELP (MIRROR) OPTIONS option_name'. 
Description: 
The MIRROR command is used to create a Mirrored Disk pair.  The devices used 
to create a Mirrored Disk pair must not currently be Mirrored Disk devices. 
The VSN, DTT, and size of the devices used to create a Mirrored Disk pair must 
be identical. 
If both devices contain a single scratch volume with the same VSN, then both 
devices are made OPERational immediately. 
If DPxx is not a single scratch volume, then DPyy must be a single scratch 
volume with the same VSN.  If DPyy is not a single scratch volume with the 
same VSN, the MIRROR command prints an error message and aborts the execution 
of the command. 
If DPxx is not a single scratch volume and DPyy is a single scratch volume 
with the same VSN, then DPxx is made OPERational and DPyy is made FAILed.  The 
MIRROR command then executes the COPY command to copy DPxx over DPyy.  When 
the COPY command completes successfully, DPyy is made OPERational. 
00002
00001
The MIRROR COMPARE, COPY, and MIRROR commands accept options.  The options are 
enclosed in parenthesis and separated by commas.  The following is a list of 
options accepted by these commands: 
    {GRANS|GRANULES} = nn 
    MXDIFF = nnnnnn 
    NREPORT 
    PAUSE = tttttt [ { SECONDS | MS } ] 
    REPORT [ = nn ] 
Not all options are accepted by each command.  For a description of an option 
type 'HELP (MIRROR) OPTIONS option_name'. 
Format: 
{ GRANS | GRANULES } =  nnn 
Parameter: 
nnn  specifies the number of granules.  nnn 
     must be between 1 and 255.  The default is 64. 
Description: 
The GRANS option specifies the maximum number of granules to be read for each 
read and written on each write. 
Larger values of nnn make the command run faster, but also increase the I/O 
wait time for other users.  Smaller values of nnn make the command run slower, 
but also limit the increase in I/O wait time for other users. 
Usage Note: 
This option is accepted by the COMPARE, COPY, and MIRROR commands. 
Format: 
MXDIFF = nnnnnn 
Parameter: 
nnnnnn specifies the maximum number of differences. nnnnnn is a decimal 
    integer from 1 to 999999.  The default is 1,000,000 (so that the entire 
    device will be compared before termination). 
Description: 
The MXDIFF option specifies the maximum number of differences that the COMPARE 
command will accept before terminating the comparison. 
Usage Note: 
This option is accepted only by the COMPARE command. 
Format: 
{NREPORT|REPORT [ = nn ] } 
Parameters: 
nn  specifies the percentage completion interval to be used to generate the 
    report.  nn is a decimal integer from 1 to 99. 
Description: 
The NREPORT option specifies that no report is to be displayed as the command 
executes. 
The REPORT option specifies that the percentage completion message is to be 
displayed as the command executes.  The display is done every time the 
percentage of completion increases by the percentage specified.  Because of 
the number of granules specified on the GRAN option, the reporting may not 
occur exactly on the percentage specified. 
The default is REPORT = 10 (i.e., report the percentage completion every 10 
percent). 
Usage Note: 
These options are accepted by the COMPARE, COPY, and MIRROR commands. 
Format: 
PAUSE =  ttttt [ { SECONDS | MS } ] 
Parameters: 
tttttt specifies the number of seconds or milliseconds. tttttt must be between 
    0 and 999999. 
SECONDS  specifies that tttttt is in seconds. 
MS  specifies that tttttt is in milliseconds. 
    The default is 0 SECONDS. 
Description: 
The PAUSE option specifies the amount of time to wait at the end of the 
COMPARE or COPY loop.  This pause is available to prevent the MIRROR program 
from degrading system performance for other users too severely. 
Larger values of ttttt make the command run slower, and allow other I/O users 
a greater opportunity to do I/O.  Smaller values of ttttt make the command run 
faster, but also reduces the opportunity for other users to do I/O. 
Usage Note: 
This option is accepted by the COMPARE, COPY, and MIRROR commands. 
00001
00002
00003
00004
00003
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
The MIRROR processor requires that the user be authorized for the SPCLMM, IOQ, 
and IOQW privileges. The MIRROR program executes in either online, batch, or 
ghost mode. 
END
COMMAND_SUMMARY
Format: 
SWITCH [ PRIMARY TO ] DPyy 
Parameter: 
DPyy  specifies a secondary Mirrored Disk device that is OPERational. 
Description: 
The SWITCH command is used to switch the primary Mirrored Disk device to the 
specified device.  This command is accepted only for a secondary Mirrored Disk 
device that is OPERational. 
00002
00001
INVOKING
DATE
Format: 
UNLOCK DPxx 
Parameter: 
DPxx specifies a Mirrored Disk device. 
Description: 
The UNLOCK command is used to unlock a Mirrored Disk device. 
Usage Note: 
This command should be used only with the LOCK command in testing the MIRROR 
program and Mirrored Disk devices. 
00002
00001
00003
END
