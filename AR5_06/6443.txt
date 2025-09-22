The SYSCON processor is used to control and display the availability of 
various components of the hardware of a CP-6 system, and to set various 
parameters for these components. 
For more information, type: 
HELP (SYSCON) COMMANDS      For a summary of SYSCON commands 
HELP (SYSCON) TOPICS        For a list of SYSCON HELP topics 
HELP (SYSCON) command       For a command format, then type 
                            ? or ?? for more information 
HELP (SYSCON) command PARA  For parameters for a specific 
                            command 
HELP (SYSCON) command DESC  For description of a specific 
                            command 
HELP (SYSCON) STATUS_CHANGE For requirements for partitioning 
HELP (SYSCON) COMPONENT     For components that may be 
                            in SYSCON commands. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
COMPONENT
To display the complete command summary, type ??.  For the summary of a 
specific command, type: 
HELP (SYSCON) COMMANDS command 
Valid commands are DATE, DIRECTORY, DISPLAY, DO, END, ENTER, ERASE, EXIT, 
HELP, OUTPUT, PARTITION, PRINT, QUIT, RETURN, RELEASE, SET, TIME, THRESH. 
  Command        Description 
  {DATE|TIME} 
                 Displays the current time and date. 
  {DIRECTORY|DIR} 
                 Changes the default account and packset. 
  DISPLAY 
                 Displays the status of a component. 
  {DO|!} 
                 Enables IBEX command execution. 
  {END|EXIT|QUIT} 
                 Terminates SYSCON. 
  ENTER 
                 Invokes a CP-6 ADAPT dialog from within this processor. 
  ERASE 
                 Deletes accumulated output for logical devices. 
  HELP 
                 Displays information on SYSCON processor and other 
                 processors. 
  OUTPUT 
                 Directs processor output to a destination. 
  PARTITION 
                 Removes a specific component from system use for testing. 
  PRINT 
                 Directs that output accumulated for logical devices be sent 
                 to destinations immediately. 
  RELEASE 
                 Releases a CPU, IOM, or SCU to system use after testing. 
  RETURN 
                 Returns a specific component to system use after testing. 
  SET 
                 Sets flags determining the type of testing permitted on a 
                 component. 
  THRESH 
                 Sets I/O error thresholds for system components. 
00004
00001
00002
00003
00004
00005
00006
00007
00005
00008
00009
00010
00011
00005
00012
00013
00014
00015
00001
COMMANDS
Components that may be specified in SYSCON commands are listed below. 
For information about when a device or channel may be partitioned, type HELP 
(SYSCON) STATUS_CHANGE 
  Component      Description 
  {AP|CP|CR|DP|LP|MT|OD|SC}nn[twsn] 
                 Peripheral device name as assigned by TIGR at boot time. 
                 nn    is the 2-character device number. 
                 twsn    is the 4-character TWSN number.  The default is 
                 '0000' which means LOCAL. 
  {AP|CP|CR|DP|LP|MT|OD|SC} ON IOM#i, CHAN[NEL] c[,DEV#d] 
                 Access path for a device.  This form affects the device not 
                 the path, except in the case of the SC in which both are 
                 affected. 
                 i    is the IOM number, 0-3. 
                 c    is the channel number, 8-127. 
                 d    is the device number.  The DEV#d specification is 
                 required for DP, MT, and OD devices but is meaningless for 
                 other devices. 
  {AC|DC|TC|UC}nn [, DEVICES] [, {CHANS|NCHANS}] 
                 Microprogrammed controller name assigned by TIGR at boot 
                 time. 
                 nn    is the 2-character controller number. 
                 DEVICES    specifies that all devices connected to the MPC 
                 are to be partitioned (or returned). 
                 CHANS|NCHANS    specifies the disposition of channels.  CHANS 
                 partitions (or returns) all channels connected to the MPC. 
                 NCHANS does not partition (or return) any channels connected 
                 to the MPC.  CHANS is the default for the PARTITION and 
                 RETURN commands. 
  {AC|DC|TC|UC} ON IOM#i, CHAN[NEL]c 
                 Access path for a controller.  This form affects the 
                 controller, not the path. 
                 i    is the IOM number, 0-3. 
                 c    is the channel number, 8-127. 
  CPU#i 
                 CPU. 
                 i    is the CPU port number, 1, 3, 5, 7. 
  FEPn 
                 Front-end processor n (and may be an optical disk 
                 controller). 
                 n    is from 1 to the maximum number of FEPs on the system. 
  FEP ON IOM#i, CHAN[NEL]c 
                 Access path for a FEP (or possibly an optical disk 
                 controller). 
                 i    is the IOM number, 0-3. 
                 c    is the channel number, 8-127. 
  IOM#i, CHAN[NEL]n[-m] 
                 IOM channel. 
                 i    is the IOM number, 0-3. 
                 n[-m]    n is a channel number; n-m is a range of channel 
                 numbers where n<m.  The channel numbers must be in the range 
                 8 to 127, inclusive. 
  IOM#i 
                 IOM. 
                 i    is the IOM number, 0-3. 
  PA[GES]n[-m] 
                 Page(s) of physical memory. 
                 n[-m]    is the page number range. 
  SCU#i 
                 SCU. 
                 i    is the SCU number, 0-1. 
COMPONENT
DISPLAY
Format: 
{DATE|TIME} 
Description: 
DATE (and its synonym TIME) displays the current date and time.  The format of 
the display is: 
mmm dd 'yy hh:mm (month)(day)(year)(hours)(minutes) 
Examples: 
>DATE 
requests a display of the current date and time.  A sample display is: 
AUG 02  '88  11:03 
00001
00002
DISPLAY
Format: 
{DIR|DIRECTORY} [fid|R[ESET]] 
Parameters: 
fid    specifies the new default account fid, and may consist of an account or 
a packset name and an account. 
RESET    specifies that the default account is to be reset to the running 
account. 
Description: 
DIRECTORY (and its synonym DIR) changes the default account and packset.  The 
default account and packset are the account and associated packset that are 
selected if an account is not supplied as part of a disk file fid 
specification.  Initially, the default account is the logon or running account 
and the packset name is nil.  When used without parameters, DIRECTORY displays 
the current directory pointer. 
Usage Note: 
The DIRECTORY and DIR commands may be used only as a direct SYSCON command. 
Examples: 
>DIRECTORY .SYSLIB 
This command directs that subsequent fids that do not include an account are 
to default to the .SYSLIB account and the packset associated with that 
account. 
>DIRECTORY DP#UTIL.Y 
This command specifies that subsequent fids that do not include an account are 
to default to the Y account on the packset named UTIL. 
>DIRECTORY RESET 
This command re-establishes the running account and its associated packset as 
the default. 
00002
00004
00001
00003
Format: 
D[ISPLAY] [component[,component] ... ] 
Parameters: 
component    may be any component.  To list the available components, type: 
HELP (SYSCON) COMPONENT.  The following options are also permitted.  The 
default is to display the status of all components. 
Option         Description 
------         ----------- 
PART           Displays all partitioned devices. 
PATH (comp)    Displays the access path to the specified component. 
               comp may be a device, FEP, or MPC. 
REL            Displays all released components. 
Description: 
The DISPLAY command is used to determine the status of a particular component. 
The possible statuses are UP and PART (partitioned). 
00002
00001
Format: 
{DO|!} IBEX-command 
Parameters: 
IBEX-command    any legal IBEX command.  (See the CP-6 Programmer Reference 
Manual (CE40).) 
Description: 
The DO command allows the user to execute an IBEX command without exiting the 
current processor. 
Note:  The ! (exclamation point) may be used instead of the word DO.  It 
    should be noted however that if the ! is used in an XEQ file, it will 
    terminate the current processor session unless preceded by at least one 
    blank, or by a double ! (!!). 
Examples: 
>DO DI 
means display the current system status 
>!LDEV LP09 TITLE='report title',PAGE=100,COPIES=3 
means set up a title and page number for a report destination 
00002
00003
00001
Format: 
{E[ND]|[E]X[IT]|Q[UIT]} 
Description: 
The END command (and its synonyms EXIT and QUIT) terminates the SYSCON 
processor. 
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
>ERASE ALL 
deletes all output accumulated for all logical devices defined for the session 
or job. 
00002
00003
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
D 
  DATE Command - 
      HELP DATE 
  DIRECTORY Command - 
      HELP DIRECTORY 
  DISPLAY Command - 
      HELP DISPLAY 
  DISPLAY Command (SYSCON) - 
      HELP DISPLAY FORMAT: 
  DO Command - 
      HELP DO 
E 
  END Command - 
      HELP END 
  ENTER Command - 
      HELP ENTER 
  ERASE Command - 
      HELP ERASE 
H 
  HELP Command - 
      HELP HELP 
I 
  Invoking SYSCON - 
      HELP INVOKING_SYSCON 
M 
  Mirrored Disks - 
      HELP STATUS_CHANGE 
O 
  OUTPUT Command - 
      HELP OUTPUT 
P 
  PARTITION Command - 
      HELP PARTITION 
  PRINT Command - 
      HELP PRINT 
  Privileges for Use of SYSCON - 
      HELP PRIVILEGES 
R 
  RELEASE Command - 
      HELP RELEASE 
  RETURN Command - 
      HELP RETURN 
S 
  SET Command - 
      HELP SET 
  SET Command (SYSCON) - 
      HELP SET FORMAT: 
  SYSCON -   
    DISPLAY Command - 
      HELP DISPLAY FORMAT: 
    PARTITION Command - 
      HELP PARTITION FORMAT: 
    RELEASE Command - 
      HELP RELEASE FORMAT: 
    RETURN Command - 
      HELP RETURN FORMAT: 
    SET Command - 
      HELP SET FORMAT: 
    THRESH Command - 
      HELP THRESH FORMAT: 
T 
  THRESH Command - 
      HELP THRESH 
00001
00002
00003
00004
00005
00006
00007
00008
00009
HELP_INDEX
SYSCON may be run as a batch, console ghost, or a on-line job.  The SYSCON 
processor is invoked by the !SYSCON command. 
The DCBs used by SYSCON are: 
o   M$SI for input 
o   M$LO for output 
When run as an on-line job, SYSCON issues the greater than (>) character to 
solicit commands. 
Format: 
         [[OVER] LP[@location]] 
OUT[PUT] [[INTO] fid          ] [(option[,option]...[)]] 
         [[ON  ] ME           ] 
         [[TO  ]              ] 
Parameters: 
fid    any valid CP-6 file identifier. 
ON or TO    indicates to only honor the OUTPUT command if the file does not 
already exist. 
OVER    indicates to honor the OUTPUT command whether or not the file exists. 
INTO    indicates to merge the result of the OUTPUT command into the file if 
it exists, or to create a new one if it does not. 
LP    directs output to the default line printer; @location specifies a line 
printer. 
ME    returns the output destination to the user's terminal. 
option    is one of the following: 
    F[ORM]={formname|'formname'}    Applies to unit record files and unit 
    record devices and specifies the name of a form to be mounted on a unit 
    record device.  formname is a 1-6 character string, which can be quoted. 
    The name must have been defined to the system by the system manager (via 
    the Form Definition File).  The default is blank, which means the default 
    form for a unit record device and form 'STDLP' for unit record files. 
    I[XTNSIZE]=value    Specifies an initial disk storage allocation (in 
    blocks) for the output file.  value must be in the range of 1 through 
    134217727.  The default is 2. 
    O[RGANIZATION={C[ONSECUTIVE]|U[NIT]R[ECORD]}    Specifies the organization 
    of the output file as either CONSECUTIVE or UNIT RECORD.  If this option 
    is not specified, the output file is created as a UR file. 
    X[TNSIZE]=value    Use of this option causes an automatic M$EXTEND when 
    needed.  value specifies a secondary disk storage allocation (in blocks) 
    for the output file, and must be in the range 1 through 32000.  The 
    default is 2. 
Description: 
The OUTPUT command is used to direct all processor output to a destination. 
OUTPUT with no options redirects output to the original output destination. 
Output can be directed to any valid file name (fid).  If none of ON, TO, OVER, 
or INTO is specified, ON will be assumed. 
00002
00001
Format: 
P[ARTITION] component[, component] ... 
Parameters: 
component    is one of the options available by typing HELP (SYSCON) 
COMPONENT. 
Description: 
The PARTITION command is used to remove a specific component from system use. 
In general, this component will then be available only for testing by a test 
and diagnostic process.  A disk spindle mounted with multiple packsets must be 
requested via the REQUEST keyin (described in the CP-6 Operations Reference 
Manual (CE34)) before partitioning is possible.  For information on when a 
device may be partitioned, type:  HELP (SYSCON) STATUS_CHANGE. 
Examples: 
Example 1: 
    !SYSCON 
    SYSCON E04 Here 
    >PART DP07 
      Device DP070000 successfully partitioned 
    >PART MT05 
      Device MT050000 successfully partitioned 
    >END 
    ! 
Example 2: 
    !SYSCON 
    SYSCON E04 Here 
    >PART DP05 
      Unable to partition device DP050000. 
      Device in use.  Will be partitioned when released. 
    >DI DP05 
    Component     Part   TDOK   Checkwrite 
    DP050000      Yes    No     No 
    >END 
    ! 
In Example 2 the "Device in use" error occurs when partitioning a multipackset 
disk device because PIG has access to the disk, but upon the partition 
request, the disk is released by PIG and then partitioned immediately via the 
normal delayed partitioning mechanism. 
00002
00003
00001
Format: 
PRINT [ALL|ldevlist] 
Parameters: 
ALL    specifies that the accumulated output for all logical devices is to be 
sent to destination(s) immediately.  This is the default. 
ldevlist    specifies that the accumulated output for the specified logical 
device or devices is to be sent to destination(s) immediately.  The list is 
entered in the format 
ldevname[,ldevname]... 
ldevname is a logical device name established through the LDEV command. 
Description: 
PRINT directs that output accumulated for logical devices be sent to 
destination(s) immediately. 
Examples: 
>PRINT LP01,LP02 
The above example causes the accumulated output associated with logical 
devices LP01 and LP02 to be sent immediately to the associated destinations. 
00002
00003
00001
The privilege (PRIVILEGE) SYSCON is required to use SYSCON to alter the status 
of a component.  The SPCLMM, SYSCON or TND privilege is required to display 
the status of a component.  The SYSCON, SYSLOG or TND privilege is required to 
alter the I/O error threshold of a component.  The processor privilege 
(PPRIVILEGE) SYSCON allows the user to do all of the above. 
RETURN
Format: 
REL[EASE] component[, component] ... 
Parameters: 
component    is the CPU, IOM, or SCU option available by typing HELP (SYSCON) 
COMPONENT. 
Description: 
The RELEASE command is used to remove a CPU, IOM, SCU from system use.  This 
component will not be available for use.  For information on when a device may 
be released, type:  HELP (SYSCON) STATUS_RELEASE. 
Examples: 
Example 1: 
    !SYSCON 
    SYSCON E04 Here 
    >REL IOM#1 
      IOM IOM#1 successfully released 
    >END 
    ! 
00002
00003
00001
Format: 
R[ETURN] component[, component] ... 
Parameters: 
To list the available components, type: HELP (SYSCON) COMPONENT. 
Description: 
The RETURN command is used to make a specific component available for system 
use. 
Usage Notes: 
In order for a device to be returned to the system, there must be an access 
path to that device.  If there is not, it cannot be returned; if there is, it 
can be returned any time, assuming that it is not busy with diagnostics. 
00002
00001
00003
Format: 
S[ET] components flag[, flag] ... = {YES|NO} 
Parameters: 
component    is any legal MPC, DEVICE, CHANNEL or FEP.  Type HELP (SYSCON) 
COMPONENT for the format of these options. 
flag    is the flag to either set or reset.  The current legal flagnames are: 
    TDOK    if set, this component may be used for Test and Diagnostic 
    functions. 
    CHECKWRITE    if set, then all writes to this device are write-and-compare 
    (legal for disks only). 
Description: 
The SET command may be used to set flags in the system tables for components. 
00002
00001
Requirements for honoring a PARTITION command are: 
Device      Description 
------      ----------- 
Array       The processor must be available; that is, no user 
Processor   may have acquired it as a resource. 
Consoles    May be partitioned any time.  There must always be one 
            non-partitioned console in a system. 
Disks       The drive must be available - no packset mounted and at 
            least one DP resource available. 
Mirrored 
Disks       If you partition a Mirrored Disk device, then both that 
            device and its mirror device are partitioned, or at least 
            marked for delayed partitioning if the devices cannot be 
            paritioned immediately. 
FEPS        May be partitioned any time. 
IOM,Chan    Channels are partitionable.  However, if the last path to 
            any device will be closed by partitioning a channel then 
            the device must be partitioned before the channel can 
            be partitioned.  FEP and console channels are partitioned 
            along with the device and therefore may not be partitioned 
            separately. 
Memory      Physical memory may be partitioned any time. 
Controllers If the only path to a device is through this controller 
            then that device must be partitioned for the controller to 
            be partitioned.  If there are other paths, the controller 
            is partitionable. 
            Note:  A controller may be partitioned (but is not required 
            to be partitioned) to allow a Customer Service 
            Representative to run ITR tests.  If the PARTITION command 
            is used in this case, only the controller, not the 
            channels should be partitioned as shown in these sample 
            commands: 
                !SYSCON 
                >PART DC01, NCHANS 
                >END 
            It is necessary to partition only the controller because 
            the ITRs reload the controller firmware after the test 
            completes.  In order for this firmware load to work, the 
            channels to the controller must not be partitioned. 
Optical     The drive must be available - no cartridge mounted. 
Disk 
Tapes       The drive must be available - no tape mounted and at least 
            one MT resource available. 
Unit        If symbiont devices, they must be locked and idle; if 
Record      resources, they must be unused and unowned. 
Devices 
Note:  Any time that a user is in control of a device that is to be 
partitioned then it may be necessary to abort the user to partition the 
device.  The user of SYSCON may ask the system operator to perform an X keyin 
for users of the device, as the user abort function is not provided in SYSCON. 
    Requirements for honoring a RELEASE command are: 
    Component   Description 
    ---------   ----------- 
    CPU         The CPU must be stopped. 
    SCU         Only high memory may be released.  A SCU is released only 
                if all pages of memory in the SCU are not in use. 
    IOM         If the IOM is not partitioned, the RELEASE command attempts 
                to PARTITION the IOM before releasing it. 
Format: 
T[HRESH] component[=value][, component[=value]] ... 
Parameters: 
component    is any legal IOM, CHANNEL, MPC or DEVICE, with the exception of 
the OD device.  Type HELP (SYSCON) COMPONENT for the format of these options. 
value    is a decimal number.  This value is the error rate, connects/error. 
If the device develops an error rate that exceeds this value, a message is 
displayed on the system console.  The default threshold for all system 
components is 1000.  If value is not specified, the current threshold setting 
is displayed. 
Description: 
The THRESH command may be used to set the I/O error threshold for system 
components. 
00002
00001
