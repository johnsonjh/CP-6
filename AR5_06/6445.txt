TIGR (Table Initialization and Generation Routine) performs the functions 
necessary to: 
o   build and initialize system control tables which are hardware 
    configuration dependent 
o   build and initialize several tables and system parameters whose size and 
    contents are affected by the intended user environment at a specific site. 
TIGR is the portion of the monitor that initializes configuration-dependent 
system tables.  The CP-6 monitor comes with the initial values of 
non-configuration-dependent tables already in place, eliminating the need for 
SYSGEN or boot-time activity to initialize these tables. 
The monitor, including TIGR, is one of the first programs loaded by the 
AARDVARK bootstrap program.  TIGR is entered during the boot process, 
immediately after AARDVARK and XDELTA have completed their functions. 
To display information about TIGR, type any of the following\ 
HELP (TIGR) COMMANDS         For a list of commands by category 
HELP (TIGR) command          For the format of a specific command. 
                             Then type ? or ?? for more. 
HELP (TIGR) command PARAM    For only parameter information on a 
                             specific command 
HELP (TIGR) command DESC     For only the description of a 
                             specific command. 
HELP (TIGR) TOPICS           For a list of all TIGR HELP topics. 
HELP (TIGR) COMMAND_SUMMARY  For a brief description of commands. 
  ************************************************************** 
  *   Copyright, (c) Bull HN Information Systems Inc., 1998 
  ************************************************************** 
Format: 
ARRAY PROCESSOR,APCNAME=apcname,MODEL=apcmode,IOM#=iom,CHAN=x[,STATUS=sta]; 
 NAME=apname, CHAN=x[,options]; 
 [NAME=apname,CHAN=x[,options]]... 
Note:  The semicolon (;) is used here to denote continuation of a line of 
text. 
Parameters: 
apcname    specifies the unique name by which the software refers to this APC 
(Array Processor Controller).  The format of the name is ACxx, where xx is a 
two-digit decimal number (01-99). 
apcmodel    specifies the APC model number, currently FPS0164. 
iom    is the system-assigned number of the IOM. 
x    is the channel connected to the APC.  The channel number range is from 8 
to 63.  The channels for the APC and devices must be consecutive values and 
must be specified in ascending order. 
sta    is the initialized partition-status of the APC and specified channel. 
The permissible values are UP or DOWN. 
apname    is the unique name used by the software when referring to the 
device.  The format of the name is APxx, where xx is a two-digit decimal 
number (01-99). 
options are as follows: 
    {SJE|SFS6125}    array processor programs run entirely on the FPS-164 
    processor under the System Job Executive (SJE), rather than running 
    partially on the CP-6 host also.  (SFS6125 is the marketing identifier for 
    SJE.  Therefore, both options are associated with the same functionality.) 
    MEM=n    where n is a decimal number (256-8192) that represents the number 
    of pages of memory in the array processor. 
Description: 
The ARRAY PROCESSOR command defines the paths connecting an array processor 
subsystem to the CP-6 system and the members of the array processor subsystem. 
00002
00001
Format: 
AUTOCONFIG 
Description: 
The AUTOCONFIG command is intended for use in first-time booting of a CP-6 
system; this command is not for use at existing sites to install new releases 
of software.  AUTOCONFIG, together with FEP commands and a MON command, is 
stored on the PO tape supplied by Bull; this tape is identical for all sites 
and reflects a minimal system.  Once the initial booting is completed from 
this tape, the system manager invokes DEF to create the installation-specific 
PO tape, containing a file of TIGR commands that reflects the actual 
configuration.  This new tape is used to re-boot the system via a Yes-New 
Files boot (see Appendix A). 
Usage Notes: 
1.  As an alternative to the AUTOCONFIG command, a complete set of TIGR 
    commands can be entered through the card reader, system console, or the 
    second patch tape. 
2.  TIGR recognizes only Federal Information Processing Standard (FIPS) disks 
    and FIP tapes as DPS 90 boot devices.  Therefore, to perform an auto 
    configuration on the DPS 90, be sure that the boot uses a FIPS disk and 
    FIPS tape(s). 
00001
00002
The maximum number of FEPs that can be connected to the host is now 14. 
The twelve commands for TIGR may be grouped into three sets, as follows: 
Hardware          Software       TIGR 
Configuration     Parameters     Control 
-------------     ----------     ------- 
  IOM                MON         READ 
  CONSOLE                        VOLINIT 
  DISK                           END 
  OPTC 
  TAPE 
  UNIT 
  FEP 
  CPU 
  AUTOCONFIG 
  ARRAY PROCESSOR 
See: HELP (TIGR) COMMAND_SUMMARY for a brief description of each command. 
A summary of TIGR commands is listed in the following table:  TIGR commands, 
some of which are lengthy, may be continued on the next line by the semicolon 
continuation character(;). 
  Command        Description 
  ARRAY PROCESSOR 
                 Defines the paths connecting an array processor subsystem to 
                 the CP-6 subsystem and the members of the array processor 
                 subsystem. 
  AUTOCONFIG 
                 Specifies a minimum system configuration, used only for the 
                 initial boot of the system. 
  CONSOLE 
                 Specifies a console name and IOM (Input/Output Multiplexer) 
                 channel connection. 
  CPU 
                 Indicates to which port a CPU is connected. 
  DISK 
                 Describes disk subsystem configurations. 
  END 
                 Causes TIGR to exit to the scheduler portion of the monitor. 
  FEP 
                 Defines path connecting Front-end Processor to the system. 
  IOM 
                 Indicates to which port an I/O multiplexer is connected.  In 
                 this processor, the term IOM refers to DPS 8 IOM, DPS 90 IOP 
                 and DPS 8000 IMX. 
  MON 
                 Sets certain software operating parameters. 
  OPTC 
                 Defines path connecting an Optical Disk Controller to the 
                 system and the device(s) attached to it. 
  READ 
                 Specifies the source of a TIGR command stream. 
  TAPE 
                 Describes tape subsystem configurations. 
  UNIT 
                 Describes a unit-record subsystem. 
  VOLINIT 
                 Invokes VOLINIT processor after completion of system 
                 initialization functions. 
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
Format: 
CONSOLE NAME=SCxx, IOM#=iom, CHAN=x[, option[, option] ... ] 
Parameters: 
xx    is a two-digit number for the system console. 
iom    is the IOM system-assigned number. 
x    is the number of the channel over which the console is connected.  The 
channel number range is from 8 to 63, unless the system is a DPS 8000 in which 
case the channel number value is in the range 8 to 127. 
option    is any one of the following: 
    AD[MIN] = {Y[ES]|N[O]|D[ISPLAY]|K[EYIN]}    specifies whether or not this 
    console can display and control running users and jobs in the batch queue 
    associated with its WSN.  The default is YES. 
    CM[D] = 'text'    is the first command executed when the console connects 
    to the system ghost KEYIN at system startup (cannot exceed 80 characters). 
    CO[MMUNICATION] = {Y[ES]|N[O]|D[ISPLAY]|K[EYIN]}    specifies whether or 
    not this console can display and control FEPs and communication devices at 
    the line level.  COM=YES or KEYIN is only legal for LOCAL consoles.  The 
    default is YES. 
    DE[VICE] = {Y[ES]|N[O]|D[ISPLAY]|K[EYIN]}    specifies whether or not this 
    console can display and control devices associated with the terminal or 
    station tname.  The default is YES. 
    MA[XPRIO] = value    specifies the maximum priority to which a job in the 
    batch queue can be raised.  The maximum value is 15.  Default is 15. 
    NA[TIVEL]= {letter|NONE}    specifies the language (within the operator 
    message file) which will be used for console messages.  letter is the 
    1-character name used to identify the language.  NONE indicates the 
    standard CP-6 console message file (in English).  The default is NONE. 
    Note:  English is the only language supplied with the CP-6 system. 
    SY[STEM] = {Y[ES]|N[O]|D[ISPLAY]|K[EYIN]}    specifies whether or not this 
    console shall have full system control powers.  SYSTEM=YES or KEYIN is 
    only legal on LOCAL consoles.  SYSTEM consoles incorporate all the other 
    attributes.  The default is YES. 
    WSN=wsnname    specifies the workstation that this device controls.  One 
    to eight characters may be entered for wsnname.  It may be wildcarded on 
    the right only.  At least one console must be defined with the default 
    (i.e., the WSN=wsnname option not specified). 
Description: 
The CONSOLE command is used to specify the system console's name and IOM 
channel connection.  The command is not optional.  At least one CONSOLE 
command per TIGR deck is required. 
Usage Note: 
For the SYSTEM, COMMUNICATION, DEVICE, and ADMIN options: 
o   DISPLAY allows display of information 
o   KEYIN allows changes 
o   YES means both DISPLAY and KEYIN 
o   NO means neither DISPLAY nor KEYIN 
00002
00001
00003
Format: 
CPU PORT# = i[, MASTER] 
Parameters: 
i    is the memory port (0<i<7). 
MASTER    has no effect and is accepted for compatibility with previous 
releases.  For all systems except DPS 8000 systems, the primary CPU is 
selected by switch settings on the System Control Unit (SCU) at boot and by 
the MAKE CPU keyin on a running system.  For DPS 8000 systems, the CPU 
configuration is contained in the Service Processor (SP) configuration file. 
Description: 
The CPU command indicates to which port a CPU is connected.  If there is more 
than one system controller, the port number is the port on the base system 
controller (low-order memory).  The CPU command is used only in a 
multi-processing configuration.  For DPS 90 and DPS 8000 systems, up to four 
CPU commands may be used.  For all other systems, up to six CPU commands may 
be used. 
00002
00001
    !TIGR 
        . 
        . 
        . 
    IOM PORT#=0 
    IOM PORT#=1 
        . 
        . 
        . 
    DISK  ; 
        MPC,MPCNAME=DC01,MODEL=MSP0450   ; 
             LA  ; 
                  IOM#=0,CHAN=8-11 ; 
             LA  ; 
                  IOM#=1,CHAN=8-11 ; 
        MPC,MPCNAME=DC02,MODEL=MSP0450  ; 
             LA  ; 
                  IOM#=0,CHAN=12-15  ; 
             LA  ; 
                  IOM#=1,CHAN=12-15  ; 
        DEV  ; 
             NAME=DP01,MODEL=(MSU0451,MSF0007),DEV#=1  ; 
             NAME=DP02,MODEL=(MSU0451,MSF0007),DEV#=2  ; 
             NAME=DP03,MODEL=(MSU0451,MSF0007),DEV#=3  ; 
             NAME=DP04,MODEL=(MSU0451,MSF0007),DEV#=4  ; 
             NAME=DP05,MODEL=(MSU0451,MSF0007),DEV#=5  ; 
             NAME=DP06,MODEL=(MSU0451,MSF0007),DEV#=6  ; 
             NAME=DP07,MODEL=(MSU0451,MSF0007),DEV#=7  ; 
             NAME=DP08,MODEL=(MSU0451,MSF0007),DEV#=8  ; 
             NAME=DP09,MODEL=(MSU0451,MSF0007),DEV#=9  ; 
             NAME=DP10,MODEL=(MSU0451,MSF0007),DEV#=10  ; 
             NAME=DP11,MODEL=(MSU0451,MSF0007),DEV#=11 
Format: 
DISK ; 
MPC,MPCNAME=mpcname[,MODEL=mpcmodel][,STATUS=sta]; 
 LA IOM#=iom,CHAN=x[-y][,STATUS=sta][[,IOM#=iom,CHAN=x[-y][,STATUS=sta]]; 
 [LA IOM#=iom,CHAN=x[-y][,STATUS=sta][[,IOM#=iom,CHAN=x[-y]][,STATUS=sta]]; 
 [MPC,MPCNAME=mpcname[[,MODEL=mpcmodel][,STATUS=sta]; 
 LA IOM#=iom,CHAN=x[-y][,STATUS=sta][[,IOM#=iom,CHAN=x[-y][,STATUS=sta]]; 
 [LA IOM#=iom,CHAN=x[-y][,STATUS=sta][[,IOM#=iom,CHAN=x[-y][,STATUS=sta]]]; 
 DEV; 
 NAME=name,MODEL=(model#[,feature#]),DEV#=devno[,options]; 
 [NAME=name,MODEL=(model#[,feature#]),DEV#=devno[,options]...] 
Note:  The semicolon (;) is used here to denote continuation of a line of 
text. 
Parameters: 
To see all of the parameters, enter ??.  For information about a specific 
parameter, enter: 
HELP (TIGR) DISK parameter 
where parameter is: 
MPCNAME, MPCMODEL, STA, IOM, X, NAME, MODEL, FEATURE, DEVNO. 
mpcname    specifies the unique name by which the software refers to this MPC 
(Microprogrammed Controller).  The format of the name is DCxx for a disk 
controller, where xx is a two-digit decimal number (00-99). 
mpcmodel    specifies the MPC model number which will be used to select 
firmware to be loaded into the MPC.  The MPC model numbers are listed below. 
The defaults are MSP0600 for DISK. 
                                              Firmware 
    MPC Model No.               Sub-system    Modules     System(s) 
    -------------               ----------    --------    --------- 
    MSP0450                        DISK         M191      All 
    MSP0600/MSP0611/MSP0612        DISK         D500      All 
    MSP8000/MSP8001                DISK         D500      All 
    MSP8021/MSP8022/MSP8023        DISK         MSP8      All 
    MSP3881/MSP3885                DISK         D388      DPS 90 (only) 
    MSP3882/MSP3886                DISK         IFDK      DPS 8000 (only) 
    MSP3991/MSP3992                DISK         IFDK      DPS 8000 (only) 
    MSP3993/MSP3994                DISK         D388      DPS 90 (only) 
    MSS8080                        DISK         IIDK      DPS 8000 (only) 
    MSS8090                        DISK         IIDK      DPS 8000 (only) 
sta    is the initialized partition-status of the MPC or specified channels. 
The permissible values are UP or DOWN.  For channel partitioning, channels 
specified immediately preceding the STATUS option are marked down.  UP is the 
default. 
iom    is the system-assigned number of the IOM.  Note:  The first Link 
Adaptor specified (LA IOM#=iom) must specify the firmware bootload channel for 
this MPC. 
x[-y]    is the channel or range of channels connected to the LA.  The channel 
number range is from 8 to 63, unless the system is a DPS 8000 in which case 
the channel number value is in the range 8 to 127.  There are hardware 
restrictions on which channels may be connected to the same MPC from different 
IOMs.  The table below summarizes these restrictions: 
    If the number of channels       then the first channel 
    specified in the IOM#iom,       address must be an integral 
    CHAN=x-y field is:              multiple of: 
           3-8                             4 
            2                              2 
            1                              1 (no restriction) 
See Usage Notes #1 and #4. 
name    is the unique name used by the software when referring to the device. 
The format of the name is DPxx for a disk drive, where xx is a two-digit 
decimal number (00-99).  See Usage Note #2 for a description of name entry 
requirements. 
model#    is the applicable model number.  See Usage Note #2 for a description 
of model entry requirements. 
The following is a list of supported disk models and their attributes: 
                                           Sectors Tracks    Cylinders Sec- 
                                           Per     Per       Per       tor 
Disk Model#  Feature# Description Granules Track   Cylinders Device    Size 
-----------  -------- ----------- -------- ------- --------- --------- ---- 
MSU0451      MSF0007  200 mb disk   38665    40       19         814    64 
MSU0501/0509 MSF0015  600 mb,      134400     8       40         840    512 
                      native mode 
                      operation 
MSU3380/3382          500 mb disk  112837    17       15         885    512 
MSU3381/3383          1000 mb disk 225675    17       15        1770    512 
MSU3390/3392          500 mb disk  112837    17       15         885    512 
MSU3391/3393          1500 mb disk 338512    17       15        2655    512 
MSU8082      MSS8080  400 mb disk   92796    11       24         703    512 
             MSF8080 
MSU8092      MSS8090  1100 mb disk 231847    19       15        1627    512 
             MSF8090 
feature#    is the applicable feature board number. 
devno    is the hardware device number.  See Usage Note #3 for DEV# 
restrictions.  Options used with devno are: 
    STATUS=sta    where status is UP or DOWN. 
    CHECKWRITE    indicates checkwriting is to be performed on DP devices. 
    Note:  CHECKWRITE does a write, read and compare for verification of what 
    has been written.  This results in an extra revolution of the disk. 
    CHECKWRITE should be unnecessary for normal functioning hardware. 
Description: 
The DISK command describes DISK subsystem configurations.  The command 
describes the configuration of the IOMs, the LAs (Link Adaptors), the MPC 
(Microprogrammed Controller), and the devices (disk drives).  There may be two 
MPCs for a disk subsystem. 
Usage Notes: 
1.  Up to 8 channels can be defined per LA.  Two LAs can be defined for an 
    MPC.  Therefore, a possible maximum of 16 channels can be defined per MPC. 
2.  The number of NAME and MODEL entries required per physical disk depends on 
    the number of logical drives per physical disk unit, as follows: 
    Model            Number of Devices 
    -----            ----------------- 
    MSU0501                  2 
    MSU3380...83             4 
    MSU3390...93             4 
3.  When MSU451 and MSU0501 disk drives are placed on the same MPC disk 
    controller, two channel adaptors are required, and: 
    o   All MSU451s on the controller must be connected to one of the channel 
        adaptors. 
    o   All MSU0501s on the same controller must be connected to the other 
        adaptor. 
    o   The DEV# of all devices connected to one controller must be unique. 
4.  If all channels to a controller have STATUS=DOWN, TIGR sets the controller 
    to STATUS=DOWN.  (If all channels to a controller are down, all paths to 
    the controller are down, and therefore, the controller must be down.  This 
    follows standard CP-6 partitioning rules).  This is accepted by TIGR if 
    there is another path to the devices that is not down or if all of the 
    devices on the controller are down.  Otherwise, TIGR aborts with error 
    messages mentioning the controller and channel number it could not 
    partition because of ALTRETs from M$SYSCON. 
5.  For MSU8082 and MSU8092 disks, in each cabinet the drives are numbered 
    from 0 to 7.  Therefore, the device numbers on the maximum configuration 
    go from 0 to 63.  The first 3 bits of the device number represent the CM 
    number.  The second 3 bits of the device number represent the drive number 
    for that CM.  The CP-6 system can merely use the device numbers from 0 to 
    63; the IPC-IPI firmware translates the device numbers in the IDCWs to the 
    appropriate CM number and drive number. 
    However, the TIGR commands must be set up with the proper device number. 
    For each CM, the device numbers are: 
        CM      Device 
        No      Numbers 
        --      ------- 
         0       0 -  7 
         1       8 - 15 
         2      16 - 23 
         3      24 - 31 
         4      32 - 39 
         5      40 - 47 
         6      48 - 55 
         7      56 - 63 
6.  For each MSU8082 or MSU8092, two devices are present in the cabinet and 
    must be defined as two separate devices. 
Related Commands: 
See TAPE command. 
00011
00010
00009
00005
00008
00003
00002
00007
00001
00013
00004
00012
00006
    !TIGR 
    " TIGR DECK FOR LADC DPS 8000 
    CPU PORT#=1 
    IOM PORT#=0 
    CONSOLE NAME=SC01,IOM#=0,CHAN=30 
    DISK ; 
        MPC,MPCNAME=DC01,MODEL=MSP0600 ; 
             LA ; 
                  IOM#=0,CHAN=64-67 ; 
        DEV ; 
             NAME=DP01,MODEL=(MSU0451,MSF0007),DEV#=1 ; 
             NAME=DP02,MODEL=(MSU0451,MSF0007),DEV#=2 ; 
             NAME=DP03,MODEL=(MSU0451,MSF0007),DEV#=3 ; 
             NAME=DP04,MODEL=(MSU0451,MSF0007),DEV#=4 ; 
             NAME=DP11,MODEL=(MSU0501,MSF0015),DEV#=11 ; 
             NAME=DP12,MODEL=(MSU0501,MSF0015),DEV#=12 
    DISK ; 
        MPC,MPCNAME=DC02,MODEL=MSP3882 ; 
             LA ; 
                  IOM#=0,CHAN=120-127 ; 
        DEV ; 
             NAME=DP80,MODEL=(MSU3381),DEV#=0 ; 
             NAME=DP81,MODEL=(MSU3381),DEV#=1 ; 
             NAME=DP82,MODEL=(MSU3381),DEV#=2 ; 
             NAME=DP83,MODEL=(MSU3381),DEV#=3 
    DISK ; 
        MPC,MPCNAME=DC05,MODEL=MSS8080 ; 
             LA ; 
                  IOM#=0,CHAN=080-087 ; 
             LA ; 
                  IOM#=1,CHAN=080-087 ; 
        MPC,MPCNAME=DC06,MODEL=MSS8080 ; 
             LA ; 
                  IOM#=0,CHAN=088-095 ; 
             LA ; 
                  IOM#=1,CHAN=088-095 ; 
        DEV ; 
             NAME=DP48,MODEL=(MSU8092,MSF8090),DEV#=08 ; 
             NAME=DP49,MODEL=(MSU8092,MSF8090),DEV#=09 ; 
             NAME=DP50,MODEL=(MSU8092),DEV#=10 ; 
             NAME=DP51,MODEL=(MSU8092),DEV#=11 ; 
             NAME=DP52,MODEL=(MSU8092),DEV#=12 ; 
             NAME=DP53,MODEL=(MSU8092),DEV#=13 ; 
             NAME=DP54,MODEL=(MSU8092),DEV#=14 ; 
             NAME=DP55,MODEL=(MSU8092),DEV#=15 
    TAPE ; 
        MPC,MPCNAME=TC01,MODEL=MTP0610 ; 
             LA ; 
                  IOM#=0,CHAN=8-9 ; 
             DEV ; 
                  NAME=MT01,MODEL=(MTU0630,MTF0637),DEV#=1 
    TAPE ; 
        MPC,MPCNAME=TC02,MODEL=MTP8225 ; 
             LA ; 
                  IOM#=0,CHAN=24-27; 
             DEV ; 
                  NAME=MT10,MODEL=(MTU8200,MTF8208),DEV#=0 ; 
                  NAME=MT11,MODEL=(MTU8200,MTF8205),DEV#=1 ; 
                  NAME=MT12,MODEL=(MTU8200,MTF8208),DEV#=2 
    UNIT,MPCNAME=UC01,MODEL=URP8601 ; 
        NAME=LP01,MODEL=(PRU1201,PRB0600),IOM#=0,CHAN=40,OUT,SYMBIONT 
    UNIT,MPCNAME=UC02,MODEL=URP8600 ; 
        NAME=CR01,MODEL=CRU0501,IOM#=0,CHAN=38,IN,SYMBIONT 
    FEP NAME=FEP7,IOM#=0,CHAN=48,STATUS=DOWN,OUTQSZ=4,INQSZ=2 
    FEP NAME=FEP13,IOM#=0,CHAN=46,OUTQSZ=4,INQSZ=2 
    MON ; 
       . 
       . 
       . 
    !FIN 
Format: 
END 
Description: 
The END command causes TIGR to exit to the scheduler portion of the monitor, 
which will start GHOST1.  The END command is assumed when TIGR gets an EOD 
indication on the patch stream.  Accordingly, the END command is not 
ordinarily included in the TIGR command stream. 
00001
Format: 
FEP NAME=FEPn, IOM#=iom, CHAN=x [,option [,option] ...] 
Parameters: 
n    is the FEP number, from 1 to 99. 
iom    is the number of the IOM to which the FEP is connected. 
x    is the channel over which the FEP is connected.  The channel number range 
is from 8 to 63, unless the system is a DPS 8000 in which case the channel 
number value is in the range 8 to 127. 
option    may be any of the following: 
    STATUS=sta    where status is UP or DOWN. 
    INQSZ=p    is the size, in pages, of the input circular queue for this 
    FEP.  The permitted range is 1-64.  The default is 2. 
    OUTQSZ=q    is the size, in pages, of the output circular queue for this 
    FEP.  The permitted range is 1-64.  The default is 4. 
    BOOTTO=bto    is the number of 5-second intervals desired for the Boot 
    timeout.  The default is 30 (150 sec). 
    DUMPTO=dto    is the number of 5-second intervals desired for the Dump 
    timeout.  The default is 2 (10 sec). 
Description: 
The FEP command defines the path connecting a Front End Processor to the 
system. 
Usage Note: 
1.  Suggested INQSZ and OUTQSZ values for TP are p=8, q=32. 
2.  The combined size of the FEP boot image plus the circular queue (INQSZ + 
    OUTQSZ) must not exceed 256 pages.  Specifying a circular queue of more 
    than 100 pages may prevent FEPs from booting. 
3.  The maximum number of local FEPs that can be connected to the HOST is 
    currently limited to 14. 
00002
00001
00003
A 
  ARRAY PROCESSOR Command - 
      HELP ARRAY_PROCESSOR 
  AUTOCONFIG Command - 
      HELP AUTOCONFIG 
  autoshared processor slot - 
      HELP MON_OPTIONS SPAUTOSPACE 
C 
  card punch model/feature numbers - 
      HELP UNIT MODEL 
  card reader model/feature numbers - 
      HELP UNIT MODEL 
  CFU - 
      HELP MON_OPTIONS CFU 
  Checkwrite - 
      HELP DISK DEVNO 
  comgroup - 
      HELP MON_OPTIONS CGMAP 
  CONSOLE Command - 
      HELP CONSOLE 
  CPU Command - 
      HELP CPU 
  Crossbarring and Dual Access - 
      HELP CROSSBARRING_AND_DUAL_ACCESS 
  Current File Users table - 
      HELP MON_OPTIONS CFU 
D 
  DISK Command - 
      HELP DISK 
  disk model/feature numbers - 
      HELP DISK MODEL 
E 
  END Command - 
      HELP END 
  ENQ/DEQ table - 
      HELP MON_OPTIONS ENQ 
F 
  FEP Command - 
      HELP FEP 
I 
  IO cache - 
      HELP MON_OPTIONS IOCACHE 
  IOM (Input/Output Multiplexer) - 
      HELP IOM DESCRIPTION: 
  IOM Command - 
      HELP IOM 
M 
  microprogrammed controller - 
      HELP DISK MPCNAME 
      HELP TAPE MPCNAME 
      HELP UNIT MPCMODEL 
  MON Command -   
    TIGR - 
      HELP MON FORMAT: 
  MON Command - 
      HELP MON 
  MPC -   
    MPC (Microprogrammed Controller) models - 
      HELP DISK MPCMODEL 
      HELP TAPE MPCMODEL 
      HELP UNIT MPCMODEL 
  MPC channel connections - 
      HELP DISK USAGE_NOTES: 
  MPC models - 
      HELP DISK RELATED_COMMANDS: 
      HELP TAPE MPCMODEL 
      HELP UNIT MPCMODEL 
N 
  Nodes, network - 
      HELP MON_OPTIONS NODES 
O 
  OPTC Command - 
      HELP OPTC 
  overlays - 
      HELP MON_OPTIONS SPROC 
P 
  patch space - 
      HELP MON_OPTIONS PATCH 
  printer model/feature numbers - 
      HELP UNIT MODEL 
R 
  READ Command -   
    TIGR - 
      HELP READ FORMAT: 
  READ Command - 
      HELP READ 
S 
  Sample DPS 8000 TIGR Deck - 
      HELP DPS_8000_TIGR_DECK_SAMPLE 
  shared processor - 
      HELP MON_OPTIONS SPROC 
  shared processor slot - 
      HELP MON_OPTIONS SPSPACE 
  symbiont - 
      HELP UNIT OPTIONS 
T 
  TAPE Command - 
      HELP TAPE 
  TIGR -   
    AUTOCONFIG Command - 
      HELP AUTOCONFIG FORMAT: 
    CONSOLE Command - 
      HELP CONSOLE FORMAT: 
    CPU Command - 
      HELP CPU FORMAT: 
    DISK Command - 
      HELP DISK FORMAT: 
    disk models - 
      HELP DISK MODEL 
    END Command - 
      HELP END FORMAT: 
    FEP Command - 
      HELP FEP FORMAT: 
    IOM Command - 
      HELP IOM FORMAT: 
    MON Command - 
      HELP MON FORMAT: 
    MPC Command - 
      HELP DISK MPCMODEL 
    MPC models - 
      HELP DISK MPCMODEL 
      HELP DISK RELATED_COMMANDS: 
      HELP TAPE MPCMODEL 
      HELP UNIT MPCMODEL 
    READ Command - 
      HELP READ FORMAT: 
    TAPE Command - 
      HELP TAPE FORMAT: 
    tape models - 
      HELP TAPE MODEL 
    UNIT Command - 
      HELP UNIT FORMAT: 
    unit record models - 
      HELP UNIT MODEL 
    VOLINIT Command - 
      HELP VOLINIT FORMAT: 
  TIGR Command Summary - 
      HELP COMMANDS 
  TIGR Implementation - 
      HELP TIGR_IMPLEMENTATION 
U 
  UNIT Command - 
      HELP UNIT 
  user slots - 
      HELP MON_OPTIONS USERS 
V 
  VOLINIT Command - 
      HELP VOLINIT 
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
HELP_INDEX
Format: 
IOM PORT# = i [,STATUS=sta] 
Parameters: 
i    is the memory port (O<i<7). 
sta    is the initialized status of the IOM (UP or DOWN). 
Description: 
The IOM command indicates to which port a system Input/Output Multiplexer is 
connected.  Note that in this processor, the term IOM is used generically to 
mean DPS 8 IOM, DPS 90 IOP and DPS 8000 IMX.  If there is more than one system 
controller, the port number is the port on the base system controller 
(low-order memory). 
Usage Notes: 
1.  For DPS 8 systems, up to two IOM commands are permitted in the command 
    stream.  As the commands are received, the IOM(s) are numbered from 0 to 
    1, beginning with zero.  This system-assigned number is the IOM number 
    used in other TIGR commands where IOM# is indicated. 
    For DPS 90 or DPS 8000 systems, up to four IOM commands are permitted in 
    the command stream.  As the commands are received, the IOM(s) are numbered 
    from 0 to 3, beginning with 0.  This system-assigned number is the IOM 
    number used in other TIGR commands where IOM# is indicated.  TIGR 
    automatically creates a device called MCnn where nn is this 
    system-assigned number.  The MC devices are used to communicate with the 
    system maintenance subsystem (MCA for the DPS 8000 or MSOS for the DPS 
    90). 
2.  All IOM commands must appear before any DISK, TAPE, UNIT, CONSOLE, or FEP 
    commands in the command stream.  The default, if no IOM command is 
    received, is one IOM on port zero.  As if: 
    IOM PORT# = 0 
    had been given. 
00002
00001
00003
Format: 
MON [option[, option] ... ] 
Parameters: 
options are listed in HELP (TIGR) MON_OPTIONS. 
00001
To see all of the options, enter ??.  For information about a specific option, 
enter: 
HELP (TIGR) MON_OPTIONS option 
where option is: 
CFU, CGCXTSZ, CGMAP, DEVMAX, DOLIST, DUMPSIZE, ENQ, FEPRESOURCES, IOCACHE, 
MTDFLT, NODES, OSIROUTE, PATCH, QUEUE, RES, SALUTATION, SITE, 
SITEID, SPAUTOSPACE, SPROC, SPSPACE, SSN_CLIENTS, SSN_MAX, 
SSN_SERVERS, STEALPGS, TCTX, USERS. 
CFU=(min,max)    indicates the range of numbers of pages assigned for the 
current file users (CFU) table blocks used by file management.  Default is 
1,1. 
    min    is the minimum number of pages of CFU table blocks in the system. 
    max    is the maximum number of pages (up to 50) of CFU table blocks that 
    are allowed to exist in the system. 
CGCXTSZ = X    is the number of comgroup page table entries to be reserved for 
mapping comgroup context and address blocks.  Each active comgroup requires, 
as well as its own data pages, a context block and an address block.  These 
last two items occupy about 200 words per comgroup.  X is thus the maximum 
number of pages that the CP-6 system will be able to acquire for comgroup 
context.  This means that the system will be capable of having a maximum of (X 
* 5) comgroups active at any time (1024 / 200 = 5).  Minimum is 4.  Maximum is 
254.  Default is 10. 
CGMAP = pages    indicates the number of pages to be reserved for the comgroup 
page tables.  The comgroup page table is used to map the data pages allocated 
for use by comgroups.  Thus the maximum number of pages the system will be 
able to allocate to all comgroups is (pages * 1024).  Note that this parameter 
only causes (pages) number of pages to be reserved - comgroups will 
dynamically acquire data pages as they require them, and will map those pages 
via this page table.  Minimum is 1.  Maximum is 10.  Default is 1.  The 
default value is sufficient for the majority of applications. 
DEVMAX=devs    is the maximum number of devices that may be connected to the 
system at one time.  This parameter determines the number of LDCTs on the 
system.  This value can be approximated by multiplying 1-1/2 by the total of 
the following: 
    1 for each IOM-connected device (includes FEP and symbiont 
      devices) 
    1 for each asynchronous line 
    5 for each synchronous line 
    6 for each FEP 
    1 for each FPRG 
    1 for each FEPRES 
    1 for each circuit connected to a CL-type FEPRES 
    1 for each symbiont device 
    40 for the CP-6 supplied ghosts 
    1 for each expected comgroup connection that users initiate 
    1 for each OSI connection that users initiate 
Default is the number of local devices defined by TIGR. 
DOLIST=dolist    is the number of dolist blocks to be built.  These blocks are 
used in processing no wait I/O and other asynchronous operations.  Default is 
the number of users, as defined below. 
DUMPSIZE=xx    is the decimal size, in number of granules, of the area to be 
reserved on the system disk for taking dumps.  The recommended value is 3000, 
which is the default.  This parameter is only meaningful for tape boots where 
New Files = Yes (see Appendix A). 
ENQ=(min, max)    indicates the range of numbers of pages assigned for ENQ/DEQ 
table blocks.  Default is 1,1. 
    min    is the minimum number of pages of ENQ/DEQ table blocks in the 
    system. 
    max    is the maximum number of pages of ENQ/DEQ table blocks that are 
    allowed to exist in the system. 
Usually, the defaults will suffice.  Use the STATS processor DISPLAY RESOURCES 
and SNAP commands to display system utilization.  The "max since system" boot 
and "Total available" columns in the STATS display will be of particular 
interest. 
FEPR[ESOURCES]=n    is the maximum number of resource devices (created via a 
SUPER CREATE DEVICES command issued with USE=RESOURCE) that can be connected 
to the system at one time.  The default is 10. 
IOCACHE=n    specifies the size of (number of entries in) the I/O CACHE table. 
The maximum value allowed is (total memory pages - 2048 pages)/4.  Usually, 
the defaults will suffice.  Use the STATS processor DISPLAY RESOURCES and SNAP 
commands to display system utilization.  The max since system boot and Total 
available columns in the STATS display will be of particular interest.  The 
default is the lesser of the number of users (see USERS options below) x 4 or 
(total memory pages - 2048 pages)/4. 
MTDFLT = (density[, density])    where density is 800, 1600, or 6250 and 
specifies the default tape density for device MT.  The default for MTDFLT is 
the density of the first drive declared in the TIGR deck. 
The following table illustrates varying results depending upon the system 
configuration and the setting of MTDFLT: 
   Configuration         MTDFLT Setting     Result 
   ------------------------------------------------------------------- 
   System uses only      MTDFLT need not    Default drive for system 
   one type of drive;    be set.            is density of first drive 
   for example,                             in the TIGR deck; in 
   800,1600.                                this case, 800/1600. 
                                            Default drive may be used 
                                            at 800 or 1600 BPI. 
   ------------------------------------------------------------------- 
   System uses several   MTDFLT is set      Default drive for system 
   types of drives,      to 1600 BPI.       may be #1, #2, or #3 
   for example:                             since 1600 BPI is common 
     #1  800/1600                           to all three.  The drive 
     #2 1600/6250                           acquired through default 
     #3  800/1600                           may be used only at 1600. 
   ------------------------------------------------------------------- 
   System uses several   MTDFLT is set      Only drives #1 and #3 may 
   types of drives,      to 800,1600.       be allocated to a user 
   for example:                             requesting the default. 
     #1  800/1600                           The drive acquired through 
     #2 1600/6250                           default can be used at 
     #3  800/1600                           either 800 or 1600 BPI. 
   ------------------------------------------------------------------- 
  Note that for a default assignment only, the setting of MTDFLT 
  determines the density at which the drive may be used; i.e., if 
  MTDFLT=1600, the drive acquired through default can only be used at 
  1600 BPI even though it is physically capable of 800 or 6250 BPI. 
NODES=nn    is the maximum number of CP-6 network nodes that can be defined, 
from 1 to 99.  This value must be as large as the largest node identification 
number in the network.  The total number of nodes includes host nodes, local 
FEP nodes, and remote FEP nodes.  The names or identifying numbers of 
individual nodes are defined by the NETCON processor.  The default is 16. 
OSIROUTE=nn    is the number of entries in the OSI Routing tables that are to 
be built on this host.  One is needed for each OSI network address known to 
this host.  Valid values are 0 to 50.  The default is 10. 
PATCH=pp    is the number of memory words assigned for procedure patch space 
after boot time patching is completed; that is, the minimum amount of patch 
space available when the system is fully up and running.  Default is 0. 
QUEUE=(ios,ioq) 
    ios    is the number of IOS packets to be built, and represents the 
    maximum number of current and pending local I/O operations.  Because the 
    memory area in which IOS packets are built is reserved for this purpose, 
    as many packets as will fit in the area are built regardless of the ios 
    specification.  However, an error is reported if the number of packets 
    built is less than ios.  The maximum for ios is 384.  Default is ios = 10 
    times (number of packs) + (number of other devices). 
    ioq    is the number of IOQ packets to be built, and represents the 
    maximum number of current and pending local and remote operations.  The 
    maximum for ioq varies such that the total space for all of the data 
    generated by TIGR ($LS83) is less than 128 KW.  Default is ioq = DEVMAX. 
Usually, the defaults will suffice.  Use the STATS processor DISPLAY RESOURCES 
and SNAP commands to display system utilization.  The max since system boot 
and Total available columns in the STATS display will be of particular 
interest. 
RES=(resnm=x[, resnm=x] ...)    establishes names of pseudo-resources and 
specifies the amount of the pseudo-resource available or permitted on the 
system.  Up to 8 pseudo-resources may be defined.  There is no default. 
    resnm    is the name of a pseudo-resource; it may be from one to eight 
    characters. 
    x    is the maximum amount or total limits of the resource that may be 
    used at any one time. 
    If batch jobs currently waiting in the :SYMI account require pseudo 
    resources, caution should be taken when changing the TIGR list of pseudo 
    resources.  New pseudo resources should be added at the end of the TIGR 
    list and currently defined ones should not be deleted until the batch jobs 
    needing pseudo resources have been executed. 
SALUTATION='salutation'    is the greeting that will welcome on-line users 
when they log onto the system.  The salutation may contain up to 43 
characters.  Default is '***CP-6 AT YOUR SERVICE!' 
SITE='site'    is the site identification, enclosed in single quotes.  The 
site may be from 1 to 120 characters.  There is no default. 
SITEID = 'siteid'    is the site identification assigned by Bull.  The site id 
may also be specified when the PO tape is DEFed.  In general, this should not 
be specified since it will already be correct on the PO tape. 
SPAUTOSPACE = slots    designates the number of automatically shared processor 
slots that are to be reserved for autosharing of processors.  Default is the 
number of user slots divided by 4.  The sum of SPAUTOSPACE and SPSPACE must be 
less than 4096. 
SPROC=(procname[, overlays][, flag])    sets the status of shared processors. 
There is no default.  The minimum SPROC names required are :SHARED_SYSTEM, 
:SHARED_SPECIAL, IBEX, DELTA, and LOGON. 
    procname    is the name of the processor. 
    overlays    is the number of overlays that the processor uses.  Shared 
    processors are allowed to have only one level of overlay structure. 
    flag    indicates the type and privilege of the processor.  The possible 
    flags are CP for Command Processor, AS for Alternate Shared Library, LI 
    for Library, DB for Debugger, or SP for a Shared Processor other than CP, 
    AS, LI, or DB. 
SPSPACE=slots    designates the number of shared processor slots to be 
reserved for dynamic addition of shared processors.  Default is 0.  The sum of 
SPSPACE and SPAUTOSPACE must be less than 4096. 
SSN_CLIENTS=nn    is the maximum number of OSI clients that may be active on 
this host at any one time.  Valid values are 0 to 50.  The default is 32. 
SSN_MAX=nn    is the maximum number of simultaneous OSI connections allowed. 
Valid values are 0 to 50.  The default is 32. 
SSN_SERVERS=nn    is the maximum number of OSI servers that may be active on 
this host at any one time.  Valid values are 0 to 50.  The default is 9. 
STEALPGS=(x,y)    specifies limits on pages available for stealing from the 
monitor; that is, removed from the monitor's list of available free pages and 
used by other system functions.  Default is 15,30. 
    x    is the minimum number of pages available for stealing. 
    y    is the maximum number of pages which may be stolen. 
TCTX=nn    is the number of transport context blocks to be built on this host. 
One is needed for each remote FEP and for each OSI connection.  The default is 
the number specified by SSN_MAX + the number specified by NODES -2. 
USERS=users    is the number of user table slots to be built.  This represents 
the maximum number of users on the system at one time.  Fifteen of these slots 
are reserved for the system ghosts.  Therefore, the value for USERS should be 
the maximum number of on-line users + batch users + TP users + installation 
ghost users + 15. 
Description: 
The MON command sets certain operating parameters of the CP-6 system. 
Usage Notes: 
1.  The QUEUE, DOLIST, ENQ, and IOCACHE options are used to tune system 
    performance in conjunction with information obtained via the STATS 
    RESOURCES display. 
2.  The message **** SYSTEM HAS RUN OUT OF IOQ PACKETS **** will appear on the 
    IOM-connected console when there are not sufficient IOQ (Input/Output 
    Queue) packets (data blocks) for the system to be able to allocate one IOQ 
    packet per I/O request. 
00001
00002
00003
00028
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
00029
00027
CHANGES
Format: 
OPTC NAME=FEPn, IOM#=icm, CHAN=x[, STATUS=sta]; 
 DEV NAME=odname, DEV#=devno[, STATUS=sta]; 
 [NAME=odname, DEV#=devno[, STATUS=sta]...] 
Parameters: 
n    is a FEP number, from 1 to 99 and must not conflict with numbers assigned 
to communications FEPs. 
devno    is the hardware device number corresponding to the OD read/write 
device attached to the optical disk controller. 
iom    is the number of the IOM to which the Optical Disk Controller is 
connected. 
x    is the channel to which the Optical Disk Controller is connected.  It may 
be any channel to which a Direct Channel Adaptor may be connected.  The number 
of Optical Disk Controllers that may be connected is limited only by the 
number of channels available for connection with Direct Channel Adaptors. 
sta    is the initialized partition status (either UP or DOWN) of the Optical 
Disk Controller, or a device attached to it.  The default is UP. 
odname    is the unique name by which the software refers to a read/write 
device attached to the Optical Disk Controller.  The format of the name is 
ODxx, where xx is a two-digit decimal number (01-99). 
Description: 
The OPTC command defines the path connecting an Optical Disk Controller to the 
system and defines the device(s) attached to it. 
This command causes TIGR to build a set of FEP communications tables, 
including input and output circular queues, I/O and Resource Management system 
tables. 
00002
00001
Format: 
R[EAD] {ME|PA} 
Parameters: 
ME    directs TIGR to read and respond to a command stream keyed in on the 
operator's console. 
PA    directs TIGR to read and respond to a command stream in the 
AARDVARK-managed patch stream. 
If no READ command is given, the patch stream is the default. 
Description: 
The READ command specifies the source of a TIGR command stream. 
00002
00001
Format: 
TAPE ; 
MPC,MPCNAME=mpcname[,MODEL=mpcmodel][,STATUS=sta]; 
 LA IOM#=iom,CHAN=x[-y][,STATUS=sta][[,IOM#=iom,CHAN=x[-y][,STATUS=sta]]; 
 [LA IOM#=iom,CHAN=x[-y][,STATUS=sta][[,IOM#=iom,CHAN=x[-y]][,STATUS=sta]]; 
 [MPC,MPCNAME=mpcname[[,MODEL=mpcmodel][,STATUS=sta]; 
 LA IOM#=iom,CHAN=x[-y][,STATUS=sta][[,IOM#=iom,CHAN=x[-y][,STATUS=sta]]; 
 [LA IOM#=iom,CHAN=x[-y][,STATUS=sta][[,IOM#=iom,CHAN=x[-y][,STATUS=sta]]]; 
 DEV; 
 NAME=name,MODEL=(model#[,feature#]),DEV#=devno[,options]; 
 [NAME=name,MODEL=(model#[,feature#]),DEV#=devno[,options]...] 
Note:  The semicolon (;) is used here to denote continuation of a line of 
text. 
Parameters: 
To see all of the parameters, enter ??.  For information about a specific 
parameter, enter: 
HELP (TIGR) TAPE parameter 
where parameter is: 
MPCNAME, MPCMODEL, STA, IOM, X, NAME, MODEL, FEATURE. 
mpcname    specifies the unique name by which the software refers to this MPC. 
The format of the name is TCxx for a tape controller, where xx is a two-digit 
decimal number (00-99). 
mpcmodel    specifies the MPC model number which will be used to select 
firmware to be loaded into the MPC.  The MPC model numbers are listed below. 
The default is MTP0610 for TAPE. 
                                                                Firmware 
    MPC Model No.                                 Sub-system    Modules 
    -------------                                 ----------    -------- 
    MTP0601/MTP8021/MTP8022/MTP8023                  TAPE         M601 
    MTP0610/MTP0611                                  TAPE         M610 
    MFP8000T/MFP8001T/MTPTPUR/MTP8000/MTP8001        TAPE         TPUR 
    MTP8215/MTP8216/MTP8218                          TAPE         M460 
    MTP8225/MTP8226/MTP8228                          TAPE         IFTP 
sta    is the initialized partition-status of the MPC or specified channels. 
The permissible values are UP or DOWN.  For channel partitioning, channels 
specified immediately preceding the STATUS option are marked down.  UP is the 
default. 
iom    is the system-assigned number of the IOM.  Note:  The first Link 
Adaptor specified (LA IOM#=iom) must specify the firmware bootload channel for 
this MPC. 
x[-y]    is the channel or range of channels connected to the LA.  The channel 
number range is from 8 to 63, unless the system is a DPS 8000 in which case 
the channel number value is in the range 8 to 127.  There are hardware 
restrictions on which channels may be connected to the same MPC from different 
IOMs.  The table below summarizes these restrictions: 
    If the number of channels       then the first channel 
    specified in the IOM#iom,       address must be an integral 
    CHAN=x-y field is:              multiple of: 
           3-8                             4 
            2                              2 
            1                              1 (no restriction) 
Also see Usage Note #2. 
name    is the unique name used by the software when referring to the device. 
The format of the name is MTxx for a 9-track tape drive, where xx is a 
two-digit decimal number (00-99). 
model#    is the applicable model number.  The following is a list of 
supported tape models: 
    Tape Model#      Feature#    Description 
    -----------      --------    ----------- 
      MTU0610        MTF0605     9 track 125 ips 800/1600 bpi 
                     MTF0607     9 track 200 ips 800/1600 bpi 
                     MTF0608     9 track 200 ips 1600/6250 bpi 
      MTU0630        MTF0634     9 track 75 ips 800/1600 bpi 
                     MTF0635     9 track 75 ips 1600/6250 bpi 
                     MTF0636     9 track 125 ips 800/1600 bpi 
                     MTF0637     9 track 125 ips 1600/6250 bpi 
      MTU8200        MTF8205     9 track 125 ips 800/1600 bpi 
                     MTF8206     9 track 125 ips 1600/6250 bpi 
                     MTF8208     9 track 200 ips 1600/6250 bpi 
feature#    is the applicable feature board number. 
Description: 
The TAPE command describes TAPE subsystem configurations.  The command 
describes the configuration of the IOMs, the LAs (Link Adaptors), the MPC 
(Microprogrammed Controller), and the tape drives. 
Usage Note: 
1.  Up to 8 channels can be defined per LA.  Two LAs can be defined for an 
    MPC.  Therefore, a possible maximum of 16 channels can be defined per MPC. 
2.  If all channels to a controller have STATUS=DOWN, TIGR sets the controller 
    to STATUS=DOWN.  (If all channels to a controller are down, all paths to 
    the controller are down, and therefore, the controller must be down.  This 
    follows standard CP-6 partitioning rules).  This is accepted by TIGR if 
    there is another path to the devices that is not down or if all of the 
    devices on the controller are down.  Otherwise, TIGR aborts with error 
    messages mentioning the controller and channel number it could not 
    partition because of ALTRETs from M$SYSCON. 
Related Commands: 
See DISK command. 
00010
00009
00005
00008
00003
00002
00007
00001
00012
00004
00011
00006
TIGR is command driven; that is, it obtains the information necessary to 
construct the tables from a command stream.  The TIGR command stream is 
included in the patch stream.  Reading of this stream is controlled by 
boot-process defaults, modifiable via AARDVARK.  The TIGR command stream may 
be read from the following sources:  the operator's console, the card reader, 
the unlabeled portion of the PO boot tape, or a second patch tape. 
Format: 
UNIT,; 
MPCNAME=UCxx[, MODEL=mpcmodel; 
[STATUS=sta][MODEL=(model#[, feature#])]; 
NAME=name, IOM#=iom, CHAN=x; 
[, IOM#=iom, CHAN=x][, options]; 
[NAME=name, MODEL=(model#[, feature#]), IOM#=iom, CHAN=x; 
[, IOM#=iom, CHAN=x][, options]] ... 
Parameters: 
To see all of the parameters, enter ??.  For information about a specific 
parameter, enter: 
HELP (TIGR) UNIT parameter 
where parameter is: 
UC, MPCMODEL, STA, MODEL, FEATURE, NAME, IOM, X, OPTIONS. 
UCxx    is the name of the MPC to which the unit record device is connected, 
where xx is a two-digit decimal number (00-99). 
mpcmodel    is the MPC model number which will be used to select firmware to 
be loaded into the mpc.  Valid MPC model numbers are listed below. 
    MPC Model No.                Sub-system    Firmware Modules 
    -------------                ----------    ---------------- 
    URPEURP                         UNIT       none 
    URP0600                         UNIT       UCMN, U400, UCRP 
    URP0601                         UNIT       UCMN, U400, UCRP 
    URP0602                         UNIT       UCMN, U400, UCRP 
    URP8000                         UNIT       UCMN, U400, UCRP 
    MFP8000U/MFP8001U/URPURTP       UNIT       URTP, U400, UCRP 
    URP8011                         UNIT       none 
    URP8012                         UNIT       none 
    URP8013                         UNIT       none 
    URP8600                         UNIT       ICRD (Loaded by the MCA) 
    URP8601                         UNIT       IPR54 (Loaded by the MCA) 
    Note:  MCA means Maintenance Channel Adapter. 
sta    is the initialized partition status of the MPC.  Permissible values are 
UP or DOWN.  UP is the default. 
Note: If a user's system does not have UR hardware, the corresponding TIGR 
definition must define the UR controller, LP device, etc. with STATUS=DOWN for 
each definition. 
model#    is the applicable model number.  The following is a list of 
supported models: 
    Unit Model#                   Feature#             Description 
    -----------                   --------             ----------- 
    (printers) 
      PRU0901/PRU0903/*PRU0908    PRB3500              64 char ASCII train 
                                  PRB3513              64 char ASCII train 
                                  PRB3524              64 char OCR-A/B 
                                  PRB3600              96 char ASCII train 
      PRU1201/PRU1203/*PRU1208    same as PRU0901 
      PRU1600                     PRB0500              64 char ASCII train 
                                  PRB0513              64 char ASCII train 
                                  PRB0524              64 char OCR-A/B 
                                  PRB0600              96 char ASCII train 
      PRU1200                     same as PRU1600 
    (readers) 
      CRU1050                                          1050 card per minute 
                                                         reader 
      CRU0501                                          500 card per minute 
                                                         reader 
    (punch) 
      PCU0121                                          100 card per minute 
                                                         punch 
    *For DPS 90 only. 
feature#    is the applicable feature board number. 
name    is the unique name used by the software when referring to the device: 
LPxx for line printer, CRxx for card reader, CPxx for card punch (xx is a 
two-digit decimal number, 00-99). 
iom    is the system assigned number of the IOM connected. 
Note:  The channel specified for the first device (IOM#=iom ... ) must specify 
the firmware bootload channel for this MPC. 
x    is the channel over which the device is connected, from 8 to 63, unless 
the system is a DPS 8000 in which case the channel number is in the range 
8-127. 
options    are as follows: 
    STATUS=sta    where status is UP or DOWN. 
    IN    indicates that the device is an input device. 
    OUT    indicates that the device is an output device. 
    SYMBIONT    indicates that the device is a symbiont device. 
    WSN=wsnname    specifies the workstation of this device.  Up to four 
    workstations may be defined, including LOCAL, the default.  One to eight 
    characters may be entered for wsnname. 
    FORM=formname    specifies the form to be mounted on the device at boot 
    time.  The formname designation is one to six characters.  This option 
    applies only to output devices, LP or CP.  The defaults are STDLP for 
    printers and STD** for punches. 
Description: 
The UNIT command describes a unit-record subsystem, that is, the 
identification of the channel and IOM over which each unit record device is 
connected to the system. 
Usage Note: 
If a site has only remote printers which are all upper-case only, that site 
must define an IOM-connected line printer via the UNIT command with the 
following characteristics: 
         Model#                   Feature#              STATUS 
         ------                   --------              ------ 
    PRU1200 or PRU1600        PRB0500 or PRB0513         DOWN 
00011
00006
00008
00005
00003
00007
00010
00001
00004
00002
00012
00009
Format: 
VOLINIT 
Description: 
The VOLINIT command causes TIGR to invoke the VOLINIT processor after 
completion of all system initialization functions.  This command is used to 
call VOLINIT to initialize disk packs at system boot time. 
00001
